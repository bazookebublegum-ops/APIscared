import os, time, secrets
from datetime import datetime
from functools import wraps
from flask import Flask, request, jsonify, render_template_string
import psycopg
from psycopg.rows import dict_row

app = Flask(__name__)

# ═══════════════════════════════════════════════
#  КОНФИГУРАЦИЯ
# ═══════════════════════════════════════════════
API_SECRET = "ScaredOPTI_OOT_88SDF76" 
DATABASE_URL = os.getenv('DATABASE_URL')

rate_limit_store = {}
RATE_LIMIT = 30
RATE_WINDOW = 60

# ═══════════════════════════════════════════════
#  ВСЕ КЛЮЧИ (120 BASIC/PREM + 4 OWNER)
# ═══════════════════════════════════════════════
ALL_KEYS = [
    # BASIC (60 шт)
    ("SCARED-BASIC-0GRF5A4M", "BASIC"), ("SCARED-BASIC-0MVAPYIX", "BASIC"),
    ("SCARED-BASIC-0P55CST0", "BASIC"), ("SCARED-BASIC-0UPJ6X4H", "BASIC"),
    ("SCARED-BASIC-16FYFTFQ", "BASIC"), ("SCARED-BASIC-1KX1H92I", "BASIC"),
    ("SCARED-BASIC-39VA4A62", "BASIC"), ("SCARED-BASIC-3DRANVCN", "BASIC"),
    ("SCARED-BASIC-53AF32WY", "BASIC"), ("SCARED-BASIC-5TCSMO0W", "BASIC"),
    ("SCARED-BASIC-5ZX65IFA", "BASIC"), ("SCARED-BASIC-7BY9KLBA", "BASIC"),
    ("SCARED-BASIC-7F969OL7", "BASIC"), ("SCARED-BASIC-7GIU1GUY", "BASIC"),
    ("SCARED-BASIC-7TWIKDSV", "BASIC"), ("SCARED-BASIC-88050UMG", "BASIC"),
    ("SCARED-BASIC-8I0L9S1Y", "BASIC"), ("SCARED-BASIC-B6U9UEJF", "BASIC"),
    ("SCARED-BASIC-B99CKJZ0", "BASIC"), ("SCARED-BASIC-CAU78JM9", "BASIC"),
    ("SCARED-BASIC-CERGLLHO", "BASIC"), ("SCARED-BASIC-ED1AYH81", "BASIC"),
    ("SCARED-BASIC-EXFSSLHB", "BASIC"), ("SCARED-BASIC-EXGIMMN3", "BASIC"),
    ("SCARED-BASIC-FJSNY16U", "BASIC"), ("SCARED-BASIC-G2SJ4AVQ", "BASIC"),
    ("SCARED-BASIC-G94PU2YO", "BASIC"), ("SCARED-BASIC-GYLFJYWQ", "BASIC"),
    ("SCARED-BASIC-HG9LJYEW", "BASIC"), ("SCARED-BASIC-HO4I7JRF", "BASIC"),
    ("SCARED-BASIC-HYKMDOZE", "BASIC"), ("SCARED-BASIC-I0YY22MP", "BASIC"),
    ("SCARED-BASIC-I2KKGZ7Y", "BASIC"), ("SCARED-BASIC-IDU3649G", "BASIC"),
    ("SCARED-BASIC-IEAR3TKM", "BASIC"), ("SCARED-BASIC-JAP4LKQ7", "BASIC"),
    ("SCARED-BASIC-LGWYVT61", "BASIC"), ("SCARED-BASIC-MHU0TIHC", "BASIC"),
    ("SCARED-BASIC-MRJNU1PJ", "BASIC"), ("SCARED-BASIC-N5YCZ0G2", "BASIC"),
    ("SCARED-BASIC-NHQ0K4N7", "BASIC"), ("SCARED-BASIC-O4TGRRZ6", "BASIC"),
    ("SCARED-BASIC-O6GV9ZJ1", "BASIC"), ("SCARED-BASIC-P3MQPS3O", "BASIC"),
    ("SCARED-BASIC-PMZJME7A", "BASIC"), ("SCARED-BASIC-Q0XE3ZJL", "BASIC"),
    ("SCARED-BASIC-Q60ORSWJ", "BASIC"), ("SCARED-BASIC-SIY657E3", "BASIC"),
    ("SCARED-BASIC-SLSRV5EV", "BASIC"), ("SCARED-BASIC-SPHHRT5Z", "BASIC"),
    ("SCARED-BASIC-TB1YJ3KV", "BASIC"), ("SCARED-BASIC-TFVVX548", "BASIC"),
    ("SCARED-BASIC-U6GB3KOY", "BASIC"), ("SCARED-BASIC-V5Z15U46", "BASIC"),
    ("SCARED-BASIC-V9RPP3FY", "BASIC"), ("SCARED-BASIC-VV7IP3O1", "BASIC"),
    ("SCARED-BASIC-XLZQDCKM", "BASIC"), ("SCARED-BASIC-Z9Q2FXE7", "BASIC"),
    ("SCARED-BASIC-ZIMZNHJR", "BASIC"), ("SCARED-BASIC-ZT0JRIYO", "BASIC"),
    # PREMIUM (60 шт)
    ("SCARED-PREM-01LEM9O1", "PREM"), ("SCARED-PREM-0FBM2MPP", "PREM"),
    ("SCARED-PREM-107RQOJ1", "PREM"), ("SCARED-PREM-10LN3WBH", "PREM"),
    ("SCARED-PREM-1CKMM6R7", "PREM"), ("SCARED-PREM-1MZIFYIK", "PREM"),
    ("SCARED-PREM-3027OZNN", "PREM"), ("SCARED-PREM-329P0GOA", "PREM"),
    ("SCARED-PREM-3PSYL9FS", "PREM"), ("SCARED-PREM-40YBBXCE", "PREM"),
    ("SCARED-PREM-46XTOAMS", "PREM"), ("SCARED-PREM-4BZPTGJ3", "PREM"),
    ("SCARED-PREM-4J9L0ARQ", "PREM"), ("SCARED-PREM-53HEFPAW", "PREM"),
    ("SCARED-PREM-6BVERWWU", "PREM"), ("SCARED-PREM-6HKXW9S3", "PREM"),
    ("SCARED-PREM-7C9OBUS0", "PREM"), ("SCARED-PREM-AFGB3VQI", "PREM"),
    ("SCARED-PREM-AHAA21MF", "PREM"), ("SCARED-PREM-AJH2HHRE", "PREM"),
    ("SCARED-PREM-CT055VX9", "PREM"), ("SCARED-PREM-EGGURNEY", "PREM"),
    ("SCARED-PREM-F38KD12Z", "PREM"), ("SCARED-PREM-F7U9VNZF", "PREM"),
    ("SCARED-PREM-G3HJ1UBF", "PREM"), ("SCARED-PREM-IIHRFPQV", "PREM"),
    ("SCARED-PREM-JG6G8V42", "PREM"), ("SCARED-PREM-JNCWF97A", "PREM"),
    ("SCARED-PREM-K3SP5MWO", "PREM"), ("SCARED-PREM-KEN8FDS8", "PREM"),
    ("SCARED-PREM-KGVM7TBN", "PREM"), ("SCARED-PREM-KJY3WDUE", "PREM"),
    ("SCARED-PREM-KO68N7SD", "PREM"), ("SCARED-PREM-LL2M2Q5C", "PREM"),
    ("SCARED-PREM-M8Y7FF8O", "PREM"), ("SCARED-PREM-OE53FDZ9", "PREM"),
    ("SCARED-PREM-QSI9HVC5", "PREM"), ("SCARED-PREM-QU6VA5BJ", "PREM"),
    ("SCARED-PREM-SZANYS01", "PREM"), ("SCARED-PREM-TGRWR6TF", "PREM"),
    ("SCARED-PREM-THPZLWMV", "PREM"), ("SCARED-PREM-U5VXE1KR", "PREM"),
    ("SCARED-PREM-UPFODCFH", "PREM"), ("SCARED-PREM-VASUPEW2", "PREM"),
    ("SCARED-PREM-VSKC4FV4", "PREM"), ("SCARED-PREM-VUJBV74K", "PREM"),
    ("SCARED-PREM-VXECK2LR", "PREM"), ("SCARED-PREM-W2JPAW11", "PREM"),
    ("SCARED-PREM-WLJOV9NV", "PREM"), ("SCARED-PREM-X1L9H8TS", "PREM"),
    ("SCARED-PREM-XC27B7YC", "PREM"), ("SCARED-PREM-XEG1S1OD", "PREM"),
    ("SCARED-PREM-XMT2J7HZ", "PREM"), ("SCARED-PREM-XOZ3WSIU", "PREM"),
    ("SCARED-PREM-XWQ28MKC", "PREM"), ("SCARED-PREM-YB2JXI6A", "PREM"),
    ("SCARED-PREM-YJUMV7LT", "PREM"), ("SCARED-PREM-YO2EMVKN", "PREM"),
    ("SCARED-PREM-ZR3SGYI0", "PREM"), ("SCARED-PREM-ZUVBT0RX", "PREM"),
]

OWNER_KEYS = [
    "SCARED-OWNER-GODMODE",
    "SCARED-OWNER-ALPHA01",
    "SCARED-OWNER-BETA002",
    "SCARED-OWNER-DELTA03",
]

def get_db():
    return psycopg.connect(DATABASE_URL, autocommit=True)

def init_db():
    try:
        with get_db() as conn:
            with conn.cursor() as cur:
                # Таблица лицензий
                cur.execute('''
                    CREATE TABLE IF NOT EXISTS licenses (
                        key TEXT PRIMARY KEY,
                        tier TEXT NOT NULL,
                        status TEXT DEFAULT 'unused',
                        hwid TEXT,
                        activated_at TIMESTAMP,
                        is_active BOOLEAN DEFAULT TRUE
                    )
                ''')
                
                # Таблица анонсов
                cur.execute('''
                    CREATE TABLE IF NOT EXISTS announcements (
                        id SERIAL PRIMARY KEY,
                        title TEXT NOT NULL,
                        content TEXT NOT NULL,
                        type TEXT DEFAULT 'update',
                        created_at TIMESTAMP DEFAULT NOW(),
                        is_active BOOLEAN DEFAULT TRUE
                    )
                ''')
                
                # Таблица юзернеймов
                cur.execute('''
                    CREATE TABLE IF NOT EXISTS usernames (
                        username TEXT PRIMARY KEY,
                        hwid TEXT NOT NULL,
                        tier TEXT NOT NULL,
                        display_name TEXT,
                        color TEXT DEFAULT '#ffffff',
                        glow INT DEFAULT 10,
                        created_at TIMESTAMP DEFAULT NOW()
                    )
                ''')
                
                # Добавляем все ключи
                for key, tier in ALL_KEYS:
                    cur.execute('''
                        INSERT INTO licenses (key, tier, status) 
                        VALUES (%s, %s, 'unused')
                        ON CONFLICT (key) DO NOTHING
                    ''', (key, tier))
                
                # Добавляем OWNER ключи
                for key in OWNER_KEYS:
                    cur.execute('''
                        INSERT INTO licenses (key, tier, status, is_active) 
                        VALUES (%s, 'OWNER', 'used', TRUE)
                        ON CONFLICT (key) DO NOTHING
                    ''', (key,))
                    
        print(f"[OK] Database initialized with {len(ALL_KEYS)} keys + {len(OWNER_KEYS)} OWNER keys")
    except Exception as e:
        print(f"[ERROR] Database initialization failed: {e}")

def check_rate_limit(ip):
    current_time = time.time()
    if ip not in rate_limit_store:
        rate_limit_store[ip] = []
    rate_limit_store[ip] = [t for t in rate_limit_store[ip] if current_time - t < RATE_WINDOW]
    if len(rate_limit_store[ip]) >= RATE_LIMIT:
        return False
    rate_limit_store[ip].append(current_time)
    return True

def require_api_secret(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        s = request.headers.get('X-API-Secret')
        if not s or not secrets.compare_digest(s, API_SECRET):
            print(f"[AUTH] Invalid API secret from {request.remote_addr}")
            return jsonify({'status': 'error', 'message': 'Invalid API secret'}), 401
        return f(*args, **kwargs)
    return decorated

# ═══════════════════════════════════════════════
#  АДМИНКА (HTML) - ЧЕРНЫЙ МИНИМАЛИЗМ
# ═══════════════════════════════════════════════
HTML_PAGE = """
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>ScaredOpti Admin</title>
    <style>
        :root { --bg: #050505; --card: #111; --border: #222; --text: #eee; --accent: #fff; --red: #ff4444; --green: #44ff44; }
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }
        body { background: var(--bg); color: var(--text); padding: 20px; min-height: 100vh; }
        .container { max-width: 1200px; margin: 0 auto; }
        h1, h2 { text-align: center; margin-bottom: 20px; font-weight: 300; letter-spacing: 2px; }
        
        /* Stats */
        .stats { display: flex; gap: 15px; justify-content: center; margin-bottom: 30px; flex-wrap: wrap; }
        .stat { background: var(--card); padding: 15px 25px; border-radius: 4px; border: 1px solid var(--border); text-align: center; min-width: 120px; }
        .stat .num { font-size: 24px; font-weight: bold; display: block; margin-top: 5px; }
        .stat h3 { font-size: 10px; text-transform: uppercase; color: #666; }

        /* Filters */
        .filters { display: flex; gap: 10px; justify-content: center; margin-bottom: 30px; }
        button, input, select, textarea { background: var(--card); border: 1px solid var(--border); color: var(--text); padding: 10px 15px; border-radius: 4px; outline: none; transition: 0.2s; }
        button:hover { border-color: var(--accent); cursor: pointer; }
        button.active { background: var(--accent); color: #000; border-color: var(--accent); }
        input:focus, textarea:focus { border-color: var(--accent); }

        /* Keys Grid */
        .keys { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 15px; }
        .key { background: var(--card); padding: 15px; border-radius: 4px; border-left: 3px solid #444; border: 1px solid var(--border); }
        .key.used { border-left-color: var(--red); }
        .key-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
        .key-code { font-family: monospace; font-weight: bold; }
        .tier { font-size: 10px; padding: 2px 6px; border-radius: 2px; background: #333; text-transform: uppercase; }
        .tier.owner { background: gold; color: #000; }
        
        .toggle-btn { width: 100%; margin-top: 10px; padding: 8px; border-radius: 4px; cursor: pointer; font-size: 12px; font-weight: bold; }
        .toggle-btn.block { background: rgba(255,68,68,0.1); color: var(--red); border: 1px solid var(--red); }
        .toggle-btn.unblock { background: rgba(68,255,68,0.1); color: var(--green); border: 1px solid var(--green); }

        /* Sections */
        .section { margin-top: 50px; border-top: 1px solid var(--border); padding-top: 30px; }
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; margin-bottom: 5px; font-size: 12px; color: #888; }
        .form-group input, .form-group textarea, .form-group select { width: 100%; }
        
        .item-list { display: flex; flex-direction: column; gap: 10px; margin-top: 20px; }
        .item { background: var(--card); padding: 15px; border-radius: 4px; border: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; }
        .item-info h4 { margin-bottom: 5px; }
        .item-info p { font-size: 12px; color: #888; }
        .delete-btn { background: transparent; border: 1px solid var(--red); color: var(--red); padding: 5px 10px; border-radius: 4px; cursor: pointer; }
        .delete-btn:hover { background: var(--red); color: #fff; }

        .loading { text-align: center; padding: 40px; color: #666; }
    </style>
</head>
<body>
    <div class="container">
        <h1>SCAREDOPTI ADMIN</h1>
        
        <div class="stats">
            <div class="stat"><h3>Total</h3><span class="num" id="total">0</span></div>
            <div class="stat"><h3>Used</h3><span class="num" id="used">0</span></div>
            <div class="stat"><h3>Blocked</h3><span class="num" id="blocked">0</span></div>
            <div class="stat"><h3>Usernames</h3><span class="num" id="usernames-count">0</span></div>
        </div>

        <div class="filters">
            <button onclick="setFilter('all')" id="btn-all" class="active">All</button>
            <button onclick="setFilter('used')" id="btn-used">Used</button>
            <button onclick="setFilter('unused')" id="btn-unused">Unused</button>
            <input type="text" id="search" placeholder="Search key..." onkeyup="render()">
        </div>

        <div id="keys" class="keys"><div class="loading">Loading...</div></div>

        <!-- ANNOUNCEMENTS -->
        <div class="section">
            <h2>ANNOUNCEMENTS</h2>
            <div style="display:grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                <div>
                    <div class="form-group"><label>Title</label><input type="text" id="ann-title"></div>
                    <div class="form-group"><label>Type</label><select id="ann-type"><option value="update">Update</option><option value="news">News</option><option value="critical">Critical</option></select></div>
                    <div class="form-group"><label>Content</label><textarea id="ann-content" rows="3"></textarea></div>
                    <button onclick="createAnnouncement()" style="width:100%">Publish</button>
                </div>
                <div id="announcements-list" class="item-list"></div>
            </div>
        </div>

        <!-- USERNAMES -->
        <div class="section">
            <h2>USERNAMES</h2>
            <div id="usernames-list" class="item-list"><div class="loading">Loading...</div></div>
        </div>
    </div>

    <script>
        let keys = [], announcements = [], usernames = [];
        let filter = 'all';

        async function load() {
            const r = await fetch('/api/keys', { headers: {'X-API-Secret': '{{ api_secret }}'} });
            const data = await r.json();
            keys = data.keys;
            updateStats();
            render();
        }

        async function loadAnnouncements() {
            const r = await fetch('/api/announcements', { headers: {'X-API-Secret': '{{ api_secret }}'} });
            const data = await r.json();
            announcements = data.announcements;
            document.getElementById('announcements-list').innerHTML = announcements.map(a => `
                <div class="item">
                    <div class="item-info"><h4>${a.title}</h4><p>${a.content.substring(0,50)}...</p></div>
                    <button class="delete-btn" onclick="deleteAnnouncement(${a.id})">Delete</button>
                </div>
            `).join('');
        }

        async function loadUsernames() {
            const r = await fetch('/api/usernames', { headers: {'X-API-Secret': '{{ api_secret }}'} });
            const data = await r.json();
            usernames = data.usernames;
            document.getElementById('usernames-count').textContent = usernames.length;
            document.getElementById('usernames-list').innerHTML = usernames.map(u => `
                <div class="item">
                    <div class="item-info"><h4>@${u.username}</h4><p>Tier: ${u.tier} | HWID: ${u.hwid.substring(0,8)}...</p></div>
                    <button class="delete-btn" onclick="banUsername('${u.username}')">Ban</button>
                </div>
            `).join('');
        }

        function updateStats() {
            document.getElementById('total').textContent = keys.length;
            document.getElementById('used').textContent = keys.filter(k => k.status === 'used').length;
            document.getElementById('blocked').textContent = keys.filter(k => !k.is_active).length;
        }

        function setFilter(f) {
            filter = f;
            document.querySelectorAll('.filters button').forEach(b => b.classList.remove('active'));
            document.getElementById('btn-' + f).classList.add('active');
            render();
        }

        function render() {
            const s = document.getElementById('search').value.toLowerCase();
            let filtered = keys.filter(k => {
                if (filter === 'used' && k.status !== 'used') return false;
                if (filter === 'unused' && k.status !== 'unused') return false;
                if (s && !k.key.toLowerCase().includes(s)) return false;
                return true;
            });

            document.getElementById('keys').innerHTML = filtered.map(k => `
                <div class="key ${k.status}" style="${!k.is_active ? 'opacity:0.5; border-left-color:red;' : ''}">
                    <div class="key-header">
                        <span class="key-code">${k.key}</span>
                        <span class="tier ${k.tier === 'OWNER' ? 'owner' : ''}">${k.tier}</span>
                    </div>
                    <div style="font-size:12px; color:#888; margin-bottom:5px;">Status: ${k.status} | Active: ${k.is_active}</div>
                    ${k.hwid ? `<div style="font-size:11px; color:#666;">HWID: ${k.hwid}</div>` : ''}
                    <button class="toggle-btn ${k.is_active ? 'block' : 'unblock'}" onclick="toggleKey('${k.key}', ${!k.is_active})">
                        ${k.is_active ? 'BLOCK KEY' : 'UNBLOCK KEY'}
                    </button>
                </div>
            `).join('');
        }

        async function toggleKey(key, isActive) {
            await fetch('/api/update', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json', 'X-API-Secret': '{{ api_secret }}' },
                body: JSON.stringify({key: key, active: isActive})
            });
            await load();
        }

        async function createAnnouncement() {
            const title = document.getElementById('ann-title').value;
            const content = document.getElementById('ann-content').value;
            const type = document.getElementById('ann-type').value;
            if(!title || !content) return alert('Fill all fields');
            
            await fetch('/api/announcements', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json', 'X-API-Secret': '{{ api_secret }}' },
                body: JSON.stringify({title, content, type})
            });
            document.getElementById('ann-title').value = '';
            document.getElementById('ann-content').value = '';
            await loadAnnouncements();
        }

        async function deleteAnnouncement(id) {
            if(!confirm('Delete?')) return;
            await fetch(`/api/announcements/${id}`, { method: 'DELETE', headers: { 'X-API-Secret': '{{ api_secret }}' } });
            await loadAnnouncements();
        }

        async function banUsername(username) {
            if(!confirm(`Ban @${username}?`)) return;
            await fetch(`/api/usernames/${username}/ban`, { method: 'POST', headers: { 'X-API-Secret': '{{ api_secret }}' } });
            await loadUsernames();
        }

        load(); loadAnnouncements(); loadUsernames();
        setInterval(load, 10000);
    </script>
</body>
</html>
"""

# ═══════════════════════════════════════════════
#  API ROUTES
# ═══════════════════════════════════════════════

@app.route('/')
@app.route('/admin')
def home():
    return render_template_string(HTML_PAGE, api_secret=API_SECRET)

@app.route('/api/keys')
@require_api_secret
def get_keys():
    with get_db() as conn:
        with conn.cursor(row_factory=dict_row) as cur:
            cur.execute('SELECT key, tier, status, hwid, activated_at, is_active FROM licenses ORDER BY tier, key')
            keys = cur.fetchall()
    return jsonify({'status': 'ok', 'keys': keys})

@app.route('/api/update', methods=['POST'])
@require_api_secret
def update():
    data = request.get_json()
    key = data.get('key')
    active = data.get('active', True) # Блокировка/Разблокировка
    
    with get_db() as conn:
        with conn.cursor() as cur:
            cur.execute("UPDATE licenses SET is_active = %s WHERE key = %s", (active, key))
    return jsonify({'ok': True})

@app.route('/activate', methods=['POST'])
def activate():
    ip = request.remote_addr
    if not check_rate_limit(ip):
        return jsonify({'status': 'error', 'message': 'Rate limit exceeded'}), 429
    
    data = request.get_json()
    key = data.get('key', '').strip()
    hwid = data.get('hwid', '').strip()
    
    if not key:
        return jsonify({'status': 'invalid', 'message': 'Key required'}), 400
    
    parts = key.split('-')
    if len(parts) != 3 or parts[0] != 'SCARED' or parts[1] not in ['BASIC', 'PREM', 'OWNER']:
        return jsonify({'status': 'invalid', 'message': 'Invalid key format'}), 400
    
    if parts[1] == 'OWNER':
        if key not in OWNER_KEYS:
            return jsonify({'status': 'invalid', 'message': 'Invalid owner key'}), 400
        return jsonify({'status': 'ok', 'tier': 'OWNER', 'message': 'Welcome back, Owner!'})
    
    if len(parts[2]) != 8:
        return jsonify({'status': 'invalid', 'message': 'Invalid key format'}), 400
    
    with get_db() as conn:
        with conn.cursor(row_factory=dict_row) as cur:
            cur.execute('SELECT * FROM licenses WHERE key = %s', (key,))
            row = cur.fetchone()
            
            if not row:
                return jsonify({'status': 'invalid', 'message': 'Key not found'}), 404
            
            if not row['is_active']:
                return jsonify({'status': 'blocked', 'message': 'Key has been blocked by admin'}), 403
            
            tier = row['tier']
            stored_hwid = row['hwid']
            
            if row['status'] == 'unused':
                cur.execute("UPDATE licenses SET status = 'used', hwid = %s, activated_at = %s WHERE key = %s", 
                           (hwid, datetime.now(), key))
                return jsonify({'status': 'activated', 'tier': tier, 'message': 'License activated'})
            
            if stored_hwid and stored_hwid != hwid:
                return jsonify({'status': 'blocked', 'message': 'HWID mismatch'})
            
            return jsonify({'status': 'ok', 'tier': tier, 'message': 'License valid'})

# Announcements API
@app.route('/api/announcements', methods=['GET'])
@require_api_secret
def get_announcements():
    with get_db() as conn:
        with conn.cursor(row_factory=dict_row) as cur:
            cur.execute('SELECT id, title, content, type, created_at FROM announcements WHERE is_active = TRUE ORDER BY created_at DESC')
            return jsonify({'status': 'ok', 'announcements': cur.fetchall()})

@app.route('/api/announcements', methods=['POST'])
@require_api_secret
def create_announcement():
    data = request.get_json()
    with get_db() as conn:
        with conn.cursor() as cur:
            cur.execute('INSERT INTO announcements (title, content, type) VALUES (%s, %s, %s)', 
                       (data['title'], data['content'], data.get('type', 'update')))
    return jsonify({'status': 'ok'})

@app.route('/api/announcements/<int:ann_id>', methods=['DELETE'])
@require_api_secret
def delete_announcement(ann_id):
    with get_db() as conn:
        with conn.cursor() as cur:
            cur.execute('UPDATE announcements SET is_active = FALSE WHERE id = %s', (ann_id,))
    return jsonify({'status': 'ok'})

# Usernames API
@app.route('/api/check-username', methods=['POST'])
@require_api_secret
def check_username():
    data = request.get_json()
    username = data.get('username', '').lower().strip()
    hwid = data.get('hwid', '')
    tier = data.get('tier', '')
    
    if len(username) < 3 or len(username) > 20 or not username.isalnum():
        return jsonify({"available": False, "error": "Invalid username"})
    
    with get_db() as conn:
        with conn.cursor(row_factory=dict_row) as cur:
            cur.execute("SELECT hwid FROM usernames WHERE username = %s", (username,))
            row = cur.fetchone()
            
            if row:
                if row['hwid'] == hwid: return jsonify({"available": True, "owned": True})
                else: return jsonify({"available": False, "error": "Taken"})
            
            max_u = 5 if tier == 'OWNER' else 1
            cur.execute("SELECT COUNT(*) as cnt FROM usernames WHERE hwid = %s", (hwid,))
            if cur.fetchone()['cnt'] >= max_u:
                return jsonify({"available": False, "error": "Limit reached"})
    
    return jsonify({"available": True, "owned": False})

@app.route('/api/save-username', methods=['POST'])
@require_api_secret
def save_username():
    data = request.get_json()
    with get_db() as conn:
        with conn.cursor() as cur:
            cur.execute("""
                INSERT INTO usernames (username, hwid, tier, display_name, color, glow) 
                VALUES (%s, %s, %s, %s, %s, %s)
                ON CONFLICT (username) DO UPDATE SET hwid=EXCLUDED.hwid, display_name=EXCLUDED.display_name, color=EXCLUDED.color, glow=EXCLUDED.glow WHERE usernames.hwid=EXCLUDED.hwid
            """, (data['username'].lower(), data['hwid'], data['tier'], data.get('display_name',''), data.get('color','#fff'), data.get('glow',10)))
    return jsonify({"success": True})

@app.route('/api/usernames')
@require_api_secret
def get_usernames():
    with get_db() as conn:
        with conn.cursor(row_factory=dict_row) as cur:
            cur.execute('SELECT * FROM usernames ORDER BY created_at DESC')
            return jsonify({'status': 'ok', 'usernames': cur.fetchall()})

@app.route('/api/usernames/<username>/ban', methods=['POST'])
@require_api_secret
def ban_username(username):
    with get_db() as conn:
        with conn.cursor() as cur:
            cur.execute('DELETE FROM usernames WHERE username = %s', (username,))
    return jsonify({'status': 'ok'})

@app.route('/health')
def health():
    return jsonify({'status': 'ok'})

init_db()
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)