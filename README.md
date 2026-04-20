# -<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>本日の1枚｜狐魂。こだま式</title>
<style>
  :root {
    --gold: #c9963a;
    --gold-light: #e8c97a;
    --cream: #f5efe3;
    --deep: #1a1108;
    --card-bg: rgba(255,255,255,0.03);
    --muted: rgba(245,239,227,0.55);
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    background: var(--deep);
    color: var(--cream);
    font-family: 'Hiragino Mincho ProN', 'Yu Mincho', serif;
    min-height: 100vh;
    padding: 40px 16px 80px;
  }
  .wrap { max-width: 680px; margin: 0 auto; }

  /* Header */
  .header { text-align: center; margin-bottom: 40px; }
  .header-sub { font-size: 10px; letter-spacing: 0.4em; color: var(--gold); opacity: 0.8; margin-bottom: 10px; font-family: Arial, sans-serif; }
  .header-title { font-size: 36px; letter-spacing: 0.12em; font-weight: 900; }
  .header-title span { color: var(--gold); }
  .header-line { width: 80px; height: 1px; background: linear-gradient(90deg,transparent,var(--gold),transparent); margin: 14px auto; }
  .header-desc { font-size: 12px; color: var(--muted); letter-spacing: 0.1em; }

  /* Button */
  .btn-wrap { text-align: center; margin-bottom: 40px; }
  .draw-btn {
    background: none; border: 1px solid var(--gold); color: var(--gold-light);
    font-size: 16px; letter-spacing: 0.2em; padding: 16px 48px;
    cursor: pointer; font-family: inherit;
  }
  .draw-btn:active { opacity: 0.7; }
  .redraw-btn {
    display: none; background: none; border: none; color: var(--muted);
    font-size: 12px; cursor: pointer; text-decoration: underline;
    margin-top: 12px; font-family: inherit;
  }

  /* Result */
  #result { display: none; }

  /* Card header */
  .card-head {
    text-align: center; border: 1px solid rgba(201,150,58,0.25);
    padding: 26px 20px; margin-bottom: 20px;
  }
  .card-num { font-size: 10px; letter-spacing: 0.4em; color: var(--gold); opacity: 0.7; margin-bottom: 6px; font-family: Arial, sans-serif; }
  .card-en { font-size: 12px; letter-spacing: 0.2em; color: var(--gold-light); margin-bottom: 8px; font-family: Arial, sans-serif; }
  .card-jp { font-size: 38px; font-weight: 900; letter-spacing: 0.08em; margin-bottom: 10px; }
  .card-deity { font-size: 18px; color: var(--gold); letter-spacing: 0.15em; }

  /* Sections */
  .section { margin-bottom: 14px; padding: 20px 22px; background: var(--card-bg); border-left: 2px solid var(--gold); }
  .sec-label { font-size: 10px; letter-spacing: 0.3em; color: var(--gold); margin-bottom: 4px; font-family: Arial, sans-serif; }
  .sec-title { font-size: 13px; font-weight: 600; color: var(--gold-light); margin-bottom: 10px; }
  .sec-text { font-size: 13px; line-height: 2; color: rgba(245,239,227,0.88); font-weight: 300; }
  .keywords { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 12px; }
  .kw { font-size: 11px; padding: 3px 10px; border: 1px solid rgba(201,150,58,0.35); color: var(--gold-light); }
  .oracle-text { font-size: 15px; line-height: 1.9; color: var(--cream); }

  /* Divider */
  .divider { display: flex; align-items: center; gap: 12px; margin: 20px 0; color: var(--gold); opacity: 0.45; font-size: 11px; font-family: Arial, sans-serif; }
  .divider-line { flex: 1; height: 1px; background: var(--gold); opacity: 0.3; }

  /* Posts */
  .posts { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  @media(max-width: 500px){ .posts { grid-template-columns: 1fr; } }
  .post-block { border: 1px solid rgba(201,150,58,0.2); padding: 16px; }
  .post-platform { font-size: 10px; letter-spacing: 0.3em; color: var(--gold); margin-bottom: 10px; font-family: Arial, sans-serif; }
  .post-text { font-size: 12px; line-height: 1.9; color: rgba(245,239,227,0.85); white-space: pre-wrap; font-weight: 300; margin-bottom: 12px; min-height: 120px; }
  .copy-btn {
    background: none; border: 1px solid rgba(201,150,58,0.35); color: var(--gold);
    font-size: 12px; padding: 7px 0; cursor: pointer; width: 100%;
    font-family: inherit; transition: all 0.3s;
  }
  .copy-btn.copied { border-color: #5a8a6a; color: #7da86e; }
</style>
</head>
<body>
<div class="wrap">

  <div class="header">
    <p class="header-sub">KODAMA-SHIKI × JAPANESE MYTHOLOGY</p>
    <h1 class="header-title">本日の<span>1枚</span></h1>
    <div class="header-line"></div>
    <p class="header-desc">日本神話 × 大アルカナ ｜ こだま式</p>
  </div>

  <div class="btn-wrap">
    <button class="draw-btn" onclick="drawCard()">✦ カードを引く ✦</button><br>
    <button class="redraw-btn" id="redrawBtn" onclick="drawCard()">引き直す</button>
  </div>

  <div id="result">
    <div class="card-head">
      <p class="card-num" id="cNum"></p>
      <p class="card-en" id="cEn"></p>
      <p class="card-jp" id="cJp"></p>
      <p class="card-deity" id="cDeity"></p>
    </div>
    <div class="section">
      <p class="sec-label">MYTHOLOGY</p>
      <p class="sec-title">⛩ 神話エピソード</p>
      <p class="sec-text" id="cMyth"></p>
    </div>
    <div class="section">
      <p class="sec-label">TAROT MEANING</p>
      <p class="sec-title">🃏 タロット的意味</p>
      <p class="sec-text" id="cTarot"></p>
      <div class="keywords" id="cKw"></div>
    </div>
    <div class="section">
      <p class="sec-label">ORACLE MESSAGE</p>
      <p class="sec-title">🌿 オラクルメッセージ</p>
      <p class="oracle-text" id="cOracle"></p>
    </div>
    <div class="divider"><div class="divider-line"></div>✦ SNS 投稿文 ✦<div class="divider-line"></div></div>
    <div class="posts">
      <div class="post-block">
        <p class="post-platform">Twitter / X</p>
        <p class="post-text" id="twText"></p>
        <button class="copy-btn" id="twBtn" onclick="copyPost('twText','twBtn')">コピーする</button>
      </div>
      <div class="post-block">
        <p class="post-platform">Instagram</p>
        <p class="post-text" id="igText"></p>
        <button class="copy-btn" id="igBtn" onclick="copyPost('igText','igBtn')">コピーする</button>
      </div>
    </div>
  </div>

</div>
<script>
const CARDS = [
  { num:"0", en:"The Fool", jp:"愚者", deity:"猿田彦",
    myth:"猿田彦は天孫降臨の際、先導役として現れた道案内の神。鼻高く神々しい姿で岐路に立ち、ニニギノミコトを正しき道へと導いた。知らない道を恐れず踏み出す者の傍らに、常に寄り添う神様です。",
    tarot:"新しい旅の始まり。「正しい準備が整ってから」ではなく、今この瞬間に一歩を踏み出すことで開ける道があります。純粋な好奇心と信頼が、あなたの羅針盤になります。",
    kw:["新出発","純粋さ","可能性","信頼"],
    oracle:"迷いは地図のない旅の証拠。でも地図のない旅だけが、まだ誰も見ていない景色へ連れていってくれます。" },
  { num:"I", en:"The Magician", jp:"魔術師", deity:"少彦名神",
    myth:"少彦名神は小さな体に無限の知恵を宿した神。大国主と共に国づくりを行い、医療・農業・酒造りの術を人々に授けた。持てる力を最大限に活かし、世界を変えた創造の神様です。",
    tarot:"今あなたの手元にある力・知識・人脈、それで十分です。「もっと揃ってから」ではなく、今持っているものを組み合わせることで道は拓けます。",
    kw:["創造力","行動","意志","技術"],
    oracle:"あなたはすでに必要なものを持っている。あとは使う勇気だけ。" },
  { num:"II", en:"The High Priestess", jp:"女教皇", deity:"豊受大神",
    myth:"豊受大神は伊勢の外宮に祀られる食と豊穣の神。天照大神の食事を司り、静かに、しかし確実に命を支え続けた。表には出ずとも、すべての根幹を担う深淵なる智慧の神様です。",
    tarot:"答えはすでにあなたの内側にあります。騒がしい外の声より、静かな自分の声に耳を傾ける時。直感と内なる知恵を信じてください。",
    kw:["直感","静けさ","内省","智慧"],
    oracle:"静かな水面こそ、深くまで見通せる。今日は答えを探すより、感じることを大切に。" },
  { num:"III", en:"The Empress", jp:"女帝", deity:"木花咲耶姫",
    myth:"木花咲耶姫は富士山の神であり、美と豊穣の象徴。炎の中で三柱の神を産んだ強さと、花のように咲き誇る美しさを併せ持つ。生命力と愛情の源泉となる神様です。",
    tarot:"豊かさ・愛情・創造のエネルギーに満ちた時。自分を慈しむことが、周りへの豊かさにも繋がります。今は受け取ることも大切にしてください。",
    kw:["豊穣","愛情","美","創造"],
    oracle:"花は急いで咲こうとしない。あなたの豊かさも、今まさに満ちていくところです。" },
  { num:"IV", en:"The Emperor", jp:"皇帝", deity:"大国主",
    myth:"大国主は出雲を中心に国を築いた神。数多の困難を乗り越え、仲間と共に地上の世界を整えた。寛大さと強さで人々を包む、大いなる秩序と慈悲の神様です。",
    tarot:"基盤を整える時。感情に流されず、地に足のついた判断が大切です。あなたの中の「軸」を確認することで、周りも安定していきます。",
    kw:["安定","基盤","秩序","リーダーシップ"],
    oracle:"揺るぎない根を持つ木は、どんな風にも折れない。今日は自分の軸を確かめる日。" },
  { num:"V", en:"The Hierophant", jp:"教皇", deity:"国常立神",
    myth:"国常立神は天地開闢の際に最初に現れた神。宇宙の根本原理そのものとされ、永遠の秩序と伝統を体現する。見えない法則を守り続ける、存在の根源となる神様です。",
    tarot:"先人の知恵や伝統の中に、今のあなたへのヒントがあります。一人で抱えるより、信頼できる誰かに相談することで道が開けることも。",
    kw:["伝統","知恵","指針","信頼"],
    oracle:"道に迷ったとき、古い地図が一番正確なこともある。温故知新の精神で。" },
  { num:"VI", en:"The Lovers", jp:"恋人", deity:"伊弉冉・伊弉諾",
    myth:"伊弉諾・伊弉冉の二柱は、天の浮き橋に立ち、矛で海をかき混ぜ国土を生んだ。愛と創造の原点となる神。別れと再会を経ても繋がり続ける、魂の絆の神様です。",
    tarot:"選択と繋がりの時。大切なのは「正しい選択」より「自分の心に正直な選択」。誰かとの関係も、まず自分自身との関係から始まります。",
    kw:["選択","絆","調和","心の声"],
    oracle:"本当の出会いは、自分自身と出会うところから始まる。" },
  { num:"VII", en:"The Chariot", jp:"戦車", deity:"建御雷",
    myth:"建御雷は雷神であり武神。大国主の国譲り交渉で毅然と役割を果たし、鹿島神宮に祀られる。迷いなく使命に向かう、勝利と前進のエネルギーを持つ神様です。",
    tarot:"前進のエネルギーが高まっています。迷いや葛藤を抱えたまま動いていい。すべてが整ってから動くのではなく、動きながら整えていく時です。",
    kw:["前進","勝利","意志","突破"],
    oracle:"嵐の中を進む者だけが、嵐の向こうの景色を知っている。" },
  { num:"VIII", en:"Strength", jp:"力", deity:"菊理媛",
    myth:"菊理媛は黄泉の国で伊弉諾と伊弉冉の仲を取り持ったとされる神。対立するものの間に立ち、静かに和解をもたらす。真の強さは包容力にあることを示す神様です。",
    tarot:"力とは押さえつけることではなく、受け入れること。今感じている感情や葛藤を否定せず、ただそこに寄り添う優しさが、最も強い力になります。",
    kw:["包容力","柔らかな強さ","受容","調和"],
    oracle:"真の強さは、やわらかさの中にある。今日は力むより、ゆるめてみて。" },
  { num:"IX", en:"The Hermit", jp:"隠者", deity:"思金神",
    myth:"思金神は天の岩戸神話で知恵を授けた神。騒がしい神々の中で一人静かに考え、天照大神を岩戸から導き出す策を生み出した。深く考えることの力を示す智慧の神様です。",
    tarot:"今は内側に光を向ける時。一人でいることは孤独ではなく、自分と深く向き合うための贈り物。静かな時間の中にこそ、次への答えがあります。",
    kw:["内省","静寂","智慧","探求"],
    oracle:"答えは外にあるのではなく、静かにした時にだけ聞こえる内なる声の中に。" },
  { num:"X", en:"Wheel of Fortune", jp:"運命の輪", deity:"保食神",
    myth:"保食神は食物を生み出す神として循環の象徴。その死から五穀が生まれたという神話は、終わりが新たな命の始まりであることを示す。巡りゆく命のサイクルの神様です。",
    tarot:"流れが変わるタイミング。今がうまくいかなくても、それは次の流れへの準備期間。すべては巡っています。変化に抵抗するより、波に乗る感覚を持って。",
    kw:["循環","転機","流れ","変化"],
    oracle:"季節が変わるように、あなたの流れも今まさに動き始めている。" },
  { num:"XI", en:"Justice", jp:"正義", deity:"瀬織津姫",
    myth:"瀬織津姫は祓いと浄化の女神。人々の罪や穢れを川から海へと流し去る。曇りなき目で物事の本質を見極め、清廉な流れを取り戻させる、清めの神様です。",
    tarot:"今こそ正直に自分を見つめる時。都合の良い解釈より、真実を見る勇気が次の扉を開けます。行動と結果は必ず繋がっています。",
    kw:["誠実さ","清明","均衡","真実"],
    oracle:"濁りを流せば、本来の清らかさが戻ってくる。今日は何かを手放す日かもしれない。" },
  { num:"XII", en:"The Hanged Man", jp:"吊るされた男", deity:"天若日子",
    myth:"天若日子は天上の使いとして地上に降りたが、地上の生に惹かれ使命を忘れた神。その死は天地に嘆かれた。立ち止まることで初めて見える大切なものがあることを示す神様です。",
    tarot:"今は動かずにいることが正解かもしれません。焦らず、ただ今の状況を違う角度から眺めてみて。視点を変えることで、見えなかったものが見えてきます。",
    kw:["停止","視点転換","待機","気づき"],
    oracle:"立ち止まることは、後退ではない。今だけ見える景色がある。" },
  { num:"XIII", en:"Death", jp:"死神", deity:"黄泉津大神",
    myth:"黄泉津大神は黄泉の国を支配する神。伊弉冉が黄泉へ渡った後に得た名。終わりを司ることで、新たな始まりを生む根源的な力を持つ、変容と再生の神様です。",
    tarot:"何かが終わろうとしています。でもそれは消えるのではなく、変容すること。手放すことへの恐れより、その先に来るものへの期待を少しだけ持ってみて。",
    kw:["終焉","変容","再生","手放す"],
    oracle:"冬が終わらなければ、春は来ない。今はその冬の中にいるあなたへ。" },
  { num:"XIV", en:"Temperance", jp:"節制", deity:"下照姫",
    myth:"下照姫は天若日子の妻となった優しき神。夫の死を嘆き泣き続けた声が天まで届いたという。感情を抑えるのではなく、その深さをそのまま生きた、調和と感受性の神様です。",
    tarot:"バランスを取り直す時。急ぎすぎず、かといって立ち止まりすぎず。今の流れの中でできることを、丁寧に一つずつ積み重ねていきましょう。",
    kw:["調和","バランス","丁寧さ","統合"],
    oracle:"急いで混ぜると濁る。ゆっくり注ぐことで、美しくブレンドされていく。" },
  { num:"XV", en:"The Devil", jp:"悪魔", deity:"金山姫",
    myth:"金山姫は鉱山・金属を司る神。鉱石は地の底深くに眠り、取り出すには困難を要する。執着や欲望の奥底に眠る本質的な価値を示す、変容の力を持つ神様です。",
    tarot:"何かに縛られていると感じているなら、その鎖は思ったより薄いかもしれません。執着の正体を見つめることで、解放への扉が見えてきます。",
    kw:["執着","解放","直視","本質"],
    oracle:"縛っているのは鎖じゃなくて、鎖があると思い込んでいる自分かもしれない。" },
  { num:"XVI", en:"The Tower", jp:"塔", deity:"火之迦具土神",
    myth:"火之迦具土神は伊弉冉が産んだ火の神。その誕生が母神の命を奪い、父神の怒りを招いた。しかしその火こそが文明と変革をもたらす力の源。破壊から創造が生まれる神様です。",
    tarot:"突然の変化や崩壊に見えることも、実は必要な更新かもしれません。無くなるものは、もともと本質ではなかったもの。残るものの中にこそ、本当のあなたがあります。",
    kw:["崩壊","解放","更新","本質"],
    oracle:"燃え尽きた後の灰が、最も肥えた土になる。" },
  { num:"XVII", en:"The Star", jp:"星", deity:"天之水分神",
    myth:"天之水分神は水を分け与える神。山から流れる清水を司り、すべての命に恵みを注ぐ。枯れることなく湧き続ける希望の源泉として、静かに世界を潤す神様です。",
    tarot:"希望と回復のエネルギー。つらい時期を越えた後の、静かな光。今は自分を責めず、ただ休むことも、前進することの一つです。",
    kw:["希望","回復","浄化","信頼"],
    oracle:"星は嵐の夜も、雲の向こうで輝き続けている。" },
  { num:"XVIII", en:"The Moon", jp:"月", deity:"月読命",
    myth:"月読命は天照大神の弟神であり、夜の世界を統べる神。月の満ち欠けのように、表と裏、見えるものと見えないものを司る。不確かさの中に宿る神秘の神様です。",
    tarot:"今は物事がはっきりしない、霧の中にいるような感覚かもしれません。答えを急がなくていい。月は満ちたり欠けたりしながら、それでも確かに存在しています。",
    kw:["不確かさ","直感","神秘","潜在意識"],
    oracle:"見えないからといって、ないわけじゃない。今夜は感じる力を信じて。" },
  { num:"XIX", en:"The Sun", jp:"太陽", deity:"天照大神",
    myth:"天照大神は太陽を司る最高神。岩戸に隠れた時、世界は闇に包まれた。しかし再び現れた時、すべての命に光が戻った。存在そのものが恵みである、光と生命の神様です。",
    tarot:"明るく、力強いエネルギーの時。あなたの持つ光を隠さないで。自分らしさを表現することが、周りへの最高の贈り物になります。",
    kw:["喜び","輝き","自己表現","活力"],
    oracle:"太陽は誰かのために輝くのではなく、ただ輝くことで世界を照らす。" },
  { num:"XX", en:"Judgement", jp:"審判", deity:"神武天皇",
    myth:"神武天皇は日向から東征し、大和に初めての国家を築いた初代天皇。使命を自覚し、長い旅を経て新たな時代を開いた。覚醒と新時代の幕開けを体現する神様です。",
    tarot:"魂の覚醒と召命の時。「自分はこう生きたい」という声が聞こえているなら、今がその声に従う時かもしれません。過去を清算し、新たなステージへ。",
    kw:["覚醒","召命","再生","新時代"],
    oracle:"内側から聞こえる声は、あなた自身の神様からのメッセージかもしれない。" },
  { num:"XXI", en:"The World", jp:"世界", deity:"玉依姫",
    myth:"玉依姫は海神の娘であり、初代天皇の母となった神。天と地、海と陸を繋ぎ、新たな命を宿す統合の象徴。すべてが繋がり、満ちていく完成の神様です。",
    tarot:"一つのサイクルが完成に向かっています。達成・統合・充実のエネルギー。ここまで歩いてきた道のりを、どうか誇りに思ってください。",
    kw:["完成","統合","充実","達成"],
    oracle:"終わりは始まりの形をしている。あなたはすでに、次の旅の入り口に立っている。" },
];

function drawCard() {
  const c = CARDS[Math.floor(Math.random() * CARDS.length)];

  document.getElementById('cNum').textContent = 'Arcana ' + c.num;
  document.getElementById('cEn').textContent = c.en;
  document.getElementById('cJp').textContent = c.jp;
  document.getElementById('cDeity').textContent = c.deity;
  document.getElementById('cMyth').textContent = c.myth;
  document.getElementById('cTarot').textContent = c.tarot;
  document.getElementById('cOracle').textContent = '「' + c.oracle + '」';

  const kwEl = document.getElementById('cKw');
  kwEl.innerHTML = '';
  c.kw.forEach(k => {
    const s = document.createElement('span');
    s.className = 'kw';
    s.textContent = k;
    kwEl.appendChild(s);
  });

  const tw = `#おはようVライバー\n🦊神秘と共に歩み、魂を導く狐🦊\n\n【本日の1枚】✨\n${c.jp}（${c.deity}）\n\n${c.oracle}\n\n#日本神話 #神言御札`;
  const ig = `【本日の1枚 ✨】\n${c.jp}（${c.deity}）\n\n⛩ 神話より\n${c.myth}\n\n🃏 今日のメッセージ\n${c.tarot}\n\n🌿 あなたへの問い\n今日、あなたが手放せるものはなんですか？\n\n「${c.oracle}」\n\n─────────────────\n#日本神話 #神言御札 #オリジナルカード`;

  document.getElementById('twText').textContent = tw;
  document.getElementById('igText').textContent = ig;

  document.getElementById('result').style.display = 'block';
  document.getElementById('redrawBtn').style.display = 'inline-block';

  // reset copy buttons
  ['twBtn','igBtn'].forEach(id => {
    const b = document.getElementById(id);
    b.textContent = 'コピーする';
    b.classList.remove('copied');
  });
}

function copyPost(textId, btnId) {
  const text = document.getElementById(textId).textContent;
  navigator.clipboard.writeText(text).then(() => {
    const btn = document.getElementById(btnId);
    btn.textContent = '✓ コピーしました';
    btn.classList.add('copied');
    setTimeout(() => {
      btn.textContent = 'コピーする';
      btn.classList.remove('copied');
    }, 2000);
  });
}
</script>
</body>
</html>
