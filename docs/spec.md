# 何ができるか？

ゆかコネNEOは次のことをサポートします。
![Image title](images/totalmap.png)

* 音声認識（との繋ぎ）
* 翻訳
* 字幕表示
* 周辺ツールへの出力

## 具体的仕様

|項目|可否|補足|
|:--|:---|:---|
|多言語翻訳|〇|母国語＋４か国語まで|
|翻訳エンジン|状況による|●Microsoft翻訳エンジン<br>●Google翻訳エンジン<br>●DeepL Pro翻訳エンジン<br>●Amazon翻訳エンジン<br>●IBM 翻訳エンジン<br>●NAVER Papago翻訳エンジン<br>●共用翻訳サーバ(lexcon）<br>●[Google Apps Script翻訳](startup/startup_gas.md)<br>●Google 翻訳v3<br>●Tencentクラウド翻訳<br>●Baidu翻訳|
|音声認識|〇| ●[UDトーク](https://udtalk.jp/)<br>●ブラウザ音声認識<br>●ブラウザ音声認識(ガムベックさん開発)<br>●オフライン音声認識ライブラリ<br>●[Whisper音声認識](https://github.com/tyapa0/YukariWhisper)（tyapa0さん開発）|
|ゆかりねっと連携|〇|●ゆかりねっとプラグイン併用モード<br>●ブラウザエミュレート|
|OBS連携|〇| OBS Studio用 WebSocket v4/v5対応|
|読み上げ|〇|プラグインを使えば可能<br>●[A.I.Voice](https://aivoice.jp/)<br>●[CeVIO](https://cevio.jp/)/[CeVIO AI](https://cevio.jp/products_cevio_ai/)<br>●[AITalk3](https://www.ai-j.jp/consumer/kantan3/)<br>●[VOICEVOX](https://voicevox.hiroshiba.jp/)<br>●[COEIROINK on VOICEVOX](https://coeiroink.com/)<br>●[LMROID](https://lmroidsoftware.wixsite.com/nhoshio)<br>●[SHAREVOIX](https://www.sharevox.app/)<br>●SAPI5<br>●[VOICEROID2](https://www.ah-soft.net/shopbrand/ct92/)  <br>●[VOICEPEAK](https://www.ah-soft.com/voice/6nare/)(v1.1b2～)<br>●[ITVOICE](https://booth.pm/ja/items/4374126))<br>●ブラウザで発話可能なWeb読み上げ音声|
|表示形式|〇|●多言語<br>●VRオーバーレイ<br>●リスト<br>●ゲーム風<br>●コラボレイアウト<br>●わんコメテンプレ|
|辞書・ルビ|〇|プラグインで実現|
|FANBOX支援|〇|支援しなくても利用はできます。<br>支援するとみんなで支える企業版翻訳サーバがつかえるようになります|
|ツール連携|〇|●[わんコメ](https://onecomme.com/)(アスティさん)<br>●[ゆかりねっと](http://www.okayulu.moe/)(おかゆぅさん)<br>●[OBS Studio](https://obsproject.com/ja/download)<br>●[HTML5コメントジェネレータ](https://seesaawiki.jp/fcg/)(kilinさん)<br>●[HTML5コメントジェネレータ改](http://twinstraycat.kagome-kagome.com/commegene/commentgenerator_kai)(彼岸扇花さん)<br>●[MTGA自動解説ツール](https://github.com/poslogithub/binary-dist/tree/main/mtga-commentary-automation)(ぽsさん)<br>●[バーチャルモーションキャプチャー](https://vmc.info/)(あきらさん)<br>●[棒読みちゃん](https://chi.usamimi.info/Program/Application/BouyomiChan/)(みちあきさん)<br>●[AssistantSeika](https://hgotoh.jp/wiki/doku.php/documents/voiceroid/assistantseika/assistantseika-001a)(ゆかコネNEOv2.0.112より対応)<br>●[Softalk](https://www.vector.co.jp/soft/winnt/art/se412443.html)(CNCCさん)<br>●[VaNiiシリーズ](https://sabowl.sakura.ne.jp/gpsnmeajp/)(gpsnmeajpさん)<br>●[VTube Studio](https://denchisoft.com/)(DenchiSoftさん)<br>●[VRChat](https://hello.vrchat.com/)<br>●[VirtualCast](https://virtualcast.jp/)<br>●[cluster](https://cluster.mu/)<br>●[twitch](https://www.twitch.tv/)<br>●[neos VR](https://neos.com/)<br>※上記は一例。他にもプラグイン等で実現例あり|


## 翻訳の種類について

![翻訳リスト](./support/images/support_countermap.jpg)

* 支援については、 [こちら](support/support_summary.md)をご覧ください。
