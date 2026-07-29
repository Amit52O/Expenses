<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>מעקב הוצאות - עמית ואלה</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: #f5f5f5; color: #1a1a1a; direction: rtl; }
.app { max-width: 430px; margin: 0 auto; padding: 1rem; min-height: 100vh; padding-bottom: 90px; }
.header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 1.2rem; padding-top: 0.5rem; }
.header h1 { font-size: 21px; font-weight: 700; }
.header span { font-size: 13px; color: #888; }

/* Bottom nav */
.bottom-nav { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 430px; background: white; border-top: 1px solid #eee; display: flex; z-index: 100; padding-bottom: env(safe-area-inset-bottom); }
.nav-btn { flex: 1; padding: 10px 4px 8px; border: none; background: transparent; font-size: 11px; color: #aaa; cursor: pointer; display: flex; flex-direction: column; align-items: center; gap: 3px; }
.nav-btn.active { color: #1a1a1a; font-weight: 600; }
.nav-icon { font-size: 20px; line-height: 1; }

.section { display: none; }
.section.active { display: block; }
.card { background: white; border: 1px solid #eee; border-radius: 16px; padding: 1.25rem; margin-bottom: 1rem; }
.card-title { font-size: 14px; font-weight: 700; color: #444; margin-bottom: 12px; }
.field { margin-bottom: 1rem; }
.field label { display: block; font-size: 13px; color: #666; margin-bottom: 6px; font-weight: 500; }
.field input, .field select { width: 100%; padding: 10px 12px; border: 1px solid #ddd; border-radius: 10px; font-size: 16px; background: white; outline: none; }

.who-btns { display: flex; gap: 8px; }
.who-btn { flex: 1; padding: 10px 4px; border: 1px solid #ddd; border-radius: 10px; background: white; font-size: 15px; cursor: pointer; color: #666; font-weight: 500; }
.who-btn.amit.active { background: #EBF4FF; border-color: #2563EB; color: #1D4ED8; }
.who-btn.ela.active { background: #FDF2F8; border-color: #9D174D; color: #831843; }
.who-btn.shared.active { background: #F0FDF4; border-color: #059669; color: #065F46; }
.who-btn.personal.active { background: #FFF7ED; border-color: #C2410C; color: #9A3412; }

.add-btn { width: 100%; padding: 14px; border: none; border-radius: 12px; background: #1a1a1a; color: white; font-size: 16px; font-weight: 600; cursor: pointer; margin-top: 0.5rem; }

.grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 10px; }
.metric { background: white; border: 1px solid #eee; border-radius: 14px; padding: 1rem; }
.metric-label { font-size: 12px; color: #888; margin-bottom: 4px; font-weight: 500; }
.metric-value { font-size: 21px; font-weight: 700; color: #1a1a1a; }
.metric-sub { font-size: 12px; margin-top: 3px; color: #888; }

/* עיצוב התראת חריגה */
.over-budget { color: #DC2626 !important; }
.budget-box { background: #F8FAFC; border: 1px dashed #CBD5E1; border-radius: 12px; padding: 12px; margin-bottom: 1rem; text-align: center; }

.month-nav { display: flex; align-items: center; justify-content: center; gap: 12px; margin-bottom: 1rem; }
.month-btn { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 5px 14px; cursor: pointer; color: #666; font-size: 18px; }
.month-label { font-size: 16px; font-weight: 600; min-width: 110px; text-align: center; }

.expense-list { display: flex; flex-direction: column; gap: 8px; }
.expense-item { background: white; border: 1px solid #eee; border-radius: 12px; padding: 12px 14px; display: flex; align-items: center; justify-content: space-between; }
.exp-dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; margin-left: 10px; }
.dot-amit { background: #2563EB; }
.dot-ela { background: #9D174D; }
.dot-shared { background: #059669; }
.exp-desc { font-size: 15px; font-weight: 500; }
.exp-meta { font-size: 12px; color: #888; margin-top: 2px; }
.del-btn { background: none; border: none; color: #ccc; cursor: pointer; font-size: 16px; padding: 2px 6px; }
.empty { text-align: center; padding: 3rem 1rem; color: #aaa; font-size: 15px; }

.toast { position: fixed; bottom: 80px; left: 50%; transform: translateX(-50%); color: white; padding: 11px 22px; border-radius: 12px; font-size: 15px; font-weight: 500; opacity: 0; transition: opacity 0.3s; z-index: 999; }
.toast.success { background: #059669; }
.toast.error { background: #DC2626; }
.toast.show { opacity: 1; }

.cat-item-edit { display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid #eee; }
.cat-item-edit:last-child { border-bottom: none; }
.add-cat-row { display: flex; gap: 8px; margin-top: 10px; }
.add-cat-row input { flex: 1; padding: 8px 12px; border: 1px solid #ddd; border-radius: 8px; }
.add-cat-row button { background: #1a1a1a; color: white; border: none; border-radius: 8px; padding: 0 16px; font-weight: bold; }

.chart-container { position: relative; width: 100%; max-width: 300px; margin: 0 auto 1.5rem auto; display: none; }
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <h1>מעקב הוצאות</h1>
    <span id="header-month"></span>
  </div>

  <!-- מסך הוספת הוצאה -->
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
          <button class="who-btn shared active" onclick="selectType('משותפת',this)">משותפת 🤝</button>
          <button class="who-btn personal" onclick="selectType('אישית',this)">אישית 👤</button>
        </div>
      </div>
      <div class="field">
        <label>סכום (₪)</label>
        <input type="number" id="amount" placeholder="0" min="0" step="0.01" inputmode="decimal">
      </div>
      <div class="field">
        <label>קטגוריה</label>
        <select id="category"></select> 
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

  <!-- מסך סיכום ותרשימים -->
  <div id="tab-summary" class="section">
    <div class="month-nav">
      <button class="month-btn" onclick="changeMonth(-1)">&#8249;</button>
      <span class="month-label" id="summary-month"></span>
      <button class="month-btn" onclick="changeMonth(1)">&#8250;</button>
    </div>
    
    <!-- תיבת מעקב תקציב משותף -->
    <div class="budget-box">
      <div class="metric-label">תקציב משותף חודשי</div>
      <div class="metric-value" id="shared-budget-status">₪0 / ₪0</div>
      <div class="metric-sub" id="shared-budget-diff">נשאר לתקציב: ₪0</div>
    </div>

    <!-- תיבת החזרים לפי היעד של אלה -->
    <div class="card" style="background: #EFF6FF; border-color: #BFDBFE;">
      <div class="card-title" style="color: #1E40AF;">סטטוס החזרים (לפי יעד אלה)</div>
      <div style="font-size: 14px; color: #1E3A8A;" id="settlement-text">טוען נתונים...</div>
    </div>

    <div class="grid2">
      <div class="metric">
        <div class="metric-label">עמית שילם (משותף)</div>
        <div class="metric-value" id="amit-shared-total">₪0</div>
      </div>
      <div class="metric">
        <div class="metric-label">אלה שילמה (משותף)</div>
        <div class="metric-value" id="ela-shared-total">₪0</div>
      </div>
    </div>
    
    <div class="metric" style="margin-bottom:1rem">
      <div class="metric-label">סה"כ הוצאות החודש (כללי)</div>
      <div class="metric-value" id="grand-total-summary">₪0</div>
    </div>

    <!-- תרשימי עוגה -->
    <div class="card" id="charts-card">
      <div class="card-title" style="text-align:center; margin-bottom: 20px;">פילוג הוצאות חודשי</div>
      
      <div class="chart-container" id="container-sharedChart">
        <canvas id="sharedChart"></canvas>
      </div>
      
      <div class="chart-container" id="container-amitChart">
        <canvas id="amitChart"></canvas>
      </div>
      
      <div class="chart-container" id="container-elaChart">
        <canvas id="elaChart"></canvas>
      </div>
    </div>
  </div>

  <!-- מסך רשימה -->
  <div id="tab-list" class="section">
    <div class="month-nav">
      <button class="month-btn" onclick="changeMonth(-1)">&#8249;</button>
      <span class="month-label" id="list-month"></span>
      <button class="month-btn" onclick="changeMonth(1)">&#8250;</button>
    </div>
    <button class="add-btn" style="background:#ddd; color:#333; margin-bottom:1rem;" onclick="loadFromSheets()">רענן רשימה מהשרת</button>
    <div class="expense-list" id="expense-list"></div>
  </div>

  <!-- מסך הגדרות -->
  <div id="tab-settings" class="section">
    <div class="card">
      <div class="card-title">הגדרות תקציב וחוקים</div>
      <div class="field">
        <label>תקציב משותף חודשי (₪)</label>
        <input type="number" id="setting-shared-budget" placeholder="0" onchange="saveBudgets()">
      </div>
      <div class="field">
        <label>יעד הוצאה משותפת לאלה (₪)</label>
        <input type="number" id="setting-ela-target" placeholder="0" onchange="saveBudgets()">
      </div>
    </div>

    <div class="card">
      <div class="card-title">עריכת קטגוריות</div>
      <div style="font-size:12px; color:#888; margin-bottom:12px;">הקטגוריות והתקציבים נשמרים במכשיר זה.</div>
      <div id="categories-edit-list"></div>
      
      <div class="add-cat-row">
        <input type="text" id="new-cat-input" placeholder="שם קטגוריה חדשה">
        <button onclick="addNewCategory()">הוסף</button>
      </div>
    </div>
  </div>
</div>

<!-- תפריט תחתון -->
<div class="bottom-nav">
  <button class="nav-btn active" onclick="showTab('add',this)"><span class="nav-icon">➕</span>הוסף</button>
  <button class="nav-btn" onclick="showTab('summary',this)"><span class="nav-icon">📊</span>סיכום</button>
  <button class="nav-btn" onclick="showTab('list',this)"><span class="nav-icon">📋</span>רשימה</button>
  <button class="nav-btn" onclick="showTab('settings',this)"><span class="nav-icon">⚙️</span>הגדרות</button>
</div>

<div class="toast" id="toast"></div>

<script>
const API = 'https://script.google.com/macros/s/AKfycbwLRDfOwDvrf3AD2Ub3_v22sBOeu9OeUBe3CToEuFGYA-s4PxzKRCApYcUV1c3kJfaJAQ/exec';
const MONTHS = ['ינואר','פברואר','מרץ','אפריל','מאי','יוני','יולי','אוגוסט','ספטמבר','אוקטובר','נובמבר','דצמבר'];

let who = 'עמית';
let expenseType = 'משותפת';
let now = new Date();
let viewMonth = now.getMonth();
let viewYear = now.getFullYear();
let expenses = [];

// טעינת הגדרות תקציב וקטגוריות מ-LocalStorage
const defaultCategories = ['דיור', 'סופר', 'ריהוט', 'פנאי', 'סטרימינג ואינטרנט', 'חשבונות', 'תחבורה', 'מתנות ואירועים', 'חופשות ונופש', 'שונות'];
let userCategories = JSON.parse(localStorage.getItem('my_categories')) || defaultCategories;
let sharedBudget = parseFloat(localStorage.getItem('my_shared_budget')) || 0;
let elaTarget = parseFloat(localStorage.getItem('my_ela_target')) || 0;

let chartInstances = { shared: null, amit: null, ela: null };
const chartColors = ['#2563EB', '#059669', '#F59E0B', '#9D174D', '#8B5CF6', '#EC4899', '#10B981', '#F43F5E', '#3B82F6', '#6366F1'];

function init() {
  document.getElementById('date').value = now.toISOString().split('T')[0];
  document.getElementById('setting-shared-budget').value = sharedBudget || '';
  document.getElementById('setting-ela-target').value = elaTarget || '';
  populateCategoryDropdowns();
  updateLabels();
  loadFromSheets();
  renderCategoriesSettings();
}

function saveBudgets() {
  sharedBudget = parseFloat(document.getElementById('setting-shared-budget').value) || 0;
  elaTarget = parseFloat(document.getElementById('setting-ela-target').value) || 0;
  localStorage.setItem('my_shared_budget', sharedBudget);
  localStorage.setItem('my_ela_target', elaTarget);
  showToast('הגדרות התקציב שנשמרו ✓', 'success');
  renderSummary();
}

function populateCategoryDropdowns() {
  const select = document.getElementById('category');
  select.innerHTML = userCategories.map(cat => `<option value="${cat}">${cat}</option>`).join('');
}

function renderCategoriesSettings() {
  const listEl = document.getElementById('categories-edit-list');
  listEl.innerHTML = userCategories.map((cat, index) => `
    <div class="cat-item-edit">
      <span>${cat}</span>
      <button class="del-btn" onclick="deleteCategory(${index})">✕</button>
    </div>
  `).join('');
}

function addNewCategory() {
  const input = document.getElementById('new-cat-input');
  const val = input.value.trim();
  if (!val) return;
  if (userCategories.includes(val)) { alert('הקטגוריה כבר קיימת'); return; }
  userCategories.push(val);
  saveCategories();
  input.value = '';
  showToast('קטגוריה נוספה ✓', 'success');
}

function deleteCategory(index) {
  if (userCategories.length <= 1) { alert('חייבת להישאר לפחות קטגוריה אחת'); return; }
  if (confirm('למחוק את הקטגוריה הזו?')) {
    userCategories.splice(index, 1);
    saveCategories();
    showToast('קטגוריה נמחקה', 'success');
  }
}

function saveCategories() {
  localStorage.setItem('my_categories', JSON.stringify(userCategories));
  populateCategoryDropdowns();
  renderCategoriesSettings();
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
  btn.closest('.who-btns').querySelectorAll('button').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
}

function changeMonth(dir) {
  viewMonth += dir;
  if (viewMonth > 11) { viewMonth = 0; viewYear++; }
  if (viewMonth < 0) { viewMonth = 11; viewYear--; }
  updateLabels();
  render();
}

function updateLabels() {
  const label = MONTHS[viewMonth] + ' ' + viewYear;
  document.getElementById('header-month').textContent = label;
  document.getElementById('summary-month').textContent = label;
  document.getElementById('list-month').textContent = label;
}

function getMonthExp() {
  return expenses.filter(e => {
    const d = new Date(e.date);
    return d.getMonth() === viewMonth && d.getFullYear() === viewYear;
  });
}

function fmt(n) { return '₪' + Math.round(n).toLocaleString('he-IL'); }

async function loadFromSheets() {
  showToast('טוען נתונים...', 'success');
  try {
    const res = await fetch(API);
    const json = await res.json();
    if (json.success) {
      expenses = json.data.map(e => ({
        id: e.id, date: e.date, who: e.who,
        amount: parseFloat(e.amount), category: e.category, desc: e.desc || '', type: e.type || 'משותפת'
      })).filter(e => e.date && !isNaN(e.amount));
      render();
    }
  } catch(err) { showToast('שגיאה בטעינה', 'error'); }
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

function showToast(msg, type) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast ' + type + ' show';
  setTimeout(() => t.classList.remove('show'), 2500);
}

function render() {
  renderSummary();
  renderList();
}

function renderSummary() {
  const list = getMonthExp();
  
  const sharedList = list.filter(e => !e.type || e.type === 'משותפת');
  const amitPersonalList = list.filter(e => e.type === 'אישית' && e.who === 'עמית');
  const elaPersonalList = list.filter(e => e.type === 'אישית' && e.who === 'אלה');
  
  const amitShared = sharedList.filter(e => e.who === 'עמית').reduce((s,e) => s+e.amount, 0);
  const elaShared = sharedList.filter(e => e.who === 'אלה').reduce((s,e) => s+e.amount, 0);
  const totalShared = amitShared + elaShared;
  const grand = list.reduce((s,e) => s+e.amount, 0);
  
  // 1. מעקב תקציב משותף
  const sharedStatusEl = document.getElementById('shared-budget-status');
  const sharedDiffEl = document.getElementById('shared-budget-diff');
  sharedStatusEl.textContent = `${fmt(totalShared)} / ${fmt(sharedBudget)}`;
  
  if (sharedBudget > 0) {
    const diff = sharedBudget - totalShared;
    if (diff < 0) {
      sharedStatusEl.classList.add('over-budget');
      sharedDiffEl.textContent = `חריגה מהתקציב المשותף: ${fmt(Math.abs(diff))}`;
      sharedDiffEl.classList.add('over-budget');
    } else {
      sharedStatusEl.classList.remove('over-budget');
      sharedDiffEl.textContent = `נשאר לתקציב المשותף: ${fmt(diff)}`;
      sharedDiffEl.classList.remove('over-budget');
    }
  } else {
    sharedDiffEl.textContent = 'לא הוגדר תקציב (ניתן להגדיר בהגדרות)';
  }

  // 2. חישוב החזרים לפי היעד של אלה
  const settlementEl = document.getElementById('settlement-text');
  if (elaTarget > 0) {
    const refund = elaShared - elaTarget;
    if (refund > 0) {
      settlementEl.innerHTML = `אלה שילמה <strong>${fmt(elaShared)}</strong> מתוך הוצאות משותפות (היעד: ${fmt(elaTarget)}).<br>👉 <strong>עמית צריך להחזיר לאלה: ${fmt(refund)}</strong>`;
    } else if (refund < 0) {
      settlementEl.innerHTML = `אלה שילמה <strong>${fmt(elaShared)}</strong> מתוך הוצאות משותפות (טרם הגיעה ליעד של ${fmt(elaTarget)}).<br>אלה יכולה לשלם עוד <strong>${fmt(Math.abs(refund))}</strong> עד שתגיע ליעד.`;
    } else {
      settlementEl.innerHTML = `אלה שילמה בדיוק <strong>${fmt(elaShared)}</strong> לפי היעד. אין צורך בהחזרים.`;
    }
  } else {
    settlementEl.textContent = 'לא הוגדר יעד הוצאה לאלה. ניתן להגדיר בלשונית הגדרות.';
  }

  document.getElementById('amit-shared-total').textContent = fmt(amitShared);
  document.getElementById('ela-shared-total').textContent = fmt(elaShared);
  document.getElementById('grand-total-summary').textContent = fmt(grand);

  function groupByCategory(expList) {
    const obj = {};
    expList.forEach(e => { obj[e.category] = (obj[e.category] || 0) + e.amount; });
    return obj;
  }

  drawPieChart('shared', 'sharedChart', 'container-sharedChart', 'פילוג הוצאות משותפות', groupByCategory(sharedList));
  drawPieChart('amit', 'amitChart', 'container-amitChart', 'הוצאות אישיות - עמית', groupByCategory(amitPersonalList));
  drawPieChart('ela', 'elaChart', 'container-elaChart', 'הוצאות אישיות - אלה', groupByCategory(elaPersonalList));
}

function drawPieChart(instanceName, canvasId, containerId, title, dataObj) {
  const container = document.getElementById(containerId);
  const labels = Object.keys(dataObj);
  const data = Object.values(dataObj);

  if (labels.length === 0) {
    container.style.display = 'none';
    return;
  }
  
  container.style.display = 'block';

  const ctx = document.getElementById(canvasId).getContext('2d');
  if (chartInstances[instanceName]) { chartInstances[instanceName].destroy(); }

  chartInstances[instanceName] = new Chart(ctx, {
    type: 'pie',
    data: {
      labels: labels,
      datasets: [{ data: data, backgroundColor: chartColors, borderWidth: 1 }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: { position: 'bottom', labels: { font: { family: 'inherit' } } },
        title: { display: true, text: title, font: { family: 'inherit', size: 14, weight: 'bold' } }
      }
    }
  });
}

function renderList() {
  const list = getMonthExp().slice().reverse();
  const el = document.getElementById('expense-list');
  if (!list.length) { el.innerHTML = '<div class="empty">אין הוצאות בחודש זה</div>'; return; }
  
  const dotClass = { 'עמית': 'dot-amit', 'אלה': 'dot-ela' };
  el.innerHTML = list.map(e => {
    const d = new Date(e.date);
    const dateStr = d.getDate() + '/' + (d.getMonth()+1);
    return `<div class="expense-item">
      <div style="display:flex;align-items:center;flex:1">
        <div class="exp-dot ${dotClass[e.who]||'dot-shared'}"></div>
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
</script>
</body>
</html>
