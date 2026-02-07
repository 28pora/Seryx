<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#1a0033">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>ABB Crêpes - Avis Clients</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html {
            font-size: 16px;
            -webkit-text-size-adjust: 100%;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(180deg, #1a0033 0%, #2d1b4e 100%);
            background-attachment: fixed;
            color: #e0e0e0;
            min-height: 100vh;
            overflow-x: hidden;
            -webkit-overflow-scrolling: touch;
        }

        .mobile-header {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 60px;
            background: rgba(26, 0, 51, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(157, 78, 221, 0.3);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 15px;
            z-index: 1000;
        }

        .mobile-header h1 {
            font-size: 1.2rem;
            color: #9d4edd;
            font-weight: 700;
        }

        .menu-btn {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, #9d4edd, #7b2cbf);
            border: none;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(157, 78, 221, 0.3);
        }

        .menu-btn span {
            width: 20px;
            height: 2px;
            background: white;
            border-radius: 2px;
            transition: all 0.3s ease;
        }

        .menu-btn.active span:nth-child(1) {
            transform: rotate(45deg) translate(5px, 5px);
        }

        .menu-btn.active span:nth-child(2) {
            opacity: 0;
        }

        .menu-btn.active span:nth-child(3) {
            transform: rotate(-45deg) translate(5px, -5px);
        }

        .menu-overlay {
            position: fixed;
            top: 60px;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            z-index: 999;
        }

        .menu-overlay.show {
            opacity: 1;
            visibility: visible;
        }

        .menu-content {
            background: rgba(30, 30, 50, 0.98);
            backdrop-filter: blur(20px);
            border-radius: 0 0 20px 20px;
            padding: 20px;
            transform: translateY(-100%);
            transition: transform 0.3s ease;
        }

        .menu-overlay.show .menu-content {
            transform: translateY(0);
        }

        .menu-item {
            padding: 16px;
            background: rgba(157, 78, 221, 0.1);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 12px;
            color: #e0e0e0;
            font-size: 1rem;
            font-weight: 600;
            text-align: center;
            cursor: pointer;
        }

        .main-content {
            padding: 75px 15px 20px;
        }

        .admin-badge {
            background: linear-gradient(135deg, #9d4edd, #7b2cbf);
            padding: 8px 16px;
            border-radius: 20px;
            color: white;
            font-weight: 700;
            font-size: 0.85rem;
            display: inline-block;
            margin-bottom: 15px;
            box-shadow: 0 4px 12px rgba(157, 78, 221, 0.4);
        }

        .welcome-card {
            background: rgba(157, 78, 221, 0.1);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
        }

        .welcome-card h2 {
            color: #9d4edd;
            font-size: 1.5rem;
            margin-bottom: 8px;
        }

        .welcome-card p {
            color: #b8b8b8;
            font-size: 0.95rem;
            line-height: 1.5;
        }

        .stats-container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .stat-box {
            background: rgba(30, 30, 50, 0.6);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 12px;
            padding: 16px 8px;
            text-align: center;
        }

        .stat-value {
            font-size: 1.8rem;
            font-weight: 700;
            color: #9d4edd;
            margin-bottom: 4px;
        }

        .stat-label {
            font-size: 0.75rem;
            color: #b8b8b8;
            line-height: 1.2;
        }

        .stars {
            color: #ffd700;
            font-size: 1rem;
            margin: 4px 0;
        }

        .admin-controls {
            display: grid;
            gap: 10px;
            margin-bottom: 20px;
        }

        .admin-btn {
            padding: 14px;
            background: linear-gradient(135deg, #9d4edd, #7b2cbf);
            border: none;
            border-radius: 12px;
            color: white;
            font-size: 0.95rem;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(157, 78, 221, 0.3);
        }

        .admin-btn.danger {
            background: linear-gradient(135deg, #dc2626, #991b1b);
        }

        .form-card {
            background: rgba(30, 30, 50, 0.6);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .form-card h3 {
            color: #9d4edd;
            font-size: 1.3rem;
            margin-bottom: 20px;
            text-align: center;
        }

        .form-section {
            margin-bottom: 24px;
        }

        .form-label {
            display: block;
            color: #e0e0e0;
            font-size: 0.95rem;
            font-weight: 600;
            margin-bottom: 12px;
            line-height: 1.4;
        }

        .input-field {
            width: 100%;
            padding: 14px;
            background: rgba(50, 50, 70, 0.5);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 12px;
            color: #e0e0e0;
            font-size: 1rem;
            font-family: inherit;
        }

        .input-field:focus {
            outline: none;
            border-color: #9d4edd;
            box-shadow: 0 0 0 3px rgba(157, 78, 221, 0.2);
        }

        textarea.input-field {
            min-height: 100px;
            resize: vertical;
        }

        .options-grid {
            display: grid;
            gap: 10px;
        }

        .option-box {
            position: relative;
        }

        .option-box input {
            position: absolute;
            opacity: 0;
            cursor: pointer;
        }

        .option-label {
            display: flex;
            align-items: center;
            padding: 14px 16px;
            background: rgba(50, 50, 70, 0.5);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 12px;
            color: #e0e0e0;
            font-size: 0.95rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .option-box input:checked + .option-label {
            background: rgba(157, 78, 221, 0.3);
            border-color: #9d4edd;
            color: white;
        }

        .option-icon {
            width: 20px;
            height: 20px;
            border: 2px solid rgba(157, 78, 221, 0.5);
            border-radius: 50%;
            margin-right: 12px;
            flex-shrink: 0;
            position: relative;
        }

        .option-box input[type="checkbox"] + .option-label .option-icon {
            border-radius: 4px;
        }

        .option-box input:checked + .option-label .option-icon {
            background: #9d4edd;
            border-color: #9d4edd;
        }

        .option-box input:checked + .option-label .option-icon::after {
            content: '✓';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-size: 0.8rem;
            font-weight: 700;
        }

        .scale-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 8px;
            margin-bottom: 8px;
        }

        .scale-item input {
            position: absolute;
            opacity: 0;
        }

        .scale-label {
            display: block;
            padding: 14px 8px;
            background: rgba(50, 50, 70, 0.5);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 12px;
            color: #e0e0e0;
            font-size: 1.1rem;
            font-weight: 700;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .scale-item input:checked + .scale-label {
            background: linear-gradient(135deg, #9d4edd, #7b2cbf);
            border-color: #9d4edd;
            transform: scale(1.1);
            box-shadow: 0 4px 12px rgba(157, 78, 221, 0.4);
        }

        .scale-helper {
            display: flex;
            justify-content: space-between;
            font-size: 0.75rem;
            color: #888;
            padding: 0 4px;
        }

        .stars-input {
            display: flex;
            justify-content: center;
            gap: 8px;
            font-size: 2.5rem;
            margin: 16px 0;
        }

        .stars-input input {
            display: none;
        }

        .stars-input label {
            color: #555;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .stars-input input:checked ~ label,
        .stars-input label:hover,
        .stars-input label:hover ~ label {
            color: #ffd700;
        }

        .submit-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #9d4edd, #7b2cbf);
            border: none;
            border-radius: 12px;
            color: white;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(157, 78, 221, 0.4);
            margin-top: 8px;
        }

        .reviews-section h3 {
            color: #9d4edd;
            font-size: 1.3rem;
            margin-bottom: 16px;
            text-align: center;
        }

        .review-item {
            background: rgba(30, 30, 50, 0.6);
            border: 2px solid rgba(157, 78, 221, 0.3);
            border-radius: 16px;
            padding: 16px;
            margin-bottom: 12px;
        }

        .review-top {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
        }

        .review-author {
            font-weight: 700;
            color: #9d4edd;
            font-size: 1rem;
        }

        .review-date {
            font-size: 0.8rem;
            color: #888;
        }

        .review-stars {
            color: #ffd700;
            font-size: 1rem;
            margin: 4px 0;
        }

        .review-text {
            color: #d0d0d0;
            font-size: 0.9rem;
            line-height: 1.6;
            margin-bottom: 12px;
        }

        .review-details {
            background: rgba(50, 50, 70, 0.3);
            border-radius: 10px;
            padding: 12px;
            margin-bottom: 12px;
            font-size: 0.85rem;
        }

        .review-details div {
            margin-bottom: 6px;
            color: #b8b8b8;
            line-height: 1.4;
        }

        .review-details strong {
            color: #9d4edd;
        }

        .review-actions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            padding-top: 12px;
            border-top: 1px solid rgba(157, 78, 221, 0.2);
        }

        .action-btn {
            padding: 10px;
            border: none;
            border-radius: 8px;
            font-size: 0.85rem;
            font-weight: 700;
            cursor: pointer;
        }

        .action-btn.edit {
            background: rgba(59, 130, 246, 0.2);
            border: 2px solid rgba(59, 130, 246, 0.5);
            color: #60a5fa;
        }

        .action-btn.delete {
            background: rgba(220, 38, 38, 0.2);
            border: 2px solid rgba(220, 38, 38, 0.5);
            color: #f87171;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.9);
            z-index: 2000;
            overflow-y: auto;
            padding: 20px;
        }

        .modal-card {
            background: linear-gradient(180deg, #1a0033 0%, #2d1b4e 100%);
            border: 2px solid rgba(157, 78, 221, 0.5);
            border-radius: 16px;
            padding: 24px;
            max-width: 500px;
            margin: 0 auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-title {
            color: #9d4edd;
            font-size: 1.4rem;
            font-weight: 700;
        }

        .close-btn {
            width: 36px;
            height: 36px;
            border: none;
            background: rgba(255, 255, 255, 0.1);
            color: #e0e0e0;
            font-size: 1.5rem;
            border-radius: 8px;
            cursor: pointer;
            line-height: 1;
        }

        .modal-actions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-top: 24px;
        }

        .btn-save {
            padding: 14px;
            background: linear-gradient(135deg, #9d4edd, #7b2cbf);
            border: none;
            border-radius: 12px;
            color: white;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
        }

        .btn-cancel {
            padding: 14px;
            background: rgba(100, 100, 120, 0.3);
            border: 2px solid rgba(100, 100, 120, 0.5);
            border-radius: 12px;
            color: #e0e0e0;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
        }

        .no-reviews {
            text-align: center;
            padding: 40px 20px;
            color: #888;
            font-size: 1rem;
        }

        .hidden {
            display: none !important;
        }

        /* Desktop responsive */
        @media (min-width: 768px) {
            .main-content {
                max-width: 800px;
                margin: 0 auto;
                padding: 90px 20px 40px;
            }

            .stats-container {
                gap: 20px;
            }

            .stat-box {
                padding: 24px 16px;
            }

            .stat-value {
                font-size: 2.5rem;
            }

            .stat-label {
                font-size: 0.9rem;
            }

            .options-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <!-- Header mobile -->
    <div class="mobile-header">
        <h1>🥞 ABB Crêpes</h1>
        <button class="menu-btn" id="menuBtn">
            <span></span>
            <span></span>
            <span></span>
        </button>
    </div>

    <!-- Menu overlay -->
    <div class="menu-overlay" id="menuOverlay">
        <div class="menu-content">
            <div class="menu-item" onclick="openAdminPanel()">🔒 Accès Admin</div>
        </div>
    </div>

    <!-- Contenu principal -->
    <div class="main-content">
        <div id="adminBadge" class="admin-badge hidden">👤 MODE ADMIN</div>

        <div class="welcome-card" id="welcomeCard">
            <h2>Avis Clients</h2>
            <p id="welcomeText">Découvrez ce que nos clients pensent de nos délicieuses crêpes</p>
        </div>

        <!-- Contrôles admin -->
        <div id="adminControls" class="admin-controls hidden">
            <button class="admin-btn" onclick="exportToExcel()">📊 Télécharger Excel</button>
            <button class="admin-btn" onclick="refreshData()">🔄 Actualiser</button>
            <button class="admin-btn" onclick="exitAdminMode()">👁️ Mode Client</button>
            <button class="admin-btn danger" onclick="clearAllData()">🗑️ Tout supprimer</button>
        </div>

        <!-- Statistiques -->
        <div class="stats-container">
            <div class="stat-box">
                <div class="stat-value" id="avgRating">4.7</div>
                <div class="stars">★★★★★</div>
                <div class="stat-label">Note Moyenne</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="totalReviews">3</div>
                <div class="stat-label">Avis Total</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="satisfied">100%</div>
                <div class="stat-label">Clients Satisfaits</div>
            </div>
        </div>

        <!-- Formulaire -->
        <div class="form-card" id="reviewForm">
            <h3>Donnez votre avis</h3>
            <form id="clientForm">
                <div class="form-section">
                    <label class="form-label">Intéressé par la livraison ?</label>
                    <div class="options-grid">
                        <div class="option-box">
                            <input type="radio" name="delivery_interest" value="Oui" id="delivery_yes" required>
                            <label for="delivery_yes" class="option-label">
                                <span class="option-icon"></span>
                                Oui
                            </label>
                        </div>
                        <div class="option-box">
                            <input type="radio" name="delivery_interest" value="Non" id="delivery_no">
                            <label for="delivery_no" class="option-label">
                                <span class="option-icon"></span>
                                Non
                            </label>
                        </div>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Moments préférés ? (plusieurs choix)</label>
                    <div class="options-grid">
                        <div class="option-box">
                            <input type="checkbox" name="moment" value="Goûter" id="moment1">
                            <label for="moment1" class="option-label">
                                <span class="option-icon"></span>
                                Goûter
                            </label>
                        </div>
                        <div class="option-box">
                            <input type="checkbox" name="moment" value="Soirée" id="moment2">
                            <label for="moment2" class="option-label">
                                <span class="option-icon"></span>
                                Soirée
                            </label>
                        </div>
                        <div class="option-box">
                            <input type="checkbox" name="moment" value="Week-end" id="moment3">
                            <label for="moment3" class="option-label">
                                <span class="option-icon"></span>
                                Week-end
                            </label>
                        </div>
                        <div class="option-box">
                            <input type="checkbox" name="moment" value="Occasion spéciale" id="moment4">
                            <label for="moment4" class="option-label">
                                <span class="option-icon"></span>
                                Occasion spéciale
                            </label>
                        </div>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Type de crêpes préféré ?</label>
                    <div class="options-grid">
                        <div class="option-box">
                            <input type="radio" name="type_crepe" value="Sucrées" id="type1" required>
                            <label for="type1" class="option-label">
                                <span class="option-icon"></span>
                                Sucrées
                            </label>
                        </div>
                        <div class="option-box">
                            <input type="radio" name="type_crepe" value="Salées" id="type2">
                            <label for="type2" class="option-label">
                                <span class="option-icon"></span>
                                Salées
                            </label>
                        </div>
                        <div class="option-box">
                            <input type="radio" name="type_crepe" value="Les deux" id="type3">
                            <label for="type3" class="option-label">
                                <span class="option-icon"></span>
                                Les deux
                            </label>
                        </div>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Goût des crêpes</label>
                    <div class="scale-grid">
                        <div class="scale-item">
                            <input type="radio" name="gout" value="1" id="gout1" required>
                            <label for="gout1" class="scale-label">1</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="gout" value="2" id="gout2">
                            <label for="gout2" class="scale-label">2</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="gout" value="3" id="gout3">
                            <label for="gout3" class="scale-label">3</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="gout" value="4" id="gout4">
                            <label for="gout4" class="scale-label">4</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="gout" value="5" id="gout5">
                            <label for="gout5" class="scale-label">5</label>
                        </div>
                    </div>
                    <div class="scale-helper">
                        <span>Pas satisfait</span>
                        <span>Très satisfait</span>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Qualité des ingrédients</label>
                    <div class="scale-grid">
                        <div class="scale-item">
                            <input type="radio" name="qualite" value="1" id="qualite1" required>
                            <label for="qualite1" class="scale-label">1</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="qualite" value="2" id="qualite2">
                            <label for="qualite2" class="scale-label">2</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="qualite" value="3" id="qualite3">
                            <label for="qualite3" class="scale-label">3</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="qualite" value="4" id="qualite4">
                            <label for="qualite4" class="scale-label">4</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="qualite" value="5" id="qualite5">
                            <label for="qualite5" class="scale-label">5</label>
                        </div>
                    </div>
                    <div class="scale-helper">
                        <span>Pas satisfait</span>
                        <span>Très satisfait</span>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Recommanderiez-vous ABB Crêpes ?</label>
                    <div class="scale-grid">
                        <div class="scale-item">
                            <input type="radio" name="recommandation" value="1" id="reco1" required>
                            <label for="reco1" class="scale-label">1</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="recommandation" value="2" id="reco2">
                            <label for="reco2" class="scale-label">2</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="recommandation" value="3" id="reco3">
                            <label for="reco3" class="scale-label">3</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="recommandation" value="4" id="reco4">
                            <label for="reco4" class="scale-label">4</label>
                        </div>
                        <div class="scale-item">
                            <input type="radio" name="recommandation" value="5" id="reco5">
                            <label for="reco5" class="scale-label">5</label>
                        </div>
                    </div>
                    <div class="scale-helper">
                        <span>Peu probable</span>
                        <span>Très probable</span>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Note globale</label>
                    <div class="stars-input">
                        <input type="radio" name="rating" id="star5" value="5" required>
                        <label for="star5">★</label>
                        <input type="radio" name="rating" id="star4" value="4">
                        <label for="star4">★</label>
                        <input type="radio" name="rating" id="star3" value="3">
                        <label for="star3">★</label>
                        <input type="radio" name="rating" id="star2" value="2">
                        <label for="star2">★</label>
                        <input type="radio" name="rating" id="star1" value="1">
                        <label for="star1">★</label>
                    </div>
                </div>

                <div class="form-section">
                    <label class="form-label">Votre prénom</label>
                    <input type="text" class="input-field" id="name" placeholder="Marie" required>
                </div>

                <div class="form-section">
                    <label class="form-label">Votre commentaire (optionnel)</label>
                    <textarea class="input-field" id="comment" placeholder="Partagez votre expérience..."></textarea>
                </div>

                <button type="submit" class="submit-btn">Envoyer mon avis</button>
            </form>
        </div>

        <!-- Liste des avis -->
        <div class="reviews-section">
            <h3>Les avis</h3>
            <div id="reviewsList"></div>
        </div>
    </div>

    <!-- Modal d'édition -->
    <div id="editModal" class="modal">
        <div class="modal-card">
            <div class="modal-header">
                <h3 class="modal-title">✏️ Modifier l'avis</h3>
                <button class="close-btn" onclick="closeModal()">×</button>
            </div>
            <form id="editForm">
                <input type="hidden" id="editId">
                <div class="form-section">
                    <label class="form-label">Prénom</label>
                    <input type="text" class="input-field" id="editAuthor" required>
                </div>
                <div class="form-section">
                    <label class="form-label">Note (1-5)</label>
                    <input type="number" class="input-field" id="editRating" min="1" max="5" required>
                </div>
                <div class="form-section">
                    <label class="form-label">Commentaire</label>
                    <textarea class="input-field" id="editText" required></textarea>
                </div>
                <div class="form-section">
                    <label class="form-label">Date</label>
                    <input type="date" class="input-field" id="editDate" required>
                </div>
                <div class="form-section">
                    <label class="form-label">Heure</label>
                    <input type="time" class="input-field" id="editTime" required>
                </div>
                <div class="modal-actions">
                    <button type="button" class="btn-cancel" onclick="closeModal()">Annuler</button>
                    <button type="submit" class="btn-save">💾 Sauvegarder</button>
                </div>
            </form>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script>
        let isAdminMode = false;
        const ADMIN_PASSWORD = "PiedSec72";

        // Menu toggle
        document.getElementById('menuBtn').addEventListener('click', function(e) {
            e.stopPropagation();
            this.classList.toggle('active');
            document.getElementById('menuOverlay').classList.toggle('show');
        });

        document.getElementById('menuOverlay').addEventListener('click', function(e) {
            if (e.target === this) {
                document.getElementById('menuBtn').classList.remove('active');
                this.classList.remove('show');
            }
        });

        function initializeReviews() {
            const existing = localStorage.getItem('abb_crepes_reviews');
            if (!existing) {
                const defaultReviews = [
                    {
                        id: 1,
                        author: "Julie",
                        rating: 5,
                        text: "Première commande hier soir, j'ai testé la crêpe Nutella. Livrée en 20 minutes, encore chaude ! Le livreur était souriant et poli. Bonne surprise pour une ouverture 😊",
                        date: "2026-02-06",
                        heure: "19:15",
                        questionnaire: {
                            deliveryInterest: "Oui",
                            moments: "Soirée",
                            typeCrepesPreferees: "Sucrées",
                            noteGout: "5",
                            noteQualite: "5",
                            noteRecommandation: "5"
                        }
                    },
                    {
                        id: 2,
                        author: "Maxime",
                        rating: 5,
                        text: "Commandé vers 19h30 hier. Service rapide, crêpe complète bien garnie. Franchement pour une première soirée c'était nickel. Je retesterai !",
                        date: "2026-02-06",
                        heure: "19:45",
                        questionnaire: {
                            deliveryInterest: "Oui",
                            moments: "Soirée, Week-end",
                            typeCrepesPreferees: "Les deux",
                            noteGout: "5",
                            noteQualite: "4",
                            noteRecommandation: "5"
                        }
                    },
                    {
                        id: 3,
                        author: "Sarah",
                        rating: 4,
                        text: "Testé hier soir, les crêpes sont bonnes ! La livraison a pris 25 min environ mais c'était l'ouverture donc normal. Contente qu'il y ait enfin ça au Mans",
                        date: "2026-02-06",
                        heure: "20:10",
                        questionnaire: {
                            deliveryInterest: "Oui",
                            moments: "Goûter, Week-end",
                            typeCrepesPreferees: "Sucrées",
                            noteGout: "4",
                            noteQualite: "4",
                            noteRecommandation: "4"
                        }
                    }
                ];
                localStorage.setItem('abb_crepes_reviews', JSON.stringify(defaultReviews));
            }
        }

        function openAdminPanel() {
            const password = prompt('🔒 Mot de passe administrateur :');
            if (password === ADMIN_PASSWORD) {
                isAdminMode = true;
                document.getElementById('adminControls').classList.remove('hidden');
                document.getElementById('adminBadge').classList.remove('hidden');
                document.getElementById('reviewForm').classList.add('hidden');
                document.getElementById('welcomeText').textContent = 'Panel de gestion des avis clients';
                document.getElementById('menuBtn').classList.remove('active');
                document.getElementById('menuOverlay').classList.remove('show');
                renderReviews();
            } else if (password !== null) {
                alert('❌ Mot de passe incorrect !');
            }
        }

        function exitAdminMode() {
            isAdminMode = false;
            document.getElementById('adminControls').classList.add('hidden');
            document.getElementById('adminBadge').classList.add('hidden');
            document.getElementById('reviewForm').classList.remove('hidden');
            document.getElementById('welcomeText').textContent = 'Découvrez ce que nos clients pensent de nos délicieuses crêpes';
            renderReviews();
        }

        function loadReviews() {
            const saved = localStorage.getItem('abb_crepes_reviews');
            return saved ? JSON.parse(saved) : [];
        }

        function saveReviews(reviews) {
            localStorage.setItem('abb_crepes_reviews', JSON.stringify(reviews));
        }

        function renderReviews() {
            const reviews = loadReviews();
            const reviewsList = document.getElementById('reviewsList');

            if (reviews.length === 0) {
                reviewsList.innerHTML = '<div class="no-reviews">Aucun avis disponible</div>';
                return;
            }

            reviewsList.innerHTML = reviews.map(review => `
                <div class="review-item">
                    <div class="review-top">
                        <div>
                            <div class="review-author">${review.author}${isAdminMode ? ' (ID: ' + review.id + ')' : ''}</div>
                            <div class="review-stars">${'★'.repeat(review.rating)}${'☆'.repeat(5-review.rating)}</div>
                        </div>
                        <div class="review-date">${formatDate(review.date)}<br>${review.heure}</div>
                    </div>
                    <div class="review-text">${review.text}</div>
                    
                    ${isAdminMode && review.questionnaire ? `
                    <div class="review-details">
                        <div><strong>Livraison:</strong> ${review.questionnaire.deliveryInterest || 'N/A'}</div>
                        <div><strong>Moments:</strong> ${review.questionnaire.moments || 'N/A'}</div>
                        <div><strong>Type:</strong> ${review.questionnaire.typeCrepesPreferees || 'N/A'}</div>
                        <div><strong>Goût:</strong> ${review.questionnaire.noteGout || 'N/A'}/5 | 
                             <strong>Qualité:</strong> ${review.questionnaire.noteQualite || 'N/A'}/5 | 
                             <strong>Reco:</strong> ${review.questionnaire.noteRecommandation || 'N/A'}/5</div>
                    </div>
                    ` : ''}

                    ${isAdminMode ? `
                    <div class="review-actions">
                        <button class="action-btn edit" onclick="editReview(${review.id})">✏️ Modifier</button>
                        <button class="action-btn delete" onclick="deleteReview(${review.id})">🗑️ Supprimer</button>
                    </div>
                    ` : ''}
                </div>
            `).join('');
        }

        function formatDate(dateStr) {
            const date = new Date(dateStr);
            return date.toLocaleDateString('fr-FR', { day: '2-digit', month: '2-digit', year: 'numeric' });
        }

        function updateStats() {
            const reviews = loadReviews();
            if (reviews.length === 0) {
                document.getElementById('totalReviews').textContent = '0';
                document.getElementById('avgRating').textContent = '-';
                document.getElementById('satisfied').textContent = '-';
                return;
            }

            const total = reviews.length;
            const avgRating = (reviews.reduce((sum, r) => sum + r.rating, 0) / total).toFixed(1);
            const satisfied = Math.round((reviews.filter(r => r.rating >= 4).length / total) * 100);
            
            document.getElementById('totalReviews').textContent = total;
            document.getElementById('avgRating').textContent = avgRating;
            document.getElementById('satisfied').textContent = satisfied + '%';
        }

        function editReview(id) {
            const reviews = loadReviews();
            const review = reviews.find(r => r.id === id);
            
            if (review) {
                document.getElementById('editId').value = review.id;
                document.getElementById('editAuthor').value = review.author;
                document.getElementById('editRating').value = review.rating;
                document.getElementById('editText').value = review.text;
                document.getElementById('editDate').value = review.date;
                document.getElementById('editTime').value = review.heure;
                document.getElementById('editModal').style.display = 'block';
            }
        }

        function deleteReview(id) {
            if (confirm('⚠️ Supprimer cet avis ?')) {
                const reviews = loadReviews();
                saveReviews(reviews.filter(r => r.id !== id));
                refreshData();
                alert('✅ Avis supprimé');
            }
        }

        function closeModal() {
            document.getElementById('editModal').style.display = 'none';
        }

        document.getElementById('editForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const id = parseInt(document.getElementById('editId').value);
            const reviews = loadReviews();
            const reviewIndex = reviews.findIndex(r => r.id === id);
            
            if (reviewIndex !== -1) {
                reviews[reviewIndex].author = document.getElementById('editAuthor').value;
                reviews[reviewIndex].rating = parseInt(document.getElementById('editRating').value);
                reviews[reviewIndex].text = document.getElementById('editText').value;
                reviews[reviewIndex].date = document.getElementById('editDate').value;
                reviews[reviewIndex].heure = document.getElementById('editTime').value;
                saveReviews(reviews);
                closeModal();
                refreshData();
                alert('✅ Avis modifié');
            }
        });

        document.getElementById('clientForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const name = document.getElementById('name').value;
            const comment = document.getElementById('comment').value || "Aucun commentaire supplémentaire";
            const rating = parseInt(document.querySelector('input[name="rating"]:checked').value);
            const deliveryInterest = document.querySelector('input[name="delivery_interest"]:checked')?.value || "";
            const typeCrepesPreferees = document.querySelector('input[name="type_crepe"]:checked')?.value || "";
            const moments = Array.from(document.querySelectorAll('input[name="moment"]:checked')).map(cb => cb.value).join(', ') || "";
            const noteGout = document.querySelector('input[name="gout"]:checked')?.value || "";
            const noteQualite = document.querySelector('input[name="qualite"]:checked')?.value || "";
            const noteRecommandation = document.querySelector('input[name="recommandation"]:checked')?.value || "";

            const now = new Date();
            const reviews = loadReviews();
            
            const newReview = {
                id: reviews.length > 0 ? Math.max(...reviews.map(r => r.id)) + 1 : 1,
                author: name,
                rating: rating,
                text: comment,
                date: now.toISOString().split('T')[0],
                heure: now.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' }),
                questionnaire: { deliveryInterest, moments, typeCrepesPreferees, noteGout, noteQualite, noteRecommandation }
            };

            reviews.unshift(newReview);
            saveReviews(reviews);
            updateStats();
            renderReviews();
            this.reset();
            window.scrollTo({ top: 0, behavior: 'smooth' });
            alert('✅ Merci pour votre avis ! 🥞');
        });

        function refreshData() {
            updateStats();
            renderReviews();
        }

        function exportToExcel() {
            const reviews = loadReviews();
            if (reviews.length === 0) {
                alert('❌ Aucun avis à exporter');
                return;
            }

            const data = reviews.map(r => ({
                'ID': r.id,
                'Date': r.date,
                'Heure': r.heure,
                'Prénom': r.author,
                'Note': r.rating,
                'Livraison': r.questionnaire?.deliveryInterest || '',
                'Moments': r.questionnaire?.moments || '',
                'Type': r.questionnaire?.typeCrepesPreferees || '',
                'Goût': r.questionnaire?.noteGout || '',
                'Qualité': r.questionnaire?.noteQualite || '',
                'Reco': r.questionnaire?.noteRecommandation || '',
                'Commentaire': r.text
            }));

            const ws = XLSX.utils.json_to_sheet(data);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Avis");
            XLSX.writeFile(wb, `ABB_Crepes_${new Date().toISOString().split('T')[0]}.xlsx`);
        }

        function clearAllData() {
            if (confirm('⚠️ Supprimer TOUS les avis ?')) {
                if (confirm('✋ Confirmation finale ?')) {
                    localStorage.removeItem('abb_crepes_reviews');
                    refreshData();
                    alert('✅ Données supprimées');
                }
            }
        }

        // Init
        initializeReviews();
        renderReviews();
        updateStats();
    </script>
</body>
</html>
