# satcon.github.io
非エンジニアですが、Pyscriptで桃鉄ワールドのカード売り場マップを作製しています。  

## マップ作成方法
コードはindex.htmlをコピペして使ってください。
### ①Google spreadsheetにデータを整理
【参考】今回、使っているスプレッドシートはこれです↓。  
https://docs.google.com/spreadsheets/d/1bG-512BNgFMSKzmBdVZEBzcyc8QsW3k-kOxe85OZE0U/edit?usp=sharing  

(1)スプレッドシートの１行目に「駅名」「緯度」「経度」「アイコン」「カード1～8(8列分)」を入力。  
 後ほど、iterrowsメソッドを使ってスプレッドシートのデータを呼び出すので、１行目の名称は重複しないようにしておく。  
 また、たくさんの場所の緯度経度を調べるのは割と手間なので、まとめてChatGPTに処理してもらった方がよい。  
(2)スプレッドシートのアクセス権を「リンクを知っている全員」「閲覧者」にする。  
(3)セルに空欄が無いようにしておく。(pandasのiterrowsメソッドを使う時に空欄があるとエラーになるもよう。)  

### ②Pandasでスプレッドシートを読み込む
(1)スプレッドシートのURLを以下のようにする。  
https://docs.google.com/spreadsheets/d/スプレッドシートID/export?format=csv&gid=シートID  
シートが2枚以上ある場合はシート毎に処理を行う。    
(2)URLを開く  
(3)読み込む  

### ③Foliumでマップを描写
(1)iterrowsメソッドでスプレッドシートの情報を1行ずつ取り出す。  
(2)Foliumで緯度・経度情報を元に地図を描く。  
インテンドを間違えるとエラーになるので注意する。

## 悪戦苦闘したところ
~~(1)アイコンの図を読み込む際は```<head>```内の```<py-env>```でパスをあらかじめ記載しておかないと「FilieNotFound」エラーになる。~~  
(2)```<py-script>```内の```<output>```のidを指定しないと画面が真っ白で何も表示されないもよう。  
成功例```<div id="任意の文字"></div>  　 
<py-script output="上記divで指定したidと同じ文字列">```  
(3)シートIDは最初のシート番号が「0」だったので次のシート番号は「1」かと思ったらそうではない。  
シートを開いている時にURLに表示される末尾の数字10桁ぐらいがシート番号。

## 2024年2月改定箇所
①```<py-env>```が使えなくなったため、```<py-config>```に変更。  
②画像ファイルが相対パスで読み込めなくなったので、絶対パスに変更。<br>
画像を絶対パスで読み込む方法<br>Github上に画像ファイルをアップ⇒画面右上の「・・・」ボタンを押す⇒「Copy permalink」を選択して絶対パスを取得する。
## 2025年3月改定箇所
①Script typeを変更<br>
修正前```<script defer src="https://pyscript.net/latest/pyscript.js"></script>```<br>
修正後```<script type="module" src="https://pyscript.net/releases/2024.1.1/core.js"></script>```<br>
②「from pyscript import display」追加<br>
③マップが表示されるまで時間がかかるので「Loading…」を追加<br>
(1)head部位<br>
```<script type="module">```<br>
```const loading = document.getElementById('loading');```<br>
```addEventListener('py:ready', () => loading.close());```<br>
```loading.showModal();```<br>
```</script>```<br>
(2)body部位<br>
```<dialog id="loading">```<br>
```<h1>Loading...</h1>```<br>
```</dialog>```<br>

