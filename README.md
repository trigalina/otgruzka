<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GDMN Отгрузка - Умное управление складом</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            overflow-x: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            transition: opacity 0.3s;
        }

        .nav-links a:hover {
            opacity: 0.8;
        }

        .hero {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 120px 2rem 80px;
            text-align: center;
            margin-top: 60px;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg"><rect width="100" height="100" fill="none"/><path d="M0 50 Q 25 40, 50 50 T 100 50" stroke="rgba(255,255,255,0.1)" fill="none" stroke-width="2"/></svg>');
            opacity: 0.3;
        }

        .hero-content {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            animation: fadeInUp 1s ease;
        }

        .hero p {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            opacity: 0.95;
            animation: fadeInUp 1s ease 0.2s backwards;
        }

        .cta-button {
            display: inline-block;
            padding: 1rem 2.5rem;
            background: white;
            color: #667eea;
            text-decoration: none;
            border-radius: 50px;
            font-weight: bold;
            font-size: 1.1rem;
            transition: transform 0.3s, box-shadow 0.3s;
            animation: fadeInUp 1s ease 0.4s backwards;
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }

        .features {
            padding: 80px 2rem;
            background: #f8f9fa;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 3rem;
            color: #333;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }

        .feature-card {
            background: white;
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
        }

        .feature-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.15);
        }

        .feature-icon {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            margin-bottom: 1.5rem;
        }

        .feature-card h3 {
            font-size: 1.5rem;
            margin-bottom: 1rem;
            color: #333;
        }

        .feature-card p {
            color: #666;
            line-height: 1.8;
        }

        .advantages {
            padding: 80px 2rem;
            background: white;
        }

        .advantages-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .advantage-item {
            text-align: center;
            padding: 2rem;
            border-radius: 10px;
            transition: background 0.3s;
        }

        .advantage-item:hover {
            background: #f8f9fa;
        }

        .advantage-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
        }

        .advantage-item h4 {
            font-size: 1.3rem;
            margin-bottom: 0.5rem;
            color: #667eea;
        }

        .integration {
            padding: 80px 2rem;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            text-align: center;
        }

        .integration-logos {
            display: flex;
            justify-content: center;
            gap: 3rem;
            margin-top: 3rem;
            flex-wrap: wrap;
        }

        .integration-logo {
            background: white;
            padding: 1.5rem 2.5rem;
            border-radius: 10px;
            font-size: 1.5rem;
            font-weight: bold;
            color: #667eea;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .contact {
            padding: 80px 2rem;
            background: #f8f9fa;
            text-align: center;
        }

        .contact-info {
            display: flex;
            justify-content: center;
            gap: 3rem;
            margin-top: 3rem;
            flex-wrap: wrap;
        }

        .contact-item {
            background: white;
            padding: 2rem;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            min-width: 250px;
        }

        .contact-item-icon {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        .contact-item a {
            color: #667eea;
            text-decoration: none;
            font-weight: bold;
            font-size: 1.1rem;
        }

        .contact-item a:hover {
            text-decoration: underline;
        }

        .footer {
            background: #333;
            color: white;
            text-align: center;
            padding: 2rem;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2rem;
            }

            .hero p {
                font-size: 1.1rem;
            }

            .nav-links {
                display: none;
            }

            .section-title {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <nav class="nav-container">
            <div class="logo">
                📦 GDMN Отгрузка
            </div>
            <ul class="nav-links">
                <li><a href="#features">Возможности</a></li>
                <li><a href="#advantages">Преимущества</a></li>
                <li><a href="#integration">Интеграция</a></li>
                <li><a href="#contact">Контакты</a></li>
            </ul>
        </nav>
    </header>

    <section class="hero">
        <div class="hero-content">
            <h1>GDMN Отгрузка</h1>
            <p>Комплексное решение для оптимизации складских операций с адресным хранением</p>
            <a href="#contact" class="cta-button">Получить консультацию</a>
        </div>
    </section>

    <section id="features" class="features">
        <div class="container">
            <h2 class="section-title">Основные возможности</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <div class="feature-icon">🎯</div>
                    <h3>Адресное хранение</h3>
                    <p>Каждое место хранения имеет уникальный адрес (камера, ряд, ячейка). Точное определение местоположения товаров и предотвращение ошибок при перемещении.</p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">🔄</div>
                    <h3>Оформление перемещения</h3>
                    <p>Удобное оформление документов перемещения товаров с указанием конкретных адресов ячеек. Прозрачный и точный процесс управления запасами.</p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">📋</div>
                    <h3>Оформление отвеса</h3>
                    <p>Создание отвес-накладных при отгрузке товаров в магазины или клиентам. Работа как с предварительными заявками, так и без них.</p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">📊</div>
                    <h3>Инвентаризация</h3>
                    <p>Оформление инвентаризации прямо с мобильного устройства. Сканирование штрихкодов и регистрация фактического наличия на складе.</p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">📱</div>
                    <h3>Мобильность</h3>
                    <p>Создание документов складского движения (Приход, Возврат, Лаборатория) на мобильных устройствах. Экономия времени и упрощение процессов.</p>
                </div>

                <div class="feature-card">
                    <div class="feature-icon">🔌</div>
                    <h3>Оффлайн-режим</h3>
                    <p>Работа без подключения к интернету. Локальное сохранение данных с последующей синхронизацией после восстановления связи.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="advantages" class="advantages">
        <div class="container">
            <h2 class="section-title">Преимущества решения</h2>
            <div class="advantages-grid">
                <div class="advantage-item">
                    <div class="advantage-icon">⚡</div>
                    <h4>Скорость</h4>
                    <p>Ускорение складских операций в 3 раза</p>
                </div>

                <div class="advantage-item">
                    <div class="advantage-icon">✅</div>
                    <h4>Точность</h4>
                    <p>Минимизация ошибок при учете товаров</p>
                </div>

                <div class="advantage-item">
                    <div class="advantage-icon">💼</div>
                    <h4>Простота</h4>
                    <p>Интуитивный интерфейс, быстрое обучение</p>
                </div>

                <div class="advantage-item">
                    <div class="advantage-icon">🔐</div>
                    <h4>Контроль</h4>
                    <p>Веб-приложение для администрирования</p>
                </div>
            </div>
        </div>
    </section>

    <section id="integration" class="integration">
        <div class="container">
            <h2 class="section-title">Интеграция с ERP-системами</h2>
            <p style="font-size: 1.2rem; margin-bottom: 2rem;">Обмен актуальными данными и синхронизация с основной системой предприятия</p>
            <div class="integration-logos">
                <div class="integration-logo">Гедымин</div>
                <div class="integration-logo">SAP</div>
                <div class="integration-logo">1C</div>
            </div>
        </div>
    </section>

    <section id="contact" class="contact">
        <div class="container">
            <h2 class="section-title">Свяжитесь с нами</h2>
            <p style="font-size: 1.2rem; margin-bottom: 2rem;">Получите консультацию и узнайте больше о возможностях GDMN Отгрузка</p>
            <div class="contact-info">
                <div class="contact-item">
                    <div class="contact-item-icon">🌐</div>
                    <p>Веб-сайт</p>
                    <a href="http://www.gsbelarus.com" target="_blank">www.gsbelarus.com</a>
                </div>

                <div class="contact-item">
                    <div class="contact-item-icon">📞</div>
                    <p>Телефон</p>
                    <a href="tel:+375173791759">+375 17 379-17-59</a>
                </div>
            </div>
        </div>
    </section>

    <footer class="footer">
        <p>&copy; Golden Software </p>
  <p>&copy; 2026 Все права защищены.</p>
    </footer>

    <script>
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.feature-card, .advantage-item').forEach(el => {
            el.style.opacity = '0';
            el.style.transform = 'translateY(30px)';
            el.style.transition = 'opacity 0.6s, transform 0.6s';
            observer.observe(el);
        });
    </script>
</body>
</html>
