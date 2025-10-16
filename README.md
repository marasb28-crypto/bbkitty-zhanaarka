<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Корзина — Магазин детских товаров</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f8f9fa;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #00bcd4;
      color: white;
      padding: 15px;
      text-align: center;
    }
    header a {
      color: white;
      text-decoration: none;
      margin: 0 10px;
      font-weight: bold;
    }
    .container {
      max-width: 900px;
      margin: 20px auto;
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      border-bottom: 1px solid #ddd;
      padding: 10px;
      text-align: center;
    }
    th {
      background-color: #00bcd4;
      color: white;
    }
    button {
      background-color: #00bcd4;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0097a7;
    }
    .total {
      text-align: right;
      margin-top: 20px;
      font-size: 18px;
      font-weight: bold;
    }
    .back-button {
      display: inline-block;
      background-color: #4caf50;
      color: white;
      padding: 10px 15px;
      border-radius: 5px;
      text-decoration: none;
      margin-top: 20px;
    }
    .back-button:hover {
      background-color: #43a047;
    }
  </style>
</head>
<body>
  <header>
    <h1>Корзина</h1>
    <nav>
      <a href="index.html">Каталог</a>
      <a href="cart.html">Корзина</a>
    </nav>
  </header>

  <div class="container">
    <table id="cartTable">
      <thead>
        <tr>
          <th>Товар</th>
          <th>Цена</th>
          <th>Количество</th>
          <th>Сумма</th>
          <th>Действие</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>

    <div class="total" id="total">Итого: 0 ₸</div>
    <br>
    <button onclick="checkout()">Оформить заказ через WhatsApp</button>
    <br><br>
    <a href="index.html" class="back-button">← Назад в каталог</a>
  </div>

  <script>
    function loadCart() {
      const cart = JSON.parse(localStorage.getItem('cart')) || [];
      const tbody = document.querySelector('#cartTable tbody');
      tbody.innerHTML = '';
      let total = 0;

      cart.forEach((item, index) => {
        const row = document.createElement('tr');
        const subtotal = item.price * item.qty;
        total += subtotal;

        row.innerHTML = `
          <td>${item.name}</td>
          <td>${item.price} ₸</td>
          <td>
            <input type="number" value="${item.qty}" min="1" style="width:60px" onchange="updateQty(${index}, this.value)">
          </td>
          <td>${subtotal} ₸</td>
          <td><button onclick="removeItem(${index})">Удалить</button></td>
        `;
        tbody.appendChild(row);
      });

      document.getElementById('total').textContent = `Итого: ${total} ₸`;
    }

    function updateQty(index, qty) {
      let cart = JSON.parse(localStorage.getItem('cart')) || [];
      cart[index].qty = parseInt(qty);
      localStorage.setItem('cart', JSON.stringify(cart));
      loadCart();
    }

    function removeItem(index) {
      let cart = JSON.parse(localStorage.getItem('cart')) || [];
      cart.splice(index, 1);
      localStorage.setItem('cart', JSON.stringify(cart));
      loadCart();
    }

    function checkout() {
      const cart = JSON.parse(localStorage.getItem('cart')) || [];
      if (cart.length === 0) {
        alert('Корзина пуста');
        return;
      }
      let message = 'Здравствуйте! Хочу заказать:\n';
      cart.forEach(item => {
        message += `${item.name} — ${item.qty} шт = ${item.price * item.qty} ₸\n`;
      });
      const total = cart.reduce((sum, i) => sum + i.price * i.qty, 0);
      message += `\nИтого: ${total} ₸`;
      const phone = '7700XXXXXXX'; // ← замени на свой номер
      const url = `https://wa.me/${phone}?text=${encodeURIComponent(message)}`;
      window.open(url, '_blank');
    }

    loadCart();
  </script>
</body>
</html>
