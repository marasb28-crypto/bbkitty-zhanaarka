
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BB Kitty zhanaarka — Магазин подгузников</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Montserrat', sans-serif; margin: 0; padding: 0; background: #f0f4f8; color: #333; }
    header { background: #4CAF50; color: white; padding: 20px; text-align: center; }
    header h1 { margin: 0; font-size: 28px; }
    nav { margin-top: 10px; }
    nav a { color: white; text-decoration: none; margin: 0 10px; font-weight: 600; }
    nav a:hover { text-decoration: underline; }

    .products { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; padding: 20px; }
    .product { background: white; padding: 15px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); text-align: center; }
    .product img { max-width: 100%; height: auto; border-radius: 8px; }
    .product h3 { margin: 10px 0 5px; font-size: 18px; }
    .product p { margin: 5px 0; color: #666; }

    .btn { display: inline-block; margin-top: 10px; padding: 10px 15px; background: #4CAF50; color: white; border: none; border-radius: 8px; cursor: pointer; font-weight: 600; }
    .btn:hover { background: #45a049; }

    #cart { position: fixed; right: 20px; top: 20px; background: white; padding: 15px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.2); width: 280px; }
    #cart h2 { font-size: 18px; margin: 0 0 10px; text-align: center; }
    #cart ul { list-style: none; padding: 0; margin: 0; max-height: 200px; overflow-y: auto; }
    #cart li { font-size: 14px; margin-bottom: 5px; border-bottom: 1px solid #eee; padding-bottom: 3px; }
    #checkout { margin-top: 10px; width: 100%; }

    section { padding: 30px 20px; margin: 20px; border-radius: 12px; background: white; box-shadow: 0 4px 10px rgba(0,0,0,0.05); }
    section h2 { margin-top: 0; font-size: 22px; color: #4CAF50; }
    footer { background: #333; color: white; text-align: center; padding: 15px; margin-top: 20px; }
  </style>
</head>
<body>
  <header>
    <h1>BB Kitty zhanaarka</h1>
    <nav>
      <a href="#catalog">Каталог</a>
      <a href="#about">О нас</a>
      <a href="#contacts">Контакты</a>
    </nav>
  </header>

  <section id="catalog">
    <h2>Каталог товаров</h2>
    <div class="products">
      <div class="product">
        <img src="https://via.placeholder.com/220x160" alt="Подгузники BBkitty" />
        <h3>BBkitty</h3>
        <p>Цена: NB (до 5 кг), 32шт</p>
        <p>Цена: 4500 ₸</p>
        <button class="btn" onclick="addToCart('BBkitty', 4500)">В корзину</button>
      </div>

      <div class="product">
        <img src="https://via.placeholder.com/220x160" alt="Подгузники Yokosun" />
        <h3>Yokosun</h3>
        <p>Цена: 3777 ₸</p>
        <button class="btn" onclick="addToCart('Yokosun', 3777)">В корзину</button>
      </div>

      <div class="product">
        <img src="https://via.placeholder.com/220x160" alt="Подгузники Mello" />
        <h3>Mello</h3>
        <p>Цена: 6666 ₸</p>
        <button class="btn" onclick="addToCart('Mello', 5555)">В корзину</button>
      </div>
    </div>
  </section>

  <section id="about">
    <h2>О нас</h2>
    <p>Мы — онлайн-магазин детских товаров. В нашем ассортименте: подгузники, салфетки, средства ухода и игрушки. Мы предлагаем только проверенные бренды: <strong>Mama Znaet, BBkitty, Yokosun, Mello, Sabiko</strong>. Доставка по Жанаарке бесплатно.</p>
  </section>

  <section id="contacts">
    <h2>Контакты</h2>
    <p>📞 Телефон: +7 747 961 31 29</p>
    <p>💬 WhatsApp: <a href="https://wa.me/77019962042" target="_blank">Написать нам</a></p>
  </section>

  <footer>
    <p>© 2025 BB Kitty zhanaarka. Все права защищены.</p>
  </footer>

  <div id="cart">
    <h2>Корзина</h2>
    <ul id="cart-items"></ul>
    <p><strong>Итого: <span id="total">0</span> ₸</strong></p>
    <button id="checkout" class="btn" onclick="checkout()">Оформить заказ</button>
  </div>

  <script>
    let cart = [];

    function addToCart(product, price) {
      cart.push({ product, price });
      renderCart();
    }

    function renderCart() {
      const cartItems = document.getElementById('cart-items');
      const total = document.getElementById('total');
      cartItems.innerHTML = '';
      let sum = 0;
      cart.forEach(item => {
        const li = document.createElement('li');
        li.textContent = item.product + ' - ' + item.price + ' ₸';
        cartItems.appendChild(li);
        sum += item.price;
      });
      total.textContent = sum;
    }

    function checkout() {
      if (cart.length === 0) {
        alert('Корзина пуста!');
        return;
      }
      let message = 'Здравствуйте! Хочу заказать:%0A';
      cart.forEach(item => {
        message += '- ' + item.product + ' (' + item.price + ' ₸)%0A';
      });
      let total = cart.reduce((sum, item) => sum + item.price, 0);
      message += 'Итого: ' + total + ' ₸';

      // Вставь сюда свой номер WhatsApp (в формате 77001234567)
      window.open('https://wa.me/77019962042?text=' + message, '_blank');
    }
  </script>
</body>
</html>
