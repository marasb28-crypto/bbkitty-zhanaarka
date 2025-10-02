<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Магазин подгузников</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #f9f9f9; }
    header { background: #4CAF50; color: white; padding: 15px; text-align: center; font-size: 24px; }
    .products { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; padding: 20px; }
    .product { background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); text-align: center; }
    .product img { max-width: 100%; height: auto; border-radius: 8px; }
    .product h3 { margin: 10px 0 5px; font-size: 18px; }
    .product p { margin: 5px 0; }
    .btn { display: inline-block; margin-top: 10px; padding: 8px 12px; background: #4CAF50; color: white; border: none; border-radius: 5px; cursor: pointer; }
    .btn:hover { background: #45a049; }
    #cart { position: fixed; right: 20px; top: 20px; background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.2); width: 250px; }
    #cart h2 { font-size: 18px; margin: 0 0 10px; }
    #cart ul { list-style: none; padding: 0; margin: 0; max-height: 200px; overflow-y: auto; }
    #cart li { font-size: 14px; margin-bottom: 5px; }
    #checkout { margin-top: 10px; width: 100%; }
  </style>
</head>
<body>
  <header>Онлайн-магазин подгузников</header>

  <div class="products">
    <div class="product">
      <img src="https://via.placeholder.com/200x150" alt="Подгузники BBkitty" />
      <h3>BBkitty</h3>
      <p>Цена: 2500 ₸</p>
      <button class="btn" onclick="addToCart('BBkitty', 2500)">В корзину</button>
    </div>

    <div class="product">
      <img src="https://via.placeholder.com/200x150" alt="Подгузники Yokosun" />
      <h3>Yokosun</h3>
      <p>Цена: 3000 ₸</p>
      <button class="btn" onclick="addToCart('Yokosun', 3000)">В корзину</button>
    </div>

    <div class="product">
      <img src="https://via.placeholder.com/200x150" alt="Подгузники Mello" />
      <h3>Mello</h3>
      <p>Цена: 2800 ₸</p>
      <button class="btn" onclick="addToCart('Mello', 2800)">В корзину</button>
    </div>
  </div>

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
