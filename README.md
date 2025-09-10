# Lisa-guest-<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Sunrise Guest House — Reception</title>
  <style>
    :root{
      --bg:#f4f7fb;
      --card:#ffffff;
      --accent:#2b6cb0;
      --accent-dark:#214f86;
      --ok:#16a34a;
      --danger:#ef4444;
      --muted:#6b7280;
      --glass: rgba(255,255,255,0.6);
      font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    html,body{height:100%}
    body{
      margin:0;
      background: linear-gradient(180deg, #eef6ff 0%, var(--bg) 100%);
      color:#0f172a;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      padding:24px;
      box-sizing:border-box;
    }
    header{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:16px;
      margin-bottom:18px;
    }
    .brand{
      display:flex;
      gap:12px;
      align-items:center;
    }
    .logo{
      width:56px;height:56px;border-radius:8px;
      background:linear-gradient(135deg,var(--accent),var(--accent-dark));
      color:white;display:flex;align-items:center;justify-content:center;font-weight:700;
      box-shadow:0 6px 18px rgba(33,79,134,0.12);
    }
    h1{font-size:20px;margin:0}
    .subtitle{color:var(--muted);font-size:13px}
    .controls{display:flex;gap:8px;align-items:center}
    button.btn{
      border:0;padding:8px 12px;border-radius:8px;background:var(--accent);color:white;cursor:pointer;
      font-weight:600;box-shadow:0 6px 12px rgba(43,108,176,0.12);
    }
    button.ghost{background:transparent;color:var(--accent);border:1px solid rgba(43,108,176,0.12);box-shadow:none}
    main{display:grid;grid-template-columns:360px 1fr;gap:18px;align-items:start}
    .left{
      background:var(--card);padding:16px;border-radius:12px;box-shadow:0 6px 30px rgba(15,23,42,0.04);
      height:calc(100vh - 128px);overflow:auto;
    }
    .right{
      background:var(--card);padding:16px;border-radius:12px;box-shadow:0 6px 30px rgba(15,23,42,0.04);
      height:calc(100vh - 128px);overflow:auto;
    }
    .stats{display:flex;gap:12px;margin-bottom:12px}
    .stat{flex:1;padding:12px;border-radius:10px;background:linear-gradient(180deg,var(--glass),#fff);box-shadow:inset 0 -1px 0 rgba(0,0,0,0.02)}
    .stat .num{font-size:20px;font-weight:700}
    .filter-row{display:flex;gap:8px;align-items:center;margin-bottom:12px}
    input[type="search"]{flex:1;padding:8px;border-radius:8px;border:1px solid #e6e8eb}
    .room-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:10px}
    .room{
      padding:10px;background:linear-gradient(180deg,#fff,var(--glass));border-radius:8px;border:1px solid rgba(15,23,42,0.03);
      display:flex;flex-direction:column;gap:6px;min-height:86px;justify-content:space-between;
    }
    .room .title{display:flex;justify-content:space-between;align-items:center;font-weight:700}
    .pill{font-size:12px;padding:4px 8px;border-radius:999px;background:#f3f4f6;color:#111}
    .vacant{background:#ecfeff;border:1px solid rgba(6,182,212,0.12);color:#0369a1}
    .occupied{background:#fff1f2;border:1px solid rgba(239,68,68,0.12);color:#9b1c1c}
    .room small{color:var(--muted)}
    .room .actions{display:flex;gap:6px}
    .btn-sm{padding:6px 8px;border-radius:8px;border:0;background:var(--accent);color:white;cursor:pointer;font-weight:600}
    .btn-green{background:var(--ok)}
    .btn-red{background:var(--danger)}
    /* modal */
    .modal-backdrop{position:fixed;inset:0;background:rgba(3,7,18,0.45);display:flex;align-items:center;justify-content:center;z-index:60}
    .modal{width:520px;background:white;padding:18px;border-radius:12px;box-shadow:0 40px 120px rgba(2,6,23,0.5)}
    label{display:block;font-size:13px;margin-top:10px;color:var(--muted)}
    input,select,textarea{width:100%;padding:8px;border-radius:8px;border:1px solid #e6e8eb;margin-top:6px;box-sizing:border-box}
    .log-table{width:100%;border-collapse:collapse;margin-top:12px}
    .log-table th, .log-table td{padding:8px;text-align:left;border-bottom:1px solid #f1f5f9;font-size:13px}
    .top-actions{display:flex;gap:8px;align-items:center}
    .note{font-size:13px;color:var(--muted);margin-top:10px}
    .room-details{margin-top:12px;padding-top:10px;border-top:1px dashed #eef2f7}
    .small{font-size:12px;color:var(--muted)}
    .csv-btn{background:transparent;border:1px dashed #cbd5e1;padding:8px;border-radius:8px;cursor:pointer}
    footer{margin-top:16px;color:var(--muted);font-size:13px;text-align:center}
    @media(max-width:980px){
      main{grid-template-columns:1fr;align-items:stretch}
      .room-grid{grid-template-columns:repeat(4,1fr)}
    }
    @media(max-width:640px){
      .room-grid{grid-template-columns:repeat(2,1fr)}
      .modal{width:92%}
    }
  </style>
</head>
<body>
  <header>
    <div class="brand">
      <div class="logo">SG</div>
      <div>
        <h1>Sunrise Guest House — Reception</h1>
        <div class="subtitle">Manage room allocation, check-ins, check-outs and logs</div>
      </div>
    </div>
    <div class="controls">
      <div class="top-actions">
        <button id="exportCsv" class="ghost btn">Export logs (CSV)</button>
        <button id="resetData" class="ghost btn">Reset data</button>
      </div>
    </div>
  </header>

  <main>
    <section class="left" aria-label="Overview & Filters">
      <div class="stats">
        <div class="stat">
          <div class="small">Total rooms</div>
          <div class="num" id="totalRooms">25</div>
        </div>
        <div class="stat">
          <div class="small">Occupied</div>
          <div class="num" id="occupiedCount">0</div>
        </div>
        <div class="stat">
          <div class="small">Vacant</div>
          <div class="num" id="vacantCount">25</div>
        </div>
      </div>

      <div class="filter-row">
        <input type="search" id="searchBox" placeholder="Search by guest name or room number" />
        <select id="filterStatus">
          <option value="all">All rooms</option>
          <option value="vacant">Vacant</option>
          <option value="occupied">Occupied</option>
        </select>
      </div>

      <div class="note">Click a room to allocate (check-in) or view details. Use "Export logs" to create a CSV report of all check-ins/outs.</div>

      <hr style="margin:12px 0;border:none;border-top:1px solid #f1f5f9" />

      <div id="roomGrid" class="room-grid" aria-live="polite"></div>

    </section>

    <section class="right" aria-label="Room details & log">
      <h2 style="margin:0 0 10px 0">Latest activity & logs</h2>
      <div id="latestActivity" class="small">No activity yet.</div>

      <div id="roomDetailCard" class="room-details" style="display:none">
        <div id="detailHeader"></div>
        <table class="log-table" id="roomLogTable">
          <thead>
            <tr><th>Room</th><th>Guest</th><th>Check-in</th><th>Check-out</th><th>Notes</th></tr>
          </thead>
          <tbody></tbody>
        </table>
      </div>

      <div style="margin-top:18px;">
        <h3 style="margin:0 0 8px 0">All bookings (most recent first)</h3>
        <table class="log-table" id="globalLogTable">
          <thead><tr><th>Time</th><th>Room</th><th>Guest</th><th>Action</th><th>Check-in</th><th>Check-out</th></tr></thead>
          <tbody></tbody>
        </table>
      </div>

      <footer>
        Built for a 25-room guest house · Data stored locally in your browser
      </footer>
    </section>
  </main>

  <!-- Modal -->
  <div id="modalBackdrop" class="modal-backdrop" style="display:none">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
      <h3 id="modalTitle">Allocate Room</h3>
      <form id="allocForm">
        <input type="hidden" id="modalRoomId" />
        <label for="guestName">Guest full name</label>
        <input id="guestName" required maxlength="100" />

        <label for="guestPhone">Phone (optional)</label>
        <input id="guestPhone" maxlength="30" />

        <label for="checkInTime">Check-in time (leave blank to use now)</label>
        <input id="checkInTime" type="datetime-local" />

        <label for="notes">Notes (optional)</label>
        <textarea id="notes" rows="3" maxlength="300"></textarea>

        <div style="display:flex;gap:8px;margin-top:12px;justify-content:flex-end">
          <button type="button" id="cancelModal" class="ghost btn">Cancel</button>
          <button type="submit" class="btn">Allocate room</button>
        </div>
      </form>
    </div>
  </div>

  <script>
    // --- Data model and persistence ---
    const STORAGE_KEY = 'sunrise_guesthouse_v1';

    function defaultState(){
      const rooms = [];
      for(let i=1;i<=25;i++){
        rooms.push({
          id: i,
          status: 'vacant', // or 'occupied'
          currentBooking: null, // object when occupied
          history: [] // array of booking objects {guestName,phone,checkInISO,checkOutISO,notes}
        });
      }
      return {
        rooms,
        logs: [] // global action logs {timestampISO,roomId,guestName,action,checkInISO,checkOutISO,notes}
      };
    }

    function loadState(){
      try{
        const raw = localStorage.getItem(STORAGE_KEY);
        if(!raw) return defaultState();
        const parsed = JSON.parse(raw);
        // basic validation
        if(!parsed.rooms || !Array.isArray(parsed.rooms)) return defaultState();
        return parsed;
      }catch(e){
        console.error('Failed to load state, resetting',e);
        return defaultState();
      }
    }
    function saveState(){
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    }

    let state = loadState();

    // --- Utilities ---
    function nowISO(){ return new Date().toISOString(); }
    function toLocalString(iso){ if(!iso) return ''; const d=new Date(iso); return d.toLocaleString(); }
    function findRoom(id){ return state.rooms.find(r=>r.id===id); }
    function pushLog(entry){
      state.logs.unshift(entry); // most recent first
      saveState();
      renderLatest();
      renderLogs();
    }

    // --- Render UI ---
    const roomGrid = document.getElementById('roomGrid');
    const totalRoomsEl = document.getElementById('totalRooms');
    const occupiedCountEl = document.getElementById('occupiedCount');
    const vacantCountEl = document.getElementById('vacantCount');
    const searchBox = document.getElementById('searchBox');
    const filterStatus = document.getElementById('filterStatus');
    const latestActivity = document.getElementById('latestActivity');
    const modalBackdrop = document.getElementById('modalBackdrop');
    const allocForm = document.getElementById('allocForm');
    const modalRoomId = document.getElementById('modalRoomId');
    const guestNameInput = document.getElementById('guestName');
    const guestPhoneInput = document.getElementById('guestPhone');
    const checkInTimeInput = document.getElementById('checkInTime');
    const notesInput = document.getElementById('notes');
    const roomDetailCard = document.getElementById('roomDetailCard');
    const detailHeader = document.getElementById('detailHeader');
    const roomLogTableBody = document.querySelector('#roomLogTable tbody');
    const globalLogTableBody = document.querySelector('#globalLogTable tbody');

    function renderRooms(){
      roomGrid.innerHTML = '';
      const q = (searchBox.value || '').trim().toLowerCase();
      const statusFilter = filterStatus.value;

      let occupied=0, vacant=0;
      state.rooms.forEach(room=>{
        if(room.status==='occupied') occupied++; else vacant++;
      });
      totalRoomsEl.textContent = state.rooms.length;
      occupiedCountEl.textContent = occupied;
      vacantCountEl.textContent = vacant;

      const filtered = state.rooms.filter(room=>{
        if(statusFilter==='vacant' && room.status!=='vacant') return false;
        if(statusFilter==='occupied' && room.status!=='occupied') return false;
        if(!q) return true;
        // search by room number or guest name
        if(String(room.id).includes(q)) return true;
        if(room.currentBooking && room.currentBooking.guestName && room.currentBooking.guestName.toLowerCase().includes(q)) return true;
        // also search history names
        if(room.history && room.history.some(h=> h.guestName && h.guestName.toLowerCase().includes(q))) return true;
        return false;
      });

      filtered.forEach(room=>{
        const el = document.createElement('div');
        el.className = 'room';
        const statusClass = room.status==='vacant' ? 'vacant' : 'occupied';
        el.innerHTML = `
          <div class="title">
            <div>Room ${room.id}</div>
            <div style="display:flex;gap:8px;align-items:center">
              <div class="pill ${statusClass}">${room.status.toUpperCase()}</div>
            </div>
          </div>
          <div>
            ${room.currentBooking ? `<div><strong>${escapeHtml(room.currentBooking.guestName)}</strong></div>
              <small>Checked in: ${toLocalString(room.currentBooking.checkInISO)}</small>` : `<small class="small">No guest</small>`}
          </div>
          <div class="actions">
            ${room.status==='vacant' ? `<button class="btn-sm" data-action="allocate" data-room="${room.id}">Allocate</button>` : `<button class="btn-sm btn-green" data-action="details" data-room="${room.id}">Details</button>`}
            ${room.status==='occupied' ? `<button class="btn-sm btn-red" data-action="checkout" data-room="${room.id}">Check-out</button>` : ``}
          </div>
        `;
        // attach listeners
        el.querySelectorAll('button').forEach(btn=>{
          btn.addEventListener('click', e=>{
            const action = btn.getAttribute('data-action');
            const rid = Number(btn.getAttribute('data-room'));
            if(action==='allocate') openAllocateModal(rid);
            if(action==='checkout') doCheckOut(rid);
            if(action==='details') showRoomDetails(rid);
          });
        });
        roomGrid.appendChild(el);
      });
    }

    function renderLatest(){
      if(state.logs.length===0){
        latestActivity.textContent = 'No activity yet.';
        return;
      }
      const last = state.logs[0];
      latestActivity.innerHTML = `<strong>${escapeHtml(last.guestName || '—')}</strong> — Room ${last.roomId} — <em>${escapeHtml(last.action)}</em> at ${toLocalString(last.timestampISO)}`;
    }

    function renderLogs(){
      // per-room details if visible
      const selectedRoomId = Number(roomDetailCard.getAttribute('data-room'));
      if(selectedRoomId){
        const room = findRoom(selectedRoomId);
        detailHeader.innerHTML = `<strong>Room ${room.id}</strong> — Status: <span class="pill ${room.status==='vacant' ? 'vacant' : 'occupied'}">${room.status}</span>`;
        // table body
        roomLogTableBody.innerHTML = '';
        for(const h of room.history.slice().reverse()){
          const tr = document.createElement('tr');
          tr.innerHTML = `<td>${room.id}</td><td>${escapeHtml(h.guestName)}</td><td>${toLocalString(h.checkInISO)}</td><td>${toLocalString(h.checkOutISO)}</td><td>${escapeHtml(h.notes||'')}</td>`;
          roomLogTableBody.appendChild(tr);
        }
      }

      // global log
      globalLogTableBody.innerHTML = '';
      for(const entry of state.logs){
        const tr = document.createElement('tr');
        tr.innerHTML = `<td>${toLocalString(entry.timestampISO)}</td><td>R${entry.roomId}</td><td>${escapeHtml(entry.guestName||'')}</td><td>${escapeHtml(entry.action)}</td><td>${toLocalString(entry.checkInISO)||''}</td><td>${toLocalString(entry.checkOutISO)||''}</td>`;
        globalLogTableBody.appendChild(tr);
      }
    }

    // --- Actions ---
    function openAllocateModal(roomId){
      modalRoomId.value = roomId;
      guestNameInput.value = '';
      guestPhoneInput.value = '';
      checkInTimeInput.value = '';
      notesInput.value = '';
      modalBackdrop.style.display = 'flex';
      guestNameInput.focus();
    }

    function closeModal(){
      modalBackdrop.style.display = 'none';
    }

    function allocateRoom(roomId, guestName, phone, checkInISO, notes){
      const room = findRoom(roomId);
      if(room.status === 'occupied'){
        alert('Room already occupied.');
        return;
      }
      const b = {
        guestName: String(guestName).trim(),
        phone: phone ? String(phone).trim() : '',
        checkInISO: checkInISO || nowISO(),
        checkOutISO: null,
        notes: notes ? String(notes).trim() : ''
      };
      room.currentBooking = {...b};
      room.status = 'occupied';
      room.history.push({...b});
      pushLog({
        timestampISO: nowISO(),
        roomId: roomId,
        guestName: b.guestName,
        action: 'check-in',
        checkInISO: b.checkInISO,
        checkOutISO: null,
        notes: b.notes
      });
      saveState();
      renderRooms();
      renderLogs();
      closeModal();
    }

    function doCheckOut(roomId){
      const room = findRoom(roomId);
      if(room.status !== 'occupied' || !room.currentBooking){
        alert('Room is not occupied.');
        return;
      }
      const confirmMsg = `Check out ${room.currentBooking.guestName} from room ${room.id}?`;
      if(!confirm(confirmMsg)) return;

      // set checkout now
      const checkOutISO = nowISO();

      // find latest history entry without checkout
      for(let i = room.history.length -1; i>=0; i--){
        if(!room.history[i].checkOutISO){
          room.history[i].checkOutISO = checkOutISO;
          break;
        }
      }
      // update current booking object
      const booking = {...room.currentBooking, checkOutISO};
      // push to logs
      pushLog({
        timestampISO: nowISO(),
        roomId: roomId,
        guestName: booking.guestName,
        action: 'check-out',
        checkInISO: booking.checkInISO,
        checkOutISO: booking.checkOutISO,
        notes: booking.notes || ''
      });

      // clear currentBooking and mark vacant
      room.currentBooking = null;
      room.status = 'vacant';
      saveState();
      renderRooms();
      renderLogs();
      // show quick toast
      alert(`Checked out ${booking.guestName} from room ${roomId}\nCheck-out: ${toLocalString(checkOutISO)}`);
    }

    function showRoomDetails(roomId){
      const room = findRoom(roomId);
      roomDetailCard.style.display = 'block';
      roomDetailCard.setAttribute('data-room', roomId);
      renderLogs();
      // scroll to right panel top
      document.querySelector('section.right').scrollTop = 0;
    }

    // --- Form handlers ---
    allocForm.addEventListener('submit', e=>{
      e.preventDefault();
      const roomId = Number(modalRoomId.value);
      const name = guestNameInput.value.trim();
      if(!name){ alert('Please enter guest name'); guestNameInput.focus(); return; }
      const phone = guestPhoneInput.value.trim();
      let checkInISO = null;
      if(checkInTimeInput.value){
        // convert local datetime-local to ISO
        const local = checkInTimeInput.value;
        // local is like "2025-09-10T13:45"
        checkInISO = new Date(local).toISOString();
      }
      const notes = notesInput.value.trim();
      allocateRoom(roomId, name, phone, checkInISO, notes);
    });

    document.getElementById('cancelModal').addEventListener('click', e=>{
      closeModal();
    });

    modalBackdrop.addEventListener('click', e=>{
      if(e.target===modalBackdrop) closeModal();
    });

    // search/filter listeners
    searchBox.addEventListener('input', renderRooms);
    filterStatus.addEventListener('change', renderRooms);

    // export CSV
    document.getElementById('exportCsv').addEventListener('click', ()=> {
      const headers = ['timestamp','roomId','guestName','action','checkInISO','checkOutISO','notes'];
      const rows = [headers.join(',')];
      for(const r of state.logs){
        const row = [
          r.timestampISO,
          r.roomId,
          csvEscape(r.guestName||''),
          r.action,
          r.checkInISO||'',
          r.checkOutISO||'',
          csvEscape(r.notes||'')
        ].join(',');
        rows.push(row);
      }
      const csv = rows.join('\\n');
      const blob = new Blob([csv], {type:'text/csv'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'guesthouse_logs.csv';
      document.body.appendChild(a);
      a.click();
      a.remove();
      URL.revokeObjectURL(url);
    });

    // reset data
    document.getElementById('resetData').addEventListener('click', ()=>{
      if(!confirm('Reset all data? This will clear bookings and logs in this browser.')) return;
      state = defaultState();
      saveState();
      renderRooms();
      renderLogs();
      renderLatest();
      alert('Data reset.');
    });

    // --- helpers ---
    function csvEscape(s){
      if(s==null) return '';
      s = String(s);
      if(s.includes(',') || s.includes('"') || s.includes('\\n')){
        return '"' + s.replace(/"/g,'""') + '"';
      }
      return s;
    }
    function escapeHtml(str){
      if(!str) return '';
      return String(str).replace(/[&<>"']/g, function(m){
        return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m];
      });
    }

    // initial render
    renderRooms();
    renderLogs();
    renderLatest();
  </script>
</body>
</html>
