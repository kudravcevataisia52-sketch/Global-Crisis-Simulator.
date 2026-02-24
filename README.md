<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Global Crisis Simulator | Геополитический тренажёр</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background: #0a0f1f;
            color: #fff;
        }

        /* Навигация */
        .navbar {
            background: rgba(10, 20, 30, 0.95);
            padding: 15px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 1000;
            border-bottom: 2px solid #ffd700;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            color: #ffd700;
            cursor: pointer;
        }

        .logo i {
            margin-right: 10px;
            color: #ffd700;
        }

        .nav-links {
            display: flex;
            gap: 30px;
            align-items: center;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            font-size: 16px;
            padding: 8px 16px;
            border-radius: 20px;
            transition: 0.3s;
            cursor: pointer;
        }

        .nav-links a:hover {
            background: rgba(255, 215, 0, 0.2);
            color: #ffd700;
        }

        .nav-links a.active {
            background: #ffd700;
            color: #0a0f1f;
            font-weight: bold;
        }

        .auth-buttons {
            display: flex;
            gap: 10px;
        }

        .btn {
            padding: 8px 20px;
            border-radius: 25px;
            border: none;
            cursor: pointer;
            font-weight: 600;
            transition: 0.3s;
        }

        .btn-login {
            background: transparent;
            border: 2px solid #ffd700;
            color: #ffd700;
        }

        .btn-login:hover {
            background: #ffd700;
            color: #0a0f1f;
        }

        .btn-register {
            background: #ffd700;
            color: #0a0f1f;
        }

        .btn-register:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px #ffd700;
        }

        /* Контейнер */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Страницы */
        .page {
            display: none;
        }

        .page.active {
            display: block;
        }

        /* Hero секция */
        .hero {
            background: linear-gradient(145deg, #1a2f3f, #0f1f2f);
            border-radius: 30px;
            padding: 80px 50px;
            margin: 30px 0;
            text-align: center;
        }

        .hero h1 {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .hero .highlight {
            color: #ffd700;
        }

        .hero p {
            font-size: 20px;
            color: #a0c0e0;
            margin-bottom: 30px;
        }

        .hero-btn {
            background: #ffd700;
            color: #0a0f1f;
            border: none;
            padding: 18px 45px;
            font-size: 20px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
        }

        .hero-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px #ffd700;
        }

        /* Карточки кризисов */
        .section-title {
            font-size: 32px;
            margin: 40px 0 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .crisis-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 25px;
        }

        .crisis-card {
            background: rgba(30, 40, 60, 0.7);
            border-radius: 25px;
            padding: 25px;
            cursor: pointer;
            transition: 0.3s;
            border: 2px solid transparent;
        }

        .crisis-card:hover {
            transform: translateY(-5px);
            border-color: #ffd700;
        }

        .crisis-type {
            display: inline-block;
            padding: 5px 15px;
            background: #1a4b8c;
            border-radius: 20px;
            font-size: 14px;
            margin-bottom: 15px;
        }

        /* Карта мира */
        .map-container {
            background: #1a2f3f;
            border-radius: 30px;
            padding: 30px;
            margin: 40px 0;
            height: 400px;
            position: relative;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 500" fill="none" stroke="%23333"><path d="M200,150 L250,120 L300,140 L350,130 L400,150 L450,140 L500,160 L550,150 L600,170 L650,160 L700,180 L750,170 L800,190" stroke="%23444"/><circle cx="300" cy="200" r="5" fill="%23ff4444"/><circle cx="500" cy="250" r="5" fill="%23ffaa44"/><circle cx="700" cy="180" r="5" fill="%2344ff44"/></svg>');
            background-size: cover;
        }

        /* Страны */
        .countries-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 20px;
            margin: 30px 0;
        }

        .country-card {
            background: rgba(30, 40, 60, 0.7);
            border-radius: 20px;
            padding: 20px;
            cursor: pointer;
            transition: 0.3s;
            border: 2px solid transparent;
        }

        .country-card:hover {
            border-color: #ffd700;
        }

        .country-card.selected {
            border-color: #ffd700;
            background: rgba(255, 215, 0, 0.1);
        }

        .country-flag {
            font-size: 40px;
            margin-bottom: 10px;
        }

        /* Игровой интерфейс */
        .game-interface {
            display: grid;
            grid-template-columns: 300px 1fr 300px;
            gap: 20px;
            margin-top: 30px;
        }

        .panel {
            background: rgba(20, 30, 45, 0.9);
            border-radius: 25px;
            padding: 20px;
        }

        .stat-item {
            display: flex;
            justify-content: space-between;
            margin: 15px 0;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #2a3f4f;
            border-radius: 4px;
            margin-top: 5px;
        }

        .progress-fill {
            height: 100%;
            background: #ffd700;
            border-radius: 4px;
        }

        .decision-btn {
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            background: #1a2f3f;
            border: 2px solid #ffd700;
            border-radius: 15px;
            color: white;
            cursor: pointer;
            transition: 0.3s;
            text-align: left;
        }

        .decision-btn:hover {
            background: #ffd700;
            color: #0a0f1f;
        }

        /* Модальное окно регистрации */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 2000;
            justify-content: center;
            align-items: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: #1a2f3f;
            padding: 40px;
            border-radius: 30px;
            width: 400px;
            border: 2px solid #ffd700;
        }

        .modal-content h2 {
            margin-bottom: 30px;
            color: #ffd700;
        }

        .modal-content input {
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            border: none;
            border-radius: 10px;
            background: #0a1f2f;
            color: white;
        }

        .modal-content button {
            width: 100%;
            padding: 15px;
            margin: 20px 0;
            background: #ffd700;
            border: none;
            border-radius: 10px;
            font-weight: bold;
            cursor: pointer;
        }

        .close {
            float: right;
            font-size: 28px;
            cursor: pointer;
            color: #ffd700;
        }

        /* Уведомления */
        .notification {
            position: fixed;
            top: 100px;
            right: 20px;
            background: #ffd700;
            color: #0a0f1f;
            padding: 15px 25px;
            border-radius: 10px;
            z-index: 1500;
            display: none;
        }

        .notification.show {
            display: block;
        }

        /* Футер */
        .footer {
            background: rgba(10, 20, 30, 0.9);
            border-radius: 30px;
            padding: 40px;
            margin-top: 60px;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 30px;
        }
    </style>
</head>
<body>
    <!-- Навигация -->
    <div class="navbar">
        <div class="logo" onclick="showPage('home')">
            <i class="fas fa-globe-americas"></i>
            GCS
        </div>
        <div class="nav-links">
            <a onclick="showPage('home')" class="active" data-page="home">Главная</a>
            <a onclick="showPage('scenarios')" data-page="scenarios">Сценарии</a>
            <a onclick="showPage('countries')" data-page="countries">Страны</a>
            <a onclick="showPage('game')" data-page="game">Игра</a>
            <a onclick="showPage('learning')" data-page="learning">Обучение</a>
            <a onclick="showPage('community')" data-page="community">Сообщество</a>
            <a onclick="showPage('rating')" data-page="rating">Рейтинг</a>
        </div>
        <div class="auth-buttons">
            <button class="btn btn-login" onclick="showLogin()">Войти</button>
            <button class="btn btn-register" onclick="showRegister()">Регистрация</button>
        </div>
    </div>

    <!-- Уведомление -->
    <div class="notification" id="notification"></div>

    <!-- Модальное окно регистрации -->
    <div class="modal" id="registerModal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('registerModal')">&times;</span>
            <h2>Регистрация</h2>
            <input type="text" placeholder="Имя пользователя" id="regName">
            <input type="email" placeholder="Email" id="regEmail">
            <input type="password" placeholder="Пароль" id="regPassword">
            <button onclick="register()">Зарегистрироваться</button>
        </div>
    </div>

    <!-- Модальное окно входа -->
    <div class="modal" id="loginModal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('loginModal')">&times;</span>
            <h2>Вход</h2>
            <input type="text" placeholder="Имя пользователя" id="loginName">
            <input type="password" placeholder="Пароль" id="loginPassword">
            <button onclick="login()">Войти</button>
        </div>
    </div>

    <div class="container">
        <!-- Главная страница -->
        <div id="home-page" class="page active">
            <div class="hero">
                <h1>
                    <span class="highlight">Почувствуй</span> себя лидером страны —<br>
                    <span class="highlight">реши кризис!</span>
                </h1>
                <p>Выберите страну. Решайте реальные международные кризисы. Смотрите последствия.</p>
                <button class="hero-btn" onclick="showPage('scenarios')">
                    <i class="fas fa-play"></i> Начать кризис
                </button>
            </div>

            <div class="section-title">
                <i class="fas fa-fire" style="color: #ffd700;"></i>
                <h2>Текущие кризисы</h2>
            </div>

            <div class="crisis-grid">
                <div class="crisis-card" onclick="selectScenario(1)">
                    <span class="crisis-type" style="background: #c41e3a;">⚡ Энергетический</span>
                    <h3>Энергетический кризис 2026</h3>
                    <p>Глобальный дефицит энергии из-за прекращения поставок</p>
                    <div style="margin-top: 15px; color: #ffd700;">
                        <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star-half-alt"></i>
                    </div>
                </div>
                <div class="crisis-card" onclick="selectScenario(2)">
                    <span class="crisis-type" style="background: #ed6c02;">🌍 Военный</span>
                    <h3>Конфликт в Восточной Европе</h3>
                    <p>Эскалация напряжённости между соседними странами</p>
                    <div style="margin-top: 15px; color: #ffd700;">
                        <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                    </div>
                </div>
                <div class="crisis-card" onclick="selectScenario(3)">
                    <span class="crisis-type" style="background: #0288d1;">💻 Кибер</span>
                    <h3>Киберугроза глобальной сети</h3>
                    <p>Массированная атака на критическую инфраструктуру</p>
                    <div style="margin-top: 15px; color: #ffd700;">
                        <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                    </div>
                </div>
            </div>

            <div class="map-container">
                <!-- Карта мира с кризисами -->
            </div>
        </div>

        <!-- Страница сценариев -->
        <div id="scenarios-page" class="page">
            <div class="section-title">
                <i class="fas fa-scroll"></i>
                <h2>Выберите сценарий</h2>
            </div>
            <div class="crisis-grid" id="scenarios-list"></div>
        </div>

        <!-- Страница выбора страны -->
        <div id="countries-page" class="page">
            <div class="section-title">
                <i class="fas fa-flag"></i>
                <h2>Выберите страну</h2>
            </div>
            <div class="countries-grid" id="countries-list"></div>
            <button class="hero-btn" style="width: 100%; margin-top: 20px;" onclick="selectCountryAndStart()">
                Начать игру с выбранной страной
            </button>
        </div>

        <!-- Страница игры -->
        <div id="game-page" class="page">
            <div class="game-interface">
                <div class="panel">
                    <h3><i class="fas fa-chart-line"></i> Показатели</h3>
                    <div id="game-stats"></div>
                </div>
                <div class="panel">
                    <h3><i class="fas fa-exclamation-triangle"></i> Кризис</h3>
                    <div id="crisis-display"></div>
                    <div id="decisions-list"></div>
                    <div class="advisor-note" id="advisor"></div>
                </div>
                <div class="panel">
                    <h3><i class="fas fa-users"></i> Команда</h3>
                    <div id="team-chat"></div>
                </div>
            </div>
        </div>

        <!-- Страница обучения -->
        <div id="learning-page" class="page">
            <div class="section-title">
                <i class="fas fa-graduation-cap"></i>
                <h2>Обучение</h2>
            </div>
            <div class="crisis-grid">
                <div class="crisis-card" onclick="startModule('basics')">
                    <i class="fas fa-book" style="font-size: 40px; color: #ffd700;"></i>
                    <h3>Основы международных отношений</h3>
                    <p>5 уроков</p>
                </div>
                <div class="crisis-card" onclick="startModule('history')">
                    <i class="fas fa-history" style="font-size: 40px; color: #ffd700;"></i>
                    <h3>История кризисов</h3>
                    <p>8 уроков</p>
                </div>
                <div class="crisis-card" onclick="startModule('diplomacy')">
                    <i class="fas fa-handshake" style="font-size: 40px; color: #ffd700;"></i>
                    <h3>Дипломатия</h3>
                    <p>4 урока</p>
                </div>
            </div>
        </div>

        <!-- Страница сообщества -->
        <div id="community-page" class="page">
            <div class="section-title">
                <i class="fas fa-users"></i>
                <h2>Сообщество</h2>
            </div>
            <div style="background: rgba(30,40,60,0.7); border-radius: 25px; padding: 30px;">
                <h3>Форум</h3>
                <div style="margin: 20px 0; padding: 15px; background: rgba(0,0,0,0.3); border-radius: 15px;">
                    <p><strong>Турнир школ:</strong> Регистрация открыта до пятницы</p>
                </div>
                <div style="margin: 20px 0; padding: 15px; background: rgba(0,0,0,0.3); border-radius: 15px;">
                    <p><strong>Лучшие решения:</strong> Голосуем за кризис месяца</p>
                </div>
            </div>
        </div>

        <!-- Страница рейтинга -->
        <div id="rating-page" class="page">
            <div class="section-title">
                <i class="fas fa-trophy"></i>
                <h2>Рейтинг лидеров</h2>
            </div>
            <div style="background: rgba(30,40,60,0.7); border-radius: 25px; padding: 30px;">
                <table style="width: 100%;">
                    <tr><th>1.</th><td>GlobalLeader</td><td>3250 очков</td></tr>
                    <tr><th>2.</th><td>CrisisManager</td><td>2980 очков</td></tr>
                    <tr><th>3.</th><td>DiplomatPro</td><td>2810 очков</td></tr>
                </table>
            </div>
        </div>

        <!-- Футер -->
        <div class="footer">
            <div>
                <h4>О проекте</h4>
                <p>Тренажёр геополитического мышления</p>
            </div>
            <div>
                <h4>Сообщество</h4>
                <p onclick="showNotification('Обсуждаем идеи')">Обсуждаем идеи</p>
                <p onclick="showNotification('Делимся стратегиями')">Делимся стратегиями</p>
            </div>
            <div>
                <h4>Поддержка</h4>
                <p onclick="showNotification('От учеников для учеников')">От учеников для учеников</p>
            </div>
            <div>
                <h4>Подписка</h4>
                <input type="email" placeholder="Email" style="padding: 10px; border-radius: 5px;">
            </div>
        </div>
    </div>

    <script>
        // Текущая страница
        let currentPage = 'home';
        let selectedCountry = null;
        let selectedScenario = null;
        let isLoggedIn = false;

        // Данные
        const countries = [
            { name: 'США', flag: '🇺🇸', power: 95, economy: 98 },
            { name: 'Россия', flag: '🇷🇺', power: 90, economy: 65 },
            { name: 'Китай', flag: '🇨🇳', power: 92, economy: 94 },
            { name: 'Германия', flag: '🇩🇪', power: 70, economy: 92 },
            { name: 'Франция', flag: '🇫🇷', power: 75, economy: 85 },
            { name: 'Великобритания', flag: '🇬🇧', power: 72, economy: 88 },
            { name: 'Япония', flag: '🇯🇵', power: 68, economy: 90 },
            { name: 'Индия', flag: '🇮🇳', power: 80, economy: 70 }
        ];

        const scenarios = [
            { name: 'Энергетический кризис', type: 'energy', difficulty: 4 },
            { name: 'Военный конфликт', type: 'military', difficulty: 5 },
            { name: 'Киберугроза', type: 'cyber', difficulty: 3 },
            { name: 'Продовольственный кризис', type: 'economic', difficulty: 4 }
        ];

        // Навигация
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId + '-page').classList.add('active');
            
            document.querySelectorAll('.nav-links a').forEach(link => {
                link.classList.remove('active');
            });
            document.querySelector(`[data-page="${pageId}"]`).classList.add('active');
            
            currentPage = pageId;
            
            if (pageId === 'countries') loadCountries();
            if (pageId === 'scenarios') loadScenarios();
            if (pageId === 'game' && selectedCountry && selectedScenario) loadGame();
            else if (pageId === 'game') showNotification('Сначала выберите страну и сценарий!');
        }

        // Загрузка стран
        function loadCountries() {
            const grid = document.getElementById('countries-list');
            grid.innerHTML = '';
            countries.forEach(country => {
                const card = document.createElement('div');
                card.className = 'country-card' + (selectedCountry === country.name ? ' selected' : '');
                card.innerHTML = `
                    <div class="country-flag">${country.flag}</div>
                    <h3>${country.name}</h3>
                    <div class="stat-item">Военная мощь: ${country.power}%</div>
                    <div class="stat-item">Экономика: ${country.economy}%</div>
                `;
                card.onclick = () => selectCountry(country.name);
                grid.appendChild(card);
            });
        }

        // Загрузка сценариев
        function loadScenarios() {
            const list = document.getElementById('scenarios-list');
            list.innerHTML = '';
            scenarios.forEach((scenario, index) => {
                const card = document.createElement('div');
                card.className = 'crisis-card';
                card.innerHTML = `
                    <span class="crisis-type">${scenario.type}</span>
                    <h3>${scenario.name}</h3>
                    <div style="color: #ffd700;">${'★'.repeat(scenario.difficulty)}</div>
                `;
                card.onclick = () => selectScenario(index);
                list.appendChild(card);
            });
        }

        // Выбор страны
        function selectCountry(country) {
            selectedCountry = country;
            loadCountries();
            showNotification(`Выбрана страна: ${country}`);
        }

        // Выбор сценария
        function selectScenario(index) {
            selectedScenario = scenarios[index];
            showNotification(`Выбран сценарий: ${selectedScenario.name}`);
            showPage('game');
        }

        // Загрузка игры
        function loadGame() {
            document.getElementById('game-stats').innerHTML = `
                <div class="stat-item">ВВП: <span>$1.2 трлн</span></div>
                <div class="progress-bar"><div class="progress-fill" style="width:70%"></div></div>
                <div class="stat-item">Стабильность: <span>65%</span></div>
                <div class="progress-bar"><div class="progress-fill" style="width:65%"></div></div>
            `;
            
            document.getElementById('crisis-display').innerHTML = `
                <h3>${selectedScenario.name}</h3>
                <p>Требуется ваше решение!</p>
            `;
            
            document.getElementById('decisions-list').innerHTML = `
                <button class="decision-btn" onclick="makeDecision('diplomacy')">🤝 Дипломатические переговоры</button>
                <button class="decision-btn" onclick="makeDecision('military')">⚔️ Военное вмешательство</button>
                <button class="decision-btn" onclick="makeDecision('economic')">💰 Экономические санкции</button>
            `;
            
            document.getElementById('advisor').innerHTML = '<i class="fas fa-robot"></i> ИИ-советник: Рекомендую дипломатический путь';
            
            document.getElementById('team-chat').innerHTML = `
                <div class="message">США: Предлагаю совместные действия</div>
                <div class="message">РФ: Нужны гарантии безопасности</div>
            `;
        }

        // Принятие решения
        function makeDecision(type) {
            let message = '';
            switch(type) {
                case 'diplomacy': message = 'Вы начали переговоры. Напряжённость снижается на 10%'; break;
                case 'military': message = 'Вы ввели войска. Влияние +15, но стабильность -8'; break;
                case 'economic': message = 'Санкции введены. Экономика -5%, международное влияние +10'; break;
            }
            showNotification(message);
        }

        // Регистрация и вход
        function showRegister() {
            document.getElementById('registerModal').classList.add('active');
        }

        function showLogin() {
            document.getElementById('loginModal').classList.add('active');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
        }

        function register() {
            const name = document.getElementById('regName').value;
            if (name) {
                isLoggedIn = true;
                document.querySelector('.auth-buttons').innerHTML = `<span style="color: #ffd700;">${name}</span>`;
                closeModal('registerModal');
                showNotification('Регистрация успешна! Добро пожаловать!');
            }
        }

        function login() {
            const name = document.getElementById('loginName').value;
            if (name) {
                isLoggedIn = true;
                document.querySelector('.auth-buttons').innerHTML = `<span style="color: #ffd700;">${name}</span>`;
                closeModal('loginModal');
                showNotification('Вход выполнен успешно!');
            }
        }

        // Уведомления
        function showNotification(text) {
            const notif = document.getElementById('notification');
            notif.textContent = text;
            notif.classList.add('show');
            setTimeout(() => notif.classList.remove('show'), 3000);
        }

        // Дополнительные функции
        function startModule(module) {
            showNotification('Модуль обучения запущен!');
        }

        function selectCountryAndStart() {
            if (selectedCountry) {
                showPage('scenarios');
            } else {
                showNotification('Сначала выберите страну!');
            }
        }

        function showProfile() {
            if (isLoggedIn) {
                showNotification('Профиль пользователя');
            } else {
                showLogin();
            }
        }

        // Инициализация
        window.onload = function() {
            loadCountries();
            loadScenarios();
        };
    </script>
</body>
</html>
