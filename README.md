<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Panificados del Sur</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:sans-serif}
body{background:#fdf8f0;min-height:100vh}
.header{background:linear-gradient(135deg,#b45309,#d97706);color:white;padding:16px 20px}
.header-top{display:flex;align-items:center;gap:10px;margin-bottom:4px}
.header h1{font-size:20px;font-weight:bold}
.header p{font-size:12px;opacity:.85}
.tabs{display:flex;gap:4px;margin-top:12px}
.tab{padding:8px 20px;border:none;cursor:pointer;border-radius:8px 8px 0 0;font-size:14px;font-weight:600;transition:all .2s}
.tab.active{background:white;color:#b45309}
.tab.inactive{background:rgba(255,255,255,0.15);color:white}
.container{max-width:700px;margin:0 auto;padding:16px}
.stats{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-bottom:16px}
.stat{background:white;border-radius:10px;padding:12px 16px;box-shadow:0 1px 4px rgba(0,0,0,0.07);display:flex;align-items:center;gap:10px}
.stat-icon{font-size:22px}
.stat-val{font-size:20px;font-weight:bold;color:#1f2937}
.stat-lbl{font-size:11px;color:#6b7280}
.toolbar{display:flex;gap:8px;margin-bottom:12px}
.toolbar input{flex:1;border:1px solid #e2e8f0;border-radius:8px;padding:8px 14px;font-size:14px;outline:none;background:#f8fafc}
.toolbar input:focus{border-color:#d97706;box-shadow:0 0 0 2px #fde68a}
.btn-primary{background:linear-gradient(135deg,#b45309,#d97706);color:white;border:none;border-radius:8px;padding:8px 18px;cursor:pointer;font-weight:600;font-size:14px;white-space:nowrap}
.card{background:white;border-radius:12px;padding:14px 18px;box-shadow:0 1px 4px rgba(0,0,0,0.07);margin-bottom:10px}
.card-top{display:flex;justify-content:space-between;align-items:flex-start}
.card-nombre{font-weight:bold;color:#1f2937;font-size:15px}
.card-sub{font-size:12px;color:#6b7280;margin-top:2px}
.card-actions{display:flex;gap:6px}
.btn-icon{background:none;border:1px solid #e2e8f0;border-radius:8px;padding:6px 10px;cursor:pointer;font-size:14px}
.btn-wsp{color:#25D366}
.btn-pdf{color:#0ea5e9}
.btn-del{color:#ef4444}
.badge{display:inline-block;padding:2px 8px;border-radius:12px;font-size:11px;font-weight:600;color:white}
.empty{text-align:center;padding:40px;color:#9ca3af;font-size:15px}
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.4);display:flex;align-items:center;justify-content:center;z-index:100;padding:16px}
.modal{background:white;border-radius:16px;padding:24px;width:100%;max-width:480px;max-height:90vh;overflow-y:auto}
.modal h2{font-weight:bold;color:#1f2937;margin-bottom:16px;font-size:17px}
.label{font-size:12px;color:#64748b;display:block;margin-bottom:4px;font-weight:600;margin-top:10px}
.input{width:100%;border:1px solid #e2e8f0;border-radius:8px;padding:8px 12px;font-size:14px;outline:none;background:#f8fafc;font-family:inherit}
.input:focus{border-color:#d97706;box-shadow:0 0 0 2px #fde68a}
.select{width:100%;border:1px solid #e2e8f0;border-radius:8px;padding:8px 12px;font-size:14px;outline:none;background:#f8fafc}
.btn-row{display:flex;gap:8px;margin-top:16px}
.btn-row button{flex:1;padding:10px;border-radius:8px;font-weight:600;font-size:14px;cursor:pointer;border:none}
.btn-save{background:linear-gradient(135deg,#b45309,#d97706);color:white}
.btn-cancel{background:#f1f5f9;color:#475569;border:1px solid #e2e8f0!important}
.items-table{width:100%;border-collapse:collapse;margin-top:8px;font-size:13px}
.items-table th{text-align:left;padding:6px 8px;color:#64748b;font-weight:600;border-bottom:1px solid #e2e8f0}
.items-table td{padding:6px 4px;border-bottom:1px solid #f0f0f0;vertical-align:middle}
.items-table input{width:100%;border:1px solid #e2e8f0;border-radius:6px;padding:4px 6px;font-size:13px;outline:none;background:#f8fafc}
.total-row{display:flex;justify-content:flex-end;padding:10px 0;font-weight:bold;color:#b45309;font-size:15px}
.btn-add-item{background:#fef3c7;color:#b45309;border:1px solid #fde68a;border-radius:6px;padding:4px 12px;cursor:pointer;font-size:13px;font-weight:600;margin-top:6px}
.toast{position:fixed;bottom:24px;left:50%;transform:translateX(-50%);background:#1f2937;color:white;padding:10px 20px;border-radius:10px;font-size:14px;z-index:200;animation:fadeIn .2s}
@keyframes fadeIn{from{opacity:0;transform:translateX(-50%) translateY(10px)}to{opacity:1;transform:translateX(-50%) translateY(0)}}
.loading{display:flex;flex-direction:column;align-items:center;justify-content:center;height:60vh;gap:12px;font-size:16px;color:#6b7280}
.pres-info{display:flex;gap:12px;font-size:12px;color:#6b7280;margin-top:4px}
</style>
</head>
<body>

<div class="header">
  <div class="header-top">
    <span style="font-size:28px">🥐</span>
    <div>
      <h1>Panificados del Sur</h1>
      <p>Pueyrredón 362 · Adelia María, Córdoba</p>
    </div>
  </div>
  <div class="tabs">
    <button class="tab active" id="tabClientes" onclick="switchTab('clientes')">👥 Clientes</button>
    <button class="tab inactive" id="tabPresupuestos" onclick="switchTab('presupuestos')">📄 Presupuestos</button>
  </div>
</div>

<div class="container">
  <div id="statsArea"></div>
  <div class="toolbar">
    <input type="text" id="searchInput" placeholder="Buscar..." oninput="render()"/>
    <button class="btn-primary" onclick="abrirModal()">+ Nuevo</button>
  </div>
  <div id="listaArea"></div>
</div>

<div id="modalArea"></div>
<div id="toastArea"></div>

<script>
let tabActual = "clientes";

const STORAGE_CLI = "panificados:clientes";
const STORAGE_PRE = "panificados:presupuestos";

const clientesDefault = [
  {id:"c1", nombre:"Supermercado El Sol", telefono:"3585-123456", direccion:"Av. San Martín 100", email:"elsol@mail.com", creado:"2024-01-10"}
];
const presupuestosDefault = [
  {id:"p1", clienteId:"c1", numero:"001", fecha:"2024-06-01", estado:"aprobado", items:[{desc:"Pan francés x100", qty:2, precio:1500}], total:3000}
];

let clientes = JSON.parse(localStorage.getItem(STORAGE_CLI) || JSON.stringify(clientesDefault));
let presupuestos = JSON.parse(localStorage.getItem(STORAGE_PRE) || JSON.stringify(presupuestosDefault));

function guardarStorage() {
  localStorage.setItem(STORAGE_CLI, JSON.stringify(clientes));
  localStorage.setItem(STORAGE_PRE, JSON.stringify(presupuestos));
}

const ESTADO_COLOR = {pendiente:"#f59e0b", aprobado:"#22c55e", rechazado:"#ef4444", facturado:"#6366f1"};
const genId = () => Math.random().toString(36).slice(2,9);
const today = () => new Date().toISOString().slice(0,10);
const fmt = n => Number(n).toLocaleString("es-AR",{style:"currency",currency:"ARS"});

function switchTab(tab) {
  tabActual = tab;
  document.getElementById("tabClientes").className = "tab " + (tab==="clientes"?"active":"inactive");
  document.getElementById("tabPresupuestos").className = "tab " + (tab==="presupuestos"?"active":"inactive");
  document.getElementById("searchInput").value = "";
  document.getElementById("searchInput").placeholder = `Buscar ${tab}...`;
  render();
}

function showToast(msg) {
  const t = document.getElementById("toastArea");
  t.innerHTML = `<div class="toast">${msg}</div>`;
  setTimeout(()=>t.innerHTML="", 2500);
}

function render() {
  renderStats();
  if(tabActual==="clientes") renderClientes();
  else renderPresupuestos();
}

function renderStats() {
  const totalFact = presupuestos.filter(p=>p.estado==="aprobado").reduce((s,p)=>s+p.total,0);
  document.getElementById("statsArea").innerHTML = `
    <div class="stats">
      <div class="stat"><span class="stat-icon">👥</span><div><div class="stat-val">${clientes.length}</div><div class="stat-lbl">Clientes</div></div></div>
      <div class="stat"><span class="stat-icon">📄</span><div><div class="stat-val">${presupuestos.length}</div><div class="stat-lbl">Presupuestos</div></div></div>
      <div class="stat"><span class="stat-icon">✅</span><div><div class="stat-val">${presupuestos.filter(p=>p.estado==="aprobado").length}</div><div class="stat-lbl">Aprobados</div></div></div>
      <div class="stat"><span class="stat-icon">💰</span><div><div class="stat-val" style="font-size:14px">${fmt(totalFact)}</div><div class="stat-lbl">Total facturado</div></div></div>
    </div>
  `;
}

function renderClientes() {
  const busq = document.getElementById("searchInput").value.toLowerCase();
  const filtrados = clientes.filter(c => c.nombre.toLowerCase().includes(busq) || c.telefono?.includes(busq) || c.email?.toLowerCase().includes(busq));
  if(!filtrados.length){ document.getElementById("listaArea").innerHTML=`<div class="empty">😕 No hay clientes</div>`; return; }
  document.getElementById("listaArea").innerHTML = filtrados.map(c => `
    <div class="card">
      <div class="card-top">
        <div>
          <div class="card-nombre">${c.nombre}</div>
          <div class="card-sub">
            ${c.telefono?`📞 ${c.telefono} &nbsp;`:""}
            ${c.email?`✉️ ${c.email} &nbsp;`:""}
            ${c.direccion?`📍 ${c.direccion}`:""}
          </div>
          <div class="card-sub" style="margin-top:4px">Presupuestos: ${presupuestos.filter(p=>p.clienteId===c.id).length}</div>
        </div>
        <div class="card-actions">
          <button class="btn-icon" onclick="editarCliente('${c.id}')">✏️</button>
          <button class="btn-icon btn-del" onclick="borrarCliente('${c.id}')">🗑️</button>
        </div>
      </div>
    </div>
  `).join("");
}

function renderPresupuestos() {
  const busq = document.getElementById("searchInput").value.toLowerCase();
  const filtrados = presupuestos.filter(p => {
    const cl = clientes.find(c=>c.id===p.clienteId);
    return cl?.nombre.toLowerCase().includes(busq) || p.numero?.includes(busq) || p.estado?.includes(busq);
  });
  if(!filtrados.length){ document.getElementById("listaArea").innerHTML=`<div class="empty">😕 No hay presupuestos</div>`; return; }
  document.getElementById("listaArea").innerHTML = filtrados.map(p => {
    const cl = clientes.find(c=>c.id===p.clienteId);
    return `
    <div class="card">
      <div class="card-top">
        <div>
          <div style="display:flex;align-items:center;gap:8px">
            <span class="card-nombre">Presupuesto #${p.numero}</span>
            <span class="badge" style="background:${ESTADO_COLOR[p.estado]||'#888'}">${p.estado.charAt(0).toUpperCase()+p.estado.slice(1)}</span>
          </div>
          <div class="pres-info">
            <span>👤 ${cl?.nombre||"Cliente eliminado"}</span>
            <span>📅 ${p.fecha}</span>
            <span>${p.items.length} ítem${p.items.length!==1?"s":""}</span>
          </div>
          <div style="font-weight:700;color:#b45309;margin-top:4px">${fmt(p.total)}</div>
        </div>
        <div class="card-actions" style="flex-wrap:wrap;gap:4px;max-width:120px">
          <button class="btn-icon btn-wsp" onclick="enviarWsp('${p.id}')" title="WhatsApp">📲</button>
          <button class="btn-icon btn-pdf" onclick="descargarPDF('${p.id}')" title="PDF">⬇️</button>
          <button class="btn-icon" onclick="editarPres('${p.id}')">✏️</button>
          <button class="btn-icon btn-del" onclick="borrarPres('${p.id}')">🗑️</button>
        </div>
      </div>
    </div>
  `}).join("");
}

// CLIENTES
function abrirModal() {
  if(tabActual==="clientes") modalNuevoCliente();
  else modalNuevoPres();
}

function modalNuevoCliente(c=null) {
  document.getElementById("modalArea").innerHTML = `
    <div class="modal-overlay" onclick="if(event.target===this)cerrarModal()">
      <div class="modal">
        <h2>${c?"Editar Cliente":"Nuevo Cliente"}</h2>
        ${[["nombre","Nombre / Razón Social",c?.nombre||""],["telefono","Teléfono",c?.telefono||""],["direccion","Dirección",c?.direccion||""],["email","Email",c?.email||""]].map(([k,l,v])=>`
          <label class="label">${l}</label>
          <input class="input" id="cl_${k}" value="${v}" placeholder="${l}"/>
        `).join("")}
        <div class="btn-row">
          <button class="btn-save" onclick="guardarCliente('${c?.id||""}')">Guardar</button>
          <button class="btn-cancel" onclick="cerrarModal()">Cancelar</button>
        </div>
      </div>
    </div>
  `;
}

function editarCliente(id) {
  const c = clientes.find(x=>x.id===id);
  modalNuevoCliente(c);
}

function guardarCliente(id) {
  const nombre = document.getElementById("cl_nombre").value.trim();
  if(!nombre) return alert("El nombre es obligatorio");
  const datos = {nombre, telefono:document.getElementById("cl_telefono").value, direccion:document.getElementById("cl_direccion").value, email:document.getElementById("cl_email").value};
  if(id) { clientes = clientes.map(c=>c.id===id?{...c,...datos}:c); }
  else { clientes.push({...datos, id:genId(), creado:today()}); }
  cerrarModal(); guardarStorage(); showToast("Cliente guardado ✓"); render();
}

function borrarCliente(id) {
  if(!confirm("¿Eliminar este cliente?")) return;
  clientes = clientes.filter(c=>c.id!==id);
  guardarStorage(); showToast("Cliente eliminado"); render();
}

// PRESUPUESTOS
let presItems = [];
let presEstado = "pendiente";

function modalNuevoPres(p=null) {
  presItems = p ? p.items.map(i=>({...i})) : [{desc:"",qty:1,precio:0}];
  presEstado = p?.estado || "pendiente";
  const nroSig = String(presupuestos.length+1).padStart(3,"0");
  document.getElementById("modalArea").innerHTML = `
    <div class="modal-overlay" onclick="if(event.target===this)cerrarModal()">
      <div class="modal" style="max-width:560px">
        <h2>${p?"Editar Presupuesto":"Nuevo Presupuesto"}</h2>
        <label class="label">Cliente *</label>
        <select class="select" id="pres_cliente">
          <option value="">-- Seleccionar --</option>
          ${clientes.map(c=>`<option value="${c.id}" ${p?.clienteId===c.id?"selected":""}>${c.nombre}</option>`).join("")}
        </select>
        <div style="display:flex;gap:12px">
          <div style="flex:1"><label class="label">Número</label><input class="input" id="pres_numero" value="${p?.numero||nroSig}"/></div>
          <div style="flex:1"><label class="label">Fecha</label><input class="input" type="date" id="pres_fecha" value="${p?.fecha||today()}"/></div>
          <div style="flex:1"><label class="label">Estado</label>
            <select class="select" id="pres_estado" onchange="presEstado=this.value">
              ${["pendiente","aprobado","rechazado","facturado"].map(e=>`<option value="${e}" ${(p?.estado||"pendiente")===e?"selected":""}>${e.charAt(0).toUpperCase()+e.slice(1)}</option>`).join("")}
            </select>
          </div>
        </div>
        <label class="label">Ítems</label>
        <div id="itemsContainer"></div>
        <button class="btn-add-item" onclick="agregarItem()">+ Agregar ítem</button>
        <div class="total-row" id="totalRow"></div>
        <div class="btn-row">
          <button class="btn-save" onclick="guardarPres('${p?.id||""}')">Guardar</button>
          <button class="btn-cancel" onclick="cerrarModal()">Cancelar</button>
        </div>
      </div>
    </div>
  `;
  renderItems();
}

function renderItems() {
  const container = document.getElementById("itemsContainer");
  if(!container) return;
  container.innerHTML = `
    <table class="items-table">
      <thead><tr><th>Descripción</th><th style="width:60px">Cant.</th><th style="width:90px">Precio</th><th style="width:30px"></th></tr></thead>
      <tbody>
        ${presItems.map((it,i)=>`
          <tr>
            <td><input class="input" value="${it.desc}" oninput="presItems[${i}].desc=this.value"/></td>
            <td><input class="input" type="number" value="${it.qty}" oninput="presItems[${i}].qty=Number(this.value);actualizarTotal()"/></td>
            <td><input class="input" type="number" value="${it.precio}" oninput="presItems[${i}].precio=Number(this.value);actualizarTotal()"/></td>
            <td><button onclick="quitarItem(${i})" style="background:none;border:none;color:#ef4444;cursor:pointer;font-size:16px">×</button></td>
          </tr>
        `).join("")}
      </tbody>
    </table>
  `;
  actualizarTotal();
}

function actualizarTotal() {
  const total = presItems.reduce((s,it)=>s+(it.qty*it.precio),0);
  const el = document.getElementById("totalRow");
  if(el) el.textContent = `Total: ${fmt(total)}`;
}

function agregarItem() { presItems.push({desc:"",qty:1,precio:0}); renderItems(); }
function quitarItem(i) { presItems.splice(i,1); renderItems(); }

function guardarPres(id) {
  const clienteId = document.getElementById("pres_cliente").value;
  if(!clienteId) return alert("Seleccioná un cliente");
  const total = presItems.reduce((s,it)=>s+(it.qty*it.precio),0);
  const datos = {
    clienteId,
    numero: document.getElementById("pres_numero").value,
    fecha: document.getElementById("pres_fecha").value,
    estado: document.getElementById("pres_estado").value,
    items: [...presItems],
    total
  };
  if(id) { presupuestos = presupuestos.map(p=>p.id===id?{...p,...datos}:p); }
  else { presupuestos.push({...datos, id:genId()}); }
  cerrarModal(); guardarStorage(); showToast("Presupuesto guardado ✓"); render();
}

function editarPres(id) { modalNuevoPres(presupuestos.find(p=>p.id===id)); }

function borrarPres(id) {
  if(!confirm("¿Eliminar este presupuesto?")) return;
  presupuestos = presupuestos.filter(p=>p.id!==id);
  guardarStorage(); showToast("Presupuesto eliminado"); render();
}

function cerrarModal() { document.getElementById("modalArea").innerHTML=""; }

function enviarWsp(id) {
  const p = presupuestos.find(x=>x.id===id);
  const cl = clientes.find(c=>c.id===p.clienteId);
  const tel = cl?.telefono?.replace(/\D/g,"")||"";
  const items = p.items.map(it=>`• ${it.desc} x${it.qty} = ${fmt(it.qty*it.precio)}`).join("\n");
  const msg = `🥐 *Panificados del Sur*\nPueyrredón 362 - Adelia María, Córdoba\n📞 3585 408466 | 3585 646244\n\n📄 *Presupuesto N° ${p.numero}*\n👤 Cliente: ${cl?.nombre||"-"}\n📅 Fecha: ${p.fecha}\n\n*Detalle:*\n${items}\n\n💰 *Total: ${fmt(p.total)}*\nEstado: ${p.estado.toUpperCase()}\n\nGracias por elegirnos! 🙌`;
  window.open(`https://wa.me/54${tel}?text=${encodeURIComponent(msg)}`,"_blank");
}

function descargarPDF(id) {
  const p = presupuestos.find(x=>x.id===id);
  const cl = clientes.find(c=>c.id===p.clienteId);
  const items = p.items.map(it=>`<tr><td>${it.desc}</td><td>${it.qty}</td><td>${fmt(it.precio)}</td><td>${fmt(it.qty*it.precio)}</td></tr>`).join("");
  const html = `<!DOCTYPE html><html><head><meta charset="UTF-8"><style>
    body{font-family:Arial,sans-serif;padding:40px;color:#222}
    .box{max-width:620px;margin:auto;border:2px solid #b45309;border-radius:12px;overflow:hidden}
    .hdr{background:linear-gradient(135deg,#b45309,#d97706);color:white;padding:24px 32px}
    .hdr h1{margin:0;font-size:22px}.hdr p{margin:4px 0 0;font-size:13px;opacity:.85}
    .body{padding:24px 32px}
    table{width:100%;border-collapse:collapse;margin-top:16px}
    th{background:#fef3c7;color:#b45309;padding:8px;text-align:left;font-size:13px}
    td{padding:8px;border-bottom:1px solid #f0f0f0;font-size:13px}
    .tot{text-align:right;font-size:17px;font-weight:700;color:#b45309;margin-top:12px}
    .ftr{text-align:center;padding:14px;font-size:12px;color:#aaa;border-top:1px solid #e5e7eb;margin-top:16px}
  </style></head><body><div class="box">
    <div class="hdr"><h1>🥐 Panificados del Sur</h1><p>Pueyrredón 362 · Adelia María, Córdoba · 📞 3585 408466</p></div>
    <div class="body">
      <p><strong>Presupuesto N° ${p.numero}</strong> · Fecha: ${p.fecha} · Estado: ${p.estado.toUpperCase()}</p>
      <p>👤 Cliente: ${cl?.nombre||"-"} ${cl?.telefono?`· 📞 ${cl.telefono}`:""}</p>
      <table><thead><tr><th>Descripción</th><th>Cant.</th><th>Precio Unit.</th><th>Subtotal</th></tr></thead><tbody>${items}</tbody></table>
      <div class="tot">Total: ${fmt(p.total)}</div>
    </div>
    <div class="ftr">Panificados del Sur · Adelia María, Córdoba · 3585 408466</div>
  </div></body></html>`;
  const blob = new Blob([html],{type:"text/html"});
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href=url; a.download=`Presupuesto_${p.numero}_${cl?.nombre||"cliente"}.html`; a.click();
  URL.revokeObjectURL(url);
  showToast("Presupuesto descargado ✓");
}

render();
</script>
</body>
</html>
