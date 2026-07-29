<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="הוצאות">
<title>מעקב הוצאות</title>
<style>
\* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: #f5f5f5; color: #1a1a1a; direction: rtl; }
.app { max-width: 430px; margin: 0 auto; padding: 1rem; min-height: 100vh; padding-bottom: 90px; }
.header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 1.2rem; padding-top: 0.5rem; }
.header h1 { font-size: 21px; font-weight: 700; }
.header span { font-size: 13px; color: #888; }
/* Bottom nav */
.bottom-nav { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 430px; background: white; border-top: 1px solid #eee; display: flex; z-index: 100; padding-bottom: env(safe-area-inset-bottom); }
.nav-btn { flex: 1; padding: 10px 4px 8px; border: none; background: transparent; font-size: 11px; color: #aaa; cursor: pointer; font-family: inherit; display: flex; flex-direction: column; align-items: center; gap: 3px; transition: color 0.15s; }
.nav-btn.active { color: #1a1a1a; font-weight: 600; }
.nav-icon { font-size: 20px; line-height: 1; }
.section { display: none; }
.section.active { display: block; }
.card { background: white; border: 1px solid #eee; border-radius: 16px; padding: 1.25rem; margin-bottom: 1rem; }
.card-title { font-size: 14px; font-weight: 700; color: #444; margin-bottom: 12px; }
.field { margin-bottom: 1rem; }
.field label { display: block; font-size: 13px; color: #666; margin-bottom: 6px; font-weight: 500; }
.field input, .field select { width: 100%; padding: 10px 12px; border: 1px solid #ddd; border-radius: 10px; font-size: 16px; background: white; color: #1a1a1a; font-family: inherit; outline: none; }
.field input:focus, .field select:focus { border-color: #1a1a1a; }
/* Who buttons */
.who-btns { display: flex; gap: 8px; }
.who-btn { flex: 1; padding: 10px 4px; border: 1px solid #ddd; border-radius: 10px; background: white; font-size: 15px; cursor: pointer; color: #666; font-family: inherit; font-weight: 500; transition: all 0.15s; }
.who-btn.amit.active { background: #EBF4FF; border-color: #2563EB; color: #1D4ED8; }
.who-btn.ela.active { background: #FDF2F8; border-color: #9D174D; color: #831843; }
.who-btn.shared.active { background: #F0FDF4; border-color: #059669; color: #065F46; }
.who-btn.personal.active { background: #FFF7ED; border-color: #C2410C; color: #9A3412; }
.add-btn { width: 100%; padding: 14px; border: none; border-radius: 12px; background: #1a1a1a; color: white; font-size: 16px; font-weight: 600; cursor: pointer; font-family: inherit; margin-top: 0.5rem; transition: opacity 0.15s; }
.add-btn:disabled { opacity: 0.5; }
/* Summary */
.grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 10px; }
.metric { background: white; border: 1px solid #eee; border-radius: 14px; padding: 1rem; }
.metric-label { font-size: 12px; color: #888; margin-bottom: 4px; font-weight: 500; }
.metric-value { font-size: 21px; font-weight: 700; color: #1a1a1a; }
.metric-sub { font-size: 12px; margin-top: 3px; }
.positive { color: #059669; }
.negative { color: #DC2626; }
.neutral { color: #888; }
.settle-card { background: white; border: 1px solid #eee; border-radius: 14px; padding: 1rem 1.25rem; margin-bottom: 10px; }
.settle-label { font-size: 12px; color: #888; font-weight: 500; margin-bottom: 4px; }
.settle-amount { font-size: 19px; font-weight: 700; }
.budget-bar-wrap { background: #f5f5f5; border-radius: 8px; height: 8px; margin-top: 8px; overflow: hidden; }
.budget-bar { height: 8px; border-radius: 8px; transition: width 0.4s; }
.bar-ok { background: #059669; }
.bar-warn { background: #F59E0B; }
.bar-over { background: #DC2626; }
.month-nav { display: flex; align-items: center; justify-content: center; gap: 12px; margin-bottom: 1rem; }
.month-btn { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 5px 14px; cursor: pointer; color: #666; font-size: 18px; font-family: inherit; }
.month-label { font-size: 16px; font-weight: 600; min-width: 110px; text-align: center; }
.cat-list { display: flex; flex-direction: column; }
.cat-row { display: flex; justify-content: space-between; align-items: center; font-size: 14px; padding: 8px 0; border-bottom: 1px solid #f0f0f0; }
.cat-row:last-child { border-bottom: none; }
.expense-list { display: flex; flex-direction: column; gap: 8px; }
.expense-item { background: white; border: 1px solid #eee; border-radius: 12px; padding: 12px 14px; display: flex; align-items: center; justify-content: space-between; }
.exp-dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; margin-left: 10px; }
.dot-amit { background: #2563EB; }
.dot-ela { background: #9D174D; }
.dot-shared { background: #059669; }
.exp-desc { font-size: 15px; font-weight: 500; }
.exp-meta { font-size: 12px; color: #888; margin-top: 2px; }
.del-btn { background: none; border: none; color: #ccc; cursor: pointer; font-size: 16px; padding: 2px 6px; }
.del-btn:hover { color: #DC2626; }
.empty { text-align: center; padding: 3rem 1rem; color: #aaa; font-size: 15px; }
/* Settings */
.setting-row { display: flex; align-items: center; justify-content: space-between; padding: 12px 0; border-bottom: 1px solid #f0f0f0; }
.setting-row:last-child { border-bottom: none; }
.setting-label { font-size: 15px; color: #1a1a1a; }
.setting-sub { font-size: 12px; color: #888; margin-top: 2px; }
.setting-input { width: 120px; padding: 7px 10px; border: 1px solid #ddd; border-radius: 8px; font-size: 15px; text-align: center; font-family: inherit; }
.toggle { position: relative; width: 44px; height: 26px; }
.toggle input { opacity: 0; width: 0; height: 0; }
.slider { position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0; background: #ddd; border-radius: 26px; transition: 0.3s; }
.slider:before { position: absolute; content: ""; height: 20px; width: 20px; right: 3px; bottom: 3px; background: white; border-radius: 50%; transition: 0.3s; }
input:checked + .slider { background: #1a1a1a; }
input:checked + .slider:before { transform: translateX(-18px); }
/* Recurring */
.recurring-item { background: white; border: 1px solid #eee; border-radius: 12px; padding: 12px 14px; display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px; }
.rec-info { flex: 1; }
.rec-name { font-size: 15px; font-weight: 500; }
.rec-meta { font-size: 12px; color: #888; margin-top: 2px; }
.rec-amount { font-size: 15px; font-weight: 700; margin-left: 10px; }
.save-btn { width: 100%; padding: 12px; border: none; border-radius: 12px; background: #1a1a1a; color: white; font-size: 15px; font-weight: 600; cursor: pointer; font-family: inherit; margin-top: 0.5rem; }
.sync-row { display: flex; align-items: center; justify-content: center; gap: 8px; margin-bottom: 1rem; }
.sync-btn { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 6px 14px; cursor: pointer; color: #666; font-size: 13px; font-family: inherit; }
.sync-status { font-size: 12px; color: #aaa; }
.toast { position: fixed; bottom: 80px; left: 50%; transform: translateX(-50%); color: white; padding: 11px 22px; border-radius: 12px; font-size: 15px; font-weight: 500; opacity: 0; pointer-events: none; transition: opacity 0.3s; z-index: 999; white-space: nowrap; }
.toast.success { background: #059669; }
.toast.error { background: #DC2626; }
.toast.show { opacity: 1; }
.filter-btns { display: flex; gap: 6px; margin-bottom: 1rem; flex-wrap: wrap; }
.filter-btn { padding: 6px 12px; border: 1px solid #ddd; border-radius: 20px; background: white; font-size: 13px; cursor: pointer; color: #666; font-family: inherit; }
.filter-btn.active { background: #1a1a1a; color: white; border-color: #1a1a1a; }
.section-badge { display: inline-block; font-size: 11px; font-weight: 600; padding: 2px 8px; border-radius: 20px; margin-right: 6px; }
.badge-amit { background: #EBF4FF; color: #1D4ED8; }
.badge-ela { background: #FDF2F8; color: #831843; }
.badge-shared { background: #F0FDF4; color: #065F46; }
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <h1>מעקב הוצאות</h1>
    <span id="header-month"></span>
  </div>
  <!-- הוסף הוצאה -->
<div id="tab-add" class="section active">
    <div class="card">
      <div class="field">
        <label>מי שילם?</label>
        <div class="who-btns">
          <button class="who-btn amit active" onclick="selectWho('עמית',this)">עמית</button>
          <button class="who-btn ela" onclick="selectWho('אלה',this)">אלה</button>
        </div>
      </div>
      <div class="field">
        <label>סוג הוצאה</label>
        <div class="who-btns">
          <button class="who-btn shared active" id="type-shared" onclick="selectType('משותפת',this)">משותפת 🤝</button>
          <button class="who-btn personal" id="type-personal" onclick="selectType('אישית',this)">אישית 👤</button>
        </div>
      </div>
      <div class="field">
        <label>סכום (₪)</label>
        <input type="number" id="amount" placeholder="0" min="0" step="0.01" inputmode="decimal">
      </div>
      <div class="field">
        <label>קטגוריה</label>
        <select id="category">
          <option>דיור</option><option>סופר</option><option>ריהוט</option><option>פנאי</option>
          <option>סטרימינג ואינטרנט</option><option>חשבונות</option><option>תחבורה</option>
          <option>מתנות ואירועים</option><option>חופשות ונופש</option><option>שונות</option>
        </select>
      </div>
      <div class="field">
        <label>תיאור (אופציונלי)</label>
        <input type="text" id="desc" placeholder="למשל: קניות בשוק">
      </div>
      <div class="field">
        <label>תאריך</label>
        <input type="date" id="date">
      </div>
      <button class="add-btn" id="add-btn" onclick="addExpense()">+ הוסף הוצאה</button>
    </div>
  </div>
  <!-- סיכום -->
<div id="tab-summary" class="section">
    <div class="month-nav">
      <button class="month-btn" onclick="changeMonth(-1)">\&#8249;</button>
      <span class="month-label" id="summary-month"></span>
      <button class="month-btn" onclick="changeMonth(1)">\&#8250;</button>
    </div>
    <div class="sync-row">
      <button class="sync-btn" onclick="loadFromSheets()">רענן</button>
      <span class="sync-status" id="sync-status"></span>
    </div>
    <!-- תקציב משותף -->
<div id="budget-card" class="card" style="display:none">
<div class="card-title">תקציב משותף</div>
<div class="grid2">
<div class="metric">
<div class="metric-label">הוצאתם יחד</div>
<div class="metric-value" id="budget-spent">₪0</div>
</div>
<div class="metric">
<div class="metric-label">נותר מהתקציב</div>
<div class="metric-value" id="budget-left">—</div>
<div class="metric-sub" id="budget-sub"></div>
</div>
</div>
<div class="budget-bar-wrap"><div class="budget-bar bar-ok" id="budget-bar" style="width:0%"></div></div>
</div>
    <!-- יעדים אישיים -->
    <div class="grid2">
      <div class="metric">
        <div class="metric-label">עמית שילם</div>
        <div class="metric-value" id="amit-total">₪0</div>
        <div class="metric-sub" id="amit-sub"></div>
      </div>
      <div class="metric">
        <div class="metric-label">אלה שילמה</div>
        <div class="metric-value" id="ela-total">₪0</div>
        <div class="metric-sub" id="ela-sub"></div>
      </div>
    </div>

    <div class="settle-card">
      <div class="settle-label">הסדר חשבון</div>
      <div class="settle-amount" id="settle-text">אין נתונים</div>
    </div>

    <div class="grid2">
      <div class="metric">
        <div class="metric-label">עמית — משותף</div>
        <div class="metric-value" id="amit-shared-total">₪0</div>
        <div class="metric-sub" id="amit-personal-sub" style="color:#888"></div>
      </div>
      <div class="metric">
        <div class="metric-label">אלה — משותף</div>
        <div class="metric-value" id="ela-shared-total">₪0</div>
        <div class="metric-sub" id="ela-personal-sub" style="color:#888"></div>
      </div>
    </div>
    <div class="card">
      <div class="card-title">פירוט לפי קטגוריה</div>
      <div class="cat-list" id="cat-list"></div>
    </div>
    <div class="metric" style="margin-bottom:10px">
      <div class="metric-label">סה"כ הוצאות החודש (כולל אישיות)</div>
      <div class="metric-value" id="grand-total-summary">₪0</div>
    </div>

</div>
  <!-- רשימה -->
<div id="tab-list" class="section">
    <div class="month-nav">
      <button class="month-btn" onclick="changeMonth(-1)">\&#8249;</button>
      <span class="month-label" id="list-month"></span>
      <button class="month-btn" onclick="changeMonth(1)">\&#8250;</button>
    </div>
    <div class="filter-btns">
      <button class="filter-btn active" onclick="setFilter('הכל',this)">הכל</button>
      <button class="filter-btn" onclick="setFilter('משותפת',this)">משותפות 🤝</button>
      <button class="filter-btn" onclick="setFilter('עמית',this)">עמית</button>
      <button class="filter-btn" onclick="setFilter('אלה',this)">אלה</button>
    </div>
    <div class="expense-list" id="expense-list"></div>
  </div>
  <!-- הגדרות -->
<div id="tab-settings" class="section">
    <div class="card">
      <div class="card-title">יעדים אישיים</div>
      <div class="setting-row">
        <div>
          <div class="setting-label">יעד עמית (₪/חודש)</div>
          <div class="setting-sub">כמה עמית אמור לשלם</div>
        </div>
        <input class="setting-input" type="number" id="s-amit-target" placeholder="ללא יעד">
      </div>
      <div class="setting-row">
        <div>
          <div class="setting-label">יעד אלה (₪/חודש)</div>
          <div class="setting-sub">כמה אלה אמורה לשלם</div>
        </div>
        <input class="setting-input" type="number" id="s-ela-target" placeholder="ללא יעד">
      </div>
    </div>
    <div class="card">
<div class="card-title">תקציב משותף</div>
<div class="setting-row">
<div>
<div class="setting-label">הפעל תקציב משותף</div>
<div class="setting-sub">תקרה חודשית לזוג</div>
</div>
<label class="toggle"><input type="checkbox" id="s-budget-on" onchange="toggleBudget()"><span class="slider"></span></label>
</div>
<div id="budget-input-row" class="setting-row" style="display:none">
<div>
<div class="setting-label">תקרה חודשית (₪)</div>
</div>
<input class="setting-input" type="number" id="s-budget-limit" placeholder="0">
</div>
</div>
    <button class="save-btn" onclick="saveSettings()">שמור הגדרות</button>

    <!-- הוצאות חוזרות -->
    <div class="card" style="margin-top:1rem">
      <div class="card-title">הוצאות חוזרות</div>
      <div id="recurring-list"></div>
      <div style="margin-top:12px; border-top:1px solid #f0f0f0; padding-top:12px;">
        <div class="field">
          <label>שם ההוצאה</label>
          <input type="text" id="r-name" placeholder="למשל: שכר דירה">
        </div>
        <div class="field">
          <label>סכום (₪)</label>
          <input type="number" id="r-amount" placeholder="0" inputmode="decimal">
        </div>
        <div class="field">
          <label>מי משלם?</label>
          <div class="who-btns">
            <button class="who-btn amit active" onclick="selectRecWho('עמית',this)">עמית</button>
            <button class="who-btn ela" onclick="selectRecWho('אלה',this)">אלה</button>
            <button class="who-btn shared" onclick="selectRecWho('משותף',this)">משותף</button>
          </div>
        </div>
        <div class="field">
          <label>קטגוריה</label>
          <select id="r-category">
            <option>דיור</option><option>סופר</option><option>ריהוט</option><option>פנאי</option>
            <option>סטרימינג ואינטרנט</option><option>חשבונות</option><option>תחבורה</option>
            <option>מתנות ואירועים</option><option>חופשות ונופש</option><option>שונות</option>
          </select>
        </div>
        <div class="field">
          <label>באיזה יום בחודש?</label>
          <input type="number" id="r-day" placeholder="1" min="1" max="28" inputmode="numeric">
        </div>
        <button class="save-btn" onclick="addRecurring()">+ הוסף הוצאה חוזרת</button>
      </div>
    </div>

</div>
</div>
<!-- Bottom Nav -->
<div class="bottom-nav">
  <button class="nav-btn active" onclick="showTab('add',this)">
    <span class="nav-icon">➕</span>הוסף
  </button>
  <button class="nav-btn" onclick="showTab('summary',this)">
    <span class="nav-icon">📊</span>סיכום
  </button>
  <button class="nav-btn" onclick="showTab('list',this)">
    <span class="nav-icon">📋</span>רשימה
  </button>
  <button class="nav-btn" onclick="showTab('settings',this)">
    <span class="nav-icon">⚙️</span>הגדרות
  </button>
</div>
<div class="toast" id="toast"></div>
<script>
const API = 'https://script.google.com/macros/s/AKfycbwLRDfOwDvrf3AD2Ub3\_v22sBOeu9OeUBe3CToEuFGYA-s4PxzKRCApYcUV1c3kJfaJAQ/exec';
const MONTHS = \['ינואר','פברואר','מרץ','אפריל','מאי','יוני','יולי','אוגוסט','ספטמבר','אוקטובר','נובמבר','דצמבר'];

let who = 'עמית';
let expenseType = 'משותפת';
let recWho = 'עמית';
let listFilter = 'הכל';
let now = new Date();
let viewMonth = now.getMonth();
let viewYear = now.getFullYear();
let expenses = \[];

// Settings stored locally
const savedSettings = localStorage.getItem('settings\_v2');
let settings = savedSettings ? JSON.parse(savedSettings) : {};
if (settings.amitTarget === undefined) settings.amitTarget = 0;
if (settings.elaTarget === undefined) settings.elaTarget = 0;
if (settings.budgetOn === undefined) settings.budgetOn = false;
if (settings.budgetLimit === undefined) settings.budgetLimit = 0;
if (!settings.recurring) settings.recurring = \[];

function saveSettingsLocal() {
  localStorage.setItem('settings\_v2', JSON.stringify(settings));
}

function init() {
  document.getElementById('date').value = now.toISOString().split('T')\[0];
  document.getElementById('header-month').textContent = MONTHS\[now.getMonth()] + ' ' + now.getFullYear();
  updateLabels();
  loadSettingsUI();
  loadFromSheets();
  checkRecurring();
}

function loadSettingsUI() {
  document.getElementById('s-amit-target').value = settings.amitTarget || '';
  document.getElementById('s-ela-target').value = settings.elaTarget || '';
  document.getElementById('s-budget-on').checked = settings.budgetOn;
  document.getElementById('s-budget-limit').value = settings.budgetLimit || '';
  document.getElementById('budget-input-row').style.display = settings.budgetOn ? 'flex' : 'none';
  renderRecurring();
}

function toggleBudget() {
  const on = document.getElementById('s-budget-on').checked;
  document.getElementById('budget-input-row').style.display = on ? 'flex' : 'none';
}

function saveSettings() {
  settings.amitTarget = parseFloat(document.getElementById('s-amit-target').value) || 0;
  settings.elaTarget = parseFloat(document.getElementById('s-ela-target').value) || 0;
  settings.budgetOn = document.getElementById('s-budget-on').checked;
  settings.budgetLimit = parseFloat(document.getElementById('s-budget-limit').value) || 0;
  saveSettingsLocal();
  showToast('ההגדרות נשמרו ✓', 'success');
  render();
}

function showTab(name, btn) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
  btn.classList.add('active');
  render();
}

function selectWho(name, btn) {
  who = name;
  btn.closest('.who-btns').querySelectorAll('button').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
}

function selectType(type, btn) {
  expenseType = type;
  const typeRow = document.getElementById('type-shared').parentElement;
  typeRow.querySelectorAll('button').forEach(b => {
    b.classList.remove('active');
  });
  btn.classList.add('active');
}

function selectRecWho(name, btn) {
  recWho = name;
  document.querySelectorAll('#tab-settings .who-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
}

function setFilter(f, btn) {
  listFilter = f;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderList();
}

function changeMonth(dir) {
  viewMonth += dir;
  if (viewMonth > 11) { viewMonth = 0; viewYear++; }
  if (viewMonth < 0) { viewMonth = 11; viewYear--; }
  updateLabels();
  render();
}

function updateLabels() {
  const label = MONTHS\[viewMonth] + ' ' + viewYear;
  document.getElementById('summary-month').textContent = label;
  document.getElementById('list-month').textContent = label;
}

function getMonthExp() {
  return expenses.filter(e => {
    const d = new Date(e.date);
    return d.getMonth() === viewMonth \&\& d.getFullYear() === viewYear;
  });
}

function fmt(n) { return '₪' + Math.round(n).toLocaleString('he-IL'); }

function setSyncStatus(msg) {
  const el = document.getElementById('sync-status');
  if (el) el.textContent = msg;
}

async function loadFromSheets() {
  setSyncStatus('טוען...');
  try {
    const res = await fetch(API);
    const json = await res.json();
    if (json.success) {
      expenses = json.data.map(e => ({
        id: e.id, date: e.date, who: e.who,
        amount: parseFloat(e.amount), category: e.category, desc: e.desc || '', type: e.type || 'משותפת'
      })).filter(e => e.date \&\& !isNaN(e.amount));
      setSyncStatus('עודכן ' + new Date().toLocaleTimeString('he-IL', {hour:'2-digit',minute:'2-digit'}));
      render();
    }
  } catch(err) {
    setSyncStatus('שגיאה');
    showToast('שגיאה בטעינה', 'error');
  }
}

async function addExpense() {
  const amount = parseFloat(document.getElementById('amount').value);
  const category = document.getElementById('category').value;
  const desc = document.getElementById('desc').value.trim();
  const date = document.getElementById('date').value;
  if (!amount || amount <= 0) { alert('נא להזין סכום תקין'); return; }
  if (!date) { alert('נא לבחור תאריך'); return; }
  const btn = document.getElementById('add-btn');
  btn.disabled = true; btn.textContent = 'שומר...';
  const expense = { id: Date.now(), who, amount, category, desc, date, type: expenseType };
  try {
    await fetch(API, { method: 'POST', body: JSON.stringify({ action: 'add', ...expense }) });
    expenses.push(expense);
    document.getElementById('amount').value = '';
    document.getElementById('desc').value = '';
    showToast('ההוצאה נוספה ✓', 'success');
    render();
  } catch(err) { showToast('שגיאה בשמירה', 'error'); }
  btn.disabled = false; btn.textContent = '+ הוסף הוצאה';
}

async function deleteExpense(id) {
  if (!confirm('למחוק את ההוצאה?')) return;
  try {
    await fetch(API, { method: 'POST', body: JSON.stringify({ action: 'delete', id }) });
    expenses = expenses.filter(e => String(e.id) !== String(id));
    render();
    showToast('נמחק', 'success');
  } catch(err) { showToast('שגיאה במחיקה', 'error'); }
}

function addRecurring() {
  const name = document.getElementById('r-name').value.trim();
  const amount = parseFloat(document.getElementById('r-amount').value);
  const category = document.getElementById('r-category').value;
  const day = parseInt(document.getElementById('r-day').value) || 1;
  if (!name) { alert('נא להזין שם'); return; }
  if (!amount || amount <= 0) { alert('נא להזין סכום'); return; }
  settings.recurring.push({ id: Date.now(), name, amount, who: recWho, category, day });
  saveSettingsLocal();
  document.getElementById('r-name').value = '';
  document.getElementById('r-amount').value = '';
  document.getElementById('r-day').value = '';
  renderRecurring();
  showToast('נוספה הוצאה חוזרת ✓', 'success');
}

function deleteRecurring(id) {
  settings.recurring = settings.recurring.filter(r => r.id !== id);
  saveSettingsLocal();
  renderRecurring();
}

function renderRecurring() {
  const el = document.getElementById('recurring-list');
  if (!settings.recurring.length) {
    el.innerHTML = '<div style="color:#aaa;font-size:14px;padding:8px 0;text-align:center">אין הוצאות חוזרות עדיין</div>';
    return;
  }
  el.innerHTML = settings.recurring.map(r => `
    <div class="recurring-item">
      <div class="rec-info">
        <div class="rec-name">${r.name}</div>
        <div class="rec-meta">${r.who} · ${r.category} · יום ${r.day} לחודש</div>
      </div>
      <span class="rec-amount">${fmt(r.amount)}</span>
      <button class="del-btn" onclick="deleteRecurring(${r.id})">✕</button>
    </div>
  `).join('');
}

async function checkRecurring() {
  if (!settings.recurring.length) return;
  const today = new Date();
  const todayDay = today.getDate();
  const monthKey = today.getFullYear() + '-' + today.getMonth();
  const doneKey = 'rec\_done\_' + monthKey;
  const done = JSON.parse(localStorage.getItem(doneKey) || '\[]');

  for (const r of settings.recurring) {
    if (done.includes(r.id)) continue;
    if (todayDay >= r.day) {
      const dateStr = today.getFullYear() + '-' + String(today.getMonth()+1).padStart(2,'0') + '-' + String(r.day).padStart(2,'0');
      const expense = { id: Date.now(), who: r.who, amount: r.amount, category: r.category, desc: r.name, date: dateStr };
      try {
        await fetch(API, { method: 'POST', body: JSON.stringify({ action: 'add', ...expense }) });
        expenses.push(expense);
        done.push(r.id);
        localStorage.setItem(doneKey, JSON.stringify(done));
      } catch(e) {}
    }
  }
  render();
}

function showToast(msg, type) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast ' + type + ' show';
  setTimeout(() => t.classList.remove('show'), 2500);
}

function render() { renderSummary(); renderList(); }

function renderSummary() {
  const list = getMonthExp();
  const sharedList = list.filter(e => !e.type || e.type === 'משותפת');
  const amitShared = sharedList.filter(e => e.who === 'עמית').reduce((s,e) => s+e.amount, 0);
  const elaShared = sharedList.filter(e => e.who === 'אלה').reduce((s,e) => s+e.amount, 0);
  const sharedGrand = sharedList.reduce((s,e) => s+e.amount, 0);
  const amitPersonal = list.filter(e => e.type === 'אישית' \&\& e.who === 'עמית').reduce((s,e) => s+e.amount, 0);
  const elaPersonal = list.filter(e => e.type === 'אישית' \&\& e.who === 'אלה').reduce((s,e) => s+e.amount, 0);
  const amitTotal = amitShared + amitPersonal;
  const elaTotal = elaShared + elaPersonal;
  const grand = amitTotal + elaTotal;

  document.getElementById('amit-total').textContent = fmt(amitTotal);
  document.getElementById('ela-total').textContent = fmt(elaTotal);

  const elaTarget = settings.elaTarget;
  const amitTarget = settings.amitTarget;
  const elaSubEl = document.getElementById('ela-sub');
  const amitSubEl = document.getElementById('amit-sub');

  if (elaTarget > 0) {
    const diff = elaShared - elaTarget;
    if (diff >= 0) { elaSubEl.textContent = 'שילמה ' + fmt(diff) + ' יותר'; elaSubEl.className = 'metric-sub positive'; }
    else { elaSubEl.textContent = 'נותרו ' + fmt(-diff); elaSubEl.className = 'metric-sub negative'; }
  } else { elaSubEl.textContent = 'ללא יעד'; elaSubEl.className = 'metric-sub neutral'; }

  if (amitTarget > 0) {
    const diff = amitShared - amitTarget;
    if (diff >= 0) { amitSubEl.textContent = 'שילם ' + fmt(diff) + ' יותר'; amitSubEl.className = 'metric-sub positive'; }
    else { amitSubEl.textContent = 'נותרו ' + fmt(-diff); amitSubEl.className = 'metric-sub negative'; }
  } else { amitSubEl.textContent = 'משלים את השאר'; amitSubEl.className = 'metric-sub neutral'; }

  // תקציב משותף (רק הוצאות משותפות)
  const budgetCard = document.getElementById('budget-card');
  if (settings.budgetOn \&\& settings.budgetLimit > 0) {
    budgetCard.style.display = 'block';
    document.getElementById('budget-spent').textContent = fmt(sharedGrand);
    const left = settings.budgetLimit - sharedGrand;
    const leftEl = document.getElementById('budget-left');
    const subEl = document.getElementById('budget-sub');
    const bar = document.getElementById('budget-bar');
    const pct = Math.min(100, Math.round((sharedGrand / settings.budgetLimit) \* 100));
    bar.style.width = pct + '%';
    if (left >= 0) {
      leftEl.textContent = fmt(left);
      leftEl.style.color = '#1a1a1a';
      subEl.textContent = pct + '% מהתקציב';
      subEl.className = 'metric-sub neutral';
      bar.className = 'budget-bar ' + (pct > 80 ? 'bar-warn' : 'bar-ok');
    } else {
      leftEl.textContent = fmt(-left) + ' חריגה!';
      leftEl.style.color = '#DC2626';
      subEl.textContent = 'חרגתם מהתקציב';
      subEl.className = 'metric-sub negative';
      bar.className = 'budget-bar bar-over';
    }
  } else {
    budgetCard.style.display = 'none';
  }

  // הסדר חשבון (מבוסס על הוצאות משותפות בלבד)
  const settleEl = document.getElementById('settle-text');
  if (sharedGrand === 0) { settleEl.textContent = 'אין הוצאות משותפות החודש'; settleEl.style.color = '#888'; }
  else if (elaTarget === 0 \&\& amitTarget === 0) {
    settleEl.textContent = 'הגדר יעד לפחות לאחד מכם בהגדרות';
    settleEl.style.color = '#888';
  } else {
    let amitOwed, elaOwed;
    if (amitTarget > 0 \&\& elaTarget > 0) {
      amitOwed = amitTarget; elaOwed = elaTarget;
    } else if (amitTarget > 0 \&\& elaTarget === 0) {
      amitOwed = amitTarget; elaOwed = sharedGrand - amitTarget;
    } else {
      elaOwed = elaTarget; amitOwed = sharedGrand - elaTarget;
    }
    const amitDiff = amitShared - amitOwed;
    if (Math.abs(amitDiff) < 1) { settleEl.textContent = 'מיושב! אין מה להחזיר'; settleEl.style.color = '#059669'; }
    else if (amitDiff > 0) { settleEl.textContent = 'אלה חייבת לעמית ' + fmt(amitDiff); settleEl.style.color = '#DC2626'; }
    else { settleEl.textContent = 'עמית חייב לאלה ' + fmt(-amitDiff); settleEl.style.color = '#2563EB'; }
  }

  // פירוט אישי/משותף
  const amitSharedEl = document.getElementById('amit-shared-total');
  if (amitSharedEl) {
    amitSharedEl.textContent = fmt(amitShared);
    document.getElementById('amit-personal-sub').textContent = amitPersonal > 0 ? 'אישי: ' + fmt(amitPersonal) : 'ללא הוצאות אישיות';
  }
  const elaSharedEl = document.getElementById('ela-shared-total');
  if (elaSharedEl) {
    elaSharedEl.textContent = fmt(elaShared);
    document.getElementById('ela-personal-sub').textContent = elaPersonal > 0 ? 'אישי: ' + fmt(elaPersonal) : 'ללא הוצאות אישיות';
  }

  // קטגוריות
  const cats = {};
  list.forEach(e => { cats\[e.category] = (cats\[e.category]||0) + e.amount; });
  const sorted = Object.entries(cats).sort((a,b) => b\[1]-a\[1]);
  document.getElementById('grand-total-summary').textContent = fmt(grand);
  document.getElementById('cat-list').innerHTML = sorted.length === 0
    ? '<div style="color:#aaa;font-size:14px;padding:8px 0">אין נתונים</div>'
    : sorted.map((\[cat,amt]) => '<div class="cat-row"><span>' + cat + '</span><span style="font-weight:700">' + fmt(amt) + '</span></div>').join('');
}

function renderList() {
  const list = getMonthExp().slice().reverse();
  const filtered = listFilter === 'הכל' ? list :
    listFilter === 'משותפת' ? list.filter(e => !e.type || e.type === 'משותפת') :
    list.filter(e => e.who === listFilter);
  const el = document.getElementById('expense-list');
  if (!filtered.length) { el.innerHTML = '<div class="empty">אין הוצאות</div>'; return; }
  const dotClass = { 'עמית': 'dot-amit', 'אלה': 'dot-ela', 'משותף': 'dot-shared' };
  el.innerHTML = filtered.map(e => {
    const d = new Date(e.date);
    const dateStr = d.getDate() + '/' + (d.getMonth()+1);
    return `<div class="expense-item">
      <div style="display:flex;align-items:center;flex:1">
        <div class="exp-dot ${dotClass\[e.who]||'dot-shared'}"></div>
        <div>
          <div class="exp-desc">${e.desc||e.category}</div>
          <div class="exp-meta">${e.who} · ${e.type||'משותפת'} · ${e.category} · ${dateStr}</div>
        </div>
      </div>
      <div style="display:flex;align-items:center;gap:8px">
        <span style="font-size:15px;font-weight:700">${fmt(e.amount)}</span>
        <button class="del-btn" onclick="deleteExpense(${e.id})">✕</button>
      </div>
    </div>`;
  }).join('');
}

init();

</body>
</html>
