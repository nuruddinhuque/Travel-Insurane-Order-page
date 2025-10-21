https://nuruddinhuque.github.io/Travel-Insurane-Order-page/
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>NextSure Admin Dashboard</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<style>
:root {
  --dark-bg:#0f172a;--dark-card:#1e293b;--light-bg:#f4f7fb;--light-card:#fff;
  --accent:#3b82f6;--success:#10b981;--danger:#ef4444;--warn:#f59e0b;
}
html[data-theme='dark'] {--bg:var(--dark-bg);--card:var(--dark-card);--text:#f9fafb;}
html[data-theme='light']{--bg:var(--light-bg);--card:var(--light-card);--text:#111827;}
body {
  margin:0;font-family:Inter,system-ui;background:var(--bg);color:var(--text);
  transition:background 0.3s,color 0.3s;
}
.container{max-width:100%;margin:auto;padding:25px;}
.card{background:var(--card);border-radius:12px;padding:50px;margin-bottom:20px;box-shadow:0 3px 10px #ffffff; }
.btn{padding:8px 14px;border:none;border-radius:6px;cursor:pointer;font-weight:600;}
.btn.primary{background:var(--accent);color:#fff;}
.btn.ghost{background:transparent;color:var(--text);border:1px solid #ffffff68;}
.btn.danger{background:var(--danger);color:#fff;}
input,select{width:100%;padding:8px;border-radius:8px;border:1px solid #ccc;margin-bottom:6px;}
table{width:100%;border-collapse:collapse;font-size:14px;margin-top:10px;}
th,td{padding:8px;border-bottom:1px solid rgba(255,255,255,0.1);}
th{background:rgba(255,255,255,0.05);}
tr.pending{background:#ffffff;}
tr.processing{background:#3b83f64f;}
tr.underwriting{background:#de2d0ea0;}
tr.deleted{background:#7977774e;}
.statusSelect{padding:30px;border-radius:20px;text-align: left;}
.action-btns{display:flex;gap:6px;}
.login{max-width:400px;margin:100px auto;background:var(--card);padding:20px;border-radius:12px;text-align:center;}
.login input{margin:10px 0;}
.login h2{margin-bottom:20px;}
#ordersTable tbody{display:block;max-height:400px;overflow-y:auto;}
.btn {
  padding: 8px 14px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  margin-right: 5px;
}
.btn.primary {
  background: #3b82f6;
  color: white;
}
.modal {
  display: none;
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.5);
}
.modal-content {
  background: #fff;
  margin: 5% auto;
  padding: 20px;
  border-radius: 10px;
  width: 480px;
  max-height: 80vh;
  overflow-y: auto;
  box-shadow: 0 4px 15px rgba(0,0,0,0.3);
}
.modal-content h3 {
  margin-top: 0;
  text-align: center;
}
.close {
  float: right;
  font-size: 22px;
  cursor: pointer;
}
.edit-field {
  margin-bottom: 10px;
}
.edit-field label {
  font-weight: 600;
  display: block;
  margin-bottom: 5px;
}
.edit-field input, .edit-field select {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 6px;
}
.btn {
  padding: 8px 14px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  margin: 5px;
}
.btn.primary {
  background: #3b82f6;
  color: white;
}


</style>
</head>
<header>



</header>
<body>
  <a href="travel rate .html"><img src="NextSure logo New.png" width="120" alt="logo"></a> 

<button class="btn ghost" id="themeToggle" style="position:absolute;right:20px;top:20px;"> Dark</button>

<div id="loginBox" class="login">
  <h2>Admin Login</h2>
  <input id="user" type="text" placeholder="Username">
  <input id="pass" type="password" placeholder="Password">
  <button class="btn primary" onclick="login()">Login</button>
</div>

<div id="dashboard" style="display:none">
  <div class="container">
    <div style="display:flex;justify-content:space-between;align-items:center;">
      <h2>NextSure Admin Dashboard</h2>
      <div>
          <button class="btn ghost" onclick="logout()">Logout</button>
         
        </select>
      
      </div>
    </div>

    <div class="card">
      <h3>Notification Settings</h3>
      <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:10px;">
        <div><label>EmailJS Service ID</label><input id="emailjs_service"></div>
        <div><label>EmailJS Template ID</label><input id="emailjs_template"></div>
        <div><label>EmailJS User ID/Public Key</label><input id="emailjs_user"></div>
        <div><label>Admin Email (notify to)</label><input id="admin_email"></div>
        <div><label>SMS Webhook URL</label><input id="sms_webhook"></div>
      </div>
      <button class="btn primary" style="margin-top:10px" onclick="saveSettings()">Save Settings</button>
    </div>


<div style="display:flex;gap:20px;flex-wrap:wrap;"></div>

    <div class="card">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <h3>All Orders</h3>
        </div>

<!-- PDF Buttons Section -->
<div style="margin-bottom: 10px;">
  <button class="btn primary" onclick="downloadSelectedPDF()">📄 Download Selected (PDF)</button>
  <button class="btn" style="background:#16a34a;color:white;" onclick="generateInvoice()">🧾 Generate Invoice</button>
</div>




  <input type="date" id="startDate" style="padding:5px;border-radius:5px;">
  <input type="date" id="endDate" style="padding:5px;border-radius:5px;">
  <button class="btn primary" onclick="exportByDate()">📥 Export by Date</button>
</div>


      <input id="search" placeholder="Search..." oninput="renderTable()">
      <table id="ordersTable" width="100%" style="overflow-y:auto;display:block;">

        <thead>
          <tr>
           <th></th> <th>Date & Time</th><th></th><th>Order ID</th><th>Company</th><th></th><th></th><th>Plan</th><th></th><th></th><th>DOB</th><th>Age Band</th><th>Duration</th>
            <th>Destination</th><th>Occupation</th><th>Travel Date</th><th>Mobile</th>
            <th>Multiplier</th><th>Offer</th><th>Total</th><th>Status</th><th>Action</th>

          </tr>
        </thead>
        <tbody></tbody>
      </table>
      <p id="count" style="font-size:13px;color:gray;"></p>
    </div>
  </div>
</div>



<script>
 function exportByDate() {
  const startDateInput = document.getElementById('startDate').value;
  const endDateInput = document.getElementById('endDate').value;

  if (!startDateInput || !endDateInput) {
    alert("⚠️ Please select both start and end dates!");
    return;
  }

  // ইনপুটকে Date অবজেক্টে রূপান্তর
  const startDate = new Date(startDateInput + "T00:00:00");
  const endDate = new Date(endDateInput + "T23:59:59");

  const orders = JSON.parse(localStorage.getItem('orders') || '[]');

  // createdAt কে dd/mm/yyyy ফরম্যাট থেকে Date অবজেক্টে কনভার্ট করে তুলনা
  const filtered = orders.filter(o => {
    if (!o.createdAt) return false;

    let parts = o.createdAt.split(/[, ]+/); // "18/10/2025, 17:45:15" → ["18","10","2025","17:45:15"]
    let dateParts = parts[0].split('/');
    let day = parseInt(dateParts[0]);
    let month = parseInt(dateParts[1]) - 1;
    let year = parseInt(dateParts[2]);

    let orderDate = new Date(year, month, day);
    return orderDate >= startDate && orderDate <= endDate;
  });

  if (filtered.length === 0) {
    alert("❌ No orders found in this date range!");
    return;
  }

  // CSV তৈরি
  let csvContent = "data:text/csv;charset=utf-8,";
  csvContent += Object.keys(filtered[0]).join(",") + "\n";
  filtered.forEach(o => {
    csvContent += Object.values(o).map(v => `"${v}"`).join(",") + "\n";
  });

  // Excel (.csv) ফাইল ডাউনলোড
  const encodedUri = encodeURI(csvContent);
  const link = document.createElement("a");
  link.setAttribute("href", encodedUri);
  link.setAttribute("download", `Orders_${startDateInput}_to_${endDateInput}.csv`);
  document.body.appendChild(link);
  link.click();
}


  function toggleAllOrders(source) {
  document.querySelectorAll('.orderSelect').forEach(cb => cb.checked = source.checked);
}

async function downloadSelectedPDF() {
  const selected = [...document.querySelectorAll('.orderSelect:checked')].map(cb => cb.value);
  if (selected.length === 0) return alert("⚠️ Please select at least one order!");
  
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();
  let y = 20;
  
  const orders = JSON.parse(localStorage.getItem('orders') || '[]');
  
  selected.forEach((id, index) => {
    const o = orders.find(x => x.orderId === id);
    if (!o) return;
    doc.text(`Order ID: ${o.orderId}`, 20, y);
    doc.text(`Date: ${o.createdAt || '-'}`, 20, y + 10);
    doc.text(`Company: ${o.company}`, 20, y + 20);
    doc.text(`Plan: ${o.plan}`, 20, y + 30);
    doc.text(`Country: ${o.country}`, 20, y + 40);
    doc.text(`Mobile: ${o.mobile}`, 20, y + 50);
    doc.text(`Total: ${o.total}`, 20, y + 60);
    y += 80;
    if (index < selected.length - 1) doc.addPage();
  });

  doc.save("Selected_Orders.pdf");
}

const themeToggle=document.getElementById('themeToggle');
function applyTheme(){
  const t=localStorage.getItem('ns_theme')||'dark';
  document.documentElement.setAttribute('data-theme',t);
  themeToggle.textContent=t==='dark'?'☀️ Light':'🌙 Dark';
 
}
themeToggle.onclick=()=>{const c=document.documentElement.getAttribute('data-theme')==='dark'?'light':'dark';localStorage.setItem('ns_theme',c);applyTheme();};
function changeTheme(v){localStorage.setItem('ns_theme',v);applyTheme();}
applyTheme();

/* Login */
function login(){if(user.value==='a'&&pass.value==='1'){localStorage.setItem('isAdmin','true');initDashboard();}else alert('❌ Wrong credentials');}
function logout(){localStorage.removeItem('isAdmin');location.reload();}
if(localStorage.getItem('isAdmin')==='true'){document.getElementById('loginBox').style.display='none';document.getElementById('dashboard').style.display='block';initDashboard();}

/* Init */
function initDashboard(){
  document.getElementById('loginBox').style.display='none';
  document.getElementById('dashboard').style.display='block';
  loadSettings();renderTable();renderChart();
}

/* Settings */
function saveSettings(){['emailjs_service','emailjs_template','emailjs_user','admin_email','sms_webhook'].forEach(k=>localStorage.setItem(k,document.getElementById(k).value));alert('Settings saved ✅');}
function loadSettings(){['emailjs_service','emailjs_template','emailjs_user','admin_email','sms_webhook'].forEach(k=>document.getElementById(k).value=localStorage.getItem(k)||'');}

/* Orders Table */


/* --- Helper: try to preserve types for number & date --- */
function detectTypeAndCreateInput(key, value) {
  const lower = key.toLowerCase();
  // common date keys
  if (lower.includes('date') || lower === 'dob' || /^\d{2}\/\d{2}\/\d{4}$/.test(value)) {
    return `<input type="date" id="edit_${key}" value="${formatToInputDate(value)}">`;
  }
  // numeric
  if (!isNaN(value) && value !== '') {
    return `<input type="number" id="edit_${key}" value="${value}">`;
  }
  // status field -> select
  if (lower === 'status') {
    return `<select id="edit_${key}">
      <option${value==='Pending'?' selected':''}>Pending</option>
      <option${value==='Processing'?' selected':''}>Processing</option>
      <option${value==='Underwriting_Done'?' selected':''}>Underwriting_Done</option>
      <option${value==='Deleted'?' selected':''}>Deleted</option>
    </select>`;
  }
  // long text fields
  if (String(value).length > 80 || lower.includes('note') || lower.includes('address')) {
    return `<textarea id="edit_${key}" rows="4">${escapeHtml(value)}</textarea>`;
  }
  // default text
  return `<input type="text" id="edit_${key}" value="${escapeHtml(value)}">`;
}

function escapeHtml(str) {
  if (str === undefined || str === null) return '';
  return String(str).replace(/[&<>"']/g, s => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"}[s]));
}

function formatToInputDate(val) {
  if (!val) return '';
  // if already YYYY-MM-DD
  if (/^\d{4}-\d{2}-\d{2}$/.test(val)) return val;
  // try dd/mm/yyyy or dd-mm-yyyy
  const m = val.match(/(\d{2})[\/\-](\d{2})[\/\-](\d{4})/);
  if (m) return `${m[3]}-${m[2]}-${m[1]}`;
  // fallback: return empty
  return '';
}
function showDetails(orderId) {
  const orders = JSON.parse(localStorage.getItem('orders') || '[]');
  const order = orders.find(o => o.orderId === orderId);
  if (!order) { alert('⚠️ Order not found'); return; }

  currentEditId = orderId;
  const form = document.getElementById('editForm');
  form.innerHTML = '';

  // Build inputs keeping original key order
  Object.entries(order).forEach(([key, value]) => {
    // don't allow editing orderId (optional: you can remove this if you want editable id)
    const readOnly = (key === 'orderId' || key === 'createdAt') ? 'readonly' : '';
    const inputHtml = detectTypeAndCreateInput(key, value);
    form.innerHTML += `
      <div class="edit-field">
        <label>${key.replace(/([A-Z])/g, ' $1').replace(/^./, c => c.toUpperCase())}</label>
        ${inputHtml}
        ${readOnly ? `<small style="color:gray">This field is read-only</small>` : ''}
      </div>
    `;
    // if readonly, add attribute after insertion
    if (readOnly) {
      const el = document.getElementById(`edit_${key}`);
      if (el) el.setAttribute('readonly', 'true');
    }
  });

  document.getElementById('detailsModal').style.display = 'block';



  

  // Build inputs keeping original key order
  Object.entries(order).forEach(([key, value]) => {
    // don't allow editing orderId (optional: you can remove this if you want editable id)
    const readOnly = (key === 'orderId' || key === 'createdAt') ? 'readonly' : '';
    const inputHtml = detectTypeAndCreateInput(key, value);
    form.innerHTML += `
      <div class="edit-field">
        <label>${key.replace(/([A-Z])/g, ' $1').replace(/^./, c => c.toUpperCase())}</label>
        ${inputHtml}
        ${readOnly ? `<small style="color:gray">This field is read-only</small>` : ''}
      </div>
    `;
    // if readonly, add attribute after insertion
    if (readOnly) {
      const el = document.getElementById(`edit_${key}`);
      if (el) el.setAttribute('readonly', 'true');
    }
  });

  document.getElementById('detailsModal').style.display = 'block';
}

/* Save edited fields back to localStorage, preserving types */
function saveDetails() {
  if (!currentEditId) return alert('⚠️ No order selected');

  const orders = JSON.parse(localStorage.getItem('orders') || '[]');
  const idx = orders.findIndex(o => o.orderId === currentEditId);
  if (idx === -1) return alert('⚠️ Order not found');

  const updated = {...orders[idx]}; // start from existing object to preserve unknown keys

  // iterate keys of the original object to keep same shape & order
  Object.keys(orders[idx]).forEach(key => {
    const el = document.getElementById(`edit_${key}`);
    if (!el) return; // skip if input not present (shouldn't happen)
    let val = el.value;

    // convert back to number/date when appropriate
    if (el.type === 'number') {
      val = val === '' ? '' : Number(val);
    } else if (el.type === 'date') {
      val = val === '' ? '' : val; // keep YYYY-MM-DD; if you prefer dd/mm/yyyy convert here
    } else if (el.tagName.toLowerCase() === 'select') {
      val = el.value;
    } else if (el.tagName.toLowerCase() === 'textarea') {
      val = el.value;
    }

    updated[key] = val;
  });

  // Save and refresh
  orders[idx] = updated;
  localStorage.setItem('orders', JSON.stringify(orders));
  alert('✅ Order updated successfully!');
  closeDetails();
  if (typeof renderTable === 'function') renderTable();
}

/* Close modal (keeps currentEditId cleared) */
function closeDetails() {
  const modal = document.getElementById('detailsModal');
  if (modal) modal.style.display = 'none';
  currentEditId = null;
}

/* click outside to close — keep existing behavior but ensure modal variable exists */
window.addEventListener('click', function(event){
  const modal = document.getElementById('detailsModal');
  if (!modal) return;
  if (event.target === modal) closeDetails();
});



function renderTable(){


  const term=document.getElementById('search').value.toLowerCase();
  const tbody=document.querySelector('#ordersTable tbody');
  const orders=JSON.parse(localStorage.getItem('orders')||'[]');
  tbody.innerHTML='';
  const filtered=orders.filter(o=>JSON.stringify(o).toLowerCase().includes(term));
  filtered.forEach(o=>{
    const tr=document.createElement('tr');
    tr.className=o.status.toLowerCase();
    tr.innerHTML=`
              <td><input type="checkbox" class="orderSelect" value="${o.orderId}"></td>
              
              <td>${o.createdAt || '-'}</td>
              <td>${o.orderId}</td>
              <td><button class="btn" onclick="showDetails('${o.orderId}')">🔍 Details</button></td>

              <td>${o.company}</td>
              <td>${o.plan}</td>
              <td>${o.dob}</td>
              <td>${o.ageBand}</td>
              <td>${o.duration}</td>
              <td>${o.country}</td>
              <td>${o.occupation || '-'}</td>
              <td>${o.travelDate}</td>
              <td>${o.mobile}</td>
              <td>${o.multiplier}</td>
              <td>${o.offer}</td>
              <td>${o.total}</td>
              <td>${o.status}</td>
  
    <button class="btn danger" onclick="removeOrder('${o.orderId}')">🗑️</button>
  </td>`;

    tbody.appendChild(tr); 
  });
  document.getElementById('count').innerText=`Total Orders: ${filtered.length}`;
}

/* Update Status */
function updateStatus(id,val){
  let orders=JSON.parse(localStorage.getItem('orders')||'[]');
  orders=orders.map(o=>o.orderId===id?{...o,status:val}:o);
  localStorage.setItem('orders',JSON.stringify(orders));
  renderTable();renderChart();
}

/* Remove Order */
function removeOrder(id){
  if(confirm("Are you sure you want to remove this order?")){
    let orders=JSON.parse(localStorage.getItem('orders')||'[]');
    orders=orders.filter(o=>o.orderId!==id);
    localStorage.setItem('orders',JSON.stringify(orders));
    renderTable();renderChart();
    alert('🗑️ Order removed successfully!');
  }
}

/* Chart */
function renderChart(){
 
  const orders=JSON.parse(localStorage.getItem('orders')||'[]');
  const counts={Pending:0,Processing:0,Underwriting:0,Deleted:0};
  orders.forEach(o=>counts[o.status]=(counts[o.status]||0)+1);
  new Chart(ctx,{type:'doughnut',data:{labels:Object.keys(counts),datasets:[{data:Object.values(counts),backgroundColor:['#f59e0b','#3b82f6','#eab308','#ef4444']}]},options:{plugins:{legend:{labels:{color:document.documentElement.getAttribute('data-theme')==='dark'?'#fff':'#000'}}}}});
}

/* PDF / Excel / CSV */
async function generateInvoice() {
  const selected = [...document.querySelectorAll('.orderSelect:checked')].map(cb => cb.value);
  if (selected.length === 0) {
    alert("⚠️ Please select at least one order to generate invoice!");
    return;
  }

  const orders = JSON.parse(localStorage.getItem('orders') || '[]');
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

   const logoUrl = "data:image/png;base64,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F/t8sg/DOxERERER+YWfGtZV7PBjm74pZ9GrWi0vusZfZDlWDhXIu4EB4JmqvraqrvpUGTasIyIiIiIiX1BBkawK7SvH9ecBw5l3IiIiIiIifysU3rdZjtTgHdd0iTXuCQB3ARBT/KcB/MXPfr75B/zdccVuhnciIiIiIiKyeMc1XaLSodS+dU+845quDT/7+WZuFVeYbZUiouqEZfNERERERERUSKngnrPuHdd03W85SrC7RwPDOxERERERERVyrMAxnLWgEY31ken/XR+p+1PLJ5HtWDZPREREREREhfwVgP8tjq9evggXLmlG5zmLcM25cXR96T+nP30yk11U4GvJZgzvREREREREZLGwsb7t/7vuTTKszybC/PZ9RyzHyTksmyciIiIiIiKLd1+47NTmlw/i57tG5anBX76KG/9lC/YfP43b33bujE9/xzVdhTrek40Y3omIiIiIiMhi1+Hx+SZMrD67RZ76wKoEbr5kqfy3KJ+//uKz87+E4d1hDO9ERERERERk8eC3vve5q85pOfn1/3oJB45OyNPnLlmAZQsa5b+vOW9GOb2t+8qTFcM7ERERERGRvxWa9T5qOVKFP3jzih99/LpVyGRNLGiM4V2XJKa/SefyRXLt+4KG6NjPfr7Zlp9HxbFhHRERERERkb9Z9mMfGR2wayZ8M4C1ixfELCeaG6LY0P1W/OzV0W9aTpLtOPNORERERERO2s1H19dEeEd9xMDh45MYOzFpuS9rrl1wFDvv6cLOewpVAFDtxsDwTkREREREThoZHbAtvCfiyVbLQXJU5Na/FTP4W7JZE42xOrQ01c/4canx08gu3PvJ7MTxTaLHHXbesxs77+nhs2IrWUXB8E5ERERERH7RyWfKEz31MSMzvyEy42efHjuBI6/uR2rXONKHdiK1fzvMyVOihP9h7LynNzSPTnG2/r4yvBMREREREVFRkbeNdUc6j0ew5BAmT03g2GuHcPA3e3Dk1QPIZrKYPNI09aXZDNJje3PfprvY9wsRWytF2LCOiIiIiIiISulGxER2/kuoX7gKwALEmhsxeTKF9KkUjHR6+kuNukiJb0O1YHgnIiIiIiKniYZbLXyU/cF42hCN5zrMq83NM26wYQCZRtTPq0f9vBgaW9SMe10aGeMVGPXzEFmwXB7akzn2TPvTRpdoWGhebbJpoQ0Y3omIiIiI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"; 
  let y = 20;

  for (let i = 0; i < selected.length; i++) {
    const order = orders.find(o => o.orderId === selected[i]);
    if (!order) continue;

    // --- Header ---
    try {
      const response = await fetch(logoUrl);
      const blob = await response.blob();
      const reader = new FileReader();
      await new Promise(resolve => {
        reader.onloadend = () => resolve();
        reader.readAsDataURL(blob);
      });
    doc.addImage(reader.result, 'PNG', 14, 14, 30, 20);
    } catch (e) {
      console.warn("Logo not loaded");
    }

    doc.setFontSize(18);
    doc.text("NextSure Insurance", 45, 25);
    doc.setFontSize(11);
    doc.text("Official Invoice", 45, 33);
    doc.line(15, 40, 195, 40);
    y = 55;

    // --- Basic Info ---
    doc.setFontSize(12);
    doc.text(`Order ID: ${order.orderId}`, 15, y);
    y += 8;
    doc.text(`Created At: ${order.createdAt || '-'}`, 15, y);
    y += 10;
    doc.line(15, y, 195, y);
    y += 10;

    // --- All Fields ---
    const fields = Object.entries(order);
    fields.forEach(([key, value]) => {
      if (['orderId', 'createdAt'].includes(key)) return;
      const label = key.replace(/([A-Z])/g, ' $1').replace(/^./, c => c.toUpperCase());
      doc.setFontSize(11);
      doc.text(`${label}:`, 15, y);
      doc.text(String(value || '-'), 70, y);
      y += 8;
      if (y > 270) { doc.addPage(); y = 20; }
    });

    // --- Footer ---
    y += 50;
    doc.line(15, y, 195, y);
    y += 10;
    doc.setFontSize(10);
    doc.text("Contact: +8801851008300", 15, y);
    y += 6;
    doc.text("Website: www.nextsure.xyz", 15, y);
    y += 6;
    doc.text("Address: Gulshan 1, Dhaka, Bangladesh", 15, y);

    // যদি আরও অর্ডার থাকে, addPage করব
    if (i < selected.length - 1) doc.addPage();
  }

  doc.save("Invoices_Selected_Orders.pdf");
}


// Download the helper library from https://www.twilio.com/docs/node/install
const twilio = require("twilio"); // Or, for ESM: import twilio from "twilio";

// Find your Account SID and Auth Token at twilio.com/console
// and set the environment variables. See http://twil.io/secure
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
const client = twilio(accountSid, authToken);

async function createMessage() {
  const message = await client.messages.create({
    body: "This is the ship that made the Kessel Run in fourteen parsecs?",
    from: "+8801851008300",
    to: "+8801886311621",
  });

  console.log(message.body);
}

createMessage();
</script>
<!-- Details/Edit Modal -->
<div id="detailsModal" class="modal">
  <div class="modal-content">
    <span class="close" onclick="closeDetails()">&times;</span>
    <h3>Edit Order Details</h3>
    <form id="editForm"></form>
    <div style="text-align:center;margin-top:15px;">
      <button class="btn primary" type="button" onclick="saveDetails()">✅ Save</button>
      <button class="btn" type="button" onclick="closeDetails()">❌ Cancel</button>
    </div>
  </div>
</div>
<!-- === Firebase Firestore + Authentication Integration === -->
<script type="module">
 // Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAnalytics } from "firebase/analytics";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyCXhfBmVjh--qFtwcMjWMR5TRu80hOe5wc",
  authDomain: "nextsure-admin.firebaseapp.com",
  projectId: "nextsure-admin",
  storageBucket: "nextsure-admin.firebasestorage.app",
  messagingSenderId: "736664254101",
  appId: "1:736664254101:web:32c59df3ea8cca168b0d9c",
  measurementId: "G-ZS2MWTK52K"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const analytics = getAnalytics(app);
  const auth = getAuth(app);

  // 🟢 Login Form
  async function login() {
    const email = document.getElementById('user').value;
    const password = document.getElementById('pass').value;
    try {
      await signInWithEmailAndPassword(auth, email, password);
      alert("✅ Login successful!");
      document.getElementById('loginBox').style.display = 'none';
      document.getElementById('dashboard').style.display = 'block';
      loadOrdersFromFirestore();
    } catch (err) {
      alert("❌ Login failed: " + err.message);
    }
  }
  window.login = login;

  // 🔴 Logout
  async function logout() {
    await signOut(auth);
    document.getElementById('loginBox').style.display = 'block';
    document.getElementById('dashboard').style.display = 'none';
  }
  window.logout = logout;

  // 🟣 Firestore: Load All Orders
  async function loadOrdersFromFirestore() {
    const querySnapshot = await getDocs(collection(db, "orders"));
    const orders = [];
    querySnapshot.forEach((docSnap) => {
      orders.push({ id: docSnap.id, ...docSnap.data() });
    });
    localStorage.setItem('orders', JSON.stringify(orders));
    renderTable();
  }

  // 🟡 Firestore: Save New Order
  async function saveOrderToFirestore(order) {
    await addDoc(collection(db, "orders"), order);
  }

  // 🟠 Firestore: Update Order
  async function updateOrderInFirestore(orderId, updatedData) {
    const ref = doc(db, "orders", orderId);
    await updateDoc(ref, updatedData);
  }

  // 👀 Auth State Listener
  onAuthStateChanged(auth, (user) => {
    if (user) {
      document.getElementById('loginBox').style.display = 'none';
      document.getElementById('dashboard').style.display = 'block';
      loadOrdersFromFirestore();
    } else {
      document.getElementById('loginBox').style.display = 'block';
      document.getElementById('dashboard').style.display = 'none';
    }
  });

  /* ✏️ Modify your existing saveDetails() */
  window.saveDetails = async function() {
    if (!currentEditId) return alert('⚠️ No order selected');
    const orders = JSON.parse(localStorage.getItem('orders') || '[]');
    const idx = orders.findIndex(o => o.orderId === currentEditId);
    if (idx === -1) return alert('⚠️ Order not found');

    const updated = {...orders[idx]};
    Object.keys(updated).forEach(key => {
      const el = document.getElementById(`edit_${key}`);
      if (el) updated[key] = el.value;
    });

    // ✅ Update Firestore
    try {
      await updateOrderInFirestore(updated.id || currentEditId, updated);
      orders[idx] = updated;
      localStorage.setItem('orders', JSON.stringify(orders));
      alert("✅ Order updated in Firestore!");
      closeDetails();
      renderTable();
    } catch (err) {
      alert("❌ Firestore update failed: " + err.message);
    }
  };
</script>

</body>
</html>
   
