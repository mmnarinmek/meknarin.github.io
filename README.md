<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mek Narin — JaoKonmek</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,400&family=DM+Sans:wght@300;400;500;600&display=swap');
  * { box-sizing:border-box; margin:0; padding:0; }
  body { font-family:'DM Sans',sans-serif; min-height:100vh; background:#07070f; display:flex; flex-direction:column; align-items:center; padding:40px 20px 60px; position:relative; overflow-x:hidden; }
  body::before { content:''; position:fixed; top:-100px; left:50%; transform:translateX(-50%); width:600px; height:600px; background:radial-gradient(ellipse,rgba(139,92,246,0.12) 0%,transparent 65%); pointer-events:none; z-index:0; }
  body::after { content:''; position:fixed; bottom:-100px; left:50%; transform:translateX(-50%); width:400px; height:400px; background:radial-gradient(ellipse,rgba(225,48,108,0.07) 0%,transparent 65%); pointer-events:none; z-index:0; }
  .container { width:100%; max-width:480px; display:flex; flex-direction:column; align-items:center; position:relative; z-index:1; }

  .avatar-wrap { position:relative; margin-bottom:16px; }
  .avatar { width:90px; height:90px; border-radius:50%; background:linear-gradient(135deg,#4c1d95,#7c3aed,#a78bfa); display:flex; align-items:center; justify-content:center; font-size:36px; border:2px solid rgba(167,139,250,0.3); box-shadow:0 0 30px rgba(139,92,246,0.25); }
  .avatar-ring { position:absolute; inset:-4px; border-radius:50%; border:1.5px solid transparent; background:linear-gradient(135deg,#a78bfa,#e1306c,#a78bfa) border-box; -webkit-mask:linear-gradient(#fff 0 0) padding-box,linear-gradient(#fff 0 0); -webkit-mask-composite:destination-out; mask-composite:exclude; animation:spin 6s linear infinite; }
  @keyframes spin { from{transform:rotate(0deg)} to{transform:rotate(360deg)} }

  .name { font-family:'Playfair Display',serif; font-size:24px; font-weight:900; color:#fff; text-align:center; margin-bottom:4px; }
  .name span { font-style:italic; color:#a78bfa; }
  .handle { font-size:13px; color:#555570; margin-bottom:10px; }
  .bio { font-size:12px; color:#6a6a8a; text-align:center; line-height:1.7; margin-bottom:10px; max-width:320px; }
  .tags { display:flex; gap:6px; flex-wrap:wrap; justify-content:center; margin-bottom:28px; }
  .tag { font-size:10px; padding:3px 10px; border-radius:20px; background:rgba(139,92,246,0.12); color:#a78bfa; border:1px solid rgba(139,92,246,0.25); }

  .sl { width:100%; font-size:9px; letter-spacing:2.5px; text-transform:uppercase; color:#3a3a5a; margin-bottom:10px; display:flex; align-items:center; gap:8px; font-weight:600; }
  .sl::before,.sl::after { content:''; flex:1; height:1px; }
  .sl::before { background:linear-gradient(90deg,transparent,#1e1e2e); }
  .sl::after { background:linear-gradient(90deg,#1e1e2e,transparent); }

  .links { width:100%; display:flex; flex-direction:column; gap:10px; margin-bottom:24px; }

  .link-btn { width:100%; display:flex; align-items:center; gap:14px; padding:14px 18px; background:#0d0d1a; border:1px solid #1a1a2e; border-radius:14px; text-decoration:none; color:#e2d9ff; font-size:14px; font-weight:600; transition:all 0.2s; position:relative; overflow:hidden; cursor:pointer; }
  .link-btn:hover { transform:translateY(-2px); box-shadow:0 8px 24px var(--shadow); border-color:var(--accent); background:var(--hover); }
  .link-btn:active { transform:translateY(0); }

  .li { width:38px; height:38px; border-radius:10px; display:flex; align-items:center; justify-content:center; font-size:18px; flex-shrink:0; background:var(--icon-bg); }
  .lt { flex:1; }
  .lt-t { font-size:14px; font-weight:600; color:#e2d9ff; margin-bottom:1px; }
  .lt-s { font-size:11px; color:#5a5a7a; font-weight:400; }
  .la { font-size:14px; color:#3a3a5a; transition:transform 0.2s,color 0.2s; }
  .link-btn:hover .la { transform:translateX(3px); color:var(--accent); }

  .yt  { --accent:#ff4444; --icon-bg:rgba(255,68,68,0.15);   --hover:rgba(255,68,68,0.04);   --shadow:rgba(255,68,68,0.15); }
  .ig  { --accent:#e1306c; --icon-bg:rgba(225,48,108,0.15);  --hover:rgba(225,48,108,0.04);  --shadow:rgba(225,48,108,0.15); }
  .tt  { --accent:#69c9d0; --icon-bg:rgba(105,201,208,0.15); --hover:rgba(105,201,208,0.04); --shadow:rgba(105,201,208,0.15); }
  .sp  { --accent:#1db954; --icon-bg:rgba(29,185,84,0.15);   --hover:rgba(29,185,84,0.04);   --shadow:rgba(29,185,84,0.15); }
  .am  { --accent:#fc3c44; --icon-bg:rgba(252,60,68,0.15);   --hover:rgba(252,60,68,0.04);   --shadow:rgba(252,60,68,0.15); }
  .dm  { --accent:#a78bfa; --icon-bg:rgba(167,139,250,0.15); --hover:rgba(167,139,250,0.04); --shadow:rgba(167,139,250,0.15); }

  .now-playing { width:100%; background:linear-gradient(135deg,#0d0a1e,#130d20); border:1px solid #2a1f4a; border-radius:14px; padding:14px 16px; display:flex; align-items:center; gap:14px; margin-bottom:10px; position:relative; overflow:hidden; }
  .now-playing::before { content:''; position:absolute; top:0;left:0;right:0; height:1px; background:linear-gradient(90deg,transparent,rgba(167,139,250,0.4),transparent); }
  .np-art { width:44px; height:44px; border-radius:8px; background:linear-gradient(135deg,#4c1d95,#7c3aed); display:flex; align-items:center; justify-content:center; font-size:20px; flex-shrink:0; }
  .np-info { flex:1; min-width:0; }
  .np-badge { font-size:8px; letter-spacing:1.5px; text-transform:uppercase; color:#a78bfa; margin-bottom:3px; font-weight:600; }
  .np-title { font-size:13px; font-weight:700; color:#e2d9ff; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
  .np-sub { font-size:11px; color:#5a5a7a; margin-top:1px; }
  .bars { display:flex; gap:3px; align-items:flex-end; height:20px; flex-shrink:0; }
  .bar { width:3px; background:#a78bfa; border-radius:2px; animation:bounce var(--d) ease-in-out infinite alternate; }
  @keyframes bounce { from{height:4px} to{height:var(--h)} }

  .footer { margin-top:32px; text-align:center; font-size:10px; color:#2a2a3a; }
  .footer span { color:#a78bfa; opacity:0.6; }
</style>
</head>
<body>
<div class="container">

  <div class="avatar-wrap">
    <div class="avatar">🎤</div>
    <div class="avatar-ring"></div>
  </div>

  <div class="name">Mek Narin <span>/ เมฆ</span></div>
  <div class="handle">@mmnarinmek · @jaokonmek.official</div>
  <div class="bio">Actor · Singer · Director · Producer · Editor · Creator<br>Covers &amp; Originals | Musicals | Storytelling</div>
  <div class="tags">
    <span class="tag">🎵 Cover & Original</span>
    <span class="tag">🎭 Musical</span>
    <span class="tag">🎬 Short Film</span>
    <span class="tag">เจ้าก้อนเมฆ</span>
  </div>

  <div class="sl">ล่าสุด</div>
  <div class="now-playing">
    <div class="np-art">🌙</div>
    <div class="np-info">
      <div class="np-badge">🎵 Latest Release</div>
      <div class="np-title">ปล่อยมือ — Mek Narin Cover</div>
      <div class="np-sub">316K views · Instagram Reels</div>
    </div>
    <div class="bars">
      <div class="bar" style="--d:0.8s;--h:18px"></div>
      <div class="bar" style="--d:1.1s;--h:12px"></div>
      <div class="bar" style="--d:0.9s;--h:20px"></div>
      <div class="bar" style="--d:1.3s;--h:10px"></div>
    </div>
  </div>

  <div class="sl" style="margin-top:8px">ติดตาม</div>
  <div class="links">

    <a href="https://www.youtube.com/jaokonmek" target="_blank" class="link-btn yt">
      <div class="li">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="#ff4444"><path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
      </div>
      <div class="lt"><div class="lt-t">YouTube</div><div class="lt-s">JaoKonmek · Cover & Original</div></div>
      <div class="la">→</div>
    </a>

    <a href="https://www.instagram.com/mmnarinmek/" target="_blank" class="link-btn ig">
      <div class="li">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="#e1306c"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/></svg>
      </div>
      <div class="lt"><div class="lt-t">Instagram</div><div class="lt-s">@mmnarinmek · 14.9K followers</div></div>
      <div class="la">→</div>
    </a>

    <a href="https://www.tiktok.com/@jaokonmek.official" target="_blank" class="link-btn tt">
      <div class="li">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="#69c9d0"><path d="M19.59 6.69a4.83 4.83 0 0 1-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 0 1-2.88 2.5 2.89 2.89 0 0 1-2.89-2.89 2.89 2.89 0 0 1 2.89-2.89c.28 0 .54.04.79.1V9.01a6.33 6.33 0 0 0-.79-.05 6.34 6.34 0 0 0-6.34 6.34 6.34 6.34 0 0 0 6.34 6.34 6.34 6.34 0 0 0 6.33-6.34V8.69a8.17 8.17 0 0 0 4.78 1.52V6.76a4.85 4.85 0 0 1-1.01-.07z"/></svg>
      </div>
      <div class="lt"><div class="lt-t">TikTok</div><div class="lt-s">@jaokonmek.official · 9.9K followers</div></div>
      <div class="la">→</div>
    </a>

  </div>

  <div class="sl">ติดต่องาน</div>
  <div class="links">
    <a href="https://www.instagram.com/mmnarinmek/" target="_blank" class="link-btn dm">
      <div class="li">✉️</div>
      <div class="lt"><div class="lt-t">ติดต่องาน / Collaboration</div><div class="lt-s">DM ที่ Instagram ได้เลยครับ</div></div>
      <div class="la">→</div>
    </a>
  </div>

  <div class="footer">Made with <span>♥</span> · Mek Narin © 2026</div>

</div>
</body>
</html>
