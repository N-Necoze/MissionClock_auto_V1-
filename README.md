# 【エヴァンゲリオン】ヤシマ作戦みたいな臨場感と緊張感があるタイマーアプリを作りたい

## はじめに

「シン・エヴァンゲリオン劇場版」の興行収入100億円超えおめでとうございます。小さい頃からエヴァンゲリオンが大好きで庵野秀明展も機会があったら行きたいと考えております。<br>
私情はさておき、今回開発したアプリケーションはエヴァンゲリオンでも絶大な人気を誇る作戦、「ヤシマ作戦」を彷彿とさせるタイマーを開発しました。<br>

## 用途
長いスパンの目標を立てるときに必ず期限を守るという作戦意識を持つときに使用します。長いスパンの目標を立てると中には途中で垂れてしまって、最終的に約束の期限を過ぎてしまい悲惨な事態になってしまうかもしれない…<br>（例えば、研究論文提出日や納期など…（とても大事））<br>
そんな時、このアプリケーションをデスクトップに画面表示させておくと、残りの時間が一目瞭然。作戦を遂行しているかのような臨場感と緊張感がある日常に変わり、大事な期限に間に合うようという意識を変えるために開発しました。<br>
ロックな方からすると「なんといやらしいタイマーなんだ…」なんて言われそうですが（笑）<br>

## 作戦画面作成方法

### 1.カウントダウン名と期限日時を設定する。

アプリを起動すると以下のようにカウントダウン名と期限日時の設定ができます。入力例は期限1個目の設定の際のみ表示されるので、例を見ながら設定していくとエラーにならずに実行できます。

<img src="https://user-images.githubusercontent.com/84171767/147560895-d0091676-a006-4a62-9e5b-2962a6820e47.png" width="550px">

### 2.画面の遷移

期限を設定後、Enterを押すとカウントダウン名が英語翻訳されます。翻訳される原理としてはSeleniumというAPIを利用して、Google翻訳を使用して翻訳結果を抽出し、その結果を表示します。

<img src="https://user-images.githubusercontent.com/84171767/147633121-6b13afec-e948-492f-a34b-02bdf6d57fb3.png" width="550px"> 
 

### 3.完成画面

実行した結果を表示すると以下のようになります。作戦が完了すると「0日 0:0:0」と表示されます。全ての作戦が終了しても表示されたままなので、作戦アプリを終了させたい時は赤ボタン(Mac)もしくは×ボタン(Win)を押すとプログラムが終了します。

<img src="https://user-images.githubusercontent.com/84171767/147385620-6a461235-a934-4e7e-a018-d7b8f4d6fed2.png" width="550px"> 

## 実装

### 開発環境

* MacBook Air (13-inch, 2017)
* Jupyterlab 3.0.14

### 試験環境(OS)

* mac OS（Big Sur）
* Windows OS（Windows 10 Pro）

### Installation

* Python 3.7.4
* tkinter 8.6
* Google Chrome 96.0.4664.110
* WebDriver 96.*
* selenium 4.1.0
* [けしのみ工房-keshikan.net]さまのDSEG(DSEG7 Classic Bold)

### それぞれのインストール方法

* 【Python】<br>
 Pythonのインストールに関してはもともと入っていると仮定して省略いたします。<br>
 もしPythonがインストールされていない場合は、以下のURLから公式HPに行けますので、ダウンロードして以下の手順に進んでください。

 [Python - 公式HP](python.org)

* 【Chrome】<br>
 WebスクレイピングツールSeleniumを使用するには、WebDriverとSeleniumモジュールをインストールしなければなりません。また、WebエンジンはGoogle Chromeを使うことを推奨されています。Chromeのダウンロードは以下からできます。

[Google Chrome - HP](https://www.google.co.jp/intl/ja/chrome/)

そしてインストールするWebDirverのバージョンを決めるために、インストールされているChromeのバージョンを確認します。私の環境では 96.0.4664.110 がインストールされていました。

<img src="https://user-images.githubusercontent.com/84171767/147740543-77461b60-5341-4e3b-9e54-b936c59a8b07.png" width="550px"> 

* 【WebDriver】<br>
 Chromeのバージョンと対応したWebDriverをインストールする必要があるので、pipで以下のようにメジャーバージョンのみ指定してWebDriverをインストールします。
 
```bash
pip install chromedriver-binary==96.*
```

* 【Selenium】<br>
 PythonへのSeleniumライブラリのインストールはpipを使います。
 
```bash
pip install selenium
```

* [けしのみ工房-keshikan.net]さまのDSEG(DSEG7 Classic Bold)<br>
  DSEGは以下のURLからダウンロードをしてください。こちらは数字をセグメント表示するために使用せていただいております。
  
  [けしのみ工房-keshikan.net - DSEG](https://www.keshikan.net/fonts.html)

## Seleniumの動作を確認してみる

先ほどのライブラリをそれぞれインストールした後、以下のプログラムを実行してみてください。<br>
正常にインストールできていましたら、以下のプログラムを実行するとGoogleの検索エンジンの画面が表示されます。

```bash
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
import time

browser = webdriver.Chrome(ChromeDriverManager().install())

browser.get('https://www.google.com/?hl=ja')
time.sleep(2)
browser.close()
```

## 実行方法
 
実行方法はそれぞれですが、今回はコマンドによる実行を記載しておきます。<br>
まず、「mission_clocke2.py」をダウンロードします。私はダウンロードしたものをデスクトップにおきます。
ターミナル(Mac)を開いてPythonと記述し、その後に「mission_clocke2.py」をドラック&ドロップしてください。
 
```bash
python /Users/ユーザーネーム/Desktop/mission_clocke2.py 
```

## 自己評価

今回作成したアプリケーションを実際に研究室で使用しているのですが、電子掲示板のように使われており、多忙な研究生からは残りの時間をすぐ見れて計画を立てやすいとの意見をいただきました。当初は緊張感や臨場感を与え、急がせるために開発したのですが、新しい観点で利用してくれた研究生もいたので、今後もアップデートをして新しい価値を生み出せたらと思いました。<br>
しかしながら、課題点もあり、時間の指定や期限名の指定はターミナル（mac）やコマンドシェル(Win)で行っており、操作性に難があると感じたと思うので、入力部分もUI化を行い、画面遷移できるアプリケーションにブラッシュアップし、期限の数も指定できるようにしたいです。また、期限名を自動で英語に変換するためにGoogle翻訳を用いて翻訳しているのですが「仕事納め」が「お金を納める」という翻訳になっているので、今後はこの部分のロジックの改良をしていきたいです。<br>
総評としては、まだまだユーザーに本格的に提供できる状態ではないのですが、多くのユーザーに使ってもらえるように改良を努力していきたいと考えています。

## 最後に

最後まで読んでいただきありがとうございます。今回はtkinterとPythonを使用してアプリケーションを作ったのですが、DjangoとPythonを用いたWebアプリケーションを開発していきたいと考えています。
また、マニュアル版アプリも作っていますので、APIの設定が面倒だな、、、と思った方はそちらを利用してもいいかもしれません。URLは以下に示しております。

## 派生アプリ（マニュアル版）
MissionClock_MT：https://github.com/N-Necoze/MissionClock_MT

## 参考文献
Python HP：https://docs.python.org/ja/3/library/tkinter.html <br>
とある科学の備忘録：https://shizenkarasuzon.hatenablog.com/entry/2018/12/31/064646 <br>
紫藤のページ：https://www.shido.info/py/tkinter2.html

## Author
 
* 作成者  : N-Necoze