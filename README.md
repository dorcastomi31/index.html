<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Disney: From Mouse House to Corporate Kingdom</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #C9A84C;
    --gold-light: #E8C97A;
    --dark: #0A0A0F;
    --dark-2: #12121A;
    --dark-3: #1C1C28;
    --accent: #4A90D9;
    --accent-2: #E8553E;
    --green: #2ECC71;
    --text: #F0EDE8;
    --text-muted: #9A9490;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #000;
    font-family: 'DM Sans', sans-serif;
    color: var(--text);
  }

  /* ===================== SCREEN MODE ===================== */
  @media screen {
    body { overflow: hidden; height: 100vh; width: 100vw; }

    .presentation { width: 100vw; height: 100vh; position: relative; }

    .slide {
      position: absolute;
      inset: 0;
      display: none;
      padding: 52px 72px;
      opacity: 0;
      transition: opacity 0.4s ease;
      overflow: hidden;
    }

    .slide.active { display: flex; flex-direction: column; opacity: 1; }

    .nav {
      position: fixed;
      bottom: 28px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      align-items: center;
      gap: 20px;
      background: rgba(255,255,255,0.06);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255,255,255,0.1);
      padding: 10px 24px;
      border-radius: 50px;
      z-index: 999;
    }

    .progress-bar {
      position: fixed;
      top: 0; left: 0;
      height: 3px;
      background: linear-gradient(90deg, var(--gold), var(--gold-light));
      transition: width 0.4s ease;
      z-index: 1000;
    }

    .key-hint {
      position: fixed;
      top: 16px; right: 20px;
      font-size: 11px;
      color: rgba(255,255,255,0.18);
      letter-spacing: 1px;
      z-index: 999;
    }

    .print-btn {
      position: fixed;
      top: 12px; left: 20px;
      background: rgba(201,168,76,0.15);
      border: 1px solid rgba(201,168,76,0.3);
      color: var(--gold);
      font-size: 12px;
      letter-spacing: 1px;
      padding: 8px 16px;
      border-radius: 20px;
      cursor: pointer;
      font-family: 'DM Sans', sans-serif;
      z-index: 999;
      transition: all 0.2s;
    }
    .print-btn:hover { background: rgba(201,168,76,0.25); }
  }

  /* ===================== PRINT MODE ===================== */
  @media print {
    @page { size: A4 landscape; margin: 0; }

    body { background: #000; overflow: visible; height: auto; }

    .presentation { width: auto; height: auto; position: static; }

    .slide {
      display: flex !important;
      flex-direction: column;
      opacity: 1 !important;
      position: relative;
      width: 297mm;
      height: 210mm;
      padding: 36px 56px;
      page-break-after: always;
      page-break-inside: avoid;
      overflow: hidden;
    }

    .nav, .progress-bar, .key-hint, .print-btn { display: none !important; }
  }

  /* ===================== SHARED STYLES ===================== */
  .nav button {
    background: none; border: none;
    color: var(--text-muted);
    font-size: 18px; cursor: pointer;
    padding: 4px 10px; border-radius: 20px;
    transition: all 0.2s;
    font-family: 'DM Sans', sans-serif;
  }
  .nav button:hover { color: var(--gold); background: rgba(201,168,76,0.1); }
  .slide-counter { font-size: 12px; color: var(--text-muted); letter-spacing: 2px; }
  .dot-nav { display: flex; gap: 5px; }
  .dot { width: 5px; height: 5px; border-radius: 50%; background: var(--text-muted); cursor: pointer; transition: all 0.3s; }
  .dot.active { background: var(--gold); width: 16px; border-radius: 3px; }

  .bg-circle {
    position: absolute; border-radius: 50%;
    filter: blur(80px); pointer-events: none;
  }

  .label-tag {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(201,168,76,0.12);
    border: 1px solid rgba(201,168,76,0.3);
    color: var(--gold);
    font-size: 10px; letter-spacing: 3px; text-transform: uppercase;
    padding: 5px 14px; border-radius: 4px;
    margin-bottom: 18px; width: fit-content;
  }

  .gold-line { width: 50px; height: 3px; background: linear-gradient(90deg, var(--gold), transparent); margin: 14px 0; }

  /* ===================== SLIDE BACKGROUNDS ===================== */
  .s-dark { background: var(--dark); }
  .s-dark2 { background: var(--dark-2); }

  /* ===================== SLIDE 1: TITLE ===================== */
  #slide-1 { justify-content: center; align-items: flex-start; }
  #slide-1 .bg-circle.c1 { width: 500px; height: 500px; background: rgba(201,168,76,0.08); right: -80px; top: -80px; }
  #slide-1 .bg-circle.c2 { width: 350px; height: 350px; background: rgba(74,144,217,0.05); left: -40px; bottom: -40px; }
  #slide-1 .big-year { position: absolute; right: 60px; top: 50%; transform: translateY(-50%); font-family: 'Playfair Display', serif; font-size: 180px; font-weight: 900; color: rgba(201,168,76,0.04); line-height: 1; pointer-events: none; user-select: none; }
  #slide-1 .castle { font-size: 44px; margin-bottom: 16px; display: block; }
  #slide-1 h1 { font-family: 'Playfair Display', serif; font-size: 58px; font-weight: 900; line-height: 1.05; max-width: 620px; }
  #slide-1 h1 span { color: var(--gold); }
  #slide-1 .subtitle { font-size: 15px; color: var(--text-muted); margin-top: 16px; line-height: 1.6; max-width: 480px; }
  #slide-1 .presenter { margin-top: 32px; display: flex; align-items: center; gap: 12px; }
  #slide-1 .presenter .line { width: 32px; height: 1px; background: var(--gold); }
  #slide-1 .presenter span { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--text-muted); }
  #slide-1 .stats-row { position: absolute; bottom: 72px; left: 72px; right: 72px; display: flex; gap: 36px; }
  #slide-1 .stat { border-left: 2px solid var(--gold); padding-left: 12px; }
  #slide-1 .stat .num { font-family: 'Playfair Display', serif; font-size: 26px; font-weight: 700; color: var(--gold); }
  #slide-1 .stat .desc { font-size: 11px; color: var(--text-muted); margin-top: 2px; }

  /* ===================== SLIDE 2: AGENDA ===================== */
  #slide-2 h2 { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; }
  #slide-2 .bg-circle.c1 { width: 400px; height: 400px; background: rgba(74,144,217,0.05); right: -80px; bottom: -80px; }
  .agenda-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-top: 24px; flex: 1; }
  .agenda-item { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 10px; padding: 20px 24px; display: flex; gap: 16px; align-items: flex-start; }
  .agenda-num { font-family: 'Playfair Display', serif; font-size: 30px; font-weight: 900; color: rgba(201,168,76,0.18); line-height: 1; min-width: 36px; }
  .agenda-text h3 { font-size: 14px; font-weight: 600; margin-bottom: 5px; }
  .agenda-text p { font-size: 12px; color: var(--text-muted); line-height: 1.5; }

  /* ===================== SLIDE 3: CRISIS ===================== */
  #slide-3 .bg-circle.c1 { width: 500px; height: 500px; background: rgba(232,85,62,0.06); right: -100px; top: -100px; }
  #slide-3 h2 { font-family: 'Playfair Display', serif; font-size: 42px; font-weight: 700; line-height: 1.1; }
  #slide-3 h2 em { color: var(--accent-2); font-style: normal; }
  .split { display: grid; grid-template-columns: 1fr 1fr; gap: 48px; flex: 1; margin-top: 24px; }
  .crisis-stats { display: flex; flex-direction: column; gap: 12px; margin-top: 20px; }
  .crisis-stat { display: flex; align-items: center; gap: 12px; padding: 12px 16px; background: rgba(232,85,62,0.07); border-left: 3px solid var(--accent-2); border-radius: 0 8px 8px 0; }
  .crisis-stat .icon { font-size: 20px; }
  .crisis-stat .text { font-size: 12px; color: var(--text-muted); line-height: 1.4; }
  .crisis-stat .text strong { color: var(--text); display: block; font-size: 13px; margin-bottom: 2px; }
  .timeline-item { display: flex; gap: 16px; align-items: flex-start; position: relative; margin-bottom: 16px; }
  .timeline-item::before { content: ''; position: absolute; left: 15px; top: 32px; bottom: -16px; width: 1px; background: rgba(255,255,255,0.07); }
  .timeline-item:last-child::before { display: none; }
  .tl-dot { width: 32px; height: 32px; border-radius: 50%; background: var(--dark-3); border: 1px solid rgba(255,255,255,0.1); display: flex; align-items: center; justify-content: center; font-size: 13px; flex-shrink: 0; }
  .tl-year { font-size: 10px; letter-spacing: 2px; color: var(--gold); text-transform: uppercase; margin-bottom: 3px; }
  .tl-text { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
  .tl-text strong { color: var(--text); }

  /* ===================== SLIDE 4: SYNERGY ===================== */
  #slide-4 { align-items: center; }
  #slide-4 .bg-circle.c1 { width: 600px; height: 600px; background: rgba(201,168,76,0.05); left: 50%; top: 50%; transform: translate(-50%, -50%); }
  #slide-4 .top { text-align: center; width: 100%; margin-bottom: 20px; }
  #slide-4 h2 { font-family: 'Playfair Display', serif; font-size: 44px; font-weight: 900; }
  #slide-4 h2 span { color: var(--gold); }
  #slide-4 .quote { font-size: 16px; color: var(--text-muted); font-style: italic; font-family: 'Playfair Display', serif; margin-top: 8px; }
  #slide-4 .quote em { color: var(--gold); font-style: normal; font-weight: 700; }
  .synergy-wheel { width: 100%; flex: 1; display: flex; align-items: center; justify-content: center; position: relative; }
  .wheel-center { width: 110px; height: 110px; border-radius: 50%; background: linear-gradient(135deg, var(--gold), #8B6914); display: flex; align-items: center; justify-content: center; flex-direction: column; z-index: 10; box-shadow: 0 0 50px rgba(201,168,76,0.3); }
  .wheel-center .big-icon { font-size: 30px; }
  .wheel-center .label { font-size: 9px; letter-spacing: 2px; text-transform: uppercase; color: var(--dark); font-weight: 700; margin-top: 3px; }
  .spoke-item { position: absolute; display: flex; flex-direction: column; align-items: center; gap: 8px; }
  .spoke-circle { width: 68px; height: 68px; border-radius: 50%; background: var(--dark-3); border: 1px solid rgba(201,168,76,0.25); display: flex; flex-direction: column; align-items: center; justify-content: center; font-size: 20px; }
  .spoke-label { font-size: 11px; color: var(--text-muted); text-align: center; }
  .spoke-item.top { top: 10px; left: 50%; transform: translateX(-50%); }
  .spoke-item.right { right: 40px; top: 50%; transform: translateY(-50%); }
  .spoke-item.bottom { bottom: 10px; left: 50%; transform: translateX(-50%); }
  .spoke-item.left { left: 40px; top: 50%; transform: translateY(-50%); }
  .spoke-item.top-right { top: 40px; right: 120px; }
  .spoke-item.bottom-left { bottom: 40px; left: 120px; }

  /* ===================== SLIDE 5: ALADDIN ===================== */
  #slide-5 .bg-circle.c1 { width: 400px; height: 400px; background: rgba(74,144,217,0.05); left: -60px; bottom: -60px; }
  #slide-5 h2 { font-family: 'Playfair Display', serif; font-size: 36px; font-weight: 700; }
  #slide-5 h2 em { color: var(--gold); font-style: italic; }
  .aladdin-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-top: 20px; flex: 1; }
  .aladdin-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 10px; padding: 16px; }
  .aladdin-card .card-icon { font-size: 22px; margin-bottom: 8px; display: block; }
  .aladdin-card .card-title { font-size: 11px; font-weight: 600; letter-spacing: 1px; text-transform: uppercase; color: var(--gold); margin-bottom: 8px; }
  .aladdin-card .card-items { list-style: none; }
  .aladdin-card .card-items li { font-size: 11px; color: var(--text-muted); padding: 3px 0 3px 10px; border-bottom: 1px solid rgba(255,255,255,0.04); position: relative; line-height: 1.4; }
  .aladdin-card .card-items li::before { content: '→'; position: absolute; left: 0; color: var(--gold); font-size: 9px; }
  .aladdin-result { margin-top: 14px; padding: 14px 20px; background: linear-gradient(135deg, rgba(201,168,76,0.1), rgba(201,168,76,0.04)); border: 1px solid rgba(201,168,76,0.25); border-radius: 10px; display: flex; align-items: center; justify-content: space-between; }
  .aladdin-result .result-text { font-size: 12px; color: var(--text-muted); }
  .aladdin-result .result-text strong { color: var(--text); font-size: 13px; }
  .result-numbers { display: flex; gap: 24px; }
  .result-num { text-align: center; }
  .result-num .big { font-family: 'Playfair Display', serif; font-size: 22px; font-weight: 700; color: var(--gold); }
  .result-num .small { font-size: 10px; color: var(--text-muted); }

  /* ===================== SLIDE 6: EISNER RISE ===================== */
  #slide-6 .bg-circle.c1 { width: 400px; height: 400px; background: rgba(201,168,76,0.05); right: -60px; top: -60px; }
  #slide-6 h2 { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; }
  #slide-6 h2 span { color: var(--gold); }
  .wins-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-top: 20px; }
  .win-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 10px; padding: 18px 16px; text-align: center; }
  .win-card .win-icon { font-size: 26px; margin-bottom: 8px; }
  .win-card .win-num { font-family: 'Playfair Display', serif; font-size: 20px; font-weight: 700; color: var(--gold); margin-bottom: 5px; }
  .win-card .win-label { font-size: 11px; color: var(--text-muted); line-height: 1.4; }
  .revenue-bar-section { margin-top: 20px; flex: 1; }
  .revenue-bar-section h3 { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--text-muted); margin-bottom: 12px; }
  .bar-row { display: flex; align-items: center; gap: 12px; margin-bottom: 9px; }
  .bar-year { font-size: 12px; color: var(--text-muted); width: 36px; flex-shrink: 0; }
  .bar-track { flex: 1; height: 8px; background: rgba(255,255,255,0.06); border-radius: 4px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 4px; background: linear-gradient(90deg, var(--gold), var(--gold-light)); }
  .bar-val { font-size: 12px; color: var(--gold); width: 68px; flex-shrink: 0; font-family: 'Playfair Display', serif; }

  /* ===================== SLIDE 7: EISNER FALL ===================== */
  #slide-7 .bg-circle.c1 { width: 500px; height: 500px; background: rgba(232,85,62,0.05); right: -80px; bottom: -80px; }
  #slide-7 h2 { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; }
  #slide-7 h2 span { color: var(--accent-2); }
  .fall-layout { display: grid; grid-template-columns: 1.2fr 1fr; gap: 40px; flex: 1; margin-top: 20px; }
  .fall-list { display: flex; flex-direction: column; gap: 10px; }
  .fall-item { display: flex; gap: 12px; align-items: flex-start; padding: 12px 14px; background: rgba(232,85,62,0.05); border: 1px solid rgba(232,85,62,0.1); border-radius: 8px; }
  .fall-item .fi-icon { font-size: 18px; flex-shrink: 0; }
  .fall-item .fi-text { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
  .fall-item .fi-text strong { color: var(--text); display: block; margin-bottom: 2px; font-size: 13px; }
  .fall-right { display: flex; flex-direction: column; justify-content: center; gap: 20px; }
  .big-metric { text-align: center; padding: 24px; background: rgba(232,85,62,0.07); border: 1px solid rgba(232,85,62,0.2); border-radius: 14px; }
  .big-metric .bm-icon { font-size: 30px; margin-bottom: 6px; }
  .big-metric .bm-num { font-family: 'Playfair Display', serif; font-size: 48px; font-weight: 900; color: var(--accent-2); line-height: 1; }
  .big-metric .bm-label { font-size: 12px; color: var(--text-muted); margin-top: 6px; }
  .verdict-box { padding: 16px 20px; background: rgba(255,255,255,0.03); border-left: 3px solid var(--gold); border-radius: 0 8px 8px 0; }
  .verdict-box p { font-size: 13px; color: var(--text-muted); line-height: 1.6; font-style: italic; font-family: 'Playfair Display', serif; }
  .verdict-box p em { color: var(--gold); font-style: normal; }

  /* ===================== SLIDE 8: IGER ACQUISITIONS ===================== */
  #slide-8 .bg-circle.c1 { width: 400px; height: 400px; background: rgba(74,144,217,0.05); left: -40px; top: -40px; }
  #slide-8 h2 { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; }
  #slide-8 h2 span { color: var(--accent); }
  .acq-cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-top: 20px; flex: 1; }
  .acq-card { border-radius: 14px; padding: 24px 20px; display: flex; flex-direction: column; gap: 12px; }
  .acq-card.pixar { background: linear-gradient(135deg, rgba(74,144,217,0.1), rgba(74,144,217,0.03)); border: 1px solid rgba(74,144,217,0.22); }
  .acq-card.marvel { background: linear-gradient(135deg, rgba(232,85,62,0.1), rgba(232,85,62,0.03)); border: 1px solid rgba(232,85,62,0.22); }
  .acq-card.star-wars { background: linear-gradient(135deg, rgba(201,168,76,0.1), rgba(201,168,76,0.03)); border: 1px solid rgba(201,168,76,0.22); }
  .acq-icon { font-size: 32px; }
  .acq-year { font-size: 10px; letter-spacing: 2px; text-transform: uppercase; color: var(--text-muted); }
  .acq-name { font-family: 'Playfair Display', serif; font-size: 24px; font-weight: 700; }
  .acq-card.pixar .acq-name { color: var(--accent); }
  .acq-card.marvel .acq-name { color: var(--accent-2); }
  .acq-card.star-wars .acq-name { color: var(--gold); }
  .acq-price { font-size: 30px; font-family: 'Playfair Display', serif; font-weight: 900; opacity: 0.4; }
  .acq-bullets { list-style: none; display: flex; flex-direction: column; gap: 6px; }
  .acq-bullets li { font-size: 12px; color: var(--text-muted); display: flex; gap: 6px; align-items: flex-start; line-height: 1.4; }
  .acq-bullets li::before { content: '✦'; font-size: 7px; margin-top: 4px; flex-shrink: 0; opacity: 0.5; }
  .acq-result { margin-top: auto; padding: 10px 14px; background: rgba(255,255,255,0.04); border-radius: 7px; font-size: 12px; font-weight: 600; }

  /* ===================== SLIDE 9: STREAMING ===================== */
  #slide-9 .bg-circle.c1 { width: 500px; height: 500px; background: rgba(232,85,62,0.05); left: 50%; top: 50%; transform: translate(-50%, -50%); }
  #slide-9 h2 { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; }
  #slide-9 h2 span { color: var(--accent-2); }
  .crisis-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; flex: 1; margin-top: 20px; }
  .crisis-metrics { display: flex; flex-direction: column; gap: 12px; }
  .c-metric { display: flex; gap: 12px; align-items: center; padding: 14px 16px; background: rgba(232,85,62,0.06); border: 1px solid rgba(232,85,62,0.13); border-radius: 9px; }
  .c-metric .cm-icon { font-size: 24px; }
  .c-metric .cm-big { font-family: 'Playfair Display', serif; font-size: 24px; font-weight: 700; color: var(--accent-2); line-height: 1; }
  .c-metric .cm-label { font-size: 11px; color: var(--text-muted); margin-top: 2px; }
  .response-section { display: flex; flex-direction: column; gap: 12px; }
  .response-section h3 { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--gold); }
  .response-item { padding: 14px 16px; background: rgba(201,168,76,0.04); border: 1px solid rgba(201,168,76,0.12); border-radius: 9px; display: flex; gap: 10px; align-items: flex-start; }
  .response-item .ri-icon { font-size: 18px; flex-shrink: 0; }
  .response-item .ri-text { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
  .response-item .ri-text strong { color: var(--text); display: block; margin-bottom: 2px; }

  /* ===================== SLIDE 10: PROSPERIS ===================== */
  #slide-10 .bg-circle.c1 { width: 500px; height: 500px; background: rgba(46,204,113,0.06); right: -80px; top: -80px; }
  #slide-10 .bg-circle.c2 { width: 300px; height: 300px; background: rgba(201,168,76,0.05); left: -60px; bottom: -60px; }
  #slide-10 h2 { font-family: 'Playfair Display', serif; font-size: 38px; font-weight: 700; line-height: 1.1; }
  #slide-10 h2 span { color: var(--green); }
  .prosperis-layout { display: grid; grid-template-columns: 1fr 1.4fr; gap: 40px; flex: 1; margin-top: 20px; }
  .prosperis-about { display: flex; flex-direction: column; gap: 14px; }
  .prosperis-badge { display: inline-flex; align-items: center; gap: 8px; background: rgba(46,204,113,0.1); border: 1px solid rgba(46,204,113,0.25); color: var(--green); font-size: 10px; letter-spacing: 2px; text-transform: uppercase; padding: 5px 12px; border-radius: 4px; width: fit-content; }
  .about-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 10px; padding: 16px; }
  .about-card .ac-title { font-size: 10px; letter-spacing: 2px; text-transform: uppercase; color: var(--green); margin-bottom: 8px; }
  .about-card p { font-size: 12px; color: var(--text-muted); line-height: 1.6; }
  .about-units { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 8px; }
  .unit-tag { background: rgba(46,204,113,0.08); border: 1px solid rgba(46,204,113,0.2); color: var(--green); font-size: 10px; padding: 4px 10px; border-radius: 4px; letter-spacing: 1px; }
  .lessons-col { display: flex; flex-direction: column; gap: 10px; }
  .lesson-row { display: flex; gap: 14px; align-items: flex-start; padding: 14px 16px; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 10px; transition: all 0.3s; }
  .lesson-row:hover { background: rgba(46,204,113,0.04); border-color: rgba(46,204,113,0.18); }
  .lr-icon { font-size: 22px; flex-shrink: 0; }
  .lr-text h4 { font-size: 13px; font-weight: 600; color: var(--green); margin-bottom: 4px; }
  .lr-text p { font-size: 12px; color: var(--text-muted); line-height: 1.5; }
  .lr-text p strong { color: var(--text); }

  /* ===================== SLIDE 11: KEY LESSONS ===================== */
  #slide-11 { align-items: center; }
  #slide-11 .bg-circle.c1 { width: 500px; height: 500px; background: rgba(201,168,76,0.05); right: -80px; bottom: -80px; }
  #slide-11 h2 { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; text-align: center; width: 100%; }
  #slide-11 h2 span { color: var(--gold); }
  .lessons-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; width: 100%; margin-top: 24px; flex: 1; }
  .lesson-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 12px; padding: 22px 24px; display: flex; gap: 16px; align-items: flex-start; }
  .lesson-num { font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 900; color: rgba(201,168,76,0.14); line-height: 1; flex-shrink: 0; width: 44px; }
  .lesson-body h3 { font-size: 14px; font-weight: 600; color: var(--gold); margin-bottom: 6px; }
  .lesson-body p { font-size: 12px; color: var(--text-muted); line-height: 1.6; }

  /* ===================== SLIDE 12: CLOSING ===================== */
  #slide-12 { justify-content: center; align-items: center; text-align: center; }
  #slide-12 .bg-circle.c1 { width: 600px; height: 600px; background: rgba(201,168,76,0.06); left: 50%; top: 50%; transform: translate(-50%, -50%); }
  #slide-12 .closing-icon { font-size: 52px; margin-bottom: 16px; display: block; }
  #slide-12 h2 { font-family: 'Playfair Display', serif; font-size: 46px; font-weight: 900; max-width: 620px; line-height: 1.1; margin-bottom: 16px; }
  #slide-12 h2 span { color: var(--gold); }
  #slide-12 .closing-quote { font-size: 15px; color: var(--text-muted); max-width: 580px; line-height: 1.7; font-style: italic; font-family: 'Playfair Display', serif; margin-bottom: 32px; }
  #slide-12 .closing-quote em { color: var(--gold); font-style: normal; }
  #slide-12 .final-stats { display: flex; gap: 40px; justify-content: center; }
  #slide-12 .fs { text-align: center; }
  #slide-12 .fs .fs-num { font-family: 'Playfair Display', serif; font-size: 34px; font-weight: 700; color: var(--gold); }
  #slide-12 .fs .fs-label { font-size: 11px; color: var(--text-muted); margin-top: 3px; letter-spacing: 1px; }
</style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>
<div class="key-hint">← → ARROW KEYS</div>
<button class="print-btn" onclick="window.print()">⬇ Download PDF</button>

<div class="presentation" id="presentation">

  <!-- SLIDE 1: TITLE -->
  <div class="slide s-dark active" id="slide-1">
    <div class="bg-circle c1"></div>
    <div class="bg-circle c2"></div>
    <div class="big-year">1923</div>
    <span class="castle">🏰</span>
    <div class="label-tag">Harvard Business School Case Study</div>
    <h1>Disney:<br><span>From Mouse</span><br>to Kingdom</h1>
    <p class="subtitle">How one company used the power of synergy to build a $173 billion empire — and had to reinvent itself to survive.</p>
    <div class="presenter">
      <div class="line"></div>
      <span>Prosperis Holdings · Graduate Trainee Programme</span>
    </div>
    <div class="stats-row">
      <div class="stat"><div class="num">$173B</div><div class="desc">Company Value by 2017</div></div>
      <div class="stat"><div class="num">94 Years</div><div class="desc">From Founding to Empire</div></div>
      <div class="stat"><div class="num">3 Eras</div><div class="desc">Walt · Eisner · Iger</div></div>
      <div class="stat"><div class="num">1 Strategy</div><div class="desc">Synergy — Above All Else</div></div>
    </div>
  </div>

  <!-- SLIDE 2: AGENDA -->
  <div class="slide s-dark2" id="slide-2">
    <div class="bg-circle c1"></div>
    <div class="label-tag">Overview</div>
    <h2>What We'll Cover Today</h2>
    <div class="gold-line"></div>
    <div class="agenda-grid">
      <div class="agenda-item"><div class="agenda-num">01</div><div class="agenda-text"><h3>🎬 The Crisis Before Eisner</h3><p>How Disney nearly went bankrupt and was almost taken over by corporate raiders after Walt's death.</p></div></div>
      <div class="agenda-item"><div class="agenda-num">02</div><div class="agenda-text"><h3>⚡ Synergy: The Core Strategy</h3><p>How Eisner turned synergy from an instinct into a formal, deliberately managed business system.</p></div></div>
      <div class="agenda-item"><div class="agenda-num">03</div><div class="agenda-text"><h3>📈 The Rise and Fall of Eisner</h3><p>The Disney Renaissance, Cap Cities/ABC, and how micromanagement ultimately destroyed what was built.</p></div></div>
      <div class="agenda-item"><div class="agenda-num">04</div><div class="agenda-text"><h3>🚀 Iger's Franchise Revolution</h3><p>Pixar, Marvel, Lucasfilm — and how Iger supercharged synergy through billion-dollar IP acquisitions.</p></div></div>
      <div class="agenda-item"><div class="agenda-num">05</div><div class="agenda-text"><h3>📺 The Streaming Pivot</h3><p>Cord-cutting, ESPN's decline, and why Disney had to bet everything on direct-to-consumer streaming.</p></div></div>
      <div class="agenda-item"><div class="agenda-num">06</div><div class="agenda-text"><h3>🏦 Implications for Prosperis</h3><p>What Disney's synergy playbook means for a diversified Nigerian financial services group in 2024.</p></div></div>
    </div>
  </div>

  <!-- SLIDE 3: CRISIS -->
  <div class="slide s-dark" id="slide-3">
    <div class="bg-circle c1"></div>
    <div class="label-tag">Context · 1966–1984</div>
    <h2>Disney Was<br><em>Dying</em></h2>
    <div class="split">
      <div>
        <p style="font-size:13px; color:var(--text-muted); line-height:1.7; max-width:380px;">When Walt Disney died in 1966, the creative soul of the company died with him. For nearly 20 years, Disney drifted — losing artists, losing market share, and almost losing the company entirely to hostile investors.</p>
        <div class="crisis-stats">
          <div class="crisis-stat"><span class="icon">📉</span><div class="text"><strong>Lowest Box Office Share</strong>Only 4% of Hollywood box office by 1979 — dead last among all major studios</div></div>
          <div class="crisis-stat"><span class="icon">👥</span><div class="text"><strong>Animation Department Collapsed</strong>Shrank from 650 artists to fewer than 200 after Walt died</div></div>
          <div class="crisis-stat"><span class="icon">⚠️</span><div class="text"><strong>Corporate Raider Attack (1984)</strong>Saul Steinberg tried to take over — Disney had to buy back its own stock at inflated prices to survive</div></div>
        </div>
      </div>
      <div>
        <p style="font-size:10px; letter-spacing:2px; text-transform:uppercase; color:var(--text-muted); margin-bottom:14px;">Timeline of Decline</p>
        <div class="timeline-item"><div class="tl-dot">🎨</div><div><div class="tl-year">1923–1966 · Walt Era</div><div class="tl-text"><strong>The Foundation.</strong> Mickey Mouse, Snow White, Disneyland. Walt's TV show promoted the park; the park promoted the films — the first synergy loop.</div></div></div>
        <div class="timeline-item"><div class="tl-dot">🏗️</div><div><div class="tl-year">1966–1971 · Transition</div><div class="tl-text"><strong>All resources diverted</strong> to building Walt Disney World. Animation gutted. Creative engine stops.</div></div></div>
        <div class="timeline-item"><div class="tl-dot">📉</div><div><div class="tl-year">1971–1984 · The Decline</div><div class="tl-text"><strong>Film profits lowest in a decade.</strong> Epcot and Disney Channel launched — high startup costs drain earnings further.</div></div></div>
        <div class="timeline-item"><div class="tl-dot">🆘</div><div><div class="tl-year">1984 · The Rescue</div><div class="tl-text"><strong>Bass family buys 25% of stock,</strong> blocking hostile takeover. Disney gets breathing room — and brings in Michael Eisner.</div></div></div>
      </div>
    </div>
  </div>

  <!-- SLIDE 4: SYNERGY -->
  <div class="slide s-dark2" id="slide-4">
    <div class="bg-circle c1"></div>
    <div class="top">
      <div class="label-tag" style="margin:0 auto 12px;">Core Strategy</div>
      <h2>The Power of <span>Synergy</span></h2>
      <p class="quote">"When Disney's divisions work together, the result is bigger than the sum of its parts. Eisner called it <em>1 + 1 = 3.</em>"</p>
    </div>
    <div class="synergy-wheel">
      <div class="spoke-item top"><div class="spoke-circle">🎬</div><div class="spoke-label">Films &<br>Animation</div></div>
      <div class="spoke-item right"><div class="spoke-circle">🎢</div><div class="spoke-label">Theme<br>Parks</div></div>
      <div class="spoke-item bottom"><div class="spoke-circle">🛒</div><div class="spoke-label">Retail &<br>Merch</div></div>
      <div class="spoke-item left"><div class="spoke-circle">📺</div><div class="spoke-label">TV &<br>Streaming</div></div>
      <div class="spoke-item top-right"><div class="spoke-circle">🎵</div><div class="spoke-label">Music &<br>Publishing</div></div>
      <div class="spoke-item bottom-left"><div class="spoke-circle">🏨</div><div class="spoke-label">Hotels &<br>Resorts</div></div>
      <div class="wheel-center"><div class="big-icon">✨</div><div class="label">SYNERGY</div></div>
    </div>
  </div>

  <!-- SLIDE 5: ALADDIN -->
  <div class="slide s-dark" id="slide-5">
    <div class="bg-circle c1"></div>
    <div class="label-tag">Synergy In Action · 1992</div>
    <h2>The <em>Aladdin</em> Blueprint — One Film, Every Division Activated</h2>
    <div class="aladdin-grid">
      <div class="aladdin-card"><span class="card-icon">🎬</span><div class="card-title">Film & TV</div><ul class="card-items"><li>Two 1-hour TV specials on CBS</li><li>Trailer on 15M Beauty & Beast VHS tapes</li><li>30-min "making of" on Disney Channel</li><li>Aladdin Sing-Along home video</li></ul></div>
      <div class="aladdin-card"><span class="card-icon">🎢</span><div class="card-title">Parks & Resorts</div><ul class="card-items"><li>Animated window displays on Main St USA</li><li>Costumed characters at Disneyland</li><li>Aladdin's Royal Caravan Parade</li><li>Aladdin's Oasis Restaurant at Disneyland</li></ul></div>
      <div class="aladdin-card"><span class="card-icon">🛍️</span><div class="card-title">Retail</div><ul class="card-items"><li>Clothing at Walmart, K-Mart, JC Penney</li><li>T-shirts on 11M boxes of Cap'N Crunch</li><li>Themed windows in Disney Stores</li><li>Promos on store register receipts</li></ul></div>
      <div class="aladdin-card"><span class="card-icon">📚</span><div class="card-title">Publishing</div><ul class="card-items"><li>Cover image in Disney Channel Magazine</li><li>Flip books, junior novelizations, pop-up books</li><li>Graphic novel and junior graphic novel</li><li>Coffee table "making of" book</li></ul></div>
      <div class="aladdin-card"><span class="card-icon">🎵</span><div class="card-title">Music</div><ul class="card-items"><li>Movie soundtrack on Walt Disney Records</li><li>Read-along collection</li><li>Sound and Story Theater audiobook</li></ul></div>
      <div class="aladdin-card"><span class="card-icon">🎪</span><div class="card-title">Live Events</div><ul class="card-items"><li>Live show at El Capitan Theatre Hollywood</li><li>Auction at Sotheby's NYC — animation cels</li><li>Sweepstakes for Disneyland/Disney World trips</li></ul></div>
    </div>
    <div class="aladdin-result">
      <div class="result-text"><strong>Result: Most Successful Film of 1992</strong><br>Every division activated. Money flowing from everywhere. This is synergy in its purest form.</div>
      <div class="result-numbers">
        <div class="result-num"><div class="big">$218M</div><div class="small">US Box Office</div></div>
        <div class="result-num"><div class="big">$504M</div><div class="small">Worldwide</div></div>
        <div class="result-num"><div class="big">#1</div><div class="small">Film of 1992</div></div>
      </div>
    </div>
  </div>

  <!-- SLIDE 6: EISNER RISE -->
  <div class="slide s-dark2" id="slide-6">
    <div class="bg-circle c1"></div>
    <div class="label-tag">The Eisner Era · 1984–2005</div>
    <h2>The <span>Turnaround</span> — Building the Empire</h2>
    <div class="wins-grid">
      <div class="win-card"><div class="win-icon">🎥</div><div class="win-num">Lion King</div><div class="win-label">$312M domestic — animated film record at the time (1994)</div></div>
      <div class="win-card"><div class="win-icon">🏪</div><div class="win-num">600+ Stores</div><div class="win-label">Disney Store retail chain launched 1987, grew worldwide</div></div>
      <div class="win-card"><div class="win-icon">📡</div><div class="win-num">$19B Deal</div><div class="win-label">Cap Cities/ABC acquired 1995 — ESPN, ABC, A&E, Lifetime</div></div>
      <div class="win-card"><div class="win-icon">🎡</div><div class="win-num">33.7M</div><div class="win-label">Disney World visitors in 1990 — despite economic recession</div></div>
    </div>
    <div class="revenue-bar-section">
      <h3>Revenue Growth Under Eisner (USD)</h3>
      <div class="bar-row"><span class="bar-year">1984</span><div class="bar-track"><div class="bar-fill" style="width:3%"></div></div><span class="bar-val">$1.66B</span></div>
      <div class="bar-row"><span class="bar-year">1987</span><div class="bar-track"><div class="bar-fill" style="width:5%"></div></div><span class="bar-val">$2.88B</span></div>
      <div class="bar-row"><span class="bar-year">1991</span><div class="bar-track"><div class="bar-fill" style="width:11%"></div></div><span class="bar-val">$6.11B</span></div>
      <div class="bar-row"><span class="bar-year">1996</span><div class="bar-track"><div class="bar-fill" style="width:34%"></div></div><span class="bar-val">$18.74B</span></div>
      <div class="bar-row"><span class="bar-year">2000</span><div class="bar-track"><div class="bar-fill" style="width:44%"></div></div><span class="bar-val">$24.42B</span></div>
      <div class="bar-row"><span class="bar-year">2004</span><div class="bar-track"><div class="bar-fill" style="width:56%"></div></div><span class="bar-val">$30.75B</span></div>
    </div>
  </div>

  <!-- SLIDE 7: EISNER FALL -->
  <div class="slide s-dark" id="slide-7">
    <div class="bg-circle c1"></div>
    <div class="label-tag">The Eisner Downfall · 1994–2005</div>
    <h2>When <span>Micromanagement</span> Killed the Magic</h2>
    <div class="fall-layout">
      <div class="fall-list">
        <div class="fall-item"><span class="fi-icon">✈️</span><div class="fi-text"><strong>Frank Wells Dies (April 1994)</strong>Disney's President died in a helicopter crash. He was the business balance to Eisner's creativity. Without him, Eisner spiralled into micromanagement.</div></div>
        <div class="fall-item"><span class="fi-icon">🎬</span><div class="fi-text"><strong>Katzenberg Leaves → DreamWorks Born</strong>Eisner refused to make him president. He left with Geffen and Spielberg to found DreamWorks — a direct competitor.</div></div>
        <div class="fall-item"><span class="fi-icon">🍎</span><div class="fi-text"><strong>Pixar Partnership Ends (2004)</strong>Steve Jobs ended the deal after failed negotiations. Pixar films = ~50% of Disney studio's operating profit at the time.</div></div>
        <div class="fall-item"><span class="fi-icon">🎭</span><div class="fi-text"><strong>Animation Collapses</strong>4 Disney films (2001–2004) combined for $650M worldwide. Finding Nemo alone made $940M for Pixar in 2003.</div></div>
        <div class="fall-item"><span class="fi-icon">🗳️</span><div class="fi-text"><strong>Board Revolts (2005)</strong>Roy E. Disney and Stanley Gold resign, calling for Eisner to step down. He officially resigns September 30, 2005.</div></div>
      </div>
      <div class="fall-right">
        <div class="big-metric"><div class="bm-icon">📉</div><div class="bm-num">-47%</div><div class="bm-label">Disney stock price fell between May 2000 and September 2004</div></div>
        <div class="verdict-box"><p>"Eisner built the machine. But his inability to share power destroyed the partnerships that made synergy work. <em>The lesson: synergy requires collaboration, not control.</em>"</p></div>
      </div>
    </div>
  </div>

  <!-- SLIDE 8: IGER ACQUISITIONS -->
  <div class="slide s-dark2" id="slide-8">
    <div class="bg-circle c1"></div>
    <div class="label-tag">The Iger Era · 2005–2017</div>
    <h2>The <span>Franchise Revolution</span></h2>
    <p style="font-size:13px; color:var(--text-muted); margin-top:6px;">Iger's strategy: own the IP that people love, then activate synergy across every Disney division.</p>
    <div class="acq-cards">
      <div class="acq-card pixar"><div class="acq-icon">🎞️</div><div class="acq-year">Acquired · January 2006</div><div class="acq-name">Pixar</div><div class="acq-price">$7.4B</div><ul class="acq-bullets"><li>Saved Disney's struggling animation division</li><li>Toy Story 3 &amp; Finding Dory each grossed $1B+ internationally</li><li>Frozen made $1.3B internationally + billions in merchandise</li><li>Disney became first media company on iTunes</li></ul><div class="acq-result" style="color:var(--accent)">💡 Frozen featured in 5 WDW attractions by 2017</div></div>
      <div class="acq-card marvel"><div class="acq-icon">🦸</div><div class="acq-year">Acquired · 2009</div><div class="acq-name">Marvel</div><div class="acq-price">$4B</div><ul class="acq-bullets"><li>Access to 5,000+ licensed characters</li><li>14 MCU films by August 2017</li><li>4 films crossed $1B internationally</li><li>Iron Man Experience opened Hong Kong Disneyland 2016</li><li>Marvel merchandise across all Disney divisions</li></ul><div class="acq-result" style="color:var(--accent-2)">💡 MCU = highest-grossing film franchise in history</div></div>
      <div class="acq-card star-wars"><div class="acq-icon">⚡</div><div class="acq-year">Acquired · 2012</div><div class="acq-name">Lucasfilm</div><div class="acq-price">~$4B</div><ul class="acq-bullets"><li>Star Wars + Indiana Jones franchises</li><li>Industrial Light &amp; Magic (world's best VFX)</li><li>US Star Wars toy sales: $700M+ in 2015 alone</li><li>Galaxy's Edge opened in Disney parks</li><li>11 franchises × $1B+ consumer product sales by 2016</li></ul><div class="acq-result" style="color:var(--gold)">💡 Star Wars toys alone: $700M in US in 2015</div></div>
    </div>
  </div>

  <!-- SLIDE 9: STREAMING -->
  <div class="slide s-dark" id="slide-9">
    <div class="bg-circle c1"></div>
    <div class="label-tag">The New Threat · 2011–2017</div>
    <h2>Cord-Cutting &amp; the <span>Streaming Pivot</span></h2>
    <div class="crisis-layout">
      <div class="crisis-metrics">
        <p style="font-size:10px; letter-spacing:2px; text-transform:uppercase; color:var(--text-muted); margin-bottom:6px;">The Problem</p>
        <div class="c-metric"><span class="cm-icon">📺</span><div><div class="cm-big">-10M</div><div class="cm-label">ESPN subscribers lost between 2011–2016</div></div></div>
        <div class="c-metric"><span class="cm-icon">👶</span><div><div class="cm-big">-41%</div><div class="cm-label">Drop in TV viewing among teens 12–17 (2012–2017)</div></div></div>
        <div class="c-metric"><span class="cm-icon">🔻</span><div><div class="cm-big">Last</div><div class="cm-label">ABC ranked last among all 4 major networks consistently from 2007</div></div></div>
        <div class="c-metric"><span class="cm-icon">🎥</span><div><div class="cm-big">49.4M</div><div class="cm-label">Netflix subscribers vs 48.6M for all top cable companies combined (Q1 2017)</div></div></div>
      </div>
      <div class="response-section">
        <h3>Disney's Response</h3>
        <div class="response-item"><span class="ri-icon">🚫</span><div class="ri-text"><strong>Pull Content from Netflix (Aug 2017)</strong>All Disney and Pixar films removed by end of 2018. Disney takes back control of its own IP distribution.</div></div>
        <div class="response-item"><span class="ri-icon">▶️</span><div class="ri-text"><strong>Launch Disney+ by 2019</strong>Own streaming platform — Disney, Pixar, Marvel, Star Wars content. Customers buy direct from Disney.</div></div>
        <div class="response-item"><span class="ri-icon">🏆</span><div class="ri-text"><strong>Launch ESPN Plus (2018)</strong>Sports streaming — 10,000 events/year including MLB, NHL, MLS. Built on $1.58B BAM Tech acquisition.</div></div>
        <div class="response-item"><span class="ri-icon">🦊</span><div class="ri-text"><strong>Buy 21st Century Fox for $52.4B (Dec 2017)</strong>Gains X-Men for MCU, 60% Hulu stake, National Geographic, FX, and international reach via Sky &amp; Star.</div></div>
      </div>
    </div>
  </div>

  <!-- SLIDE 10: PROSPERIS IMPLICATIONS -->
  <div class="slide s-dark2" id="slide-10">
    <div class="bg-circle c1"></div>
    <div class="bg-circle c2"></div>
    <div class="label-tag" style="background:rgba(46,204,113,0.1); border-color:rgba(46,204,113,0.3); color:var(--green);">Strategic Implications</div>
    <h2>What This Means for<br><span>Prosperis Holdings</span></h2>
    <div class="prosperis-layout">
      <div class="prosperis-about">
        <div class="about-card">
          <div class="ac-title">About Prosperis Holdings</div>
          <p>A diversified Nigerian financial services group incorporated in 2005, operating across investment banking, securities trading, asset management, trusteeship, lending, real estate, and Bureau de Change. Their vision: <em style="color:var(--green)">"an ecosystem of prosperous, value-adding businesses in Sub-Saharan Africa."</em></p>
          <div class="about-units">
            <span class="unit-tag">AVA Securities</span>
            <span class="unit-tag">AVA Global Asset Mgrs</span>
            <span class="unit-tag">AVA Capital</span>
            <span class="unit-tag">AVA Trustees</span>
            <span class="unit-tag">Trives Financials</span>
            <span class="unit-tag">Jabetza Realty</span>
            <span class="unit-tag">Sharjah BDC</span>
          </div>
        </div>
        <div class="about-card" style="background:rgba(46,204,113,0.05); border-color:rgba(46,204,113,0.15);">
          <div class="ac-title">The Core Parallel</div>
          <p>Like Disney, Prosperis is a <strong style="color:var(--text)">diversified group with multiple business units</strong> serving overlapping customer bases. Disney's synergy playbook — making every division feed every other — is directly applicable here.</p>
        </div>
      </div>

      <div class="lessons-col">
        <div class="lesson-row">
          <span class="lr-icon">🔗</span>
          <div class="lr-text">
            <h4>Build Cross-Division Synergy Deliberately</h4>
            <p>Disney didn't leave synergy to chance — it created a <strong>dedicated department</strong> for it. Prosperis should create formal channels for AVA Securities, AVA Trustees, AVA Capital, and Trives Financials to share client referrals, co-structure products, and cross-market services. A client who trades securities can also need trusteeship, asset management, and real estate.</p>
          </div>
        </div>
        <div class="lesson-row">
          <span class="lr-icon">🏆</span>
          <div class="lr-text">
            <h4>Own Your Core IP — Your Client Relationships</h4>
            <p>Disney's IP was its characters. <strong>Prosperis's equivalent is its client base and brand trust.</strong> Just as Disney pulled content from Netflix to own distribution, Prosperis should ensure it owns the client relationship end-to-end — not cede it to third-party platforms or intermediaries.</p>
          </div>
        </div>
        <div class="lesson-row">
          <span class="lr-icon">📱</span>
          <div class="lr-text">
            <h4>Adapt Early to Digital Disruption</h4>
            <p>Disney waited too long before pivoting to streaming — and lost millions of subscribers in the meantime. <strong>Nigerian fintech is growing fast.</strong> Prosperis should invest in digital channels now, before disruption from fintechs forces a reactive, more expensive pivot later.</p>
          </div>
        </div>
        <div class="lesson-row">
          <span class="lr-icon">🤝</span>
          <div class="lr-text">
            <h4>Synergy Requires Trust, Not Just Structure</h4>
            <p>Eisner had the synergy structure but <strong>broke the relationships</strong> that made it work. Prosperis's Graduate Trainee Programme builds exactly what Disney needed more of — people who understand the whole organisation and can drive collaboration across units from the inside.</p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- SLIDE 11: KEY LESSONS -->
  <div class="slide s-dark" id="slide-11">
    <div class="bg-circle c1"></div>
    <div class="label-tag">Business Analysis</div>
    <h2>Four <span>Universal Lessons</span> from Disney</h2>
    <div class="lessons-grid">
      <div class="lesson-card"><div class="lesson-num">01</div><div class="lesson-body"><h3>Synergy Must Be Managed, Not Assumed</h3><p>Eisner built a whole department for synergy, held weekly cross-division meetings, and sent regular newsletters. Synergy is a strategy that must be actively engineered. If you don't manage it, it won't happen on its own.</p></div></div>
      <div class="lesson-card"><div class="lesson-num">02</div><div class="lesson-body"><h3>IP Is the Foundation of Everything</h3><p>Disney's greatest asset wasn't its parks or TV channels — it was the characters people loved. Strong IP enables synergy across every division, indefinitely. Identify and protect your most irreplaceable assets.</p></div></div>
      <div class="lesson-card"><div class="lesson-num">03</div><div class="lesson-body"><h3>Strategy Without Trust Collapses</h3><p>Eisner and Iger both understood synergy. But Eisner's micromanagement destroyed the partnerships (Pixar, Katzenberg, Steve Jobs) that made it work. The best structure fails without the right relationships inside it.</p></div></div>
      <div class="lesson-card"><div class="lesson-num">04</div><div class="lesson-body"><h3>Cannibalise Yourself Before Others Do</h3><p>Disney's cable TV model was being killed by the internet. Rather than wait, Iger launched Disney+ — competing with his own channels. If your business model faces disruption, be the disruptor. Don't let others do it to you.</p></div></div>
    </div>
  </div>

  <!-- SLIDE 12: CLOSING -->
  <div class="slide s-dark" id="slide-12">
    <div class="bg-circle c1"></div>
    <span class="closing-icon">🏰</span>
    <h2>The Magic Was Always <span>Synergy</span></h2>
    <p class="closing-quote">"Disney grew from nearly bankrupt in 1984 to a $173 billion empire by 2017. That is the power of a well-executed synergy strategy — compounded over time, across every part of the business. <em>One story. Every division. Unlimited value.</em>"</p>
    <div class="final-stats">
      <div class="fs"><div class="fs-num">$173B</div><div class="fs-label">Value by 2017</div></div>
      <div class="fs"><div class="fs-num">34×</div><div class="fs-label">Revenue Growth 1984–2016</div></div>
      <div class="fs"><div class="fs-num">11</div><div class="fs-label">$1B+ Franchises by 2016</div></div>
      <div class="fs"><div class="fs-num">1</div><div class="fs-label">Core Strategy: Synergy</div></div>
    </div>
  </div>

</div>

<!-- NAV -->
<nav class="nav" id="navBar">
  <button onclick="prevSlide()">←</button>
  <div class="dot-nav" id="dotNav"></div>
  <span class="slide-counter" id="counter">01 / 12</span>
  <button onclick="nextSlide()">→</button>
</nav>

<script>
  const slides = document.querySelectorAll('.slide');
  const total = slides.length;
  let cur = 0;
  const dotNav = document.getElementById('dotNav');
  const counter = document.getElementById('counter');
  const progressBar = document.getElementById('progressBar');

  slides.forEach((_, i) => {
    const d = document.createElement('div');
    d.className = 'dot' + (i === 0 ? ' active' : '');
    d.onclick = () => goTo(i);
    dotNav.appendChild(d);
  });

  function goTo(n) {
    slides[cur].classList.remove('active');
    cur = Math.max(0, Math.min(n, total - 1));
    slides[cur].classList.add('active');
    updateNav();
  }

  function nextSlide() { if (cur < total - 1) goTo(cur + 1); }
  function prevSlide() { if (cur > 0) goTo(cur - 1); }

  function updateNav() {
    dotNav.querySelectorAll('.dot').forEach((d, i) => d.classList.toggle('active', i === cur));
    counter.textContent = String(cur + 1).padStart(2, '0') + ' / ' + String(total).padStart(2, '0');
    progressBar.style.width = ((cur + 1) / total * 100) + '%';
  }

  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowRight' || e.key === 'ArrowDown') nextSlide();
    if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') prevSlide();
  });

  updateNav();
</script>
</body>
</html>
