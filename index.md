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
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root{--bg-base:#1E2228;--bg-raised:#252A31;--bg-panel:#22272E;--bg-row-hover:#262C33;--bg-input:#2A3038;--accent:#00D89A;--accent-dark:#00A878;--text-bright:#F2F4F7;--text-primary:#C8D1DC;--text-muted:#9AA6B4;--text-dim:#7A8694;--text-faint:#5E6873;--border:#2E343D;--border-soft:#282E35;--border-input:#353C46;--bar-hot:#FF6B85;--bar-warm:#FFB454;--bar-cool:#00D89A;--positive:#00D89A;--negative:#FF6B85;--font-display:'Space Grotesk',sans-serif;--font-mono:'Space Mono',monospace;}
  *{margin:0;padding:0;box-sizing:border-box;}
  body{font-family:var(--font-display);background:var(--bg-base);color:var(--text-primary);min-height:100vh;}
  .tm-header{padding:20px 24px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--border);background:var(--bg-raised);flex-wrap:wrap;gap:16px;}
  .tm-title-wrap{display:flex;align-items:center;gap:14px;}
  .tm-badge{width:38px;height:38px;border-radius:8px;background:var(--accent);display:flex;align-items:center;justify-content:center;font-family:var(--font-mono);font-weight:700;font-size:13px;color:var(--bg-base);}
  .tm-title{font-family:var(--font-display);font-weight:700;font-size:19px;color:var(--text-bright);letter-spacing:-0.3px;line-height:1;}
  .tm-title-sub{font-family:var(--font-mono);font-size:10px;color:var(--text-dim);letter-spacing:1px;margin-top:3px;}
  .tm-meta{display:flex;gap:24px;}
  .tm-meta-item{text-align:right;}
  .tm-meta-label{font-family:var(--font-mono);font-size:8px;letter-spacing:1.5px;text-transform:uppercase;color:var(--text-dim);}
  .tm-meta-value{font-family:var(--font-display);font-weight:700;font-size:17px;color:var(--accent);margin-top:2px;line-height:1;}
  .tm-controls{display:flex;gap:10px;padding:12px 24px;background:var(--bg-panel);border-bottom:1px solid var(--border);flex-wrap:wrap;align-items:center;}
  .ctrl-group{display:flex;flex-direction:column;}
  .ctrl-label{font-family:var(--font-mono);font-size:8px;letter-spacing:1.5px;text-transform:uppercase;color:var(--text-dim);margin-bottom:4px;}
  .tm-controls select,.tm-controls input{font-family:var(--font-mono);font-size:12px;padding:7px 11px;border:1px solid var(--border-input);border-radius:6px;background:var(--bg-input);color:var(--text-bright);outline:none;transition:border-color .15s;}
  .tm-controls select:focus,.tm-controls input:focus{border-color:var(--accent);}
  .tm-controls input[type="text"]{min-width:170px;}.tm-controls input::placeholder{color:var(--text-faint);}
  .reset-btn{align-self:flex-end;font-family:var(--font-mono);font-size:9px;letter-spacing:1.5px;text-transform:uppercase;padding:8px 14px;border:1px solid var(--border-input);background:var(--bg-input);color:var(--text-muted);border-radius:6px;cursor:pointer;transition:all .15s;}
  .reset-btn:hover{border-color:var(--accent);color:var(--text-bright);}
  .loading{text-align:center;padding:80px 20px;}
  .spinner{width:34px;height:34px;border:3px solid var(--border);border-top:3px solid var(--accent);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 14px;}
  @keyframes spin{to{transform:rotate(360deg);}}
  .loading p{font-family:var(--font-mono);font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--text-dim);}
  .table-wrap{overflow-x:auto;}
  table{width:100%;border-collapse:collapse;min-width:950px;}
  thead th{background:var(--bg-raised);color:var(--text-dim);font-family:var(--font-mono);font-size:9px;text-transform:uppercase;letter-spacing:1.5px;padding:12px 14px;text-align:left;border-bottom:1px solid var(--border);position:sticky;top:0;z-index:10;cursor:pointer;user-select:none;white-space:nowrap;transition:color .15s;font-weight:400;}
  thead th:hover{color:var(--accent);}
  thead th.sorted-asc::after{content:' ▲';color:var(--accent);font-size:8px;}
  thead th.sorted-desc::after{content:' ▼';color:var(--accent);font-size:8px;}
  thead th.col-right{text-align:right;}
  tbody tr{border-bottom:1px solid var(--border-soft);background:var(--bg-base);transition:background .12s;}
  tbody tr:hover{background:var(--bg-row-hover);}
  td{padding:10px 14px;vertical-align:middle;white-space:nowrap;font-family:var(--font-mono);font-size:12px;color:var(--text-primary);}
  td.col-right{text-align:right;}
  .player-name{font-family:var(--font-display);font-weight:600;font-size:13px;color:var(--text-bright);}
  .pos-badge{display:inline-block;padding:2px 7px;border-radius:3px;font-size:8px;font-weight:400;font-family:var(--font-mono);letter-spacing:1px;text-transform:uppercase;background:rgba(0,216,154,0.12);color:var(--accent);min-width:28px;text-align:center;}
  .team-cell{display:flex;align-items:center;gap:8px;}
  .team-logo{width:24px;height:24px;object-fit:contain;flex-shrink:0;}
  .team-name-sm{color:var(--text-dim);font-size:11px;font-family:var(--font-mono);}
  .money.positive{color:var(--positive);font-weight:700;}
  .money.negative{color:var(--negative);font-weight:700;}
  .money.neutral{color:var(--text-primary);}
  .tm-footer{padding:13px 24px;font-family:var(--font-mono);font-size:9px;letter-spacing:1.5px;color:var(--text-faint);text-transform:uppercase;background:var(--bg-panel);border-top:1px solid var(--border);display:flex;justify-content:space-between;}
  .refresh-btn{position:fixed;bottom:20px;right:20px;background:var(--accent);color:var(--bg-base);border:none;padding:10px 18px;border-radius:6px;font-family:var(--font-mono);font-size:9px;letter-spacing:2px;text-transform:uppercase;font-weight:700;cursor:pointer;box-shadow:0 4px 16px rgba(0,0,0,0.4);z-index:100;}
  @media(max-width:768px){.tm-header{padding:16px;}}
  ::-webkit-scrollbar{width:7px;height:7px;}::-webkit-scrollbar-track{background:var(--bg-base);}::-webkit-scrollbar-thumb{background:var(--border);border-radius:4px;}
</style>
</head>
<body>

<div class="tm-header">
  <div class="tm-title-wrap">
    <div class="tm-badge">RX</div>
    <div>
      <div class="tm-title">Rookie Extension EPV</div>
      <div class="tm-title-sub">// Projected value vs. extension terms</div>
    </div>
  </div>
  <div class="tm-meta">
    <div class="tm-meta-item"><div class="tm-meta-label">Players</div><div class="tm-meta-value" id="kpiPlayers">0</div></div>
    <div class="tm-meta-item"><div class="tm-meta-label">Net Over/Under</div><div class="tm-meta-value" id="kpiNet">$0</div></div>
  </div>
</div>

<div class="tm-controls" id="controls"></div>
<div class="table-wrap"><div id="app"><div class="loading"><div class="spinner"></div><p>Fetching live data&hellip;</p></div></div></div>

<div class="tm-footer">
  <span>Source · Live Workbook</span>
  <span>Updated Daily</span>
</div>
<button class="refresh-btn" onclick="init()">&#8635; Refresh</button>

<script>
const nbaIds={ATL:1610612737,BOS:1610612738,BKN:1610612751,CHO:1610612766,CHI:1610612741,CLE:1610612739,DAL:1610612742,DEN:1610612743,DET:1610612765,GSW:1610612744,HOU:1610612745,IND:1610612754,LAC:1610612746,LAL:1610612747,MEM:1610612763,MIA:1610612748,MIL:1610612749,MIN:1610612750,NOP:1610612740,NYK:1610612752,OKC:1610612760,ORL:1610612753,PHI:1610612755,PHX:1610612756,POR:1610612757,SAC:1610612758,SAS:1610612759,TOR:1610612761,UTA:1610612762,WAS:1610612764};
function logoUrl(code){const id=nbaIds[code];return id?`https://cdn.nba.com/logos/nba/${id}/primary/L/logo.svg`:'';}

const CSV_URL='https://docs.google.com/spreadsheets/d/e/2PACX-1vRTwTOS_rNBYI8d8zDUivGFWXsXcxlOZgrqn5o-WCvFC5aNAR3vLsSqllE7aO0BRw/pub?gid=1927803434&single=true&output=csv';
let allRows=[],sortCol='EPV Annualized',sortAsc=false,filters={pos:'',team:'',search:''};

function parseMoney(s){if(!s||!s.trim()||s.trim()==='-')return null;let c=s.replace(/[$,"\s]/g,'');if(c.startsWith('(')&&c.endsWith(')'))c='-'+c.slice(1,-1);const n=parseFloat(c);return isNaN(n)?null:n;}
function fmt(n){if(n===null||n===undefined)return'—';const abs=Math.abs(n);const s='$'+abs.toLocaleString('en-US',{maximumFractionDigits:0});return n<0?'('+s+')':s;}
function fmtShort(n){if(n===null)return'$0';return(n<0?'-$':'$')+(Math.abs(n)/1e6).toFixed(1)+'M';}
function parseCSVLine(line){const r=[];let cur='',inQ=false;for(let i=0;i<line.length;i++){const c=line[i];if(inQ){if(c==='"'&&line[i+1]==='"'){cur+='"';i++;}else if(c==='"')inQ=false;else cur+=c;}else{if(c==='"')inQ=true;else if(c===','){r.push(cur);cur='';}else cur+=c;}}r.push(cur);return r;}

async function init(){
  document.getElementById('app').innerHTML='<div class="loading"><div class="spinner"></div><p>Fetching live data&hellip;</p></div>';
  document.getElementById('controls').innerHTML='';
  try{
    const resp=await fetch(CSV_URL);if(!resp.ok)throw new Error('HTTP '+resp.status);
    const text=await resp.text();if(text.trim().startsWith('<'))throw new Error('Sheet not published');
    const lines=text.trim().split('\n');const headers=parseCSVLine(lines[0]);
    allRows=[];for(let i=1;i<lines.length;i++){const vals=parseCSVLine(lines[i]);if(!vals[0]||!vals[0].trim())continue;const row={};headers.forEach((h,j)=>row[h.trim()]=vals[j]?.trim()||'');allRows.push(row);}
    buildControls();render();
  }catch(e){document.getElementById('app').innerHTML=`<div style="text-align:center;padding:60px;color:var(--bar-hot);font-family:var(--font-mono);font-size:11px;letter-spacing:2px">Error: ${e.message}<br><br>Make sure the Google Sheet is published.</div>`;}
}
function buildControls(){
  const positions=[...new Set(allRows.map(r=>r['Position']||r['Pos']||'').filter(Boolean))].sort();
  const teams=[...new Set(allRows.map(r=>r['Team']||'').filter(Boolean))].sort();
  document.getElementById('controls').innerHTML=`
    <div class="ctrl-group"><span class="ctrl-label">Position</span><select onchange="filters.pos=this.value;render()"><option value="">All</option>${positions.map(p=>`<option>${p}</option>`).join('')}</select></div>
    <div class="ctrl-group"><span class="ctrl-label">Team</span><select onchange="filters.team=this.value;render()"><option value="">All</option>${teams.map(t=>`<option>${t}</option>`).join('')}</select></div>
    <div class="ctrl-group"><span class="ctrl-label">Search</span><input type="text" placeholder="Player name..." oninput="filters.search=this.value;render()"></div>
    <button class="reset-btn" onclick="filters={pos:'',team:'',search:''};document.querySelectorAll('#controls select,#controls input').forEach(e=>e.value='');render()">Reset</button>`;
}
function getFiltered(){return allRows.filter(r=>{const pos=r['Position']||r['Pos']||'';if(filters.pos&&pos!==filters.pos)return false;if(filters.team&&(r['Team']||'')!==filters.team)return false;if(filters.search&&!(r['Player']||'').toLowerCase().includes(filters.search.toLowerCase()))return false;return true;});}
const COLS=['Player','Position','Team','EPV Annualized','Extension Value (Ann.)','Over/Under (Ann.)'];

function render(){
  const data=[...getFiltered()].sort((a,b)=>{let av=a[sortCol],bv=b[sortCol];const an=parseMoney(av),bn=parseMoney(bv);if(an!==null&&bn!==null)return sortAsc?an-bn:bn-an;av=(av||'').toLowerCase();bv=(bv||'').toLowerCase();return sortAsc?av.localeCompare(bv):bv.localeCompare(av);});
  let totalOU=0;data.forEach(r=>{const ou=parseMoney(r['Over/Under (Ann.)']);if(ou!==null)totalOU+=ou;});
  document.getElementById('kpiPlayers').textContent=data.length;
  const netEl=document.getElementById('kpiNet');netEl.textContent=fmtShort(totalOU);netEl.style.color=totalOU>=0?'var(--positive)':'var(--negative)';

  const thHTML=COLS.map(c=>{const cls=c===sortCol?(sortAsc?'sorted-asc':'sorted-desc'):'';const right=['EPV Annualized','Extension Value (Ann.)','Over/Under (Ann.)'].includes(c)?'col-right':'';return`<th class="${cls} ${right}" onclick="sortBy('${c}')">${c}</th>`;}).join('');
  const tbody=data.map(r=>{
    const player=r['Player']||'';const pos=r['Position']||r['Pos']||'';const team=r['Team']||'';
    const epv=parseMoney(r['EPV Annualized']);const ext=parseMoney(r['Extension Value (Ann.)']);const ou=parseMoney(r['Over/Under (Ann.)']);
    const logo=logoUrl(team);const ouClass=ou===null?'neutral':ou>0?'positive':ou<0?'negative':'neutral';
    return`<tr>
      <td><span class="player-name">${player}</span></td>
      <td><span class="pos-badge">${pos||'—'}</span></td>
      <td><div class="team-cell">${logo?`<img src="${logo}" alt="${team}" class="team-logo">`:''}<span class="team-name-sm">${team}</span></div></td>
      <td class="col-right money neutral">${fmt(epv)}</td>
      <td class="col-right money neutral">${fmt(ext)}</td>
      <td class="col-right money ${ouClass}">${fmt(ou)}</td>
    </tr>`;
  }).join('');
  document.getElementById('app').innerHTML=`<table><thead><tr>${thHTML}</tr></thead><tbody>${tbody||'<tr><td colspan="6" style="text-align:center;padding:40px;color:var(--text-dim)">No players found</td></tr>'}</tbody></table>`;
}
function sortBy(col){if(sortCol===col)sortAsc=!sortAsc;else{sortCol=col;sortAsc=false;}render();}
init();
</script>
</body>
</html>
