<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rectus Femoris Pathway — Aspetar</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=DM+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { font-size: 14px; }
  body { background: #F7FAFC; font-family: 'DM Sans', sans-serif; color: #1A202C; }
  button { cursor: pointer; font-family: 'DM Sans', sans-serif; }
  button:focus { outline: none; }
  ::-webkit-scrollbar { width: 6px; height: 6px; }
  ::-webkit-scrollbar-track { background: #F7FAFC; }
  ::-webkit-scrollbar-thumb { background: #CBD5E0; border-radius: 3px; }

  /* ── Layout ── */
  #app { min-height: 100vh; }
  .topbar {
    background: #1A202C; height: 56px; padding: 0 24px;
    display: flex; align-items: center; justify-content: space-between;
    position: sticky; top: 0; z-index: 100;
    border-bottom: 3px solid #C0392B;
    transition: border-color 0.3s;
  }
  .topbar-left { display: flex; align-items: center; gap: 12px; }
  .topbar-icon {
    width: 30px; height: 30px; border-radius: 7px;
    display: flex; align-items: center; justify-content: center;
    font-size: 15px; transition: background 0.3s;
  }
  .topbar-title { font-family: 'DM Serif Display', serif; color: #fff; font-size: 15px; line-height: 1.1; }
  .topbar-sub { color: #718096; font-size: 10px; letter-spacing: 0.5px; margin-top: 2px; }
  .phase-badge {
    padding: 4px 12px; border-radius: 20px;
    font-size: 11px; font-weight: 700; letter-spacing: 0.3px;
    transition: all 0.3s;
  }

  .main { max-width: 1200px; margin: 0 auto; padding: 20px 20px 60px; }

  /* ── Cards ── */
  .card {
    background: white; border-radius: 14px; border: 1px solid #E2E8F0;
    box-shadow: 0 1px 4px rgba(0,0,0,0.06);
  }
  .card-pad { padding: 16px 20px; }

  /* ── Phase selector pills ── */
  .phase-pills { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 14px; }
  .phase-pill {
    padding: 6px 14px; border-radius: 20px; font-size: 12px;
    font-weight: 600; transition: all 0.2s; border: 2px solid #E2E8F0;
    background: white; color: #4A5568;
  }
  .phase-pill.active { color: white; }

  /* ── Tabs ── */
  .tab-bar {
    display: flex; gap: 4px; background: white;
    padding: 4px; border-radius: 10px; border: 1px solid #E2E8F0;
    margin: 16px 0; width: fit-content;
  }
  .tab-btn {
    padding: 8px 18px; border-radius: 7px; border: none;
    background: transparent; color: #718096;
    font-size: 12px; font-weight: 500; transition: all 0.15s;
  }
  .tab-btn.active { color: white; }

  /* ── Freq grid ── */
  .freq-grid {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 8px; margin-bottom: 16px;
  }
  .freq-card {
    background: white; border-radius: 10px; padding: 10px 12px;
    border: 1px solid #E2E8F0;
  }
  .freq-label { font-size: 10px; font-weight: 700; letter-spacing: 0.3px; margin-bottom: 4px; }
  .freq-val { font-family: 'DM Serif Display', serif; font-size: 18px; }

  /* ── Day grid ── */
  .day-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 8px;
  }
  .day-card {
    border-radius: 12px; border: 1px solid #E2E8F0; overflow: hidden;
    box-shadow: 0 1px 4px rgba(0,0,0,0.05); transition: all 0.2s;
    background: white;
  }
  .day-card.today { border-width: 2px; }
  .day-card.recovery { background: #FAFAFA; }
  .day-header {
    padding: 10px 12px;
    border-bottom: none; cursor: pointer;
  }
  .day-header.has-sessions:hover { filter: brightness(0.97); }
  .day-name { font-family: 'DM Serif Display', serif; font-size: 13px; color: #1A202C; }
  .day-today-badge {
    display: inline-block; margin-left: 6px;
    font-size: 9px; font-weight: 700; letter-spacing: 1px;
    font-family: 'DM Sans', sans-serif;
  }
  .day-focus-pill {
    display: inline-flex; align-items: center;
    padding: 2px 8px; border-radius: 4px;
    font-size: 9px; font-weight: 800; letter-spacing: 0.8px;
    margin-top: 5px;
  }
  .day-caret { color: #A0AEC0; font-size: 11px; float: right; margin-top: 2px; }
  .day-body { padding: 10px 12px; display: none; border-top: 1px solid #EDF2F7; }
  .day-body.open { display: block; }
  .session-card {
    padding: 10px 12px; border-radius: 8px;
    background: #FAFAFA; border: 1px solid #EDF2F7;
    margin-bottom: 8px;
  }
  .session-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 6px; }
  .session-name { font-family: 'DM Serif Display', serif; font-size: 12px; color: #1A202C; margin-bottom: 2px; }
  .session-detail { font-size: 11px; color: #718096; line-height: 1.4; }
  .comp-tag {
    display: inline-block; padding: 2px 8px; border-radius: 4px;
    font-size: 10px; font-weight: 700; letter-spacing: 0.3px;
  }
  .intensity-badge {
    display: inline-flex; align-items: center; gap: 4px;
    padding: 2px 8px; border-radius: 10px;
    font-size: 10px; font-weight: 600;
  }
  .intensity-dot { width: 6px; height: 6px; border-radius: 50%; display: inline-block; }
  .day-other { padding-top: 6px; border-top: 1px solid #EDF2F7; margin-top: 2px; }
  .day-other-item { font-size: 11px; color: #A0AEC0; padding: 2px 0; }

  /* ── Progress bar ── */
  .progress-strip {
    background: white; border-radius: 12px; padding: 12px 20px;
    border: 1px solid #E2E8F0; margin-bottom: 16px;
  }
  .progress-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 6px; }
  .progress-label { font-size: 11px; font-weight: 700; color: #4A5568; letter-spacing: 0.5px; }
  .progress-count { font-family: 'DM Serif Display', serif; font-size: 14px; }
  .progress-track { height: 6px; background: #EDF2F7; border-radius: 3px; overflow: hidden; }
  .progress-fill { height: 100%; border-radius: 3px; transition: width 0.5s cubic-bezier(0.16,1,0.3,1); }

  /* ── Milestones ── */
  .criteria-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .criteria-section { background: white; border-radius: 12px; padding: 16px 18px; border: 1px solid #E2E8F0; }
  .criteria-title { font-family: 'DM Serif Display', serif; font-size: 15px; color: #1A202C; margin-bottom: 3px; }
  .criteria-sub { font-size: 11px; color: #718096; margin-bottom: 12px; }
  .check-item {
    display: flex; align-items: flex-start; gap: 10px;
    padding: 8px 10px; border-radius: 8px;
    background: #FAFAFA; border: 1px solid #E2E8F0;
    margin-bottom: 4px; cursor: pointer; transition: all 0.15s;
  }
  .check-item.checked { background: #F0FFF4; border-color: #9AE6B4; }
  .check-box {
    width: 18px; height: 18px; border-radius: 4px; flex-shrink: 0;
    border: 2px solid #CBD5E0; background: white;
    display: flex; align-items: center; justify-content: center;
    margin-top: 1px; transition: all 0.15s;
  }
  .check-box.checked { background: #38A169; border-color: #38A169; }
  .check-tick { color: white; font-size: 11px; font-weight: bold; display: none; }
  .check-box.checked .check-tick { display: block; }
  .check-label {
    font-size: 12.5px; color: #4A5568; line-height: 1.4; transition: all 0.15s;
  }
  .check-label.checked { color: #276749; text-decoration: line-through; opacity: 0.7; }

  .summary-card {
    background: #EBF5FB; border-radius: 12px; padding: 16px 18px;
    border: 2px solid rgba(0,0,0,0.1);
    grid-column: 1 / -1;
    display: flex; align-items: center; justify-content: space-between;
  }
  .summary-pct { font-family: 'DM Serif Display', serif; font-size: 40px; opacity: 0.25; }
  .summary-title { font-family: 'DM Serif Display', serif; font-size: 16px; margin-bottom: 4px; }
  .summary-sub { font-size: 12px; color: #718096; }

  .timeline-card { background: white; border-radius: 12px; padding: 16px 18px; border: 1px solid #E2E8F0; grid-column: 1 / -1; }
  .timeline-title { font-family: 'DM Serif Display', serif; font-size: 15px; color: #1A202C; margin-bottom: 12px; }
  .timeline-track { display: flex; align-items: center; gap: 0; }
  .timeline-phase-wrap { flex: 1; display: flex; align-items: center; }
  .timeline-phase-btn {
    flex: 1; padding: 8px 4px; border-radius: 8px;
    border: 2px solid #E2E8F0; background: white;
    transition: all 0.2s;
  }
  .timeline-phase-btn span { font-size: 9px; font-weight: 700; letter-spacing: 0.3px; display: block; text-align: center; }
  .timeline-connector { width: 14px; height: 2px; background: #E2E8F0; flex-shrink: 0; transition: background 0.3s; }

  /* ── Exercise Library ── */
  .ex-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .ex-card { background: white; border-radius: 12px; padding: 16px 18px; border: 1px solid #E2E8F0; }
  .ex-title { font-family: 'DM Serif Display', serif; font-size: 15px; color: #1A202C; margin-bottom: 12px; }
  .accordion-btn {
    width: 100%; text-align: left; padding: 9px 12px;
    border-radius: 8px; border: 1px solid #E2E8F0;
    background: white; display: flex; justify-content: space-between; align-items: center;
    font-size: 12px; font-weight: 600; transition: all 0.15s;
    margin-bottom: 6px;
  }
  .accordion-btn.open { border-radius: 8px 8px 0 0; margin-bottom: 0; }
  .accordion-body {
    border: 1px solid; border-top: none;
    border-radius: 0 0 8px 8px; padding: 10px 12px;
    display: none; margin-bottom: 6px;
  }
  .accordion-body.open { display: block; }
  .ex-item {
    display: flex; align-items: flex-start; gap: 8px;
    padding: 4px 0; font-size: 12px; color: #2D3748; line-height: 1.4;
    border-bottom: 1px dashed rgba(0,0,0,0.08);
  }
  .ex-item:last-child { border-bottom: none; }
  .ex-dot { width: 5px; height: 5px; border-radius: 50%; flex-shrink: 0; margin-top: 6px; }

  .prog-section { margin-top: 0; }
  .prog-title { font-family: 'DM Serif Display', serif; font-size: 15px; color: #1A202C; margin-bottom: 14px; }
  .prog-row { margin-bottom: 14px; }
  .prog-row-header { display: flex; justify-content: space-between; margin-bottom: 4px; }
  .prog-row-label { font-size: 10px; font-weight: 800; letter-spacing: 1px; }
  .prog-row-range { font-size: 10px; color: #718096; }
  .prog-track-wrap { position: relative; height: 8px; background: #EDF2F7; border-radius: 4px; }
  .prog-fill { position: absolute; left: 0; top: 0; height: 100%; border-radius: 4px; transition: width 0.6s cubic-bezier(0.16,1,0.3,1); }
  .prog-marker {
    position: absolute; top: 50%; transform: translate(-50%, -50%);
    border-radius: 50%; border: 2px solid; transition: all 0.3s; z-index: 2;
  }

  .pain-grid { display: flex; gap: 8px; margin-top: 6px; }
  .pain-cell {
    flex: 1; padding: 8px; background: #FAFAFA; border-radius: 8px;
    border: 1px solid #E2E8F0; text-align: center;
  }
  .pain-cell-label { font-size: 9px; color: #718096; margin-bottom: 2px; }
  .pain-cell-val { font-family: 'DM Serif Display', serif; font-size: 18px; }

  .prog-note {
    padding: 12px; border-radius: 8px; border: 1px solid;
    margin-top: 14px;
  }
  .prog-note-label { font-size: 11px; font-weight: 700; margin-bottom: 6px; }
  .prog-note-text { font-size: 12px; color: #4A5568; line-height: 1.5; }

  /* ── Progress button ── */
  .progress-btn {
    padding: 8px 18px; color: white; border: none;
    border-radius: 8px; font-size: 12px; font-weight: 700;
    transition: all 0.2s; display: none;
  }
  .progress-btn:hover { filter: brightness(1.1); transform: translateY(-1px); }

  /* ── Legend ── */
  .legend { display: flex; align-items: center; gap: 14px; flex-wrap: wrap; font-size: 11px; color: #A0AEC0; margin-top: 14px; }
  .legend-dot { width: 8px; height: 8px; border-radius: 50%; display: inline-block; margin-right: 4px; }

  @media (max-width: 900px) {
    .day-grid { grid-template-columns: repeat(4, 1fr); }
    .freq-grid { grid-template-columns: repeat(3, 1fr); }
    .criteria-grid { grid-template-columns: 1fr; }
    .ex-grid { grid-template-columns: 1fr; }
  }
  @media (max-width: 600px) {
    .day-grid { grid-template-columns: repeat(2, 1fr); }
    .freq-grid { grid-template-columns: repeat(2, 1fr); }
  }
</style>
</head>
<body>
<div id="app">

  <!-- TOP BAR -->
  <div class="topbar" id="topbar">
    <div class="topbar-left">
      <div class="topbar-icon" id="topbar-icon">🦵</div>
      <div>
        <div class="topbar-title">Rectus Femoris Pathway</div>
        <div class="topbar-sub">ASPETAR &nbsp;·&nbsp; Exercise Programming Dashboard</div>
      </div>
    </div>
    <div class="phase-badge" id="phase-badge-top">FOUNDATION</div>
  </div>

  <div class="main">

    <!-- PHASE SELECTOR CARD -->
    <div class="card card-pad" style="margin-bottom:16px">
      <div style="display:flex;align-items:flex-start;justify-content:space-between;flex-wrap:wrap;gap:12px">
        <div>
          <div style="display:flex;align-items:baseline;gap:10px;flex-wrap:wrap">
            <span id="phase-heading" style="font-family:'DM Serif Display',serif;font-size:22px;color:#1A202C">Foundation</span>
            <span id="phase-sub" style="font-size:12px;font-weight:600;color:#C0392B">Repair &amp; Restore</span>
          </div>
          <div style="font-size:11px;color:#A0AEC0;margin-top:4px">Select phase to view suggested weekly program and exit criteria</div>
        </div>
        <button class="progress-btn" id="progress-btn">Progress to Reload →</button>
      </div>
      <div class="phase-pills" id="phase-pills"></div>
    </div>

    <!-- PROGRESS STRIP -->
    <div class="progress-strip" id="progress-strip">
      <div class="progress-header">
        <span class="progress-label">EXIT CRITERIA PROGRESS</span>
        <span class="progress-count" id="progress-count">
          <span id="done-count">0</span> / <span id="total-count">0</span>
          <span id="progress-status" style="font-family:'DM Sans',sans-serif;font-size:11px;font-weight:600;margin-left:6px;color:#718096">0% complete</span>
        </span>
      </div>
      <div class="progress-track"><div class="progress-fill" id="progress-fill" style="width:0%;background:#C0392B"></div></div>
    </div>

    <!-- TABS -->
    <div class="tab-bar">
      <button class="tab-btn active" id="tab-week" onclick="switchTab('week')">Weekly Program</button>
      <button class="tab-btn" id="tab-milestones" onclick="switchTab('milestones')">Exit Criteria</button>
      <button class="tab-btn" id="tab-exercises" onclick="switchTab('exercises')">Exercise Library</button>
    </div>

    <!-- TAB: WEEKLY PROGRAM -->
    <div id="pane-week">
      <div class="freq-grid" id="freq-grid"></div>
      <div class="day-grid" id="day-grid"></div>
      <div class="legend" id="legend">
        <span>Click any day to expand</span>
        <span id="today-legend"></span>
        <span><span class="legend-dot" style="background:#2E86C1"></span>Low</span>
        <span><span class="legend-dot" style="background:#27AE60"></span>Mod</span>
        <span><span class="legend-dot" style="background:#D4AC0D"></span>High</span>
        <span><span class="legend-dot" style="background:#C0392B"></span>Very High</span>
      </div>
    </div>

    <!-- TAB: MILESTONES -->
    <div id="pane-milestones" style="display:none">
      <div class="criteria-grid" id="criteria-grid"></div>
    </div>

    <!-- TAB: EXERCISES -->
    <div id="pane-exercises" style="display:none">
      <div class="ex-grid" id="ex-grid"></div>
    </div>

  </div>
</div>

<script>
// ─── DATA ────────────────────────────────────────────────────────────────────

const PHASES = [
  { id:0, key:"foundation",   label:"Foundation",   sub:"Repair & Restore",                     color:"#C0392B", light:"#FDEDEC" },
  { id:1, key:"reload",       label:"Reload",       sub:"Strength & Movement Re-Development",   color:"#D35400", light:"#FEF0E7" },
  { id:2, key:"accumulation", label:"Accumulation", sub:"Strength & Running Volume",             color:"#D4AC0D", light:"#FEF9E7" },
  { id:3, key:"transition",   label:"Transition",   sub:"High Speed Running & Drill-Based",     color:"#1E8449", light:"#EAFAF1" },
  { id:4, key:"simulation",   label:"Simulation",   sub:"Game Scenarios, Intensity & Volume",   color:"#1A5276", light:"#EAF2FF" },
  { id:5, key:"resilience",   label:"Resilience",   sub:"Return to Performance & Robustness",   color:"#4A235A", light:"#F5EEF8" },
];

const COMP_COLORS = {
  "Strength":"#2C5364","Motor Control":"#1A5276",
  "Explosiveness":"#6C3483","Running":"#1E8449",
  "Sport Specific":"#784212","Conditioning":"#717D7E",
};

const INTENSITY = {
  "Low":      { bg:"#EBF5FB", text:"#1A5276", dot:"#2E86C1" },
  "Low–Mod":  { bg:"#E8F8F5", text:"#1E8449", dot:"#27AE60" },
  "Mod":      { bg:"#FEF9E7", text:"#7D6608", dot:"#D4AC0D" },
  "Mod–High": { bg:"#FEF0E7", text:"#784212", dot:"#D35400" },
  "High":     { bg:"#FDEDEC", text:"#7B241C", dot:"#C0392B" },
  "Very High":{ bg:"#F9EBEA", text:"#641E16", dot:"#A93226" },
  "Max":      { bg:"#F4ECF7", text:"#4A235A", dot:"#7D3C98" },
};

const EXIT_CRITERIA = {
  foundation: {
    clinical:[
      { id:"pain_adl",   label:"Rehab pain ≤4/10 during / after sessions" },
      { id:"squat_3",    label:"3 reps: double leg squat, straight leg raise, double leg bridge, mini SL squat" },
      { id:"leg_swings", label:"Leg swings tolerated (within surgical restrictions)" },
    ],
    strength:[
      { id:"knee_ext_f", label:"Reclined knee extension ISO (40/60°) LSI ≥70%", note:"Target: ≥70% LSI" },
      { id:"hip_flex_f", label:"90/90 Hip Flexion Break LSI ≥70%", note:"Target: ≥70% LSI" },
      { id:"slr_f",      label:"SLR Break LSI ≥70%", note:"Target: ≥70% LSI" },
    ],
  },
  reload: {
    clinical:[
      { id:"pain_r",     label:"Rehab pain ≤2/10" },
      { id:"palp_r",     label:"Palpation pain length — Improving" },
      { id:"pkf_100",    label:"Prone passive knee flexion ≥100° (hip 0°)" },
      { id:"swings_50",  label:"Leg swings ≥50% intensity" },
    ],
    strength:[
      { id:"ke_r",  label:"Knee Extension ISO LSI ≥70%", note:"Target: ≥70% LSI" },
      { id:"hf_r",  label:"90/90 Hip Flexion LSI ≥70%", note:"Target: ≥70% LSI" },
      { id:"slr_r", label:"SLR Break LSI ≥70%", note:"Target: ≥70% LSI" },
    ],
    performance:[
      { id:"speed_r",   label:"Max Sprint Speed ≥70% Linear & Multi-directional" },
      { id:"td_r",      label:"Total Distance ≥50% match demands" },
      { id:"hsr_r",     label:"High Speed Running ≥50% match demands" },
      { id:"kick_med",  label:"Tolerating Medium Demand Kicking" },
    ],
  },
  accumulation: {
    clinical:[
      { id:"pain_a",    label:"Rehab pain free (0/10)" },
      { id:"palp_a",    label:"Palpation pain length — Improving" },
      { id:"pkf_90",    label:"Prone passive knee flexion ROM LSI ≥90%" },
      { id:"outer_a",   label:"Outer range pain provocation NRS ≥9/10 power, pain free" },
    ],
    strength:[
      { id:"ke_a",  label:"Knee Extension ISO LSI ≥90%", note:"Target: ≥90% LSI" },
      { id:"hf_a",  label:"90/90 Hip Flexion LSI ≥90%", note:"Target: ≥90% LSI" },
      { id:"slr_a", label:"SLR Break LSI ≥90%", note:"Target: ≥90% LSI" },
    ],
    performance:[
      { id:"speed_a",   label:"Max Sprint Speed ≥75% Linear & Multi-directional" },
      { id:"td_a",      label:"Total Distance ≥50% match demands" },
      { id:"kick_hi",   label:"Tolerating High Demand Kicking" },
    ],
  },
  transition: {
    clinical:[
      { id:"pain_t",   label:"Pain free during rehab (0/10)" },
      { id:"palp_t",   label:"No palpation pain" },
      { id:"pkf_95",   label:"Prone passive knee flexion ROM LSI ≥95%" },
      { id:"outer_t",  label:"Outer range pain provocation — Symmetrical" },
    ],
    strength:[
      { id:"ke_t",  label:"Knee Extension ISO LSI ≥95%", note:"Target: ≥95% LSI" },
      { id:"hf_t",  label:"90/90 Hip Flexion LSI ≥95%", note:"Target: ≥95% LSI" },
      { id:"slr_t", label:"SLR Break LSI ≥95%", note:"Target: ≥95% LSI" },
    ],
    performance:[
      { id:"speed_t",  label:"Max Sprint Speed ≥80% Linear & Multi-directional" },
      { id:"cmj_t",    label:"Countermovement Jump LSI ≥90%" },
      { id:"dj_t",     label:"Drop Jump LSI ≥90%" },
      { id:"kick_max", label:"Tolerating Maximal Demand Kicking" },
    ],
  },
  simulation: {
    clinical:[
      { id:"no_reg_s", label:"No regression of clinical assessment from previous phase" },
    ],
    performance:[
      { id:"speed_s",  label:"Max Sprint Speed ≥95% Linear & Multi-directional" },
      { id:"vol_s",    label:"Total Distance, HSR, VHSR ≥75% match demands" },
      { id:"wcs_s",    label:"≥2 exposures of 100% WCS for 1 & 5-min blocks" },
      { id:"f0_s",     label:"F0 ≥90% baseline or ≥7.5 N/kg" },
    ],
  },
  resilience: {
    clinical:[
      { id:"no_reg_r",  label:"No regression of clinical assessment" },
      { id:"targets_r", label:"All outstanding performance assessment targets achieved" },
    ],
  },
};

const FREQ = {
  Strength:      { foundation:"5×/wk", reload:"3×/wk", accumulation:"2–3×/wk", transition:"2×/wk", simulation:"2×/wk", resilience:"Maintain" },
  "Motor Control":{ foundation:"5×/wk", reload:"3×/wk", accumulation:"3×/wk",   transition:"2×/wk", simulation:"2×/wk", resilience:"Maintain" },
  Explosiveness: { foundation:"N/A",    reload:"2×/wk", accumulation:"2×/wk",   transition:"2×/wk", simulation:"2×/wk", resilience:"Maintain" },
  Running:       { foundation:"N/A",    reload:"4×/wk", accumulation:"3–4×/wk", transition:"4×/wk", simulation:"5×/wk", resilience:"Maintain" },
  "Sport Specific":{ foundation:"N/A", reload:"N/A",    accumulation:"3–4×/wk", transition:"4×/wk", simulation:"5×/wk", resilience:"Full" },
  Conditioning:  { foundation:"UL only",reload:"Mostly UL",accumulation:"Cross-train",transition:"Mixed",simulation:"Run-based",resilience:"Maintain" },
};

const WEEKLY = {
  foundation:[
    { day:"Monday",   focus:"STRENGTH", sessions:[
        { comp:"Strength",      label:"Rectus Femoris & General", detail:"Knee ext ISO + Hip flex ISO, 3×5 reps",           intensity:"Low–Mod" },
        { comp:"Motor Control", label:"Motor Control",            detail:"SL squat, bridge, heel raise, hip hinge — 3 reps",intensity:"Low" }],
      other:["Conditioning: Upper limb only","Recovery"] },
    { day:"Tuesday",  focus:"MOTOR CONTROL", sessions:[
        { comp:"Motor Control", label:"Motor Control",    detail:"Compound movements, hip control, trunk",           intensity:"Low" },
        { comp:"Strength",      label:"Rectus Femoris",   detail:"Focused muscle contraction, isometric ramp",       intensity:"Low" }],
      other:["Hydrotherapy (if required)"] },
    { day:"Wednesday",focus:"STRENGTH", sessions:[
        { comp:"Strength",      label:"Rectus Femoris & General", detail:"Knee ext ISO + Hip flex ISO, progress range", intensity:"Low–Mod" },
        { comp:"Motor Control", label:"Motor Control",            detail:"Movement patterns — quality focus",           intensity:"Low" }],
      other:["Conditioning: Upper limb","Recovery"] },
    { day:"Thursday", focus:"MOTOR CONTROL", sessions:[
        { comp:"Motor Control", label:"Motor Control",  detail:"Segmental: ASLR, hip abduction, bridges",    intensity:"Low" },
        { comp:"Strength",      label:"Rectus Femoris", detail:"Isometric holds — short to mid range",       intensity:"Low" }],
      other:["Hydrotherapy (if required)"] },
    { day:"Friday",   focus:"STRENGTH", sessions:[
        { comp:"Strength",      label:"Rectus Femoris & General", detail:"Progress loads within pain tolerance",intensity:"Mod" },
        { comp:"Motor Control", label:"Motor Control",            detail:"SL balance, hip hinge, RDL pattern", intensity:"Low" }],
      other:["Conditioning: Upper limb","Recovery"] },
    { day:"Saturday", focus:"OPTIONAL", sessions:[
        { comp:"Motor Control", label:"Motor Control",  detail:"Light motor control — optional",                     intensity:"Low" },
        { comp:"Strength",      label:"Rectus Femoris", detail:"Maintenance RF strength if tolerated",               intensity:"Low" }],
      other:["Conditioning: Upper limb"] },
    { day:"Sunday",   focus:"RECOVERY", sessions:[], other:["Rest & Recovery"] },
  ],
  reload:[
    { day:"Monday",   focus:"STRENGTH", sessions:[
        { comp:"Explosiveness", label:"Reactive Strength — General Lower Limb", detail:"Pogos, multi-dir hop (low intensity)",intensity:"Low–Mod" },
        { comp:"Running",       label:"Running: Mechanics & Jog",               detail:"Run drills + jogging <40% MSS",       intensity:"Low" }],
      other:["Strength: RF & General (Session 2)","Recovery"] },
    { day:"Tuesday",  focus:"MC / RUN PREP", sessions:[
        { comp:"Motor Control", label:"Motor Control",          detail:"Compound movements, foot & ankle, RF lengthening",intensity:"Low" },
        { comp:"Running",       label:"Running: Mechanics & Jog",detail:"A-skip, wall drill, figure-of-4 drills",          intensity:"Low" }],
      other:["Conditioning: Cross-training"] },
    { day:"Wednesday",focus:"STRENGTH", sessions:[
        { comp:"Strength", label:"Rectus Femoris", detail:"Tri-phasic: progress range & load", intensity:"Mod" }],
      other:["Recovery"] },
    { day:"Thursday", focus:"MC / RUN PREP", sessions:[
        { comp:"Explosiveness", label:"Reactive Strength — Lower Limb",  detail:"Hopping progression",        intensity:"Low–Mod" },
        { comp:"Running",       label:"Running: Mechanics & Jog",        detail:"Mechanics + light jog",      intensity:"Low" }],
      other:["Conditioning: Cross-training"] },
    { day:"Friday",   focus:"STRENGTH", sessions:[
        { comp:"Strength", label:"Rectus Femoris & General", detail:"Tri-phasic: slow tempo, progress load",intensity:"Mod" },
        { comp:"Running",  label:"Running: Mechanics",       detail:"Pre-run drills only",                  intensity:"Low" }],
      other:["Recovery"] },
    { day:"Saturday", focus:"OPTIONAL", sessions:[
        { comp:"Motor Control", label:"Motor Control", detail:"Optional maintenance session", intensity:"Low" }],
      other:["Conditioning: Cross-training"] },
    { day:"Sunday",   focus:"RECOVERY", sessions:[], other:["Rest & Recovery"] },
  ],
  accumulation:[
    { day:"Monday",   focus:"RUNNING & PLYOS", sessions:[
        { comp:"Explosiveness",  label:"Reactive Strength",        detail:"Isometric hopping, pogo progressions",   intensity:"Mod" },
        { comp:"Running",        label:"Running: Mechanics & Speed",detail:"Fly 10s, 30–100m tempos, <75% MSS",     intensity:"Mod" },
        { comp:"Sport Specific", label:"Sport Specific: Kicking",  detail:"Low intensity drills incl. kicking",    intensity:"Low–Mod" }],
      other:["Strength: RF (Session 2)","Motor Control","Conditioning: Cross-training"] },
    { day:"Tuesday",  focus:"STRENGTH / EXPL", sessions:[
        { comp:"Explosiveness", label:"Explosiveness",      detail:"Reclined explosive knee ext (45°), squat jump",intensity:"Mod–High" },
        { comp:"Strength",      label:"Strength: General",  detail:"General lower limb: squat/lunge, hamstrings",  intensity:"Mod" }],
      other:["Running: Volume (Session 2)","Sport Specific: Kicking","Recovery"] },
    { day:"Wednesday",focus:"MOTOR CONTROL / RECOVERY", sessions:[
        { comp:"Motor Control", label:"Motor Control", detail:"Compound movements + RF lengthening", intensity:"Low" }],
      other:["Conditioning: Cross-training","Recovery"] },
    { day:"Thursday", focus:"STRENGTH / EXPL", sessions:[
        { comp:"Explosiveness",  label:"Reactive Strength",         detail:"CMJ, multi-dir hops",           intensity:"Mod–High" },
        { comp:"Running",        label:"Running: Mechanics & Speed", detail:"Speed exposure, shuttles",     intensity:"Mod" },
        { comp:"Sport Specific", label:"Sport Specific: Kicking",   detail:"Progress kicking volume",      intensity:"Mod" }],
      other:["Strength: RF (Session 2)","Motor Control"] },
    { day:"Friday",   focus:"RUNNING & PLYOS", sessions:[
        { comp:"Explosiveness", label:"Explosiveness",     detail:"Countermovement jump, horizontal jumps",intensity:"High" },
        { comp:"Running",       label:"Running: Volume",   detail:"Running volume accumulation",           intensity:"Mod" }],
      other:["Sport Specific: Kicking","Recovery"] },
    { day:"Saturday", focus:"OPTIONAL", sessions:[
        { comp:"Strength",      label:"Strength: RF",   detail:"Maintenance / eccentric overload",  intensity:"Mod" },
        { comp:"Motor Control", label:"Motor Control",  detail:"Optional supplementary session",    intensity:"Low" }],
      other:["Recovery"] },
    { day:"Sunday",   focus:"RECOVERY", sessions:[], other:["Rest & Recovery"] },
  ],
  transition:[
    { day:"Monday",   focus:"FAST", sessions:[
        { comp:"Motor Control", label:"Motor Control",       detail:"Dynamic warm-up focus",                    intensity:"Low" },
        { comp:"Explosiveness", label:"Reactive Strength",   detail:"Max intent hopping, resisted kicking",     intensity:"High" },
        { comp:"Running",       label:"Running: Mechanics",  detail:"Linear/curvilinear speed, accel/decel",    intensity:"High" }],
      other:["Sport Specific: Drill-based (speed) — Session 2","Recovery"] },
    { day:"Tuesday",  focus:"FIT / STRONG", sessions:[
        { comp:"Explosiveness", label:"Explosiveness",        detail:"Flywheel kick, sled accel, broad jump",   intensity:"High" },
        { comp:"Strength",      label:"Strength: RF & General",detail:"Unrestricted individualised loading",   intensity:"High" }],
      other:["Running: Mechanics — Session 2","Sport Specific: Drill-based (volume)"] },
    { day:"Wednesday",focus:"OPTIONAL", sessions:[
        { comp:"Running",        label:"Running: Static Mechanics",    detail:"Mechanics only, low intensity",  intensity:"Low" },
        { comp:"Sport Specific", label:"Sport Specific: Low Intensity",detail:"Low demand drill work",          intensity:"Low" }],
      other:["Conditioning: Cross-training","Recovery"] },
    { day:"Thursday", focus:"FAST", sessions:[
        { comp:"Motor Control", label:"Motor Control",       detail:"Reactive motor control",           intensity:"Low–Mod" },
        { comp:"Explosiveness", label:"Reactive Strength",   detail:"Max intent hopping progression",   intensity:"High" },
        { comp:"Running",       label:"Running: Mechanics",  detail:"COD, reactive drills",             intensity:"High" }],
      other:["Sport Specific: Drill-based (speed) — Session 2","Recovery"] },
    { day:"Friday",   focus:"FIT / STRONG", sessions:[
        { comp:"Explosiveness", label:"Explosiveness",    detail:"Cable cross kick, flywheel progressions",  intensity:"High" },
        { comp:"Strength",      label:"Strength: RF",     detail:"Individualised RF loading",               intensity:"High" }],
      other:["Running: Mechanics — Session 2","Sport Specific: Drill-based (volume)"] },
    { day:"Saturday", focus:"OPTIONAL", sessions:[
        { comp:"Strength",      label:"Strength: General", detail:"General lower limb maintenance", intensity:"Mod" },
        { comp:"Motor Control", label:"Motor Control",     detail:"Optional supplementary session", intensity:"Low" }],
      other:["Recovery"] },
    { day:"Sunday",   focus:"RECOVERY", sessions:[], other:["Rest & Recovery"] },
  ],
  simulation:[
    { day:"Monday",   focus:"FAST", sessions:[
        { comp:"Motor Control",  label:"Motor Control",                   detail:"Pre-activation / warm-up",                  intensity:"Low" },
        { comp:"Explosiveness",  label:"Explosiveness & Reactive Strength",detail:"CMJ, drop jumps, resisted kicking",         intensity:"High" },
        { comp:"Running",        label:"Running: Mechanics",              detail:"Speed exposure, sprinting",                  intensity:"High" }],
      other:["Sport Specific: Game-based (speed) — Session 2","Recovery"] },
    { day:"Tuesday",  focus:"FIT / STRONG", sessions:[
        { comp:"Running",        label:"Running: Mechanics",          detail:"Mechanics drills, tempo runs",            intensity:"Mod" },
        { comp:"Sport Specific", label:"Sport Specific: Game-based (Volume)",detail:"Small-sided games, high demand kicking",intensity:"High" }],
      other:["Strength: RF & General — Session 2","Recovery"] },
    { day:"Wednesday",focus:"OPTIONAL", sessions:[
        { comp:"Running",        label:"Running: Mechanics",              detail:"Light mechanics only",       intensity:"Low" },
        { comp:"Sport Specific", label:"Sport Specific: Low Intensity",   detail:"Low intensity sport-specific",intensity:"Low" }],
      other:["Conditioning: Cross-training","Recovery"] },
    { day:"Thursday", focus:"FAST", sessions:[
        { comp:"Motor Control",  label:"Motor Control",                    detail:"Pre-activation",                           intensity:"Low" },
        { comp:"Explosiveness",  label:"Explosiveness & Reactive Strength",detail:"Game simulation plyometrics",              intensity:"High" },
        { comp:"Running",        label:"Running: Mechanics + Speed",       detail:"Full speed exposure, sprints",             intensity:"Very High" }],
      other:["Sport Specific: Game-based (speed) — Session 2","Recovery"] },
    { day:"Friday",   focus:"FIT / STRONG", sessions:[
        { comp:"Running",        label:"Running: Mechanics",          detail:"Volume mechanics",          intensity:"Mod" },
        { comp:"Sport Specific", label:"Sport Specific: Game-based (Volume)",detail:"Full game simulation session",intensity:"Very High" }],
      other:["Strength: RF & General — Session 2","Recovery"] },
    { day:"Saturday", focus:"OPTIONAL", sessions:[
        { comp:"Motor Control",  label:"Motor Control",             detail:"Optional recovery session",  intensity:"Low" },
        { comp:"Sport Specific", label:"Sport Specific: Low Int.",  detail:"Light skills work",          intensity:"Low" }],
      other:["Conditioning: Cross-training","Recovery"] },
    { day:"Sunday",   focus:"RECOVERY", sessions:[], other:["Rest & Recovery"] },
  ],
  resilience:[
    { day:"Monday",   focus:"TEAM TRAINING", sessions:[
        { comp:"Sport Specific", label:"Return to Full Team Training", detail:"Unrestricted team training / match play", intensity:"Very High" }],
      other:["Strength: Progress / maintain","Conditioning: Progress / maintain"] },
    { day:"Tuesday",  focus:"RECOVERY / STR", sessions:[
        { comp:"Strength",      label:"Strength: Progress / Maintain", detail:"Ongoing RF loading program", intensity:"Mod–High" },
        { comp:"Motor Control", label:"Motor Control",                 detail:"Maintenance",                intensity:"Low" }],
      other:["Recovery"] },
    { day:"Wednesday",focus:"TEAM TRAINING", sessions:[
        { comp:"Sport Specific", label:"Team Training / Tactical", detail:"Full participation", intensity:"Very High" }],
      other:["Conditioning: Maintain"] },
    { day:"Thursday", focus:"STRENGTH / REC", sessions:[
        { comp:"Strength", label:"Strength: Maintain", detail:"RF specific maintenance loading", intensity:"Mod" }],
      other:["Recovery"] },
    { day:"Friday",   focus:"TEAM TRAINING", sessions:[
        { comp:"Sport Specific", label:"Match Preparation", detail:"Pre-match preparation", intensity:"High" }],
      other:["Conditioning: Maintain"] },
    { day:"Saturday", focus:"MATCH / TEAM", sessions:[
        { comp:"Sport Specific", label:"Match / Team Training", detail:"Full unrestricted participation", intensity:"Max" }],
      other:[] },
    { day:"Sunday",   focus:"RECOVERY", sessions:[], other:["Rest & Recovery"] },
  ],
};

const EXERCISES = {
  Strength:{
    foundation:["Focused muscle contraction (isometric ramp)","Reclined knee extension ISO 40/60°","Hip flexion isometric (bent knee) — inner to mid range","Supine hip flexion isometric","General: DL squat, bridge, heel raise"],
    reload:["Reclined knee extension — tri-phasic, progress range","Hip flexion (knee flexed) — progress to standing cable","Hip flexion (knee extended) — isometric to tri-phasic","General: hamstring, squat/lunge, calf"],
    accumulation:["Knee extension tri-phasic to eccentric overload","Hip flexion standing cable kick — controlled to max intent","Split squat, ½ kneel cable knee extension","General: eccentric loading, plyometric prep"],
    transition:["Reclined knee extension eccentric overload — 2-up/1-down","½ kneel cable knee extension eccentric","Flywheel kick","Unrestricted individualised loading"],
    simulation:["Flywheel kick — max load","Unrestricted individualised","General lower limb maintenance"],
    resilience:["Progress / maintain RF loading","Individualised programme"],
  },
  "Motor Control":{
    foundation:["Double & single leg squat","Double & single leg bridge","Double & single leg heel raise","Hip hinge","Segmental: ASLR, hip abduction, inner range hamstring"],
    reload:["Assisted SL squat → SL squat to 90°","SL hinge (RDL bodyweight → +waterbag)","Hip hitch (supported → unsupported)","External rotators: 4-point kneeling → squat clam","Iliopsoas: supine inner range hold → standing resisted"],
    accumulation:["SL squat to 90° + dowel / waterbag","SL RDL + rotation + waterbag","Hurdle hip hitch","Trunk: Pallof press, supine oblique cable","RF lengthening: assisted reverse nordic, leg swings"],
    transition:["Isolated & compound motor control","Supplement running mechanics as required","Foot & ankle: blackboard, FHL, intrinsics"],
    simulation:["Isolated & compound","Integrated into sport-specific warm-up"],
    resilience:["Progress / maintain"],
  },
  Running:{
    reload:["Run mechanics drills: A-skip, wall drill, figure of 4","Jogging <40% MSS (12 km/hr)","30–200m upright tempo runs"],
    accumulation:["Generic running <75% MSS","Fly 10s, 30–100m tempos","10–50m shuttles","Accel/decel: 5–20m submaximal"],
    transition:["Mixed generic & sport-specific <85% MSS","Linear/curvilinear speed exposure","Shuttles (HIIT)","5–30m accel/decel","Planned COD: domino run, 5-0-5 to 15-0-5"],
    simulation:["Predominantly sport-specific <100% MSS","Reactive COD","Small-sided games","Game-based training"],
    resilience:["Progress / maintain field metrics"],
  },
};

const PROG_NOTES = {
  foundation:   "Predominantly isometric: short to mid range. 5×/week. Pain ≤4/10. Minimum 6 hr recovery between sessions.",
  reload:       "Tri-phasic: progress range & load. 3×/week. Slow tempo throughout. 48 hr recovery between heavy sessions.",
  accumulation: "Tri-phasic progress to eccentric overload. 2–3×/week. Controlled to max intent. 48–72 hr recovery.",
  transition:   "Unrestricted, individualised. 2×/week. Max intent throughout. 48–72 hr recovery between sessions.",
  simulation:   "Unrestricted, individualised. 2×/week. Eccentric overload and flywheel work. Integrate into game-day week.",
  resilience:   "Progress and maintain. Integrate RF loading into full training week.",
};

const PAIN_GUIDE = {
  foundation:   { iso:"≤4/10", tri:"≤3/10", ecc:"0/10" },
  reload:       { iso:"≤3/10", tri:"≤3/10", ecc:"0/10" },
  accumulation: { iso:"≤1/10", tri:"≤1/10", ecc:"0/10" },
  transition:   { iso:"0/10",  tri:"0/10",  ecc:"0/10" },
  simulation:   { iso:"0/10",  tri:"0/10",  ecc:"0/10" },
  resilience:   { iso:"0/10",  tri:"0/10",  ecc:"0/10" },
};

// ─── STATE ───────────────────────────────────────────────────────────────────
let currentPhase = 0;
let checks = {};
let currentTab = "week";
const todayIdx = (() => { const d=new Date().getDay(); return d===0?6:d-1; })();

// ─── UTILS ───────────────────────────────────────────────────────────────────
function hex2rgba(hex, a) {
  const r=parseInt(hex.slice(1,3),16), g=parseInt(hex.slice(3,5),16), b=parseInt(hex.slice(5,7),16);
  return `rgba(${r},${g},${b},${a})`;
}
function el(id){ return document.getElementById(id); }
function mk(tag,attrs={},children=[]){
  const e=document.createElement(tag);
  Object.entries(attrs).forEach(([k,v])=>{ if(k==='style')Object.assign(e.style,v); else if(k==='className')e.className=v; else e[k]=v; });
  children.forEach(c=>{ if(typeof c==='string')e.appendChild(document.createTextNode(c)); else if(c)e.appendChild(c); });
  return e;
}

// ─── RENDER PHASE PILLS ──────────────────────────────────────────────────────
function renderPills() {
  const container = el('phase-pills'); container.innerHTML='';
  PHASES.forEach(p => {
    const btn = mk('button',{
      className:'phase-pill'+(currentPhase===p.id?' active':''),
      onclick:()=>{ currentPhase=p.id; render(); }
    },[p.label]);
    if(currentPhase===p.id){
      btn.style.background=p.color; btn.style.borderColor=p.color;
      btn.style.boxShadow=`0 2px 8px ${p.color}55`;
    }
    container.appendChild(btn);
  });
}

// ─── RENDER FREQ GRID ────────────────────────────────────────────────────────
function renderFreq() {
  const p = PHASES[currentPhase];
  const container = el('freq-grid'); container.innerHTML='';
  Object.entries(FREQ).forEach(([comp,freqs])=>{
    const f = freqs[p.key]||'—';
    const isNA = f==='N/A';
    const col = COMP_COLORS[comp]||'#4A5568';
    const card = mk('div',{className:'freq-card',style:{
      opacity: isNA?'0.4':'1',
      border:`1px solid ${isNA?'#EDF2F7':col+'33'}`,
      background: isNA?'#FAFAFA':'white',
    }});
    const label = mk('div',{className:'freq-label',style:{color:col}},
      [comp.replace(' & Reactive Strength','').replace('Explosiveness','Expl.')]);
    const val = mk('div',{className:'freq-val',style:{color:isNA?'#CBD5E0':col}},[f]);
    card.appendChild(label); card.appendChild(val);
    container.appendChild(card);
  });
}

// ─── RENDER DAY GRID ─────────────────────────────────────────────────────────
function renderDays() {
  const p = PHASES[currentPhase];
  const days = WEEKLY[p.key];
  const container = el('day-grid'); container.innerHTML='';

  days.forEach((day,i)=>{
    const isToday = i===todayIdx;
    const isRec = day.focus==='RECOVERY';
    const isOpt = day.focus==='OPTIONAL';
    const hasSessions = day.sessions.length>0;

    const card = mk('div',{className:`day-card${isToday?' today':''}${isRec?' recovery':''}`,style:{
      borderColor: isToday?p.color:'#E2E8F0',
      borderWidth: isToday?'2px':'1px',
      boxShadow: isToday?`0 4px 20px ${p.color}33`:'0 1px 4px rgba(0,0,0,0.05)',
    }});

    // Header
    const hdr = mk('div',{className:`day-header${hasSessions?' has-sessions':''}`,style:{
      background: isRec?'#F7FAFC': isToday?hex2rgba(p.color,0.07):'white',
    }});
    if(hasSessions) hdr.style.cursor='pointer';

    const topRow = mk('div',{style:{display:'flex',justifyContent:'space-between',alignItems:'center'}});
    const nameSpan = mk('span',{className:'day-name'},[day.day]);
    if(isToday){
      const badge = mk('span',{className:'day-today-badge',style:{color:p.color}},['TODAY']);
      nameSpan.appendChild(badge);
    }
    topRow.appendChild(nameSpan);
    if(hasSessions) topRow.appendChild(mk('span',{className:'day-caret'},['▼']));
    hdr.appendChild(topRow);

    // Focus pill
    const focusPill = mk('div',{className:'day-focus-pill',style:{
      background: isRec||isOpt ? '#EDF2F7' : hex2rgba(p.color,0.13),
      color: isRec||isOpt ? '#718096' : p.color,
    }},[day.focus]);
    hdr.appendChild(focusPill);

    // Body
    const body = mk('div',{className:'day-body'});
    day.sessions.forEach(s=>{
      const sc = mk('div',{className:'session-card'});
      const top = mk('div',{className:'session-top'});

      // comp tag
      const cc = COMP_COLORS[s.comp]||'#4A5568';
      const ctag = mk('span',{className:'comp-tag',style:{
        background:cc+'18',color:cc
      }},[s.comp]);
      top.appendChild(ctag);

      // intensity badge
      const ic = INTENSITY[s.intensity]||INTENSITY['Mod'];
      const ibadge = mk('span',{className:'intensity-badge',style:{background:ic.bg,color:ic.text}});
      ibadge.appendChild(mk('span',{className:'intensity-dot',style:{background:ic.dot}}));
      ibadge.appendChild(document.createTextNode(' '+s.intensity));
      top.appendChild(ibadge);
      sc.appendChild(top);

      sc.appendChild(mk('div',{className:'session-name'},[s.label]));
      sc.appendChild(mk('div',{className:'session-detail'},[s.detail]));
      body.appendChild(sc);
    });
    if(day.other.length){
      const oth = mk('div',{className:'day-other'});
      day.other.forEach(o=>{ oth.appendChild(mk('div',{className:'day-other-item'},['• '+o])); });
      body.appendChild(oth);
    }

    // Toggle
    if(hasSessions){
      hdr.addEventListener('click',()=>{
        const caret = hdr.querySelector('.day-caret');
        const isOpen = body.classList.contains('open');
        body.classList.toggle('open',!isOpen);
        if(caret) caret.textContent = isOpen?'▼':'▲';
      });
    }

    card.appendChild(hdr);
    card.appendChild(body);
    container.appendChild(card);
  });
}

// ─── CRITERIA HELPERS ────────────────────────────────────────────────────────
function getCriteria(){
  const c = EXIT_CRITERIA[PHASES[currentPhase].key]||{};
  return [
    ...(c.clinical||[]).map(x=>({...x,cat:'clinical'})),
    ...(c.strength||[]).map(x=>({...x,cat:'strength'})),
    ...(c.performance||[]).map(x=>({...x,cat:'performance'})),
  ];
}
function updateProgress(){
  const p = PHASES[currentPhase];
  const all = getCriteria();
  const done = all.filter(c=>checks[`${p.key}_${c.id}`]).length;
  const total = all.length;
  const pct = total>0?Math.round(done/total*100):0;
  const ready = pct===100 && total>0;

  el('done-count').textContent=done;
  el('total-count').textContent=total;
  const fill = el('progress-fill');
  fill.style.width=pct+'%';
  fill.style.background = ready?'#38A169':p.color;
  const status = el('progress-status');
  status.textContent = ready?'✓ Ready to progress':`${pct}% complete`;
  status.style.color = ready?'#276749':'#718096';

  const btn = el('progress-btn');
  if(ready && currentPhase<5){
    btn.style.display='block';
    btn.textContent=`Progress to ${PHASES[currentPhase+1].label} →`;
    btn.style.background=p.color;
    btn.style.boxShadow=`0 4px 12px ${p.color}55`;
    btn.onclick=()=>{ currentPhase++; render(); };
  } else { btn.style.display='none'; }
}

// ─── RENDER MILESTONES ───────────────────────────────────────────────────────
function renderMilestones(){
  const p = PHASES[currentPhase];
  const crit = EXIT_CRITERIA[p.key]||{};
  const container = el('criteria-grid'); container.innerHTML='';

  function makeSection(title, sub, items, fullWidth){
    if(!items||!items.length) return;
    const sec = mk('div',{className:'criteria-section',style: fullWidth?{gridColumn:'1/-1'}:{}});
    sec.appendChild(mk('div',{className:'criteria-title'},[title]));
    sec.appendChild(mk('div',{className:'criteria-sub'},[sub]));
    items.forEach(item=>{
      const key=`${p.key}_${item.id}`;
      const checked=!!checks[key];
      const row = mk('div',{className:`check-item${checked?' checked':''}`,onclick:()=>{
        checks[key]=!checks[key];
        render();
      }});
      const box = mk('div',{className:`check-box${checked?' checked':''}`});
      box.appendChild(mk('span',{className:'check-tick'},['✓']));
      row.appendChild(box);
      const lbl = mk('span',{className:`check-label${checked?' checked':''}`},[item.label]);
      row.appendChild(lbl);
      sec.appendChild(row);
      if(item.note && !checked){
        const note = mk('div',{style:{padding:'0 10px 4px 28px',fontSize:'10px',color:'#718096'}},['→ '+item.note]);
        sec.appendChild(note);
      }
    });
    container.appendChild(sec);
  }

  makeSection('Clinical Criteria','Daily monitoring',crit.clinical);
  makeSection('Strength Criteria','Bi-weekly assessment',crit.strength);
  makeSection('Performance / Field Criteria','GPS & kicking metrics',crit.performance, !crit.clinical&&!crit.strength);

  // Summary
  const all = getCriteria();
  const done = all.filter(c=>checks[`${p.key}_${c.id}`]).length;
  const total = all.length;
  const ready = done===total && total>0;
  const summary = mk('div',{className:'summary-card',style:{
    background: ready?'#F0FFF4':p.light,
    borderColor: ready?'#9AE6B4':p.color+'44',
  }});
  const sLeft = mk('div');
  sLeft.appendChild(mk('div',{className:'summary-title',style:{color:ready?'#276749':p.color}},
    [ready?`✓ All ${p.label} criteria met — ready to progress`:`${done} of ${total} ${p.label} criteria met`]));
  sLeft.appendChild(mk('div',{className:'summary-sub'},
    [ready?(currentPhase<5?`Discuss progression to ${PHASES[currentPhase+1].label} with clinical team`:'Continue in Resilience phase')
           :'Continue working through current phase criteria before progressing']));
  summary.appendChild(sLeft);
  summary.appendChild(mk('div',{className:'summary-pct',style:{color:ready?'#276749':p.color}},
    [done&&total?(Math.round(done/total*100)+'%'):'0%']));
  container.appendChild(summary);

  // Timeline
  const tl = mk('div',{className:'timeline-card'});
  tl.appendChild(mk('div',{className:'timeline-title'},['Phase Timeline']));
  const track = mk('div',{className:'timeline-track'});
  PHASES.forEach((ph,i)=>{
    const wrap = mk('div',{className:'timeline-phase-wrap'});
    const btn = mk('button',{className:'timeline-phase-btn',style:{
      borderColor: i===currentPhase?ph.color:i<currentPhase?'#9AE6B4':'#E2E8F0',
      background: i===currentPhase?ph.color:i<currentPhase?'#F0FFF4':'white',
    },onclick:()=>{ currentPhase=i; render(); }});
    const lbl = mk('span',{style:{
      color: i===currentPhase?'white':i<currentPhase?'#276749':'#A0AEC0',
    }},[ph.label.toUpperCase()]);
    btn.appendChild(lbl);
    wrap.appendChild(btn);
    if(i<PHASES.length-1){
      wrap.appendChild(mk('div',{className:'timeline-connector',style:{
        background: i<currentPhase?'#9AE6B4':'#E2E8F0'
      }}));
    }
    track.appendChild(wrap);
  });
  tl.appendChild(track);
  container.appendChild(tl);
}

// ─── RENDER EXERCISES ────────────────────────────────────────────────────────
function renderExercises(){
  const p = PHASES[currentPhase];
  const container = el('ex-grid'); container.innerHTML='';

  // Left: exercise library accordion
  const libCard = mk('div',{className:'ex-card'});
  libCard.appendChild(mk('div',{className:'ex-title'},['Exercise Library']));
  libCard.appendChild(mk('div',{style:{fontSize:'11px',color:'#718096',marginBottom:'10px'}},['Key exercises for this phase']));

  const relevantComps = Object.keys(EXERCISES).filter(c=>EXERCISES[c][p.key]);
  relevantComps.forEach(comp=>{
    const col = COMP_COLORS[comp]||'#4A5568';
    const items = EXERCISES[comp][p.key];
    const uid = `acc_${comp.replace(/\s/g,'_')}`;

    const btn = mk('button',{className:'accordion-btn',style:{borderColor:'#E2E8F0',color:col},
      onclick:()=>{
        const body=el(uid);
        const isOpen=body.classList.contains('open');
        // close all
        libCard.querySelectorAll('.accordion-body').forEach(b=>b.classList.remove('open'));
        libCard.querySelectorAll('.accordion-btn').forEach(b=>{
          b.classList.remove('open');
          b.style.background='white'; b.style.borderColor='#E2E8F0'; b.style.color=COMP_COLORS[b.dataset.comp]||'#4A5568';
          b.style.borderRadius='8px'; b.style.marginBottom='6px';
        });
        if(!isOpen){
          body.classList.add('open');
          btn.classList.add('open');
          btn.style.background=col; btn.style.borderColor=col; btn.style.color='white';
          btn.style.borderRadius='8px 8px 0 0'; btn.style.marginBottom='0';
        }
      }
    });
    btn.dataset.comp=comp;
    btn.appendChild(document.createTextNode(comp));
    btn.appendChild(mk('span',{style:{color:'inherit',fontSize:'11px'}},['▼']));
    libCard.appendChild(btn);

    const body = mk('div',{className:'accordion-body',id:uid,style:{borderColor:col,background:col+'08'}});
    items.forEach(ex=>{
      const item = mk('div',{className:'ex-item'});
      item.appendChild(mk('span',{className:'ex-dot',style:{background:col}}));
      item.appendChild(document.createTextNode(ex));
      body.appendChild(item);
    });
    libCard.appendChild(body);
  });
  container.appendChild(libCard);

  // Right: progression principles + pain guide
  const rightCard = mk('div',{className:'ex-card'});
  rightCard.appendChild(mk('div',{className:'prog-title'},['Strength Progression Principles']));

  const progs = [
    { label:'LENGTH',      from:'Short / inner range', to:'Long outer range',          phases:5 },
    { label:'CONTRACTION', from:'Isometric',           to:'Eccentric overload',         phases:4 },
    { label:'TEMPO',       from:'Slow (3–5:1:3–5)',    to:'Max intent',                 phases:4 },
    { label:'LOAD',        from:'Low (≤60% 1RM)',      to:'Supramaximal (>100% 1RM)',   phases:5 },
  ];

  progs.forEach(prog=>{
    const row = mk('div',{className:'prog-row'});
    const hdr = mk('div',{className:'prog-row-header'});
    hdr.appendChild(mk('span',{className:'prog-row-label',style:{color:p.color}},[prog.label]));
    hdr.appendChild(mk('span',{className:'prog-row-range'},[prog.from+' → '+prog.to]));
    row.appendChild(hdr);

    const trackWrap = mk('div',{className:'prog-track-wrap'});

    const fillPct = Math.min(Math.max((currentPhase/prog.phases)*100,0),100);
    const fill = mk('div',{className:'prog-fill',style:{
      width:fillPct+'%',
      background:`linear-gradient(90deg, ${PHASES[0].color}, ${p.color})`,
    }});
    trackWrap.appendChild(fill);

    PHASES.forEach((ph,i)=>{
      const marker = mk('div',{className:'prog-marker',style:{
        left:`${(i/(PHASES.length-1))*100}%`,
        width: i===currentPhase?'12px':'8px',
        height: i===currentPhase?'12px':'8px',
        background: i<=currentPhase?ph.color:'white',
        borderColor: ph.color,
      }});
      trackWrap.appendChild(marker);
    });
    row.appendChild(trackWrap);
    rightCard.appendChild(row);
  });

  // Programming note
  const note = mk('div',{className:'prog-note',style:{
    background:p.light, borderColor:p.color+'44',
  }});
  note.appendChild(mk('div',{className:'prog-note-label',style:{color:p.color}},
    [p.label.toUpperCase()+' — Programming Focus']));
  note.appendChild(mk('div',{className:'prog-note-text'},[PROG_NOTES[p.key]]));
  rightCard.appendChild(note);

  // Pain guide
  const painTitle = mk('div',{style:{fontFamily:"'DM Serif Display',serif",fontSize:'14px',color:'#1A202C',marginTop:'16px',marginBottom:'8px'}},
    ['Acceptable Pain Response']);
  rightCard.appendChild(painTitle);
  const painG = PAIN_GUIDE[p.key];
  const painGrid = mk('div',{className:'pain-grid'});
  [{label:'Isometric',val:painG.iso},{label:'Tri-phasic',val:painG.tri},{label:'Eccentric',val:painG.ecc}].forEach(item=>{
    const cell = mk('div',{className:'pain-cell'});
    cell.appendChild(mk('div',{className:'pain-cell-label'},[item.label]));
    const valEl = mk('div',{className:'pain-cell-val',style:{
      color:item.val==='0/10'?'#276749':p.color
    }},[item.val]);
    cell.appendChild(valEl);
    painGrid.appendChild(cell);
  });
  rightCard.appendChild(painGrid);
  container.appendChild(rightCard);
}

// ─── RENDER TOPBAR ───────────────────────────────────────────────────────────
function renderTopbar(){
  const p = PHASES[currentPhase];
  el('topbar').style.borderBottomColor=p.color;
  el('topbar-icon').style.background=p.color;
  const badge = el('phase-badge-top');
  badge.textContent=p.label.toUpperCase();
  badge.style.background=p.color+'22';
  badge.style.border=`1px solid ${p.color}44`;
  badge.style.color=p.color;
}

// ─── SWITCH TAB ──────────────────────────────────────────────────────────────
function switchTab(tab){
  currentTab=tab;
  ['week','milestones','exercises'].forEach(t=>{
    el('pane-'+t).style.display=t===tab?'block':'none';
    const btn = el('tab-'+t);
    btn.classList.toggle('active',t===tab);
    btn.style.background = t===tab?PHASES[currentPhase].color:'transparent';
    btn.style.color = t===tab?'white':'#718096';
    btn.style.fontWeight = t===tab?'700':'500';
  });
}

// ─── MAIN RENDER ─────────────────────────────────────────────────────────────
function render(){
  const p = PHASES[currentPhase];
  renderTopbar();
  renderPills();

  el('phase-heading').textContent=p.label;
  el('phase-sub').textContent=p.sub;
  el('phase-sub').style.color=p.color;

  updateProgress();
  switchTab(currentTab);

  renderFreq();
  renderDays();
  renderMilestones();
  renderExercises();

  // Update tab button backgrounds
  ['week','milestones','exercises'].forEach(t=>{
    const btn=el('tab-'+t);
    if(btn.classList.contains('active')) btn.style.background=p.color;
  });
}

// ─── INIT ────────────────────────────────────────────────────────────────────
render();
</script>
</body>
</html>
