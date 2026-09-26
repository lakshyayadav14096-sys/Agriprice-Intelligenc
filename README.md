# Agriprice-Intelligenc
AgriPrice Intelligence: A web app for tracking, comparing, and analyzing agricultural Mandi price trends and alerts.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>AgriPrice Intelligence</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<style>
:root{--bg:#f3f6f3;--card:#fff;--ink:#1b2a1f;--muted:#5f6f64;--brand:#1f7a3f;--brand2:#2e9e57;--line:#dde5df;--up:#178a4c;--down:#c8362b;--warn:#b7791f;--soft:#eef5ef}
*{box-sizing:border-box}
body{margin:0;font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;background:var(--bg);color:var(--ink);font-size:14px}
header{background:linear-gradient(90deg,#14532d,#1f7a3f);color:#fff;padding:12px 20px;display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.brand{display:flex;align-items:center;gap:10px}.brand h1{margin:0;font-size:18px}.brand small{opacity:.85}
.logo{font-size:28px}
.hdr-tools{display:flex;gap:12px;align-items:center;flex-wrap:wrap}.hdr-tools select{padding:5px 8px;border-radius:6px;border:none}
.badge{background:rgba(255,255,255,.18);padding:4px 10px;border-radius:999px;font-size:12px}
nav{display:flex;gap:2px;background:#fff;border-bottom:1px solid var(--line);padding:0 12px;overflow-x:auto;position:sticky;top:0;z-index:5}
nav a{padding:12px 14px;text-decoration:none;color:var(--muted);border-bottom:3px solid transparent;white-space:nowrap;font-weight:500}
nav a.active{color:var(--brand);border-color:var(--brand)}
.pill{background:var(--down);color:#fff;border-radius:999px;padding:1px 7px;font-size:11px;margin-left:4px;display:none}
main{max-width:1200px;margin:0 auto;padding:16px}
h2{margin:0 0 12px;font-size:20px}h3{margin:0 0 10px;font-size:15px;color:var(--muted);font-weight:600;text-transform:uppercase;letter-spacing:.04em}
.grid{display:grid;gap:14px;margin-bottom:14px}.g2{grid-template-columns:repeat(2,1fr)}.g3{grid-template-columns:repeat(3,1fr)}.g4{grid-template-columns:repeat(4,1fr)}.g5{grid-template-columns:repeat(5,1fr)}
@media(max-width:900px){.g3,.g4,.g5{grid-template-columns:repeat(2,1fr)}}@media(max-width:600px){.g2,.g3,.g4,.g5{grid-template-columns:1fr}}
.card{background:var(--card);border:1px solid var(--line);border-radius:10px;padding:14px}
.kpi .v{font-size:22px;font-weight:700}.kpi .l{color:var(--muted);font-size:12px}.kpi .s{font-size:12px;margin-top:2px}
.up{color:var(--up)}.down{color:var(--down)}.flat{color:var(--muted)}.warn{color:var(--warn)}
.filters{display:flex;gap:10px;flex-wrap:wrap;align-items:flex-end}.filters label{display:flex;flex-direction:column;gap:4px;font-size:12px;color:var(--muted);min-width:120px;flex:1}
input,select,textarea,button{font:inherit}
input[type=text],input[type=date],input[type=number],select,textarea{padding:7px 9px;border:1px solid var(--line);border-radius:7px;background:#fff;width:100%}
textarea{font-family:ui-monospace,Menlo,Consolas,monospace;font-size:12px;min-height:160px}
button,.btn{padding:8px 14px;border-radius:7px;border:1px solid var(--brand);background:var(--brand);color:#fff;cursor:pointer;font-weight:500;text-decoration:none;display:inline-block}
button.ghost,.btn.ghost{background:#fff;color:var(--brand)}button.danger{background:#fff;color:var(--down);border-color:var(--down)}button.sm{padding:4px 10px;font-size:12px}
button:disabled{opacity:.5;cursor:not-allowed}
.seg{display:inline-flex;border:1px solid var(--line);border-radius:7px;overflow:hidden}.seg button{border:none;border-radius:0;background:#fff;color:var(--muted);padding:6px 12px}.seg button.on{background:var(--brand);color:#fff}
.tbl-wrap{overflow-x:auto}table{width:100%;border-collapse:collapse;font-size:13px}th,td{padding:8px 10px;text-align:left;border-bottom:1px solid var(--line);white-space:nowrap}th{color:var(--muted);font-weight:600;font-size:12px;background:var(--soft)}
td.num,th.num{text-align:right;font-variant-numeric:tabular-nums}tr.click{cursor:pointer}tr.click:hover{background:var(--soft)}
.chart{position:relative;height:320px}.chart.sm{height:240px}
.empty{padding:40px;text-align:center;color:var(--muted)}.empty b{display:block;font-size:16px;color:var(--ink);margin-bottom:6px}
.list{display:flex;flex-direction:column;gap:6px}.row{display:flex;justify-content:space-between;align-items:center;padding:8px 10px;border-radius:7px;background:var(--soft);cursor:pointer}.row:hover{outline:2px solid var(--brand2)}
.row .n{font-weight:600}.row .m{font-size:12px;color:var(--muted)}.row .p{font-weight:700;text-align:right}
.pager{display:flex;gap:8px;align-items:center;justify-content:flex-end;margin-top:10px;color:var(--muted);font-size:13px}
.note{font-size:12px;color:var(--muted)}.insight{background:var(--soft);border-left:4px solid var(--brand);padding:10px 12px;border-radius:6px;margin-bottom:12px}
.report li{font-size:12px;margin:2px 0}.report ul{max-height:200px;overflow:auto;margin:6px 0;padding-left:18px}
.drop{border:2px dashed var(--line);border-radius:10px;padding:22px;text-align:center;color:var(--muted);cursor:pointer}.drop.over{border-color:var(--brand);background:var(--soft)}
.chk{display:flex;flex-wrap:wrap;gap:6px 14px}.chk label{display:flex;gap:6px;align-items:center;font-size:13px}
.tag{display:inline-block;padding:2px 8px;border-radius:999px;font-size:11px;font-weight:600}.tag.hot{background:#fde8e6;color:var(--down)}.tag.ok{background:#e4f4ea;color:var(--up)}.tag.off{background:#eee;color:#777}
#toasts{position:fixed;right:16px;bottom:16px;display:flex;flex-direction:column;gap:8px;z-index:50}.toast{background:#1b2a1f;color:#fff;padding:10px 14px;border-radius:8px;box-shadow:0 4px 14px rgba(0,0,0,.2);max-width:320px;font-size:13px}.toast.err{background:var(--down)}.toast.warn{background:var(--warn)}
.matrix td{text-align:right}.matrix td:first-child{text-align:left;font-weight:600}
code{background:var(--soft);padding:1px 5px;border-radius:4px;font-size:12px}
.toolbar{display:flex;gap:8px;flex-wrap:wrap;align-items:center;margin-bottom:12px}
</style>
</head>
<body>
<header>
  <div class="brand"><span class="logo">🌾</span><div><h1>AgriPrice Intelligence</h1><small>Mandi price trends, comparisons &amp; alerts</small></div></div>
  <div class="hdr-tools">
    <label>Unit&nbsp;<select id="unitSel"><option value="quintal">₹ / quintal</option><option value="kg">₹ / kg</option></select></label>
    <span id="dataBadge" class="badge">…</span>
  </div>
</header>
<nav id="nav">
  <a href="#dashboard" data-route="dashboard">Dashboard</a>
  <a href="#explore" data-route="explore">Explore</a>
  <a href="#trends" data-route="trends">Trends</a>
  <a href="#compare" data-route="compare">Compare</a>
  <a href="#alerts" data-route="alerts">Alerts<span id="alertCount" class="pill"></span></a>
  <a href="#import" data-route="import">Import</a>
</nav>
<main id="app"></main>
<div id="toasts"></div>

<script>
/* =====================================================================
   0. UTILITIES
   ===================================================================== */
const $=(s,el=document)=>el.querySelector(s);
const $$=(s,el=document)=>[...el.querySelectorAll(s)];
const toISO=d=>d.toISOString().slice(0,10);
const TODAY=toISO(new Date());
const addDays=(iso,n)=>{const d=new Date(iso+'T00:00:00Z');d.setUTCDate(d.getUTCDate()+n);return toISO(d);};
const daysBetween=(a,b)=>Math.round((Date.parse(b+'T00:00:00Z')-Date.parse(a+'T00:00:00Z'))/86400000);
const shortDate=iso=>{const d=new Date(iso+'T00:00:00Z');return d.toLocaleDateString('en-IN',{day:'2-digit',month:'short',timeZone:'UTC'});};
const esc=s=>String(s??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const slug=s=>String(s).toLowerCase().trim().replace(/[^a-z0-9]+/g,'-').replace(/^-|-$/g,'');
const titleCase=s=>String(s).trim().replace(/\s+/g,' ').toLowerCase().replace(/\b\w/g,c=>c.toUpperCase());
const str=v=>v==null?'':String(v).trim();
const num=v=>{if(v==null||str(v)==='')return null;const n=parseFloat(String(v).replace(/[₹,\s]/g,''));return isNaN(n)?null:n;};
const mean=a=>a.reduce((s,x)=>s+x,0)/a.length;
const stdev=a=>{if(a.length<2)return 0;const m=mean(a);return Math.sqrt(a.reduce((s,x)=>s+(x-m)**2,0)/(a.length-1));};
function mulberry32(a){return function(){a|=0;a=a+0x6D2B79F5|0;let t=Math.imul(a^a>>>15,1|a);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296;};}
const PALETTE=['#1f7a3f','#d97706','#2563eb','#dc2626','#7c3aed','#0891b2','#be185d','#65a30d'];
function toast(msg,type=''){const t=document.createElement('div');t.className='toast '+type;t.textContent=msg;$('#toasts').appendChild(t);setTimeout(()=>t.remove(),4000);}
function downloadText(name,text,mime='text/csv'){const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([text],{type:mime}));a.download=name;a.click();setTimeout(()=>URL.revokeObjectURL(a.href),1000);}

/* =====================================================================
   1. DATA LAYER  (normalised in-memory tables)
   crops(id,name,category)  markets(id,name,district,state)
   prices(cropId,marketId,date,min,max,modal,unit='quintal',arrivals,source)
   PK of prices = cropId|marketId|date  (canonical unit: ₹ per quintal)
   ===================================================================== */
const DB={crops:new Map(),markets:new Map(),prices:new Map()};
const LS={prices:'api_user_prices_v1',alerts:'api_alerts_v1',unit:'api_unit_v1'};
const priceKey=(c,m,d)=>`${c}|${m}|${d}`;
const pairKey=(c,m)=>`${c}|${m}`;

// crop-name aliases → canonical (extend freely; Hindi/plural variants)
const CROP_ALIASES={tomatoes:'tomato',tamatar:'tomato',onions:'onion',pyaz:'onion',kanda:'onion',potatoes:'potato',aloo:'potato',batata:'potato',paddy:'rice (paddy)',rice:'rice (paddy)',dhan:'rice (paddy)',soyabean:'soybean','soya bean':'soybean',soyabeans:'soybean',gehu:'wheat',gehun:'wheat'};
const canonicalCrop=n=>{const k=str(n).toLowerCase().replace(/\s+/g,' ');return CROP_ALIASES[k]||k;};
const cropIdFor=n=>slug(canonicalCrop(n));
function upsertCrop(name,category){const id=cropIdFor(name);const c=DB.crops.get(id);if(!c)DB.crops.set(id,{id,name:titleCase(canonicalCrop(name)),category:category||'Other'});else if(category&&c.category==='Other')c.category=category;return id;}
function upsertMarket(name,district,state){const id=slug(name);const m=DB.markets.get(id);if(!m)DB.markets.set(id,{id,name:titleCase(name),district:district||'',state:state||''});else{if(district&&!m.district)m.district=district;if(state&&!m.state)m.state=state;}return id;}

// ---- header mapping: accept many column names from different sources
const HEADER_ALIASES={
 crop:['crop','crop_name','cropname','commodity','commodity_name','produce','item','variety_crop'],
 market:['market','market_name','mandi','mandi_name','apmc','location','market_center'],
 district:['district','city'],state:['state','region','province'],
 date:['date','price_date','arrival_date','reported_date','report_date','day'],
 min:['min','min_price','minimum','minimum_price','minprice','low'],
 max:['max','max_price','maximum','maximum_price','maxprice','high'],
 modal:['modal','modal_price','modalprice','mode','mode_price','price','avg_price','average_price'],
 unit:['unit','price_unit','uom','units'],
 arrivals:['arrivals','arrival','arrivals_tonnes','arrival_tonnes','quantity','qty','volume'],
 category:['category','type','crop_type','group']};
const ALIAS_LOOKUP=new Map();for(const k in HEADER_ALIASES)HEADER_ALIASES[k].forEach(a=>ALIAS_LOOKUP.set(a,k));
const normHeader=h=>String(h).toLowerCase().replace(/\(.*?\)/g,'').trim().replace(/[^a-z0-9]+/g,'_').replace(/^_|_$/g,'');
function normalizeRow(raw){const out={};for(const k in raw){const canon=ALIAS_LOOKUP.get(normHeader(k));if(canon&&out[canon]===undefined)out[canon]=raw[k];}return out;}

// ---- parsers
function parseCSV(text){
  text=text.replace(/^\uFEFF/,'');
  const firstLine=text.split(/\r?\n/)[0]||'';
  const delim=(firstLine.split(';').length>firstLine.split(',').length)?';':(firstLine.split('\t').length>firstLine.split(',').length?'\t':',');
  const rows=[];let row=[],field='',inQ=false;
  for(let i=0;i<text.length;i++){const c=text[i];
    if(inQ){if(c==='"'){if(text[i+1]==='"'){field+='"';i++;}else inQ=false;}else field+=c;}
    else if(c==='"')inQ=true;
    else if(c===delim){row.push(field);field='';}
    else if(c==='\n'){row.push(field);rows.push(row);row=[];field='';}
    else if(c==='\r'){}
    else field+=c;}
  if(field.length||row.length){row.push(field);rows.push(row);}
  const nonEmpty=rows.filter(r=>r.some(v=>v.trim()!==''));
  if(nonEmpty.length<2)return{headers:nonEmpty[0]||[],rows:[]};
  const headers=nonEmpty[0].map(h=>h.trim());
  return{headers,rows:nonEmpty.slice(1).map(r=>Object.fromEntries(headers.map((h,i)=>[h,(r[i]??'').trim()])))};
}
function buildDate(y,mo,d){y=+y;mo=+mo;d=+d;if(mo<1||mo>12||d<1||d>31)return null;const dt=new Date(Date.UTC(y,mo-1,d));return dt.getUTCMonth()===mo-1?toISO(dt):null;}
function parseDate(v){v=str(v);if(!v)return null;let m;
  if(m=v.match(/^(\d{4})[-\/.](\d{1,2})[-\/.](\d{1,2})/))return buildDate(m[1],m[2],m[3]);
  if(m=v.match(/^(\d{1,2})[-\/.](\d{1,2})[-\/.](\d{4})$/))return buildDate(m[3],m[2],m[1]); // DD/MM/YYYY (Indian convention)
  const d=new Date(v);return isNaN(d)?null:toISO(d);}
function unitFactor(u){u=str(u).toLowerCase().replace(/[^a-z0-9]/g,'');if(!u)return 1;
  if(['quintal','quintals','qtl','q','rsquintal','perquintal','100kg','inrquintal','rsqtl'].includes(u))return 1;
  if(['kg','kgs','kilogram','kilograms','kilo','rskg','perkg','inrkg'].includes(u))return 100;
  if(['tonne','tonnes','ton','tons','mt','metricton','rstonne'].includes(u))return 0.1;
  return null;}

// ---- caches
let _sorted=null,_pairs=null,_medians=null;
function invalidate(){_sorted=_pairs=_medians=null;}
function allPrices(){if(!_sorted)_sorted=[...DB.prices.values()].sort((a,b)=>a.date<b.date?-1:a.date>b.date?1:0);return _sorted;}
function pairSeries(){if(!_pairs){_pairs=new Map();for(const p of allPrices()){const k=pairKey(p.cropId,p.marketId);if(!_pairs.has(k))_pairs.set(k,[]);_pairs.get(k).push(p);}}return _pairs;}
function cropMedians(){if(!_medians){const by=new Map();for(const p of allPrices()){if(!by.has(p.cropId))by.set(p.cropId,[]);by.get(p.cropId).push(p.modal);}_medians=new Map();for(const[c,a]of by){a.sort((x,y)=>x-y);_medians.set(c,a[Math.floor(a.length/2)]);}}return _medians;}

/* ---- INGESTION PIPELINE ------------------------------------------------
   parse → map headers → validate/normalise each row → de-duplicate →
   upsert dimension tables → upsert facts → report
   opts.dryRun = validate only (used for import preview)                */
function ingestRecords(rows,source,opts={}){
  const rep={source,total:rows.length,inserted:0,updated:0,skipped:0,duplicates:0,warnings:[],errors:[],newCrops:new Set(),newMarkets:new Set()};
  const batch=new Map();const med=cropMedians();
  rows.forEach((raw,i)=>{
    const ln=i+2;const r=normalizeRow(raw);
    const cropName=str(r.crop),marketName=str(r.market);
    if(!cropName||!marketName){rep.errors.push(`Row ${ln}: missing crop or market name`);rep.skipped++;return;}
    const date=parseDate(r.date);
    if(!date){rep.errors.push(`Row ${ln}: unparseable date "${str(r.date)}"`);rep.skipped++;return;}
    if(date>TODAY){rep.errors.push(`Row ${ln}: date ${date} is in the future`);rep.skipped++;return;}
    let min=num(r.min),max=num(r.max),modal=num(r.modal);
    if(modal==null){if(min!=null&&max!=null){modal=(min+max)/2;rep.warnings.push(`Row ${ln}: modal missing → used midpoint of min/max`);}else{rep.errors.push(`Row ${ln}: no usable price values`);rep.skipped++;return;}}
    if(min==null){min=modal;rep.warnings.push(`Row ${ln}: min missing → set to modal`);}
    if(max==null){max=modal;rep.warnings.push(`Row ${ln}: max missing → set to modal`);}
    if(min<=0||max<=0||modal<=0){rep.errors.push(`Row ${ln}: non-positive price`);rep.skipped++;return;}
    let f=unitFactor(r.unit);if(f==null){f=1;rep.warnings.push(`Row ${ln}: unknown unit "${str(r.unit)}" → assumed ₹/quintal`);}
    min*=f;max*=f;modal*=f;
    if(min>max){[min,max]=[max,min];rep.warnings.push(`Row ${ln}: min > max → swapped`);}
    if(modal<min||modal>max){const c=Math.min(Math.max(modal,min),max);rep.warnings.push(`Row ${ln}: modal ${Math.round(modal)} outside [min,max] → clamped to ${Math.round(c)}`);modal=c;}
    const cropId=cropIdFor(cropName),marketId=slug(marketName);
    const m=med.get(cropId);
    if(m&&(modal>m*8||modal<m/8)){rep.errors.push(`Row ${ln}: modal ${Math.round(modal)} is an outlier vs crop median ${Math.round(m)} → skipped`);rep.skipped++;return;}
    const key=priceKey(cropId,marketId,date);if(batch.has(key))rep.duplicates++;
    batch.set(key,{cropName,category:str(r.category),marketName,district:str(r.district),state:str(r.state),cropId,marketId,date,min:Math.round(min),max:Math.round(max),modal:Math.round(modal),arrivals:num(r.arrivals),source});
  });
  for(const[key,b]of batch){
    if(!DB.crops.has(b.cropId))rep.newCrops.add(titleCase(canonicalCrop(b.cropName)));
    if(!DB.markets.has(b.marketId))rep.newMarkets.add(titleCase(b.marketName));
    if(DB.prices.has(key))rep.updated++;else rep.inserted++;
    if(opts.dryRun)continue;
    upsertCrop(b.cropName,b.category);upsertMarket(b.marketName,b.district,b.state);
    DB.prices.set(key,{cropId:b.cropId,marketId:b.marketId,date:b.date,min:b.min,max:b.max,modal:b.modal,unit:'quintal',arrivals:b.arrivals,source});
  }
  if(!opts.dryRun){invalidate();if(source!=='seed'&&!opts.noPersist)persistUserData();}
  return rep;
}

// denormalised row (for export / persistence)
function toRow(p){const c=DB.crops.get(p.cropId)||{},m=DB.markets.get(p.marketId)||{};return{crop:c.name,category:c.category,market:m.name,district:m.district,state:m.state,date:p.date,min:p.min,max:p.max,modal:p.modal,unit:'quintal',arrivals:p.arrivals??'',source:p.source};}
function toCSV(rows){if(!rows.length)return'';const h=Object.keys(rows[0]);const q=v=>{v=String(v??'');return/[",\n]/.test(v)?'"'+v.replace(/"/g,'""')+'"':v;};return[h.join(','),...rows.map(r=>h.map(k=>q(r[k])).join(','))].join('\n');}
function persistUserData(){try{localStorage.setItem(LS.prices,JSON.stringify(allPrices().filter(p=>p.source!=='seed').map(toRow)));}catch(e){console.warn(e);}}
function restoreUserData(){try{const arr=JSON.parse(localStorage.getItem(LS.prices)||'[]');const by={};arr.forEach(r=>(by[r.source]=by[r.source]||[]).push(r));for(const s in by)ingestRecords(by[s],s,{noPersist:true});}catch(e){console.warn('restore failed',e);}}

/* ---- SEED DATA (deterministic synthetic mandi series) ---------------- */
const SEED_MARKETS=[{name:'Azadpur',district:'Delhi',state:'Delhi'},{name:'Vashi APMC',district:'Thane',state:'Maharashtra'},{name:'Lasalgaon',district:'Nashik',state:'Maharashtra'},{name:'Yeshwanthpur',district:'Bengaluru',state:'Karnataka'},{name:'Indore Chhawni',district:'Indore',state:'Madhya Pradesh'}];
const SEED_CROPS=[{name:'Tomato',category:'Vegetable',base:1800,vol:.06,trend:.004,arr:300},{name:'Onion',category:'Vegetable',base:1500,vol:.045,trend:-.003,arr:700},{name:'Potato',category:'Vegetable',base:1200,vol:.025,trend:.001,arr:600},{name:'Wheat',category:'Cereal',base:2350,vol:.008,trend:.0005,arr:900},{name:'Rice (Paddy)',category:'Cereal',base:2200,vol:.01,trend:.0008,arr:800},{name:'Soybean',category:'Oilseed',base:4600,vol:.015,trend:-.001,arr:1100}];
function seedData(){
  const rng=mulberry32(20260925);const gauss=()=>{let u=0,v=0;while(!u)u=rng();while(!v)v=rng();return Math.sqrt(-2*Math.log(u))*Math.cos(2*Math.PI*v);};
  const DAYS=45,start=addDays(TODAY,-(DAYS-1));const rows=[];
  SEED_CROPS.forEach(c=>SEED_MARKETS.forEach(m=>{
    const target=c.base*(0.88+rng()*0.24);let p=target*(0.95+rng()*0.1);const arrBase=c.arr*(0.5+rng());
    for(let d=0;d<DAYS;d++){const date=addDays(start,d);
      p=p*(1+c.trend+c.vol*gauss())+(target-p)*0.05;
      if(rng()<0.03)p*=(rng()<0.5?0.9:1.12);           // occasional shock
      if(rng()<0.06)continue;                          // simulate missing day / holiday
      rows.push({crop:c.name,category:c.category,market:m.name,district:m.district,state:m.state,date,min:(p*(0.86+rng()*0.08)).toFixed(0),max:(p*(1.05+rng()*0.1)).toFixed(0),modal:p.toFixed(0),unit:'quintal',arrivals:(arrBase*(0.7+rng()*0.6)).toFixed(1)});}
  }));
  return ingestRecords(rows,'seed');
}
function resetData(){DB.crops.clear();DB.markets.clear();DB.prices.clear();invalidate();localStorage.removeItem(LS.prices);seedData();}

/* ---- MOCK EXTERNAL API (simulates an Agmarknet-style feed) ----------- */
function mockApiFetch(){return new Promise(res=>setTimeout(()=>{
  const last=latestByPair();const maxDate=allPrices().length?allPrices().at(-1).date:addDays(TODAY,-3);
  const days=Math.min(3,Math.max(0,daysBetween(maxDate,TODAY)));const records=[];
  if(days===0){res({status:'ok',source:'agmarknet-mock',records:[],message:'Feed already up to date'});return;}
  for(let d=1;d<=days;d++){const date=addDays(maxDate,d);
    for(const rec of last.values()){const c=DB.crops.get(rec.cropId),m=DB.markets.get(rec.marketId);
      const modal=rec.modal*(1+(Math.random()-0.5)*0.08);const kg=c.name==='Tomato';const f=kg?0.01:1;
      records.push({commodity:c.name.toUpperCase(),market_name:m.name,district:m.district,state:m.state,arrival_date:date.split('-').reverse().join('/'),min_price:(modal*0.9*f).toFixed(kg?2:0),max_price:(modal*1.1*f).toFixed(kg?2:0),modal_price:(modal*f).toFixed(kg?2:0),unit:kg?'Rs/Kg':'Rs/Quintal',arrivals:(rec.arrivals||200)*(0.8+Math.random()*0.4)});}}
  // deliberately dirty rows to exercise the pipeline
  records.push({commodity:'Onion',market_name:'Azadpur',arrival_date:'31/02/2026',min_price:1500,max_price:1800,modal_price:1650,unit:'quintal'});
  records.push({commodity:'',market_name:'Vashi APMC',arrival_date:TODAY,min_price:1500,max_price:1800,modal_price:1650});
  records.push({commodity:'Potato',market_name:'Indore Chhawni',arrival_date:TODAY,min_price:1400,max_price:1100,modal_price:1250,unit:'quintal'});
  res({status:'ok',source:'agmarknet-mock',records});
},800));}

const sampleCSV=()=>`crop,market,district,state,date,min_price,max_price,modal_price,unit,arrivals
Tomato,Azadpur,Delhi,Delhi,${TODAY},14,26,20,kg,310
Tomatoes,Azadpur,Delhi,Delhi,${TODAY.split('-').reverse().join('/')},1400,2600,2050,quintal,310
Onion,Vashi APMC,Thane,Maharashtra,${TODAY},2400,1800,2100,quintal,540
Potato,Lasalgaon,Nashik,Maharashtra,${TODAY},1000,1400,,quintal,220
Wheat,Indore Chhawni,Indore,Madhya Pradesh,not-a-date,2300,2500,2400,quintal,800
Green Chilli,Yeshwanthpur,Bengaluru,Karnataka,${TODAY},3000,4500,3800,quintal,95
Brinjal,Kolar APMC,Kolar,Karnataka,${TODAY},1500,2200,1900,quintal,60
Soybean,Indore Chhawni,Indore,Madhya Pradesh,${TODAY},4200,4900,99999,quintal,1200
Wheat,Azadpur,Delhi,Delhi,${TODAY},2300,2500,2400,,650`;
const templateCSV=()=>`crop,market,district,state,date,min_price,max_price,modal_price,unit,arrivals\nTomato,Azadpur,Delhi,Delhi,${TODAY},1400,2600,2000,quintal,310`;

/* =====================================================================
   2. ANALYTICS
   ===================================================================== */
function query({cropId,marketId,state,from,to,q}={}){const ql=str(q).toLowerCase();return allPrices().filter(p=>{
  if(cropId&&p.cropId!==cropId)return false;if(marketId&&p.marketId!==marketId)return false;
  if(state&&(DB.markets.get(p.marketId)||{}).state!==state)return false;
  if(from&&p.date<from)return false;if(to&&p.date>to)return false;
  if(ql){const c=DB.crops.get(p.cropId).name.toLowerCase(),m=DB.markets.get(p.marketId);if(!c.includes(ql)&&!m.name.toLowerCase().includes(ql)&&!(m.state||'').toLowerCase().includes(ql)&&!(m.district||'').toLowerCase().includes(ql))return false;}
  return true;});}
function seriesFor(cropId,marketId,from,to){const s=pairSeries().get(pairKey(cropId,marketId))||[];return s.filter(p=>(!from||p.date>=from)&&(!to||p.date<=to));}
function latestByPair(){const m=new Map();for(const p of allPrices())m.set(pairKey(p.cropId,p.marketId),p);return m;}
function prevRecord(p){const s=pairSeries().get(pairKey(p.cropId,p.marketId))||[];const i=s.indexOf(p);return i>0?s[i-1]:null;}
function changeOverDays(rec,days){const s=pairSeries().get(pairKey(rec.cropId,rec.marketId))||[];const target=addDays(rec.date,-days);let base=null;for(const p of s){if(p.date<=target)base=p;else break;}if(!base&&s.length>1&&s[0].date<rec.date)base=s[0];if(!base)return null;return{pct:(rec.modal-base.modal)/base.modal*100,base};}
function movingAvg(a,n){return a.map((_,i)=>i<n-1?null:mean(a.slice(i-n+1,i+1)));}
function computeStats(recs){const n=recs.length;if(!n)return null;const modals=recs.map(r=>r.modal);const avg=mean(modals);
  const rets=[];for(let i=1;i<n;i++)rets.push((modals[i]-modals[i-1])/modals[i-1]);
  return{count:n,avg,lo:Math.min(...recs.map(r=>r.min)),hi:Math.max(...recs.map(r=>r.max)),minModal:Math.min(...modals),maxModal:Math.max(...modals),first:modals[0],last:modals[n-1],lastDate:recs[n-1].date,changePct:(modals[n-1]-modals[0])/modals[0]*100,vol:stdev(rets)*100,cv:stdev(modals)/avg*100,gaps:daysBetween(recs[0].date,recs[n-1].date)+1-n};}

/* =====================================================================
   3. ALERTS
   ===================================================================== */
function loadAlerts(){try{return JSON.parse(localStorage.getItem(LS.alerts)||'[]');}catch(e){return[];}}
function saveAlerts(){localStorage.setItem(LS.alerts,JSON.stringify(state.alerts));}
function evaluateAlerts(){const latest=latestByPair();return state.alerts.map(a=>{const hits=[];if(a.active!==false)for(const rec of latest.values()){if(rec.cropId!==a.cropId)continue;if(a.marketId&&rec.marketId!==a.marketId)continue;if(a.cond==='below'?rec.modal<a.threshold:rec.modal>a.threshold)hits.push(rec);}return{alert:a,hits};});}
function checkAlertsNotify(){let n=0;for(const{alert,hits}of evaluateAlerts()){alert.notified=alert.notified||[];for(const h of hits){const k=`${h.marketId}|${h.date}`;if(!alert.notified.includes(k)){alert.notified.push(k);n++;toast(`🔔 ${DB.crops.get(h.cropId).name} @ ${DB.markets.get(h.marketId).name} is ${fmtP(h.modal)} — ${alert.cond} your ${fmtP(alert.threshold)} threshold`,'warn');}}}
  if(n)saveAlerts();updateBadges();}

/* =====================================================================
   4. UI STATE, FORMATTING, ROUTING
   ===================================================================== */
const state={route:'dashboard',unit:localStorage.getItem(LS.unit)||'quintal',
  explore:{crop:'',market:'',state:'',from:'',to:'',q:'',sort:'date_desc',page:1,pageSize:25},
  trends:{crop:'',market:'',range:30,showBand:true,showMA:true},
  compare:{mode:'markets',crop:'',market:'',markets:[],crops:[],range:30},
  alerts:loadAlerts(),import:{text:'',fileName:'',preview:null}};
const dispFactor=()=>state.unit==='kg'?0.01:1;
const unitLabel=()=>state.unit==='kg'?'₹/kg':'₹/quintal';
function fmtP(v){if(v==null||isNaN(v))return'—';const x=v*dispFactor();const d=state.unit==='kg'?2:0;return'₹'+x.toLocaleString('en-IN',{minimumFractionDigits:d,maximumFractionDigits:d});}
const fmtN=v=>v==null||isNaN(v)?'—':Number(v).toLocaleString('en-IN',{maximumFractionDigits:1});
const fmtPct=v=>v==null||isNaN(v)?'—':(v>0?'+':'')+v.toFixed(2)+'%';
const pctClass=v=>v==null?'flat':v>0.05?'up':v<-0.05?'down':'flat';
const arrow=v=>v==null?'':v>0.05?'▲':v<-0.05?'▼':'●';
const cropsList=()=>[...DB.crops.values()].sort((a,b)=>a.name.localeCompare(b.name));
const marketsList=()=>[...DB.markets.values()].sort((a,b)=>a.name.localeCompare(b.name));
const statesList=()=>[...new Set(marketsList().map(m=>m.state).filter(Boolean))].sort();
const optsHTML=(items,sel,all)=>(all?`<option value="">${esc(all)}</option>`:'')+items.map(i=>`<option value="${esc(i.id??i)}" ${(i.id??i)===sel?'selected':''}>${esc(i.name??i)}</option>`).join('');
const emptyState=(t,s,link)=>`<div class="card empty"><b>${esc(t)}</b>${esc(s)}${link?`<div style="margin-top:12px"><a class="btn" href="#${link}">Go to ${link}</a></div>`:''}</div>`;

const charts={};
function makeChart(id,cfg){if(charts[id]){charts[id].destroy();delete charts[id];}const el=document.getElementById(id);if(!el)return;
  if(typeof Chart==='undefined'){el.parentElement.innerHTML='<div class="empty">Chart.js failed to load (offline?). Data tables still work.</div>';return;}
  Chart.defaults.font.family=getComputedStyle(document.body).fontFamily;charts[id]=new Chart(el,cfg);}
function destroyCharts(){for(const k in charts){charts[k].destroy();delete charts[k];}}

const ROUTES={dashboard:renderDashboard,explore:renderExplore,trends:renderTrends,compare:renderCompare,alerts:renderAlerts,import:renderImport};
function navigate(route,params){if(params)Object.assign(state[route],params);if(location.hash==='#'+route)render();else location.hash=route;}
function render(){destroyCharts();const r=(location.hash||'#dashboard').slice(1);state.route=ROUTES[r]?r:'dashboard';
  $$('#nav a').forEach(a=>a.classList.toggle('active',a.dataset.route===state.route));
  $('#app').innerHTML='';try{ROUTES[state.route]();}catch(e){console.error(e);$('#app').innerHTML=emptyState('Something went wrong rendering this view',e.message);}
  updateBadges();window.scrollTo(0,0);}
function updateBadges(){const n=allPrices().length;$('#dataBadge').textContent=`${n.toLocaleString('en-IN')} records · ${DB.crops.size} crops · ${DB.markets.size} markets`;
  const trig=evaluateAlerts().filter(x=>x.hits.length).length;const p=$('#alertCount');p.textContent=trig;p.style.display=trig?'inline-block':'none';}

/* =====================================================================
   5. VIEWS
   ===================================================================== */
// ---------- DASHBOARD ----------
function renderDashboard(){
  const app=$('#app'),prices=allPrices();
  if(!prices.length){app.innerHTML=emptyState('No price data yet','Import a CSV or sync the mock API to get started.','import');return;}
  const maxDate=prices.at(-1).date,latest=latestByPair();
  const moves=[];for(const rec of latest.values()){const ch=changeOverDays(rec,7);if(ch)moves.push({rec,pct:ch.pct,base:ch.base});}
  moves.sort((a,b)=>b.pct-a.pct);const gainers=moves.slice(0,5),losers=moves.slice(-5).reverse();
  const from7=addDays(maxDate,-6);const traded=new Map();prices.filter(p=>p.date>=from7).forEach(p=>traded.set(p.cropId,(traded.get(p.cropId)||0)+(p.arrivals||0)));
  const tradedArr=[...traded].map(([id,v])=>({name:DB.crops.get(id).name,v})).sort((a,b)=>b.v-a.v).slice(0,8);
  const recent=[...prices].reverse().slice(0,12).map(r=>{const prev=prevRecord(r);return{r,dod:prev?(r.modal-prev.modal)/prev.modal*100:null};});
  const allMod=prices.filter(p=>p.date===maxDate);
  const crops=cropsList(),mkts=marketsList();
  const mkRow=x=>`<div class="row" data-c="${x.rec.cropId}" data-m="${x.rec.marketId}"><div><div class="n">${esc(DB.crops.get(x.rec.cropId).name)}</div><div class="m">${esc(DB.markets.get(x.rec.marketId).name)} · ${shortDate(x.rec.date)}</div></div><div class="p"><div class="${pctClass(x.pct)}">${arrow(x.pct)} ${fmtPct(x.pct)}</div><div class="m">${fmtP(x.rec.modal)}</div></div></div>`;
  app.innerHTML=`<h2>Market Dashboard <span class="note">— latest data ${shortDate(maxDate)}${maxDate<TODAY?` <span class="warn">(${daysBetween(maxDate,TODAY)}d old — sync in Import)</span>`:''}</span></h2>
  <div class="grid g4">
    <div class="card kpi"><div class="l">Price records</div><div class="v">${prices.length.toLocaleString('en-IN')}</div><div class="s note">${[...new Set(prices.map(p=>p.source))].length} data source(s)</div></div>
    <div class="card kpi"><div class="l">Crops tracked</div><div class="v">${DB.crops.size}</div><div class="s note">${[...new Set(crops.map(c=>c.category))].join(', ')}</div></div>
    <div class="card kpi"><div class="l">Markets / mandis</div><div class="v">${DB.markets.size}</div><div class="s note">${statesList().length} states</div></div>
    <div class="card kpi"><div class="l">Reported today (${shortDate(maxDate)})</div><div class="v">${allMod.length}</div><div class="s note">of ${latest.size} crop-market pairs</div></div>
  </div>
  <div class="grid g3">
    <div class="card"><h3>Top gainers (7d)</h3><div class="list">${gainers.length?gainers.map(mkRow).join(''):'<div class="note">Not enough history</div>'}</div></div>
    <div class="card"><h3>Top losers (7d)</h3><div class="list">${losers.length?losers.map(mkRow).join(''):'<div class="note">Not enough history</div>'}</div></div>
    <div class="card"><h3>Most traded crops (arrivals, last 7d)</h3><div class="chart sm"><canvas id="chTraded"></canvas></div></div>
  </div>
  <div class="grid g2">
    <div class="card"><h3>Latest modal price matrix (${unitLabel()})</h3><div class="tbl-wrap"><table class="matrix"><thead><tr><th>Crop</th>${mkts.map(m=>`<th class="num">${esc(m.name)}</th>`).join('')}</tr></thead><tbody>
      ${crops.map(c=>{const vals=mkts.map(m=>latest.get(pairKey(c.id,m.id)));const nums=vals.filter(Boolean).map(v=>v.modal);const lo=Math.min(...nums),hi=Math.max(...nums);
        return`<tr><td>${esc(c.name)}</td>${vals.map((v,i)=>{if(!v)return'<td class="note">—</td>';const t=hi>lo?(v.modal-lo)/(hi-lo):0.5;const stale=v.date<addDays(maxDate,-2);return`<td class="click" style="background:rgba(31,122,63,${(0.06+0.32*t).toFixed(2)});cursor:pointer" data-c="${c.id}" data-m="${mkts[i].id}" title="${v.date}${stale?' (stale)':''}">${fmtP(v.modal)}${stale?' <span class="warn">⚠</span>':''}</td>`;}).join('')}</tr>`;}).join('')}
    </tbody></table></div><div class="note" style="margin-top:6px">Darker = higher price within the crop row. ⚠ = last report older than 2 days.</div></div>
    <div class="card"><h3>Recent price movements</h3><div class="tbl-wrap"><table><thead><tr><th>Date</th><th>Crop</th><th>Market</th><th class="num">Modal</th><th class="num">Δ vs prev</th></tr></thead><tbody>
      ${recent.map(x=>`<tr class="click" data-c="${x.r.cropId}" data-m="${x.r.marketId}"><td>${shortDate(x.r.date)}</td><td>${esc(DB.crops.get(x.r.cropId).name)}</td><td>${esc(DB.markets.get(x.r.marketId).name)}</td><td class="num">${fmtP(x.r.modal)}</td><td class="num ${pctClass(x.dod)}">${arrow(x.dod)} ${fmtPct(x.dod)}</td></tr>`).join('')}
    </tbody></table></div></div>
  </div>`;
  makeChart('chTraded',{type:'bar',data:{labels:tradedArr.map(t=>t.name),datasets:[{label:'Arrivals (tonnes)',data:tradedArr.map(t=>+t.v.toFixed(1)),backgroundColor:'#2e9e57'}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{beginAtZero:true}}}});
  $$('[data-c][data-m]',app).forEach(el=>el.addEventListener('click',()=>navigate('trends',{crop:el.dataset.c,market:el.dataset.m})));
}

// ---------- EXPLORE / SEARCH ----------
function renderExplore(){
  const app=$('#app'),f=state.explore;
  app.innerHTML=`<h2>Explore prices</h2>
  <div class="card" style="margin-bottom:14px"><div class="filters">
    <label>Search<input type="text" id="fq" placeholder="crop, market, district, state…" value="${esc(f.q)}"></label>
    <label>Crop<select id="fcrop">${optsHTML(cropsList(),f.crop,'All crops')}</select></label>
    <label>Market<select id="fmarket">${optsHTML(marketsList(),f.market,'All markets')}</select></label>
    <label>State<select id="fstate">${optsHTML(statesList(),f.state,'All states')}</select></label>
    <label>From<input type="date" id="ffrom" value="${f.from}"></label>
    <label>To<input type="date" id="fto" value="${f.to}"></label>
    <label>Sort<select id="fsort">${optsHTML([{id:'date_desc',name:'Date ↓'},{id:'date_asc',name:'Date ↑'},{id:'modal_desc',name:'Modal ↓'},{id:'modal_asc',name:'Modal ↑'},{id:'arr_desc',name:'Arrivals ↓'}],f.sort)}</select></label>
    <label>&nbsp;<button class="ghost" id="fclear">Clear</button></label>
  </div></div>
  <div id="exploreResults"></div>`;
  const bind=(id,key,reset=true)=>$(id).addEventListener(id==='#fq'?'input':'change',e=>{f[key]=e.target.value;if(reset)f.page=1;renderExploreResults();});
  bind('#fq','q');bind('#fcrop','crop');bind('#fmarket','market');bind('#fstate','state');bind('#ffrom','from');bind('#fto','to');bind('#fsort','sort');
  $('#fclear').addEventListener('click',()=>{Object.assign(f,{crop:'',market:'',state:'',from:'',to:'',q:'',page:1});render();});
  renderExploreResults();
}
function renderExploreResults(){
  const f=state.explore,box=$('#exploreResults');
  if(f.from&&f.to&&f.from>f.to){box.innerHTML=emptyState('Invalid date range','"From" must be before "To".');return;}
  let rows=query({cropId:f.crop,marketId:f.market,state:f.state,from:f.from,to:f.to,q:f.q});
  const sorters={date_desc:(a,b)=>b.date.localeCompare(a.date),date_asc:(a,b)=>a.date.localeCompare(b.date),modal_desc:(a,b)=>b.modal-a.modal,modal_asc:(a,b)=>a.modal-b.modal,arr_desc:(a,b)=>(b.arrivals||0)-(a.arrivals||0)};
  rows=[...rows].sort(sorters[f.sort]||sorters.date_desc);
  if(!rows.length){box.innerHTML=emptyState('No records match','Try widening the date range or clearing filters.');return;}
  const pages=Math.max(1,Math.ceil(rows.length/f.pageSize));f.page=Math.min(Math.max(1,f.page),pages);
  const page=rows.slice((f.page-1)*f.pageSize,f.page*f.pageSize);const st=computeStats([...rows].sort((a,b)=>a.date.localeCompare(b.date)));
  box.innerHTML=`<div class="grid g4"><div class="card kpi"><div class="l">Matching records</div><div class="v">${rows.length.toLocaleString('en-IN')}</div></div><div class="card kpi"><div class="l">Avg modal</div><div class="v">${fmtP(st.avg)}</div></div><div class="card kpi"><div class="l">Modal range</div><div class="v" style="font-size:16px">${fmtP(st.minModal)} – ${fmtP(st.maxModal)}</div></div><div class="card kpi"><div class="l">Dispersion (CV)</div><div class="v">${st.cv.toFixed(1)}%</div></div></div>
  <div class="card"><div class="toolbar"><span class="note">Click a row to open its trend. Prices in ${unitLabel()}.</span><span style="flex:1"></span>
    ${f.crop&&f.market?`<button class="ghost sm" id="toTrend">Open in Trends</button>`:''}<button class="ghost sm" id="exportCsv">Export CSV (${rows.length})</button></div>
  <div class="tbl-wrap"><table><thead><tr><th>Date</th><th>Crop</th><th>Market</th><th>State</th><th class="num">Min</th><th class="num">Max</th><th class="num">Modal</th><th class="num">Δ vs prev</th><th class="num">Arrivals (t)</th><th>Source</th></tr></thead><tbody>
  ${page.map(p=>{const c=DB.crops.get(p.cropId),m=DB.markets.get(p.marketId),pr=prevRecord(p),d=pr?(p.modal-pr.modal)/pr.modal*100:null;return`<tr class="click" data-c="${p.cropId}" data-m="${p.marketId}"><td>${p.date}</td><td>${esc(c.name)}</td><td>${esc(m.name)}</td><td>${esc(m.state)}</td><td class="num">${fmtP(p.min)}</td><td class="num">${fmtP(p.max)}</td><td class="num"><b>${fmtP(p.modal)}</b></td><td class="num ${pctClass(d)}">${fmtPct(d)}</td><td class="num">${fmtN(p.arrivals)}</td><td class="note">${esc(p.source)}</td></tr>`;}).join('')}
  </tbody></table></div>
  <div class="pager"><label>Rows <select id="pgsize">${optsHTML([25,50,100,250],f.pageSize)}</select></label><button class="ghost sm" id="pgPrev" ${f.page<=1?'disabled':''}>‹ Prev</button><span>Page ${f.page} / ${pages}</span><button class="ghost sm" id="pgNext" ${f.page>=pages?'disabled':''}>Next ›</button></div></div>`;
  $('#pgPrev').onclick=()=>{f.page--;renderExploreResults();};$('#pgNext').onclick=()=>{f.page++;renderExploreResults();};
  $('#pgsize').onchange=e=>{f.pageSize=+e.target.value;f.page=1;renderExploreResults();};
  $('#exportCsv').onclick=()=>downloadText(`agriprice_export_${TODAY}.csv`,toCSV(rows.map(toRow)));
  const tt=$('#toTrend');if(tt)tt.onclick=()=>navigate('trends',{crop:f.crop,market:f.market});
  $$('tr.click',box).forEach(tr=>tr.onclick=()=>navigate('trends',{crop:tr.dataset.c,market:tr.dataset.m}));
}

// ---------- TRENDS ----------
function renderTrends(){
  const app=$('#app'),t=state.trends;
  if(!DB.crops.size){app.innerHTML=emptyState('No data','Import price data first.','import');return;}
  if(!DB.crops.has(t.crop))t.crop=cropsList()[0].id;
  const mktsWithData=marketsList().filter(m=>pairSeries().has(pairKey(t.crop,m.id)));
  if(!mktsWithData.some(m=>m.id===t.market))t.market=(mktsWithData[0]||marketsList()[0]||{}).id||'';
  const full=seriesFor(t.crop,t.market);const lastDate=full.length?full.at(-1).date:TODAY;
  const from=t.range==='all'?'':addDays(lastDate,-(t.range-1));const recs=seriesFor(t.crop,t.market,from);
  const c=DB.crops.get(t.crop),m=DB.markets.get(t.market);
  app.innerHTML=`<h2>Price trends</h2>
  <div class="card" style="margin-bottom:14px"><div class="filters">
    <label>Crop<select id="tcrop">${optsHTML(cropsList(),t.crop)}</select></label>
    <label>Market<select id="tmarket">${optsHTML(marketsList().map(x=>({id:x.id,name:x.name+(pairSeries().has(pairKey(t.crop,x.id))?'':' (no data)')})),t.market)}</select></label>
    <label>Range<div class="seg">${[7,30,90,'all'].map(r=>`<button data-r="${r}" class="${String(t.range)===String(r)?'on':''}">${r==='all'?'All':r+'d'}</button>`).join('')}</div></label>
    <label>Overlays<div class="chk"><label><input type="checkbox" id="tband" ${t.showBand?'checked':''}>Min–max band</label><label><input type="checkbox" id="tma" ${t.showMA?'checked':''}>7-day MA</label></div></label>
    <label>&nbsp;<button class="ghost" id="tcompare">Compare across markets →</button></label>
  </div></div>
  <div id="trendBody"></div>`;
  $('#tcrop').onchange=e=>{t.crop=e.target.value;t.market='';render();};$('#tmarket').onchange=e=>{t.market=e.target.value;render();};
  $$('.seg button',app).forEach(b=>b.onclick=()=>{t.range=b.dataset.r==='all'?'all':+b.dataset.r;render();});
  $('#tband').onchange=e=>{t.showBand=e.target.checked;render();};$('#tma').onchange=e=>{t.showMA=e.target.checked;render();};
  $('#tcompare').onclick=()=>navigate('compare',{mode:'markets',crop:t.crop,markets:[]});
  const body=$('#trendBody');
  if(!m){body.innerHTML=emptyState('No market selected','');return;}
  if(!recs.length){body.innerHTML=emptyState(`No ${c.name} prices for ${m.name}`,'Try another market, a longer range, or import data for this pair.');return;}
  const s=computeStats(recs);const modals=recs.map(r=>r.modal);const ma=movingAvg(modals,7);
  const ch7=changeOverDays(recs.at(-1),7);const vsAvg=(s.last-s.avg)/s.avg*100;
  const maNow=ma.at(-1),maPrev=ma.length>7?ma.at(-8):null;const maDir=maNow!=null&&maPrev!=null?(maNow>maPrev*1.005?'rising':maNow<maPrev*0.995?'falling':'flat'):null;
  const volLabel=s.vol<1?'low':s.vol<3?'moderate':'high';
  body.innerHTML=`<div class="insight"><b>${esc(c.name)} at ${esc(m.name)}</b> last traded at <b>${fmtP(s.last)}</b> (${shortDate(s.lastDate)}), ${Math.abs(vsAvg).toFixed(1)}% ${vsAvg>=0?'above':'below'} its ${recs.length}-point average of ${fmtP(s.avg)}.${ch7?` Over the last 7 days it moved <span class="${pctClass(ch7.pct)}"><b>${fmtPct(ch7.pct)}</b></span>.`:''}${maDir?` The 7-day moving average is <b>${maDir}</b>.`:''} Volatility is <b>${volLabel}</b> (σ of daily change ${s.vol.toFixed(2)}%).${s.gaps?` <span class="warn">${s.gaps} missing day(s) in this window.</span>`:''}</div>
  <div class="grid g5">
    <div class="card kpi"><div class="l">Latest modal</div><div class="v">${fmtP(s.last)}</div><div class="s note">${shortDate(s.lastDate)}</div></div>
    <div class="card kpi"><div class="l">Average modal</div><div class="v">${fmtP(s.avg)}</div><div class="s note">${s.count} data points</div></div>
    <div class="card kpi"><div class="l">Period change</div><div class="v ${pctClass(s.changePct)}">${fmtPct(s.changePct)}</div><div class="s note">${fmtP(s.first)} → ${fmtP(s.last)}</div></div>
    <div class="card kpi"><div class="l">Traded range</div><div class="v" style="font-size:16px">${fmtP(s.lo)} – ${fmtP(s.hi)}</div><div class="s note">min / max across period</div></div>
    <div class="card kpi"><div class="l">Volatility</div><div class="v">${s.vol.toFixed(2)}%</div><div class="s note">σ daily returns · CV ${s.cv.toFixed(1)}%</div></div>
  </div>
  <div class="card"><h3>${esc(c.name)} — ${esc(m.name)} (${unitLabel()})</h3><div class="chart"><canvas id="chTrend"></canvas></div></div>`;
  const k=dispFactor();const ds=[];
  if(t.showBand){ds.push({label:'Min',data:recs.map(r=>r.min*k),borderColor:'rgba(31,122,63,.25)',borderWidth:1,pointRadius:0,tension:.3});ds.push({label:'Max',data:recs.map(r=>r.max*k),borderColor:'rgba(31,122,63,.25)',backgroundColor:'rgba(46,158,87,.12)',borderWidth:1,pointRadius:0,fill:'-1',tension:.3});}
  ds.push({label:'Modal price',data:modals.map(v=>v*k),borderColor:'#1f7a3f',backgroundColor:'#1f7a3f',borderWidth:2.5,pointRadius:recs.length>60?0:3,tension:.25});
  if(t.showMA)ds.push({label:'7-day MA',data:ma.map(v=>v==null?null:v*k),borderColor:'#d97706',borderDash:[6,4],borderWidth:2,pointRadius:0,spanGaps:true,tension:.3});
  makeChart('chTrend',{type:'line',data:{labels:recs.map(r=>shortDate(r.date)),datasets:ds},options:{responsive:true,maintainAspectRatio:false,interaction:{mode:'index',intersect:false},plugins:{legend:{position:'bottom'},tooltip:{callbacks:{label:ctx=>` ${ctx.dataset.label}: ${fmtP(ctx.parsed.y/k)}`}}},scales:{y:{title:{display:true,text:unitLabel()},ticks:{callback:v=>fmtP(v/k)}},x:{ticks:{maxTicksLimit:12}}}}});
}

// ---------- COMPARE ----------
function renderCompare(){
  const app=$('#app'),cs=state.compare;
  if(!DB.crops.size){app.innerHTML=emptyState('No data','Import price data first.','import');return;}
  const byMarkets=cs.mode==='markets';
  if(!DB.crops.has(cs.crop))cs.crop=cropsList()[0].id;if(!DB.markets.has(cs.market))cs.market=marketsList()[0].id;
  const maxDate=allPrices().at(-1).date;const from=cs.range==='all'?'':addDays(maxDate,-(cs.range-1));
  const availMarkets=marketsList().filter(m=>pairSeries().has(pairKey(cs.crop,m.id)));
  const availCrops=cropsList().filter(c=>pairSeries().has(pairKey(c.id,cs.market)));
  const selected=byMarkets?(cs.markets.length?cs.markets.filter(id=>availMarkets.some(m=>m.id===id)):availMarkets.slice(0,6).map(m=>m.id)):(cs.crops.length?cs.crops.filter(id=>availCrops.some(c=>c.id===id)):availCrops.slice(0,6).map(c=>c.id));
  app.innerHTML=`<h2>Compare</h2>
  <div class="card" style="margin-bottom:14px"><div class="filters">
    <label>Mode<div class="seg"><button data-mode="markets" class="${byMarkets?'on':''}">One crop, many markets</button><button data-mode="crops" class="${!byMarkets?'on':''}">One market, many crops</button></div></label>
    ${byMarkets?`<label>Crop<select id="ccrop">${optsHTML(cropsList(),cs.crop)}</select></label>`:`<label>Market<select id="cmarket">${optsHTML(marketsList(),cs.market)}</select></label>`}
    <label>Range<div class="seg">${[7,30,90,'all'].map(r=>`<button data-r="${r}" class="${String(cs.range)===String(r)?'on':''}">${r==='all'?'All':r+'d'}</button>`).join('')}</div></label>
  </div>
  <div style="margin-top:10px"><div class="note" style="margin-bottom:6px">${byMarkets?'Markets':'Crops'} to compare:</div><div class="chk" id="cchk">${(byMarkets?availMarkets:availCrops).map(x=>`<label><input type="checkbox" value="${x.id}" ${selected.includes(x.id)?'checked':''}>${esc(x.name)}</label>`).join('')||'<span class="note">Nothing available for this selection.</span>'}</div></div></div>
  <div id="cmpBody"></div>`;
  $$('[data-mode]',app).forEach(b=>b.onclick=()=>{cs.mode=b.dataset.mode;render();});
  $$('[data-r]',app).forEach(b=>b.onclick=()=>{cs.range=b.dataset.r==='all'?'all':+b.dataset.r;render();});
  const cc=$('#ccrop');if(cc)cc.onchange=e=>{cs.crop=e.target.value;cs.markets=[];render();};
  const cm=$('#cmarket');if(cm)cm.onchange=e=>{cs.market=e.target.value;cs.crops=[];render();};
  $('#cchk').onchange=()=>{const ids=$$('#cchk input:checked').map(i=>i.value);if(byMarkets)cs.markets=ids;else cs.crops=ids;render();};
  const body=$('#cmpBody');
  const items=selected.map(id=>{const recs=byMarkets?seriesFor(cs.crop,id,from):seriesFor(id,cs.market,from);return{id,name:byMarkets?DB.markets.get(id).name:DB.crops.get(id).name,recs,stats:computeStats(recs)};}).filter(x=>x.stats);
  if(items.length<1){body.innerHTML=emptyState('Nothing to compare','Select at least one item with data in this range.');return;}
  const byLatest=[...items].sort((a,b)=>b.stats.last-a.stats.last);const hi=byLatest[0],lo=byLatest.at(-1);
  const spread=items.length>1?(hi.stats.last-lo.stats.last)/lo.stats.last*100:0;
  const subject=byMarkets?DB.crops.get(cs.crop).name:DB.markets.get(cs.market).name;
  body.innerHTML=`${items.length>1?`<div class="insight">${byMarkets?`<b>${esc(subject)}</b> currently fetches the most at <b>${esc(hi.name)}</b> (${fmtP(hi.stats.last)}) and the least at <b>${esc(lo.name)}</b> (${fmtP(lo.stats.last)}) — a <b>${spread.toFixed(1)}%</b> spread. Sellers may prefer ${esc(hi.name)}; buyers ${esc(lo.name)} (before logistics cost).`:`At <b>${esc(subject)}</b>, <b>${esc(hi.name)}</b> is the highest-priced selected crop (${fmtP(hi.stats.last)}); <b>${esc([...items].sort((a,b)=>b.stats.changePct-a.stats.changePct)[0].name)}</b> has gained the most over the period.`}</div>`:''}
  <div class="grid g2"><div class="card"><h3>Average vs latest modal (${unitLabel()})</h3><div class="chart"><canvas id="chBar"></canvas></div></div>
  <div class="card"><h3>Indexed trend (start of period = 100)</h3><div class="chart"><canvas id="chIdx"></canvas></div></div></div>
  <div class="card"><h3>Comparison table</h3><div class="tbl-wrap"><table><thead><tr><th>${byMarkets?'Market':'Crop'}</th><th class="num">Latest</th><th>As of</th><th class="num">Average</th><th class="num">Min–Max</th><th class="num">Period Δ</th><th class="num">Volatility</th><th class="num">Points</th><th></th></tr></thead><tbody>
  ${items.map((x,i)=>`<tr><td><span style="display:inline-block;width:10px;height:10px;border-radius:2px;background:${PALETTE[i%PALETTE.length]};margin-right:6px"></span>${esc(x.name)}${x===hi&&items.length>1?' <span class="tag ok">highest</span>':''}${x===lo&&items.length>1?' <span class="tag off">lowest</span>':''}</td><td class="num"><b>${fmtP(x.stats.last)}</b></td><td>${shortDate(x.stats.lastDate)}</td><td class="num">${fmtP(x.stats.avg)}</td><td class="num">${fmtP(x.stats.lo)} – ${fmtP(x.stats.hi)}</td><td class="num ${pctClass(x.stats.changePct)}">${fmtPct(x.stats.changePct)}</td><td class="num">${x.stats.vol.toFixed(2)}%</td><td class="num">${x.stats.count}</td><td><button class="ghost sm" data-c="${byMarkets?cs.crop:x.id}" data-m="${byMarkets?x.id:cs.market}">Trend</button></td></tr>`).join('')}
  </tbody></table></div></div>`;
  $$('button[data-c]',body).forEach(b=>b.onclick=()=>navigate('trends',{crop:b.dataset.c,market:b.dataset.m}));
  const k=dispFactor();
  makeChart('chBar',{type:'bar',data:{labels:items.map(x=>x.name),datasets:[{label:'Average modal',data:items.map(x=>x.stats.avg*k),backgroundColor:'rgba(31,122,63,.45)'},{label:'Latest modal',data:items.map(x=>x.stats.last*k),backgroundColor:'#1f7a3f'}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'bottom'},tooltip:{callbacks:{label:c=>` ${c.dataset.label}: ${fmtP(c.parsed.y/k)}`}}},scales:{y:{beginAtZero:false,ticks:{callback:v=>fmtP(v/k)}}}}});
  const dates=[...new Set(items.flatMap(x=>x.recs.map(r=>r.date)))].sort();
  makeChart('chIdx',{type:'line',data:{labels:dates.map(shortDate),datasets:items.map((x,i)=>{const base=x.recs[0].modal;const map=new Map(x.recs.map(r=>[r.date,r.modal/base*100]));return{label:x.name,data:dates.map(d=>map.has(d)?+map.get(d).toFixed(2):null),borderColor:PALETTE[i%PALETTE.length],borderWidth:2,pointRadius:0,spanGaps:true,tension:.25};})},options:{responsive:true,maintainAspectRatio:false,interaction:{mode:'index',intersect:false},plugins:{legend:{position:'bottom'}},scales:{y:{title:{display:true,text:'Index'}},x:{ticks:{maxTicksLimit:10}}}}});
}

// ---------- ALERTS ----------
function renderAlerts(){
  const app=$('#app');const evals=evaluateAlerts();
  app.innerHTML=`<h2>Price alerts</h2>
  <div class="grid g2">
  <div class="card"><h3>Create alert</h3><form id="alertForm" class="filters" style="align-items:flex-end">
    <label>Crop<select name="crop" required>${optsHTML(cropsList(),'', 'Select crop…')}</select></label>
    <label>Market<select name="market">${optsHTML(marketsList(),'','Any market')}</select></label>
    <label>Condition<select name="cond"><option value="below">Modal drops below</option><option value="above">Modal rises above</option></select></label>
    <label>Threshold (${unitLabel()})<input type="number" name="threshold" min="0" step="any" required placeholder="e.g. ${state.unit==='kg'?'20':'2000'}"></label>
    <label>&nbsp;<button type="submit">Add alert</button></label>
  </form><div class="note" style="margin-top:8px">Alerts are evaluated against the latest reported modal price of each market and re-checked automatically whenever new data is imported. Stored locally in your browser.</div></div>
  <div class="card"><h3>Triggered now (${evals.filter(e=>e.hits.length).length})</h3><div class="list">${evals.filter(e=>e.hits.length).flatMap(({alert,hits})=>hits.map(h=>`<div class="row" data-c="${h.cropId}" data-m="${h.marketId}"><div><div class="n">🔔 ${esc(DB.crops.get(h.cropId).name)} @ ${esc(DB.markets.get(h.marketId).name)}</div><div class="m">${alert.cond} ${fmtP(alert.threshold)} · reported ${shortDate(h.date)}</div></div><div class="p ${alert.cond==='below'?'down':'up'}">${fmtP(h.modal)}</div></div>`)).join('')||'<div class="note">No alerts triggered right now.</div>'}</div></div>
  </div>
  <div class="card"><h3>All alerts (${state.alerts.length})</h3>${state.alerts.length?`<div class="tbl-wrap"><table><thead><tr><th>Status</th><th>Crop</th><th>Market</th><th>Condition</th><th class="num">Threshold</th><th class="num">Current modal</th><th>Created</th><th></th></tr></thead><tbody>
  ${evals.map(({alert:a,hits})=>{const c=DB.crops.get(a.cropId),m=a.marketId?DB.markets.get(a.marketId):null;const latest=latestByPair();const cur=m?latest.get(pairKey(a.cropId,a.marketId)):null;
    const curTxt=m?(cur?`${fmtP(cur.modal)} <span class="note">(${shortDate(cur.date)})</span>`:'—'):`${hits.length} of ${[...latest.values()].filter(r=>r.cropId===a.cropId).length} markets`;
    return`<tr><td>${a.active===false?'<span class="tag off">paused</span>':hits.length?'<span class="tag hot">triggered</span>':'<span class="tag ok">watching</span>'}</td><td>${esc(c?c.name:a.cropId)}</td><td>${m?esc(m.name):'<i>Any market</i>'}</td><td>${a.cond==='below'?'drops below':'rises above'}</td><td class="num">${fmtP(a.threshold)}</td><td class="num">${curTxt}</td><td class="note">${a.created}</td><td><button class="ghost sm" data-toggle="${a.id}">${a.active===false?'Resume':'Pause'}</button> <button class="danger sm" data-del="${a.id}">Delete</button></td></tr>`;}).join('')}
  </tbody></table></div>`:'<div class="note">No alerts yet. Create one above — e.g. "Tomato at Azadpur drops below ₹20/kg".</div>'}</div>`;
  $('#alertForm').onsubmit=e=>{e.preventDefault();const fd=new FormData(e.target);const thr=parseFloat(fd.get('threshold'));
    if(!fd.get('crop')){toast('Select a crop','err');return;}if(!(thr>0)){toast('Threshold must be a positive number','err');return;}
    state.alerts.push({id:Date.now().toString(36),cropId:fd.get('crop'),marketId:fd.get('market')||'',cond:fd.get('cond'),threshold:thr/dispFactor(),created:TODAY,active:true,notified:[]});
    saveAlerts();toast('Alert added');checkAlertsNotify();render();};
  $$('[data-del]',app).forEach(b=>b.onclick=()=>{state.alerts=state.alerts.filter(a=>a.id!==b.dataset.del);saveAlerts();render();});
  $$('[data-toggle]',app).forEach(b=>b.onclick=()=>{const a=state.alerts.find(a=>a.id===b.dataset.toggle);a.active=a.active===false;saveAlerts();render();});
  $$('.row[data-c]',app).forEach(el=>el.onclick=()=>navigate('trends',{crop:el.dataset.c,market:el.dataset.m}));
}

// ---------- IMPORT ----------
function renderImport(){
  const app=$('#app'),im=state.import;
  const bySrc=new Map();for(const p of allPrices()){const s=bySrc.get(p.source)||{n:0,from:p.date,to:p.date};s.n++;if(p.date<s.from)s.from=p.date;if(p.date>s.to)s.to=p.date;bySrc.set(p.source,s);}
  app.innerHTML=`<h2>Import price data</h2>
  <div class="grid g2">
    <div class="card"><h3>1 · CSV upload / paste</h3>
      <div class="drop" id="drop">📄 Drop a CSV here or <u>click to choose a file</u><input type="file" id="file" accept=".csv,text/csv" hidden></div>
      <div class="toolbar" style="margin:10px 0 6px"><button class="ghost sm" id="loadSample">Load sample (with dirty rows)</button><button class="ghost sm" id="dlTemplate">Download template</button><span class="note">${im.fileName?'File: '+esc(im.fileName):''}</span></div>
      <textarea id="csvText" placeholder="crop,market,district,state,date,min_price,max_price,modal_price,unit,arrivals&#10;Tomato,Azadpur,Delhi,Delhi,${TODAY},1400,2600,2000,quintal,310">${esc(im.text)}</textarea>
      <div class="toolbar" style="margin-top:10px"><button id="preview">Validate &amp; preview</button><button id="commit" ${im.preview?'':'disabled'}>Import ${im.preview?im.preview.inserted+im.preview.updated:''} rows</button></div>
      <div class="note" style="margin-top:8px">Accepted columns (case/alias-insensitive): <code>crop|commodity</code>, <code>market|mandi</code>, <code>district</code>, <code>state</code>, <code>date</code> (YYYY-MM-DD or DD/MM/YYYY), <code>min_price</code>, <code>max_price</code>, <code>modal_price</code>, <code>unit</code> (quintal · kg · tonne → normalised to ₹/quintal), <code>arrivals</code>, <code>category</code>.</div>
    </div>
    <div>
      <div class="card" style="margin-bottom:14px"><h3>2 · External feed (mock API)</h3><p class="note" style="margin-top:0">Simulates pulling the next up-to-3 days from an Agmarknet-style JSON feed with different field names, mixed units, and a few malformed records — all handled by the same pipeline.</p><button id="sync">Sync from mock API</button> <span id="syncStatus" class="note"></span></div>
      <div class="card"><h3>Data sources loaded</h3><div class="tbl-wrap"><table><thead><tr><th>Source</th><th class="num">Records</th><th>Coverage</th></tr></thead><tbody>${[...bySrc].map(([s,v])=>`<tr><td>${esc(s)}</td><td class="num">${v.n}</td><td>${v.from} → ${v.to}</td></tr>`).join('')||'<tr><td colspan=3 class="note">None</td></tr>'}</tbody></table></div>
      <div class="toolbar" style="margin-top:10px"><button class="ghost sm" id="exportAll">Export all (CSV)</button><button class="danger sm" id="reset">Reset to seed data</button></div></div>
    </div>
  </div>
  <div id="report">${im.preview?reportHTML(im.preview,true):''}</div>`;
  const drop=$('#drop'),file=$('#file'),ta=$('#csvText');
  drop.onclick=()=>file.click();
  drop.ondragover=e=>{e.preventDefault();drop.classList.add('over');};drop.ondragleave=()=>drop.classList.remove('over');
  drop.ondrop=e=>{e.preventDefault();drop.classList.remove('over');if(e.dataTransfer.files[0])readFile(e.dataTransfer.files[0]);};
  file.onchange=()=>{if(file.files[0])readFile(file.files[0]);};
  function readFile(f){if(f.size>5*1024*1024){toast('File too large (max 5 MB for the browser prototype)','err');return;}const r=new FileReader();r.onload=()=>{im.text=r.result;im.fileName=f.name;im.preview=null;render();setTimeout(()=>$('#preview').click(),0);};r.onerror=()=>toast('Could not read file','err');r.readAsText(f);}
  ta.oninput=()=>{im.text=ta.value;im.preview=null;$('#commit').disabled=true;};
  $('#loadSample').onclick=()=>{im.text=sampleCSV();im.fileName='sample.csv';im.preview=null;render();};
  $('#dlTemplate').onclick=()=>downloadText('agriprice_template.csv',templateCSV());
  $('#preview').onclick=()=>{const parsed=parseCSV(im.text);if(!parsed.rows.length){toast('No data rows found — need a header row plus at least one record','err');return;}
    const mapped=parsed.headers.map(h=>ALIAS_LOOKUP.get(normHeader(h)));const missing=['crop','market','date'].filter(k=>!mapped.includes(k));
    if(missing.length){$('#report').innerHTML=`<div class="card"><b class="down">Cannot import:</b> required column(s) not found: ${missing.map(m=>`<code>${m}</code>`).join(' ')}. Detected headers: ${parsed.headers.map(h=>`<code>${esc(h)}</code>`).join(' ')}</div>`;return;}
    if(!mapped.includes('modal')&&!(mapped.includes('min')&&mapped.includes('max'))){$('#report').innerHTML=`<div class="card"><b class="down">Cannot import:</b> need a <code>modal_price</code> column, or both <code>min_price</code> and <code>max_price</code>.</div>`;return;}
    im.preview=ingestRecords(parsed.rows,'csv:'+(im.fileName||'pasted'),{dryRun:true});im.preview.headerMap=parsed.headers.map((h,i)=>`${h} → ${mapped[i]||'(ignored)'}`);
    $('#report').innerHTML=reportHTML(im.preview,true);$('#commit').disabled=false;$('#commit').textContent=`Import ${im.preview.inserted+im.preview.updated} rows`;};
  $('#commit').onclick=()=>{const parsed=parseCSV(im.text);const rep=ingestRecords(parsed.rows,'csv:'+(im.fileName||'pasted'));im.preview=null;im.text='';im.fileName='';
    render();$('#report').innerHTML=reportHTML(rep,false);toast(`Imported ${rep.inserted} new, ${rep.updated} updated`);checkAlertsNotify();};
  $('#sync').onclick=async()=>{const b=$('#sync');b.disabled=true;$('#syncStatus').textContent='Fetching…';
    try{const res=await mockApiFetch();if(!res.records.length){$('#syncStatus').textContent=res.message||'No new records';b.disabled=false;return;}
      const rep=ingestRecords(res.records,res.source);render();$('#report').innerHTML=reportHTML(rep,false);toast(`Synced ${rep.inserted} new records from ${res.source}`);checkAlertsNotify();}
    catch(e){$('#syncStatus').textContent='Sync failed: '+e.message;b.disabled=false;}};
  $('#exportAll').onclick=()=>downloadText(`agriprice_all_${TODAY}.csv`,toCSV(allPrices().map(toRow)));
  $('#reset').onclick=()=>{if(confirm('Remove all imported data and restore the seeded dataset?')){resetData();render();toast('Reset to seed data');}};
}
function reportHTML(r,dry){return`<div class="card report"><h3>${dry?'Validation preview (nothing written yet)':'Import result'} — <code>${esc(r.source)}</code></h3>
  <div class="grid g5"><div class="kpi"><div class="l">Rows read</div><div class="v">${r.total}</div></div><div class="kpi"><div class="l">${dry?'Will insert':'Inserted'}</div><div class="v up">${r.inserted}</div></div><div class="kpi"><div class="l">${dry?'Will update':'Updated'} existing</div><div class="v">${r.updated}</div></div><div class="kpi"><div class="l">Skipped (invalid)</div><div class="v ${r.skipped?'down':''}">${r.skipped}</div></div><div class="kpi"><div class="l">In-batch duplicates</div><div class="v ${r.duplicates?'warn':''}">${r.duplicates}</div></div></div>
  ${r.newCrops.size||r.newMarkets.size?`<div class="note">New crops: ${[...r.newCrops].map(esc).join(', ')||'none'} · New markets: ${[...r.newMarkets].map(esc).join(', ')||'none'}</div>`:''}
  ${r.headerMap?`<details><summary class="note">Column mapping</summary><ul>${r.headerMap.map(h=>`<li>${esc(h)}</li>`).join('')}</ul></details>`:''}
  ${r.errors.length?`<details open><summary class="down">${r.errors.length} error(s) — rows skipped</summary><ul>${r.errors.slice(0,100).map(e=>`<li>${esc(e)}</li>`).join('')}${r.errors.length>100?'<li>…</li>':''}</ul></details>`:''}
  ${r.warnings.length?`<details><summary class="warn">${r.warnings.length} warning(s) — rows auto-corrected</summary><ul>${r.warnings.slice(0,100).map(e=>`<li>${esc(e)}</li>`).join('')}${r.warnings.length>100?'<li>…</li>':''}</ul></details>`:''}
  </div>`;}

/* =====================================================================
   6. BOOT
   ===================================================================== */
(function boot(){
  seedData();restoreUserData();
  $('#unitSel').value=state.unit;
  $('#unitSel').onchange=e=>{state.unit=e.target.value;localStorage.setItem(LS.unit,state.unit);render();};
  window.addEventListener('hashchange',render);
  render();checkAlertsNotify();
})();
</script>
</body>
</html>
