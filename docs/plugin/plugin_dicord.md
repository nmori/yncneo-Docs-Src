# Discord BOT連携プラグイン

<div class="tips-box">
  <h4>このプラグインでできること</h4>
  <p>ゆかコネとDiscordを連携させ、以下のことができるようになります：</p>
  <ul>
    <li>あなたの音声認識結果をDiscordチャンネルに自動送信</li>
    <li>Discordチャンネルの会話をゆかコネに取り込み</li>
    <li>読み上げ音声をDiscordボイスチャンネルに流し込み</li>
  </ul>
</div>

<div class="purpose-grid">
  <a href="#_1" class="purpose-card">
    <div class="purpose-icon">⚙️</div>
    <h3>基本設定をする</h3>
    <p>Discord BOTの作成と連携設定</p>
  </a>
  <a href="#_2" class="purpose-card">
    <div class="purpose-icon">💬</div>
    <h3>使ってみる</h3>
    <p>実際の使い方と活用例</p>
  </a>
  <a href="#_3" class="purpose-card">
    <div class="purpose-icon">🔊</div>
    <h3>音声を流す</h3>
    <p>読み上げ音声をDiscordに流す</p>
  </a>
</div>

## 準備するもの

1. **Discordアカウント** - BOT登録に必要です
2. **Discord BOTの設定情報** - この後の手順で作成します
3. **書き込み先のDiscordチャンネル** - テキストチャンネルのIDが必要です

## 基本設定の手順

### ステップ1：プラグインを有効にする

<div class="step-guide">
  <div class="step-item">
    <h3>プラグイン一覧からDiscord BOTを有効化</h3>
    <p>ゆかコネのプラグイン設定画面を開き、Discord BOTプラグインを有効にします</p>
    <div class="annotated-image">
      <img src="../images/plugin_discord_p1.png" alt="Discord BOTプラグイン有効化">
      <div class="annotation" style="top: 0%; left: 60%;">
        チェックボックスをONにする
      </div>
    </div>
  </div>
</div>

### ステップ2：Discord BOTを作成する

<div class="step-guide">
  <div class="step-item">
    <h3>Discord開発者ポータルにアクセス</h3>
    <p><a href="https://discord.com/developers/applications" target="_blank">Discord開発者ポータル</a>を開き、アカウントでログインします</p>
    <div class="annotated-image">
      <img src="../../cs/images/cs_colab_discord_p9.png" alt="Discord開発者ポータル">
      <div class="annotation" style="top: 0%; left: 70%;">
        「New Application」をクリック
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>アプリケーション名を設定</h3>
    <p>BOTの名前を入力します（例：「ゆかコネ連携BOT」など）</p>
    <div class="annotated-image">
      <img src="../../cs/images/cs_colab_discord_p10.png" alt="アプリケーション名設定">
      <div class="annotation" style="top: 40%; left: 60%;">
        わかりやすい名前を入力
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>BOTの設定を行う</h3>
    <p>左メニューから「Bot」を選択し、BOTを作成します</p>
    <ol>
      <li>左側のメニューから「Bot」をクリック</li>
      <li>「Add Bot」ボタンをクリック</li>
      <li>確認ダイアログが表示されたら「Yes, do it!」をクリック</li>
    </ol>
  </div>
  
  <div class="step-item">
    <h3>重要：メッセージ閲覧権限を有効にする</h3>
    <p>BOTがメッセージを読めるように設定します（必須）</p>
    <div class="annotated-image">
      <img src="../images/plugin_discord_p3.png" alt="Intents設定">
      <div class="annotation" style="top: 10%; left: 50%;">
        「Message Content Intent」をONにする（重要）
      </div>
    </div>
    <div class="tips-box">
      <h4>注意</h4>
      <p>この設定を忘れると、BOTがDiscordのメッセージを読み取れず、連携機能が動作しません！</p>
    </div>
  </div>
</div>

### ステップ3：接続情報を取得する

<div class="step-guide">
  <div class="step-item">
    <h3>Client IDを取得</h3>
    <p>左メニューの「General Information」から「Application ID」をコピーします</p>
    <div class="annotated-image">
      <img src="../../cs/images/cs_colab_discord_p11-4.png" alt="Client ID取得">
      <div class="annotation" style="top: 30%; left: 60%;">
        この「Application ID」をコピー
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>トークンを取得</h3>
    <p>「Bot」ページで「Reset Token」をクリックし、トークンを表示してコピーします</p>
    <div class="annotated-image">
      <img src="../../cs/images/cs_colab_discord_p11.png" alt="トークン取得">
      <div class="annotation" style="top: 30%; left: 60%;">
        「Reset Token」→トークンをコピー
      </div>
    </div>
    <div class="tips-box">
      <h4>トークンの取り扱いに注意</h4>
      <p>トークンは他人に知られると、あなたのBOTを操作される恐れがあります。安全に管理してください。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>チャンネルIDを取得</h3>
    <p>Discordアプリでチャンネル名を右クリックし「IDをコピー」を選択</p>
    <div class="annotated-image">
      <img src="../../cs/images/cs_colab_discord_p13.png" alt="チャンネルID取得">
      <div class="annotation" style="top: 40%; left: 60%;">
        テキストチャンネルを右クリック→「IDをコピー」
      </div>
    </div>
    <div class="tips-box">
      <h4>IDが見つからない場合</h4>
      <p>IDをコピーするオプションが表示されない場合は、Discordの設定で「開発者モード」をオンにしてください。（設定→詳細設定→開発者モード）</p>
    </div>
  </div>
</div>

### ステップ4：プラグインに情報を設定

<div class="step-guide">
  <div class="step-item">
    <h3>プラグイン設定画面を開く</h3>
    <p>Discord BOTプラグインの「設定」ボタンをクリックします</p>
    <div class="annotated-image">
      <img src="../images/plugin_discord_p2.png" alt="プラグイン設定画面">
      <div class="annotation" style="top: 20%; left: 60%;">
        取得した情報を入力する
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>接続情報を入力</h3>
    <p>先ほど取得した3つの情報を入力します</p>
    <table>
      <tr>
        <th>設定項目</th>
        <th>入力する内容</th>
      </tr>
      <tr>
        <td>Client ID</td>
        <td>コピーしたApplication ID</td>
      </tr>
      <tr>
        <td>token</td>
        <td>コピーしたBOTトークン</td>
      </tr>
      <tr>
        <td>ChannelID</td>
        <td>コピーしたチャンネルID</td>
      </tr>
    </table>
  </div>
  
  <div class="step-item">
    <h3>接続認証を行う</h3>
    <p>「接続認証」ボタンをクリックして、BOTとの接続をテストします</p>
    <div class="annotated-image">
      <img src="../../cs/images/cs_colab_discord_p14.png" alt="接続認証">
      <div class="annotation" style="top: 10%; left: 60%;">
        「接続認証」を押す
      </div>
    </div>
    <div class="tips-box">
      <h4>接続に失敗する場合</h4>
      <ul>
        <li>入力情報（Client ID、トークン、チャンネルID）が正しいか確認</li>
        <li>BOTの「Message Content Intent」がONになっているか確認</li>
        <li>インターネット接続に問題がないか確認</li>
      </ul>
    </div>
  </div>
</div>

### ステップ5：転送設定を行う

<div class="step-guide">
  <div class="step-item">
    <h3>転送方向を選択</h3>
    <p>どの方向でデータをやり取りするか設定します</p>
    <ul>
      <li><strong>Discord→NEO</strong>：Discordのメッセージをゆかコネに取り込む</li>
      <li><strong>NEO→Discord</strong>：ゆかコネの音声認識結果をDiscordに送信する</li>
    </ul>
    <div class="tips-box">
      <h4>使い方に合わせて選択</h4>
      <p>両方向を有効にすると、音声認識した内容がDiscordに送信され、その返信も取り込めます。コラボ配信などで便利です。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>追加オプションを設定</h3>
    <p>必要に応じて追加設定を行います</p>
    <ul>
      <li><strong>トークセッションに対応</strong>：コラボ配信など複数人のやり取りではONにする</li>
      <li><strong>BOTも受信対象</strong>：BOTの投稿も受信したい場合はONにする</li>
      <li><strong>次の文字を含む文字の投稿を受信</strong>：特定のキーワードを含むメッセージだけ取り込みたい場合に設定</li>
    </ul>
  </div>
</div>

### ステップ6：BOTをDiscordサーバーに招待

<div class="step-guide">
  <div class="step-item">
    <h3>招待URLを生成</h3>
    <p>Discord開発者ポータルの「OAuth2」→「URL Generator」で招待URLを作成</p>
    <ol>
      <li>左メニューから「OAuth2」→「URL Generator」を選択</li>
      <li>「SCOPES」で「bot」にチェック</li>
      <li>「BOT PERMISSIONS」で必要な権限（最低限「Send Messages」と「Read Message History」）にチェック</li>
      <li>生成されたURLをコピー</li>
    </ol>
  </div>
  
  <div class="step-item">
    <h3>BOTをサーバーに追加</h3>
    <p>コピーしたURLをブラウザで開き、BOTを追加したいサーバーを選択</p>
    <div class="annotated-image">
      <img src="../images/plugin_discord_p4.png" alt="BOT権限設定">
      <div class="annotation" style="top: 40%; left: 60%;">
        必要な権限を選択
      </div>
    </div>
    <div class="tips-box">
      <h4>最小限の権限設定</h4>
      <p>セキュリティのため、BOTに必要最小限の権限だけを与えることをおすすめします。基本は「メッセージの送信」と「メッセージ履歴の閲覧」だけで十分です。</p>
    </div>
  </div>
</div>

## 具体的な使い方

設定が完了したら、以下のような使い方ができます：

<div class="purpose-grid">
  <a href="../../cs/cs_colab_discord/" class="purpose-card">
    <div class="purpose-icon">🎮</div>
    <h3>Discord経由でコラボ配信</h3>
    <p>配信者同士の音声を字幕共有</p>
  </a>
  <a class="purpose-card">
    <div class="purpose-icon">🌐</div>
    <h3>国際交流</h3>
    <p>翻訳字幕をDiscordに送信して多言語コミュニケーション</p>
  </a>
  <a class="purpose-card">
    <div class="purpose-icon">📝</div>
    <h3>議事録作成</h3>
    <p>会議の内容を自動的にDiscordに記録</p>
  </a>
</div>

より詳しい使い方は、[Discord経由でコラボする方法](../cs/cs_colab_discord.md)を参考にしてください。

## 特殊な使い方：読み上げ音声をDiscordに流す

ゆかコネの読み上げ機能と組み合わせて、音声をDiscordのボイスチャンネルに流すことができます。

<div class="step-guide">
  <div class="step-item">
    <h3>前提条件を確認</h3>
    <p>以下の条件をすべて満たす必要があります</p>
    <ul>
      <li>読み上げプラグインが有効になっている</li>
      <li>読み上げプラグインで読み上げる設定になっている</li>
      <li>Discord側でボイスチャンネルを用意している</li>
      <li>BOTに音声チャンネルへの参加権限を付与している</li>
    </ul>
  </div>
  
  <div class="step-item">
    <h3>設定を有効にする</h3>
    <p>Discord BOTプラグインの設定で「Discordに音声を流し込む」にチェックを入れます</p>
    <div class="tips-box">
      <h4>使用許諾について</h4>
      <p>一部の音声合成エンジンでは、この使い方が禁止されている場合があります。使用する音声エンジンの利用規約を必ず確認してください。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>動作確認をする</h3>
    <p>ゆかコネで音声認識し、読み上げが行われるとDiscordのボイスチャンネルにも音声が流れます</p>
    <div class="tips-box">
      <h4>対応していないエンジン</h4>
      <p>音声ファイルを生成できるエンジンのみ対応しています。CeVIO CS/AI、A.I.Voiceなど一部のエンジンでは機能しない場合があります。</p>
    </div>
  </div>
</div>

## トラブルシューティング

<div class="tips-box">
  <h4>BOTがメッセージを取得できない</h4>
  <ul>
    <li>Discord開発者ポータルのBot設定で「Message Content Intent」がONになっているか確認</li>
    <li>BOTがチャンネルのメッセージを読む権限を持っているか確認</li>
    <li>チャンネルIDが正しいか確認（カテゴリではなく個別のチャンネルIDが必要）</li>
  </ul>
</div>

<div class="tips-box">
  <h4>「接続認証」でエラーが出る</h4>
  <ul>
    <li>Client IDとトークンが正しいか確認</li>
    <li>インターネット接続に問題がないか確認</li>
    <li>トークンが再生成された場合は新しいトークンを設定</li>
  </ul>
</div>

<div class="tips-box">
  <h4>BOTがDiscordサーバーに表示されない</h4>
  <ul>
    <li>招待URLのパーミッション設定を確認</li>
    <li>開発者ポータルでBOTが作成されているか確認</li>
    <li>BOTを正しいサーバーに招待したか確認</li>
  </ul>
</div>
