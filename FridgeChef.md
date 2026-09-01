<!doctype html>
<html lang="it">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="FridgeChef">
<meta name="theme-color" content="#10130f">
<title>FridgeChef</title>
<style>
:root{
  --bg:#10130f;--panel:#171c15;--panel2:#20271d;--text:#f7f5ef;--muted:#aeb5a8;
  --line:#2b3428;--accent:#b7e66b;--accent2:#f4c95d;--danger:#ff8c82;--shadow:0 16px 42px rgba(0,0,0,.3);
  --r:22px;
}
*{box-sizing:border-box}
html,body{margin:0;background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,"SF Pro Display","Segoe UI",sans-serif}
body{min-height:100dvh;padding-bottom:90px}
button,input,select{font:inherit}
button{cursor:pointer}
.safe{height:env(safe-area-inset-top)}
header{position:sticky;top:0;z-index:20;padding:12px 16px 14px;background:linear-gradient(180deg,rgba(16,19,15,.99),rgba(16,19,15,.94),rgba(16,19,15,.72))}
.head{display:flex;align-items:center;gap:10px}
.brand{font-size:23px;font-weight:850;letter-spacing:-.045em;flex:1}
.brand span{color:var(--accent)}
.status{font-size:11px;color:var(--muted);display:flex;align-items:center;gap:6px}
.dot{width:8px;height:8px;border-radius:50%;background:var(--accent)}
.iconbtn{width:42px;height:42px;border-radius:14px;border:1px solid var(--line);background:var(--panel);color:var(--text)}
.hero{padding:10px 16px 2px}
.hero h1{font-size:31px;line-height:.98;margin:6px 0 10px;letter-spacing:-.05em}
.hero p{color:var(--muted);line-height:1.45;margin:0 0 14px;font-size:14px}
.panel{background:var(--panel);border:1px solid var(--line);border-radius:var(--r);padding:14px;box-shadow:var(--shadow)}
.fieldwrap{position:relative}
.field{width:100%;border:1px solid var(--line);background:#11150f;color:var(--text);border-radius:16px;padding:14px 14px;outline:none}
.field:focus{border-color:#5b6e50}
.addrow{display:grid;grid-template-columns:1fr auto;gap:9px}
.btn{border:0;border-radius:15px;padding:13px 15px;font-weight:800;background:var(--accent);color:#15200d}
.btn.secondary{background:var(--panel2);color:var(--text);border:1px solid var(--line)}
.btn.ghost{background:transparent;color:var(--muted);border:1px solid var(--line)}
.btn.danger{background:#321b18;color:#ffc5bf;border:1px solid #56302a}
.chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:11px}
.chip{display:inline-flex;align-items:center;gap:7px;padding:8px 10px;border-radius:999px;background:var(--panel2);border:1px solid var(--line);font-size:13px;color:#dfe5db}
.chip button{border:0;background:transparent;color:var(--muted);padding:0;font-size:15px}
.actions{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-top:12px}
.tip{font-size:11px;color:var(--muted);margin-top:10px;line-height:1.4}
main{padding:8px 16px 18px}
.sectionhead{display:flex;align-items:flex-end;gap:10px;margin:14px 0 12px}
.sectionhead h2{font-size:24px;margin:0;letter-spacing:-.04em;flex:1}
.sectionhead span{font-size:12px;color:var(--muted)}
.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:14px}
.card{min-width:0;position:relative}
.thumb{aspect-ratio:1/1;border-radius:19px;overflow:hidden;background:var(--panel);border:1px solid var(--line)}
.thumb img{width:100%;height:100%;object-fit:cover;display:block}
.meta{padding:8px 2px 0}
.title{font-size:15px;font-weight:760;line-height:1.2;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden}
.sub{font-size:12px;color:var(--muted);margin-top:5px;display:flex;gap:5px;align-items:center}
.match{position:absolute;left:8px;top:8px;background:rgba(16,19,15,.82);backdrop-filter:blur(8px);border:1px solid rgba(255,255,255,.1);padding:6px 8px;border-radius:10px;font-size:11px;font-weight:800}
.fav{position:absolute;right:8px;top:8px;width:36px;height:36px;border-radius:12px;border:0;background:rgba(16,19,15,.82);color:white;font-size:19px;backdrop-filter:blur(8px)}
.empty{grid-column:1/-1;border:1px dashed var(--line);background:var(--panel);border-radius:20px;padding:28px;text-align:center;color:var(--muted);line-height:1.5}
.loader{grid-column:1/-1;text-align:center;padding:44px 0;color:var(--muted)}
.spinner{width:30px;height:30px;border:3px solid var(--line);border-top-color:var(--accent);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 10px}
@keyframes spin{to{transform:rotate(360deg)}}
.tabs{position:fixed;z-index:25;left:12px;right:12px;bottom:max(10px,env(safe-area-inset-bottom));height:66px;border-radius:22px;border:1px solid var(--line);background:rgba(23,28,21,.95);backdrop-filter:blur(16px);display:grid;grid-template-columns:repeat(4,1fr);box-shadow:var(--shadow)}
.tab{border:0;background:transparent;color:var(--muted);display:flex;flex-direction:column;gap:3px;align-items:center;justify-content:center;font-size:11px}
.tab b{font-size:19px;line-height:1}
.tab.on{color:var(--text)}
.screen{display:none}.screen.on{display:block}
.searchbar{display:grid;grid-template-columns:1fr auto;gap:9px;margin-bottom:12px}
.filters{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:14px}
.filters select{width:100%;border:1px solid var(--line);background:var(--panel);color:var(--text);border-radius:14px;padding:12px}
.overlay{position:fixed;inset:0;z-index:50;background:rgba(0,0,0,.64);backdrop-filter:blur(8px);display:none;align-items:flex-end}
.overlay.open{display:flex}
.sheet{width:100%;max-height:93dvh;overflow:auto;background:var(--panel);border-radius:29px 29px 0 0;border:1px solid var(--line);padding:17px 17px calc(26px + env(safe-area-inset-bottom));box-shadow:var(--shadow)}
.handle{width:43px;height:5px;background:#485143;border-radius:99px;margin:0 auto 16px}
.detailtop{display:grid;grid-template-columns:120px 1fr;gap:15px}
.detailimg{width:120px;aspect-ratio:1/1;border-radius:19px;object-fit:cover;background:#11150f}
.kicker{font-size:11px;font-weight:850;letter-spacing:.1em;text-transform:uppercase;color:var(--accent)}
.sheet h2{font-size:25px;margin:3px 0 7px;letter-spacing:-.04em}
.pills{display:flex;gap:6px;flex-wrap:wrap;margin-top:9px}
.pill{font-size:11px;border:1px solid var(--line);background:#11150f;color:#d8dfd3;border-radius:999px;padding:6px 8px}
.sectiontitle{font-size:16px;margin:20px 0 9px}
.ingredients{display:grid;gap:7px}
.ingredient{display:grid;grid-template-columns:1fr auto;gap:8px;border-bottom:1px solid var(--line);padding:8px 1px;font-size:13px}
.ingredient span:last-child{color:var(--muted);text-align:right}
.instructions{white-space:pre-line;line-height:1.55;color:#dce3d7;font-size:14px}
.notice{margin:12px 0;padding:12px;border-radius:15px;background:#182316;border:1px solid #31492b;color:#d9f5c4;font-size:12px;line-height:1.45}
.error{margin:12px 0;padding:12px;border-radius:15px;background:#2a1816;border:1px solid #57312c;color:#ffd0cb;font-size:12px;line-height:1.45}
.suggestionbox{position:absolute;left:0;right:0;top:52px;z-index:10;background:#121710;border:1px solid var(--line);border-radius:14px;max-height:220px;overflow:auto;display:none;box-shadow:var(--shadow)}
.suggestionbox.open{display:block}
.suggestion{padding:11px 12px;border-bottom:1px solid var(--line);font-size:13px}
.suggestion:last-child{border-bottom:0}
.randomHero{display:grid;grid-template-columns:130px 1fr;gap:14px}
.randomHero img{width:130px;aspect-ratio:1/1;border-radius:20px;object-fit:cover}
.muted{color:var(--muted);font-size:13px;line-height:1.45}
.about{font-size:12px;color:var(--muted);line-height:1.55}
@media(min-width:720px){
 body{max-width:980px;margin:0 auto}
 .grid{grid-template-columns:repeat(4,minmax(0,1fr))}
 .tabs{left:50%;right:auto;transform:translateX(-50%);width:min(680px,calc(100% - 24px))}
 .sheet{max-width:680px;margin:0 auto}
}
</style>
</head>
<body>
<div class="safe"></div>
<header>
  <div class="head">
    <div class="brand">Fridge<span>Chef</span></div>
    <div class="status"><span class="dot"></span> TheMealDB</div>
    <button class="iconbtn" id="aboutBtn" aria-label="Info">ⓘ</button>
  </div>
</header>

<section id="fridgeScreen" class="screen on">
  <div class="hero">
    <h1>Cosa hai<br>in frigo?</h1>
    <p>Inserisci gli ingredienti che hai già. FridgeChef trova le ricette che ne utilizzano il maggior numero.</p>
    <div class="panel">
      <div class="addrow">
        <div class="fieldwrap">
          <input id="ingredientInput" class="field" placeholder="es. pollo, pomodoro, limone" autocomplete="off">
          <div id="ingredientSuggestions" class="suggestionbox"></div>
        </div>
        <button id="addIngredient" class="btn">Aggiungi</button>
      </div>
      <div id="ingredientChips" class="chips"></div>
      <div class="actions">
        <button id="findRecipes" class="btn">Trova ricette</button>
        <button id="clearIngredients" class="btn secondary">Svuota</button>
      </div>
      <div class="tip">Puoi scrivere in italiano. Esempi: pollo, manzo, salmone, tonno, pomodoro, patate, riso, pasta, uova, mozzarella, limone.</div>
    </div>
  </div>
  <main>
    <div class="sectionhead">
      <h2 id="fridgeTitle">Idee per te</h2>
      <span id="fridgeCount"></span>
    </div>
    <div id="fridgeResults" class="grid">
      <div class="empty">Aggiungi almeno un ingrediente e premi <strong>Trova ricette</strong>.</div>
    </div>
  </main>
</section>

<section id="searchScreen" class="screen">
  <main>
    <div class="sectionhead"><h2>Cerca</h2><span>per nome</span></div>
    <div class="searchbar">
      <input id="mealSearch" class="field" placeholder="es. carbonara, curry, salmon">
      <button id="mealSearchBtn" class="btn">Cerca</button>
    </div>
    <div id="searchResults" class="grid">
      <div class="empty">Cerca una ricetta per nome. Il database internazionale utilizza spesso i nomi originali o inglesi.</div>
    </div>
  </main>
</section>

<section id="exploreScreen" class="screen">
  <main>
    <div class="sectionhead"><h2>Esplora</h2><span>scopri qualcosa</span></div>
    <div class="filters">
      <select id="categorySelect"><option value="">Categoria</option></select>
      <select id="areaSelect"><option value="">Cucina</option></select>
    </div>
    <div class="actions" style="margin:0 0 14px">
      <button id="browseBtn" class="btn">Mostra</button>
      <button id="randomBtn" class="btn secondary">Ricetta casuale</button>
    </div>
    <div id="exploreResults" class="grid">
      <div class="empty">Scegli una categoria o una cucina, oppure prova una ricetta casuale.</div>
    </div>
  </main>
</section>

<section id="favoritesScreen" class="screen">
  <main>
    <div class="sectionhead"><h2>Preferiti</h2><span id="favCount"></span></div>
    <div id="favoriteResults" class="grid"></div>
  </main>
</section>

<nav class="tabs">
  <button class="tab on" data-screen="fridgeScreen"><b>⌂</b><span>Frigo</span></button>
  <button class="tab" data-screen="searchScreen"><b>⌕</b><span>Cerca</span></button>
  <button class="tab" data-screen="exploreScreen"><b>✦</b><span>Esplora</span></button>
  <button class="tab" data-screen="favoritesScreen"><b>♡</b><span>Preferiti</span></button>
</nav>

<div class="overlay" id="detailOverlay">
  <div class="sheet">
    <div class="handle"></div>
    <div id="detailContent"></div>
  </div>
</div>

<div class="overlay" id="aboutOverlay">
  <div class="sheet">
    <div class="handle"></div>
    <div style="display:flex;align-items:center;gap:10px">
      <h2 style="flex:1">FridgeChef</h2>
      <button class="iconbtn" data-close="aboutOverlay">×</button>
    </div>
    <div class="notice"><strong>Già pronto:</strong> utilizza la chiave gratuita di sviluppo <strong>1</strong> di TheMealDB. Non devi inserire nessuna API key.</div>
    <p class="about">
      I dati delle ricette e le immagini provengono da TheMealDB. L'app salva ingredienti e preferiti esclusivamente nel localStorage del browser.
      Il piano gratuito permette il filtro per un singolo ingrediente; FridgeChef interroga separatamente i tuoi ingredienti e incrocia i risultati direttamente sul dispositivo.
    </p>
    <p class="about">
      Le istruzioni delle ricette dipendono dalla lingua presente nel database e possono essere in inglese. Se usi Safari puoi utilizzare la funzione di traduzione della pagina quando disponibile.
    </p>
    <p class="about">
      La chiave gratuita “1” è indicata da TheMealDB per sviluppo, apprendimento e progetti personali. Per un rilascio pubblico commerciale o su App Store va verificato il piano previsto dal servizio.
    </p>
    <button id="resetApp" class="btn danger">Cancella dati locali</button>
  </div>
</div>

<script>
(() => {
'use strict';

const API_KEY = '1';
const BASE = `https://www.themealdb.com/api/json/v1/${API_KEY}`;
const LS = {
  pantry:'fridgechef_pantry_v1',
  favs:'fridgechef_favorites_v1'
};

const IT_TO_EN = {
  'pollo':'chicken','petto di pollo':'chicken breast','manzo':'beef','carne macinata':'minced beef',
  'maiale':'pork','agnello':'lamb','salmone':'salmon','tonno':'tuna','gamberi':'prawns','gamberetti':'shrimp',
  'merluzzo':'cod','pesce':'fish','uova':'eggs','uovo':'egg','latte':'milk','burro':'butter',
  'panna':'cream','formaggio':'cheese','parmigiano':'parmesan','mozzarella':'mozzarella',
  'ricotta':'ricotta','yogurt':'yogurt','pomodoro':'tomato','pomodori':'tomatoes',
  'passata':'passata','patata':'potato','patate':'potatoes','cipolla':'onion','cipolle':'onions',
  'aglio':'garlic','carota':'carrot','carote':'carrots','zucchina':'courgettes','zucchine':'courgettes',
  'melanzana':'aubergine','melanzane':'aubergine','peperone':'red pepper','peperoni':'red pepper',
  'spinaci':'spinach','broccoli':'broccoli','cavolfiore':'cauliflower','funghi':'mushrooms',
  'piselli':'peas','fagioli':'beans','ceci':'chickpeas','lenticchie':'lentils','mais':'sweetcorn',
  'riso':'rice','pasta':'pasta','spaghetti':'spaghetti','tagliatelle':'tagliatelle',
  'farina':'flour','pane':'bread','pangrattato':'breadcrumbs','olio':'olive oil','olio evo':'olive oil',
  'aceto':'vinegar','limone':'lemon','lime':'lime','arancia':'orange','mela':'apple','mele':'apples',
  'banana':'banana','banane':'bananas','fragole':'strawberries','mirtilli':'blueberries',
  'avocado':'avocado','basilico':'basil','prezzemolo':'parsley','rosmarino':'rosemary',
  'salvia':'sage','timo':'thyme','origano':'oregano','menta':'mint','coriandolo':'coriander',
  'peperoncino':'chilli','zenzero':'ginger','curry':'curry powder','paprika':'paprika',
  'senape':'mustard','miele':'honey','zucchero':'sugar','cioccolato':'chocolate','cacao':'cocoa',
  'noci':'walnuts','mandorle':'almonds','nocciole':'hazelnuts','pinoli':'pine nuts',
  'acciughe':'anchovy','acciuga':'anchovy','capperi':'capers','olive':'olives',
  'prosciutto':'ham','pancetta':'bacon','salsiccia':'sausage','salsicce':'sausages'
};

const EN_TO_IT = Object.fromEntries(Object.entries(IT_TO_EN).map(([it,en])=>[en,it]));

const state = {
  pantry: JSON.parse(localStorage.getItem(LS.pantry)||'[]'),
  favs: new Set(JSON.parse(localStorage.getItem(LS.favs)||'[]')),
  ingredientList: [],
  lastCards: []
};

const $ = s => document.querySelector(s);
const $$ = s => [...document.querySelectorAll(s)];
const esc = s => String(s??'').replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#039;'}[m]));

async function api(path, params={}){
  const url = new URL(BASE + path);
  Object.entries(params).forEach(([k,v])=>{
    if(v!=='' && v!==null && v!==undefined) url.searchParams.set(k,String(v));
  });
  const r = await fetch(url);
  if(!r.ok) throw new Error(`TheMealDB: errore ${r.status}`);
  return r.json();
}

function normalizeText(s){
  return String(s||'').trim().toLowerCase().replace(/\s+/g,' ');
}
function toApiIngredient(raw){
  const n = normalizeText(raw);
  return IT_TO_EN[n] || n;
}
function prettyIngredient(raw){
  const n = normalizeText(raw);
  return EN_TO_IT[n] || raw;
}
function cardKey(m){return String(m.idMeal)}
function saved(m){return state.favs.has(cardKey(m))}
function persistPantry(){localStorage.setItem(LS.pantry,JSON.stringify(state.pantry))}
function persistFavs(){localStorage.setItem(LS.favs,JSON.stringify([...state.favs]))}

function setScreen(id){
  $$('.screen').forEach(s=>s.classList.toggle('on',s.id===id));
  $$('.tab').forEach(t=>t.classList.toggle('on',t.dataset.screen===id));
  if(id==='favoritesScreen') renderFavorites();
}
$$('.tab').forEach(t=>t.onclick=()=>setScreen(t.dataset.screen));

function renderPantry(){
  $('#ingredientChips').innerHTML = state.pantry.map((x,i)=>`
    <span class="chip">${esc(x.original)}<button data-remove="${i}" aria-label="Rimuovi">×</button></span>
  `).join('');
  $$('[data-remove]').forEach(b=>b.onclick=()=>{
    state.pantry.splice(Number(b.dataset.remove),1);
    persistPantry(); renderPantry();
  });
}
function addIngredient(raw){
  raw = raw.trim();
  if(!raw) return;
  const parts = raw.split(',').map(x=>x.trim()).filter(Boolean);
  for(const p of parts){
    const apiName = toApiIngredient(p);
    if(!state.pantry.some(x=>x.api===apiName)){
      state.pantry.push({original:p,api:apiName});
    }
  }
  persistPantry(); renderPantry(); $('#ingredientInput').value=''; hideSuggestions();
}
$('#addIngredient').onclick=()=>addIngredient($('#ingredientInput').value);
$('#ingredientInput').addEventListener('keydown',e=>{
  if(e.key==='Enter'){e.preventDefault();addIngredient(e.target.value)}
});
$('#clearIngredients').onclick=()=>{
  state.pantry=[];persistPantry();renderPantry();
  $('#fridgeResults').innerHTML='<div class="empty">Aggiungi almeno un ingrediente e premi <strong>Trova ricette</strong>.</div>';
  $('#fridgeCount').textContent='';
};

function loader(el,text='Cerco ricette…'){
  el.innerHTML=`<div class="loader"><div class="spinner"></div>${esc(text)}</div>`;
}
function error(el,msg){
  el.innerHTML=`<div class="empty">⚠️ ${esc(msg)}</div>`;
}

async function findFromPantry(){
  const out=$('#fridgeResults');
  if(!state.pantry.length){return error(out,'Inserisci almeno un ingrediente.')}
  loader(out,'Incrocio gli ingredienti…');
  $('#fridgeTitle').textContent='Risultati';
  try{
    const lists = await Promise.all(state.pantry.map(async ing=>{
      const j=await api('/filter.php',{i:ing.api.replace(/\s+/g,'_')});
      return {ing, meals:j.meals||[]};
    }));
    const score = new Map();
    for(const {ing,meals} of lists){
      for(const m of meals){
        const id=String(m.idMeal);
        if(!score.has(id)) score.set(id,{...m,matched:[],score:0});
        const x=score.get(id);x.matched.push(ing.original);x.score++;
      }
    }
    const all=[...score.values()].sort((a,b)=>b.score-a.score || a.strMeal.localeCompare(b.strMeal));
    state.lastCards=all;
    $('#fridgeCount').textContent = `${all.length} trovate`;
    if(!all.length){
      return error(out,'Nessuna ricetta trovata. Prova ingredienti più semplici o in inglese.');
    }
    renderCards(out,all.slice(0,40),true);
  }catch(e){error(out,e.message)}
}
$('#findRecipes').onclick=findFromPantry;

function renderCards(el,meals,showMatch=false){
  if(!meals.length){el.innerHTML='<div class="empty">Nessun risultato.</div>';return}
  el.innerHTML=meals.map(m=>`
    <article class="card" data-card="${m.idMeal}">
      <div class="thumb" data-open="${m.idMeal}">
        <img loading="lazy" src="${esc(m.strMealThumb||'')}" alt="${esc(m.strMeal)}">
      </div>
      ${showMatch && m.score ? `<div class="match">${m.score}/${state.pantry.length} ingredienti</div>`:''}
      <button class="fav" data-fav="${m.idMeal}" aria-label="Preferito">${saved(m)?'♥':'♡'}</button>
      <div class="meta" data-open="${m.idMeal}">
        <div class="title">${esc(m.strMeal)}</div>
        <div class="sub">${m.matched?.length?esc(m.matched.join(' · ')):'Apri la ricetta'}</div>
      </div>
    </article>
  `).join('');
  $$('[data-open]').forEach(x=>x.onclick=()=>openDetail(x.dataset.open));
  $$('[data-fav]').forEach(b=>b.onclick=e=>{
    e.stopPropagation();
    const id=String(b.dataset.fav);
    if(state.favs.has(id)) state.favs.delete(id); else state.favs.add(id);
    persistFavs(); b.textContent=state.favs.has(id)?'♥':'♡';
  });
}

async function openDetail(id){
  $('#detailOverlay').classList.add('open');
  $('#detailContent').innerHTML='<div class="loader"><div class="spinner"></div>Carico la ricetta…</div>';
  try{
    const j=await api('/lookup.php',{i:id});
    const m=j.meals?.[0];
    if(!m) throw new Error('Ricetta non trovata.');
    const ingredients=[];
    for(let i=1;i<=20;i++){
      const ing=(m['strIngredient'+i]||'').trim();
      const measure=(m['strMeasure'+i]||'').trim();
      if(ing) ingredients.push([prettyIngredient(ing),measure]);
    }
    $('#detailContent').innerHTML=`
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:13px">
        <div class="kicker" style="flex:1">${esc(m.strArea||'')} · ${esc(m.strCategory||'')}</div>
        <button class="iconbtn" data-close="detailOverlay">×</button>
      </div>
      <div class="detailtop">
        <img class="detailimg" src="${esc(m.strMealThumb||'')}" alt="">
        <div>
          <h2>${esc(m.strMeal)}</h2>
          <div class="pills">
            ${m.strCategory?`<span class="pill">${esc(m.strCategory)}</span>`:''}
            ${m.strArea?`<span class="pill">${esc(m.strArea)}</span>`:''}
            ${m.strTags?m.strTags.split(',').slice(0,3).map(t=>`<span class="pill">${esc(t.trim())}</span>`).join(''):''}
          </div>
          <button id="detailFav" class="btn secondary" style="margin-top:12px">${state.favs.has(String(id))?'♥ Preferita':'♡ Salva'}</button>
        </div>
      </div>
      <h3 class="sectiontitle">Ingredienti</h3>
      <div class="ingredients">
        ${ingredients.map(([i,q])=>`<div class="ingredient"><span>${esc(i)}</span><span>${esc(q)}</span></div>`).join('')}
      </div>
      <h3 class="sectiontitle">Preparazione</h3>
      <div class="instructions">${esc(m.strInstructions||'Istruzioni non disponibili.')}</div>
      ${m.strYoutube?`<p style="margin-top:18px"><a class="btn secondary" style="display:inline-block;text-decoration:none" href="${esc(m.strYoutube)}" target="_blank" rel="noopener">Video ricetta</a></p>`:''}
      <div class="notice">Le istruzioni sono mostrate nella lingua disponibile su TheMealDB. Safari può offrire la traduzione della pagina.</div>
    `;
    $('#detailFav').onclick=()=>{
      const k=String(id);
      if(state.favs.has(k)) state.favs.delete(k); else state.favs.add(k);
      persistFavs();
      $('#detailFav').textContent=state.favs.has(k)?'♥ Preferita':'♡ Salva';
    };
    $$('[data-close]').forEach(bindClose);
  }catch(e){error($('#detailContent'),e.message)}
}

async function searchMeals(){
  const q=$('#mealSearch').value.trim();
  if(!q)return;
  const out=$('#searchResults');loader(out,'Cerco…');
  try{
    const j=await api('/search.php',{s:q});
    const meals=j.meals||[];
    state.lastCards=meals;
    renderCards(out,meals);
  }catch(e){error(out,e.message)}
}
$('#mealSearchBtn').onclick=searchMeals;
$('#mealSearch').addEventListener('keydown',e=>{if(e.key==='Enter')searchMeals()});

async function loadExploreFilters(){
  try{
    const [c,a]=await Promise.all([api('/list.php',{c:'list'}),api('/list.php',{a:'list'})]);
    $('#categorySelect').innerHTML='<option value="">Categoria</option>'+(c.meals||[]).map(x=>`<option>${esc(x.strCategory)}</option>`).join('');
    $('#areaSelect').innerHTML='<option value="">Cucina</option>'+(a.meals||[]).map(x=>`<option>${esc(x.strArea)}</option>`).join('');
  }catch{}
}
$('#browseBtn').onclick=async()=>{
  const c=$('#categorySelect').value,a=$('#areaSelect').value,out=$('#exploreResults');
  if(!c&&!a)return error(out,'Scegli almeno una categoria o una cucina.');
  loader(out,'Carico…');
  try{
    let meals=[];
    if(c&&a){
      const [jc,ja]=await Promise.all([api('/filter.php',{c}),api('/filter.php',{a})]);
      const aset=new Set((ja.meals||[]).map(x=>x.idMeal));
      meals=(jc.meals||[]).filter(x=>aset.has(x.idMeal));
    }else{
      const j=await api('/filter.php',c?{c}:{a});
      meals=j.meals||[];
    }
    renderCards(out,meals.slice(0,40));
  }catch(e){error(out,e.message)}
};
$('#randomBtn').onclick=async()=>{
  const out=$('#exploreResults');loader(out,'Scelgo per te…');
  try{
    const j=await api('/random.php');
    renderCards(out,j.meals||[]);
  }catch(e){error(out,e.message)}
};

async function renderFavorites(){
  const out=$('#favoriteResults');
  const ids=[...state.favs];
  $('#favCount').textContent=ids.length?`${ids.length} salvate`:'';
  if(!ids.length){return out.innerHTML='<div class="empty">Le ricette che salvi compariranno qui.</div>'}
  loader(out,'Carico i preferiti…');
  try{
    const meals=[];
    for(const id of ids){
      const j=await api('/lookup.php',{i:id});
      if(j.meals?.[0])meals.push(j.meals[0]);
    }
    renderCards(out,meals);
  }catch(e){error(out,e.message)}
}

async function loadIngredientList(){
  try{
    const j=await api('/list.php',{i:'list'});
    state.ingredientList=(j.meals||[]).map(x=>x.strIngredient).filter(Boolean);
  }catch{}
}
function showSuggestions(value){
  const box=$('#ingredientSuggestions');
  const q=normalizeText(value);
  if(!q){hideSuggestions();return}
  const apiQ=toApiIngredient(q);
  const dictMatches=Object.entries(IT_TO_EN)
    .filter(([it,en])=>it.includes(q)||en.includes(apiQ))
    .slice(0,5)
    .map(([it,en])=>({label:`${it} → ${en}`,value:it}));
  const apiMatches=state.ingredientList
    .filter(x=>x.toLowerCase().includes(apiQ))
    .slice(0,6)
    .map(x=>({label:x,value:x}));
  const items=[...dictMatches,...apiMatches].slice(0,8);
  if(!items.length){hideSuggestions();return}
  box.innerHTML=items.map(x=>`<div class="suggestion" data-suggest="${esc(x.value)}">${esc(x.label)}</div>`).join('');
  box.classList.add('open');
  $$('[data-suggest]').forEach(x=>x.onclick=()=>{addIngredient(x.dataset.suggest)});
}
function hideSuggestions(){$('#ingredientSuggestions').classList.remove('open')}
$('#ingredientInput').addEventListener('input',e=>showSuggestions(e.target.value));
document.addEventListener('click',e=>{if(!e.target.closest('.fieldwrap'))hideSuggestions()});

$('#aboutBtn').onclick=()=>$('#aboutOverlay').classList.add('open');
function bindClose(el){el.onclick=()=>$('#'+el.dataset.close).classList.remove('open')}
$$('[data-close]').forEach(bindClose);
$$('.overlay').forEach(o=>o.addEventListener('click',e=>{if(e.target===o)o.classList.remove('open')}));
$('#resetApp').onclick=()=>{
  localStorage.removeItem(LS.pantry);localStorage.removeItem(LS.favs);
  state.pantry=[];state.favs=new Set();renderPantry();renderFavorites();
  $('#aboutOverlay').classList.remove('open');
};

renderPantry();
loadExploreFilters();
loadIngredientList();
})();
</script>
</body>
</html>
