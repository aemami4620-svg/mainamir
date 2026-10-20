# <html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="امیر امامی">
    <meta name="theme-color" content="#0b1324">

    <title>سامانه جامع مدیریت پرونده‌ها و اوقات رسیدگی</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500;600;700;800&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Vazirmatn', sans-serif; -webkit-tap-highlight-color: transparent; }
        body { background-color: #f1f5f9; color: #1e293b; direction: rtl; padding-bottom: 40px; }

        :root {
            --navy-950: #060a14; --navy-900: #0b1324; --navy-800: #111c30;
            --gold-500: #c59a3f; --gold-600: #ab822e; --emerald-600: #059669; --rose-600: #e11d48;
        }

        .header { 
            background: var(--navy-900); color: white; padding: 14px 20px; 
            padding-top: max(14px, env(safe-area-inset-top));
            display: flex; justify-content: space-between; align-items: center; 
            border-bottom: 2px solid var(--gold-500); position: sticky; top: 0; z-index: 40; flex-wrap: wrap; gap: 10px;
        }
        .header h1 { font-size: 15px; font-weight: 700; display: flex; align-items: center; gap: 8px; }
        .btn { padding: 8px 12px; border-radius: 8px; border: none; cursor: pointer; font-size: 12px; font-weight: 600; display: inline-flex; align-items: center; gap: 6px; text-decoration: none; transition: 0.2s; }
        .btn-gold { background: var(--gold-500); color: var(--navy-950); }
        .btn-gold:hover { background: var(--gold-600); }
        .btn-navy { background: var(--navy-900); color: white; }
        .btn-navy:hover { background: var(--navy-800); }
        .btn-emerald { background: var(--emerald-600); color: white; }
        .btn-slate { background: #e2e8f0; color: #334155; }
        .btn-rose { background: #fee2e2; color: var(--rose-600); border: 1px solid #fecdd3; }

        .container { max-width: 1280px; margin: 16px auto; padding: 0 12px; }
        
        .grid-top { display: grid; grid-template-columns: 2fr 1fr; gap: 16px; margin-bottom: 20px; }
        @media(max-width: 850px) { 
            .grid-top { grid-template-columns: 1fr; }
            .header { padding: 12px; }
            .header-actions { width: 100%; display: grid !important; grid-template-columns: repeat(2, 1fr); gap: 6px !important; }
            .header-actions .btn { justify-content: center; font-size: 11px; padding: 8px 6px; }
        }

        .card { background: white; border-radius: 14px; border: 1px solid #e2e8f0; padding: 16px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
        .card-gold-bg { background: linear-gradient(135deg, var(--navy-900), var(--navy-800)); color: white; border: 1px solid #1e293b; display: flex; flex-direction: column; justify-content: space-between; }

        .form-control { width: 100%; padding: 10px 12px; border: 1px solid #cbd5e1; border-radius: 8px; font-size: 13px; background: #f8fafc; margin-top: 4px; }
        .form-control:focus { outline: none; border-color: var(--navy-900); background: white; }

        table { width: 100%; border-collapse: collapse; font-size: 12px; text-align: right; min-width: 650px; }
        th { background: #f8fafc; padding: 10px 12px; color: #64748b; font-weight: 600; border-bottom: 2px solid #e2e8f0; }
        td { padding: 12px; border-bottom: 1px solid #f1f5f9; vertical-align: top; }
        tr:hover td { background: #f8fafc; }

        .modal-overlay { position: fixed; inset: 0; background: rgba(11, 19, 36, 0.75); backdrop-filter: blur(4px); display: flex; align-items: center; justify-content: center; z-index: 50; padding: 12px; }
        .modal-content { background: white; border-radius: 16px; width: 100%; max-width: 650px; max-height: 90vh; overflow-y: auto; padding: 20px; box-shadow: 0 20px 25px -5px rgba(0,0,0,0.3); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <!-- صفحه ورود -->
    <div id="login-overlay" class="modal-overlay">
        <div class="modal-content" style="max-width: 390px; text-align: center;">
            <div style="font-size: 40px; margin-bottom: 8px;">⚖️</div>
            <h2 style="font-size: 17px; font-weight: 800; color: var(--navy-900);">ورود به سامانه مدیریت پرونده‌ها</h2>
            <form onsubmit="handleLogin(event)" style="text-align: right; margin-top: 14px;">
                <div id="login-err" class="hidden" style="background:#fee2e2; color:#991b1b; padding:8px; border-radius:8px; font-size:11px; margin-bottom:12px;">نام کاربری یا رمز عبور اشتباه است.</div>
                <div style="margin-bottom: 12px;"><label style="font-size: 12px; font-weight: 600;">نام کاربری:</label><input type="text" id="log-user" required value="admin" class="form-control"></div>
                <div style="margin-bottom: 18px;"><label style="font-size: 12px; font-weight: 600;">رمز عبور:</label><input type="password" id="log-pass" required value="Vakil@1403" class="form-control"></div>
                <button type="submit" class="btn btn-navy" style="width: 100%; justify-content: center; padding: 12px; font-size: 13px;">ورود به سامانه</button>
            </form>
        </div>
    </div>

    <!-- برنامه اصلی -->
    <div id="main-app" class="hidden">
        <header class="header">
            <div>
                <h1>⚖️ دفتر امیر امامی <span style="font-size: 10px; background: rgba(255,255,255,0.1); padding: 2px 6px; border-radius: 4px; color: var(--gold-500);" id="user-role-badge"> سرپرست</span></h1>
                <div style="font-size: 10px; color: #94a3b8; margin-top: 3px;" id="user-name-display">کاربر جاری: دکتر امامی</div>
            </div>
            <div class="header-actions" style="display: flex; gap: 8px; align-items: center; flex-wrap: wrap;">
                <button onclick="showAllCasesView()" class="btn btn-slate" style="background:#1e293b; color:white;">📁 همه پرونده‌ها</button>
                <button onclick="openNewCaseModal()" class="btn btn-gold">+ ثبت پرونده و جلسه</button>
                <a href="https://docs.google.com/spreadsheets/d/18ve0d68Yiqch9qbZkGq6OGbpsSr8K7hOi5evKhIuBME/edit" target="_blank" class="btn btn-emerald">📊 باز کردن شیت درایو</a>
                <button onclick="syncDataFromCloud()" class="btn btn-slate" style="background:#0284c7; color:white;">🔄 همگام‌سازی ابری</button>
                <button onclick="openSettingsModal()" class="btn btn-slate" style="background:#334155; color:white;">⚙️ تنظیمات</button>
            </div>
        </header>

        <div class="container">
            <div id="cloud-status" style="font-size: 12px; font-weight: 600; padding: 10px 14px; border-radius: 8px; margin-bottom: 14px; display: none;"></div>

            <div id="case-workspace-view">
                <div class="grid-top">
                    <div class="card">
                        <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #f1f5f9; padding-bottom: 10px; margin-bottom: 12px; flex-wrap: wrap; gap: 8px;">
                            <span style="font-weight: 700; font-size: 13px;">📁 پرونده فعال:</span>
                            <select id="case-select" onchange="switchCase(this.value)" class="form-control" style="max-width: 260px; margin:0;"></select>
                        </div>
                        <div id="case-details-box" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 8px; font-size: 11px;"></div>
                        <div id="case-hearing-card"></div>
                    </div>

                    <div class="card card-gold-bg">
                        <div>
                            <div style="font-size: 11px; color: var(--gold-500); font-weight: 700;">📑 گزارش رسمی موکل</div>
                            <h3 style="font-size: 14px; margin: 6px 0;">پیش‌نویس مستند اقدامات و دادرسی</h3>
                            <p style="font-size: 11px; color: #cbd5e1; line-height: 1.6;">استخراج سوابق دادرسی همراه با جزئیات اصحاب دعوا و وضعیت دادگاه.</p>
                        </div>
                        <button onclick="openModal('report-filter-modal')" class="btn btn-gold" style="width: 100%; justify-content: center; margin-top: 14px; padding: 10px;">ایجاد پیش‌نویس گزارش</button>
                    </div>
                </div>

                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; flex-wrap: wrap; gap: 10px;">
                        <div>
                            <h2 style="font-size: 14px; font-weight: 700;">📋 سوابق اقدامات و تصمیمات</h2>
                            <span id="act-count" style="font-size: 11px; color: #64748b;">۰ اقدام</span>
                        </div>
                        <div style="display: flex; gap: 8px; flex-wrap: wrap; width: 100%; max-width: 520px; justify-content: flex-end;">
                            <input type="text" id="search-input" oninput="renderTable()" placeholder="جست‌وجو..." class="form-control" style="flex: 1; min-width: 120px; margin:0;">
                            <select id="filter-doc" onchange="renderTable()" class="form-control" style="width: 130px; margin:0;">
                                <option value="all">همه اقدامات</option>
                                <option value="doc">دارای سند رسمی</option>
                                <option value="nodoc">فاقد مدرک</option>
                            </select>
                            <button onclick="openNewActionModal()" class="btn btn-navy">+ ثبت اقدام</button>
                        </div>
                    </div>
                    <div style="overflow-x: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>تاریخ شمسی</th>
                                    <th>شرح اقدام حقوقی</th>
                                    <th>نتیجه حاصله</th>
                                    <th>مدرک استنادی</th>
                                    <th>اقدام بعدی</th>
                                    <th>مسئول</th>
                                    <th style="text-align: center;">عملیات</th>
                                </tr>
                            </thead>
                            <tbody id="actions-tbody"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <div id="all-cases-view" class="card hidden">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px;">
                    <h2 style="font-size: 14px; font-weight: 700;">📁 فهرست کلی پرونده‌ها</h2>
                    <button onclick="showCaseWorkspaceView()" class="btn btn-slate">بازگشت به میزکار</button>
                </div>
                <div style="overflow-x: auto;">
                    <table>
                        <thead>
                            <tr><th>شماره پرونده / بایگانی</th><th>موکل (سمت)</th><th>طرف مقابل (سمت)</th><th>موضوع</th><th>مرجع</th><th>جلسه 🔔</th><th>عملیات</th></tr>
                        </thead>
                        <tbody id="all-cases-tbody"></tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- مودال تنظیمات -->
    <div id="settings-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 440px;">
            <h3 style="font-size: 14px; font-weight: 700; margin-bottom: 14px;">⚙️ تنظیمات حساب کاربری</h3>
            <form onsubmit="saveUserProfile(event)">
                <div style="margin-bottom: 10px;"><label style="font-size: 11px; font-weight: 600;">نام و نام خانوادگی:</label><input type="text" id="set-fullname" required class="form-control"></div>
                <div style="display: flex; gap: 8px; margin-bottom: 10px;">
                    <div style="flex: 1;"><label style="font-size: 11px; font-weight: 600;">نام کاربری:</label><input type="text" id="set-username" required class="form-control"></div>
                    <div style="flex: 1;"><label style="font-size: 11px; font-weight: 600;">رمز عبور:</label><input type="password" id="set-password" required class="form-control"></div>
                </div>
                <div style="margin-bottom: 16px;">
                    <label style="font-size: 11px; font-weight: 600;">سمت سازمانی:</label>
                    <select id="set-role" class="form-control">
                        <option value="وکیل سرپرست">وکیل سرپرست</option>
                        <option value="وکیل همکار">وکیل همکار</option>
                        <option value="کارآموز وکالت">کارآموز وکالت</option>
                    </select>
                </div>
                <div style="display: flex; justify-content: space-between; align-items: center;">
                    <button type="button" onclick="handleLogout()" class="btn btn-rose">خروج</button>
                    <div style="display: flex; gap: 8px;">
                        <button type="button" onclick="closeModal('settings-modal')" class="btn btn-slate">انصراف</button>
                        <button type="submit" class="btn btn-navy">ذخیره</button>
                    </div>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال ثبت و ویرایش پرونده -->
    <div id="new-case-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 540px;">
            <h3 id="case-modal-title" style="font-size: 14px; font-weight: 700; margin-bottom: 12px;">ثبت پرونده و وقت جلسه</h3>
            <form onsubmit="saveCase(event)">
                <input type="hidden" id="c-edit-mode" value="new">
                
                <div style="display:flex; gap:8px; margin-bottom:8px;">
                    <div style="flex:1;"><label style="font-size: 11px;">شماره پرونده:</label><input id="c-id" required class="form-control"></div>
                    <div style="flex:1;"><label style="font-size: 11px;">شماره بایگانی:</label><input id="c-archive" placeholder="بایگانی شعبه..." class="form-control"></div>
                </div>

                <div style="display:flex; gap:8px; margin-bottom:8px;">
                    <div style="flex:2;"><label style="font-size: 11px;">نام موکل:</label><input id="c-client" required class="form-control"></div>
                    <div style="flex:1;"><label style="font-size: 11px;">سمت موکل:</label>
                        <select id="c-client-role" class="form-control">
                            <option value="خواهان">خواهان</option><option value="خوانده">خوانده</option><option value="شاکی">شاکی</option><option value="مشتکی‌عنه">مشتکی‌عنه</option><option value="تجدیدنظرخواه">تجدیدنظرخواه</option><option value="تجدیدنظرخوانده">تجدیدنظرخوانده</option><option value="متهم">متهم</option><option value="شخص ثالث">شخص ثالث</option>
                        </select>
                    </div>
                </div>

                <div style="display:flex; gap:8px; margin-bottom:8px;">
                    <div style="flex:2;"><label style="font-size: 11px;">طرف مقابل پرونده:</label><input id="c-opponent" class="form-control"></div>
                    <div style="flex:1;"><label style="font-size: 11px;">سمت طرف مقابل:</label>
                        <select id="c-opponent-role" class="form-control">
                            <option value="خوانده">خوانده</option><option value="خواهان">خواهان</option><option value="مشتکی‌عنه">مشتکی‌عنه</option><option value="شاکی">شاکی</option><option value="تجدیدنظرخوانده">تجدیدنظرخوانده</option><option value="تجدیدنظرخواه">تجدیدنظرخواه</option><option value="متهم">متهم</option><option value="شخص ثالث">شخص ثالث</option>
                        </select>
                    </div>
                </div>

                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">موضوع دعوا:</label><input id="c-subject" required class="form-control"></div>
                
                <div style="display:flex; gap:8px; margin-bottom:8px;">
                    <div style="flex:1;"><label style="font-size: 11px;">مرجع رسیدگی:</label><input id="c-court" required class="form-control"></div>
                    <div style="flex:1;"><label style="font-size: 11px;">شعبه:</label><input id="c-branch" required class="form-control"></div>
                </div>

                <div style="display:flex; gap:8px; margin-bottom:8px;">
                    <div style="flex:2;"><label style="font-size: 11px;">تاریخ جلسه (شمسی):</label><input id="c-hearing-date" placeholder="۱۴۰۵/۰۷/۲۹" class="form-control"></div>
                    <div style="flex:1;"><label style="font-size: 11px;">ساعت:</label><input id="c-hearing-time" placeholder="۰۹:۳۰" class="form-control"></div>
                </div>

                <div style="margin-bottom: 14px;"><label style="font-size: 11px;">وضعیت پرونده:</label>
                    <select id="c-status" class="form-control">
                        <option>در جریان رسیدگی</option><option>تجدیدنظرخواهی</option><option>اجرای احکام</option><option>مختومه</option>
                    </select>
                </div>

                <div style="display:flex; justify-content:flex-end; gap:8px;">
                    <button type="button" onclick="closeModal('new-case-modal')" class="btn btn-slate">انصراف</button>
                    <button type="submit" class="btn btn-navy">ذخیره اطلاعات</button>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال ثبت اقدام -->
    <div id="action-modal" class="modal-overlay hidden">
        <div class="modal-content">
            <h3 style="font-size: 14px; font-weight: 700; margin-bottom: 12px;">ثبت اقدام حقوقی</h3>
            <form onsubmit="saveAction(event)">
                <div style="display:flex; gap:8px; margin-bottom:8px;">
                    <div style="flex:1;"><label style="font-size: 11px;">تاریخ:</label><input id="act-date" required class="form-control"></div>
                    <div style="flex:1;"><label style="font-size: 11px;">مسئول:</label><input id="act-assignee" required class="form-control"></div>
                </div>
                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">شرح اقدام:</label><textarea id="act-desc" required rows="3" class="form-control"></textarea></div>
                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">نتیجه:</label><input id="act-result" class="form-control"></div>
                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">مدرک استنادی:</label><input id="act-doc" class="form-control"></div>
                <div style="display:flex; justify-content:flex-end; gap:8px;">
                    <button type="button" onclick="closeModal('action-modal')" class="btn btn-slate">انصراف</button>
                    <button type="submit" class="btn btn-navy">ثبت اقدام</button>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال گزارش -->
    <div id="report-filter-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 420px;">
            <h3 style="font-size: 14px; font-weight: 700; margin-bottom: 12px;">تنظیم بازه گزارش</h3>
            <div style="margin-bottom: 8px;"><label style="font-size: 11px;">از تاریخ:</label><input id="rep-from" value="۱۴۰۳/۰۱/۰۱" class="form-control"></div>
            <div style="margin-bottom: 14px;"><label style="font-size: 11px;">تا تاریخ:</label><input id="rep-to" value="۱۴۰۵/۱۲/۲۹" class="form-control"></div>
            <div style="display:flex; justify-content:flex-end; gap:8px;">
                <button onclick="closeModal('report-filter-modal')" class="btn btn-slate">انصراف</button>
                <button onclick="buildReport()" class="btn btn-gold">مشاهده پیش‌نویس</button>
            </div>
        </div>
    </div>

    <div id="report-preview-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 820px; max-height: 95vh;">
            <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #e2e8f0; padding-bottom: 10px; margin-bottom: 14px;">
                <span style="font-weight: 700; font-size: 13px;">🔍 پیش‌نمایش گزارش</span>
                <div style="display: flex; gap: 8px;">
                    <button onclick="window.print()" class="btn btn-gold">🖨️ چاپ / PDF</button>
                    <button onclick="closeModal('report-preview-modal')" class="btn btn-slate">بستن</button>
                </div>
            </div>
            <div id="report-print-container"></div>
        </div>
    </div>

    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbySwwahh0582QM1-DNdONQXMBnUTd_8VHhA8Jw1H7CQ5y9JpLMZOQW0A2ICLRsPfrH8/exec";
        
        let currentUser = JSON.parse(localStorage.getItem('law_user')) || { u: 'admin', p: 'Vakil@1403', name: 'دکتر امامی', role: 'وکیل سرپرست' };
        let cases = [];
        let actions = [];
        let curCaseId = '';

        function persistLocal() {
            localStorage.setItem('law_cases', JSON.stringify(cases));
            localStorage.setItem('law_actions', JSON.stringify(actions));
        }

        async function syncDataFromCloud() {
            setStatus('در حال بارگیری از گوگل درایو... ⏳');
            try {
                const res = await fetch(SCRIPT_URL + "?action=read");
                const data = await res.json();
                if (data.cases) {
                    cases = data.cases;
                    actions = data.actions || [];
                    if (cases.length > 0 && !curCaseId) curCaseId = cases[0].id;
                    persistLocal();
                    initApp();
                    setStatus('همگام‌سازی ابری موفق بود ✔️');
                }
            } catch (err) {
                loadLocal();
            }
        }

        function loadLocal() {
            cases = JSON.parse(localStorage.getItem('law_cases')) || [];
            actions = JSON.parse(localStorage.getItem('law_actions')) || [];
            if (cases.length > 0 && !curCaseId) curCaseId = cases[0].id;
            initApp();
        }

        function setStatus(msg, isError = false) {
            const el = document.getElementById('cloud-status');
            if (!el) return;
            el.style.display = 'block';
            el.innerText = msg;
            el.style.background = isError ? '#fee2e2' : '#e0f2fe';
            el.style.color = isError ? '#991b1b' : '#0369a1';
            setTimeout(() => { el.style.display = 'none'; }, 4000);
        }

        function updateHeaderUser() {
            document.getElementById('user-name-display').textContent = `کاربر جاری: ${currentUser.name}`;
            document.getElementById('user-role-badge').textContent = currentUser.role;
        }

        function handleLogin(e) {
            e.preventDefault();
            const u = document.getElementById('log-user').value.trim();
            const p = document.getElementById('log-pass').value.trim();
            if (u === currentUser.u && p === currentUser.p) {
                document.getElementById('login-overlay').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                updateHeaderUser();
                syncDataFromCloud();
            } else {
                document.getElementById('login-err').classList.remove('hidden');
            }
        }

        function handleLogout() {
            closeModal('settings-modal');
            document.getElementById('main-app').classList.add('hidden');
            document.getElementById('login-overlay').classList.remove('hidden');
        }

        function openSettingsModal() {
            document.getElementById('set-fullname').value = currentUser.name;
            document.getElementById('set-username').value = currentUser.u;
            document.getElementById('set-password').value = currentUser.p;
            document.getElementById('set-role').value = currentUser.role;
            openModal('settings-modal');
        }

        function saveUserProfile(e) {
            e.preventDefault();
            currentUser.name = document.getElementById('set-fullname').value.trim();
            currentUser.u = document.getElementById('set-username').value.trim();
            currentUser.p = document.getElementById('set-password').value.trim();
            currentUser.role = document.getElementById('set-role').value;
            localStorage.setItem('law_user', JSON.stringify(currentUser));
            updateHeaderUser();
            closeModal('settings-modal');
            setStatus('تنظیمات ذخیره شد ✔️');
        }

        function initApp() {
            renderCaseSelect();
            renderCaseInfo();
            renderTable();
            updateHeaderUser();
        }

        function renderCaseSelect() {
            const sel = document.getElementById('case-select');
            if (!sel) return;
            sel.innerHTML = '';
            cases.forEach(c => {
                const opt = document.createElement('option');
                opt.value = c.id;
                opt.textContent = `${c.id} (${c.client})`;
                if (c.id === curCaseId) opt.selected = true;
                sel.appendChild(opt);
            });
        }

        function switchCase(id) {
            curCaseId = id;
            renderCaseInfo();
            renderTable();
        }

        function renderCaseInfo() {
            const c = cases.find(x => x.id === curCaseId);
            const box = document.getElementById('case-details-box');
            const hBox = document.getElementById('case-hearing-card');
            if (!c) { if(box) box.innerHTML = ''; if(hBox) hBox.innerHTML = ''; return; }
            
            box.innerHTML = `
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>شماره پرونده:</strong> ${c.id}</div>
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>شماره بایگانی:</strong> ${c.archive || '—'}</div>
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>موکل:</strong> ${c.client} (${c.clientRole || 'خواهان'})</div>
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>طرف مقابل:</strong> ${c.opponent || '—'} (${c.opponentRole || 'خوانده'})</div>
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>موضوع:</strong> ${c.subject}</div>
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>مرجع:</strong> ${c.court} (${c.branch})</div>
                <div style="background:#f8fafc; padding:8px; border-radius:6px; border:1px solid #e2e8f0;"><strong>وضعیت:</strong> ${c.status}</div>
            `;

            if (c.hearingDate) {
                hBox.innerHTML = `
                    <div style="background:#fffbeb; border:1px solid #fde68a; border-radius:8px; padding:10px 12px; margin-top:12px; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:8px;">
                        <div style="font-size:12px; color:#92400e;"><strong>🔔 جلسه دادگاه:</strong> ${c.hearingDate} | ساعت: <strong>${c.hearingTime || '—'}</strong></div>
                        <button onclick="editCurrentCaseModal()" class="btn btn-slate" style="font-size:11px; padding:6px 10px;">ویرایش پرونده</button>
                    </div>
                `;
            } else {
                hBox.innerHTML = `
                    <div style="background:#f8fafc; border:1px dashed #cbd5e1; border-radius:8px; padding:10px 12px; margin-top:12px; display:flex; justify-content:space-between; align-items:center;">
                        <span style="font-size:11px; color:#64748b;">وقت جلسه ثبت نشده است.</span>
                        <button onclick="editCurrentCaseModal()" class="btn btn-gold" style="font-size:11px; padding:5px 8px;">+ ثبت وقت</button>
                    </div>
                `;
            }
        }

        function renderTable() {
            const tbody = document.getElementById('actions-tbody');
            if (!tbody) return;
            let acts = actions.filter(a => a.caseId === curCaseId);
            document.getElementById('act-count').textContent = `${acts.length} اقدام ثبتی`;
            tbody.innerHTML = '';
            acts.forEach(a => {
                tbody.innerHTML += `
                    <tr>
                        <td style="white-space:nowrap; font-weight:600;">${a.date}</td>
                        <td>${a.desc}</td>
                        <td>${a.result || '—'}</td>
                        <td>${a.doc || '—'}</td>
                        <td>${a.next || '—'}</td>
                        <td>${a.assignee}</td>
                        <td style="text-align:center;"><button onclick="deleteAction('${a.id}')" class="btn btn-slate" style="padding:4px 8px; font-size:11px; color:var(--rose-600);">حذف</button></td>
                    </tr>
                `;
            });
        }

        function openModal(id) { document.getElementById(id).classList.remove('hidden'); }
        function closeModal(id) { document.getElementById(id).classList.add('hidden'); }
        
        function openNewCaseModal() {
            document.getElementById('c-edit-mode').value = 'new';
            document.getElementById('case-modal-title').textContent = 'ثبت پرونده جدید و وقت جلسه';
            document.getElementById('c-id').disabled = false; // امکان نوشتن شناسه جدید
            document.getElementById('c-id').value = '';
            document.getElementById('c-archive').value = '';
            document.getElementById('c-client').value = '';
            document.getElementById('c-client-role').value = 'خواهان';
            document.getElementById('c-opponent').value = '';
            document.getElementById('c-opponent-role').value = 'خوانده';
            document.getElementById('c-subject').value = '';
            document.getElementById('c-court').value = '';
            document.getElementById('c-branch').value = '';
            document.getElementById('c-hearing-date').value = '';
            document.getElementById('c-hearing-time').value = '';
            openModal('new-case-modal');
        }

        function editCurrentCaseModal() {
            const c = cases.find(x => x.id === curCaseId);
            if (!c) return;
            document.getElementById('c-edit-mode').value = c.id; // نگهداری شناسه قبلی برای تشخیص ویرایش
            document.getElementById('case-modal-title').textContent = 'ویرایش اطلاعات و شماره پرونده';
            document.getElementById('c-id').disabled = false; // باز کردن فیلد شناسه برای امکان ویرایش آن
            document.getElementById('c-id').value = c.id;
            document.getElementById('c-archive').value = c.archive || '';
            document.getElementById('c-client').value = c.client;
            document.getElementById('c-client-role').value = c.clientRole || 'خواهان';
            document.getElementById('c-opponent').value = c.opponent || '';
            document.getElementById('c-opponent-role').value = c.opponentRole || 'خوانده';
            document.getElementById('c-subject').value = c.subject;
            document.getElementById('c-court').value = c.court;
            document.getElementById('c-branch').value = c.branch;
            document.getElementById('c-hearing-date').value = c.hearingDate || '';
            document.getElementById('c-hearing-time').value = c.hearingTime || '';
            document.getElementById('c-status').value = c.status;
            openModal('new-case-modal');
        }

        function openNewActionModal() { 
            document.getElementById('act-date').value = '';
            document.getElementById('act-assignee').value = currentUser.name;
            document.getElementById('act-desc').value = '';
            document.getElementById('act-result').value = '';
            document.getElementById('act-doc').value = '';
            openModal('action-modal'); 
        }

        async function saveCase(e) {
            e.preventDefault();
            const editMode = document.getElementById('c-edit-mode').value;
            const newId = document.getElementById('c-id').value.trim();
            
            const caseData = {
                id: newId,
                oldId: editMode !== 'new' ? editMode : null,
                archive: document.getElementById('c-archive').value.trim(),
                client: document.getElementById('c-client').value.trim(),
                clientRole: document.getElementById('c-client-role').value,
                opponent: document.getElementById('c-opponent').value.trim(),
                opponentRole: document.getElementById('c-opponent-role').value,
                subject: document.getElementById('c-subject').value.trim(),
                court: document.getElementById('c-court').value.trim(),
                branch: document.getElementById('c-branch').value.trim(),
                hearingDate: document.getElementById('c-hearing-date').value.trim(),
                hearingTime: document.getElementById('c-hearing-time').value.trim(),
                status: document.getElementById('c-status').value,
                createdAt: new Date().toLocaleDateString('fa-IR')
            };

            if (editMode === 'new') {
                cases.unshift(caseData);
                curCaseId = newId;
            } else {
                const idx = cases.findIndex(x => x.id === editMode);
                if (idx !== -1) {
                    cases[idx] = caseData;
                }
                // اگر شناسه پرونده تغییر کرده باشد، اقدامات مرتبط با آن هم آپدیت می‌شوند
                actions.forEach(a => { if (a.caseId === editMode) a.caseId = newId; });
                curCaseId = newId;
            }

            persistLocal();
            initApp();
            closeModal('new-case-modal');
            
            await fetch(SCRIPT_URL, {
                method: 'POST', mode: 'no-cors',
                headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                body: JSON.stringify({ type: "SAVE_CASE", data: caseData })
            });
            setStatus('اطلاعات پرونده در گوگل‌شیت ذخیره شد ✔️');
        }

        async function saveAction(e) {
            e.preventDefault();
            const actionObj = {
                id: 'act-' + Date.now(),
                caseId: curCaseId,
                date: document.getElementById('act-date').value.trim(),
                assignee: document.getElementById('act-assignee').value.trim(),
                desc: document.getElementById('act-desc').value.trim(),
                result: document.getElementById('act-result').value.trim(),
                doc: document.getElementById('act-doc').value.trim() || 'سند ضمیمه',
                isDoc: true, next: '', deadline: ''
            };
            actions.unshift(actionObj);
            persistLocal();
            renderTable();
            closeModal('action-modal');

            await fetch(SCRIPT_URL, {
                method: 'POST', mode: 'no-cors',
                headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                body: JSON.stringify({ type: "SAVE_ACTION", data: actionObj })
            });
            setStatus('اقدام در گوگل‌شیت ثبت شد ✔️');
        }

        function deleteAction(id) {
            if (confirm('حذف این اقدام؟')) {
                actions = actions.filter(x => x.id !== id);
                persistLocal();
                renderTable();
            }
        }

        function showAllCasesView() {
            document.getElementById('case-workspace-view').classList.add('hidden');
            document.getElementById('all-cases-view').classList.remove('hidden');
            const tbody = document.getElementById('all-cases-tbody');
            tbody.innerHTML = '';
            cases.forEach(c => {
                tbody.innerHTML += `
                    <tr>
                        <td><b>${c.id}</b><br><span style="font-size:10px; color:#64748b;">بایگانی: ${c.archive || '—'}</span></td>
                        <td>${c.client} <span style="font-size:10px; background:#e0f2fe; padding:2px 4px; border-radius:4px;">${c.clientRole || ''}</span></td>
                        <td>${c.opponent || '—'} <span style="font-size:10px; background:#fee2e2; padding:2px 4px; border-radius:4px;">${c.opponentRole || ''}</span></td>
                        <td>${c.subject}</td>
                        <td>${c.court} (${c.branch})</td>
                        <td>${c.hearingDate || '—'}</td>
                        <td><button onclick="showCaseWorkspaceView('${c.id}')" class="btn btn-gold" style="padding:4px 8px; font-size:11px;">انتخاب</button></td>
                    </tr>
                `;
            });
        }

        function showCaseWorkspaceView(id) {
            if(id) curCaseId = id;
            document.getElementById('all-cases-view').classList.add('hidden');
            document.getElementById('case-workspace-view').classList.remove('hidden');
            initApp();
        }

        function buildReport() {
            const c = cases.find(x => x.id === curCaseId);
            if (!c) return;
            let acts = actions.filter(a => a.caseId === curCaseId);
            let rows = '';
            acts.forEach((a, i) => {
                rows += `<tr style="border-bottom:1px solid #e2e8f0;"><td style="padding:8px;">${i+1}</td><td style="padding:8px;">${a.date}</td><td style="padding:8px;">${a.desc}</td><td style="padding:8px;">${a.result || '—'}</td><td style="padding:8px;">${a.doc}</td></tr>`;
            });
            document.getElementById('report-print-container').innerHTML = `
                <div style="border-bottom:2px solid #0b1324; padding-bottom:10px; margin-bottom:14px;">
                    <h3>گزارش رسمی پرونده: ${c.client} (${c.clientRole}) مقابل ${c.opponent || '—'} (${c.opponentRole})</h3>
                    <div style="font-size:12px; color:#475569; margin-top:4px;">شماره پرونده: ${c.id} | شماره بایگانی: ${c.archive || '—'} | موضوع: ${c.subject}</div>
                </div>
                <table style="width:100%; border-collapse:collapse;">
                    <thead><tr style="background:#f8fafc;"><th>ردیف</th><th>تاریخ</th><th>شرح اقدام</th><th>نتیجه</th><th>مدرک</th></tr></thead>
                    <tbody>${rows}</tbody>
                </table>
            `;
            closeModal('report-filter-modal');
            openModal('report-preview-modal');
        }
    </script>
</body>
</html>
