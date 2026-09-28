<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>CC&R Reader — Plain-English HOA Document Review</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Source+Serif+4:opsz,wght@8..60,400;8..60,600;8..60,700&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@500&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#1c2230;
    --ink-soft:#3c4658;
    --paper:#f2efe6;
    --paper-raised:#fbfaf5;
    --line:#d8d3c2;
    --navy:#233b52;
    --navy-deep:#182838;
    --brass:#a9822f;
    --brass-soft:#efe3c2;
    --red:#9c3b31;
    --red-soft:#f5e2dd;
    --amber:#9c6f22;
    --amber-soft:#f6ecd3;
    --green:#3c6b4c;
    --green-soft:#e2ede4;
    --slate:#48586e;
    --slate-soft:#e6eaf0;
    --radius:3px;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--paper);
    color:var(--ink);
    font-family:'Inter',system-ui,sans-serif;
    font-size:15px;
    line-height:1.5;
  }
  h1,h2,h3,h4{font-family:'Source Serif 4',Georgia,serif;font-weight:600;margin:0 0 .4em;color:var(--ink);}
  a{color:var(--navy);}
  .mono{font-family:'IBM Plex Mono',monospace;}
  button{font-family:inherit;cursor:pointer;}
  ::selection{background:var(--brass-soft);}

  /* ---------- Setup screen ---------- */
  #setup{
    max-width:760px;
    margin:0 auto;
    padding:64px 24px 96px;
  }
  .masthead{
    border-bottom:3px double var(--ink);
    padding-bottom:18px;
    margin-bottom:36px;
  }
  .masthead .kicker{
    font-family:'IBM Plex Mono',monospace;
    font-size:11.5px;
    letter-spacing:.04em;
    color:var(--brass);
    margin-bottom:10px;
  }
  .masthead h1{font-size:32px;line-height:1.15;}
  .masthead p{color:var(--ink-soft);font-size:15.5px;max-width:56ch;}

  .card{
    background:var(--paper-raised);
    border:1px solid var(--line);
    border-radius:var(--radius);
    padding:24px 26px;
    margin-bottom:20px;
  }
  .card h3{font-size:17px;margin-bottom:6px;}
  .card .sub{color:var(--ink-soft);font-size:13.5px;margin-bottom:16px;}

  label{display:block;font-size:13px;font-weight:600;margin-bottom:6px;color:var(--ink-soft);}
  input[type=text],input[type=password],select,textarea{
    width:100%;
    border:1px solid var(--line);
    background:#fff;
    border-radius:var(--radius);
    padding:10px 12px;
    font-family:inherit;
    font-size:14.5px;
    color:var(--ink);
  }
  textarea{min-height:140px;resize:vertical;font-family:'IBM Plex Mono',monospace;font-size:13px;}
  input:focus,select:focus,textarea:focus{outline:2px solid var(--navy);outline-offset:1px;}
  .field{margin-bottom:16px;}
  .row{display:flex;gap:14px;}
  .row > *{flex:1;}
  .hint{font-size:12.5px;color:var(--ink-soft);margin-top:5px;}

  .dropzone{
    border:1.5px dashed var(--line);
    border-radius:var(--radius);
    padding:26px;
    text-align:center;
    color:var(--ink-soft);
    font-size:14px;
    background:#fff;
    transition:border-color .15s, background .15s;
  }
  .dropzone.drag{border-color:var(--navy);background:var(--slate-soft);}
  .dropzone strong{color:var(--navy);text-decoration:underline;cursor:pointer;}
  #fileName{margin-top:10px;font-size:13px;color:var(--green);font-weight:600;}

  .btn{
    display:inline-flex;align-items:center;gap:8px;
    background:var(--navy);color:#fdfcf8;
    border:none;border-radius:var(--radius);
    padding:11px 20px;font-size:14.5px;font-weight:600;
    box-shadow:0 1px 0 rgba(0,0,0,.15);
  }
  .btn:hover{background:var(--navy-deep);}
  .btn:disabled{background:#b7b2a0;cursor:not-allowed;}
  .btn.secondary{background:transparent;color:var(--navy);border:1px solid var(--navy);box-shadow:none;}
  .btn.secondary:hover{background:var(--slate-soft);}
  .btn.small{padding:7px 12px;font-size:13px;}

  .divider-or{display:flex;align-items:center;gap:12px;color:var(--ink-soft);font-size:12px;margin:18px 0;}
  .divider-or::before,.divider-or::after{content:"";flex:1;height:1px;background:var(--line);}

  .privacy-note{
    font-size:12.5px;color:var(--ink-soft);
    border-left:2px solid var(--brass);
    padding:8px 14px;background:var(--brass-soft);
    border-radius:0 var(--radius) var(--radius) 0;
  }

  #progressWrap{display:none;margin-top:8px;}
  #progressBar{height:6px;background:var(--line);border-radius:3px;overflow:hidden;}
  #progressFill{height:100%;width:0%;background:var(--navy);transition:width .3s;}
  #progressLabel{font-size:13px;color:var(--ink-soft);margin-top:8px;}
  #errorBox{display:none;margin-top:14px;padding:12px 14px;background:var(--red-soft);color:var(--red);border-radius:var(--radius);font-size:13.5px;}

  /* ---------- App shell ---------- */
  #app{display:none;height:100vh;}
  .shell{display:flex;height:100%;}
  .sidebar{
    width:270px;flex-shrink:0;
    background:var(--navy-deep);color:#e8e6dd;
    display:flex;flex-direction:column;
    padding:20px 0;
  }
  .sidebar-head{padding:0 20px 18px;border-bottom:1px solid rgba(255,255,255,.12);margin-bottom:10px;}
  .sidebar-head .kicker{font-family:'IBM Plex Mono',monospace;font-size:10.5px;letter-spacing:.05em;color:#c7a86b;margin-bottom:4px;}
  .sidebar-head h2{color:#fdfcf8;font-size:17px;margin:0;}
  .sidebar-stats{display:flex;gap:14px;padding:14px 20px;font-size:12px;color:#b9bcc6;}
  .sidebar-stats b{display:block;font-size:18px;font-family:'Source Serif 4',serif;color:#fdfcf8;}
  .navlist{flex:1;overflow-y:auto;padding:4px 10px;}
  .navitem{
    display:flex;justify-content:space-between;align-items:center;
    padding:9px 12px;border-radius:var(--radius);
    font-size:13.5px;color:#d4d6db;cursor:pointer;margin-bottom:2px;
  }
  .navitem:hover{background:rgba(255,255,255,.06);}
  .navitem.active{background:rgba(255,255,255,.12);color:#fff;font-weight:600;}
  .navitem .count{font-family:'IBM Plex Mono',monospace;font-size:11px;color:#9aa0ad;}
  .navitem.hasflag .count{color:#e2a89a;}
  .sidebar-foot{padding:14px 20px 4px;border-top:1px solid rgba(255,255,255,.12);margin-top:10px;}
  .sidebar-foot button{width:100%;margin-bottom:8px;}

  .main{flex:1;overflow-y:auto;background:var(--paper);}
  .topbar{
    position:sticky;top:0;z-index:5;
    background:var(--paper-raised);border-bottom:1px solid var(--line);
    padding:14px 32px;display:flex;justify-content:space-between;align-items:center;gap:16px;
  }
  .topbar h2{font-size:19px;margin:0;}
  .topbar .actions{display:flex;gap:8px;}
  .searchbox{position:relative;flex:1;max-width:340px;}
  .searchbox input{width:100%;padding:8px 12px;border:1px solid var(--line);border-radius:var(--radius);font-size:13.5px;}

  .content{padding:26px 32px 80px;max-width:900px;}

  .summary-block{background:var(--paper-raised);border:1px solid var(--line);border-radius:var(--radius);padding:22px 24px;margin-bottom:22px;}
  .summary-block h3{font-size:15px;color:var(--navy);text-transform:none;margin-bottom:8px;}
  .summary-block p{margin:0;color:var(--ink-soft);font-size:14.5px;}

  .finding{
    background:var(--paper-raised);
    border:1px solid var(--line);
    border-left:4px solid var(--slate);
    border-radius:0 var(--radius) var(--radius) 0;
    padding:16px 20px;margin-bottom:14px;
  }
  .finding.red_flag{border-left-color:var(--red);}
  .finding.caution{border-left-color:var(--amber);}
  .finding.info{border-left-color:var(--green);}
  .finding-head{display:flex;justify-content:space-between;align-items:baseline;gap:12px;margin-bottom:6px;}
  .finding-head h4{font-size:15.5px;margin:0;}
  .badge{
    font-family:'IBM Plex Mono',monospace;font-size:10.5px;letter-spacing:.03em;
    padding:2px 8px;border-radius:10px;white-space:nowrap;
  }
  .badge.red_flag{background:var(--red-soft);color:var(--red);}
  .badge.caution{background:var(--amber-soft);color:var(--amber);}
  .badge.info{background:var(--green-soft);color:var(--green);}
  .finding p.plain{margin:6px 0 10px;color:var(--ink);}
  .finding .cite{font-size:12px;color:var(--ink-soft);}
  .finding .cite button{background:none;border:none;color:var(--navy);text-decoration:underline;font-size:12px;padding:0;}
  .finding .excerpt{display:none;margin-top:8px;padding:10px 12px;background:#fbf8f0;border-radius:var(--radius);font-size:13px;font-style:italic;color:var(--ink-soft);border:1px solid var(--line);}

  table.rtable{width:100%;border-collapse:collapse;background:var(--paper-raised);border:1px solid var(--line);}
  table.rtable th,table.rtable td{text-align:left;padding:10px 12px;font-size:13.5px;border-bottom:1px solid var(--line);}
  table.rtable th{background:#eee9db;font-size:12px;text-transform:uppercase;letter-spacing:.03em;color:var(--ink-soft);}
  .resp-pill{font-size:11.5px;font-weight:600;padding:2px 9px;border-radius:10px;}
  .resp-owner{background:var(--slate-soft);color:var(--slate);}
  .resp-hoa{background:var(--navy);color:#fff;}
  .resp-shared{background:var(--brass-soft);color:var(--brass);}
  .resp-unclear{background:#eee;color:#888;}

  .hc-row{display:flex;gap:14px;align-items:flex-start;background:var(--paper-raised);border:1px solid var(--line);border-radius:var(--radius);padding:16px 18px;margin-bottom:12px;}
  .hc-status{flex-shrink:0;width:92px;text-align:center;font-size:11px;font-weight:700;padding:5px 0;border-radius:12px;font-family:'IBM Plex Mono',monospace;}
  .hc-status.present{background:var(--green-soft);color:var(--green);}
  .hc-status.missing{background:var(--red-soft);color:var(--red);}
  .hc-status.absent{background:var(--green-soft);color:var(--green);}
  .hc-status.unclear{background:var(--amber-soft);color:var(--amber);}
  .hc-body h4{font-size:14.5px;margin-bottom:3px;}
  .hc-body p{margin:0;font-size:13.5px;color:var(--ink-soft);}

  .glossary-item{display:flex;gap:16px;padding:11px 0;border-bottom:1px solid var(--line);}
  .glossary-term{width:220px;flex-shrink:0;font-weight:600;font-family:'Source Serif 4',serif;}
  .glossary-def{color:var(--ink-soft);font-size:14px;}

  .readgrade{display:flex;gap:28px;background:var(--paper-raised);border:1px solid var(--line);border-radius:var(--radius);padding:20px 24px;}
  .readgrade .num{font-family:'Source Serif 4',serif;font-size:38px;color:var(--navy);}
  .readgrade .lbl{font-size:12px;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.03em;margin-top:4px;}

  .empty{color:var(--ink-soft);font-size:14px;padding:30px 0;text-align:center;}

  /* Chat drawer */
  #chatToggle{
    position:fixed;bottom:26px;right:28px;z-index:20;
    background:var(--brass);color:#2a2210;border:none;border-radius:24px;
    padding:12px 20px;font-weight:700;font-size:13.5px;box-shadow:0 4px 14px rgba(0,0,0,.25);
  }
  #chatDrawer{
    position:fixed;top:0;right:-420px;width:400px;height:100%;
    background:var(--paper-raised);border-left:1px solid var(--line);
    z-index:30;transition:right .25s ease;display:flex;flex-direction:column;
    box-shadow:-6px 0 24px rgba(0,0,0,.12);
  }
  #chatDrawer.open{right:0;}
  .chat-head{padding:16px 18px;border-bottom:1px solid var(--line);display:flex;justify-content:space-between;align-items:center;}
  .chat-head h3{font-size:15.5px;margin:0;}
  .chat-head button{background:none;border:none;font-size:18px;color:var(--ink-soft);}
  .chat-log{flex:1;overflow-y:auto;padding:16px 18px;font-size:13.8px;}
  .chat-msg{margin-bottom:14px;}
  .chat-msg.user .bubble{background:var(--navy);color:#fff;margin-left:auto;}
  .chat-msg.assistant .bubble{background:#fff;border:1px solid var(--line);}
  .bubble{display:inline-block;padding:9px 13px;border-radius:10px;max-width:88%;white-space:pre-wrap;}
  .chat-msg.user{text-align:right;}
  .chat-input{padding:14px;border-top:1px solid var(--line);display:flex;gap:8px;}
  .chat-input textarea{min-height:44px;font-family:inherit;font-size:13.5px;}

  @media print{
    .sidebar,#chatToggle,#chatDrawer,.topbar .actions,.searchbox{display:none !important;}
    .main{overflow:visible;}
    .shell,#app{height:auto;display:block;}
    .content{max-width:100%;}
  }
</style>
</head>
<body>

<!-- ============ SETUP SCREEN ============ -->
<div id="setup">
  <div class="masthead">
    <div class="kicker">BROWSER-BASED · YOUR DOCUMENT STAYS ON YOUR DEVICE</div>
    <h1>CC&amp;R Reader</h1>
    <p>Upload your HOA's Covenants, Conditions &amp; Restrictions and get a plain-English breakdown: what you can and can't do, who's responsible for what, red flags, and a glossary — organized so you can actually find things.</p>
  </div>

  <div class="card">
    <h3>1. Your Google AI Studio API key (free)</h3>
    <div class="sub">This tool calls Google's Gemini API directly from your browser to read and translate the document. Your key and the extracted document text go directly from your browser to Google's API. The PDF itself is processed in your browser and is not uploaded to this website. Get a free key (no credit card) at <a href="https://aistudio.google.com/apikey" target="_blank">aistudio.google.com/apikey</a> — just sign in with a Google account and click "Create API key."</div>
    <div class="field">
      <label for="apiKey">API key</label>
      <input type="password" id="apiKey" placeholder="AIza...">
    </div>
    <div class="row">
      <div class="field">
        <label for="model">Model</label>
        <input type="text" id="model" value="gemini-3.1-flash-lite">
        <div class="hint">Default is Google's free-tier Flash model. You can try "gemini-3.1-flash-lite-pro" if you want higher quality, but it has a much lower free daily limit.</div>
      </div>
      <div class="field">
        <label><input type="checkbox" id="rememberKey" style="width:auto;display:inline;margin-right:6px;">Remember key on this device</label>
        <div class="hint">Stored only in this browser's local storage, never sent anywhere but Google.</div>
      </div>
    </div>
  </div>

  <div class="card">
    <h3>2. Your CC&amp;R document</h3>
    <div class="sub">Text-based PDFs are read directly; scanned PDFs are automatically processed with OCR. You can also paste text directly.</div>
    <div class="dropzone" id="dropzone">
      <div>Drop a PDF here, or <strong id="browseBtn">browse for a file</strong></div>
      <div id="fileName"></div>
      <input type="file" id="fileInput" accept=".pdf,.txt" style="display:none;">
    </div>
    <div class="divider-or">or paste the text instead</div>
    <textarea id="pasteText" placeholder="Paste the full CC&R text here..."></textarea>
  </div>

  <button class="btn" id="analyzeBtn">Analyze my CC&amp;R</button>
  <div id="progressWrap">
    <div id="progressBar"><div id="progressFill"></div></div>
    <div id="progressLabel"></div>
  </div>
  <div id="errorBox"></div>

  <p class="privacy-note" style="margin-top:22px;">Everything runs locally in this file — nothing is uploaded to a server of ours (we don't have one). Your document text and API key are sent only to Google's API to generate the analysis. Google's free tier may use this traffic to improve its models, so avoid pasting anything you consider sensitive if that matters to you. This tool gives general information for your own reference, not legal advice — for anything you plan to act on, it's worth a quick check against the actual document or a local attorney.</p>
</div>

<!-- ============ APP ============ -->
<div id="app">
  <div class="shell">
    <div class="sidebar">
      <div class="sidebar-head">
        <div class="kicker">CC&amp;R READER</div>
        <h2 id="docTitle">Your Community</h2>
      </div>
      <div class="sidebar-stats">
        <div><b id="statRed">0</b>Red flags</div>
        <div><b id="statTotal">0</b>Rules found</div>
        <div><b id="statGrade">–</b>Read level</div>
      </div>
      <div class="navlist" id="navlist"></div>
      <div class="sidebar-foot">
        <button class="btn secondary small" id="printBtn">Print / Save PDF</button>
        <button class="btn secondary small" id="exportBtn">Export as Markdown</button>
        <button class="btn secondary small" id="startOverBtn">Start over</button>
      </div>
    </div>
    <div class="main">
      <div class="topbar">
        <h2 id="viewTitle">Summary</h2>
        <div class="searchbox"><input type="text" id="searchInput" placeholder="Search everything found in the document..."></div>
      </div>
      <div class="content" id="content"></div>
    </div>
  </div>
</div>

<button id="chatToggle">Ask about your CC&amp;R</button>
<div id="chatDrawer">
  <div class="chat-head"><h3>Ask a question</h3><button id="chatClose">✕</button></div>
  <div class="chat-log" id="chatLog">
    <div class="chat-msg assistant"><div class="bubble">Ask me anything about your CC&R — e.g. "Can I put up a fence?" or "What happens if I don't pay my dues?" I'll answer based on the actual document text.</div></div>
  </div>
  <div class="chat-input">
    <textarea id="chatInput" placeholder="Type a question..."></textarea>
    <button class="btn small" id="chatSend">Ask</button>
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js"></script>
<script>
(function(){
"use strict";

pdfjsLib.GlobalWorkerOptions.workerSrc = "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";

const CATEGORIES = [
  "Use Restrictions (General)",
  "Rental & Leasing Rules",
  "Short-Term Rentals",
  "Pets & Animals",
  "Architectural Review & Exterior Changes",
  "Parking & Vehicles",
  "Landscaping & Yard Maintenance",
  "Noise & Nuisance",
  "Common Areas & Amenities",
  "Fines & Enforcement",
  "Assessments & Fees",
  "Liens & Foreclosure",
  "Insurance & Damage Responsibility",
  "Amendment Procedures",
  "Board Powers & Governance",
  "Other"
];

const state = {
  apiKey: "",
  model: "gemini-3.1-flash-lite",
  rawText: "",
  chunks: [],       // {text, index}
  findings: [],      // merged findings
  jargon: [],
  synthesis: null,
  readability: null
};

// Change this whenever analysis prompts or extraction logic changes so cached results are not reused incorrectly.
const ANALYSIS_VERSION = "2026-09-26-r3";

// ---------- small utils ----------
function $(id){ return document.getElementById(id); }
function esc(s){ return (s||"").replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
function download(filename, text){
  const blob = new Blob([text], {type:"text/markdown"});
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url; a.download = filename;
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
  URL.revokeObjectURL(url);
}
function stripFences(s){
  let t = s.trim();
  t = t.replace(/^```(json)?/i, "").replace(/```$/,"").trim();
  return t;
}
function safeParseJSON(s){
  try { return JSON.parse(stripFences(s)); }
  catch(e){
    // try to salvage: find first { and last }
    const t = stripFences(s);
    const start = t.indexOf("{"); const end = t.lastIndexOf("}");
    if(start >= 0 && end > start){
      try { return JSON.parse(t.slice(start, end+1)); } catch(e2){ return null; }
    }
    return null;
  }
}

// ---------- Gemini API ----------

async function callGemini(system, messages, maxTokens){

  const contents = messages.map(m => ({
    role: m.role === "assistant" ? "model" : "user",
    parts: [{ text: m.content }]
  }));

  const body = {
    system_instruction: { parts: [{ text: system }] },
    contents: contents,
    generationConfig: {
      maxOutputTokens: maxTokens || 2000
    }
  };

  const url =
    "https://generativelanguage.googleapis.com/v1beta/models/" +
    encodeURIComponent(state.model) +
    ":generateContent";

  const res = await fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "x-goog-api-key": state.apiKey
    },
    body: JSON.stringify(body)
  });

  if(!res.ok){
    const errText = await res.text();
    throw new Error(
      "API error " + res.status + ": " + errText.slice(0,300)
    );
  }

  const data = await res.json();

  const candidate = (data.candidates || [])[0];

  if(!candidate){
    const blockReason =
      data.promptFeedback && data.promptFeedback.blockReason;

    throw new Error(
      blockReason
        ? "Blocked by Google's safety filter: " + blockReason
        : "No response returned"
    );
  }

  const parts =
    (candidate.content && candidate.content.parts) || [];

  return parts.map(p => p.text || "").join("\n");
}

// ---------- PDF / text extraction ----------
async function extractPdfText(file){
  const buf = await file.arrayBuffer();
  const pdf = await pdfjsLib.getDocument({data: buf}).promise;

  let nativeText = "";
  let pagesWithText = 0;

  // Fast path: extract selectable PDF text first.
  for(let i=1; i<=pdf.numPages; i++){
    const page = await pdf.getPage(i);
    const content = await page.getTextContent();
    const pageText = content.items
      .map(item => item.str || "")
      .join(" ")
      .trim();

    if(pageText.length > 30) pagesWithText++;
    nativeText += "\n\n[Page " + i + "]\n" + pageText;
  }

  const nativeCharacters = nativeText.replace(/\s/g, "").length;
  const mostlyScanned =
    nativeCharacters < 500 ||
    pagesWithText < Math.max(1, Math.ceil(pdf.numPages * 0.25));

  if(!mostlyScanned){
    updateProgress(5, "Text-based PDF detected — preparing analysis...");
    return nativeText;
  }

  // Scanned PDF path: render each page with PDF.js, then OCR the canvas.
  updateProgress(5, "Scanned PDF detected — starting OCR...");

  if(typeof Tesseract === "undefined"){
    throw new Error(
      "OCR could not start because Tesseract.js did not load. Check your internet connection and reload the page."
    );
  }

  let worker = null;
  let ocrText = "";

  try{
    worker = await Tesseract.createWorker("eng");

    for(let i=1; i<=pdf.numPages; i++){
      const page = await pdf.getPage(i);
      const viewport = page.getViewport({scale: 2.2});
      const canvas = document.createElement("canvas");
      const context = canvas.getContext("2d", {willReadFrequently:true});

      canvas.width = Math.ceil(viewport.width);
      canvas.height = Math.ceil(viewport.height);

      updateProgress(
        5 + ((i - 1) / pdf.numPages) * 35,
        "OCR: page " + i + " of " + pdf.numPages + "..."
      );

      await page.render({
        canvasContext: context,
        viewport: viewport
      }).promise;

      const result = await worker.recognize(canvas);
      const pageText = result && result.data && result.data.text
        ? result.data.text.trim()
        : "";

      ocrText += "\n\n[Page " + i + "]\n" + pageText;

      canvas.width = 0;
      canvas.height = 0;
    }
  } finally {
    if(worker){
      try{ await worker.terminate(); }catch(e){}
    }
  }

  if(ocrText.replace(/\s/g, "").length < 200){
    throw new Error(
      "OCR finished, but very little text could be recognized. The scanned pages may be too low-resolution, heavily degraded, or handwritten."
    );
  }

  updateProgress(40, "OCR complete — preparing analysis...");
  return ocrText;
}

function chunkText(text, size, overlap){
  // Larger chunks reduce Gemini requests while keeping enough local context for extraction.
  size = size || 20000; overlap = overlap || 800;
  const chunks = [];
  let i = 0;
  while(i < text.length){
    const end = Math.min(i + size, text.length);
    chunks.push({ text: text.slice(i, end), index: chunks.length });
    if(end >= text.length) break;
    i = end - overlap;
  }
  return chunks;
}

// ---------- Readability (Flesch-Kincaid grade, approximate) ----------
function countSyllables(word){
  word = word.toLowerCase().replace(/[^a-z]/g,"");
  if(word.length <= 3) return 1;
  word = word.replace(/(?:[^laeiouy]es|ed|[^laeiouy]e)$/,"");
  word = word.replace(/^y/,"");
  const matches = word.match(/[aeiouy]{1,2}/g);
  return matches ? matches.length : 1;
}
function computeReadability(text){
  const clean = text.replace(/\[Page \d+\]/g,"");
  const sentences = clean.split(/[.!?]+/).filter(s => s.trim().length > 3);
  const words = clean.match(/[A-Za-z']+/g) || [];
  if(sentences.length === 0 || words.length === 0) return {grade: null, words: words.length, sentences: 0};
  const syllables = words.reduce((sum,w) => sum + countSyllables(w), 0);
  const grade = 0.39 * (words.length / sentences.length) + 11.8 * (syllables / words.length) - 15.59;
  return { grade: Math.max(1, Math.round(grade*10)/10), words: words.length, sentences: sentences.length };
}
function gradeLabel(grade){
  if(grade === null) return "n/a";
  if(grade <= 8) return "Plain (~8th grade)";
  if(grade <= 12) return "High school level";
  if(grade <= 16) return "College level";
  return "Graduate / legalese";
}

// ---------- Analysis prompts ----------
const CHUNK_SYSTEM = `You are conducting a comprehensive HOA CC&R due-diligence review for a homeowner or prospective homebuyer.

Your job is to identify EVERY substantive provision in THESE EXCERPTS that could affect ownership, occupancy, use, maintenance, modification, cost, rental, transfer, enforcement, or enjoyment of the property. Do not merely summarize unusual rules. Completeness is more important than producing a short list.

Analyze ONLY the provided excerpts. Do not use outside knowledge to fill gaps, and do not invent facts. When in doubt about whether a substantive provision matters, INCLUDE it rather than omit it. Preserve distinctions such as owner vs. HOA responsibility, mandatory vs. optional actions, approval vs. notice, and \"may\" vs. \"shall/must\". Avoid duplicate findings when overlapping excerpts contain the same provision.

Actively look for: property use and occupancy; prohibited activities; home businesses; guest or occupancy restrictions; exterior changes and structures; fences, gates, sheds, garages, carports, driveways, patios, pools and spas; architectural review and HOA approvals; landscaping, trees, gardens, irrigation, drainage, grading, easements and setbacks; pets and animals including breed, number, livestock, poultry, service/assistance animals and nuisance rules; parking and vehicles including RVs, boats, trailers, commercial and inoperable vehicles; rentals, leasing, minimum terms, rental caps, owner occupancy, tenant registration, short-term rentals and subleasing; owner and HOA maintenance, repair and replacement duties for roofs, siding, windows, doors, fences, landscaping, plumbing, water/sewer lines, drainage, electrical, HVAC, structures, common areas and exclusive-use areas; insurance and damage responsibilities; assessments, dues, special assessments, fees, late charges, interest, reimbursements, fines, attorney fees and collection costs; enforcement, notices, cure periods, hearings, fines, privilege suspension, HOA entry, self-help, liens and foreclosure; board and committee powers; owner voting, notice, hearing, inspection, document-access, accommodation and dispute-resolution rights; transfer and sale requirements; amendment and rule-change procedures; and any unusual provision that could materially affect a buyer's plans or ongoing ownership.

For every distinct finding:
- Translate it into plain English in 1-3 sentences and explain the practical homeowner impact.
- Assign exactly one category: ${CATEGORIES.join(" | ")}.
- Rate severity as \"red_flag\" for a significant restriction, financial exposure, major owner obligation, major use restriction, enforcement power, or provision likely to materially affect a homeowner/buyer; \"caution\" for a meaningful but moderate restriction, obligation, cost, approval requirement or enforcement provision; or \"info\" for routine or low-impact substantive information. Severity describes homeowner impact, not whether the rule is good or bad.
- If the provision assigns any maintenance, repair, replacement, insurance, payment, or other property responsibility, use \"owner\", \"hoa\", or \"shared\"; otherwise use null. Never infer responsibility from normal HOA practice.
- Give a citation using the article/section number when clearly labeled, otherwise the visible page marker, otherwise \"unlabeled\". Never invent a citation.
- Give a source_excerpt of no more than 20 words copied from the provided text.
- Include excerpt_index using the number of the excerpt where the finding was found.

Also collect important legal, HOA, property, or technical terms that a normal homeowner may not understand, with a concise plain-English definition. Do not list ordinary words merely because they appear in legal writing.

If an excerpt contains no substantive provision, return no finding for it. Do not combine separate rules merely because they concern the same subject when separate findings would make the homeowner-facing report clearer.

Respond with ONLY valid JSON, no markdown fences, matching exactly this shape:
{\"findings\":[{\"excerpt_index\":1,\"category\":\"\",\"title\":\"\",\"plain_english\":\"\",\"severity\":\"\",\"responsibility\":null,\"citation\":\"\",\"source_excerpt\":\"\"}],\"jargon_terms\":[{\"term\":\"\",\"plain_definition\":\"\"}]}`;

const SYNTH_SYSTEM = `You are preparing the homeowner-facing synthesis of a comprehensive HOA CC&R due-diligence review. You will receive a condensed list of findings extracted from the document. Use ONLY those findings. Do not invent facts, fill gaps with general HOA knowledge, or claim a provision is absent merely because it was not included in the findings. Use \"unclear\" when the findings do not establish an answer.

Produce a practical overview that identifies the documented community/property type when supported, the major things a homeowner can or cannot do, HOA approval requirements, ongoing owner obligations, HOA responsibilities, costs and assessments, rental restrictions, pet and vehicle restrictions, property/exterior restrictions, enforcement powers, financial or legal consequences, and unusual provisions that could matter to a buyer.

For quick_summary, provide 3-5 plain-English sentences based on documented findings. Do not make a vague overall judgment that the HOA is good, bad, fair, unfair, strict, or lenient; describe the actual documented characteristics instead.

For top_red_flags, select the 4-8 findings with the greatest potential practical impact, such as significant use restrictions, major exterior limitations, rental restrictions, financial exposure, substantial maintenance duties, broad enforcement powers, lien/foreclosure provisions, unusual approval requirements, or major insurance/damage responsibilities. Explain why each matters based on the finding.

For responsibility_matrix, include relevant items actually supported by the findings, such as roof, exterior paint/siding, fences, driveway/walkways, individual landscaping, common-area landscaping, pools/amenities, water/sewer lines, windows, doors, structural components, insurance, snow/ice removal, pest control, trash, and any other clearly mentioned obligation. Use owner, hoa, shared, or unclear.

For health_checks, use present when the findings establish the provision exists, absent when the findings explicitly establish that it does not exist, and unclear when the findings do not establish its status. Check reasonable accommodation/ADA language, breed-specific pet restrictions, fine authority including cap/notice/hearing process, dispute resolution such as mediation/arbitration, and special assessment/reserve-related provisions. Do not label something absent merely because it was not found.

Respond with ONLY valid JSON, no markdown fences, no commentary, matching exactly this shape:
{
 \"quick_summary\":\"\",
 \"top_red_flags\":[{\"title\":\"\",\"why_it_matters\":\"\"}],
 \"responsibility_matrix\":[{\"item\":\"\",\"responsible\":\"owner|hoa|shared|unclear\",\"notes\":\"\"}],
 \"health_checks\":[
  {\"check\":\"Reasonable accommodation / ADA language\",\"status\":\"present|absent|unclear\",\"explanation\":\"\"},
  {\"check\":\"Breed-specific pet restrictions\",\"status\":\"present|absent|unclear\",\"explanation\":\"\"},
  {\"check\":\"Fine authority has a clear cap, notice, and hearing process\",\"status\":\"present|absent|unclear\",\"explanation\":\"\"},
  {\"check\":\"Dispute resolution process (mediation/arbitration) before lawsuits\",\"status\":\"present|absent|unclear\",\"explanation\":\"\"},
  {\"check\":\"Special assessment authority vs. reserve funding risk\",\"status\":\"present|absent|unclear\",\"explanation\":\"\"}
 ]
}`;

const CHAT_SYSTEM = `You are helping a homeowner understand their own HOA CC&R document. Answer the question using ONLY the excerpts of the document provided below, plus the previously-extracted findings list if given. Be direct and plain-spoken — no legal jargon. If the excerpts don't clearly address the question, say so plainly rather than guessing, and suggest which section of the document they might check themselves. When you do find an answer, mention roughly where it comes from (section name or page number) if visible in the excerpt. This is general information, not legal advice.`;

// ---------- Analysis pipeline ----------
async function analyzeChunkBatch(chunks, attempt){
  attempt = attempt || 1;
  const prompt = chunks.map((c,i) =>
    "===== EXCERPT " + (i+1) + " =====\n" + c.text
  ).join("\n\n");
  try{
    const out = await callGemini(CHUNK_SYSTEM, [{role:"user", content: prompt}], 6000);
    const parsed = safeParseJSON(out);
    if(!parsed) throw new Error("could not parse JSON");
    return parsed;
  } catch(e){
    if(attempt < 2){ await new Promise(r=>setTimeout(r,3000)); return analyzeChunkBatch(chunks, attempt+1); }
    return {findings:[], jargon_terms:[], _error:e.message};
  }
}

function mergeJargon(list, incoming){
  const seen = new Map(list.map(j => [j.term.toLowerCase(), j]));
  incoming.forEach(j => {
    if(!j || !j.term) return;
    const key = j.term.toLowerCase();
    if(!seen.has(key)){ seen.set(key, j); list.push(j); }
  });
}

async function hashText(text){
  const data = new TextEncoder().encode(text);
  const hash = await crypto.subtle.digest("SHA-256", data);
  return Array.from(new Uint8Array(hash)).map(b=>b.toString(16).padStart(2,"0")).join("");
}

function saveAnalysisCache(){
  if(!state.documentHash) return;
  try{
    localStorage.setItem("ccr-analysis-" + state.documentHash, JSON.stringify({
      analysisVersion: ANALYSIS_VERSION,
      model: state.model, findings: state.findings, jargon: state.jargon,
      synthesis: state.synthesis, readability: state.readability, savedAt: Date.now()
    }));
  }catch(e){
    // If localStorage is full, the app still works normally.
  }
}

function loadAnalysisCache(){
  if(!state.documentHash) return false;
  try{
    const raw = localStorage.getItem("ccr-analysis-" + state.documentHash);
    if(!raw) return false;
    const cached = JSON.parse(raw);
    if(cached.analysisVersion !== ANALYSIS_VERSION || cached.model !== state.model || !Array.isArray(cached.findings) || !cached.synthesis) return false;
    state.findings = cached.findings;
    state.jargon = cached.jargon || [];
    state.synthesis = cached.synthesis;
    state.readability = cached.readability || computeReadability(state.rawText);
    return true;
  }catch(e){ return false; }
}

function normalizeForMatch(value){
  return String(value || "")
    .toLowerCase()
    .replace(/[^a-z0-9]+/g, " ")
    .trim();
}

function findingKey(f){
  const category = normalizeForMatch(f.category);
  const title = normalizeForMatch(f.title);
  const source = normalizeForMatch(f.source_excerpt);
  if(source) return category + "|" + title + "|" + source;
  return category + "|" + title + "|" + normalizeForMatch(f.plain_english);
}

function mergeFindings(list, incoming){
  const seen = new Set(list.map(findingKey));
  incoming.forEach(f => {
    if(!f || !f.plain_english) return;
    if(!CATEGORIES.includes(f.category)) f.category = "Other";
    const key = findingKey(f);
    if(seen.has(key)) return;
    seen.add(key);
    list.push(f);
  });
}

async function runAnalysis(){
  showProgress(true);
  setError("");
  try{
    state.documentHash = await hashText(state.rawText);

    // IMPORTANT: if this exact document was already analyzed with this model,
    // reuse the saved result instead of spending API quota again.
    if(loadAnalysisCache()){
      updateProgress(100, "Loaded saved analysis — no Gemini calls needed.");
      renderApp();
      document.getElementById("setup").style.display = "none";
      document.getElementById("app").style.display = "block";
      return;
    }

    state.chunks = chunkText(state.rawText, 20000, 800);
    const total = state.chunks.length;
    state.findings = [];
    state.jargon = [];
    let failedBatches = 0;

    // Analyze 5 chunks per Gemini request instead of one request per chunk.
    // A typical 50-page document therefore takes roughly 5-8 analysis calls,
    // plus one synthesis call, instead of dozens of calls.
    const BATCH_SIZE = 5;
    const totalBatches = Math.ceil(total / BATCH_SIZE);

    for(let b=0; b<totalBatches; b++){
      const batch = state.chunks.slice(b * BATCH_SIZE, (b+1) * BATCH_SIZE);
      updateProgress((b/totalBatches)*80, "Reading section group " + (b+1) + " of " + totalBatches + "...");
      const result = await analyzeChunkBatch(batch);
      if(result._error) failedBatches++;
      mergeFindings(state.findings, result.findings || []);
      mergeJargon(state.jargon, result.jargon_terms || []);

      // Short pause helps with per-minute throttling without pretending it
      // removes the daily quota.
      if(b < totalBatches-1) await new Promise(r=>setTimeout(r,1500));
    }

    updateProgress(85, "Computing readability...");
    state.readability = computeReadability(state.rawText);

    updateProgress(90, "Synthesizing summary, red flags, and responsibility matrix...");
    await runSynthesis();
    saveAnalysisCache();

    updateProgress(100, "Done.");
    if(failedBatches > 0){
      setError(failedBatches + " section group(s) could not be analyzed after retrying. The rest of the report is complete.");
    }
    renderApp();
    document.getElementById("setup").style.display = "none";
    document.getElementById("app").style.display = "block";
  } catch(e){
    setError("Analysis failed: " + e.message);
  } finally {
    showProgress(false);
  }
}

async function runSynthesis(){
  const condensed = state.findings.map(f => ({
    category: f.category, title: f.title, severity: f.severity,
    summary: f.plain_english, citation: f.citation
  }));
  const out = await callGemini(SYNTH_SYSTEM, [{role:"user", content: JSON.stringify(condensed)}], 4000);
  const parsed = safeParseJSON(out);
  state.synthesis = parsed || {quick_summary:"", top_red_flags:[], responsibility_matrix:[], health_checks:[]};
}

// ---------- UI: setup screen wiring ----------
function showProgress(on){ $("progressWrap").style.display = on ? "block" : "none"; }
function updateProgress(pct, label){ $("progressFill").style.width = pct + "%"; $("progressLabel").textContent = label; }
function setError(msg){ const box = $("errorBox"); box.textContent = msg; box.style.display = msg ? "block" : "none"; }

$("browseBtn").addEventListener("click", () => $("fileInput").click());
$("dropzone").addEventListener("click", (e) => { if(e.target.id !== "browseBtn") $("fileInput").click(); });
$("dropzone").addEventListener("dragover", (e) => { e.preventDefault(); $("dropzone").classList.add("drag"); });
$("dropzone").addEventListener("dragleave", () => $("dropzone").classList.remove("drag"));
$("dropzone").addEventListener("drop", (e) => {
  e.preventDefault(); $("dropzone").classList.remove("drag");
  if(e.dataTransfer.files.length) handleFile(e.dataTransfer.files[0]);
});
$("fileInput").addEventListener("change", (e) => { if(e.target.files.length) handleFile(e.target.files[0]); });

let uploadedFile = null;
function handleFile(file){
  uploadedFile = file;
  $("fileName").textContent = "Selected: " + file.name + " (" + Math.round(file.size/1024) + " KB)";
}

(function loadSavedKey(){
  const saved = localStorage.getItem("ccr_api_key");
  if(saved){ $("apiKey").value = saved; $("rememberKey").checked = true; }
})();

$("analyzeBtn").addEventListener("click", async () => {
  setError("");
  const key = $("apiKey").value.trim();
  const model = $("model").value.trim() || "gemini-3.1-flash-lite";
  if(!key){ setError("Enter your Google AI Studio API key first — get a free one at aistudio.google.com/apikey."); return; }
  state.apiKey = key; state.model = model;
  if($("rememberKey").checked) localStorage.setItem("ccr_api_key", key);
  else localStorage.removeItem("ccr_api_key");

  const pasted = $("pasteText").value.trim();
  if(!uploadedFile && !pasted){ setError("Upload a PDF or paste the CC&R text first."); return; }

  $("analyzeBtn").disabled = true;
  try{
    showProgress(true);

    if(uploadedFile){
      updateProgress(2, uploadedFile.name.toLowerCase().endsWith(".pdf")
        ? "Reading PDF..."
        : "Reading text file...");

      if(uploadedFile.name.toLowerCase().endsWith(".pdf")){
        state.rawText = await extractPdfText(uploadedFile);
      } else {
        state.rawText = await uploadedFile.text();
      }
    } else {
      state.rawText = pasted;
    }

    if(state.rawText.replace(/\s/g, "").length < 200){
      setError("The document could not be read well enough to analyze. If this is a scanned PDF, make sure the pages are clear enough for OCR to recognize the printed text.");
      showProgress(false);
      return;
    }

    await runAnalysis();
  } catch(e){
    setError("Couldn't read the document: " + e.message);
  } finally {
    $("analyzeBtn").disabled = false;
  }
});

$("startOverBtn").addEventListener("click", () => {
  if(!confirm("Start over? This clears the current analysis (your API key stays saved if you checked 'remember').")) return;
  document.getElementById("app").style.display = "none";
  document.getElementById("setup").style.display = "block";
  state.rawText = ""; state.findings = []; state.jargon = []; state.synthesis = null;
  uploadedFile = null; $("fileName").textContent = ""; $("pasteText").value = "";
});

// ---------- App rendering ----------
let currentView = "summary";
let searchTerm = "";

const RESTRICTION_CATEGORIES = [
  "Use Restrictions (General)",
  "Rental & Leasing Rules",
  "Short-Term Rentals",
  "Pets & Animals",
  "Architectural Review & Exterior Changes",
  "Parking & Vehicles",
  "Landscaping & Yard Maintenance",
  "Noise & Nuisance"
];

function countsByCategory(){
  const counts = {};
  CATEGORIES.forEach(c => counts[c] = {total:0, red:0});
  state.findings.forEach(f => {
    if(!counts[f.category]) counts[f.category] = {total:0, red:0};
    counts[f.category].total++;
    if(f.severity === "red_flag") counts[f.category].red++;
  });
  return counts;
}

function renderApp(){
  const redCount = state.findings.filter(f => f.severity === "red_flag").length;
  $("statRed").textContent = redCount;
  $("statTotal").textContent = state.findings.length;
  $("statGrade").textContent = state.readability && state.readability.grade ? state.readability.grade : "–";

  const counts = countsByCategory();
  const nav = [
    ["summary", "Summary"],
    ["candocant", "Can / Can't Do"],
    ["responsibility", "Who's Responsible"],
    ["healthcheck", "Health Check"],
  ].concat(CATEGORIES.map(c => [c, c])).concat([["glossary","Glossary"]]);

  $("navlist").innerHTML = nav.map(([key,label]) => {
    let count = "";
    let flagClass = "";
    if(CATEGORIES.includes(key)){
      const c = counts[key];
      if(c && c.total){ count = '<span class="count">'+c.total+'</span>'; if(c.red) flagClass=" hasflag"; }
      else return "";
    }
    return '<div class="navitem'+flagClass+(key===currentView?" active":"")+'" data-view="'+esc(key)+'">'+esc(label)+count+'</div>';
  }).join("");

  document.querySelectorAll(".navitem").forEach(el => {
    el.addEventListener("click", () => { currentView = el.getAttribute("data-view"); renderApp(); });
  });

  $("viewTitle").textContent = CATEGORIES.includes(currentView) ? currentView :
    {summary:"Summary", candocant:"What You Can / Can't Do", responsibility:"Who's Responsible: You vs. the HOA", healthcheck:"Document Health Check", glossary:"Glossary — Legal Terms in Plain English"}[currentView];

  renderContent();
}

function matchesSearch(f){
  if(!searchTerm) return true;
  const s = searchTerm.toLowerCase();
  return (f.title+" "+f.plain_english+" "+f.category).toLowerCase().includes(s);
}

function findingCard(f){
  const sev = f.severity && ["red_flag","caution","info"].includes(f.severity) ? f.severity : "info";
  const sevLabel = {red_flag:"Red Flag", caution:"Caution", info:"Info"}[sev];
  const id = "exc_" + Math.random().toString(36).slice(2,9);
  return '<div class="finding '+sev+'">'
    + '<div class="finding-head"><h4>'+esc(f.title)+'</h4><span class="badge '+sev+'">'+sevLabel+'</span></div>'
    + '<p class="plain">'+esc(f.plain_english)+'</p>'
    + '<div class="cite">'+esc(f.citation||"unlabeled")
    + (f.source_excerpt ? ' &middot; <button onclick="document.getElementById(\''+id+'\').style.display = document.getElementById(\''+id+'\').style.display===\'block\'?\'none\':\'block\'">show original text</button>' : '')
    + '</div>'
    + (f.source_excerpt ? '<div class="excerpt" id="'+id+'">"'+esc(f.source_excerpt)+'"</div>' : '')
    + '</div>';
}

function renderContent(){
  const c = $("content");
  const view = currentView;

  if(view === "summary"){
    const s = state.synthesis || {};
    let html = '<div class="summary-block"><h3>Overview</h3><p>'+esc(s.quick_summary||"No summary available.")+'</p></div>';
    html += '<div class="readgrade"><div><div class="num">'+(state.readability && state.readability.grade!==null ? state.readability.grade : "–")+'</div><div class="lbl">'+esc(state.readability?gradeLabel(state.readability.grade):"")+'</div></div>'
      + '<div><div class="num">'+state.findings.length+'</div><div class="lbl">Rules &amp; clauses found</div></div>'
      + '<div><div class="num">'+state.findings.filter(f=>f.severity==="red_flag").length+'</div><div class="lbl">Red flags</div></div></div>';
    html += '<h3 style="margin-top:26px;">Top Red Flags</h3>';
    if(s.top_red_flags && s.top_red_flags.length){
      html += s.top_red_flags.map(r => '<div class="finding red_flag"><div class="finding-head"><h4>'+esc(r.title)+'</h4><span class="badge red_flag">Red Flag</span></div><p class="plain">'+esc(r.why_it_matters)+'</p></div>').join("");
    } else {
      html += '<div class="empty">No major red flags identified.</div>';
    }
    c.innerHTML = html;
    return;
  }

  if(view === "candocant"){
    const relevant = state.findings.filter(f => RESTRICTION_CATEGORIES.includes(f.category) && matchesSearch(f));
    relevant.sort((a,b) => (b.severity==="red_flag") - (a.severity==="red_flag"));
    c.innerHTML = relevant.length ? relevant.map(findingCard).join("") : '<div class="empty">Nothing found for this view yet.</div>';
    return;
  }

  if(view === "responsibility"){
    const rows = (state.synthesis && state.synthesis.responsibility_matrix) || [];
    if(!rows.length){ c.innerHTML = '<div class="empty">No responsibility matrix could be generated from this document.</div>'; return; }
    const pill = r => '<span class="resp-pill resp-'+(["owner","hoa","shared"].includes(r)?r:"unclear")+'">'+esc((r||"unclear"))+'</span>';
    c.innerHTML = '<table class="rtable"><thead><tr><th>Item</th><th>Responsible</th><th>Notes</th></tr></thead><tbody>'
      + rows.filter(r => matchesSearch({title:r.item, plain_english:r.notes, category:""})).map(r => '<tr><td>'+esc(r.item)+'</td><td>'+pill(r.responsible)+'</td><td>'+esc(r.notes||"")+'</td></tr>').join("")
      + '</tbody></table>';
    return;
  }

  if(view === "healthcheck"){
    const checks = (state.synthesis && state.synthesis.health_checks) || [];
    if(!checks.length){ c.innerHTML = '<div class="empty">No health check results available.</div>'; return; }
    c.innerHTML = checks.map(h => '<div class="hc-row"><div class="hc-status '+esc(h.status)+'">'+esc((h.status||"unclear").toUpperCase())+'</div><div class="hc-body"><h4>'+esc(h.check)+'</h4><p>'+esc(h.explanation)+'</p></div></div>').join("");
    return;
  }

  if(view === "glossary"){
    const terms = state.jargon.slice().sort((a,b) => a.term.localeCompare(b.term)).filter(t => !searchTerm || (t.term+" "+t.plain_definition).toLowerCase().includes(searchTerm.toLowerCase()));
    c.innerHTML = terms.length ? terms.map(t => '<div class="glossary-item"><div class="glossary-term">'+esc(t.term)+'</div><div class="glossary-def">'+esc(t.plain_definition)+'</div></div>').join("") : '<div class="empty">No jargon terms flagged.</div>';
    return;
  }

  // category view
  const items = state.findings.filter(f => f.category === view && matchesSearch(f));
  items.sort((a,b) => (b.severity==="red_flag") - (a.severity==="red_flag"));
  c.innerHTML = items.length ? items.map(findingCard).join("") : '<div class="empty">Nothing found in this category.</div>';
}

$("searchInput").addEventListener("input", (e) => { searchTerm = e.target.value; renderContent(); });
$("printBtn").addEventListener("click", () => window.print());

$("exportBtn").addEventListener("click", () => {
  const s = state.synthesis || {};
  let md = "# CC&R Plain-English Report\n\n## Summary\n\n" + (s.quick_summary||"") + "\n\n";
  md += "**Rules found:** " + state.findings.length + " · **Red flags:** " + state.findings.filter(f=>f.severity==="red_flag").length;
  md += " · **Readability:** grade " + (state.readability?state.readability.grade:"n/a") + "\n\n";
  md += "## Top Red Flags\n\n";
  (s.top_red_flags||[]).forEach(r => { md += "- **" + r.title + "** — " + r.why_it_matters + "\n"; });
  md += "\n## Who's Responsible\n\n| Item | Responsible | Notes |\n|---|---|---|\n";
  (s.responsibility_matrix||[]).forEach(r => { md += "| " + r.item + " | " + r.responsible + " | " + (r.notes||"") + " |\n"; });
  md += "\n## Document Health Check\n\n";
  (s.health_checks||[]).forEach(h => { md += "- **" + h.check + "**: " + h.status + " — " + h.explanation + "\n"; });
  CATEGORIES.forEach(cat => {
    const items = state.findings.filter(f => f.category === cat);
    if(!items.length) return;
    md += "\n## " + cat + "\n\n";
    items.forEach(f => {
      md += "**" + f.title + "** _(" + f.severity + ")_ — " + f.plain_english + "  \n_Source: " + (f.citation||"unlabeled") + "_\n\n";
    });
  });
  md += "\n## Glossary\n\n";
  state.jargon.forEach(t => { md += "- **" + t.term + "**: " + t.plain_definition + "\n"; });
  download("ccr-report.md", md);
});

// ---------- Chat ----------
$("chatToggle").addEventListener("click", () => $("chatDrawer").classList.add("open"));
$("chatClose").addEventListener("click", () => $("chatDrawer").classList.remove("open"));

function tokenizeQuery(q){
  const stop = new Set(["the","and","for","are","can","you","your","what","how","does","this","that","with","have","from","into","about","when"]);
  return q.toLowerCase().match(/[a-z']+/g)?.filter(w => w.length > 2 && !stop.has(w)) || [];
}
function topRelevantChunks(query, n){
  const terms = tokenizeQuery(query);
  const scored = state.chunks.map(ch => {
    const lower = ch.text.toLowerCase();
    const score = terms.reduce((s,t) => s + (lower.split(t).length - 1), 0);
    return {ch, score};
  });
  scored.sort((a,b) => b.score - a.score);
  return scored.slice(0, n).filter(s => s.score > 0).map(s => s.ch);
}

async function sendChat(){
  const input = $("chatInput");
  const q = input.value.trim();
  if(!q || !state.apiKey) return;
  input.value = "";
  appendChat("user", q);
  appendChat("assistant", "Thinking...", true);

  const relevant = topRelevantChunks(q, 2);
  const context = relevant.length
    ? relevant.map((c,i) => "Excerpt " + (i+1) + ":\n" + c.text.slice(0,14000)).join("\n\n---\n\n")
    : state.chunks.slice(0,2).map((c,i) => "Excerpt " + (i+1) + ":\n" + c.text.slice(0,14000)).join("\n\n---\n\n");

  try{
    const answer = await callGemini(CHAT_SYSTEM,
      [{role:"user", content: "Document excerpts:\n\n" + context + "\n\nQuestion: " + q}], 1200);
    replaceLastAssistant(answer);
  } catch(e){
    replaceLastAssistant("Something went wrong asking that: " + e.message);
  }
}
function appendChat(role, text, placeholder){
  const log = $("chatLog");
  const div = document.createElement("div");
  div.className = "chat-msg " + role;
  div.innerHTML = '<div class="bubble">'+esc(text)+'</div>';
  if(placeholder) div.dataset.placeholder = "1";
  log.appendChild(div);
  log.scrollTop = log.scrollHeight;
}
function replaceLastAssistant(text){
  const log = $("chatLog");
  const nodes = log.querySelectorAll(".chat-msg.assistant");
  const last = nodes[nodes.length-1];
  if(last) last.querySelector(".bubble").textContent = text;
  log.scrollTop = log.scrollHeight;
}
$("chatSend").addEventListener("click", sendChat);
$("chatInput").addEventListener("keydown", (e) => { if(e.key==="Enter" && !e.shiftKey){ e.preventDefault(); sendChat(); } });

})();
</script>
</body>
</html>
