<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scholar Desk | Internal Order Management Dashboard</title>
    <!-- Fonts & Icons -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --primary: #0a192f;
            --secondary: #1e3a8a;
            --accent: #d4af37;
            --bg: #f8fafc;
            --text: #1e293b;
            --card-bg: #ffffff;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; }

        body {
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* Header */
        header {
            background-color: var(--primary);
            color: white;
            padding: 1rem 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--accent);
            display: flex;
            align-items: center;
            gap: 10px;
            text-decoration: none;
        }

        .nav-links { display: flex; align-items: center; gap: 1.5rem; }
        .nav-links a { color: white; text-decoration: none; font-weight: 600; font-size: 0.95rem; transition: color 0.2s; }
        .nav-links a:hover { color: var(--accent); }

        /* Container */
        .container { max-width: 1200px; margin: 0 auto; padding: 2.5rem 1rem; width: 100%; flex: 1; }

        /* Admin Navigation Bar */
        .admin-nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--primary);
            padding: 1rem 1.5rem;
            border-radius: 12px;
            margin-bottom: 2rem;
            color: white;
            flex-wrap: wrap;
            gap: 1rem;
            border: 1px solid rgba(212, 175, 55, 0.3);
        }

        /* Data Dashboard Styles */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1.5rem; margin-bottom: 2rem; }
        .stat-card { background: var(--card-bg); padding: 1.5rem; border-radius: 12px; border: 1px solid #e2e8f0; border-top: 4px solid var(--secondary); text-align: center; box-shadow: 0 4px 6px rgba(0,0,0,0.02); }
        .stat-title { font-size: 0.85rem; color: #64748b; font-weight: 800; text-transform: uppercase; margin-bottom: 0.5rem; letter-spacing: 0.5px; }
        .stat-value { font-size: 2rem; font-weight: 900; color: var(--primary); }
        .stat-profit { color: #10b981; }

        .dashboard-grid { display: grid; grid-template-columns: 1fr 2fr; gap: 1.5rem; }
        @media(max-width: 1024px) { .dashboard-grid { grid-template-columns: 1fr; } }
        
        .card { background: var(--card-bg); border-radius: 12px; padding: 1.5rem; box-shadow: 0 4px 15px -3px rgba(0,0,0,0.05); border: 1px solid #e2e8f0; }
        .form-group { margin-bottom: 1rem; }
        .form-group label { display: block; font-size: 0.85rem; font-weight: 600; margin-bottom: 0.4rem; color: #475569; }
        .form-group input, .form-group select { width: 100%; padding: 0.6rem; border: 1px solid #cbd5e1; border-radius: 6px; font-size: 0.9rem; outline: none; }
        .form-group input:focus, .form-group select:focus { border-color: var(--secondary); }
        
        .checkbox-group { display: flex; align-items: center; gap: 8px; margin: 1rem 0; font-size: 0.9rem; font-weight: 600; }
        
        .live-calc { background: #f8fafc; padding: 1rem; border-radius: 8px; margin: 1rem 0; border: 1px solid #e2e8f0; }
        .calc-row { display: flex; justify-content: space-between; font-size: 0.9rem; margin-bottom: 0.5rem; font-weight: 600; }
        .calc-total { font-weight: 800; font-size: 1.1rem; color: var(--secondary); border-top: 1px solid #cbd5e1; padding-top: 0.5rem; margin-top: 0.5rem; }

        table { width: 100%; border-collapse: collapse; font-size: 0.9rem; min-width: 700px; }
        th { text-align: left; padding: 1rem; background-color: #f8fafc; color: #64748b; border-bottom: 2px solid #e2e8f0; }
        td { padding: 1rem; border-bottom: 1px solid #e2e8f0; }
        
        .status-badge { padding: 0.4rem 0.8rem; border-radius: 20px; font-size: 0.8rem; font-weight: 700; border: none; outline: none; cursor: pointer; }
        .action-btn { background: #fee2e2; border: none; color: #ef4444; cursor: pointer; padding: 8px; border-radius: 6px; transition: 0.2s; }
        .action-btn:hover { background: #ef4444; color: white; }

        .btn-tool { border: none; border-radius: 8px; padding: 0.75rem 1.25rem; font-weight: 700; cursor: pointer; transition: 0.2s; display: inline-flex; align-items: center; gap: 8px; font-size: 0.9rem; text-decoration: none; justify-content: center; }
        .btn-tool-primary { background: var(--secondary); color: white; }
        .btn-tool-primary:hover { background: var(--primary); }
        .btn-tool-success { background: #10b981; color: white; }
        .btn-tool-success:hover { background: #059669; }
        .btn-tool-secondary { background: #e2e8f0; color: var(--text); }
        .btn-tool-danger { background: #fee2e2; color: #991b1b; }
        .btn-tool-danger:hover { background: #ef4444; color: white; }

        /* Footer */
        footer { background: var(--primary); color: white; text-align: center; padding: 2rem; margin-top: auto; }

        /* Print Settings for Report Generation */
        @media print {
            body * { visibility: hidden; }
            #printable-report, #printable-report * { visibility: visible; }
            #printable-report { position: absolute; left: 0; top: 0; width: 100%; }
            .no-print { display: none !important; }
            .card { border: none; box-shadow: none; padding: 0; }
            body { background: white; }
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header class="no-print">
        <a href="index.html" class="logo">🎓 Scholar Desk</a>
        <nav class="nav-links">
            <a href="index.html">Back to Main Site</a>
        </nav>
    </header>

    <!-- Main Container -->
    <div class="container" id="printable-report">
        
        <!-- Navigation / Title Bar -->
        <div class="admin-nav no-print">
            <div style="display: flex; align-items: center; gap: 10px;">
                <span style="font-size: 1.2rem; font-weight: 800; color: var(--accent);">👑 Internal Order Management Dashboard</span>
            </div>
            <a href="index.html" class="btn-tool" style="background: #ef4444; color: white; padding: 0.5rem 1rem;">
                <i class="fa-solid fa-arrow-left"></i> Return to Site
            </a>
        </div>

        <!-- Print Report Header (Only visible on print) -->
        <div style="display: none; text-align: center; margin-bottom: 2rem;" class="print-header">
            <h1 style="color: var(--primary);">Scholar Desk Official Order Report</h1>
            <p id="print-date" style="color: #64748b; font-style: italic;"></p>
        </div>

        <!-- Stats Summary -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-title">Total Orders</div>
                <div class="stat-value" id="stat-orders">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Gross Revenue (Rs.)</div>
                <div class="stat-value" id="stat-revenue">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">Net Profit (Rs.)</div>
                <div class="stat-value stat-profit" id="stat-profit">0</div>
            </div>
        </div>

        <!-- Dashboard Controls (Hidden on Print) -->
        <div class="dashboard-grid no-print">
            <!-- New Order Form -->
            <div class="card">
                <h2 style="color: var(--primary); font-size: 1.2rem; border-bottom: 2px solid #f1f5f9; padding-bottom: 0.5rem; margin-bottom: 1rem;">Log New Order</h2>
                <form id="orderForm" onsubmit="submitOrder(event)">
                    <div class="form-group">
                        <label>Customer Info</label>
                        <input type="text" id="customer" required placeholder="Name - Phone">
                    </div>
                    <div class="form-group">
                        <label>Service</label>
                        <select id="serviceType" onchange="calculateDashPreview()">
                            <option value="250">Handwritten (10 Pgs) - Rs. 250</option>
                            <option value="300">Handwritten (15 Pgs) - Rs. 300</option>
                            <option value="150">Word Doc - Rs. 150</option>
                            <option value="250">Presentation - Rs. 250</option>
                            <option value="399">Article - Rs. 399</option>
                            <option value="150">Plagiarism Removal - Rs. 150</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Assignee</label>
                        <select id="assignee">
                            <option value="Unassigned">Unassigned</option>
                            <option value="Samar">Samar</option>
                            <option value="Ahmed">Ahmed</option>
                            <option value="Urwa">Urwa</option>
                            <option value="Saman">Saman</option>
                        </select>
                    </div>
                    <div class="checkbox-group">
                        <input type="checkbox" id="dash-delivery" onchange="calculateDashPreview()">
                        <label for="dash-delivery" style="margin:0;">Physical Delivery (+Rs. 250)</label>
                    </div>
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                        <div class="form-group">
                            <label>Extra Charges (+)</label>
                            <input type="number" id="extraCharge" value="0" min="0" oninput="calculateDashPreview()">
                        </div>
                        <div class="form-group">
                            <label>Writer Cost (-)</label>
                            <input type="number" id="dash-cost" value="0" min="0" oninput="calculateDashPreview()">
                        </div>
                        <div class="form-group" style="grid-column: span 2;">
                            <label>Ad / Marketing Cost (-)</label>
                            <input type="number" id="adCharge" value="0" min="0" oninput="calculateDashPreview()">
                        </div>
                    </div>

                    <div class="live-calc">
                        <div class="calc-row"><span>Base:</span> <span id="preview-base">Rs. 250</span></div>
                        <div class="calc-row"><span>Extra/Delivery:</span> <span id="preview-extra">Rs. 0</span></div>
                        <div class="calc-row"><span>Cost/Ads Deduction:</span> <span id="preview-deduct" style="color:#ef4444;">Rs. 0</span></div>
                        <div class="calc-row calc-total"><span>Total Charge:</span> <span id="preview-total">Rs. 250</span></div>
                        <div class="calc-row"><span style="color:#10b981;">Net Profit:</span> <span id="preview-profit" style="color:#10b981; font-weight:800;">Rs. 250</span></div>
                    </div>

                    <button type="submit" class="btn-tool btn-tool-primary" style="width: 100%;"><i class="fa-solid fa-plus"></i> Add to Board</button>
                </form>
            </div>

            <!-- Management Actions -->
            <div class="card">
                <h2 style="color: var(--primary); font-size: 1.2rem; border-bottom: 2px solid #f1f5f9; padding-bottom: 0.5rem; margin-bottom: 1rem;">Data Management & Backups</h2>
                <div style="display: flex; flex-direction: column; gap: 12px;">
                    <button class="btn-tool" style="background:#475569; color:white;" onclick="window.print()">
                        <i class="fa-solid fa-print"></i> Print Official Report
                    </button>
                    <button class="btn-tool btn-tool-success" onclick="exportData()">
                        <i class="fa-solid fa-download"></i> Backup Orders (JSON)
                    </button>
                    <label class="btn-tool btn-tool-secondary" style="text-align: center; justify-content: center; border: 1px solid #cbd5e1; cursor: pointer;">
                        <i class="fa-solid fa-upload"></i> Restore / Upload Backup
                        <input type="file" accept=".json" style="display:none;" onchange="importData(event)">
                    </label>
                    <button class="btn-tool btn-tool-danger" style="margin-top: 1rem;" onclick="clearAllOrders()">
                        <i class="fa-solid fa-trash"></i> Wipe All Data
                    </button>
                </div>
            </div>
        </div>

        <!-- Orders Table -->
        <div class="card" style="margin-top: 1.5rem; overflow-x: auto;">
            <h2 style="color: var(--primary); font-size: 1.2rem; margin-bottom: 1rem;" class="no-print">Active Order Board</h2>
            <table id="ordersTable">
                <thead>
                    <tr>
                        <th>Customer</th>
                        <th>Service</th>
                        <th>Assignee</th>
                        <th>Revenue</th>
                        <th>Profit</th>
                        <th>Status</th>
                        <th class="no-print">Action</th>
                    </tr>
                </thead>
                <tbody id="tableBody"></tbody>
            </table>
        </div>
    </div>

    <!-- Footer -->
    <footer class="no-print">
        <h2 style="color: var(--accent); margin-bottom: 0.5rem; font-size: 1.2rem;">Scholar Desk Internal</h2>
        <p style="color: #cbd5e1; font-size: 0.85rem;">© 2026 Scholar Desk. All rights reserved.</p>
    </footer>

    <!-- Logic Script -->
    <script>
        let orders = JSON.parse(localStorage.getItem('scholarOrders_standalone')) || [];

        function calculateDashPreview() {
            const basePrice = parseInt(document.getElementById('serviceType').value) || 0;
            const hasDelivery = document.getElementById('dash-delivery').checked;
            const deliveryCharge = hasDelivery ? 250 : 0;
            const extraCharge = parseInt(document.getElementById('extraCharge').value) || 0;
            const cost = parseInt(document.getElementById('dash-cost').value) || 0;
            const adCharge = parseInt(document.getElementById('adCharge').value) || 0;

            const total = basePrice + deliveryCharge + extraCharge;
            const profit = (basePrice + extraCharge) - cost - adCharge; 

            document.getElementById('preview-base').innerText = `Rs. ${basePrice}`;
            document.getElementById('preview-extra').innerText = `Rs. ${extraCharge + deliveryCharge}`;
            document.getElementById('preview-deduct').innerText = `Rs. ${cost + adCharge}`;
            document.getElementById('preview-total').innerText = `Rs. ${total}`;
            document.getElementById('preview-profit').innerText = `Rs. ${profit}`;

            return { total, profit };
        }

        function submitOrder(e) {
            e.preventDefault();
            const serviceSelect = document.getElementById('serviceType');
            const calc = calculateDashPreview();

            const newOrder = {
                id: Date.now(),
                customer: document.getElementById('customer').value,
                service: serviceSelect.options[serviceSelect.selectedIndex].text.split(' - ')[0],
                assignee: document.getElementById('assignee').value,
                total: calc.total,
                profit: calc.profit,
                status: 'New'
            };

            orders.push(newOrder);
            saveData();
            document.getElementById('orderForm').reset();
            calculateDashPreview();
        }

        function updateStatus(id, newStatus) {
            const idx = orders.findIndex(o => o.id === id);
            if(idx > -1) { orders[idx].status = newStatus; saveData(); }
        }

        function deleteOrder(id) {
            if(confirm("Delete this order?")) {
                orders = orders.filter(o => o.id !== id);
                saveData();
            }
        }

        function saveData() {
            localStorage.setItem('scholarOrders_standalone', JSON.stringify(orders));
            renderDashboard();
        }

        function renderDashboard() {
            const tbody = document.getElementById('tableBody');
            tbody.innerHTML = '';
            let tRev = 0, tProf = 0;

            orders.forEach(order => {
                tRev += order.total; tProf += order.profit;
                
                let statColor = order.status === 'Completed' ? '#065f46' : (order.status === 'In Progress' ? '#b45309' : '#991b1b');

                tbody.innerHTML += `
                    <tr>
                        <td><strong>${order.customer}</strong></td>
                        <td>${order.service}</td>
                        <td>${order.assignee}</td>
                        <td style="color:var(--secondary); font-weight:bold;">Rs. ${order.total}</td>
                        <td style="color:#10b981; font-weight:bold;">Rs. ${order.profit}</td>
                        <td>
                            <select class="status-badge no-print" onchange="updateStatus(${order.id}, this.value)" style="color:${statColor}">
                                <option value="New" ${order.status === 'New' ? 'selected' : ''}>New</option>
                                <option value="In Progress" ${order.status === 'In Progress' ? 'selected' : ''}>In Progress</option>
                                <option value="Completed" ${order.status === 'Completed' ? 'selected' : ''}>Completed</option>
                            </select>
                            <span style="display:none; color:${statColor}; font-weight:bold;" class="print-status">${order.status}</span>
                        </td>
                        <td class="no-print"><button class="action-btn" onclick="deleteOrder(${order.id})"><i class="fa-solid fa-trash"></i></button></td>
                    </tr>
                `;
            });

            document.getElementById('stat-orders').innerText = orders.length;
            document.getElementById('stat-revenue').innerText = tRev.toLocaleString();
            document.getElementById('stat-profit').innerText = tProf.toLocaleString();
            document.getElementById('print-date').innerText = "Generated: " + new Date().toLocaleDateString();
        }

        function exportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(orders));
            const a = document.createElement('a');
            a.href = dataStr;
            a.download = "scholar_desk_orders_backup.json";
            a.click();
        }

        function importData(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = e => {
                try {
                    const imported = JSON.parse(e.target.result);
                    if (Array.isArray(imported)) {
                        orders = imported;
                        saveData();
                        alert("Backup restored successfully!");
                    }
                } catch (err) { alert("Invalid JSON backup file."); }
            };
            reader.readAsText(file);
        }

        function clearAllOrders() {
            if(confirm("WARNING: Wiping data permanently from local storage. Are you sure?")) { orders = []; saveData(); }
        }

        window.addEventListener('beforeprint', () => {
            document.querySelectorAll('.print-header').forEach(el => el.style.display = 'block');
            document.querySelectorAll('.print-status').forEach(el => el.style.display = 'inline');
            document.querySelectorAll('.status-badge').forEach(el => el.style.display = 'none');
        });
        window.addEventListener('afterprint', () => {
            document.querySelectorAll('.print-header').forEach(el => el.style.display = 'none');
            document.querySelectorAll('.print-status').forEach(el => el.style.display = 'none');
            document.querySelectorAll('.status-badge').forEach(el => el.style.display = 'inline-block');
        });

        renderDashboard();
        calculateDashPreview();
    </script>
</body>
</html>
