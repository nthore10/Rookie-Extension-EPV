---
layout: null
---
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rookie Scale Extension EPV</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{--primary:#0A0A0A;--accent:#C8102E;--accent-light:#FFF0F2;--surface:#FFFFFF;--surface-2:#F5F4F0;--surface-3:#EDECEA;--ink:#0A0A0A;--ink-secondary:#5A5A5A;--ink-muted:#9A9A9A;--border:rgba(0,0,0,0.10);--border-strong:rgba(0,0,0,0.22);--success:#1A7A4A;--success-bg:#EBF8F1;--info:#1E5FA8;--info-bg:#EBF2FC;--warning:#A06B00;--warning-bg:#FEF6E0;--font-display:'Bebas Neue',sans-serif;--font-body:'DM Sans',sans-serif;--font-mono:'DM Mono',monospace;}
  *{margin:0;padding:0;box-sizing:border-box;}
  body{font-family:var(--font-body);background:var(--surface-2);color:var(--ink);min-height:100vh;}
  .masthead{background:var(--primary);padding:20px 24px 18px;display:flex;align-items:center;justify-content:center;text-align:center;border-bottom:3px solid var(--accent);}
  .masthead-wordmark{font-family:var(--font-display);font-size:32px;color:#fff;letter-spacing:1.5px;line-height:1;}
  .masthead-wordmark span{color:var(--accent);}
  .masthead-sub{font-family:var(--font-mono);font-size:10px;color:rgba(255,255,255,0.45);letter-spacing:2px;padding-bottom:3px;}
  .controls{display:flex;gap:10px;padding:14px 24px;background:var(--surface);border-bottom:1px solid var(--border);flex-wrap:wrap;align-items:center;}
  .ctrl-label{font-family:var(--font-mono);font-size:9px;letter-spacing:2px;text-transform:uppercase;color:var(--ink-muted);}
  .controls select,.controls input{font-family:var(--font-body);font-size:13px;padding:7px 11px;border:1px solid var(--border-strong);border-radius:6px;background:var(--surface);color:var(--ink);outline:none;transition:border-color .15s;}
  .controls select:focus,.controls input:focus{border-color:var(--accent);}
  .controls input[type="text"]{width:180px;}
  .controls button{font-family:var(--font-body);font-size:12px;font-weight:600;padding:7px 14px;border-radius:6px;border:1.5px solid var(--border-strong);background:var(--surface);color:var(--ink);cursor:pointer;transition:all .15s;}
  .controls button:hover{background:var(--primary);color:#fff;border-color:var(--primary);}
  .ctrl-group{display:flex;align-items:center;gap:6px;}
  .summary-bar{display:flex;gap:24px;padding:13px 24px;background:var(--surface);border-bottom:1px solid var(--border);flex-wrap:wrap;}
  .sum-stat{display:flex;flex-direction:column;gap:2px;}
  .sum-label{font-family:var(--font-mono);font-size:8px;letter-spacing:2px;text-transform:uppercase;color:var(--ink-muted);}
  .sum-value{font-family:var(--font-display);font-size:20px;color:var(--ink);line-height:1;}
  .table-wrap{overflow-x:auto;}
  table{width:100%;border-collapse:collapse;font-size:13px;min-width:1000px;}
  thead th{background:var(--primary);color:rgba(255,255,255,0.55);font-family:var(--font-mono);font-weight:500;font-size:9px;text-transform:uppercase;letter-spacing:2px;padding:12px 13px;text-align:left;border-bottom:2px solid var(--accent);position:sticky;top:0;z-index:10;cursor:pointer;user-select:none;white-space:nowrap;transition:color .15s;}
  thead th:hover{color:#fff;}
  thead th.sorted-asc::after{content:' ▲';color:var(--accent);font-size:8px;}
  thead th.sorted-desc::after{content:' ▼';color:var(--accent);font-size:8px;}
  thead th.col-right{text-align:right;}
  tbody tr{border-bottom:1px solid var(--border);background:var(--surface);transition:background .1s;}
  tbody tr:hover{background:var(--surface-2);}
  td{padding:10px 13px;vertical-align:middle;white-space:nowrap;}
  td.col-right{text-align:right;font-family:var(--font-mono);font-size:12px;}
  .player-name{font-weight:600;color:var(--ink);}
  .pos-badge{display:inline-block;padding:2px 7px;border-radius:3px;font-size:9px;font-weight:500;font-family:var(--font-mono);letter-spacing:1px;text-transform:uppercase;background:var(--info-bg);color:var(--info);min-width:28px;text-align:center;}
  .team-cell{display:flex;align-items:center;gap:8px;}
  .team-logo{width:22px;height:22px;object-fit:contain;flex-shrink:0;}
  .team-name-sm{color:var(--ink-muted);font-size:12px;font-family:var(--font-mono);}
  .money{font-family:var(--font-mono);font-variant-numeric:tabular-nums;}
  .money.positive{color:var(--success);font-weight:600;}
  .money.negative{color:var(--accent);font-weight:600;}
  .money.neutral{color:var(--ink);}
  .loading{text-align:center;padding:80px 20px;}
  .spinner{width:36px;height:36px;border:3px solid var(--surface-3);border-top:3px solid var(--accent);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 14px;}
  @keyframes spin{to{transform:rotate(360deg);}}
  .loading p{font-family:var(--font-mono);font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--ink-muted);}
  .refresh-btn{position:fixed;bottom:20px;right:20px;background:var(--accent);color:#fff;border:none;padding:10px 20px;border-radius:6px;font-family:var(--font-mono);font-size:9px;letter-spacing:2px;text-transform:uppercase;cursor:pointer;box-shadow:0 4px 16px rgba(200,16,46,0.25);z-index:100;}
  @media(max-width:768px){td,thead th{padding:8px 10px;}.team-logo{width:18px;height:18px;}}
</style>
</head>
<body>

<div class="masthead">
  <div class="masthead-wordmark">ROOKIE EXTENSION <span>EPV</span></div>
  
</div>

<div class="controls" id="controls"></div>
<div class="summary-bar" id="summary"></div>
<div class="table-wrap"><div id="app"><div class="loading"><div class="spinner"></div><p>Fetching live data&hellip;</p></div></div></div>
<button class="refresh-btn" onclick="init()">&#8635; Refresh</button>

<script>
const TEAM_LOGOS={ATL:'https://cdn.nba.com/logos/nba/1610612737/primary/L/logo.svg',BOS:'https://cdn.nba.com/logos/nba/1610612738/primary/L/logo.svg',BKN:'https://cdn.nba.com/logos/nba/1610612751/primary/L/logo.svg',CHO:'https://cdn.nba.com/logos/nba/1610612766/primary/L/logo.svg',CHI:'https://cdn.nba.com/logos/nba/1610612741/primary/L/logo.svg',CLE:'https://cdn.nba.com/logos/nba/1610612739/primary/L/logo.svg',DAL:'https://cdn.nba.com/logos/nba/1610612742/primary/L/logo.svg',DEN:'https://cdn.nba.com/logos/nba/1610612743/primary/L/logo.svg',DET:'https://cdn.nba.com/logos/nba/1610612765/primary/L/logo.svg',GSW:'https://cdn.nba.com/logos/nba/1610612744/primary/L/logo.svg',HOU:'https://cdn.nba.com/logos/nba/1610612745/primary/L/logo.svg',IND:'https://cdn.nba.com/logos/nba/1610612754/primary/L/logo.svg',LAC:'https://cdn.nba.com/logos/nba/1610612746/primary/L/logo.svg',LAL:'https://cdn.nba.com/logos/nba/1610612747/primary/L/logo.svg',MEM:'https://cdn.nba.com/logos/nba/1610612763/primary/L/logo.svg',MIA:'https://cdn.nba.com/logos/nba/1610612748/primary/L/logo.svg',MIL:'https://cdn.nba.com/logos/nba/1610612749/primary/L/logo.svg',MIN:'https://cdn.nba.com/logos/nba/1610612750/primary/L/logo.svg',NOP:'https://cdn.nba.com/logos/nba/1610612740/primary/L/logo.svg',NYK:'https://cdn.nba.com/logos/nba/1610612752/primary/L/logo.svg',OKC:'https://cdn.nba.com/logos/nba/1610612760/primary/L/logo.svg',ORL:'https://cdn.nba.com/logos/nba/1610612753/primary/L/logo.svg',PHI:'https://cdn.nba.com/logos/nba/1610612755/primary/L/logo.svg',PHX:'https://cdn.nba.com/logos/nba/1610612756/primary/L/logo.svg',POR:'https://cdn.nba.com/logos/nba/1610612757/primary/L/logo.svg',SAC:'https://cdn.nba.com/logos/nba/1610612758/primary/L/logo.svg',SAS:'https://cdn.nba.com/logos/nba/1610612759/primary/L/logo.svg',TOR:'https://cdn.nba.com/logos/nba/1610612761/primary/L/logo.svg',UTA:'https://cdn.nba.com/logos/nba/1610612762/primary/L/logo.svg',WAS:'https://cdn.nba.com/logos/nba/1610612764/primary/L/logo.svg'};

const CSV_URL='https://docs.google.com/spreadsheets/d/e/2PACX-1vRTwTOS_rNBYI8d8zDUivGFWXsXcxlOZgrqn5o-WCvFC5aNAR3vLsSqllE7aO0BRw/pub?gid=1927803434&single=true&output=csv';

let allRows=[],sortCol='EPV Annualized',sortAsc=false,filters={pos:'',team:'',search:''};

function parseMoney(s){if(!s||!s.trim()||s.trim()==='-')return null;let c=s.replace(/[$,"\s]/g,'');if(c.startsWith('(')&&c.endsWith(')'))c='-'+c.slice(1,-1);const n=parseFloat(c);return isNaN(n)?null:n;}
function fmt(n){if(n===null||n===undefined)return'—';const abs=Math.abs(n);const s='$'+abs.toLocaleString('en-US',{maximumFractionDigits:0});return n<0?'('+s+')':s;}

function parseCSVLine(line){const r=[];let cur='',inQ=false;for(let i=0;i<line.length;i++){const c=line[i];if(inQ){if(c==='"'&&line[i+1]==='"'){cur+='"';i++;}else if(c==='"')inQ=false;else cur+=c;}else{if(c==='"')inQ=true;else if(c===','){r.push(cur);cur='';}else cur+=c;}}r.push(cur);return r;}

async function init(){
  document.getElementById('app').innerHTML='<div class="loading"><div class="spinner"></div><p>Fetching live data&hellip;</p></div>';
  document.getElementById('controls').innerHTML='';document.getElementById('summary').innerHTML='';
  try{
    const resp=await fetch(CSV_URL);
    if(!resp.ok)throw new Error('HTTP '+resp.status);
    const text=await resp.text();
    if(text.trim().startsWith('<'))throw new Error('Sheet not published');
    const lines=text.trim().split('\n');
    const headers=parseCSVLine(lines[0]);
    allRows=[];
    for(let i=1;i<lines.length;i++){
      const vals=parseCSVLine(lines[i]);
      if(!vals[0]||!vals[0].trim())continue;
      const row={};headers.forEach((h,j)=>row[h.trim()]=vals[j]?.trim()||'');
      allRows.push(row);
    }
    buildControls();render();
  }catch(e){
    document.getElementById('app').innerHTML=`<div style="text-align:center;padding:60px;color:var(--accent);font-family:var(--font-mono);font-size:11px;letter-spacing:2px">Error: ${e.message}<br><br>Make sure the Google Sheet is published to the web.</div>`;
  }
}

function buildControls(){
  const positions=[...new Set(allRows.map(r=>r['Position']||r['Pos']||'').filter(Boolean))].sort();
  const teams=[...new Set(allRows.map(r=>r['Team']||'').filter(Boolean))].sort();
  document.getElementById('controls').innerHTML=`
    <div class="ctrl-group"><span class="ctrl-label">Position</span>
      <select onchange="filters.pos=this.value;render()"><option value="">All</option>${positions.map(p=>`<option>${p}</option>`).join('')}</select></div>
    <div class="ctrl-group"><span class="ctrl-label">Team</span>
      <select onchange="filters.team=this.value;render()"><option value="">All</option>${teams.map(t=>`<option>${t}</option>`).join('')}</select></div>
    <div class="ctrl-group"><span class="ctrl-label">Search</span>
      <input type="text" placeholder="Player name..." oninput="filters.search=this.value;render()"></div>
    <button onclick="filters={pos:'',team:'',search:''};document.querySelectorAll('#controls select,#controls input').forEach(e=>e.value='');render()">Reset</button>`;
}

const COLS=['Player','Position','Team','EPV Annualized','Extension Value (Ann.)','Over/Under (Ann.)'];

function getFiltered(){
  return allRows.filter(r=>{
    const pos=r['Position']||r['Pos']||'';
    if(filters.pos&&pos!==filters.pos)return false;
    if(filters.team&&(r['Team']||'')!==filters.team)return false;
    if(filters.search&&!(r['Player']||'').toLowerCase().includes(filters.search.toLowerCase()))return false;
    return true;
  });
}

function render(){
  const data=[...getFiltered()].sort((a,b)=>{
    let av=a[sortCol],bv=b[sortCol];
    const an=parseMoney(av),bn=parseMoney(bv);
    if(an!==null&&bn!==null)return sortAsc?an-bn:bn-an;
    av=(av||'').toLowerCase();bv=(bv||'').toLowerCase();
    return sortAsc?av.localeCompare(bv):bv.localeCompare(av);
  });

  let totalEPV=0,totalExt=0,totalOU=0;
  data.forEach(r=>{
    const epv=parseMoney(r['EPV Annualized']);const ext=parseMoney(r['Extension Value (Ann.)']);const ou=parseMoney(r['Over/Under (Ann.)']);
    if(epv!==null)totalEPV+=epv;if(ext!==null)totalExt+=ext;if(ou!==null)totalOU+=ou;
  });
  document.getElementById('summary').innerHTML=`
    <div class="sum-stat"><div class="sum-label">Players</div><div class="sum-value">${data.length}</div></div>
    <div class="sum-stat"><div class="sum-label">Total EPV</div><div class="sum-value">${fmt(totalEPV)}</div></div>
    <div class="sum-stat"><div class="sum-label">Total Extension Value</div><div class="sum-value">${fmt(totalExt)}</div></div>
    <div class="sum-stat"><div class="sum-label">Net Over/Under</div><div class="sum-value" style="color:${totalOU>=0?'var(--success)':'var(--accent)'}">${fmt(totalOU)}</div></div>`;

  const thHTML=COLS.map(c=>{
    const cls=c===sortCol?(sortAsc?'sorted-asc':'sorted-desc'):'';
    const right=['EPV Annualized','Extension Value (Ann.)','Over/Under (Ann.)'].includes(c)?'col-right':'';
    return`<th class="${cls} ${right}" onclick="sortBy('${c}')">${c}</th>`;
  }).join('');

  const tbody=data.map(r=>{
    const player=r['Player']||'';const pos=r['Position']||r['Pos']||'';const team=r['Team']||'';
    const epv=parseMoney(r['EPV Annualized']);const ext=parseMoney(r['Extension Value (Ann.)']);const ou=parseMoney(r['Over/Under (Ann.)']);
    const logo=TEAM_LOGOS[team]||'';
    const ouClass=ou===null?'neutral':ou>0?'positive':ou<0?'negative':'neutral';
    return`<tr>
      <td><span class="player-name">${player}</span></td>
      <td><span class="pos-badge">${pos||'—'}</span></td>
      <td><div class="team-cell">${logo?`<img src="${logo}" alt="${team}" class="team-logo">`:''}
        <span class="team-name-sm">${team}</span></div></td>
      <td class="col-right money neutral">${fmt(epv)}</td>
      <td class="col-right money neutral">${fmt(ext)}</td>
      <td class="col-right money ${ouClass}">${fmt(ou)}</td>
    </tr>`;
  }).join('');

  document.getElementById('app').innerHTML=`<table><thead><tr>${thHTML}</tr></thead><tbody>${tbody||'<tr><td colspan="6" style="text-align:center;padding:40px;color:var(--ink-muted)">No players found</td></tr>'}</tbody></table>`;
}

function sortBy(col){if(sortCol===col)sortAsc=!sortAsc;else{sortCol=col;sortAsc=false;}render();}

init();
</script>
</body>
</html>
