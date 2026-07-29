<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ניהול הוצאות משותפות</title>
    <style>
        :root {
            --primary: #4f46e5;
            --primary-hover: #4338ca;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-secondary: #64748b;
            --border: #e2e8f0;
            --danger: #ef4444;
            --success: #10b981;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding-bottom: 80px;
        }

        header {
            background: var(--card-bg);
            padding: 1rem;
            text-align: center;
            border-bottom: 1px solid var(--border);
            font-size: 1.25rem;
            font-weight: bold;
            color: var(--primary);
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 1rem;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* Metrics Grid */
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 0.75rem;
            margin-bottom: 1rem;
        }

        .metric-card {
            background: var(--card-bg);
            padding: 1rem;
            border-radius: 12px;
            border: 1px solid var(--border);
            text-align: center;
        }

        .metric-card h3 {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-bottom: 0.25rem;
        }

        .metric-card .value {
            font-size: 1.25rem;
            font-weight: bold;
            color: var(--text-main);
        }

        /* Forms & Inputs */
        .card {
            background: var(--card-bg);
            padding: 1.25rem;
            border-radius: 12px;
            border: 1px solid var(--border);
            margin-bottom: 1rem;
        }

        .form-group {
            margin-bottom: 1rem;
        }

        label {
            display: block;
            font-size: 0.9rem;
            font-weight: 600;
            margin-bottom: 0.35rem;
        }

        input, select, textarea {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border);
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            background: #fff;
        }

        input:focus, select:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }

        .btn {
            width: 100%;
            padding: 0.75rem;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.2s;
        }

        .btn:hover {
            background: var(--primary-hover);
        }

        .btn-secondary {
            background: #e2e8f0;
            color: var(--text-main);
            margin-top: 0.5rem;
        }

        .btn-secondary:hover {
            background: #cbd5e1;
        }

        /* Expense List */
        .expense-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.75rem;
            border-bottom: 1px solid var(--border);
        }

        .expense-item:last-child {
            border-bottom: none;
        }

        .expense-info h4 {
            font-size: 1rem;
            margin-bottom: 0.1rem;
        }

        .expense-info p {
            font-size: 0.8rem;
            color: var(--text-secondary);
        }

        .expense-amount {
            font-weight: bold;
            font-size: 1rem;
        }

        .delete-btn {
            background: none;
            border: none;
            color: var(--danger);
            cursor: pointer;
            font-size: 1.1rem;
            padding: 0.25rem 0.5rem;
        }

        /* Navigation Bar */
        nav {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: var(--card-bg);
            border-top: 1px solid var(--border);
            display: flex;
            justify-content: space-around;
            padding: 0.5rem 0;
            z-index: 1000;
        }

        .nav-item {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 0.8rem;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.2rem;
        }

        .nav-item.active {
            color: var(--primary);
            font-weight: bold;
        }

        .nav-item span {
            font-size: 1.2rem;
        }

        /* Toast Notifications */
        #toast {
            position: fixed;
            top: 1rem;
            left: 50%;
            transform: translateX(-50%) translateY(-100px);
            background: var(--text-main);
            color: white;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            transition: transform 0.3s ease;
            z-index: 2000;
            font-size: 0.9rem;
        }

        #toast.show {
            transform: translateX(-50%) translateY(0);
        }
    </style>
</head>
<body>

    <header>ניהול הוצאות משותפות</header>

    <div id="toast">הודעה</div>

    <div class="container">
        <!-- Dashboard Tab -->
        <div id="tab-dashboard" class="tab-content active">
            <div class="metrics-grid">
                <div class="metric-card">
                    <h3>עמית שילם (משותף)</h3>
                    <div class="value" id="metric-amit-shared">₪0</div>
                </div>
                <div class="metric-card">
                    <h3>אלה שילמה (משותף)</h3>
                    <div class="value" id="metric-ela-shared">₪0</div>
                </div>
                <div class="metric-card">
                    <h3>הוצאות אישיות עמית</h3>
                    <div class="value" id="metric-amit-personal">₪0</div>
                </div>
                <div class="metric-card">
                    <h3>הוצאות אישיות אלה</h3>
                    <div class="value" id="metric-ela-personal">₪0</div>
                </div>
            </div>

            <div class="card">
                <h3 style="margin-bottom: 0.75rem;">סיכום התחשבנות</h3>
                <p id="settlement-text" style="font-size: 0.95rem; line-height: 1.5;">טוען נתונים...</p>
            </div>
        </div>

        <!-- Add Expense Tab -->
        <div id="tab-add" class="tab-content">
            <div class="card">
                <h3 style="margin-bottom: 1rem;">הוספת הוצאה חדשה</h3>
                <form id="expense-form" onsubmit="handleFormSubmit(event)">
                    <div class="form-group">
                        <label>מי שילם?</label>
                        <select id="who">
                            <option value="עמית">עמית</option>
                            <option value="אלה">אלה</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label>סכום (₪)</label>
                        <input type="number" id="amount" step="0.01" required placeholder="0.00">
                    </div>

                    <div class="form-group">
                        <label>קטגוריה</label>
                        <select id="category"></select>
                    </div>

                    <div class="form-group">
                        <label>סוג הוצאה</label>
                        <select id="type">
                            <option value="משותפת">משותפת (50/50)</option>
                            <option value="אישית">אישית</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label>תאריך</label>
                        <input type="date" id="date" required>
                    </div>

                    <div class="form-group">
                        <label>תיאור (אופציונלי)</label>
                        <input type="text" id="desc" placeholder="למשל: קניות בסופר">
                    </div>

                    <button type="submit" class="btn">שמור הוצאה</button>
                </form>
            </div>
        </div>

        <!-- List Tab -->
        <div id="tab-list" class="tab-content">
            <div class="card">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem;">
                    <h3>רשימת הוצאות</h3>
                    <button class="btn" style="width: auto; padding: 0.4rem 0.8rem; font-size: 0.85rem;" onclick="loadFromSheets()">רענן מהשרת</button>
                </div>
                <div id="expenses-list">
                    <p style="color: var(--text-secondary); text-align: center; padding: 1rem;">אין הוצאות להצגה.</p>
                </div>
            </div>
        </div>

        <!-- Settings / Categories Tab -->
        <div id="tab-settings" class="tab-content">
            <div class="card">
                <h3 style="margin-bottom: 1rem;">ניהול קטגוריות</h3>
                <div class="form-group">
                    <label>הוסף קטגוריה חדשה</label>
                    <div style="display: flex; gap: 0.5rem;">
                        <input type="text" id="new-category-input" placeholder="שם הקטגוריה...">
                        <button class="btn" style="width: auto; padding: 0 1rem;" onclick="addCategory()">הוסף</button>
                    </div>
                </div>
                <div id="categories-settings-list" style="margin-top: 1rem;"></div>
            </div>
        </div>
    </div>

    <!-- Navigation -->
    <nav>
        <button class="nav-item active" onclick="switchTab('dashboard', this)">
            <span>📊</span>סיכום
        </button>
        <button class="nav-item" onclick="switchTab('add', this)">
            <span>➕</span>הוספה
        </button>
        <button class="nav-item" onclick="switchTab('list', this)">
            <span>📋</span>רשימה
        </button>
        <button class="nav-item" onclick="switchTab('settings', this)">
            <span>⚙️</span>הגדרות
        </button>
    </nav>

    <script>
        // ==========================================
        
        const API = 'https://script.google.com/macros/s/AKfycbxhGbyXIDOfFMWk02oKgefVkA84QuxaqWoQ6fNrlZcpfWM8WL-DILpRM1qJZx8gN8Tnjg/exec';

        let expenses = [];
        let categories = ["דיור", "סופר", "ריהוט", "פנאי", "סטרימינג ואינטרנט", "חשבונות", "תחבורה", "מתנות ואירועים", "חופשות ונופש", "שונות"];

        document.getElementById('date').valueAsDate = new Date();

        function showToast(text, type = 'success') {
            const toast = document.getElementById('toast');
            toast.textContent = text;
            toast.style.background = type === 'error' ? 'var(--danger)' : 'var(--text-main)';
            toast.classList.add('show');
            setTimeout(() => toast.classList.remove('show'), 3000);
        }

        function switchTab(tabId, el) {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            
            document.getElementById('tab-' + tabId).classList.add('active');
            el.classList.add('active');
        }

        async function loadFromSheets() {
            if (API === 'PUT_YOUR_REAL_LINK_HERE') {
                showToast('שגיאה: חסר קישור לשרת', 'error');
                return;
            }
            showToast('טוען נתונים...', 'success');
            try {
                const res = await fetch(API);
                const json = await res.json();
                
                if (json.success) {
                    if (json.categories && json.categories.length > 0) {
                        categories = json.categories;
                    }
                    
                    if (json.data && Array.isArray(json.data)) {
                        expenses = json.data.map(e => ({
                            id: String(e.id || Date.now() + Math.random()), 
                            date: e.date ? String(e.date).split('T')[0] : new Date().toISOString().split('T')[0],
                            who: e.who || 'עמית',
                            amount: parseFloat(e.amount) || 0,
                            category: e.category || categories[0],
                            desc: e.desc || '',
                            type: e.type || 'משותפת'
                        })).filter(e => !isNaN(e.amount) && e.amount > 0);
                    } else {
                        expenses = [];
                    }
                    
                    populateCategoryDropdowns();
                    renderCategoriesSettings();
                    render();
                    showToast('הנתונים נטענו בהצלחה', 'success');
                } else {
                    showToast('שגיאה בשרת: ' + (json.error || 'לא ידוע'), 'error');
                }
            } catch(err) {
                console.error('שגיאת טעינה:', err);
                showToast('שגיאה בחיבור לשרת', 'error');
            }
        }

        async function sendToServer(action, payload) {
            if (API === 'PUT_YOUR_REAL_LINK_HERE') return;
            try {
                await fetch(API, {
                    method: 'POST',
                    mode: 'no-cors',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify({ action: action, ...payload })
                });
            } catch (err) {
                console.error('שגיאת שליחה לשרת:', err);
            }
        }

        function populateCategoryDropdowns() {
            const select = document.getElementById('category');
            select.innerHTML = '';
            categories.forEach(cat => {
                const opt = document.createElement('option');
                opt.value = cat;
                opt.textContent = cat;
                select.appendChild(opt);
            });
        }

        function renderCategoriesSettings() {
            const container = document.getElementById('categories-settings-list');
            container.innerHTML = '';
            categories.forEach((cat, index) => {
                const div = document.createElement('div');
                div.style.cssText = "display: flex; justify-content: space-between; align-items: center; padding: 0.5rem 0; border-bottom: 1px solid var(--border);";
                div.innerHTML = `<span>${cat}</span> <button class="delete-btn" onclick="removeCategory(${index})">🗑️</button>`;
                container.appendChild(div);
            });
        }

        async function addCategory() {
            const input = document.getElementById('new-category-input');
            const val = input.value.trim();
            if (val && !categories.includes(val)) {
                categories.push(val);
                input.value = '';
                populateCategoryDropdowns();
                renderCategoriesSettings();
                await sendToServer('saveCategories', { categories: categories });
                showToast('הקטגוריה נוספה בהצלחה');
            }
        }

        async function removeCategory(index) {
            if (categories.length <= 1) {
                showToast('חייבת להישאר לפחות קטגוריה אחת', 'error');
                return;
            }
            categories.splice(index, 1);
            populateCategoryDropdowns();
            renderCategoriesSettings();
            await sendToServer('saveCategories', { categories: categories });
            showToast('הקטגוריה נמחקה');
        }

        async function handleFormSubmit(e) {
            e.preventDefault();
            const expense = {
                id: 'exp_' + Date.now(),
                who: document.getElementById('who').value,
                amount: parseFloat(document.getElementById('amount').value),
                category: document.getElementById('category').value,
                type: document.getElementById('type').value,
                date: document.getElementById('date').value,
                desc: document.getElementById('desc').value
            };

            expenses.push(expense);
            render();
            
            document.getElementById('amount').value = '';
            document.getElementById('desc').value = '';
            switchTab('list', document.querySelectorAll('.nav-item')[2]);

            await sendToServer('add', expense);
            showToast('ההוצאה נוספה בהצלחה');
        }

        async function deleteExpense(id) {
            expenses = expenses.filter(e => e.id !== id);
            render();
            await sendToServer('delete', { id: id });
            showToast('ההוצאה נמחקה');
        }

        function render() {
            let amitShared = 0, elaShared = 0, amitPersonal = 0, elaPersonal = 0;
            const listEl = document.getElementById('expenses-list');
            listEl.innerHTML = '';

            if (expenses.length === 0) {
                listEl.innerHTML = '<p style="color: var(--text-secondary); text-align: center; padding: 1rem;">אין הוצאות להצגה.</p>';
            }

            // מיון לפי תאריך חדש ישן
            const sorted = [...expenses].sort((a, b) => new Date(b.date) - new Date(a.date));

            sorted.forEach(e => {
                if (e.type === 'משותפת') {
                    if (e.who === 'עמית') amitShared += e.amount;
                    else elaShared += e.amount;
                } else {
                    if (e.who === 'עמית') amitPersonal += e.amount;
                    else elaPersonal += e.amount;
                }

                const item = document.createElement('div');
                item.className = 'expense-item';
                item.innerHTML = `
                    <div class="expense-info">
                        <h4>${e.category} (${e.who}) ${e.type === 'אישית' ? '- אישית' : ''}</h4>
                        <p>${e.date} ${e.desc ? '• ' + e.desc : ''}</p>
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <span class="expense-amount">₪${e.amount.toFixed(2)}</span>
                        <button class="delete-btn" onclick="deleteExpense('${e.id}')">🗑️</button>
                    </div>
                `;
                listEl.appendChild(item);
            });

            document.getElementById('metric-amit-shared').textContent = '₪' + amitShared.toFixed(2);
            document.getElementById('metric-ela-shared').textContent = '₪' + elaShared.toFixed(2);
            document.getElementById('metric-amit-personal').textContent = '₪' + amitPersonal.toFixed(2);
            document.getElementById('metric-ela-personal').textContent = '₪' + elaPersonal.toFixed(2);

            // חישוב התחשבנות
            const totalShared = amitShared + elaShared;
            const targetPerPerson = totalShared / 2;
            const settlementText = document.getElementById('settlement-text');

            if (totalShared === 0) {
                settlementText.textContent = 'אין עדיין הוצאות משותפות להתחשבנות.';
            } else {
                const diff = amitShared - targetPerPerson;
                if (Math.abs(diff) < 0.01) {
                    settlementText.textContent = 'ההוצאות המשותפות מאוזנות לחלוטין! אין הפרשים.';
                } else if (diff > 0) {
                    settlementText.textContent = `אלה צריכה להעביר לעמית ₪${diff.toFixed(2)} כדי לאזן את ההוצאות המשותפות.`;
                } else {
                    settlementText.textContent = `עמית צריך להעביר לאלה ₪${Math.abs(diff).toFixed(2)} כדי לאזן את ההוצאות המשותפות.`;
                }
            }
        }

        // טעינת נתונים ראשונית עם פתיחת העמוד
        window.onload = () => {
            populateCategoryDropdowns();
            renderCategoriesSettings();
            loadFromSheets();
        };
    </script>
</body>
</html>
