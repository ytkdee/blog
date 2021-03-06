---
title: 【Report】Osaka RubyKaigi 01  
date: "2018-09-09"
---

![Jaguar](./jaguar.jpg)  

---

## Osaka RubyKaigi 01  
<http://regional.rubykaigi.org/osaka01/>

---

* 日時   ： 2018年7月21日（土）
* 主催者 ： Ruby関西
* 会場   ： 大阪科学技術センター 4F 401号室

---

### Key Note : Rubyはなんでできてるの？
@matz さん

Rubyは何で出来ているのかの話でした。

今回の出張で、PCを忘れて名古屋で中古のPCを買って  
EmacsセットアップできなくてVimでスライドを書いたそうです。

### Ruby25周年

wikipediaによると初版リリースは1995年の12月である。  
しかし、まつもと氏のローカルには既にRubyは存在していたので、Rubyという名前をつけた日が誕生日としている。  
1993年2月24日。  

### Rubyをつくったきっかけ

1993年頃にバブル崩壊したことが一番のキッカケ。  
Rubyは不況の産物であった。  
社内システムの開発をしていたが、そのチームは景気が悪くなって解散した。

大半のメンバーはお金を稼ぐ部署に異動となった。  
しかし、社内システムのメンテナンスのために2人だけ残された。そのうちの1人がmatz。  
新規の開発は禁止されいたため、基本暇だった。  
何かやろうかと思って作ったのがRuby。  

### 高校時代の夢

BASIC使っていた当時、これよりましな言語が欲しいと感じていた。  
大学にて言語を勉強しているうちに言語は面白い。  
⇒言語作りたいと思うようになった。  

当時はまだネットがなかったので情報が本か雑誌しかない。  
やさしいコンパイラのつくりかた という書籍を買ってみたが、  
コンパイラをやさしく作る本ではなく、シンプルなやさしいロジックのコンパイラを作る本だった。  

### 思考の表現方法
プログラミングとはコンピュータに分かるように思考を表現すること。  
思考の表現方法を自分で作りたくなった。  

プログラミング言語を作るにあたって、オブジェクト指向が好きであったのでオブジェクト指向の言語を作ろうと思った。  

当時はUnix Cプログラマだったが、コンパイル型言語を作ってもCと競争するのは難しいと考えており、  
スクリプト言語なら移植性もあるし色んなのがある為、スクリプト言語を選択した。  

そして、過去の言語のいいとこどりをしようと考えた。  

著作権はアイディアを保護しない、言語デザインに著作権は及ばない。という判例もあるそう。  

### 発想の源

#### Emacs

<https://www.gnu.org/software/emacs/>

大学時代Sun3ワークステーションを学部生100人で共有して使っていた。  
Emacsのインストールは禁止されていた（100人ぐらいがEmacsを使うと耐えられない）のでソースの中を見てみた。  
(vi を使うのは嫌だった。)

そこで学んだのが以下の2点

* Tagged Pointer
* Garbage Collector


文法についてはauto-indentが使いたかったので、ruby が動く前に auto-indentのemacs拡張を書いた。  
* ruby-mode.el

endがついた文法でもauto-indentできることが分かったから、end を使うようになった。

#### Lisp

<https://ja.wikipedia.org/wiki/LISP>

シンボルを継承した。  
よく、シンボルは要らないと言われるが、Lisperだったのでシンボルは当たり前の存在であった。  
pythonやluaもシンボルはないのだが、そのことに気付くのに20年かかった。

また、以下の名前もLispから影響を受けている。

* Bignum
* Fixnum

Bignumを最初に入れた時には凄く悩んだ。  
(fcntl)をよぶメソッドで以下の問題に直面。  
* Tagged Pointer だと 整数の数が31ビット目を使ってしまっていた。  

また、メタプログラミングについてもLispからの影響を受けている。

オブジェクト指向機能はSmall Talkからの影響というよりも

CLOS（Common Lisp Object System）の影響が強い。  
CLOS - <https://ja.wikipedia.org/wiki/Common_Lisp_Object_System>

bit別冊 CommonLispオブジェクトシステムは1988年当時、最も影響を受けた書籍。

また、nilについてもLispから継承した。

#### Eiffel

<https://ja.wikipedia.org/wiki/Eiffel>

Ada like なプログラミング言語とのこと。  
昔は金融系などで使われていた。  
Ada - <https://ja.wikipedia.org/wiki/Ada>

Object-criented software constructionオブジェクト指向入門

櫛形構文を継承した。

以下の名前も影響を受けている。

* rewuire
* ensure
* rescue
　(機能は違うが)

#### CLU

<https://ja.wikipedia.org/wiki/CLU>

リスコフ置換原則で有名なBarbara Liskovが作者。  
抽象型言語  

Rubyにおけるブロックの御先祖である。  
ブロックのついたメソッドをCLUに倣ってイテレータと呼んでいた。  
Lispの高階関数の様な構文。  

1関数しか取らない高階関数

* 98%の高階関数は一つしかとらない(OCaml調べ)
* 制約されたほうが分かりやすい。
* 読みやすい。
* 効率がいい(こともある)。

#### Sather

<https://ja.wikipedia.org/wiki/Sather>

UCBで開発されたEiffel Like なプログラミング言語。

以下の2つが影響を受けた。

* undef
* alias

undefについてはver.0.8には存在していたががLSPに反するからなのか、1.0ではSatherから無くなった。  
しかし、Rubyに取り込まれて生き残った。

#### Python

以下を継承した

* class
* undef

#### Smaltalk

以下を継承した

* select
* collect
* detect
* reject
* ブロック引数の ||

#### C言語

演算字の優先順位のみを継承。

#### Perl

当初のRubyの目標としてはPerlと同じような仕事が出来ることであった。
そして以下の機能に影響を受けた

* システムグローバル変数
* 文字列メソッド
* 配列メソッド
* 正規表現

これらをオブジェクト指向で再構成した。  
これが正解であった。

しかし、グローバル変数は失敗であった。  
Ruby on Railsによって、Webアプリケーションの作成に使われることは想定できていなかった。

### 真似なかった言語

#### Icon

<https://ja.wikipedia.org/wiki/Icon>

制御構造を真理値によるものから、成功か失敗によるものへと変更した言語。  
SwiftのOptionなどが近いそう。

#### APL

<https://ja.wikipedia.org/wiki/APL>

配列指向言語

#### Forth

<https://ja.wikipedia.org/wiki/Forth>

天文台のコントロールなどに使われているスタックベースの言語。

### デザインの困難さ

何をどれだけ取り込むかが大事。  
取り込むには周囲との整合性が重要である。

エクストリームよりも「ちょうどいい」が必要。  
エクストリームだとボリュームのつまみを一番上まで上げるようなもので、  
極端なものであるので簡単であるが、バランスが大切。  

その「ちょうどいい」が難しい。  
答えもないし人や時代、条件によって変容するものである。

また、互換性は重要である。  
互換性がないと古いバージョンを使い続ける人がでてくる。  
しかし、変化を止める事は出来ない。  
進歩を止める事は緩やかな死を意味する。  

一方でRuby on Railsではバージョンアップ地獄というくらい互換性は保たれていない。  
下にいる人が苦労して互換性を保っても上側で壊れているのが現状。  

しかし、WEBのドメインは進化が早いので進歩し続けなければならない。  
例え、互換性を壊してでも変化を続けなければ取り残されてしまう世界。  

### Ruby 3 について

* JIT

Rubyバージョン 2.6にはMJITが含まれる。  
しかし、JITしててまだ動くだけ。

MJITはかなり複雑な実装になっていたので枠組みだけ取り込んだところ、  
MJITの提案者がMIRというLight Weightな実装を更に提案してきた。

* マルチコア時代

GIL を外すとクラッシュするのが現状。  
真の並列処理を実現するために笹田氏がGuildを作成中。

* メモリ容量の変化

GC改善する事により対応

* 関数型プログラミング
* 列志向プログラミング
* パターンマッチングの導入

等、鋭意開発中。

バランスを重視してより良いRubyにしようと画策中。  
既存のコードを壊さない用に性能改善を図っている。  
既存のソフトウェアを壊さない選択肢を探しながらの細い一本道を進んでいく。

Rubyはいい言語であるとは思っているが、デザインは厳しくなってきており選択の余地もかなり狭まっている。  
しかし、その難しさを乗り切るのが言語デザイナーの醍醐味である。  
プログラマー≒デザイナーだと考えており、仕様をどうするかを決めないといけない。

決めるということは設計する事である。  
またそれには困難が付きまとうが、それが一番面白く、醍醐味であると考える。

### 質疑応答

1. 細い一本道の上を進むということの実例を挙げて詳しく説明してほしい。

　Rubyを作っていると新しい機能を作りたくなるが、
　互換性を考えると必ずしも作れるとは限らない。
　既存の処理を壊さないように考慮しながら新しい機能を作っていかなくてはならない。

2. もし、Rubyを開発してないとすると今、参考にしたい言語(or プログラム)は？

* Elixer  
<https://ja.wikipedia.org/wiki/Elixir_(%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E8%A8%80%E8%AA%9E)>
* Amazon Lambda  
<https://docs.aws.amazon.com/ja_jp/lambda/latest/dg/welcome.html>

3. Eiffelを参考にした際に事前条件/事後条件を入れなかったのはなぜか？

　入れなかった理由としては少し固すぎる。  
　こぼれ話としてはEiffelは継承の使い方が独特だとのこと。

4. パターンマッチングなぜ入れたいか？

　データが流れてきた時にデータの構造ことに処理を変えたい場合にif文の羅列は嫌。  
　上記の場合に手続き的になる印象があるのでそれを防ぐべく入れたいと考えている。

---

## Tech Talk : Complexity and you
@yuki24 さん

### 過去と現在のWeb開発の違い

過去のWeb開発は選択の余地が狭かった。

* HTTPサーバは基本Apache。
* ファイル構造が表示されるだけで感動していた。
* PerlやPHPでページごとに処理を書く。
* 単なるテキストファイルをデータベースの様に使用。
* アクセスがある度にディスクI/Oが走る。
* 適当なロック処理。
* 紙のページを彷彿とさせるデザイン。
* マウスポインタを追従するキラキラしたアニメーション。
* JavaScriptはまだ使えるようなものでは無かった。

以下のようなデザインのWebサイトが多かった。  
<http://bitfission.com/>

今日のWeb開発は様々な選択を必要とする。

* 数多に存在するフレームワーク。
* 当たり前のようにRDBMSを使用。
* Node.jsでSSR(Server Side Rendering)。
* バックエンドなしでもアプリ開発が可能に。
* Firebase(MBaas / BaaS)
* Google Mapの登場でJavaScript復活。
* Protorype.js
* jQuery
* フロントエンドライブラリ(React / Angular / Vue)
* SPA(Single Page Application)
* Virtual DOM / SSR(Server Side Rendering) / PWA(Progressive Web Apps)
* GraphQL

何を使うかが非常に悩ましい現状。

### 今日のWeb開発の印象

* 非常にスムーズに動くUI複数の要素が同時にロード。
* ページングなしで画面遷移。
* エッジケースも簡単になっている。

### プロジェクトが始まってから明らかになる事実

パッと見良さそうに見えても、プロジェクトが始まってから問題が明らかになる。

* JavaScript難しい。
* Angular等のフレームワーク、難しい
* SEOの問題
* Bundled JSのファイルサイズが大きすぎる。
* Progressive Web Apps難しい。
* JavaScriptが依存しているライブラリがメンテナンスされていない。
* ちゃんとテストされていない。

　そこで言われる一言 ```「それRailsで5分でできるよ」```

しかし、ソフトウエア開発は線形な仕事ではない。複雑。  
日々積み重なる複雑度により、同じ機能でも別アプリだと実装の速度が変わってしまう。

価値は二つの軸がある

1. 高価値-低価値
2. 実現容易-実現困難

いくつかの技術に当てはめると以下のようになる。

* Apache + PHP
　高価値 && 実現困難

* JavaScript before Google Map
　低価値 && 実現困難

* Rails
　高価値 && 実現困難 ⇒ 高価値 && 実現容易 (価値があって実現困難なものが実現容易なものに変化)

* JavaScript after Google Maps
　低価値 && 実現困難 ⇒ 高価値 && 実現容易

とあるRailsのWebサービスで高価値で実現困難なものに直面した時に言われる一言。  
```「それReactで簡単にできるよ」```

* Railsだけでやろうと思うと見当もつかない。
* JavaScriptならさっと思い浮かぶ。
* Reduxでデータを共通管理すれば解決する事も。
* イベントもReduxで。

しかし、Reactで実現した後、また高価値で実現困難な要求が発生。
* 認証系機能
* 管理画面
* バージネーション

そこで言われる一言 ```「それRailsで5分でできるよ」```  
「Railsで出来る→Reactで出来る→…」が循環している。

いいとこどりしようとした結果

* 大量に発生するyak-shaving
* 変な設計のRailsコード。
* 変な設計のReactコンポーネント。
* Rails/Reactエンジニアのどちらからも賛成してもらえない。

### 常にXを使え(使うな)という人々

以下を念頭に置くべきである。

* 銀の弾丸は存在しない。
* ライブラリ/フレームワークが本当に適切なのかを判断する事。
* アイデアやプロダクトが変わっていくという前提はあるのかを考慮する事。
* 継続的にメンテナンスすることが可能なのかを考慮する事。

### 道具はツールボックスのように整理されていて使わないといけない。

* 学習とはツールボックスの中身を増やしていくこと。
* 慣れたツールもあればそうでないツールもある。
* よく使うツールもあれば使わないツールもある。
* 高価値 && 実現容易でユーザーを獲得しないと何もできない。
* 高価値 && 実現困難にフォーカスできているのはプロジェクトとしてはヘルシーな状態である。
* 高価値 && 実現困難をシンプルにするにはどうしたら良いかを考える。

### 「それXでできるよ」の投げ合いは解決に至らない

以下の2点を意識すべきである。

* その道具の過去の成果に対するリスペクトを持つ事。
* 道具に対する知識を十分に習得する事。

### 質疑応答

* 高価値 && 実現困難 ⇒ 高価値 && 実現容易にするために意識している事は？

分からないことがあれば分かるためにはどうすればいいかをまず考える。  
ちっちゃなプロトタイプを作り、実際に触ってみると難しいことやるべきことが見えてくる。

---

## Tech Talk : GR-CITRUS いろいろ
@たろサ さん

### スライド資料

<https://speakerdeck.com/tarosay/gr-citrus-iroiro>


### GR-CITRUSの紹介

* 凄く小さい Ruby ボード(Ras-Pi Zeroより小さい)
* Ruby(mruby)でプログラム出来るマイコンボード
* 2014年ごろから地域RubyコミュニティのWakayama.rbで開発
* オープンソースハードウェア

### Ruby Cam-Robo360

*  センサで障害物自動検知が可能。
*  mp3を再生出来るスピーカー搭載。
*  Wi-Fiアクセスポイント機能。  
　→ スマホブラウザからも操作可能。 GR-CITRUSがAPになってサーバになる。  
* Arudinoライクな実装ができる。

動いている様子が youtube にアップロードされているので気になる方はご確認ください。

### 開発環境

VS-Code Studio + Rubic(拡張)  

Rubic  
<https://marketplace.visualstudio.com/items?itemName=kimushu.rubic>

以下のサイトが参考になる。

<http://tarosay.hatenablog.com/entry/2017/09/30/133805>

### 開発当初からの変更点
* プログラムサイズ制限をなくした（4KBから無制限）  
　→経緯としては大きなコードが動かないという声が多数あった。  
　※但し、大きすぎると暴走する事があるので自己責任(20KB程度までなら大丈夫との事)  
* プログラム実行の自動切り替え
　* 電源起動すると main.mrb が自動起動する。
　* USBでPCにつないだときはデバックモードで手動実行する。
* 強制ブレイク機能の追加
　* 無限ループであってもブレイクできる

### Sample

以下にてサンプルコードが提供されている。

<https://github.com/wakayamarb/wrbb-v2lib-firm/>

---

## Lightning Talk : Introducing Fn Project
@ayumin さん

### スライド資料

<https://www.slideshare.net/ayumin/introducing-fn-project>

オラクルはデータベースの会社からクラウドの会社に移行しようとしている。  
FaaSプラットフォームのfn projectの紹介。

### fn projectの特徴

* オープンソースのプロジェクトである
* 様々な言語に対応している(Java, Go, Ruby, Python, PHP, Node.js)
* ネイティブなDocker上で動く。
* Go言語で書かれている

### リファレンスの紹介

* Project Home  
<http://fnproject.io/>
* 8 Reasons why we built the Fn Project  
<https://medium.com/fnproject/8-reasons-why-we-built-the-fn-project-bcfe45c5ae63>

### 参考: Github/fnproject  

<https://github.com/fnproject>

---

## Lightning Talk : 怒り駆動開発 - キレる技術
@joker1007 さん

### スライド資料

<https://speakerdeck.com/joker1007/nu-riqu-dong-kai-fa-kireruji-shu-number-osrk01>

### 怒りの重要性について

心穏やかに生きていくほうが良い。  
しかし、怒りは無意味ではない。  

* イライラを持続させて仕事をすることは生産性が強烈に悪化する。
* 不満をため込む方が危険。

そして、単純にストレスコントロールとして重要であるだけではない。

怒りとは不満の発露。  
そもそも何も不満がないと、問題解決しようとは思わない。

### システム開発者＝問題解決者

我々は世の中への怒りや不満を解決するために仕事をしている。  
ある種、怒りと向き合う仕事であるともいえる。

### 身近な環境の不満

* 拡張しやすく読みやすいコード
* リソース豊富な開発機
* 高速で終わるCI
* 簡単なデプロイ環境
* 無駄のないアラート設計
* 必要十分な機能要求

すべてを満たしているだろうか？  
不満があって、より良くしたいと思わないだろうか？

### 不満を感じないのはある種の諦め

* 我々は完璧ではない。日々間違えて失敗する。そして失敗は蓄積し残る。
* 人間はすでにあるものを参考にしがちである。
* 割れ窓は容易に伝染する。よくないものは放置するだけでマイナスの結果につながる。

つまり「誰かが間違いを明確に示さなければならない。」でないと物事は改善しない。

### 誰が示すのか？

不満の閾値が低い人間。  
つまり怒りっぽい人間が示す。

### 怒りを示すときのルールは必要

以下のようなルールを策定している。

* 状態やコードにキレる。
* 自分の仕事の結果。
* 人間を対象にはしない。(自分の仕事の時だけは明確に自分に怒る。)
* 怒りを感じる合理的な理由を示す。
* 具体的にどうしたいかを示す。
* オープンに怒る。
* 可能なら直すまでやってしまう。

そして、行動して結果に出すまでに至るのが大事。

### しかし一方で…

確実に人にダメージを与える事も理解せねばならない。  
直接触れずとも自分の不始末は分かる。  
また、不満や問題点を表明するには怒りだけではない。

### まとめ

* 怒りはセンサーでありエネルギー源
* 仕事は不満と向き合い、より上手くやることを日々考える事が大事である。
* 人に罪は無い、人間は必ず間違る。

日々、問題を解決するのは簡単ではない、  
不満と向き合わねばならないが、だからこそ考える価値がある。

---

## Lightning Talk : Excelが嫌でRubyを始めたけど Excelから離れられない話
@satomicchy さん

Railsアプリから官庁への提出資料を出力する必要があった  
しかし形式がExcelだった。

### やりたいこと

* xslxテンプレートの準備
* Ralsアプリでデータ流し込み
* Ralsでxslxをダウンロード

### 現状何ができるか

gemが無いか調べて見たところ、  
spreadsheetx という物があったが、7年前から更新がなかった。

### やってみたこと

xslx = xmlファイルをzipしたものなので、  
ファイル名と同じフォルダを作って、その中でxslxをunzipして構造を確認した。  
gemの nokogiri でタグの改行とインデントを整形するところまでは出来ている。  

### 問題点

* standaloneじゃないxmlは、nokogiriで整形できなかった。
* libleOfficeで保存したxslxは、一部のxmlのstandaloneが変わる。

---

## Lightning Talk : CTOのおしごと
@yalab さん

### CTOになった経緯

プレスリリース駆動によりデスマでプロダクトを世に出してきた、その流れで燃え尽きた前CTOが辞任。

### 現状のメンバの状況

素直で頭の良い方々であったが我流が横行していた。

### 実施したこと

1. バージョンアップポリシーの策定  
　　- rubyはリリースから１ヶ月以内  
　　- gem, npm は随時  
　　- rails/SQLなどのインフラ周りは半年
2. インフラの統一  
3. 1on1 ペアプロを実施。  
　　- アイウエオ順で毎日一人ずつ1hに限ってペアプロを実施した。(我流の作業手順を排除するのが目的。)
4. esaの導入  
　　- 障害報告とチーム黄疸の知識の集約を実施。  
5. SPOFの解消  
　　- mailgunが2hほど止まっていた事があり大変な事になった。  
6. 避難訓練の整備  
　　- 誤ったデプロイのロールバック  
　　- バックアップからの復旧  
　　- 外部サービスのインシデントの際のフェイルバック

### これらの施策の結果

計測ツールを作成中。

---

## Lightning Talk : コミュニティを立ち上げて痛感した「ガチ初心者向け」勉強会の失敗しないやり方について。
@yukisun さん

### スライド資料

<https://www.slideshare.net/yukimasaki/the-way-ofstudymeetingnotfailing>

### Ruby歴2年程の発表者がRubyコミュニティを立ち上げた話。

関西Ruby開発

### なぜ、立ち上げたのか？

よくある勉強会で「初心者向け」と言いつつ、全然初心者向きじゃない。

* いざイベントに行くと小難しい話で溢れてる。
* 何を言っているのか理解できない。
* 勉強会が発表する為の場所と化しているように感じる。

### やってみたこと

RailsやGR-CいTRUSの勉強会を実施。  
とりあえず触ってみようがコンセプト。

### 対象者を初心者に絞った結果

PCも操作もままならないけど、プログラミングをやってみたい人が集まった。

しかし、以下のような問題があった。

* iPadだけを持ってきた人がいた。
* 罫線つきノートを持ってきた。(ハンズオンという言葉も理解していなかった様子。)

### 対策

* 概要欄にはPC持ち込みと書く。
* ハンズオンは3Hが限界。(適宜休憩を入れる)
* メンター1人につき、参加者は5人くらいが望ましい。
* Wi-Fi環境は必ず用意する。
* 資料はスライドとは別で紙媒体も用意する。
* 継続性を高めたほうが良いので続編を用意し、1週間以内に開催する。

### 課題を与える。

* scaffoldで構築したアプリを手作業でやってもらって、その結果などをSlackでフィードバック。
* Railsチュートリアルも課題としては良い。
* 最終的には万葉プロジェクトを。
　　<https://github.com/everyleaf/el-training>

課題を与えられる勉強会を開催してコミュニティを活性化したい。

---

## Lightning Talk : もう「クレデンシャルください」なんて言わせない
@zaru さん

### スライド資料

<https://speakerdeck.com/zaru_sakuraba/mou-kuredensiyarukudasai-nanteyan-wasenai>

### 好きなRubyメソッド

Enumerable#cycle  
<https://docs.ruby-lang.org/ja/latest/method/Enumerable/i/cycle.html>  

### Railsで秘匿情報の管理をどうするか？

プロジェクトに新しくプログラマがjoinした。

* 「.envください」
* 「アクセスキーください」

その都度、手で渡すのが面倒。  
秘匿情報の渡し方に神経を使う。

他の例で言うと開発をしていて環境変数を追加した。

* 「デプロイ前に環境変数をサーバへ追加」
* 「デプロイ前に .env.production修正します」
* 「Ansibleでサーバへ環境変数を追加します」

デプロイフローが煩雑になり、マージ以外に気を遣わねばならない。  
手順を間違えるとデプロイ失敗する。

### 解決策

Rails 5.2から Credentials が導入された。

Credentialsとは？

* 秘匿情報を１つのファイルで管理することができる。
* マスターキーで暗号化・復号化ができる。
* Gitで管理できるのでチームで共有しやすい

ただし、完璧な解決策ではない。

* 暗号化すると構造を維持していないので、中身がわからない
* コードレビューがやりにくい
* マスターキはやっぱり必要でマスターキーの管理の問題はある。

そこで解決策として、 (AWS|GCP)KMS + yaml_vault

yaml_vault  
<https://github.com/joker1007/yaml_vault>

yaml_vaultの恩恵

* YAMLの構造を保ったままvalueだけを暗号化できる。
* コードレビューがやりやすい
* デプロイ時にファイル展開ではなくメモリ展開出来るので、物理ファイルとしての秘匿情報をサーバに置かなくて良い。

マスターキーではなく IAM で開発者毎のクレデンシャルを渡せばOKなので開発者自身に管理して貰える。  
AWS EC2にロールを付与すればマスターキーなしに復元可。(マスターキーの管理も不要となる。)

### 現状の分からないこと

Herokuでの運用。  
AWS API Key があればどこでも使えるので問題はないが、  
Herokuアサインユーザであれば Config vars が見れてしまうので、キーが見えてしまう。

---

### Lightning Talk : Jupyter Notebook でRubyに親しむ
@kozo2 さん

Webブラウザで簡単にRubyを試したい。
　
Jupyter Notebook  
<http://jupyter.org/>

web browser 場で文芸的プログラミングを実現するようなサービス。  
PythonではJN場でスニペットを連ねてワークフローとして実行することが多くなった。  
jsの可視化ライブラリとの連携に強み。

Rubyでもデータ処理のワークフローの情報共有が行われないか？  
インストールフリーのNotebook SaaSでRubyも試せるようなサービスが出てくるといいな
