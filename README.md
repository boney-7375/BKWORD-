```html
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>MS Word + कृतिदेव स्टूडियो (PC Edition)</title>
<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
<style>
  :root {
    --word-blue: #185abd;
    --word-blue-dark: #103f91;
    --word-ribbon: #f3f2f1;
    --word-bg: #e1dfdd;
    --card: #ffffff;
    --tx: #201f1e;
    --mu: #605e5c;
    --bd: #d2d0ce;
    --ac: #c2410c;
    --acx: #ffffff;
    --page-bg: #ffffff;
    --page-tx: #111111;
  }

  :root[data-theme="dark"] {
    --word-blue: #0f408f;
    --word-blue-dark: #092c66;
    --word-ribbon: #252423;
    --word-bg: #161514;
    --card: #2d2c2b;
    --tx: #f3f2f1;
    --mu: #a19f9d;
    --bd: #3b3a39;
    --ac: #fb923c;
    --acx: #1a1308;
    color-scheme: dark;
  }

  * {
    box-sizing: border-box;
    user-select: none;
  }

  body {
    margin: 0;
    background: var(--word-bg);
    color: var(--tx);
    font-family: "Segoe UI", system-ui, -apple-system, Roboto, "Noto Sans Devanagari", sans-serif;
    height: 100vh;
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  /* Ribbon Styling */
  .ribbon-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 5px;
    padding: 5px 8px;
    min-height: 30px;
    border-radius: 5px;
    border: 1px solid transparent;
    background: transparent;
    color: var(--tx);
    font-size: 0.82rem;
    cursor: pointer;
    transition: all 0.12s ease;
  }
  .ribbon-btn:hover {
    background: rgba(128, 128, 128, 0.14);
    border-color: var(--bd);
  }
  .ribbon-btn:active, .ribbon-btn.active {
    background: rgba(24, 90, 189, 0.16);
    border-color: #185abd;
  }
  .ribbon-btn-lg {
    flex-direction: column;
    padding: 6px 10px;
    min-height: 54px;
    font-size: 0.75rem;
    gap: 4px;
  }
  .ribbon-btn-lg i {
    font-size: 1.15rem;
  }

  .ribbon-group {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 4px 10px 2px;
    border-right: 1px solid var(--bd);
    min-height: 76px;
  }
  .ribbon-group-content {
    display: flex;
    align-items: center;
    gap: 4px;
    flex-wrap: wrap;
    flex: 1;
  }
  .ribbon-group-label {
    text-align: center;
    font-size: 0.68rem;
    color: var(--mu);
    margin-top: 2px;
    letter-spacing: 0.02em;
  }

  select.ribbon-select, input.ribbon-input {
    font: inherit;
    font-size: 0.82rem;
    padding: 4px 8px;
    height: 30px;
    border-radius: 5px;
    border: 1px solid var(--bd);
    background: var(--card);
    color: var(--tx);
    outline: none;
  }
  select.ribbon-select:focus, input.ribbon-input:focus {
    border-color: #185abd;
  }

  /* Pinned Kruti Dev Quick Bar */
  .kd-bar {
    background: var(--card);
    border-bottom: 1px solid var(--bd);
    padding: 6px 12px;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    align-items: center;
    z-index: 10;
  }
  .kd-bar button, .kd-bar select {
    font: inherit;
    font-size: 0.84rem;
    padding: 4px 10px;
    min-height: 30px;
    border-radius: 6px;
    border: 1px solid var(--bd);
    background: var(--card);
    color: var(--tx);
    cursor: pointer;
  }
  .kd-bar button:hover {
    border-color: var(--ac);
  }
  .kd-bar button.p {
    background: var(--ac);
    color: var(--acx);
    border-color: var(--ac);
    font-weight: 600;
  }

  /* Workspace & Ruler */
  .workspace {
    flex: 1;
    overflow: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0 16px 60px;
    position: relative;
  }

  .ruler-wrap {
    position: sticky;
    top: 0;
    z-index: 4;
    width: 100%;
    display: flex;
    justify-content: center;
    background: var(--word-bg);
    padding: 6px 0 4px;
  }
  .ruler {
    width: 816px;
    height: 22px;
    background: var(--card);
    border: 1px solid var(--bd);
    border-radius: 3px;
    position: relative;
    overflow: hidden;
    display: flex;
    align-items: flex-end;
    font-size: 9px;
    color: var(--mu);
    box-shadow: 0 1px 3px rgba(0,0,0,0.06);
  }

  /* Document Page (A4 Default) */
  .page-shell {
    position: relative;
    width: 816px;
    min-height: 1056px;
    background: var(--page-bg);
    color: var(--page-tx);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.22);
    margin-top: 6px;
    transition: width 0.2s, min-height 0.2s, padding 0.2s;
    transform-origin: top center;
  }

  /* Page Borders */
  .page-shell.border-box::after {
    content: "";
    position: absolute;
    inset: 24px;
    border: 2px solid #222;
    pointer-events: none;
  }
  .page-shell.border-double::after {
    content: "";
    position: absolute;
    inset: 22px;
    border: 5px double #222;
    pointer-events: none;
  }
  .page-shell.border-dashed::after {
    content: "";
    position: absolute;
    inset: 24px;
    border: 2px dashed #444;
    pointer-events: none;
  }
  .page-shell.border-gold::after {
    content: "";
    position: absolute;
    inset: 20px;
    border: 4px ridge #b45309;
    pointer-events: none;
  }

  /* Watermark Overlay */
  .watermark-layer {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    pointer-events: none;
    overflow: hidden;
    z-index: 0;
  }
  .watermark-text {
    font-size: 4.5rem;
    font-weight: 800;
    color: rgba(0, 0, 0, 0.065);
    transform: rotate(-35deg);
    white-space: nowrap;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  /* Editable Content Area */
  #ed {
    position: relative;
    z-index: 1;
    width: 100%;
    min-height: 1056px;
    padding: 72px 72px;
    outline: none;
    font-size: 18px;
    line-height: 1.65;
    font-family: "Noto Sans Devanagari", Mangal, Calibri, sans-serif;
    overflow-wrap: anywhere;
    user-select: text;
    color: #111;
  }
  #ed:empty:before {
    content: attr(data-ph);
    color: #9ca3af;
    pointer-events: none;
  }
  #ed table {
    border-collapse: collapse;
    width: 100%;
    margin: 12px 0;
  }
  #ed td, #ed th {
    border: 1px solid #6b7280;
    padding: 8px 10px;
    min-width: 40px;
  }
  #ed blockquote {
    border-left: 4px solid #185abd;
    margin: 10px 0;
    padding: 6px 14px;
    background: rgba(24, 90, 189, 0.06);
    font-style: italic;
  }
  #ed hr.page-break {
    border: none;
    border-top: 2px dashed #9ca3af;
    margin: 28px -40px;
    position: relative;
  }
  #ed img {
    max-width: 100%;
    height: auto;
    border-radius: 4px;
    cursor: pointer;
  }

  /* Status Bar */
  .status-bar {
    background: var(--word-blue);
    color: #ffffff;
    height: 28px;
    padding: 0 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.76rem;
    z-index: 20;
  }

  /* Print Styles */
  @media print {
    body {
      background: #fff !important;
      height: auto !important;
      overflow: visible !important;
    }
    .no-print {
      display: none !important;
    }
    .workspace {
      padding: 0 !important;
      overflow: visible !important;
    }
    .page-shell {
      width: 100% !important;
      min-height: auto !important;
      box-shadow: none !important;
      margin: 0 !important;
      transform: none !important;
    }
    #ed hr.page-break {
      page-break-after: always;
      border: none;
    }
  }

  @media (max-width: 860px) {
    .page-shell {
      width: 100%;
      min-height: 78vh;
    }
    #ed {
      padding: 24px 18px !important;
      min-height: 78vh;
    }
    .ruler-wrap {
      display: none;
    }
  }
</style>
</head>
<body>

  <!-- TOP TITLE BAR (MS Word Style) -->
  <header class="no-print flex items-center justify-between px-3 py-1.5 text-white" style="background: var(--word-blue);">
    <div class="flex items-center gap-2.5">
      <div class="flex items-center gap-1.5 font-bold text-sm tracking-wide bg-white/15 px-2.5 py-1 rounded">
        <i class="fa-solid fa-file-word text-base"></i>
        <span>Word + कृतिदेव Studio</span>
      </div>
      <!-- Quick Access Icons -->
      <button id="qa-save" class="hover:bg-white/20 p-1.5 rounded text-xs" title="Save as MS Word (.doc) [Ctrl+S]">
        <i class="fa-solid fa-floppy-disk"></i>
      </button>
      <button data-c="undo" class="qa-cmd hover:bg-white/20 p-1.5 rounded text-xs" title="Undo (Ctrl+Z)">
        <i class="fa-solid fa-rotate-left"></i>
      </button>
      <button data-c="redo" class="qa-cmd hover:bg-white/20 p-1.5 rounded text-xs" title="Redo (Ctrl+Y)">
        <i class="fa-solid fa-rotate-right"></i>
      </button>
      <button id="qa-print" class="hover:bg-white/20 p-1.5 rounded text-xs" title="Print / Export PDF (Ctrl+P)">
        <i class="fa-solid fa-print"></i>
      </button>
      <span class="text-white/40">|</span>
      <input id="doc-title" type="text" value="मेरा_दस्तावेज़" class="bg-white/15 hover:bg-white/25 focus:bg-white focus:text-gray-900 text-white text-xs px-2.5 py-1 rounded outline-none w-40 sm:w-52 transition" title="Document File Name">
    </div>

    <div class="flex items-center gap-2">
      <button id="btn-find-open" class="bg-white/15 hover:bg-white/25 px-2.5 py-1 rounded text-xs flex items-center gap-1.5" title="Find & Replace (Ctrl+H)">
        <i class="fa-solid fa-magnifying-glass"></i> <span class="hidden sm:inline">खोजें / बदलें</span>
      </button>
      <button id="btn-pc-guide" class="bg-amber-500 hover:bg-amber-600 text-slate-950 font-semibold px-2.5 py-1 rounded text-xs flex items-center gap-1.5 shadow-sm" title="PC में सॉफ्टवेयर की तरह कैसे चलाएँ">
        <i class="fa-solid fa-desktop"></i> <span class="hidden md:inline">PC App कैसे बनाएँ</span>
      </button>
      <button id="btn-theme" class="bg-white/15 hover:bg-white/25 p-1.5 rounded text-xs" title="Dark / Light Mode">
        <i class="fa-solid fa-moon" id="theme-icon"></i>
      </button>
    </div>
  </header>

  <!-- RIBBON TAB HEADERS -->
  <nav class="no-print flex items-center gap-1 px-3 pt-1 border-b" style="background: var(--word-Blue); background-color: var(--word-ribbon); border-color: var(--bd);">
    <button data-tab="file" class="tab-btn px-3.5 py-1.5 text-xs font-semibold rounded-t-md bg-amber-600 text-white hover:bg-amber-700 transition">
      <i class="fa-solid fa-folder-open mr-1"></i> फ़ाइल (File)
    </button>
    <button data-tab="home" class="tab-btn active-tab px-3.5 py-1.5 text-xs font-semibold rounded-t-md border-b-2 border-blue-600 text-blue-600 bg-white/60 dark:bg-zinc-800">
      होम (Home)
    </button>
    <button data-tab="insert" class="tab-btn px-3.5 py-1.5 text-xs font-semibold rounded-t-md hover:bg-black/5">
      इन्सर्ट (Insert)
    </button>
    <button data-tab="layout" class="tab-btn px-3.5 py-1.5 text-xs font-semibold rounded-t-md hover:bg-black/5">
      पेज लेआउट (Page Layout)
    </button>
    <button data-tab="kruti" class="tab-btn px-3.5 py-1.5 text-xs font-semibold rounded-t-md hover:bg-black/5 text-orange-700 dark:text-orange-400">
      <i class="fa-solid fa-language mr-1"></i> कृतिदेव स्टूडियो
    </button>
    <div class="ml-auto flex items-center gap-2 pr-1">
      <button id="toggle-ribbon" class="text-xs px-2 py-1 rounded hover:bg-black/10" title="Show/Hide Ribbon">
        <i class="fa-solid fa-chevron-up" id="ribbon-chevron"></i>
      </button>
    </div>
  </nav>

  <!-- RIBBON PANELS CONTAINER -->
  <section id="ribbon-body" class="no-print border-b overflow-x-auto" style="background: var(--word-ribbon); border-color: var(--bd);">
    
    <!-- 1. FILE TAB PANEL -->
    <div id="panel-file" class="ribbon-panel hidden flex items-stretch px-2 py-1 min-w-max">
      <div class="ribbon-group">
        <div class="ribbon-group-content">
          <button id="file-new" class="ribbon-btn ribbon-btn-lg">
            <i class="fa-regular fa-file text-blue-600"></i>
            <span>नया (New)</span>
          </button>
          <button id="file-open-btn" class="ribbon-btn ribbon-btn-lg">
            <i class="fa-regular fa-folder-open text-amber-600"></i>
            <span>खोलें (Open)</span>
          </button>
          <input type="file" id="file-open-input" accept=".html,.htm,.txt,.doc" class="hidden">
        </div>
        <div class="ribbon-group-label">दस्तावेज़</div>
      </div>

      <div class="ribbon-group">
        <div class="ribbon-group-content">
          <button id="file-save-doc" class="ribbon-btn ribbon-btn-lg">
            <i class="fa-solid fa-file-word text-blue-700"></i>
            <span>Save .DOC (Word)</span>
          </button>
          <button id="file-save-html" class="ribbon-btn ribbon-btn-lg">
            <i class="fa-solid fa-code text-emerald-600"></i>
            <span>Save .HTML</span>
          </button>
          <button id="file-save-txt" class="ribbon-btn ribbon-btn-lg">
            <i class="fa-regular fa-file-lines text-slate-600"></i>
            <span>Save .TXT</span>
          </button>
        </div>
        <div class="ribbon-group-label">कंप्यूटर में सेव करें (Download)</div>
      </div>

      <div class="ribbon-group">
        <div class="ribbon-group-content">
          <button id="file-print" class="ribbon-btn ribbon-btn-lg">
            <i class="fa-solid fa-print text-purple-600"></i>
            <span>प्रिंट / Save PDF</span>
          </button>
        </div>
        <div class="ribbon-group-label">प्रिंट और PDF</div>
      </div>

      <div class="ribbon-group border-r-0">
        <div class="ribbon-group-content">
          <button id="file-template-letter" class="ribbon-btn">
            <i class="fa-solid fa-envelope-open-text text-orange-600"></i> सरकारी पत्र टेम्पलेट
          </button>
          <button id="file-template-app" class="ribbon-btn">
            <i class="fa-solid fa-file-signature text-teal-600"></i> प्रार्थना-पत्र (Application)
          </button>
        </div>
        <div class="ribbon-group-label">रेडीमेड हिंदी टेम्पलेट</div>
      </div>
    </div>

    <!-- 2. HOME TAB PANEL (Default Active) -->
    <div id="panel-home" class="ribbon-panel flex items-stretch px-2 py-1 min-w-max" id="tb">
      <!-- Clipboard -->
      <div class="ribbon-group">
        <div class="ribbon-group-content">
          <button id="btn-paste" class="ribbon-btn ribbon-btn-lg" title="Paste">
            <i class="fa-regular fa-paste text-amber-600"></i>
            <span>Paste</span>
          </button>
          <div class="flex flex-col gap-1">
            <button data-c="cut" class="ribbon-btn !py-0.5 !min-h-[24px]" title="Cut (Ctrl+X)">
              <i class="fa-solid fa-scissors text-xs"></i> Cut
            </button>
            <button data-c="copy" class="ribbon-btn !py-0.5 !min-h-[24px]" title="Copy (Ctrl+C)">
              <i class="fa-regular fa-copy text-xs"></i> Copy
            </button>
          </div>
        </div>
        <div class="ribbon-group-label">क्लिपबोर्ड</div>
      </div>

      <!-- Font Family & Size & Formatting -->
      <div class="ribbon-group">
        <div class="ribbon-group-content flex-col !items-start gap-1.5">
          <div class="flex items-center gap-1.5">
            <select id="ff" class="ribbon-select w-40" title="Font Family">
              <option value="Kruti Dev 010">Kruti Dev 010</option>
              <option value="Devlys 010">Devlys 010</option>
              <option value="Noto Sans Devanagari" selected>Noto Sans Devanagari</option>
              <option value="Mangal">Mangal (मंगल)</option>
              <option value="Arial">Arial</option>
              <option value="Calibri">Calibri</option>
              <option value="Times New Roman">Times New Roman</option>
              <option value="Courier New">Courier New</option>
              <option value="Georgia">Georgia</option>
              <option value="Verdana">Verdana</option>
            </select>

            <select id="fs" class="ribbon-select w-16" title="Font Size (px)">
              <option>10</option>
              <option>12</option>
              <option>14</option>
              <option>16</option>
              <option selected>18</option>
              <option>20</option>
              <option>22</option>
              <option>24</option>
              <option>28</option>
              <option>32</option>
              <option>36</option>
              <option>48</option>
              <option>64</option>
            </select>

            <button id="font-grow" class="ribbon-btn" title="Grow Font Size"><b>A</b><span class="text-[10px]">▲</span></button>
            <button id="font-shrink" class="ribbon-btn" title="Shrink Font Size"><b>A</b><span class="text-[10px]">▼</span></button>
            <button data-c="removeFormat" class="ribbon-btn" title="Clear Formatting">
              <i class="fa-solid fa-eraser text-rose-600"></i>
            </button>
          </div>

          <div class="flex items-center gap-1">
            <button data-c="bold" class="ribbon-btn w-8 font-bold" title="Bold (Ctrl+B)">B</button>
            <button data-c="italic" class="ribbon-btn w-8 italic font-serif" title="Italic (Ctrl+I)">I</button>
            <button data-c="underline" class="ribbon-btn w-8 underline" title="Underline (Ctrl+U)">U</button>
            <button data-c="strikeThrough" class="ribbon-btn w-8 line-through" title="Strikethrough">S</button>
            <button data-c="subscript" class="ribbon-btn w-8" title="Subscript">X<sub>2</sub></button>
            <button data-c="superscript" class="ribbon-btn w-8" title="Superscript">X<sup>2</sup></button>

            <span class="w-px h-5 bg-gray-300 dark:bg-zinc-600 mx-1"></span>

            <label class="ribbon-btn cursor-pointer gap-1" title="Text Color">
              <i class="fa-solid fa-font text-red-600"></i>
              <input type="color" id="fc" value="#000000" class="w-5 h-5 border-0 p-0 bg-transparent cursor-pointer">
            </label>
            <label class="ribbon-btn cursor-pointer gap-1" title="Highlight Color">
              <i class="fa-solid fa-highlighter text-yellow-500"></i>
              <input type="color" id="hc" value="#ffff00" class="w-5 h-5 border-0 p-0 bg-transparent cursor-pointer">
            </label>
          </div>
        </div>
        <div class="ribbon-group-label">फ़ॉन्ट (Font)</div>
      </div>

      <!-- Paragraph & Alignment -->
      <div class="ribbon-group">
        <div class="ribbon-group-content flex-col !items-start gap-1.5">
          <div class="flex items-center gap-1">
            <button data-c="insertUnorderedList" class="ribbon-btn" title="Bullet List">
              <i class="fa-solid fa-list-ul"></i>
            </button>
            <button data-c="insertOrderedList" class="ribbon-btn" title="Numbered List">
              <i class="fa-solid fa-list-ol"></i>
            </button>
            <button data-c="outdent" class="ribbon-btn" title="Decrease Indent">
              <i class="fa-solid fa-outdent"></i>
            </button>
            <button data-c="indent" class="ribbon-btn" title="Increase Indent">
              <i class="fa-solid fa-indent"></i>
            </button>
            <select id="line-spacing" class="ribbon-select ml-1" title="Line Spacing">
              <option value="1.2">↕ 1.0</option>
              <option value="1.45">↕ 1.15</option>
              <option value="1.65" selected>↕ 1.5</option>
              <option value="2.0">↕ 2.0</option>
              <option value="2.4">↕ 2.5</option>
            </select>
          </div>

          <div class="flex items-center gap-1">
            <button data-c="justifyLeft" class="ribbon-btn" title="Align Left (Ctrl+L)">
              <i class="fa-solid fa-align-left"></i>
            </button>
            <button data-c="justifyCenter" class="ribbon-btn" title="Align Center (Ctrl+E)">
              <i class="fa-sol
