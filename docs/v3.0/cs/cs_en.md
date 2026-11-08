# 5分で英語字幕表示を始める方法

<!-- version-banner -->
!!! info ""
    ゆかコネNEO **v3.0** のドキュメントです。v2.3 をお使いの方は [v2.3 版のこのページ](../../v2.3/cs/cs_en.md) を、違いを知りたい方は [v2.3 から v3.0 への移行](../../mig/mig_neo_v3.0.md) をご覧ください。


<div class="tips-box">
  <h4>このページについて</h4>
  <p>あなたの日本語を英語に翻訳して字幕表示する最も簡単な設定方法を説明します。このガイドに沿って操作すれば、約5分で翻訳字幕の表示を始められます！</p>
</div>

<div class="purpose-grid">
  <a href="#basic" class="purpose-card">
    <div class="purpose-icon">⚙️</div>
    <h3>基本設定をする</h3>
    <p>初めての設定手順</p>
  </a>
  <a href="#obs" class="purpose-card">
    <div class="purpose-icon">🎬</div>
    <h3>配信で使う</h3>
    <p>OBSなどへの取り込み方</p>
  </a>
  <a href="#faq" class="purpose-card">
    <div class="purpose-icon">❓</div>
    <h3>困ったときは</h3>
    <p>トラブルシューティング</p>
  </a>
</div>

## 基本設定（たった6ステップ） { #basic }

!!! tip "はじめての設定の案内を使うと、もっと簡単です"
    上のタブ **ホーム** → **はじめての設定** の 3 ステップの案内に沿うと、ステップ2〜6 をまとめて設定できます。→ [はじめての設定](cs_startup.md)

### ステップ1：画面の見かた

<div class="step-guide">
  <div class="step-item">
    <h3>上のタブを左から順に設定します</h3>
    <p>ゆかコネNEO の設定は、画面上部のタブ（ホーム／操作パネル／音声と翻訳／字幕デザイン／プラグイン…）から開きます。タブを選ぶと、左にそのタブの中の画面が並びます。</p>
    <img src="../images/cs_en_p8.png" alt="上のタブ">
  </div>
</div>

### ステップ2：あなたの話す言語を設定する

<div class="step-guide">
  <div class="step-item">
    <h3>母国語を設定</h3>
    <p>上のタブ <strong>音声と翻訳</strong> → <strong>話す言語と名前</strong> で、あなたが話す言語（この例では日本語）を選びます。名前は字幕に出す名前です。</p>
    <img src="../images/cs_en_p1.png" alt="話す言語と名前">
  </div>
</div>

### ステップ3：字幕のデザインを選ぶ

<div class="step-guide">
  <div class="step-item">
    <h3>字幕の表示方法を選ぶ</h3>
    <p>上のタブ <strong>字幕デザイン</strong> → <strong>デザイン</strong> の下の一覧から、テンプレートのタイルを押して選びます。「多言語」の分類が一番おすすめです（原文と翻訳を両方表示）。上のプレビューで見え方を確かめられ、「ランダム送信」で見本の字幕を流せます。</p>
    <img src="../images/cs_en_p2.png" alt="字幕デザイン">
    <div class="tips-box">
      <h4>デザイン選びのポイント</h4>
      <ul>
        <li>「多言語」：原文と翻訳を両方表示（最もおすすめ）</li>
        <li>「リスト」：過去の字幕も含めて表示したい場合</li>
        <li>「１行レイアウト」：シンプルにコンパクト表示したい場合</li>
      </ul>
      <p>テンプレートの一覧は <a href="../../startup/startup_layout/">レイアウト</a> にあります。</p>
    </div>
  </div>
</div>

### ステップ4：翻訳設定をする

<div class="step-guide">
  <div class="step-item">
    <h3>翻訳先の言語と翻訳エンジンを選ぶ</h3>
    <p>上のタブ <strong>音声と翻訳</strong> → <strong>翻訳する言語</strong> で、翻訳1 を英語、エンジンを無料の共用翻訳にします。</p>
    <img src="../images/cs_en_p3.png" alt="翻訳設定">
    <table>
      <tr><th>設定項目</th><th>設定値</th></tr>
      <tr><td>翻訳 1（言語）</td><td>17:英語/English(en-US)</td></tr>
      <tr><td>翻訳 1（エンジン）</td><td>共用翻訳(m2m100/無料)</td></tr>
    </table>
  </div>
</div>

### ステップ5：音声認識の種類を選ぶ

<div class="step-guide">
  <div class="step-item">
    <h3>「ブラウザ音声認識(Chrome)」が最も簡単です</h3>
    <p>上のタブ <strong>音声と翻訳</strong> → <strong>音声の入れ方</strong> で、<strong>ブラウザ音声認識(Chrome)</strong> のスイッチを ON にします。</p>
    <img src="../images/cs_en_p4.png" alt="音声の入れ方">
  </div>
</div>

### ステップ6：音声認識を開始する

<div class="step-guide">
  <div class="step-item">
    <h3>「認識用画面を開く」を押します</h3>
    <p>同じ画面のいちばん上の <strong>認識用画面を開く</strong> を押すと、音声認識のブラウザが開きます。</p>
    <img src="../images/cs_en_p5.png" alt="認識用画面を開く">
  </div>
</div>

<div class="step-guide">
  <div class="step-item">
    <h3>ブラウザでStartをクリック</h3>
    <p>音声認識ブラウザが開いたら「Start」をクリックします</p>
    <img src="../images/cs_en_p6.png" alt="ブラウザStart">
    <div class="tips-box">
      <h4>マイク許可について</h4>
      <p>初めて使う場合は「マイクへのアクセスを許可しますか？」という確認が表示されます。必ず「許可する」を選んでください。</p>
    </div>
  </div>
</div>

## 配信ソフトでの取り込み方 { #obs }

字幕を配信画面に表示するには、以下の2つの方法があります：

<div class="step-guide">
  <div class="step-item">
    <h3>方法1：ドラッグ＆ドロップ（簡単）</h3>
    <p>字幕デザインのタイル、または「OBSへ」ボタンを配信ソフトの画面にドラッグする方法</p>
    <ol>
      <li>上のタブ <strong>字幕デザイン</strong> → <strong>デザイン</strong> の一覧で使うテンプレートのタイルを（または <strong>配信ソフトへ</strong> の画面の <strong>OBSへ</strong> を）クリックしたまま</li>
      <li>OBSの画面までドラッグして</li>
      <li>配置したい場所でマウスを離します</li>
    </ol>
  </div>
  
  <div class="step-item">
    <h3>方法2：ウィンドウキャプチャ（確実）</h3>
    <p>OBSなどのウィンドウキャプチャ機能を使う方法</p>
    <ol>
      <li>OBSで「ソースの追加」→「ウィンドウキャプチャ」を選択</li>
      <li>「ウィンドウ」の欄から字幕ウィンドウを選択</li>
      <li>必要に応じて「色域」で背景色の透明化を設定</li>
    </ol>
    <a href="../cs_import_obs/" class="md-button">詳しい取り込み方法を見る</a>
  </div>
</div>

## よくある質問 { #faq }

<div class="tips-box">
  <h4>音声がうまく認識されない</h4>
  <p>音声認識画面で「onSound」という行に「@」マークが表示されない場合は、マイクがうまく認識されていません。</p>
  <ul>
    <li>ブラウザのマイク許可設定を確認</li>
    <li>マイクのミュートが解除されているか確認</li>
    <li>Windowsの設定でマイクがデフォルトデバイスになっているか確認</li>
  </ul>
  <a href="../../startup/startup_asr/" class="md-button">音声認識のトラブルシューティング</a>
</div>

<div class="tips-box">
  <h4>翻訳の精度を上げたい</h4>
  <p>無料の共用翻訳エンジンでも十分使えますが、より高精度な翻訳をご希望の場合は支援版をお試しください。</p>
  <a href="../cs_en_sp/" class="md-button">支援版の設定方法を見る</a>
</div>

<div class="purpose-grid">
  <a href="../../cs/cs_obs/" class="purpose-card">
    <div class="purpose-icon">📺</div>
    <h3>OBSでもっときれいに表示したい</h3>
    <p>OBSでの高度な設定方法</p>
  </a>
  <a href="../../qa/troubleshooting/" class="purpose-card">
    <div class="purpose-icon">🔧</div>
    <h3>他に問題が発生した場合</h3>
    <p>一般的なトラブルシューティング</p>
  </a>
</div>
