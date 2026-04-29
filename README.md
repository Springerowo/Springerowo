<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Springerowo — Hodowla · Sport · Fotografia</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400;1,700&family=Jost:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#080808;
  --surface:#111;
  --card:#161616;
  --border:#222;
  --accent:#b8860b;
  --accent2:#d4a017;
  --accent-soft:rgba(184,134,11,.12);
  --text:#f0ece3;
  --muted:#6e6860;
  --muted2:#9a9088;
  --paw:#c8b89a;
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'Jost',sans-serif;font-size:15px;overflow-x:hidden;cursor:none}

/* CUSTOM CURSOR */
.cursor{position:fixed;width:10px;height:10px;background:var(--accent);border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);transition:width .2s,height .2s,background .2s}
.cursor-ring{position:fixed;width:36px;height:36px;border:1px solid var(--accent);border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:all .12s ease}
body:hover .cursor{opacity:1}

/* GRAIN */
body::after{content:'';position:fixed;inset:0;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.032'/%3E%3C/svg%3E");
  pointer-events:none;z-index:9990;mix-blend-mode:overlay}

/* ── NAV ─────────────────────────────────────────────────────── */
nav{position:sticky;top:0;z-index:100;height:68px;
  background:rgba(8,8,8,.9);backdrop-filter:blur(20px);
  border-bottom:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;
  padding:0 52px}
.logo{display:flex;align-items:center;gap:12px;cursor:pointer}
.logo-paw{font-size:1.3rem;color:var(--accent)}
.logo-text{font-family:'Playfair Display',serif;font-size:1.4rem;letter-spacing:2px;color:var(--text)}
.logo-text em{color:var(--accent);font-style:italic}
.nav-links{display:flex;gap:32px;list-style:none}
.nav-links a{color:var(--muted2);text-decoration:none;font-size:.75rem;letter-spacing:2.5px;
  text-transform:uppercase;cursor:pointer;transition:color .2s;
  padding-bottom:3px;border-bottom:1px solid transparent}
.nav-links a:hover,.nav-links a.active{color:var(--text);border-bottom-color:var(--accent)}

/* ── PAGE SYSTEM ─────────────────────────────────────────────── */
.page{display:none}
.page.active{display:block;animation:fadeUp .5s ease both}
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}

/* ── HOME HERO ───────────────────────────────────────────────── */
.home-hero{position:relative;height:100vh;overflow:hidden;display:flex;align-items:center}
.hero-bg{position:absolute;inset:0}
.hero-bg img{width:100%;height:100%;object-fit:cover;
  filter:brightness(.45) saturate(.7);
  transform:scale(1.05);animation:heroZoom 14s ease-in-out infinite alternate}
@keyframes heroZoom{from{transform:scale(1.05)}to{transform:scale(1.0)}}
.hero-bg::after{content:'';position:absolute;inset:0;
  background:linear-gradient(105deg,rgba(8,8,8,.92) 0%,rgba(8,8,8,.4) 55%,transparent 100%)}
.hero-content{position:relative;z-index:2;padding:0 52px;max-width:700px}
.hero-tag{font-size:.68rem;letter-spacing:4px;text-transform:uppercase;color:var(--accent);
  margin-bottom:24px;display:flex;align-items:center;gap:12px}
.hero-tag::before{content:'';width:40px;height:1px;background:var(--accent)}
.hero-h{font-family:'Playfair Display',serif;
  font-size:clamp(3.5rem,8vw,7.5rem);line-height:.9;
  letter-spacing:-1px;margin-bottom:28px}
.hero-h .italic{font-style:italic;color:var(--accent)}
.hero-sub{color:var(--muted2);font-size:1rem;line-height:1.8;max-width:480px;
  margin-bottom:48px;font-weight:300}
.hero-ctas{display:flex;gap:14px;flex-wrap:wrap}
.btn-gold{background:var(--accent);color:#080808;border:none;cursor:pointer;
  padding:14px 36px;font-family:'Jost',sans-serif;font-weight:500;
  font-size:.78rem;letter-spacing:2.5px;text-transform:uppercase;
  transition:background .2s,transform .15s}
.btn-gold:hover{background:var(--accent2);transform:translateY(-2px)}
.btn-outline{background:transparent;color:var(--text);border:1px solid rgba(255,255,255,.2);
  cursor:pointer;padding:14px 36px;font-family:'Jost',sans-serif;
  font-size:.78rem;letter-spacing:2.5px;text-transform:uppercase;
  transition:border-color .2s,color .2s}
.btn-outline:hover{border-color:var(--accent);color:var(--accent)}
.hero-scroll{position:absolute;bottom:40px;left:52px;z-index:2;
  display:flex;align-items:center;gap:12px;color:var(--muted);
  font-size:.7rem;letter-spacing:2px;text-transform:uppercase}
.scroll-line{width:60px;height:1px;background:var(--muted);
  animation:scrollLine 2s ease-in-out infinite}
@keyframes scrollLine{0%,100%{width:60px}50%{width:20px}}

/* ABOUT STRIP */
.about-strip{display:grid;grid-template-columns:1fr 1fr;min-height:80vh;overflow:hidden}
.about-img{position:relative;overflow:hidden}
.about-img img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.8) brightness(.85);
  transition:transform .8s cubic-bezier(.22,1,.36,1)}
.about-img:hover img{transform:scale(1.04)}
.about-img::after{content:'';position:absolute;inset:0;
  background:linear-gradient(to right,transparent 70%,var(--bg) 100%)}
.about-text{padding:80px 60px;display:flex;flex-direction:column;justify-content:center;
  background:var(--bg)}
.about-kicker{font-size:.68rem;letter-spacing:4px;text-transform:uppercase;
  color:var(--accent);margin-bottom:20px;display:flex;align-items:center;gap:10px}
.about-kicker::before{content:'';width:30px;height:1px;background:var(--accent)}
.about-h{font-family:'Playfair Display',serif;font-size:clamp(2rem,4vw,3.5rem);
  line-height:1.1;margin-bottom:28px}
.about-h em{font-style:italic;color:var(--accent)}
.about-body{color:var(--muted2);line-height:1.9;font-size:.95rem;margin-bottom:32px;font-weight:300}
.about-tags{display:flex;gap:10px;flex-wrap:wrap}
.tag{border:1px solid var(--border);color:var(--muted2);padding:5px 14px;
  font-size:.72rem;letter-spacing:1.5px;text-transform:uppercase;
  transition:border-color .2s,color .2s}
.tag:hover{border-color:var(--accent);color:var(--accent)}

/* PILLARS */
.pillars{display:grid;grid-template-columns:repeat(4,1fr);border-top:1px solid var(--border)}
.pillar{padding:44px 36px;border-right:1px solid var(--border);
  transition:background .3s}
.pillar:last-child{border-right:none}
.pillar:hover{background:var(--accent-soft)}
.pillar-icon{font-size:1.8rem;margin-bottom:16px}
.pillar-name{font-family:'Playfair Display',serif;font-size:1.1rem;margin-bottom:10px}
.pillar-desc{font-size:.8rem;color:var(--muted);line-height:1.7;font-weight:300}
.pillar-link{display:inline-block;margin-top:16px;font-size:.7rem;letter-spacing:2px;
  text-transform:uppercase;color:var(--accent);cursor:pointer;
  border-bottom:1px solid transparent;transition:border-color .2s}
.pillar-link:hover{border-bottom-color:var(--accent)}

/* HOME GALLERY PREVIEW */
.sec-head{padding:72px 52px 40px;display:flex;align-items:flex-end;justify-content:space-between;
  border-bottom:1px solid var(--border)}
.sec-h{font-family:'Playfair Display',serif;font-size:2.8rem;letter-spacing:1px}
.sec-h em{font-style:italic;color:var(--accent)}
.sec-more{font-size:.72rem;letter-spacing:2px;text-transform:uppercase;color:var(--muted2);
  cursor:pointer;border-bottom:1px solid var(--border);padding-bottom:2px;
  transition:color .2s,border-color .2s}
.sec-more:hover{color:var(--accent);border-bottom-color:var(--accent)}

.home-gallery-grid{display:grid;grid-template-columns:2fr 1fr 1fr;grid-template-rows:300px 300px;gap:3px;
  margin:3px 0}
.hgg-item{overflow:hidden;position:relative;cursor:pointer}
.hgg-item img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.75) brightness(.8);
  transition:transform .7s cubic-bezier(.22,1,.36,1),filter .4s}
.hgg-item:hover img{transform:scale(1.08);filter:saturate(1) brightness(.9)}
.hgg-item.tall{grid-row:span 2}
.hgg-overlay{position:absolute;inset:0;
  background:linear-gradient(to top,rgba(0,0,0,.75) 0%,transparent 50%);
  opacity:0;transition:opacity .35s;
  display:flex;align-items:flex-end;padding:20px 22px}
.hgg-item:hover .hgg-overlay{opacity:1}
.hgg-label{font-family:'Playfair Display',serif;font-size:1rem;font-style:italic;color:#fff}

/* HOME DOGS PREVIEW */
.dogs-preview{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin:3px 0}
.dog-card-home{position:relative;overflow:hidden;cursor:pointer;aspect-ratio:3/4}
.dog-card-home img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.7) brightness(.75);
  transition:transform .7s cubic-bezier(.22,1,.36,1),filter .5s}
.dog-card-home:hover img{transform:scale(1.07);filter:saturate(1) brightness(.85)}
.dog-card-home-info{position:absolute;bottom:0;left:0;right:0;
  background:linear-gradient(to top,rgba(0,0,0,.88),transparent);
  padding:28px 24px 20px;transform:translateY(8px);transition:transform .35s}
.dog-card-home:hover .dog-card-home-info{transform:translateY(0)}
.dc-breed{font-size:.65rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:4px}
.dc-name{font-family:'Playfair Display',serif;font-size:1.4rem;font-style:italic}
.dc-title{font-size:.75rem;color:rgba(255,255,255,.55);margin-top:2px}

/* HOME EVENTS */
.events-row{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;margin:3px 0 0}
.event-card-home{background:var(--card);border:1px solid var(--border);cursor:pointer;
  overflow:hidden;transition:border-color .25s,transform .3s cubic-bezier(.22,1,.36,1)}
.event-card-home:hover{border-color:#333;transform:translateY(-5px)}
.ech-img{height:200px;overflow:hidden}
.ech-img img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.7);transition:transform .6s,filter .4s}
.event-card-home:hover .ech-img img{transform:scale(1.06);filter:saturate(1)}
.ech-body{padding:22px 24px}
.ech-type{font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:8px}
.ech-name{font-family:'Playfair Display',serif;font-size:1.2rem;margin-bottom:8px;line-height:1.3}
.ech-date{font-size:.75rem;color:var(--muted)}

/* ── PAGE HEADER ─────────────────────────────────────────────── */
.page-hero{position:relative;height:340px;overflow:hidden;display:flex;align-items:flex-end}
.page-hero img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;
  filter:brightness(.35) saturate(.6)}
.page-hero::after{content:'';position:absolute;inset:0;
  background:linear-gradient(to top,var(--bg) 0%,transparent 60%)}
.page-hero-content{position:relative;z-index:2;padding:0 52px 48px}
.ph-tag{font-size:.68rem;letter-spacing:4px;text-transform:uppercase;color:var(--accent);margin-bottom:12px}
.ph-h{font-family:'Playfair Display',serif;font-size:clamp(2.5rem,6vw,5rem);
  letter-spacing:1px;line-height:.92}
.ph-h em{font-style:italic;color:var(--accent)}

/* ── DOGS PAGE ───────────────────────────────────────────────── */
.dogs-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(320px,1fr));gap:2px;
  padding:3px 0}
.dog-card{position:relative;overflow:hidden;cursor:pointer;aspect-ratio:4/5}
.dog-card img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.7) brightness(.8);
  transition:transform .7s cubic-bezier(.22,1,.36,1),filter .5s}
.dog-card:hover img{transform:scale(1.06);filter:saturate(1) brightness(.9)}
.dog-overlay{position:absolute;inset:0;
  background:linear-gradient(to top,rgba(0,0,0,.9) 0%,transparent 55%);
  display:flex;flex-direction:column;justify-content:flex-end;
  padding:28px 26px;transform:translateY(10px);transition:transform .4s}
.dog-card:hover .dog-overlay{transform:translateY(0)}
.do-breed{font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:6px}
.do-name{font-family:'Playfair Display',serif;font-size:2rem;font-style:italic;line-height:1}
.do-titles{font-size:.75rem;color:rgba(255,255,255,.5);margin-top:6px;line-height:1.6}
.do-btn{display:inline-block;margin-top:14px;font-size:.68rem;letter-spacing:2px;
  text-transform:uppercase;color:var(--accent);
  border-bottom:1px solid var(--accent);padding-bottom:2px;
  opacity:0;transition:opacity .3s}
.dog-card:hover .do-btn{opacity:1}

/* DOG DETAIL */
.dog-detail{max-width:1200px;margin:0 auto;padding:60px 52px 100px;
  display:grid;grid-template-columns:1fr 1fr;gap:72px;align-items:start}
.dd-img-wrap{position:relative}
.dd-img-wrap img{width:100%;aspect-ratio:3/4;object-fit:cover;filter:saturate(.85)}
.dd-badge{position:absolute;bottom:20px;right:20px;
  background:var(--accent);color:#080808;
  font-size:.65rem;letter-spacing:2.5px;text-transform:uppercase;padding:6px 14px;font-weight:500}
.dd-info{}
.dd-breed{font-size:.68rem;letter-spacing:4px;text-transform:uppercase;color:var(--accent);margin-bottom:14px}
.dd-name{font-family:'Playfair Display',serif;font-size:3.5rem;font-style:italic;
  line-height:.92;margin-bottom:8px}
.dd-full{font-family:'Playfair Display',serif;font-size:1rem;color:var(--muted2);
  margin-bottom:32px;font-weight:300}
.dd-desc{color:var(--muted2);line-height:1.9;font-size:.92rem;margin-bottom:36px;font-weight:300}
.dd-stats{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:36px}
.dd-stat{background:var(--card);border:1px solid var(--border);padding:16px 18px}
.dds-label{font-size:.62rem;letter-spacing:2.5px;text-transform:uppercase;color:var(--muted);margin-bottom:4px}
.dds-val{font-size:.92rem;color:var(--text)}
.dd-titles-list{border-top:1px solid var(--border);padding-top:24px}
.dtl-head{font-size:.68rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:14px}
.dtl-item{font-size:.82rem;color:var(--muted2);padding:8px 0;border-bottom:1px solid var(--border);
  display:flex;justify-content:space-between}
.dtl-year{color:var(--muted)}

/* ── HODOWLA PAGE ────────────────────────────────────────────── */
.hodowla-intro{display:grid;grid-template-columns:1fr 1fr;gap:0;overflow:hidden;
  border-bottom:1px solid var(--border)}
.hi-text{padding:72px 52px;display:flex;flex-direction:column;justify-content:center}
.hi-img{overflow:hidden}
.hi-img img{width:100%;height:100%;object-fit:cover;filter:saturate(.75) brightness(.8);
  transition:transform .8s}
.hi-img:hover img{transform:scale(1.04)}
.hodowla-values{display:grid;grid-template-columns:repeat(3,1fr);
  border-bottom:1px solid var(--border)}
.hv-item{padding:48px 40px;border-right:1px solid var(--border);
  transition:background .3s}
.hv-item:last-child{border-right:none}
.hv-item:hover{background:var(--accent-soft)}
.hv-num{font-family:'Playfair Display',serif;font-size:3.5rem;color:var(--accent);
  opacity:.3;line-height:1;margin-bottom:16px}
.hv-title{font-family:'Playfair Display',serif;font-size:1.3rem;margin-bottom:12px}
.hv-desc{font-size:.82rem;color:var(--muted);line-height:1.8;font-weight:300}

/* ── GALERIA PAGE ────────────────────────────────────────────── */
.gallery-filters{padding:28px 52px;display:flex;gap:10px;flex-wrap:wrap;align-items:center;
  border-bottom:1px solid var(--border)}
.gf-label{font-size:.68rem;color:var(--muted);text-transform:uppercase;letter-spacing:2px;margin-right:8px}
.gf-btn{background:transparent;border:1px solid var(--border);color:var(--muted2);
  padding:6px 18px;font-family:'Jost',sans-serif;font-size:.75rem;letter-spacing:.5px;
  cursor:pointer;transition:all .2s}
.gf-btn:hover{border-color:var(--accent);color:var(--text)}
.gf-btn.active{background:var(--accent);border-color:var(--accent);color:#080808;font-weight:500}
.gallery-masonry{padding:32px 52px 80px;columns:3;column-gap:12px}
.gm-item{break-inside:avoid;margin-bottom:12px;overflow:hidden;cursor:pointer;
  border:1px solid var(--border);transition:transform .35s cubic-bezier(.22,1,.36,1),border-color .2s}
.gm-item:hover{transform:translateY(-4px);border-color:#333}
.gm-item img{width:100%;display:block;filter:saturate(.8);transition:transform .6s,filter .4s}
.gm-item:hover img{transform:scale(1.05);filter:saturate(1)}

/* ── EVENTS PAGE ─────────────────────────────────────────────── */
.events-grid-page{padding:40px 52px 80px;
  display:grid;grid-template-columns:repeat(auto-fill,minmax(380px,1fr));gap:24px}
.event-card-page{background:var(--card);border:1px solid var(--border);
  cursor:pointer;overflow:hidden;
  transition:transform .35s cubic-bezier(.22,1,.36,1),border-color .25s}
.event-card-page:hover{transform:translateY(-6px);border-color:#2a2a2a}
.ecp-img{height:240px;overflow:hidden;position:relative}
.ecp-img img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.7);transition:transform .6s,filter .4s}
.event-card-page:hover .ecp-img img{transform:scale(1.07);filter:saturate(1)}
.ecp-type{position:absolute;bottom:14px;left:14px;
  background:var(--accent);color:#080808;
  font-size:.6rem;letter-spacing:2.5px;text-transform:uppercase;padding:4px 12px;font-weight:500}
.ecp-body{padding:24px 26px}
.ecp-date{font-size:.7rem;color:var(--muted);letter-spacing:1.5px;margin-bottom:8px}
.ecp-name{font-family:'Playfair Display',serif;font-size:1.4rem;margin-bottom:10px;line-height:1.2}
.ecp-desc{font-size:.82rem;color:var(--muted2);line-height:1.7;margin-bottom:16px}
.ecp-footer{border-top:1px solid var(--border);padding-top:14px;
  display:flex;justify-content:space-between;align-items:center}
.ecp-place{font-size:.72rem;color:var(--muted)}
.ecp-arrow{color:var(--accent);transition:transform .2s}
.event-card-page:hover .ecp-arrow{transform:translateX(4px)}

/* ── BLOG PAGE ───────────────────────────────────────────────── */
.blog-grid-page{padding:40px 52px 80px;
  display:grid;grid-template-columns:repeat(auto-fill,minmax(360px,1fr));gap:28px}
.blog-card-page{background:var(--card);border:1px solid var(--border);
  cursor:pointer;overflow:hidden;
  transition:transform .35s cubic-bezier(.22,1,.36,1),border-color .25s}
.blog-card-page:hover{transform:translateY(-6px);border-color:#2a2a2a}
.bcp-img{height:240px;overflow:hidden}
.bcp-img img{width:100%;height:100%;object-fit:cover;
  filter:saturate(.7);transition:transform .6s,filter .4s}
.blog-card-page:hover .bcp-img img{transform:scale(1.07);filter:saturate(1)}
.bcp-body{padding:26px 28px}
.bcp-cat{font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:10px}
.bcp-title{font-family:'Playfair Display',serif;font-size:1.4rem;line-height:1.3;margin-bottom:12px}
.bcp-exc{font-size:.82rem;color:var(--muted2);line-height:1.75;margin-bottom:18px}
.bcp-footer{border-top:1px solid var(--border);padding-top:14px;
  display:flex;justify-content:space-between;align-items:center}
.bcp-date{font-size:.72rem;color:var(--muted)}
.bcp-read{font-size:.7rem;color:var(--accent);letter-spacing:1.5px;text-transform:uppercase}

/* BLOG POST */
.post-wrap{max-width:800px;margin:0 auto;padding:0 52px 100px}
.post-header{padding:60px 0 40px}
.post-cat-tag{font-size:.65rem;letter-spacing:3.5px;text-transform:uppercase;color:var(--accent);margin-bottom:16px}
.post-title{font-family:'Playfair Display',serif;
  font-size:clamp(2rem,5vw,3.5rem);font-weight:400;line-height:1.15;margin-bottom:20px}
.post-meta{font-size:.78rem;color:var(--muted);display:flex;gap:20px;margin-bottom:40px}
.post-hero-img{width:calc(100% + 104px);margin-left:-52px;height:500px;object-fit:cover;
  filter:saturate(.85);display:block;margin-bottom:56px}
.post-body{line-height:1.95;color:var(--muted2);font-size:.98rem;font-weight:300}
.post-body p{margin-bottom:24px}
.post-body h2{font-family:'Playfair Display',serif;font-size:1.9rem;font-weight:400;
  font-style:italic;color:var(--text);margin:48px 0 20px}
.post-body blockquote{border-left:2px solid var(--accent);padding:16px 24px;
  background:var(--card);margin:32px 0;
  font-family:'Playfair Display',serif;font-size:1.25rem;font-style:italic;
  color:var(--muted2);line-height:1.65}
.post-tags{display:flex;gap:8px;flex-wrap:wrap;margin-top:48px;padding-top:32px;
  border-top:1px solid var(--border)}
.ptag{font-size:.68rem;letter-spacing:1.5px;text-transform:uppercase;
  border:1px solid var(--border);color:var(--muted2);padding:4px 14px;
  transition:border-color .2s,color .2s;cursor:default}
.ptag:hover{border-color:var(--accent);color:var(--accent)}

/* ── KONTAKT PAGE ────────────────────────────────────────────── */
.kontakt-wrap{max-width:680px;margin:60px auto 100px;padding:0 52px}
.kontakt-grid{display:grid;gap:16px}
.k-label{font-size:.68rem;letter-spacing:2.5px;text-transform:uppercase;color:var(--muted);
  display:block;margin-bottom:8px}
.k-input{width:100%;background:var(--card);border:1px solid var(--border);
  color:var(--text);padding:12px 16px;font-family:'Jost',sans-serif;font-size:.92rem;
  outline:none;transition:border-color .2s}
.k-input:focus{border-color:var(--accent)}
.k-textarea{resize:vertical;min-height:140px}
.kontakt-info{margin-top:60px;padding-top:40px;border-top:1px solid var(--border);
  display:grid;grid-template-columns:repeat(3,1fr);gap:32px}
.ki-label{font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:8px}
.ki-val{font-size:.88rem;color:var(--muted2)}

/* ── LIGHTBOX ────────────────────────────────────────────────── */
.lightbox{position:fixed;inset:0;background:rgba(0,0,0,.96);z-index:500;
  display:flex;align-items:center;justify-content:center;
  opacity:0;pointer-events:none;transition:opacity .35s}
.lightbox.open{opacity:1;pointer-events:all}
.lb-img{max-height:90vh;max-width:90vw;object-fit:contain;display:block}
.lb-close{position:fixed;top:24px;right:28px;background:none;border:none;
  color:var(--muted);font-size:2rem;cursor:pointer;transition:color .2s;z-index:501}
.lb-close:hover{color:var(--text)}

/* ── BACK BUTTON ─────────────────────────────────────────────── */
.back-btn{display:inline-flex;align-items:center;gap:8px;color:var(--muted2);
  cursor:pointer;font-size:.75rem;letter-spacing:2px;text-transform:uppercase;
  padding:24px 52px 0;transition:color .2s}
.back-btn:hover{color:var(--accent)}

/* ── FOOTER ──────────────────────────────────────────────────── */
footer{border-top:1px solid var(--border);padding:36px 52px;
  display:flex;justify-content:space-between;align-items:center;
  color:var(--muted);font-size:.75rem}
.footer-logo{font-family:'Playfair Display',serif;font-size:1.1rem;color:var(--muted2)}
.footer-logo em{color:var(--accent);font-style:italic}

/* ── TOAST ───────────────────────────────────────────────────── */
.toast{position:fixed;bottom:32px;left:50%;
  transform:translateX(-50%) translateY(80px);
  background:var(--accent);color:#080808;padding:12px 30px;
  font-size:.82rem;font-weight:500;z-index:600;
  transition:transform .4s cubic-bezier(.22,1,.36,1);white-space:nowrap}
.toast.show{transform:translateX(-50%) translateY(0)}
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="logo" onclick="showPage('home')">
    <span class="logo-paw">🐾</span>
    <span class="logo-text">Spring<em>erowo</em></span>
  </div>
  <ul class="nav-links">
    <li><a id="nav-home"     onclick="showPage('home')"     class="active">Start</a></li>
    <li><a id="nav-psy"      onclick="showPage('psy')">Nasze psy</a></li>
    <li><a id="nav-hodowla"  onclick="showPage('hodowla')">Hodowla</a></li>
    <li><a id="nav-events"   onclick="showPage('events')">Eventy</a></li>
    <li><a id="nav-galeria"  onclick="showPage('galeria')">Galeria</a></li>
    <li><a id="nav-blog"     onclick="showPage('blog')">Blog</a></li>
    <li><a id="nav-kontakt"  onclick="showPage('kontakt')">Kontakt</a></li>
  </ul>
</nav>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- HOME                                                           -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-home" class="page active">
  <div class="home-hero">
    <div class="hero-bg">
      <img src="https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=1800&q=85" alt="">
    </div>
    <div class="hero-content">
      <div class="hero-tag">Hodowla · Sport · Trening · Fotografia</div>
      <h1 class="hero-h">Spring<br><span class="italic">erowo</span></h1>
      <p class="hero-sub">Pasja do Springer Spanieli przekuta w hodowlę, sport kynologiczny i fotografię. Tu żyją psy z charakterem.</p>
      <div class="hero-ctas">
        <button class="btn-gold" onclick="showPage('psy')">Poznaj nasze psy</button>
        <button class="btn-outline" onclick="showPage('hodowla')">O hodowli</button>
      </div>
    </div>
    <div class="hero-scroll"><span class="scroll-line"></span>Przewiń</div>
  </div>

  <!-- ABOUT -->
  <div class="about-strip">
    <div class="about-img">
      <img src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=900&q=80" alt="">
    </div>
    <div class="about-text">
      <div class="about-kicker">O mnie</div>
      <h2 class="about-h">Springer Spaniele<br>to mój <em>świat</em></h2>
      <p class="about-body">Od ponad dekady hodują English Springer Spaniele z pasją do sportu kynologicznego, wystaw i zdrowej hodowli. Każdy pies to osobna historia — pełna medali, przygód i bezwarunkowej miłości.</p>
      <p class="about-body">Jestem też fotografem — uchwytującym te ulotne momenty, kiedy pies i człowiek tworzą doskonały duet.</p>
      <div class="about-tags">
        <span class="tag">English Springer Spaniel</span>
        <span class="tag">Wystawy FCI</span>
        <span class="tag">Agility</span>
        <span class="tag">Fotografia</span>
        <span class="tag">Hodowla ZKwP</span>
      </div>
    </div>
  </div>

  <!-- PILLARS -->
  <div class="pillars">
    <div class="pillar" onclick="showPage('psy')">
      <div class="pillar-icon">🐕</div>
      <div class="pillar-name">Nasze psy</div>
      <div class="pillar-desc">Poznaj naszych Springerów — każdy z własnym charakterem, tytułami i historią.</div>
      <span class="pillar-link">Zobacz →</span>
    </div>
    <div class="pillar" onclick="showPage('hodowla')">
      <div class="pillar-icon">🏡</div>
      <div class="pillar-name">Hodowla</div>
      <div class="pillar-desc">Zarejestrowana hodowla ZKwP. Zdrowie, temperament i rasowość na pierwszym miejscu.</div>
      <span class="pillar-link">Dowiedz się więcej →</span>
    </div>
    <div class="pillar" onclick="showPage('events')">
      <div class="pillar-icon">🏆</div>
      <div class="pillar-name">Eventy & Zawody</div>
      <div class="pillar-desc">Wystawy, zawody agility, szkolenia — relacje i zdjęcia z naszego życia w sporcie.</div>
      <span class="pillar-link">Przeglądaj →</span>
    </div>
    <div class="pillar" onclick="showPage('galeria')">
      <div class="pillar-icon">📷</div>
      <div class="pillar-name">Galeria</div>
      <div class="pillar-desc">Archiwum fotograficzne — portrety psów, eventy, życie codzienne hodowli.</div>
      <span class="pillar-link">Galeria →</span>
    </div>
  </div>

  <!-- GALLERY PREVIEW -->
  <div class="sec-head">
    <h2 class="sec-h">Ostatnie <em>zdjęcia</em></h2>
    <span class="sec-more" onclick="showPage('galeria')">Cała galeria →</span>
  </div>
  <div class="home-gallery-grid">
    <div class="hgg-item tall" onclick="openLB('https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=1200&q=90')">
      <img src="https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=800&q=80" alt="">
      <div class="hgg-overlay"><span class="hgg-label">Portret</span></div>
    </div>
    <div class="hgg-item" onclick="openLB('https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1200&q=90')">
      <img src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=600&q=80" alt="">
      <div class="hgg-overlay"><span class="hgg-label">Agility</span></div>
    </div>
    <div class="hgg-item" onclick="openLB('https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=1200&q=90')">
      <img src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=600&q=80" alt="">
      <div class="hgg-overlay"><span class="hgg-label">Trening</span></div>
    </div>
    <div class="hgg-item" onclick="openLB('https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=1200&q=90')">
      <img src="https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=600&q=80" alt="">
      <div class="hgg-overlay"><span class="hgg-label">Wystawa</span></div>
    </div>
    <div class="hgg-item" onclick="openLB('https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=1200&q=90')">
      <img src="https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=600&q=80" alt="">
      <div class="hgg-overlay"><span class="hgg-label">Codzienność</span></div>
    </div>
  </div>

  <!-- DOGS PREVIEW -->
  <div class="sec-head">
    <h2 class="sec-h">Nasze <em>psy</em></h2>
    <span class="sec-more" onclick="showPage('psy')">Wszyscy →</span>
  </div>
  <div class="dogs-preview">
    <div class="dog-card-home" onclick="showPage('psy')">
      <img src="https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=700&q=80" alt="">
      <div class="dog-card-home-info">
        <div class="dc-breed">English Springer Spaniel</div>
        <div class="dc-name">Luna</div>
        <div class="dc-title">JCh. PL · Ch. PL</div>
      </div>
    </div>
    <div class="dog-card-home" onclick="showPage('psy')">
      <img src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=700&q=80" alt="">
      <div class="dog-card-home-info">
        <div class="dc-breed">English Springer Spaniel</div>
        <div class="dc-name">Axis</div>
        <div class="dc-title">Ch. PL · Agility Grade 3</div>
      </div>
    </div>
    <div class="dog-card-home" onclick="showPage('psy')">
      <img src="https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=700&q=80" alt="">
      <div class="dog-card-home-info">
        <div class="dc-breed">English Springer Spaniel</div>
        <div class="dc-name">Riko</div>
        <div class="dc-title">JCh. PL · Kandydat Ch.</div>
      </div>
    </div>
  </div>

  <!-- EVENTS PREVIEW -->
  <div class="sec-head">
    <h2 class="sec-h">Ostatnie <em>eventy</em></h2>
    <span class="sec-more" onclick="showPage('events')">Wszystkie →</span>
  </div>
  <div class="events-row">
    <div class="event-card-home" onclick="openEventDetail(0)">
      <div class="ech-img"><img src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=600&q=80" alt=""></div>
      <div class="ech-body">
        <div class="ech-type">Zawody Agility</div>
        <div class="ech-name">Mistrzostwa Polski Agility 2024</div>
        <div class="ech-date">14–15 września 2024 · Warszawa</div>
      </div>
    </div>
    <div class="event-card-home" onclick="openEventDetail(1)">
      <div class="ech-img"><img src="https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=600&q=80" alt=""></div>
      <div class="ech-body">
        <div class="ech-type">Wystawa</div>
        <div class="ech-name">Międzynarodowa Wystawa Psów CACIB Kraków</div>
        <div class="ech-date">6 października 2024 · Kraków</div>
      </div>
    </div>
    <div class="event-card-home" onclick="openEventDetail(2)">
      <div class="ech-img"><img src="https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=600&q=80" alt=""></div>
      <div class="ech-body">
        <div class="ech-type">Szkolenie</div>
        <div class="ech-name">Obóz Szkoleniowy Springer Spaniel Club</div>
        <div class="ech-date">2–4 sierpnia 2024 · Mazury</div>
      </div>
    </div>
  </div>

  <footer>
    <span class="footer-logo">Spring<em>erowo</em></span>
    <span>© 2025 Springerowo · Hodowla ZKwP</span>
    <span>kontakt@springerowo.pl</span>
  </footer>
</div>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- NASZE PSY                                                      -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-psy" class="page">
  <div class="page-hero">
    <img src="https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=1600&q=85" alt="">
    <div class="page-hero-content">
      <div class="ph-tag">Hodowla Springerowo</div>
      <h1 class="ph-h">Nasze <em>psy</em></h1>
    </div>
  </div>
  <div class="dogs-grid" id="dogsGrid"></div>
</div>

<!-- DOG DETAIL -->
<div id="page-dog-detail" class="page">
  <span class="back-btn" onclick="showPage('psy')">← Powrót do psów</span>
  <div class="dog-detail" id="dogDetail"></div>
</div>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- HODOWLA                                                        -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-hodowla" class="page">
  <div class="page-hero">
    <img src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=1600&q=85" alt="">
    <div class="page-hero-content">
      <div class="ph-tag">O nas</div>
      <h1 class="ph-h">Ho<em>dowla</em></h1>
    </div>
  </div>

  <div class="hodowla-intro">
    <div class="hi-text" style="padding:72px 52px">
      <div class="about-kicker">Nasza filozofia</div>
      <h2 class="about-h" style="font-size:2.6rem">Zdrowie.<br>Charakter.<br><em>Piękno.</em></h2>
      <p class="about-body" style="margin-top:24px">Hodowla Springerowo działa pod patronatem ZKwP od 2013 roku. Specjalizujemy się w English Springer Spanielach — rasie łączącej elegancję wystawową z niesamowitymi zdolnościami sportowymi.</p>
      <p class="about-body">Wszystkie nasze psy są regularnie badane pod kątem dysplazji bioder, oczu i innych chorób genetycznych. Dobieramy pary z dbałością o różnorodność genetyczną i wzmocnienie najlepszych cech rasy.</p>
      <button class="btn-gold" style="width:fit-content;margin-top:16px" onclick="showPage('kontakt')">Zapytaj o szczenięta</button>
    </div>
    <div class="hi-img">
      <img src="https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=900&q=80" alt="">
    </div>
  </div>

  <div class="hodowla-values">
    <div class="hv-item">
      <div class="hv-num">01</div>
      <div class="hv-title">Zdrowie przede wszystkim</div>
      <div class="hv-desc">Każdy reproduktor posiada aktualne badania: dysplazja bioder (HD/ED), badania oczu (CAER), test DNA. Szczenięta wyjeżdżają zaszczepione, odrobaczone i z kompletem dokumentów FCI.</div>
    </div>
    <div class="hv-item">
      <div class="hv-num">02</div>
      <div class="hv-title">Temperament i praca</div>
      <div class="hv-desc">Springer Spaniel to pies do pracy i sportu. Nasze linie łączą wystawowe tytuły z wynikami w agility, nosework i strzelectwie. Szczenięta socjalizujemy od urodzenia.</div>
    </div>
    <div class="hv-item">
      <div class="hv-num">03</div>
      <div class="hv-title">Wsparcie przez całe życie</div>
      <div class="hv-desc">Nabywcy naszych szczeniąt mogą liczyć na stałe wsparcie — od diety i szczepień po porady treningowe i wystawowe. Jesteśmy dostępni zawsze, gdy potrzebna jest pomoc.</div>
    </div>
  </div>

  <div class="sec-head" style="border-top:1px solid var(--border)">
    <h2 class="sec-h">Plany <em>miotów</em></h2>
  </div>
  <div style="padding:32px 52px 80px;display:grid;grid-template-columns:repeat(auto-fill,minmax(360px,1fr));gap:20px">
    <div style="background:var(--card);border:1px solid var(--border);padding:32px">
      <div style="font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:12px">Planowany miot</div>
      <div style="font-family:'Playfair Display',serif;font-size:1.5rem;margin-bottom:8px">Luna × Champ</div>
      <div style="font-size:.82rem;color:var(--muted2);line-height:1.7;margin-bottom:16px">Planowany na wiosnę 2025. Luna — Ch. PL, HD-A, badania oczu czyste. Champ — Multi Ch., tytuły w 5 krajach.</div>
      <button class="btn-outline" style="font-size:.7rem;padding:10px 24px" onclick="showPage('kontakt')">Zapisz się na listę →</button>
    </div>
    <div style="background:var(--card);border:1px solid var(--border);padding:32px">
      <div style="font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--muted);margin-bottom:12px">Informacyjnie</div>
      <div style="font-family:'Playfair Display',serif;font-size:1.5rem;margin-bottom:8px">Wymagania dla nabywców</div>
      <div style="font-size:.82rem;color:var(--muted2);line-height:1.7">Szczenięta trafiają do domów z ogrodem lub zapewniających odpowiednią aktywność. Wymagana umowa i zobowiązanie kastracyjne dla psów niehodowlanych.</div>
    </div>
  </div>
  <footer style="border-top:1px solid var(--border);padding:36px 52px;display:flex;justify-content:space-between;color:var(--muted);font-size:.75rem">
    <span class="footer-logo">Spring<em>erowo</em></span>
    <span>© 2025 Springerowo · Hodowla ZKwP</span>
    <span>kontakt@springerowo.pl</span>
  </footer>
</div>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- EVENTS                                                         -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-events" class="page">
  <div class="page-hero">
    <img src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1600&q=85" alt="">
    <div class="page-hero-content">
      <div class="ph-tag">Z naszego życia</div>
      <h1 class="ph-h">E<em>venty</em> & Zawody</h1>
    </div>
  </div>
  <div class="events-grid-page" id="eventsGrid"></div>
</div>

<!-- EVENT DETAIL -->
<div id="page-event-detail" class="page">
  <span class="back-btn" onclick="showPage('events')">← Powrót do eventów</span>
  <div id="eventDetailContent"></div>
</div>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- GALERIA                                                        -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-galeria" class="page">
  <div class="page-hero">
    <img src="https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=1600&q=85" alt="">
    <div class="page-hero-content">
      <div class="ph-tag">Archiwum fotograficzne</div>
      <h1 class="ph-h"><em>Galeria</em></h1>
    </div>
  </div>
  <div class="gallery-filters">
    <span class="gf-label">Filtruj:</span>
    <button class="gf-btn active" onclick="filterGallery('all',this)">Wszystkie</button>
    <button class="gf-btn" onclick="filterGallery('portret',this)">Portrety</button>
    <button class="gf-btn" onclick="filterGallery('sport',this)">Sport</button>
    <button class="gf-btn" onclick="filterGallery('wystawa',this)">Wystawy</button>
    <button class="gf-btn" onclick="filterGallery('codzien',this)">Codzienność</button>
  </div>
  <div class="gallery-masonry" id="galleryMasonry"></div>
</div>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- BLOG                                                           -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-blog" class="page">
  <div class="page-hero">
    <img src="https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=1600&q=85" alt="">
    <div class="page-hero-content">
      <div class="ph-tag">Notatki z hodowli i sportu</div>
      <h1 class="ph-h"><em>Blog</em></h1>
    </div>
  </div>
  <div class="blog-grid-page" id="blogGrid"></div>
</div>

<!-- BLOG POST -->
<div id="page-post" class="page">
  <span class="back-btn" onclick="showPage('blog')">← Powrót do bloga</span>
  <div class="post-wrap">
    <div id="postContent"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════════════ -->
<!-- KONTAKT                                                        -->
<!-- ══════════════════════════════════════════════════════════════ -->
<div id="page-kontakt" class="page">
  <div class="page-hero">
    <img src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=1600&q=85" alt="">
    <div class="page-hero-content">
      <div class="ph-tag">Napisz do nas</div>
      <h1 class="ph-h">Kon<em>takt</em></h1>
    </div>
  </div>
  <div class="kontakt-wrap">
    <div class="kontakt-grid" style="margin-top:0">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:16px">
        <div><label class="k-label">Imię i nazwisko</label><input class="k-input" type="text" placeholder="Anna Kowalska"></div>
        <div><label class="k-label">E-mail</label><input class="k-input" type="email" placeholder="anna@example.pl"></div>
      </div>
      <div><label class="k-label">Temat</label>
        <select class="k-input" style="cursor:pointer">
          <option>Pytanie o szczenięta</option>
          <option>Sesja fotograficzna</option>
          <option>Szkolenie / trening</option>
          <option>Wystawy i zawody</option>
          <option>Inne</option>
        </select>
      </div>
      <div><label class="k-label">Wiadomość</label>
        <textarea class="k-input k-textarea" placeholder="Napisz do nas..."></textarea>
      </div>
      <button class="btn-gold" style="width:fit-content" onclick="showToast('Wiadomość wysłana! Odpiszemy wkrótce 🐾')">Wyślij wiadomość</button>
    </div>
    <div class="kontakt-info">
      <div><div class="ki-label">E-mail</div><div class="ki-val">kontakt@springerowo.pl</div></div>
      <div><div class="ki-label">Telefon</div><div class="ki-val">+48 600 000 000</div></div>
      <div><div class="ki-label">Instagram</div><div class="ki-val">@springerowo</div></div>
    </div>
  </div>
</div>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox" onclick="closeLB()">
  <button class="lb-close">✕</button>
  <img class="lb-img" id="lbImg" src="" alt="">
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
// ═══════════════════════════════════════════════════════════════════
// DATA
// ═══════════════════════════════════════════════════════════════════
const dogs = [
  {id:0, name:'Luna', full:'Springerowo Moonlight Sonata', breed:'English Springer Spaniel',
   color:'Wątrobiano-biała', born:'12 marca 2020', sex:'Suka',
   desc:'Luna to nasza prymuska wystawowa — elegancka, pewna siebie i uwielbiająca ring. Zdobyła tytuł Championa Polski jako 18-miesięczna. Poza ringiem jest nieodłączną towarzyszką treningów agility i najlepszą przyjaciółką każdego kota w okolicy.',
   titles:['Junior Champion Polski 2021','Champion Polski 2022','CAC × 8','CACIB × 3'],
   years:['2021','2022','2022–2023','2022–2024'],
   badge:'Reproduktorka', img:'https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=900&q=85',
   stats:{HD:'A/A', Oczy:'Czyste (2024)', Kolor:'Wątrobiano-biały', Wzrost:'49 cm'}},
  {id:1, name:'Axis', full:'Springerowo Axis of the World', breed:'English Springer Spaniel',
   color:'Czarno-biały', born:'5 lipca 2019', sex:'Pies',
   desc:'Axis to nasz sportowiec — niestrudzony, szybki i inteligentny. W agility osiągnął Grade 3, w nosework wygrał kilka regionalnych zawodów. Na wystawach zdobywa serca sędziów swoją energią i kondycją.',
   titles:['Champion Polski 2021','Agility Grade 3','Nosework Regional Winner 2023','CAC × 6'],
   years:['2021','2022','2023','2021–2023'],
   badge:'Reproduktor', img:'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=900&q=85',
   stats:{HD:'A/B', Oczy:'Czyste (2024)', Kolor:'Czarno-biały', Wzrost:'52 cm'}},
  {id:2, name:'Riko', full:'Springerowo Rising Star', breed:'English Springer Spaniel',
   color:'Wątrobiano-biały', born:'18 listopada 2022', sex:'Pies',
   desc:'Najmłodszy z naszych psów — pełen energii i obietnic. Riko ma już Junior Championa Polski i jest kandydatem do tytułu Championa. W wolnym czasie terroryzuje frisbee i porywa serca wszystkich na treningach.',
   titles:['Junior Champion Polski 2023','CAC × 3','Res. CACIB × 1'],
   years:['2023','2023–2024','2024'],
   badge:'Młody talent', img:'https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=900&q=85',
   stats:{HD:'A/A', Oczy:'Czyste (2023)', Kolor:'Wątrobiano-biały', Wzrost:'50 cm'}},
];

const events = [
  {id:0, name:'Mistrzostwa Polski Agility 2024', type:'Zawody Agility',
   date:'14–15 września 2024', place:'Warszawa, Tor Agility Bemowo',
   desc:'Reprezentowaliśmy Springerowo w dwóch kategoriach. Axis zajął 3. miejsce w klasie Large Grade 3, Luna startowała w klasie Large Grade 2 kończąc na 5. pozycji. Niesamowita atmosfera i świetna organizacja.',
   result:'Axis: 3. miejsce Grade 3 Large', img:'https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=900&q=80',
   gallery:['https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=500&q=75','https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=500&q=75','https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=500&q=75']},
  {id:1, name:'Międzynarodowa Wystawa Psów CACIB Kraków', type:'Wystawa',
   date:'6 października 2024', place:'Kraków, EXPO Kraków',
   desc:'Luna zdobyła CACIB i Najlepszego Przedstawiciela Rasy (BOB). Riko dostał ocenę Bardzo Dobry w klasie młodzieży z lokatą 2. Ogromna ekspozycja — ponad 3000 psów z całej Europy.',
   result:'Luna: CACIB + BOB', img:'https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=900&q=80',
   gallery:['https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=500&q=75','https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=500&q=75','https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=500&q=75']},
  {id:2, name:'Obóz Szkoleniowy Springer Spaniel Club', type:'Szkolenie',
   date:'2–4 sierpnia 2024', place:'Mazury, Ośrodek Leśna Polana',
   desc:'Trzy intensywne dni z najlepszymi trenerami w Polsce. Warsztaty z posłuszeństwa, agility i pokazowe sesje zdjęciowe. Zwinęliśmy obóz z wieloma nowymi przyjaźniami (ludzkimi i psimi).',
   result:'Certyfikat ukończenia szkolenia', img:'https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=900&q=80',
   gallery:['https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=500&q=75','https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=500&q=75','https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=500&q=75']},
  {id:3, name:'Krajowa Wystawa Psów Rasowych Wrocław', type:'Wystawa',
   date:'12 maja 2024', place:'Wrocław, Hala Stulecia',
   desc:'Pierwsza wystawa Rika — zdobył ocenę Doskonały i 1. lokatę w klasie szczeniąt. Luna dołożyła kolejny CAC do kolekcji. Piękny, słoneczny dzień pełen psów i emocji.',
   result:'Riko: Doskonały, 1. lokata', img:'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=900&q=80',
   gallery:['https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=500&q=75','https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=500&q=75','https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=500&q=75']},
  {id:4, name:'Regionalne Zawody Nosework', type:'Nosework',
   date:'3 marca 2024', place:'Poznań, Centrum Szkolenia K9',
   desc:'Axis zawalczył w kategorii Exterior i Interior — wygrał obie! To był jego debiut w noseworku na poziomie regionalnym. Niesamowita koncentracja i nos jak laserowy.',
   result:'Axis: 1. miejsce Exterior + Interior', img:'https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=900&q=80',
   gallery:['https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=500&q=75','https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=500&q=75','https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=500&q=75']},
  {id:5, name:'Springer Spaniel Speciality Show', type:'Wystawa',
   date:'18 lutego 2024', place:'Gdańsk, MOSiR',
   desc:'Wyjątkowa specjalistyczna wystawa dla Springer Spanieli. Sędzia z Wielkiej Brytanii oceniał 48 springerów. Luna zdobyła tytuł Best of Breed, Axis Best in Show Sport.',
   result:'Luna: BOB · Axis: BIS Sport', img:'https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=900&q=80',
   gallery:['https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=500&q=75','https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=500&q=75','https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=500&q=75']},
];

const galleryPhotos = [
  {id:0,cat:'portret',img:'https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=700&q=80'},
  {id:1,cat:'sport',  img:'https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=600&q=80'},
  {id:2,cat:'portret',img:'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=700&q=80'},
  {id:3,cat:'wystawa',img:'https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=600&q=80'},
  {id:4,cat:'codzien',img:'https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=700&q=80'},
  {id:5,cat:'sport',  img:'https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=500&q=80'},
  {id:6,cat:'portret',img:'https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=600&q=80'},
  {id:7,cat:'wystawa',img:'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=500&q=80'},
  {id:8,cat:'codzien',img:'https://images.unsplash.com/photo-1534361960057-19f4434a337d?w=700&q=80'},
  {id:9,cat:'sport',  img:'https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=600&q=80'},
  {id:10,cat:'portret',img:'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=700&q=80'},
  {id:11,cat:'wystawa',img:'https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=500&q=80'},
];

const blogPosts = [
  {id:0, cat:'Hodowla', date:'15 listopada 2024', readTime:'5 min',
   title:'Jak przygotować szczeniaka Springer Spaniela na wystawę',
   excerpt:'Pierwszy ring może być stresujący — dla psa i dla właściciela. Opowiadam jak u nas wygląda przygotowanie od pierwszych tygodni życia.',
   img:'https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=1200&q=85',
   tags:['hodowla','wystawy','szczenięta','socjalizacja'],
   content:`<div class="post-cat-tag">Hodowla</div>
<h1 class="post-title">Jak przygotować szczeniaka Springer Spaniela na wystawę</h1>
<div class="post-meta"><span>15 listopada 2024</span><span>·</span><span>5 min czytania</span></div>
<img class="post-hero-img" src="https://images.unsplash.com/photo-1587300003388-59208cc962cb?w=1400&q=90" alt="">
<div class="post-body">
<p>Pierwsze doświadczenia ringowe szczeniaka kształtują jego stosunek do wystaw na całe życie. Dlatego przygotowania zaczynamy znacznie wcześniej niż większość hodowców myśli — jeszcze przed otwarciem oczu.</p>
<h2>Socjalizacja od pierwszych tygodni</h2>
<p>Szczenięta od 3. tygodnia życia przyzwyczajamy do różnych bodźców: dźwięków, faktur podłóg, zapachów obcych ludzi. To fundament pod pewnego siebie wystawowego psa.</p>
<blockquote>Pewność siebie w ringu nie bierze się z treningu — bierze się z bezpiecznego dzieciństwa.</blockquote>
<p>Od 6. tygodnia ćwiczymy stack — ustawianie psa w pozycji wystawowej. Trwają tylko minutę, kończą się smaczkiem. Pies ma się cieszyć, nie pracować.</p>
</div>
<div class="post-tags"><span class="ptag">#hodowla</span><span class="ptag">#wystawy</span><span class="ptag">#szczenięta</span></div>`},
  {id:1, cat:'Sport', date:'2 października 2024', readTime:'7 min',
   title:'Agility z Springerem — dlaczego to idealne połączenie',
   excerpt:'Springer Spaniel i agility to match made in heaven. Energia, inteligencja i zamiłowanie do pracy z człowiekiem sprawiają, że ta rasa błyszczy na torze.',
   img:'https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1200&q=85',
   tags:['agility','sport','springer spaniel','trening'],
   content:`<div class="post-cat-tag">Sport</div>
<h1 class="post-title">Agility z Springerem — dlaczego to idealne połączenie</h1>
<div class="post-meta"><span>2 października 2024</span><span>·</span><span>7 min czytania</span></div>
<img class="post-hero-img" src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1400&q=90" alt="">
<div class="post-body">
<p>Kiedy pierwszy raz postawiłam Axisa przed przeszkodą agility, zrozumiał co robić po... jednej próbie. Springer Spaniele mają w genach chęć do pracy z człowiekiem i niesamowitą zdolność uczenia się przez naśladowanie.</p>
<h2>Predyspozycje rasy</h2>
<p>ESS to pies myśliwski — stworzony do pracy w terenie, szybkich decyzji i ścisłej współpracy z przewodnikiem. Te cechy przekładają się bezpośrednio na sukces w agility.</p>
<blockquote>Axis na torze agility jest tym samym psem co w polu — skupiony, szybki i niestrudzony.</blockquote>
</div>
<div class="post-tags"><span class="ptag">#agility</span><span class="ptag">#sport</span><span class="ptag">#springer</span></div>`},
  {id:2, cat:'Fotografia', date:'18 września 2024', readTime:'6 min',
   title:'Jak fotografować psy w ruchu — moje 5 zasad',
   excerpt:'Pies w biegu to jeden z najtrudniejszych obiektów fotograficznych. Opowiadam o ustawieniach aparatu i technikach które dają ostre, dynamiczne kadry.',
   img:'https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=1200&q=85',
   tags:['fotografia','technika','psy','ruch'],
   content:`<div class="post-cat-tag">Fotografia</div>
<h1 class="post-title">Jak fotografować psy w ruchu — moje 5 zasad</h1>
<div class="post-meta"><span>18 września 2024</span><span>·</span><span>6 min czytania</span></div>
<img class="post-hero-img" src="https://images.unsplash.com/photo-1601979031925-424e53b6caaa?w=1400&q=90" alt="">
<div class="post-body">
<p>Pies w pełnym biegu to marzenie fotografa — i jego koszmar. Miga przez kadr w ułamku sekundy, zmienia kierunek bez ostrzeżenia, a jego oczy muszą być ostre. Po kilku latach fotografowania własnych springerów mam zestaw zasad, które naprawdę działają.</p>
<h2>Zasada 1: Czas naświetlania minimum 1/1000s</h2>
<p>To absolutne minimum dla biegnącego psa. Przy szybszych springerach wolę 1/2000s — szczególnie gdy fotografuję agility lub frisbee.</p>
<blockquote>Ostry nos i rozmyte uszy to zdjęcie zmarnowane. Ostry nos i ostre oczy to portret.</blockquote>
</div>
<div class="post-tags"><span class="ptag">#fotografia</span><span class="ptag">#psy</span><span class="ptag">#technika</span></div>`},
  {id:3, cat:'Życie hodowli', date:'5 sierpnia 2024', readTime:'4 min',
   title:'Nasz miot "L" — relacja z pierwszych tygodni',
   excerpt:'8 szczeniąt, jedna zmęczona Luna i niezliczone godziny spędzone na obserwowaniu jak otwierają oczy. Relacja z naszego ostatniego miotu.',
   img:'https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=1200&q=85',
   tags:['miot','hodowla','szczenięta','luna'],
   content:`<div class="post-cat-tag">Życie hodowli</div>
<h1 class="post-title">Nasz miot "L" — relacja z pierwszych tygodni</h1>
<div class="post-meta"><span>5 sierpnia 2024</span><span>·</span><span>4 min czytania</span></div>
<img class="post-hero-img" src="https://images.unsplash.com/photo-1548199973-03cce0bbc87b?w=1400&q=90" alt="">
<div class="post-body">
<p>6 maja o 3:42 w nocy Luna zaczęła rodzić. Osiem godzin później na świecie było 8 szczeniąt — 5 suk i 3 psy, wszystkie zdrowe i głośne. Najpiękniejszy hałas świata.</p>
<h2>Pierwsze dni</h2>
<p>Pierwsze 72 godziny to maratony karmienia i ważenia. Ważymy każdego szczeniaka dwa razy dziennie — przyrost wagi to najlepszy wskaźnik zdrowia noworodka.</p>
<blockquote>Luna okazała się idealną mamą — spokojna, uważna i nieustraszona. Dumna z niej bardziej niż z jakiegokolwiek tytułu.</blockquote>
</div>
<div class="post-tags"><span class="ptag">#miot</span><span class="ptag">#hodowla</span><span class="ptag">#luna</span></div>`},
];

// ═══════════════════════════════════════════════════════════════════
// PAGE NAVIGATION
// ═══════════════════════════════════════════════════════════════════
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));
  const nl = document.getElementById('nav-'+id);
  if (nl) nl.classList.add('active');
  window.scrollTo(0,0);
  if (id==='galeria') renderGallery();
  if (id==='events')  renderEvents();
  if (id==='blog')    renderBlog();
  if (id==='psy')     renderDogs();
}

// ═══════════════════════════════════════════════════════════════════
// DOGS
// ═══════════════════════════════════════════════════════════════════
function renderDogs() {
  document.getElementById('dogsGrid').innerHTML = dogs.map(d => `
    <div class="dog-card" onclick="openDogDetail(${d.id})">
      <img src="${d.img}" alt="${d.name}" loading="lazy">
      <div class="dog-overlay">
        <div class="do-breed">${d.breed}</div>
        <div class="do-name">${d.name}</div>
        <div class="do-titles">${d.titles.slice(0,2).join(' · ')}</div>
        <span class="do-btn">Zobacz profil →</span>
      </div>
    </div>`).join('');
}

function openDogDetail(id) {
  const d = dogs[id];
  document.getElementById('dogDetail').innerHTML = `
    <div class="dd-img-wrap">
      <img src="${d.img}" alt="${d.name}">
      <span class="dd-badge">${d.badge}</span>
    </div>
    <div class="dd-info">
      <div class="dd-breed">${d.breed}</div>
      <div class="dd-name">${d.name}</div>
      <div class="dd-full">${d.full}</div>
      <p class="dd-desc">${d.desc}</p>
      <div class="dd-stats">
        ${Object.entries(d.stats).map(([k,v])=>`
          <div class="dd-stat">
            <div class="dds-label">${k}</div>
            <div class="dds-val">${v}</div>
          </div>`).join('')}
      </div>
      <div class="dd-titles-list">
        <div class="dtl-head">Tytuły i osiągnięcia</div>
        ${d.titles.map((t,i)=>`
          <div class="dtl-item"><span>${t}</span><span class="dtl-year">${d.years[i]}</span></div>`).join('')}
      </div>
    </div>`;
  showPage('dog-detail');
  document.getElementById('nav-psy').classList.add('active');
}

// ═══════════════════════════════════════════════════════════════════
// EVENTS
// ═══════════════════════════════════════════════════════════════════
function renderEvents() {
  document.getElementById('eventsGrid').innerHTML = events.map(e => `
    <div class="event-card-page" onclick="openEventDetail(${e.id})">
      <div class="ecp-img">
        <img src="${e.img}" alt="${e.name}" loading="lazy">
        <span class="ecp-type">${e.type}</span>
      </div>
      <div class="ecp-body">
        <div class="ecp-date">${e.date}</div>
        <div class="ecp-name">${e.name}</div>
        <div class="ecp-desc">${e.desc.substring(0,120)}...</div>
        <div class="ecp-footer">
          <span class="ecp-place">📍 ${e.place}</span>
          <span class="ecp-arrow">→</span>
        </div>
      </div>
    </div>`).join('');
}

function openEventDetail(id) {
  const e = events[id];
  document.getElementById('eventDetailContent').innerHTML = `
    <div style="position:relative;height:400px;overflow:hidden">
      <img src="${e.img}" style="width:100%;height:100%;object-fit:cover;filter:brightness(.4) saturate(.6)" alt="">
      <div style="position:absolute;inset:0;background:linear-gradient(to top,var(--bg),transparent 60%);display:flex;flex-direction:column;justify-content:flex-end;padding:48px 52px">
        <div style="font-size:.65rem;letter-spacing:3.5px;text-transform:uppercase;color:var(--accent);margin-bottom:10px">${e.type}</div>
        <h2 style="font-family:'Playfair Display',serif;font-size:clamp(2rem,5vw,3.8rem);line-height:.95;font-style:italic">${e.name}</h2>
        <div style="font-size:.82rem;color:rgba(255,255,255,.45);margin-top:12px">${e.date} · ${e.place}</div>
      </div>
    </div>
    <div style="max-width:900px;margin:0 auto;padding:52px 52px 80px;display:grid;grid-template-columns:2fr 1fr;gap:60px">
      <div>
        <p style="color:var(--muted2);line-height:1.9;font-size:.95rem;font-weight:300;margin-bottom:32px">${e.desc}</p>
        <div style="display:columns:3;column-gap:10px;columns:3">
          ${e.gallery.map(img=>`<div style="margin-bottom:10px;overflow:hidden;cursor:pointer" onclick="openLB('${img}')">
            <img src="${img}" style="width:100%;display:block;filter:saturate(.75);transition:transform .5s,filter .3s" onmouseover="this.style.transform='scale(1.05)';this.style.filter='saturate(1)'" onmouseout="this.style.transform='';this.style.filter='saturate(.75)'" loading="lazy">
          </div>`).join('')}
        </div>
      </div>
      <div>
        <div style="background:var(--card);border:1px solid var(--border);padding:24px">
          <div style="font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:14px">Wynik</div>
          <div style="font-family:'Playfair Display',serif;font-size:1.1rem;font-style:italic;color:var(--text)">${e.result}</div>
          <div style="margin-top:20px;padding-top:16px;border-top:1px solid var(--border)">
            <div style="font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--muted);margin-bottom:8px">Data</div>
            <div style="font-size:.85rem;color:var(--muted2)">${e.date}</div>
          </div>
          <div style="margin-top:16px;padding-top:16px;border-top:1px solid var(--border)">
            <div style="font-size:.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--muted);margin-bottom:8px">Miejsce</div>
            <div style="font-size:.85rem;color:var(--muted2)">${e.place}</div>
          </div>
        </div>
      </div>
    </div>`;
  showPage('event-detail');
  document.getElementById('nav-events').classList.add('active');
}

// ═══════════════════════════════════════════════════════════════════
// GALLERY
// ═══════════════════════════════════════════════════════════════════
let galleryFilter = 'all';
function renderGallery() {
  const list = galleryFilter==='all' ? galleryPhotos : galleryPhotos.filter(p=>p.cat===galleryFilter);
  document.getElementById('galleryMasonry').innerHTML = list.map(p=>`
    <div class="gm-item" onclick="openLB('${p.img.replace('w=700','w=1200').replace('w=600','w=1200').replace('w=500','w=1200')}')">
      <img src="${p.img}" loading="lazy">
    </div>`).join('');
}
function filterGallery(cat, btn) {
  galleryFilter = cat;
  document.querySelectorAll('.gf-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderGallery();
}

// ═══════════════════════════════════════════════════════════════════
// BLOG
// ═══════════════════════════════════════════════════════════════════
function renderBlog() {
  document.getElementById('blogGrid').innerHTML = blogPosts.map(p=>`
    <div class="blog-card-page" onclick="openPost(${p.id})">
      <div class="bcp-img"><img src="${p.img}" loading="lazy" alt="${p.title}"></div>
      <div class="bcp-body">
        <div class="bcp-cat">${p.cat}</div>
        <div class="bcp-title">${p.title}</div>
        <div class="bcp-exc">${p.excerpt}</div>
        <div class="bcp-footer">
          <span class="bcp-date">${p.date} · ${p.readTime}</span>
          <span class="bcp-read">Czytaj →</span>
        </div>
      </div>
    </div>`).join('');
}
function openPost(id) {
  const p = blogPosts[id];
  document.getElementById('postContent').innerHTML = p.content;
  showPage('post');
  document.getElementById('nav-blog').classList.add('active');
}

// ═══════════════════════════════════════════════════════════════════
// LIGHTBOX
// ═══════════════════════════════════════════════════════════════════
function openLB(src) {
  document.getElementById('lbImg').src = src;
  document.getElementById('lightbox').classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeLB() {
  document.getElementById('lightbox').classList.remove('open');
  document.body.style.overflow = '';
}

// ═══════════════════════════════════════════════════════════════════
// TOAST
// ═══════════════════════════════════════════════════════════════════
let tt;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(tt); tt = setTimeout(()=>t.classList.remove('show'), 2800);
}

// ═══════════════════════════════════════════════════════════════════
// CURSOR
// ═══════════════════════════════════════════════════════════════════
const cur = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
document.addEventListener('mousemove', e => {
  cur.style.left = e.clientX+'px'; cur.style.top = e.clientY+'px';
  ring.style.left = e.clientX+'px'; ring.style.top = e.clientY+'px';
});
document.addEventListener('mousedown', ()=>{ cur.style.width='6px';cur.style.height='6px'; });
document.addEventListener('mouseup',   ()=>{ cur.style.width='10px';cur.style.height='10px'; });
</script>
</body>
</html>
