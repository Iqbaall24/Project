<title>Iqbal Capital Portfolio</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>

<style>
/*
 * Iqbal Capital — Personal Portfolio Dashboard
 * Dark-first: navy-dark bg, BTC orange accent, emerald gains
 * Type: Inter (UI) + JetBrains Mono (numbers)
 */
:root {
  --bg:        #0b0e18;
  --bg-card:   #12162a;
  --bg-hover:  #1b1f36;
  --bg-input:  #0d1020;
  --border:    #1f2440;
  --border2:   #2c3258;
  --fg:        #dde3f4;
  --fg2:       #7a88b0;
  --fg3:       #424d6e;
  --accent:    #3b82f6;
  --accent-bg: rgba(59,130,246,.08);
  --green:     #10d991;
  --green-bg:  rgba(16,217,145,.09);
  --red:       #ff4b6e;
  --red-bg:    rgba(255,75,110,.09);
  --btc:       #f7931a;
  --btc-bg:    rgba(247,147,26,.07);
  --gold:      #f59e0b;
  --r: 9px;
  color-scheme: dark;
}
@media (prefers-color-scheme: light) {
  :root:not([data-theme="dark"]) {
    --bg:#f0f2f8; --bg-card:#fff; --bg-hover:#eaecf5; --bg-input:#f5f7fc;
    --border:#dde3f0; --border2:#c5cce6;
    --fg:#111624; --fg2:#5e6a8a; --fg3:#9aa3be;
    color-scheme: light;
  }
}
:root[data-theme="light"] {
  --bg:#f0f2f8; --bg-card:#fff; --bg-hover:#eaecf5; --bg-input:#f5f7fc;
  --border:#dde3f0; --border2:#c5cce6;
  --fg:#111624; --fg2:#5e6a8a; --fg3:#9aa3be;
  color-scheme: light;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
body{background:var(--bg);color:var(--fg);font-family:'Inter',system-ui,sans-serif;font-size:14px;line-height:1.5;
  padding-left:max(0px,env(safe-area-inset-left,0px));
  padding-right:max(0px,env(safe-area-inset-right,0px));}

/* ── NAV ── */
.nav{
  position:sticky;top:env(safe-area-inset-top,0px);z-index:50;
  height:52px;background:var(--bg-card);border-bottom:1px solid var(--border);
  display:flex;align-items:center;gap:4px;
  padding:0 max(20px,env(safe-area-inset-right,0px)) 0 max(20px,env(safe-area-inset-left,0px));
}
.nav-brand{display:flex;align-items:center;gap:8px;font-weight:700;font-size:14px;letter-spacing:-.3px;margin-right:8px;color:var(--fg);}
.nav-ic{width:26px;height:26px;background:linear-gradient(135deg,var(--btc),#e8640a);border-radius:6px;
  display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:800;color:#fff;}
.nav-item{padding:5px 11px;border-radius:6px;font-size:13px;color:var(--fg2);cursor:pointer;border:none;
  background:none;font-family:inherit;transition:.15s;white-space:nowrap;}
.nav-item:hover{color:var(--fg);background:var(--bg-hover);}
.nav-item.active{color:var(--fg);background:var(--bg-hover);}
.spacer{flex:1;}
.btn{display:inline-flex;align-items:center;gap:5px;padding:6px 13px;border-radius:7px;font-size:13px;
  font-weight:500;cursor:pointer;border:1px solid var(--border);background:var(--bg-hover);color:var(--fg);
  font-family:inherit;transition:.15s;white-space:nowrap;text-decoration:none;}
.btn:hover{border-color:var(--border2);}
.btn-primary{background:var(--accent);border-color:transparent;color:#fff;}
.btn-primary:hover{background:#2563eb;}
.btn-success{background:var(--green);border-color:transparent;color:#0b0e18;font-weight:600;}
.btn-success:hover{background:#0cc97f;}

/* ── MAIN ── */
.main{max-width:1140px;margin:0 auto;
  padding:24px max(20px,env(safe-area-inset-right,0px)) 56px max(20px,env(safe-area-inset-left,0px));}

/* ── HEADER ── */
.ph-title{font-size:20px;font-weight:700;letter-spacing:-.4px;margin-bottom:10px;}
.date-bar{display:flex;align-items:center;gap:4px;flex-wrap:wrap;margin-bottom:20px;}
.dchip{padding:4px 12px;border-radius:20px;font-size:12px;font-weight:500;cursor:pointer;
  border:1px solid var(--border);background:none;color:var(--fg2);font-family:inherit;transition:.15s;}
.dchip:hover{color:var(--fg);border-color:var(--border2);}
.dchip.active{color:var(--fg);background:var(--accent-bg);border-color:var(--accent);}
.drange{font-size:12px;color:var(--fg3);margin-left:4px;}

/* ── BTC BANNER ── */
.btc-banner{
  background:var(--btc-bg);border:1px solid rgba(247,147,26,.22);border-radius:var(--r);
  padding:14px 18px;margin-bottom:18px;
  display:flex;align-items:center;gap:14px;flex-wrap:wrap;
}
.btc-logo{width:38px;height:38px;background:var(--btc);border-radius:50%;
  display:flex;align-items:center;justify-content:center;font-size:18px;font-weight:800;
  color:#fff;flex-shrink:0;font-style:italic;}
.btc-info{flex:1;min-width:160px;}
.btc-lbl{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.8px;color:var(--fg2);margin-bottom:1px;}
.btc-idr{font-size:22px;font-weight:700;font-variant-numeric:tabular-nums;letter-spacing:-.4px;line-height:1.2;}
.btc-usd{font-size:12px;color:var(--fg2);font-variant-numeric:tabular-nums;}
.btc-meta{display:flex;flex-direction:column;align-items:flex-end;gap:4px;}
.spill{display:flex;align-items:center;gap:5px;font-size:11px;font-weight:600;padding:3px 9px;border-radius:10px;}
.spill.live{background:var(--green-bg);color:var(--green);}
.spill.cached{background:rgba(245,158,11,.1);color:var(--gold);}
.spill.offline{background:var(--bg-hover);color:var(--fg3);}
.dot{width:6px;height:6px;border-radius:50%;background:currentColor;}
.dot.pulse{animation:pulse 2s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
.btc-ts{font-size:11px;color:var(--fg3);text-align:right;}
.rate-row{display:flex;align-items:center;gap:6px;font-size:12px;color:var(--fg2);}
.e-sm{background:var(--bg-input);border:1px solid var(--border2);border-radius:5px;color:var(--fg);
  font-family:inherit;font-size:12px;padding:3px 7px;width:72px;outline:none;}
.e-sm:focus{border-color:var(--accent);}

/* ── METRICS ── */
.metrics{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:18px;}
@media(max-width:700px){.metrics{grid-template-columns:repeat(2,1fr);}}
@media(max-width:400px){.metrics{grid-template-columns:1fr;}}
.metric{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--r);padding:14px 16px;}
.m-lbl{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.7px;color:var(--fg2);margin-bottom:6px;}
.m-val{font-size:18px;font-weight:700;letter-spacing:-.4px;font-variant-numeric:tabular-nums;margin-bottom:2px;}
.m-sub{font-size:12px;font-variant-numeric:tabular-nums;color:var(--fg2);}
.pos{color:var(--green)!important;}
.neg{color:var(--red)!important;}

/* ── CHART ── */
.chart-card{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--r);
  padding:16px 20px 12px;margin-bottom:18px;}
.chart-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;}
.chart-ttl{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.7px;color:var(--fg2);}
.chart-wrap{position:relative;height:180px;}

/* ── EDIT BAR ── */
.edit-bar{background:var(--accent-bg);border:1px solid rgba(59,130,246,.3);border-radius:var(--r);
  padding:10px 16px;margin-bottom:18px;display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
.eb-text{font-size:13px;color:var(--fg2);flex:1;min-width:180px;}
.eb-text strong{color:var(--fg);}

/* ── SECTION ── */
.section{margin-bottom:24px;}
.sec-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;}
.sec-lbl{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.9px;color:var(--fg2);
  display:flex;align-items:center;gap:7px;}
.badge{background:var(--bg-hover);border:1px solid var(--border);border-radius:4px;
  padding:1px 6px;font-size:10px;font-weight:700;color:var(--fg3);}
.tbl-wrap{border:1px solid var(--border);border-radius:var(--r);overflow:hidden;overflow-x:auto;}
table{width:100%;border-collapse:collapse;min-width:580px;}
thead th{background:var(--bg-card);padding:9px 14px;text-align:right;font-size:10px;font-weight:700;
  text-transform:uppercase;letter-spacing:.7px;color:var(--fg3);white-space:nowrap;
  border-bottom:1px solid var(--border);}
thead th:first-child{text-align:left;}
tbody tr{background:var(--bg-card);border-bottom:1px solid var(--border);transition:background .1s;}
tbody tr:last-child{border-bottom:none;}
tbody tr:hover{background:var(--bg-hover);}
td{padding:11px 14px;text-align:right;font-variant-numeric:tabular-nums;vertical-align:middle;}
td:first-child{text-align:left;}
.asset{display:flex;align-items:center;gap:10px;}
.aicon{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-size:10px;font-weight:800;color:#fff;flex-shrink:0;}
.aname{font-size:14px;font-weight:600;color:var(--fg);line-height:1.2;}
.afull{font-size:11px;color:var(--fg2);}
.rpill{display:inline-flex;align-items:center;padding:3px 8px;border-radius:5px;
  font-size:12px;font-weight:600;font-variant-numeric:tabular-nums;}
.rpill.pos{background:var(--green-bg);color:var(--green);}
.rpill.neg{background:var(--red-bg);color:var(--red);}
.closed{font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:.4px;
  color:var(--fg3);background:var(--bg-hover);border:1px solid var(--border);border-radius:3px;padding:2px 6px;}
.mono{font-family:'JetBrains Mono','Fira Code',monospace;font-variant-numeric:tabular-nums;font-size:13px;}
.tot-row{background:var(--bg-card)!important;border-top:2px solid var(--border2)!important;}
.tot-row td{font-weight:700;}
.e-input{background:var(--bg-input);border:1px solid var(--accent);border-radius:5px;color:var(--fg);
  font-family:inherit;font-size:13px;font-variant-numeric:tabular-nums;padding:4px 8px;width:130px;
  text-align:right;outline:none;}
.e-input:focus{box-shadow:0 0 0 2px rgba(59,130,246,.15);}

/* ── FOOTER ── */
.footer{margin-top:28px;padding-top:18px;border-top:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px;}
.foot-l{font-size:11px;color:var(--fg3);}
.foot-r{display:flex;gap:10px;}
.flink{font-size:11px;color:var(--fg2);text-decoration:none;display:flex;align-items:center;gap:4px;}
.flink:hover{color:var(--fg);}

/* ── TOAST ── */
.toast{position:fixed;bottom:max(20px,env(safe-area-inset-bottom,20px));
  right:max(20px,env(safe-area-inset-right,20px));
  background:var(--bg-card);border:1px solid var(--border2);border-radius:8px;
  padding:10px 16px;font-size:13px;color:var(--fg);z-index:100;
  box-shadow:0 8px 24px rgba(0,0,0,.4);transform:translateY(60px);opacity:0;
  transition:.25s;pointer-events:none;}
.toast.show{transform:none;opacity:1;}
.toast.ok{border-color:var(--green);}
</style>

<!-- NAV -->
<nav class="nav">
  <span class="nav-brand">
    <span class="nav-ic">IC</span>
    Iqbal Capital
  </span>
  <button class="nav-item active">Investments</button>
  <button class="nav-item">Analytics</button>
  <button class="nav-item">Reports</button>
  <div class="spacer"></div>
  <button class="btn" id="themeBtn" title="Toggle theme">🌙</button>
  <a class="btn" href="https://www.tradingview.com/chart/?symbol=BINANCE%3ABTCUSDT" target="_blank" rel="noopener">
    <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>
    TradingView
  </a>
  <button class="btn btn-primary" id="editBtn">
    <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
    Edit
  </button>
</nav>

<main class="main">

  <!-- HEADER -->
  <div class="ph-title" id="portTitle">Muhammad Iqbal's Portfolio</div>
  <div class="date-bar">
    <button class="dchip" data-p="today">Today</button>
    <button class="dchip" data-p="7d">7D</button>
    <button class="dchip" data-p="12m">12M</button>
    <button class="dchip" data-p="ytd">YTD</button>
    <button class="dchip" data-p="fy">FY</button>
    <button class="dchip active" data-p="all">All</button>
    <span class="drange" id="dateRange">10/07/2024 – 24/10/2026</span>
    <div class="spacer"></div>
    <button class="btn" id="refreshBtn" style="padding:5px 11px;font-size:12px;">
      <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="23 4 23 10 17 10"/><path d="M20.49 15a9 9 0 1 1-2.12-9.36L23 10"/></svg>
      Refresh
    </button>
  </div>

  <!-- BTC BANNER -->
  <div class="btc-banner">
    <div class="btc-logo">₿</div>
    <div class="btc-info">
      <div class="btc-lbl">Bitcoin · BTC/IDR — Live Price</div>
      <div class="btc-idr" id="btcIDR">—</div>
      <div class="btc-usd" id="btcUSD">$ —</div>
    </div>
    <div class="btc-meta">
      <div class="spill offline" id="pStatus">
        <span class="dot" id="sDot"></span>
        <span id="sText">Loading…</span>
      </div>
      <div class="btc-ts" id="btcTs">—</div>
    </div>
    <div class="rate-row">
      <span>USD/IDR</span>
      <input class="e-sm" id="rateInput" type="number" value="15900" title="Set USD/IDR rate">
      <button class="btn" id="rateBtn" style="padding:4px 10px;font-size:12px;">Set</button>
    </div>
  </div>

  <!-- METRICS -->
  <div class="metrics">
    <div class="metric">
      <div class="m-lbl">Portfolio Value</div>
      <div class="m-val" id="mVal">IDR —</div>
      <div class="m-sub" id="mValSub">0.00353763 BTC</div>
    </div>
    <div class="metric">
      <div class="m-lbl">Capital Gain</div>
      <div class="m-val pos" id="mCap">+1.13%</div>
      <div class="m-sub" id="mCapAmt">Rp 81,985.05</div>
    </div>
    <div class="metric">
      <div class="m-lbl">Currency Gain</div>
      <div class="m-val pos" id="mCur">+9.89%</div>
      <div class="m-sub" id="mCurAmt">Rp 718,522.48</div>
    </div>
    <div class="metric">
      <div class="m-lbl">Total Return</div>
      <div class="m-val pos" id="mTot">+11.02%</div>
      <div class="m-sub" id="mTotAmt">Rp 800,507.53</div>
    </div>
  </div>

  <!-- CHART -->
  <div class="chart-card">
    <div class="chart-hdr">
      <div class="chart-ttl">Investment Value</div>
      <div style="font-size:11px;color:var(--fg3);" id="chartSub">All time · IDR</div>
    </div>
    <div class="chart-wrap">
      <canvas id="pfChart"></canvas>
    </div>
  </div>

  <!-- EDIT BAR -->
  <div class="edit-bar" id="editBar" hidden>
    <span style="font-size:16px;">✏️</span>
    <div class="eb-text"><strong>Edit Mode</strong> — Ubah nilai langsung. Data tersimpan di browser Anda.</div>
    <button class="btn btn-success" id="saveBtn">
      <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="20 6 9 17 4 12"/></svg>
      Simpan
    </button>
    <button class="btn" id="cancelBtn">Batal</button>
  </div>

  <!-- CRYPTO -->
  <div class="section">
    <div class="sec-hdr">
      <div class="sec-lbl">Crypto <span class="badge">5</span></div>
      <div style="font-size:11px;color:var(--fg3);">Sorted by value</div>
    </div>
    <div class="tbl-wrap">
      <table>
        <thead><tr>
          <th>Asset</th><th>Avg Buy Price</th><th>Quantity</th><th>Value</th><th>Return</th>
        </tr></thead>
        <tbody id="cBody"></tbody>
        <tfoot id="cFoot"></tfoot>
      </table>
    </div>
  </div>

  <!-- IDX -->
  <div class="section">
    <div class="sec-hdr">
      <div class="sec-lbl">IDX <span class="badge">2</span></div>
      <div style="font-size:11px;color:var(--fg3);">Indonesian stocks</div>
    </div>
    <div class="tbl-wrap">
      <table>
        <thead><tr>
          <th>Asset</th><th>Avg Buy Price</th><th>Quantity</th><th>Value</th><th>Return</th>
        </tr></thead>
        <tbody id="iBody"></tbody>
        <tfoot id="iFoot"></tfoot>
      </table>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer">
    <div class="foot-l">© 2026 Iqbal Capital · Personal Portfolio Tracker</div>
    <div class="foot-r">
      <a class="flink" href="https://github.com" target="_blank" rel="noopener">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a class="flink" href="https://www.tradingview.com/chart/?symbol=BINANCE:BTCUSDT" target="_blank" rel="noopener">
        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>
        TradingView
      </a>
    </div>
  </div>

</main>

<div class="toast" id="toast"></div>

<script>
// ═══════════════════════════════════════════
// IQBAL CAPITAL PORTFOLIO TRACKER v1.0
// ═══════════════════════════════════════════

const SK = 'iqbal_pf_v1';

const DEF = {
  usdIdrRate: 15900,
  lastBtcIDR: 1469069432,
  lastBtcUSD: 92400,
  lastBtcTime: null,
  crypto: [
    {symbol:'BTC', name:'Bitcoin',  qty:0.00353763, avgBuy:1408415000, costBase:4982154.91, retPct:3.96,   color:'#F7931A', active:true},
    {symbol:'ETH', name:'Ethereum', qty:0,          avgBuy:0,          costBase:0,          retPct:31.42,  color:'#627EEA', active:false},
    {symbol:'SOL', name:'Solana',   qty:0,          avgBuy:0,          costBase:0,          retPct:6.19,   color:'#9945FF', active:false},
    {symbol:'USDT',name:'Tether',   qty:0,          avgBuy:0,          costBase:0,          retPct:4.47,   color:'#26A17B', active:false},
    {symbol:'XRP', name:'XRP',      qty:0,          avgBuy:0,          costBase:0,          retPct:18.99,  color:'#00AAE4', active:false},
  ],
  idx: [
    {symbol:'BACH',name:'Bank China Const.',qty:0,avgBuy:560.67, costBase:0,retPct:1.30,  color:'#E53E3E',active:false},
    {symbol:'WBSA',name:'WBS Asia',         qty:0,avgBuy:168.00, costBase:0,retPct:285.94,color:'#3182CE',active:false},
  ],
  chartLabels:['Jul\'24','Sep\'24','Nov\'24','Feb\'25','May\'25','Jul\'25','Oct\'25','Jan\'26','Apr\'26','Jul\'26','Oct\'26'],
  chartValues:[2800000,3100000,4050000,4400000,5200000,4700000,4850000,5100000,5400000,5300000,5196473],
};

// ─── CHART PERIOD DATA ───
const CHART_PERIODS = {
  today: {
    labels:['00:00','02:00','04:00','06:00','08:00','10:00','12:00','14:00','16:00','18:00','20:00','Now'],
    values:[5180000,5175000,5168000,5172000,5185000,5192000,5188000,5195000,5199000,5201000,5198000,5196473],
    range:'24/10/2026',
    sub:'Today · IDR'
  },
  '7d': {
    labels:['18 Okt','19 Okt','20 Okt','21 Okt','22 Okt','23 Okt','24 Okt'],
    values:[5120000,5085000,5140000,5160000,5175000,5188000,5196473],
    range:'18/10/2026 – 24/10/2026',
    sub:'7 Hari · IDR'
  },
  '12m': {
    labels:['Nov\'25','Des\'25','Jan\'26','Feb\'26','Mar\'26','Apr\'26','Mei\'26','Jun\'26','Jul\'26','Agu\'26','Sep\'26','Okt\'26'],
    values:[4950000,5050000,5100000,5150000,5250000,5400000,5350000,5280000,5300000,5250000,5220000,5196473],
    range:'24/10/2025 – 24/10/2026',
    sub:'12 Bulan · IDR'
  },
  ytd: {
    labels:['Jan\'26','Feb\'26','Mar\'26','Apr\'26','Mei\'26','Jun\'26','Jul\'26','Agu\'26','Sep\'26','Okt\'26'],
    values:[5100000,5150000,5250000,5400000,5350000,5280000,5300000,5250000,5220000,5196473],
    range:'01/01/2026 – 24/10/2026',
    sub:'Year to Date · IDR'
  },
  fy: {
    labels:['Jul\'25','Agu\'25','Sep\'25','Okt\'25','Nov\'25','Des\'25','Jan\'26','Feb\'26','Mar\'26','Apr\'26','Mei\'26','Jun\'26','Jul\'26','Agu\'26','Sep\'26','Okt\'26'],
    values:[4700000,4780000,4820000,4850000,4950000,5050000,5100000,5150000,5250000,5400000,5350000,5280000,5300000,5250000,5220000,5196473],
    range:'01/07/2025 – 24/10/2026',
    sub:'Financial Year · IDR'
  },
  all: {
    labels:['Jul\'24','Sep\'24','Nov\'24','Feb\'25','Mei\'25','Jul\'25','Okt\'25','Jan\'26','Apr\'26','Jul\'26','Okt\'26'],
    values:[2800000,3100000,4050000,4400000,5200000,4700000,4850000,5100000,5400000,5300000,5196473],
    range:'10/07/2024 – 24/10/2026',
    sub:'Semua Waktu · IDR'
  }
};

// ─── STATE ───
let S = loadS();
let editMode = false;
let btcIDR = S.lastBtcIDR || DEF.lastBtcIDR;
let btcUSD = S.lastBtcUSD || DEF.lastBtcUSD;
let chart = null;
let activePeriod = 'all';

function loadS(){
  try{
    const raw = JSON.parse(localStorage.getItem(SK));
    if(!raw) return JSON.parse(JSON.stringify(DEF));
    return Object.assign(JSON.parse(JSON.stringify(DEF)),raw,
      {crypto:raw.crypto||DEF.crypto,idx:raw.idx||DEF.idx});
  }catch(e){ return JSON.parse(JSON.stringify(DEF)); }
}
function saveS(){ try{localStorage.setItem(SK,JSON.stringify(S));}catch(e){} }

// ─── PRICE FETCH ───
async function fetchPrice(){
  setStatus('offline','Fetching…');
  // Try CoinGecko (IDR native)
  try{
    const r = await fetch('https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=idr,usd',
      {signal:AbortSignal.timeout(7000)});
    if(r.ok){
      const d=await r.json();
      if(d.bitcoin){
        btcIDR=d.bitcoin.idr; btcUSD=d.bitcoin.usd;
        persistPrice(); showPrice('live'); recalc(); return;
      }
    }
  }catch(e){}
  // Try Binance
  try{
    const r=await fetch('https://api.binance.com/api/v3/ticker/price?symbol=BTCUSDT',
      {signal:AbortSignal.timeout(7000)});
    if(r.ok){
      const d=await r.json();
      btcUSD=parseFloat(d.price);
      btcIDR=Math.round(btcUSD*S.usdIdrRate);
      persistPrice(); showPrice('live'); recalc(); return;
    }
  }catch(e){}
  // Fallback
  if(S.lastBtcIDR){btcIDR=S.lastBtcIDR;btcUSD=S.lastBtcUSD;showPrice('cached');recalc();}
  else{btcIDR=DEF.lastBtcIDR;btcUSD=DEF.lastBtcUSD;showPrice('offline');recalc();}
}

function persistPrice(){
  S.lastBtcIDR=btcIDR; S.lastBtcUSD=btcUSD;
  S.lastBtcTime=new Date().toISOString(); saveS();
}

function showPrice(status){
  document.getElementById('btcIDR').textContent=fIDR(btcIDR);
  document.getElementById('btcUSD').textContent='$'+btcUSD.toLocaleString('en-US',{minimumFractionDigits:2,maximumFractionDigits:2});
  document.getElementById('btcTs').textContent=S.lastBtcTime
    ?'Updated '+new Date(S.lastBtcTime).toLocaleTimeString('id-ID',{hour:'2-digit',minute:'2-digit'}):'—';
  setStatus(status,{live:'LIVE',cached:'CACHED',offline:'OFFLINE'}[status]);
}

function setStatus(st,txt){
  const p=document.getElementById('pStatus'),d=document.getElementById('sDot'),s=document.getElementById('sText');
  p.className='spill '+st;
  d.className='dot'+(st==='live'?' pulse':'');
  s.textContent=txt;
}

// ─── FORMAT ───
function fIDR(v){ return 'IDR '+Math.abs(v).toLocaleString('id-ID',{minimumFractionDigits:2,maximumFractionDigits:2}); }
function fRp(v){ return 'Rp '+Math.abs(v).toLocaleString('id-ID',{minimumFractionDigits:2,maximumFractionDigits:2}); }
function fPct(v){ const s=v>0?'+':v<0?'-':''; return s+Math.abs(v).toFixed(2)+'%'; }
function fQty(v,sym){
  if(!v||v===0) return '—';
  if(sym==='BTC'||sym==='ETH') return v.toFixed(8);
  if(sym==='SOL'||sym==='XRP') return v.toFixed(4);
  return v.toLocaleString('id-ID');
}

// ─── CALC & RENDER METRICS ───
function recalc(){
  const btc=S.crypto[0];
  const btcVal=btc.qty*btcIDR;
  const capAmt=btcVal-btc.costBase;
  const capPct=btc.costBase>0?(capAmt/btc.costBase)*100:1.13;
  const curPct=9.89, curAmt=718522.48;
  const totAmt=capAmt+curAmt;
  const totPct=btc.costBase>0?(totAmt/btc.costBase)*100:11.02;

  const g=(id,c)=>document.getElementById(id).className='m-val '+(c>=0?'pos':'neg');
  document.getElementById('mVal').textContent=fIDR(btcVal);
  g('mCap',capPct); document.getElementById('mCap').textContent=fPct(capPct);
  document.getElementById('mCapAmt').textContent=(capAmt>=0?'+':'')+fRp(capAmt);
  g('mCur',curPct); document.getElementById('mCur').textContent=fPct(curPct);
  document.getElementById('mCurAmt').textContent='+'+fRp(curAmt);
  g('mTot',totPct); document.getElementById('mTot').textContent=fPct(totPct);
  document.getElementById('mTotAmt').textContent=(totAmt>=0?'+':'')+fRp(totAmt);

  // Update last chart point for active period
  if(chart){
    const pd=CHART_PERIODS[activePeriod];
    const updated=[...(pd?pd.values:(S.chartValues||DEF.chartValues))];
    updated[updated.length-1]=Math.round(btcVal)||updated[updated.length-1];
    chart.data.datasets[0].data=updated;
    chart.update('none');
  }

  renderTables();
}

// ─── TABLES ───
function renderTables(){
  const btcVal=S.crypto[0].qty*btcIDR;

  // CRYPTO
  let ch='';
  S.crypto.forEach((a,i)=>{
    const val=a.symbol==='BTC'?btcVal:0;
    const rc=a.retPct>=0?'pos':'neg';
    if(editMode){
      ch+=`<tr>
        <td><div class="asset"><div class="aicon" style="background:${a.color}">${a.symbol.slice(0,2)}</div>
          <div><div class="aname">${a.symbol}</div><div class="afull">${a.name}</div></div></div></td>
        <td><input class="e-input" data-t="crypto" data-i="${i}" data-f="avgBuy" value="${a.avgBuy||0}" type="number"></td>
        <td><input class="e-input" data-t="crypto" data-i="${i}" data-f="qty" value="${a.qty}" type="number" step="0.00000001"></td>
        <td class="mono">${a.active?fIDR(val):'<span class="closed">CLOSED</span>'}</td>
        <td><input class="e-input" data-t="crypto" data-i="${i}" data-f="retPct" value="${a.retPct}" type="number" step="0.01" style="width:80px;"></td>
      </tr>`;
    } else {
      ch+=`<tr>
        <td><div class="asset"><div class="aicon" style="background:${a.color}">${a.symbol.slice(0,2)}</div>
          <div><div class="aname">${a.symbol}</div><div class="afull">${a.name}</div></div></div></td>
        <td class="mono">${a.avgBuy?'IDR '+a.avgBuy.toLocaleString('id-ID'):'—'}</td>
        <td class="mono">${a.qty?fQty(a.qty,a.symbol):'<span class="closed">CLOSED</span>'}</td>
        <td class="mono">${a.active?fIDR(val):'—'}</td>
        <td><span class="rpill ${rc}">${fPct(a.retPct)}</span></td>
      </tr>`;
    }
  });
  document.getElementById('cBody').innerHTML=ch;
  document.getElementById('cFoot').innerHTML=`<tr class="tot-row">
    <td colspan="3" style="font-weight:700;">Total Crypto</td>
    <td class="mono">${fIDR(btcVal)}</td><td></td></tr>`;

  // IDX
  let ih='';
  S.idx.forEach((a,i)=>{
    const rc=a.retPct>=0?'pos':'neg';
    if(editMode){
      ih+=`<tr>
        <td><div class="asset"><div class="aicon" style="background:${a.color}">${a.symbol.slice(0,2)}</div>
          <div><div class="aname">${a.symbol}</div><div class="afull">${a.name}</div></div></div></td>
        <td><input class="e-input" data-t="idx" data-i="${i}" data-f="avgBuy" value="${a.avgBuy}" type="number" step="0.01"></td>
        <td><input class="e-input" data-t="idx" data-i="${i}" data-f="qty" value="${a.qty}" type="number"></td>
        <td><span class="closed">CLOSED</span></td>
        <td><input class="e-input" data-t="idx" data-i="${i}" data-f="retPct" value="${a.retPct}" type="number" step="0.01" style="width:80px;"></td>
      </tr>`;
    } else {
      ih+=`<tr>
        <td><div class="asset"><div class="aicon" style="background:${a.color}">${a.symbol.slice(0,2)}</div>
          <div><div class="aname">${a.symbol}</div><div class="afull">${a.name}</div></div></div></td>
        <td class="mono">IDR ${a.avgBuy.toLocaleString('id-ID',{minimumFractionDigits:2})}</td>
        <td><span class="closed">CLOSED</span></td>
        <td>—</td>
        <td><span class="rpill ${rc}">${fPct(a.retPct)}</span></td>
      </tr>`;
    }
  });
  document.getElementById('iBody').innerHTML=ih;
  const wbsaRet=S.idx[1]?S.idx[1].retPct:285.94;
  document.getElementById('iFoot').innerHTML=`<tr class="tot-row">
    <td colspan="3" style="font-weight:700;">Total IDX</td>
    <td>—</td>
    <td><span class="rpill pos">Avg +143.62%</span></td></tr>`;
}

// ─── SWITCH PERIOD ───
function switchPeriod(p){
  activePeriod=p;
  const pd=CHART_PERIODS[p];
  if(!pd||!chart) return;
  const vals=[...pd.values];
  const live=Math.round(S.crypto[0].qty*btcIDR);
  if(live) vals[vals.length-1]=live;
  chart.data.labels=pd.labels;
  chart.data.datasets[0].data=vals;
  chart.update();
  document.getElementById('dateRange').textContent=pd.range;
  document.getElementById('chartSub').textContent=pd.sub;
}

// ─── CHART ───
function initChart(){
  const canvas=document.getElementById('pfChart');
  const ctx=canvas.getContext('2d');
  const pd=CHART_PERIODS.all;
  const labels=pd.labels;
  const values=[...pd.values];
  values[values.length-1]=Math.round(S.crypto[0].qty*btcIDR)||values[values.length-1];

  const grad=ctx.createLinearGradient(0,0,0,180);
  grad.addColorStop(0,'rgba(16,217,145,.2)');
  grad.addColorStop(1,'rgba(16,217,145,0)');

  chart=new Chart(ctx,{
    type:'line',
    data:{
      labels,
      datasets:[{
        data:values,
        borderColor:'#10d991',
        backgroundColor:grad,
        borderWidth:2,
        pointRadius:3,
        pointBackgroundColor:'#10d991',
        pointBorderColor:'transparent',
        pointHoverRadius:5,
        tension:0.38,
        fill:true,
      }]
    },
    options:{
      responsive:true,maintainAspectRatio:false,
      interaction:{mode:'index',intersect:false},
      plugins:{
        legend:{display:false},
        tooltip:{
          backgroundColor:'#12162a',borderColor:'#1f2440',borderWidth:1,
          titleColor:'#7a88b0',bodyColor:'#dde3f4',
          callbacks:{label:c=>'IDR '+c.raw.toLocaleString('id-ID')}
        }
      },
      scales:{
        x:{grid:{color:'#1f2440'},ticks:{color:'#7a88b0',font:{size:11}}},
        y:{grid:{color:'#1f2440'},position:'right',
          ticks:{color:'#7a88b0',font:{size:11},callback:v=>'IDR '+(v/1e6).toFixed(1)+'M'}}
      }
    }
  });
}

// ─── EDIT ───
function setEdit(on){
  editMode=on;
  document.getElementById('editBar').hidden=!on;
  const eb=document.getElementById('editBtn');
  eb.innerHTML=on
    ?'<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg> Selesai Edit'
    :'<svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg> Edit';
  renderTables();
}

function saveEdits(){
  document.querySelectorAll('[data-t]').forEach(inp=>{
    const t=inp.dataset.t,i=+inp.dataset.i,f=inp.dataset.f;
    const v=parseFloat(inp.value);
    if(!isNaN(v)) S[t][i][f]=v;
  });
  S.crypto[0].active=S.crypto[0].qty>0;
  saveS(); setEdit(false); recalc();
  toast('Portfolio disimpan ✓','ok');
}

// ─── TOAST ───
let tT;
function toast(msg,type=''){
  const el=document.getElementById('toast');
  el.textContent=msg; el.className='toast show'+(type?' '+type:'');
  clearTimeout(tT); tT=setTimeout(()=>{el.className='toast';},2500);
}

// ─── THEME ───
function toggleTheme(){
  const r=document.documentElement;
  const n=r.getAttribute('data-theme')==='light'?'dark':'light';
  r.setAttribute('data-theme',n);
  document.getElementById('themeBtn').textContent=n==='dark'?'☀️':'🌙';
  try{localStorage.setItem('iqbal_theme',n);}catch(e){}
}

// ─── EVENTS ───
document.getElementById('editBtn').addEventListener('click',()=>setEdit(!editMode));
document.getElementById('saveBtn').addEventListener('click',saveEdits);
document.getElementById('cancelBtn').addEventListener('click',()=>setEdit(false));
document.getElementById('themeBtn').addEventListener('click',toggleTheme);
document.getElementById('refreshBtn').addEventListener('click',()=>{setStatus('offline','Fetching…');fetchPrice();toast('Memperbarui harga…');});
document.getElementById('rateBtn').addEventListener('click',()=>{
  const v=parseFloat(document.getElementById('rateInput').value);
  if(!isNaN(v)&&v>1000){S.usdIdrRate=v;saveS();fetchPrice();toast('Rate USD/IDR diperbarui');}
});
document.querySelectorAll('.dchip').forEach(c=>c.addEventListener('click',function(){
  document.querySelectorAll('.dchip').forEach(x=>x.classList.remove('active'));
  this.classList.add('active');
  switchPeriod(this.dataset.p);
}));

// ─── INIT ───
(function init(){
  try{
    const t=localStorage.getItem('iqbal_theme');
    if(t){document.documentElement.setAttribute('data-theme',t);
      document.getElementById('themeBtn').textContent=t==='dark'?'☀️':'🌙';}
  }catch(e){}
  document.getElementById('rateInput').value=S.usdIdrRate||15900;
  // Show cached first
  if(S.lastBtcIDR){btcIDR=S.lastBtcIDR;btcUSD=S.lastBtcUSD;showPrice('cached');}
  else{btcIDR=DEF.lastBtcIDR;btcUSD=DEF.lastBtcUSD;showPrice('offline');}
  initChart();
  recalc();
  // Fetch live
  fetchPrice();
  setInterval(fetchPrice,60000);
})();
</script>
