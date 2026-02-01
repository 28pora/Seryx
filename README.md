<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ABB Crêpes</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        *{margin:0;padding:0;box-sizing:border-box}
        :root{--bg:#0a0a0f;--card:rgba(20,15,35,0.9);--purple:#8b5cf6;--purple-light:#a78bfa;--purple-dark:#6d28d9;--glow:rgba(139,92,246,0.4);--green:#10b981;--red:#ef4444;--orange:#f59e0b;--blue:#3b82f6;--text:#f1f5f9;--text2:#94a3b8;--muted:#64748b;--border:rgba(139,92,246,0.2)}
        body{font-family:'Rajdhani',sans-serif;background:var(--bg);color:var(--text);min-height:100vh}
        body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(139,92,246,0.03) 1px,transparent 1px),linear-gradient(90deg,rgba(139,92,246,0.03) 1px,transparent 1px);background-size:50px 50px;pointer-events:none}
        body::after{content:'';position:fixed;top:-50%;left:-50%;width:200%;height:200%;background:radial-gradient(ellipse at 30% 20%,rgba(139,92,246,0.12) 0%,transparent 50%);pointer-events:none}
        .login-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.95);z-index:10000;display:flex;align-items:center;justify-content:center}
        .login-overlay.hidden{display:none}
        .login-box{background:var(--card);border:1px solid var(--border);border-radius:20px;padding:40px;width:400px;text-align:center}
        .login-logo{font-size:50px;margin-bottom:15px}
        .login-title{font-family:'Orbitron',sans-serif;font-size:1.6rem;background:linear-gradient(135deg,var(--purple-light),var(--text));-webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:5px}
        .login-subtitle{color:var(--text2);margin-bottom:25px}
        .login-tabs{display:flex;gap:10px;margin-bottom:20px}
        .login-tab{flex:1;padding:12px;background:rgba(139,92,246,0.1);border:1px solid var(--border);border-radius:10px;color:var(--text2);font-family:'Rajdhani',sans-serif;font-weight:600;cursor:pointer;transition:all 0.3s}
        .login-tab.active{background:linear-gradient(135deg,var(--purple),var(--purple-dark));color:white;border-color:var(--purple)}
        .login-select,.login-input{width:100%;padding:14px 18px;background:rgba(10,10,15,0.8);border:1px solid var(--border);border-radius:10px;color:var(--text);font-family:'Rajdhani',sans-serif;font-size:1rem;margin-bottom:12px;outline:none}
        .login-input:focus,.login-select:focus{border-color:var(--purple);box-shadow:0 0 15px var(--glow)}
        .login-select-wrap{display:none}.login-select-wrap.show{display:block}
        .login-btn{width:100%;padding:14px;background:linear-gradient(135deg,var(--purple),var(--purple-dark));border:none;border-radius:10px;color:white;font-family:'Orbitron',sans-serif;font-size:0.95rem;font-weight:700;cursor:pointer}
        .login-btn:hover{transform:translateY(-2px);box-shadow:0 8px 25px var(--glow)}
        .login-error{color:var(--red);font-size:0.85rem;margin-top:12px;display:none}.login-error.show{display:block}
        .app{display:none;position:relative;z-index:1}
        .app.active{display:grid;grid-template-columns:260px 1fr 340px;grid-template-rows:65px 1fr;min-height:100vh}
        .app.livreur-mode{grid-template-columns:1fr 340px}
        .app.livreur-mode .sidebar{display:none}
        .header{grid-column:1/-1;background:var(--card);display:flex;align-items:center;justify-content:space-between;padding:0 25px;border-bottom:1px solid var(--border)}
        .logo{display:flex;align-items:center;gap:12px}
        .logo-icon{width:42px;height:42px;background:linear-gradient(135deg,var(--purple),var(--purple-dark));border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:22px}
        .logo-text{font-family:'Orbitron',sans-serif;font-size:1.3rem;font-weight:900;background:linear-gradient(135deg,var(--purple-light),var(--text));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
        .header-right{display:flex;align-items:center;gap:15px}
        .status-pill{display:flex;align-items:center;gap:6px;padding:6px 14px;background:rgba(16,185,129,0.15);border:1px solid rgba(16,185,129,0.3);border-radius:20px;font-size:0.8rem;font-weight:600}
        .status-dot{width:8px;height:8px;background:var(--green);border-radius:50%;animation:pulse 2s infinite}
        @keyframes pulse{0%,100%{box-shadow:0 0 8px var(--green)}50%{box-shadow:0 0 2px var(--green);opacity:0.6}}
        .role-badge{padding:6px 14px;border-radius:20px;font-size:0.75rem;font-weight:700;font-family:'Orbitron',sans-serif}
        .role-badge.admin{background:linear-gradient(135deg,var(--purple),var(--purple-dark));color:white}
        .role-badge.livreur{background:linear-gradient(135deg,var(--green),#059669);color:white}
        .user-info{display:flex;align-items:center;gap:10px;padding:6px 12px;border-radius:8px}
        .user-avatar{width:36px;height:36px;background:linear-gradient(135deg,var(--purple),var(--blue));border-radius:8px;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:0.9rem}
        .user-name{font-weight:600;font-size:0.9rem}
        .user-role{font-size:0.7rem;color:var(--text2)}
        .logout-btn{background:rgba(239,68,68,0.15);border:1px solid rgba(239,68,68,0.3);color:var(--red);padding:8px 14px;border-radius:8px;font-family:'Rajdhani',sans-serif;font-weight:600;cursor:pointer}
        .logout-btn:hover{background:var(--red);color:white}
        .sidebar{background:var(--card);padding:20px 12px;border-right:1px solid var(--border);overflow-y:auto}
        .nav-section{margin-bottom:20px}
        .nav-title{font-size:0.65rem;text-transform:uppercase;letter-spacing:2px;color:var(--muted);padding:8px 15px;font-weight:600}
        .nav-item{display:flex;align-items:center;gap:10px;padding:12px 15px;border-radius:8px;cursor:pointer;color:var(--text2);font-weight:500;transition:all 0.3s;margin-bottom:4px}
        .nav-item:hover{background:rgba(139,92,246,0.1);color:var(--text)}
        .nav-item.active{background:rgba(139,92,246,0.15);color:var(--purple-light)}
        .nav-icon{font-size:1.1rem;width:22px;text-align:center}
        .nav-badge{margin-left:auto;background:var(--purple);color:white;font-size:0.65rem;padding:2px 7px;border-radius:8px;font-weight:700}
        .main{background:var(--bg);padding:20px;overflow-y:auto}
        .stats{display:grid;grid-template-columns:repeat(4,1fr);gap:15px;margin-bottom:20px}
        .stats.small{grid-template-columns:repeat(3,1fr)}
        .stat-card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:18px;position:relative;overflow:hidden;cursor:pointer;transition:all 0.3s}
        .stat-card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--purple),var(--purple-light))}
        .stat-card:hover{transform:translateY(-3px);box-shadow:0 10px 30px rgba(139,92,246,0.15)}
        .stat-card.green::before{background:linear-gradient(90deg,var(--green),#34d399)}
        .stat-card.orange::before{background:linear-gradient(90deg,var(--orange),#fbbf24)}
        .stat-card.blue::before{background:linear-gradient(90deg,var(--blue),#60a5fa)}
        .stat-icon{width:40px;height:40px;background:rgba(139,92,246,0.15);border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:1.2rem;margin-bottom:12px}
        .stat-card.green .stat-icon{background:rgba(16,185,129,0.15)}
        .stat-card.orange .stat-icon{background:rgba(245,158,11,0.15)}
        .stat-card.blue .stat-icon{background:rgba(59,130,246,0.15)}
        .stat-value{font-family:'Orbitron',sans-serif;font-size:1.8rem;font-weight:700}
        .stat-label{color:var(--text2);font-size:0.8rem}
        .section{background:var(--card);border:1px solid var(--border);border-radius:14px;overflow:hidden;margin-bottom:20px}
        .section-header{display:flex;justify-content:space-between;align-items:center;padding:16px 20px;border-bottom:1px solid var(--border)}
        .section-title{font-family:'Orbitron',sans-serif;font-size:1rem;font-weight:700;display:flex;align-items:center;gap:8px}
        .section-actions{display:flex;gap:8px}
        .btn{padding:9px 16px;border-radius:8px;border:none;font-family:'Rajdhani',sans-serif;font-weight:600;font-size:0.85rem;cursor:pointer;transition:all 0.3s;display:flex;align-items:center;gap:6px}
        .btn-primary{background:linear-gradient(135deg,var(--purple),var(--purple-dark));color:white}
        .btn-primary:hover{transform:translateY(-1px);box-shadow:0 5px 15px var(--glow)}
        .btn-secondary{background:rgba(139,92,246,0.1);color:var(--purple-light);border:1px solid var(--border)}
        .btn-danger{background:rgba(239,68,68,0.2);color:var(--red)}
        .btn-danger:hover{background:var(--red);color:white}
        .btn-success{background:rgba(16,185,129,0.2);color:var(--green)}
        .btn-success:hover{background:var(--green);color:white}
        .table-row{display:grid;grid-template-columns:70px 1.5fr 1fr 1fr 90px 100px;padding:14px 20px;align-items:center;border-bottom:1px solid var(--border);transition:all 0.3s}
        .table-row.livreur-row{grid-template-columns:70px 1.5fr 1fr 90px 100px}
        .table-row:last-child{border-bottom:none}
        .table-row.header{background:rgba(139,92,246,0.05);font-size:0.7rem;text-transform:uppercase;letter-spacing:1px;color:var(--muted);font-weight:600}
        .table-row:not(.header):hover{background:rgba(139,92,246,0.05)}
        .order-id{font-family:'Orbitron',sans-serif;font-weight:700;color:var(--purple-light);font-size:0.9rem}
        .customer-name{font-weight:600}
        .customer-address{font-size:0.75rem;color:var(--text2)}
        .status-badge{display:inline-flex;align-items:center;gap:5px;padding:5px 10px;border-radius:15px;font-size:0.75rem;font-weight:600;cursor:pointer;transition:all 0.3s}
        .status-badge:hover{transform:scale(1.05)}
        .status-badge.pending{background:rgba(245,158,11,0.15);color:var(--orange)}
        .status-badge.progress{background:rgba(59,130,246,0.15);color:var(--blue)}
        .status-badge.completed{background:rgba(16,185,129,0.15);color:var(--green)}
        .status-badge.cancelled{background:rgba(239,68,68,0.15);color:var(--red)}
        .table-actions{display:flex;gap:6px}
        .action-btn{width:32px;height:32px;border-radius:6px;border:none;background:rgba(139,92,246,0.1);color:var(--text2);cursor:pointer;transition:all 0.3s;display:flex;align-items:center;justify-content:center;font-size:0.85rem}
        .action-btn:hover{background:var(--purple);color:white}
        .action-btn.delete:hover{background:var(--red)}
        .action-btn.success:hover{background:var(--green)}
        .reminder{display:flex;align-items:center;gap:12px;padding:14px;background:rgba(10,10,15,0.5);border-radius:10px;margin-bottom:10px;border-left:3px solid var(--purple);transition:all 0.3s;position:relative}
        .reminder:hover{background:rgba(139,92,246,0.08)}
        .reminder.urgent{border-left-color:var(--red)}
        .reminder.warning{border-left-color:var(--orange)}
        .reminder.info{border-left-color:var(--blue)}
        .reminder-icon{width:36px;height:36px;background:rgba(139,92,246,0.15);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:1rem}
        .reminder.urgent .reminder-icon{background:rgba(239,68,68,0.15)}
        .reminder.warning .reminder-icon{background:rgba(245,158,11,0.15)}
        .reminder.info .reminder-icon{background:rgba(59,130,246,0.15)}
        .reminder-content{flex:1}
        .reminder-title{font-weight:600;font-size:0.9rem}
        .reminder-desc{font-size:0.75rem;color:var(--text2)}
        .reminder-time{font-size:0.7rem;color:var(--muted)}
        .reminder-actions{position:absolute;right:12px;display:flex;gap:4px;opacity:0;transition:all 0.3s}
        .reminder:hover .reminder-actions{opacity:1}
        .reminder-btn{width:26px;height:26px;border-radius:5px;border:none;background:rgba(139,92,246,0.2);color:var(--text2);cursor:pointer;font-size:0.7rem;transition:all 0.3s}
        .reminder-btn:hover{background:var(--purple);color:white}
        .reminder-btn.delete:hover{background:var(--red)}
        .livreurs-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:12px;padding:15px}
        .livreur-card{background:rgba(10,10,15,0.5);border:1px solid var(--border);border-radius:10px;padding:18px;text-align:center;transition:all 0.3s;position:relative}
        .livreur-card:hover{border-color:var(--purple);transform:translateY(-2px)}
        .livreur-avatar{width:50px;height:50px;border-radius:12px;margin:0 auto 12px;display:flex;align-items:center;justify-content:center;font-size:1.2rem;font-weight:700}
        .livreur-avatar.purple{background:linear-gradient(135deg,var(--purple),var(--purple-dark))}
        .livreur-avatar.blue{background:linear-gradient(135deg,var(--blue),#2563eb)}
        .livreur-avatar.green{background:linear-gradient(135deg,var(--green),#059669)}
        .livreur-avatar.orange{background:linear-gradient(135deg,var(--orange),#d97706)}
        .livreur-name{font-weight:600;margin-bottom:6px}
        .livreur-status{font-size:0.75rem;padding:4px 10px;border-radius:12px;cursor:pointer}
        .livreur-status.online{background:rgba(16,185,129,0.15);color:var(--green)}
        .livreur-status.busy{background:rgba(245,158,11,0.15);color:var(--orange)}
        .livreur-status.offline{background:rgba(100,116,139,0.15);color:var(--muted)}
        .livreur-actions{position:absolute;top:8px;right:8px;display:flex;gap:4px;opacity:0;transition:all 0.3s}
        .livreur-card:hover .livreur-actions{opacity:1}
        .chat{background:var(--card);border-left:1px solid var(--border);display:flex;flex-direction:column}
        .chat-header{padding:16px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between}
        .chat-title{font-family:'Orbitron',sans-serif;font-size:0.95rem;font-weight:700}
        .online-indicator{display:flex;align-items:center;gap:8px}
        .online-avatars{display:flex}
        .online-avatar{width:26px;height:26px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:0.6rem;font-weight:700;margin-left:-6px;border:2px solid var(--card)}
        .online-avatar:first-child{margin-left:0}
        .online-count{background:var(--green);color:white;font-size:0.65rem;padding:3px 8px;border-radius:10px;font-weight:600}
        .chat-messages{flex:1;overflow-y:auto;padding:15px;display:flex;flex-direction:column;gap:12px}
        .chat-msg{display:flex;gap:10px;position:relative}
        .chat-msg:hover .msg-delete{opacity:1}
        .msg-delete{position:absolute;top:0;right:0;width:18px;height:18px;background:var(--red);border:none;border-radius:50%;color:white;font-size:0.6rem;cursor:pointer;opacity:0;transition:all 0.3s}
        .msg-avatar{width:34px;height:34px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:0.75rem;flex-shrink:0}
        .msg-content{flex:1}
        .msg-meta{display:flex;align-items:center;gap:8px;margin-bottom:4px}
        .msg-sender{font-weight:600;font-size:0.85rem}
        .msg-time{font-size:0.65rem;color:var(--muted)}
        .msg-text{background:rgba(139,92,246,0.1);padding:10px 12px;border-radius:0 10px 10px 10px;font-size:0.85rem;color:var(--text2);line-height:1.4}
        .chat-input-area{padding:15px;border-top:1px solid var(--border)}
        .chat-input-wrap{display:flex;gap:8px;background:rgba(10,10,15,0.5);border:1px solid var(--border);border-radius:10px;padding:6px}
        .chat-input{flex:1;background:none;border:none;color:var(--text);font-family:'Rajdhani',sans-serif;font-size:0.9rem;padding:8px 10px;outline:none}
        .chat-input::placeholder{color:var(--muted)}
        .chat-send{width:38px;height:38px;border-radius:8px;border:none;background:linear-gradient(135deg,var(--purple),var(--purple-dark));color:white;cursor:pointer;transition:all 0.3s}
        .chat-send:hover{transform:scale(1.05)}
        .modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.8);z-index:9999;display:flex;align-items:center;justify-content:center;opacity:0;visibility:hidden;transition:all 0.3s}
        .modal-overlay.active{opacity:1;visibility:visible}
        .modal{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:25px;width:450px;max-width:90%;transform:scale(0.9);transition:all 0.3s}
        .modal-overlay.active .modal{transform:scale(1)}
        .modal-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:20px}
        .modal-title{font-family:'Orbitron',sans-serif;font-size:1.1rem;font-weight:700}
        .modal-close{background:none;border:none;color:var(--text2);font-size:1.3rem;cursor:pointer}
        .modal-close:hover{color:var(--red)}
        .form-group{margin-bottom:15px}
        .form-label{display:block;margin-bottom:6px;font-weight:600;color:var(--text2);font-size:0.85rem}
        .form-input,.form-select{width:100%;padding:11px 14px;background:rgba(10,10,15,0.8);border:1px solid var(--border);border-radius:8px;color:var(--text);font-family:'Rajdhani',sans-serif;font-size:0.95rem;outline:none}
        .form-input:focus,.form-select:focus{border-color:var(--purple);box-shadow:0 0 10px var(--glow)}
        .form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
        .modal-actions{display:flex;gap:10px;justify-content:flex-end;margin-top:20px}
        .toast{position:fixed;bottom:25px;right:25px;background:var(--card);border:1px solid var(--green);border-radius:10px;padding:12px 20px;display:flex;align-items:center;gap:10px;z-index:10001;transform:translateY(80px);opacity:0;transition:all 0.3s}
        .toast.show{transform:translateY(0);opacity:1}
        .toast.error{border-color:var(--red)}
        .status-selector{display:flex;gap:10px;padding:15px;background:rgba(10,10,15,0.5);border-radius:10px;margin-bottom:20px}
        .status-opt{flex:1;padding:12px;border-radius:8px;border:1px solid var(--border);background:transparent;color:var(--text2);font-family:'Rajdhani',sans-serif;font-weight:600;cursor:pointer;text-align:center;transition:all 0.3s}
        .status-opt:hover{border-color:var(--purple)}
        .status-opt.active.online{background:var(--green);color:white;border-color:var(--green)}
        .status-opt.active.busy{background:var(--orange);color:white;border-color:var(--orange)}
        .status-opt.active.offline{background:var(--muted);color:white;border-color:var(--muted)}
        .content-grid{display:grid;grid-template-columns:1fr 320px;gap:20px}
        .view{display:none}.view.active{display:block}
        @media(max-width:1200px){.app.active{grid-template-columns:220px 1fr 300px}.stats{grid-template-columns:repeat(2,1fr)}.content-grid{grid-template-columns:1fr}}
        @media(max-width:900px){.app.active,.app.livreur-mode{grid-template-columns:1fr}.sidebar,.chat{display:none}.table-row{grid-template-columns:1fr;gap:8px}.table-row.header{display:none}}
    </style>
</head>
<body>
<div class="login-overlay" id="loginOverlay">
    <div class="login-box">
        <div class="login-logo">🥞</div>
        <h1 class="login-title">ABB CRÊPES</h1>
        <p class="login-subtitle">Connectez-vous pour continuer</p>
        <div class="login-tabs">
            <button class="login-tab active" onclick="setLoginMode('admin')">👑 Admin</button>
            <button class="login-tab" onclick="setLoginMode('livreur')">🚴 Livreur</button>
        </div>
        <div class="login-select-wrap" id="livreurSelectWrap">
            <select class="login-select" id="livreurSelect"></select>
        </div>
        <input type="password" class="login-input" id="loginInput" placeholder="Mot de passe">
        <button class="login-btn" onclick="login()">CONNEXION</button>
        <p class="login-error" id="loginError">Mot de passe incorrect</p>
    </div>
</div>
<div class="toast" id="toast"><span id="toastIcon">✅</span><span id="toastMsg">OK</span></div>
<div class="app" id="app">
    <header class="header">
        <div class="logo"><div class="logo-icon">🥞</div><span class="logo-text">ABB CRÊPES</span></div>
        <div class="header-right">
            <div class="status-pill"><span class="status-dot"></span>Service Actif</div>
            <div class="role-badge admin" id="roleBadge">👑 ADMIN</div>
            <div class="user-info"><div><div class="user-name" id="userName">Admin</div><div class="user-role" id="userRoleText">Administrateur</div></div><div class="user-avatar" id="userAvatar">AD</div></div>
            <button class="logout-btn" onclick="logout()">Déconnexion</button>
        </div>
    </header>
    <nav class="sidebar" id="sidebar">
        <div class="nav-section">
            <div class="nav-title">Principal</div>
            <div class="nav-item active" onclick="showView('dashboard')"><span class="nav-icon">📊</span>Dashboard</div>
            <div class="nav-item" onclick="showView('orders')"><span class="nav-icon">📦</span>Commandes<span class="nav-badge" id="ordersBadge">0</span></div>
            <div class="nav-item" onclick="showView('livreurs')"><span class="nav-icon">🚴</span>Livreurs<span class="nav-badge" id="livreursBadge">0</span></div>
        </div>
        <div class="nav-section">
            <div class="nav-title">Gestion</div>
            <div class="nav-item" onclick="showView('reminders')"><span class="nav-icon">📌</span>Rappels</div>
            <div class="nav-item" onclick="showView('settings')"><span class="nav-icon">⚙️</span>Paramètres</div>
        </div>
    </nav>
    <main class="main" id="main">
        <div class="view active" id="dashboardView">
            <div class="stats" id="statsContainer"></div>
            <div class="content-grid">
                <div class="section">
                    <div class="section-header"><h2 class="section-title">📦 Livraisons</h2><div class="section-actions"><button class="btn btn-primary" onclick="openModal('order')">+ Nouvelle</button></div></div>
                    <div id="ordersTable"></div>
                </div>
                <div class="section">
                    <div class="section-header"><h2 class="section-title">📌 À Penser</h2><button class="btn btn-secondary" onclick="openModal('reminder')">+ Ajouter</button></div>
                    <div style="padding:15px" id="remindersContainer"></div>
                </div>
            </div>
        </div>
        <div class="view" id="ordersView">
            <div class="section">
                <div class="section-header"><h2 class="section-title">📦 Toutes les Commandes</h2><div class="section-actions"><button class="btn btn-danger" onclick="clearCompleted()">🗑️ Nettoyer</button><button class="btn btn-primary" onclick="openModal('order')">+ Nouvelle</button></div></div>
                <div id="allOrdersTable"></div>
            </div>
        </div>
        <div class="view" id="livreursView">
            <div class="section">
                <div class="section-header"><h2 class="section-title">🚴 Équipe de Livreurs</h2><button class="btn btn-primary" onclick="openModal('livreur')">+ Ajouter</button></div>
                <div class="livreurs-grid" id="livreursGrid"></div>
            </div>
        </div>
        <div class="view" id="remindersView">
            <div class="section">
                <div class="section-header"><h2 class="section-title">📌 Tous les Rappels</h2><button class="btn btn-primary" onclick="openModal('reminder')">+ Nouveau</button></div>
                <div style="padding:15px" id="allRemindersContainer"></div>
            </div>
        </div>
        <div class="view" id="settingsView">
            <div class="section">
                <div class="section-header"><h2 class="section-title">⚙️ Paramètres</h2></div>
                <div style="padding:20px">
                    <div class="form-group"><label class="form-label">Nom Admin</label><input type="text" class="form-input" id="settingAdminName"></div>
                    <div class="form-row" style="margin-top:15px"><button class="btn btn-primary" onclick="saveSettings()">💾 Sauvegarder</button><button class="btn btn-danger" onclick="resetData()">🗑️ Réinitialiser</button></div>
                </div>
            </div>
        </div>
        <div class="view" id="livreurDashView">
            <div class="section" style="margin-bottom:20px">
                <div class="section-header"><h2 class="section-title">🚴 Mon Statut</h2></div>
                <div style="padding:15px"><div class="status-selector" id="statusSelector"></div></div>
            </div>
            <div class="stats small" id="livreurStats"></div>
            <div class="section">
                <div class="section-header"><h2 class="section-title">📦 Mes Livraisons</h2></div>
                <div id="myOrdersTable"></div>
            </div>
        </div>
    </main>
    <aside class="chat" id="chatPanel">
        <div class="chat-header">
            <h3 class="chat-title">💬 Chat Équipe</h3>
            <div class="online-indicator"><div class="online-avatars" id="onlineAvatars"></div><span class="online-count" id="onlineCount">0</span></div>
        </div>
        <div class="chat-messages" id="chatMessages"></div>
        <div class="chat-input-area">
            <div class="chat-input-wrap"><input type="text" class="chat-input" id="chatInput" placeholder="Écrire un message..."><button class="chat-send" onclick="sendMessage()">➤</button></div>
        </div>
    </aside>
</div>
<div class="modal-overlay" id="modalOverlay" onclick="if(event.target===this)closeModal()"><div class="modal" id="modalContent"></div></div>
<script>
const ADMIN_PASS='PoraUHQ',LIVREUR_PASS='ABB Crêpes';
let currentUser=null,loginMode='admin';
let data={stats:{completed:47,pending:8,revenue:892},orders:[{id:2847,customer:'Marie Laurent',address:'12 Rue de la Paix',livreurId:1,status:'progress',time:'12:45',items:'Crêpe Nutella x2'},{id:2846,customer:'Pierre Durand',address:'45 Ave des Champs',livreurId:2,status:'pending',time:'12:52',items:'Crêpe Complète x1'},{id:2845,customer:'Sophie Martin',address:'8 Blvd Haussman',livreurId:3,status:'completed',time:'12:30',items:'Crêpe Sucre x3'},{id:2844,customer:'Jean Petit',address:'23 Rue Rivoli',livreurId:1,status:'completed',time:'12:15',items:'Crêpe Citron x1'},{id:2843,customer:'Claire Dubois',address:'67 Rue de Rome',livreurId:4,status:'cancelled',time:'11:58',items:'Crêpe Beurre x2'}],livreurs:[{id:1,name:'Lucas M.',initials:'LM',color:'purple',status:'online'},{id:2,name:'Emma T.',initials:'ET',color:'blue',status:'busy'},{id:3,name:'Noah R.',initials:'NR',color:'green',status:'online'},{id:4,name:'Léa B.',initials:'LB',color:'orange',status:'online'},{id:5,name:'Adam K.',initials:'AK',color:'purple',status:'offline'}],reminders:[{id:1,title:'Stock Nutella Bas',desc:'Seulement 3 pots restants',time:'Urgent',type:'urgent',icon:'🔴'},{id:2,title:'Maintenance Scooter #3',desc:'Révision prévue demain',time:'Demain',type:'warning',icon:'🟠'},{id:3,title:'Formation Nouveau Livreur',desc:'Adam - Vendredi 14h',time:'Vendredi',type:'info',icon:'🔵'},{id:4,title:'Commande Farine',desc:'Passer commande fournisseur',time:'Cette semaine',type:'',icon:'💡'}],messages:[{id:1,senderId:1,text:'Je suis en route pour #2847, ETA 10 min 🚴',time:'12:42'},{id:2,senderId:2,text:'La #2846 est presque prête, je pars dans 5 min',time:'12:44'},{id:3,senderId:3,text:'Livraison #2845 effectuée ✅',time:'12:46'},{id:4,senderId:4,text:'Je reviens au shop 👍',time:'12:48'}],settings:{adminName:'Admin'},nextOrderId:2848};
function save(){localStorage.setItem('abbCrepes',JSON.stringify(data))}
function load(){const s=localStorage.getItem('abbCrepes');if(s)data=JSON.parse(s)}
function setLoginMode(m){loginMode=m;document.querySelectorAll('.login-tab').forEach((t,i)=>t.classList.toggle('active',(m==='admin'&&i===0)||(m==='livreur'&&i===1)));document.getElementById('livreurSelectWrap').classList.toggle('show',m==='livreur');document.getElementById('loginError').classList.remove('show')}
function populateLivreurSelect(){document.getElementById('livreurSelect').innerHTML=data.livreurs.map(l=>`<option value="${l.id}">${l.name}</option>`).join('')}
function login(){const pass=document.getElementById('loginInput').value,err=document.getElementById('loginError');if(loginMode==='admin'&&pass===ADMIN_PASS){currentUser={type:'admin',name:data.settings.adminName};err.classList.remove('show');startApp()}else if(loginMode==='livreur'&&pass===LIVREUR_PASS){const lid=parseInt(document.getElementById('livreurSelect').value),liv=data.livreurs.find(l=>l.id===lid);if(liv){currentUser={type:'livreur',id:lid,name:liv.name,initials:liv.initials,color:liv.color};liv.status='online';save();err.classList.remove('show');startApp()}}else{err.classList.add('show')}}
function logout(){if(currentUser?.type==='livreur'){const liv=data.livreurs.find(l=>l.id===currentUser.id);if(liv){liv.status='offline';save()}}currentUser=null;document.getElementById('app').classList.remove('active');document.getElementById('loginOverlay').classList.remove('hidden');document.getElementById('loginInput').value=''}
document.getElementById('loginInput').addEventListener('keypress',e=>{if(e.key==='Enter')login()});
document.getElementById('chatInput').addEventListener('keypress',e=>{if(e.key==='Enter')sendMessage()});
function startApp(){document.getElementById('loginOverlay').classList.add('hidden');document.getElementById('app').classList.add('active');if(currentUser.type==='admin'){document.getElementById('app').classList.remove('livreur-mode');document.getElementById('roleBadge').className='role-badge admin';document.getElementById('roleBadge').textContent='👑 ADMIN';document.getElementById('userName').textContent=data.settings.adminName;document.getElementById('userRoleText').textContent='Administrateur';document.getElementById('userAvatar').textContent='AD';showView('dashboard')}else{document.getElementById('app').classList.add('livreur-mode');document.getElementById('roleBadge').className='role-badge livreur';document.getElementById('roleBadge').textContent='🚴 LIVREUR';document.getElementById('userName').textContent=currentUser.name;document.getElementById('userRoleText').textContent='Livreur';document.getElementById('userAvatar').textContent=currentUser.initials;showView('livreurDash')}renderAll()}
function showView(v){document.querySelectorAll('.view').forEach(x=>x.classList.remove('active'));document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));document.getElementById(v+'View').classList.add('active');renderAll()}
function renderAll(){renderStats();renderOrders();renderReminders();renderLivreurs();renderChat();updateBadges();if(currentUser?.type==='livreur')renderLivreurDash()}
function renderStats(){const ol=data.livreurs.filter(l=>l.status!=='offline').length;document.getElementById('statsContainer').innerHTML=`<div class="stat-card green"><div class="stat-icon">✅</div><div class="stat-value">${data.stats.completed}</div><div class="stat-label">Livraisons Effectuées</div></div><div class="stat-card orange"><div class="stat-icon">⏳</div><div class="stat-value">${data.stats.pending}</div><div class="stat-label">En Attente</div></div><div class="stat-card blue"><div class="stat-icon">🚴</div><div class="stat-value">${ol}</div><div class="stat-label">Livreurs Actifs</div></div><div class="stat-card"><div class="stat-icon">💰</div><div class="stat-value">€${data.stats.revenue}</div><div class="stat-label">Revenus du Jour</div></div>`}
function renderOrders(){const h=`<div class="table-row header"><div>ID</div><div>Client</div><div>Livreur</div><div>Statut</div><div>Heure</div><div>Actions</div></div>`,r=data.orders.map(o=>{const l=data.livreurs.find(x=>x.id===o.livreurId);return`<div class="table-row"><div class="order-id">#${o.id}</div><div><div class="customer-name">${o.customer}</div><div class="customer-address">${o.address}</div></div><div>${l?.name||'-'}</div><div><span class="status-badge ${o.status}" onclick="cycleStatus(${o.id})">${sIcon(o.status)} ${sText(o.status)}</span></div><div>${o.time}</div><div class="table-actions"><button class="action-btn" onclick="openModal('order',${o.id})">✏️</button><button class="action-btn delete" onclick="deleteOrder(${o.id})">🗑️</button></div></div>`}).join('');document.getElementById('ordersTable').innerHTML=h+r;document.getElementById('allOrdersTable').innerHTML=h+r}
function renderReminders(){const html=data.reminders.map(r=>`<div class="reminder ${r.type}"><div class="reminder-icon">${r.icon}</div><div class="reminder-content"><div class="reminder-title">${r.title}</div><div class="reminder-desc">${r.desc}</div></div><div class="reminder-time">${r.time}</div><div class="reminder-actions"><button class="reminder-btn" onclick="openModal('reminder',${r.id})">✏️</button><button class="reminder-btn delete" onclick="deleteReminder(${r.id})">🗑️</button></div></div>`).join('');document.getElementById('remindersContainer').innerHTML=html;document.getElementById('allRemindersContainer').innerHTML=html}
function renderLivreurs(){document.getElementById('livreursGrid').innerHTML=data.livreurs.map(l=>`<div class="livreur-card"><div class="livreur-actions"><button class="action-btn" onclick="openModal('livreur',${l.id})">✏️</button><button class="action-btn delete" onclick="deleteLivreur(${l.id})">🗑️</button></div><div class="livreur-avatar ${l.color}">${l.initials}</div><div class="livreur-name">${l.name}</div><span class="livreur-status ${l.status}" onclick="cycleLivreurStatus(${l.id})">${sLabel(l.status)}</span></div>`).join('')}
function renderChat(){const isA=currentUser?.type==='admin';document.getElementById('chatMessages').innerHTML=data.messages.map(m=>{const s=m.senderId===0?{name:data.settings.adminName,initials:'AD',color:'purple'}:data.livreurs.find(l=>l.id===m.senderId)||{name:'?',initials:'?',color:'purple'};return`<div class="chat-msg">${isA?`<button class="msg-delete" onclick="deleteMessage(${m.id})">×</button>`:''}<div class="msg-avatar ${s.color}">${s.initials}</div><div class="msg-content"><div class="msg-meta"><span class="msg-sender">${s.name}</span><span class="msg-time">${m.time}</span></div><div class="msg-text">${m.text}</div></div></div>`}).join('');document.getElementById('chatMessages').scrollTop=99999;const on=data.livreurs.filter(l=>l.status!=='offline');document.getElementById('onlineAvatars').innerHTML=on.slice(0,4).map(l=>`<div class="online-avatar ${l.color}">${l.initials}</div>`).join('');document.getElementById('onlineCount').textContent=on.length+' en ligne'}
function renderLivreurDash(){const liv=data.livreurs.find(l=>l.id===currentUser.id);if(!liv)return;document.getElementById('statusSelector').innerHTML=['online','busy','offline'].map(s=>`<button class="status-opt ${s} ${liv.status===s?'active':''}" onclick="setMyStatus('${s}')">${sLabel(s)}</button>`).join('');const my=data.orders.filter(o=>o.livreurId===currentUser.id),mc=my.filter(o=>o.status==='completed').length,mp=my.filter(o=>o.status==='pending'||o.status==='progress').length;document.getElementById('livreurStats').innerHTML=`<div class="stat-card green"><div class="stat-icon">✅</div><div class="stat-value">${mc}</div><div class="stat-label">Effectuées</div></div><div class="stat-card orange"><div class="stat-icon">⏳</div><div class="stat-value">${mp}</div><div class="stat-label">En cours</div></div><div class="stat-card blue"><div class="stat-icon">📦</div><div class="stat-value">${my.length}</div><div class="stat-label">Total</div></div>`;const h=`<div class="table-row livreur-row header"><div>ID</div><div>Client</div><div>Statut</div><div>Heure</div><div>Actions</div></div>`,r=my.map(o=>`<div class="table-row livreur-row" style="${o.status==='progress'?'border-left:3px solid var(--purple);':''}"><div class="order-id">#${o.id}</div><div><div class="customer-name">${o.customer}</div><div class="customer-address">${o.address}</div></div><div><span class="status-badge ${o.status}" onclick="cycleMyOrder(${o.id})">${sIcon(o.status)} ${sText(o.status)}</span></div><div>${o.time}</div><div class="table-actions">${o.status==='pending'?`<button class="action-btn success" onclick="startOrder(${o.id})">▶️</button>`:''}${o.status==='progress'?`<button class="action-btn success" onclick="completeOrder(${o.id})">✅</button>`:''}</div></div>`).join('');document.getElementById('myOrdersTable').innerHTML=h+(r||'<div style="padding:30px;text-align:center;color:var(--muted)">Aucune livraison</div>')}
function updateBadges(){document.getElementById('ordersBadge').textContent=data.orders.filter(o=>o.status!=='completed'&&o.status!=='cancelled').length;document.getElementById('livreursBadge').textContent=data.livreurs.filter(l=>l.status!=='offline').length}
function sIcon(s){return{pending:'⏳',progress:'🚴',completed:'✅',cancelled:'❌'}[s]||'📦'}
function sText(s){return{pending:'Préparation',progress:'En route',completed:'Livrée',cancelled:'Annulée'}[s]||s}
function sLabel(s){return{online:'🟢 En ligne',busy:'🟠 Occupé',offline:'⚫ Hors ligne'}[s]||s}
function getTime(){const n=new Date();return n.getHours().toString().padStart(2,'0')+':'+n.getMinutes().toString().padStart(2,'0')}
function toast(m,e){const t=document.getElementById('toast');document.getElementById('toastIcon').textContent=e?'❌':'✅';document.getElementById('toastMsg').textContent=m;t.className='toast show'+(e?' error':'');setTimeout(()=>t.classList.remove('show'),3000)}
function cycleStatus(id){const o=data.orders.find(x=>x.id===id),a=['pending','progress','completed','cancelled'];o.status=a[(a.indexOf(o.status)+1)%a.length];save();renderAll();toast('Statut mis à jour')}
function cycleMyOrder(id){const o=data.orders.find(x=>x.id===id);if(o.status==='pending')o.status='progress';else if(o.status==='progress')o.status='completed';save();renderAll();toast('Statut mis à jour')}
function startOrder(id){data.orders.find(x=>x.id===id).status='progress';save();renderAll();toast('Livraison démarrée')}
function completeOrder(id){data.orders.find(x=>x.id===id).status='completed';save();renderAll();toast('Livraison terminée 🎉')}
function cycleLivreurStatus(id){const l=data.livreurs.find(x=>x.id===id),a=['online','busy','offline'];l.status=a[(a.indexOf(l.status)+1)%a.length];save();renderAll();toast(`${l.name}: ${sLabel(l.status)}`)}
function setMyStatus(s){data.livreurs.find(x=>x.id===currentUser.id).status=s;save();renderAll();toast(`Statut: ${sLabel(s)}`)}
function deleteOrder(id){if(confirm('Supprimer?')){data.orders=data.orders.filter(o=>o.id!==id);save();renderAll();toast('Supprimé')}}
function deleteReminder(id){if(confirm('Supprimer?')){data.reminders=data.reminders.filter(r=>r.id!==id);save();renderAll();toast('Supprimé')}}
function deleteLivreur(id){if(confirm('Supprimer?')){data.livreurs=data.livreurs.filter(l=>l.id!==id);save();renderAll();populateLivreurSelect();toast('Supprimé')}}
function deleteMessage(id){data.messages=data.messages.filter(m=>m.id!==id);save();renderChat()}
function clearCompleted(){if(confirm('Supprimer terminées?')){data.orders=data.orders.filter(o=>o.status!=='completed'&&o.status!=='cancelled');save();renderAll();toast('Nettoyé')}}
function sendMessage(){const i=document.getElementById('chatInput'),t=i.value.trim();if(!t)return;data.messages.push({id:Date.now(),senderId:currentUser.type==='admin'?0:currentUser.id,text:t,time:getTime()});save();renderChat();i.value=''}
function saveSettings(){data.settings.adminName=document.getElementById('settingAdminName').value||'Admin';save();if(currentUser?.type==='admin')document.getElementById('userName').textContent=data.settings.adminName;toast('Sauvegardé')}
function resetData(){if(confirm('⚠️ Tout réinitialiser?')){localStorage.removeItem('abbCrepes');location.reload()}}
function openModal(type,id=null){const m=document.getElementById('modalContent');let h='';if(type==='order'){const o=id?data.orders.find(x=>x.id===id):null;h=`<div class="modal-header"><h3 class="modal-title">${o?'Modifier':'Nouvelle'} Commande</h3><button class="modal-close" onclick="closeModal()">×</button></div><div class="form-group"><label class="form-label">Client</label><input class="form-input" id="mCustomer" value="${o?.customer||''}"></div><div class="form-group"><label class="form-label">Adresse</label><input class="form-input" id="mAddress" value="${o?.address||''}"></div><div class="form-group"><label class="form-label">Articles</label><input class="form-input" id="mItems" value="${o?.items||''}"></div><div class="form-row"><div class="form-group"><label class="form-label">Livreur</label><select class="form-select" id="mLivreur">${data.livreurs.map(l=>`<option value="${l.id}" ${o?.livreurId===l.id?'selected':''}>${l.name}</option>`).join('')}</select></div><div class="form-group"><label class="form-label">Statut</label><select class="form-select" id="mStatus"><option value="pending" ${o?.status==='pending'?'selected':''}>⏳ Préparation</option><option value="progress" ${o?.status==='progress'?'selected':''}>🚴 En route</option><option value="completed" ${o?.status==='completed'?'selected':''}>✅ Livrée</option><option value="cancelled" ${o?.status==='cancelled'?'selected':''}>❌ Annulée</option></select></div></div><div class="modal-actions"><button class="btn btn-secondary" onclick="closeModal()">Annuler</button><button class="btn btn-primary" onclick="saveOrder(${id})">Sauvegarder</button></div>`}else if(type==='reminder'){const r=id?data.reminders.find(x=>x.id===id):null;h=`<div class="modal-header"><h3 class="modal-title">${r?'Modifier':'Nouveau'} Rappel</h3><button class="modal-close" onclick="closeModal()">×</button></div><div class="form-group"><label class="form-label">Titre</label><input class="form-input" id="mTitle" value="${r?.title||''}"></div><div class="form-group"><label class="form-label">Description</label><input class="form-input" id="mDesc" value="${r?.desc||''}"></div><div class="form-row"><div class="form-group"><label class="form-label">Échéance</label><input class="form-input" id="mTime" value="${r?.time||''}"></div><div class="form-group"><label class="form-label">Priorité</label><select class="form-select" id="mType"><option value="" ${r?.type===''?'selected':''}>💡 Normal</option><option value="info" ${r?.type==='info'?'selected':''}>🔵 Info</option><option value="warning" ${r?.type==='warning'?'selected':''}>🟠 Attention</option><option value="urgent" ${r?.type==='urgent'?'selected':''}>🔴 Urgent</option></select></div></div><div class="modal-actions"><button class="btn btn-secondary" onclick="closeModal()">Annuler</button><button class="btn btn-primary" onclick="saveReminder(${id})">Sauvegarder</button></div>`}else if(type==='livreur'){const l=id?data.livreurs.find(x=>x.id===id):null;h=`<div class="modal-header"><h3 class="modal-title">${l?'Modifier':'Nouveau'} Livreur</h3><button class="modal-close" onclick="closeModal()">×</button></div><div class="form-group"><label class="form-label">Nom</label><input class="form-input" id="mName" value="${l?.name||''}"></div><div class="form-row"><div class="form-group"><label class="form-label">Initiales</label><input class="form-input" id="mInitials" value="${l?.initials||''}" maxlength="2"></div><div class="form-group"><label class="form-label">Couleur</label><select class="form-select" id="mColor"><option value="purple" ${l?.color==='purple'?'selected':''}>🟣 Violet</option><option value="blue" ${l?.color==='blue'?'selected':''}>🔵 Bleu</option><option value="green" ${l?.color==='green'?'selected':''}>🟢 Vert</option><option value="orange" ${l?.color==='orange'?'selected':''}>🟠 Orange</option></select></div></div><div class="form-group"><label class="form-label">Statut</label><select class="form-select" id="mLivStatus"><option value="online" ${l?.status==='online'?'selected':''}>🟢 En ligne</option><option value="busy" ${l?.status==='busy'?'selected':''}>🟠 Occupé</option><option value="offline" ${l?.status==='offline'?'selected':''}>⚫ Hors ligne</option></select></div><div class="modal-actions"><button class="btn btn-secondary" onclick="closeModal()">Annuler</button><button class="btn btn-primary" onclick="saveLivreur(${id})">Sauvegarder</button></div>`}m.innerHTML=h;document.getElementById('modalOverlay').classList.add('active')}
function closeModal(){document.getElementById('modalOverlay').classList.remove('active')}
function saveOrder(id){const o={id:id||data.nextOrderId++,customer:document.getElementById('mCustomer').value,address:document.getElementById('mAddress').value,items:document.getElementById('mItems').value,livreurId:parseInt(document.getElementById('mLivreur').value),status:document.getElementById('mStatus').value,time:getTime()};if(id){const i=data.orders.findIndex(x=>x.id===id);data.orders[i]=o}else data.orders.unshift(o);save();renderAll();closeModal();toast('Sauvegardé')}
function saveReminder(id){const icons={'':'💡',info:'🔵',warning:'🟠',urgent:'🔴'},type=document.getElementById('mType').value,r={id:id||Date.now(),title:document.getElementById('mTitle').value,desc:document.getElementById('mDesc').value,time:document.getElementById('mTime').value,type:type,icon:icons[type]};if(id){const i=data.reminders.findIndex(x=>x.id===id);data.reminders[i]=r}else data.reminders.unshift(r);save();renderAll();closeModal();toast('Sauvegardé')}
function saveLivreur(id){const l={id:id||Date.now(),name:document.getElementById('mName').value,initials:document.getElementById('mInitials').value.toUpperCase(),color:document.getElementById('mColor').value,status:document.getElementById('mLivStatus').value};if(id){const i=data.livreurs.findIndex(x=>x.id===id);data.livreurs[i]=l}else data.livreurs.push(l);save();renderAll();populateLivreurSelect();closeModal();toast('Sauvegardé')}
load();populateLivreurSelect();document.getElementById('settingAdminName').value=data.settings.adminName;
</script>
</body>
</html>
