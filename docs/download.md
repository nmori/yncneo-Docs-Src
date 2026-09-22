# ダウンロードとインストール

<div class="purpose-grid">
  <a href="#_3" class="purpose-card">
    <div class="purpose-icon">🚀</div>
    <h3>最新版を使いたい</h3>
    <p>最新機能が使える最新バージョン</p>
  </a>
  <a href="#_2" class="purpose-card">
    <div class="purpose-icon">✅</div>
    <h3>安定版を使いたい</h3>
    <p>動作が安定している推奨バージョン</p>
  </a>
  <a href="#_5" class="purpose-card">
    <div class="purpose-icon">🔄</div>
    <h3>再インストールしたい</h3>
    <p>問題解決のための再インストール手順</p>
  </a>
</div>

!!! tip "どれを選べばいい？"
    * ふだん配信で使うなら **最新版（v2.3 系）** がおすすめです
    * **v3.0 は先行開発版（ベータ）**です。画面と設定の持ち方が大きく変わっています。
      上げる前に [v2.3 → v3.0 の移行](mig/mig_neo_v3.0.md) を読んでください
    * どちらのドキュメントを読むかは [ドキュメントのバージョン](versions.md) をご覧ください

## 安定版をダウンロード

### v2.3.58 [ダウンロード](https://machanbazaar.com/wp-content/uploads/2026/02/YNCNEO_v2.3.58.zip)

・アプリが勝手に落ちるパターンを修正
※最新版が安定次第、安定版に移行します。

## 最新版をダウンロード

### v2.3.133 [ダウンロード](https://machanbazaar.com/wp-content/uploads/2026/09/YNCNEO_v2.3.133.zip)

・プリセット周りの修正

## 先行開発版をダウンロード

### v3.0.0 beta 24 [ダウンロード](https://machanbazaar.com/wp-content/uploads/2026/09/YNCNEO_v3.0.0-beta24.zip)

・表記の修正

<div class="tips-box">
  <h4>v3.0 を入れる前に</h4>
  <ul>
    <li><strong>v2.3 と同じフォルダに上書きしないでください。</strong>別のフォルダに展開します</li>
    <li>.NET ランタイムを同梱しているので<strong>別途インストールは要りません</strong>。内蔵ブラウザが WebView2 になったぶん、容量は v2.3 より小さくなっています（展開後でおよそ 1GB）</li>
    <li>設定は自動では完全に引き継がれません。<strong>「設定保存・復元」→「v2.3設定を移行」</strong>を 1 回実行してください</li>
    <li>自作・個人配布のプラグインは、<strong>.NET 10 対応版でないと読み込めません</strong></li>
    <li><a href="../mig/mig_neo_v3.0/">v2.3 → v3.0 の移行</a>に、やることがまとまっています</li>
  </ul>
</div>

<div class="tips-box">
  <h4>インストール前のポイント</h4>
  <ul>
    <li>配信直前などの重要な時間帯は避けてインストールしましょう</li>
    <li>「ゆかりねっと」のフォルダとは別のフォルダにインストールしてください</li>
    <li>支援モードを使う方は<a href="https://nmori.github.io/yncneo-Docs/support/support_howto/#2">FANBOXから新しいキーを取得</a>してください</li>
  </ul>
</div>

## インストール後によくある問題と解決法

<div class="step-guide">
  <div class="step-item">
    <h3>表示レイアウトがおかしい場合</h3>
    <p>テンプレートを再生成すると解決することがあります</p>
    <div class="annotated-image">
      <img src="../images/templete_remake.png" alt="テンプレート再生成ボタン">
      <div class="annotation" style="top: 30%; left: 70%;">
        このボタンをクリック
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>再起動するたび表示が消える場合</h3>
    <p>フォームを取り込むことで解決できます</p>
    <div class="annotated-image">
      <img src="../images/tolocal.png" alt="フォーム取り込みボタン">
      <div class="annotation" style="top: 30%; left: 70%;">
        このボタンをクリック
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>支援翻訳ができなくなった場合</h3>
    <p>内部認証の再実行が必要かもしれません</p>
    <a href="../v3.0/support/support_enabled/" class="md-button">支援機能の設定方法</a>
  </div>
</div>

## 開発版

<div class="tips-box">
  <h4>開発版について</h4>
  <p>開発版は最新機能を試せる一方で、不具合が含まれている可能性があります。通常利用には安定版または最新版をおすすめします。</p>
</div>

<div class="tips-box">
  <h4>もっと詳しく知りたい方へ</h4>
  <ul>
    <li><a href="../qa/history/">更新履歴を確認する</a></li>
    <li><a href="../v3.0/qa/before_help/">トラブルシューティングガイド</a></li>
  </ul>
</div>

## 再インストール方法

問題が解決しない場合は、再インストールをお試しください。特に長期間アップデートしていない場合は再インストールをおすすめします。

<a href="../v3.0/qa/reinstall/" class="md-button">再インストール手順を見る</a>
