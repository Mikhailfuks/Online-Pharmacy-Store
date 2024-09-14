<!DOCTYPE html>
<html>
<head>
  <title>Online Pharmacy Store</title>
</head>
<body>
  <h1>Welcome to Our Pharmacy</h1>

  <div id="medicine-catalog">
    <!-- Medicine items will be displayed here -->
  </div>

  <h2>Your Cart</h2>
  <div id="cart-items">
    <!-- Cart items will be displayed here -->
  </div>

  <button onclick="placeOrder()">Place Order</button>

  <script src="script.js"></script>
</body>
</html>

// Sample medicine data (replace with your actual data)
const medicines = [
  { id: 1, name: "Paracetamol", price: 5.99, description: "Pain reliever" },
  { id: 2, name: "Ibuprofen", price: 7.99, description: "Anti-inflammatory" },
  { id: 3,  name: "Antihistamine", price: 4.99, description: "Allergy relief" },
  // Add more medicines here...
];

// Cart array to store selected medicines
const cart = [];

// Function to display the medicine catalog
function displayMedicineCatalog() {
  const catalogContainer = document.getElementById('medicine-catalog');
  catalogContainer.innerHTML = ''; // Clear previous catalog

  medicines.forEach(medicine => {
    const medicineItem = document.createElement('div');
    medicineItem.innerHTML = 
      <h3>${medicine.name}</h3>
      <p>${medicine.description}</p>
      <p>Price: $${medicine.price.toFixed(2)}</p>
      <button onclick="addToCart(${medicine.id})">Add to Cart</button>
    ;
    catalogContainer.appendChild(medicineItem);
  });
}

// Function to add a medicine to the cart
function addToCart(medicineId) {
  const medicine = medicines.find(med => med.id === medicineId);
  cart.push(medicine);
  updateCart();
  console.log(${medicine.name} added to cart);
}

// Function to update the cart display
function updateCart() {
  const cartItemsContainer = document.getElementById('cart-items');
  cartItemsContainer.innerHTML = ''; // Clear previous cart

  if (cart.length === 0) {
    cartItemsContainer.innerHTML = '<p>Your cart is empty</p>';
    return;
  }

  let totalPrice = 0;
  cart.forEach(medicine => {
    const cartItem = document.createElement('div');
    cartItem.innerHTML = 
      <h3>${medicine.name}</h3>
      <p>Price: $${medicine.price.toFixed(2)}</p>
    ;
    cartItemsContainer.appendChild(cartItem);
    totalPrice += medicine.price;
  });

  const totalPriceElement = document.createElement('p');
  totalPriceElement.textContent = Total: $${totalPrice.toFixed(2)};
  cartItemsContainer.appendChild(totalPriceElement);
}

// Function to simulate placing an order (in real-world, send to a server)
function placeOrder() {
  if (cart.length === 0) {
    alert('Your cart is empty!');
    return;
  }

  console.log('Order placed!');
  console.log('Medicines:', cart);
  cart.length = 0; // Clear the cart
  updateCart();
}

// Display the initial medicine catalog
displayMedicineCatalog();
