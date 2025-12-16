<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Свободный Я — Прототип (улучшенный)</title>
<meta name="description" content="Прототип: Индекс Жизненной Свободы + Финансовый Доппельгангер — переработанный интерфейс" />

<style>
 :root{
    /* === ОСНОВНАЯ ПАЛИТРА СБЕРА === */
    --blue: #0087cd;       /* Основной голубой [citation:1] */
    --green: #21BA72;      /* Основной зеленый (Изумрудный) [citation:1] */
    --green-soft: #42E3B4; /* Мягкий бирюзовый (Арктический) [citation:1] */
    --yellow: #FAED00;     /* Основной желтый (Солнечный) [citation:1] */

    /* === ФОН И ОСНОВА === */
    --bg-color: #FFFFFF;   /* Белый фон приложения */
    --card-bg: #FFFFFF;    /* Белый фон карточек */
    --card-border: rgba(0, 0, 0, 0.08); /* Тонкая серая граница для карточек */

    /* === ТЕКСТ === */
    --text-main: #333333;      /* Основной текст - темно-серый */
    --text-muted: #666666;     /* Второстепенный текст */
    --text-on-accent: #FFFFFF; /* Текст на цветном акценте (белый) */

    /* === АКЦЕНТЫ И ГРАДИЕНТЫ === */
    --accent1: var(--green);
    --accent2: var(--blue);
    --accent3: var(--yellow);

    --gradient-primary: linear-gradient(90deg, var(--green), var(--blue));
    --gradient-secondary: linear-gradient(90deg, var(--green-soft), var(--blue));

    /* === ОБЩИЕ ПЕРЕМЕННЫЕ === */
    --radius: 16px;
    font-family: Inter, "Segoe UI", Roboto, Arial, sans-serif;
    color-scheme: light;
}

*{box-sizing:border-box}

body{
    margin:0;
    min-height:100vh;
    background: var(--bg-color); /* Сплошной белый фон */
    color: var(--text-main);
    -webkit-font-smoothing:antialiased;
    padding:28px;
    font-size:15px;
}

/* === КАРТОЧКИ === */
.card{
    background: var(--card-bg);
    backdrop-filter: none; /* Убран эффект стекла */
    border-radius: var(--radius);
    border: 1px solid var(--card-border); /* Светлая граница */
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05); /* Легкая тень для глубины */
    padding: 18px;
}

.logo{
    width:48px;height:48px;border-radius:12px;
    background: var(--gradient-primary); /* Градиент Сбера */
    display:grid;place-items:center;
    font-weight:800;color: var(--text-on-accent); /* Белый текст на градиенте */
}

/* === КРУГОВАЯ ДИАГРАММА (ИНДЕКС) === */
svg.progress circle#arcMain{
    stroke: url(#lg2);
}

#lg2 stop[offset="0"]{ stop-color: var(--blue); }
#lg2 stop[offset="1"]{ stop-color: var(--green); }

/* === КНОПКИ === */
.primaryBtn{
    background: var(--gradient-primary);
    color: var(--text-on-accent);
    font-weight:700;
    padding:9px 14px;
    border:none;
    border-radius:10px;
    cursor:pointer;
    transition:0.2s;
}
.primaryBtn:hover{
    transform:translateY(-2px);
    filter:brightness(1.08);
}
.primaryBtn:active{
    transform:translateY(0);
}

.quickBtn{
    background:transparent;
    border:1px solid var(--blue); /* Голубая граница */
    border-radius:10px;
    padding:8px 12px;
    color: var(--blue); /* Голубой текст */
    transition:0.15s;
}
.quickBtn:hover{
    background: rgba(0, 135, 205, 0.08); /* Светло-голубой фон при наведении */
    color: var(--blue);
}
/* === ТЕКСТ === */
.subtitle, #privacyState, small, label span{
    color: var(--text-muted);
}

/* === ПЛИТКИ И ЭЛЕМЕНТЫ === */
.tile{
    background: rgba(33, 186, 114, 0.05); /* Очень светлый зеленый фон */
    border-radius:12px;
    border:1px solid rgba(33, 186, 114, 0.15); /* Светло-зеленая граница */
}

/* === СООБЩЕНИЯ В ЧАТЕ === */
.botMsg{
    background: var(--gradient-secondary);
    color: var(--text-on-accent);
    padding:12px;
    border-radius:14px;
}
.userMsg{
    background: rgba(0, 0, 0, 0.04); /* Светло-серый фон для сообщений пользователя */
    border: 1px solid rgba(0, 0, 0, 0.08);
    color: var(--text-main);
    padding:12px;
    border-radius:14px;
}

.avatar{
    background: rgba(0, 135, 205, 0.08); /* Светло-голубой фон */
    border:1px solid rgba(0, 135, 205, 0.2);
}

.mission{
    background: rgba(0, 0, 0, 0.02); /* Очень светлый серый фон */
    border:1px solid var(--card-border);
}

/* === ПОЛЗУНОК (RANGE INPUT) === */
input[type=range] {
    accent-color: var(--green); /* Зеленый ползунок */
</style>
</head>
<body>
  <div class="app" role="application" aria-label="Свободный Я прототип">
    <!-- LEFT COLUMN -->
    <div class="leftCol">
      <div class="card hover-lift" aria-hidden="false">
        <div class="appHeader">
          <div class="logo" aria-hidden="true">SD</div>
          <div>
            <div class="title">Свободный Я</div>
            <div class="subtitle">Индекс свободы + Финансовый Доппельгангер</div>
          </div>
        </div>
        <div class="avatarWrap" aria-hidden="false">
          <div class="avatar" role="img" aria-label="Аватар пользователя">
            <svg viewBox="0 0 200 200" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
              <defs>
                <linearGradient id="gA" x1="0" x2="1"><stop offset="0" stop-color="#20C3D6"/><stop offset="1" stop-color="#8B6CF6"/></linearGradient>
              </defs>
              <rect width="200" height="200" rx="18" fill="#071A1B"></rect>
              <g transform="translate(30,20)" fill="none" stroke="#E6F2EF" stroke-opacity="0.08">
                <path d="M40 120c-10-28 0-54 40-54s50 28 40 54" stroke-width="3"/>
                <circle cx="60" cy="40" r="28" stroke-width="4" stroke-opacity="0.08" />
              </g>
            </svg>
            <div class="overlay" aria-hidden="true"></div>
          </div>
          <div class="indexBox" role="region" aria-label="Индекс свободы">
            <div style="display:flex;align-items:center;gap:12px;width:100%">
              <div style="flex:1">
                <div style="font-weight:800">Привет, <span id="userName">Алекс</span></div>
                <div style="font-size:13px;color:var(--muted)">Вот как поживает твоя свобода сегодня</div>
              </div>
              <button class="primaryBtn ripple" id="exportBtn" title="Экспортировать текущее состояние">Экспорт</button>
            </div>
            <div class="circle" aria-hidden="false" id="arcWrap">
              <svg class="progress" viewBox="0 0 120 120" width="150" height="150" aria-hidden="true">
                <defs>
                  <linearGradient id="lg2" x1="0" x2="1"><stop offset="0" stop-color="#20C3D6"/><stop offset="1" stop-color="#8B6CF6"/></linearGradient>
                </defs>
                <circle cx="60" cy="60" r="48" stroke="rgba(255,255,255,0.03)" stroke-width="12" fill="none"></circle>
                <circle id="arcMain" cx="60" cy="60" r="48" stroke="url(#lg2)" stroke-width="12" stroke-linecap="round" fill="none" stroke-dasharray="302" stroke-dashoffset="302"></circle>
                <circle cx="60" cy="60" r="52" fill="none" stroke="rgba(255,255,255,0.01)"></circle>
              </svg>
              <div class="score" id="score">--</div>
              <div class="scoreLabel">Индекс свободы</div>
            </div>
            <div class="leftSmall" style="margin-top:8px">
              <div class="chip" id="nextTip">Совет: —</div>
              <div class="chip" id="privacyChip">Приватность: <strong id="privacyState">on</strong></div>
            </div>
          </div>
        </div>
        <div style="margin-top:12px" class="card" aria-hidden="false">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div style="font-weight:800">Миссии</div>
            <div style="color:var(--muted);font-size:13px">Прогресс</div>
          </div>
          <div class="missions" id="missions">
            <!-- JS inject -->
          </div>
          <div class="controls">
            <button class="primaryBtn ripple" id="newMission">Добавить миссию</button>
            <button class="quickBtn" id="completeAll">Завершить всё</button>
          </div>
        </div>
      </div>
      <div class="card hover-lift" aria-hidden="false">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
          <div style="font-weight:800">Настройки приватности</div>
          <div style="color:var(--muted);font-size:13px">Контроль данных</div>
        </div>
        <div style="display:flex;flex-direction:column;gap:8px">
          <label style="display:flex;justify-content:space-between;align-items:center">
            <span style="color:var(--muted)">Анализ транзакций</span>
            <input type="checkbox" id="toggleTx" />
          </label>
          <label style="display:flex;justify-content:space-between;align-items:center">
            <span style="color:var(--muted)">Использовать цели</span>
            <input type="checkbox" id="toggleGoals" />
          </label>
          <label style="display:flex;justify-content:space-between;align-items:center">
            <span style="color:var(--muted)">Анонимные рекомендации</span>
            <input type="checkbox" id="toggleAnon" />
          </label>
          <small style="color:var(--muted)">Все изменения применяются локально и можно экспортировать состояние.</small>
        </div>
      </div>
    </div>
    <!-- RIGHT COLUMN -->
    <div class="rightCol">
      <div class="card panelLarge hover-lift" aria-live="polite">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div>
            <div style="font-weight:900;font-size:20px">Карта свободы</div>
            <div style="color:var(--muted)">Разбивка по сферам и прогнозы</div>
          </div>
          <div style="text-align:right;color:var(--muted);font-size:13px" id="lastUpdated">Обновлено: сейчас</div>
        </div>
        <div style="margin-top:14px;display:flex;gap:12px">
          <div style="flex:1">
            <div class="freedomTiles" id="breakdown">
              <!-- tiles inserted by JS -->
            </div>
            <div style="margin-top:14px">
              <div style="display:flex;justify-content:space-between;align-items:center">
                <div style="font-weight:800">Прогнозы</div>
                <div style="color:var(--muted);font-size:13px">Смоделируйте своё будущее</div>
              </div>
              <div style="margin-top:10px" class="card">
                <div style="display:flex;gap:12px;align-items:center">
                  <div style="width:36px;height:36px;border-radius:9px;background:linear-gradient(90deg,var(--accent2),var(--accent3));display:grid;place-items:center;font-weight:700">7</div>
                  <div>
                    <div style="font-weight:700">7 дней</div>
                    <div style="font-size:13px;color:var(--muted)">Мелкие корректировки без дискомфорта</div>
                  </div>
                </div>
                <div style="margin-top:12px;display:flex;gap:12px">
                  <div style="flex:1">
                    <label style="font-size:13px;color:var(--muted)">Сдвинуть платеж (руб/мес)</label>
                    <input type="range" id="shiftRange" min="0" max="10000" step="100" value="0" />
                    <div style="display:flex;justify-content:space-between;font-size:13px;color:var(--muted)"><span>0 ₽</span><span id="shiftVal">0 ₽</span></div>
                  </div>
                  <div style="width:200px">
                    <div style="font-size:13px;color:var(--muted)">Рассчитать эффект</div>
                    <button class="primaryBtn ripple" id="applyShift">Смоделировать</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div style="width:320px">
            <div style="font-weight:800">Сценарии свободы</div>
            <div class="scenarioList" style="margin-top:10px">
              <div class="card tile" id="scenarioConservative">
                <h4>Консервативный</h4>
                <small class="muted">Снижение расхода 8% → +4 ИЖС</small>
                <div style="margin-top:8px;display:flex;gap:8px">
                  <button class="primaryBtn ripple" onclick="applyScenario('conservative')">Применить</button>
                  <button class="quickBtn" onclick="detailScenario('conservative')">Подробнее</button>
                </div>
              </div>
              <div class="card tile" id="scenarioAggressive">
                <h4>Агрессивный</h4>
                <small class="muted">Перенаправление 15% дохода → +9 ИЖС</small>
                <div style="margin-top:8px;display:flex;gap:8px">
                  <button class="primaryBtn ripple" onclick="applyScenario('aggressive')">Применить</button>
                  <button class="quickBtn" onclick="detailScenario('aggressive')">Подробнее</button>
                </div>
              </div>
            </div>
            <div style="margin-top:12px" class="card">
              <div style="font-weight:800">История действий</div>
              <div id="history" style="margin-top:8px;font-size:13px;color:var(--muted);max-height:160px;overflow:auto"></div>
            </div>
          </div>
        </div>
      </div>
      <div class="card panelLarge hover-lift" aria-hidden="false">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div style="font-weight:800">Диалог с Доппельгангером</div>
          <div style="color:var(--muted);font-size:13px">Советы, сценарии и мягкие напоминания</div>
        </div>
        <div class="chatWindow" style="margin-top:12px">
          <div class="chatLog" id="chatLog" role="log" aria-live="polite">
            <!-- messages -->
          </div>
          <div style="display:flex;gap:8px;align-items:center">
            <input id="userInput" type="text" aria-label="Введите сообщение" placeholder="Спросить доппельгангера..." style="flex:1;padding:12px;border-radius:12px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit" />
            <button class="primaryBtn ripple" id="sendBtn">Отправить</button>
          </div>
          <div class="quickActions" id="quickActions">
            <!-- quick suggestions injected -->
          </div>
        </div>
      </div>
      <footer>
        Прототип: Свободный Я — индекс свободы + финансовый доппельгангер. Сохраните экспорт для демонстрации.
      </footer>
    </div>
  </div>

  <!-- Overlay Panel for details -->
  <div class="overlayPanel" id="overlayPanel" aria-hidden="true">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">
      <div>
        <h4 id="overlayTitle">Детали</h4>
        <div style="font-size:13px;color:var(--muted)" id="overlaySub">Информация</div>
      </div>
      <button class="overlayClose" id="overlayClose">Закрыть</button>
    </div>
    <div id="overlayBody" style="font-size:13px;color:var(--muted)"></div>
  </div>

<script>
/* ========== State with persistence ========== */
const STORAGE_KEY = 'freedom_state_v2';
let state = {
  userId: 'u_01',
  name: 'Алекс',
  freedomIndex: 67,
  lastUpdated: new Date().toISOString(),
  breakdown: { work:72, home:85, mobility:60, savings:50, risk:70, time:65 },
  doppel: {
    persona: 'Практичный советчик',
    tone: 'supportive',
    predictions: [
      { horizon_days:7, freedomIndex:66 },
      { horizon_days:30, freedomIndex:64 },
      { horizon_days:90, freedomIndex:61 }
    ],
    recommendedActions: [
      { id:'r1', title:'Оптимизация подписок', impact:2 },
      { id:'r2', title:'Автосбережение 5%', impact:4 },
      { id:'r3', title:'Ревизия расходов', impact:3 }
    ]
  },
  missions: [
    {id:'m1', title:'Проверить и отменить неиспользуемые подписки', progress:30},
    {id:'m2', title:'Включить 5% автосбережение', progress:0}
  ],
  history: [],
  privacy: {tx:true, goals:true, anon:false}
};

const saveState = () => {
  try{ localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); }catch(e){}
};
const loadState = ()=>{
  try{
    const raw = localStorage.getItem(STORAGE_KEY);
    if(raw) Object.assign(state, JSON.parse(raw));
  }catch(e){}
};
loadState();

/* ===== Utils ===== */
function setText(id, txt){ const el = document.getElementById(id); if(el) el.textContent = txt }
function formatRub(n){ return n.toLocaleString('ru-RU') + ' ₽' }
function now(){ return new Date().toLocaleString() }
function clamp(v,a,b){ return Math.max(a, Math.min(b, v)); }

/* ===== Renderers ===== */
const arc = document.getElementById('arcMain');
let arcAnimFrame = null;
function animateArc(toValue){
  // animate numeric value and stroke offset
  cancelAnimationFrame(arcAnimFrame);
  const r = 48;
  const c = 2*Math.PI*r;
  const start = parseFloat(arc.getAttribute('data-current') || 0);
  const end = clamp(toValue,0,100);
  const dur = 900;
  const startTime = performance.now();
  function step(t){
    const p = clamp((t - startTime)/dur, 0, 1);
    // easeOutCubic
    const ease = 1 - Math.pow(1-p,3);
    const cur = start + (end - start) * ease;
    const offset = c * (1 - cur/100);
    arc.style.strokeDashoffset = offset;
    arc.setAttribute('data-current', cur.toFixed(2));
    setText('score', Math.round(cur));
    if(p < 1) arcAnimFrame = requestAnimationFrame(step);
  }
  arcAnimFrame = requestAnimationFrame(step);
}

function renderScore(){
  animateArc(state.freedomIndex);
  setText('nextTip', 'Совет: ' + (state.doppel.recommendedActions[1]?.title || '—') + ' → +' + (state.doppel.recommendedActions[1]?.impact || '—'));
  setText('privacyState', state.privacy.anon ? 'anon' : 'on');
  setText('lastUpdated', 'Обновлено: ' + new Date(state.lastUpdated).toLocaleString());
  setText('userName', state.name);
  saveState();
}

function renderBreakdown(){
  const container = document.getElementById('breakdown');
  container.innerHTML = '';
  for(const [k,v] of Object.entries(state.breakdown)){
    const tile = document.createElement('div'); tile.className='tile hover-lift';
    tile.tabIndex = 0;
    tile.dataset.key = k;
    tile.innerHTML = `<h4>${titleCase(k)}</h4><div class="pct">${v}%</div><div class="desc">${shortDesc(k)}</div>`;
    tile.addEventListener('click', ()=> openOverlay(`${titleCase(k)}`, `Текущий показатель ${v}%. Рекомендации: ${recommendationFor(k)}`));
    tile.addEventListener('keypress', (e)=>{ if(e.key==='Enter') tile.click() });
    container.appendChild(tile);
  }
}

function renderMissions(){
  const mWrap = document.getElementById('missions'); mWrap.innerHTML='';
  state.missions.forEach((m, idx)=>{
    const el = document.createElement('div'); el.className='mission';
    el.innerHTML = `<div class="left"><div class="title">${m.title}</div><div style="font-size:13px;color:var(--muted)">${m.progress}% завершено</div>
      <div class="progressBar" aria-hidden="true"><i style="width:0%"></i></div></div>
      <div style="display:flex;flex-direction:column;gap:6px">
        <button class="primaryBtn ripple" data-id="${m.id}" data-action="complete">Выполнить +</button>
        <button class="quickBtn" data-id="${m.id}" data-action="delete">Удалить</button>
      </div>`;
    mWrap.appendChild(el);
    // animate progress bar
    requestAnimationFrame(()=>{
      const bar = el.querySelector('.progressBar > i');
      bar.style.width = m.progress + '%';
    });
  });
  // delegate mission buttons
  mWrap.querySelectorAll('button').forEach(btn=>{
    btn.addEventListener('click', (e)=>{
      const id = btn.dataset.id;
      const action = btn.dataset.action;
      if(action === 'complete') completeMission(id);
      if(action === 'delete') removeMission(id);
    });
  });
}

function renderHistory(){
  const h = document.getElementById('history'); h.innerHTML='';
  state.history.slice().reverse().forEach((item, i)=>{
    const line = document.createElement('div'); line.style.padding='6px 0';
    line.innerHTML = `<div style="font-weight:600">${item.title}</div><div style="font-size:12px;color:var(--muted)">${item.desc} • ${new Date(item.time).toLocaleString()}</div>`;
    h.appendChild(line);
  });
}

function renderQuickActions(){
  const q = document.getElementById('quickActions'); q.innerHTML='';
  const items = [
    'Оптимизация подписок',
    'Включить автосбережение',
    'Показать сценарии',
    'Как поднять индекс на 5?'
  ];
  items.forEach((txt, idx)=>{
    const b = document.createElement('button'); b.className='quickBtn'; b.textContent=txt;
    b.onclick = ()=>{ sendUserMessage(txt) };
    q.appendChild(b);
  });
}

/* ===== Helpers ===== */
function titleCase(k){
  const map = {work:'Работа', home:'Дом', mobility:'Передвижение', savings:'Накопления', risk:'Риски', time:'Время'};
  return map[k] || k;
}
function shortDesc(k){
  const map = {
    work:'Стабильность дохода',
    home:'Жилищные расходы',
    mobility:'Траты на транспорт и поездки',
    savings:'Размер подушки',
    risk:'Кредитная нагрузка',
    time:'Время для себя'
  };
  return map[k] || '';
}
function recommendationFor(k){
  const rec = {
    work:'Разделите доход на критичные и экспериментальные потоки; ищите гибкие контракты',
    home:'Проверьте тарифы ЖКУ и страховые опции',
    mobility:'Сравните каршеринг с общественным транспортом',
    savings:'Увеличьте автосбережение на 1-2%',
    risk:'Снизьте кредитную нагрузку у источника с высоким процентом',
    time:'Автоматизируйте рутинные задачи — сэкономите пару часов в неделю'
  };
  return rec[k] || 'Рекомендация отсутствует';
}

/* ===== Actions ===== */
function completeMission(id){
  const m = state.missions.find(x=>x.id===id);
  if(m){
    m.progress = 100;
    pushHistory({title:'Миссия завершена', desc: m.title});
    // demo effect
    state.freedomIndex = Math.min(100, state.freedomIndex + 2);
    state.lastUpdated = new Date().toISOString();
    renderAll();
  }
}
function removeMission(id){
  state.missions = state.missions.filter(x=>x.id!==id);
  pushHistory({title:'Миссия удалена', desc: id});
  renderAll();
}
function addMission(title){
  const id = 'm' + Math.floor(Math.random()*10000);
  state.missions.push({id, title, progress:0});
  pushHistory({title:'Добавлена миссия', desc:title});
  renderAll();
}
function pushHistory(event){
  state.history.push({...event, time:new Date().toISOString()});
  renderHistory();
  saveState();
}

/* ===== Chat simulation (doppel) ===== */
const chatLogEl = document.getElementById('chatLog');

function appendChat(text, who='bot', opts = {}){
  const delay = opts.delay || 0;
  const el = document.createElement('div'); el.className='message';
  el.style.setProperty('--delay', `${(chatLogEl.children.length * 0.03) + delay}s`);
  if(who==='bot'){
    el.innerHTML = `<div class="botMsg" role="status">${text}</div>`;
  } else {
    el.innerHTML = `<div class="userMsg">${text}</div>`;
  }
  chatLogEl.appendChild(el);
  chatLogEl.scrollTop = chatLogEl.scrollHeight;
}

function showTypingThenReply(replyText, ms = 700){
  // show typing indicator
  const typ = document.createElement('div'); typ.className='message';
  typ.innerHTML = `<div class="typing"><span class="dots"><span></span><span></span><span></span></span></div>`;
  chatLogEl.appendChild(typ);
  chatLogEl.scrollTop = chatLogEl.scrollHeight;
  setTimeout(()=>{
    typ.remove();
    appendChat(replyText,'bot');
    pushHistory({title:'Ответ Доппеля', desc: replyText});
  }, ms + Math.random()*500);
}

function sendUserMessage(txt){
  if(!txt || txt.trim()==='') return;
  appendChat(txt,'user');
  handleUserQuery(txt);
  document.getElementById('userInput').value = '';
  chatLogEl.scrollTop = chatLogEl.scrollHeight;
}

function handleUserQuery(q){
  q = q.toLowerCase();
  pushHistory({title:'Вопрос Доппелю', desc:q});
  if(q.includes('подпис') || q.includes('подписки')){
    showTypingThenReply('Я нашёл 3 подписки, которые вы редко используете. Предлагаю заморозить 2 — это даст +2 к индексу.', 700);
  } else if(q.includes('автосбер') || q.includes('автосбереж')){
    showTypingThenReply('Можно включить автосбережение: 5% от дохода. Ожидаемый эффект: +4 к Индексу свободы через 90 дней. Применить?', 700);
  } else if(q.includes('сколько') || q.includes('почему')){
    showTypingThenReply('Индекс снизился из-за сезонного увеличения расходов на путешествия и подписки. Хочешь варианты смягчения?', 700);
  } else if(q.includes('показать сценар') || q.includes('сценари')){
    showTypingThenReply('Показываю сценарии: консервативный и агрессивный. Нужна помощь с выбором?', 700);
  } else if(q.includes('как поднять') || q.includes('поднять индекс')){
    showTypingThenReply('Рекомендую: 1) Включить автосбережение; 2) Оптимизировать подписки; 3) Пересмотреть транспортные расходы. Хотите применить первый?', 700);
  } else {
    showTypingThenReply('Понял. Могу предложить план: 1) Быстрые шаги 2) Среднесрочные (автосбережение) 3) Долгосрочные (инвестиции). Что интересно?', 700);
  }
}

/* Quick send handlers */
document.getElementById('sendBtn').addEventListener('click', ()=>{
  const txt = document.getElementById('userInput').value;
  sendUserMessage(txt);
});
document.getElementById('userInput').addEventListener('keypress', (e)=>{
  if(e.key === 'Enter'){ sendUserMessage(e.target.value); e.preventDefault(); }
});

/* Quick actions */
document.getElementById('newMission').addEventListener('click', ()=>{
  const title = prompt('Название новой миссии:', 'Снизить расходы на подписки');
  if(title) addMission(title);
});
document.getElementById('completeAll').addEventListener('click', ()=>{
  state.missions.forEach(m=>m.progress=100);
  pushHistory({title:'Все миссии завершены', desc:'Пользователь завершил все активные миссии'});
  state.freedomIndex = Math.min(100, state.freedomIndex + 6);
  renderAll();
});

/* scenario apply */
function applyScenario(kind){
  if(kind==='conservative'){
    state.freedomIndex = Math.min(100, state.freedomIndex + 4);
    pushHistory({title:'Применён сценарий', desc:'Консервативный (сокращение расходов 8%)'});
    showTypingThenReply('Консервативный сценарий активирован. Ожидаемый прирост +4 ИЖС через 90 дн.', 600);
  } else {
    state.freedomIndex = Math.min(100, state.freedomIndex + 9);
    pushHistory({title:'Применён сценарий', desc:'Агрессивный (15% дохода → сбережения)'});
    showTypingThenReply('Агрессивный сценарий активирован. Ожидаемый прирост +9 ИЖС через 90 дн.', 600);
  }
  state.lastUpdated = new Date().toISOString();
  renderAll();
}

function detailScenario(kind){
  alert(kind === 'conservative' ? 'Консервативный: снизить некритичные траты, пересмотреть подписки, настроить автосбережение 5%.' : 'Агрессивный: направить 15% дохода на сбережения/инвестиции, возможен временный дискомфорт.' );
}

/* shift simulation */
const shiftRange = document.getElementById('shiftRange');
const shiftVal = document.getElementById('shiftVal');
shiftRange.addEventListener('input', ()=>{ shiftVal.textContent = formatRub(parseInt(shiftRange.value)); });
document.getElementById('applyShift').addEventListener('click', ()=>{
  const shift = parseInt(shiftRange.value);
  if(shift>0){
    const delta = Math.min(8, Math.round(shift/2000)); // demo conversion
    state.freedomIndex = Math.min(100, state.freedomIndex + delta);
    pushHistory({title:'Сдвиг платежа', desc:`Сдвинули платежи на ${formatRub(shift)} → +${delta} ИЖС`});
    showTypingThenReply(`Я смоделировал: сдвиг ${formatRub(shift)} даёт ~+${delta} к Индексу свободы через 7 дней.`, 600);
    renderAll();
  } else {
    showTypingThenReply('Сдвиг равен 0 — эффект отсутствует', 300);
  }
});

/* Export with animation */
document.getElementById('exportBtn').addEventListener('click', (e)=>{
  const btn = e.currentTarget;
  // ripple effect
  const rect = btn.getBoundingClientRect();
  const r = document.createElement('span');
  r.style.left = ((event.clientX || rect.left + rect.width/2) - rect.left) + 'px';
  r.style.top = ((event.clientY || rect.top + rect.height/2) - rect.top) + 'px';
  r.style.position = 'absolute';
  r.style.width = r.style.height = '8px';
  r.style.background = 'rgba(255,255,255,0.12)';
  r.style.borderRadius = '50%';
  r.style.transform = 'translate(-50%,-50%) scale(0)';
  r.style.transition = 'transform 420ms cubic-bezier(.16,.84,.32,1), opacity 420ms';
  btn.appendChild(r);
  requestAnimationFrame(()=>{ r.style.transform = 'translate(-50%,-50%) scale(40)'; r.style.opacity = '0'; });
  setTimeout(()=> r.remove(), 420);

  const blob = new Blob([JSON.stringify(state,null,2)], {type:'application/json;charset=utf-8'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href = url; a.download = 'freedom_state.json'; document.body.appendChild(a); a.click(); a.remove();
  URL.revokeObjectURL(url);
  pushHistory({title:'Экспорт', desc:'Пользователь экспортировал состояние'});
});

/* Privacy toggles */
document.getElementById('toggleTx').checked = !!state.privacy.tx;
document.getElementById('toggleGoals').checked = !!state.privacy.goals;
document.getElementById('toggleAnon').checked = !!state.privacy.anon;
document.getElementById('toggleTx').addEventListener('change', (e)=>{ state.privacy.tx = e.target.checked; pushHistory({title:'Настройка', desc:'Анализ транзакций: ' + (e.target.checked?'вкл':'выкл')}); renderAll();});
document.getElementById('toggleGoals').addEventListener('change', (e)=>{ state.privacy.goals = e.target.checked; pushHistory({title:'Настройка', desc:'Использовать цели: ' + (e.target.checked?'вкл':'выкл')}); renderAll();});
document.getElementById('toggleAnon').addEventListener('change', (e)=>{ state.privacy.anon = e.target.checked; pushHistory({title:'Настройка', desc:'Анонимные рекомендации: ' + (e.target.checked?'вкл':'выкл')}); renderAll();});

/* Overlay panel */
const overlay = document.getElementById('overlayPanel');
const overlayClose = document.getElementById('overlayClose');
function openOverlay(title, sub){
  document.getElementById('overlayTitle').textContent = title;
  document.getElementById('overlaySub').textContent = sub;
  document.getElementById('overlayBody').innerHTML = `<p style="margin:0;color:var(--muted)">Подробная информация по ${title}. Здесь могут быть графики, ссылки и быстрые действия.</p>
    <div style="margin-top:12px;display:flex;gap:8px"><button class="primaryBtn ripple" id="overlayAction">Выполнить рекомендацию</button><button class="quickBtn" id="overlayCloseBtn">Закрыть</button></div>`;
  overlay.classList.add('open');
  overlay.setAttribute('aria-hidden','false');

  document.getElementById('overlayAction').addEventListener('click', ()=>{
    // small demo effect: increase corresponding breakdown by 2%
    const key = Object.keys(state.breakdown).find(k => titleCase(k) === title);
    if(key){ state.breakdown[key] = clamp(state.breakdown[key] + 2, 0, 100); state.freedomIndex = Math.min(100, state.freedomIndex + 1); pushHistory({title:'Применена рекомендация', desc:`Улучшение по ${title}`}); renderAll(); }
    closeOverlay();
  });
  document.getElementById('overlayCloseBtn').addEventListener('click', closeOverlay);
}
function closeOverlay(){
  overlay.classList.remove('open');
  overlay.setAttribute('aria-hidden','true');
}
overlayClose.addEventListener('click', closeOverlay);

/* Little cursor parallax & responsive subtle motion */
document.addEventListener('mousemove', (e)=>{
  const w = window.innerWidth, h = window.innerHeight;
  const x = (e.clientX / w) * 100;
  const y = (e.clientY / h) * 100;
  document.body.style.setProperty('--cursorX', x + '%');
  document.body.style.setProperty('--cursorY', y + '%');

  // subtle card motion
  document.querySelectorAll('.hover-lift').forEach(el=>{
    const rect = el.getBoundingClientRect();
    const cx = rect.left + rect.width / 2;
    const cy = rect.top + rect.height / 2;
    const dx = (e.clientX - cx) / rect.width;
    const dy = (e.clientY - cy) / rect.height;
    el.style.transform = `translateY(${ -8 - dy * 6 }px) translateX(${ -dx * 6 }px)`;
    el.style.transition = 'transform 600ms cubic-bezier(.16,.84,.32,1)';
  });
});
document.addEventListener('mouseleave', ()=>{
  document.querySelectorAll('.hover-lift').forEach(el=>{
    el.style.transform = '';
  });
});

/* Clean up transforms when hovering interactive elements to avoid sticky effect */
['mouseenter','mouseleave'].forEach(evt=>{
  document.querySelectorAll('.hover-lift').forEach(el=>{
    el.addEventListener(evt, ()=> el.style.transition = 'transform 300ms cubic-bezier(.16,.84,.32,1)');
  });
});

/* ===== Misc helpers ===== */
function recommendationFor(k){
  // kept earlier function in case of duplicate declaration
  const rec = {
    work:'Разделите доход на критичные и экспериментальные потоки; ищите гибкие контракты',
    home:'Проверьте тарифы ЖКУ и страховые опции',
    mobility:'Сравните каршеринг с общественным транспортом',
    savings:'Увеличьте автосбережение на 1-2%',
    risk:'Снизьте кредитную нагрузку у источника с высоким процентом',
    time:'Автоматизируйте рутинные задачи — сэкономите пару часов в неделю'
  };
  return rec[k] || 'Рекомендация отсутствует';
}

/* ===== rendering entrypoint ===== */
function renderAll(){
  renderScore();
  renderBreakdown();
  renderMissions();
  renderHistory();
  renderQuickActions();
  setText('shiftVal', formatRub(parseInt(shiftRange.value)));
  // ensure arc initial current is set
  arc.setAttribute('data-current', Math.round(state.freedomIndex));
  saveState();
}
renderAll();

/* initial chat welcome */
pushHistory({title:'Инициализация профиля', desc:'Загружен профиль пользователя'});
appendChat('Привет! Я твой Доппель — могу подсказать, как повысить Индекс Свободы. Спроси меня о подписках, автосбережении или сценариях.', 'bot');

/* Ripple utility (delegated) */
document.addEventListener('click', function(e){
  const el = e.target.closest('.ripple');
  if(!el) return;
  const rect = el.getBoundingClientRect();
  const circle = document.createElement('span');
  circle.style.position = 'absolute';
  circle.style.borderRadius = '50%';
  circle.style.width = circle.style.height = '10px';
  circle.style.left = (e.clientX - rect.left) + 'px';
  circle.style.top = (e.clientY - rect.top) + 'px';
  circle.style.background = 'rgba(255,255,255,0.12)';
  circle.style.transform = 'translate(-50%,-50%) scale(0)';
  circle.style.transition = 'transform 420ms cubic-bezier(.16,.84,.32,1), opacity 420ms';
  el.appendChild(circle);
  requestAnimationFrame(()=> circle.style.transform = 'translate(-50%,-50%) scale(30)');
  setTimeout(()=> circle.remove(), 420);
});

/* safety: expose some functions for UI */
window.applyScenario = applyScenario;
window.detailScenario = detailScenario;
window.completeMission = completeMission;
window.removeMission = removeMission;
window.addMission = addMission;
window.sendUserMessage = sendUserMessage;

</script>
</body>
</html>
