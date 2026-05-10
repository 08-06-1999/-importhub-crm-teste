<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ImportHub CRM</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
:root{
  --brand:#1a2332;--brand-mid:#243044;--accent:#c8a96e;--accent-light:#e8d5a8;--accent-dark:#a8893e;
  --bg:#f4f2ee;--bg2:#eceae5;--bg3:#e0ddd6;--white:#fff;
  --text:#1a2332;--text2:#4a5568;--text3:#8a97a8;
  --border:rgba(26,35,50,.1);--border2:rgba(26,35,50,.06);
  --red:#c0392b;--red-bg:#fdf0ee;--green:#1a7a4a;--green-bg:#eef7f2;
  --amber:#b5650d;--amber-bg:#fef8ee;--blue:#1a4a7a;--blue-bg:#eef3fa;
  --purple:#5a3a8a;--purple-bg:#f3eefa;
  --shadow:0 2px 12px rgba(26,35,50,.08);--shadow-lg:0 8px 32px rgba(26,35,50,.12);
  --radius:10px;--radius-lg:16px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--text);font-size:14px;line-height:1.6}
button,input,select,textarea{font-family:inherit}
button{cursor:pointer}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-thumb{background:var(--bg3);border-radius:3px}

/* ── LOGIN ── */
#login-screen{position:fixed;inset:0;background:var(--brand);display:flex;align-items:center;justify-content:center;z-index:1000;transition:opacity .4s}
#login-screen.hidden{opacity:0;pointer-events:none}
.login-box{width:380px;padding:48px 40px;background:var(--white);border-radius:var(--radius-lg);box-shadow:var(--shadow-lg)}
.login-logo{display:flex;align-items:center;gap:10px;margin-bottom:36px}
.login-logo-mark{width:38px;height:38px;background:var(--brand);border-radius:8px;display:flex;align-items:center;justify-content:center}
.login-logo-mark svg{width:22px;height:22px;fill:var(--accent)}
.login-logo-text{font-family:'DM Serif Display',serif;font-size:22px;color:var(--brand);letter-spacing:-.5px}
.login-logo-text span{color:var(--accent)}
.lf{margin-bottom:14px}
.lf label{display:block;font-size:12px;font-weight:500;color:var(--text2);margin-bottom:5px;text-transform:uppercase;letter-spacing:.5px}
.lf input{width:100%;padding:11px 14px;border:1.5px solid var(--border);border-radius:var(--radius);font-size:14px;color:var(--text);background:var(--bg);outline:none;transition:border-color .2s}
.lf input:focus{border-color:var(--accent);background:var(--white)}
.btn-login{width:100%;padding:13px;background:var(--brand);color:var(--white);border:none;border-radius:var(--radius);font-size:14px;font-weight:500;margin-top:8px;cursor:pointer;transition:background .2s}
.btn-login:hover{background:var(--brand-mid)}
.login-error{color:var(--red);font-size:12px;margin-top:8px;display:none}

/* ── APP ── */
#app{display:none;height:100vh;flex-direction:column}
#app.visible{display:flex}
.topbar{height:52px;background:var(--brand);display:flex;align-items:center;padding:0 20px;gap:16px;flex-shrink:0}
.topbar-logo{font-family:'DM Serif Display',serif;font-size:17px;color:var(--white);letter-spacing:-.3px}
.topbar-logo span{color:var(--accent)}
.topbar-nav{display:flex;gap:2px;flex:1;margin-left:24px}
.nav-btn{padding:7px 14px;border:none;background:transparent;color:rgba(255,255,255,.55);font-size:13px;border-radius:6px;transition:all .15s;cursor:pointer}
.nav-btn:hover{background:rgba(255,255,255,.08);color:rgba(255,255,255,.85)}
.nav-btn.active{background:rgba(200,169,110,.2);color:var(--accent)}
.topbar-right{display:flex;align-items:center;gap:10px;margin-left:auto}
.user-av{width:30px;height:30px;border-radius:50%;background:var(--accent);display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:600;color:var(--brand)}
.user-name{font-size:12px;color:rgba(255,255,255,.7)}
.btn-logout{padding:5px 12px;border:1px solid rgba(255,255,255,.15);background:transparent;color:rgba(255,255,255,.55);font-size:12px;border-radius:6px;cursor:pointer;transition:all .15s}
.btn-logout:hover{border-color:rgba(255,255,255,.3);color:rgba(255,255,255,.8)}

/* ── ALERT BADGE ON NAV ── */
.nav-badge{background:var(--red);color:#fff;border-radius:10px;padding:0 5px;font-size:10px;font-weight:600;margin-left:4px;vertical-align:middle}

/* ── CONTENT ── */
.content{flex:1;overflow:auto;padding:24px}
.page{display:none}
.page.active{display:block}
.page-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:20px}
.page-title{font-family:'DM Serif Display',serif;font-size:22px;color:var(--brand)}
.page-sub{font-size:13px;color:var(--text3);margin-top:2px}

/* ── BUTTONS ── */
.btn{padding:8px 16px;border-radius:var(--radius);font-size:13px;font-weight:500;border:none;display:inline-flex;align-items:center;gap:7px;cursor:pointer;transition:all .15s}
.btn-primary{background:var(--brand);color:var(--white)}
.btn-primary:hover{background:var(--brand-mid)}
.btn-accent{background:var(--accent);color:var(--brand)}
.btn-accent:hover{background:var(--accent-dark);color:var(--white)}
.btn-ghost{background:transparent;color:var(--text2);border:1.5px solid var(--border)}
.btn-ghost:hover{background:var(--bg2)}
.btn-danger{background:var(--red-bg);color:var(--red);border:1px solid rgba(192,57,43,.2)}
.btn-danger:hover{background:var(--red);color:var(--white)}
.btn-sm{padding:5px 10px;font-size:12px}

/* ── CARDS ── */
.card{background:var(--white);border-radius:var(--radius-lg);border:1px solid var(--border2);box-shadow:var(--shadow)}
.card-header{padding:14px 18px;border-bottom:1px solid var(--border2);display:flex;align-items:center;justify-content:space-between}
.card-title{font-size:13px;font-weight:600;color:var(--text)}
.card-body{padding:18px}

/* ── STATS ── */
.stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:20px}
.stat-card{background:var(--white);border-radius:var(--radius-lg);padding:16px 18px;border:1.5px solid var(--border2);box-shadow:var(--shadow);cursor:pointer;transition:all .15s}
.stat-card:hover{border-color:var(--accent-light);transform:translateY(-2px);box-shadow:0 6px 20px rgba(26,35,50,.1)}
.stat-card.active{border-color:var(--accent);background:rgba(200,169,110,.05)}
.stat-label{font-size:11px;font-weight:500;color:var(--text3);text-transform:uppercase;letter-spacing:.6px;margin-bottom:6px}
.stat-value{font-family:'DM Serif Display',serif;font-size:24px;color:var(--brand)}
.stat-sub{font-size:11px;color:var(--text3);margin-top:3px}

/* ── BADGES ── */
.badge{display:inline-flex;align-items:center;padding:2px 8px;border-radius:20px;font-size:11px;font-weight:500}
.badge-quality{background:#eef7f2;color:#1a7a4a}
.badge-bad{background:#fdf0ee;color:#c0392b}
.badge-budget{background:#fef8ee;color:#b5650d}
.badge-noqual{background:#f0eef7;color:#5a3a8a}
.badge-new{background:var(--blue-bg);color:var(--blue)}
.badge-gray{background:var(--bg2);color:var(--text2)}
.badge-green{background:var(--green-bg);color:var(--green)}
.badge-red{background:var(--red-bg);color:var(--red)}
.badge-amber{background:var(--amber-bg);color:var(--amber)}

/* ── ALERT ITEMS ── */
.alert-item{border-radius:var(--radius);padding:10px 14px;display:flex;align-items:flex-start;gap:10px;margin-bottom:8px;font-size:12px;line-height:1.5}
.alert-item:last-child{margin-bottom:0}
.alert-warn{background:var(--amber-bg);border:1px solid rgba(181,101,13,.2);color:var(--amber)}
.alert-danger{background:var(--red-bg);border:1px solid rgba(192,57,43,.2);color:var(--red)}
.alert-info{background:var(--blue-bg);border:1px solid rgba(26,74,122,.15);color:var(--blue)}
.alert-icon{font-size:14px;flex-shrink:0;margin-top:1px}
.alert-body{flex:1}
.alert-title{font-weight:600;margin-bottom:1px}
.alert-sub{opacity:.85}
.alert-action{font-size:11px;margin-top:5px;display:inline-flex;align-items:center;gap:4px;cursor:pointer;text-decoration:underline;opacity:.8}

/* ── PIPELINE ── */
.pipeline-wrap{display:flex;gap:10px;overflow-x:auto;padding-bottom:12px;align-items:flex-start}
.pipeline-col{min-width:200px;flex:0 0 200px}
.pipeline-col-head{padding:8px 10px;display:flex;align-items:center;justify-content:space-between;margin-bottom:6px}
.pipeline-col-name{font-size:10px;font-weight:600;color:var(--text2);text-transform:uppercase;letter-spacing:.5px}
.pipeline-col-count{background:var(--bg2);border-radius:10px;padding:1px 7px;font-size:10px;color:var(--text3)}
.pipeline-dot{width:7px;height:7px;border-radius:50%;display:inline-block;flex-shrink:0}
.stage-bar{height:2px;border-radius:1px;margin-bottom:6px;opacity:.25}
.deal-card{background:var(--white);border-radius:var(--radius);border:1px solid var(--border2);padding:10px 12px;margin-bottom:7px;cursor:pointer;transition:all .15s;box-shadow:var(--shadow);position:relative}
.deal-card:hover{border-color:var(--accent-light);transform:translateY(-1px)}
.deal-card.has-alert::after{content:'';position:absolute;top:8px;right:8px;width:7px;height:7px;border-radius:50%;background:var(--red)}
.deal-card.has-warn::after{background:var(--amber)}
.deal-name{font-size:12px;font-weight:500}
.deal-phone{font-size:10px;color:var(--text3);font-family:monospace}
.deal-car{font-size:11px;color:var(--text2);margin:5px 0 7px}
.deal-footer{display:flex;align-items:center;justify-content:space-between}
.deal-comercial{font-size:10px;color:var(--text3)}
.deal-days{font-size:10px;padding:2px 6px;border-radius:8px}
.days-ok{background:var(--green-bg);color:var(--green)}
.days-warn{background:var(--amber-bg);color:var(--amber)}
.days-danger{background:var(--red-bg);color:var(--red)}

/* ── TABLE ── */
.table-wrap{overflow-x:auto}
table{width:100%;border-collapse:collapse}
th{font-size:11px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.5px;padding:9px 13px;text-align:left;border-bottom:1px solid var(--border2);background:var(--bg)}
td{padding:10px 13px;border-bottom:1px solid var(--border2);font-size:13px;color:var(--text);vertical-align:middle}
tr:last-child td{border-bottom:none}
tr:hover td{background:var(--bg)}
.td-muted{color:var(--text3)}
.td-mono{font-family:monospace;font-size:11px}

/* ── MODAL ── */
.modal-overlay{position:fixed;inset:0;background:rgba(26,35,50,.45);display:none;align-items:center;justify-content:center;z-index:500;padding:20px;backdrop-filter:blur(2px)}
.modal-overlay.open{display:flex}
.modal{background:var(--white);border-radius:var(--radius-lg);width:100%;max-width:580px;max-height:90vh;overflow-y:auto;box-shadow:var(--shadow-lg)}
.modal-header{padding:18px 22px;border-bottom:1px solid var(--border2);display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;background:var(--white);z-index:1}
.modal-title{font-size:15px;font-weight:600}
.modal-close{width:28px;height:28px;border:none;background:var(--bg2);border-radius:6px;cursor:pointer;font-size:16px;color:var(--text2)}
.modal-body{padding:22px}
.modal-footer{padding:14px 22px;border-top:1px solid var(--border2);display:flex;justify-content:flex-end;gap:8px}

/* ── FORM ── */
.fg{margin-bottom:14px}
.fl{display:block;font-size:11px;font-weight:600;color:var(--text2);margin-bottom:4px;text-transform:uppercase;letter-spacing:.4px}
.fc{width:100%;padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius);font-size:13px;color:var(--text);background:var(--bg);outline:none;transition:border-color .2s}
.fc:focus{border-color:var(--accent);background:var(--white)}
.fr{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.fr3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
textarea.fc{resize:vertical;min-height:70px}
.fh{font-size:11px;color:var(--text3);margin-top:3px}
.fsec{font-size:11px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.6px;margin:18px 0 10px;padding-bottom:5px;border-bottom:1px solid var(--border2)}

/* ── DEAL DETAIL ── */
.detail-back{display:flex;align-items:center;gap:6px;color:var(--text3);font-size:12px;cursor:pointer;margin-bottom:14px;width:fit-content}
.detail-back:hover{color:var(--text)}
.detail-grid{display:grid;grid-template-columns:1fr 300px;gap:14px;align-items:start}

/* ── CHECKLIST ── */
.cl-section{font-size:11px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.5px;margin:14px 0 6px;padding-bottom:4px;border-bottom:1px solid var(--border2)}
.cl-section:first-child{margin-top:0}
.cl-item{display:flex;align-items:center;gap:8px;padding:6px 0;border-bottom:1px solid var(--border2)}
.cl-item:last-child{border-bottom:none}
.cl-box{width:17px;height:17px;border-radius:4px;border:1.5px solid var(--border);cursor:pointer;flex-shrink:0;display:flex;align-items:center;justify-content:center;transition:all .15s;font-size:10px}
.cl-box.checked{background:var(--green);border-color:var(--green);color:white;font-weight:700}
.cl-box.checked::after{content:'✓'}
.cl-box.na{background:var(--bg2);border-color:var(--bg3);font-size:9px;color:var(--text3)}
.cl-box.na::after{content:'N/A'}
.cl-lbl{font-size:12px;flex:1}
.cl-lbl.checked{color:var(--text3);text-decoration:line-through}
.cl-alert{font-size:10px;color:var(--red);margin-left:auto;flex-shrink:0}

/* ── PROGRESS ── */
.pipe-progress{display:flex;gap:3px;margin-bottom:14px}
.pp-step{flex:1;height:3px;border-radius:2px;background:var(--bg3)}
.pp-step.done{background:var(--green)}
.pp-step.current{background:var(--accent)}

/* ── TIMELINE ── */
.timeline{position:relative;padding-left:20px}
.timeline::before{content:'';position:absolute;left:5px;top:0;bottom:0;width:1px;background:var(--border2)}
.tl-item{position:relative;margin-bottom:10px}
.tl-dot{position:absolute;left:-17px;top:3px;width:9px;height:9px;border-radius:50%;border:2px solid var(--white);box-shadow:0 0 0 1px var(--border)}
.tl-dot.done{background:var(--green);box-shadow:0 0 0 1px var(--green)}
.tl-dot.alert{background:var(--red);box-shadow:0 0 0 1px var(--red)}
.tl-title{font-size:12px;font-weight:500}
.tl-date{font-size:11px;color:var(--text3)}

/* ── QUALIFICATION ── */
.qual-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.qual-opt{padding:12px;border-radius:var(--radius);border:2px solid var(--border);cursor:pointer;transition:all .15s;text-align:center}
.qual-opt:hover{border-color:var(--accent-light)}
.qual-opt.selected{border-color:var(--accent)}
.qual-opt.q-quality.selected{border-color:var(--green);background:var(--green-bg)}
.qual-opt.q-bad.selected{border-color:var(--red);background:var(--red-bg)}
.qual-opt.q-budget.selected{border-color:var(--amber);background:var(--amber-bg)}
.qual-opt.q-noqual.selected{border-color:var(--purple);background:var(--purple-bg)}
.qual-icon{font-size:18px;margin-bottom:3px}
.qual-name{font-size:12px;font-weight:600;margin-bottom:2px}
.qual-desc{font-size:10px;color:var(--text3)}

/* ── FOLLOWUP ── */
.fu-item{display:flex;align-items:center;justify-content:space-between;padding:7px 0;border-bottom:1px solid var(--border2)}
.fu-item:last-child{border-bottom:none}
.fu-label{font-size:12px;display:flex;align-items:center;gap:7px}
.fu-actions{display:flex;gap:4px}

/* ── WA / EMAIL ── */
.btn-wa{background:#25D366;color:#fff;display:inline-flex;align-items:center;gap:4px;padding:4px 9px;border-radius:6px;font-size:11px;font-weight:500;border:none;cursor:pointer}
.btn-wa:hover{background:#1da851}
.btn-em{background:var(--brand);color:#fff;display:inline-flex;align-items:center;gap:4px;padding:4px 9px;border-radius:6px;font-size:11px;font-weight:500;border:none;cursor:pointer}
.btn-em:hover{background:var(--brand-mid)}

/* ── ADMIN ── */
.admin-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-bottom:20px}
.admin-card{background:var(--white);border-radius:var(--radius-lg);padding:18px;border:1px solid var(--border2);cursor:pointer;transition:all .15s;box-shadow:var(--shadow)}
.admin-card:hover{border-color:var(--accent-light);transform:translateY(-2px)}
.admin-card-icon{font-size:26px;margin-bottom:8px}
.admin-card-title{font-size:13px;font-weight:600;margin-bottom:3px}
.admin-card-desc{font-size:11px;color:var(--text3)}

/* ── EMPTY ── */
.empty{text-align:center;padding:36px 20px;color:var(--text3)}
.empty-icon{font-size:30px;margin-bottom:8px;opacity:.4}
.empty-title{font-size:13px;font-weight:500;color:var(--text2)}

/* ── ALERTS PAGE ── */
.alerts-page-header{display:flex;align-items:center;gap:10px;margin-bottom:6px}
.alerts-group{margin-bottom:20px}
.alerts-group-title{font-size:12px;font-weight:600;color:var(--text2);text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px;display:flex;align-items:center;gap:8px}
.alerts-count-badge{background:var(--red);color:#fff;border-radius:10px;padding:1px 7px;font-size:10px;font-weight:600}
.alerts-count-badge.warn{background:var(--amber)}
</style>
</head>
<body>

<!-- LOGIN -->
<div id="login-screen">
  <div class="login-box">
    <div class="login-logo">
      <div class="login-logo-mark"><svg viewBox="0 0 24 24"><path d="M12 2L4 6v6c0 5.5 3.5 10.7 8 12 4.5-1.3 8-6.5 8-12V6l-8-4z"/></svg></div>
      <div class="login-logo-text">Import<span>Hub</span></div>
    </div>
    <div style="font-size:16px;font-weight:500;margin-bottom:5px">Acesso à plataforma</div>
    <div style="font-size:13px;color:var(--text3);margin-bottom:26px">Introduza as suas credenciais</div>
    <div class="lf"><label>Utilizador</label><input type="text" id="login-user" placeholder="nome de utilizador" autocomplete="username"></div>
    <div class="lf"><label>Palavra-passe</label><input type="password" id="login-pass" placeholder="••••••••" autocomplete="current-password"></div>
    <button class="btn-login" onclick="doLogin()">Entrar</button>
    <div class="login-error" id="login-error">Credenciais incorretas. Tente novamente.</div>
  </div>
</div>

<!-- APP -->
<div id="app">
  <nav class="topbar">
    <div class="topbar-logo">Import<span>Hub</span></div>
    <div class="topbar-nav" id="topbar-nav"></div>
    <div class="topbar-right">
      <div class="user-av" id="user-av">IH</div>
      <div class="user-name" id="user-name-lbl"></div>
      <button class="btn-logout" onclick="doLogout()">Sair</button>
    </div>
  </nav>
  <div class="content">
    <!-- DASHBOARD -->
    <div class="page" id="page-dashboard">
      <div class="page-header">
        <div><div class="page-title" id="dash-title">Dashboard</div><div class="page-sub" id="dash-sub"></div></div>
        <div style="display:flex;gap:8px">
          <button class="btn btn-ghost" onclick="openSimulateLead()">+ Simular lead</button>
          <button class="btn btn-accent" onclick="openNewDeal()">+ Novo Deal</button>
        </div>
      </div>

      <!-- 1. STATS — compact row -->
      <div class="stats-grid" id="stats-grid" style="margin-bottom:12px"></div>

      <!-- 2. CAIXA DE LEADS -->
      <div id="leads-summary-wrap" style="margin-bottom:12px">
        <div class="card" id="leads-summary-card" onclick="showPage('leads')" style="cursor:pointer;border:1.5px solid var(--border2);transition:all .15s" onmouseover="this.style.borderColor='var(--accent-light)'" onmouseout="this.style.borderColor='var(--border2)'">
          <div style="padding:12px 18px;display:flex;align-items:center;gap:16px;flex-wrap:wrap">
            <span style="font-size:18px">📬</span>
            <div style="flex:1">
              <div style="font-size:13px;font-weight:600;color:var(--text)">Caixa de Leads</div>
              <div style="font-size:11px;color:var(--text3);margin-top:1px">Clique para gerir todas as leads</div>
            </div>
            <div style="display:flex;gap:10px;flex-wrap:wrap" id="leads-summary-counts"></div>
            <span style="color:var(--text3);font-size:13px">→</span>
          </div>
        </div>
      </div>

      <!-- 3. O MEU DIA — compact card -->
      <div style="margin-bottom:12px">
        <div class="card" onclick="showPage('meudia')" style="cursor:pointer;border:1.5px solid var(--border2);transition:all .15s" onmouseover="this.style.borderColor='var(--accent-light)'" onmouseout="this.style.borderColor='var(--border2)'">
          <div style="padding:12px 18px;display:flex;align-items:center;gap:16px;flex-wrap:wrap">
            <span style="font-size:18px">📋</span>
            <div style="flex:1">
              <div style="font-size:13px;font-weight:600;color:var(--text)">O meu dia</div>
              <div style="font-size:11px;color:var(--text3);margin-top:1px" id="planner-date"></div>
            </div>
            <div style="display:flex;gap:8px;flex-wrap:wrap" id="planner-summary"></div>
            <span style="color:var(--text3);font-size:13px">→</span>
          </div>
        </div>
      </div>

      <!-- 4. DEALS + ALERTAS -->
      <div style="display:grid;grid-template-columns:1fr 300px;gap:16px;align-items:start">
        <div class="card">
          <div class="card-header">
            <span class="card-title" id="dash-list-title">Deals recentes</span>
            <div style="display:flex;gap:6px;align-items:center">
              <button class="btn btn-ghost btn-sm" id="dash-clear-filter" onclick="dashFilter(null)" style="display:none">× Limpar filtro</button>
              <button class="btn btn-ghost btn-sm" onclick="showPage('pipeline')">Ver pipeline →</button>
            </div>
          </div>
          <div style="padding:0" id="recent-wrap"></div>
        </div>
        <div class="card">
          <div class="card-header"><span class="card-title">⚠️ Alertas ativos</span><span id="dash-alert-count" class="badge badge-red" style="display:none"></span></div>
          <div style="padding:12px 14px;max-height:320px;overflow-y:auto" id="dash-alerts"></div>
        </div>
      </div>
    </div>

    <!-- O MEU DIA — página dedicada -->
    <div class="page" id="page-meudia">
      <div class="page-header">
        <div>
          <div class="page-title">O meu dia</div>
          <div class="page-sub" id="meudia-sub"></div>
        </div>
      </div>
      <!-- day tabs -->
      <div style="display:flex;gap:4px;background:var(--bg2);border-radius:var(--radius);padding:3px;width:fit-content;margin-bottom:16px" id="meudia-tabs"></div>
      <!-- task list -->
      <div id="meudia-list"></div>
    </div>

    <!-- LEADS PAGE -->
    <div class="page" id="page-leads">
      <div class="page-header">
        <div><div class="page-title">Leads</div><div class="page-sub" id="leads-page-sub">Caixa de entrada de leads</div></div>
        <div style="display:flex;gap:8px">
          <button class="btn btn-ghost" onclick="openSimulateLead()">+ Simular lead</button>
        </div>
      </div>

      <!-- COUNTER CARDS -->
      <div style="display:grid;grid-template-columns:repeat(5,1fr);gap:10px;margin-bottom:18px" id="leads-counters"></div>

      <!-- FILTERS -->
      <div style="display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap">
        <div style="display:flex;gap:4px;background:var(--bg2);border-radius:var(--radius);padding:3px" id="leads-filter-tabs"></div>
        <input class="fc" style="flex:1;min-width:160px;max-width:260px" id="leads-search" placeholder="Pesquisar nome, email ou carro..." oninput="renderLeadsPage()">
      </div>

      <!-- LEADS TABLE -->
      <div class="card">
        <div class="table-wrap">
          <table>
            <thead><tr><th>Lead</th><th>Contacto</th><th>Veículo</th><th>Orçamento</th><th>Origem</th><th>Estado</th><th>Comercial</th><th>Recebido</th><th></th></tr></thead>
            <tbody id="leads-tbody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- LEAD DETAIL PAGE -->
    <div class="page" id="page-lead-detail">
      <div class="detail-back" onclick="showPage('leads')">← Voltar às leads</div>
      <div id="lead-detail-content"></div>
    </div>

    <!-- PIPELINE -->
    <div class="page" id="page-pipeline">
      <div class="page-header">
        <div><div class="page-title">Pipeline</div><div class="page-sub" id="pipeline-sub"></div></div>
        <div style="display:flex;gap:8px">
          <select class="fc" style="width:auto;padding:7px 10px" id="pipeline-filter" onchange="renderPipeline()"><option value="">Todos os comerciais</option></select>
          <button class="btn btn-accent" onclick="openNewDeal()">+ Novo Deal</button>
        </div>
      </div>
      <div class="pipeline-wrap" id="pipeline-board"></div>
    </div>

    <!-- DEAL DETAIL -->
    <div class="page" id="page-deal-detail">
      <div class="detail-back" onclick="goBack()">← Voltar</div>
      <div id="deal-detail-content"></div>
    </div>

    <!-- ALERTAS -->
    <div class="page" id="page-alerts">
      <div class="page-header">
        <div><div class="page-title">Alertas</div><div class="page-sub">Ações pendentes por fase</div></div>
      </div>
      <div id="alerts-full-page"></div>
    </div>

    <!-- CONTACTOS -->
    <div class="page" id="page-contacts">
      <div class="page-header">
        <div><div class="page-title">Contactos</div><div class="page-sub">Clientes e leads</div></div>
        <div style="display:flex;gap:8px">
          <button class="btn btn-ghost" onclick="exportCSV('contacts')">↓ Exportar CSV</button>
          <button class="btn btn-accent" onclick="openNewContact()">+ Novo Contacto</button>
        </div>
      </div>
      <div style="display:flex;gap:8px;margin-bottom:14px">
        <input class="fc" style="flex:1" id="contact-search" placeholder="Pesquisar nome, telemóvel ou email..." oninput="renderContacts()">
        <select class="fc" style="width:auto;padding:7px 10px" id="contact-filter" onchange="renderContacts()"><option value="">Todos</option><option>Particular</option><option>Empresa</option></select>
      </div>
      <div class="card"><div class="table-wrap"><table>
        <thead><tr><th>Cliente</th><th>Telemóvel</th><th>Tipo</th><th>Email</th><th>Deals</th><th>Comercial</th><th></th></tr></thead>
        <tbody id="contacts-tbody"></tbody>
      </table></div></div>
    </div>

    <!-- VENDEDORES -->
    <div class="page" id="page-sellers">
      <div class="page-header">
        <div><div class="page-title">Vendedores</div><div class="page-sub" id="sellers-sub">Stands e contactos por marca</div></div>
        <div style="display:flex;gap:8px">
          <button class="btn btn-ghost" onclick="exportCSV('sellers')">↓ Exportar CSV</button>
          <button class="btn btn-accent" onclick="openNewSeller()">+ Novo Vendedor</button>
        </div>
      </div>
      <div style="display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap">
        <input class="fc" style="flex:1;min-width:180px" id="seller-search" placeholder="Pesquisar vendedor, stand ou localização..." oninput="renderSellers()">
        <select class="fc" style="width:auto;padding:7px 10px" id="seller-brand-filter" onchange="renderSellers()"><option value="">Todas as marcas</option></select>
        <select class="fc" style="width:auto;padding:7px 10px" id="seller-rating-filter" onchange="renderSellers()">
          <option value="">Todos os ratings</option>
          <option value="5">★★★★★ (5)</option>
          <option value="4">★★★★☆ (4+)</option>
          <option value="3">★★★☆☆ (3+)</option>
        </select>
      </div>
      <div class="card"><div class="table-wrap"><table>
        <thead><tr><th>Vendedor</th><th>Stand</th><th>Marca</th><th>Localização</th><th>Telefone</th><th>Email</th><th>Rating</th><th>Deals</th><th></th></tr></thead>
        <tbody id="sellers-tbody"></tbody>
      </table></div></div>
    </div>

    <!-- ADMIN -->
    <div class="page" id="page-admin">
      <div class="page-header"><div><div class="page-title">Administração</div><div class="page-sub">Gestão da plataforma</div></div></div>
      <div class="admin-grid">
        <div class="admin-card" onclick="adminSection('users')"><div class="admin-card-icon">👥</div><div class="admin-card-title">Utilizadores</div><div class="admin-card-desc">Gerir comerciais, operacional e admins</div></div>
        <div class="admin-card" onclick="adminSection('email')"><div class="admin-card-icon">📧</div><div class="admin-card-title">Integração Email IMAP</div><div class="admin-card-desc">Captura automática de leads</div></div>
        <div class="admin-card" onclick="adminSection('templates')"><div class="admin-card-icon">✉️</div><div class="admin-card-title">Templates</div><div class="admin-card-desc">Emails e WhatsApp por tipo de lead</div></div>
        <div class="admin-card" onclick="adminSection('alert-rules')"><div class="admin-card-icon">🔔</div><div class="admin-card-title">Regras de Alertas</div><div class="admin-card-desc">Configurar dias e condições</div></div>
        <div class="admin-card" onclick="adminSection('stats')"><div class="admin-card-icon">📊</div><div class="admin-card-title">Relatórios</div><div class="admin-card-desc">Performance por comercial</div></div>
        <div class="admin-card" onclick="adminSection('integration')"><div class="admin-card-icon">🔗</div><div class="admin-card-title">Integração CRM / WA</div><div class="admin-card-desc">API, webhooks, WhatsApp Business</div></div>
      </div>
      <div id="admin-section"></div>
    </div>
  </div>
</div>

<!-- MODAL NOVO DEAL -->
<div class="modal-overlay" id="modal-deal">
  <div class="modal">
    <div class="modal-header"><div class="modal-title">Novo Deal</div><button class="modal-close" onclick="closeModal('modal-deal')">×</button></div>
    <div class="modal-body">
      <div class="fsec">Cliente</div>
      <div class="fr"><div class="fg"><label class="fl">Nome completo *</label><input class="fc" id="nd-name" placeholder="Nome do cliente"></div><div class="fg"><label class="fl">Telemóvel (nº processo) *</label><input class="fc" id="nd-phone" placeholder="9XX XXX XXX"></div></div>
      <div class="fr"><div class="fg"><label class="fl">Email</label><input class="fc" id="nd-email" type="email" placeholder="email@exemplo.pt"></div><div class="fg"><label class="fl">Tipo</label><select class="fc" id="nd-type"><option>Particular</option><option>Empresa</option></select></div></div>
      <div class="fsec">Veículo pretendido</div>
      <div class="fr"><div class="fg"><label class="fl">Marca</label><input class="fc" id="nd-brand" placeholder="BMW"></div><div class="fg"><label class="fl">Modelo</label><input class="fc" id="nd-model" placeholder="Serie 3 320d"></div></div>
      <div class="fr3"><div class="fg"><label class="fl">Ano</label><input class="fc" id="nd-year" placeholder="2021"></div><div class="fg"><label class="fl">Km máx.</label><input class="fc" id="nd-km" placeholder="80.000"></div><div class="fg"><label class="fl">Orçamento €</label><input class="fc" id="nd-budget" placeholder="30.000"></div></div>
      <div class="fsec">Atribuição</div>
      <div class="fr"><div class="fg"><label class="fl">Comercial *</label><select class="fc" id="nd-comercial"></select></div><div class="fg"><label class="fl">Origem</label><select class="fc" id="nd-source"><option>Formulário website</option><option>Email direto</option><option>WhatsApp</option><option>Referência</option><option>Redes sociais</option><option>Outro</option></select></div></div>
      <div class="fg"><label class="fl">Observações</label><textarea class="fc" id="nd-notes" placeholder="Notas..."></textarea></div>
    </div>
    <div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-deal')">Cancelar</button><button class="btn btn-accent" onclick="saveDeal()">Criar Deal</button></div>
  </div>
</div>

<!-- MODAL QUALIFICAÇÃO -->
<div class="modal-overlay" id="modal-qualify">
  <div class="modal" style="max-width:460px">
    <div class="modal-header"><div class="modal-title">Qualificar lead</div><button class="modal-close" onclick="closeModal('modal-qualify')">×</button></div>
    <div class="modal-body">
      <p style="font-size:12px;color:var(--text2);margin-bottom:14px">Selecione o tipo para definir o fluxo de follow-up automático.</p>
      <div class="qual-grid">
        <div class="qual-opt q-quality" onclick="selectQual('quality')"><div class="qual-icon">⭐</div><div class="qual-name">Lead de qualidade</div><div class="qual-desc">Follow-up completo + chamadas</div></div>
        <div class="qual-opt q-bad" onclick="selectQual('bad')"><div class="qual-icon">👎</div><div class="qual-name">Má lead</div><div class="qual-desc">Proposta + 1 follow-up email/WA</div></div>
        <div class="qual-opt q-budget" onclick="selectQual('budget')"><div class="qual-icon">💰</div><div class="qual-name">Falta de budget</div><div class="qual-desc">Proposta acima do orçamento</div></div>
        <div class="qual-opt q-noqual" onclick="selectQual('noqual')"><div class="qual-icon">🚫</div><div class="qual-name">Sem qualidade</div><div class="qual-desc">Email de recusa, sem proposta</div></div>
      </div>
      <div id="qual-info" style="margin-top:12px;padding:10px;background:var(--bg);border-radius:var(--radius);font-size:12px;color:var(--text2);display:none"></div>
      <div class="fg" style="margin-top:14px"><label class="fl">Link da proposta</label><input class="fc" id="qual-link" placeholder="https://proposta.importhub.pt/p/..."><div class="fh">Cole o link do software de propostas</div></div>
    </div>
    <div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-qualify')">Cancelar</button><button class="btn btn-accent" onclick="saveQual()">Confirmar</button></div>
  </div>
</div>

<!-- MODAL QUALIFICAR LEAD (a partir de lead respondida) -->
<div class="modal-overlay" id="modal-lead-qualify">
  <div class="modal" style="max-width:500px">
    <div class="modal-header">
      <div>
        <div class="modal-title">Qualificar e iniciar journey</div>
        <div style="font-size:11px;color:var(--text3);margin-top:2px" id="lq-lead-info"></div>
      </div>
      <button class="modal-close" onclick="closeModal('modal-lead-qualify')">×</button>
    </div>
    <div class="modal-body">
      <p style="font-size:12px;color:var(--text2);margin-bottom:14px">A qualificação cria automaticamente o deal e inicia o fluxo de follow-up.</p>
      <div class="qual-grid">
        <div class="qual-opt q-quality" onclick="selectLeadQual('quality')"><div class="qual-icon">⭐</div><div class="qual-name">Lead de qualidade</div><div class="qual-desc">Follow-up completo + chamadas</div></div>
        <div class="qual-opt q-bad" onclick="selectLeadQual('bad')"><div class="qual-icon">👎</div><div class="qual-name">Má lead</div><div class="qual-desc">Proposta + 1 follow-up email/WA</div></div>
        <div class="qual-opt q-budget" onclick="selectLeadQual('budget')"><div class="qual-icon">💰</div><div class="qual-name">Falta de budget</div><div class="qual-desc">Proposta acima do orçamento</div></div>
        <div class="qual-opt q-noqual" onclick="selectLeadQual('noqual')"><div class="qual-icon">🚫</div><div class="qual-name">Sem qualidade</div><div class="qual-desc">Email de recusa, sem deal</div></div>
      </div>
      <div id="lq-info" style="margin-top:12px;padding:10px;background:var(--bg);border-radius:var(--radius);font-size:12px;color:var(--text2);display:none"></div>
      <div class="fg" style="margin-top:14px"><label class="fl">Link da proposta (opcional)</label>
        <input class="fc" id="lq-link" placeholder="https://proposta.importhub.pt/p/...">
        <div class="fh">Pode adicionar depois na ficha do deal</div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeModal('modal-lead-qualify')">Cancelar</button>
      <button class="btn btn-accent" id="lq-confirm-btn" onclick="confirmLeadQual()" disabled>Confirmar e criar deal →</button>
    </div>
  </div>
</div>

<!-- MODAL CONTACTO -->
<div class="modal-overlay" id="modal-contact">
  <div class="modal" style="max-width:440px">
    <div class="modal-header"><div class="modal-title" id="contact-modal-title">Novo Contacto</div><button class="modal-close" onclick="closeModal('modal-contact')">×</button></div>
    <div class="modal-body">
      <div class="fr"><div class="fg"><label class="fl">Nome *</label><input class="fc" id="nc-name"></div><div class="fg"><label class="fl">Telemóvel *</label><input class="fc" id="nc-phone"></div></div>
      <div class="fr"><div class="fg"><label class="fl">Email</label><input class="fc" id="nc-email" type="email"></div><div class="fg"><label class="fl">Tipo</label><select class="fc" id="nc-type"><option>Particular</option><option>Empresa</option></select></div></div>
      <div class="fg"><label class="fl">Empresa</label><input class="fc" id="nc-company"></div>
      <div class="fg"><label class="fl">Notas</label><textarea class="fc" id="nc-notes"></textarea></div>
    </div>
    <div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-contact')">Cancelar</button><button class="btn btn-accent" onclick="saveContact()">Guardar</button></div>
  </div>
</div>

<!-- MODAL VENDEDOR -->
<div class="modal-overlay" id="modal-seller">
  <div class="modal" style="max-width:520px">
    <div class="modal-header"><div class="modal-title" id="seller-modal-title">Novo Vendedor</div><button class="modal-close" onclick="closeModal('modal-seller')">×</button></div>
    <div class="modal-body">
      <div class="fr"><div class="fg"><label class="fl">Marca *</label><input class="fc" id="ns-brand" placeholder="Mercedes-Benz" list="ns-brand-list"><datalist id="ns-brand-list"></datalist></div><div class="fg"><label class="fl">Rating</label>
        <div style="display:flex;gap:6px;align-items:center;padding-top:6px" id="ns-rating-stars">
          <span class="star-btn" data-v="1" onclick="setSellerRating(1)" style="font-size:22px;cursor:pointer;opacity:.4">★</span>
          <span class="star-btn" data-v="2" onclick="setSellerRating(2)" style="font-size:22px;cursor:pointer;opacity:.4">★</span>
          <span class="star-btn" data-v="3" onclick="setSellerRating(3)" style="font-size:22px;cursor:pointer;opacity:.4">★</span>
          <span class="star-btn" data-v="4" onclick="setSellerRating(4)" style="font-size:22px;cursor:pointer;opacity:.4">★</span>
          <span class="star-btn" data-v="5" onclick="setSellerRating(5)" style="font-size:22px;cursor:pointer;opacity:.4">★</span>
          <span id="ns-rating-val" style="font-size:12px;color:var(--text3);margin-left:4px">0/5</span>
        </div>
      </div></div>
      <div class="fg"><label class="fl">Nome do vendedor *</label><input class="fc" id="ns-name" placeholder="Nome do vendedor"></div>
      <div class="fg"><label class="fl">Stand / Empresa *</label><input class="fc" id="ns-stand" placeholder="Nome do stand"></div>
      <div class="fr"><div class="fg"><label class="fl">Telefone</label><input class="fc" id="ns-phone" placeholder="+49 ..."></div><div class="fg"><label class="fl">Email</label><input class="fc" id="ns-email" type="email" placeholder="vendedor@stand.de"></div></div>
      <div class="fg"><label class="fl">Localização</label><input class="fc" id="ns-location" placeholder="DE-12345 Cidade"></div>
      <div class="fg"><label class="fl">Notas internas</label><textarea class="fc" id="ns-notes" placeholder="Observações sobre este vendedor..."></textarea></div>
    </div>
    <div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-seller')">Cancelar</button><button class="btn btn-accent" onclick="saveSeller()">Guardar</button></div>
  </div>
</div>

<!-- MODAL RATING OBRIGATÓRIO -->
<div class="modal-overlay" id="modal-rating">
  <div class="modal" style="max-width:400px">
    <div class="modal-header"><div class="modal-title">⭐ Avaliar o vendedor</div></div>
    <div class="modal-body">
      <p style="font-size:13px;color:var(--text2);margin-bottom:16px">Antes de avançar para "Entregue", avalie a experiência com este vendedor. É obrigatório.</p>
      <div id="rating-seller-info" style="padding:10px 12px;background:var(--bg);border-radius:var(--radius);margin-bottom:16px;font-size:13px"></div>
      <div style="display:flex;gap:8px;justify-content:center;margin-bottom:8px" id="rating-stars-row">
        <span onclick="setDealRating(1)" style="font-size:32px;cursor:pointer;opacity:.35" class="deal-star">★</span>
        <span onclick="setDealRating(2)" style="font-size:32px;cursor:pointer;opacity:.35" class="deal-star">★</span>
        <span onclick="setDealRating(3)" style="font-size:32px;cursor:pointer;opacity:.35" class="deal-star">★</span>
        <span onclick="setDealRating(4)" style="font-size:32px;cursor:pointer;opacity:.35" class="deal-star">★</span>
        <span onclick="setDealRating(5)" style="font-size:32px;cursor:pointer;opacity:.35" class="deal-star">★</span>
      </div>
      <div id="rating-label" style="text-align:center;font-size:12px;color:var(--text3);min-height:18px"></div>
    </div>
    <div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-rating')">Cancelar</button><button class="btn btn-accent" id="rating-confirm-btn" onclick="confirmRating()" disabled>Confirmar e avançar</button></div>
  </div>
</div>

<style>
/* Autocomplete */
.ac-wrap{position:relative}
.ac-list{position:absolute;top:100%;left:0;right:0;background:var(--white);border:1.5px solid var(--accent);border-top:none;border-radius:0 0 var(--radius) var(--radius);z-index:200;max-height:220px;overflow-y:auto;box-shadow:var(--shadow-lg)}
.ac-item{padding:9px 12px;font-size:13px;cursor:pointer;display:flex;flex-direction:column;gap:2px;border-bottom:0.5px solid var(--border2)}
.ac-item:last-child{border-bottom:none}
.ac-item:hover{background:var(--bg2)}
.ac-name{font-weight:500;color:var(--text)}
.ac-sub{font-size:11px;color:var(--text3)}
.ac-rating{font-size:11px;color:var(--amber)}
/* Stars */
.stars{color:var(--amber);font-size:13px;letter-spacing:1px}
.deal-star{transition:opacity .1s;color:var(--accent)}
</style>

<!-- MODAL CONVERTER LEAD -->
<div class="modal-overlay" id="modal-convert-lead">
  <div class="modal" style="max-width:680px">
    <div class="modal-header">
      <div class="modal-title">📬 Converter lead em deal</div>
      <button class="modal-close" onclick="closeModal('modal-convert-lead')">×</button>
    </div>
    <div class="modal-body">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">
        <!-- Email original -->
        <div>
          <div class="fsec" style="margin-top:0">Email original</div>
          <div id="lead-email-preview" style="background:var(--bg);border-radius:var(--radius);padding:14px;font-size:12px;line-height:1.8;color:var(--text2);border:1px solid var(--border2);max-height:380px;overflow-y:auto;white-space:pre-wrap;font-family:monospace"></div>
        </div>
        <!-- Dados do deal -->
        <div>
          <div class="fsec" style="margin-top:0">Dados do deal</div>
          <div class="fg"><label class="fl">Nome *</label><input class="fc" id="cl-name" placeholder="Nome do cliente"></div>
          <div class="fg"><label class="fl">Telemóvel *</label><input class="fc" id="cl-phone" placeholder="9XX XXX XXX"></div>
          <div class="fg"><label class="fl">Email</label><input class="fc" id="cl-email" type="email"></div>
          <div class="fr">
            <div class="fg"><label class="fl">Marca</label><input class="fc" id="cl-brand" placeholder="BMW"></div>
            <div class="fg"><label class="fl">Modelo</label><input class="fc" id="cl-model" placeholder="Série 3"></div>
          </div>
          <div class="fr">
            <div class="fg"><label class="fl">Ano desde</label><input class="fc" id="cl-year" placeholder="2020"></div>
            <div class="fg"><label class="fl">Km até</label><input class="fc" id="cl-km" placeholder="80.000"></div>
          </div>
          <div class="fg"><label class="fl">Preço até (€)</label><input class="fc" id="cl-budget" placeholder="30.000"></div>
          <div class="fg"><label class="fl">Origem</label><input class="fc" id="cl-source" placeholder="Pesquisa Google"></div>
          <div class="fg"><label class="fl">Notas / Mensagem</label><textarea class="fc" id="cl-notes" style="min-height:55px"></textarea></div>
          <div class="fg"><label class="fl">Atribuir a</label><select class="fc" id="cl-comercial"></select></div>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-danger btn-sm" onclick="dismissLead()">Ignorar lead</button>
      <button class="btn btn-ghost" onclick="closeModal('modal-convert-lead')">Cancelar</button>
      <button class="btn btn-accent" onclick="convertLead()">Criar deal →</button>
    </div>
  </div>
</div>

<!-- MODAL SIMULAR LEAD -->
<div class="modal-overlay" id="modal-simulate-lead">
  <div class="modal" style="max-width:500px">
    <div class="modal-header">
      <div class="modal-title">Simular chegada de lead por email</div>
      <button class="modal-close" onclick="closeModal('modal-simulate-lead')">×</button>
    </div>
    <div class="modal-body">
      <p style="font-size:12px;color:var(--text2);margin-bottom:14px">Simula como o CRM recebe um email de lead. Escolhe o tipo para ver como aparece na caixa de entrada.</p>
      <div style="display:flex;gap:8px;margin-bottom:14px">
        <button class="btn btn-ghost btn-sm" onclick="simulateLead('form')" style="flex:1">📋 Formulário</button>
        <button class="btn btn-ghost btn-sm" onclick="simulateLead('free')" style="flex:1">✉️ Email direto</button>
      </div>
      <div class="fg"><label class="fl">Ou cola um email real aqui</label><textarea class="fc" id="sim-email-text" style="min-height:140px;font-family:monospace;font-size:12px" placeholder="Cola o conteúdo do email..."></textarea></div>
      <button class="btn btn-accent" style="width:100%;margin-top:4px" onclick="simulateLeadFromText()">Processar email →</button>
    </div>
  </div>
</div>

<!-- MODAL FOLLOW-UP MANUAL -->
<div class="modal-overlay" id="modal-manual-fu">
  <div class="modal" style="max-width:420px">
    <div class="modal-header">
      <div class="modal-title">Adicionar follow-up</div>
      <button class="modal-close" onclick="closeModal('modal-manual-fu')">×</button>
    </div>
    <div class="modal-body">
      <div id="mfu-deal-info" style="padding:10px 12px;background:var(--bg);border-radius:var(--radius);font-size:13px;margin-bottom:14px"></div>
      <div class="fg"><label class="fl">Tipo de contacto</label>
        <div style="display:flex;gap:8px">
          <label style="flex:1;display:flex;align-items:center;gap:7px;padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius);cursor:pointer;font-size:13px" id="mfu-type-call">
            <input type="radio" name="mfu-type" value="call" onchange="selectMfuType('call')"> 📞 Chamada
          </label>
          <label style="flex:1;display:flex;align-items:center;gap:7px;padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius);cursor:pointer;font-size:13px" id="mfu-type-ew">
            <input type="radio" name="mfu-type" value="email_wa" onchange="selectMfuType('email_wa')"> 📨 Email+WA
          </label>
          <label style="flex:1;display:flex;align-items:center;gap:7px;padding:9px 12px;border:1.5px solid var(--border);border-radius:var(--radius);cursor:pointer;font-size:13px" id="mfu-type-both">
            <input type="radio" name="mfu-type" value="both" onchange="selectMfuType('both')"> 📞📨 Ambos
          </label>
        </div>
      </div>
      <div class="fg"><label class="fl">Data</label>
        <input class="fc" type="date" id="mfu-date">
        <div class="fh">Deixe vazio para hoje</div>
      </div>
      <div class="fg"><label class="fl">Nota para si próprio</label>
        <textarea class="fc" id="mfu-note" placeholder="Ex: Cliente disse que decide na sexta. Ligar de manhã." style="min-height:70px"></textarea>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeModal('modal-manual-fu')">Cancelar</button>
      <button class="btn btn-accent" onclick="saveManualFU()">Guardar follow-up</button>
    </div>
  </div>
</div>

<!-- MODAL ADIAR TAREFA -->
<div class="modal-overlay" id="modal-snooze">
  <div class="modal" style="max-width:380px">
    <div class="modal-header">
      <div class="modal-title">⏰ Adiar tarefa</div>
      <button class="modal-close" onclick="closeModal('modal-snooze')">×</button>
    </div>
    <div class="modal-body">
      <div id="snooze-task-info" style="font-size:13px;color:var(--text2);margin-bottom:14px;padding:10px 12px;background:var(--bg);border-radius:var(--radius)"></div>
      <div class="fg">
        <label class="fl">Nota (motivo do adiamento)</label>
        <textarea class="fc" id="snooze-note" placeholder="Ex: Cliente disse que decide na sexta. Ligar de manhã." style="min-height:65px"></textarea>
      </div>
      <div class="fg"><label class="fl">Para quando?</label>
        <div style="display:flex;flex-direction:column;gap:6px">
          <button class="btn btn-ghost" onclick="snoozeTask('tomorrow')" style="justify-content:flex-start;font-size:13px">📅 Amanhã</button>
          <button class="btn btn-ghost" onclick="snoozeTask('2days')" style="justify-content:flex-start;font-size:13px">📅 Daqui a 2 dias úteis</button>
          <button class="btn btn-ghost" onclick="snoozeTask('nextweek')" style="justify-content:flex-start;font-size:13px">📅 Semana que vem</button>
          <div style="display:flex;gap:8px;align-items:center;margin-top:4px">
            <input class="fc" type="date" id="snooze-custom-date" style="flex:1">
            <button class="btn btn-accent" onclick="snoozeTask('custom')">Confirmar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
.task-row{background:var(--white);border-radius:var(--radius-lg);border:1px solid var(--border2);margin-bottom:8px;overflow:hidden;box-shadow:var(--shadow)}
.task-row-head{display:flex;align-items:center;padding:12px 16px;gap:12px}
.task-row-client{font-size:13px;font-weight:500;color:var(--text);flex:1}
.task-row-car{font-size:11px;color:var(--text2)}
.task-row-note{font-size:11px;color:var(--amber);background:var(--amber-bg);padding:4px 10px;border-radius:6px;margin:0 16px 10px;line-height:1.5}
.task-row-actions{display:flex;align-items:center;gap:6px;padding:8px 16px;border-top:1px solid var(--border2);background:var(--bg);flex-wrap:wrap}
.task-type-badge{font-size:11px;font-weight:600;padding:3px 9px;border-radius:10px}
.task-auto{background:var(--blue-bg);color:var(--blue)}
.task-manual{background:var(--purple-bg);color:var(--purple)}
.meudia-day-empty{text-align:center;padding:40px;color:var(--text3);font-size:13px}
</style>

<style>
.inbox-item:last-child{border-bottom:none}
.inbox-item:hover{background:var(--bg)}
.inbox-name{font-size:13px;font-weight:500;color:var(--text)}
.inbox-car{font-size:12px;color:var(--text2);margin-top:2px}
.inbox-meta{font-size:11px;color:var(--text3);margin-top:2px}
.inbox-badge{font-size:10px;padding:2px 7px;border-radius:10px;font-weight:500}
.inbox-form{background:#eef3fa;color:#1a4a7a}
.inbox-free{background:#fef8ee;color:#b5650d}
.lead-filter-tab{padding:5px 12px;border:none;background:transparent;border-radius:7px;font-size:12px;font-weight:500;color:var(--text2);cursor:pointer;transition:all .15s;white-space:nowrap}
.lead-filter-tab.active{background:var(--white);color:var(--text);box-shadow:var(--shadow)}
.lead-counter{background:var(--white);border-radius:var(--radius-lg);padding:12px 14px;border:1px solid var(--border2);cursor:pointer;transition:all .15s;text-align:center;box-shadow:var(--shadow)}
.lead-counter:hover{border-color:var(--accent-light);transform:translateY(-1px)}
.lead-counter.active{border-color:var(--accent);background:rgba(200,169,110,.05)}
.lead-counter-val{font-family:'DM Serif Display',serif;font-size:22px;color:var(--brand)}
.lead-counter-lbl{font-size:10px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:.5px;margin-top:3px}

/* Planner */
.planner-col{background:var(--white);border-radius:var(--radius-lg);border:1px solid var(--border2);box-shadow:var(--shadow);overflow:hidden}
.planner-col-head{padding:10px 14px;border-bottom:1px solid var(--border2);display:flex;align-items:center;justify-content:space-between}
.planner-col-title{font-size:12px;font-weight:600;color:var(--text)}
.planner-col-date{font-size:11px;color:var(--text3)}
.planner-col-count{font-size:10px;padding:1px 7px;border-radius:10px;font-weight:600}
.planner-task{padding:9px 14px;border-bottom:1px solid var(--border2);display:flex;flex-direction:column;gap:4px}
.planner-task:last-child{border-bottom:none}
.planner-task-name{font-size:12px;font-weight:500;color:var(--text)}
.planner-task-car{font-size:11px;color:var(--text2)}
.planner-task-actions{display:flex;gap:5px;margin-top:4px;flex-wrap:wrap}
.planner-task-type{display:flex;align-items:center;gap:5px;font-size:11px;font-weight:500;margin-bottom:4px}
.planner-section{padding:8px 14px 2px;font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.6px;color:var(--text3);background:var(--bg);border-bottom:1px solid var(--border2)}
.planner-empty{padding:20px 14px;text-align:center;font-size:12px;color:var(--text3)}
.planner-today .planner-col-head{background:rgba(200,169,110,.07)}
.task-done{opacity:.5;text-decoration:line-through}
</style>

<script>
// ══════════════════════════════════════════════════════
// DATA
// ══════════════════════════════════════════════════════
const USERS=[
  {id:'admin1',name:'Admin — José',pass:'admin1',role:'admin',initials:'JA',phone:'912000001'},
  {id:'admin2',name:'Admin — Ricardo',pass:'admin2',role:'admin',initials:'RA',phone:'912000002'},
  {id:'op1',name:'Operacional — Marta',pass:'op123',role:'op',initials:'MO',phone:'912000003'},
  {id:'ze',name:'Zé',pass:'ze123',role:'comercial',initials:'ZÉ',phone:'912111111'},
  {id:'rodrigo',name:'Rodrigo',pass:'rodrigo123',role:'comercial',initials:'RO',phone:'912222222'},
  {id:'joao',name:'João',pass:'joao123',role:'comercial',initials:'JO',phone:'912333333'},
  {id:'antonio',name:'António',pass:'antonio123',role:'comercial',initials:'AN',phone:'912444444'},
];

const STAGES=[
  {id:0,name:'Novo Pedido',color:'#1a4a7a',phase:'comercial'},
  {id:1,name:'Proposta em Preparação',color:'#b5650d',phase:'comercial'},
  {id:2,name:'Proposta Enviada',color:'#5a3a8a',phase:'comercial'},
  {id:3,name:'Negociação / Ajustes',color:'#1a3a7a',phase:'comercial'},
  {id:4,name:'Adjudicado (Sinal)',color:'#8b2500',phase:'comercial'},
  {id:5,name:'Compra Confirmada',color:'#1a7a4a',phase:'op'},
  {id:6,name:'Em Transporte',color:'#2d7a1a',phase:'op'},
  {id:7,name:'Chegada / Receção',color:'#0f6e56',phase:'op'},
  {id:8,name:'Legalização / ISV',color:'#3b6d11',phase:'op'},
  {id:9,name:'Pronto para Entrega',color:'#1a5a7a',phase:'op'},
  {id:10,name:'Entregue',color:'#4a7a1a',phase:'op'},
  {id:11,name:'Pós-venda',color:'#6a6a1a',phase:'op'},
  {id:99,name:'Fechado Perdido',color:'#888',phase:'lost'},
];

// Checklists completas por fase (replicadas do Excel VD + OP)
const CHECKLISTS={
  vd_proposta:[
    {key:'prop_id',label:'ID de proposta registado',alert:'Adjudicado sem proposta registada'},
  ],
  vd_docs:[
    {key:'doc_teil1',label:'Teil I'},
    {key:'doc_teil2',label:'Teil II'},
    {key:'doc_coc',label:'COC'},
    {key:'doc_manutencoes',label:'Manutenções'},
  ],
  vd_analise:[
    {key:'ana_mecanica',label:'Mecânica'},
    {key:'ana_acidentes',label:'Histórico de acidentes'},
    {key:'ana_chaves',label:'Chaves'},
    {key:'ana_cabos',label:'Cabos'},
    {key:'ana_danos',label:'Danos'},
    {key:'ana_garantias',label:'Garantias'},
    {key:'ana_baterias',label:'Baterias'},
    {key:'ana_vin',label:'Relatório VIN'},
    {key:'ana_stand',label:'Stand verificado'},
  ],
  vd_cliente:[
    {key:'cli_cc',label:'Cartão de Cidadão'},
    {key:'cli_morada',label:'Morada'},
    {key:'cli_certidao',label:'Certidão Permanente (empresas)'},
  ],
  vd_contrato:[
    {key:'cont_revisao',label:'Revisão do contrato'},
    {key:'cont_email_fecho',label:'Email de fecho enviado'},
    {key:'cont_importhub',label:'Contrato ImportHub assinado'},
    {key:'cont_stand',label:'Contrato Stand assinado'},
  ],
  vd_outros:[
    {key:'out_localizacao',label:'Localização do veículo'},
    {key:'out_data_prep',label:'Data de preparação definida'},
  ],
  op_transporte:[
    {key:'op_transportadora',label:'Transportadora definida'},
    {key:'op_prev_recolha',label:'Previsão de recolha'},
    {key:'op_data_recolha',label:'Data de recolha confirmada'},
    {key:'op_data_chegada',label:'Data de chegada PT'},
    {key:'op_pag_transporte',label:'Pagamento de transporte'},
  ],
  op_legal_pre:[
    {key:'op_abertura',label:'Abertura de processo'},
    {key:'op_modelo9',label:'Modelo 9'},
    {key:'op_proc_legal',label:'Procuração (legalização)'},
  ],
  op_cliente_pre:[
    {key:'op_email_proc',label:'Email de procedimento ao cliente'},
    {key:'op_autorizacoes',label:'Autorizações do cliente'},
    {key:'op_proc_cliente',label:'Procuração do cliente'},
    {key:'op_pagamentos',label:'Pagamentos do cliente'},
  ],
  op_inspecao:[
    {key:'op_insp_checklist',label:'Checklist de inspeção'},
    {key:'op_insp_fotos',label:'Fotografias de receção'},
    {key:'op_insp_inspecao',label:'Inspeção realizada'},
  ],
  op_legal_chegada:[
    {key:'op_leg_docs',label:'Documentação'},
    {key:'op_leg_originais',label:'Documentos originais'},
    {key:'op_leg_isv',label:'ISV'},
    {key:'op_leg_dav',label:'DAV'},
  ],
  op_seguro:[
    {key:'op_seguro',label:'Seguro do cliente'},
  ],
  op_entrega:[
    {key:'op_ent_lavagem',label:'Data de lavagem'},
    {key:'op_ent_matriculas',label:'Matrículas prontas'},
    {key:'op_ent_data',label:'Data de entrega'},
    {key:'op_ent_pagamento',label:'Pagamento final'},
    {key:'op_ent_fotos',label:'Fotografias de entrega'},
    {key:'op_ent_declaracao',label:'Declaração assinada'},
    {key:'op_ent_procuracao',label:'Procuração de entrega'},
  ],
  op_processo:[
    {key:'op_proc_chaves',label:'Chaves entregues'},
    {key:'op_dev_iva',label:'Devolução IVA'},
    {key:'op_review',label:'Review do cliente'},
  ],
};

// Regras de alertas: {fase mínima, chaves obrigatórias, mensagem, tipo, para quem}
const ALERT_RULES=[
  // COMERCIAIS
  {minStage:0,maxStage:0,check:d=>!d.qual,msg:'Lead por qualificar',sub:'Atribuir tipo de lead para ativar follow-up',type:'danger',role:'comercial',icon:'⚡'},
  {minStage:2,maxStage:3,check:d=>daysAgo(d.createdAt)>3&&d.qual,msg:'Proposta enviada há mais de 3 dias sem resposta',sub:'Considerar follow-up ou chamada',type:'warn',role:'comercial',icon:'📩'},
  {minStage:4,check:d=>!d.checks?.prop_id&&!d.proposalLink,msg:'Adjudicado sem proposta registada',sub:'Registar ID ou link da proposta',type:'danger',role:'comercial',icon:'📋'},
  {minStage:4,check:d=>['doc_teil1','doc_teil2','doc_coc'].some(k=>!d.checks?.[k]),msg:'Documentação do veículo incompleta',sub:'Teil I, Teil II ou COC em falta',type:'danger',role:'comercial',icon:'📄'},
  {minStage:4,check:d=>['ana_mecanica','ana_vin','ana_acidentes'].some(k=>!d.checks?.[k]),msg:'Análise do veículo incompleta',sub:'Mecânica, VIN ou historial por verificar',type:'danger',role:'comercial',icon:'🔧'},
  {minStage:4,check:d=>!d.checks?.cli_cc,msg:'Cartão de Cidadão do cliente em falta',sub:'Necessário para o contrato',type:'danger',role:'comercial',icon:'🪪'},
  {minStage:4,check:d=>!d.checks?.cont_importhub,msg:'Contrato ImportHub não assinado',sub:'Necessário antes de avançar para operacional',type:'danger',role:'comercial',icon:'📝'},
  {minStage:4,check:d=>!d.checks?.cont_stand,msg:'Contrato Stand não assinado',sub:'Necessário antes de avançar para operacional',type:'warn',role:'comercial',icon:'📝'},
  {minStage:4,check:d=>!d.checks?.out_localizacao,msg:'Localização do veículo não registada',sub:'Necessária para logística de transporte',type:'warn',role:'comercial',icon:'📍'},
  // OPERACIONAL
  {minStage:5,maxStage:6,check:d=>!d.checks?.op_transportadora,msg:'Transportadora não definida',sub:'Atribuir antes do início do transporte',type:'danger',role:'op',icon:'🚚'},
  {minStage:5,maxStage:6,check:d=>!d.checks?.op_prev_recolha,msg:'Previsão de recolha em falta',sub:'Data de recolha não definida',type:'warn',role:'op',icon:'📅'},
  {minStage:5,check:d=>!d.checks?.op_abertura,msg:'Processo de legalização não aberto',sub:'Abertura deve ocorrer assim que a compra é confirmada',type:'danger',role:'op',icon:'⚖️'},
  {minStage:5,check:d=>!d.checks?.op_email_proc,msg:'Email de procedimento não enviado ao cliente',sub:'Cliente deve ser informado do processo',type:'warn',role:'op',icon:'✉️'},
  {minStage:5,check:d=>!d.checks?.op_pagamentos,msg:'Pagamentos do cliente não confirmados',sub:'Verificar se todos os pagamentos foram recebidos',type:'danger',role:'op',icon:'💶'},
  {minStage:7,check:d=>!d.checks?.op_insp_checklist||!d.checks?.op_insp_fotos,msg:'Inspeção de chegada incompleta',sub:'Checklist ou fotografias em falta',type:'danger',role:'op',icon:'🔍'},
  {minStage:7,check:d=>!d.checks?.op_leg_isv,msg:'ISV não processado',sub:'Necessário após chegada do veículo',type:'danger',role:'op',icon:'📋'},
  {minStage:7,check:d=>!d.checks?.op_pag_transporte,msg:'Pagamento de transporte em falta',sub:'Transportadora ainda não paga',type:'warn',role:'op',icon:'💶'},
  {minStage:9,check:d=>!d.checks?.op_seguro,msg:'Seguro do cliente não confirmado',sub:'Obrigatório antes da entrega',type:'danger',role:'op',icon:'🛡️'},
  {minStage:9,check:d=>!d.checks?.op_ent_matriculas,msg:'Matrículas não prontas',sub:'Necessário para entrega',type:'warn',role:'op',icon:'🔢'},
  {minStage:10,check:d=>!d.checks?.op_ent_pagamento,msg:'Pagamento final não confirmado',sub:'Verificar liquidação total',type:'danger',role:'op',icon:'💶'},
  {minStage:10,check:d=>!d.checks?.op_ent_declaracao,msg:'Declaração de entrega não assinada',sub:'Documento obrigatório na entrega',type:'danger',role:'op',icon:'📝'},
  {minStage:11,check:d=>!d.checks?.op_review,msg:'Review do cliente pendente',sub:'Solicitar avaliação Google',type:'warn',role:'op',icon:'⭐'},
  {minStage:11,check:d=>d.checks?.op_dev_iva===false,msg:'Devolução IVA pendente',sub:'Verificar se aplicável e processar',type:'warn',role:'op',icon:'💶'},
];

const QLABELS={quality:'Lead de qualidade',bad:'Má lead',budget:'Falta de budget',noqual:'Sem qualidade','':'Não qualificada'};
const QBADGE={quality:'badge-quality',bad:'badge-bad',budget:'badge-budget',noqual:'badge-noqual','':'badge-new'};

let currentUser=null,currentDealId=null,qualifyingDealId=null,selectedQual='',editContactId=null,prevPage='pipeline';

let deals=[
  {id:1,clientName:'Alexandre Sousa',phone:'916420066',email:'alexandre@empresa.pt',type:'Empresa',brand:'VW',model:'ID.4',year:'2023',km:'45.000',budget:'42000',comercialId:'ze',stage:11,qual:'quality',proposalLink:'https://proposta.importhub.pt/p/a92d9dbe',notes:'',source:'Formulário website',createdAt:'2024-01-15',chassis:'WVWZZZ1KZMP123456',location:'DE-Berlin',transporter:'Transtomas',followupStep:2,
    checks:{prop_id:true,doc_teil1:true,doc_teil2:true,doc_coc:true,doc_manutencoes:true,ana_mecanica:true,ana_acidentes:true,ana_chaves:true,ana_cabos:true,ana_danos:true,ana_garantias:true,ana_baterias:true,ana_vin:true,ana_stand:true,cli_cc:true,cli_morada:true,cli_certidao:false,cont_revisao:true,cont_email_fecho:true,cont_importhub:true,cont_stand:true,out_localizacao:true,out_data_prep:true,op_transportadora:true,op_prev_recolha:true,op_data_recolha:true,op_data_chegada:true,op_pag_transporte:true,op_abertura:true,op_modelo9:true,op_proc_legal:true,op_email_proc:true,op_autorizacoes:true,op_proc_cliente:true,op_pagamentos:true,op_insp_checklist:true,op_insp_fotos:true,op_insp_inspecao:true,op_leg_docs:true,op_leg_originais:true,op_leg_isv:true,op_leg_dav:true,op_seguro:true,op_ent_lavagem:true,op_ent_matriculas:true,op_ent_data:true,op_ent_pagamento:true,op_ent_fotos:true,op_ent_declaracao:true,op_ent_procuracao:true,op_proc_chaves:true,op_dev_iva:false,op_review:false}},
  {id:2,clientName:'João Ferreira',phone:'913000002',email:'joao@inovacao.pt',type:'Particular',brand:'BMW',model:'Serie 3 320d',year:'2022',km:'60.000',budget:'35000',comercialId:'rodrigo',stage:2,qual:'quality',proposalLink:'https://proposta.importhub.pt/p/b81d8cae',notes:'Cliente muito interessado',source:'WhatsApp',createdAt:'2026-05-09',chassis:'',location:'DE-Hamburg',transporter:'',followupStep:0,
    checks:{prop_id:true,doc_teil1:true,doc_teil2:true,doc_coc:true,doc_manutencoes:true,ana_mecanica:true,ana_acidentes:true,ana_chaves:true,ana_cabos:true,ana_danos:true,ana_garantias:true,ana_baterias:true,ana_vin:true,ana_stand:true,cli_cc:false,cli_morada:false,cli_certidao:false,cont_revisao:false,cont_email_fecho:false,cont_importhub:false,cont_stand:false,out_localizacao:true,out_data_prep:false}},
  {id:3,clientName:'Sofia Almeida',phone:'914000003',email:'sofia@studio.pt',type:'Empresa',brand:'Mercedes',model:'GLA 250e',year:'2022',km:'30.000',budget:'48000',comercialId:'ze',stage:5,qual:'quality',proposalLink:'',notes:'',source:'Referência',createdAt:'2024-02-20',chassis:'WDC1569031J123789',location:'DE-Munich',transporter:'Cascão',followupStep:2,
    checks:{prop_id:true,doc_teil1:true,doc_teil2:true,doc_coc:true,doc_manutencoes:true,ana_mecanica:true,ana_acidentes:true,ana_chaves:true,ana_cabos:true,ana_danos:true,ana_garantias:true,ana_baterias:true,ana_vin:true,ana_stand:true,cli_cc:true,cli_morada:true,cli_certidao:true,cont_revisao:true,cont_email_fecho:true,cont_importhub:true,cont_stand:true,out_localizacao:true,out_data_prep:true,op_transportadora:true,op_prev_recolha:true,op_data_recolha:false,op_data_chegada:false,op_pag_transporte:false,op_abertura:true,op_modelo9:true,op_proc_legal:true,op_email_proc:true,op_autorizacoes:true,op_proc_cliente:true,op_pagamentos:true}},
  {id:4,clientName:'Rui Mendes',phone:'915000004',email:'rui@consultx.pt',type:'Particular',brand:'Audi',model:'Q4 E-tron',year:'2023',km:'20.000',budget:'50000',comercialId:'joao',stage:1,qual:'',proposalLink:'',notes:'',source:'Formulário website',createdAt:'2026-05-10',chassis:'',location:'',transporter:'',followupStep:0,checks:{}},
  {id:5,clientName:'Mariana Costa',phone:'916000005',email:'mariana@empresa.pt',type:'Empresa',brand:'Cupra',model:'Formentor',year:'2022',km:'55.000',budget:'28000',comercialId:'rodrigo',stage:4,qual:'budget',proposalLink:'https://proposta.importhub.pt/p/c72f7bdf',notes:'',source:'Email direto',createdAt:'2026-05-09',chassis:'',location:'DE-Frankfurt',transporter:'',followupStep:0,
    checks:{prop_id:true,doc_teil1:true,doc_teil2:true,doc_coc:true,doc_manutencoes:true,ana_mecanica:true,ana_acidentes:true,ana_chaves:true,ana_cabos:true,ana_danos:true,ana_garantias:true,ana_baterias:true,ana_vin:true,ana_stand:true,cli_cc:true,cli_morada:true,cli_certidao:false,cont_revisao:true,cont_email_fecho:false,cont_importhub:false,cont_stand:false,out_localizacao:true,out_data_prep:false}},
  {id:6,clientName:'Pedro Santos',phone:'917000006',email:'pedro@email.pt',type:'Particular',brand:'Tesla',model:'Model 3',year:'2020',km:'120.000',budget:'15000',comercialId:'antonio',stage:99,qual:'noqual',proposalLink:'',notes:'Km demasiado alta',source:'Formulário website',createdAt:'2024-03-12',chassis:'',location:'',transporter:'',followupStep:0,checks:{}},
  {id:7,clientName:'Gonçalo Magano',phone:'914037067',email:'goncalo@email.pt',type:'Particular',brand:'Audi',model:'Q4 E-tron',year:'2022',km:'35.000',budget:'52000',comercialId:'rodrigo',stage:7,qual:'quality',proposalLink:'https://proposta.importhub.pt/p/aa1a5ee6',notes:'',source:'Formulário website',createdAt:'2024-02-10',chassis:'WAUZZZFY3N2001234',location:'DE-Hunfeld',transporter:'Transtomas',followupStep:2,
    checks:{prop_id:true,doc_teil1:true,doc_teil2:true,doc_coc:true,doc_manutencoes:true,ana_mecanica:true,ana_acidentes:true,ana_chaves:true,ana_cabos:true,ana_danos:true,ana_garantias:true,ana_baterias:true,ana_vin:true,ana_stand:true,cli_cc:true,cli_morada:true,cli_certidao:false,cont_revisao:true,cont_email_fecho:true,cont_importhub:true,cont_stand:true,out_localizacao:true,out_data_prep:true,op_transportadora:true,op_prev_recolha:true,op_data_recolha:true,op_data_chegada:true,op_pag_transporte:false,op_abertura:true,op_modelo9:true,op_proc_legal:true,op_email_proc:true,op_autorizacoes:true,op_proc_cliente:true,op_pagamentos:true,op_insp_checklist:true,op_insp_fotos:true,op_insp_inspecao:true,op_leg_docs:false,op_leg_originais:false,op_leg_isv:false,op_leg_dav:false}},
  {id:8,clientName:'Catarina Fonseca',phone:'918000008',email:'catarina@gmail.com',type:'Particular',brand:'Mercedes',model:'Classe C 220d',year:'2022',km:'40.000',budget:'38000',comercialId:'ze',stage:2,qual:'quality',proposalLink:'https://proposta.importhub.pt/p/d91e2fa3',notes:'Muito interessada, responde rápido',source:'Instagram',createdAt:'2026-05-09',chassis:'',location:'',transporter:'',followupStep:0,checks:{prop_id:true}},
  {id:9,clientName:'Bruno Carvalho',phone:'919000009',email:'bruno@empresa.pt',type:'Empresa',brand:'BMW',model:'X5 xDrive40e',year:'2023',km:'25.000',budget:'72000',comercialId:'rodrigo',stage:2,qual:'quality',proposalLink:'https://proposta.importhub.pt/p/e82d1cb4',notes:'Precisa de fatura a empresa',source:'Referência',createdAt:'2026-05-09',chassis:'',location:'',transporter:'',followupStep:0,checks:{prop_id:true}},
  {id:10,clientName:'Inês Martins',phone:'910000010',email:'ines@email.pt',type:'Particular',brand:'Volvo',model:'XC60 T8',year:'2022',km:'50.000',budget:'55000',comercialId:'joao',stage:2,qual:'bad',proposalLink:'https://proposta.importhub.pt/p/f73c0da5',notes:'Lead fria mas tem orçamento',source:'Formulário website',createdAt:'2026-05-09',chassis:'',location:'',transporter:'',followupStep:0,checks:{prop_id:true}},
  {id:11,clientName:'Tiago Nunes',phone:'911000011',email:'tiago@gmail.com',type:'Particular',brand:'Audi',model:'A6 Avant 40 TDI',year:'2021',km:'60.000',budget:'42000',comercialId:'antonio',stage:2,qual:'quality',proposalLink:'https://proposta.importhub.pt/p/g64b9ec6',notes:'Quer entregar o carro atual',source:'Pesquisa Google',createdAt:'2026-05-08',chassis:'',location:'',transporter:'',followupStep:0,checks:{prop_id:true}},
];
let contacts=[
  {id:1,name:'Alexandre Sousa',phone:'916420066',email:'alexandre@empresa.pt',type:'Empresa',company:'Sousa & Filhos Lda',notes:''},
  {id:2,name:'João Ferreira',phone:'913000002',email:'joao@inovacao.pt',type:'Particular',company:'',notes:''},
  {id:3,name:'Sofia Almeida',phone:'914000003',email:'sofia@studio.pt',type:'Empresa',company:'Design Studio Lda',notes:''},
  {id:4,name:'Rui Mendes',phone:'915000004',email:'rui@consultx.pt',type:'Particular',company:'',notes:''},
  {id:5,name:'Mariana Costa',phone:'916000005',email:'mariana@empresa.pt',type:'Empresa',company:'Costa Corp',notes:''},
  {id:6,name:'Gonçalo Magano',phone:'914037067',email:'goncalo@email.pt',type:'Particular',company:'',notes:''},
  {id:7,name:'Catarina Fonseca',phone:'918000008',email:'catarina@gmail.com',type:'Particular',company:'',notes:''},
  {id:8,name:'Bruno Carvalho',phone:'919000009',email:'bruno@empresa.pt',type:'Empresa',company:'Carvalho Lda',notes:''},
  {id:9,name:'Inês Martins',phone:'910000010',email:'ines@email.pt',type:'Particular',company:'',notes:''},
  {id:10,name:'Tiago Nunes',phone:'911000011',email:'tiago@gmail.com',type:'Particular',company:'',notes:''},
];
let nextDID=12,nextCID=11;

// ══════════════════════════════════════════════════════
// ALERT ENGINE
// ══════════════════════════════════════════════════════
function getAlertsForDeal(d){
  if(d.stage===99)return[];
  const role=currentUser?.role||'admin';
  return ALERT_RULES.filter(r=>{
    const stageOk=d.stage>=r.minStage&&(r.maxStage===undefined||d.stage<=r.maxStage);
    const roleOk=role==='admin'||r.role===role||(role==='comercial'&&r.role==='comercial')||(role==='op'&&r.role==='op');
    return stageOk&&roleOk&&r.check(d);
  });
}

function getAllAlerts(){
  const my=myDeals().filter(d=>d.stage!==99);
  const all=[];
  my.forEach(d=>{
    getAlertsForDeal(d).forEach(a=>{
      all.push({...a,deal:d});
    });
  });
  return all;
}

function alertHtml(a,showDeal=false){
  const cls=a.type==='danger'?'alert-danger':'alert-warn';
  const dealId=a.deal?.id||currentDealId||null;
  const dealLabel=a.deal?`${a.deal.clientName} — ${a.deal.brand} ${a.deal.model}`:'';
  return`<div class="alert-item ${cls}"><div class="alert-icon">${a.icon}</div><div class="alert-body">${showDeal&&dealLabel?`<div class="alert-title">${dealLabel}</div>`:''}<div class="${showDeal&&dealLabel?'alert-sub':'alert-title'}">${a.msg}</div><div class="alert-sub">${a.sub}</div>${dealId?`<span class="alert-action" onclick="openDeal(${dealId})">Ver deal →</span>`:''}</div></div>`;
}

// ══════════════════════════════════════════════════════
// AUTH
// ══════════════════════════════════════════════════════
function doLogin(){
  const u=document.getElementById('login-user').value.trim();
  const p=document.getElementById('login-pass').value;
  const user=USERS.find(x=>x.id===u&&x.pass===p);
  if(!user){document.getElementById('login-error').style.display='block';return;}
  currentUser=user;
  document.getElementById('login-screen').classList.add('hidden');
  document.getElementById('app').classList.add('visible');
  document.getElementById('user-av').textContent=user.initials;
  document.getElementById('user-name-lbl').textContent=user.name;
  buildNav();showPage('dashboard');
}
document.getElementById('login-pass').addEventListener('keydown',e=>{if(e.key==='Enter')doLogin();});
document.getElementById('login-user').addEventListener('keydown',e=>{if(e.key==='Enter')doLogin();});
function doLogout(){currentUser=null;document.getElementById('login-screen').classList.remove('hidden');document.getElementById('app').classList.remove('visible');document.getElementById('login-user').value='';document.getElementById('login-pass').value='';document.getElementById('login-error').style.display='none';}

// ══════════════════════════════════════════════════════
// NAV
// ══════════════════════════════════════════════════════
function buildNav(){
  const pages=[{id:'dashboard',label:'Dashboard',icon:'📊'},{id:'pipeline',label:'Pipeline',icon:'🔄'},{id:'alerts',label:'Alertas',icon:'⚠️'},{id:'contacts',label:'Contactos',icon:'👤'}];
  if(currentUser.role==='admin')pages.push({id:'admin',label:'Admin',icon:'⚙️'});
  document.getElementById('topbar-nav').innerHTML=pages.map(p=>`<button class="nav-btn" id="nav-${p.id}" onclick="showPage('${p.id}')">${p.icon} ${p.label}</button>`).join('');
  updateNavBadge();
}
function updateNavBadge(){
  const count=getAllAlerts().filter(a=>a.type==='danger').length;
  const btn=document.getElementById('nav-alerts');
  if(btn&&count>0)btn.innerHTML=`⚠️ Alertas <span class="nav-badge">${count}</span>`;
  // Leads badge - show count of nova leads
  const nova=typeof inboxLeads!=='undefined'?inboxLeads.filter(l=>l.status==='nova').length:0;
  const leadsBtn=document.getElementById('nav-leads');
  if(leadsBtn)leadsBtn.innerHTML=nova>0?`📬 Leads <span class="nav-badge" style="background:var(--blue)">${nova}</span>`:'📬 Leads';
  if(typeof renderInbox==='function')renderInbox();
}
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+id)?.classList.add('active');
  document.getElementById('nav-'+id)?.classList.add('active');
  if(id==='dashboard')renderDashboard();
  if(id==='pipeline')renderPipeline();
  if(id==='alerts')renderAlertsPage();
  if(id==='contacts')renderContacts();
}
function goBack(){showPage(prevPage||'pipeline');}

// ══════════════════════════════════════════════════════
// HELPERS
// ══════════════════════════════════════════════════════
function myDeals(){
  if(currentUser.role==='admin')return deals;
  if(currentUser.role==='op')return deals.filter(d=>d.stage>=5&&d.stage!==99);
  return deals.filter(d=>d.comercialId===currentUser.id);
}
function uName(id){return USERS.find(x=>x.id===id)?.name||id;}
function stageInfo(id){return STAGES.find(s=>s.id===id)||STAGES[0];}
function daysAgo(ds){return Math.floor((Date.now()-new Date(ds))/86400000);}
function initials(n){return n.split(' ').slice(0,2).map(w=>w[0]).join('').toUpperCase();}
function qBadge(q){return`<span class="badge ${QBADGE[q]||'badge-new'}">${QLABELS[q]||'Não qualificada'}</span>`;}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}
document.querySelectorAll('.modal-overlay').forEach(m=>m.addEventListener('click',e=>{if(e.target===m)m.classList.remove('open');}));

function dealAlertLevel(d){
  const alerts=getAlertsForDeal(d);
  if(alerts.some(a=>a.type==='danger'))return'danger';
  if(alerts.some(a=>a.type==='warn'))return'warn';
  return'none';
}

// ══════════════════════════════════════════════════════
// DASHBOARD
// ══════════════════════════════════════════════════════
let dashActiveFilter = null;

function dashFilter(type) {
  dashActiveFilter = type;
  const clearBtn = document.getElementById('dash-clear-filter');
  if(clearBtn) clearBtn.style.display = type ? 'inline-flex' : 'none';
  // Update active card style
  document.querySelectorAll('.stat-card').forEach(c => c.classList.remove('active'));
  if(type) {
    const el = document.getElementById('stat-card-' + type);
    if(el) el.classList.add('active');
  }
  renderDashDeals();
}

function renderDashDeals() {
  const myD = myDeals();
  const allAlerts = getAllAlerts();
  let filtered, title;

  if(dashActiveFilter === 'active') {
    filtered = myD.filter(d => d.stage !== 99);
    title = `Deals ativos (${filtered.length})`;
  } else if(dashActiveFilter === 'adjudicados') {
    filtered = myD.filter(d => d.stage >= 4 && d.stage !== 99);
    title = `Adjudicados (${filtered.length})`;
  } else if(dashActiveFilter === 'alertas') {
    const dealIds = [...new Set(allAlerts.filter(a=>a.type==='danger').map(a=>a.deal?.id))].filter(Boolean);
    filtered = myD.filter(d => dealIds.includes(d.id));
    title = `Deals com alertas críticos (${filtered.length})`;
  } else if(dashActiveFilter === 'entregues') {
    filtered = myD.filter(d => d.stage === 10);
    title = `Entregues (${filtered.length})`;
  } else {
    filtered = [...myD.filter(d=>d.stage!==99)].sort((a,b)=>b.id-a.id).slice(0,8);
    title = 'Deals recentes';
  }

  const titleEl = document.getElementById('dash-list-title');
  if(titleEl) titleEl.textContent = title;

  const wrap = document.getElementById('recent-wrap');
  if(!wrap) return;

  if(!filtered.length) {
    wrap.innerHTML = '<div class="empty"><div class="empty-icon">📋</div><div class="empty-title">Nenhum deal nesta categoria</div></div>';
    return;
  }

  const showCom = currentUser.role !== 'comercial';
  wrap.innerHTML = `<table><thead><tr>
    <th>Cliente</th><th>Veículo</th><th>Fase</th><th>Qualificação</th>
    ${showCom ? '<th>Comercial</th>' : ''}
    <th>Vendedor</th><th>Alerta</th><th></th>
  </tr></thead><tbody>${filtered.map(d => {
    const st = stageInfo(d.stage);
    const al = dealAlertLevel(d);
    const seller = d.sellerId ? sellerById(d.sellerId) : null;
    return `<tr>
      <td><div style="font-weight:500">${d.clientName}</div><div class="td-mono td-muted">${d.phone}</div></td>
      <td style="font-size:12px">${d.brand} ${d.model}${d.year?' · '+d.year:''}</td>
      <td><span class="badge badge-gray" style="background:${st.color}18;color:${st.color}">${st.name}</span></td>
      <td>${qBadge(d.qual)}</td>
      ${showCom ? `<td class="td-muted">${uName(d.comercialId)}</td>` : ''}
      <td style="font-size:11px;color:var(--text3)">${seller ? seller.name : '—'}</td>
      <td>${al==='danger'?'<span style="color:var(--red)">🔴</span>':al==='warn'?'<span style="color:var(--amber)">🟡</span>':'<span style="color:var(--green)">✓</span>'}</td>
      <td><button class="btn btn-ghost btn-sm" onclick="openDeal(${d.id})">Ver →</button></td>
    </tr>`;
  }).join('')}</tbody></table>`;
}

function renderDashboard(){
  const myD=myDeals();
  const active=myD.filter(d=>d.stage!==99);
  const allAlerts=getAllAlerts();
  const dangerCount=allAlerts.filter(a=>a.type==='danger').length;

  if(currentUser.role==='comercial') document.getElementById('dash-title').textContent='Olá, '+currentUser.name;
  document.getElementById('dash-sub').textContent=new Date().toLocaleDateString('pt-PT',{weekday:'long',year:'numeric',month:'long',day:'numeric'});

  document.getElementById('stats-grid').innerHTML=`
    <div class="stat-card" id="stat-card-active" onclick="dashFilter('active')" style="padding:12px 16px">
      <div class="stat-label">Deals ativos</div>
      <div class="stat-value" style="font-size:20px">${active.length}</div>
      <div class="stat-sub">clique para ver</div>
    </div>
    <div class="stat-card" id="stat-card-adjudicados" onclick="dashFilter('adjudicados')" style="padding:12px 16px">
      <div class="stat-label">Adjudicados</div>
      <div class="stat-value" style="font-size:20px;color:var(--accent-dark)">${active.filter(d=>d.stage>=4).length}</div>
      <div class="stat-sub">clique para ver</div>
    </div>
    <div class="stat-card" id="stat-card-alertas" onclick="dashFilter('alertas')" style="padding:12px 16px">
      <div class="stat-label">Alertas críticos</div>
      <div class="stat-value" style="font-size:20px;color:${dangerCount>0?'var(--red)':'var(--green)'}">${dangerCount}</div>
      <div class="stat-sub">clique para ver</div>
    </div>
    <div class="stat-card" id="stat-card-entregues" onclick="dashFilter('entregues')" style="padding:12px 16px">
      <div class="stat-label">Entregues</div>
      <div class="stat-value" style="font-size:20px;color:var(--green)">${myD.filter(d=>d.stage===10).length}</div>
      <div class="stat-sub">clique para ver</div>
    </div>`;

  // Restore active filter state after re-render
  if(dashActiveFilter) {
    const el = document.getElementById('stat-card-' + dashActiveFilter);
    if(el) el.classList.add('active');
    const clearBtn = document.getElementById('dash-clear-filter');
    if(clearBtn) clearBtn.style.display = 'inline-flex';
  }

  renderDashDeals();
  renderInbox();

  // Alerts panel
  const topAlerts = allAlerts.sort((a,b)=>(b.type==='danger'?1:0)-(a.type==='danger'?1:0)).slice(0,5);
  const alertEl = document.getElementById('dash-alerts');
  const countEl = document.getElementById('dash-alert-count');
  if(allAlerts.length){countEl.style.display='inline-flex';countEl.textContent=allAlerts.length;}
  else{countEl.style.display='none';}
  alertEl.innerHTML = topAlerts.length
    ? topAlerts.map(a=>alertHtml(a,true)).join('') + '<div style="text-align:center;margin-top:8px"><button class="btn btn-ghost btn-sm" id="btn-ver-alertas">Ver todos →</button></div>'
    : '<div style="font-size:12px;color:var(--text3);text-align:center;padding:10px">✅ Sem alertas ativos</div>';
  const btnVer = document.getElementById('btn-ver-alertas');
  if(btnVer) btnVer.onclick = () => showPage('alerts');

  if(typeof renderPlanner==='function') renderPlanner();
  if(typeof renderInbox==='function') renderInbox();
  updateNavBadge();
}

// ══════════════════════════════════════════════════════
// ALERTS PAGE
// ══════════════════════════════════════════════════════
function renderAlertsPage(){
  const allAlerts=getAllAlerts();
  const el=document.getElementById('alerts-full-page');
  if(!allAlerts.length){el.innerHTML='<div class="card"><div class="card-body"><div class="empty"><div class="empty-icon">✅</div><div class="empty-title">Sem alertas ativos</div><p style="font-size:12px;color:var(--text3);margin-top:6px">Todos os deals estão em ordem.</p></div></div></div>';return;}
  const dangers=allAlerts.filter(a=>a.type==='danger');
  const warns=allAlerts.filter(a=>a.type==='warn');
  let html='';
  if(dangers.length){html+=`<div class="alerts-group"><div class="alerts-group-title">🔴 Críticos <span class="alerts-count-badge">${dangers.length}</span></div>${dangers.map(a=>alertHtml(a,true)).join('')}</div>`;}
  if(warns.length){html+=`<div class="alerts-group"><div class="alerts-group-title">🟡 Atenção <span class="alerts-count-badge warn">${warns.length}</span></div>${warns.map(a=>alertHtml(a,true)).join('')}</div>`;}
  el.innerHTML=html;
  updateNavBadge();
}

// ══════════════════════════════════════════════════════
// PIPELINE
// ══════════════════════════════════════════════════════
function renderPipeline(){
  const sel=document.getElementById('pipeline-filter');
  if(sel.options.length===1)USERS.filter(u=>u.role==='comercial').forEach(c=>{const o=document.createElement('option');o.value=c.id;o.textContent=c.name;sel.appendChild(o);});
  const fv=sel.value;
  let myD=myDeals().filter(d=>d.stage!==99);
  if(fv)myD=myD.filter(d=>d.comercialId===fv);
  let stages=STAGES.filter(s=>s.phase!=='lost');
  if(currentUser.role==='op')stages=STAGES.filter(s=>s.phase==='op');
  if(currentUser.role==='comercial')stages=STAGES.filter(s=>s.phase==='comercial');
  document.getElementById('pipeline-sub').textContent=`${myD.length} deal${myD.length!==1?'s':''} ativos`;
  document.getElementById('pipeline-board').innerHTML=stages.map(st=>{
    const sd=myD.filter(d=>d.stage===st.id);
    return`<div class="pipeline-col"><div class="pipeline-col-head"><div style="display:flex;align-items:center;gap:5px"><span class="pipeline-dot" style="background:${st.color}"></span><span class="pipeline-col-name">${st.name}</span></div><span class="pipeline-col-count">${sd.length}</span></div><div class="stage-bar" style="background:${st.color}"></div>${sd.map(d=>{const days=daysAgo(d.createdAt);const dc=days>7?'days-danger':days>3?'days-warn':'days-ok';const al=dealAlertLevel(d);return`<div class="deal-card ${al==='danger'?'has-alert':al==='warn'?'has-warn':''}" onclick="openDeal(${d.id})"><div style="display:flex;justify-content:space-between;margin-bottom:3px"><div><div class="deal-name">${d.clientName}</div><div class="deal-phone">${d.phone}</div></div>${qBadge(d.qual)}</div><div class="deal-car">🚗 ${d.brand} ${d.model}${d.year?' · '+d.year:''}</div><div class="deal-footer"><span class="deal-comercial">${uName(d.comercialId)}</span><span class="deal-days ${dc}">${days}d</span></div></div>`;}).join('')}${sd.length===0?'<div style="padding:14px;text-align:center;font-size:11px;color:var(--text3)">Vazio</div>':''}</div>`;
  }).join('');
}

// ══════════════════════════════════════════════════════
// DEAL DETAIL
// ══════════════════════════════════════════════════════
function openDeal(id){
  prevPage=document.querySelector('.nav-btn.active')?.id?.replace('nav-','')||'pipeline';
  currentDealId=id;
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-deal-detail').classList.add('active');
  renderDeal(deals.find(x=>x.id===id));
}

function renderDeal(d){
  if(!d)return;
  const st=stageInfo(d.stage);
  const canEdit=currentUser.role==='admin'||currentUser.id===d.comercialId;
  const canOp=currentUser.role==='admin'||currentUser.role==='op';
  const allStages=STAGES.filter(s=>s.phase!=='lost');
  const progress=allStages.map(s=>`<div class="pp-step ${s.id<d.stage?'done':s.id===d.stage?'current':''}"></div>`).join('');
  const dealAlerts=getAlertsForDeal(d);
  const alertsHtml=dealAlerts.length?`<div style="margin-bottom:14px">${dealAlerts.map(a=>alertHtml(a,false)).join('')}</div>`:'';

  document.getElementById('deal-detail-content').innerHTML=`
    <div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:12px;flex-wrap:wrap;gap:10px">
      <div>
        <div style="display:flex;align-items:center;gap:10px;margin-bottom:5px">
          <h2 style="font-family:'DM Serif Display',serif;font-size:21px;color:var(--brand)">${d.clientName}</h2>
          ${qBadge(d.qual)}
        </div>
        <div style="display:flex;gap:12px;font-size:12px;color:var(--text2);flex-wrap:wrap">
          <span>📞 <a href="tel:${d.phone}">${d.phone}</a></span>
          <span>✉️ <a href="mailto:${d.email}">${d.email}</a></span>
          <span>👤 ${uName(d.comercialId)}</span>
          <span>📅 ${new Date(d.createdAt).toLocaleDateString('pt-PT')}</span>
        </div>
      </div>
      <div style="display:flex;gap:7px;flex-wrap:wrap">
        ${d.stage===0&&canEdit?`<button class="btn btn-accent" onclick="openQualify(${d.id})">⚡ Qualificar</button>`:''}
        ${d.stage<11&&d.stage!==99&&(canEdit||canOp)?`<button class="btn btn-primary" onclick="advanceStage(${d.id})">Avançar →</button>`:''}
        ${canEdit&&d.stage!==99?`<button class="btn btn-ghost btn-sm" onclick="openManualFU(${d.id})">+ Follow-up</button>`:''}
        ${d.stage!==99&&(canEdit||canOp)?`<button class="btn btn-danger btn-sm" onclick="markLost(${d.id})">Fechar perdido</button>`:''}
        ${d.stage===99?`<button class="btn btn-ghost btn-sm" onclick="reopenDeal(${d.id})">Reabrir</button>`:''}
      </div>
    </div>
    <div class="pipe-progress">${progress}</div>
    <div style="display:flex;align-items:center;gap:8px;padding:9px 14px;background:var(--white);border-radius:var(--radius-lg);border:1px solid var(--border2);margin-bottom:14px">
      <span class="pipeline-dot" style="background:${st.color}"></span>
      <span style="font-weight:500;font-size:13px;color:${st.color}">${st.name}</span>
      <span style="color:var(--text3);font-size:11px">· ${daysAgo(d.createdAt)} dias em aberto</span>
      ${dealAlerts.length?`<span class="badge badge-red" style="margin-left:auto">${dealAlerts.length} alerta${dealAlerts.length!==1?'s':''}</span>`:'<span class="badge badge-green" style="margin-left:auto">✓ Sem alertas</span>'}
    </div>
    ${alertsHtml}
    <div class="detail-grid">
      <div style="display:flex;flex-direction:column;gap:12px">
        ${vehicleCard(d)}
        ${d.qual&&d.qual!=='noqual'?commCard(d):''}
        ${d.qual==='noqual'?`<div class="card"><div class="card-header"><span class="card-title">📨 Email de recusa</span></div><div class="card-body" style="padding:8px 14px"><div class="fu-item"><span class="fu-label">Email de recusa enviado</span>${emBtn(d,'noqual')}</div></div></div>`:''}
        ${vdChecklistCard(d,canEdit)}
        ${d.stage>=5&&canOp?opChecklistCard(d):''}
        <div class="card"><div class="card-header"><span class="card-title">📝 Notas</span></div><div class="card-body"><textarea class="fc" id="dn-${d.id}" style="min-height:65px"${!canEdit&&!canOp?' disabled':''}>${d.notes}</textarea>${canEdit||canOp?`<button class="btn btn-ghost btn-sm" style="margin-top:7px" onclick="saveNotes(${d.id})">Guardar</button>`:''}</div></div>
      </div>
      <div style="display:flex;flex-direction:column;gap:12px">
        ${clientCard(d)}
        ${d.qual===''&&d.stage===0&&canEdit?qualifyPrompt(d):''}
        ${timelineCard(d)}
      </div>
    </div>`;
}

function vehicleCard(d){
  return`<div class="card"><div class="card-header"><span class="card-title">🚗 Veículo</span></div><div class="card-body">
    <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:10px">
      <div><div class="fl" style="margin-bottom:2px">Marca/Modelo</div><div style="font-weight:500;font-size:13px">${d.brand} ${d.model}</div></div>
      <div><div class="fl" style="margin-bottom:2px">Ano</div><div style="font-size:13px">${d.year||'—'}</div></div>
      <div><div class="fl" style="margin-bottom:2px">Km</div><div style="font-size:13px">${d.km||'—'}</div></div>
      <div><div class="fl" style="margin-bottom:2px">Orçamento</div><div style="font-size:13px;font-weight:500;color:var(--accent-dark)">${d.budget?Number(d.budget).toLocaleString('pt-PT')+'€':'—'}</div></div>
    </div>
    ${d.chassis||d.location?`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:10px;padding-top:10px;border-top:1px solid var(--border2)">
      ${d.chassis?`<div><div class="fl" style="margin-bottom:2px">Chassis (VIN)</div><div class="td-mono" style="font-size:11px">${d.chassis}</div></div>`:''}
      ${d.location?`<div><div class="fl" style="margin-bottom:2px">Localização</div><div style="font-size:12px">📍 ${d.location}</div></div>`:''}
      ${d.transporter?`<div><div class="fl" style="margin-bottom:2px">Transportadora</div><div style="font-size:12px">${d.transporter}</div></div>`:''}
    </div>`:''}
    ${d.proposalLink?`<div style="margin-top:10px;padding-top:10px;border-top:1px solid var(--border2)"><div class="fl" style="margin-bottom:2px">Proposta</div><a href="${d.proposalLink}" target="_blank" style="font-size:12px;color:var(--blue)">${d.proposalLink} ↗</a></div>`:''}
  </div></div>`;
}

function commCard(d){
  const items=[];
  items.push({done:d.stage>=2,label:'Proposta enviada (email + WA)',actions:d.stage>=2?[]:[{t:'wa',tmpl:'proposal'},{t:'em',tmpl:'proposal'}]});
  if(d.qual==='quality'){
    items.push({done:d.followupStep>=1,label:'📞 Ligar D+2 — 1.ª tentativa',actions:[]});
    items.push({done:d.followupStep>=1,label:'1.º Follow-up email+WA',actions:d.followupStep>=1?[]:[{t:'wa',tmpl:'followup1'},{t:'em',tmpl:'followup1'}]});
    items.push({done:d.followupStep>=2,label:'📞 Ligar D+4 — 2.ª tentativa',actions:[]});
    items.push({done:d.followupStep>=2,label:'2.º Follow-up email+WA',actions:d.followupStep>=2?[]:[{t:'wa',tmpl:'followup2'},{t:'em',tmpl:'followup2'}]});
  } else {
    items.push({done:d.followupStep>=1,label:'1.º Follow-up email+WA (sem chamada)',actions:d.followupStep>=1?[]:[{t:'wa',tmpl:'followup1'},{t:'em',tmpl:'followup1'}]});
    items.push({done:true,label:'Processo termina após 1.º follow-up',actions:[]});
  }
  return`<div class="card"><div class="card-header"><span class="card-title">📨 Comunicação & Follow-up</span><div style="display:flex;gap:4px">${waBtn(d,'proposal')} ${emBtn(d,'proposal')}</div></div><div class="card-body" style="padding:6px 14px">${items.map(it=>`<div class="fu-item"><div class="fu-label"><div class="cl-box ${it.done?'checked':''}"></div><span style="${it.done?'text-decoration:line-through;color:var(--text3)':''}">${it.label}</span></div>${it.actions.length?`<div class="fu-actions">${it.actions.map(a=>a.t==='wa'?waBtn(d,a.tmpl):emBtn(d,a.tmpl)).join('')}</div>`:''}</div>`).join('')}</div></div>`;
}

function vdChecklistCard(d,canEdit){
  const sections=[
    {title:'Proposta',list:CHECKLISTS.vd_proposta},
    {title:'Documentação do veículo',list:CHECKLISTS.vd_docs},
    {title:'Análise do veículo',list:CHECKLISTS.vd_analise},
    {title:'Dados do cliente',list:CHECKLISTS.vd_cliente},
    {title:'Contrato',list:CHECKLISTS.vd_contrato},
    {title:'Outros',list:CHECKLISTS.vd_outros},
  ];
  return`<div class="card"><div class="card-header"><span class="card-title">📋 Checklist comercial (VD)</span><span class="badge badge-gray">${countChecked(d,sections)} / ${countTotal(sections)}</span></div><div class="card-body" style="padding:6px 14px">${sections.map(sec=>`<div class="cl-section">${sec.title}</div>${sec.list.map(it=>{const checked=!!d.checks?.[it.key];const hasAlert=checked===false&&getAlertsForDeal(d).some(a=>a.check(d));return`<div class="cl-item"><div class="cl-box ${checked?'checked':''}" onclick="${canEdit?`toggleCheck(${d.id},'${it.key}')`:''}" style="${!canEdit?'cursor:default':''}"></div><span class="cl-lbl ${checked?'checked':''}">${it.label}</span></div>`;}).join('')}`).join('')}</div></div>`;
}

function opChecklistCard(d){
  const sections=[
    {title:'Transporte',list:CHECKLISTS.op_transporte},
    {title:'Legalização (pré-transporte)',list:CHECKLISTS.op_legal_pre},
    {title:'Cliente (pré-transporte)',list:CHECKLISTS.op_cliente_pre},
    {title:'Inspeção (chegada)',list:CHECKLISTS.op_inspecao},
    {title:'Legalização (chegada)',list:CHECKLISTS.op_legal_chegada},
    {title:'Seguro',list:CHECKLISTS.op_seguro},
    {title:'Entrega',list:CHECKLISTS.op_entrega},
    {title:'Processo final',list:CHECKLISTS.op_processo},
  ];
  return`<div class="card"><div class="card-header"><span class="card-title">⚙️ Checklist operacional (OP)</span><span class="badge badge-gray">${countChecked(d,sections)} / ${countTotal(sections)}</span></div><div class="card-body" style="padding:6px 14px">${sections.map(sec=>`<div class="cl-section">${sec.title}</div>${sec.list.map(it=>{const checked=!!d.checks?.[it.key];return`<div class="cl-item"><div class="cl-box ${checked?'checked':''}" onclick="toggleCheck(${d.id},'${it.key}')"></div><span class="cl-lbl ${checked?'checked':''}">${it.label}</span></div>`;}).join('')}`).join('')}</div></div>`;
}

function countChecked(d,sections){return sections.reduce((sum,s)=>sum+s.list.filter(it=>d.checks?.[it.key]).length,0);}
function countTotal(sections){return sections.reduce((sum,s)=>sum+s.list.length,0);}

function toggleCheck(dealId,key){
  const d=deals.find(x=>x.id===dealId);
  if(!d)return;
  if(!d.checks)d.checks={};
  d.checks[key]=!d.checks[key];
  renderDeal(d);
  updateNavBadge();
}

function clientCard(d){
  return`<div class="card"><div class="card-header"><span class="card-title">👤 Cliente</span></div><div class="card-body" style="padding:12px 14px">
    <div style="display:flex;align-items:center;gap:9px;margin-bottom:10px"><div style="width:34px;height:34px;border-radius:50%;background:var(--brand);color:var(--accent);display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:600">${initials(d.clientName)}</div><div><div style="font-weight:500;font-size:13px">${d.clientName}</div><div style="font-size:11px;color:var(--text3)">${d.type}</div></div></div>
    <table style="width:100%;font-size:11px"><tr><td style="color:var(--text3);padding:3px 0">Telemóvel</td><td style="text-align:right"><a href="tel:${d.phone}">${d.phone}</a></td></tr><tr><td style="color:var(--text3);padding:3px 0">Email</td><td style="text-align:right;word-break:break-all"><a href="mailto:${d.email}">${d.email}</a></td></tr><tr><td style="color:var(--text3);padding:3px 0">Origem</td><td style="text-align:right">${d.source}</td></tr><tr><td style="color:var(--text3);padding:3px 0">Comercial</td><td style="text-align:right">${uName(d.comercialId)}</td></tr></table>
  </div></div>`;
}

function qualifyPrompt(d){
  return`<div class="card" style="border:2px solid var(--accent-light)"><div class="card-body" style="text-align:center;padding:18px"><div style="font-size:22px;margin-bottom:7px">⚡</div><div style="font-weight:600;margin-bottom:5px;font-size:13px">Lead por qualificar</div><div style="font-size:11px;color:var(--text3);margin-bottom:12px">Qualifique para ativar o follow-up automático</div><button class="btn btn-accent" onclick="openQualify(${d.id})">Qualificar agora</button></div></div>`;
}

function timelineCard(d){
  const events=[
    {done:true,title:'Deal criado',date:new Date(d.createdAt).toLocaleDateString('pt-PT')},
    {done:!!d.qual,title:`Qualificado: ${QLABELS[d.qual]||'—'}`},
    {done:d.stage>=2,title:'Proposta enviada'},
    {done:d.stage>=4,title:'Sinal recebido'},
    {done:d.stage>=5,title:'Compra confirmada'},
    {done:d.stage>=6,title:'Em transporte'},
    {done:d.stage>=7,title:'Chegada a Portugal'},
    {done:d.stage>=8,title:'Legalização iniciada'},
    {done:d.stage>=9,title:'Pronto para entrega'},
    {done:d.stage>=10,title:'Entregue ao cliente'},
    {done:d.stage===99,title:'Fechado perdido',alert:true},
  ].filter(e=>e.done);
  return`<div class="card"><div class="card-header"><span class="card-title">🕐 Histórico</span></div><div class="card-body" style="padding:12px 14px"><div class="timeline">${events.map(e=>`<div class="tl-item"><div class="tl-dot ${e.alert?'alert':'done'}"></div><div><div class="tl-title" ${e.alert?'style="color:var(--red)"':''}>${e.title}</div>${e.date?`<div class="tl-date">${e.date}</div>`:''}</div></div>`).join('')}</div></div></div>`;
}

// ══════════════════════════════════════════════════════
// DEAL ACTIONS
// ══════════════════════════════════════════════════════
function advanceStage(id){const d=deals.find(x=>x.id===id);if(!d||d.stage>=11)return;d.stage++;renderDeal(d);updateNavBadge();}
function markLost(id){if(!confirm('Confirma fechar este deal como perdido?'))return;const d=deals.find(x=>x.id===id);if(d){d.stage=99;renderDeal(d);updateNavBadge();}}
function reopenDeal(id){const d=deals.find(x=>x.id===id);if(d){d.stage=0;d.qual='';renderDeal(d);updateNavBadge();}}
function saveNotes(id){const d=deals.find(x=>x.id===id);if(d){d.notes=document.getElementById(`dn-${id}`).value;}}

// ══════════════════════════════════════════════════════
// NEW DEAL
// ══════════════════════════════════════════════════════
function openNewDeal(){
  const sel=document.getElementById('nd-comercial');sel.innerHTML='';
  USERS.filter(u=>u.role==='comercial').forEach(u=>{const o=document.createElement('option');o.value=u.id;o.textContent=u.name;if(currentUser.role==='comercial'&&u.id===currentUser.id)o.selected=true;sel.appendChild(o);});
  ['nd-name','nd-phone','nd-email','nd-brand','nd-model','nd-year','nd-km','nd-budget','nd-notes'].forEach(id=>document.getElementById(id).value='');
  openModal('modal-deal');
}
function saveDeal(){
  const name=document.getElementById('nd-name').value.trim();
  const phone=document.getElementById('nd-phone').value.trim();
  if(!name||!phone){alert('Nome e telemóvel são obrigatórios.');return;}
  const d={id:nextDID++,clientName:name,phone,email:document.getElementById('nd-email').value.trim(),type:document.getElementById('nd-type').value,brand:document.getElementById('nd-brand').value.trim(),model:document.getElementById('nd-model').value.trim(),year:document.getElementById('nd-year').value.trim(),km:document.getElementById('nd-km').value.trim(),budget:document.getElementById('nd-budget').value.trim(),comercialId:document.getElementById('nd-comercial').value,source:document.getElementById('nd-source').value,notes:document.getElementById('nd-notes').value.trim(),stage:0,qual:'',proposalLink:'',chassis:'',location:'',transporter:'',followupStep:0,createdAt:new Date().toISOString().split('T')[0],checks:{}};
  deals.unshift(d);
  if(!contacts.find(c=>c.phone===phone))contacts.unshift({id:nextCID++,name,phone,email:d.email,type:d.type,company:'',notes:''});
  closeModal('modal-deal');openDeal(d.id);updateNavBadge();
}

// ══════════════════════════════════════════════════════
// QUALIFY
// ══════════════════════════════════════════════════════
function openQualify(id){
  qualifyingDealId=id;selectedQual='';
  document.querySelectorAll('.qual-opt').forEach(e=>e.classList.remove('selected'));
  document.getElementById('qual-info').style.display='none';
  document.getElementById('qual-link').value=deals.find(x=>x.id===id)?.proposalLink||'';
  openModal('modal-qualify');
}
function selectQual(q){
  selectedQual=q;
  document.querySelectorAll('.qual-opt').forEach(e=>e.classList.remove('selected'));
  document.querySelector(`.q-${q}`)?.classList.add('selected');
  const info={quality:'Follow-up completo: liga D+2 → email+WA → liga D+4 → email+WA → termina.',bad:'Proposta + 1 follow-up (email+WA). Sem chamadas.',budget:'Proposta acima do orçamento + 1 follow-up (email+WA). Sem chamadas.',noqual:'Email de recusa enviado. Sem proposta. Deal fecha.'};
  const el=document.getElementById('qual-info');el.style.display='block';el.textContent=info[q]||'';
}
function saveQual(){
  if(!selectedQual){alert('Selecione um tipo de qualificação.');return;}
  const d=deals.find(x=>x.id===qualifyingDealId);if(!d)return;
  d.qual=selectedQual;d.proposalLink=document.getElementById('qual-link').value.trim();
  if(selectedQual==='noqual')d.stage=99;
  else if(d.stage===0)d.stage=1;
  closeModal('modal-qualify');renderDeal(d);updateNavBadge();
}

// ══════════════════════════════════════════════════════
// WA / EMAIL
// ══════════════════════════════════════════════════════
const TMPL={
  proposal:{wa:d=>`Olá ${d.clientName.split(' ')[0]}!\n\nObrigado pelo contacto com a *ImportHub*.\n\nPreparámos uma proposta personalizada:\n\n👉 ${d.proposalLink||'[link da proposta]'}\n\nO valor inclui todos os custos chave-na-mão em Portugal.\n\nObrigado!\n*ImportHub*`,em:d=>({s:`Proposta de importação — ${d.brand} ${d.model}`,b:`Boa tarde ${d.clientName.split(' ')[0]},\n\nObrigado pelo seu contacto e interesse na ImportHub.\n\nPreparámos uma proposta personalizada com preço chave-na-mão:\n\n👉 ${d.proposalLink||'[link da proposta]'}\n\nEstamos disponíveis para qualquer dúvida.\n\nCom os melhores cumprimentos,\nImportHub`})},
  followup1:{wa:d=>`Boa tarde ${d.clientName.split(' ')[0]},\n\nGostaria de confirmar se já analisou a proposta.\n\n👉 ${d.proposalLink||'[link]'}\n\nFicamos disponíveis.\n\nObrigado!\n*ImportHub*`,em:d=>({s:`Seguimento — ${d.brand} ${d.model}`,b:`Boa tarde ${d.clientName.split(' ')[0]},\n\nGostaríamos de confirmar se teve oportunidade de analisar a proposta.\n\n👉 ${d.proposalLink||'[link]'}\n\nEstamos disponíveis para qualquer dúvida.\n\nCom os melhores cumprimentos,\nImportHub`})},
  followup2:{wa:d=>`Olá ${d.clientName.split(' ')[0]}!\n\nQueria confirmar se o processo de importação faz sentido para si agora.\n\nObrigado!\n*ImportHub*`,em:d=>({s:`Retoma — ${d.brand} ${d.model}`,b:`Boa tarde ${d.clientName.split(' ')[0]},\n\nEntramos em contacto para perceber se o processo de importação faz sentido neste momento.\n\nCaso não seja o timing ideal, diga-nos.\n\nCom os melhores cumprimentos,\nImportHub`})},
  noqual:{em:d=>({s:`Resposta ao seu pedido — ImportHub`,b:`Boa tarde ${d.clientName.split(' ')[0]},\n\nObrigado pelo seu interesse na ImportHub.\n\nApós análise do pedido, verificámos que, nas condições indicadas, não nos é possível apresentar uma proposta viável.\n\nContinuamos à disposição para qualquer esclarecimento.\n\nCom os melhores cumprimentos,\nImportHub`})},
};
function waBtn(d,tmpl){return`<button class="btn-wa" onclick="sendWA(${d.id},'${tmpl}')">WhatsApp</button>`;}
function emBtn(d,tmpl){return`<button class="btn-em" onclick="sendEmail(${d.id},'${tmpl}')">Email</button>`;}
function sendWA(did,tmpl){const d=deals.find(x=>x.id===did);if(!d)return;const msg=TMPL[tmpl]?.wa?.(d)||'';const ph=d.phone.replace(/\s/g,'');const num=ph.startsWith('+')?ph.slice(1):'351'+ph;window.open(`https://wa.me/${num}?text=${encodeURIComponent(msg)}`,'_blank');markFU(did,tmpl);}
function sendEmail(did,tmpl){const d=deals.find(x=>x.id===did);if(!d)return;const t=TMPL[tmpl]?.em?.(d)||{s:'',b:''};window.location.href=`mailto:${d.email}?subject=${encodeURIComponent(t.s)}&body=${encodeURIComponent(t.b)}`;markFU(did,tmpl);}
function markFU(did,tmpl){const d=deals.find(x=>x.id===did);if(!d)return;if(tmpl==='followup1'&&d.followupStep<1)d.followupStep=1;if(tmpl==='followup2'&&d.followupStep<2)d.followupStep=2;}

// ══════════════════════════════════════════════════════
// CONTACTS
// ══════════════════════════════════════════════════════
function renderContacts(){
  const q=(document.getElementById('contact-search').value||'').toLowerCase();
  const tf=document.getElementById('contact-filter').value;
  let myC=currentUser.role==='comercial'?contacts.filter(c=>deals.find(d=>d.comercialId===currentUser.id&&d.phone===c.phone)):contacts;
  const filtered=myC.filter(c=>(!q||(c.name+c.phone+c.email).toLowerCase().includes(q))&&(!tf||c.type===tf));
  const tbody=document.getElementById('contacts-tbody');
  if(!filtered.length){tbody.innerHTML=`<tr><td colspan="7"><div class="empty"><div class="empty-icon">👤</div><div class="empty-title">Nenhum contacto encontrado</div></div></td></tr>`;return;}
  tbody.innerHTML=filtered.map(c=>{const cd=deals.filter(d=>d.phone===c.phone);return`<tr><td><div style="display:flex;align-items:center;gap:7px"><div style="width:26px;height:26px;border-radius:50%;background:var(--brand);color:var(--accent);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:600;flex-shrink:0">${initials(c.name)}</div><div><div style="font-weight:500;font-size:13px">${c.name}</div>${c.company?`<div style="font-size:11px;color:var(--text3)">${c.company}</div>`:''}</div></div></td><td class="td-mono">${c.phone}</td><td><span class="badge badge-gray">${c.type}</span></td><td class="td-muted" style="font-size:12px">${c.email||'—'}</td><td>${cd.length?`<button class="btn btn-ghost btn-sm" onclick="openDeal(${cd[cd.length-1].id})">${cd.length} deal${cd.length!==1?'s':''}</button>`:'—'}</td><td class="td-muted">${cd.length?uName(cd[0].comercialId):'—'}</td><td><button class="btn btn-ghost btn-sm" onclick="editContact(${c.id})">✏️</button></td></tr>`;}).join('');
}
function openNewContact(){editContactId=null;document.getElementById('contact-modal-title').textContent='Novo Contacto';['nc-name','nc-phone','nc-email','nc-company','nc-notes'].forEach(id=>document.getElementById(id).value='');openModal('modal-contact');}
function editContact(id){const c=contacts.find(x=>x.id===id);if(!c)return;editContactId=id;document.getElementById('contact-modal-title').textContent='Editar Contacto';document.getElementById('nc-name').value=c.name;document.getElementById('nc-phone').value=c.phone;document.getElementById('nc-email').value=c.email||'';document.getElementById('nc-type').value=c.type;document.getElementById('nc-company').value=c.company||'';document.getElementById('nc-notes').value=c.notes||'';openModal('modal-contact');}
function saveContact(){const name=document.getElementById('nc-name').value.trim();const phone=document.getElementById('nc-phone').value.trim();if(!name||!phone){alert('Nome e telemóvel são obrigatórios.');return;}if(editContactId){const c=contacts.find(x=>x.id===editContactId);if(c){c.name=name;c.phone=phone;c.email=document.getElementById('nc-email').value.trim();c.type=document.getElementById('nc-type').value;c.company=document.getElementById('nc-company').value.trim();c.notes=document.getElementById('nc-notes').value.trim();}}else contacts.unshift({id:nextCID++,name,phone,email:document.getElementById('nc-email').value.trim(),type:document.getElementById('nc-type').value,company:document.getElementById('nc-company').value.trim(),notes:document.getElementById('nc-notes').value.trim()});closeModal('modal-contact');renderContacts();}

// ══════════════════════════════════════════════════════
// ADMIN
// ══════════════════════════════════════════════════════
function adminSection(sec){
  const el=document.getElementById('admin-section');
  if(sec==='users'){el.innerHTML=`<div class="card"><div class="card-header"><span class="card-title">Utilizadores</span></div><div class="table-wrap"><table><thead><tr><th>Nome</th><th>Username</th><th>Perfil</th><th>Tel. WA Business</th></tr></thead><tbody>${USERS.map(u=>`<tr><td><div style="display:flex;align-items:center;gap:7px"><div style="width:26px;height:26px;border-radius:50%;background:var(--brand);color:var(--accent);display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:600">${u.initials}</div>${u.name}</div></td><td class="td-mono">${u.id}</td><td><span class="badge ${u.role==='admin'?'badge-quality':u.role==='op'?'badge-new':'badge-gray'}">${u.role==='admin'?'Admin':u.role==='op'?'Operacional':'Comercial'}</span></td><td class="td-muted">${u.phone}</td></tr>`).join('')}</tbody></table></div></div>`;}
  else if(sec==='email'){el.innerHTML=`<div class="card"><div class="card-header"><span class="card-title">Integração IMAP — Captura automática de leads</span></div><div class="card-body"><div class="alert-item alert-info" style="margin-bottom:14px"><div class="alert-icon">🔌</div><div class="alert-body">Ligação ao servidor de email próprio (cPanel/IMAP). As leads recebidas criam automaticamente um novo deal no CRM.</div></div><div class="fr"><div class="fg"><label class="fl">Servidor IMAP</label><input class="fc" placeholder="mail.importhub.pt"></div><div class="fg"><label class="fl">Porta</label><input class="fc" value="993"></div></div><div class="fr"><div class="fg"><label class="fl">Email</label><input class="fc" placeholder="leads@importhub.pt"></div><div class="fg"><label class="fl">Palavra-passe</label><input class="fc" type="password"></div></div><div class="fg"><label class="fl">Assunto que identifica leads</label><input class="fc" placeholder="Novo pedido de importação"></div><div style="display:flex;gap:8px;margin-top:8px"><button class="btn btn-ghost">Testar ligação</button><button class="btn btn-accent">Guardar</button></div></div></div>`;}
  else if(sec==='alert-rules'){el.innerHTML=`<div class="card"><div class="card-header"><span class="card-title">Regras de alertas automáticos</span></div><div class="card-body"><p style="font-size:12px;color:var(--text2);margin-bottom:14px">Os alertas são calculados em tempo real com base no estado das checklists e na fase de cada deal.</p>${ALERT_RULES.map(r=>`<div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border2)"><span style="font-size:14px">${r.icon}</span><div style="flex:1"><div style="font-size:12px;font-weight:500">${r.msg}</div><div style="font-size:11px;color:var(--text3)">${r.role==='comercial'?'Comercial':'Operacional'} · fase ≥ ${r.minStage}${r.maxStage!==undefined?' e ≤ '+r.maxStage:''}</div></div><span class="badge ${r.type==='danger'?'badge-red':'badge-amber'}">${r.type==='danger'?'Crítico':'Atenção'}</span></div>`).join('')}</div></div>`;}
  else if(sec==='stats'){el.innerHTML=`<div class="card"><div class="card-header"><span class="card-title">Performance por comercial</span></div><div class="table-wrap"><table><thead><tr><th>Comercial</th><th>Deals ativos</th><th>Adjudicados</th><th>Entregues</th><th>Perdidos</th><th>Alertas críticos</th></tr></thead><tbody>${USERS.filter(u=>u.role==='comercial').map(u=>{const d=deals.filter(x=>x.comercialId===u.id);const prevU=currentUser;const crit=d.filter(x=>x.stage!==99).reduce((sum,deal)=>sum+getAlertsForDeal(deal).filter(a=>a.type==='danger').length,0);return`<tr><td style="font-weight:500">${u.name}</td><td>${d.filter(x=>x.stage!==99).length}</td><td style="color:var(--accent-dark);font-weight:500">${d.filter(x=>x.stage>=4&&x.stage!==99).length}</td><td style="color:var(--green)">${d.filter(x=>x.stage===10).length}</td><td style="color:var(--red)">${d.filter(x=>x.stage===99).length}</td><td>${crit>0?`<span class="badge badge-red">${crit}</span>`:'<span class="badge badge-green">✓</span>'}</td></tr>`;}).join('')}</tbody></table></div></div>`;}
  else if(sec==='templates'){el.innerHTML=`<div class="card"><div class="card-header"><span class="card-title">Templates de comunicação</span></div><div class="card-body"><p style="font-size:12px;color:var(--text2);margin-bottom:14px">Variáveis: {{Nome}}, {{LinkProposta}}, {{Viatura}}, {{Comercial}}</p>${['Confirmação de pedido (automático)','Envio de proposta — email','Envio de proposta — WhatsApp','1.º Follow-up — email','1.º Follow-up — WhatsApp','2.º Follow-up — email','2.º Follow-up — WhatsApp','Email sem proposta (sem qualidade)','Retoma futura (programado)','Acompanhamento venda veículo atual'].map(t=>`<div style="display:flex;align-items:center;justify-content:space-between;padding:9px 0;border-bottom:1px solid var(--border2)"><span style="font-size:12px">${t}</span><button class="btn btn-ghost btn-sm">Editar</button></div>`).join('')}</div></div>`;}
  else if(sec==='integration'){el.innerHTML=`<div class="card"><div class="card-header"><span class="card-title">Integração — Software de propostas e WhatsApp</span></div><div class="card-body"><div class="alert-item alert-warn" style="margin-bottom:14px"><div class="alert-icon">🔗</div><div class="alert-body"><div class="alert-title">Modo atual: integração manual assistida</div><div class="alert-sub">Integração automática disponível após acesso ao código do crm.importhub.pt</div></div></div><div class="fsec">WhatsApp Business por comercial</div>${USERS.filter(u=>u.role==='comercial').map(u=>`<div class="fr" style="margin-bottom:8px"><div class="fg" style="margin-bottom:0"><label class="fl">${u.name}</label><input class="fc" value="${u.phone}"></div><div class="fg" style="margin-bottom:0"><label class="fl">Provider</label><select class="fc" disabled><option>WhatsApp Web (atual)</option><option>360dialog</option><option>Twilio</option><option>Z-API</option></select></div></div>`).join('')}<button class="btn btn-accent" style="margin-top:12px">Guardar</button></div></div>`;}

}



// ══════════════════════════════════════════════════════
// LEADS — DATA & STATE
// ══════════════════════════════════════════════════════
// Lead states: nova | assumida | respondida | convertida | ignorada
let inboxLeads = [
  {
    id:'lead-demo-1',
    type:'form',
    status:'nova',
    assumedBy: null,
    assumedAt: null,
    respondedAt: null,
    receivedAt: new Date(Date.now()-1000*60*12).toISOString(),
    raw:`De: Fernando Rui Azevedo\nEmail: fernandoruiazevedo@gmail.com\nTelefone: 933213000\n\nComo nos conheceu?: Pesquisa Google\n\nMarca: Porsche\nModelo: 911\nAno desde: 1999\nQuilometragem até: 100000\nPreço até: 77000\n\nOutras Características | Mensagem:\nJá tenho o carro em vista`,
    parsed:{name:'Fernando Rui Azevedo',phone:'933213000',email:'fernandoruiazevedo@gmail.com',brand:'Porsche',model:'911',year:'1999',km:'100.000',budget:'77000',source:'Pesquisa Google',notes:'Já tenho o carro em vista'},
    dealId: null,
    notes: ''
  },
  {
    id:'lead-demo-2',
    type:'free',
    status:'assumida',
    assumedBy:'ze',
    assumedAt: new Date(Date.now()-1000*60*45).toISOString(),
    respondedAt: null,
    receivedAt: new Date(Date.now()-1000*60*60).toISOString(),
    raw:`Boa tarde,\n\nEstou interessado em importar um BMW X5 de 2021, até 65.000€ e menos de 80.000km.\nContacto: 912 111 222\n\nObrigado,\nRicardo Silva\nricardo@empresa.pt`,
    parsed:{name:'Ricardo Silva',phone:'912111222',email:'ricardo@empresa.pt',brand:'BMW',model:'X5',year:'2021',km:'80.000',budget:'65000',source:'Email direto',notes:''},
    dealId: null,
    notes: ''
  }
];
let nextLeadId = 3;
let convertingLeadId = null;
let leadsPageFilter = 'todas';

const LEAD_STATUS = {
  nova:      {label:'Nova',                badge:'badge-new',    icon:'🔵'},
  assumida:  {label:'Assumida',            badge:'badge-amber',  icon:'🟡'},
  respondida:{label:'Respondida',          badge:'badge-green',  icon:'🟢'},
  convertida:{label:'Convertida',          badge:'badge-gray',   icon:'✅'},
  ignorada:  {label:'Ignorada',            badge:'badge-red',    icon:'❌'},
};

// ── HELPERS ──────────────────────────────────────────
function parseFormEmail(text) {
  const get = (label) => {
    const m = text.match(new RegExp(label + '[:\\s]+([^\\n]+)', 'i'));
    return m ? m[1].trim() : '';
  };
  return {
    name:   get('De') || get('Nome'),
    phone:  get('Telefone') || get('Tel'),
    email:  (text.match(/Email[:\s]+([^\s\n]+@[^\s\n]+)/i)||[])[1]?.trim() || '',
    brand:  get('Marca'),
    model:  get('Modelo'),
    year:   get('Ano desde') || get('Ano'),
    km:     get('Quilometragem até') || get('Km'),
    budget: get('Preço até') || get('Orçamento'),
    source: get('Como nos conheceu') || 'Formulário',
    notes:  get('Mensagem') || get('Outras Características \\| Mensagem') || '',
  };
}

function timeAgo(iso) {
  const mins = Math.floor((Date.now() - new Date(iso)) / 60000);
  if(mins < 60) return `há ${mins} min`;
  if(mins < 1440) return `há ${Math.floor(mins/60)}h`;
  return `há ${Math.floor(mins/1440)}d`;
}

function myLeads() {
  // Comerciais: vêem todas as novas + as que assumiram
  if(currentUser.role === 'comercial')
    return inboxLeads.filter(l => l.status === 'nova' || l.assumedBy === currentUser.id);
  return inboxLeads; // admins e operacional vêem todas
}

// ── DASHBOARD SUMMARY CARD ────────────────────────────
function renderInbox() {
  const all = inboxLeads;
  const nova = all.filter(l=>l.status==='nova').length;
  const assumida = all.filter(l=>l.status==='assumida').length;
  const respondida = all.filter(l=>l.status==='respondida').length;

  const counts = document.getElementById('leads-summary-counts');
  if(!counts) return;
  counts.innerHTML = `
    <div style="text-align:center;padding:4px 10px;background:var(--blue-bg);border-radius:8px">
      <div style="font-size:16px;font-weight:600;color:var(--blue)">${nova}</div>
      <div style="font-size:10px;color:var(--blue);opacity:.8">Novas</div>
    </div>
    <div style="text-align:center;padding:4px 10px;background:var(--amber-bg);border-radius:8px">
      <div style="font-size:16px;font-weight:600;color:var(--amber)">${assumida}</div>
      <div style="font-size:10px;color:var(--amber);opacity:.8">Assumidas</div>
    </div>
    <div style="text-align:center;padding:4px 10px;background:var(--green-bg);border-radius:8px">
      <div style="font-size:16px;font-weight:600;color:var(--green)">${respondida}</div>
      <div style="font-size:10px;color:var(--green);opacity:.8">Respondidas</div>
    </div>`;

  // Nav badge for new leads
  const navBtn = document.getElementById('nav-leads');
  if(navBtn) {
    navBtn.innerHTML = nova > 0
      ? `📬 Leads <span class="nav-badge">${nova}</span>`
      : '📬 Leads';
  }
}

// ── LEADS PAGE ────────────────────────────────────────
function renderLeadsPage() {
  const all = inboxLeads;
  const q = (document.getElementById('leads-search')?.value||'').toLowerCase();

  // Counters
  const counts = {
    todas: all.length,
    nova: all.filter(l=>l.status==='nova').length,
    assumida: all.filter(l=>l.status==='assumida' && !l.respondedAt).length,
    respondida: all.filter(l=>l.status==='respondida').length,
    ass_nao_resp: all.filter(l=>l.status==='assumida' && !l.respondedAt).length,
    convertida: all.filter(l=>l.status==='convertida').length,
  };

  const countersEl = document.getElementById('leads-counters');
  if(countersEl) {
    const counterDefs = [
      {key:'todas',    label:'Total',              val:all.length,           color:'var(--text)'},
      {key:'nova',     label:'Novas',              val:counts.nova,          color:'var(--blue)'},
      {key:'assumida', label:'Assumidas',          val:all.filter(l=>l.status==='assumida').length, color:'var(--amber)'},
      {key:'respondida',label:'Respondidas',       val:counts.respondida,    color:'var(--green)'},
      {key:'convertida',label:'Convertidas',       val:counts.convertida,    color:'var(--text3)'},
    ];
    countersEl.innerHTML = counterDefs.map(c=>`
      <div class="lead-counter ${leadsPageFilter===c.key?'active':''}" onclick="setLeadsFilter('${c.key}')">
        <div class="lead-counter-val" style="color:${c.color}">${c.val}</div>
        <div class="lead-counter-lbl">${c.label}</div>
      </div>`).join('');
  }

  // Filter tabs
  const tabsEl = document.getElementById('leads-filter-tabs');
  if(tabsEl) {
    const tabs = [
      {key:'todas', label:'Todas'},
      {key:'nova', label:'🔵 Novas'},
      {key:'assumida', label:'🟡 Assumidas'},
      {key:'respondida', label:'🟢 Respondidas'},
      {key:'convertida', label:'✅ Convertidas'},
      {key:'ignorada', label:'❌ Ignoradas'},
    ];
    tabsEl.innerHTML = tabs.map(t=>`<button class="lead-filter-tab ${leadsPageFilter===t.key?'active':''}" onclick="setLeadsFilter('${t.key}')">${t.label}</button>`).join('');
  }

  // Filtered list
  let filtered = inboxLeads.filter(l => {
    const matchFilter = leadsPageFilter==='todas' || l.status===leadsPageFilter;
    const p = l.parsed;
    const matchQ = !q || (p.name+p.email+p.phone+p.brand+p.model).toLowerCase().includes(q);
    return matchFilter && matchQ;
  });

  document.getElementById('leads-page-sub').textContent = `${filtered.length} lead${filtered.length!==1?'s':''} · clique para ver detalhes`;

  const tbody = document.getElementById('leads-tbody');
  if(!tbody) return;

  if(!filtered.length) {
    tbody.innerHTML = `<tr><td colspan="9"><div class="empty"><div class="empty-icon">📬</div><div class="empty-title">Nenhuma lead nesta categoria</div></div></td></tr>`;
    return;
  }

  tbody.innerHTML = filtered.map(l => {
    const p = l.parsed;
    const st = LEAD_STATUS[l.status] || LEAD_STATUS.nova;
    const budget = p.budget ? Number(String(p.budget).replace(/\D/g,'')).toLocaleString('pt-PT')+'€' : '—';
    const car = [p.brand, p.model].filter(Boolean).join(' ') || '—';
    const owner = l.assumedBy ? uName(l.assumedBy) : '—';
    const isMine = l.assumedBy === currentUser.id;
    return `<tr style="cursor:pointer" onclick="openLeadDetail('${l.id}')">
      <td><div style="font-weight:500">${p.name||'(sem nome)'}</div>
        <span class="inbox-badge ${l.type==='form'?'inbox-form':'inbox-free'}">${l.type==='form'?'Formulário':'Email direto'}</span>
      </td>
      <td class="td-muted" style="font-size:12px"><div>${p.phone||'—'}</div><div>${p.email||'—'}</div></td>
      <td style="font-size:12px">${car}${p.year?' ('+p.year+')':''}</td>
      <td style="font-size:12px;font-weight:500;color:var(--accent-dark)">${budget}</td>
      <td class="td-muted" style="font-size:12px">${p.source||'—'}</td>
      <td><span class="badge ${st.badge}">${st.icon} ${st.label}</span></td>
      <td class="td-muted" style="font-size:12px">${owner}${isMine?' (eu)':''}</td>
      <td class="td-muted" style="font-size:11px">${timeAgo(l.receivedAt)}</td>
      <td><button class="btn btn-ghost btn-sm" onclick="event.stopPropagation();openLeadDetail('${l.id}')">Ver →</button>${l.dealId?` <button class="btn btn-ghost btn-sm" onclick="event.stopPropagation();openDeal(${l.dealId})" style="font-size:11px">Deal →</button>`:''}</td>
    </tr>`;
  }).join('');
}

function setLeadsFilter(f) {
  leadsPageFilter = f;
  renderLeadsPage();
}

// ── LEAD DETAIL ───────────────────────────────────────
function openLeadDetail(id) {
  const lead = inboxLeads.find(l=>l.id===id);
  if(!lead) return;
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-lead-detail').classList.add('active');
  document.getElementById('nav-leads')?.classList.add('active');
  renderLeadDetail(lead);
}

function renderLeadDetail(lead) {
  const p = lead.parsed;
  const st = LEAD_STATUS[lead.status] || LEAD_STATUS.nova;
  const isNova = lead.status === 'nova';
  const isMine = lead.assumedBy === currentUser.id;
  const canAct = currentUser.role === 'admin' || currentUser.role === 'comercial';
  const budget = p.budget ? Number(String(p.budget).replace(/\D/g,'')).toLocaleString('pt-PT')+'€' : '—';

  document.getElementById('lead-detail-content').innerHTML = `
    <div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:16px;flex-wrap:wrap;gap:10px">
      <div>
        <div style="display:flex;align-items:center;gap:10px;margin-bottom:5px">
          <h2 style="font-family:'DM Serif Display',serif;font-size:21px;color:var(--brand)">${p.name||'Lead sem nome'}</h2>
          <span class="badge ${st.badge}">${st.icon} ${st.label}</span>
          <span class="inbox-badge ${lead.type==='form'?'inbox-form':'inbox-free'}">${lead.type==='form'?'Formulário':'Email direto'}</span>
        </div>
        <div style="font-size:12px;color:var(--text3)">Recebido ${timeAgo(lead.receivedAt)}${lead.assumedBy?' · Assumido por '+uName(lead.assumedBy):''}</div>
      </div>
      <div style="display:flex;gap:7px;flex-wrap:wrap">
        ${isNova && canAct ? `<button class="btn btn-accent" onclick="assumeLead('${lead.id}')">Assumir esta lead</button>` : ''}
        ${isMine && lead.status==='assumida' ? `<button class="btn btn-primary" onclick="markLeadResponded('${lead.id}')">✓ Respondida — Qualificar →</button>` : ''}
        ${lead.dealId ? `<button class="btn btn-ghost" onclick="openDeal(${lead.dealId})">Ver deal →</button>` : ''}
        ${lead.status!=='ignorada' && lead.status!=='nova' && (isMine||currentUser.role==='admin') ? `<button class="btn btn-danger btn-sm" onclick="ignoreLead('${lead.id}')">Ignorar</button>` : ''}
      </div>
    </div>

    <div style="display:grid;grid-template-columns:1fr 320px;gap:14px;align-items:start">
      <div style="display:flex;flex-direction:column;gap:12px">

        <div class="card"><div class="card-header"><span class="card-title">📋 Dados do pedido</span></div>
          <div class="card-body">
            <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px">
              <div><div class="fl" style="margin-bottom:2px">Marca / Modelo</div><div style="font-weight:500">${p.brand||'—'} ${p.model||''}</div></div>
              <div><div class="fl" style="margin-bottom:2px">Ano desde</div><div>${p.year||'—'}</div></div>
              <div><div class="fl" style="margin-bottom:2px">Km até</div><div>${p.km||'—'}</div></div>
            </div>
            <div style="margin-top:12px;padding-top:12px;border-top:1px solid var(--border2);display:grid;grid-template-columns:1fr 1fr;gap:12px">
              <div><div class="fl" style="margin-bottom:2px">Orçamento máx.</div><div style="font-weight:500;color:var(--accent-dark);font-size:15px">${budget}</div></div>
              <div><div class="fl" style="margin-bottom:2px">Origem</div><div>${p.source||'—'}</div></div>
            </div>
            ${p.notes?`<div style="margin-top:12px;padding-top:12px;border-top:1px solid var(--border2)"><div class="fl" style="margin-bottom:4px">Mensagem do cliente</div><div style="font-size:13px;color:var(--text2);background:var(--bg);padding:10px;border-radius:var(--radius);line-height:1.6">${p.notes}</div></div>`:''}
          </div>
        </div>

        <div class="card"><div class="card-header"><span class="card-title">📧 Email original</span></div>
          <div class="card-body" style="padding:14px 16px">
            <pre style="font-size:12px;color:var(--text2);line-height:1.8;white-space:pre-wrap;font-family:monospace;background:var(--bg);padding:12px;border-radius:var(--radius)">${lead.raw}</pre>
          </div>
        </div>

        <div class="card"><div class="card-header"><span class="card-title">📝 Notas internas</span></div>
          <div class="card-body">
            <textarea class="fc" id="lead-notes-${lead.id}" style="min-height:70px">${lead.notes||''}</textarea>
            <button class="btn btn-ghost btn-sm" style="margin-top:7px" onclick="saveLeadNotes('${lead.id}')">Guardar notas</button>
          </div>
        </div>
      </div>

      <div style="display:flex;flex-direction:column;gap:12px">
        <div class="card"><div class="card-header"><span class="card-title">👤 Cliente</span></div>
          <div class="card-body" style="padding:12px 14px">
            <div style="font-weight:500;font-size:14px;margin-bottom:10px">${p.name||'—'}</div>
            <table style="width:100%;font-size:12px">
              <tr><td style="color:var(--text3);padding:3px 0">Telemóvel</td><td style="text-align:right">${p.phone?`<a href="tel:${p.phone}">${p.phone}</a>`:'—'}</td></tr>
              <tr><td style="color:var(--text3);padding:3px 0">Email</td><td style="text-align:right;word-break:break-all">${p.email?`<a href="mailto:${p.email}">${p.email}</a>`:'—'}</td></tr>
              <tr><td style="color:var(--text3);padding:3px 0">Origem</td><td style="text-align:right">${p.source||'—'}</td></tr>
            </table>
            ${p.phone?`<div style="display:flex;gap:6px;margin-top:10px">
              ${waBtn({id:-1,clientName:p.name,phone:p.phone,email:p.email,brand:p.brand,model:p.model,proposalLink:''},'proposal')}
              <a href="tel:${p.phone}" class="btn btn-ghost btn-sm">📞 Ligar</a>
            </div>`:''}
          </div>
        </div>

        <div class="card"><div class="card-header"><span class="card-title">🕐 Histórico</span></div>
          <div class="card-body" style="padding:12px 14px">
            <div class="timeline">
              <div class="tl-item"><div class="tl-dot done"></div><div><div class="tl-title">Lead recebida</div><div class="tl-date">${timeAgo(lead.receivedAt)}</div></div></div>
              ${lead.assumedBy?`<div class="tl-item"><div class="tl-dot done"></div><div><div class="tl-title">Assumida por ${uName(lead.assumedBy)}</div><div class="tl-date">${lead.assumedAt?timeAgo(lead.assumedAt):''}</div></div></div>`:''}
              ${lead.respondedAt?`<div class="tl-item"><div class="tl-dot done"></div><div><div class="tl-title">Marcada como respondida</div><div class="tl-date">${timeAgo(lead.respondedAt)}</div></div></div>`:''}
              ${lead.status==='convertida'?`<div class="tl-item"><div class="tl-dot done"></div><div><div class="tl-title">Convertida em deal</div></div></div>`:''}
              ${lead.status==='ignorada'?`<div class="tl-item"><div class="tl-dot alert"></div><div><div class="tl-title" style="color:var(--red)">Ignorada</div></div></div>`:''}
            </div>
          </div>
        </div>
      </div>
    </div>`;
}

function assumeLead(id) {
  const lead = inboxLeads.find(l=>l.id===id);
  if(!lead) return;
  lead.status = 'assumida';
  lead.assumedBy = currentUser.id;
  lead.assumedAt = new Date().toISOString();
  renderLeadDetail(lead);
  renderInbox();
  updateNavBadge();
}

function markLeadResponded(id) {
  const lead = inboxLeads.find(l=>l.id===id);
  if(!lead) return;
  // Open qualify modal — deal is created on confirm
  leadQualifyingId = id;
  selectedLeadQual = '';
  document.querySelectorAll('.qual-opt').forEach(e=>e.classList.remove('selected'));
  document.getElementById('lq-info').style.display = 'none';
  document.getElementById('lq-link').value = '';
  document.getElementById('lq-confirm-btn').disabled = true;
  const p = lead.parsed;
  document.getElementById('lq-lead-info').textContent =
    `${p.name||'—'} · ${p.brand||''} ${p.model||''}${p.budget?' · até '+Number(String(p.budget).replace(/\D/g,'')).toLocaleString('pt-PT')+'€':''}`;
  openModal('modal-lead-qualify');
}

let leadQualifyingId = null;
let selectedLeadQual = '';

function selectLeadQual(q) {
  selectedLeadQual = q;
  document.querySelectorAll('#modal-lead-qualify .qual-opt').forEach(e=>e.classList.remove('selected'));
  document.querySelector(`#modal-lead-qualify .q-${q}`)?.classList.add('selected');
  const info = {
    quality:'Follow-up completo: liga D+2 → email+WA → liga D+4 → email+WA → termina.',
    bad:'Proposta + 1 follow-up (email+WA). Sem chamadas.',
    budget:'Proposta acima do orçamento + 1 follow-up (email+WA). Sem chamadas.',
    noqual:'Email de recusa enviado. Sem proposta. Lead fecha.',
  };
  const el = document.getElementById('lq-info');
  el.style.display = 'block';
  el.textContent = info[q] || '';
  document.getElementById('lq-confirm-btn').disabled = false;
}

function confirmLeadQual() {
  if(!selectedLeadQual) return;
  const lead = inboxLeads.find(l=>l.id===leadQualifyingId);
  if(!lead) return;
  const p = lead.parsed;

  // Mark lead as responded
  lead.status = 'respondida';
  lead.respondedAt = new Date().toISOString();

  // Create deal automatically
  const d = {
    id: nextDID++,
    clientName: p.name || 'Cliente',
    phone: p.phone || '',
    email: p.email || '',
    type: 'Particular',
    brand: p.brand || '',
    model: p.model || '',
    year: p.year || '',
    km: p.km || '',
    budget: p.budget ? String(p.budget).replace(/\D/g,'') : '',
    comercialId: lead.assumedBy || currentUser.id,
    source: p.source || 'Email direto',
    notes: p.notes || '',
    qual: selectedLeadQual,
    proposalLink: document.getElementById('lq-link').value.trim(),
    stage: selectedLeadQual === 'noqual' ? 99 : 2,
    chassis: '', location: '', transporter: '',
    followupStep: 0,
    createdAt: new Date().toISOString().split('T')[0],
    checks: {}
  };
  deals.unshift(d);

  // Mark lead as responded + link deal (but keep as respondida, not convertida)
  lead.status = 'respondida';
  lead.respondedAt = new Date().toISOString();
  lead.dealId = d.id;

  // Add to contacts if new
  if(!contacts.find(c=>c.phone===d.phone))
    contacts.unshift({id:nextCID++,name:d.clientName,phone:d.phone,email:d.email,type:'Particular',company:'',notes:''});

  closeModal('modal-lead-qualify');
  renderInbox();
  updateNavBadge();
  // Go straight to the deal
  openDeal(d.id);
}

function ignoreLead(id) {
  if(!confirm('Tens a certeza que queres ignorar esta lead?')) return;
  const lead = inboxLeads.find(l=>l.id===id);
  if(!lead) return;
  lead.status = 'ignorada';
  renderLeadDetail(lead);
  renderInbox();
  updateNavBadge();
}

function saveLeadNotes(id) {
  const lead = inboxLeads.find(l=>l.id===id);
  const el = document.getElementById('lead-notes-'+id);
  if(lead && el) { lead.notes = el.value; }
}

// ── CONVERT TO DEAL ───────────────────────────────────
function openConvertLead(leadId) {
  const lead = inboxLeads.find(l=>l.id===leadId);
  if(!lead) return;
  convertingLeadId = leadId;
  const p = lead.parsed;

  document.getElementById('lead-email-preview').textContent = lead.raw;
  document.getElementById('cl-name').value = p.name || '';
  document.getElementById('cl-phone').value = p.phone || '';
  document.getElementById('cl-email').value = p.email || '';
  document.getElementById('cl-brand').value = p.brand || '';
  document.getElementById('cl-model').value = p.model || '';
  document.getElementById('cl-year').value = p.year || '';
  document.getElementById('cl-km').value = p.km || '';
  document.getElementById('cl-budget').value = p.budget ? String(p.budget).replace(/\D/g,'') : '';
  document.getElementById('cl-source').value = p.source || 'Email direto';
  document.getElementById('cl-notes').value = p.notes || '';

  const sel = document.getElementById('cl-comercial');
  sel.innerHTML = '';
  USERS.filter(u=>u.role==='comercial').forEach(u=>{
    const o = document.createElement('option');
    o.value = u.id; o.textContent = u.name;
    if(lead.assumedBy === u.id) o.selected = true;
    sel.appendChild(o);
  });

  openModal('modal-convert-lead');
}

function convertLead() {
  const name = document.getElementById('cl-name').value.trim();
  const phone = document.getElementById('cl-phone').value.trim();
  if(!name || !phone) { alert('Nome e telemóvel são obrigatórios.'); return; }

  const d = {
    id: nextDID++,
    clientName: name, phone,
    email: document.getElementById('cl-email').value.trim(),
    type: 'Particular',
    brand: document.getElementById('cl-brand').value.trim(),
    model: document.getElementById('cl-model').value.trim(),
    year: document.getElementById('cl-year').value.trim(),
    km: document.getElementById('cl-km').value.trim(),
    budget: document.getElementById('cl-budget').value.trim(),
    comercialId: document.getElementById('cl-comercial').value,
    source: document.getElementById('cl-source').value.trim() || 'Email direto',
    notes: document.getElementById('cl-notes').value.trim(),
    stage: 0, qual: '', proposalLink: '', chassis: '', location: '',
    transporter: '', followupStep: 0,
    createdAt: new Date().toISOString().split('T')[0],
    checks: {}
  };
  deals.unshift(d);
  if(!contacts.find(c=>c.phone===phone))
    contacts.unshift({id:nextCID++,name,phone,email:d.email,type:'Particular',company:'',notes:''});

  // Update lead status
  const lead = inboxLeads.find(l=>l.id===convertingLeadId);
  if(lead) { lead.status = 'convertida'; lead.dealId = d.id; }

  closeModal('modal-convert-lead');
  renderInbox();
  updateNavBadge();
  openDeal(d.id);
}

function dismissLead() {
  ignoreLead(convertingLeadId);
  closeModal('modal-convert-lead');
}

// ── SIMULATE ──────────────────────────────────────────
function openSimulateLead() {
  document.getElementById('sim-email-text').value = '';
  openModal('modal-simulate-lead');
}

function simulateLead(type) {
  let raw;
  if(type === 'form') {
    raw = `De: Ana Rodrigues\nEmail: ana.rodrigues@gmail.com\nTelefone: 916543210\n\nComo nos conheceu?: Instagram\n\nMarca: BMW\nModelo: X3\nAno desde: 2021\nQuilometragem até: 50000\nPreço até: 45000\n\nOutras Características | Mensagem:\nPrefiro cor escura, de preferência cinzento ou preto`;
  } else {
    raw = `Olá,\n\nEstou interessado em importar um Mercedes GLC de 2022, com menos de 60.000 km e até 55.000€. Vi o vosso website.\n\nContacto: 912 345 678\n\nCumprimentos,\nPedro Mota\npedro.mota@empresa.pt`;
  }
  inboxLeads.unshift({
    id:'lead-sim-'+(nextLeadId++), type,
    status:'nova', assumedBy:null, assumedAt:null, respondedAt:null,
    receivedAt:new Date().toISOString(),
    raw, parsed:parseFormEmail(raw), dealId:null, notes:''
  });
  closeModal('modal-simulate-lead');
  renderInbox();
  if(document.getElementById('page-leads')?.classList?.contains('active')) renderLeadsPage();
}

function simulateLeadFromText() {
  const text = document.getElementById('sim-email-text').value.trim();
  if(!text) { alert('Cola o conteúdo do email primeiro.'); return; }
  const isForm = /marca:/i.test(text) && /modelo:/i.test(text);
  inboxLeads.unshift({
    id:'lead-sim-'+(nextLeadId++), type:isForm?'form':'free',
    status:'nova', assumedBy:null, assumedAt:null, respondedAt:null,
    receivedAt:new Date().toISOString(),
    raw:text, parsed:parseFormEmail(text), dealId:null, notes:''
  });
  closeModal('modal-simulate-lead');
  renderInbox();
  if(document.getElementById('page-leads')?.classList?.contains('active')) renderLeadsPage();
}


// ══════════════════════════════════════════════════════
// DAILY PLANNER — full page engine
// ══════════════════════════════════════════════════════
function addBusinessDays(dateStr, n) {
  const d = new Date(dateStr + 'T12:00:00');
  let added = 0;
  while(added < n) {
    d.setDate(d.getDate() + 1);
    const dow = d.getDay();
    if(dow !== 0 && dow !== 6) added++;
  }
  return d.toISOString().split('T')[0];
}
function toDateStr(d) { return d.toISOString().split('T')[0]; }
function isBusinessDay(dateStr) { const dow = new Date(dateStr+'T12:00:00').getDay(); return dow!==0&&dow!==6; }

// Manual follow-ups store: {id, dealId, type, dueDate, note, done, createdBy}
let manualFUs = [];
let nextMFUID = 1;
let mfuDealId = null;
let mfuType = '';
let snoozeTaskId = null;
let snoozeTaskIsManual = false;
let meudioActiveDay = 0; // 0=today, 1=tomorrow, 2=day after

function tasksForDeal(d) {
  if(d.stage===99||d.stage>=3||!d.qual||d.qual==='noqual') return [];
  const tasks = [];
  const sent = d.createdAt;
  if(d.qual==='quality') {
    const call1 = addBusinessDays(sent,1);
    const fu1   = addBusinessDays(sent,1);
    const call2 = addBusinessDays(sent,3);
    const fu2   = addBusinessDays(sent,3);
    if(d.followupStep<1){
      tasks.push({id:`auto-${d.id}-c1`,type:'call',     label:'1.ª chamada',         dueDate:call1, dealId:d.id, done:false, auto:true});
      tasks.push({id:`auto-${d.id}-e1`,type:'email_wa', label:'Email+WA (não atendeu)',dueDate:fu1,  dealId:d.id, done:false, auto:true});
    }
    if(d.followupStep<2){
      tasks.push({id:`auto-${d.id}-c2`,type:'call',     label:'2.ª chamada',         dueDate:call2, dealId:d.id, done:d.followupStep>=1, auto:true});
      tasks.push({id:`auto-${d.id}-e2`,type:'email_wa', label:'Email+WA (2.º follow-up)',dueDate:fu2,dealId:d.id, done:d.followupStep>=1, auto:true});
    }
  } else {
    const fu1 = addBusinessDays(sent,1);
    if(d.followupStep<1)
      tasks.push({id:`auto-${d.id}-e1`,type:'email_wa',label:'Email+WA follow-up',dueDate:fu1,dealId:d.id,done:false,auto:true});
  }
  return tasks;
}

function getAllTasksForDay(dayStr, todayStr) {
  const myD = myDeals().filter(x=>x.stage!==99&&x.stage<3&&x.qual&&x.qual!=='noqual');
  const autoTasks = myD.flatMap(d=>tasksForDeal(d));

  // For today: include overdue auto tasks
  let auto = dayStr === todayStr
    ? autoTasks.filter(t=>t.dueDate<=dayStr&&!t.done)
    : autoTasks.filter(t=>t.dueDate===dayStr&&!t.done);

  // Manual tasks for this day
  const manual = manualFUs.filter(m=>
    m.createdBy===currentUser.id && !m.done &&
    (dayStr===todayStr ? m.dueDate<=dayStr : m.dueDate===dayStr)
  );

  // Group by dealId, merge types
  const map = {};
  [...auto, ...manual].forEach(t => {
    if(!map[t.dealId]) map[t.dealId] = {dealId:t.dealId, types:new Set(), tasks:[], note:''};
    map[t.dealId].types.add(t.type==='both'?'call_ew':t.type);
    if(t.type==='both'){map[t.dealId].types.add('call');map[t.dealId].types.add('email_wa');}
    map[t.dealId].tasks.push(t);
    if(t.note) map[t.dealId].note = t.note;
  });
  return Object.values(map);
}

// ── DASHBOARD SUMMARY (compact card) ─────────────────
function renderPlanner() {
  const today = new Date();
  const todayStr = toDateStr(today);
  const dateLabel = document.getElementById('planner-date');
  if(dateLabel) dateLabel.textContent = today.toLocaleDateString('pt-PT',{weekday:'long',day:'numeric',month:'long'});

  const groups = getAllTasksForDay(todayStr, todayStr);
  const calls = groups.filter(g=>g.types.has('call')).length;
  const ews   = groups.filter(g=>g.types.has('email_wa')).length;
  const total = groups.length;

  const summary = document.getElementById('planner-summary');
  if(!summary) return;
  if(total===0) {
    summary.innerHTML = '<span style="font-size:12px;color:var(--green)">✅ Sem tarefas hoje</span>';
  } else {
    summary.innerHTML = [
      calls ? `<span class="badge badge-gray">📞 ${calls} chamada${calls!==1?'s':''}</span>` : '',
      ews   ? `<span class="badge badge-gray">📨 ${ews} email+WA</span>` : '',
      `<span class="badge badge-amber">${total} cliente${total!==1?'s':''}</span>`,
    ].filter(Boolean).join('');
  }
}

// ── MEU DIA PAGE ──────────────────────────────────────
function renderMeuDia() {
  const today = new Date();
  const todayStr = toDateStr(today);

  // Build 3 business days
  const days = [];
  let cursor = new Date(today);
  while(days.length < 3) {
    const str = toDateStr(cursor);
    if(isBusinessDay(str)) days.push(str);
    cursor.setDate(cursor.getDate()+1);
  }
  const dayLabels = ['Hoje','Amanhã','Depois de amanhã'];

  // Sub header
  const sub = document.getElementById('meudia-sub');
  if(sub) sub.textContent = today.toLocaleDateString('pt-PT',{weekday:'long',day:'numeric',month:'long',year:'numeric'});

  // Tabs
  const tabs = document.getElementById('meudia-tabs');
  if(tabs) {
    tabs.innerHTML = days.map((d,i) => {
      const groups = getAllTasksForDay(d, todayStr);
      const count = groups.length;
      return `<button class="lead-filter-tab ${meudioActiveDay===i?'active':''}" onclick="setMeuDiaDay(${i})">
        ${dayLabels[i]}${count>0?` <span class="nav-badge" style="background:${i===0?'var(--accent-dark)':'var(--text3)'}">${count}</span>`:''}
      </button>`;
    }).join('');
  }

  const dayStr = days[meudioActiveDay];
  const groups = getAllTasksForDay(dayStr, todayStr);
  const list = document.getElementById('meudia-list');
  if(!list) return;

  if(!groups.length) {
    list.innerHTML = `<div class="meudia-day-empty"><div style="font-size:32px;margin-bottom:10px">✅</div><div style="font-weight:500;color:var(--text2)">Sem tarefas para ${dayLabels[meudioActiveDay].toLowerCase()}</div><div style="margin-top:6px;font-size:12px">Aproveita para avançar deals ou criar follow-ups manuais.</div></div>`;
    return;
  }

  // Summary bar
  const calls = groups.filter(g=>g.types.has('call')).length;
  const ews   = groups.filter(g=>g.types.has('email_wa')).length;
  const summaryBar = `<div style="display:flex;gap:8px;margin-bottom:12px;align-items:center;flex-wrap:wrap">
    <span style="font-size:13px;color:var(--text2);font-weight:500">${groups.length} cliente${groups.length!==1?'s':''} para contactar</span>
    <span style="color:var(--border2)">·</span>
    ${calls?`<span class="badge badge-gray">📞 ${calls} chamada${calls!==1?'s':''}</span>`:''}
    ${ews?`<span class="badge badge-gray">📨 ${ews} email+WA</span>`:''}
  </div>`;

  list.innerHTML = summaryBar + groups.map(g => {
    const deal = deals.find(x=>x.id===g.dealId);
    if(!deal) return '';
    const hasCall = g.types.has('call');
    const hasEW   = g.types.has('email_wa');
    const typeLabels = [hasCall?'📞 Chamada':null, hasEW?'📨 Email+WA':null].filter(Boolean).join(' · ');
    const isManual = g.tasks.some(t=>!t.auto);
    const isAuto   = g.tasks.some(t=>t.auto);
    const fuTmpl   = deal.followupStep===0?'followup1':'followup2';

    return `<div class="task-row">
      <div class="task-row-head">
        <div style="flex:1">
          <div style="display:flex;align-items:center;gap:8px;margin-bottom:3px">
            <span class="task-row-client">${deal.clientName}</span>
            ${isManual?`<span class="task-type-badge task-manual">Manual</span>`:''}
            ${isAuto?`<span class="task-type-badge task-auto">Auto</span>`:''}
          </div>
          <div class="task-row-car">🚗 ${deal.brand} ${deal.model}${deal.year?' · '+deal.year:''} · ${typeLabels}</div>
        </div>
        <button class="btn btn-ghost btn-sm" onclick="openDeal(${deal.id})" style="font-size:11px;flex-shrink:0">Ver deal →</button>
      </div>
      ${g.note?`<div class="task-row-note">📌 ${g.note}</div>`:''}
      <div class="task-row-actions">
        ${hasCall?`<a href="tel:${deal.phone}" class="btn btn-ghost btn-sm" style="font-size:12px">📞 ${deal.phone}</a>`:''}
        ${hasEW?`${waBtn(deal,fuTmpl)} ${emBtn(deal,fuTmpl)}`:''}
        <div style="flex:1"></div>
        <button class="btn btn-ghost btn-sm" style="font-size:11px" onclick="openSnooze('${g.tasks[0]?.id}',${!!isManual&&!isAuto})">⏰ Adiar</button>
        <button class="btn btn-ghost btn-sm" onclick="openManualFU(${deal.id})" style="font-size:11px">+ Follow-up</button>
        <button class="btn btn-primary btn-sm" style="font-size:11px" onclick="markTaskDone(${deal.id},'${dayStr}')">✓ Feito</button>
      </div>
    </div>`;
  }).join('');
}

function setMeuDiaDay(i) {
  meudioActiveDay = i;
  renderMeuDia();
}

function markTaskDone(dealId, dayStr) {
  const d = deals.find(x=>x.id===dealId);
  if(!d) return;
  // Mark auto followup step
  if(d.followupStep < 2) { d.followupStep++; }
  // Mark manual FUs for this deal+day as done
  manualFUs.filter(m=>m.dealId===dealId&&m.dueDate<=dayStr&&!m.done).forEach(m=>m.done=true);
  renderMeuDia();
  renderPlanner();
}

// ── SNOOZE ────────────────────────────────────────────
function openSnooze(taskId, isManual) {
  snoozeTaskId = taskId;
  snoozeTaskIsManual = isManual;
  // Find deal name from taskId
  let dealName = '';
  if(taskId) {
    const parts = taskId.split('-');
    const dealId = parseInt(parts[1]);
    const deal = deals.find(x=>x.id===dealId);
    if(deal) dealName = `${deal.clientName} · ${deal.brand} ${deal.model}`;
  }
  const info = document.getElementById('snooze-task-info');
  if(info) info.textContent = dealName || 'Tarefa selecionada';
  document.getElementById('snooze-custom-date').value = '';
  document.getElementById('snooze-note').value = '';
  openModal('modal-snooze');
}

function snoozeTask(type) {
  const todayStr = toDateStr(new Date());
  let newDate;
  if(type==='tomorrow')  newDate = addBusinessDays(todayStr,1);
  if(type==='2days')     newDate = addBusinessDays(todayStr,2);
  if(type==='nextweek')  newDate = addBusinessDays(todayStr,5);
  if(type==='custom') {
    newDate = document.getElementById('snooze-custom-date').value;
    if(!newDate) return;
  }
  const note = document.getElementById('snooze-note').value.trim();

  if(snoozeTaskIsManual) {
    const mfu = manualFUs.find(m=>m.id===snoozeTaskId);
    if(mfu) { mfu.dueDate = newDate; if(note) mfu.note = note; }
  } else {
    const parts = (snoozeTaskId||'').split('-');
    const dealId = parseInt(parts[1]);
    if(dealId) {
      manualFUs.push({
        id:'mfu-'+(nextMFUID++), dealId, type:'email_wa',
        dueDate:newDate, note: note || 'Adiado de '+todayStr,
        done:false, createdBy:currentUser.id, snoozed:true
      });
      // Mark the auto task as done so it doesn't show twice
      const d = deals.find(x=>x.id===dealId);
      if(d && d.followupStep < 1) d.followupStep = 0.5; // fractional = snoozed
    }
  }
  closeModal('modal-snooze');
  renderMeuDia();
  renderPlanner();
}

// ── MANUAL FOLLOW-UP ──────────────────────────────────
function openManualFU(dealId) {
  mfuDealId = dealId; mfuType = '';
  const deal = deals.find(x=>x.id===dealId);
  const info = document.getElementById('mfu-deal-info');
  if(info) info.innerHTML = `<strong>${deal?.clientName||'—'}</strong> · ${deal?.brand||''} ${deal?.model||''}`;
  document.querySelectorAll('input[name="mfu-type"]').forEach(r=>r.checked=false);
  document.getElementById('mfu-date').value = addBusinessDays(toDateStr(new Date()),1);
  document.getElementById('mfu-note').value = '';
  // Reset type label borders
  ['mfu-type-call','mfu-type-ew','mfu-type-both'].forEach(id=>{
    const el=document.getElementById(id);
    if(el)el.style.borderColor='var(--border)';
  });
  openModal('modal-manual-fu');
}

function selectMfuType(t) {
  mfuType = t;
  ['mfu-type-call','mfu-type-ew','mfu-type-both'].forEach(id=>{
    const el=document.getElementById(id);
    if(el)el.style.borderColor='var(--border)';
  });
  const map={call:'mfu-type-call',email_wa:'mfu-type-ew',both:'mfu-type-both'};
  const el=document.getElementById(map[t]);
  if(el)el.style.borderColor='var(--accent)';
}

function saveManualFU() {
  if(!mfuType){alert('Seleciona o tipo de contacto.');return;}
  const date = document.getElementById('mfu-date').value || toDateStr(new Date());
  const note = document.getElementById('mfu-note').value.trim();
  manualFUs.push({
    id:'mfu-'+(nextMFUID++), dealId:mfuDealId, type:mfuType,
    dueDate:date, note, done:false, createdBy:currentUser.id, auto:false
  });
  closeModal('modal-manual-fu');
  renderMeuDia();
  renderPlanner();
}

// ══════════════════════════════════════════════════════
let sellers = [
  {id:1,brand:'Mercedes-Benz',stand:'Stern-Center Regensburg GmbH & Co. KG',name:'Moritz Geier',phone:'+49 9417843473',email:'moritz.geier@stern-center.de',location:'DE-93053 Regensburg',rating:5,notes:''},
  {id:2,brand:'Mercedes-Benz',stand:'Schreiner & Wollenstein GmbH & Co. KG',name:'Robert Pohl',phone:'+49 871759641',email:'robert.pohl@mbsw.de',location:'DE-84030 Landshut-Ergoling',rating:5,notes:''},
  {id:3,brand:'Mercedes-Benz',stand:'Mercedes-Benz Niederlassung',name:'Clemens Kuhnke',phone:'+49 4069414972',email:'clemens.kuhnke@mercedes-benz.com',location:'DE-22047 Hamburg',rating:5,notes:''},
  {id:4,brand:'Mercedes-Benz',stand:'Mercedes-Benz AG Niederlassung Reutlingen und Tübingen',name:'Joachim Wagemann',phone:'+49 71219473437',email:'joachim.wagemann@mercedes-benz.com',location:'DE 72783 Pfullingen',rating:5,notes:''},
  {id:5,brand:'Mercedes-Benz',stand:'Simon Gruber GmbH & Co. KG',name:'Christopher Spatina',phone:'+49 89608006213',email:'christopher.spatina@mercedes-gruber.de',location:'DE-85652 Landsham',rating:5,notes:''},
  {id:6,brand:'Mercedes-Benz',stand:'Kestenholz Automobil GmbH',name:'Margo Castor',phone:'+49 2614910',email:'m.castor@kestenholzgruppe.com',location:'DE-56073 Koblenz',rating:5,notes:''},
  {id:7,brand:'Mercedes-Benz',stand:'Wackenhut GmbH & Co. KG',name:'Fadi Khalil',phone:'+49 72216862266',email:'f.khalil@wackenhut.de',location:'DE-76532 Baden-Baden',rating:5,notes:''},
  {id:8,brand:'Mercedes-Benz',stand:'Auto Braininger GbR',name:'Weger Nico',phone:'+49 8711433125',email:'weger@auto-braininger.de',location:'DE-84032 Altdorf/Landshut',rating:5,notes:''},
  {id:9,brand:'Mercedes-Benz',stand:'Alfons Schoenauen GmbH & Co. KG',name:'Ionnis Tsintzos',phone:'',email:'',location:'DE-42281 Wuppertal',rating:5,notes:''},
  {id:10,brand:'Mercedes-Benz',stand:'Jürgens GmbH Mercedes-Benz',name:'Julian Schawaller',phone:'+49 15129174333',email:'j.schawaller@autohaus-juergens.de',location:'DE-58135 Hagen',rating:5,notes:''},
  {id:11,brand:'Mercedes-Benz',stand:'S&G Automobil AG',name:'Jaime Seco',phone:'+49 7219565272',email:'jaime.seco@sug.de',location:'DE-76185 Karlsruhe',rating:5,notes:''},
  {id:12,brand:'Mercedes-Benz',stand:'S&G Automobil AG',name:'Nikola Kolev',phone:'+49 7219565507',email:'nikola.kolev@sug.de',location:'DE-76185 Karlsruhe',rating:5,notes:''},
  {id:13,brand:'Mercedes-Benz',stand:'AHG Hoffmann GmbH & Co. KG',name:'Tobias Skoumal',phone:'+49 7141300018',email:'T.Skoumal@ahg-hoffmann.de',location:'DE-71636 Ludwigsburg',rating:5,notes:''},
  {id:14,brand:'Mercedes-Benz',stand:'Mercedes-Benz AG Niederlassung Darmstadt',name:'Marcel Appelt',phone:'+49 15158621393',email:'marcel.appelt@mercedes-benz.com',location:'DE-64295 Darmstadt',rating:4,notes:''},
  {id:15,brand:'Mercedes-Benz',stand:'Mercedes-Benz AG Niederlassung Schwäbisch Gmünd',name:'Artur Oll',phone:'+49 71713572183',email:'artur.oll@mercedes-benz.com',location:'DE-73529 Schwäbisch Gmünd',rating:4,notes:''},
  {id:16,brand:'Mercedes-Benz',stand:'Senger GmbH & Co KG',name:'Michael Ernst',phone:'+49 604296243831',email:'Michael.ernst@auto-senger.de',location:'DE-63654 Buedingen',rating:4,notes:''},
  {id:17,brand:'Mercedes-Benz',stand:'Bald Automobile GmbH',name:'Lars Bennewitz',phone:'+49 2741280820',email:'l.bennewitz@bald.de',location:'DE-57518 Betzdorf',rating:4,notes:''},
  {id:18,brand:'Mercedes-Benz',stand:'Auto Nagel GmbH & Co. KG',name:'Enes Karakazik',phone:'+49 81656474949',email:'enes.karakazik@auto-nagel.de',location:'DE-85435 Erding',rating:4,notes:''},
  {id:19,brand:'Mercedes-Benz',stand:'Peter Praunsmändtl GmbH & Co. KG',name:'Ivica Krizanac',phone:'+49 841504136',email:'i.krizanac@praunsmaendtl.de',location:'DE-85007 Ingolstadt',rating:4,notes:''},
  {id:20,brand:'Mercedes-Benz',stand:'Autohaus Rieger GmbH',name:'Ralph Handke',phone:'+49 9187951934',email:'ralph.handke@auto-rieger.de',location:'DE-90518 Altdorf',rating:4,notes:''},
  {id:21,brand:'Mercedes-Benz',stand:'Abel+Ruf GmbH',name:'Daniel Wudy',phone:'+49 90678071902',email:'daniel.wudy@abel-ruf.de',location:'DE-86609 Donauwörth',rating:4,notes:''},
  {id:22,brand:'Mercedes-Benz',stand:'autocenter schmolke SE & Co. KG',name:'Michael Behlau',phone:'',email:'Michael.Behlau@autocenter-schmolke.de',location:'DE-28865 Lilienthal',rating:4,notes:''},
  {id:23,brand:'Mercedes-Benz',stand:'Autorisierter Mercedes-Benz PK',name:'Steffen Roesch',phone:'+49 34125851982',email:'steffen.roesch@sternauto.de',location:'DE-04277 Leipzig',rating:4,notes:''},
  {id:24,brand:'Mercedes-Benz',stand:'Mercedes-Benz Niederlassung Berlin',name:'Fabian Schulz',phone:'+49 15158627419',email:'fabian.fs.schulz@mercedes-benz.com',location:'DE-10901 Berlin',rating:4,notes:''},
  {id:25,brand:'Mercedes-Benz',stand:'Autohaus Ebert GmbH & Co. KG',name:'Jacek Sobczak',phone:'+49 6201992265',email:'jacek.sobczak@autowelt-ebert.de',location:'DE-69469 Weinheim',rating:4,notes:''},
  {id:26,brand:'Mercedes-Benz',stand:'Auto Expo',name:'Ben-André Haas',phone:'+49 64049266213',email:'ben-andre.haas@autoexpo.de',location:'DE-35463',rating:3,notes:''},
  {id:27,brand:'Mercedes-Benz',stand:'Egon Senger GmbH',name:'Holger Weber',phone:'+49 44177078039',email:'holger.weber@auto-senger.de',location:'DE-26129 Oldenburg',rating:3,notes:''},
  {id:28,brand:'Mercedes-Benz',stand:'Jürgens GmbH Mercedes-Benz Lüdenscheid',name:'Burak Secgel',phone:'+49 2351955232',email:'',location:'DE-58507 Lüdenscheid',rating:2,notes:''},
  {id:29,brand:'Mercedes-Benz',stand:'Senger & Kraft GmbH & Co. KG',name:'Marcel Schrnitt',phone:'+49 15161088549',email:'marcel.schrnitt@senger-kraft.de',location:'DE-35039 Marburg',rating:2,notes:''},
  {id:30,brand:'Mercedes-Benz',stand:'Automobile Z. Huber',name:'—',phone:'+49 68388409947',email:'verkauf@automobilehuber.de',location:'DE-66809 Nalbach',rating:0,notes:''},
  {id:31,brand:'VW',stand:'Volkswagen Zentrum Bergkamen Hülpert SK GmbH',name:'Maurice Knichel-Peters',phone:'+49 23079822018',email:'maurice.knichel@hulpert.de',location:'DE-59192 Bergkamen',rating:5,notes:''},
  {id:32,brand:'VW',stand:'MAHAG Gebrauchtwagencentrum',name:'Benjamin Weinbacher',phone:'+49 17611996047',email:'benjamin.weinbacher@mahag.de',location:'DE 81669 München',rating:4,notes:''},
  {id:33,brand:'VW',stand:'Hülpert VZ GmbH',name:'Petr Litvin',phone:'+49 215133936',email:'petr.litvin@huelpert.de',location:'DE-44379 Dortmund',rating:4,notes:''},
  {id:34,brand:'VW',stand:'Hahn Automobile GmbH + Co. KG',name:'Filip Mickan',phone:'+49 7119384839',email:'filip.mickan@hahn-automobile.de',location:'DE-73734 Esslingen',rating:4,notes:''},
  {id:35,brand:'VW',stand:'Autohaus Glinicke in Erfurt',name:'Majid Esmati',phone:'+49 3613435818',email:'majid.esmati@glinicke.de',location:'DE-99099 Erfurt',rating:4,notes:''},
  {id:36,brand:'VW',stand:'Autohaus Wolfsburg Hotz und Heitmann',name:'Peter Damaziak',phone:'+49 8441899944',email:'p.damaziak@autobauer-paf.de',location:'DE-38440 Wolfsburg',rating:3,notes:''},
  {id:37,brand:'VW',stand:'Hildburg Automobile',name:'Kerim Kaplan',phone:'+49 3072324926',email:'info@hildburg-automobile.de',location:'DE-12279 Berlin',rating:3,notes:''},
  {id:38,brand:'VW',stand:'Autohaus Feser GmbH',name:'Johannes Kast',phone:'',email:'',location:'DE-91126 Schwabach',rating:3,notes:''},
  {id:39,brand:'VW',stand:'Fischer Automobile GmbH',name:'Paul Stanke',phone:'+49 91814755250',email:'P.Stanke@fischer-automobile.de',location:'DE-92318 Neumarkt',rating:3,notes:''},
  {id:40,brand:'Audi',stand:'Audi Zentrum Krefeld - Tölke & Fischer',name:'Frank Beckers',phone:'+49 2151339361',email:'frank.beckers@toefi.de',location:'DE-47805 Krefeld',rating:5,notes:''},
  {id:41,brand:'Audi',stand:'MH Autoforum GmbH + Co. KG',name:'Abdul Erdogan',phone:'+49 6414990929',email:'a.erdogan@mh-autoforum.de',location:'DE-35394 Giessen',rating:5,notes:''},
  {id:42,brand:'Audi',stand:'Autozentrum Dobler GmbH',name:'Markus Janssen',phone:'+49 7041966481',email:'m.janssen@autozentrum-dobler.de',location:'DE-75417 Mühlacker',rating:5,notes:''},
  {id:43,brand:'Audi',stand:'Auto Koch GmbH Öhringen',name:'Tobias Reinhard',phone:'+49 7919300120',email:'tobias.reinhard@koch-autogruppe.de',location:'DE-74613 Öhringen',rating:4,notes:''},
  {id:44,brand:'Audi',stand:'Autohaus Michael Stiglmayr GmbH',name:'Lino Hindelang',phone:'+49 8441809047',email:'l.hindelang@audi-stiglmayr.fahrzeuganfrage.net',location:'DE-85276 Pfaffenhofen',rating:4,notes:''},
  {id:45,brand:'Audi',stand:'Anke Schröder Fahrzeughandel GmbH',name:'Steven Schmidt',phone:'+49 30666077858',email:'steven.schmidt@berlin.audi',location:'D-36179 Bebra',rating:3,notes:''},
  {id:46,brand:'Audi',stand:'Deisenroth & Söhne GmbH & Co. KG',name:'Michael Geier',phone:'',email:'',location:'DE-36088 Hünfeld',rating:3,notes:''},
  {id:47,brand:'Audi',stand:'Gohm + Graf Hardenberg GmbH',name:'Tufan Ozturk',phone:'+49 15158330345',email:'tufan.oeztuerk@grafhatdenberg.de',location:'DE-78467 Konstanz',rating:0,notes:''},
  {id:48,brand:'BMW',stand:'BMW Niederlassung Dreieich-Sprendlingen',name:'Erik Papenberg',phone:'+49 61039300212',email:'erik.papenberg@bmw.de',location:'DE-63303 Dreieich',rating:5,notes:''},
  {id:49,brand:'BMW',stand:'BMW Niederlassung Stuttgart',name:'Natascha Schierke',phone:'+49 71113185218',email:'natascha.schierke@bmw.de',location:'DE-70569 Stuttgart',rating:4,notes:''},
  {id:50,brand:'BMW',stand:'Fett & Wirtz Automobile GmbH & Co KG',name:'Carsten Roenicke',phone:'+49 28412072735',email:'c.roenicke@bmw-fett-wirtz.de',location:'DE-47441 Moers',rating:4,notes:''},
  {id:51,brand:'BMW',stand:'Autohaus Kaltenbach GmbH & Co KG',name:'Claus Bartels',phone:'+49 2261947243',email:'claus.bartels@kaltenbach-gruppe.de',location:'DE-51674 Wiehl',rating:3,notes:''},
  {id:52,brand:'BMW',stand:'Erwin Schmidt GmbH & Co. KG',name:'Pascal Panchyrz',phone:'+49 2306705318',email:'pascal.panchyrz@autowelt-schmidt.de',location:'DE-44534 Lünen',rating:2,notes:''},
  {id:53,brand:'Smart',stand:'Senger Südwestfalen GmbH',name:'Moritz Matthes',phone:'+49 23814255316',email:'moritz.matthes@auto-senger.de',location:'DE-59067 Hamm',rating:5,notes:''},
  {id:54,brand:'Smart',stand:'Mercedes-Benz AG Niederlassung Bremen Gebrauchtwagen',name:'Marc Domke',phone:'+49 4214681318',email:'michael.wehking@mercedes-benz.com',location:'DE-28307 Bremen',rating:5,notes:''},
  {id:55,brand:'Smart',stand:'Beresa GmbH & Co. KG',name:'Victor Vilarino',phone:'+49 25171834105',email:'victor.arensvilarino@beresa.de',location:'DE-48308 Senden-Bösensell',rating:5,notes:''},
  {id:56,brand:'Smart',stand:'Merbag S.A.',name:'Christophe Mangenot',phone:'+352 40801521',email:'christophe.mangenot@merbag.lu',location:'LU-1248',rating:5,notes:''},
  {id:57,brand:'Smart',stand:'Süverkrüp Automobile GmbH smartCenter',name:'Devin Uyar',phone:'+49 1743099858',email:'devin.uyar@sueverkruep.de',location:'DE-24109 Kiel',rating:2,notes:''},
  {id:58,brand:'Renault',stand:'KIFFE V & N GmbH',name:'Nemat Mamedov',phone:'+49 2381955040',email:'n.mamedov@kiffe-vn.de',location:'DE-59063 Hamm',rating:5,notes:''},
  {id:59,brand:'Renault',stand:'Autohaus Walter Mulfinger GmbH',name:'Alisa Kovarcek',phone:'+49 7321358037',email:'alisa.kovarcek@mulfinger.de',location:'DE-89520 Heidenheim',rating:4,notes:''},
  {id:60,brand:'Renault',stand:'BOB Automobile',name:'Ulf Wiebel',phone:'+49 2022433337',email:'ulf.wiebel@bob-automobile.de',location:'DE-45355 Essen',rating:4,notes:''},
  {id:61,brand:'Renault',stand:'Preckel Automobile GmbH',name:'Jürgen Dersch',phone:'+49 215137115229',email:'J.Dersch@preckel.de',location:'DE-47805 Krefeld',rating:1,notes:''},
  {id:62,brand:'Range Rover',stand:'Avalon Premium Cars GmbH',name:'Felix Rudolf',phone:'+49 6173999680',email:'kronberg@autohaus-avalon.de',location:'61476 Kronberg',rating:5,notes:''},
  {id:63,brand:'Range Rover',stand:'Auto Nagel Essen GmbH & Co. KG',name:'Benedikt Bock',phone:'+49 1703713692',email:'benedikt.bock@auto-nagel.de',location:'DE-45141 Essen',rating:5,notes:''},
  {id:64,brand:'Range Rover',stand:'Vigar Motors bvba',name:'Matthew Vigar',phone:'+32 470835580',email:'matthew@vigarmotors.be',location:'BE',rating:1,notes:''},
  {id:65,brand:'Volvo',stand:'Autohaus Geisser GmbH',name:'Philipp Hurst',phone:'+49 7222931144',email:'philipp.hurst@autohaus-geisser.de',location:'DE-76187 Karlsruhe',rating:5,notes:''},
  {id:66,brand:'Volvo',stand:'Auto Nagel Westfalen GmbH & Co. KG',name:'Burak Alca',phone:'+49 255193390',email:'burak.alca@auto-nagel.de',location:'DE-48565 Steinfurt',rating:4,notes:''},
  {id:67,brand:'Volvo',stand:'B & E Kraftfahrzeuge GmbH',name:'Rafael Nunes',phone:'+49 4719615021',email:'nunes@be-automobile.de',location:'DE-27619 Schiffdorf-Spaden',rating:4,notes:''},
  {id:68,brand:'Hyundai',stand:'BRANDT GROUP c/o Autohaus Brandt & Strupp',name:'Przemylaw Mikolajczyk',phone:'+49 3816370030',email:'Mikolajczyk@ah-brandt.de',location:'DE-18146 Rostock',rating:4,notes:''},
  {id:69,brand:'Hyundai',stand:'Autobedrijf Wesselink Emst B.V',name:'Jesse Tan',phone:'+31 578661439',email:'j.tan@honda-wesselink.nl',location:'NL-8166 AE EMST',rating:3,notes:''},
  {id:70,brand:'Land Rover',stand:'Jaguar & Land Rover House Woltmann',name:'Benny Latwessen',phone:'+49 42146890601',email:'benny.latwesen@woltmann-gruppe.de',location:'DE-28329 Bremen',rating:4,notes:''},
  {id:71,brand:'Land Rover',stand:'Autohaus Elegance e.K.',name:'—',phone:'',email:'',location:'DE-51147 Köln',rating:2,notes:'Contacto já não trabalha lá'},
  {id:72,brand:'MG',stand:'Riess GmbH & Co. KG',name:'Alexander Rosgen',phone:'+49 74124021',email:'alexander.roesgen@riess-gruppe.de',location:'DE-78628 Rottweil',rating:4,notes:''},
  {id:73,brand:'MG',stand:'Dehn GmbH',name:'Dennis Ramin',phone:'+49 15222588495',email:'d.ramin@dehn-automobile.de',location:'DE-39576 Stendal',rating:3,notes:''},
  {id:74,brand:'Mini',stand:'Autohaus Karl + Co. GmbH KG',name:'Ralf Fraedert',phone:'+49 4214681272',email:'ralf.fraedert@bmw-karl-co.de',location:'DE-65203 Wiesbaden',rating:4,notes:''},
  {id:75,brand:'Mini',stand:'Vogelsang Automobile GmbH & Co. KG',name:'Juergen Meyer',phone:'+49 2361919391',email:'j.meyer@vogelsang-automobile.de',location:'DE-45659 Recklinghausen',rating:3,notes:''},
  {id:76,brand:'Porsche',stand:'MK Automobile Markus Kräml e.K.',name:'Markus Kraml',phone:'+49 92059884510',email:'info@mk-sportwagon.de',location:'DE-95519 Oberbibrach',rating:5,notes:''},
  {id:77,brand:'Porsche',stand:'Porsche Zentrum Schwäbisch Gmünd',name:'Josua Horster',phone:'+49 717177991925',email:'josua.hoerster@porsche-schwaebischgmuend.de',location:'DE-73529 Schwäbisch Gmünd',rating:5,notes:''},
  {id:78,brand:'Toyota',stand:'WELLER Performance GmbH & Co. KG',name:'Duc Manh Nguyen',phone:'+49 3419450201',email:'DucManh.Nguyen@wellergruppe.de',location:'DE-04178 Leipzig',rating:5,notes:''},
  {id:79,brand:'Toyota',stand:'Autohaus Kreinhöfner GmbH & Co. KG',name:'Nicolai Paul',phone:'+49 968192090',email:'service@ah-kreinhoefner.de',location:'DE-92670 Windischeschenbach',rating:4,notes:''},
  {id:80,brand:'Cupra',stand:'Schwaba GmbH',name:'Mus Merve',phone:'+49 821490011437',email:'merve.mus@schwaba.de',location:'DE-86368 Gersthofen',rating:4,notes:''},
  {id:81,brand:'Maxus',stand:'Autohaus Puehheim H.G. GmbH',name:'Stephan Gottner',phone:'+49 15110221059',email:'autohauspuchheinm@aol.com',location:'DE-82178 Puchheim',rating:3,notes:''},
  {id:82,brand:'Suzuki',stand:'PR-Automobile KG',name:'Rodriguez',phone:'+49 20935980445',email:'pr-automobile@t-online.de',location:'DE-45892 Gelsenkirchen',rating:3,notes:''},
  {id:83,brand:'Tesla',stand:'EURL AUTO GR',name:'Xavier',phone:'+33 684613868',email:'autogari@gmail.com',location:'FR-13700 Marignane',rating:4,notes:''},
  {id:84,brand:'XPENG',stand:'WAHL-GROUP Horst Wahl GmbH & Co. KG',name:'Niklas Rabenau',phone:'+49 64216877624',email:'n.rabenau@wahl-group.de',location:'DE-35039 Marburg',rating:0,notes:''},
];
let nextSID = 85;
let editSellerId = null;
let sellerRatingVal = 0;
let dealRatingVal = 0;
let ratingDealId = null;
let ratingPendingStage = null;

// ══════════════════════════════════════════════════════
// SELLERS — HELPERS
// ══════════════════════════════════════════════════════
function starsHtml(n, max=5){
  let s='';
  for(let i=1;i<=max;i++) s+=`<span style="color:${i<=n?'var(--accent)':'var(--bg3)'}">${i<=n?'★':'☆'}</span>`;
  return s;
}
function sellerBrands(){return [...new Set(sellers.map(s=>s.brand))].sort();}
function sellerById(id){return sellers.find(s=>s.id===id);}

function dealsForSeller(sellerId){return deals.filter(d=>d.sellerId===sellerId);}

// ══════════════════════════════════════════════════════
// SELLERS — RENDER
// ══════════════════════════════════════════════════════
function renderSellers(){
  const q=(document.getElementById('seller-search')?.value||'').toLowerCase();
  const bf=document.getElementById('seller-brand-filter')?.value||'';
  const rf=parseInt(document.getElementById('seller-rating-filter')?.value||'0');

  // Populate brand filter
  const bsel=document.getElementById('seller-brand-filter');
  if(bsel&&bsel.options.length<=1){
    sellerBrands().forEach(b=>{const o=document.createElement('option');o.value=b;o.textContent=b;bsel.appendChild(o);});
  }

  const filtered=sellers.filter(s=>{
    const matchQ=!q||(s.name+s.stand+s.brand+s.location).toLowerCase().includes(q);
    const matchB=!bf||s.brand===bf;
    const matchR=!rf||s.rating>=rf;
    return matchQ&&matchB&&matchR;
  });

  document.getElementById('sellers-sub').textContent=`${filtered.length} de ${sellers.length} vendedores`;

  const tbody=document.getElementById('sellers-tbody');
  if(!filtered.length){tbody.innerHTML=`<tr><td colspan="9"><div class="empty"><div class="empty-icon">🏪</div><div class="empty-title">Nenhum vendedor encontrado</div></div></td></tr>`;return;}

  tbody.innerHTML=filtered.map(s=>{
    const sd=dealsForSeller(s.id);
    return`<tr>
      <td><div style="font-weight:500;font-size:13px">${s.name}</div>${s.notes?`<div style="font-size:10px;color:var(--text3)">${s.notes}</div>`:''}</td>
      <td style="font-size:12px;max-width:180px"><div style="white-space:nowrap;overflow:hidden;text-overflow:ellipsis" title="${s.stand}">${s.stand}</div></td>
      <td><span class="badge badge-gray">${s.brand}</span></td>
      <td style="font-size:12px;color:var(--text2)">📍 ${s.location||'—'}</td>
      <td style="font-size:12px">${s.phone?`<a href="tel:${s.phone}">${s.phone}</a>`:'—'}</td>
      <td style="font-size:11px;color:var(--blue)">${s.email?`<a href="mailto:${s.email}">${s.email}</a>`:'—'}</td>
      <td><div class="stars">${starsHtml(s.rating)}</div></td>
      <td>${sd.length?`<span class="badge badge-gray">${sd.length}</span>`:'—'}</td>
      <td style="display:flex;gap:4px">
        <button class="btn btn-ghost btn-sm" onclick="editSeller(${s.id})">✏️</button>
        <button class="btn btn-ghost btn-sm" onclick="contactSeller(${s.id})" title="Contactar">📞</button>
      </td>
    </tr>`;
  }).join('');
}

function contactSeller(id){
  const s=sellerById(id);
  if(!s)return;
  if(s.phone){window.open(`tel:${s.phone}`);}
  else if(s.email){window.location.href=`mailto:${s.email}`;}
}

// ══════════════════════════════════════════════════════
// SELLERS — CRUD
// ══════════════════════════════════════════════════════
function openNewSeller(){
  editSellerId=null;sellerRatingVal=0;
  document.getElementById('seller-modal-title').textContent='Novo Vendedor';
  ['ns-brand','ns-name','ns-stand','ns-phone','ns-email','ns-location','ns-notes'].forEach(id=>document.getElementById(id).value='');
  updateSellerStars(0);
  // Populate brand datalist
  const dl=document.getElementById('ns-brand-list');dl.innerHTML='';
  sellerBrands().forEach(b=>{const o=document.createElement('option');o.value=b;dl.appendChild(o);});
  openModal('modal-seller');
}

function editSeller(id){
  const s=sellerById(id);if(!s)return;
  editSellerId=id;sellerRatingVal=s.rating;
  document.getElementById('seller-modal-title').textContent='Editar Vendedor';
  document.getElementById('ns-brand').value=s.brand;
  document.getElementById('ns-name').value=s.name;
  document.getElementById('ns-stand').value=s.stand;
  document.getElementById('ns-phone').value=s.phone;
  document.getElementById('ns-email').value=s.email;
  document.getElementById('ns-location').value=s.location;
  document.getElementById('ns-notes').value=s.notes;
  const dl=document.getElementById('ns-brand-list');dl.innerHTML='';
  sellerBrands().forEach(b=>{const o=document.createElement('option');o.value=b;dl.appendChild(o);});
  updateSellerStars(s.rating);
  openModal('modal-seller');
}

function setSellerRating(v){sellerRatingVal=v;updateSellerStars(v);}
function updateSellerStars(v){
  document.querySelectorAll('.star-btn').forEach(s=>{
    s.style.opacity=parseInt(s.dataset.v)<=v?'1':'.3';
    s.style.color=parseInt(s.dataset.v)<=v?'var(--accent)':'var(--bg3)';
  });
  const lbl=document.getElementById('ns-rating-val');
  if(lbl)lbl.textContent=v+'/5';
}

function saveSeller(){
  const brand=document.getElementById('ns-brand').value.trim();
  const name=document.getElementById('ns-name').value.trim();
  const stand=document.getElementById('ns-stand').value.trim();
  if(!brand||!name||!stand){alert('Marca, nome e stand são obrigatórios.');return;}
  if(editSellerId){
    const s=sellerById(editSellerId);
    if(s){s.brand=brand;s.name=name;s.stand=stand;s.phone=document.getElementById('ns-phone').value.trim();s.email=document.getElementById('ns-email').value.trim();s.location=document.getElementById('ns-location').value.trim();s.notes=document.getElementById('ns-notes').value.trim();s.rating=sellerRatingVal;}
  } else {
    sellers.push({id:nextSID++,brand,name,stand,phone:document.getElementById('ns-phone').value.trim(),email:document.getElementById('ns-email').value.trim(),location:document.getElementById('ns-location').value.trim(),notes:document.getElementById('ns-notes').value.trim(),rating:sellerRatingVal});
  }
  closeModal('modal-seller');renderSellers();
}

// ══════════════════════════════════════════════════════
// SELLER AUTOCOMPLETE IN DEAL
// ══════════════════════════════════════════════════════
function initSellerAutocomplete(){
  const wrap=document.getElementById('deal-seller-wrap');
  if(!wrap)return;
  const inp=document.getElementById('deal-seller-input');
  const list=document.getElementById('deal-seller-list');
  if(!inp)return;
  inp.addEventListener('input',()=>{
    const q=inp.value.toLowerCase().trim();
    if(!q){list.style.display='none';return;}
    const matches=sellers.filter(s=>(s.name+s.stand+s.brand).toLowerCase().includes(q)).slice(0,8);
    if(!matches.length){list.style.display='none';return;}
    list.innerHTML=matches.map(s=>`<div class="ac-item" onclick="selectSeller(${s.id})">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <span class="ac-name">${s.name}</span><span class="ac-rating">${starsHtml(s.rating)}</span>
      </div>
      <span class="ac-sub">${s.stand} · ${s.brand} · ${s.location}</span>
    </div>`).join('');
    list.style.display='block';
  });
  document.addEventListener('click',e=>{if(!wrap.contains(e.target))list.style.display='none';});
}

function selectSeller(id){
  const s=sellerById(id);if(!s)return;
  document.getElementById('deal-seller-input').value=s.name+' — '+s.stand;
  document.getElementById('deal-seller-id').value=id;
  document.getElementById('deal-seller-list').style.display='none';
  // Auto-fill location
  const locInp=document.getElementById('deal-seller-location');
  if(locInp&&s.location)locInp.value=s.location;
}

// ══════════════════════════════════════════════════════
// RATING MODAL (obrigatório ao avançar para "Entregue")
// ══════════════════════════════════════════════════════
const RATING_LABELS={1:'Muito fraco',2:'Fraco',3:'Razoável',4:'Bom',5:'Excelente'};

function setDealRating(v){
  dealRatingVal=v;
  document.querySelectorAll('.deal-star').forEach((s,i)=>{s.style.opacity=i<v?'1':'.25';});
  document.getElementById('rating-label').textContent=RATING_LABELS[v]||'';
  document.getElementById('rating-confirm-btn').disabled=false;
}

function confirmRating(){
  const d=deals.find(x=>x.id===ratingDealId);if(!d)return;
  // Update seller rating (weighted average with existing)
  if(d.sellerId){
    const s=sellerById(d.sellerId);
    if(s){
      const prevDeals=dealsForSeller(s.id).filter(dd=>dd.sellerRating&&dd.id!==d.id);
      const ratings=[...prevDeals.map(dd=>dd.sellerRating),dealRatingVal];
      s.rating=Math.round(ratings.reduce((a,b)=>a+b,0)/ratings.length);
    }
  }
  d.sellerRating=dealRatingVal;
  d.stage=ratingPendingStage;
  closeModal('modal-rating');
  renderDeal(d);updateNavBadge();
}

// Override advanceStage to intercept stage 10 (Entregue)
const _origAdvanceStage=advanceStage;
advanceStage=function(id){
  const d=deals.find(x=>x.id===id);
  if(!d)return;
  const nextStage=d.stage+1;
  if(nextStage===10){
    // Rating required
    ratingDealId=id;ratingPendingStage=10;dealRatingVal=0;
    document.querySelectorAll('.deal-star').forEach(s=>s.style.opacity='.25');
    document.getElementById('rating-label').textContent='';
    document.getElementById('rating-confirm-btn').disabled=true;
    const s=d.sellerId?sellerById(d.sellerId):null;
    document.getElementById('rating-seller-info').innerHTML=s
      ?`<strong>${s.name}</strong> — ${s.stand}<br><span style="color:var(--text3);font-size:11px">Rating atual: ${starsHtml(s.rating)}</span>`
      :'<span style="color:var(--text3)">Vendedor não associado a este deal.</span>';
    openModal('modal-rating');
    return;
  }
  _origAdvanceStage(id);
};

// ══════════════════════════════════════════════════════
// UPDATE NAV to include Sellers
// ══════════════════════════════════════════════════════
const _origBuildNav=buildNav;
buildNav=function(){
  const pages=[
    {id:'dashboard',label:'Dashboard',icon:'📊'},
    {id:'pipeline',label:'Pipeline',icon:'🔄'},
    {id:'meudia',label:'O meu dia',icon:'📋'},
    {id:'leads',label:'Leads',icon:'📬'},
    {id:'alerts',label:'Alertas',icon:'⚠️'},
    {id:'sellers',label:'Vendedores',icon:'🏪'},
    {id:'contacts',label:'Contactos',icon:'👤'},
  ];
  if(currentUser.role==='admin')pages.push({id:'admin',label:'Admin',icon:'⚙️'});
  document.getElementById('topbar-nav').innerHTML=pages.map(p=>`<button class="nav-btn" id="nav-${p.id}" onclick="showPage('${p.id}')">${p.icon} ${p.label}</button>`).join('');
  updateNavBadge();
};

// Extend showPage for sellers
const _origShowPage=showPage;
showPage=function(id){
  _origShowPage(id);
  if(id==='sellers')renderSellers();
  if(id==='leads')renderLeadsPage();
  if(id==='meudia'){meudioActiveDay=0;renderMeuDia();}
};

// ══════════════════════════════════════════════════════
// SELLER FIELD IN DEAL DETAIL (patch vehicleCard)
// ══════════════════════════════════════════════════════
const _origVehicleCard=vehicleCard;
vehicleCard=function(d){
  const s=d.sellerId?sellerById(d.sellerId):null;
  const canEdit=currentUser.role==='admin'||currentUser.id===d.comercialId;
  const sellerSection=`<div style="margin-top:10px;padding-top:10px;border-top:1px solid var(--border2)">
    <div class="fl" style="margin-bottom:6px">Vendedor do stand</div>
    ${canEdit?`<div class="ac-wrap" id="deal-seller-wrap" style="position:relative">
      <input class="fc" id="deal-seller-input" placeholder="Pesquisar vendedor ou stand..." value="${s?s.name+' — '+s.stand:''}" autocomplete="off">
      <input type="hidden" id="deal-seller-id" value="${d.sellerId||''}">
      <div class="ac-list" id="deal-seller-list" style="display:none"></div>
    </div>
    <div class="fg" style="margin-top:8px;margin-bottom:0">
      <label class="fl">Localização do veículo</label>
      <input class="fc" id="deal-seller-location" placeholder="DE-12345 Cidade" value="${d.location||''}">
      <div class="fh">Usada pelo operacional para a transportadora</div>
    </div>
    <button class="btn btn-ghost btn-sm" style="margin-top:8px" onclick="saveDealSeller(${d.id})">Guardar vendedor</button>`
    :`<div style="font-size:13px">${s?`<strong>${s.name}</strong> — ${s.stand} <span class="stars">${starsHtml(s.rating)}</span>`:'Não associado'}</div>
    ${d.location?`<div style="font-size:12px;color:var(--text2);margin-top:4px">📍 ${d.location}</div>`:''}`}
    ${s?`<div style="margin-top:8px;display:flex;gap:6px">
      ${s.phone?`<a href="tel:${s.phone}" class="btn btn-ghost btn-sm">📞 ${s.phone}</a>`:''}
      ${s.email?`<a href="mailto:${s.email}" class="btn btn-ghost btn-sm">✉️ Email</a>`:''}
    </div>`:''}
  </div>`;
  const base=_origVehicleCard(d);
  return base.replace('</div></div>',sellerSection+'</div></div>');
};

function saveDealSeller(dealId){
  const d=deals.find(x=>x.id===dealId);if(!d)return;
  const sid=parseInt(document.getElementById('deal-seller-id').value);
  const loc=document.getElementById('deal-seller-location').value.trim();
  if(sid)d.sellerId=sid;
  if(loc)d.location=loc;
  renderDeal(d);
  // init autocomplete after re-render
  setTimeout(()=>initSellerAutocomplete(),50);
}

// Init autocomplete when deal opens
const _origOpenDeal=openDeal;
openDeal=function(id){
  _origOpenDeal(id);
  setTimeout(()=>initSellerAutocomplete(),100);
};

// ══════════════════════════════════════════════════════
// EXPORT CSV
// ══════════════════════════════════════════════════════
function exportCSV(type){
  let rows=[], filename='';
  if(type==='contacts'){
    filename='importhub_clientes.csv';
    rows=[['Nome','Telemóvel','Email','Tipo','Empresa','Deals','Comercial']];
    contacts.forEach(c=>{
      const cd=deals.filter(d=>d.phone===c.phone);
      rows.push([c.name,c.phone,c.email,c.type,c.company||'',cd.length,cd.length?uName(cd[0].comercialId):'']);
    });
  } else if(type==='sellers'){
    filename='importhub_vendedores.csv';
    rows=[['Marca','Stand','Vendedor','Telefone','Email','Localização','Rating','Deals realizados']];
    sellers.forEach(s=>{
      const sd=dealsForSeller(s.id);
      rows.push([s.brand,s.stand,s.name,s.phone,s.email,s.location,s.rating,sd.length]);
    });
  }
  const csv=rows.map(r=>r.map(v=>'"'+(String(v||'').replace(/"/g,'""'))+'"').join(',')).join('\n');
  const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');a.href=url;a.download=filename;a.click();
  URL.revokeObjectURL(url);
}

</script>
</body>
</html>
