# Rizki.github.io
belajar 

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Stok - Demo</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        
        .header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .header h1 {
            color: #333;
            font-size: 24px;
            margin-bottom: 10px;
        }
        
        .header p {
            color: #666;
            font-size: 14px;
        }
        
        .tabs {
            display: flex;
            margin-bottom: 25px;
            background: #f8f9fa;
            border-radius: 12px;
            padding: 4px;
        }
        
        .tab {
            flex: 1;
            padding: 12px;
            text-align: center;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            font-weight: 500;
        }
        
        .tab.active {
            background: #667eea;
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .menu-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .menu-item {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            border: none;
            font-size: 14px;
            font-weight: 600;
        }
        
        .menu-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        
        .menu-item:active {
            transform: translateY(0);
        }
        
        .menu-item.unavailable {
            background: #95a5a6;
            cursor: not-allowed;
        }
        
        .menu-item.unavailable:hover {
            transform: none;
        }
        
        .stock-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 12px;
            margin-bottom: 10px;
        }
        
        .stock-name {
            font-weight: 600;
            color: #333;
        }
        
        .stock-amount {
            font-weight: 700;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 12px;
        }
        
        .stock-high {
            background: #27ae60;
            color: white;
        }
        
        .stock-medium {
            background: #f39c12;
            color: white;
        }
        
        .stock-low {
            background: #e74c3c;
            color: white;
        }
        
        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            border-bottom: 1px solid #eee;
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-time {
            font-size: 12px;
            color: #666;
        }
        
        .transaction-menu {
            font-weight: 600;
            color: #333;
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #27ae60;
            color: white;
            padding: 15px 20px;
            border-radius: 10px;
            font-weight: 600;
            transform: translateX(100%);
            transition: all 0.3s;
            z-index: 1000;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .notification.error {
            background: #e74c3c;
        }
        
        .summary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }
        
        .summary h3 {
            margin-bottom: 15px;
            font-size: 18px;
        }
        
        .summary-stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-number {
            font-size: 24px;
            font-weight: 700;
            display: block;
        }
        
        .stat-label {
            font-size: 12px;
            opacity: 0.8;
        }
        
        .reset-btn {
            width: 100%;
            padding: 15px;
            background: #e74c3c;
            color: white;
            border: none;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
            margin-top: 20px;
        }
        
        .reset-btn:hover {
            background: #c0392b;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🍽️ Sistem Stok</h1>
            <p>Tap menu untuk jual & potong stok otomatis</p>
        </div>
        
        <div class="tabs">
            <div class="tab active" onclick="showTab('penjualan')">Penjualan</div>
            <div class="tab" onclick="showTab('stok')">Stok</div>
            <div class="tab" onclick="showTab('laporan')">Laporan</div>
        </div>
        
        <div id="penjualan" class="tab-content active">
            <div class="menu-grid">
                <button class="menu-item" onclick="sellItem('Ayam Goreng', 'ayam-goreng')">
                    🍗<br>Ayam Goreng<br>Rp 15.000
                </button>
                <button class="menu-item" onclick="sellItem('Nasi Gudeg', 'nasi-gudeg')">
                    🍛<br>Nasi Gudeg<br>Rp 12.000
                </button>
                <button class="menu-item" onclick="sellItem('Es Teh Manis', 'es-teh')">
                    🧊<br>Es Teh Manis<br>Rp 3.000
                </button>
                <button class="menu-item" onclick="sellItem('Soto Ayam', 'soto-ayam')">
                    🍜<br>Soto Ayam<br>Rp 10.000
                </button>
                <button class="menu-item" onclick="sellItem('Gado-gado', 'gado-gado')">
                    🥗<br>Gado-gado<br>Rp 8.000
                </button>
                <button class="menu-item" onclick="sellItem('Jus Jeruk', 'jus-jeruk')">
                    🍊<br>Jus Jeruk<br>Rp 5.000
                </button>
            </div>
        </div>
        
        <div id="stok" class="tab-content">
            <div id="stock-list">
                <!-- Stock items will be populated by JavaScript -->
            </div>
        </div>
        
        <div id="laporan" class="tab-content">
            <div class="summary">
                <h3>📊 Ringkasan Hari Ini</h3>
                <div class="summary-stats">
                    <div class="stat">
                        <span class="stat-number" id="total-sales">0</span>
                        <span class="stat-label">Total Penjualan</span>
                    </div>
                    <div class="stat">
                        <span class="stat-number" id="total-revenue">Rp 0</span>
                        <span class="stat-label">Total Pendapatan</span>
                    </div>
                </div>
            </div>
            
            <div id="transaction-list">
                <!-- Transactions will be populated by JavaScript -->
            </div>
            
            <button class="reset-btn" onclick="resetData()">🔄 Reset Data Hari Ini</button>
        </div>
    </div>
    
    <div id="notification" class="notification"></div>
    
    <script>
        // Data struktur
        let stock = {
            'ayam': { name: 'Ayam (kg)', amount: 10, unit: 'kg', threshold: 2 },
            'beras': { name: 'Beras (kg)', amount: 25, unit: 'kg', threshold: 5 },
            'minyak': { name: 'Minyak Goreng (liter)', amount: 8, unit: 'liter', threshold: 2 },
            'gula': { name: 'Gula (kg)', amount: 5, unit: 'kg', threshold: 1 },
            'teh': { name: 'Teh Celup (box)', amount: 3, unit: 'box', threshold: 1 },
            'jeruk': { name: 'Jeruk (kg)', amount: 6, unit: 'kg', threshold: 1 },
            'sayuran': { name: 'Sayuran Campur (kg)', amount: 4, unit: 'kg', threshold: 1 },
            'bumbu': { name: 'Bumbu Masak (paket)', amount: 8, unit: 'paket', threshold: 2 }
        };
        
        let recipes = {
            'ayam-goreng': {
                'ayam': 0.3,
                'beras': 0.2,
                'minyak': 0.1
            },
            'nasi-gudeg': {
                'ayam': 0.1,
                'beras': 0.2,
                'bumbu': 0.1
            },
            'es-teh': {
                'teh': 0.05,
                'gula': 0.02
            },
            'soto-ayam': {
                'ayam': 0.2,
                'beras': 0.15,
                'bumbu': 0.1
            },
            'gado-gado': {
                'sayuran': 0.3,
                'bumbu': 0.1
            },
            'jus-jeruk': {
                'jeruk': 0.3,
                'gula': 0.02
            }
        };
        
        let menuPrices = {
            'ayam-goreng': 15000,
            'nasi-gudeg': 12000,
            'es-teh': 3000,
            'soto-ayam': 10000,
            'gado-gado': 8000,
            'jus-jeruk': 5000
        };
        
        let transactions = [];
        let totalRevenue = 0;
        
        // Functions
        function showTab(tabName) {
            document.querySelectorAll('.tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
            
            event.target.classList.add('active');
            document.getElementById(tabName).classList.add('active');
            
            if (tabName === 'stok') {
                updateStockDisplay();
            } else if (tabName === 'laporan') {
                updateReportDisplay();
            }
        }
        
        function sellItem(menuName, menuId) {
            const recipe = recipes[menuId];
            const price = menuPrices[menuId];
            
            // Check if ingredients are sufficient
            for (let ingredient in recipe) {
                if (stock[ingredient].amount < recipe[ingredient]) {
                    showNotification(`Stok ${stock[ingredient].name} tidak cukup!`, 'error');
                    return;
                }
            }
            
            // Deduct ingredients
            for (let ingredient in recipe) {
                stock[ingredient].amount -= recipe[ingredient];
                stock[ingredient].amount = Math.max(0, Math.round(stock[ingredient].amount * 100) / 100);
            }
            
            // Add transaction
            transactions.push({
                time: new Date().toLocaleTimeString('id-ID'),
                menu: menuName,
                price: price
            });
            
            totalRevenue += price;
            
            showNotification(`✅ ${menuName} terjual!`);
            
            // Check for low stock alerts
            checkLowStock();
        }
        
        function checkLowStock() {
            for (let key in stock) {
                if (stock[key].amount <= stock[key].threshold) {
                    setTimeout(() => {
                        showNotification(`⚠️ Stok ${stock[key].name} hampir habis!`, 'error');
                    }, 1000);
                }
            }
        }
        
        function updateStockDisplay() {
            const stockList = document.getElementById('stock-list');
            stockList.innerHTML = '';
            
            for (let key in stock) {
                const item = stock[key];
                const stockLevel = item.amount > item.threshold * 2 ? 'high' : 
                                 item.amount > item.threshold ? 'medium' : 'low';
                
                stockList.innerHTML += `
                    <div class="stock-item">
                        <span class="stock-name">${item.name}</span>
                        <span class="stock-amount stock-${stockLevel}">
                            ${item.amount} ${item.unit}
                        </span>
                    </div>
                `;
            }
        }
        
        function updateReportDisplay() {
            document.getElementById('total-sales').textContent = transactions.length;
            document.getElementById('total-revenue').textContent = 
                new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(totalRevenue);
            
            const transactionList = document.getElementById('transaction-list');
            transactionList.innerHTML = '';
            
            transactions.slice(-10).reverse().forEach(transaction => {
                transactionList.innerHTML += `
                    <div class="transaction-item">
                        <div>
                            <div class="transaction-menu">${transaction.menu}</div>
                            <div class="transaction-time">${transaction.time}</div>
                        </div>
                        <div style="font-weight: 600; color: #27ae60;">
                            ${new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(transaction.price)}
                        </div>
                    </div>
                `;
            });
        }
        
        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${type}`;
            notification.classList.add('show');
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        function resetData() {
            if (confirm('Reset semua data hari ini?')) {
                transactions = [];
                totalRevenue = 0;
                updateReportDisplay();
                showNotification('Data berhasil direset!');
            }
        }
        
        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateStockDisplay();
        });
    </script>
</body>
</html>