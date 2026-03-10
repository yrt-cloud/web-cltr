[index.html](https://github.com/user-attachments/files/25857474/index.html)
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator Kasir Pro - Shortcut 00 & 000</title>
    <style>
        :root {
            --bg-color: #f3f4f6;
            --calculator-bg: #1e293b;
            --screen-bg: #ced4da; 
            --btn-num: #334155;
            --btn-op: #f59e0b;
            --btn-action: #10b981;
            --btn-clear: #ef4444;
            --text-light: #ffffff;
        }

        * { box-sizing: border-box; }

        body {
            background-color: var(--bg-color);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Inter', sans-serif;
            overflow: hidden;
        }

        .container {
            display: flex;
            background: #ffffff;
            padding: 15px;
            border-radius: 20px;
            box-shadow: 0 25px 50px -12px rgba(0,0,0,0.15);
            gap: 15px;
            width: 98%;
            max-width: 950px;
            height: 95vh;
            align-items: stretch;
        }

        /* --- STYLE STRUK SUPERMARKET --- */
        .receipt-container {
            flex: 0 0 300px;
            display: flex;
            flex-direction: column;
            background: #fff;
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            overflow: hidden;
        }

        .receipt-main {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
            overflow: hidden;
            padding: 15px;
        }

        .receipt-header {
            text-align: center;
            margin-bottom: 0px;
            position: relative;
            flex-shrink: 0;
        }

        .settings-icon {
            position: absolute;
            top: -5px;
            right: -5px;
            cursor: pointer;
            font-size: 16px;
            padding: 5px;
            color: #3b82f6;
            z-index: 10;
        }

        .receipt-header h2 { margin: 0; font-size: 15px; text-transform: uppercase; }
        .receipt-header p { margin: 2px 0; font-size: 10px; color: #4b5563; }
        
        #realtime-clock {
            font-weight: 900;
            color: #000000;
            font-size: 14px;
            margin: 5px 0;
            display: block;
            letter-spacing: 1px;
        }

        .receipt-body {
            flex-grow: 1;
            overflow-y: auto;
            font-family: 'Courier New', Courier, monospace;
            font-size: 13px;
            color: #1a1a1a;
            line-height: 1.2;
            padding-right: 5px;
        }

        .receipt-body::-webkit-scrollbar { width: 4px; }
        .receipt-body::-webkit-scrollbar-track { background: #f1f1f1; }
        .receipt-body::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 10px; }

        .divider { border-top: 1px dashed #334155; margin: 8px 0; }
        .receipt-item { display: flex; justify-content: space-between; margin-bottom: 4px; }

        .receipt-footer {
            text-align: center;
            margin-top: 15px;
            font-size: 10px;
            color: #6b7280;
            flex-shrink: 0;
        }

        /* --- STYLE KALKULATOR --- */
        .calculator {
            flex: 1;
            background: var(--calculator-bg);
            padding: 15px;
            border-radius: 15px;
            display: flex;
            flex-direction: column;
        }

        .screen-container { margin-bottom: 12px; }

        #display {
            width: 100%;
            height: 65px;
            background: var(--screen-bg);
            color: #0f172a;
            text-align: right;
            font-size: 32px;
            padding: 10px 15px;
            border: 4px solid #0f172a;
            border-radius: 8px;
            font-family: 'monospace';
            font-weight: 700;
            white-space: nowrap;
            overflow: hidden;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 8px;
            flex-grow: 1;
        }

        button {
            width: 100%;
            height: 100%;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            color: var(--text-light);
            transition: all 0.05s;
            box-shadow: 0 3px 0 #0f172a;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        button:active, button.active { 
            transform: translateY(2px); 
            box-shadow: 0 1px 0 #0f172a;
        }

        .btn-num { background: var(--btn-num); }
        .btn-op { background: var(--btn-op); }
        .btn-clear { background: var(--btn-clear); }
        .btn-pay { 
            background: var(--btn-action); 
            grid-column: span 2;
            font-size: 14px;
        }
        .btn-enter { background: #3b82f6; grid-row: span 2; }
        .btn-util { background: #475569; font-size: 14px; }

        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.9);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal {
            background: white;
            padding: 25px;
            border-radius: 20px;
            width: 90%;
            max-width: 320px;
            text-align: center;
        }

        .modal input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            font-size: 18px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            text-align: center;
        }

        .modal-btn {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            margin-top: 8px;
            font-weight: bold;
            border: none;
            cursor: pointer;
        }

        .shortcut-info {
            font-size: 9px;
            color: #94a3b8;
            text-align: center;
            padding-top: 10px;
            line-height: 1.4;
        }

        .small-text { font-size: 22px !important; }
        .extra-small-text { font-size: 16px !important; }

        /* --- PRINT CSS --- */
        @media print {
            body { background: white; height: auto; display: block; overflow: visible; }
            .container { 
                box-shadow: none; 
                padding: 0; 
                margin: 0; 
                display: block; 
                width: 100%;
                height: auto;
            }
            .calculator, .settings-icon, .shortcut-info, #btn-reset-main, #btn-print-receipt { 
                display: none !important; 
            }
            .receipt-container {
                border: none;
                width: 80mm; 
                margin: 0 auto;
                height: auto;
                overflow: visible;
            }
            .receipt-main { padding: 0; overflow: visible; height: auto; display: block; }
            .receipt-body { overflow: visible; height: auto; display: block; padding-right: 0; }
            .receipt-footer { display: block !important; }
        }
    </style>
</head>
<body>

<div class="container">
    <div class="receipt-container">
        <div class="receipt-main" id="print-area">
            <div class="receipt-header">
                <span class="settings-icon" onclick="openSettings()" title="Pengaturan">⚙️</span>
                <h2 id="header-name">KOPERASI SWADHARMA</h2>
                <p id="header-addr">Jl.Asia Afrika No.119 Kota Bandung</p>
                <div class="divider"></div>
                <p id="receipt-date"></p>
                <span id="realtime-clock">00:00:00</span>
                <p id="receipt-id"></p>
                <div class="divider"></div>
            </div>
            
            <div class="receipt-body" id="receipt-scroll-area">
                <div id="log-content"></div>
                <div id="receipt-summary"></div>
                <div class="receipt-footer" id="thanks-note" style="display:none;">
                    <div class="divider"></div>
                    <p>BARANG TIDAK DAPAT DITUKAR</p>
                    <p>TERIMA KASIH</p>
                </div>
            </div>
        </div>
        
        <div style="padding: 10px; background: #f8fafc; display: flex; flex-direction: column; gap: 5px;">
            <button class="btn-util" id="btn-print-receipt" style="width:100%; height:35px; font-size:11px; box-shadow:none; background: #6366f1;" onclick="printReceipt()">CETAK STRUK (P)</button>
            <button class="btn-clear" id="btn-reset-main" style="width:100%; height:35px; font-size:11px; box-shadow:none;" onclick="resetAll()">RESET STRUK (R)</button>
        </div>
    </div>

    <div class="calculator">
        <div class="screen-container">
            <input type="text" id="display" value="0" readonly>
        </div>
        <div class="buttons">
            <button class="btn-clear" id="key-c" onclick="clearDisplay()">C</button>
            <button class="btn-op" id="key-/" onclick="appendOp('/')">÷</button>
            <button class="btn-op" id="key-*" onclick="appendOp('*')">×</button>
            <button class="btn-op" id="key-backspace" onclick="deleteLast()">DEL</button>
            
            <button class="btn-num" id="key-7" onclick="appendNum('7')">7</button>
            <button class="btn-num" id="key-8" onclick="appendNum('8')">8</button>
            <button class="btn-num" id="key-9" onclick="appendNum('9')">9</button>
            <button class="btn-op" id="key--" onclick="appendOp('-')">−</button>
            
            <button class="btn-num" id="key-4" onclick="appendNum('4')">4</button>
            <button class="btn-num" id="key-5" onclick="appendNum('5')">5</button>
            <button class="btn-num" id="key-6" onclick="appendNum('6')">6</button>
            <button class="btn-op" id="key-+" onclick="appendOp('+')">+</button>
            
            <button class="btn-num" id="key-1" onclick="appendNum('1')">1</button>
            <button class="btn-num" id="key-2" onclick="appendNum('2')">2</button>
            <button class="btn-num" id="key-3" onclick="appendNum('3')">3</button>
            <button class="btn-enter" id="key-enter" onclick="processEntry()">OK</button>
            
            <button class="btn-num" id="key-0" onclick="appendNum('0')">0</button>
            <button class="btn-util" id="key-00" onclick="appendNum('00')">00</button>
            <button class="btn-util" id="key-000" onclick="appendNum('000')">000</button>
            
            <button class="btn-num" id="key-." onclick="appendNum('.')">.</button>
            <button class="btn-pay" id="key-pay" onclick="openPaymentModal()">BAYAR (SPACE)</button>
        </div>
        <div class="shortcut-info">
            0-9, +, -, *, /, Ent (OK), Bksp (Del), Esc (C), Space (Pay), P (Print), R (Reset)<br>
            <strong>Shortcut Cepat: [ (00) , ] (000)</strong>
        </div>
    </div>
</div>

<!-- Modals -->
<div class="modal-overlay" id="paymentModal">
    <div class="modal">
        <h3>TOTAL</h3>
        <h1 id="modalTotalDisplay">0</h1>
        <input type="number" id="cashInput" placeholder="Tunai...">
        <div style="display:flex; gap:10px">
            <button class="modal-btn" style="background:#f1f5f9; color:#475569" onclick="closeModal()">BATAL</button>
            <button class="modal-btn" style="background:#10b981; color:white" onclick="processPayment()">OK</button>
        </div>
    </div>
</div>

<div class="modal-overlay" id="settingsModal">
    <div class="modal">
        <h3>EDIT HEADER</h3>
        <input type="text" id="shopNameInput" placeholder="Nama Toko">
        <input type="text" id="shopAddrInput" placeholder="Alamat Toko">
        <button class="modal-btn" style="background:#3b82f6; color:white" onclick="saveSettings()">SIMPAN</button>
        <button class="modal-btn" style="background:#f1f5f9; color:#475569" onclick="closeSettings()">BATAL</button>
    </div>
</div>

<script>
    const display = document.getElementById('display');
    const logContent = document.getElementById('log-content');
    const summaryContent = document.getElementById('receipt-summary');
    const clockElement = document.getElementById('realtime-clock');
    const scrollArea = document.getElementById('receipt-scroll-area');
    let currentTotal = 0;
    let itemCount = 0;
    let isModalOpen = false;
    let isSettingsOpen = false;
    let transactionFinalized = false;

    function updateClock() {
        const now = new Date();
        const hours = String(now.getHours()).padStart(2, '0');
        const minutes = String(now.getMinutes()).padStart(2, '0');
        const seconds = String(now.getSeconds()).padStart(2, '0');
        clockElement.innerText = `${hours}:${minutes}:${seconds}`;
    }

    function initReceiptInfo() {
        const now = new Date();
        const options = { year: 'numeric', month: 'long', day: 'numeric' };
        document.getElementById('receipt-date').innerText = now.toLocaleDateString('id-ID', options);
        document.getElementById('receipt-id').innerText = "TRX#" + Math.random().toString(36).substr(2, 6).toUpperCase();
        
        updateClock();
        setInterval(updateClock, 1000);
    }

    function formatNumber(num) { return num.toLocaleString('id-ID'); }

    function adjustFontSize() {
        const len = display.value.length;
        display.classList.remove('small-text', 'extra-small-text');
        if (len > 15) display.classList.add('extra-small-text');
        else if (len > 11) display.classList.add('small-text');
    }

    function appendNum(num) {
        if (transactionFinalized) return;
        if (display.value === "0") display.value = num;
        else display.value += num;
        adjustFontSize();
        animateButton("key-" + num);
    }

    function appendOp(op) {
        if (transactionFinalized) return;
        const val = display.value.trim();
        const lastChar = val.slice(-1);
        if (['+', '-', '*', '/'].includes(lastChar)) {
            display.value = val.slice(0, -1) + " " + op + " ";
        } else {
            display.value += " " + op + " ";
        }
        adjustFontSize();
        animateButton("key-" + op);
    }

    function clearDisplay() { 
        display.value = "0"; 
        adjustFontSize();
        animateButton("key-c");
    }

    function deleteLast() {
        if (transactionFinalized) return;
        let val = display.value.trim();
        if (val.length > 1) {
            display.value = val.slice(0, -1).trim();
        } else {
            display.value = "0";
        }
        adjustFontSize();
        animateButton("key-backspace");
    }

    function animateButton(id) {
        const btn = document.getElementById(id);
        if (btn) {
            btn.classList.add('active');
            setTimeout(() => btn.classList.remove('active'), 100);
        }
    }

    function processEntry() {
        if (transactionFinalized) return;
        animateButton("key-enter");
        try {
            let expression = display.value.replace(/×/g, '*').replace(/÷/g, '/');
            let result = eval(expression);
            if (result === undefined || isNaN(result) || result === Infinity) return;
            
            itemCount++;
            const itemDiv = document.createElement('div');
            itemDiv.className = 'receipt-item';
            itemDiv.innerHTML = `<span>ITEM ${itemCount}</span> <span>${formatNumber(result)}</span>`;
            logContent.appendChild(itemDiv);
            currentTotal += result;
            display.value = "0";
            adjustFontSize();
            
            scrollArea.scrollTop = scrollArea.scrollHeight;
        } catch (e) { display.value = "Error"; setTimeout(clearDisplay, 800); }
    }

    function openPaymentModal() {
        if (transactionFinalized) return;
        if (currentTotal <= 0 && display.value !== "0") processEntry();
        if (currentTotal <= 0) return;
        isModalOpen = true;
        document.getElementById('modalTotalDisplay').innerText = formatNumber(currentTotal);
        document.getElementById('paymentModal').style.display = 'flex';
        document.getElementById('cashInput').value = '';
        setTimeout(() => document.getElementById('cashInput').focus(), 150);
    }

    function closeModal() { document.getElementById('paymentModal').style.display = 'none'; isModalOpen = false; }

    function processPayment() {
        const cashInput = document.getElementById('cashInput');
        const cash = parseFloat(cashInput.value);
        if (isNaN(cash) || cash < currentTotal) { alert("Uang Tunai Kurang!"); return; }
        
        const change = cash - currentTotal;
        summaryContent.innerHTML = `
            <div class="divider"></div>
            <div class="receipt-item"><strong>TOTAL</strong> <strong>${formatNumber(currentTotal)}</strong></div>
            <div class="receipt-item">TUNAI <span>${formatNumber(cash)}</span></div>
            <div class="receipt-item" style="color:#10b981; font-weight:bold">KEMBALI <span>${formatNumber(change)}</span></div>
        `;
        document.getElementById('thanks-note').style.display = 'block';
        closeModal();
        transactionFinalized = true;
        
        scrollArea.scrollTop = scrollArea.scrollHeight;
    }

    function printReceipt() {
        if (!transactionFinalized) {
            alert("Selesaikan pembayaran terlebih dahulu sebelum mencetak!");
            return;
        }
        window.print();
    }

    function openSettings() {
        isSettingsOpen = true;
        document.getElementById('shopNameInput').value = document.getElementById('header-name').innerText;
        document.getElementById('shopAddrInput').value = document.getElementById('header-addr').innerText;
        document.getElementById('settingsModal').style.display = 'flex';
    }
    function closeSettings() { 
        document.getElementById('settingsModal').style.display = 'none'; 
        isSettingsOpen = false;
    }
    function saveSettings() {
        document.getElementById('header-name').innerText = document.getElementById('shopNameInput').value || "TOKO";
        document.getElementById('header-addr').innerText = document.getElementById('shopAddrInput').value || "Alamat";
        closeSettings();
    }
    
    function resetAll() { 
        if(confirm("Hapus struk dan mulai transaksi baru?")) {
            location.reload(); 
        }
    }

    window.addEventListener('keydown', (e) => {
        if (isSettingsOpen) return;

        if (isModalOpen) {
            if (e.key === "Enter") processPayment();
            if (e.key === "Escape") closeModal();
            return;
        }

        const key = e.key;
        
        // Handle angka 0-9
        if (key >= "0" && key <= "9") appendNum(key);
        if (key === ".") appendNum(".");
        
        // Shortcut Tambahan: 00 dan 000
        if (key === "[") appendNum("00");
        if (key === "]") appendNum("000");

        if (key === "+") appendOp("+");
        if (key === "-") appendOp("-");
        if (key === "*") appendOp("*");
        if (key === "/") { e.preventDefault(); appendOp("/"); }
        if (key === "Enter") { e.preventDefault(); processEntry(); }
        if (key === "Backspace") deleteLast();
        if (key === "Escape") clearDisplay();
        if (key === " ") { e.preventDefault(); openPaymentModal(); }
        if (key.toLowerCase() === "r") resetAll();
        if (key.toLowerCase() === "p") printReceipt();
    });

    window.onload = initReceiptInfo;
</script>
</body>
</html>
