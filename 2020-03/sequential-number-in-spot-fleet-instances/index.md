---
title: "SpotFleet内の複数インスタンスで連番を生成するスクリプト"
date: 2020-03-01
---

AWS でスポットインスタンスを複数起動して大量の処理を行うことがたまにあります。
Terraform で SpotFleet をリクエストして複数のインスタンスを立ち上げることはできますが、個別に user_data を指定するのは
少し面倒です。

ただ、同じ user_data でも、重複しない連番さえ取ることができればなんとかなることも多いはず……と思っていて、
パラメータストアを使ったり DynamoDB の AtomicCounter を使ったりしているようですが、
AWS CLI + jq だけで生成する方法を考えてみました。

## スクリプト

```shell script
#!/bin/bash

TOKEN=$(curl -s -XPUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
INSTANCE_ID=$(curl -sH "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/instance-id)
FLEET_ID=$(aws ec2 describe-instances --instance-ids $INSTANCE_ID | jq -r '.Reservations[].Instances[].Tags[] | select(.Key == "aws:ec2spot:fleet-request-id").Value')
TARGET_CAPACITY=$(aws ec2 describe-spot-fleet-requests --spot-fleet-request-ids $FLEET_ID | jq '.SpotFleetRequestConfigs[].SpotFleetRequestConfig.TargetCapacity')

while true; do
  aws ec2 describe-instances --filter Name=tag:aws:ec2spot:fleet-request-id,Values=$FLEET_ID | jq -r '.Reservations[].Instances[].InstanceId' | sort > /tmp/instance_ids.txt
  if [ $(cat /tmp/instance_ids.txt | wc -l) -eq $TARGET_CAPACITY ]; then
    break
  fi
  sleep 10
done

cat /tmp/instance_ids.txt|awk "/$INSTANCE_ID/{print FNR - 1}"
rm /tmp/instance_ids.txt
```

SpotFleet で起動したインスタンスには、 FleetRequestId のタグが付けられています(というか taggingRole がありますよね)。
Tag がついているということはインスタンスをフィルタリングできるので、 FleetRequest 内のインスタンスIDを列挙してソートし、
自分のインスタンスIDの位置を awk で導出しています。(今回は 0-origin にしました。)

これの弱点？として、インスタンスが全て立ち上がっているときを想定しているため、起動していないインスタンスは待ちますが、
既に終了したインスタンスがあって CLI で取得できなくなった場合は永遠に待ち続けてしまいます。
時間が経ってから呼ぶ可能性があるなら `/tmp/instance_ids` を消さないようにするか、
起動時に自動実行しておいて番号自体をキャッシュすればある程度回避できそうです。

Ansible とか使えばいいのでは？という気持ちも少しずつ出てきています。
というか、こういった分離しやすいワークロードを分散して実行するようなツール、ありそうなんですよね……。
Docker 化してオーケストレーションが早そうではあります。 
