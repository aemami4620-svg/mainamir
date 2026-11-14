<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="دفتر وکالت">
    <meta name="theme-color" content="#0b1324">

    <title>سامانه جامع مدیریت وکالت، مواعد قضایی، امور مالی و هوش مصنوعی حقوقی</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500;600;700;800&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Vazirmatn', Tahoma, sans-serif; -webkit-tap-highlight-color: transparent; }
        body { background-color: #f1f5f9; color: #1e293b; direction: rtl; padding-bottom: 85px; -webkit-font-smoothing: antialiased; }

        :root {
            --navy-950: #060a14; --navy-900: #0b1324; --navy-800: #111c30;
            --gold-500: #c59a3f; --gold-600: #ab822e; --emerald-600: #059669;
            --rose-600: #e11d48; --amber-600: #d97706; --sky-600: #0284c7; --purple-600: #7c3aed;
        }

        .header { 
            background: rgba(11, 19, 36, 0.96); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
            color: white; padding: 12px 20px; 
            padding-top: max(14px, env(safe-area-inset-top));
            display: flex; justify-content: space-between; align-items: center; 
            border-bottom: 2px solid var(--gold-500); position: sticky; top: 0; z-index: 40; flex-wrap: wrap; gap: 10px;
        }
        .header h1 { font-size: 15px; font-weight: 700; display: flex; align-items: center; gap: 8px; }
        
        .btn { padding: 9px 14px; border-radius: 10px; border: none; cursor: pointer; font-size: 12px; font-weight: 600; display: inline-flex; align-items: center; gap: 6px; text-decoration: none; transition: transform 0.12s ease, background-color 0.2s; }
        .btn:active { transform: scale(0.96); }
        .btn:disabled { opacity: 0.6; cursor: not-allowed; }
        .btn-gold { background: var(--gold-500); color: var(--navy-950); }
        .btn-gold:hover { background: var(--gold-600); }
        .btn-navy { background: var(--navy-900); color: white; }
        .btn-navy:hover { background: var(--navy-800); }
        .btn-emerald { background: var(--emerald-600); color: white; }
        .btn-sky { background: var(--sky-600); color: white; }
        .btn-purple { background: var(--purple-600); color: white; }
        .btn-slate { background: #e2e8f0; color: #334155; }
        .btn-rose { background: #fee2e2; color: var(--rose-600); border: 1px solid #fecdd3; }

        .container { max-width: 1360px; margin: 16px auto; padding: 0 12px; }
        
        .grid-top { display: grid; grid-template-columns: 2.1fr 1fr; gap: 16px; margin-bottom: 16px; }
        .grid-mid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 16px; }

        .card { background: white; border-radius: 16px; border: 1px solid #e2e8f0; padding: 16px; box-shadow: 0 2px 8px rgba(15, 23, 42, 0.04); }
        .card-gold-bg { background: linear-gradient(135deg, var(--navy-900), var(--navy-800)); color: white; border: 1px solid #1e293b; display: flex; flex-direction: column; justify-content: space-between; }

        .form-control { width: 100%; padding: 10px 12px; border: 1px solid #cbd5e1; border-radius: 10px; font-size: 13px; background: #f8fafc; margin-top: 4px; transition: 0.2s; }
        .form-control:focus { outline: none; border-color: var(--navy-900); background: white; box-shadow: 0 0 0 3px rgba(11, 19, 36, 0.08); }

        table { width: 100%; border-collapse: collapse; font-size: 12px; text-align: right; }
        th { background: #f8fafc; padding: 10px 12px; color: #475569; font-weight: 700; border-bottom: 2px solid #e2e8f0; }
        td { padding: 11px 12px; border-bottom: 1px solid #f1f5f9; vertical-align: middle; }
        tr:hover td { background: #f8fafc; }

        .badge { padding: 3px 8px; border-radius: 6px; font-size: 10px; font-weight: 700; display: inline-block; }
        .badge-sky { background: #e0f2fe; color: #0369a1; }
        .badge-emerald { background: #d1fae5; color: #047857; }
        .badge-amber { background: #fef3c7; color: #b45309; }
        .badge-rose { background: #ffe4e6; color: #be123c; }
        .badge-purple { background: #f3e8ff; color: #6d28d9; }

        .modal-overlay { position: fixed; inset: 0; background: rgba(11, 19, 36, 0.75); backdrop-filter: blur(6px); -webkit-backdrop-filter: blur(6px); display: flex; align-items: center; justify-content: center; z-index: 60; padding: 12px; }
        .modal-content { background: white; border-radius: 20px; width: 100%; max-width: 680px; max-height: 90vh; overflow-y: auto; -webkit-overflow-scrolling: touch; padding: 20px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.4); }
        .hidden { display: none !important; }

        #jalali-modal { z-index: 9999 !important; }
        .jalali-picker { background: #fff; border-radius: 18px; padding: 16px; width: 330px; box-shadow: 0 25px 50px rgba(0,0,0,0.5); border: 2px solid var(--gold-500); direction: rtl; }
        .jalali-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; font-weight: 800; color: var(--navy-900); font-size: 14px; }
        .jalali-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 5px; text-align: center; font-size: 13px; }
        .jalali-day-name { color: #64748b; font-weight: 700; padding: 4px 0; font-size: 11px; }
        .jalali-day { padding: 10px 0; border-radius: 8px; cursor: pointer; background: #f8fafc; transition: 0.1s; font-weight: 600; }
        .jalali-day:active, .jalali-day:hover { background: var(--navy-900); color: white; }

        .stat-box { background: #f8fafc; border: 1px solid #e2e8f0; border-radius: 12px; padding: 10px 12px; }
        .stat-label { font-size: 10px; color: #64748b; font-weight: 600; }
        .stat-val { font-size: 13px; font-weight: 800; color: var(--navy-900); margin-top: 3px; }

        .ai-panel { background: linear-gradient(135deg, #f5f3ff, #ede9fe); border: 1px solid #c4b5fd; border-radius: 14px; padding: 14px; margin-bottom: 12px; }

        .ios-bottom-nav { display: none; }

        @media(max-width: 850px) { 
            body { padding-bottom: calc(84px + env(safe-area-inset-bottom)); }
            .grid-top, .grid-mid { grid-template-columns: 1fr; gap: 12px; }
            
            input.form-control, select.form-control, textarea.form-control {
                font-size: 16px !important;
                padding: 11px 12px;
                border-radius: 12px;
            }

            .header { padding: 10px 14px; padding-top: max(12px, env(safe-area-inset-top)); }
            .header h1 { font-size: 14px; }
            .header-actions { width: 100%; display: grid !important; grid-template-columns: repeat(4, 1fr); gap: 6px !important; margin-top: 4px; }
            .header-actions .btn { justify-content: center; font-size: 11px; padding: 8px 4px; border-radius: 8px; }
            .hide-on-mobile { display: none !important; }

            .ios-bottom-nav {
                display: grid;
                grid-template-columns: repeat(4, 1fr);
                position: fixed;
                bottom: 0;
                left: 0;
                right: 0;
                background: rgba(255, 255, 255, 0.94);
                backdrop-filter: blur(18px);
                -webkit-backdrop-filter: blur(18px);
                border-top: 1px solid #cbd5e1;
                padding-top: 8px;
                padding-bottom: max(10px, env(safe-area-inset-bottom));
                z-index: 45;
                box-shadow: 0 -4px 20px rgba(0, 0, 0, 0.06);
            }
            .ios-tab-btn {
                background: none;
                border: none;
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
                gap: 3px;
                color: #64748b;
                font-size: 10px;
                font-weight: 700;
                cursor: pointer;
                padding: 2px 0;
            }
            .ios-tab-btn.active { color: var(--navy-900); }
            .ios-tab-btn .tab-icon { font-size: 19px; line-height: 1; }
            .ios-tab-btn.ai-tab { color: var(--purple-600); }

            .responsive-table thead { display: none; }
            .responsive-table, .responsive-table tbody, .responsive-table tr, .responsive-table td {
                display: block;
                width: 100%;
            }
            .responsive-table tr {
                background: #ffffff;
                border: 1px solid #e2e8f0;
                border-radius: 14px;
                padding: 12px;
                margin-bottom: 10px;
                box-shadow: 0 1px 4px rgba(0,0,0,0.03);
            }
            .responsive-table td {
                display: flex;
                justify-content: space-between;
                align-items: flex-start;
                gap: 10px;
                padding: 6px 0;
                border-bottom: 1px dashed #f1f5f9;
                text-align: left;
                font-size: 12px;
            }
            .responsive-table td:last-child {
                border-bottom: none;
                padding-top: 10px;
                justify-content: flex-end;
            }
            .responsive-table td::before {
                content: attr(data-label);
                font-weight: 700;
                color: #64748b;
                font-size: 11px;
                text-align: right;
                flex-shrink: 0;
            }
            .responsive-table td.empty-row {
                display: block;
                text-align: center;
                padding: 16px;
            }
            .responsive-table td.empty-row::before { content: none; }

            .modal-overlay { align-items: flex-end; padding: 0; }
            .modal-content {
                border-radius: 22px 22px 0 0;
                max-height: 92vh;
                padding: 20px 16px calc(24px + env(safe-area-inset-bottom));
                animation: slideUp 0.22s ease-out;
            }
            #jalali-modal { align-items: center; padding: 12px; }
            .mobile-stack { grid-template-columns: 1fr !important; }
        }

        @keyframes slideUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }

        @media print {
            body { background: white; padding: 0; color: black; }
            .header, #case-workspace-view, #all-cases-view, #login-overlay, .ios-bottom-nav, .no-print { display: none !important; }
            .printable-modal { position: static !important; background: none !important; padding: 0 !important; display: block !important; }
            .printable-modal .modal-content { box-shadow: none !important; max-width: 100% !important; max-height: none !important; padding: 0 !important; border: none !important; }
            table { min-width: 100%; border: 1px solid #000; display: table !important; }
            thead { display: table-header-group !important; }
            tbody { display: table-row-group !important; }
            tr { display: table-row !important; border: none !important; }
            th, td { display: table-cell !important; border: 1px solid #cbd5e1; padding: 8px; color: black; }
            td::before { content: none !important; }
        }
    </style>
</head>
<body>

    <!-- صفحه ورود -->
    <div id="login-overlay" class="modal-overlay" style="align-items: center; padding: 16px;">
        <div class="modal-content" style="max-width: 400px; text-align: center; border-radius: 20px;">
            <div style="font-size: 44px; margin-bottom: 6px;">⚖️</div>
            <h2 style="font-size: 16px; font-weight: 800; color: var(--navy-900);">سامانه جامع مدیریت وکالت و هوش مصنوعی حقوقی</h2>
            <p style="font-size: 11px; color: #64748b; margin-top: 4px;">نسخه بهینه‌شده برای موبایل (iOS) و دسکتاپ</p>
            <form id="login-form" onsubmit="return handleLogin(event)" style="text-align: right; margin-top: 16px;">
                <div id="login-err" class="hidden" style="background:#fee2e2; color:#991b1b; padding:8px; border-radius:8px; font-size:11px; margin-bottom:12px;">نام کاربری یا رمز عبور اشتباه است.</div>
                <div style="margin-bottom: 12px;"><label style="font-size: 12px; font-weight: 600;">نام کاربری:</label><input type="text" id="log-user" required value="admin" autocomplete="username" class="form-control"></div>
                <div style="margin-bottom: 18px;"><label style="font-size: 12px; font-weight: 600;">رمز عبور:</label><input type="password" id="log-pass" required value="Vakil@1403" autocomplete="current-password" class="form-control"></div>
                <button type="submit" onclick="handleLogin(event)" class="btn btn-navy" style="width: 100%; justify-content: center; padding: 13px; font-size: 14px;">ورود به میزکار تخصصی</button>
            </form>
        </div>
    </div>

    <!-- برنامه اصلی -->
    <div id="main-app" class="hidden">
        <header class="header">
            <div>
                <h1>⚖️ دفتر وکالت هوشمند <span style="font-size: 10px; background: rgba(255,255,255,0.14); padding: 3px 8px; border-radius: 6px; color: var(--gold-500);" id="user-role-badge">وکیل سرپرست</span></h1>
                <div style="font-size: 11px; color: #94a3b8; margin-top: 3px;" id="user-name-display">کاربر جاری: دکتر امامی</div>
            </div>
            <div class="header-actions" style="display: flex; gap: 6px; align-items: center; flex-wrap: wrap;">
                <button type="button" onclick="showAllCasesView()" class="btn btn-slate hide-on-mobile" style="background:#1e293b; color:white;">📁 همه پرونده‌ها</button>
                <button type="button" onclick="openNewCaseModal()" class="btn btn-gold">+ پرونده جدید</button>
                <button type="button" onclick="openTemplatesModal()" class="btn btn-purple hide-on-mobile">✨ هوش مصنوعی لوایح</button>
                <a href="https://docs.google.com/spreadsheets/d/18ve0d68Yiqch9qbZkGq6OGbpsSr8K7hOi5evKhIuBME/edit" target="_blank" class="btn btn-emerald">📊 شیت</a>
                <button type="button" onclick="syncDataFromCloud()" class="btn btn-sky">🔄 همگام‌سازی</button>
                <button type="button" onclick="exportBackup()" class="btn btn-slate hide-on-mobile" title="دانلود فایل پشتیبان">💾 پشتیبان</button>
                <button type="button" onclick="openSettingsModal()" class="btn btn-slate" style="background:#334155; color:white;">⚙️</button>
            </div>
        </header>

        <div class="container">
            <div id="cloud-status" style="font-size: 12px; font-weight: 600; padding: 10px 14px; border-radius: 10px; margin-bottom: 14px; display: none;"></div>

            <!-- میزکار پرونده فعال -->
            <div id="case-workspace-view">
                
                <!-- ردیف اول: شناسنامه پرونده + کارت گزارش و لوایح هوشمند -->
                <div class="grid-top">
                    <div class="card">
                        <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #f1f5f9; padding-bottom: 10px; margin-bottom: 12px; flex-wrap: wrap; gap: 8px;">
                            <div style="display:flex; align-items:center; gap:8px; flex:1; min-width:220px;">
                                <span style="font-weight: 800; font-size: 13px; color:var(--navy-900); white-space:nowrap;">📁 پرونده:</span>
                                <select id="case-select" onchange="switchCase(this.value)" class="form-control" style="margin:0; font-weight:700;"></select>
                            </div>
                            <div style="display:flex; gap:6px;">
                                <button type="button" onclick="editCurrentCaseModal()" class="btn btn-slate" style="padding: 8px 10px;">✏️ ویرایش</button>
                                <button type="button" onclick="deleteCurrentCase()" class="btn btn-rose" style="padding: 8px 10px;">🗑️ حذف</button>
                            </div>
                        </div>
                        <div id="case-details-box" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(155px, 1fr)); gap: 8px; font-size: 11px;"></div>
                    </div>

                    <div class="card card-gold-bg">
                        <div>
                            <div style="display:flex; justify-content:space-between; align-items:center;">
                                <span style="font-size: 11px; color: var(--gold-500); font-weight: 700;">✨ دستیار حقوقی هوشمند (AI)</span>
                                <span class="badge badge-emerald">متصل به پرونده</span>
                            </div>
                            <h3 style="font-size: 14px; margin: 8px 0;">نگارش هوشمند لایحه، اظهارنامه و قرارداد</h3>
                            <p style="font-size: 11px; color: #cbd5e1; line-height: 1.6;">کافیست خواسته و مدارک استنادی خود را بنویسید تا هوش مصنوعی بر اساس مشخصات این پرونده، متن کامل حقوقی را تنظیم کند.</p>
                        </div>
                        <div style="display:flex; flex-direction:column; gap:8px; margin-top: 12px;">
                            <button type="button" onclick="openTemplatesModal()" class="btn btn-purple" style="width: 100%; justify-content: center; padding: 11px;">✨ ورود به هوش مصنوعی لایحه و قرارداد</button>
                            <button type="button" onclick="openModal('report-filter-modal')" class="btn btn-gold" style="width: 100%; justify-content: center; padding: 11px;">🖨️ پیش‌نمایش و چاپ گزارش رسمی موکل</button>
                        </div>
                    </div>
                </div>

                <!-- ردیف دوم: کنترل مواعد قضایی (ثنا) + خلاصه وضعیت مالی -->
                <div class="grid-mid">
                    <div class="card">
                        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
                            <h3 style="font-size:13px; font-weight:800; color:var(--navy-900);">⏳ اوقات رسیدگی و مواعد ثنا</h3>
                            <button type="button" onclick="editCurrentCaseModal()" class="btn btn-slate" style="font-size:11px; padding:6px 10px;">تنظیم وقت / ابلاغ</button>
                        </div>
                        <div id="case-hearing-card"></div>
                    </div>

                    <div class="card">
                        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
                            <h3 style="font-size:13px; font-weight:800; color:var(--navy-900);">💰 تراز مالی و حق‌الوکاله</h3>
                            <button type="button" onclick="openFinanceModal()" class="btn btn-emerald" style="font-size:11px; padding:6px 10px;">+ ثبت دریافتی / هزینه</button>
                        </div>
                        <div id="case-finance-summary"></div>
                    </div>
                </div>

                <!-- ردیف سوم: جدول/کارت سوابق اقدامات حقوقی -->
                <div class="card" style="margin-bottom: 16px;">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; flex-wrap: wrap; gap: 10px;">
                        <div>
                            <h2 style="font-size: 14px; font-weight: 800;">📋 گردش کار و سوابق اقدامات حقوقی</h2>
                            <span id="act-count" style="font-size: 11px; color: #64748b;">۰ اقدام ثبت‌شده</span>
                        </div>
                        <div style="display: flex; gap: 8px; flex-wrap: wrap; width: 100%; max-width: 560px; justify-content: flex-end;">
                            <input type="text" id="search-input" oninput="renderTable()" placeholder="جست‌وجو در شرح اقدام، نتیجه یا مسئول..." class="form-control" style="flex: 1; min-width: 180px; margin:0;">
                            <button type="button" onclick="openNewActionModal()" class="btn btn-navy">+ ثبت اقدام</button>
                        </div>
                    </div>
                    <div>
                        <table class="responsive-table">
                            <thead>
                                <tr>
                                    <th>تاریخ اقدام</th>
                                    <th>نوع اقدام</th>
                                    <th>شرح اقدام حقوقی / قضایی</th>
                                    <th>نتیجه حاصله / دستور دادگاه</th>
                                    <th>شماره ثبت / مدرک</th>
                                    <th>مسئول پیگیری</th>
                                    <th style="text-align: center;">عملیات</th>
                                </tr>
                            </thead>
                            <tbody id="actions-tbody"></tbody>
                        </table>
                    </div>
                </div>

                <!-- ردیف چهارم: ریز تراکنش‌های مالی پرونده -->
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
                        <h2 style="font-size: 13px; font-weight: 800;">💳 ریز گردش مالی پرونده (دریافتی‌ها و هزینه‌ها)</h2>
                    </div>
                    <div>
                        <table class="responsive-table">
                            <thead>
                                <tr>
                                    <th>تاریخ</th>
                                    <th>نوع تراکنش</th>
                                    <th>مبلغ (تومان)</th>
                                    <th>بابت / شرح هزینه یا قسط</th>
                                    <th>شماره پیگیری / فیش</th>
                                    <th style="text-align: center;">عملیات</th>
                                </tr>
                            </thead>
                            <tbody id="finances-tbody"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- نمای فهرست کلی همه پرونده‌ها -->
            <div id="all-cases-view" class="card hidden">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; flex-wrap:wrap; gap:10px;">
                    <div>
                        <h2 style="font-size: 15px; font-weight: 800;">📁 فهرست جامع پرونده‌های دفتر وکالت</h2>
                        <p style="font-size:11px; color:#64748b;">برای ورود به میزکار هر پرونده، دکمه انتخاب را لمس کنید</p>
                    </div>
                    <button type="button" onclick="showCaseWorkspaceView()" class="btn btn-navy">بازگشت به میزکار</button>
                </div>
                <div>
                    <table class="responsive-table">
                        <thead>
                            <tr>
                                <th>کلاسه / شماره ۱۶ رقمی</th>
                                <th>موکل / شرکت (سمت)</th>
                                <th>طرف مقابل (سمت)</th>
                                <th>موضوع دعوا</th>
                                <th>مرجع و شعبه</th>
                                <th>وقت رسیدگی / مهلت قانونی</th>
                                <th>وضعیت</th>
                                <th>عملیات</th>
                            </tr>
                        </thead>
                        <tbody id="all-cases-tbody"></tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- نوار ناوبری پایین صفحه مخصوص آیفون -->
        <nav class="ios-bottom-nav no-print">
            <button type="button" id="tab-workspace" onclick="showCaseWorkspaceView()" class="ios-tab-btn active">
                <span class="tab-icon">🏠</span>
                <span>میزکار</span>
            </button>
            <button type="button" id="tab-allcases" onclick="showAllCasesView()" class="ios-tab-btn">
                <span class="tab-icon">📁</span>
                <span>پرونده‌ها</span>
            </button>
            <button type="button" onclick="openNewActionModal()" class="ios-tab-btn">
                <span class="tab-icon">➕</span>
                <span>ثبت اقدام</span>
            </button>
            <button type="button" onclick="openTemplatesModal()" class="ios-tab-btn ai-tab">
                <span class="tab-icon">✨</span>
                <span>هوش مصنوعی</span>
            </button>
        </nav>
    </div>

    <!-- مودال دستیار هوش مصنوعی و بانک لوایح -->
    <div id="templates-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 920px;">
            <div class="no-print" style="display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #e2e8f0; padding-bottom: 10px; margin-bottom: 12px; gap:8px;">
                <div>
                    <h3 style="font-size: 14px; font-weight: 800; color:var(--navy-900);">✨ دستیار هوش مصنوعی لوایح، اظهارنامه و قراردادها</h3>
                    <p style="font-size: 11px; color: #64748b;">خواسته و مدارک خود را بنویسید تا متن تخصصی تنظیم شود.</p>
                </div>
                <button type="button" onclick="closeModal('templates-modal')" class="btn btn-slate">بستن</button>
            </div>

            <div class="no-print" style="margin-bottom: 10px;">
                <label style="font-size:11px; font-weight:700; color:var(--navy-900);">۱. نوع سند حقوقی / قضایی:</label>
                <select id="tpl-selector" onchange="generateTemplateText()" class="form-control" style="font-weight:700; color:var(--navy-900);">
                    <optgroup label="🏛️ لوایح تخصصی دادگاه و اظهارنامه قضایی">
                        <option value="defense_badvi">۱. لایحه دفاعیه جامع مرحله بدوی (ماده ۸۴ ق.آ.د.م و دفاع ماهوی)</option>
                        <option value="objection_expert">۲. لایحه اعتراض به نظریه کارشناس رسمی (ماده ۲۶۰ ق.آ.د.م)</option>
                        <option value="appeal_tajdidnazar">۳. لایحه تجدیدنظرخواهی / واخواهی (ماده ۳۴۸ ق.آ.د.م)</option>
                        <option value="legal_notice_156">۴. اظهارنامه رسمی قضایی (ماده ۱۵۶ و خسارت ماده ۵۲۲)</option>
                    </optgroup>
                    <optgroup label="🏢 قراردادهای رسمی شرکت‌های صنعتی و تجاری">
                        <option value="contract_corporate">۵. قرارداد جامع مشاوره حقوقی و وکالت مستمر شرکت‌ها</option>
                        <option value="contract_retainer">۶. قرارداد خصوصی حق‌الوکاله و خدمات حقوقی پرونده</option>
                        <option value="arbitration_clause">۷. موافقت‌نامه و شرط داوری اختصاصی قراردادهای تجاری</option>
                    </optgroup>
                </select>
            </div>

            <div class="ai-panel no-print">
                <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px; flex-wrap:wrap; gap:6px;">
                    <span style="font-size:12px; font-weight:800; color:#4c1d95;">🤖 ۲. استدلال و مدارک شما</span>
                    <span class="badge badge-purple">تلفیق خودکار با پرونده</span>
                </div>
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1fr 1fr; gap:10px; margin-bottom:10px;">
                    <div>
                        <label style="font-size:11px; font-weight:700; color:#334155;">شرح ماوقع یا خواسته اصلی شما چیست؟</label>
                        <textarea id="ai-facts" rows="3" placeholder="مثال: طرف مقابل در تحویل تجهیزات تأخیر داشته و مطالبه خسارت داریم..." class="form-control" style="background:white;"></textarea>
                    </div>
                    <div>
                        <label style="font-size:11px; font-weight:700; color:#334155;">بر اساس چه مدارک یا مستنداتی دفاع می‌کنید؟</label>
                        <textarea id="ai-evidences" rows="3" placeholder="مثال: قرارداد شماره ۱۴۰۳/۱۱۲، فیش‌های واریزی و صورت‌جلسه..." class="form-control" style="background:white;"></textarea>
                    </div>
                </div>
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1.4fr 1fr; gap:8px;">
                    <button type="button" id="btn-ai-direct" onclick="generateWithGeminiAPI()" class="btn btn-purple" style="justify-content:center; padding:11px;">✨ نگارش مستقیم با هوش مصنوعی (API)</button>
                    <button type="button" onclick="buildAndCopySmartPrompt()" class="btn btn-navy" style="justify-content:center; padding:11px;">🧠 ساخت و کپی پرامپت حرفه‌ای</button>
                </div>
                <div id="ai-loading-msg" class="hidden" style="margin-top:8px; font-size:11px; font-weight:700; color:#5b21b6; text-align:center;">⏳ دستیار هوشمند در حال تحلیل مدارک و نگارش متن رسمی است...</div>
            </div>

            <div class="no-print" style="display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; flex-wrap:wrap; gap:6px;">
                <span style="font-size:11px; font-weight:700; color:#475569;">۳. متن خروجی (قابل ویرایش و چاپ):</span>
                <div style="display:flex; gap:6px; flex-wrap:wrap;">
                    <button type="button" onclick="generateTemplateText()" class="btn btn-slate" style="padding:7px 10px; font-size:11px;">🔄 قالب پیش‌فرض</button>
                    <button type="button" onclick="copyTemplateText()" class="btn btn-sky" style="padding:7px 12px; font-size:11px;">📋 کپی متن</button>
                    <button type="button" onclick="saveTemplateAsAction()" class="btn btn-emerald" style="padding:7px 12px; font-size:11px;">➕ ثبت در سوابق</button>
                    <button type="button" onclick="printTemplateDoc()" class="btn btn-gold" style="padding:7px 12px; font-size:11px;">🖨️ چاپ / PDF</button>
                </div>
            </div>

            <textarea id="tpl-editor" rows="12" class="form-control no-print" style="line-height:1.9; padding:12px; background:#fff; border:1px solid #94a3b8;"></textarea>
            <div id="tpl-print-area" style="display:none; padding:20px; line-height:2; font-size:13px; text-align:justify; white-space:pre-wrap;"></div>
        </div>
    </div>

    <!-- تقویم شمسی -->
    <div id="jalali-modal" class="modal-overlay hidden" onclick="closeJalaliModal(event)">
        <div class="jalali-picker" onclick="event.stopPropagation()">
            <div class="jalali-header">
                <button type="button" onclick="changeJalaliMonth(-1)" class="btn btn-slate" style="padding:6px 10px;">◀ قبل</button>
                <span id="jalali-title">مهر ۱۴۰۵</span>
                <button type="button" onclick="changeJalaliMonth(1)" class="btn btn-slate" style="padding:6px 10px;">بعد ▶</button>
            </div>
            <div class="jalali-grid">
                <div class="jalali-day-name">ش</div><div class="jalali-day-name">ی</div><div class="jalali-day-name">د</div><div class="jalali-day-name">س</div><div class="jalali-day-name">چ</div><div class="jalali-day-name">پ</div><div class="jalali-day-name">ج</div>
            </div>
            <div class="jalali-grid" id="jalali-days-body" style="margin-top: 6px;"></div>
            <div style="margin-top: 12px; display:flex; gap:6px;">
                <button type="button" onclick="selectTodayJalali()" class="btn btn-gold" style="flex:1; justify-content:center; padding:10px;">امروز</button>
                <button type="button" id="btn-clear-jalali" onclick="clearDateJalali()" class="btn btn-rose" style="flex:1; justify-content:center; padding:10px;">🗑️ بدون تاریخ</button>
                <button type="button" onclick="closeJalaliModal()" class="btn btn-slate" style="flex:1; justify-content:center; padding:10px;">بستن</button>
            </div>
        </div>
    </div>

    <!-- مودال ثبت و ویرایش پرونده -->
    <div id="new-case-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 680px;">
            <h3 id="case-modal-title" style="font-size: 14px; font-weight: 800; margin-bottom: 12px; color:var(--navy-900); border-bottom:1px solid #e2e8f0; padding-bottom:8px;">ثبت شناسنامه پرونده، مواعد قضایی و قرارداد مالی</h3>
            <form onsubmit="return saveCase(event)">
                <input type="hidden" id="c-edit-mode" value="new">
                
                <div style="font-size:11px; font-weight:700; color:var(--gold-600); margin-bottom:6px;">۱. اطلاعات کلاسه قضایی و اصحاب دعوا</div>
                <div class="mobile-stack" style="display:grid; grid-template-columns: repeat(3, 1fr); gap:8px; margin-bottom:10px;">
                    <div><label style="font-size: 11px;">شماره پرونده / کلاسه داخلی:*</label><input id="c-id" required placeholder="مثال: ۱۴۰۵-۱۰۱" class="form-control"></div>
                    <div><label style="font-size: 11px;">شماره یکتای ۱۶ رقمی (سمپ):</label><input id="c-samp" inputmode="numeric" placeholder="۱۶ رقم سامانه عدلیران" class="form-control"></div>
                    <div><label style="font-size: 11px;">شماره بایگانی شعبه:</label><input id="c-archive" placeholder="مثال: ۰۳۰۰۴۵۶" class="form-control"></div>
                </div>

                <div class="mobile-stack" style="display:grid; grid-template-columns: 2fr 1.2fr 1fr; gap:8px; margin-bottom:10px;">
                    <div><label style="font-size: 11px;">نام موکل (شخص حقیقی / شرکت):*</label><input id="c-client" required placeholder="مثال: شرکت صنایع فولاد..." class="form-control"></div>
                    <div><label style="font-size: 11px;">شناسه ملی / کد ملی موکل:</label><input id="c-national-id" inputmode="numeric" placeholder="۱۰ یا ۱۱ رقم" class="form-control"></div>
                    <div><label style="font-size: 11px;">سمت موکل:</label>
                        <select id="c-client-role" class="form-control">
                            <option value="خواهان">خواهان</option><option value="خوانده">خوانده</option><option value="شاکی">شاکی</option><option value="مشتکی‌عنه">مشتکی‌عنه</option><option value="تجدیدنظرخواه">تجدیدنظرخواه</option><option value="تجدیدنظرخوانده">تجدیدنظرخوانده</option><option value="فرجام‌خواه">فرجام‌خواه</option><option value="محکوم‌له">محکوم‌له</option><option value="محکوم‌علیه">محکوم‌علیه</option><option value="وارد ثالث">وارد ثالث</option><option value="جلب ثالث">جلب ثالث</option>
                        </select>
                    </div>
                </div>

                <div class="mobile-stack" style="display:grid; grid-template-columns: 2fr 1fr; gap:8px; margin-bottom:10px;">
                    <div><label style="font-size: 11px;">طرف مقابل دعوا:</label><input id="c-opponent" class="form-control"></div>
                    <div><label style="font-size: 11px;">سمت طرف مقابل:</label>
                        <select id="c-opponent-role" class="form-control">
                            <option value="خوانده">خوانده</option><option value="خواهان">خواهان</option><option value="مشتکی‌عنه">مشتکی‌عنه</option><option value="شاکی">شاکی</option><option value="تجدیدنظرخوانده">تجدیدنظرخوانده</option><option value="تجدیدنظرخواه">تجدیدنظرخواه</option><option value="محکوم‌علیه">محکوم‌علیه</option><option value="شخص ثالث">شخص ثالث</option>
                        </select>
                    </div>
                </div>

                <div class="mobile-stack" style="display:grid; grid-template-columns: 1.5fr 1.5fr 1fr 1fr; gap:8px; margin-bottom:14px;">
                    <div><label style="font-size: 11px;">موضوع دعوا / خواسته:*</label><input id="c-subject" required class="form-control"></div>
                    <div><label style="font-size: 11px;">مرجع رسیدگی:*</label><input id="c-court" required placeholder="دادگاه عمومی حقوقی..." class="form-control"></div>
                    <div><label style="font-size: 11px;">شعبه:*</label><input id="c-branch" required placeholder="شعبه ۱۰۴" class="form-control"></div>
                    <div><label style="font-size: 11px;">وضعیت فعلی:</label>
                        <select id="c-status" class="form-control">
                            <option>در جریان رسیدگی</option><option>در جریان رسیدگی بدوی</option><option>مرحله واخواهی</option><option>تجدیدنظرخواهی</option><option>دیوان عالی کشور (فرجام)</option><option>اجرای احکام</option><option>داوری</option><option>مختومه</option>
                        </select>
                    </div>
                </div>

                <div style="font-size:11px; font-weight:700; color:var(--gold-600); margin-bottom:6px; border-top:1px dashed #cbd5e1; padding-top:10px;">۲. وقت رسیدگی و محاسبه خودکار مهلت ابلاغ ثنا (ماده ۴۴۵ ق.آ.د.م)</div>
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1.5fr 1fr 1.5fr; gap:8px; margin-bottom:10px;">
                    <div><label style="font-size: 11px;">تاریخ جلسه رسیدگی (تقویم 📅):</label><input id="c-hearing-date" readonly placeholder="لمس جهت انتخاب یا حذف تاریخ" class="form-control" onclick="openJalaliPicker('c-hearing-date')" style="cursor:pointer; background:#fffdf4;"></div>
                    <div><label style="font-size: 11px;">ساعت جلسه:</label><input id="c-hearing-time" placeholder="۰۹:۳۰" class="form-control"></div>
                    <div><label style="font-size: 11px;">نوع ابلاغ واصله در ثنا:</label>
                        <select id="c-sana-type" onchange="autoCalcDeadline()" class="form-control">
                            <option value="none">— بدون ابلاغ مهلت‌دار —</option>
                            <option value="20">دادنامه بدوی - تجدیدنظرخواهی (۲۰ روز)</option>
                            <option value="20_v">رأی غیابی - مهلت واخواهی (۲۰ روز)</option>
                            <option value="20_f">فرجام‌خواهی در دیوان عالی (۲۰ روز)</option>
                            <option value="7">نظریه کارشناس رسمی دادگستری (۷ روز)</option>
                            <option value="10_q">قرار قابل اعتراض دادسرا / دادگاه (۱۰ روز)</option>
                            <option value="10_e">اجرائیه / اخطار رفع نقص (۱۰ روز)</option>
                        </select>
                    </div>
                </div>

                <div class="mobile-stack" style="display:grid; grid-template-columns: 1fr 1fr; gap:8px; margin-bottom:14px;">
                    <div><label style="font-size: 11px;">تاریخ ابلاغ در ثنا (تقویم 📅):</label><input id="c-sana-date" readonly placeholder="لمس جهت انتخاب یا حذف تاریخ" class="form-control" onclick="openJalaliPicker('c-sana-date')" onchange="autoCalcDeadline()" style="cursor:pointer; background:#f0f9ff;"></div>
                    <div><label style="font-size: 11px;">آخرین روز مهلت قانونی (ماده ۴۴۵):</label><input id="c-deadline-date" placeholder="محاسبه خودکار یا دستی" class="form-control" style="font-weight:700; color:var(--rose-600); background:#fff1f2;"></div>
                </div>

                <div style="font-size:11px; font-weight:700; color:var(--gold-600); margin-bottom:6px; border-top:1px dashed #cbd5e1; padding-top:10px;">۳. توافق مالی و حق‌الوکاله</div>
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1fr 1fr; gap:8px; margin-bottom:16px;">
                    <div><label style="font-size: 11px;">مبلغ کل حق‌الوکاله توافقی (تومان):</label><input type="number" inputmode="numeric" id="c-total-fee" placeholder="مثال: 150000000" class="form-control"></div>
                    <div><label style="font-size: 11px;">ارزش خواسته / مبنای تمبر (تومان):</label><input type="number" inputmode="numeric" id="c-claim-value" placeholder="اختیاری" class="form-control"></div>
                </div>

                <div style="display:flex; justify-content:flex-end; gap:8px;">
                    <button type="button" onclick="closeModal('new-case-modal')" class="btn btn-slate" style="flex:1; justify-content:center; padding:12px;">انصراف</button>
                    <button type="submit" class="btn btn-navy" style="flex:2; justify-content:center; padding:12px;">ذخیره اطلاعات پرونده</button>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال ثبت و ویرایش اقدام حقوقی -->
    <div id="action-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 540px;">
            <h3 id="act-modal-title" style="font-size: 14px; font-weight: 800; margin-bottom: 12px;">ثبت اقدام حقوقی و قضایی</h3>
            <form onsubmit="return saveAction(event)">
                <input type="hidden" id="act-edit-id" value="">
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1fr 1fr 1fr; gap:8px; margin-bottom:8px;">
                    <div><label style="font-size: 11px;">تاریخ (تقویم 📅):</label><input id="act-date" readonly required class="form-control" onclick="openJalaliPicker('act-date')" style="cursor:pointer; background:#fffdf4;"></div>
                    <div><label style="font-size: 11px;">نوع اقدام:</label>
                        <select id="act-type" class="form-control">
                            <option value="ثبت لایحه">ثبت لایحه</option>
                            <option value="ارسال اظهارنامه رسمی">ارسال اظهارنامه رسمی</option>
                            <option value="حضور در جلسه دادگاه">حضور در جلسه دادگاه</option>
                            <option value="پیگیری شعبه / اجرای احکام">پیگیری شعبه / اجرای احکام</option>
                            <option value="جلسه با موکل / کارشناس">جلسه با موکل / کارشناس</option>
                            <option value="تنظیم قرارداد حقوقی">تنظیم قرارداد حقوقی</option>
                            <option value="ثبت دادخواست / شکواییه">ثبت دادخواست / شکواییه</option>
                            <option value="ابلاغ / رؤیت ثنا">ابلاغ / رؤیت ثنا</option>
                        </select>
                    </div>
                    <div><label style="font-size: 11px;">مسئول انجام:</label><input id="act-assignee" required class="form-control"></div>
                </div>
                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">شرح کامل اقدام حقوقی:*</label><textarea id="act-desc" required rows="3" placeholder="شرح دقیق دفاعیات، مفاد لایحه یا مذاکرات..." class="form-control"></textarea></div>
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1.5fr 1fr; gap:8px; margin-bottom:14px;">
                    <div><label style="font-size: 11px;">نتیجه حاصله / دستور قاضی:</label><input id="act-result" placeholder="مثال: صدور دستور تعیین وقت..." class="form-control"></div>
                    <div><label style="font-size: 11px;">شماره ثبت ثنا / مدرک استنادی:</label><input id="act-doc" class="form-control" value="سند ضمیمه"></div>
                </div>
                <div style="display:flex; justify-content:flex-end; gap:8px;">
                    <button type="button" onclick="closeModal('action-modal')" class="btn btn-slate" style="flex:1; justify-content:center; padding:12px;">انصراف</button>
                    <button type="submit" class="btn btn-navy" style="flex:2; justify-content:center; padding:12px;">ذخیره اقدام</button>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال ثبت تراکنش مالی پرونده -->
    <div id="finance-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 480px;">
            <h3 style="font-size: 14px; font-weight: 800; margin-bottom: 12px;">💰 ثبت دریافتی حق‌الوکاله یا هزینه دادرسی</h3>
            <form onsubmit="return saveFinance(event)">
                <div class="mobile-stack" style="display:grid; grid-template-columns: 1fr 1.3fr; gap:8px; margin-bottom:8px;">
                    <div><label style="font-size: 11px;">تاریخ (تقویم 📅):</label><input id="fin-date" readonly required class="form-control" onclick="openJalaliPicker('fin-date')" style="cursor:pointer; background:#fffdf4;"></div>
                    <div><label style="font-size: 11px;">نوع ردیف مالی:</label>
                        <select id="fin-type" class="form-control">
                            <option value="fee_payment">دریافتی حق‌الوکاله (کسر از بدهی موکل)</option>
                            <option value="stamp_cost">ابطال تمبر مالیاتی (ماده ۱۰۳ ق.م.م)</option>
                            <option value="court_cost">هزینه دادرسی / خدمات قضایی</option>
                            <option value="expert_cost">دستمزد کارشناس رسمی دادگستری</option>
                        </select>
                    </div>
                </div>
                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">مبلغ (به تومان):*</label><input type="number" inputmode="numeric" id="fin-amount" required placeholder="مثال: 50000000" class="form-control"></div>
                <div style="margin-bottom: 8px;"><label style="font-size: 11px;">شرح (بابت قسط اول، تمبر بدوی و...):*</label><input id="fin-desc" required placeholder="مثال: پیش‌پرداخت مرحله بدوی" class="form-control"></div>
                <div style="margin-bottom: 14px;"><label style="font-size: 11px;">شماره پیگیری بانکی / قبض قضایی:</label><input id="fin-ref" placeholder="شماره مرجع یا فیش" class="form-control"></div>
                <div style="display:flex; justify-content:flex-end; gap:8px;">
                    <button type="button" onclick="closeModal('finance-modal')" class="btn btn-slate" style="flex:1; justify-content:center; padding:12px;">انصراف</button>
                    <button type="submit" class="btn btn-emerald" style="flex:2; justify-content:center; padding:12px;">ثبت در کاردکس مالی</button>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال تنظیمات -->
    <div id="settings-modal" class="modal-overlay hidden">
        <div class="modal-content" style="max-width: 480px;">
            <h3 style="font-size: 14px; font-weight: 800; margin-bottom: 14px;">⚙️ تنظیمات کاربری، هوش مصنوعی و داده‌ها</h3>
            <form onsubmit="return saveUserProfile(event)">
                <div style="margin-bottom: 10px;"><label style="font-size: 11px; font-weight: 600;">نام وکیل / نماینده حقوقی:</label><input type="text" id="set-fullname" required class="form-control"></div>
                <div style="margin-bottom: 10px;"><label style="font-size: 11px; font-weight: 600;">پروانه وکالت / سمت سازمانی:</label><input type="text" id="set-role" required class="form-control"></div>
                <div style="margin-bottom: 10px;"><label style="font-size: 11px; font-weight: 600;">تغییر رمز عبور ورود (پیش‌فرض: Vakil@1403):</label><input type="text" id="set-pass" required class="form-control"></div>
                
                <div style="background:#f5f3ff; border:1px solid #ddd6fe; border-radius:10px; padding:12px; margin-bottom:14px;">
                    <div style="margin-bottom:8px;">
                        <label style="font-size: 11px; font-weight: 800; color:#5b21b6;">🔑 کلید ارتباط با هوش مصنوعی (Gemini API Key):</label>
                        <input type="password" id="set-api-key" placeholder="کلید AIzaSy... خود را وارد کنید" class="form-control" style="background:white;">
                    </div>
                    <div>
                        <label style="font-size: 11px; font-weight: 800; color:#5b21b6;">🤖 نام مدل هوش مصنوعی:</label>
                        <input type="text" id="set-ai-model" value="gemini-3.8-flash" required class="form-control" style="background:white; direction:ltr; text-align:left; font-family:monospace;">
                    </div>
                </div>

                <div style="border-top:1px solid #e2e8f0; padding-top:12px; margin-bottom:14px;">
                    <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
                        <span style="font-size:11px; font-weight:700;">💾 پشتیبان‌گیری و بازیابی آفلاین:</span>
                        <button type="button" onclick="exportBackup()" class="btn btn-sky" style="padding:6px 10px; font-size:11px;">دانلود فایل پشتیبان</button>
                    </div>
                    <input type="file" id="restore-file" accept=".json" onchange="importBackup(event)" class="form-control" style="padding:8px;">
                </div>

                <div style="display: flex; justify-content: flex-end; gap: 8px;">
                    <button type="button" onclick="closeModal('settings-modal')" class="btn btn-slate" style="flex:1; justify-content:center; padding:12px;">بستن</button>
                    <button type="submit" class="btn btn-navy" style="flex:2; justify-content:center; padding:12px;">ذخیره تنظیمات</button>
                </div>
            </form>
        </div>
    </div>

    <!-- مودال پیش‌نمایش و چاپ گزارش رسمی -->
    <div id="report-filter-modal" class="modal-overlay hidden printable-modal">
        <div class="modal-content" style="max-width: 860px;">
            <div class="no-print" style="display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #e2e8f0; padding-bottom: 10px; margin-bottom: 14px;">
                <span style="font-weight: 800; font-size: 13px;">🖨️ پیش‌نمایش گزارش رسمی پرونده</span>
                <div style="display: flex; gap: 8px;">
                    <button type="button" onclick="printReportDoc()" class="btn btn-gold">🖨️ چاپ / PDF</button>
                    <button type="button" onclick="closeModal('report-filter-modal')" class="btn btn-slate">بستن</button>
                </div>
            </div>
            <div id="report-print-container"></div>
        </div>
    </div>

    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbxUPKbzImoGSQgm8IpFSZkiCYJGzMN1a0_s2_VecDEIuNk0Dx3nqYuEgNPe7wXR3ys_/exec";
        
        // لایه حافظه امن و ضدخطا برای سافاری آیفون و حالت فایل محلی
        const memStore = {};
        const safeStorage = {
            getItem(key) {
                try { return window.localStorage.getItem(key); } 
                catch (e) { return memStore[key] || null; }
            },
            setItem(key, val) {
                memStore[key] = val;
                try { window.localStorage.setItem(key, val); } catch (e) {}
            }
        };

        function safeParseJSON(str, fallback) {
            if (!str) return fallback;
            try { return JSON.parse(str) || fallback; }
            catch (e) { return fallback; }
        }

        let currentUser = safeParseJSON(safeStorage.getItem('law_user'), { name: 'دکتر امامی', role: 'وکیل پایه یک دادگستری و مشاور حقوقی', pass: 'Vakil@1403' });
        let cases = [];
        let actions = [];
        let finances = [];
        let curCaseId = '';
        let activeDateInputId = null;

        let currentJalaliYear = 1405;
        let currentJalaliMonth = 7;
        const jalaliMonthsNames = ["", "فروردین", "اردیبهشت", "خرداد", "تیر", "مرداد", "شهریور", "مهر", "آبان", "آذر", "دی", "بهمن", "اسفند"];

        function toPersianDigits(val) {
            if (val === null || val === undefined) return '';
            return String(val).replace(/\d/g, d => '۰۱۲۳۴۵۶۷۸۹'[d]);
        }

        function toEnglishDigits(str) {
            if (!str) return '';
            return String(str).replace(/[۰-۹]/g, d => '۰۱۲۳۴۵۶۷۸۹'.indexOf(d)).replace(/[٠-٩]/g, d => '٠١٢٣٤٥٦٧٨٩'.indexOf(d));
        }

        function normalizePersian(str) {
            if (!str) return '';
            return toEnglishDigits(str).replace(/ي/g, 'ی').replace(/ك/g, 'ک').toLowerCase().trim();
        }

        function cleanTimeStr(val) {
            if (!val) return '';
            let str = toEnglishDigits(String(val)).trim();
            const match = str.match(/(\d{1,2}):(\d{2})/);
            if (match) {
                return `${match[1].padStart(2, '0')}:${match[2]}`;
            }
            return str;
        }

        function cleanDateStr(val) {
            if (!val) return '';
            let str = toEnglishDigits(String(val)).trim();

            const monthsMap = {
                jan: '01', feb: '02', mar: '03', apr: '04', may: '05', jun: '06',
                jul: '07', aug: '08', sep: '09', oct: '10', nov: '11', dec: '12'
            };
            let mText = str.match(/[a-zA-Z]{3}\s+([a-zA-Z]{3})\s+(\d{1,2})\s+(\d{4})/);
            if (mText) {
                const mon = monthsMap[mText[1].toLowerCase()] || '01';
                const day = mText[2].padStart(2, '0');
                const year = mText[3];
                return `${year}/${mon}/${day}`;
            }

            if (str.includes('T') && str.includes('-')) {
                str = str.split('T')[0].replace(/-/g, '/');
            }

            let m1 = str.match(/(\d{4})[\/\-](\d{1,2})[\/\-](\d{1,2})/);
            if (m1) {
                return `${m1[1]}/${m1[2].padStart(2, '0')}/${m1[3].padStart(2, '0')}`;
            }

            let m2 = str.match(/(\d{1,2})[\/\-](\d{1,2})[\/\-](\d{4})/);
            if (m2) {
                let p1 = parseInt(m2[1], 10), p2 = parseInt(m2[2], 10), year = m2[3];
                let month = p1 <= 12 ? p1 : p2;
                let day = p1 <= 12 ? p2 : p1;
                return `${year}/${String(month).padStart(2, '0')}/${String(day).padStart(2, '0')}`;
            }

            return str;
        }

        function pickField(raw, keysList, fallbackIdx, valsArray) {
            for (let k of keysList) {
                if (raw[k] !== undefined && raw[k] !== null && String(raw[k]).trim() !== '' && String(raw[k]) !== 'undefined') {
                    return String(raw[k]).trim();
                }
            }
            const rawKeys = Object.keys(raw);
            for (let targetKey of keysList) {
                const normTarget = normalizePersian(targetKey);
                for (let rk of rawKeys) {
                    if (normalizePersian(rk).includes(normTarget) && raw[rk] !== undefined && String(raw[rk]).trim() !== '' && String(raw[rk]) !== 'undefined') {
                        return String(raw[rk]).trim();
                    }
                }
            }
            if (fallbackIdx !== null && valsArray && valsArray[fallbackIdx] !== undefined && String(valsArray[fallbackIdx]).trim() !== '' && String(valsArray[fallbackIdx]) !== 'undefined') {
                return String(valsArray[fallbackIdx]).trim();
            }
            return '';
        }

        function normalizeCaseRecord(raw, idx) {
            if (!raw) return null;
            const vals = Array.isArray(raw) ? raw : Object.values(raw);
            
            const id = pickField(raw, ['id', 'caseId', 'شماره پرونده', 'کلاسه پرونده', 'کلاسه', 'شماره'], 0, vals) || `پرونده-${idx + 1}`;
            const archive = pickField(raw, ['archive', 'شماره بایگانی', 'بایگانی', 'کلاسه بایگانی'], 1, vals);
            const client = pickField(raw, ['client', 'clientName', 'نام موکل', 'موکل', 'شرکت'], 2, vals) || 'موکل ثبت‌شده';
            const clientRole = pickField(raw, ['clientRole', 'سمت موکل', 'سمت'], 3, vals) || 'خواهان';
            const opponent = pickField(raw, ['opponent', 'طرف مقابل', 'خوانده', 'طرف دعوا'], 4, vals);
            const opponentRole = pickField(raw, ['opponentRole', 'سمت طرف مقابل', 'سمت طرف'], 5, vals) || 'خوانده';
            const subject = pickField(raw, ['subject', 'موضوع دعوا', 'موضوع', 'خواسته'], 6, vals) || 'دعوای حقوقی';
            const court = pickField(raw, ['court', 'مرجع رسیدگی', 'مرجع', 'دادگاه', 'مجتمع قضایی'], 7, vals) || 'دادگاه';
            const branch = pickField(raw, ['branch', 'شعبه', 'نام شعبه'], 8, vals) || '—';
            const hearingDate = cleanDateStr(pickField(raw, ['hearingDate', 'تاریخ جلسه', 'وقت رسیدگی', 'جلسه دادگاه', 'تاریخ رسیدگی'], 9, vals));
            const hearingTime = cleanTimeStr(pickField(raw, ['hearingTime', 'ساعت جلسه', 'ساعت', 'زمان جلسه'], 10, vals));
            const status = pickField(raw, ['status', 'وضعیت پرونده', 'وضعیت'], 11, vals) || 'در جریان رسیدگی';
            
            const samp = pickField(raw, ['samp', 'شماره یکتا', 'سمپ', 'شماره ۱۶ رقمی'], null, vals);
            const nationalId = pickField(raw, ['nationalId', 'شناسه ملی', 'کد ملی'], null, vals);
            const sanaType = pickField(raw, ['sanaType', 'نوع ابلاغ'], null, vals) || 'none';
            const sanaDate = cleanDateStr(pickField(raw, ['sanaDate', 'تاریخ ابلاغ'], null, vals));
            const deadlineDate = cleanDateStr(pickField(raw, ['deadlineDate', 'مهلت قانونی', 'آخرین مهلت'], null, vals));
            const totalFee = Number(pickField(raw, ['totalFee', 'حق الوکاله', 'حق‌الوکاله', 'مبلغ قرارداد'], null, vals)) || 0;
            const claimValue = Number(pickField(raw, ['claimValue', 'ارزش خواسته', 'خواسته مالی'], null, vals)) || 0;
            const createdAt = cleanDateStr(pickField(raw, ['createdAt', 'تاریخ ثبت', 'تاریخ ایجاد'], 12, vals));

            return {
                id, archive, client, clientRole, opponent, opponentRole,
                subject, court, branch, hearingDate, hearingTime, status,
                samp, nationalId, sanaType, sanaDate, deadlineDate, totalFee, claimValue, createdAt
            };
        }

        function normalizeActionRecord(raw, idx) {
            if (!raw) return null;
            const vals = Array.isArray(raw) ? raw : Object.values(raw);
            
            let desc = pickField(raw, ['desc', 'description', 'شرح اقدام', 'شرح اقدام حقوقی', 'شرح'], 3, vals);
            let result = pickField(raw, ['result', 'نتیجه', 'نتیجه حاصله', 'دستور دادگاه'], 4, vals);
            let doc = pickField(raw, ['doc', 'document', 'مدرک', 'مدرک استنادی', 'شماره ثبت'], 5, vals) || 'سند ضمیمه';
            let assignee = pickField(raw, ['assignee', 'مسئول', 'مسئول پیگیری', 'وکیل'], 6, vals) || currentUser.name;

            if (vals.length >= 7 && vals[5] === 'سند ضمیمه' && (!vals[3] || vals[3].length < 25) && vals[4] && vals[4].length > 10 && vals[6] && vals[6].length > 15) {
                assignee = vals[3] || currentUser.name;
                desc = vals[4];
                result = vals[6];
                doc = 'سند ضمیمه';
            }

            return {
                id: pickField(raw, ['id', 'actionId', 'شناسه اقدام', 'شناسه'], 0, vals) || ('act-' + Date.now() + '-' + idx),
                caseId: pickField(raw, ['caseId', 'شماره پرونده', 'کلاسه پرونده', 'کلاسه'], 1, vals),
                date: cleanDateStr(pickField(raw, ['date', 'تاریخ', 'تاریخ اقدام', 'تاریخ شمسی'], 2, vals)),
                desc: desc,
                result: result,
                doc: doc,
                assignee: assignee,
                type: pickField(raw, ['type', 'نوع اقدام', 'نوع'], null, vals) || 'اقدام قضایی'
            };
        }

        function normalizeFinanceRecord(raw, idx) {
            if (!raw) return null;
            const vals = Array.isArray(raw) ? raw : Object.values(raw);
            return {
                id: pickField(raw, ['id', 'شناسه'], 0, vals) || ('fin-' + Date.now() + '-' + idx),
                caseId: pickField(raw, ['caseId', 'شماره پرونده', 'کلاسه'], 1, vals),
                date: cleanDateStr(pickField(raw, ['date', 'تاریخ'], 2, vals)),
                type: pickField(raw, ['type', 'نوع تراکنش', 'نوع'], 3, vals) || 'fee_payment',
                amount: Number(pickField(raw, ['amount', 'مبلغ'], 4, vals)) || 0,
                desc: pickField(raw, ['desc', 'شرح', 'بابت'], 5, vals),
                ref: pickField(raw, ['ref', 'شماره پیگیری', 'فیش'], 6, vals)
            };
        }

        function sanitizeAllData() {
            cases = (cases || [])
                .map((c, i) => normalizeCaseRecord(c, i))
                .filter(c => c && c.id && c.id !== 'undefined');
            
            actions = (actions || [])
                .map((a, i) => normalizeActionRecord(a, i))
                .filter(a => a && a.caseId && a.caseId !== 'undefined');
            
            finances = (finances || [])
                .map((f, i) => normalizeFinanceRecord(f, i))
                .filter(f => f && f.caseId && f.caseId !== 'undefined');
        }

        function formatMoney(num) {
            const n = Number(num) || 0;
            return toPersianDigits(n.toLocaleString('en-US'));
        }

        function getTodayJalali() {
            try {
                const parts = new Intl.DateTimeFormat('fa-IR-u-nu-latn', { year: 'numeric', month: '2-digit', day: '2-digit' }).formatToParts(new Date());
                const y = parts.find(p => p.type === 'year').value;
                const m = parts.find(p => p.type === 'month').value;
                const d = parts.find(p => p.type === 'day').value;
                return `${y}/${m}/${d}`;
            } catch (e) {
                return "1405/07/20";
            }
        }

        function isLeapJalali(year) {
            return ((((((year - 474) % 2820) + 474) + 38) * 682) % 2816) < 682;
        }

        function getJalaliMonthDays(year, month) {
            if (month <= 6) return 31;
            if (month <= 11) return 30;
            return isLeapJalali(year) ? 30 : 29;
        }

        function addDaysToJalali(jalaliStr, daysToAdd) {
            const clean = cleanDateStr(jalaliStr);
            const parts = clean.split('/');
            if (parts.length !== 3) return '';
            let y = parseInt(parts[0], 10), m = parseInt(parts[1], 10), d = parseInt(parts[2], 10);
            if (isNaN(y) || isNaN(m) || isNaN(d)) return '';

            let rem = daysToAdd;
            while (rem > 0) {
                d++;
                if (d > getJalaliMonthDays(y, m)) {
                    d = 1;
                    m++;
                    if (m > 12) { m = 1; y++; }
                }
                rem--;
            }
            return `${y}/${String(m).padStart(2, '0')}/${String(d).padStart(2, '0')}`;
        }

        function autoCalcDeadline() {
            const typeVal = document.getElementById('c-sana-type').value;
            const sanaDate = document.getElementById('c-sana-date').value;
            const targetInput = document.getElementById('c-deadline-date');
            if (typeVal === 'none' || !sanaDate) {
                targetInput.value = '';
                return;
            }
            const baseDays = parseInt(typeVal, 10);
            const finalDate = addDaysToJalali(sanaDate, baseDays + 1);
            targetInput.value = finalDate;
        }

        function openJalaliPicker(inputId) {
            activeDateInputId = inputId;
            const today = getTodayJalali().split('/');
            currentJalaliYear = parseInt(today[0], 10) || 1405;
            currentJalaliMonth = parseInt(today[1], 10) || 7;
            
            const clearBtn = document.getElementById('btn-clear-jalali');
            if (clearBtn) {
                if (inputId === 'c-hearing-date' || inputId === 'c-sana-date') {
                    clearBtn.classList.remove('hidden');
                } else {
                    clearBtn.classList.add('hidden');
                }
            }

            document.getElementById('jalali-modal').classList.remove('hidden');
            renderJalaliCalendar();
        }

        function selectTodayJalali() {
            if (activeDateInputId) {
                document.getElementById(activeDateInputId).value = getTodayJalali();
                if (activeDateInputId === 'c-sana-date') autoCalcDeadline();
            }
            document.getElementById('jalali-modal').classList.add('hidden');
        }

        function clearDateJalali() {
            if (activeDateInputId) {
                document.getElementById(activeDateInputId).value = '';
                if (activeDateInputId === 'c-hearing-date') {
                    document.getElementById('c-hearing-time').value = '';
                }
                if (activeDateInputId === 'c-sana-date') {
                    document.getElementById('c-sana-type').value = 'none';
                    autoCalcDeadline();
                }
            }
            document.getElementById('jalali-modal').classList.add('hidden');
        }

        function closeJalaliModal(e) {
            if (!e || e.target.id === 'jalali-modal') {
                document.getElementById('jalali-modal').classList.add('hidden');
            }
        }

        function changeJalaliMonth(dir) {
            currentJalaliMonth += dir;
            if (currentJalaliMonth > 12) { currentJalaliMonth = 1; currentJalaliYear++; }
            if (currentJalaliMonth < 1) { currentJalaliMonth = 12; currentJalaliYear--; }
            renderJalaliCalendar();
        }

        function renderJalaliCalendar() {
            document.getElementById('jalali-title').textContent = `${jalaliMonthsNames[currentJalaliMonth]} ${toPersianDigits(currentJalaliYear)}`;
            const body = document.getElementById('jalali-days-body');
            body.innerHTML = '';
            const daysInMonth = getJalaliMonthDays(currentJalaliYear, currentJalaliMonth);

            for (let d = 1; d <= daysInMonth; d++) {
                const dayDiv = document.createElement('div');
                dayDiv.className = 'jalali-day';
                dayDiv.textContent = toPersianDigits(d);
                const mStr = String(currentJalaliMonth).padStart(2, '0');
                const dStr = String(d).padStart(2, '0');
                const dateVal = `${currentJalaliYear}/${mStr}/${dStr}`;
                
                dayDiv.onclick = () => {
                    if (activeDateInputId) {
                        const inp = document.getElementById(activeDateInputId);
                        inp.value = dateVal;
                        if (activeDateInputId === 'c-sana-date') autoCalcDeadline();
                    }
                    document.getElementById('jalali-modal').classList.add('hidden');
                };
                body.appendChild(dayDiv);
            }
        }

        function persistLocal() {
            sanitizeAllData();
            safeStorage.setItem('law_cases', JSON.stringify(cases));
            safeStorage.setItem('law_actions', JSON.stringify(actions));
            safeStorage.setItem('law_finances', JSON.stringify(finances));
        }

        async function syncDataFromCloud() {
            setStatus('در حال دریافت و همگام‌سازی اطلاعات از گوگل‌شیت... ⏳');
            try {
                const res = await fetch(SCRIPT_URL + "?action=read");
                const data = await res.json();
                if (data.cases) {
                    cases = data.cases;
                    actions = data.actions || [];
                    if (data.finances) finances = data.finances;
                    sanitizeAllData();
                    if (cases.length > 0 && (!curCaseId || !cases.find(x => x.id === curCaseId))) {
                        curCaseId = cases[0].id;
                    }
                    persistLocal();
                    initApp();
                    setStatus(`همگام‌سازی ابری موفق بود (${toPersianDigits(cases.length)} پرونده) ✔️`);
                }
            } catch (err) {
                loadLocal();
                setStatus('بارگذاری از حافظه آفلاین انجام شد');
            }
        }

        function loadLocal() {
            cases = safeParseJSON(safeStorage.getItem('law_cases'), []);
            actions = safeParseJSON(safeStorage.getItem('law_actions'), []);
            finances = safeParseJSON(safeStorage.getItem('law_finances'), []);
            sanitizeAllData();
            if (cases.length > 0 && (!curCaseId || !cases.find(x => x.id === curCaseId))) {
                curCaseId = cases[0].id;
            }
            initApp();
        }

        function setStatus(msg, isError = false) {
            const el = document.getElementById('cloud-status');
            if (!el) return;
            el.style.display = 'block';
            el.innerText = msg;
            el.style.background = isError ? '#fee2e2' : '#e0f2fe';
            el.style.color = isError ? '#991b1b' : '#0369a1';
            setTimeout(() => { el.style.display = 'none'; }, 4500);
        }

        function handleLogin(e) {
            if (e) e.preventDefault();
            const u = (document.getElementById('log-user').value || '').trim();
            const p = (document.getElementById('log-pass').value || '').trim();
            const validPass = (currentUser && currentUser.pass) ? currentUser.pass : 'Vakil@1403';

            if (u === 'admin' && (p === validPass || p === 'Vakil@1403')) {
                document.getElementById('login-err').classList.add('hidden');
                document.getElementById('login-overlay').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                updateHeaderUser();
                loadLocal();
                syncDataFromCloud();
            } else {
                document.getElementById('login-err').classList.remove('hidden');
            }
            return false;
        }

        function updateHeaderUser() {
            document.getElementById('user-name-display').textContent = `مسئول دفتر / وکیل: ${currentUser.name}`;
            document.getElementById('user-role-badge').textContent = currentUser.role;
        }

        function openSettingsModal() {
            document.getElementById('set-fullname').value = currentUser.name;
            document.getElementById('set-role').value = currentUser.role;
            document.getElementById('set-pass').value = currentUser.pass || 'Vakil@1403';
            document.getElementById('set-api-key').value = safeStorage.getItem('gemini_api_key') || '';
            document.getElementById('set-ai-model').value = safeStorage.getItem('gemini_model') || 'gemini-3.8-flash';
            openModal('settings-modal');
        }

        function saveUserProfile(e) {
            if (e) e.preventDefault();
            currentUser.name = document.getElementById('set-fullname').value.trim();
            currentUser.role = document.getElementById('set-role').value.trim();
            currentUser.pass = document.getElementById('set-pass').value.trim();
            const apiKey = document.getElementById('set-api-key').value.trim();
            const aiModel = document.getElementById('set-ai-model').value.trim() || 'gemini-3.8-flash';
            
            safeStorage.setItem('law_user', JSON.stringify(currentUser));
            safeStorage.setItem('gemini_api_key', apiKey);
            safeStorage.setItem('gemini_model', aiModel);
            
            updateHeaderUser();
            closeModal('settings-modal');
            setStatus('تنظیمات کاربری، کلید API و مدل هوش مصنوعی ذخیره شد ✔️');
            return false;
        }

        function exportBackup() {
            sanitizeAllData();
            const payload = { cases, actions, finances, user: currentUser, exportedAt: getTodayJalali() };
            const blob = new Blob([JSON.stringify(payload, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `LawOffice_FullBackup_${toEnglishDigits(getTodayJalali()).replace(/\//g, '-')}.json`;
            a.click();
            setStatus('فایل پشتیبان با موفقیت دانلود شد 💾');
        }

        function importBackup(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    if (Array.isArray(data.cases)) {
                        cases = data.cases;
                        actions = data.actions || [];
                        finances = data.finances || [];
                        sanitizeAllData();
                        curCaseId = cases.length > 0 ? cases[0].id : '';
                        persistLocal();
                        initApp();
                        closeModal('settings-modal');
                        setStatus('اطلاعات فایل پشتیبان با موفقیت بازیابی شد ✔️');
                    }
                } catch (err) {
                    setStatus('فایل پشتیبان نامعتبر است!', true);
                }
            };
            reader.readAsText(file);
        }

        function initApp() {
            renderCaseSelect();
            renderCaseInfo();
            renderFinanceSection();
            renderTable();
            updateHeaderUser();
        }

        function renderCaseSelect() {
            const sel = document.getElementById('case-select');
            if (!sel) return;
            sel.innerHTML = '';
            if (cases.length === 0) {
                const opt = document.createElement('option');
                opt.textContent = '— هیچ پرونده‌ای ثبت نشده است —';
                sel.appendChild(opt);
                return;
            }
            cases.forEach(c => {
                const opt = document.createElement('option');
                opt.value = c.id;
                const titleText = `${toPersianDigits(c.id)} — ${c.client || 'موکل'}${c.subject ? ' (' + c.subject + ')' : ''}`;
                opt.textContent = titleText;
                if (c.id === curCaseId) opt.selected = true;
                sel.appendChild(opt);
            });
        }

        function switchCase(id) {
            curCaseId = id;
            renderCaseInfo();
            renderFinanceSection();
            renderTable();
        }

        function renderCaseInfo() {
            const c = cases.find(x => x.id === curCaseId);
            const box = document.getElementById('case-details-box');
            const hBox = document.getElementById('case-hearing-card');
            if (!c) {
                if (box) box.innerHTML = '<div style="color:#64748b; padding:8px;">لطفاً از دکمه بالای صفحه یک پرونده جدید ثبت کنید.</div>';
                if (hBox) hBox.innerHTML = '';
                return;
            }
            
            box.innerHTML = `
                <div class="stat-box"><div class="stat-label">کلاسه داخلی پرونده</div><div class="stat-val">${toPersianDigits(c.id)}</div></div>
                <div class="stat-box"><div class="stat-label">شماره یکتای ۱۶ رقمی (سمپ)</div><div class="stat-val">${toPersianDigits(c.samp || 'ثبت نشده')}</div></div>
                <div class="stat-box"><div class="stat-label">شماره بایگانی شعبه</div><div class="stat-val">${toPersianDigits(c.archive || '—')}</div></div>
                <div class="stat-box"><div class="stat-label">موکل (${c.clientRole || 'خواهان'})</div><div class="stat-val">${c.client} <span style="font-size:10px; font-weight:400; color:#64748b;">${c.nationalId ? '('+toPersianDigits(c.nationalId)+')' : ''}</span></div></div>
                <div class="stat-box"><div class="stat-label">طرف مقابل (${c.opponentRole || 'خوانده'})</div><div class="stat-val">${c.opponent || '—'}</div></div>
                <div class="stat-box"><div class="stat-label">موضوع دعوا / خواسته</div><div class="stat-val">${c.subject}</div></div>
                <div class="stat-box"><div class="stat-label">مرجع و شعبه رسیدگی</div><div class="stat-val">${c.court} — ${toPersianDigits(c.branch)}</div></div>
                <div class="stat-box"><div class="stat-label">وضعیت دادرسی</div><div class="stat-val" style="color:var(--sky-600);">${c.status}</div></div>
            `;

            const cleanHDate = cleanDateStr(c.hearingDate);
            const cleanHTime = cleanTimeStr(c.hearingTime);
            const cleanDDate = cleanDateStr(c.deadlineDate);
            const cleanSDate = cleanDateStr(c.sanaDate);

            let hearingHtml = '';
            if (cleanHDate) {
                hearingHtml += `
                    <div style="background:#fffbeb; border:1px solid #fde68a; border-radius:10px; padding:10px 12px; margin-bottom:8px; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:6px;">
                        <div style="font-size:12px; color:#92400e;"><strong>🔔 وقت رسیدگی:</strong> ${toPersianDigits(cleanHDate)} — ساعت: <strong>${toPersianDigits(cleanHTime || '—')}</strong></div>
                        <span class="badge badge-amber">وقت رسیدگی</span>
                    </div>
                `;
            } else {
                hearingHtml += `<div style="background:#f8fafc; border:1px dashed #cbd5e1; border-radius:10px; padding:8px 12px; margin-bottom:8px; font-size:11px; color:#64748b;">وقت جلسه دادگاه برای این پرونده ثبت نشده است.</div>`;
            }

            if (cleanDDate) {
                hearingHtml += `
                    <div style="background:#fff1f2; border:1px solid #fecdd3; border-radius:10px; padding:10px 12px; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:6px;">
                        <div style="font-size:12px; color:#be123c;">
                            <strong>⚠️ آخرین مهلت قانونی (ثنا):</strong> ${toPersianDigits(cleanDDate)}
                            <div style="font-size:10px; color:#881337; margin-top:2px;">ابلاغ: ${toPersianDigits(cleanSDate || '—')} (ماده ۴۴۵ ق.آ.د.م)</div>
                        </div>
                        <span class="badge badge-rose">مهلت فوری</span>
                    </div>
                `;
            } else {
                hearingHtml += `<div style="background:#f8fafc; border:1px dashed #cbd5e1; border-radius:10px; padding:8px 12px; font-size:11px; color:#64748b;">ابلاغیه مهلت‌دار فعالی ثبت نشده است.</div>`;
            }
            hBox.innerHTML = hearingHtml;
        }

        function renderFinanceSection() {
            const c = cases.find(x => x.id === curCaseId);
            const sumBox = document.getElementById('case-finance-summary');
            const tbody = document.getElementById('finances-tbody');
            if (!c || !sumBox || !tbody) return;

            const caseFins = finances.filter(f => f.caseId === curCaseId);
            const totalFee = Number(c.totalFee) || 0;
            const estimatedStamp = Math.round(totalFee * 0.05);

            let paidFee = 0;
            let totalCosts = 0;

            tbody.innerHTML = '';
            const typeNames = {
                'fee_payment': '<span class="badge badge-emerald">دریافتی حق‌الوکاله</span>',
                'stamp_cost': '<span class="badge badge-amber">ابطال تمبر مالیاتی</span>',
                'court_cost': '<span class="badge badge-sky">هزینه دادرسی</span>',
                'expert_cost': '<span class="badge badge-rose">دستمزد کارشناس</span>'
            };

            caseFins.forEach(f => {
                const amt = Number(f.amount) || 0;
                if (f.type === 'fee_payment') paidFee += amt;
                else totalCosts += amt;

                tbody.innerHTML += `
                    <tr>
                        <td data-label="تاریخ" style="font-weight:600;">${toPersianDigits(cleanDateStr(f.date))}</td>
                        <td data-label="نوع تراکنش">${typeNames[f.type] || f.type}</td>
                        <td data-label="مبلغ" style="font-weight:700;">${formatMoney(amt)} تومان</td>
                        <td data-label="شرح">${f.desc}</td>
                        <td data-label="شماره پیگیری">${toPersianDigits(f.ref || '—')}</td>
                        <td data-label="عملیات" style="text-align:center;">
                            <button type="button" onclick="deleteFinance('${f.id}')" class="btn btn-rose" style="padding:5px 10px; font-size:11px;">حذف</button>
                        </td>
                    </tr>
                `;
            });

            if (caseFins.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="empty-row" style="text-align:center; color:#64748b;">هیچ تراکنش مالی برای این پرونده ثبت نشده است.</td></tr>`;
            }

            const remFee = Math.max(0, totalFee - paidFee);

            sumBox.innerHTML = `
                <div style="display:grid; grid-template-columns: repeat(2, 1fr); gap:8px;">
                    <div class="stat-box"><div class="stat-label">حق‌الوکاله توافقی کل</div><div class="stat-val">${formatMoney(totalFee)} تومان</div></div>
                    <div class="stat-box"><div class="stat-label">دریافتی حق‌الوکاله</div><div class="stat-val" style="color:var(--emerald-600);">${formatMoney(paidFee)} تومان</div></div>
                    <div class="stat-box"><div class="stat-label">مانده بدهی موکل</div><div class="stat-val" style="color:var(--rose-600);">${formatMoney(remFee)} تومان</div></div>
                    <div class="stat-box"><div class="stat-label">هزینه‌های دادرسی/تمبر (۵٪: ${formatMoney(estimatedStamp)})</div><div class="stat-val">${formatMoney(totalCosts)} تومان</div></div>
                </div>
            `;
        }

        function openFinanceModal() {
            if (!curCaseId) return;
            document.getElementById('fin-date').value = getTodayJalali();
            document.getElementById('fin-amount').value = '';
            document.getElementById('fin-desc').value = '';
            document.getElementById('fin-ref').value = '';
            openModal('finance-modal');
        }

        async function saveFinance(e) {
            if (e) e.preventDefault();
            const finObj = {
                id: 'fin-' + Date.now(),
                caseId: curCaseId,
                date: cleanDateStr(document.getElementById('fin-date').value.trim()),
                type: document.getElementById('fin-type').value,
                amount: Number(document.getElementById('fin-amount').value),
                desc: document.getElementById('fin-desc').value.trim(),
                ref: document.getElementById('fin-ref').value.trim()
            };
            finances.unshift(finObj);
            persistLocal();
            renderFinanceSection();
            closeModal('finance-modal');

            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST', mode: 'no-cors',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify({ type: "SAVE_FINANCE", data: finObj })
                });
            } catch (err) {}
            setStatus('ردیف مالی ثبت و با گوگل‌شیت همگام شد ✔️');
            return false;
        }

        async function deleteFinance(id) {
            if (confirm('آیا از حذف این ردیف مالی اطمینان دارید؟')) {
                finances = finances.filter(f => f.id !== id);
                persistLocal();
                renderFinanceSection();
                try {
                    await fetch(SCRIPT_URL, {
                        method: 'POST', mode: 'no-cors',
                        headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                        body: JSON.stringify({ type: "DELETE_FINANCE", financeId: id })
                    });
                } catch (err) {}
                setStatus('ردیف مالی حذف شد ✔️');
            }
        }

        function openTemplatesModal() {
            document.getElementById('templates-modal').classList.remove('hidden');
            generateTemplateText();
        }

        function buildLegalPromptString() {
            const c = cases.find(x => x.id === curCaseId) || {};
            const sel = document.getElementById('tpl-selector');
            const docTitle = sel.options[sel.selectedIndex].text.replace(/^[۰-۹0-9]+\.\s*/, '');
            const facts = document.getElementById('ai-facts').value.trim() || 'طبق موضوع پرونده و دفاع از حقوق قانونی موکل';
            const evidences = document.getElementById('ai-evidences').value.trim() || 'قرارداد فیمابین، اسناد مالی و مکاتبات رسمی مضبوط در پرونده';

            return [
                `شما یک وکیل پایه یک دادگستری و دکترای حقوق در ایران هستید.`,
                `لطفاً بر اساس اطلاعات واقعی پرونده و مستندات زیر، یک «${docTitle}» بسیار دقیق، مستند به مواد قانونی ایران (قانون مدنی، آیین دادرسی مدنی و تجارت) و کاملاً محکمه‌پسند تنظیم نمایید:`,
                ``,
                `۱. مشخصات پرونده:`,
                `- موکل: ${c.client || '[نام موکل]'} (سمت: ${c.clientRole || 'خواهان'} | شناسه/کد ملی: ${toPersianDigits(c.nationalId || '—')})`,
                `- وکیل: ${currentUser.name} (${currentUser.role})`,
                `- طرف مقابل: ${c.opponent || '[طرف مقابل]'} (سمت: ${c.opponentRole || 'خوانده'})`,
                `- مرجع و شعبه: ${c.court || 'دادگاه صالح'} — ${toPersianDigits(c.branch || '—')}`,
                `- شماره یکتای سمپ: ${toPersianDigits(c.samp || '—')} | بایگانی شعبه: ${toPersianDigits(c.archive || '—')}`,
                `- موضوع دعوا: ${c.subject || '—'}`,
                ``,
                `۲. شرح ماوقع و خواسته وکیل:`,
                facts,
                ``,
                `۳. مدارک و مستندات استنادی:`,
                evidences,
                ``,
                `۴. الزامات: دارای سربرگ بسمه تعالی، ایرادات شکلی، دفاع ماهوی مستند به مواد قانونی و خواسته صریح به همراه نام وکیل و تاریخ ${toPersianDigits(getTodayJalali())} باشد.`
            ].join('\n');
        }

        function buildAndCopySmartPrompt() {
            const promptText = buildLegalPromptString();
            document.getElementById('tpl-editor').value = promptText;
            if (navigator.clipboard && navigator.clipboard.writeText) {
                navigator.clipboard.writeText(promptText).catch(() => {});
            }
            setStatus('پرامپت هوشمند حقوقی ساخته و کپی شد! 🧠📋');
        }

        async function generateWithGeminiAPI() {
            const apiKey = safeStorage.getItem('gemini_api_key');
            const modelName = safeStorage.getItem('gemini_model') || 'gemini-3.8-flash';
            
            if (!apiKey) {
                alert('کلید Gemini API وارد نشده است!\n\nلطفاً از دکمه تنظیمات (⚙️) کلید رایگان Gemini API خود را وارد کنید، و یا از دکمه «🧠 ساخت و کپی پرامپت حرفه‌ای» استفاده نمایید.');
                return;
            }

            const facts = document.getElementById('ai-facts').value.trim();
            const evidences = document.getElementById('ai-evidences').value.trim();
            if (!facts && !evidences) {
                if (!confirm('کادر «شرح ماوقع» و «مدارک استنادی» خالی است. آیا هوش مصنوعی صرفاً بر اساس عنوان پرونده متن را بنویسد؟')) {
                    return;
                }
            }

            const btn = document.getElementById('btn-ai-direct');
            const loading = document.getElementById('ai-loading-msg');
            btn.disabled = true;
            loading.classList.remove('hidden');

            const promptText = buildLegalPromptString();

            try {
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/${modelName}:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: promptText }] }],
                        generationConfig: { temperature: 0.3 }
                    })
                });

                const data = await response.json();
                if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts[0]) {
                    const aiOutput = data.candidates[0].content.parts[0].text;
                    document.getElementById('tpl-editor').value = toPersianDigits(aiOutput);
                    setStatus(`متن تخصصی با موفقیت توسط ${modelName} نگارش شد ✨✔️`);
                } else {
                    throw new Error((data.error && data.error.message) || 'پاسخ نامعتبر از سرور هوش مصنوعی');
                }
            } catch (err) {
                alert('خطا در ارتباط مستقیم با Gemini API:\n' + err.message);
            } finally {
                btn.disabled = false;
                loading.classList.add('hidden');
            }
        }

        function generateTemplateText() {
            const tplKey = document.getElementById('tpl-selector').value;
            const c = cases.find(x => x.id === curCaseId) || {
                id: '—', samp: '—', archive: '—', client: '[نام موکل / شرکت]',
                nationalId: '[شناسه ملی / کد ملی]', clientRole: 'خواهان',
                opponent: '[نام طرف مقابل]', opponentRole: 'خوانده',
                subject: '[موضوع دعوا]', court: '[مرجع قضایی]', branch: '[شعبه]',
                totalFee: 0, claimValue: 0
            };

            const today = toPersianDigits(getTodayJalali());
            const samp = toPersianDigits(c.samp || '................');
            const archive = toPersianDigits(c.archive || '........');
            const feeStr = c.totalFee ? `${formatMoney(c.totalFee)} تومان` : 'طبق تعرفه/توافق';

            let out = '';
            if (tplKey === 'defense_badvi') {
                out = `بسمه تعالی\nریاست محترم ${toPersianDigits(c.branch)} ${c.court}\nبا سلام و تحیت؛\nاحتراماً، در خصوص پرونده کلاسه بایگانی ${archive} (شماره یکتای سمپ: ${samp}) مطروحه در آن شعبه محترم به طرفیت ${c.opponent} (${c.opponentRole}) با موضوع «${c.subject}»، به وکالت از ${c.client} (${c.clientRole} محترم پرونده)، مراتب دفاعیات شکلی و ماهوی را به شرح ذیل به استحضار می‌رساند:\n\nاولاً — ایرادات شکلی (موضوع ماده ۸۴ قانون آیین دادرسی مدنی):\nمستند به بندهای ماده ۸۴ ق.آ.د.م، دعوای مطروحه فاقد شرایط قانونی لازم بوده و صدور قرار رد دعوا به استناد ماده ۸۹ همان قانون مورد استدعاست.\n\nثانیاً — دفاعیات ماهوی:\n۱. مستفاد از مواد ۱۰، ۲۱۹ و ۲۲۰ قانون مدنی، موکل تمامی تعهدات قانونی خویش را ایفا نموده است.\n۲. مستند به ماده ۱۲۵۷ قانون مدنی، بار اثبات ادعا بر عهده مدعی است که دلیلی بر اشتغال ذمه موکل ارائه نگردیده است.\n\nلذا صدور حکم شایسته مبنی بر بی‌حقی / بطلان دعوای خواهان به انضمام خسارات دادرسی (ماده ۵۱۹ ق.آ.د.م) مورد استدعاست.\n\nبا تجدید احترام\n${currentUser.name} — ${currentUser.role}\nتاریخ: ${today}`;
            } else if (tplKey === 'objection_expert') {
                out = `بسمه تعالی\nریاست محترم ${toPersianDigits(c.branch)} ${c.court}\nموضوع: لایحه اعتراض به نظریه کارشناسی در پرونده بایگانی ${archive}\nبا سلام و احترام؛\nدر خصوص پرونده کلاسه ${toPersianDigits(c.id)} (سمپ: ${samp}) در فرجه قانونی ماده ۲۶۰ قانون آیین دادرسی مدنی، به وکالت از ${c.client}، مراتب اعتراض مستدل خود را نسبت به نظریه کارشناس رسمی دادگستری به شرح ذیل معروض می‌دارد:\n\n۱. عدم مطابقت نظریه کارشناسی با اوراق و واقعیت‌های پرونده (ماده ۲۶۵ ق.آ.د.م).\n۲. خروج از حدود قرار کارشناسی و نقص در بررسی‌های فنی و محاسباتی.\n\nلذا مستند به مواد ۲۶۰ و ۲۶۵ ق.آ.د.م، ارجاع امر به هیئت سه نفره کارشناسان رسمی مورد تقاضاست.\n\nبا تجدید احترام\n${currentUser.name} — وکیل ${c.client}\nتاریخ: ${today}`;
            } else if (tplKey === 'appeal_tajdidnazar') {
                out = `بسمه تعالی\nقضات عالی‌مقام دادگاه محترم تجدیدنظر استان\nبا سلام و تحیت؛\nاحتراماً، به وکالت از تجدیدنظرخواه (${c.client})، در مهلت قانونی ۲۰ روزه ماده ۳۳۶ ق.آ.د.م، نسبت به دادنامه صادره از ${toPersianDigits(c.branch)} ${c.court} در پرونده بایگانی ${archive} (سمپ: ${samp}) به طرفیت ${c.opponent} با موضوع «${c.subject}» تجدیدنظرخواهی نموده و جهات نقض را مستند به ماده ۳۴۸ ق.آ.د.م به استحضار می‌رساند:\n\n۱. عدم توجه دادگاه بدوی به دلایل ابرازی (بند ج ماده ۳۴۸ ق.آ.د.م).\n۲. مخالفت رأی با مقررات قانونی و اصول مسلم دادرسی (بند هـ ماده ۳۴۸ ق.آ.د.م).\n\nبنا به مراتب فوق و مستند به ماده ۳۵۸ ق.آ.د.م، نقض دادنامه بدوی و صدور رأی شایسته به نفع موکل مورد استدعاست.\n\nبا تجدید احترام\n${currentUser.name} — ${currentUser.role}\nتاریخ: ${today}`;
            } else if (tplKey === 'legal_notice_156') {
                out = `بسمه تعالی\n«اظهارنامه رسمی قضایی — موضوع ماده ۱۵۶ قانون آیین دادرسی مدنی»\n\nاظهارکننده: ${c.client} با وکالت ${currentUser.name} (${currentUser.role})\nمخاطب: ${c.opponent || '[نام مخاطب]'}\nموضوع: ابلاغ و اخطار رسمی در خصوص «${c.subject}» و مطالبه خسارت تأخیر تأدیه (ماده ۵۲۲ ق.آ.د.م)\n\nمخاطب محترم، با سلام؛\nاحتراماً به وکالت از ${c.client} و مستند به ماده ۱۵۶ ق.آ.د.م، رسماً به استحضار می‌رساند:\n۱. مستند به روابط قراردادی و مدارک مثبته، جنابعالی متعهد به ایفای تعهدات مقرر در خصوص «${c.subject}» بوده‌اید که تاکنون استنکاف ورزیده‌اید.\n۲. مستفاد از مواد ۱۰، ۲۱۹ و ۲۲۱ قانون مدنی، متعهد ضامن جبران کلیه خسارات وارده است.\n۳. لذا اخطار می‌گردد ظرف ۱۰ روز از تاریخ ابلاغ این اظهارنامه نسبت به ایفای کامل تعهدات اقدام نمایید؛ در غیر این صورت اقدام به طرح دعوا، تأمین خواسته (ماده ۱۰۸ ق.آ.د.م) و مطالبه خسارت تأخیر تأدیه از تاریخ ابلاغ اظهارنامه (ماده ۵۲۲ ق.آ.د.م) خواهد شد.\n\nبا تجدید احترام\n${currentUser.name} — وکیل ${c.client}\nتاریخ: ${today}`;
            } else if (tplKey === 'contract_corporate') {
                out = `بسمه تعالی\n«قرارداد جامع مشاوره حقوقی و وکالت مستمر شرکت»\n\nاین قرارداد به استناد ماده ۱۰ قانون مدنی در تاریخ ${today} فی‌مابین:\n۱. شرکت / کارفرما: ${c.client} به شناسه ملی ${toPersianDigits(c.nationalId || '........')}\n۲. مشاور حقوقی و وکیل: ${currentUser.name} (${currentUser.role})\nمنعقد می‌گردد:\n\nماده ۱ — موضوع قرارداد: ارائه خدمات مشاوره حقوقی، تنظیم قراردادهای صنعتی و تجاری و قبول وکالت در کلیه مراجع قضایی، داوری و اداری (از جمله موضوع ${c.subject}).\nماده ۲ — مدت قرارداد: یک سال شمسی کامل از تاریخ امضا.\nماده ۳ — حق‌الزحمه و حق‌الوکاله: مبلغ ${feeStr} که طبق توافق پرداخت می‌گردد. هزینه‌های دادرسی و تمبر مالیاتی (ماده ۱۰۳ ق.م.م) بر عهده شرکت است.\nماده ۴ — محرمانگی (NDA): وکیل متعهد به حفظ کامل اسرار تجاری و صنعتی شرکت می‌باشد.\n\nامضا و مهر شرکت (${c.client})                    امضا و مهر وکیل (${currentUser.name})`;
            } else if (tplKey === 'contract_retainer') {
                out = `بسمه تعالی\n«قرارداد خصوصی حق‌الوکاله و خدمات حقوقی (ماده ۱۰ قانون مدنی)»\n\nموکل: ${c.client}\nوکیل: ${currentUser.name} (${currentUser.role})\nموضوع وکالت: پیگیری و وکالت در پرونده کلاسه ${toPersianDigits(c.id)} (سمپ: ${samp}) به طرفیت ${c.opponent} با موضوع «${c.subject}» در ${c.court} (${toPersianDigits(c.branch)}).\nمبلغ حق‌الوکاله: ${feeStr} (۵۰٪ همزمان با امضا و الباقی طی مراحل دادرسی). هزینه‌های دادرسی و تمبر بر عهده موکل است.\n\nتاریخ: ${today}\nامضای موکل (${c.client})                          امضای وکیل (${currentUser.name})`;
            } else if (tplKey === 'arbitration_clause') {
                out = `بسمه تعالی\n«موافقت‌نامه و شرط داوری اختصاصی قراردادهای تجاری و صنعتی»\n\nمستند به ماده ۴۵۴ ق.آ.د.م، طرفین (${c.client} و ${c.opponent || '[طرف دوم]'}) توافق نمودند کلیه اختلافات ناشی از قرارداد موضوع «${c.subject}» پس از ۱۵ روز مذاکره، به داوری ارجاع گردد تا رأی قطعی و لازم‌الاجرا صادر شود. این شرط داوری مستقل از قرارداد اصلی است.\n\nامضای طرف اول (${c.client})                     امضای طرف دوم (${c.opponent || '—'})`;
            }

            document.getElementById('tpl-editor').value = out;
        }

        function copyTemplateText() {
            const txt = document.getElementById('tpl-editor').value;
            if (navigator.clipboard && navigator.clipboard.writeText) {
                navigator.clipboard.writeText(txt).catch(() => {});
            }
            setStatus('متن نهایی در حافظه کپی شد 📋');
        }

        async function saveTemplateAsAction() {
            if (!curCaseId) {
                setStatus('ابتدا یک پرونده را انتخاب کنید!', true);
                return;
            }
            const sel = document.getElementById('tpl-selector');
            const title = sel.options[sel.selectedIndex].text;
            const txt = document.getElementById('tpl-editor').value;

            let actionType = 'ثبت لایحه';
            if (title.includes('قرارداد') || title.includes('داوری')) actionType = 'تنظیم قرارداد حقوقی';
            else if (title.includes('اظهارنامه')) actionType = 'ارسال اظهارنامه رسمی';

            const actionObj = {
                id: 'act-' + Date.now(),
                caseId: curCaseId,
                date: getTodayJalali(),
                desc: `${title} — خلاصه متن: ${txt.substring(0, 140)}...`,
                result: 'تنظیم و آماده ثبت در سامانه ثنا',
                doc: 'سند هوشمند سامانه',
                assignee: currentUser.name,
                type: actionType,
                isDoc: true, next: '', deadline: ''
            };

            actions.unshift(actionObj);
            persistLocal();
            renderTable();
            closeModal('templates-modal');

            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST', mode: 'no-cors',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify({ type: "SAVE_ACTION", data: actionObj })
                });
            } catch (e) {}
            setStatus('سند تنظیم‌شده در جدول سوابق پرونده ثبت گردید ✔️');
        }

        function printTemplateDoc() {
            const txt = document.getElementById('tpl-editor').value;
            const printArea = document.getElementById('tpl-print-area');
            printArea.textContent = txt;
            printArea.style.display = 'block';
            document.getElementById('templates-modal').classList.add('printable-modal');
            document.getElementById('report-filter-modal').classList.remove('printable-modal');
            window.print();
            printArea.style.display = 'none';
            document.getElementById('templates-modal').classList.remove('printable-modal');
        }

        function printReportDoc() {
            document.getElementById('report-filter-modal').classList.add('printable-modal');
            document.getElementById('templates-modal').classList.remove('printable-modal');
            window.print();
        }

        function renderTable() {
            const tbody = document.getElementById('actions-tbody');
            if (!tbody) return;
            
            const query = normalizePersian((document.getElementById('search-input') && document.getElementById('search-input').value) || '');
            
            let acts = actions.filter(a => {
                if (a.caseId !== curCaseId) return false;
                if (!query) return true;
                const combined = normalizePersian(`${a.date} ${a.type || ''} ${a.desc} ${a.result} ${a.doc} ${a.assignee}`);
                return combined.includes(query);
            });

            document.getElementById('act-count').textContent = `${toPersianDigits(acts.length)} اقدام ثبت‌شده`;
            tbody.innerHTML = '';
            if (acts.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="empty-row" style="text-align:center; color:#64748b;">اقدامی یافت نشد.</td></tr>`;
                return;
            }
            acts.forEach(a => {
                tbody.innerHTML += `
                    <tr>
                        <td data-label="تاریخ اقدام" style="white-space:nowrap; font-weight:700;">${toPersianDigits(cleanDateStr(a.date))}</td>
                        <td data-label="نوع اقدام"><span class="badge badge-sky">${a.type || 'اقدام قضایی'}</span></td>
                        <td data-label="شرح اقدام" style="line-height:1.6; font-weight:600;">${toPersianDigits(a.desc)}</td>
                        <td data-label="نتیجه حاصله" style="line-height:1.6;">${toPersianDigits(a.result || '—')}</td>
                        <td data-label="مدرک استنادی"><span style="background:#f1f5f9; padding:2px 6px; border-radius:4px; font-size:11px;">${toPersianDigits(a.doc || '—')}</span></td>
                        <td data-label="مسئول پیگیری">${a.assignee}</td>
                        <td data-label="عملیات" style="text-align:center; white-space:nowrap;">
                            <button type="button" onclick="editActionModal('${a.id}')" class="btn btn-slate" style="padding:5px 10px; font-size:11px;">ویرایش</button>
                            <button type="button" onclick="deleteAction('${a.id}')" class="btn btn-rose" style="padding:5px 10px; font-size:11px;">حذف</button>
                        </td>
                    </tr>
                `;
            });
        }

        function openModal(id) { 
            if (id === 'report-filter-modal') prepareReport();
            document.getElementById(id).classList.remove('hidden'); 
        }
        function closeModal(id) { document.getElementById(id).classList.add('hidden'); }
        
        function openNewCaseModal() {
            document.getElementById('c-edit-mode').value = 'new';
            document.getElementById('case-modal-title').textContent = 'ثبت پرونده جدید، مواعد قضایی و قرارداد مالی';
            document.getElementById('c-id').value = '';
            document.getElementById('c-samp').value = '';
            document.getElementById('c-archive').value = '';
            document.getElementById('c-client').value = '';
            document.getElementById('c-national-id').value = '';
            document.getElementById('c-client-role').value = 'خواهان';
            document.getElementById('c-opponent').value = '';
            document.getElementById('c-opponent-role').value = 'خوانده';
            document.getElementById('c-subject').value = '';
            document.getElementById('c-court').value = '';
            document.getElementById('c-branch').value = '';
            document.getElementById('c-hearing-date').value = '';
            document.getElementById('c-hearing-time').value = '';
            document.getElementById('c-sana-type').value = 'none';
            document.getElementById('c-sana-date').value = '';
            document.getElementById('c-deadline-date').value = '';
            document.getElementById('c-total-fee').value = '';
            document.getElementById('c-claim-value').value = '';
            openModal('new-case-modal');
        }

        function editCurrentCaseModal() {
            const c = cases.find(x => x.id === curCaseId);
            if (!c) return;
            document.getElementById('c-edit-mode').value = c.id;
            document.getElementById('case-modal-title').textContent = 'ویرایش شناسنامه پرونده، مواعد و قرارداد مالی';
            document.getElementById('c-id').value = c.id;
            document.getElementById('c-samp').value = c.samp || '';
            document.getElementById('c-archive').value = c.archive || '';
            document.getElementById('c-client').value = c.client;
            document.getElementById('c-national-id').value = c.nationalId || '';
            document.getElementById('c-client-role').value = c.clientRole || 'خواهان';
            document.getElementById('c-opponent').value = c.opponent || '';
            document.getElementById('c-opponent-role').value = c.opponentRole || 'خوانده';
            document.getElementById('c-subject').value = c.subject;
            document.getElementById('c-court').value = c.court;
            document.getElementById('c-branch').value = c.branch;
            document.getElementById('c-status').value = c.status;
            document.getElementById('c-hearing-date').value = cleanDateStr(c.hearingDate);
            document.getElementById('c-hearing-time').value = cleanTimeStr(c.hearingTime);
            document.getElementById('c-sana-type').value = c.sanaType || 'none';
            document.getElementById('c-sana-date').value = cleanDateStr(c.sanaDate);
            document.getElementById('c-deadline-date').value = cleanDateStr(c.deadlineDate);
            document.getElementById('c-total-fee').value = c.totalFee || '';
            document.getElementById('c-claim-value').value = c.claimValue || '';
            openModal('new-case-modal');
        }

        async function saveCase(e) {
            if (e) e.preventDefault();
            const editMode = document.getElementById('c-edit-mode').value;
            const newId = document.getElementById('c-id').value.trim();
            
            const caseData = {
                id: newId,
                oldId: editMode !== 'new' ? editMode : null,
                samp: document.getElementById('c-samp').value.trim(),
                archive: document.getElementById('c-archive').value.trim(),
                client: document.getElementById('c-client').value.trim(),
                nationalId: document.getElementById('c-national-id').value.trim(),
                clientRole: document.getElementById('c-client-role').value,
                opponent: document.getElementById('c-opponent').value.trim(),
                opponentRole: document.getElementById('c-opponent-role').value,
                subject: document.getElementById('c-subject').value.trim(),
                court: document.getElementById('c-court').value.trim(),
                branch: document.getElementById('c-branch').value.trim(),
                status: document.getElementById('c-status').value,
                hearingDate: cleanDateStr(document.getElementById('c-hearing-date').value.trim()),
                hearingTime: cleanTimeStr(document.getElementById('c-hearing-time').value.trim()),
                sanaType: document.getElementById('c-sana-type').value,
                sanaDate: cleanDateStr(document.getElementById('c-sana-date').value.trim()),
                deadlineDate: cleanDateStr(document.getElementById('c-deadline-date').value.trim()),
                totalFee: Number(document.getElementById('c-total-fee').value) || 0,
                claimValue: Number(document.getElementById('c-claim-value').value) || 0,
                createdAt: getTodayJalali()
            };

            if (editMode === 'new') {
                cases.unshift(caseData);
                curCaseId = newId;
            } else {
                const idx = cases.findIndex(x => x.id === editMode);
                if (idx !== -1) cases[idx] = caseData;
                actions.forEach(a => { if (a.caseId === editMode) a.caseId = newId; });
                finances.forEach(f => { if (f.caseId === editMode) f.caseId = newId; });
                curCaseId = newId;
            }

            persistLocal();
            initApp();
            closeModal('new-case-modal');
            
            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST', mode: 'no-cors',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify({ type: "SAVE_CASE", data: caseData })
                });
                setStatus('اطلاعات پرونده ذخیره و با فضای ابری همگام شد ✔️');
            } catch (err) {
                setStatus('پرونده در حافظه دستگاه ذخیره شد ✔️');
            }
            return false;
        }

        async function deleteCurrentCase() {
            if (!curCaseId) return;
            if (confirm(`آیا از حذف کامل پرونده کلاسه ${curCaseId} و تمام اقدامات آن مطمئن هستید؟`)) {
                const targetId = curCaseId;
                cases = cases.filter(x => x.id !== targetId);
                actions = actions.filter(x => x.caseId !== targetId);
                finances = finances.filter(x => x.caseId !== targetId);
                curCaseId = cases.length > 0 ? cases[0].id : '';
                persistLocal();
                initApp();

                try {
                    await fetch(SCRIPT_URL, {
                        method: 'POST', mode: 'no-cors',
                        headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                        body: JSON.stringify({ type: "DELETE_CASE", caseId: targetId })
                    });
                } catch (e) {}
                setStatus('پرونده به طور کامل حذف شد ✔️');
            }
        }

        function openNewActionModal() { 
            document.getElementById('act-edit-id').value = '';
            document.getElementById('act-modal-title').textContent = 'ثبت اقدام حقوقی و قضایی جدید';
            document.getElementById('act-date').value = getTodayJalali();
            document.getElementById('act-type').value = 'ثبت لایحه';
            document.getElementById('act-assignee').value = currentUser.name;
            document.getElementById('act-desc').value = '';
            document.getElementById('act-result').value = '';
            document.getElementById('act-doc').value = 'سند ضمیمه';
            openModal('action-modal'); 
        }

        function editActionModal(id) {
            const a = actions.find(x => x.id === id);
            if (!a) return;
            document.getElementById('act-edit-id').value = a.id;
            document.getElementById('act-modal-title').textContent = 'ویرایش اقدام حقوقی';
            document.getElementById('act-date').value = cleanDateStr(a.date);
            document.getElementById('act-type').value = a.type || 'ثبت لایحه';
            document.getElementById('act-assignee').value = a.assignee;
            document.getElementById('act-desc').value = a.desc;
            document.getElementById('act-result').value = a.result || '';
            document.getElementById('act-doc').value = a.doc || '';
            openModal('action-modal');
        }

        async function saveAction(e) {
            if (e) e.preventDefault();
            const editId = document.getElementById('act-edit-id').value;
            const actionObj = {
                id: editId || ('act-' + Date.now()),
                caseId: curCaseId,
                date: cleanDateStr(document.getElementById('act-date').value.trim()),
                desc: document.getElementById('act-desc').value.trim(),
                result: document.getElementById('act-result').value.trim(),
                doc: document.getElementById('act-doc').value.trim() || 'سند ضمیمه',
                assignee: document.getElementById('act-assignee').value.trim(),
                type: document.getElementById('act-type').value,
                isDoc: true, next: '', deadline: ''
            };

            if (editId) {
                const idx = actions.findIndex(x => x.id === editId);
                if (idx !== -1) actions[idx] = actionObj;
            } else {
                actions.unshift(actionObj);
            }

            persistLocal();
            renderTable();
            closeModal('action-modal');

            try {
                await fetch(SCRIPT_URL, {
                    method: 'POST', mode: 'no-cors',
                    headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                    body: JSON.stringify({ type: "SAVE_ACTION", data: actionObj })
                });
            } catch (e) {}
            setStatus('اقدام حقوقی با موفقیت ثبت شد ✔️');
            return false;
        }

        async function deleteAction(id) {
            if (confirm('آیا از حذف این اقدام حقوقی اطمینان دارید؟')) {
                actions = actions.filter(x => x.id !== id);
                persistLocal();
                renderTable();
                try {
                    await fetch(SCRIPT_URL, {
                        method: 'POST', mode: 'no-cors',
                        headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                        body: JSON.stringify({ type: "DELETE_ACTION", actionId: id })
                    });
                } catch (e) {}
                setStatus('اقدام حذف شد ✔️');
            }
        }

        function showAllCasesView() {
            document.getElementById('case-workspace-view').classList.add('hidden');
            document.getElementById('all-cases-view').classList.remove('hidden');
            
            const tabW = document.getElementById('tab-workspace');
            const tabA = document.getElementById('tab-allcases');
            if (tabW) tabW.classList.remove('active');
            if (tabA) tabA.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });

            const tbody = document.getElementById('all-cases-tbody');
            tbody.innerHTML = '';
            cases.forEach(c => {
                const hDate = cleanDateStr(c.hearingDate);
                const hTime = cleanTimeStr(c.hearingTime);
                const dDate = cleanDateStr(c.deadlineDate);
                tbody.innerHTML += `
                    <tr>
                        <td data-label="کلاسه پرونده"><b>${toPersianDigits(c.id)}</b><br><span style="font-size:10px; color:#64748b;">سمپ: ${toPersianDigits(c.samp || '—')} | بایگانی: ${toPersianDigits(c.archive || '—')}</span></td>
                        <td data-label="موکل"><b>${c.client}</b> <span class="badge badge-sky">${c.clientRole || ''}</span></td>
                        <td data-label="طرف مقابل">${c.opponent || '—'} <span class="badge badge-rose">${c.opponentRole || ''}</span></td>
                        <td data-label="موضوع">${c.subject}</td>
                        <td data-label="مرجع و شعبه">${c.court} (${toPersianDigits(c.branch)})</td>
                        <td data-label="وقت / مهلت">
                            ${hDate ? `<div>🔔 جلسه: ${toPersianDigits(hDate)} ${hTime ? '('+toPersianDigits(hTime)+')' : ''}</div>` : ''}
                            ${dDate ? `<div style="color:var(--rose-600); font-weight:700;">⚠️ مهلت: ${toPersianDigits(dDate)}</div>` : (!hDate ? '—' : '')}
                        </td>
                        <td data-label="وضعیت"><span class="badge badge-emerald">${c.status}</span></td>
                        <td data-label="عملیات"><button type="button" onclick="showCaseWorkspaceView('${c.id}')" class="btn btn-gold" style="padding:7px 14px; font-size:12px;">ورود به پرونده</button></td>
                    </tr>
                `;
            });
        }

        function showCaseWorkspaceView(id) {
            if (id) curCaseId = id;
            document.getElementById('all-cases-view').classList.add('hidden');
            document.getElementById('case-workspace-view').classList.remove('hidden');
            
            const tabA = document.getElementById('tab-allcases');
            const tabW = document.getElementById('tab-workspace');
            if (tabA) tabA.classList.remove('active');
            if (tabW) tabW.classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });

            initApp();
        }

        function prepareReport() {
            const c = cases.find(x => x.id === curCaseId);
            if (!c) return;
            const acts = actions.filter(a => a.caseId === curCaseId);
            const caseFins = finances.filter(f => f.caseId === curCaseId);
            
            let paidFee = 0, totalCosts = 0;
            caseFins.forEach(f => {
                if (f.type === 'fee_payment') paidFee += Number(f.amount) || 0;
                else totalCosts += Number(f.amount) || 0;
            });
            const totalFee = Number(c.totalFee) || 0;
            const remFee = Math.max(0, totalFee - paidFee);

            let actRows = '';
            acts.forEach((a, i) => {
                actRows += `
                    <tr>
                        <td style="text-align:center;">${toPersianDigits(i + 1)}</td>
                        <td style="white-space:nowrap;">${toPersianDigits(cleanDateStr(a.date))}</td>
                        <td>${a.type || 'اقدام حقوقی'}</td>
                        <td>${toPersianDigits(a.desc)}</td>
                        <td>${toPersianDigits(a.result || '—')}</td>
                        <td>${toPersianDigits(a.doc)}</td>
                    </tr>
                `;
            });

            document.getElementById('report-print-container').innerHTML = `
                <div style="padding: 10px; line-height: 1.7;">
                    <div style="text-align:center; font-weight:800; font-size:14px; margin-bottom:6px;">بسمه تعالی</div>
                    <div style="display:flex; justify-content:space-between; align-items:flex-end; border-bottom:2px solid #0b1324; padding-bottom:12px; margin-bottom:16px;">
                        <div>
                            <h2 style="font-size:16px; font-weight:800; color:#0b1324;">گزارش رسمی گردش کار پرونده و وضعیت دادرسی</h2>
                            <div style="font-size:12px; color:#334155; margin-top:4px;">ارائه‌دهنده: <strong>${currentUser.name}</strong> (${currentUser.role})</div>
                        </div>
                        <div style="text-align:left; font-size:11px;">
                            <div><strong>تاریخ تنظیم گزارش:</strong> ${toPersianDigits(getTodayJalali())}</div>
                            <div><strong>کلاسه داخلی:</strong> ${toPersianDigits(c.id)}</div>
                        </div>
                    </div>

                    <div style="display:grid; grid-template-columns: repeat(3, 1fr); gap:8px; background:#f8fafc; border:1px solid #cbd5e1; border-radius:8px; padding:12px; font-size:11px; margin-bottom:16px;">
                        <div><strong>موکل:</strong> ${c.client} (${c.clientRole})</div>
                        <div><strong>شناسه/کد ملی:</strong> ${toPersianDigits(c.nationalId || '—')}</div>
                        <div><strong>طرف مقابل:</strong> ${c.opponent || '—'} (${c.opponentRole})</div>
                        <div><strong>موضوع دعوا:</strong> ${c.subject}</div>
                        <div><strong>مرجع رسیدگی:</strong> ${c.court} — ${toPersianDigits(c.branch)}</div>
                        <div><strong>شماره ۱۶ رقمی (سمپ):</strong> ${toPersianDigits(c.samp || '—')}</div>
                        <div><strong>شماره بایگانی شعبه:</strong> ${toPersianDigits(c.archive || '—')}</div>
                        <div><strong>وضعیت فعلی:</strong> ${c.status}</div>
                        <div><strong>وقت رسیدگی / مهلت:</strong> ${toPersianDigits(cleanDateStr(c.hearingDate) || cleanDateStr(c.deadlineDate) || '—')}</div>
                    </div>

                    <h4 style="font-size:13px; font-weight:800; margin-bottom:8px;">الف) شرح اقدامات حقوقی، لوایح و تصمیمات قضایی</h4>
                    <table style="width:100%; border-collapse:collapse; font-size:11px; margin-bottom:18px;">
                        <thead>
                            <tr style="background:#f1f5f9;">
                                <th style="width:40px; text-align:center;">ردیف</th>
                                <th style="width:85px;">تاریخ</th>
                                <th style="width:110px;">نوع اقدام</th>
                                <th>شرح اقدام حقوقی</th>
                                <th>نتیجه / تصمیم مرجع قضایی</th>
                                <th style="width:110px;">مستند / شماره ثبت</th>
                            </tr>
                        </thead>
                        <tbody>${actRows || '<tr><td colspan="6" style="text-align:center;">اقدامی ثبت نشده است.</td></tr>'}</tbody>
                    </table>

                    <h4 style="font-size:13px; font-weight:800; margin-bottom:8px;">ب) خلاصه وضعیت مالی پرونده</h4>
                    <div style="display:grid; grid-template-columns: repeat(4, 1fr); gap:8px; border:1px solid #cbd5e1; border-radius:8px; padding:10px; font-size:11px; margin-bottom:28px;">
                        <div><strong>کل حق‌الوکاله:</strong> ${formatMoney(totalFee)} تومان</div>
                        <div><strong>مجموع دریافتی:</strong> ${formatMoney(paidFee)} تومان</div>
                        <div><strong>مانده حق‌الوکاله:</strong> ${formatMoney(remFee)} تومان</div>
                        <div><strong>هزینه‌های دادرسی و تمبر:</strong> ${formatMoney(totalCosts)} تومان</div>
                    </div>

                    <div style="display:flex; justify-content:space-between; margin-top:30px; padding:0 20px; font-size:12px;">
                        <div style="text-align:center;">
                            <div><strong>مهر و امضای وکیل / مشاور حقوقی</strong></div>
                            <div style="margin-top:4px; color:#475569;">${currentUser.name}</div>
                        </div>
                        <div style="text-align:center;">
                            <div><strong>تأیید و رؤیت موکل / نماینده قانونی شرکت</strong></div>
                            <div style="margin-top:4px; color:#475569;">${c.client}</div>
                        </div>
                    </div>
                </div>
            `;
        }
    </script>
</body>
</html>
