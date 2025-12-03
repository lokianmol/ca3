# ca3 of cse 111 project for github 
# project is related to food website of lpu


<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>LPU Food Hub</title>
  <meta name="description" content="Food guide, stalls, menus and student reviews for Lovely Professional University (LPU)." />
  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --accent:#ff6b35; --muted:#94a3b8; --glass: rgba(255,255,255,0.03);
      --maxw:1200px;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
    }
    *{box-sizing:border-box}
    body{margin:0;background:linear-gradient(180deg,#071021 0%, #0b1220 100%);color:#e6eef8;min-height:100vh}
    .wrap{max-width:var(--maxw);margin:28px auto;padding:20px}
    header{display:flex;align-items:center;gap:18px}
    .logo{width:56px;height:56px;border-radius:12px;background:linear-gradient(135deg,var(--accent),#ff9b71);display:grid;place-items:center;font-weight:800;color:#08101a}
    h1{font-size:20px;margin:0}
    nav{margin-left:auto;display:flex;gap:8px}
    button.navbtn{background:transparent;border:1px solid transparent;padding:8px 12px;border-radius:8px;color:var(--muted);cursor:pointer}
    button.navbtn.active, button.navbtn:hover{color:#fff;border-color:rgba(255,255,255,0.06);background:var(--glass)}

    .hero{display:grid;grid-template-columns:1fr 340px;gap:22px;margin-top:22px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent);padding:18px;border-radius:14px;box-shadow:0 6px 20px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}

    .search{display:flex;gap:10px;margin-bottom:12px}
    .search input{flex:1;padding:10px 12px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit}
    .search select{padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit}

    .stalls{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
    .stall{display:flex;gap:12px;align-items:center;padding:12px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), transparent)}
    .stub{width:64px;height:64px;border-radius:10px;background:linear-gradient(135deg,#ffd6c9,#ffc0a3);display:grid;place-items:center;color:#08101a;font-weight:700}
    .meta small{color:var(--muted)}

    .sidebar h3{margin:0 0 10px 0}
    .menu-list{display:flex;flex-direction:column;gap:8px}
    .menu-item{display:flex;justify-content:space-between;align-items:center;padding:8px;border-radius:8px}
    .price{font-weight:700}

    .reviews{margin-top:14px}
    .review{padding:10px;border-radius:8px;background:rgba(255,255,255,0.02);margin-bottom:8px}
    .stars{color:var(--accent);font-weight:800}

    footer{margin-top:26px;text-align:center;color:var(--muted);font-size:13px}

    /* responsive */
    @media (max-width:900px){
      .hero{grid-template-columns:1fr}
      .stalls{grid-template-columns:1fr}
      nav{display:none}
    }

    /* small UI */
    .chip{padding:6px 8px;border-radius:999px;border:1px solid rgba(255,255,255,0.03);font-size:13px}
    .btn{background:var(--accent);border:none;padding:8px 12px;border-radius:10px;color:#08101a;font-weight:700;cursor:pointer}
    .muted{color:var(--muted)}

    /* page containers */
    .page{display:none}
    .page.active{display:block}

    .contact form{display:grid;gap:8px}
    input,textarea,select{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:10px;border-radius:8px;color:inherit}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">LPU</div>
      <div>
        <h1>LPU Food Hub</h1>
        <div class="muted">Campus food stalls • menus • student reviews</div>
      </div>

      <nav>
        <button class="navbtn active" data-page="home">Home</button>
        <button class="navbtn" data-page="stalls">Food Stalls</button>
        <button class="navbtn" data-page="menu">Menus</button>
        <button class="navbtn" data-page="reviews">Reviews</button>
        <button class="navbtn" data-page="contact">Contact</button>
      </nav>
    </header>

    <!-- pages -->
    <main>
      <section id="home" class="page active">
        <div class="hero">
          <div class="card">
            <div style="display:flex;justify-content:space-between;align-items:center">
              <div>
                <h2 style="margin:0">Discover campus food</h2>
                <div class="muted">Quickly find what's good on campus</div>
              </div>
              <div class="chip">Open now</div>
            </div>

            <div style="margin-top:12px" class="search">
              <input id="q" placeholder="Search stalls, dishes or cuisine..." />
              <select id="cuisineFilter"><option value="">All campus cuisines</option></select>
              <button class="btn" id="searchBtn">Search</button>
            </div>

            <div class="stalls" id="stallsContainer">
              <!-- stalls injected by JS -->
            </div>

          </div>

          <aside class="card sidebar">
            <h3>Featured menu</h3>
            <div class="menu-list" id="featuredMenu">
              <!-- injected -->
            </div>

            <div style="margin-top:14px">
              <h3 style="margin-bottom:6px">Top reviews</h3>
              <div class="reviews" id="topReviews"></div>
            </div>
          </aside>
        </div>
      </section>

      <section id="stalls" class="page">
        <div class="card">
          <h2>Food Stalls — directory</h2>
          <div class="muted" style="margin-bottom:12px">Tap a stall to view menu and reviews.</div>
          <div class="stalls" id="allStalls" style="max-height:520px;overflow:auto"></div>
        </div>
      </section>

      <section id="menu" class="page">
        <div class="card">
          <h2>Menu Viewer</h2>
          <div class="muted">Select a stall to inspect its menu</div>
          <div style="margin-top:12px" id="menuDetail"></div>
        </div>
      </section>

      <section id="reviews" class="page">
        <div class="card">
          <h2>Student Reviews</h2>
          <div class="muted">Share your experience — reviews saved locally in your browser.</div>
          <div style="margin-top:12px;display:grid;grid-template-columns:1fr 320px;gap:12px">
            <div>
              <div id="reviewsList"></div>
            </div>
            <aside class="card contact">
              <h3>Leave a review</h3>
              <form id="reviewForm">
                <input id="revName" placeholder="Your name" required />
                <input id="revStall" placeholder="Stall name" required />
                <select id="revRating" required>
                  <option value="">Rating</option>
                  <option value="5">5 - Excellent</option>
                  <option value="4">4 - Very good</option>
                  <option value="3">3 - Good</option>
                  <option value="2">2 - Okay</option>
                  <option value="1">1 - Poor</option>
                </select>
                <textarea id="revText" rows="4" placeholder="Tell others what's good..." required></textarea>
                <button class="btn" type="submit">Submit</button>
              </form>
            </aside>
          </div>
        </div>
      </section>

      <section id="contact" class="page">
        <div class="card">
          <h2>Contact & Suggestions</h2>
          <p class="muted">Want a stall added or found a problem? Send a message.</p>
          <form id="contactForm" style="margin-top:12px;display:grid;gap:8px;max-width:520px">
            <input id="cname" placeholder="Your name" required />
            <input id="cemail" placeholder="Your email (optional)" />
            <textarea id="cmsg" rows="5" placeholder="Message" required></textarea>
            <div style="display:flex;justify-content:space-between;align-items:center">
              <div class="muted">Or email: lpu.foodhub@example.com</div>
              <button class="btn" type="submit">Send</button>
            </div>
          </form>
        </div>
      </section>

    </main>

    <footer>
      Built for LPU • Demo site • Data stored locally in your browser
    </footer>
  </div>

  <script>
    /* --- campus-style cuisines (100+) --- */
    const cuisines = [
      'South Indian Mess','North Indian Dhaba','Punjabi Tadka','Punjabi Chai Adda','Momos Hub','Wrap House','Roll Corner','Pizza Stop','Burger Point','Pasta Studio',
      'Street Snacks','Chaat Wala','Samosa Point','Kathi Roll Stall','Tandoori Corner','Kebab House','Paratha Junction','Dosa Plaza','Udupi Corner','Idli Express',
      'Chinese Fast','Noodle Shack','Fried Rice Point','Manchurian Stall','Schezwan Kitchen','Thai Bowl','Sushi Tryout','Ramen Corner','Korean Grill','Bibimbap Bar',
      'Healthy Salads','Green Bowl','Smoothie Bar','Juice Corner','Yogurt & Lassi','Desi Sweets','Sweet Shop','Ice Cream Parlor','Shake Station','Coffee Corner',
      'Tea Stall','Breakfast Nook','Pancake Stand','Omelette Hub','Sandwich Stop','Grill & Skewer','Seafood Corner','Fish Fry Stall','Vegan Delights','Jain Food Corner',
      'Biryani House','Kacchi Biryani Stall','Rice Bowl','Thali Counter','Mess Specials','Curry Corner','Paneer House','Egg Roll Stall','Snack Box','Budget Bites',
      'Ghar Ka Khana','Home Cooked','Mom’s Kitchen','Family Dabba','Fusion Bistro','Continental Cafe','Bakery Corner','Cookie Jar','Donut Point','Sweets & Snacks',
      'Qawwali Kebabs','Shawarma Point','Falafel Hut','Middle Eastern','Lebanese Corner','Turkish Kebab','Mexican Fiesta','Taco Stand','Burrito Bar','Quesadilla Stop',
      'BBQ Pit','Grill House','Steak Slice','Hotpot Corner','Soup & Bowl','Comfort Food','Comfort Cafe','Late Night Bites','Study Snacks','Exam Special',
      'Budget Thali','Premium Dining','Chef Special','Weekend Pop-up','Festival Food Stall','Organic Corner','Farm-to-Table','Local Flavors','Regional Delights','Campus Catering'
    ];

    // make sure we have at least 100 entries
    while(cuisines.length < 100){ cuisines.push('Campus Special ' + (cuisines.length+1)) }

    /* Generate a larger stalls dataset programmatically (120 stalls) */
    function rnd(min,max){ return Math.floor(Math.random()*(max-min+1))+min }
    function genMenuItems(base){ const items = []; const count = rnd(3,5); for(let i=0;i<count;i++){ const dish = base + ' ' + ['Delight','Special','Combo','Plate','Bowl','Wrap','Roll'][rnd(0,6)]; const price = rnd(40,220); items.push({name:dish,price}) } return items }

    const stalls = [];
    const streetPrefixes = ['Corner','House','Hub','Stop','Point','Express','Kitchen','Plaza','Junction','Bar','Studio','Cafe','Dabba','Stand','Mart'];
    let id=1;
    // create 120 stalls, trying to cover cuisines
    for(let i=0;i<120;i++){
      const cu = cuisines[i % cuisines.length];
      const prefix = streetPrefixes[i % streetPrefixes.length];
      const name = cu.split(' ')[0] + ' ' + prefix; // e.g. 'South Corner'
      const desc = cu + ' — campus-style quick eats and pocket-friendly options.';
      const hours = (8 + (i%6)) + ':00 - ' + (20 + (i%4)) + ':00';
      const menu = genMenuItems(cu.split(' ')[0]);
      stalls.push({id:id++, name, cuisine:cu, desc, hours, menu});
    }

    /* localStorage keys */
    const REV_KEY = 'lpu_foodhub_reviews_v2';

    /* helpers */
    function el(tag,cls){const e=document.createElement(tag);if(cls)e.className=cls;return e}

    function renderStalls(container, list){container.innerHTML='';list.forEach(s=>{
      const row=el('div','stall');
      const stub=el('div','stub'); stub.textContent=s.name.split(' ').map(w=>w[0]).slice(0,2).join('');
      const meta=el('div'); meta.innerHTML=`<div style="font-weight:700">${s.name}</div><div class="muted" style="font-size:13px">${s.cuisine} • ${s.hours}<br><small>${s.desc}</small></div>`;
      const view=el('div'); view.style.marginLeft='auto'; view.innerHTML=`<button class="btn" data-id="${s.id}">View</button>`;
      row.appendChild(stub); row.appendChild(meta); row.appendChild(view); container.appendChild(row);
      view.querySelector('button').addEventListener('click',()=>{ showMenu(s.id); navigateTo('menu'); });
    })}

    function showMenu(id){
      const s = stalls.find(x=>x.id===id);
      const container = document.getElementById('menuDetail');
      container.innerHTML = '';
      if(!s) return container.textContent='Stall not found';
      const c = el('div'); c.innerHTML = `<h3 style="margin:0 0 8px 0">${s.name} <small class=\"muted\">${s.cuisine}</small></h3><div class=\"muted\">${s.desc}</div>`;
      const list = el('div','menu-list'); s.menu.forEach(it=>{const row=el('div','menu-item');row.innerHTML=`<div>${it.name}</div><div class="price">₹${it.price}</div>`; list.appendChild(row)});
      c.appendChild(list);
      container.appendChild(c);
    }

    function topReviewsHTML(){
      const revs = loadReviews().slice(-3).reverse();
      const out = document.getElementById('topReviews'); out.innerHTML='';
      revs.forEach(r=>{const d=el('div','review'); d.innerHTML=`<div style="display:flex;justify-content:space-between"><div><strong>${escapeHtml(r.name)}</strong> <small class=\"muted\">@${escapeHtml(r.stall)}</small></div><div class=\"stars\">${'★'.repeat(r.rating)}</div></div><div style=\"margin-top:6px\">${escapeHtml(r.text)}</div>`; out.appendChild(d)})
    }

    function renderFeatured(){
      const f = stalls[Math.floor(Math.random()*stalls.length)]; const elF = document.getElementById('featuredMenu'); elF.innerHTML=''; f.menu.forEach(it=>{const item=el('div','menu-item'); item.innerHTML=`<div>${it.name}</div><div class=\"price\">₹${it.price}</div>`; elF.appendChild(item)})
    }

    function loadReviews(){ try{ return JSON.parse(localStorage.getItem(REV_KEY) || '[]') }catch(e){return []} }
    function saveReviews(a){ localStorage.setItem(REV_KEY, JSON.stringify(a)) }

    function renderAllReviews(){ const list = document.getElementById('reviewsList'); list.innerHTML=''; const revs = loadReviews().slice().reverse(); if(revs.length===0) list.innerHTML='<div class="muted">No reviews yet — be the first!</div>'; revs.forEach(r=>{const d=el('div','review'); d.innerHTML=`<div style="display:flex;justify-content:space-between"><div><strong>${escapeHtml(r.name)}</strong> <small class=\"muted\">@${escapeHtml(r.stall)}</small></div><div class=\"stars\">${'★'.repeat(r.rating)}</div></div><div style=\"margin-top:6px\">${escapeHtml(r.text)}</div>`; list.appendChild(d) }) }

    function escapeHtml(s){ if(!s) return ''; return s.replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;') }

    /* populate cuisine dropdown */
    function populateCuisineDropdown(){ const sel = document.getElementById('cuisineFilter'); cuisines.forEach(c=>{ const o = document.createElement('option'); o.value = c; o.textContent = c; sel.appendChild(o) }) }

    /* search */
    document.getElementById('searchBtn').addEventListener('click', ()=>{ doSearch() })
    document.getElementById('q').addEventListener('keyup', (e)=>{ if(e.key==='Enter') doSearch() })

    function doSearch(){ const q=document.getElementById('q').value.toLowerCase(); const cu=document.getElementById('cuisineFilter').value; const filtered = stalls.filter(s=>{ const hay = (s.name+' '+s.desc+' '+s.cuisine+' '+s.menu.map(m=>m.name).join(' ')).toLowerCase(); const matchQ = !q || hay.includes(q); const matchC = !cu || s.cuisine===cu; return matchQ && matchC }); renderStalls(document.getElementById('stallsContainer'), filtered) }

    /* page nav */
    document.querySelectorAll('.navbtn').forEach(b=>b.addEventListener('click',e=>{ document.querySelectorAll('.navbtn').forEach(x=>x.classList.remove('active')); b.classList.add('active'); navigateTo(b.dataset.page) }))
    function navigateTo(page){ document.querySelectorAll('.page').forEach(p=>p.classList.remove('active')); const elPage=document.getElementById(page); if(elPage) elPage.classList.add('active'); }

    /* init */
    function init(){ populateCuisineDropdown(); renderStalls(document.getElementById('stallsContainer'), stalls.slice(0,20)); renderStalls(document.getElementById('allStalls'), stalls); renderFeatured(); topReviewsHTML(); renderAllReviews(); }
    init();

    /* review form */
    document.getElementById('reviewForm').addEventListener('submit', e=>{
      e.preventDefault(); const name=document.getElementById('revName').value.trim(); const stall=document.getElementById('revStall').value.trim(); const rating=Number(document.getElementById('revRating').value); const text=document.getElementById('revText').value.trim(); if(!name||!stall||!rating||!text) return alert('Please fill all fields'); const rev= {name,stall,rating,text,ts:Date.now()}; const arr=loadReviews(); arr.push(rev); saveReviews(arr); renderAllReviews(); topReviewsHTML(); e.target.reset(); alert('Thanks! Your review is saved locally.') });

    /* contact form */
    document.getElementById('contactForm').addEventListener('submit', e=>{ e.preventDefault(); alert('Thanks — message recorded (demo).') });

    // clicking stall in other lists to show menu
    document.getElementById('allStalls').addEventListener('click', ev=>{ const btn = ev.target.closest('button'); if(btn && btn.dataset.id) { showMenu(Number(btn.dataset.id)); navigateTo('menu'); } })

    // seed demo reviews only once
    if(!localStorage.getItem(REV_KEY+'-seeded')){
      const seed=[{name:'Aisha',stall:'Wrap House',rating:5,text:'Best rolls on campus!'}, {name:'Ravi',stall:'South Corner',rating:4,text:'Filling and cheap.'}, {name:'Meera',stall:'Green Bowl',rating:5,text:'Healthy and fresh.'}]; saveReviews(seed); localStorage.setItem(REV_KEY+'-seeded', '1'); init(); }
  </script>
</body>
</html>
