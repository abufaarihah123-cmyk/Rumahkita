// Service worker Rumah Kita. Naikkan nomor V setiap kali kamu mengubah index.html agar HP/PC mengambil versi baru.
const V='rumahkita-v1';
const SHELL=['./','index.html','manifest.json','icon-192.png','icon-512.png'];
self.addEventListener('install',e=>{e.waitUntil(caches.open(V).then(c=>c.addAll(SHELL)).then(()=>self.skipWaiting()))});
self.addEventListener('activate',e=>{e.waitUntil(caches.keys().then(k=>Promise.all(k.filter(x=>x!==V).map(x=>caches.delete(x)))).then(()=>self.clients.claim()))});
const simpan=(r,res)=>{if(res.ok||res.type==='opaque'){const cp=res.clone();caches.open(V).then(c=>c.put(r,cp))}return res};
self.addEventListener('fetch',e=>{
  const r=e.request;if(r.method!=='GET')return;
  const u=new URL(r.url);
  if(u.origin===location.origin){
    // file aplikasi: ambil terbaru dari jaringan, cadangan dari cache saat offline
    e.respondWith(fetch(r).then(res=>simpan(r,res)).catch(()=>caches.match(r).then(m=>m||caches.match('index.html'))));
  }else if(/(^|\.)jsdelivr\.net$|^fonts\.(googleapis|gstatic)\.com$/.test(u.hostname)){
    // library dan font: cache dulu supaya cepat dan tetap jalan offline
    e.respondWith(caches.match(r).then(m=>m||fetch(r).then(res=>simpan(r,res))));
  }
  // permintaan ke Supabase tidak disentuh (selalu lewat jaringan)
});
self.addEventListener('notificationclick',e=>{
  e.notification.close();
  e.waitUntil(clients.matchAll({type:'window',includeUncontrolled:true}).then(l=>l.length?l[0].focus():clients.openWindow('./')));
});
