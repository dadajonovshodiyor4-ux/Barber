<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Fresh Ultra Pro Max</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@700&family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #030303;
            --accent: #1aff80;
            --card: rgba(255, 255, 255, 0.05);
            --border: rgba(255, 255, 255, 0.08);
            --text: #ffffff;
            --ease: cubic-bezier(0.2, 1, 0.3, 1);
        }

        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; margin: 0; padding: 0; }
        
        body { 
            background: var(--bg); color: var(--text); 
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-image: radial-gradient(circle at 50% 0%, #1a1a1a 0%, #030303 100%);
            min-height: 100vh;
        }

        /* HEADER */
        .header {
            padding: 15px 20px; display: flex; justify-content: space-between; align-items: center;
            background: rgba(3, 3, 3, 0.8); backdrop-filter: blur(20px);
            position: sticky; top: 0; z-index: 100; border-bottom: 1px solid var(--border);
            gap: 10px;
        }
        .logo { font-family: 'Space Grotesk', sans-serif; font-size: 18px; color: var(--accent); flex-shrink: 0; }
        
        .demo-note {
            color: #ff4d4d;
            font-size: 8px;
            font-weight: 800;
            text-align: center;
            line-height: 1.1;
            text-transform: uppercase;
            animation: pulse 2s infinite;
            max-width: 140px;
        }

        @keyframes pulse {
            0% { opacity: 0.5; }
            50% { opacity: 1; }
            100% { opacity: 0.5; }
        }

        .lang-pills { display: flex; gap: 4px; background: #111; padding: 4px; border-radius: 12px; flex-shrink: 0; }
        .l-btn { border: none; background: none; color: #555; font-size: 9px; font-weight: 800; padding: 6px 8px; border-radius: 8px; cursor: pointer; }
        .l-btn.active { background: #fff; color: #000; }

        /* CATEGORIES */
        .cat-scroll { display: flex; overflow-x: auto; gap: 8px; padding: 15px 20px; scrollbar-width: none; }
        .cat-chip {
            background: var(--card); padding: 10px 18px; border-radius: 15px;
            white-space: nowrap; font-size: 12px; font-weight: 600; color: #777;
            border: 1px solid var(--border); transition: 0.3s;
        }
        .cat-chip.active { background: var(--accent); color: #000; border-color: var(--accent); }

        /* GRID */
        .prod-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; padding: 0 15px 120px; }
        .prod-card { 
            background: var(--card); border-radius: 24px; padding: 15px;
            border: 1px solid var(--border); position: relative;
            display: flex; flex-direction: column; transition: 0.4s var(--ease);
        }
        .prod-icon { font-size: 32px; margin-bottom: 25px; }
        .prod-name { font-weight: 700; font-size: 14px; margin-bottom: 4px; height: 34px; overflow: hidden; }
        .prod-price { color: var(--accent); font-family: 'Space Grotesk'; font-size: 13px; }
        .prod-vol { color: #555; font-size: 10px; margin-top: 2px; }
        
        .add-btn {
            position: absolute; bottom: 15px; right: 15px;
            width: 32px; height: 32px; background: #fff; color: #000;
            border-radius: 10px; display: flex; align-items: center; justify-content: center;
            font-weight: 800; font-size: 18px; cursor: pointer;
        }

        /* CART BAR */
        .cart-bar {
            position: fixed; bottom: 20px; left: 15px; right: 15px;
            background: #fff; color: #000; padding: 18px 25px;
            border-radius: 20px; display: flex; justify-content: space-between; align-items: center;
            font-weight: 800; box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            z-index: 500; transition: 0.5s var(--ease);
            transform: translateY(150%);
        }
        .cart-bar.visible { transform: translateY(0); }

        /* MODAL */
        .cart-overlay {
            position: fixed; inset: 0; background: rgba(0,0,0,0.9);
            backdrop-filter: blur(10px); z-index: 1000; display: none;
            justify-content: flex-end; flex-direction: column;
        }
        .cart-sheet {
            background: #0f0f0f; border-top-left-radius: 30px; border-top-right-radius: 30px;
            padding: 25px; max-height: 80vh; display: flex; flex-direction: column;
        }

        .item-row {
            display: flex; justify-content: space-between; align-items: center;
            padding: 12px 0; border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        .qty-ctrl { display: flex; align-items: center; gap: 12px; background: #1a1a1a; padding: 6px 12px; border-radius: 12px; }
        .qty-btn { background: none; border: none; color: #fff; font-size: 18px; width: 20px; cursor: pointer; }

        .order-btn {
            background: var(--accent); border: none; width: 100%; padding: 18px;
            border-radius: 15px; font-weight: 800; font-size: 16px; margin-top: 15px;
        }
    </style>
</head>
<body>

    <div class="header">
        <div class="logo">FRESH.U</div>
        <div class="demo-note"><h2>ESLATIB O'TAMIZ BU WEBAPP NAMUNA SIFATIDA QILINGAN!</h2></div>
        <div class="lang-pills">
            <button class="l-btn active" onclick="setLang('uz', this)">UZ</button>
            <button class="l-btn" onclick="setLang('ru', this)">RU</button>
            <button class="l-btn" onclick="setLang('en', this)">EN</button>
        </div>
    </div>

    <div class="cat-scroll" id="cat-list"></div>
    <div class="prod-grid" id="main-grid"></div>

    <div class="cart-bar" id="cart-bar" onclick="toggleCart()">
        <span id="ui-count">0 mahsulot</span>
        <span id="ui-total">0 so'm</span>
    </div>

    <div class="cart-overlay" id="cart-modal">
        <div class="cart-sheet">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
                <h2 id="ui-cart-title" style="font-family:'Space Grotesk'">Savatcha</h2>
                <div onclick="toggleCart()" style="font-size:32px; opacity:0.5; cursor:pointer;">&times;</div>
            </div>
            <div id="cart-items-list" style="flex-grow:1; overflow-y:auto;"></div>
            <div style="padding-top:15px;">
                <div style="display:flex; justify-content:space-between; font-size:18px; font-weight:800; margin-bottom:10px;">
                    <span id="ui-total-text" style="opacity:0.5">Jami:</span>
                    <span id="final-price" style="color:var(--accent)">0 so'm</span>
                </div>
                <button class="order-btn" id="ui-order-btn" onclick="sendOrder()">TASDIQLASH</button>
            </div>
        </div>
    </div>

    <script>
        const tg = window.Telegram.WebApp;
        tg.expand();

        const UI = {
            uz: { items: "mahsulot", cats: ["Hammasi", "Mevalar", "Sutli", "Go'sht", "Ichimlik"], cart: "Savatcha", total: "Jami:", order: "TASDIQLASH", confirm: "Buyurtmani tasdiqlaysizmi?" },
            ru: { items: "товаров", cats: ["Все", "Фрукты", "Молочное", "Мясо", "Напитки"], cart: "Корзина", total: "Итого:", order: "ПОДТВЕРДИТЬ", confirm: "Подтвердить заказ?" },
            en: { items: "items", cats: ["All", "Fruits", "Dairy", "Meat", "Drinks"], cart: "Cart", total: "Total:", order: "CONFIRM", confirm: "Confirm order?" }
        };

        const DATA = [
            { id: 1, n: {uz:"Qizil Olma", ru:"Красное яблоко", en:"Red Apple"}, p: 12000, c: 1, i: "🍎", v: "1 kg" },
            { id: 2, n: {uz:"Banan Premium", ru:"Банан", en:"Banana"}, p: 23000, c: 1, i: "🍌", v: "1 kg" },
            { id: 3, n: {uz:"Shirin Uzum", ru:"Виноград", en:"Grapes"}, p: 33000, c: 1, i: "🍇", v: "1 kg" },
            { id: 4, n: {uz:"Nok", ru:"Груша", en:"Pear"}, p: 20000, c: 1, i: "🍐", v: "1 kg" },
            { id: 5, n: {uz:"Qulupnay", ru:"Клубника", en:"Strawberry"}, p: 45000, c: 1, i: "🍓", v: "500 gr" },
            { id: 6, n: {uz:"Ananas", ru:"Ананас", en:"Pineapple"}, p: 19000, c: 1, i: "🍍", v: "1 dona" },
            { id: 7, n: {uz:"Kivi", ru:"Киви", en:"Kiwi"}, p: 32000, c: 1, i: "🥝", v: "1 kg" },
            { id: 8, n: {uz:"Tabiiy Sut", ru:"Молоко", en:"Milk"}, p: 13000, c: 2, i: "🥛", v: "1 L" },
            { id: 9, n: {uz:"Pishloq", ru:"Сыр", en:"Cheese"}, p: 65000, c: 2, i: "🧀", v: "500 gr" },
            { id: 10, n: {uz:"Qaymoq", ru:"Сливки", en:"Cream"}, p: 12000, c: 2, i: "🥣", v: "250 gr" },
            { id: 11, n: {uz:"Qatiq", ru:"Кефир", en:"Kefir"}, p: 6000, c: 2, i: "🍶", v: "1 L" },
            { id: 12, n: {uz:"Sariyog'", ru:"Сливочное масло", en:"Butter"}, p: 22000, c: 2, i: "🧈", v: "200 gr" },
            { id: 13, n: {uz:"Tvorog", ru:"Творог", en:"Curd"}, p: 18000, c: 2, i: "🍚", v: "400 gr" },
            { id: 14, n: {uz:"Mol go'shti", ru:"Говядина", en:"Beef"}, p: 100000, c: 3, i: "🥩", v: "1 kg" },
            { id: 15, n: {uz:"Qo'y go'shti", ru:"Баранина", en:"Lamb"}, p: 120000, c: 3, i: "🍖", v: "1 kg" },
            { id: 16, n: {uz:"Tovuq go'shti", ru:"Курица", en:"Chicken"}, p: 38000, c: 3, i: "🍗", v: "1 kg" },
            { id: 17, n: {uz:"Kurka go'shti", ru:"Индейка", en:"Turkey"}, p: 75000, c: 3, i: "🦃", v: "1 kg" },
            { id: 18, n: {uz:"Farsh", ru:"Фарш", en:"Minced Meat"}, p: 55000, c: 3, i: "🍱", v: "1 kg" },
            { id: 19, n: {uz:"Baliq", ru:"Рыба", en:"Fish"}, p: 50000, c: 3, i: "🐟", v: "1 kg" },
            { id: 20, n: {uz:"Pepsi 1.5 L", ru:"Пепси 1.5 л", en:"Pepsi 1.5 L"}, p: 14000, c: 4, i: "🥤", v: "1.5 L" },
            { id: 21, n: {uz:"Coca-Cola 1.5 L", ru:"Кока-кола 1.5 л", en:"Coca-Cola 1.5 L"}, p: 13000, c: 4, i: "🥤", v: "1.5 L" },
            { id: 22, n: {uz:"Olma sharbati", ru:"Яблочный сок", en:"Apple Juice"}, p: 15000, c: 4, i: "🧃", v: "1 L" },
            { id: 23, n: {uz:"Gazlangan suv", ru:"Газировка", en:"Sparkling Water"}, p: 5000, c: 4, i: "🫧", v: "1.5 L" },
            { id: 24, n: {uz:"Kofe Arabica", ru:"Кофе", en:"Coffee"}, p: 45000, c: 4, i: "☕", v: "250 gr" },
            { id: 25, n: {uz:"Ko'k choy", ru:"Зеленый чай", en:"Green Tea"}, p: 8000, c: 4, i: "🍵", v: "1 quti" },
            { id: 26, n: {uz:"Energetik", ru:"Энергетик", en:"Energy Drink"}, p: 10000, c: 4, i: "⚡", v: "540"} ,
        ];

        let lang = 'uz', cat = 0, cart = {};

        function setLang(l, b) {
            lang = l;
            document.querySelectorAll('.l-btn').forEach(x => x.classList.remove('active'));
            b.classList.add('active');
            render(); updateTexts(); refreshCartUI();
        }

        function updateTexts() {
            document.getElementById('ui-cart-title').innerText = UI[lang].cart;
            document.getElementById('ui-total-text').innerText = UI[lang].total;
            document.getElementById('ui-order-btn').innerText = UI[lang].order;
        }

        function filterCat(i) { cat = i; render(); tg.HapticFeedback.impactOccurred('light'); }

        function render() {
            document.getElementById('cat-list').innerHTML = UI[lang].cats.map((c, i) => `
                <div class="cat-chip ${cat === i ? 'active' : ''}" onclick="filterCat(${i})">${c}</div>
            `).join('');

            const filtered = cat === 0 ? DATA : DATA.filter(x => x.c === cat);
            document.getElementById('main-grid').innerHTML = filtered.map(p => `
                <div class="prod-card">
                    <span class="prod-icon">${p.i}</span>
                    <div class="prod-name">${p.n[lang]}</div>
                    <div class="prod-price">${p.p.toLocaleString()} so'm</div>
                    <div class="prod-vol">${p.v}</div>
                    <div class="add-btn" onclick="updateCart(${p.id}, 1)">+</div>
                </div>
            `).join('');
        }

        function updateCart(id, delta) {
            if (!cart[id] && delta > 0) cart[id] = { ...DATA.find(x => x.id === id), q: 0 };
            if (cart[id]) {
                cart[id].q += delta;
                if (cart[id].q <= 0) delete cart[id];
            }
            refreshCartUI();
            tg.HapticFeedback.impactOccurred('medium');
        }

        function refreshCartUI() {
            const items = Object.values(cart);
            let count = 0, total = 0;
            
            document.getElementById('cart-items-list').innerHTML = items.length === 0 ? 
                `<div style="text-align:center; opacity:0.3; padding:40px 0;">Savatcha bo'sh</div>` :
                items.map(i => {
                    count += i.q; total += i.p * i.q;
                    return `
                        <div class="item-row">
                            <div><b>${i.n[lang]}</b><br><small style="opacity:0.5">${i.p.toLocaleString()} / ${i.v}</small></div>
                            <div class="qty-ctrl">
                                <button class="qty-btn" onclick="updateCart(${i.id}, -1)">−</button>
                                <span>${i.q}</span>
                                <button class="qty-btn" onclick="updateCart(${i.id}, 1)">+</button>
                            </div>
                        </div>
                    `;
                }).join('');

            const bar = document.getElementById('cart-bar');
            bar.classList.toggle('visible', count > 0);
            document.getElementById('ui-count').innerText = `${count} ${UI[lang].items}`;
            document.getElementById('ui-total').innerText = total.toLocaleString() + " so'm";
            document.getElementById('final-price').innerText = total.toLocaleString() + " so'm";
        }

        function toggleCart() {
            const m = document.getElementById('cart-modal');
            m.style.display = m.style.display === 'flex' ? 'none' : 'flex';
        }

        function sendOrder() {
            const items = Object.values(cart);
            if (items.length === 0) return;
            tg.showConfirm(UI[lang].confirm, (ok) => {
                if (ok) {
                    let msg = "🛒 BUYURTMA:\n\n";
                    items.forEach(i => msg += `▪️ ${i.n[lang]} (${i.v}) x ${i.q} = ${(i.p*i.q).toLocaleString()} so'm\n`);
                    tg.sendData(msg);
                    tg.close();
                }
            });
        }

        render();
        updateTexts();
    </script>
</body>
</html>
