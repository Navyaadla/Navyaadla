- 👋 Hi, I’m @Navyaadla
Here is the code for creating Grocery inventory Management system there is UI , Backend javascript and css
These two arrays, addItemInventory and getItemsInventory, are used to store information about added items. addItemInventory keeps track of items added via the "Add Item" form (POST), and getItemsInventory stores items when the "Get Items" button is clicked (GET).
Rendering Functions:
javascript
Copy code
// Function to render added items table
function renderAddItemTable() {
  const addItemBody = document.getElementById('addItemBody');
  addItemBody.innerHTML = ''; // Clear the table body

  addItemInventory.forEach(item => {
    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${item.name}</td>
      <td>${item.quantity}</td>
    `;
    addItemBody.appendChild(row);
  });
}

// Function to render items when "Get Items" button is clicked (GET)
function renderGetItemsTable() {
  const getItemsBody = document.getElementById('getItemsBody');
  getItemsBody.innerHTML = ''; // Clear the table body

  getItemsInventory.forEach(item => {
    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${item.name}</td>
      <td>${item.quantity}</td>
    `;
    getItemsBody.appendChild(row);
  });
}
These functions (renderAddItemTable and renderGetItemsTable) are responsible for rendering the tables that display added items and items retrieved when the "Get Items" button is clicked, respectively. They dynamically create table rows and cells based on the content of the corresponding inventories.
Event Listeners:
javascript
Copy code
// Function to handle form submission and add item to inventory (POST)
document.getElementById('addItemForm').addEventListener('submit', function(event) {
  event.preventDefault();

  const itemName = document.getElementById('itemName').value;
  const quantity = parseInt(document.getElementById('quantity').value);

  if (itemName && quantity) {
    const newItem = { name: itemName, quantity: quantity };
    addItemInventory.push(newItem);
    renderAddItemTable(); // Render added items table
    document.getElementById('addItemForm').reset(); // Reset form fields
  } else {
    alert('Please fill in all fields');
  }
});

// Function to handle displaying items when "Get Items" button is clicked (GET)
document.getElementById('getItemsBtn').addEventListener('click', function() {
  getItemsInventory = addItemInventory.slice(); // Copy added items to "Get Items" inventory
  renderGetItemsTable(); 
});
The first event listener is attached to the "Add Item" form. It prevents the default form submission behavior, extracts values from the form fields, creates a new item object, adds it to the addItemInventory, renders the updated table, and resets the form fields. If any field is missing, it displays an alert.

The second event listener is attached to the "Get Items" button. When clicked, it copies the contents of addItemInventory to getItemsInventory, renders the "Get Items" table, and sets the display property of the table to 'table', making it visible.
