# sneha-uncle
Bill genarate
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cement & Steel Bill</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      padding: 20px;
    }

    .container {
      max-width: 1000px;
      margin: 0 auto;
      background: white;
      border-radius: 20px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.1);
      overflow: hidden;
    }

    .header {
      background: linear-gradient(135deg, #2c3e50, #3498db);
      color: white;
      padding: 30px;
      text-align: center;
    }

    .header h1 {
      font-size: 2.5em;
      margin-bottom: 10px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }

    .header p {
      opacity: 0.9;
      font-size: 1.1em;
    }

    .content {
      padding: 30px;
    }

    .form-section {
      background: #f8f9fa;
      padding: 25px;
      border-radius: 15px;
      margin-bottom: 25px;
      border: 1px solid #e9ecef;
    }

    .form-section h3 {
      color: #2c3e50;
      margin-bottom: 20px;
      font-size: 1.3em;
      display: flex;
      align-items: center;
    }

    .form-section h3:before {
      content: "📋";
      margin-right: 10px;
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
      margin-bottom: 20px;
    }

    .form-group {
      display: flex;
      flex-direction: column;
    }

    label {
      font-weight: 600;
      margin-bottom: 5px;
      color: #495057;
    }

    input, select, textarea {
      padding: 12px 15px;
      border: 2px solid #e9ecef;
      border-radius: 8px;
      font-size: 16px;
      transition: all 0.3s ease;
      background: white;
    }

    textarea {
      resize: vertical;
      min-height: 80px;
    }

    input:focus, select:focus, textarea:focus {
      outline: none;
      border-color: #3498db;
      box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
    }

    .btn {
      background: linear-gradient(135deg, #3498db, #2980b9);
      color: white;
      border: none;
      padding: 12px 25px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      font-weight: 600;
      transition: all 0.3s ease;
      margin: 5px;
      min-width: 140px;
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
    }

    .btn-success {
      background: linear-gradient(135deg, #27ae60, #2ecc71);
    }

    .btn-info {
      background: linear-gradient(135deg, #17a2b8, #20c997);
    }

    .btn-warning {
      background: linear-gradient(135deg, #f39c12, #e67e22);
    }

    .btn-danger {
      background: linear-gradient(135deg, #e74c3c, #c0392b);
    }

    .button-group {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin: 20px 0;
    }

    .table-container {
      overflow-x: auto;
      margin: 20px 0;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }

    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
    }

    th {
      background: linear-gradient(135deg, #34495e, #2c3e50);
      color: white;
      padding: 15px;
      text-align: center;
      font-weight: 600;
    }

    td {
      padding: 12px 15px;
      text-align: center;
      border-bottom: 1px solid #eee;
    }

    tbody tr:hover {
      background-color: #f8f9fa;
    }

    .delete-btn {
      background: #e74c3c;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 12px;
    }

    .delete-btn:hover {
      background: #c0392b;
    }

    .summary {
      background: linear-gradient(135deg, #ecf0f1, #bdc3c7);
      padding: 25px;
      border-radius: 15px;
      margin-top: 25px;
      text-align: right;
    }

    .summary p {
      margin: 8px 0;
      font-size: 1.1em;
    }

    .summary .grand-total {
      font-size: 1.4em;
      font-weight: bold;
      color: #2c3e50;
      border-top: 2px solid #3498db;
      padding-top: 15px;
      margin-top: 15px;
    }

    .amount-in-words {
      background: #e8f4f8;
      padding: 15px;
      border-radius: 8px;
      margin-top: 15px;
      text-align: left;
      font-style: italic;
      color: #2c3e50;
    }

    .empty-state {
      text-align: center;
      padding: 40px;
      color: #6c757d;
      font-style: italic;
    }

    .print-only {
      display: none;
    }

    @media (max-width: 768px) {
      .form-grid {
        grid-template-columns: 1fr;
      }
      
      .button-group {
        flex-direction: column;
        align-items: center;
      }
      
      .btn {
        width: 200px;
        margin: 5px 0;
      }
    }

    @media print {
      body {
        background: white;
        padding: 0;
        font-size: 12px;
      }
      
      .container {
        box-shadow: none;
        border-radius: 0;
        max-width: none;
      }
      
      .form-section, .button-group {
        display: none;
      }
      
      .header {
        background: #2c3e50 !important;
        -webkit-print-color-adjust: exact;
        padding: 20px;
      }

      .print-only {
        display: block;
      }

      .no-print {
        display: none;
      }

      .shop-details {
        background: #f8f9fa;
        padding: 15px;
        border: 2px solid #2c3e50;
        margin-bottom: 20px;
      }

      .bill-header {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
        border-bottom: 2px solid #333;
        padding-bottom: 10px;
      }

      table {
        font-size: 11px;
      }

      th, td {
        padding: 8px 5px;
      }

      .summary {
        background: none;
        border: 1px solid #333;
        font-size: 12px;
      }
    }

    .toast {
      position: fixed;
      top: 20px;
      right: 20px;
      background: #27ae60;
      color: white;
      padding: 15px 20px;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      z-index: 1000;
      transform: translateX(400px);
      transition: transform 0.3s ease;
    }

    .toast.show {
      transform: translateX(0);
    }

    .toast.error {
      background: #e74c3c;
    }

    .shop-details {
      background: #f0f8ff;
      padding: 20px;
      border-radius: 10px;
      margin-bottom: 20px;
      border-left: 4px solid #3498db;
    }

    .shop-details h4 {
      color: #2c3e50;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>🏗️ Cement & Steel Bill</h1>
      <p>Professional Billing System for Construction Materials</p>
    </div>

    <div class="content">
      <!-- Shop Details Section -->
      <div class="form-section no-print">
        <h3>Shop Details</h3>
        <div class="form-grid">
          <div class="form-group">
            <label for="shopName">Shop Name</label>
            <input type="text" id="shopName" placeholder="Enter shop name" value="ABC Cement & Steel Mart">
          </div>
          <div class="form-group">
            <label for="shopGST">Shop GST Number</label>
            <input type="text" id="shopGST" placeholder="Enter GST number" value="29ABCDE1234F1Z5">
          </div>
          <div class="form-group">
            <label for="shopPhone">Phone Number</label>
            <input type="text" id="shopPhone" placeholder="Enter phone number" value="+91 98765 43210">
          </div>
          <div class="form-group">
            <label for="shopEmail">Email</label>
            <input type="email" id="shopEmail" placeholder="Enter email" value="info@abccement.com">
          </div>
        </div>
        <div class="form-group">
          <label for="shopAddress">Shop Address</label>
          <textarea id="shopAddress" placeholder="Enter complete shop address">123 Industrial Area, Sector 25
Bangalore, Karnataka - 560001
India</textarea>
        </div>
      </div>

      <!-- Shop Details Display for Print -->
      <div class="shop-details print-only">
        <div style="text-align: center; margin-bottom: 20px;">
          <h2 id="printShopName" style="margin: 0; color: #2c3e50;">ABC Cement & Steel Mart</h2>
          <p id="printShopAddress" style="margin: 5px 0;">123 Industrial Area, Sector 25, Bangalore, Karnataka - 560001, India</p>
          <p style="margin: 5px 0;">
            <strong>GST:</strong> <span id="printShopGST">29ABCDE1234F1Z5</span> | 
            <strong>Phone:</strong> <span id="printShopPhone">+91 98765 43210</span> | 
            <strong>Email:</strong> <span id="printShopEmail">info@abccement.com</span>
          </p>
        </div>
      </div>

      <div class="form-section no-print">
        <h3>Bill Information</h3>
        <div class="form-grid">
          <div class="form-group">
            <label for="customerName">Customer Name</label>
            <input type="text" id="customerName" placeholder="Enter customer name">
          </div>
          <div class="form-group">
            <label for="customerPhone">Customer Phone</label>
            <input type="text" id="customerPhone" placeholder="Enter customer phone">
          </div>
          <div class="form-group">
            <label for="billDate">Bill Date</label>
            <input type="date" id="billDate">
          </div>
          <div class="form-group">
            <label for="billNo">Bill Number</label>
            <input type="text" id="billNo" placeholder="Auto-generated" readonly>
          </div>
        </div>
        <div class="form-group">
          <label for="customerAddress">Customer Address</label>
          <textarea id="customerAddress" placeholder="Enter customer address (optional)"></textarea>
        </div>
      </div>

      <!-- Bill Header for Print -->
      <div class="bill-header print-only">
        <div>
          <strong>Bill To:</strong><br>
          <span id="printCustomerName">Walk-in Customer</span><br>
          <span id="printCustomerPhone"></span><br>
          <span id="printCustomerAddress"></span>
        </div>
        <div style="text-align: right;">
          <strong>Bill No:</strong> <span id="printBillNo">BILL-1001</span><br>
          <strong>Date:</strong> <span id="printBillDate"></span><br>
        </div>
      </div>

      <div class="form-section no-print">
        <h3>Add Item</h3>
        <div class="form-grid">
          <div class="form-group">
            <label for="itemName">Item Name</label>
            <input type="text" id="itemName" placeholder="e.g., Cement, Steel Rod">
          </div>
          <div class="form-group">
            <label for="qty">Quantity</label>
            <input type="number" id="qty" placeholder="Enter quantity" min="0.01" step="0.01">
          </div>
          <div class="form-group">
            <label for="rate">Rate per Unit (₹)</label>
            <input type="number" id="rate" placeholder="Enter rate" min="0.01" step="0.01">
          </div>
          <div class="form-group">
            <label for="hsn">HSN Code</label>
            <input type="text" id="hsn" placeholder="Enter HSN code">
          </div>
          <div class="form-group">
            <label for="gst">GST (%)</label>
            <select id="gst">
              <option value="0">0%</option>
              <option value="5">5%</option>
              <option value="12">12%</option>
              <option value="18" selected>18%</option>
              <option value="28">28%</option>
            </select>
          </div>
        </div>
        <div class="button-group">
          <button class="btn btn-success" onclick="addItem()">➕ Add Item</button>
        </div>
      </div>

      <div class="table-container">
        <table id="billTable">
          <thead>
            <tr>
              <th>S.No</th>
              <th>Item</th>
              <th>HSN</th>
              <th>Qty</th>
              <th>Rate (₹)</th>
              <th>Amount (₹)</th>
              <th>GST %</th>
              <th>GST Amount (₹)</th>
              <th>Total (₹)</th>
              <th class="no-print">Action</th>
            </tr>
          </thead>
          <tbody></tbody>
        </table>
        <div id="emptyState" class="empty-state">
          No items added yet. Add your first item above! 📦
        </div>
      </div>

      <div class="summary">
        <p id="subtotal">Subtotal: ₹0.00</p>
        <p id="totalGST">Total GST: ₹0.00</p>
        <p id="grandTotal" class="grand-total">Grand Total: ₹0.00</p>
        <div class="amount-in-words">
          <strong>Amount in Words:</strong> <span id="amountInWords">Zero Rupees Only</span>
        </div>
      </div>

      <div class="button-group no-print">
        <button class="btn btn-info" onclick="printBill()">🖨️ Print</button>
        <button class="btn btn-warning" onclick="downloadPDF()">📄 Download PDF</button>
        <button class="btn btn-danger" onclick="clearAll()">🗑️ Clear All</button>
      </div>
    </div>
  </div>

  <script>
    let subtotal = 0;
    let totalGST = 0;
    let billNoCounter = 1001;
    let items = [];

    // Initialize
    document.getElementById('billDate').value = new Date().toISOString().split('T')[0];
    document.getElementById('billNo').value = "BILL-" + billNoCounter;

    function showToast(message, isError = false) {
      const toast = document.createElement('div');
      toast.className = `toast ${isError ? 'error' : ''}`;
      toast.textContent = message;
      document.body.appendChild(toast);
      
      setTimeout(() => toast.classList.add('show'), 100);
      setTimeout(() => {
        toast.classList.remove('show');
        setTimeout(() => document.body.removeChild(toast), 300);
      }, 3000);
    }

    function numberToWords(num) {
      if (num === 0) return "Zero";
      
      const ones = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"];
      const teens = ["Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"];
      const tens = ["", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"];
      const thousands = ["", "Thousand", "Lakh", "Crore"];

      function convertGroup(n) {
        let result = "";
        if (n >= 100) {
          result += ones[Math.floor(n / 100)] + " Hundred ";
          n %= 100;
        }
        if (n >= 20) {
          result += tens[Math.floor(n / 10)] + " ";
          n %= 10;
        } else if (n >= 10) {
          result += teens[n - 10] + " ";
          return result;
        }
        if (n > 0) {
          result += ones[n] + " ";
        }
        return result;
      }

      const integerPart = Math.floor(num);
      const decimalPart = Math.round((num - integerPart) * 100);

      if (integerPart === 0) {
        return decimalPart > 0 ? `Zero Rupees and ${convertGroup(decimalPart).trim()} Paise Only` : "Zero Rupees Only";
      }

      let result = "";
      let groupIndex = 0;

      // Handle Indian numbering system
      if (integerPart >= 10000000) { // Crores
        const crores = Math.floor(integerPart / 10000000);
        result += convertGroup(crores) + "Crore ";
        integerPart %= 10000000;
      }
      
      if (integerPart >= 100000) { // Lakhs
        const lakhs = Math.floor(integerPart / 100000);
        result += convertGroup(lakhs) + "Lakh ";
        integerPart %= 100000;
      }
      
      if (integerPart >= 1000) { // Thousands
        const thousands = Math.floor(integerPart / 1000);
        result += convertGroup(thousands) + "Thousand ";
        integerPart %= 1000;
      }
      
      if (integerPart > 0) {
        result += convertGroup(integerPart);
      }

      result = result.trim() + " Rupees";
      
      if (decimalPart > 0) {
        result += " and " + convertGroup(decimalPart).trim() + " Paise";
      }
      
      return result + " Only";
    }

    function addItem() {
      const item = document.getElementById("itemName").value.trim();
      const qty = parseFloat(document.getElementById("qty").value);
      const rate = parseFloat(document.getElementById("rate").value);
      const hsn = document.getElementById("hsn").value.trim();
      const gstPercent = parseFloat(document.getElementById("gst").value);

      if (!item) {
        showToast("Please enter item name", true);
        return;
      }
      if (!qty || qty <= 0) {
        showToast("Please enter valid quantity", true);
        return;
      }
      if (!rate || rate <= 0) {
        showToast("Please enter valid rate", true);
        return;
      }

      const itemTotal = qty * rate;
      const gstAmount = (itemTotal * gstPercent) / 100;
      const finalTotal = itemTotal + gstAmount;

      const newItem = {
        id: Date.now(),
        name: item,
        hsn: hsn,
        qty: qty,
        rate: rate,
        gstPercent: gstPercent,
        itemTotal: itemTotal,
        gstAmount: gstAmount,
        finalTotal: finalTotal
      };

      items.push(newItem);
      updateTable();
      clearItemFields();
      showToast("Item added successfully!");
    }

    function updateTable() {
      const tbody = document.querySelector("#billTable tbody");
      const emptyState = document.getElementById("emptyState");
      
      tbody.innerHTML = "";
      
      if (items.length === 0) {
        emptyState.style.display = "block";
        document.querySelector(".table-container table").style.display = "none";
      } else {
        emptyState.style.display = "none";
        document.querySelector(".table-container table").style.display = "table";
        
        items.forEach((item, index) => {
          const row = tbody.insertRow();
          row.insertCell(0).innerText = index + 1;
          row.insertCell(1).innerText = item.name;
          row.insertCell(2).innerText = item.hsn;
          row.insertCell(3).innerText = item.qty;
          row.insertCell(4).innerText = `₹${item.rate.toFixed(2)}`;
          row.insertCell(5).innerText = `₹${item.itemTotal.toFixed(2)}`;
          row.insertCell(6).innerText = `${item.gstPercent}%`;
          row.insertCell(7).innerText = `₹${item.gstAmount.toFixed(2)}`;
          row.insertCell(8).innerText = `₹${item.finalTotal.toFixed(2)}`;
          const actionCell = row.insertCell(9);
          actionCell.className = "no-print";
          actionCell.innerHTML = `<button class="delete-btn" onclick="deleteItem(${item.id})">Delete</button>`;
        });
      }
      
      updateSummary();
    }

    function deleteItem(id) {
      items = items.filter(item => item.id !== id);
      updateTable();
      showToast("Item deleted successfully!");
    }

    function updateSummary() {
      subtotal = items.reduce((sum, item) => sum + item.itemTotal, 0);
      totalGST = items.reduce((sum, item) => sum + item.gstAmount, 0);
      const grandTotal = subtotal + totalGST;

      document.getElementById("subtotal").innerText = `Subtotal: ₹${subtotal.toFixed(2)}`;
      document.getElementById("totalGST").innerText = `Total GST: ₹${totalGST.toFixed(2)}`;
      document.getElementById("grandTotal").innerText = `Grand Total: ₹${grandTotal.toFixed(2)}`;
      
      // Update amount in words
      document.getElementById("amountInWords").innerText = numberToWords(grandTotal);
    }

    function clearItemFields() {
      document.getElementById("itemName").value = "";
      document.getElementById("qty").value = "";
      document.getElementById("rate").value = "";
      document.getElementById("hsn").value = "";
      document.getElementById("gst").value = "18";
    }

    function clearAll() {
      if (confirm("Are you sure you want to clear all items?")) {
        items = [];
        updateTable();
        billNoCounter++;
        document.getElementById('billNo').value = "BILL-" + billNoCounter;
        showToast("All items cleared!");
      }
    }

    function updatePrintElements() {
      // Update shop details for print
      document.getElementById("printShopName").innerText = document.getElementById("shopName").value || "Shop Name";
      document.getElementById("printShopAddress").innerText = document.getElementById("shopAddress").value || "Shop Address";
      document.getElementById("printShopGST").innerText = document.getElementById("shopGST").value || "GST Number";
      document.getElementById("printShopPhone").innerText = document.getElementById("shopPhone").value || "Phone";
      document.getElementById("printShopEmail").innerText = document.getElementById("shopEmail").value || "Email";
      
      // Update customer details for print
      document.getElementById("printCustomerName").innerText = document.getElementById("customerName").value || "Walk-in Customer";
      document.getElementById("printCustomerPhone").innerText = document.getElementById("customerPhone").value ? "Phone: " + document.getElementById("customerPhone").value : "";
      document.getElementById("printCustomerAddress").innerText = document.getElementById("customerAddress").value || "";
      document.getElementById("printBillNo").innerText = document.getElementById("billNo").value || "N/A";
      document.getElementById("printBillDate").innerText = document.getElementById("billDate").value || new Date().toISOString().split('T')[0];
    }

    function printBill() {
      if (items.length === 0) {
        showToast("Please add items before printing", true);
        return;
      }
      updatePrintElements();
      window.print();
    }

    async function downloadPDF() {
      if (items.length === 0) {
        showToast("Please add items before downloading PDF", true);
        return;
      }

      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      const shopName = document.getElementById("shopName").value || "Shop Name";
      const shopAddress = document.getElementById("shopAddress").value || "Shop Address";
      const shopGST = document.getElementById("shopGST").value || "GST Number";
      const shopPhone = document.getElementById("shopPhone").value || "Phone";
      const shopEmail = document.getElementById("shopEmail").value || "Email";

      const customerName = document.getElementById("customerName").value || "Walk-in Customer";
      const customerPhone = document.getElementById("customerPhone").value || "";
      const customerAddress = document.getElementById("customerAddress").value || "";
      const date = document.getElementById("billDate").value || new Date().toISOString().split('T')[0];
      const billNo = document.getElementById("billNo").value || "N/A";

      // Shop Header
      doc.setFontSize(18);
      doc.setFont(undefined, 'bold');
      doc.text(shopName, 105, 20, { align: 'center' });
      
      doc.setFontSize(10);
      doc.setFont(undefined, 'normal');
      doc.text(shopAddress, 105, 30, { align: 'center' });
      doc.text(`GST: ${shopGST} | Phone: ${shopPhone} | Email: ${shopEmail}`, 105, 38, { align: 'center' });
      
      // Line separator
      doc.line(15, 45, 195, 45);

      // Bill details
      doc.setFontSize(12);
      doc.setFont(undefined, 'bold');
      doc.text("BILL DETAILS", 15, 55);
      
      doc.setFont(undefined, 'normal');
      doc.text(`Bill No: ${billNo}`, 15, 65);
      doc.text(`Date: ${date}`, 15, 72);
      
      doc.text(`Customer: ${customerName}`, 105, 65);
      if (customerPhone) doc.text(`Phone: ${customerPhone}`, 105, 72);
      if (customerAddress) {
        const addressLines = customerAddress.split('\n');
        addressLines.forEach((line, index) => {
          doc.text(line, 105, 79 + (index * 7));
        });
      }

      // Table header
      let y = 95;
      doc.setFont(undefined, 'bold');
      doc.setFontSize(9);
      doc.text("S.No", 15, y);
      doc.text("Item", 30, y);
      doc.text("HSN", 70, y);
      doc.text("Qty", 85, y);
      doc.text("Rate", 100, y);
      doc.text("Amount", 118, y);
      doc.text("GST%", 140, y);
      doc.text("GST Amt", 155, y);
      doc.text("Total", 175, y);

      // Line under header
      doc.line(15, y + 3, 195, y + 3);

      // Table content
      y += 10;
      doc.setFont(undefined, 'normal');
      items.forEach((item, index) => {
        doc.text((index + 1).toString(), 15, y);
        doc.text(item.name.substring(0, 12), 30, y);
        doc.text(item.hsn, 70, y);
        doc.text(item.qty.toString(), 85, y);
        doc.text(`₹${item.rate.toFixed(2)}`, 100, y);
        doc.text(`₹${item.itemTotal.toFixed(2)}`, 118, y);
        doc.text(`${item.gstPercent}%`, 140, y);
        doc.text(`₹${item.gstAmount.toFixed(2)}`, 155, y);
        doc.text(`₹${item.finalTotal.toFixed(2)}`, 175, y);
        y += 8;
      });

      // Summary
      y += 10;
      doc.line(15, y, 195, y);
      y += 10;
      
      doc.setFont(undefined, 'bold');
      doc.text(`Subtotal: ₹${subtotal.toFixed(2)}`, 140, y);
      y += 8;
      doc.text(`Total GST: ₹${totalGST.toFixed(2)}`, 140, y);
      y += 8;
      doc.setFontSize(12);
      doc.text(`Grand Total: ₹${(subtotal + totalGST).toFixed(2)}`, 140, y);

      // Amount in words
      y += 15;
      doc.setFontSize(10);
      doc.setFont(undefined, 'normal');
      doc.text("Amount in Words:", 15, y);
      y += 7;
      const amountWords = numberToWords(subtotal + totalGST);
      const wordsLines = doc.splitTextToSize(amountWords, 180);
      doc.text(wordsLines, 15, y);

      // Footer
      y += (wordsLines.length * 7) + 15;
      doc.setFontSize(8);
      doc.text("Thank you for your business!", 105, y, { align: 'center' });

      doc.save(`${billNo}_cement_steel_bill.pdf`);
      showToast("PDF downloaded successfully!");
    }

    // Enter key support for adding items
    document.addEventListener('keydown', function(event) {
      if (event.key === 'Enter' && event.target.closest('.form-section')) {
        const inputs = ['itemName', 'qty', 'rate', 'hsn'];
        const currentInput = event.target.id;
        const currentIndex = inputs.indexOf(currentInput);
        
        if (currentIndex !== -1 && currentIndex < inputs.length - 1) {
          document.getElementById(inputs[currentIndex + 1]).focus();
        } else if (currentInput === 'hsn' || currentInput === 'gst') {
          addItem();
        }
      }
    });

    // Initialize table
    updateTable();
  </script>
</body>
</html>
