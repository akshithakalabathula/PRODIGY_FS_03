<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Local Store E-commerce</title>
  <style>
    body {
      font-family: sans-serif;
      margin: 0;
      padding: 0;
    }

    header {
      background-color: #333;
      color: white;
      padding: 10px;
      text-align: center;
    }

    .products {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      padding: 10px;
    }

    .product {
      border: 1px solid #ddd;
      margin: 5px;
      padding: 15px;
      width: 200px;
      text-align: center;
    }

    .product img {
      max-width: 100%;
      height: auto;
    }

    .cart {
      position: fixed;
      top: 10px;
      right: 10px;
      border: 1px solid #ccc;
      padding: 10px;
      background-color: white;
    }

    .cart ul {
      list-style: none;
      padding: 0;
    }

    .filters {
      padding: 10px;
      background-color: #f0f0f0;
      text-align: center;
    }
  </style>
</head>
<body>
  <header>
    <h1>Local Store</h1>
  </header>

  <div class="filters">
    <select id="sort">
      <option value="">Sort By</option>
      <option value="price-asc">Price: Low to High</option>
      <option value="price-desc">Price: High to Low</option>
    </select>
    <select id="category">
      <option value="">Category</option>
      <option value="electronics">Electronics</option>
      <option value="clothing">Clothing</option>
      <option value="books">Books</option>
      <option value="Footwear">Footwear</option>
      <option value="Facials">Facials</option>
      <option value="Hair Care">Hair Care</option>
      <option value="jewllery">jewllery</option>
      <option value="watches">watches</option>
      <option value="sarees">sarees</option>
    </select>
  </div>

  <div class="products" id="product-list">
    </div>

  <div class="cart">
    <h2>Shopping Cart</h2>
    <ul id="cart-items">
      </ul>
    <p>Total: $<span id="cart-total">0</span></p>
    <button onclick="checkout()">Checkout</button>
  </div>

  <script>
    const products = [
      { id: 1, name: 'Laptop', price: 800, image: 'laptop.jpeg', category: 'electronics', description: 'Powerful laptop' },
      { id: 2, name: 'T-Shirt', price: 20, image: 't-shirts.jpeg', category: 'clothing', description: 'Cotton t-shirt' },
      { id: 3, name: 'Book', price: 15, image: 'books.jpeg', category: 'books', description: 'Novel' },
      { id: 4, name: 'Headphones', price: 100, image: 'headphones.jpeg', category: 'electronics', description: 'Noise cancelling headphones' },
      { id: 5, name: 'Jeans', price: 50, image: 'jeans.jpeg', category: 'clothing', description: 'Denim jeans' },
      { id: 6, name: 'Cookbook', price: 25, image: 'cookbook.jpeg', category: 'books', description: 'Delicious recipes' },
      { id: 7, name: 'Facials', price: 30, image: 'facials.jpeg', category: 'Facials', description: 'Chemical free products' },
      { id: 8, name: 'Hair Care', price: 30, image: 'Hair Care.jpeg', category: 'Hair Care', description: 'Natural herbs' },
      { id: 9, name: 'jewllery', price: 35, image: 'jewllery.jpeg', category: 'jewllery', description: 'Gold coated' },
      { id: 10, name: 'watches', price: 40, image: 'watches.jpeg', category: 'watches', description: 'Classy watches' },
      { id: 11, name: 'sarees', price: 25, image: 'sarees.jpeg', category: 'sarees', description: 'Elegant sarees' },
      { id: 12, name: 'Earrings', price: 20, image: 'earrings.jpeg', category: 'jewllery', description: 'Elegant jewllery' },
      { id: 13, name: 'anklets', price: 25, image: 'anklets.jpeg', category: 'jewllery', description: 'simple anklets' },
      { id: 14, name: 'banarasi sarees', price: 25, image: 'banarasi sarees.jpeg', category: 'sarees', description: 'Elegant sarees' },
      { id: 15, name: 'shampoo', price: 25, image: 'shampoo.jpeg', category: 'Hair Care', description: 'Natural herbs' },
      { id: 16, name: 'shoes', price: 45, image: 'shoes.jpeg', category: 'Footwear', description: 'Stylish shoes' },
      { id: 17, name: 'jackets', price: 40, image: 'jackets.jpeg', category: 'clothing', description: 'Denim jackets' },

    ];

    let cart = [];

    function renderProducts(productList = products) {
      const productListDiv = document.getElementById('product-list');
      productListDiv.innerHTML = '';

      productList.forEach(product => {
        const productDiv = document.createElement('div');
        productDiv.classList.add('product');
        productDiv.innerHTML = `
          <img src="${product.image}" alt="${product.name}">
          <h3>${product.name}</h3>
          <p>${product.description}</p>
          <p>$${product.price}</p>
          <button onclick="addToCart(${product.id})">Add to Cart</button>
        `;
        productListDiv.appendChild(productDiv);
      });
    }

    function addToCart(productId) {
      const product = products.find(p => p.id === productId);
      if (product) {
        cart.push(product);
        renderCart();
      }
    }

    function renderCart() {
      const cartItemsList = document.getElementById('cart-items');
      const cartTotalSpan = document.getElementById('cart-total');
      cartItemsList.innerHTML = '';
      let total = 0;

      cart.forEach(item => {
        const cartItem = document.createElement('li');
        cartItem.textContent = `${item.name} - $${item.price}`;
        cartItemsList.appendChild(cartItem);
        total += item.price;
      });

      cartTotalSpan.textContent = total;
    }

    function checkout() {
      alert( ('Checkout functionality (not implemented).Total: $' + document.getElementById('cart-total').textContent));
      cart = [];
      renderCart();
    }

    function sortProducts(sortBy) {
      let sortedProducts = [...products];

      if (sortBy === 'price-asc') {
        sortedProducts.sort((a, b) => a.price - b.price);
      } else if (sortBy === 'price-desc') {
        sortedProducts.sort((a, b) => b.price - a.price);
      }
      renderProducts(sortedProducts);
    }

    function filterProducts(category) {
      let filteredProducts;
      if (category) {
        filteredProducts = products.filter(product => product.category === category);
      } else {
        filteredProducts = products;
      }
      renderProducts(filteredProducts);
    }

    document.getElementById('sort').addEventListener('change', (event) => {
      sortProducts(event.target.value);
    });

    document.getElementById('category').addEventListener('change', (event) => {
      filterProducts(event.target.value);
    });

    renderProducts();
    renderCart();

  </script>
</body>
