# VRChatで自分の声を字幕表示する方法

<div class="tips-box">
  <h4>このページについて</h4>
  <p>VRChatで自分の話した言葉を字幕として表示する方法を説明します。これにより、チャット入力なしで会話内容を共有したり、多言語翻訳で国際交流を楽しめるようになります！</p>
</div>

<div class="purpose-grid">
  <a href="#_1" class="purpose-card">
    <div class="purpose-icon">📋</div>
    <h3>必要なものを確認</h3>
    <p>VRChat連携に必要なもの</p>
  </a>
  <a href="#_2" class="purpose-card">
    <div class="purpose-icon">⚙️</div>
    <h3>設定する</h3>
    <p>ゆかコネとVRChatの連携設定方法</p>
  </a>
  <a href="#_3" class="purpose-card">
    <div class="purpose-icon">🎮</div>
    <h3>使ってみる</h3>
    <p>実際の使い方と設定のコツ</p>
  </a>
</div>

## 準備するもの

VRChat連携を始める前に、以下のものが必要です：

1. **ゆかコネNEO** - 最新バージョンがインストール済みであること
2. **VRChat OSCプラグイン** - v1.3b以上が必要
3. **VRChat** - 最新版（VRモードでもデスクトップモードでも可）
4. **同一PC上で動作** - ゆかコネとVRChatは同じPC上で動かす必要があります

## 基本設定の手順

### ステップ1：ゆかコネNEOの基本設定

<div class="step-guide">
  <div class="step-item">
    <h3>プロフィールを設定する</h3>
    <p>自分の名前と話す言語を設定します</p>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p4.png" alt="プロフィール設定画面">
      <div class="annotation" style="top: 40%; left: 60%;">
        あなたの名前と言語を入力
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>音声認識方法を選ぶ</h3>
    <p>「ブラウザ音声認識」が最も簡単です</p>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p5.png" alt="音声認識設定画面">
      <div class="annotation" style="top: 30%; left: 70%;">
        「ブラウザ音声認識」を選択
      </div>
    </div>
    <div class="tips-box">
      <h4>マイク設定について</h4>
      <p>マイク入力デバイスはブラウザの設定画面で選択します。うまく認識しない場合は<a href="../startup/startup_asr/">音声認識トラブルシューティング</a>をご覧ください。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>翻訳方法を選ぶ</h3>
    <p>無料の共用翻訳サーバーか、支援版翻訳を選べます</p>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p6.png" alt="翻訳設定画面">
      <div class="annotation" style="top: 25%; left: 65%;">
        「共用翻訳サーバー」が無料で使えます
      </div>
    </div>
    <div class="tips-box">
      <h4>支援版翻訳について</h4>
      <p>支援版を使う場合は、<a href="../support/support_howto/">FANBOXからプロモーションコード</a>を取得する必要があります。お試しコードをお持ちの方は下の画面で入力できます。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>支援コードを入力（支援版のみ）</h3>
    <p>支援版翻訳を使う場合は、プロモーションコードを入力します</p>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p8.png" alt="プロモーションコード入力画面">
      <div class="annotation" style="top: 40%; left: 70%;">
        ここにコードを入力
      </div>
    </div>
  </div>
</div>

### ステップ2：VRChat OSCプラグインの設定

<div class="step-guide">
  <div class="step-item">
    <h3>OSCプラグインを有効にする</h3>
    <p>プラグインメニューからVRChat OSCプラグインを有効にします</p>
    <div class="annotated-image">
      <img src="../../plugin/images/plugin_vrchat_osc_p1.png" alt="OSCプラグイン有効化画面">
      <div class="annotation" style="top: 10%; left: 70%;">
        プラグインを選択して「有効化」をクリック
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>VRChatを起動する</h3>
    <p>ゆかコネNEOと同じPC上でVRChatを起動します</p>
    <div class="tips-box">
      <h4>VRChatについて</h4>
      <p>VRモードでもデスクトップモードでも使用可能です。必ず最新版にアップデートしておきましょう。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>OSC送信設定を行う</h3>
    <p>OSCプラグインの設定画面を開き、送信設定を行います</p>
    <div class="annotated-image">
      <img src="../../plugin/images/plugin_vrchat_osc_p2.png" alt="OSC送信設定画面">
      <div class="annotation" style="top: 30%; left: 60%;">
        「Open」をクリック
      </div>
      <div class="annotation" style="top: 50%; left: 70%;">
        「Native」と「Translate1」をONに
      </div>
    </div>
    <ol>
      <li>プラグイン設定から「Open」をクリック</li>
      <li>VRChat枠内の「Native」と「Translate1」をONにする</li>
      <li>ゆかコネNEOで翻訳1の設定をする</li>
      <li>「OK」を押して設定を保存</li>
    </ol>
  </div>
</div>

### ステップ3：VRChat側の設定

<div class="step-guide">
  <div class="step-item">
    <h3>VRChat内でOSC機能をONにする</h3>
    <p>VRChat内のリングメニューからOSC機能を有効にします</p>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p1.png" alt="VRChatメニュー画面1">
    </div>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p2.png" alt="VRChatメニュー画面2">
      <div class="annotation" style="top: 40%; left: 70%;">
        この項目を選択
      </div>
    </div>
    <div class="annotated-image">
      <img src="../images/cs_vrchat_p3.png" alt="VRChatメニュー画面3">
      <div class="annotation" style="top: 40%; left: 60%;">
        機能をONにする
      </div>
    </div>
  </div>
</div>

## 実際に使ってみる

<div class="step-guide">
  <div class="step-item">
    <h3>音声認識を開始する</h3>
    <p>ゆかコネNEOの音声認識ボタンをクリックして、認識を開始します</p>
    <ol>
      <li>ゆかコネNEOの「音声認識」ボタンをクリック</li>
      <li>ブラウザで「Start」を押す</li>
      <li>マイクに向かって話してみる</li>
    </ol>
  </div>
  
  <div class="step-item">
    <h3>VRChatで字幕を確認</h3>
    <p>あなたの話した言葉とその翻訳がVRChat内のチャットボックスに表示されます</p>
    <div class="tips-box">
      <h4>表示のカスタマイズ</h4>
      <ul>
        <li>VRChatメインメニューの設定でチャットボックスの表示位置を調整できます</li>
        <li>文字サイズや表示方法は各ユーザーが自分の設定で調整できます</li>
        <li>文字数が多すぎると表示が切れることがあるので、短めの文章がおすすめです</li>
      </ul>
    </div>
  </div>
</div>

## よくある質問と解決法

<div class="tips-box">
  <h4>VRChatに字幕が表示されない場合</h4>
  <ul>
    <li>VRChat側でOSC機能が有効になっているか確認</li>
    <li>ゆかコネのOSCプラグイン設定で「Native」と「Translate1」がONになっているか確認</li>
    <li>ゆかコネとVRChatは同じPC上で動作しているか確認</li>
    <li>VRChatを最新バージョンにアップデートしてみる</li>
  </ul>
</div>

<div class="tips-box">
  <h4>翻訳が表示されない場合</h4>
  <ul>
    <li>翻訳設定で正しい言語を選択しているか確認</li>
    <li>支援版を使用している場合はプロモーションコードが正しく入力されているか確認</li>
    <li>音声認識がうまくいっているか確認（ゆかコネの画面で認識結果が表示されるか）</li>
  </ul>
</div>

<div class="purpose-grid">
  <a href="../../plugin/plugin_vrchat_osc/" class="purpose-card">
    <div class="purpose-icon">🔧</div>
    <h3>より詳しい設定を知りたい</h3>
    <p>VRChat OSCプラグインの詳細設定</p>
  </a>
  <a href="../../startup/startup_asr/" class="purpose-card">
    <div class="purpose-icon">🎤</div>
    <h3>音声認識が上手くいかない</h3>
    <p>音声認識のトラブルシューティング</p>
  </a>
</div>
