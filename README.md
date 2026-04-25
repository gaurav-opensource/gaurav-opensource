
<!DOCTYPE html>
<html>
<head>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: 'DM Sans', sans-serif;
    background: #0a0a0f;
    color: #e8e6f0;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .noise {
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.035'/%3E%3C/svg%3E");
    opacity: 0.4;
  }

  .grid-bg {
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background-image:
      linear-gradient(rgba(99,74,241,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(99,74,241,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
  }

  .glow {
    position: fixed; top: -200px; left: 50%; transform: translateX(-50%);
    width: 800px; height: 500px;
    background: radial-gradient(ellipse, rgba(99,74,241,0.12) 0%, transparent 70%);
    pointer-events: none; z-index: 0;
  }

  .container {
    position: relative; z-index: 1;
    max-width: 860px; margin: 0 auto;
    padding: 60px 40px 80px;
  }

  /* HEADER */
  .header {
    display: flex; align-items: flex-start; justify-content: space-between;
    margin-bottom: 56px;
    border-bottom: 1px solid rgba(99,74,241,0.2);
    padding-bottom: 40px;
  }

  .header-left { flex: 1; }

  .badge-row {
    display: flex; align-items: center; gap: 10px;
    margin-bottom: 16px;
  }

  .badge {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 0.15em; text-transform: uppercase;
    padding: 4px 10px;
    border-radius: 2px;
    font-weight: 400;
  }
  .badge-open { background: rgba(34,197,94,0.12); color: #4ade80; border: 1px solid rgba(74,222,128,0.25); }
  .badge-hire { background: rgba(99,74,241,0.12); color: #a78bfa; border: 1px solid rgba(167,139,250,0.25); }

  h1 {
    font-family: 'DM Sans', sans-serif;
    font-size: 42px; font-weight: 600; line-height: 1.1;
    color: #ffffff; letter-spacing: -0.02em;
    margin-bottom: 10px;
  }

  h1 span { color: #7c5ff5; }

  .tagline {
    font-size: 15px; color: #7a7890; font-weight: 400; letter-spacing: 0.01em;
    font-family: 'Space Mono', monospace;
  }

  .header-right {
    display: flex; flex-direction: column; align-items: flex-end; gap: 12px;
    padding-top: 8px;
  }

  .stat-pill {
    display: flex; align-items: center; gap: 8px;
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 6px; padding: 8px 16px;
    font-family: 'Space Mono', monospace;
  }
  .stat-num { font-size: 20px; font-weight: 700; color: #fff; }
  .stat-lbl { font-size: 10px; color: #5a5870; text-transform: uppercase; letter-spacing: 0.1em; }
  .stat-sep { width: 1px; height: 20px; background: rgba(255,255,255,0.08); }

  /* SECTIONS */
  .section { margin-bottom: 52px; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 0.18em; text-transform: uppercase;
    color: #7c5ff5; margin-bottom: 20px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::after {
    content: ''; flex: 1; height: 1px;
    background: linear-gradient(90deg, rgba(124,95,245,0.3), transparent);
  }

  /* ABOUT GRID */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .about-item {
    display: flex; align-items: flex-start; gap: 12px;
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.05);
    border-radius: 8px; padding: 14px 16px;
    transition: border-color 0.2s;
  }
  .about-item:hover { border-color: rgba(124,95,245,0.25); }

  .about-icon {
    width: 28px; height: 28px; border-radius: 6px;
    background: rgba(124,95,245,0.1);
    display: flex; align-items: center; justify-content: center;
    font-size: 13px; flex-shrink: 0;
  }

  .about-text { font-size: 13.5px; color: #b0adc8; line-height: 1.5; }
  .about-text strong { color: #e8e6f0; font-weight: 500; }

  /* TECH STACK */
  .stack-groups { display: flex; flex-direction: column; gap: 14px; }

  .stack-row {
    display: flex; align-items: center; gap: 12px;
  }

  .stack-cat {
    font-family: 'Space Mono', monospace;
    font-size: 10px; color: #5a5870; text-transform: uppercase;
    letter-spacing: 0.1em; min-width: 80px;
  }

  .stack-chips { display: flex; flex-wrap: wrap; gap: 6px; }

  .chip {
    font-family: 'Space Mono', monospace;
    font-size: 11px; padding: 4px 10px;
    border-radius: 4px; border: 1px solid;
    font-weight: 400; letter-spacing: 0.02em;
    white-space: nowrap;
  }

  .chip-purple { background: rgba(124,95,245,0.08); color: #a78bfa; border-color: rgba(167,139,250,0.2); }
  .chip-teal   { background: rgba(20,184,166,0.08); color: #2dd4bf; border-color: rgba(45,212,191,0.2); }
  .chip-amber  { background: rgba(245,158,11,0.08); color: #fbbf24; border-color: rgba(251,191,36,0.2); }
  .chip-green  { background: rgba(34,197,94,0.08);  color: #4ade80; border-color: rgba(74,222,128,0.2); }
  .chip-blue   { background: rgba(59,130,246,0.08); color: #60a5fa; border-color: rgba(96,165,250,0.2); }
  .chip-coral  { background: rgba(249,115,22,0.08); color: #fb923c; border-color: rgba(251,146,60,0.2); }

  /* PROJECTS */
  .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

  .project-card {
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 10px; padding: 20px 22px;
    transition: border-color 0.2s, background 0.2s;
    cursor: default;
  }
  .project-card:hover {
    border-color: rgba(124,95,245,0.3);
    background: rgba(124,95,245,0.04);
  }

  .proj-header { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 10px; }

  .proj-emoji {
    width: 34px; height: 34px; border-radius: 8px;
    background: rgba(124,95,245,0.1);
    display: flex; align-items: center; justify-content: center;
    font-size: 15px;
  }

  .proj-tag {
    font-family: 'Space Mono', monospace; font-size: 9px;
    text-transform: uppercase; letter-spacing: 0.12em;
    padding: 3px 8px; border-radius: 3px;
    background: rgba(124,95,245,0.1); color: #a78bfa;
    border: 1px solid rgba(167,139,250,0.2);
  }

  .proj-name {
    font-size: 14px; font-weight: 600; color: #fff;
    margin-bottom: 6px; line-height: 1.3;
  }

  .proj-desc {
    font-size: 12.5px; color: #6e6c86; line-height: 1.6; margin-bottom: 14px;
  }

  .proj-chips { display: flex; flex-wrap: wrap; gap: 5px; }

  .proj-chip {
    font-family: 'Space Mono', monospace; font-size: 10px;
    padding: 2px 8px; border-radius: 3px;
    background: rgba(255,255,255,0.04); color: #6e6c86;
    border: 1px solid rgba(255,255,255,0.06);
  }

  /* ACHIEVEMENTS */
  .ach-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }

  .ach-card {
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.05);
    border-radius: 8px; padding: 16px;
    text-align: center;
  }

  .ach-icon { font-size: 20px; margin-bottom: 8px; }
  .ach-title { font-size: 12px; font-weight: 500; color: #e8e6f0; margin-bottom: 4px; }
  .ach-sub { font-size: 11px; color: #5a5870; font-family: 'Space Mono', monospace; }

  /* CURRENTLY */
  .current-list { display: flex; flex-direction: column; gap: 10px; }

  .current-item {
    display: flex; align-items: center; gap: 14px;
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.05);
    border-radius: 8px; padding: 14px 18px;
  }

  .pulse {
    width: 8px; height: 8px; border-radius: 50%;
    background: #4ade80; flex-shrink: 0;
    box-shadow: 0 0 0 0 rgba(74,222,128,0.4);
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0% { box-shadow: 0 0 0 0 rgba(74,222,128,0.4); }
    70% { box-shadow: 0 0 0 6px rgba(74,222,128,0); }
    100% { box-shadow: 0 0 0 0 rgba(74,222,128,0); }
  }

  .current-text { font-size: 13.5px; color: #b0adc8; }
  .current-text strong { color: #e8e6f0; font-weight: 500; }

  /* CONNECT */
  .connect-bar {
    display: flex; align-items: center; justify-content: space-between;
    background: linear-gradient(135deg, rgba(124,95,245,0.08), rgba(99,74,241,0.04));
    border: 1px solid rgba(124,95,245,0.2);
    border-radius: 10px; padding: 20px 24px;
  }

  .connect-left h3 {
    font-size: 16px; font-weight: 500; color: #fff; margin-bottom: 4px;
  }
  .connect-left p {
    font-size: 12.5px; color: #6e6c86;
    font-family: 'Space Mono', monospace;
  }

  .connect-links { display: flex; gap: 10px; }

  .connect-btn {
    font-family: 'Space Mono', monospace; font-size: 11px;
    letter-spacing: 0.06em; padding: 9px 18px;
    border-radius: 6px; border: 1px solid;
    cursor: pointer; text-decoration: none;
    transition: all 0.2s; display: inline-block;
  }
  .btn-primary {
    background: #7c5ff5; color: #fff; border-color: #7c5ff5;
  }
  .btn-primary:hover { background: #6b4ee4; }
  .btn-ghost {
    background: transparent; color: #a78bfa; border-color: rgba(167,139,250,0.3);
  }
  .btn-ghost:hover { background: rgba(124,95,245,0.1); }

  /* GITHUB STATS PLACEHOLDER */
  .stats-row {
    display: grid; grid-template-columns: repeat(4,1fr); gap: 10px;
  }
  .stat-card {
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.05);
    border-radius: 8px; padding: 18px 16px; text-align: center;
  }
  .stat-card .num {
    font-family: 'Space Mono', monospace;
    font-size: 26px; font-weight: 700; color: #7c5ff5;
    margin-bottom: 4px;
  }
  .stat-card .lbl {
    font-size: 11px; color: #5a5870;
    font-family: 'Space Mono', monospace;
    text-transform: uppercase; letter-spacing: 0.1em;
  }

  .divider { height: 1px; background: rgba(255,255,255,0.05); margin: 48px 0; }
</style>
</head>
<body>
<div class="noise"></div>
<div class="grid-bg"></div>
<div class="glow"></div>

<div class="container">

  <!-- HEADER -->
  <div class="header">
    <div class="header-left">
      <div class="badge-row">
        <span class="badge badge-open">&#9679; Open to Work</span>
        <span class="badge badge-hire">Available for Hire</span>
      </div>
      <h1>Full Stack <span>Developer</span></h1>
      <p class="tagline">MERN &middot; WebRTC &middot; AI/ML &middot; Real-time Systems</p>
    </div>
    <div class="header-right">
      <div class="stat-pill">
        <div>
          <div class="stat-num">800+</div>
          <div class="stat-lbl">DSA Solved</div>
        </div>
        <div class="stat-sep"></div>
        <div>
          <div class="stat-num">25+</div>
          <div class="stat-lbl">Projects</div>
        </div>
      </div>
    </div>
  </div>

  <!-- ABOUT -->
  <div class="section">
    <div class="section-label">About Me</div>
    <div class="about-grid">
      <div class="about-item">
        <div class="about-icon">&#128187;</div>
        <div class="about-text"><strong>Full Stack Developer</strong> specializing in MERN stack &amp; real-time systems</div>
      </div>
      <div class="about-item">
        <div class="about-icon">&#128225;</div>
        <div class="about-text"><strong>WebRTC expert</strong> &mdash; built peer-to-peer video platforms from scratch</div>
      </div>
      <div class="about-item">
        <div class="about-icon">&#129504;</div>
        <div class="about-text"><strong>AI/ML integrations</strong> in real-world production applications</div>
      </div>
      <div class="about-item">
        <div class="about-icon">&#127757;</div>
        <div class="about-text"><strong>System design</strong> &amp; backend scalability enthusiast, always improving</div>
      </div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section">
    <div class="section-label">Tech Stack</div>
    <div class="stack-groups">
      <div class="stack-row">
        <span class="stack-cat">Frontend</span>
        <div class="stack-chips">
          <span class="chip chip-purple">React.js</span>
          <span class="chip chip-purple">JavaScript</span>
          <span class="chip chip-purple">HTML</span>
          <span class="chip chip-purple">CSS</span>
          <span class="chip chip-purple">Tailwind</span>
        </div>
      </div>
      <div class="stack-row">
        <span class="stack-cat">Backend</span>
        <div class="stack-chips">
          <span class="chip chip-teal">Node.js</span>
          <span class="chip chip-teal">Express.js</span>
          <span class="chip chip-teal">Flask</span>
        </div>
      </div>
      <div class="stack-row">
        <span class="stack-cat">Database</span>
        <div class="stack-chips">
          <span class="chip chip-green">MongoDB</span>
          <span class="chip chip-green">MySQL</span>
          <span class="chip chip-green">PostgreSQL</span>
        </div>
      </div>
      <div class="stack-row">
        <span class="stack-cat">Real-time</span>
        <div class="stack-chips">
          <span class="chip chip-amber">WebRTC</span>
          <span class="chip chip-amber">Socket.IO</span>
        </div>
      </div>
      <div class="stack-row">
        <span class="stack-cat">AI / ML</span>
        <div class="stack-chips">
          <span class="chip chip-coral">Python</span>
          <span class="chip chip-coral">NumPy</span>
          <span class="chip chip-coral">Pandas</span>
          <span class="chip chip-coral">Scikit-learn</span>
          <span class="chip chip-coral">TensorFlow</span>
        </div>
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <!-- PROJECTS -->
  <div class="section">
    <div class="section-label">Featured Projects</div>
    <div class="projects-grid">

      <div class="project-card">
        <div class="proj-header">
          <div class="proj-emoji">&#127973;</div>
          <span class="proj-tag">Healthcare</span>
        </div>
        <div class="proj-name">AI Smart Healthcare Platform</div>
        <div class="proj-desc">Doctor discovery, booking &amp; peer-to-peer video consultation. Real-time chat, scalable backend.</div>
        <div class="proj-chips">
          <span class="proj-chip">WebRTC</span>
          <span class="proj-chip">Socket.IO</span>
          <span class="proj-chip">Node.js</span>
          <span class="proj-chip">MongoDB</span>
        </div>
      </div>

      <div class="project-card">
        <div class="proj-header">
          <div class="proj-emoji">&#128188;</div>
          <span class="proj-tag">AI / ML</span>
        </div>
        <div class="proj-name">Smart Hiring Platform</div>
        <div class="proj-desc">AI-based recruitment with live coding tests via Judge0 API and ML candidate scoring.</div>
        <div class="proj-chips">
          <span class="proj-chip">Judge0</span>
          <span class="proj-chip">ML</span>
          <span class="proj-chip">React</span>
          <span class="proj-chip">Node.js</span>
        </div>
      </div>

      <div class="project-card">
        <div class="proj-header">
          <div class="proj-emoji">&#127909;</div>
          <span class="proj-tag">Real-time</span>
        </div>
        <div class="proj-name">Video Meeting Platform</div>
        <div class="proj-desc">Room-based video conferencing with low-latency signaling and scalable architecture.</div>
        <div class="proj-chips">
          <span class="proj-chip">WebRTC</span>
          <span class="proj-chip">Socket.IO</span>
          <span class="proj-chip">React</span>
        </div>
      </div>

      <div class="project-card">
        <div class="proj-header">
          <div class="proj-emoji">&#127823;</div>
          <span class="proj-tag">Collaboration</span>
        </div>
        <div class="proj-name">Real-Time Canvas Board</div>
        <div class="proj-desc">Multi-user collaborative drawing board with live sync, smooth UX, and WebSocket backbone.</div>
        <div class="proj-chips">
          <span class="proj-chip">WebSockets</span>
          <span class="proj-chip">Canvas API</span>
          <span class="proj-chip">Node.js</span>
        </div>
      </div>

    </div>
  </div>

  <!-- STATS -->
  <div class="section">
    <div class="section-label">GitHub Stats</div>
    <div class="stats-row">
      <div class="stat-card">
        <div class="num">800+</div>
        <div class="lbl">Problems Solved</div>
      </div>
      <div class="stat-card">
        <div class="num">25+</div>
        <div class="lbl">Projects Built</div>
      </div>
      <div class="stat-card">
        <div class="num">&#9733;</div>
        <div class="lbl">OSS Contributor</div>
      </div>
      <div class="stat-card">
        <div class="num">&#127942;</div>
        <div class="lbl">Hackathon SIH</div>
      </div>
    </div>
  </div>

  <!-- ACHIEVEMENTS -->
  <div class="section">
    <div class="section-label">Achievements</div>
    <div class="ach-grid">
      <div class="ach-card">
        <div class="ach-icon">&#127942;</div>
        <div class="ach-title">Smart India Hackathon</div>
        <div class="ach-sub">Participant</div>
      </div>
      <div class="ach-card">
        <div class="ach-icon">&#129352;</div>
        <div class="ach-title">ByteCode DSA Contest</div>
        <div class="ach-sub">Rank Holder</div>
      </div>
      <div class="ach-card">
        <div class="ach-icon">&#127757;</div>
        <div class="ach-title">Open Source</div>
        <div class="ach-sub">Active Contributor</div>
      </div>
    </div>
  </div>

  <!-- CURRENTLY WORKING ON -->
  <div class="section">
    <div class="section-label">Currently Building</div>
    <div class="current-list">
      <div class="current-item">
        <div class="pulse"></div>
        <div class="current-text"><strong>AI-powered healthcare assistant</strong> &mdash; LLM integration with real-time patient interaction</div>
      </div>
      <div class="current-item">
        <div class="pulse"></div>
        <div class="current-text"><strong>Real-time collaboration tools</strong> &mdash; next-gen whiteboard &amp; document co-editing</div>
      </div>
      <div class="current-item">
        <div class="pulse"></div>
        <div class="current-text"><strong>System design mastery</strong> &mdash; distributed systems &amp; scalable backend architecture</div>
      </div>
    </div>
  </div>

  <!-- CONNECT -->
  <div class="section">
    <div class="connect-bar">
      <div class="connect-left">
        <h3>Let's build something impactful</h3>
        <p>Open to jobs, collaborations &amp; interesting ideas</p>
      </div>
      <div class="connect-links">
        <a class="connect-btn btn-ghost" href="#">GitHub</a>
        <a class="connect-btn btn-ghost" href="#">LinkedIn</a>
        <a class="connect-btn btn-primary" href="#">Hire Me &#8594;</a>
      </div>
    </div>
  </div>

</div>
</body>
</html>
