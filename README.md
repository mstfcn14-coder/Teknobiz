```html
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TeknoBiz Veresiye Takip</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
    font-family:Arial,Helvetica,sans-serif;
}

body{
    background:#f1f4f8;
    color:#172033;
    min-height:100vh;
}

header{
    background:#071a33;
    color:white;
    padding:22px;
    text-align:center;
    box-shadow:0 3px 12px rgba(0,0,0,.15);
}

header h1{
    font-size:28px;
}

header p{
    margin-top:6px;
    opacity:.8;
}

.container{
    max-width:1200px;
    margin:auto;
    padding:20px;
}

.cards{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:15px;
    margin-bottom:20px;
}

.card{
    background:white;
    border-radius:15px;
    padding:20px;
    box-shadow:0 3px 12px rgba(0,0,0,.08);
}

.card small{
    color:#687386;
}

.card strong{
    display:block;
    font-size:25px;
    margin-top:8px;
}

.actions{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:12px;
    margin-bottom:20px;
}

button{
    border:0;
    border-radius:10px;
    padding:13px 15px;
    cursor:pointer;
    font-weight:bold;
    transition:.2s;
}

button:hover{
    transform:translateY(-1px);
    opacity:.92;
}

.btn-blue{
    background:#1479ff;
    color:white;
}

.btn-green{
    background:#16a36a;
    color:white;
}

.btn-red{
    background:#dc3545;
    color:white;
}

.btn-dark{
    background:#172033;
    color:white;
}

.search{
    background:white;
    padding:15px;
    border-radius:15px;
    margin-bottom:15px;
    box-shadow:0 3px 12px rgba(0,0,0,.07);
}

.search input{
    width:100%;
    padding:14px;
    border:1px solid #d7dce4;
    border-radius:10px;
    outline:none;
    font-size:16px;
}

.table-box{
    background:white;
    border-radius:15px;
    padding:15px;
    box-shadow:0 3px 12px rgba(0,0,0,.07);
    overflow-x:auto;
}

table{
    width:100%;
    border-collapse:collapse;
    min-width:750px;
}

th,td{
    padding:13px 10px;
    border-bottom:1px solid #edf0f4;
    text-align:left;
}

th{
    background:#f7f9fc;
}

.badge{
    padding:6px 9px;
    border-radius:20px;
    font-size:12px;
    font-weight:bold;
}

.badge-red{
    background:#ffe2e5;
    color:#c52232;
}

.badge-green{
    background:#dcf8eb;
    color:#087a4a;
}

.empty{
    text-align:center;
    padding:40px;
    color:#777;
}

.modal{
    display:none;
    position:fixed;
    inset:0;
    background:rgba(0,0,0,.55);
    align-items:center;
    justify-content:center;
    padding:20px;
    z-index:999;
}

.modal.active{
    display:flex;
}

.modal-content{
    background:white;
    width:100%;
    max-width:520px;
    border-radius:18px;
    padding:22px;
    max-height:90vh;
    overflow-y:auto;
}

.modal-content h2{
    margin-bottom:18px;
}

.form-group{
    margin-bottom:13px;
}

.form-group label{
    display:block;
    margin-bottom:6px;
    font-weight:bold;
    font-size:14px;
}

.form-group input,
.form-group textarea{
    width:100%;
    padding:12px;
    border:1px solid #d5dbe4;
    border-radius:9px;
    outline:none;
    font-size:15px;
}

.form-group textarea{
    min-height:80px;
    resize:vertical;
}

.modal-buttons{
    display:flex;
    gap:10px;
    margin-top:18px;
}

.modal-buttons button{
    flex:1;
}

.detail{
    background:#f7f9fc;
    border-radius:12px;
    padding:13px;
    margin-bottom:10px;
}

.detail strong{
    display:block;
    margin-bottom:5px;
}

.history{
    margin-top:15px;
}

.history-item{
    background:white;
    border:1px solid #e7eaf0;
    border-radius:10px;
    padding:12px;
    margin-top:8px;
}

.close{
    float:right;
    font-size:25px;
    cursor:pointer;
}

footer{
    text-align:center;
    padding:25px;
    color:#718096;
}

@media(max-width:800px){
    .cards{
        grid-template-columns:repeat(2,1fr);
    }

    .actions{
        grid-template-columns:repeat(2,1fr);
    }
}

@media(max-width:500px){
    .container{
        padding:12px;
    }

    .cards{
        grid-template-columns:1fr 1fr;
        gap:9px;
    }

    .card{
        padding:14px;
    }

    .card strong{
        font-size:20px;
    }

    .actions{
        grid-template-columns:1fr 1fr;
    }
}
</style>
</head>

<body>

<header>
    <h1>📒 TeknoBiz Veresiye</h1>
    <p>Veresiye Takip Sistemi</p>
</header>

<div class="container">

    <div class="cards">
        <div class="card">
            <small>Toplam Açık Borç</small>
            <strong id="totalDebt">0,00 TL</strong>
        </div>

        <div class="card">
            <small>Borçlu Müşteri</small>
            <strong id="customerCount">0</strong>
        </div>

        <div class="card">
            <small>Bugünkü Tahsilat</small>
            <strong id="todayPayment">0,00 TL</strong>
        </div>

        <div class="card">
            <small>Toplam Kayıt</small>
            <strong id="totalCustomer">0</strong>
        </div>
    </div>

    <div class="actions">
        <button class="btn-blue" onclick="openCustomerModal()">
            👤 Müşteri Ekle
        </button>

        <button class="btn-green" onclick="openDebtModal()">
            💰 Borç Ekle
        </button>

        <button class="btn-dark" onclick="openPaymentModal()">
            💵 Ödeme Al
        </button>

        <button class="btn-red" onclick="clearAllData()">
            🗑️ Tüm Verileri Sil
        </button>
    </div>

    <div class="search">
        <input
            type="text"
            id="searchInput"
            placeholder="🔎 Müşteri adı veya telefon ara..."
            oninput="renderCustomers()"
        >
    </div>

    <div class="table-box">
        <table>
            <thead>
                <tr>
                    <th>Müşteri</th>
                    <th>Telefon</th>
                    <th>Borç</th>
                    <th>Son İşlem</th>
                    <th>Durum</th>
                    <th>İşlem</th>
                </tr>
            </thead>

            <tbody id="customerTable"></tbody>
        </table>
    </div>

</div>

<footer>
    TeknoBiz Veresiye Takip • Bilgiler bu cihazda saklanır.
</footer>


<!-- MÜŞTERİ EKLE -->

<div class="modal" id="customerModal">
    <div class="modal-content">

        <span class="close" onclick="closeModal('customerModal')">&times;</span>

        <h2>👤 Müşteri Ekle</h2>

        <div class="form-group">
            <label>Ad Soyad</label>
            <input id="customerName" placeholder="Örn: Ahmet Yılmaz">
        </div>

        <div class="form-group">
            <label>Telefon</label>
            <input id="customerPhone" placeholder="05XXXXXXXXX">
        </div>

        <div class="form-group">
            <label>Not</label>
            <textarea id="customerNote" placeholder="Müşteri hakkında not..."></textarea>
        </div>

        <div class="modal-buttons">
            <button class="btn-dark" onclick="closeModal('customerModal')">
                Vazgeç
            </button>

            <button class="btn-blue" onclick="addCustomer()">
                Kaydet
            </button>
        </div>

    </div>
</div>


<!-- BORÇ EKLE -->

<div class="modal" id="debtModal">
    <div class="modal-content">

        <span class="close" onclick="closeModal('debtModal')">&times;</span>

        <h2>💰 Borç Ekle</h2>

        <div class="form-group">
            <label>Müşteri</label>
            <select id="debtCustomer"></select>
        </div>

        <div class="form-group">
            <label>Borç Tutarı</label>
            <input id="debtAmount" type="number" step="0.01" placeholder="0">
        </div>

        <div class="form-group">
            <label>Ürün / Açıklama</label>
            <textarea id="debtDescription" placeholder="Örn: iPhone 15 kılıfı"></textarea>
        </div>

        <div class="modal-buttons">
            <button class="btn-dark" onclick="closeModal('debtModal')">
                Vazgeç
            </button>

            <button class="btn-green" onclick="addDebt()">
                Borç Ekle
            </button>
        </div>

    </div>
</div>


<!-- ÖDEME -->

<div class="modal" id="paymentModal">
    <div class="modal-content">

        <span class="close" onclick="closeModal('paymentModal')">&times;</span>

        <h2>💵 Ödeme Al</h2>

        <div class="form-group">
            <label>Müşteri</label>
            <select id="paymentCustomer"></select>
        </div>

        <div class="form-group">
            <label>Ödeme Tutarı</label>
            <input id="paymentAmount" type="number" step="0.01" placeholder="0">
        </div>

        <div class="form-group">
            <label>Not</label>
            <textarea id="paymentNote" placeholder="Ödeme hakkında not..."></textarea>
        </div>

        <div class="modal-buttons">
            <button class="btn-dark" onclick="closeModal('paymentModal')">
                Vazgeç
            </button>

            <button class="btn-green" onclick="addPayment()">
                Ödemeyi Kaydet
            </button>
        </div>

    </div>
</div>


<!-- DETAY -->

<div class="modal" id="detailModal">
    <div class="modal-content">

        <span class="close" onclick="closeModal('detailModal')">&times;</span>

        <h2 id="detailTitle">Müşteri</h2>

        <div id="detailContent"></div>

    </div>
</div>


<script>

let customers = JSON.parse(localStorage.getItem("teknoVeresiye")) || [];

function saveData(){
    localStorage.setItem("teknoVeresiye", JSON.stringify(customers));
}

function money(value){
    return Number(value || 0).toLocaleString("tr-TR", {
        minimumFractionDigits:2,
        maximumFractionDigits:2
    }) + " TL";
}

function today(){
    return new Date().toLocaleDateString("tr-TR");
}

function now(){
    return new Date().toLocaleString("tr-TR");
}

function getBalance(customer){
    let balance = 0;

    customer.transactions.forEach(t=>{
        if(t.type === "debt"){
            balance += Number(t.amount);
        }

        if(t.type === "payment"){
            balance -= Number(t.amount);
        }
    });

    return Math.max(0,balance);
}

function openModal(id){
    document.getElementById(id).classList.add("active");
}

function closeModal(id){
    document.getElementById(id).classList.remove("active");
}

function openCustomerModal(){

    document.getElementById("customerName").value="";
    document.getElementById("customerPhone").value="";
    document.getElementById("customerNote").value="";

    openModal("customerModal");
}

function addCustomer(){

    const name =
        document.getElementById("customerName").value.trim();

    const phone =
        document.getElementById("customerPhone").value.trim();

    const note =
        document.getElementById("customerNote").value.trim();

    if(!name){
        alert("Lütfen müşteri adını yaz.");
        return;
    }

    customers.push({
        id:Date.now(),
        name:name,
        phone:phone,
        note:note,
        created:now(),
        transactions:[]
    });

    saveData();
    renderAll();

    closeModal("customerModal");

    alert("Müşteri başarıyla eklendi.");
}

function fillCustomerSelects(){

    const debtSelect =
        document.getElementById("debtCustomer");

    const paymentSelect =
        document.getElementById("paymentCustomer");

    debtSelect.innerHTML="";
    paymentSelect.innerHTML="";

    customers.forEach(c=>{

        const option1=document.createElement("option");
        option1.value=c.id;
        option1.textContent=c.name;

        debtSelect.appendChild(option1);

        const option2=document.createElement("option");
        option2.value=c.id;
        option2.textContent=c.name;

        paymentSelect.appendChild(option2);

    });
}

function openDebtModal(){

    if(customers.length===0){
        alert("Önce müşteri eklemelisin.");
        return;
    }

    fillCustomerSelects();

    document.getElementById("debtAmount").value="";
    document.getElementById("debtDescription").value="";

    openModal("debtModal");
}

function addDebt(){

    const customerId =
        Number(document.getElementById("debtCustomer").value);

    const amount =
        Number(document.getElementById("debtAmount").value);

    const description =
        document.getElementById("debtDescription").value.trim();

    if(!amount || amount<=0){
        alert("Geçerli bir borç tutarı gir.");
        return;
    }

    const customer =
        customers.find(c=>c.id===customerId);

    if(!customer) return;

    customer.transactions.push({
        type:"debt",
        amount:amount,
        description:description || "Veresiye",
        date:now()
    });

    saveData();
    renderAll();

    closeModal("debtModal");

    alert("Borç başarıyla eklendi.");
}

function openPaymentModal(){

    if(customers.length===0){
        alert("Önce müşteri eklemelisin.");
        return;
    }

    fillCustomerSelects();

    document.getElementById("paymentAmount").value="";
    document.getElementById("paymentNote").value="";

    openModal("paymentModal");
}

function addPayment(){

    const customerId =
        Number(document.getElementById("paymentCustomer").value);

    const amount =
        Number(document.getElementById("paymentAmount").value);

    const note =
        document.getElementById("paymentNote").value.trim();

    if(!amount || amount<=0){
        alert("Geçerli bir ödeme tutarı gir.");
        return;
    }

    const customer =
        customers.find(c=>c.id===customerId);

    if(!customer) return;

    const balance=getBalance(customer);

    if(amount>balance){
        alert("Ödeme tutarı mevcut borçtan fazla olamaz.");
        return;
    }

    customer.transactions.push({
        type:"payment",
        amount:amount,
        description:note || "Ödeme",
        date:now()
    });

    saveData();
    renderAll();

    closeModal("paymentModal");

    alert("Ödeme başarıyla kaydedildi.");
}

function renderCustomers(){

    const search =
        document.getElementById("searchInput")
        .value
        .toLowerCase()
        .trim();

    const table =
        document.getElementById("customerTable");

    table.innerHTML="";

    const filtered =
        customers.filter(c=>
            c.name.toLowerCase().includes(search) ||
            c.phone.toLowerCase().includes(search)
        );

    if(filtered.length===0){

        table.innerHTML=`
        <tr>
            <td colspan="6" class="empty">
                Kayıt bulunamadı.
            </td>
        </tr>`;

        return;
    }

    filtered.forEach(c=>{

        const balance=getBalance(c);

        let last="";

        if(c.transactions.length){
            last=c.transactions[c.transactions.length-1].date;
        }else{
            last=c.created;
        }

        const status =
            balance>0
            ? `<span class="badge badge-red">Borçlu</span>`
            : `<span class="badge badge-green">Borç Yok</span>`;

        const tr=document.createElement("tr");

        tr.innerHTML=`
            <td><strong>${escapeHtml(c.name)}</strong></td>

            <td>${escapeHtml(c.phone || "-")}</td>

            <td><strong>${money(balance)}</strong></td>

            <td>${last}</td>

            <td>${status}</td>

            <td>
                <button
                    class="btn-blue"
                    onclick="showDetail(${c.id})">
                    Detay
                </button>
            </td>
        `;

        table.appendChild(tr);
    });
}

function showDetail(id){

    const customer =
        customers.find(c=>c.id===id);

    if(!customer) return;

    const balance=getBalance(customer);

    document.getElementById("detailTitle").textContent =
        customer.name;

    let html=`

        <div class="detail">
            <strong>Telefon</strong>
            ${escapeHtml(customer.phone || "-")}
        </div>

        <div class="detail">
            <strong>Not</strong>
            ${escapeHtml(customer.note || "-")}
        </div>

        <div class="detail">
            <strong>Mevcut Borç</strong>
            ${money(balance)}
        </div>

        <div class="history">
            <h3>📜 İşlem Geçmişi</h3>
    `;

    if(customer.transactions.length===0){

        html+=`
            <div class="history-item">
                Henüz işlem bulunmuyor.
            </div>
        `;

    }else{

        [...customer.transactions]
        .reverse()
        .forEach(t=>{

            const isDebt=t.type==="debt";

            html+=`
                <div class="history-item">

                    <strong>
                        ${isDebt ? "💰 Borç" : "💵 Ödeme"}
                        ${money(t.amount)}
                    </strong>

                    <div>${escapeHtml(t.description || "")}</div>

                    <small>${t.date}</small>

                </div>
            `;
        });
    }

    html+=`</div>`;

    if(balance===0 && customer.transactions.length>0){

        html+=`
            <button
                class="btn-red"
                style="width:100%;margin-top:15px;"
                onclick="deleteCustomer(${customer.id})">
                🗑️ Müşteriyi Sil
            </button>
        `;
    }

    document.getElementById("detailContent").innerHTML=html;

    openModal("detailModal");
}

function deleteCustomer(id){

    const customer =
        customers.find(c=>c.id===id);

    if(!customer) return;

    if(getBalance(customer)>0){
        alert("Borcu bulunan müşteri silinemez.");
        return;
    }

    if(confirm(customer.name+" adlı müşteriyi silmek istediğine emin misin?")){

        customers =
            customers.filter(c=>c.id!==id);

        saveData();
        renderAll();

        closeModal("detailModal");
    }
}

function clearAllData(){

    if(customers.length===0){
        alert("Silinecek veri yok.");
        return;
    }

    const answer =
        prompt(
            "TÜM VERİLER SİLİNECEK!\n\nDevam etmek için SİL yaz:"
        );

    if(answer==="SİL"){

        customers=[];

        saveData();
        renderAll();

        alert("Tüm veriler silindi.");
    }
}

function updateStats(){

    let totalDebt=0;
    let debtors=0;
    let todayPayment=0;

    customers.forEach(c=>{

        const balance=getBalance(c);

        totalDebt+=balance;

        if(balance>0){
            debtors++;
        }

        c.transactions.forEach(t=>{

            if(
                t.type==="payment" &&
                t.date.startsWith(today())
            ){
                todayPayment+=Number(t.amount);
            }

        });

    });

    document.getElementById("totalDebt").textContent =
        money(totalDebt);

    document.getElementById("customerCount").textContent =
        debtors;

    document.getElementById("todayPayment").textContent =
        money(todayPayment);

    document.getElementById("totalCustomer").textContent =
        customers.length;
}

function renderAll(){

    updateStats();
    renderCustomers();
    fillCustomerSelects();
}

function escapeHtml(text){

    return String(text)
        .replaceAll("&","&amp;")
        .replaceAll("<","&lt;")
        .replaceAll(">","&gt;")
        .replaceAll('"',"&quot;")
        .replaceAll("'","&#039;");
}

renderAll();

</script>

</body>
</html>
```
