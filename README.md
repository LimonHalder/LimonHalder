<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Limon Halder — AI Researcher</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:ital,wght@0,300;0,400;1,300&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #050810;
      --bg2: #080d1a;
      --surface: #0c1425;
      --border: rgba(99,179,237,0.12);
      --accent: #63b3ed;
      --accent2: #a78bfa;
      --accent3: #34d399;
      --text: #e2eaf8;
      --muted: #7a90b0;
      --glow: rgba(99,179,237,0.15);
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'DM Mono', monospace;
      overflow-x: hidden;
      cursor: none;
    }

    /* Custom cursor */
    .cursor {
      position: fixed; width: 10px; height: 10px;
      background: var(--accent); border-radius: 50%;
      pointer-events: none; z-index: 9999;
      transform: translate(-50%,-50%);
      transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
      mix-blend-mode: screen;
    }
    .cursor-ring {
      position: fixed; width: 36px; height: 36px;
      border: 1.5px solid var(--accent); border-radius: 50%;
      pointer-events: none; z-index: 9998;
      transform: translate(-50%,-50%);
      transition: transform 0.18s ease, width 0.25s, height 0.25s, opacity 0.2s;
      opacity: 0.5;
    }

    /* Starfield */
    #stars { position: fixed; inset: 0; z-index: 0; overflow: hidden; pointer-events: none; }
    .star {
      position: absolute; border-radius: 50%;
      background: white; opacity: 0;
      animation: twinkle var(--d, 4s) var(--delay, 0s) infinite ease-in-out;
    }
    @keyframes twinkle {
      0%, 100% { opacity: 0; transform: scale(0.8); }
      50% { opacity: var(--op, 0.7); transform: scale(1); }
    }

    /* Noise overlay */
    body::before {
      content: '';
      position: fixed; inset: 0; z-index: 1;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none; opacity: 0.4;
    }

    /* Nav */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; justify-content: space-between; align-items: center;
      padding: 1.2rem 4rem;
      background: rgba(5,8,16,0.8);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
    }
    .nav-logo {
      font-family: 'Syne', sans-serif;
      font-weight: 800; font-size: 1.1rem;
      color: var(--accent); letter-spacing: 0.05em;
    }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      color: var(--muted); text-decoration: none;
      font-size: 0.75rem; letter-spacing: 0.12em; text-transform: uppercase;
      transition: color 0.2s;
    }
    .nav-links a:hover { color: var(--accent); }

    /* Sections */
    section { position: relative; z-index: 2; }

    /* Hero */
    #hero {
      min-height: 100vh;
      display: flex; align-items: center; justify-content: center;
      padding: 8rem 4rem 4rem;
      text-align: center;
      overflow: hidden;
    }
    .hero-glow {
      position: absolute;
      width: 600px; height: 600px;
      background: radial-gradient(circle, rgba(99,179,237,0.08) 0%, transparent 70%);
      border-radius: 50%;
      top: 50%; left: 50%; transform: translate(-50%,-50%);
      animation: pulse 6s ease-in-out infinite;
    }
    .hero-glow2 {
      position: absolute;
      width: 400px; height: 400px;
      background: radial-gradient(circle, rgba(167,139,250,0.06) 0%, transparent 70%);
      border-radius: 50%;
      top: 40%; left: 55%; transform: translate(-50%,-50%);
      animation: pulse 8s ease-in-out infinite reverse;
    }
    @keyframes pulse {
      0%, 100% { transform: translate(-50%,-50%) scale(1); opacity: 1; }
      50% { transform: translate(-50%,-50%) scale(1.1); opacity: 0.7; }
    }
    .hero-content { position: relative; z-index: 2; max-width: 900px; }
    .hero-tag {
      display: inline-block;
      font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
      color: var(--accent3); border: 1px solid rgba(52,211,153,0.3);
      padding: 0.35rem 1rem; border-radius: 2rem;
      margin-bottom: 2rem;
      animation: fadeUp 0.8s ease forwards;
    }
    .hero-name {
      font-family: 'Syne', sans-serif;
      font-size: clamp(3.5rem, 8vw, 7rem);
      font-weight: 800; line-height: 0.95;
      letter-spacing: -0.02em;
      background: linear-gradient(135deg, #fff 0%, var(--accent) 50%, var(--accent2) 100%);
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      background-clip: text;
      animation: fadeUp 0.8s 0.1s ease both;
    }
    .hero-title {
      font-family: 'Instrument Serif', serif;
      font-style: italic;
      font-size: clamp(1.1rem, 2.5vw, 1.6rem);
      color: var(--muted); margin-top: 1rem;
      animation: fadeUp 0.8s 0.2s ease both;
    }
    .hero-desc {
      font-size: 0.85rem; line-height: 1.9; color: var(--muted);
      max-width: 600px; margin: 1.5rem auto 0;
      animation: fadeUp 0.8s 0.3s ease both;
    }
    .hero-cta {
      display: flex; gap: 1rem; justify-content: center;
      margin-top: 2.5rem;
      animation: fadeUp 0.8s 0.4s ease both;
    }
    .btn {
      display: inline-flex; align-items: center; gap: 0.5rem;
      padding: 0.75rem 1.8rem;
      font-family: 'DM Mono', monospace;
      font-size: 0.75rem; letter-spacing: 0.1em; text-transform: uppercase;
      border-radius: 4px; text-decoration: none;
      transition: all 0.25s;
      cursor: none;
    }
    .btn-primary {
      background: var(--accent); color: #050810;
      font-weight: 400;
    }
    .btn-primary:hover { background: #90cdf4; transform: translateY(-2px); box-shadow: 0 8px 30px rgba(99,179,237,0.3); }
    .btn-outline {
      border: 1px solid var(--border); color: var(--muted);
    }
    .btn-outline:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

    .hero-stats {
      display: flex; gap: 3rem; justify-content: center;
      margin-top: 3.5rem; padding-top: 2.5rem;
      border-top: 1px solid var(--border);
      animation: fadeUp 0.8s 0.5s ease both;
    }
    .stat { text-align: center; }
    .stat-num {
      font-family: 'Syne', sans-serif; font-size: 2rem; font-weight: 800;
      color: var(--accent);
    }
    .stat-label { font-size: 0.65rem; color: var(--muted); letter-spacing: 0.12em; text-transform: uppercase; margin-top: 0.2rem; }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Container */
    .container { max-width: 1100px; margin: 0 auto; padding: 0 2rem; }

    /* Section titles */
    .section-header { margin-bottom: 3.5rem; }
    .section-tag {
      font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
      color: var(--accent); margin-bottom: 0.6rem;
    }
    .section-title {
      font-family: 'Syne', sans-serif;
      font-size: clamp(2rem, 4vw, 3rem);
      font-weight: 800; line-height: 1.1;
      letter-spacing: -0.02em;
    }
    .section-line {
      width: 3rem; height: 2px;
      background: linear-gradient(to right, var(--accent), transparent);
      margin-top: 1rem;
    }

    /* About */
    #about { padding: 8rem 0; }
    .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 5rem; align-items: center; }
    .about-text p { font-size: 0.88rem; line-height: 2; color: var(--muted); margin-bottom: 1.2rem; }
    .about-text p span { color: var(--text); }
    .about-cards { display: flex; flex-direction: column; gap: 1rem; }
    .about-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px; padding: 1.2rem 1.5rem;
      display: flex; align-items: center; gap: 1rem;
      transition: border-color 0.2s, transform 0.2s;
    }
    .about-card:hover { border-color: var(--accent); transform: translateX(4px); }
    .about-card-icon { font-size: 1.4rem; }
    .about-card-text { font-size: 0.78rem; color: var(--muted); line-height: 1.5; }
    .about-card-text strong { color: var(--text); display: block; margin-bottom: 0.1rem; }

    /* Skills */
    #skills { padding: 6rem 0; background: linear-gradient(180deg, transparent, var(--bg2) 50%, transparent); }
    .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 1.5rem; }
    .skill-group {
      background: var(--surface); border: 1px solid var(--border);
      border-radius: 10px; padding: 1.8rem;
      transition: border-color 0.25s, transform 0.25s;
    }
    .skill-group:hover { border-color: var(--accent2); transform: translateY(-4px); }
    .skill-group-title {
      font-family: 'Syne', sans-serif; font-size: 0.8rem;
      letter-spacing: 0.1em; text-transform: uppercase;
      color: var(--accent2); margin-bottom: 1.2rem;
    }
    .skill-tags { display: flex; flex-wrap: wrap; gap: 0.5rem; }
    .skill-tag {
      font-size: 0.68rem; padding: 0.3rem 0.7rem;
      background: rgba(167,139,250,0.08);
      border: 1px solid rgba(167,139,250,0.2);
      border-radius: 3px; color: var(--muted);
      transition: all 0.2s;
    }
    .skill-tag:hover { background: rgba(167,139,250,0.18); color: var(--text); }

    /* Projects */
    #projects { padding: 8rem 0; }
    .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 1.5rem; }
    .project-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px; padding: 2rem;
      position: relative; overflow: hidden;
      transition: border-color 0.25s, transform 0.25s;
      display: flex; flex-direction: column;
    }
    .project-card::before {
      content: '';
      position: absolute; top: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(to right, var(--accent), var(--accent2));
      opacity: 0; transition: opacity 0.25s;
    }
    .project-card:hover { border-color: rgba(99,179,237,0.3); transform: translateY(-5px); }
    .project-card:hover::before { opacity: 1; }
    .project-number {
      font-family: 'Syne', sans-serif; font-size: 0.65rem;
      color: var(--accent3); letter-spacing: 0.15em;
      margin-bottom: 1rem;
    }
    .project-title {
      font-family: 'Syne', sans-serif; font-size: 1.05rem;
      font-weight: 700; line-height: 1.3;
      margin-bottom: 0.8rem;
    }
    .project-desc {
      font-size: 0.78rem; line-height: 1.8;
      color: var(--muted); flex-grow: 1; margin-bottom: 1.5rem;
    }
    .project-tags { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-bottom: 1.5rem; }
    .project-tag {
      font-size: 0.62rem; padding: 0.2rem 0.6rem;
      background: rgba(99,179,237,0.08);
      border: 1px solid rgba(99,179,237,0.15);
      border-radius: 2px; color: var(--accent);
    }
    .project-footer {
      display: flex; align-items: center; justify-content: space-between;
      padding-top: 1rem; border-top: 1px solid var(--border);
    }
    .project-status {
      font-size: 0.65rem; letter-spacing: 0.1em;
      text-transform: uppercase;
    }
    .status-published { color: var(--accent3); }
    .status-ongoing { color: var(--accent2); }
    .status-review { color: #fbbf24; }
    .project-link {
      font-size: 0.7rem; color: var(--accent);
      text-decoration: none; letter-spacing: 0.05em;
      display: flex; align-items: center; gap: 0.3rem;
      transition: gap 0.2s;
    }
    .project-link:hover { gap: 0.6rem; }

    /* Publications */
    #publications { padding: 8rem 0; background: linear-gradient(180deg, transparent, var(--bg2) 50%, transparent); }
    .pub-list { display: flex; flex-direction: column; gap: 1.2rem; }
    .pub-card {
      background: var(--surface); border: 1px solid var(--border);
      border-radius: 10px; padding: 1.8rem 2rem;
      display: grid; grid-template-columns: auto 1fr;
      gap: 1.5rem; align-items: start;
      transition: border-color 0.25s;
    }
    .pub-card:hover { border-color: rgba(99,179,237,0.3); }
    .pub-year {
      font-family: 'Syne', sans-serif; font-size: 0.75rem;
      font-weight: 700; color: var(--accent); min-width: 45px;
      padding-top: 0.2rem;
    }
    .pub-title {
      font-size: 0.9rem; line-height: 1.6; font-weight: 400;
      margin-bottom: 0.5rem;
    }
    .pub-venue {
      font-size: 0.72rem; color: var(--accent2);
      font-style: italic; margin-bottom: 0.6rem;
    }
    .pub-badge {
      display: inline-block; font-size: 0.62rem;
      padding: 0.2rem 0.7rem; border-radius: 2rem;
      letter-spacing: 0.08em; text-transform: uppercase;
    }
    .badge-published { background: rgba(52,211,153,0.1); color: var(--accent3); border: 1px solid rgba(52,211,153,0.2); }
    .badge-review { background: rgba(251,191,36,0.1); color: #fbbf24; border: 1px solid rgba(251,191,36,0.2); }
    .pub-doi { font-size: 0.65rem; color: var(--muted); margin-top: 0.5rem; }
    .pub-doi a { color: var(--accent); text-decoration: none; }
    .pub-doi a:hover { text-decoration: underline; }

    /* Experience */
    #experience { padding: 8rem 0; }
    .timeline { position: relative; }
    .timeline::before {
      content: '';
      position: absolute; left: 8px; top: 0; bottom: 0;
      width: 1px; background: var(--border);
    }
    .timeline-item { padding-left: 3rem; position: relative; margin-bottom: 3rem; }
    .timeline-dot {
      position: absolute; left: 0; top: 6px;
      width: 17px; height: 17px; border-radius: 50%;
      border: 2px solid var(--accent);
      background: var(--bg);
      transition: background 0.2s;
    }
    .timeline-item:hover .timeline-dot { background: var(--accent); }
    .timeline-date {
      font-size: 0.65rem; color: var(--accent3); letter-spacing: 0.12em;
      text-transform: uppercase; margin-bottom: 0.4rem;
    }
    .timeline-title {
      font-family: 'Syne', sans-serif; font-size: 1.1rem;
      font-weight: 700; margin-bottom: 0.2rem;
    }
    .timeline-org { font-size: 0.78rem; color: var(--accent2); margin-bottom: 0.8rem; }
    .timeline-desc { font-size: 0.78rem; line-height: 1.9; color: var(--muted); }
    .timeline-desc li { margin-bottom: 0.3rem; list-style: none; padding-left: 1rem; position: relative; }
    .timeline-desc li::before { content: '›'; position: absolute; left: 0; color: var(--accent); }

    /* Awards */
    #awards { padding: 6rem 0; }
    .awards-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1.5rem; }
    .award-card {
      background: var(--surface); border: 1px solid var(--border);
      border-radius: 10px; padding: 2rem;
      text-align: center;
      transition: border-color 0.25s, transform 0.25s;
    }
    .award-card:hover { border-color: rgba(251,191,36,0.4); transform: translateY(-4px); }
    .award-icon { font-size: 2.2rem; margin-bottom: 1rem; }
    .award-title {
      font-family: 'Syne', sans-serif; font-size: 0.95rem;
      font-weight: 700; margin-bottom: 0.5rem;
    }
    .award-desc { font-size: 0.75rem; color: var(--muted); line-height: 1.7; }

    /* Contact */
    #contact {
      padding: 8rem 0 6rem;
      text-align: center;
      background: linear-gradient(180deg, transparent, var(--bg2));
    }
    .contact-inner { max-width: 600px; margin: 0 auto; }
    .contact-inner .section-title { margin-bottom: 1rem; }
    .contact-inner p { font-size: 0.83rem; color: var(--muted); line-height: 1.9; margin-bottom: 2.5rem; }
    .contact-links { display: flex; flex-wrap: wrap; gap: 1rem; justify-content: center; }
    .contact-link {
      display: flex; align-items: center; gap: 0.6rem;
      padding: 0.8rem 1.5rem;
      background: var(--surface); border: 1px solid var(--border);
      border-radius: 6px; text-decoration: none;
      font-size: 0.75rem; color: var(--muted);
      transition: all 0.25s; cursor: none;
    }
    .contact-link:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

    /* Footer */
    footer {
      text-align: center; padding: 2rem;
      border-top: 1px solid var(--border);
      font-size: 0.65rem; color: var(--muted);
      letter-spacing: 0.1em; text-transform: uppercase;
      position: relative; z-index: 2;
    }

    /* Scroll reveal */
    .reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
    .reveal.visible { opacity: 1; transform: translateY(0); }

    /* Scrollbar */
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 2px; }

    @media (max-width: 768px) {
      nav { padding: 1rem 1.5rem; }
      .nav-links { display: none; }
      #hero { padding: 6rem 1.5rem 3rem; }
      .hero-stats { gap: 1.5rem; }
      .about-grid { grid-template-columns: 1fr; gap: 2.5rem; }
      .container { padding: 0 1.5rem; }
      #about, #projects, #publications, #experience, #awards, #contact { padding: 5rem 0; }
    }
  </style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<!-- Stars -->
<div id="stars"></div>

<!-- Nav -->
<nav>
  <div class="nav-logo">LH.</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#publications">Publications</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- Hero -->
<section id="hero">
  <div class="hero-glow"></div>
  <div class="hero-glow2"></div>
  <div class="hero-content">
    <div class="hero-tag">📍 Jashore, Bangladesh · Open to Research &amp; Opportunities</div>
    <h1 class="hero-name">Limon<br/>Halder</h1>
    <p class="hero-title">AI Researcher &amp; Engineer — Medical Imaging · LLMs · Agentic AI</p>
    <p class="hero-desc">
      Building intelligent systems at the intersection of deep learning, medical imaging, and large language models.
      Currently exploring agentic federated learning and vision-language models.
    </p>
    <div class="hero-cta">
      <a href="#projects" class="btn btn-primary">View Projects</a>
      <a href="mailto:limonhalder79@gmail.com" class="btn btn-outline">Get in Touch</a>
    </div>
    <div class="hero-stats">
      <div class="stat">
        <div class="stat-num">3</div>
        <div class="stat-label">Publications</div>
      </div>
      <div class="stat">
        <div class="stat-num">40+</div>
        <div class="stat-label">Kaggle Notebooks</div>
      </div>
      <div class="stat">
        <div class="stat-num">500+</div>
        <div class="stat-label">Upvotes</div>
      </div>
      <div class="stat">
        <div class="stat-num">2</div>
        <div class="stat-label">IEEE Papers</div>
      </div>
    </div>
  </div>
</section>

<!-- About -->
<section id="about">
  <div class="container">
    <div class="about-grid">
      <div class="reveal">
        <div class="section-header">
          <p class="section-tag">// 01 — About</p>
          <h2 class="section-title">Researcher.<br/>Builder.<br/>Explorer.</h2>
          <div class="section-line"></div>
        </div>
        <div class="about-text">
          <p>I'm an <span>AI/ML researcher and engineer</span> from Bangladesh, with a B.Sc. in Electrical and Electronic Engineering from <span>KUET</span>.</p>
          <p>My research spans <span>medical image segmentation</span>, EEG-based neurological disease detection using GNNs and 3D-CNNs, and <span>LLM-powered agentic systems</span> with RAG pipelines.</p>
          <p>Currently working as a <span>Trainee AI Engineer at PetaBytz Technologies</span>, building production-grade agentic AI and federated learning systems.</p>
        </div>
      </div>
      <div class="about-cards reveal">
        <div class="about-card">
          <span class="about-card-icon">🎓</span>
          <div class="about-card-text">
            <strong>B.Sc. EEE — KUET</strong>
            Jan 2020 – Sep 2025 · CGPA 3.27/4.00
          </div>
        </div>
        <div class="about-card">
          <span class="about-card-icon">🏢</span>
          <div class="about-card-text">
            <strong>Trainee AI Engineer — PetaBytz Technologies</strong>
            2025 – Present · Agentic AI &amp; RAG Systems
          </div>
        </div>
        <div class="about-card">
          <span class="about-card-icon">🧬</span>
          <div class="about-card-text">
            <strong>Research Focus</strong>
            Medical Imaging · EEG · LLMs · Federated Learning
          </div>
        </div>
        <div class="about-card">
          <span class="about-card-icon">🏆</span>
          <div class="about-card-text">
            <strong>Kaggle Notebooks Expert</strong>
            40+ notebooks · 500+ community upvotes
          </div>
        </div>
        <div class="about-card">
          <span class="about-card-icon">🌍</span>
          <div class="about-card-text">
            <strong>Research Interests</strong>
            World Models · VLMs · Model Alignment · Agentic AI
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Skills -->
<section id="skills">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-tag">// 02 — Tech Stack</p>
      <h2 class="section-title">Tools &amp; Frameworks</h2>
      <div class="section-line"></div>
    </div>
    <div class="skills-grid">
      <div class="skill-group reveal">
        <div class="skill-group-title">Languages</div>
        <div class="skill-tags">
          <span class="skill-tag">Python</span>
          <span class="skill-tag">C</span>
          <span class="skill-tag">C++</span>
          <span class="skill-tag">MATLAB</span>
          <span class="skill-tag">LaTeX</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">ML / DL Frameworks</div>
        <div class="skill-tags">
          <span class="skill-tag">PyTorch</span>
          <span class="skill-tag">TensorFlow</span>
          <span class="skill-tag">Keras</span>
          <span class="skill-tag">LangChain</span>
          <span class="skill-tag">LangGraph</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">Systems &amp; Infra</div>
        <div class="skill-tags">
          <span class="skill-tag">FastAPI</span>
          <span class="skill-tag">Docker</span>
          <span class="skill-tag">GitHub Actions</span>
          <span class="skill-tag">Apache Airflow</span>
        </div>
      </div>
      <div class="skill-group reveal">
        <div class="skill-group-title">Databases</div>
        <div class="skill-tags">
          <span class="skill-tag">MongoDB</span>
          <span class="skill-tag">PostgreSQL</span>
          <span class="skill-tag">FAISS</span>
          <span class="skill-tag">ChromaDB</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Projects -->
<section id="projects">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-tag">// 03 — Projects</p>
      <h2 class="section-title">Featured Work</h2>
      <div class="section-line"></div>
    </div>
    <div class="projects-grid">

      <div class="project-card reveal">
        <div class="project-number">PROJECT 01 — IEEE PUBLISHED</div>
        <h3 class="project-title">EEG-Based Neurological Disease Detection</h3>
        <p class="project-desc">Developed two EEG representations — functional brain connectivity graphs and 3D connectivity matrices — to classify Alzheimer's Disease and Frontotemporal Dementia. Benchmarked GNNs vs 3D-CNNs; the 3D-CNN approach achieved superior performance.</p>
        <div class="project-tags">
          <span class="project-tag">PyTorch</span>
          <span class="project-tag">GNN</span>
          <span class="project-tag">3D-CNN</span>
          <span class="project-tag">EEG</span>
          <span class="project-tag">MNE</span>
        </div>
        <div class="project-footer">
          <span class="project-status status-published">● Published · IEEE ECCE 2025</span>
          <a href="https://doi.org/10.1109/ECCE64574.2025.11013802" class="project-link" target="_blank">DOI →</a>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-number">PROJECT 02 — IEEE PUBLISHED</div>
        <h3 class="project-title">Fetal Head Segmentation &amp; HC Measurement</h3>
        <p class="project-desc">Built a Residual U-Net architecture to segment fetal heads in ultrasound images and automatically measure head circumference — enabling precise, automated prenatal clinical measurements.</p>
        <div class="project-tags">
          <span class="project-tag">TensorFlow</span>
          <span class="project-tag">Residual U-Net</span>
          <span class="project-tag">Ultrasound</span>
          <span class="project-tag">OpenCV</span>
          <span class="project-tag">Keras</span>
        </div>
        <div class="project-footer">
          <span class="project-status status-published">● Published · IEEE ICICT 2024</span>
          <a href="https://doi.org/10.1109/ICICT64387.2024.10839692" class="project-link" target="_blank">DOI →</a>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-number">PROJECT 03 — UNDER REVIEW</div>
        <h3 class="project-title">Anatomy-Agnostic Medical Segmentation</h3>
        <p class="project-desc">Designed a prompt-conditioned channel attention mechanism for hierarchical feature modulation, enabling anatomy-agnostic segmentation that generalizes across diverse medical imaging domains without organ-specific tuning.</p>
        <div class="project-tags">
          <span class="project-tag">PyTorch</span>
          <span class="project-tag">Transformers</span>
          <span class="project-tag">Attention</span>
          <span class="project-tag">Segmentation</span>
        </div>
        <div class="project-footer">
          <span class="project-status status-review">● Under Review · IEEE JTEHM</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-number">PROJECT 04 — PRODUCTION</div>
        <h3 class="project-title">Agentic RAG System</h3>
        <p class="project-desc">Designed and deployed production-grade multi-agent AI workflows with tool-calling, autonomous reasoning chains, and RAG pipelines. Fine-tuned Gemma 3 models to cut API dependence. Integrated with ServiceNow for enterprise workflows.</p>
        <div class="project-tags">
          <span class="project-tag">LangGraph</span>
          <span class="project-tag">FastAPI</span>
          <span class="project-tag">FAISS</span>
          <span class="project-tag">ChromaDB</span>
          <span class="project-tag">Gemma 3</span>
        </div>
        <div class="project-footer">
          <span class="project-status status-published">● Production · PetaBytz Technologies</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-number">PROJECT 05 — ONGOING RESEARCH</div>
        <h3 class="project-title">Agentic Federated Learning</h3>
        <p class="project-desc">Developing Agentic AI-driven Federated Learning strategies to mitigate client drift and performance degradation from heterogeneous (non-IID) data distributions across decentralized federated clients.</p>
        <div class="project-tags">
          <span class="project-tag">PyTorch</span>
          <span class="project-tag">Federated Learning</span>
          <span class="project-tag">LangGraph</span>
          <span class="project-tag">Airflow</span>
        </div>
        <div class="project-footer">
          <span class="project-status status-ongoing">● In Progress · 2025–Present</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-number">PROJECT 06 — COMPETITION</div>
        <h3 class="project-title">Heart Sound Classification</h3>
        <p class="project-desc">National-level Biomed Datathon (BUET BME 2024). Designed a BiLSTM-based model for 4-class heart sound classification. Ranked among top teams in the Kaggle online evaluation and invited to present in Dhaka.</p>
        <div class="project-tags">
          <span class="project-tag">PyTorch</span>
          <span class="project-tag">BiLSTM</span>
          <span class="project-tag">Audio DSP</span>
          <span class="project-tag">Kaggle</span>
        </div>
        <div class="project-footer">
          <span class="project-status status-published">● Finalist · BUET BME 2024</span>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- Publications -->
<section id="publications">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-tag">// 04 — Publications</p>
      <h2 class="section-title">Research Output</h2>
      <div class="section-line"></div>
    </div>
    <div class="pub-list">

      <div class="pub-card reveal">
        <div class="pub-year">2025</div>
        <div>
          <p class="pub-title">EEG Connectivity and Power Spectral Density-Based Classification of Alzheimer's Disease and Frontotemporal Dementia Using 3D Convolutional Neural Networks</p>
          <p class="pub-venue">IEEE Energy Conversion Congress &amp; Exposition (ECCE)</p>
          <span class="pub-badge badge-published">Published</span>
          <p class="pub-doi">DOI: <a href="https://doi.org/10.1109/ECCE64574.2025.11013802" target="_blank">10.1109/ECCE64574.2025.11013802</a></p>
        </div>
      </div>

      <div class="pub-card reveal">
        <div class="pub-year">2024</div>
        <div>
          <p class="pub-title">Fetal Head Segmentation and Head Circumference Measurement Using Residual U-Net</p>
          <p class="pub-venue">IEEE International Conference on Information and Communication Technology (ICICT)</p>
          <span class="pub-badge badge-published">Published</span>
          <p class="pub-doi">DOI: <a href="https://doi.org/10.1109/ICICT64387.2024.10839692" target="_blank">10.1109/ICICT64387.2024.10839692</a></p>
        </div>
      </div>

      <div class="pub-card reveal">
        <div class="pub-year">2026</div>
        <div>
          <p class="pub-title">Prompt-Conditioned Channel Attention for Hierarchical Feature Modulation toward Anatomy-Agnostic Segmentation</p>
          <p class="pub-venue">IEEE Journal of Translational Engineering in Health and Medicine (JTEHM)</p>
          <span class="pub-badge badge-review">Under Review</span>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- Experience -->
<section id="experience">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-tag">// 05 — Experience</p>
      <h2 class="section-title">Journey</h2>
      <div class="section-line"></div>
    </div>
    <div class="timeline">
      <div class="timeline-item reveal">
        <div class="timeline-dot"></div>
        <div class="timeline-date">2025 – Present</div>
        <div class="timeline-title">Trainee AI Engineer</div>
        <div class="timeline-org">PetaBytz Technologies Inc</div>
        <ul class="timeline-desc">
          <li>Built Agentic AI &amp; RAG systems using LangGraph and OpenAI APIs</li>
          <li>Designed multi-agent workflows with tool integration and autonomous reasoning</li>
          <li>Fine-tuned Gemma 3 models to improve efficiency and reduce API dependence</li>
          <li>Deployed scalable solutions using FastAPI, FAISS, ChromaDB, and ServiceNow</li>
        </ul>
      </div>
      <div class="timeline-item reveal">
        <div class="timeline-dot"></div>
        <div class="timeline-date">2024 – 2025</div>
        <div class="timeline-title">Undergraduate Thesis Research</div>
        <div class="timeline-org">KUET — EEG-Based Neurological Disease Detection</div>
        <ul class="timeline-desc">
          <li>Developed functional brain connectivity graphs and 3D connectivity representations from EEG</li>
          <li>Evaluated GNNs and 3D-CNNs for Alzheimer's and FTD classification</li>
          <li>Demonstrated 3D connectivity representations achieved superior classification performance</li>
        </ul>
      </div>
      <div class="timeline-item reveal">
        <div class="timeline-dot"></div>
        <div class="timeline-date">2025 – Present</div>
        <div class="timeline-title">Ongoing Research</div>
        <div class="timeline-org">Agentic Federated Learning</div>
        <ul class="timeline-desc">
          <li>Developing Agentic AI-driven FL to address client drift in non-IID data distributions</li>
        </ul>
      </div>
      <div class="timeline-item reveal">
        <div class="timeline-dot"></div>
        <div class="timeline-date">2020 – 2025</div>
        <div class="timeline-title">B.Sc. Electrical &amp; Electronic Engineering</div>
        <div class="timeline-org">Khulna University of Engineering &amp; Technology (KUET)</div>
        <ul class="timeline-desc">
          <li>CGPA: 3.27 / 4.00 · Merit Scholarship throughout undergraduate</li>
          <li>Senior Executive at NeuralNet AI Club — organized workshops &amp; mentored juniors</li>
          <li>Organizing Secretary at EEE Makers HUB — coordinated nationwide robotics competition</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- Awards -->
<section id="awards">
  <div class="container">
    <div class="section-header reveal">
      <p class="section-tag">// 06 — Recognition</p>
      <h2 class="section-title">Honors &amp; Awards</h2>
      <div class="section-line"></div>
    </div>
    <div class="awards-grid">
      <div class="award-card reveal">
        <div class="award-icon">🥇</div>
        <div class="award-title">Biomed Datathon Finalist</div>
        <div class="award-desc">BUET BME 2024 · National-level 4-class heart sound classification. Ranked among top teams online and invited to present in Dhaka.</div>
      </div>
      <div class="award-card reveal">
        <div class="award-icon">📓</div>
        <div class="award-title">Kaggle Notebooks Expert</div>
        <div class="award-desc">Published 40+ public notebooks on ML &amp; DL applications. Received 500+ community upvotes across the Kaggle platform.</div>
      </div>
      <div class="award-card reveal">
        <div class="award-icon">🎓</div>
        <div class="award-title">KUET Merit Scholarship</div>
        <div class="award-desc">Awarded academic merit scholarship throughout the undergraduate program for outstanding academic performance.</div>
      </div>
    </div>
  </div>
</section>

<!-- Contact -->
<section id="contact">
  <div class="container">
    <div class="contact-inner reveal">
      <div class="section-header">
        <p class="section-tag">// 07 — Contact</p>
        <h2 class="section-title">Let's Connect</h2>
        <div class="section-line" style="margin: 1rem auto 0;"></div>
      </div>
      <p>I'm always open to discussing research collaborations, AI opportunities, or just exchanging ideas. Feel free to reach out!</p>
      <div class="contact-links">
        <a href="mailto:limonhalder79@gmail.com" class="contact-link">
          <span>✉</span> limonhalder79@gmail.com
        </a>
        <a href="https://github.com/" class="contact-link" target="_blank">
          <span>⌥</span> GitHub
        </a>
        <a href="https://linkedin.com/" class="contact-link" target="_blank">
          <span>↗</span> LinkedIn
        </a>
        <a href="https://kaggle.com/" class="contact-link" target="_blank">
          <span>◈</span> Kaggle
        </a>
      </div>
    </div>
  </div>
</section>

<footer>
  <p>© 2025 Limon Halder · Built with care · limonhalder.github.io</p>
</footer>

<script>
  // Stars
  const starsEl = document.getElementById('stars');
  for (let i = 0; i < 120; i++) {
    const s = document.createElement('div');
    s.className = 'star';
    const size = Math.random() * 2 + 0.5;
    s.style.cssText = `
      width:${size}px; height:${size}px;
      left:${Math.random()*100}%; top:${Math.random()*100}%;
      --d:${3+Math.random()*5}s; --delay:${Math.random()*6}s;
      --op:${0.3+Math.random()*0.6};
    `;
    starsEl.appendChild(s);
  }

  // Cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursor-ring');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();
  document.querySelectorAll('a, button').forEach(el => {
    el.addEventListener('mouseenter', () => { cursor.style.width = '18px'; cursor.style.height = '18px'; ring.style.width = '50px'; ring.style.height = '50px'; });
    el.addEventListener('mouseleave', () => { cursor.style.width = '10px'; cursor.style.height = '10px'; ring.style.width = '36px'; ring.style.height = '36px'; });
  });

  // Scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
  }, { threshold: 0.12 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>
</body>
</html>
