# cluster チャット転送プラグイン

<div class="tips-box">
  <h4>このプラグインでできること</h4>
  <p>あなたの音声認識結果を自動でclusterのチャット欄に送信し、VR空間でのコミュニケーションをサポートします。音声認識したメッセージをチャットに表示できるため、VR空間でのコミュニケーションがよりスムーズになります。</p>
  <p><strong>注意：</strong> この機能はcluster公式が提供しているものではありません。何か問題が発生した場合は、ゆかコネDiscordのサポートフォーラムに質問してください。</p>
</div>

<div class="purpose-grid">
  <a href="#_1" class="purpose-card">
    <div class="purpose-icon">⚙️</div>
    <h3>基本設定をする</h3>
    <p>最短1分でセットアップ</p>
  </a>
  <a href="#_2" class="purpose-card">
    <div class="purpose-icon">💬</div>
    <h3>使ってみる</h3>
    <p>実際にclusterで使ってみる</p>
  </a>
  <a href="#_3" class="purpose-card">
    <div class="purpose-icon">⚠️</div>
    <h3>注意点</h3>
    <p>使用時の注意点</p>
  </a>
</div>

## 準備するもの

1. **clusterデスクトップアプリ** - 事前にインストールしておく必要があります
2. **cluster内で参加可能なワールド** - 試してみるためのワールド
3. **ゆかコネの基本設定** - 音声認識が正しく動作する状態であること

## 基本設定の手順

<div class="step-guide">
  <div class="step-item">
    <h3>プラグインを有効にする</h3>
    <p>ゆかコネのプラグイン設定画面を開き、「cluster チャット転送」プラグインを有効にします</p>
    <div class="annotated-image">
      <img src="../images/plugin_clustertransfer_p1.png" alt="cluster連携プラグイン有効化">
      <div class="annotation" style="top: 40%; left: 70%;">
        チェックボックスをONにする
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>送信内容を選択する</h3>
    <p>設定ボタンをクリックし、どの内容を送信するか選択します</p>
    <div class="annotated-image">
      <img src="../images/plugin_clustertransfer_p2.png" alt="送信内容設定">
      <div class="annotation" style="top: 40%; left: 60%;">
        送信したい内容にチェックを入れる
      </div>
    </div>
    <div class="tips-box">
      <h4>送信内容の選択肢</h4>
      <ul>
        <li><strong>音声認識元言語のみ</strong>：あなたが話した言葉をそのまま送信</li>
        <li><strong>翻訳言語のみ</strong>：翻訳結果だけを送信</li>
        <li><strong>両方</strong>：元の言葉と翻訳の両方を送信</li>
      </ul>
    </div>
  </div>
</div>

## 使い方

<div class="step-guide">
  <div class="step-item">
    <h3>clusterを起動する</h3>
    <p>clusterデスクトップアプリを起動し、ワールドに入ります</p>
    <div class="tips-box">
      <h4>ポイント</h4>
      <p>cluster公式クライアント（デスクトップアプリ版）が必要です。ブラウザ版では動作しません。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>チャット画面を表示する</h3>
    <p>cluster内でチャットパネルを開き、入力欄にカーソルを合わせます</p>
    <div class="annotated-image">
      <img src="../images/plugin_clustertransfer_p3.png" alt="cluster画面">
      <div class="annotation" style="top: 40%; left: 60%;">
        チャット入力欄にカーソルを合わせる
      </div>
    </div>
    <div class="tips-box">
      <h4>重要</h4>
      <p>必ずチャット入力欄にカーソルを合わせた状態にしてください。そうしないと、音声認識の結果がキャラクターの動作に誤って反映される場合があります。</p>
    </div>
  </div>
  
  <div class="step-item">
    <h3>音声認識を開始する</h3>
    <p>ゆかコネで音声認識を開始します</p>
    <ul>
      <li>ゆかコネの音声認識ボタンをクリックし、認識を開始</li>
      <li>話し始めると、認識結果が自動的にclusterのチャット欄に送信されます</li>
    </ul>
  </div>
</div>

## 注意事項

<div class="tips-box">
  <h4>正しく動作させるためのポイント</h4>
  <ul>
    <li><strong>clusterが前面にある必要があります</strong> - バックグラウンドになっていると送信されません</li>
    <li><strong>チャット入力欄にカーソルを合わせる</strong> - カーソルがない場合、アバターが意図しない動作をする可能性があります</li>
    <li><strong>タイミング</strong> - 音声認識が確定した時点でチャットに送信されます</li>
    <li><strong>翻訳設定</strong> - 翻訳機能も使いたい場合は、あらかじめゆかコネ本体で翻訳設定を行っておく必要があります</li>
  </ul>
</div>

<div class="tips-box">
  <h4>対応していない機能</h4>
  <ul>
    <li>ブラウザ版clusterは非対応です</li> 
    <li>clusterからゆかコネへの転送はできません（一方向のみ）</li>
  </ul>
</div>

## 活用アイデア

<div class="purpose-grid">
  <div class="purpose-card">
    <div class="purpose-icon">🌎</div>
    <h3>多言語コミュニケーション</h3>
    <p>翻訳機能と組み合わせて国際交流を楽しむ</p>
  </div>
  <div class="purpose-card">
    <div class="purpose-icon">🎭</div>
    <h3>ロールプレイサポート</h3>
    <p>キャラクターのセリフを音声認識で素早く入力</p>
  </div>
  <div class="purpose-card">
    <div class="purpose-icon">🎤</div>
    <h3>イベントMC支援</h3>
    <p>話した内容を自動的にチャットに表示</p>
  </div>
</div>

<div class="tips-box">
  <h4>より快適に使うコツ</h4>
  <p>cluster内のボイスチャットを使いながら、同時に音声認識したテキストをチャットに流すことで、音声が聞き取りにくい環境でも会話を楽しめます。</p>
</div>
