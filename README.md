# satcon.github.io
非エンジニアですが、Pyscriptで桃鉄ワールドのカード売り場マップを作製しています。  

## Google spreadsheetにデータを整理
①「駅名、緯度、経度、アイコンのファイル名、カード1～8」を入力  
 たくさんの場所の緯度経度を調べるのは割と手間なので、まとめてChatGPTに処理してもらった方がよい。  
②スプレッドシートのアクセスを「リンクを知っている全員」「閲覧者」にする。  
③セルに空欄が無いようにしておく。(pandasのiterrowsメソッドを使うため、空欄があるとエラーになる。)  
【参考】今回、使っているスプレッドシートはこれ↓  
https://docs.google.com/spreadsheets/d/1bG-512BNgFMSKzmBdVZEBzcyc8QsW3k-kOxe85OZE0U/edit?usp=sharing

## Pandasで読み込む
①スプレッドシートのURLを以下のようにする。  
https://docs.google.com/spreadsheets/d/スプレッドシートID/export?format=csv&gid=シートID  
シートが2枚以上ある場合はシート毎に処理を行う。シートIDは最初のシート番号が「0」だったので次のシート番号は「1」かと思ったらそうではなかった。シートを開いている時にURLに表示されている末尾の数字10桁ぐらい数字がシート番号になる。  
② URLを開いて、読み込む  

## Foliumでマップを描写
①iterrowsメソッドでスプレッドシートの情報を1行ずつ取り出す。  
②Foliumで緯度・経度情報を元に地図を描く。  
インテンドでグループ化されるので注意すること。

## 悪戦苦闘したところ
①図を読み込む際は、 「head」内の「py-env」でパスをあらかじめ記載しておかないと「FilieNotFound」エラーになる。  
②「py-script」のoutputでidをちゃんと指定しないと画面が真っ白で何も表示されなかった。  
例```<div id="任意の文字"></div>  　 
<py-script output="上記と同じ文字">```
