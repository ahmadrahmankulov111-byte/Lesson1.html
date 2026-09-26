<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ахмат Group — Погода</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: url('https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1920&q=80') no-repeat center center fixed;
            background-size: cover;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .glass-card {
            background: rgba(30, 41, 59, 0.55);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
            width: 100%;
            max-width: 360px;
            text-align: center;
            box-sizing: border-box;
            color: #fff;
            position: relative;
        }
        .logo-area img {
            width: 45px !important;
            height: 45px !important;
            max-width: 45px !important;
            max-height: 45px !important;
            object-fit: contain;
            display: block;
            margin: 0 auto 5px auto;
        }
        .brand-title {
            font-size: 14px;
            font-weight: bold;
            color: #38bdf8;
            letter-spacing: 1px;
        }
        .brand-sub {
            font-size: 12px;
            color: #cbd5e1;
            margin-bottom: 20px;
        }
        .control-row {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            position: relative;
        }
        
        .custom-select {
            flex: 1;
            background: rgba(15, 23, 42, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 10px;
            color: #fff;
            padding: 12px;
            font-size: 14px;
            text-align: left;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            user-select: none;
        }
        .dropdown-list {
            position: absolute;
            top: 50px;
            left: 0;
            right: 75px;
            background: rgba(15, 23, 42, 0.95);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.6);
            z-index: 100;
            max-height: 200px;
            overflow-y: auto;
            text-align: left;
            display: none;
        }
        .dropdown-list.show {
            display: block;
        }
        .opt-category {
            padding: 8px 12px;
            font-size: 12px;
            color: #38bdf8;
            font-weight: bold;
            background: rgba(30, 41, 59, 0.8);
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        .opt-item {
            padding: 10px 15px;
            font-size: 14px;
            color: #fff;
            cursor: pointer;
            transition: background 0.2s;
        }
        .opt-item:hover {
            background: rgba(56, 189, 248, 0.2);
        }

        .btn-sm {
            padding: 12px 18px;
            background: #2563eb;
            border: none;
            border-radius: 10px;
            color: #fff;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.2s;
        }
        .btn-sm:hover {
            background: #1d4ed8;
        }
        .temp-display {
            font-size: 48px;
            font-weight: bold;
            color: #38bdf8;
            margin: 15px 0 25px 0;
        }
        .info-row {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 14px;
            color: #cbd5e1;
            text-align: left;
        }
        .info-row:last-of-type {
            border-bottom: none;
            margin-bottom: 25px;
        }
        .logout-link {
            background: none;
            border: none;
            color: #94a3b8;
            font-size: 13px;
            cursor: pointer;
            text-decoration: underline;
            margin-top: 10px;
            display: inline-block;
        }
        .logout-link:hover {
            color: #fff;
        }
    </style>
</head>
<body>
    <div class="glass-card">
        <div class="logo-area">
            <img src="logo.svg" alt="Логотип">
            <div class="brand-title">AXMAT GROUP</div>
            <div class="brand-sub" id="usernameDisplay">@raxmankulowww</div>
        </div>

        <div class="control-row">
            <div class="custom-select" onclick="toggleDropdown()">
                <span id="selectedCityText">Ташкент</span>
                <span>▼</span>
            </div>

            <div class="dropdown-list" id="dropdownMenu">
                <div class="opt-category">🇺🇿 Узбекистан</div>
                <div class="opt-item" onclick="selectCity('Ташкент')">Ташкент</div>
                <div class="opt-item" onclick="selectCity('Самарканд')">Самарканд</div>
                <div class="opt-item" onclick="selectCity('Бухара')">Бухара</div>
                <div class="opt-item" onclick="selectCity('Фергана')">Фергана</div>
                
                <div class="opt-category">🇰🇬 Кыргызстан</div>
                <div class="opt-item" onclick="selectCity('Бишкек')">Бишкек</div>
                <div class="opt-item" onclick="selectCity('Ош')">Ош</div>
                <div class="opt-item" onclick="selectCity('Жалал-Абад')">Жалал-Абад</div>
            </div>

            <button class="btn-sm" onclick="updateWeather()">Смотреть</button>
        </div>

        <div class="temp-display" id="tempVal">Загрузка...</div>

        <div class="info-row">
            <span>💧 Влажность</span>
            <span id="humidityVal">--</span>
        </div>
        <div class="info-row">
            <span>💨 Ветер</span>
            <span id="windVal">--</span>
        </div>

        <a href="index.html" class="logout-link">← Выйти</a>
    </div>

    <script>
        // Координаты городов для реального API погоды
        const cityCoords = {
            'Ташкент': { lat: 41.2995, lon: 69.2401 },
            'Самарканд': { lat: 39.6542, lon: 66.9597 },
            'Бухара': { lat: 39.7747, lon: 64.4286 },
            'Фергана': { lat: 40.3842, lon: 71.7842 },
            'Бишкек': { lat: 42.8746, lon: 74.5698 },
            'Ош': { lat: 40.5282, lon: 72.7985 },
            'Жалал-Абад': { lat: 40.9333, lon: 73.0000 }
        };

        function toggleDropdown() {
            const menu = document.getElementById('dropdownMenu');
            menu.classList.toggle('show');
        }

        function selectCity(cityName) {
            document.getElementById('selectedCityText').innerText = cityName;
            document.getElementById('dropdownMenu').classList.remove('show');
            updateWeather(); // Автоматически обновлять погоду при смене города
        }

        window.onclick = function(event) {
            if (!event.target.closest('.control-row')) {
                document.getElementById('dropdownMenu').classList.remove('show');
            }
        }

        // Функция запроса реальной погоды через интернет
        async function updateWeather() {
            const cityName = document.getElementById('selectedCityText').innerText;
            const coords = cityCoords[cityName];
            if (!coords) return;

            document.getElementById('tempVal').innerText = '...';

            try {
                const response = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${coords.lat}&longitude=${coords.lon}&current=temperature_2m,relative_humidity_2m,wind_speed_10m`);
                const data = await response.json();
                
                const temp = Math.round(data.current.temperature_2m);
                const humidity = data.current.relative_humidity_2m;
                const wind = data.current.wind_speed_10m;

                document.getElementById('tempVal').innerText = (temp > 0 ? '+' : '') + temp + ' °C';
                document.getElementById('humidityVal').innerText = humidity + '%';
                document.getElementById('windVal').innerText = wind + ' м/с';
            } catch (error) {
                document.getElementById('tempVal').innerText = 'Ошибка';
                console.error(error);
            }
        }

        // Автоматически подгружаем погоду для Ташкента при открытии страницы
        window.onload = function() {
            // Если сохранено имя на странице входа, покажем его
            const savedUser = localStorage.getItem('axmat_user');
            if (savedUser) {
                document.getElementById('usernameDisplay').innerText = savedUser;
            }
            updateWeather();
        };
    </script>
</body>
</html>
