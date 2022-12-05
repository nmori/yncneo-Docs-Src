!!! Info "前提条件"
    * なし

## このプラグインで出来ること

* GPT3を使い画像を生成し、写真を表示します

!!! Warn "ライセンスについて"
    * この機能を使うためには、個人がOpenAIからAPIキーを取得する必要があります。
    * 使用条件はOpenAIの規約に従ってください。

##　有効化

![再生](images/plugin_gpt3_p1.png)

* プラグインを使うチェックをONにしてください。

## 動作の仕組み

基本的にはGPT３をつかった機能として2つ用意されています。

* 会話内容を判断しマスクする機能
* 会話内容に応じて画像を生成する機能

!!! Info "会話内容のマスクについて"
    会話内容のマスクは、現在英語のみサポートされており、他の言語では判断が鈍ることがあります

## 設定

![再生](images/plugin_gpt3_p2.png)

|設定|意味|
|:--|:---|
|写真画面|写真を表示するための画面を表示します|
|いつまで出すか|画像表示をどれぐらい行うか決めます|
|APIキー| OpenAIのページで取得したキーを入れます  |
|Organaization| OpenAIに複数の契約をしている場合は、所属判別のキーをいれます。特に指定がない場合は空欄にします。|
|Model|判断させるAIのモデルをえらびます。これによってAPIが出力する結果およびOpenAIで処理すべき費用がかわります。|


![再生](images/plugin_gpt3_p3.png)

|設定|意味|
|:--|:---|
|場合によって発言を削除|特定のレートを超えた場合に、文を「***」に置き換えます|
|いつまで出すか|画像表示をどれぐらい行うか決めます|
|閾値|この数値を超えた場合に「***」に置き換えます。目安として75%ぐらいから様子を見るとよいでしょう|
|画像を生成|認識した文章をもとに画像を生成します。画像サイズも自分でえらびます|
|起動ワード|すべての認識を生成すると、OpenAIの利用料金が高くなるため、指定ワードが含まれていたときのみ生成するように指定できます(利用推奨)。空欄にするとすべての認識を変換するようになります|

## 使い方
1. 音声認識させると自動的に処理されます。
