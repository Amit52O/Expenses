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
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: #f5f5f5; color: #1a1a1a; direction: rtl; }
  .app { max-width: 430px; margin: 0 auto; padding: 1rem; min-height: 100vh; }
  .header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 1.5rem; padding-top: 0.5rem; }
  .header h1 { font-size: 22px; font-weight: 600; }
  .header span { font-size: 13px; color: #888; }
  .tabs { display: flex; gap: 8px; margin-bottom: 1.5rem; }
  .tab { flex: 1; padding: 9px 4px; border: 1px solid #ddd; border-radius: 10px; background: white; font-size: 14px; cursor: pointer; color: #666; font-family: inherit; transition: all 0.15s; }
  .tab.active { background: #1a1a1a; color: white; border-color: #1a1a1a; font-weight: 500; }
  .section { display: none; }
  .section.active { display: block; }
  .card { background: white; border: 1px solid #eee; border-radius: 16px; padding: 1.25rem; margin-bottom: 1rem; }
  .field { margin-bottom: 1rem; }
  .field:last-child { margin-bottom: 0; }
  .field label { display: block; font-size: 13px; color: #666; margin-bottom: 6px; font-weight: 500; }
  .field input, .field select { width: 100%; padding: 10px 12px; border: 1px solid #ddd; border-radius: 10px; font-size: 16px; background: white; color: #1a1a1a; font-family: inherit; outline: none; }
  .field input:focus, .field select:focus { border-color: #1a1a1a; }
  .who-btns { display: flex; gap: 8px; }
  .who-btn { flex: 1; padding: 11px; border: 1px solid #ddd; border-radius: 10px; background: white; font-size: 16px; cursor: pointer; color: #666; font-family: inherit; transition: all 0.15s; font-weight: 500; }
  .who-btn.amit.active { background: #EBF4FF; border-color: #2563EB; color: #1D4ED8; }
  .who-btn.ela.active { background: #FDF2F8; border-color: #9D174D; color: #831843; }
  .add-btn { width: 100%; padding: 14px; border: none; border-radius: 12px; background: #1a1a1a; color: white; font-size: 16px; font-weight: 600; cursor: pointer; font-family: inherit; margin-top: 0.5rem; transition: opacity 0.15s; }
  .add-btn:active { opacity: 0.8; }
  .add-btn:disabled { opacity: 0.5; cursor: not-allowed; }
  .summary-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 10px; }
  .metric { background: white; border: 1px solid #eee; border-radius: 14px; padding: 1rem; }
  .metric-label { font-size: 12px; color: #888; margin-bottom: 4px; font-weight: 500; }
  .metric-value { font-size: 22px; font-weight: 600; color: #1a1a1a; }
  .metric-sub { font-size: 12px; margin-top: 3px; }
  .positive { color: #059669; }
  .negative { color: #DC2626; }
  .settle-card { background: white; border: 1px solid #eee; border-radius: 14px; padding: 1rem 1.25rem; margin-bottom: 10px; }
  .settle-label { font-size: 12px; color: #888; font-weight: 500; margin-bottom: 4px; }
  .settle-amount { font-size: 20px; font-weight: 600; }
  .month-nav { display: flex; align-items: center; justify-content: center; gap: 12px; margin-bottom: 1rem; }
  .month-btn { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 5px 14px; cursor: pointer; color: #666; font-size: 18px; line-height: 1; font-family: inherit; }
  .month-label { font-size: 16px; font-weight: 600; min-width: 110px; text-align: center; }
  .cat-list { display: flex; flex-direction: column; }
  .cat-row { display: flex; justify-content: space-between; align-items: center; font-size: 14px; padding: 8px 0; border-bottom: 1px solid #f0f0f0; }
  .cat-row:last-child { border-bottom: none; }
  .cat-name { color: #444; }
  .cat-amount { font-weight: 600; color: #1a1a1a; }
  .expense-list { display: flex; flex-direction: column; gap: 8px; }
  .expense-item { background: white; border: 1px solid #eee; border-radius: 12px; padding: 12px 14px; display: flex; align-items: center; justify-content: space-between; }
  .exp-right { display: flex; align-items: center; gap: 10px; }
  .exp-dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; }
  .dot-amit { background: #2563EB; }
  .dot-ela { background: #9D174D; }
  .exp-desc { font-size: 15px; color: #1a1a1a; font-weight: 500; }
  .exp-meta { font-size: 12px; color: #888; margin-top: 2px; }
  .exp-left { display: flex; align-items: center; gap: 8px; }
  .exp-amount { font-size: 15px; font-weight: 600; color: #1a1a1a; }
  .del-btn { background: none; border: none; color: #ccc; cursor: pointer; font-size: 16px; padding: 2px 4px; line-height: 1; }
  .del-btn:hover { color: #DC2626; }
  .empty { text-align: center; padding: 3rem 1rem; color: #aaa; font-size: 15px; }
  .toast { position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%); color: white; padding: 11px 22px; border-radius: 12px; font-size: 15px; font-weight: 500; opacity: 0; pointer-events: none; transition: opacity 0.3s; z-index: 999; white-space: nowrap; }
  .toast.success { background: #059669; }
  .toast.error { background: #DC2626; }
  .toast.show { opacity: 1; }
  .section-title { font-size: 14px; font-weight: 600; color: #444; margin-bottom: 10px; }
  .sync-row { display: flex; align-items: center; justify-content: center; gap: 8px; margin-bottom: 1rem; }
  .sync-btn { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 6px 14px; cursor: pointer; color: #666; font-size: 13px; font-family: inherit; }
  .sync-status { font-size: 12px; color: #aaa; }
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <h1>מעקב הוצאות</h1>
    <span id="header-month"></span>
  </div>

  <div class="tabs">
    <button class="tab active" onclick="showTab('add', this)">הוסף</button>
    <button class="tab" onclick="showTab('summary', this)">סיכום</button>
    <button class="tab" onclick="showTab('list', this)">רשימה</button>
  </div>

  <div id="tab-add" class="section active">
    <div class="card">
      <div class="field">
        <label>מי שילם?</label>
        <div class="who-btns">
          <button class="who-btn amit active" onclick="selectWho('עמית', this)">עמית</button>
          <button class="who-btn ela" onclick="selectWho('אלה', this)">אלה</button>
        </div>
      </div>
      <div class="field">
        <label>סכום (₪)</label>
        <input type="number" id="amount" placeholder="0" min="0" step="0.01" inputmode="decimal">
      </div>
      <div class="field">
        <label>קטגוריה</label>
        <select id="category">
          <option value="דיור">דיור</option>
          <option value="סופר">סופר</option>
          <option value="ריהוט">ריהוט</option>
          <option value="פנאי">פנאי</option>
          <option value="סטרימינג ואינטרנט">סטרימינג ואינטרנט</option>
          <option value="חשבונות">חשבונות</option>
          <option value="תחבורה">תחבורה</option>
          <option value="מתנות ואירועים">מתנות ואירועים</option>
          <option value="חופשות ונופש">חופשות ונופש</option>
          <option value="שונות">שונות</option>
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

  <div id="tab-summary" class="section">
    <div class="month-nav">
      <button class="month-btn" onclick="changeMonth(-1)">&#8249;</button>
      <span class="month-label" id="summary-month"></span>
      <button class="month-btn" onclick="changeMonth(1)">&#8250;</button>
    </div>
    <div class="sync-row">
      <button class="sync-btn" onclick="loadFromSheets()">רענן נתונים</button>
      <span class="sync-status" id="sync-status"></span>
    </div>
    <div class="summary-grid">
      <div class="metric">
        <div class="metric-label">עמית שילם</div>
        <div class="metric-value" id="amit-total">₪0</div>
      </div>
      <div class="metric">
        <div class="metric-label">אלה שילמה</div>
        <div class="metric-value" id="ela-total">₪0</div>
      </div>
    </div>
    <div class="summary-grid">
      <div class="metric">
        <div class="metric-label">סה"כ החודש</div>
        <div class="metric-value" id="grand-total">₪0</div>
      </div>
      <div class="metric">
        <div class="metric-label">יעד אלה</div>
        <div class="metric-value">₪3,000</div>
        <div class="metric-sub" id="ela-target-sub"></div>
      </div>
    </div>
    <div class="settle-card">
      <div class="settle-label">הסדר חשבון</div>
      <div class="settle-amount" id="settle-text">טוען...</div>
    </div>
    <div class="card">
      <div class="section-title">פירוט לפי קטגוריה</div>
      <div class="cat-list" id="cat-list"></div>
    </div>
  </div>

  <div id="tab-list" class="section">
    <div class="month-nav">
      <button class="month-btn" onclick="changeMonth(-1)">&#8249;</button>
      <span class="month-label" id="list-month"></span>
      <button class="month-btn" onclick="changeMonth(1)">&#8250;</button>
    </div>
    <div class="sync-row">
      <button class="sync-btn" onclick="loadFromSheets()">רענן נתונים</button>
      <span class="sync-status" id="sync-status2"></span>
    </div>
    <div class="expense-list" id="expense-list"></div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const API = 'https://script.google.com/macros/s/AKfycbwLRDfOwDvrf3AD2Ub3_v22sBOeu9OeUBe3CToEuFGYA-s4PxzKRCApYcUV1c3kJfaJAQ/exec';
const MONTHS = ['ינואר','פברואר','מרץ','אפריל','מאי','יוני','יולי','אוגוסט','ספטמבר','אוקטובר','נובמבר','דצמבר'];
const ELA_TARGET = 3000;

let who = 'עמית';
let now = new Date();
let viewMonth = now.getMonth();
let viewYear = now.getFullYear();
let expenses = [];

function init() {
  document.getElementById('date').value = now.toISOString().split('T')[0];
  document.getElementById('header-month').textContent = MONTHS[now.getMonth()] + ' ' + now.getFullYear();
  updateLabels();
  loadFromSheets();
}

function showTab(name, btn) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
  btn.classList.add('active');
  render();
}

function selectWho(name, btn) {
  who = name;
  document.querySelectorAll('.who-btn').forEach(b => b.classList.remove('active'));
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
  document.getElementById('summary-month').textContent = label;
  document.getElementById('list-month').textContent = label;
}

function getMonthExp() {
  return expenses.filter(e => {
    const d = new Date(e.date);
    return d.getMonth() === viewMonth && d.getFullYear() === viewYear;
  });
}

function fmt(n) {
  return '₪' + Math.round(n).toLocaleString('he-IL');
}

function setSyncStatus(msg) {
  ['sync-status','sync-status2'].forEach(id => {
    const el = document.getElementById(id);
    if (el) el.textContent = msg;
  });
}

async function loadFromSheets() {
  setSyncStatus('טוען...');
  try {
    const res = await fetch(API);
    const json = await res.json();
    if (json.success) {
      expenses = json.data.map(e => ({
        id: e.id,
        date: e.date,
        who: e.who,
        amount: parseFloat(e.amount),
        category: e.category,
        desc: e.desc || ''
      })).filter(e => e.date && !isNaN(e.amount));
      setSyncStatus('עודכן ' + new Date().toLocaleTimeString('he-IL', {hour:'2-digit',minute:'2-digit'}));
      render();
    }
  } catch(err) {
    setSyncStatus('שגיאה בטעינה');
    showToast('שגיאה בטעינת הנתונים', 'error');
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
  btn.disabled = true;
  btn.textContent = 'שומר...';
  const expense = { id: Date.now(), who, amount, category, desc, date };
  try {
    await fetch(API, { method: 'POST', body: JSON.stringify({ action: 'add', ...expense }) });
    expenses.push(expense);
    document.getElementById('amount').value = '';
    document.getElementById('desc').value = '';
    showToast('ההוצאה נוספה ✓', 'success');
    render();
  } catch(err) {
    showToast('שגיאה בשמירה', 'error');
  }
  btn.disabled = false;
  btn.textContent = '+ הוסף הוצאה';
}

async function deleteExpense(id) {
  if (!confirm('למחוק את ההוצאה?')) return;
  try {
    await fetch(API, { method: 'POST', body: JSON.stringify({ action: 'delete', id }) });
    expenses = expenses.filter(e => String(e.id) !== String(id));
    render();
    showToast('ההוצאה נמחקה', 'success');
  } catch(err) {
    showToast('שגיאה במחיקה', 'error');
  }
}

function showToast(msg, type) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast ' + type + ' show';
  setTimeout(() => t.classList.remove('show'), 2500);
}

function render() {
  const list = getMonthExp();
  const amitTotal = list.filter(e => e.who === 'עמית').reduce((s,e) => s+e.amount, 0);
  const elaTotal = list.filter(e => e.who === 'אלה').reduce((s,e) => s+e.amount, 0);
  const grand = amitTotal + elaTotal;

  document.getElementById('amit-total').textContent = fmt(amitTotal);
  document.getElementById('ela-total').textContent = fmt(elaTotal);
  document.getElementById('grand-total').textContent = fmt(grand);

  const elaDiff = elaTotal - ELA_TARGET;
  const elaTargetSub = document.getElementById('ela-target-sub');
  if (grand === 0) { elaTargetSub.textContent = ''; }
  else if (elaDiff >= 0) { elaTargetSub.textContent = 'שילמה ' + fmt(elaDiff) + ' יותר'; elaTargetSub.className = 'metric-sub positive'; }
  else { elaTargetSub.textContent = 'נותרו ' + fmt(-elaDiff); elaTargetSub.className = 'metric-sub negative'; }

  const settleEl = document.getElementById('settle-text');
  if (grand === 0) { settleEl.textContent = 'אין הוצאות החודש'; settleEl.style.color = '#888'; }
  else {
    const amitOwed = grand - ELA_TARGET;
    const amitDiff = amitTotal - amitOwed;
    if (Math.abs(amitDiff) < 1) { settleEl.textContent = 'מיושב! אין מה להחזיר'; settleEl.style.color = '#059669'; }
    else if (amitDiff < 0) { settleEl.textContent = 'עמית חייב לאלה ' + fmt(-amitDiff); settleEl.style.color = '#DC2626'; }
    else { settleEl.textContent = 'אלה חייבת לעמית ' + fmt(amitDiff); settleEl.style.color = '#2563EB'; }
  }

  const cats = {};
  list.forEach(e => { cats[e.category] = (cats[e.category]||0) + e.amount; });
  const sorted = Object.entries(cats).sort((a,b) => b[1]-a[1]);
  document.getElementById('cat-list').innerHTML = sorted.length === 0
    ? '<div style="color:#aaa;font-size:14px;padding:8px 0">אין נתונים</div>'
    : sorted.map(([cat,amt]) => `<div class="cat-row"><span class="cat-name">${cat}</span><span class="cat-amount">${fmt(amt)}</span></div>`).join('');

  const reversed = list.slice().reverse();
  document.getElementById('expense-list').innerHTML = reversed.length === 0
    ? '<div class="empty">אין הוצאות בחודש זה</div>'
    : reversed.map(e => {
        const d = new Date(e.date);
        const dateStr = d.getDate() + '/' + (d.getMonth()+1);
        return `<div class="expense-item">
          <div class="exp-right">
            <div class="exp-dot ${e.who==='עמית'?'dot-amit':'dot-ela'}"></div>
            <div>
              <div class="exp-desc">${e.desc||e.category}</div>
              <div class="exp-meta">${e.who} · ${e.category} · ${dateStr}</div>
            </div>
          </div>
          <div class="exp-left">
            <span class="exp-amount">${fmt(e.amount)}</span>
            <button class="del-btn" onclick="deleteExpense(${e.id})">✕</button>
          </div>
        </div>`;
      }).join('');
}

init();
</script>
</body>
</html>
