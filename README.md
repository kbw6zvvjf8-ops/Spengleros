# Spengleros
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#0f5b66">
<title>SpenglerOS</title>

<style>
:root{
  --bg:#edf2f4;
  --card:#ffffff;
  --text:#17212b;
  --muted:#697681;
  --primary:#0f5b66;
  --dark:#093f47;
  --light:#dceff1;
  --accent:#d48b2d;
  --accent-light:#fff0db;
  --danger:#b74747;
  --border:#d7e0e4;
}

*{box-sizing:border-box}

body{
  margin:0;
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Arial,sans-serif;
  background:var(--bg);
  color:var(--text);
}

.app{
  max-width:550px;
  min-height:100vh;
  margin:auto;
  padding-bottom:90px;
}

header{
  position:sticky;
  top:0;
  z-index:10;
  padding:20px 16px 24px;
  color:white;
  background:linear-gradient(135deg,var(--dark),var(--primary));
  border-radius:0 0 25px 25px;
}

header small{
  font-weight:800;
  letter-spacing:1.3px;
  opacity:.8;
}

header h1{
  margin:5px 0 3px;
}

header p{
  margin:0;
  font-size:13px;
  opacity:.9;
}

main{padding:14px}

.screen{display:none}
.screen.active{display:block}

.grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
}

.card,.item{
  background:var(--card);
  border:1px solid var(--border);
  border-radius:16px;
  padding:14px;
  margin-bottom:11px;
  box-shadow:0 7px 22px rgba(20,40,50,.07);
}

.card h3{
  margin:0 0 9px;
  color:var(--dark);
}

.item strong{
  display:block;
  margin-bottom:5px;
}

.item p{
  margin:3px 0;
  color:var(--muted);
  font-size:13px;
}

.metric{
  font-size:25px;
  font-weight:850;
  margin-top:8px;
}

label{
  display:block;
  margin:11px 0 5px;
  font-size:13px;
  font-weight:800;
}

input,select,textarea{
  width:100%;
  padding:11px;
  border:1px solid var(--border);
  border-radius:11px;
  background:white;
  font-size:15px;
}

textarea{
  min-height:85px;
  resize:vertical;
}

.row{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:9px;
}

.btn{
  width:100%;
  margin-top:10px;
  padding:12px;
  border:0;
  border-radius:12px;
  color:white;
  font-weight:800;
  font-size:14px;
  background:linear-gradient(135deg,var(--dark),var(--primary));
}

.btn.secondary{
  color:#845212;
  background:var(--accent-light);
  border:1px solid #edca96;
}

.btn.danger{
  background:var(--danger);
}

.tabs{
  display:flex;
  gap:7px;
  overflow:auto;
  margin-bottom:11px;
}

.tab{
  white-space:nowrap;
  padding:8px 12px;
  border:1px solid var(--border);
  border-radius:999px;
  background:white;
  font-weight:750;
  color:var(--muted);
}

.tab.active{
  color:white;
  background:var(--primary);
}

.sub{display:none}
.sub.active{display:block}

.chips{
  display:flex;
  flex-wrap:wrap;
  gap:7px;
  margin-top:10px;
}

.chip{
  padding:8px 11px;
  border:1px solid var(--border);
  border-radius:999px;
  background:white;
  color:var(--primary);
  font-weight:800;
}

.chip.active{
  background:var(--primary);
  color:white;
}

.result{
  margin-top:12px;
  padding:12px;
  line-height:1.5;
  border:1px solid #c7e1e4;
  border-radius:13px;
  background:#eef8f9;
}

.note{
  color:var(--muted);
  font-size:12px;
}

table{
  width:100%;
  border-collapse:collapse;
  font-size:13px;
}

td,th{
  padding:8px 3px;
  border-bottom:1px solid var(--border);
  text-align:left;
}

td:last-child,th:last-child{
  text-align:right;
}

nav{
  position:fixed;
  left:50%;
  bottom:0;
  transform:translateX(-50%);
  width:min(550px,100%);
  display:grid;
  grid-template-columns:repeat(5,1fr);
  padding:8px 4px calc(10px + env(safe-area-inset-bottom));
  background:rgba(255,255,255,.98);
  border-top:1px solid var(--border);
}

nav button{
  padding:6px 2px;
  border:0;
  border-radius:11px;
  background:transparent;
  color:#75838d;
  font-size:11px;
}

nav button span{
  display:block;
  font-size:20px;
}

nav button.active{
  color:var(--primary);
  background:var(--light);
  font-weight:800;
}

@media(max-width:390px){
  .grid,.row{grid-template-columns:1fr}
}
</style>
</head>

<body>
<div class="app">

<header>
  <small>DIGITALES HANDWERKERBÜRO</small>
  <h1>SpenglerOS</h1>
  <p>Rapport schreiben – Rechnung automatisch erstellen</p>
</header>

<main>

<section id="home" class="screen active">
  <div class="grid">
    <div class="card">
      <h3>Kunden</h3>
      <div id="countCustomers" class="metric">0</div>
    </div>

    <div class="card">
      <h3>Aufträge</h3>
      <div id="countOrders" class="metric">0</div>
    </div>

    <div class="card">
      <h3>Rapporte</h3>
      <div id="countReports" class="metric">0</div>
    </div>

    <div class="card">
      <h3>Rechnungen</h3>
      <div id="countInvoices" class="metric">0</div>
    </div>
  </div>

  <div class="card">
    <h3>Schnellstart</h3>
    <button class="btn" onclick="goTo('customers',1)">
      Neuen Kunden anlegen
    </button>

    <button class="btn secondary" onclick="goTo('report',3)">
      Rapport schreiben
    </button>
  </div>

  <div class="card">
    <h3>Speicherung</h3>
    <p class="note">
      Die eingegebenen Daten werden lokal in deinem Browser gespeichert.
      Verwende zunächst nur Testdaten.
    </p>
  </div>
</section>

<section id="customers" class="screen">
  <div class="tabs">
    <button class="tab active"
      onclick="showSub('customerListArea',this,'customers')">
      Kunden
    </button>

    <button class="tab"
      onclick="showSub('customerNewArea',this,'customers')">
      Neuer Kunde
    </button>
  </div>

  <div id="customerListArea" class="sub active">
    <div id="customerList"></div>
  </div>

  <div id="customerNewArea" class="sub">
    <div class="card">
      <h3>Neuer Kunde</h3>

      <label>Name oder Firma</label>
      <input id="customerName">

      <label>Adresse</label>
      <input id="customerAddress">

      <label>Telefon</label>
      <input id="customerPhone">

      <label>E-Mail</label>
      <input id="customerEmail">

      <button class="btn" onclick="addCustomer()">
        Kunde speichern
      </button>
    </div>
  </div>
</section>

<section id="orders" class="screen">
  <div class="tabs">
    <button class="tab active"
      onclick="showSub('orderListArea',this,'orders')">
      Aufträge
    </button>

    <button class="tab"
      onclick="showSub('orderNewArea',this,'orders')">
      Neuer Auftrag
    </button>
  </div>

  <div id="orderListArea" class="sub active">
    <div id="orderList"></div>
  </div>

  <div id="orderNewArea" class="sub">
    <div class="card">
      <h3>Neuer Auftrag</h3>

      <label>Kunde</label>
      <select id="orderCustomer"></select>

      <label>Bezeichnung</label>
      <input id="orderTitle"
        placeholder="z. B. Dachrinne erneuern">

      <label>Beschreibung</label>
      <textarea id="orderDescription"></textarea>

      <label>Status</label>
      <select id="orderStatus">
        <option>Geplant</option>
        <option>In Arbeit</option>
        <option>Abgeschlossen</option>
      </select>

      <button class="btn" onclick="addOrder()">
        Auftrag speichern
      </button>
    </div>
  </div>
</section>

<section id="report" class="screen">
  <div class="card">
    <h3>Rapport erstellen</h3>

    <label>Auftrag</label>
    <select id="reportOrder"></select>

    <label>Ausgeführte Arbeiten</label>
    <textarea id="reportText"
      placeholder="Was wurde auf der Baustelle gemacht?"></textarea>

    <div class="row">
      <div>
        <label>Mitarbeiter</label>
        <input id="workers" type="number" value="2">
      </div>

      <div>
        <label>Stunden je Mitarbeiter</label>
        <input id="hours" type="number" value="5">
      </div>
    </div>

    <div class="row">
      <div>
        <label>Stundenlohn netto</label>
        <input id="hourlyRate" type="number" value="58">
      </div>

      <div>
        <label>Fahrtkosten netto</label>
        <input id="travelCost" type="number" value="35">
      </div>
    </div>
  </div>

  <div class="card">
    <h3>Lieferantenrechnung</h3>

    <label>Rechnung fotografieren oder auswählen</label>
    <input type="file" accept="image/*,.pdf">

    <p class="note">
      In dieser Version überträgst du die Positionen und Einkaufspreise
      noch manuell aus der Rechnung.
    </p>

    <div id="materialRows"></div>

    <button class="btn secondary" onclick="addMaterialRow()">
      + Materialposition
    </button>
  </div>

  <div class="card">
    <h3>Materialaufschlag</h3>

    <div class="chips">
      <button class="chip" onclick="setMarkup(5,this)">5 %</button>
      <button class="chip" onclick="setMarkup(10,this)">10 %</button>
      <button class="chip active" onclick="setMarkup(25,this)">25 %</button>
      <button class="chip" onclick="setMarkup(50,this)">50 %</button>
      <button class="chip" onclick="setMarkup(75,this)">75 %</button>
      <button class="chip" onclick="setMarkup(100,this)">100 %</button>
    </div>

    <label>Eigener Aufschlag in Prozent</label>
    <input id="customMarkup"
      type="number"
      placeholder="z. B. 35"
      oninput="setCustomMarkup()">

    <div id="materialSummary" class="result"></div>
  </div>

  <button class="btn" onclick="createInvoice()">
    Rapport speichern und Rechnung erstellen
  </button>
</section>

<section id="invoices" class="screen">
  <div id="invoiceList"></div>
</section>

<section id="settings" class="screen">
  <div class="card">
    <h3>Firmendaten</h3>

    <label>Firmenname</label>
    <input id="companyName">

    <label>Firmenadresse</label>
    <input id="companyAddress">

    <label>Nächste Rechnungsnummer</label>
    <input id="nextInvoiceNumber" type="number">

    <button class="btn" onclick="saveCompanySettings()">
      Einstellungen speichern
    </button>
  </div>

  <div class="card">
    <h3>Datensicherung</h3>

    <button class="btn secondary" onclick="exportData()">
      Sicherung herunterladen
    </button>

    <button class="btn danger" onclick="deleteAllData()">
      Alle Daten löschen
    </button>
  </div>
</section>

</main>

<nav>
  <button class="active" onclick="showScreen('home',this)">
    <span>⌂</span>Start
  </button>

  <button onclick="showScreen('customers',this)">
    <span>👤</span>Kunden
  </button>

  <button onclick="showScreen('orders',this)">
    <span>📁</span>Aufträge
  </button>

  <button onclick="showScreen('report',this)">
    <span>📝</span>Rapport
  </button>

  <button onclick="showScreen('invoices',this)">
    <span>🧾</span>Rechnungen
  </button>
</nav>

</div>

<script>
const defaultData = {
  customers: [],
  orders: [],
  reports: [],
  invoices: [],
  settings: {
    companyName: "Mein Spenglerbetrieb",
    companyAddress: "",
    nextInvoiceNumber: 1001
  }
};

let data =
  JSON.parse(localStorage.getItem("spenglerosData")) ||
  defaultData;

let markup = 25;

function saveData(){
  localStorage.setItem(
    "spenglerosData",
    JSON.stringify(data)
  );

  renderEverything();
}

function euro(value){
  return new Intl.NumberFormat("de-DE",{
    style:"currency",
    currency:"EUR"
  }).format(value || 0);
}

function showScreen(id,button){
  document.querySelectorAll(".screen").forEach(screen => {
    screen.classList.remove("active");
  });

  document.getElementById(id).classList.add("active");

  document.querySelectorAll("nav button").forEach(btn => {
    btn.classList.remove("active");
  });

  if(button){
    button.classList.add("active");
  }

  renderEverything();
}

function goTo(id,index){
  const button = document.querySelectorAll("nav button")[index];
  showScreen(id,button);
}

function showSub(id,button,parentId){
  document.querySelectorAll("#"+parentId+" .sub").forEach(area => {
    area.classList.remove("active");
  });

  document.getElementById(id).classList.add("active");

  button.parentElement.querySelectorAll(".tab").forEach(tab => {
    tab.classList.remove("active");
  });

  button.classList.add("active");
}

function addCustomer(){
  const name = customerName.value.trim();

  if(!name){
    alert("Bitte einen Kundennamen eingeben.");
    return;
  }

  data.customers.push({
    id: Date.now(),
    name: name,
    address: customerAddress.value,
    phone: customerPhone.value,
    email: customerEmail.value
  });

  customerName.value = "";
  customerAddress.value = "";
  customerPhone.value = "";
  customerEmail.value = "";

  saveData();
  alert("Kunde wurde gespeichert.");
}

function addOrder(){
  if(!orderCustomer.value || !orderTitle.value.trim()){
    alert("Bitte Kunde und Auftragsbezeichnung eingeben.");
    return;
  }

  data.orders.push({
    id: Date.now(),
    customerId: Number(orderCustomer.value),
    title: orderTitle.value.trim(),
    description: orderDescription.value,
    status: orderStatus.value
  });

  orderTitle.value = "";
  orderDescription.value = "";

  saveData();
  alert("Auftrag wurde gespeichert.");
}

function addMaterialRow(
  name="",
  quantity=1,
  unit="Stk.",
  purchasePrice=0
){
  const row = document.createElement("div");
  row.className = "item material-row";

  row.innerHTML = `
    <label>Materialbezeichnung</label>
    <input class="material-name" value="${name}">

    <div class="row">
      <div>
        <label>Menge</label>
        <input class="material-quantity"
          type="number"
          step="0.01"
          value="${quantity}"
          oninput="updateMaterialSummary()">
      </div>

      <div>
        <label>Einheit</label>
        <input class="material-unit" value="${unit}">
      </div>
    </div>

    <label>Einkaufspreis je Einheit netto</label>
    <input class="material-price"
      type="number"
      step="0.01"
      value="${purchasePrice}"
      oninput="updateMaterialSummary()">

    <button class="btn danger"
      onclick="this.closest('.material-row').remove();
      updateMaterialSummary()">
      Position löschen
    </button>
  `;

  materialRows.appendChild(row);
  updateMaterialSummary();
}

function getMaterials(){
  return [...document.querySelectorAll(".material-row")]
    .map(row => ({
      name:
        row.querySelector(".material-name").value ||
        "Material",

      quantity:
        Number(row.querySelector(".material-quantity").value) ||
        0,

      unit:
        row.querySelector(".material-unit").value ||
        "Stk.",

      purchasePrice:
        Number(row.querySelector(".material-price").value) ||
        0
    }));
}

function setMarkup(value,button){
  markup = value;
  customMarkup.value = "";

  document.querySelectorAll(".chip").forEach(chip => {
    chip.classList.remove("active");
  });

  button.classList.add("active");
  updateMaterialSummary();
}

function setCustomMarkup(){
  markup = Number(customMarkup.value) || 0;

  document.querySelectorAll(".chip").forEach(chip => {
    chip.classList.remove("active");
  });

  updateMaterialSummary();
}

function updateMaterialSummary(){
  const materials = getMaterials();

  const purchaseTotal = materials.reduce(
    (sum,item) =>
      sum + item.quantity * item.purchasePrice,
    0
  );

  const saleTotal =
    purchaseTotal * (1 + markup / 100);

  const materialProfit =
    saleTotal - purchaseTotal;

  materialSummary.innerHTML = `
    Material-Einkauf:
    <strong>${euro(purchaseTotal)}</strong><br>

    Aufschlag:
    <strong>${markup} %</strong><br>

    Material-Verkauf:
    <strong>${euro(saleTotal)}</strong><br>

    Material-Rohertrag:
    <strong>${euro(materialProfit)}</strong>
  `;
}

function createInvoice(){
  if(!reportOrder.value){
    alert("Bitte zuerst einen Auftrag anlegen.");
    return;
  }

  const materials = getMaterials();

  const workerCount = Number(workers.value) || 0;
  const hoursEach = Number(hours.value) || 0;
  const rate = Number(hourlyRate.value) || 0;
  const travel = Number(travelCost.value) || 0;

  const labor =
    workerCount * hoursEach * rate;

  const materialPurchase = materials.reduce(
    (sum,item) =>
      sum + item.quantity * item.purchasePrice,
    0
  );

  const materialSale =
    materialPurchase * (1 + markup / 100);

  const net =
    labor + materialSale + travel;

  const vat = net * 0.19;
  const gross = net + vat;

  const report = {
    id: Date.now(),
    orderId: Number(reportOrder.value),
    text: reportText.value,
    workerCount,
    hoursEach,
    rate,
    travel,
    materials,
    markup,
    date: new Date().toISOString()
  };

  data.reports.push(report);

  const invoice = {
    id: Date.now() + 1,
    number: data.settings.nextInvoiceNumber,
    orderId: Number(reportOrder.value),
    reportId: report.id,
    labor,
    materialPurchase,
    materialSale,
    travel,
    materials,
    markup,
    net,
    vat,
    gross,
    date: new Date().toISOString()
  };

  data.settings.nextInvoiceNumber++;
  data.invoices.push(invoice);

  saveData();

  alert(
    "Rapport gespeichert und Rechnung erstellt."
  );

  goTo("invoices",4);
}

function renderCustomers(){
  customerList.innerHTML =
    data.customers.length
    ? data.customers.map(customer => `
      <div class="item">
        <strong>${customer.name}</strong>
        <p>${customer.address || ""}</p>
        <p>${customer.phone || ""}</p>
        <p>${customer.email || ""}</p>
      </div>
    `).join("")
    : `<p class="note">Noch keine Kunden gespeichert.</p>`;

  orderCustomer.innerHTML =
    data.customers.map(customer => `
      <option value="${customer.id}">
        ${customer.name}
      </option>
    `).join("");
}

function renderOrders(){
  orderList.innerHTML =
    data.orders.length
    ? data.orders.map(order => {
      const customer = data.customers.find(
        item => item.id === order.customerId
      );

      return `
        <div class="item">
          <strong>${order.title}</strong>
          <p>${customer ? customer.name : ""}</p>
          <p>${order.description || ""}</p>
          <p>Status: ${order.status}</p>
        </div>
      `;
    }).join("")
    : `<p class="note">Noch keine Aufträge gespeichert.</p>`;

  reportOrder.innerHTML =
    data.orders.map(order => `
      <option value="${order.id}">
        ${order.title}
      </option>
    `).join("");
}

function renderInvoices(){
  invoiceList.innerHTML =
    data.invoices.length
    ? data.invoices.slice().reverse().map(invoice => {
      const order = data.orders.find(
        item => item.id === invoice.orderId
      );

      const customer = order
        ? data.customers.find(
            item => item.id === order.customerId
          )
        : null;

      return `
        <div class="card">
          <h3>Rechnung ${invoice.number}</h3>

          <p>
            ${customer ? customer.name : ""}
            ·
            ${order ? order.title : ""}
          </p>

          <p class="note">
            ${new Date(invoice.date)
              .toLocaleDateString("de-DE")}
          </p>

          <table>
            <tr>
              <td>Arbeitszeit</td>
              <td>${euro(invoice.labor)}</td>
            </tr>

            <tr>
              <td>
                Material
                <br>
                <span class="note">
                  ${invoice.markup} % Aufschlag
                </span>
              </td>
              <td>${euro(invoice.materialSale)}</td>
            </tr>

            <tr>
              <td>Fahrtkosten</td>
              <td>${euro(invoice.travel)}</td>
            </tr>

            <tr>
              <td>Netto</td>
              <td>${euro(invoice.net)}</td>
            </tr>

            <tr>
              <td>19 % MwSt.</td>
              <td>${euro(invoice.vat)}</td>
            </tr>

            <tr>
              <th>Gesamt</th>
              <th>${euro(invoice.gross)}</th>
            </tr>
          </table>

          <button class="btn secondary"
            onclick="window.print()">
            Drucken oder als PDF sichern
          </button>
        </div>
      `;
    }).join("")
    : `<p class="note">Noch keine Rechnungen erstellt.</p>`;
}

function saveCompanySettings(){
  data.settings.companyName =
    companyName.value;

  data.settings.companyAddress =
    companyAddress.value;

  data.settings.nextInvoiceNumber =
    Number(nextInvoiceNumber.value) || 1001;

  saveData();
  alert("Einstellungen gespeichert.");
}

function exportData(){
  const file = new Blob(
    [JSON.stringify(data,null,2)],
    {type:"application/json"}
  );

  const url = URL.createObjectURL(file);
  const link = document.createElement("a");

  link.href = url;
  link.download = "spengleros-sicherung.json";
  link.click();

  URL.revokeObjectURL(url);
}

function deleteAllData(){
  if(!confirm(
    "Möchtest du wirklich alle Daten löschen?"
  )){
    return;
  }

  localStorage.removeItem("spenglerosData");
  location.reload();
}

function renderEverything(){
  countCustomers.textContent =
    data.customers.length;

  countOrders.textContent =
    data.orders.length;

  countReports.textContent =
    data.reports.length;

  countInvoices.textContent =
    data.invoices.length;

  renderCustomers();
  renderOrders();
  renderInvoices();

  companyName.value =
    data.settings.companyName;

  companyAddress.value =
    data.settings.companyAddress;

  nextInvoiceNumber.value =
    data.settings.nextInvoiceNumber;
}

addMaterialRow(
  "Zinkrinne 333",
  8,
  "m",
  28.40
);

addMaterialRow(
  "Ablaufstutzen",
  2,
  "Stk.",
  19.90
);

renderEverything();
</script>
</body>
</html>
