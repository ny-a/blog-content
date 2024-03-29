---
title: "TsukuCTF2021 Writeup(OSINT)"
date: 2021-09-16
---

[TsukuCTF](https://tsukuctf.sechack365.com/)

ny_a です。ごめんなさい。

## OSINT

OSINT メインの CTF なのに OSINT 以外の Writeup を書いてしまって反省しています。
ちゃんと書くので許して。

今回は Google Lens 問が多かったようですね。
Google Lens については知っておりました。
知っていましたが、これだけ問題数があって、100点くらいの問題から500点くらいの問題まであります。
ということは、高得点の問題は多分 Google Lens でも一筋縄ではいかない問題なのでしょう。
きっと運営スタッフが何度も Lens で位置をズラしながら検索しても全く出なかったから高得点になっているに違いありません。
つまり、Lens の運命に託す時間があれば、なんとか言葉で表現して検索してみて、
1つでも多くの検索結果に目を通すのが最適解ということです。やる気が湧いてきました。

よし、頑張るぞ〜〜〜〜〜〜〜！！！！！！！！！！！！！！！！

というわけで、ひたすらキーワードを基にした画像検索と Google Maps の目 grep でのパワープレイの記録をお楽しみください。

### ramen

そのまま画像検索に投げてみるも、うまく見つからず。
というかキーワードが "soup" になってしまう。いや、気持ちは分かる。

インスタグラムのアカウントということなので、インスタ映えするラーメンを頑張って検索します。
「ラーメン インスタ」とかで検索したと思います。「ヤングコーン」とかもつけてみたけど出てこなかった記憶。

麺と同じような淡い黄色の、クリーミーそうなスープ。
これだけ麺と色が近かったら、麺もスープとの境界があまり認識できていないかもしれません。
それに加えてこの不透明度、こうなってしまうともう麺は溺れてし

……。

スープの色やヤングコーン、お皿などの特徴を目に焼きつけて、目 grep します。

すると、確かこの [Instagrammer news](https://instagrammernews.com/detail/2245512484830076188)
が出てきました。ここに店の名前が書いてあるので、本店のアカウントを調べればいいです。

### shop

なるほど、イオンモールですね。

近くを通った2台の車のナンバーが、多分名古屋と滋賀。じゃあ滋賀のあたりですかね、知らんけど。

トヨタの入っているイオンで探して、草津が出てきました。

### train

山手線と京浜東北線が併走している区間ですね。
あと山手線の方面表示が、電光掲示板の表示の方は隠れていなくて、
片方は東京・上野方面、もう片方は品川・渋谷方面と書かれていることが分かります。

ということは、東京〜品川の、両端を含まない区間ということが分かります。

あとは京浜東北線の快速が通過する駅は有楽町と新橋だけに絞ることができるので、
構内図を見ながら北改札などの特徴に合致するか調べます。

15:35 から京浜東北線が停車するということで、時刻表から絞るかなーと思ったのですが、
普通に2択になったので時刻表は見ませんでした。

あと、普通に新橋ってこんな感じだったし工事してましたよね。うん。

### YUUGEN

全国のキッズが大好きなやつ(偏見)ですね。

調べてみるとJR九州ということと、走っていた区間が分かります。

まあなんか、在来線の上を高架が分岐していく感じだということが分かります。

あとは Google Maps で航空写真をローリング作戦(しらみ潰し)で条件に合いそうな所を探します。

近くに黄色いビルなんかがあれば完璧ですね。

### Beach

「レンタルスペース」「BBQ」という文字が見えますが、それ以外はあまり読み取れず……。

東京近郊とのことなので、「東京 海水浴」みたいに検索をして、海岸線などが似ている画像を探すと、江ノ島なんかがヒットします。
1枚目の奥に見える白いものは、江ノ島の灯台でしょうか。

Google Maps で手前の海岸線の情報をヒントにたどっていくと、サザンビーチちがさき海水浴場のあたりに、
Cの形のモニュメントがあることが分かります。

一番近い駅は茅ヶ崎ですね。

### tram

海外のようです。日本の面積は地球上の陸地の1%に満たないので、だいたい探さなければいけない範囲が数百倍オーダーになることが分かります。
あと土地勘がないのが痛いですね。日本から出たことないので。

更に、夜の写真なので背景から情報を得にくいですね。
暗いところは見えにくく、明るいところも白く飛んでしまって見にくくなっていてつらいです。

読みやすいのは広告くらいです。スマートフォンの広告から地理的特徴を取るのは難しそうです。
見えにくい文字も見てみると、アルファベットにダイアクリティカルマークがついていることが分かります。
はい、アメリカではなさそうですね。

文字以外に読み取れる情報としては、厚着をしているので高緯度地域ではないのかなという印象と、
なんか管制塔みたいなイメージの特徴的な建物があることくらいでしょうか。
あと路面電車が交差していますね。これから探すのは少し厳しいので文字から調べましょう。

ダイアクリティカルマークを打つのは面倒なので、Googleがエスパーしてくれることを期待して"CSOB"で検索します。
きちんと読めそうな文字がそれくらいしかないので。

調べてみると銀行であることが分かります。めっちゃおしゃれですね。
kinko's みたいでよくないですか？いいなあ。私は好きです。kinko's 使ったことないけど。

あとはまあプラハのあたりの tram で調べると、プラハ市電が出てきます。Wikipediaのページを見てみると、いろいろ系統があるようです。
写真をもう一度見てみると、前に5と表示があります。5系統かなと考えて、
始点と終点の Sídliště Barrandov、Ústřední dílny Dopravního podniku あたりを調べてみます。
始点の方から路線が交差する所の近くの銀行を Google Maps の衛星写真から探していくと、
Anděl 駅の近くにそれらしい組み合わせがあります。ストリートビューで確認するとまさにそこでした。

### Tsukushi_no_email1

Gmail で宛先メールアドレスを打ったあとダブルクリックすると、ユーザー情報が開きます。
アイコンにフラグがあるので、適当に画像を新しいタブで開いて確認します。

### Tsukushi_no_email2

Google Calendar ですかね？メールアドレスから公開カレンダーを追加することができるので、自分のアカウントに追加してしまいます。
すると予定が1つ見えました。普通にフラグが書いてあります。

### cafe

当該アカウントのメディア欄をさかのぼると、「萌え萌えキューーン」という写真付きツイートが見つかります。
画像は2枚あり、片方はインターネットで何度も見たことがあるものでした。

もう片方はオリジナルでしょうか。どうやら同じポーズをしているようです。
パロディという感じでしょうか。

窓の外向きに "PASTA" "OME……" という文字が見えますが、これはメニューを表わしているのでしょう。
ここから探すのは難しそうです。

キャストさんは胸元で手をクロスさせており、ここに名札があっても見えないでしょう。
(目線入っているし頭部は全く見ていませんでした。)
コスチュームをよく見ると "No.1 メイドカフェグループ" という文字が見えます。

ググったらめいどりーみんというグループのようです。
店舗一覧を見ると、それぞれの店舗で内装が結構違うようです。
空色のクロスが使われているのは秋葉原 中央通り店だけです。

ちなみに、Writeup を書きながらそのツイートを見ていたのですが、
ご本人にいいねされていたようで、ここを見ればすぐだったかなと思いました。

### train2

駅にある文字としては乗車口の看板くらいでしょうか。

線路の向こう側には、踏切動作反応灯の下に「出町柳」の文字が見えます。

はい、出町柳と言えば京阪ですね。京阪と言えば出町柳です。
京阪乗る人おけいはん。意味が分からないと言われても動じることはありません。もう答えも目前です。
とはいえ、出町柳まで行ったことはあるものの、この乗車口の看板は見たことがありません。
「京阪 乗車口」なんかで検索してみますが、見覚えのあるものしか出てきません……。

なんか変だなーと思いながら Google Maps でしらみ潰しに京阪本線の路線を航空写真で見ていきます。
ホームが片方のみにある地上駅……、そんな駅に思い当たりません。。。

京阪にはいくつか別の路線があるのでそれも調べてみたのですが、
よく考えてみればそもそも本線以外は出町柳に行かないのでは……？

写真をもう一度見てみます。出町柳9号、これは踏切を表しているのでしょう。
ですが、京阪本線の出町柳周辺は地下を通っています。おかしい……。

出町柳9号で検索してみます。叡山電車が出てきます。はい。乗ったことないんですよねー。

踏切の名前にはだいたい隣の駅の名前がついていたはずです。出町柳から線路を見ていくと、
隣の元田中駅の写真であることが分かります。

すぐ京阪って分かって(？)よかったですね！！！！！！！！

### fishing

あーはい、この橋ね、分かります。あーあの、あれです。あの、あー

超有名ブリッジですね。

とりあえず日本ということが分かりました。そんな辺鄙なところにはなかったはず。
いやなんというか、東京周辺じゃなかったですかね？

「東京 橋」とかで適当に画像検索してザーーーーーーーっと見ていきます。
あった。東京ゲートブリッジです。

そのままフラグとして投げてみます。incorrect……。釣り場ということでしたね、はい。

Google Mapsで見て、撮影地らしきあたりを見てみます。
若洲海浜公園というらしいです。それは知らなかったです。

超有名ブリッジの横にある、普遍釣り場。有名なものの近くにある、無名なもの。
えっもしかしてこの組み合わせって奇跡じゃないですかね？

……。

考えるまでもなくどこにでもあります。次行きましょう。

### dam

えーっと、はい。自然ですね。すごい自然です。
特徴的なものといえば、奥の方に小さく見える赤い橋でしょうか。

適当に画像をクロッピングして Google の画像検索に投げてみますが、うまく見つかりません。

このなんというか、アーチ状の、橋、ですね。赤い。

「アーチ 橋」とかで画像検索してみます。
すると、[近いけど違う橋](https://images.app.goo.gl/DHFUCHUfBWHKuC96A) が出てきます。

うーん、近いんだけどちょっと違うんだよな……と思いながらクリックしてみると、
関連画像に [めちゃくちゃそれっぽい画像](https://images.app.goo.gl/rnBvUAenJP2S1JTV9) があるではないですか！！

Google Maps で見るとどうやらここで合っていることが分かります。

ちなみにこの橋、トラス構造 (レンティキュラートラス構造) らしいですね。橋梁、難しい……。

### park

はい、完全に住宅街ですね。撮影した場所は少し高くなっていて、そのまま背後には山がある感じでしょうか。

拡大してみると、中央に何やら明るいものが2つくらいありますね。大きな反射板か何かがあって太陽の光でも反射しているのでしょうか。
(一応部活の大会とかでこういう投光設備のある会場には行ったことがあるのですが、昼で使われていなかったため全く思い当たらず……。)

新幹線が走っていることも分かります。東海道……にしては短い気がしますね。とはいえ新幹線沿線も(しらみ潰しに探すには)すこし範囲が広すぎます。
あとは新幹線の奥にネオン看板っぽい？ものが見えますが、文字は読めません。
また、新幹線の線路と高速道路のようなものが交差していそうだということも分かります。

写真の奥の方は、割と高い山が連続していることが分かります。恐らく海の方向を向いて撮られた写真ではなく、内陸の方を向いているのでしょう。
写真中央には高めのビルが2つ、左側の近い山の上には紅白の塔、その手前にはイオンらしき看板、
右側の山にはネットの張られた施設、右端には山の中にポツンと白い建物が見えることが分かります。

高速道路の沿線を見てみると、何やら見慣れないスーパーのような看板が見えます。
「スーパー ロゴ」で Google 画像検索してみると、サンリブというスーパーであることが分かります。
どうやら九州の方に展開しているようです。

ここで気付いてしまいます。さっきの問題でもJR九州が出てきたし、さては作文者が九州に住んでいるな……？と。
九州に住んでいるので、九州の問題が多く出題される。ということはこれも九州です。完全に読めました。

九州の新幹線、九州新幹線の近くにあるサンリブを Google Maps でしらみ潰しに見てみます。
どこにもそれらしいサンリブはありません。というより、それらしき山すらありません。

サンリブの店舗一覧を見てみます。中国地方にも展開しているようでした。
九州ではない可能性も出てきました。

とにかくサンリブの店舗を Google Maps で見ていくと、サンリブ 府中店が新幹線に程近くいい感じではないかと思いました。
左側の近い山は比治山でしょうか。紅白の塔もあります。近くに広島段原 ショッピングセンターがあり、イオンの看板があります。

中央の高いビルは、シティタワー広島とグランクロスタワー広島でしょうか。
ネットに囲まれた施設は広電ゴルフのようです。
山の中に見える白い建物はペルル中山南参番館ですかねー。

写真に写っている左の端を特定しましょう。本当の左端は木に隠れてしまって分かりづらいので、
新幹線の手前にある、屋根の上に屋上というか階段のある建物を探します。アーバンビュー府中八幡のようです。

右端は白い建物でよさそうです。その手前には、もしゃっとした森があります。
府中出張城跡だと仮定しましょう。
その近くには、何やら整然と部屋が並んだ施設と、かまぼこ型の施設があります。
近くを探してみると府中町立府中中学校とその体育館のようです。

府中町立府中中学校、府中町立府中中、府中町中立府中府中中…………

……ゲシュタルト崩壊してきましたが、続きを進めましょう。

これまでに分かっている位置同士を、写真で真っ直ぐ並んでいる所を結ぶように地図上に直線で結んでいきます。
そうすると、画角もだいたい分かっているため、写真の撮られた位置がかなり絞られます。

あとは、学校の手前の住宅地の屋根から詳しい位置を特定していきます。
太陽光パネルのある家が分かりやすいでしょうか。

それが見つかれば、あとは一番手前にある、三角の突起のある白い屋根の建物を探します。
山の中だから〜と山の方を探していると永遠に見つかりません。
直線を信じて探していくと、瀬戸ハイム第一児童遊園地 公衆トイレであることが分かります。

ちょうど後ろに道路が通っているので、ストリートビューで合っているか確認して、
問題なさそうなので、この問題との戦いに終止符を打ちます。対戦ありがとうございました。

### OBOG

「SecHack365 非公式」で探すと、公式の [ツイート](https://twitter.com/SecHack365/status/1370017773817004037)、
作文者の [ツイート](https://twitter.com/ryusei_ishika/status/1369996158530060289) が出てきますがドメイン名が変わっているようです。
[リプライ](https://twitter.com/ryusei_ishika/status/1370260927879081986) のページは生きていそうなので、ここから辿りました。

リポジトリへのリンクがあるので確認します。
CI/CD は使っているでしょうが、コミットログにその変更が残っていれば簡単に分かってしまうでしょう。
一応コミットを見てみましたが、怪しいコミットはなさそうです。

となると、CI/CD を無視して、サーバー上のデータだけ書き換えた感じでしょうか。
ソースを clone してきてビルドして、実際のサーバー上のファイルと比較してもいいですが、面倒です。

適当に開発者ツールを開きながらページを探索していると、コンソールに何か怪しいログが出ています。
見てみると、「締切駆動コース」というページが怪しいです。

そのあたりのソースを見てみると、[src/pages/timer/script/display.js](https://github.com/SecHack365-Fans/SecHack365-Fans.github.io/blob/master/src/pages/timer/script/display.js)
で `console.log` を呼んでいるようです。blame してみると、
[fix: 微細な修正](https://github.com/SecHack365-Fans/SecHack365-Fans.github.io/commit/2243cd0f7dcab26698854b6b9a645365aa18d293)
というコミットで base64 デコードしないように修正されているようでした。

まあ、適当に `base64 -d` に食わせてデコードしてみると、フラグが得られるという感じですね。

### InterPlanetary Protocol

なんか先頭7文字が同じなので(`http://` ？)換字暗号かなと思ったのですが、よく分かりません。
先頭7文字で検索してみると、ipfs というものがヒットします。
"https://ipfs.io/ipfs/bafybei……" という URL の一部？がたくさんヒットするので、
ここに3つの特殊な URL を入れてみると、フラグの断片が得られます。

アンダーバーが2つ連続しているので、多分ミスだろうな〜と思いながら、
twitter かどこかで修正済みだと見た気がしたのでそのまま投げました。

### WildTsukushi

解けませんでした。

「きりん」「恐竜」「遊具」「滑り台」「つくし」「港」「海岸」など手当たり次第に思いつくキーワードで検索してみましたが、
見つからず……。

他の人の writeup で、いみのさんの最近のメディアツイートに近くの写真があった、と見たのですが、
いやこのツイートはTLで見てました……見たけど全く思い出せず……分からないよ……

### uiui

zip のパスワードは、一般的に `infected` とかが使われるようです。
少しググったら出てきますし、セキュリティキャンプでも講義で実際にこのパスワードが使用されました。

適当に unar ([unarchiver](https://archlinux.org/packages/community/x86_64/unarchiver/)) で解凍して、
(こいつは複数ファイルを解凍すると自動でアーカイブのファイル名なディレクトリを作ってくれてちょっと便利です、)
(今回はファイルが1つだけだったのでディレクトリは作成されませんでした、)
(zsh では cd を省略してディレクトリを実行すると cd してくれます、)
(アーカイブのファイル名と中身のファイル名が同じでした、)
という感じで解凍したディレクトリに cd して……しようとして、
`./Virus` を実行して普通にバイナリをホストで実行してしまいました。

インシデントです……。ごめんなさい……。
皆さん！！！！インシデントはこのような偶然？の組み合わせで起こります！！！！！！気をつけましょう！！！！！

ps で変なプロセスが残っていないことを確認して、まあ CTF だしマルウェアではないだろうと運営を信じることにします。

あとは頑張って Gdidra でリバーシングを頑張ります。というか自分のことも運営も信じられないので徹底的に動作を確認します。
でもまあいくら頑張ってもテキストを表示して終了するだけのようにしか見えません。自己書き換えコードでもなさそうです。
さあ、困った。インシデントも発生させたしお手上げです。

……という感じで諦めてしばらく放置していたんですが、「IoC と IaC って似てるよな……フヒヒw」とか
「IoC って初めて聞いたとき普通にオリンピック時期だし IOC かと思ったよ」とかクソくだらないことを考えていたら、
sha256sum から調べることを思いつきました。

でまあ一応 Google で検索してみるんですが、出るわけがありません。
宅配便の伝票番号みたいに「8fa168f38e54fb0f63e6674a4f463ef3a0971f71546e6f4ed1b69c121d1de1f3 を VirusTotal で見る」
なんてリンクが出てきたら一般の人は混乱してしまいますよね。

なのでまあ VirusTotal を開いて、sha256 をペーストして……と思ったのですが、デフォルトでファイルを選択する画面が出ていました。
何も考えずにアップロードして……

…………

インシデントです……。ごめんなさい……。
皆さん！！！！！！！！！！！！！……

フラグが私の胸に深く刺さりました。申し訳ございませんでした。

想定解法(一歩手前？)で正答しましたが、完全に不正解です。なんなら今から点数下げてもらっても構わないレベルです……。
CTF でよかった……………………

ちゃんとサンドボックスで解凍しましょう！！！！ホストで解凍厳禁！！！！！ホストに生バイナリ出さない！！！！
肝に命じておきます。

### udon

解けませんでした。

ひたすらカレーうどんを検索しました。

おしまい。
