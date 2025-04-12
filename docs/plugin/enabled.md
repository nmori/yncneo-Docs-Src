# プラグインの使い方ガイド

<div class="tips-box">
  <h4>このページについて</h4>
  <p>プラグインの有効化・無効化や基本的な使い方を説明します。プラグインを使えば、ゆかコネの機能を大幅に拡張できます！</p>
</div>

<div class="purpose-grid">
  <a href="#プラグインを有効にする" class="purpose-card">
    <div class="purpose-icon">✅</div>
    <h3>プラグインを有効にする</h3>
    <p>インストール済みのプラグインを使えるようにする</p>
  </a>
  <a href="#プラグインをロードする-非ロードにする" class="purpose-card">
    <div class="purpose-icon">⚙️</div>
    <h3>プラグインを管理する</h3>
    <p>プラグインのロード・非ロード設定</p>
  </a>
  <a href="#知っておくと便利なポイント" class="purpose-card">
    <div class="purpose-icon">💡</div>
    <h3>上手な使い方のコツ</h3>
    <p>プラグインの特性と効果的な使い方</p>
  </a>
</div>

## プラグインを有効にする

<div class="step-guide">
  <div class="step-item">
    <h3>メインメニューからプラグイン設定を開く</h3>
    <p>ゆかコネNEOのメインメニューから「プラグイン」を選択します</p>
    <div class="annotated-image">
      <img src="images/plugin_enabled_p1.png" alt="プラグイン有効化画面">
      <div class="annotation" style="top: 40%; left: 70%;">
        使いたいプラグインにチェックを入れる
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>使いたいプラグインを選択する</h3>
    <p>有効にしたいプラグインのチェックボックスをクリックします</p>
    <ul>
      <li><strong>チェックを入れる</strong> → プラグインが<strong>有効</strong>になります</li>
      <li><strong>チェックを外す</strong> → プラグインが<strong>無効</strong>になります</li>
    </ul>
  </div>
  
  <div class="step-item">
    <h3>設定を確認する</h3>
    <p>チェックを入れた直後からプラグインが機能します</p>
    <div class="tips-box">
      <h4>動作を軽くするコツ</h4>
      <p>必要なプラグインだけを有効にすると、動作が軽くなります。使わないプラグインはチェックを外しておきましょう。</p>
    </div>
  </div>
</div>

## プラグインをロードする・非ロードにする

使わないプラグインを完全に非ロード状態にすると、起動が速くなりメモリ消費も減ります。

<div class="step-guide">
  <div class="step-item">
    <h3>メンテナンスツールを開く</h3>
    <p>ゆかコネNEOのフォルダにある「MaintenanceTool.exe」を実行します</p>
    <div class="annotated-image">
      <img src="images/plugin_enabled_p2.png" alt="メンテナンスツール画面">
      <div class="annotation" style="top: 30%; left: 60%;">
        ロードしたいプラグインにチェックを入れる
      </div>
    </div>
  </div>
  
  <div class="step-item">
    <h3>ロード・非ロードを設定する</h3>
    <p>プラグインのチェックボックスで設定します</p>
    <ul>
      <li><strong>チェックを入れる</strong> → 起動時にプラグインが<strong>ロード</strong>されます</li>
      <li><strong>チェックを外す</strong> → 起動時にプラグインが<strong>ロードされなく</strong>なります</li>
    </ul>
  </div>
  
  <div class="step-item">
    <h3>ゆかコネを再起動する</h3>
    <p>設定は次回ゆかコネNEO起動時に反映されます</p>
    <div class="tips-box">
      <h4>ロードと有効化の違い</h4>
      <p>「ロード」はプラグインをメモリに読み込むかどうかの設定で、「有効化」はロードされたプラグインを使うかどうかの設定です。非ロードにすると起動が速くなりますが、使う場合はまずロードする必要があります。</p>
    </div>
  </div>
</div>

## 知っておくと便利なポイント

<div class="tips-box">
  <h4>プラグインの処理順序について</h4>
  <p>プラグインはリストの<strong>上から順に処理</strong>されます。例えば、辞書プラグインが適用した結果は、リストでその下にあるプラグインに影響します。重要なプラグインは上位に配置すると良いでしょう。</p>
</div>

<div class="tips-box">
  <h4>表示タイミングとプラグインの関係</h4>
  <p>表示タイミングの時間が経過すると、プラグイン側にデータを非表示にするよう指示されます。文字を消さずに維持したい場合は、オプション設定で表示タイミングを最大値にしてください。</p>
</div>

<div class="step-guide">
  <div class="step-item">
    <h3>プラグインの組み合わせ例</h3>
    <p>目的に合わせた効果的な組み合わせ例</p>
    <table>
      <tr>
        <th>使用目的</th>
        <th>おすすめプラグイン組み合わせ</th>
      </tr>
      <tr>
        <td>配信で英語字幕を表示</td>
        <td>・辞書プラグイン<br>・内蔵ブラウザプラグイン<br>・OBS連携プラグイン</td>
      </tr>
      <tr>
        <td>VRChatで多言語コミュニケーション</td>
        <td>・辞書プラグイン<br>・VRChat OSC連携プラグイン</td>
      </tr>
      <tr>
        <td>配信コメント連携</td>
        <td>・辞書プラグイン<br>・わんコメ連携プラグイン</td>
      </tr>
    </table>
  </div>
</div>

## よくある質問

<div class="step-guide">
  <div class="step-item">
    <h3>プラグインの設定はどこで変更できますか？</h3>
    <p>各プラグインの設定方法</p>
    <ol>
      <li>プラグインを有効化した状態で</li>
      <li>プラグイン名の右側にある「設定」ボタンをクリック</li>
      <li>プラグインごとの設定画面が開きます</li>
    </ol>
  </div>
  
  <div class="step-item">
    <h3>プラグインが機能しない場合は？</h3>
    <p>以下の点を確認してみてください</p>
    <ul>
      <li>プラグインがメンテナンスツールでロードされているか</li>
      <li>プラグインのチェックボックスが有効になっているか</li>
      <li>プラグインの設定が正しく行われているか</li>
      <li>他のプラグインが影響していないか（処理順序を確認）</li>
    </ul>
  </div>
  
  <div class="step-item">
    <h3>プラグインを新しく追加するには？</h3>
    <p>新しいプラグインは以下の方法で追加できます</p>
    <ol>
      <li>ゆかコネNEOを一度終了する</li>
      <li>プラグインファイル（.dll）をゆかコネNEOのPluginsフォルダにコピー</li>
      <li>ゆかコネNEOを起動し、メンテナンスツールでロード設定を行う</li>
    </ol>
  </div>
</div>

<div class="purpose-grid">
  <a href="../plugin/index/" class="purpose-card">
    <div class="purpose-icon">🧩</div>
    <h3>利用可能なプラグイン一覧</h3>
    <p>様々なプラグインの詳細を見る</p>
  </a>
  <a href="../qa/troubleshooting/" class="purpose-card">
    <div class="purpose-icon">🔧</div>
    <h3>トラブルシューティング</h3>
    <p>問題解決のヒント</p>
  </a>
</div>
