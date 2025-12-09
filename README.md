<!doctype html>
<html lang="ru">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Свободный Я — Прототип (улучшенный)</title>
<meta name="description" content="Прототип: Индекс Жизненной Свободы + Финансовый Доппельгангер — переработанный интерфейс" />

<style>
  :root{
    --bg-1: #071019;
    --bg-2: #041219;
    --card: rgba(255,255,255,0.04);
    --glass: rgba(255,255,255,0.06);
    --muted: #9FB0B9;
    --accent1: #17A74F;
    --accent2: #19C4D9;
    --accent3: #8B6CF6;
    --accent-glow: rgba(32,195,214,0.12);
    --radius-lg: 18px;
    --radius-md: 12px;
    --ease: cubic-bezier(.16,.84,.32,1);
    --font-sans: Inter, "SF Pro Text", "Segoe UI", Roboto, Arial, sans-serif;
    color-scheme: dark;
  }

  *{box-sizing:border-box}
  html,body{height:100%}
  body{
    margin:0;
    min-height:100vh;
    background:
      radial-gradient(800px 400px at 10% 10%, rgba(139,108,246,0.08), transparent 6%),
      radial-gradient(600px 300px at 85% 80%, rgba(25,196,217,0.06), transparent 6%),
      linear-gradient(180deg,var(--bg-1), var(--bg-2) 85%);
    color:#E6F2EF;
    -webkit-font-smoothing:antialiased;
    font-family:var(--font-sans);
    padding:34px;
    font-size:15px;
    transition:background 400ms var(--ease);
    --cursorX: 50%;
    --cursorY: 50%;
  }

  /* Layout */
  .app{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:360px 1fr;gap:22px;align-items:start}
  .card{
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    border-radius:var(--radius-lg);
    border:1px solid rgba(255,255,255,0.03);
    padding:18px;
    box-shadow: 0 10px 30px rgba(2,7,9,0.6), 0 1px 0 rgba(255,255,255,0.02) inset;
    backdrop-filter: blur(8px) saturate(120%);
    transform: translateZ(0);
    transition: transform 300ms var(--ease), box-shadow 300ms var(--ease);
  }
  .card.hover-lift:hover{ transform: translateY(-8px) translateZ(0); box-shadow: 0 18px 50px rgba(2,7,9,0.65);}

  header.appHeader{display:flex;align-items:center;gap:14px;margin-bottom:10px}
  .logo{width:52px;height:52px;border-radius:12px;background:linear-gradient(135deg,var(--accent1), var(--accent2));display:grid;place-items:center;font-weight:800;color:#041010;font-size:18px;box-shadow:0 6px 18px rgba(25,196,217,0.06)}
  .title{font-weight:800;font-size:18px}
  .subtitle{font-size:13px;color:var(--muted)}

  /* LEFT column */
  .leftCol{display:flex;flex-direction:column;gap:16px}
  .avatarWrap{display:flex;flex-direction:column;align-items:center;gap:12px}
  .avatar{
    width:150px;height:150px;border-radius:26px;background:linear-gradient(180deg, rgba(255,255,255,0.016), rgba(255,255,255,0.008));
    display:grid;place-items:center;position:relative;overflow:hidden;border:1px solid rgba(255,255,255,0.04);
    transition: transform 400ms var(--ease), box-shadow 300ms var(--ease);
  }
  .avatar:hover{ transform: translateY(-6px) scale(1.02); box-shadow: 0 18px 40px rgba(12,20,22,0.5) }
  .avatar svg{width:100%;height:100%}
  .avatar .overlay{position:absolute;inset:0;background:radial-gradient(400px circle at 20% 10%, rgba(32,195,214,0.14), transparent 18%);mix-blend-mode:screen;pointer-events:none;opacity:.9}

  .indexBox{width:100%;display:flex;flex-direction:column;align-items:center;gap:12px;padding:14px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.012), rgba(255,255,255,0.008));border:1px solid rgba(255,255,255,0.02)}
  .circle{width:150px;height:150px;position:relative;display:grid;place-items:center}
  svg.progress{transform:rotate(-90deg);filter: drop-shadow(0 6px 18px rgba(20,60,120,0.08))}
  .score{position:absolute;font-weight:900;font-size:30px;letter-spacing:-0.5px}
  .scoreLabel{font-size:13px;color:var(--muted)}

  .leftSmall{display:flex;gap:8px;flex-wrap:wrap;justify-content:center}
  .chip{padding:8px 10px;border-radius:10px;background:rgba(255,255,255,0.02);font-size:13px;border:1px solid rgba(255,255,255,0.02)}

  /* Right column */
  .rightCol{display:flex;flex-direction:column;gap:16px}
  .topRow{display:flex;gap:16px}
  .panelLarge{flex:1}
  .panelSmall{width:320px}

  .freedomTiles{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:6px}
  .tile{
    padding:12px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.012), rgba(255,255,255,0.006));
    border:1px solid rgba(255,255,255,0.02);
    transition: transform 260ms var(--ease), box-shadow 260ms var(--ease), background 260ms var(--ease);
    cursor:pointer;
  }
  .tile:hover{ transform: translateY(-8px) scale(1.01); box-shadow: 0 16px 36px rgba(2,7,9,0.5) }
  .tile h4{margin:0;font-size:13px}
  .tile .pct{font-weight:800;font-size:18px;margin-top:8px}
  .tile .desc{font-size:12px;color:var(--muted);margin-top:6px}

  /* Missions */
  .missions{display:flex;flex-direction:column;gap:8px}
  .mission{display:flex;justify-content:space-between;align-items:center;padding:10px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));border:1px solid rgba(255,255,255,0.02)}
  .mission .left{max-width:68%}
  .mission .title{font-weight:700}
  .progressBar{height:8px;background:rgba(255,255,255,0.03);border-radius:8px;overflow:hidden;margin-top:8px}
  .progressBar > i{display:block;height:100%;background:linear-gradient(90deg,var(--accent2),var(--accent3));width:0%;transition:width 900ms cubic-bezier(.2,.9,.3,1)}

  /* Chat */
  .chatWindow{display:flex;flex-direction:column;gap:10px;height:420px}
  .chatLog{overflow:auto;padding:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));border-radius:10px;border:1px solid rgba(255,255,255,0.02);flex:1;scroll-behavior:smooth}
  .message{display:flex;gap:8px;padding:8px;opacity:0;transform:translateY(6px);animation:msgIn .26s forwards var(--delay,0s)}
  @keyframes msgIn { to{opacity:1;transform:none} }
  .botMsg{background:linear-gradient(90deg,var(--accent2), var(--accent3));color:#061014;padding:10px;border-radius:12px;max-width:78%;align-self:flex-start;box-shadow:0 8px 24px rgba(26,40,50,0.4)}
  .userMsg{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px;border-radius:10px;color:var(--muted);align-self:flex-end}

  .typing{
    display:inline-block;height:18px;padding:8px 10px;border-radius:12px;background:linear-gradient(90deg,var(--accent2), var(--accent3));color:#061014;
  }
  .dots span{display:inline-block;width:5px;height:5px;margin:0 3px;background:#061014;border-radius:50%;opacity:0;animation:dots 1s infinite;}
  .dots span:nth-child(1){animation-delay:0s}
  .dots span:nth-child(2){animation-delay:.12s}
  .dots span:nth-child(3){animation-delay:.24s}
  @keyframes dots{0%{opacity:0;transform:translateY(0)}40%{opacity:1;transform:translateY(-6px)}80%{opacity:0;transform:translateY(0)}}

  .quickActions{display:flex;gap:8px;flex-wrap:wrap;margin-top:6px}
  .quickBtn{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 10px;border-radius:8px;color:var(--muted);cursor:pointer;transition:transform 160ms var(--ease)}
  .quickBtn:hover{transform:translateY(-6px);border-color:rgba(255,255,255,0.09);color:#EAF7F7}
  .primaryBtn{background:linear-gradient(90deg,var(--accent1), var(--accent2));border:none;color:#061014;padding:9px 12px;border-radius:10px;font-weight:800;cursor:pointer;transition:transform 160ms var(--ease), box-shadow 160ms var(--ease)}
  .primaryBtn:active{transform:translateY(1px) scale(.997)}
  .ripple{position:relative;overflow:hidden}
  .ripple::after{content:"";position:absolute;border-radius:50%;transform:scale(0);opacity:.6;pointer-events:none}

  /* controls */
  .controls{display:flex;gap:8px;margin-top:8px;align-items:center}
  input[type=range]{width:100%;accent-color:var(--accent2)}

  /* small */
  footer{margin-top:18px;color:var(--muted);font-size:13px;text-align:center}
  .muted{color:var(--muted)}

  /* overlay detail */
  .overlayPanel{
    position:fixed;right:28px;top:24%;width:360px;padding:18px;border-radius:16px;background:linear-gradient(180deg, rgba(10,18,22,0.95), rgba(10,18,22,0.92));border:1px solid rgba(255,255,255,0.03);box-shadow:0 30px 80px rgba(0,0,0,0.7);transform:translateY(12px) scale(.98);opacity:0;pointer-events:none;transition:all 260ms var(--ease);
    z-index:80;
  }
  .overlayPanel.open{opacity:1;transform:none;pointer-events:auto}
  .overlayPanel h4{margin:0 0 6px 0}
  .overlayClose{background:transparent;border:1px solid rgba(255,255,255,0.03);padding:6px 8px;border-radius:8px;color:var(--muted);cursor:pointer}

  /* responsive */
  @media (max-width:1100px){
    .app{grid-template-columns:1fr; padding:12px}
    .panelSmall{width:100%}
    .overlayPanel{right:14px;left:14px;top:40%}
  }

  /* reduced motion */
  @media (prefers-reduced-motion: reduce){
    *{transition:none!important;animation:none!important}
  }
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
