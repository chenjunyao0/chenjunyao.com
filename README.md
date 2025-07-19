<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<script src="https://www.google.com/recaptcha/api.js?render=6Ld09HwrAAAAAAqcZ8qCHNZVEdAswqrleNze9oSF"></script>
<link rel="icon" href="nn.png" type="image/png">
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BMI 計算器</title>
  <style>
    :root {
      --bg: #fff0f5;
      --card-bg: #fff5e6;
      --accent: #70a1ff;
      --stroke: #3f3a3a;
      --radius: 32px;
      --font: 'Comic Neue', sans-serif;
      --under-bg: #ffe4e1;
      --normal-bg: #e0ffe0;
      --over-bg: #fff7e1;
      --obese-bg: #ffe0e0;
    }
    .dark-mode {
      --bg: #1e1e1e;
      --card-bg: #2a2a2a;
      --accent: #4a90e2;
      --stroke: #ddd;
    }
    *, *::before, *::after { box-sizing: border-box; }
    body {
      margin: 0;
      padding: 1rem;
      background: var(--bg);
      color: var(--stroke);
      font-family: var(--font);
      text-align: center;
    }
    h1 { margin-bottom: .5rem; }

    form {
      max-width: 450px;
      margin: 0 auto 2rem;
      padding: 2rem;
      background: var(--card-bg);
      border: 3px solid #000;
      border-radius: var(--radius);
      box-shadow: 6px 6px 0 var(--accent);
      text-align: left;
    }
    .form-group { margin: .8rem 0; }
    .form-group label { display: block; margin-bottom: .3rem; }
    .form-group input,
    .form-group select {
      width: 100%;
      padding: .5rem;
      border: 2px solid #000;
      border-radius: var(--radius);
      background: #fff;
      text-align: center;
      font-family: var(--font);
      outline: none;
    }
    button[type="submit"] {
      width: 100%;
      margin-top: 1rem;
      padding: .6rem;
      background: var(--accent);
      border: 2px solid #000;
      border-radius: var(--radius);
      color: #fff;
      font-size: 1.1rem;
      cursor: pointer;
      box-shadow: 4px 4px 0 var(--stroke);
      transition: transform .2s;
    }
    button[type="submit"]:hover {
      transform: rotate(-2deg) scale(1.05);
    }

    #overviewStats,
    #historyTable,
    #historyCards { display: none; }

    .history-visible #overviewStats {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 2rem;
    }

    .card {
      width: 140px;
      padding: 1rem;
      background: #fff;
      border: 4px solid var(--stroke);
      border-radius: var(--radius);
      box-shadow: 4px 4px 0 var(--accent);
      text-align: center;
    }
    .card h3 { margin: 0; font-size: 1.6rem; }
    .card p { margin: .3rem 0 0; font-size: .9rem; }

    @media (min-width:769px) {
      .history-visible #historyTable { display: block; }
      .history-visible #historyCards { display: none; }
    }

   @media (max-width:768px) {
     .history-visible #historyCards {display: block;}
     .history-visible #historyTable {display: none;}


  /* 粉红主色 */
  :root {
    --accent: #ff98c3;
  }

  /* 表单 6px 黑边 + 6px 粉红阴影 */
  form {
    border: 6px solid #000 !important;
    box-shadow: 6px 6px 0 var(--accent) !important;
  }

  /* 提交按钮 3px 黑边 + 3px 粉红阴影 */
  button[type="submit"] {
    background: var(--accent);
    border: 2.5px solid #000 !important;
    box-shadow: 3px 3px 0.25var(--accent) !important;
  }
}




    #historyTable {
      max-width: 900px;
      margin: 0 auto 2rem;
    }
    #historyTable table {
      width: 100%;
      border-collapse: collapse;
    }
    #historyTable th,
    #historyTable td {
      padding: 1rem;
      border: 3px solid var(--stroke);
      background: #fff;
      text-align: center;
      color: #000 !important;
    }
    #historyTable th {
      background: var(--accent);
      color: #fff !important;
    }

    #historyCards {
      max-width: 900px;
      margin: 0 auto 2rem;
    }
    .history-card {
      background: #fff;
      padding: 1.5rem;
      margin-bottom: 1rem;
      border: 4px solid var(--stroke);
      border-radius: var(--radius);
      box-shadow: 4px 4px 0 var(--accent);
      text-align: left;
      font-size: 1rem;
      color: #000 !important;
    }
    .history-card p { margin: .3rem 0; }

    .status-underweight td { background: var(--under-bg); }
    .status-normal td      { background: var(--normal-bg); }
    .status-overweight td  { background: var(--over-bg); }
    .status-obese td       { background: var(--obese-bg); }

    .history-card.status-underweight { border-color: #ff7f7f; }
    .history-card.status-normal      { border-color: #7fff7f; }
    .history-card.status-overweight  { border-color: #ffc27f; }
    .history-card.status-obese       { border-color: #ff4f4f; }

    #cookieBanner {
      position: fixed;
      bottom: 0; left: 0; right: 0;
      background: var(--stroke);
      color: #fff;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 9999;
    }
    #cookieBanner button {
      background: var(--accent);
      border: none;
      color: #fff;
      padding: .5rem 1rem;
      border-radius: var(--radius);
      cursor: pointer;
    }
    @media (max-width:768px) {
      #cookieBanner { flex-direction: column; text-align: center; }
      #cookieBanner > div { margin-top: .5rem; }
    }

    .dark-mode #overviewStats .card { color: #000 !important; }
  </style>
</head>
<body>
  <h1>BMI 計算器</h1>
  <div id="currentTime"></div>

  <form id="bmiForm" action="bmi.php" method="post" novalidate>
   <input type="hidden" name="recaptcha_token" id="recaptcha_token">
    <div class="form-group">
      <label for="nameInput">姓名</label>
      <input id="nameInput" required />
    </div>
    <div class="form-group">
      <label for="studentIdInput">學號</label>
      <input id="studentIdInput" required maxlength="4" />
    </div>
    <div class="form-group">
      <label for="genderInput">性別</label>
      <select id="genderInput" required>
        <option value="">請選擇</option>
        <option>男</option>
        <option>女</option>
        <option>不便透露</option>
      </select>
    </div>
 <!-- 身高 (cm) -->
<div class="form-group">
  <label for="heightInput">身高 (cm)</label>
  <input
    id="heightInput"
    type="number"
    min="100"
    max="250"
    step="0.1"
    lang="en"
    required
  />
</div>

<!-- 體重 (kg) -->
<div class="form-group">
  <label for="weightInput">體重 (kg)</label>
  <input
    id="weightInput"
    type="number"
    min="10"
    max="250"
    step="0.1"
    lang="en"
    required
  />
</div>


    <button type="submit">計算並提交</button>
  </form>

  <section id="overviewStats"></section>
  <div id="historyTable">
    <table>
      <thead>
        <tr>
          <th>時間</th><th>姓名</th><th>學號</th><th>性別</th>
          <th>身高</th><th>體重</th><th>BMI</th><th>狀態</th>
        </tr>
      </thead>
      <tbody></tbody>
    </table>
  </div>
  <div id="historyCards"></div>

  <div id="cookieBanner">
    <span>本網站使用 Cookie 顯示最近 7 天的歷史。是否同意永久保留？</span>
    <div>
      <button id="acceptCookies">同意</button>
      <button id="rejectCookies">拒絕</button>
    </div>
  </div>

  <script>
  (function(){
    const CONSENT_KEY = 'bmiConsent';
    const DATA_KEY    = 'bmiRecords';
    const SEVEN_DAYS  = 7 * 24 * 3600 * 1000;

    // 深色模式偵測
    const mq = window.matchMedia('(prefers-color-scheme: dark)');
    function applyTheme(d) { document.documentElement.classList.toggle('dark-mode', d); }
    applyTheme(mq.matches);
    mq.addEventListener('change', e => applyTheme(e.matches));

    // 讀寫紀錄
    let consent = localStorage.getItem(CONSENT_KEY) === 'accepted';
    function loadRecords(){
      const store = consent ? localStorage : sessionStorage;
      let arr = JSON.parse(store.getItem(DATA_KEY) || '[]');
      const now = Date.now();
      arr = arr.filter(r => now - new Date(r.time).getTime() <= SEVEN_DAYS);
      if (consent) localStorage.setItem(DATA_KEY, JSON.stringify(arr));
      return arr;
    }
    function saveRecords(arr){
      const store = consent ? localStorage : sessionStorage;
      store.setItem(DATA_KEY, JSON.stringify(arr));
    }
    window.addEventListener('beforeunload', ()=> {
      if (!consent) {
        sessionStorage.removeItem(DATA_KEY);
        localStorage.removeItem(DATA_KEY);
      }
    });

    document.addEventListener('DOMContentLoaded', ()=>{
      const nowEl = document.getElementById('currentTime');
      function tick(){ nowEl.textContent = new Date().toLocaleString(); }
      tick(); setInterval(tick, 1000);
      if (consent) document.getElementById('cookieBanner').style.display = 'none';
    });

    // Cookie Banner
    const banner = document.getElementById('cookieBanner');
    document.getElementById('acceptCookies').addEventListener('click', ()=>{
      consent = true;
      localStorage.setItem(CONSENT_KEY, 'accepted');
      const sess = JSON.parse(sessionStorage.getItem(DATA_KEY) || '[]');
      const pers = JSON.parse(localStorage.getItem(DATA_KEY)   || '[]');
      localStorage.setItem(DATA_KEY, JSON.stringify(pers.concat(sess)));
      sessionStorage.removeItem(DATA_KEY);
      banner.style.display = 'none';
    });
    document.getElementById('rejectCookies').addEventListener('click', ()=>{
      consent = false;
      localStorage.removeItem(CONSENT_KEY);
      sessionStorage.removeItem(DATA_KEY);
      banner.style.display = 'none';
    });

    // 元素選取
    const form   = document.getElementById('bmiForm');
    const nameI  = document.getElementById('nameInput');
    const idI    = document.getElementById('studentIdInput');  
    const genderI= document.getElementById('genderInput');
    const heightI= document.getElementById('heightInput');
    const weightI= document.getElementById('weightInput');

  nameI.addEventListener('input', () => {
  // 记录原来光标位置
  const start = nameI.selectionStart;
  const end   = nameI.selectionEnd;

  const original = nameI.value;
  // 过滤非法字符（保留空格）
  let filtered = original.replace(/[^A-Za-z\u4e00-\u9fa5 ]/g, '');
  if (original !== filtered) {
    alert('只允许输入中文、英文和空格');
  }
  // 首字母及每个空格后字符大写
  filtered = filtered.replace(/(^|\s)([a-z])/g, (m, p1, p2) => p1 + p2.toUpperCase());

  // 赋值并复位光标
  nameI.value = filtered;
  const diff = filtered.length - original.length;
  nameI.setSelectionRange(start + diff, end + diff);
});


   // 學號：只允許英文字母與數字，並自動轉大寫，並對非法字元彈窗提示
   idI.addEventListener('input', () => {
   const original = idI.value;
   // 過濾掉非 A–Z, a–z, 0–9 的字元
   const filtered = original.replace(/[^A-Za-z0-9]/g, '');
   if (original !== filtered) {
   alert('學號只能包含英文字母與數字！');
   }
   
   // 全部轉為大寫
   idI.value = filtered.toUpperCase();
   });

    // 數字檢驗
   // ------------------ 在此處插入 ------------------
// 只允許 最多 3 位整數 + 1 位小數
// 放在获取到 heightI、weightI 之后，任何 blur／submit 事件之前
const numPat = /^[0-9]{0,3}(?:\.[0-9])?$/;

function filterNum(inp, label) {
  if (inp.value && !numPat.test(inp.value)) {
    inp.value = inp.value.slice(0, -1);
    alert(label + ' 只能輸入最多 3 位整數及 1 位小數');
  }
}

heightI.addEventListener('input', () => filterNum(heightI, '身高'));
weightI.addEventListener('input', () => filterNum(weightI, '體重'));


    heightI.addEventListener('blur', ()=>{
      const v = parseFloat(heightI.value);
      if (!isNaN(v)) {
        if (v < 100) { alert('身高最小100cm'); heightI.value='100'; }
        if (v > 250) { alert('身高最大250cm'); heightI.value='250'; }
      }
    });
    weightI.addEventListener('blur', ()=>{
      const v = parseFloat(weightI.value);
      if (!isNaN(v)) {
        if (v < 10)  { alert('體重最小10kg');  weightI.value='10'; }
        if (v > 250) { alert('體重最大250kg'); weightI.value='250'; }
      }
    });

    // 計算並提交
    form.addEventListener('submit', e=>{
      e.preventDefault();
      if (!genderI.value) {
        alert('請選擇性別');
        return;
      }
      const h = parseFloat(heightI.value),
            w = parseFloat(weightI.value);
      if (isNaN(h) || h<100 || h>250) {
        alert('身高需 100~250cm');
        return;
      }
      if (isNaN(w) || w<10 || w>250) {
        alert('體重需 10~250kg');
        return;
      }
      const raw = w / ((h/100)**2),
            bmi = Math.min(raw, 30).toFixed(2),
            status = raw<18.5 ? '過輕'
                   : raw<24   ? '正常'
                   : raw<30   ? '過重'
                   : '嚴重肥胖';
      const rec = {
        time: new Date().toISOString(),
        name: nameI.value.trim(),
        studentId: idI.value.trim(),
        gender: genderI.value,
        height: h,
        weight: w,
        bmi, status
      };
      const arr = loadRecords();
      arr.push(rec);
      saveRecords(arr);
      refreshUI();
      form.reset();
    });

    // 更新 UI
    function refreshUI(){
      const arr = loadRecords();
      renderOverview(arr);
      renderHistory(arr);
      document.body.classList.add('history-visible');
    }
    function renderOverview(arr){
      const o = document.getElementById('overviewStats');
      o.innerHTML = '';
      const total = arr.length;
      const latest = total ? arr[total-1].bmi : '-';
      const avg3 = total>=3
                 ? (arr.slice(-3).reduce((s,r)=>s+parseFloat(r.bmi),0)/3).toFixed(2)
                 : '-';
      [['總筆數', total], ['最新 BMI', latest], ['近三筆平均', avg3]]
        .forEach(([label,val])=>{
          const d = document.createElement('div');
          d.className = 'card';
          d.innerHTML = `<h3>${val}</h3><p>${label}</p>`;
          o.appendChild(d);
        });
    }
    function renderHistory(arr){
      const tbody = document.querySelector('#historyTable tbody');
      const cards = document.getElementById('historyCards');
      tbody.innerHTML = cards.innerHTML = '';
      const map = {
        '過輕': {cls:'status-underweight', icon:'🐤'},
        '正常': {cls:'status-normal',    icon:'😊'},
        '過重': {cls:'status-overweight',icon:'😐'},
        '嚴重肥胖': {cls:'status-obese',     icon:'😡'}
      };
      arr.forEach(r=>{
        const info = map[r.status];
        const tr = document.createElement('tr');
        tr.className = info.cls;
        ['time','name','studentId','gender','height','weight']
          .forEach(k=>{
            const td = document.createElement('td');
            td.textContent = k==='time'
              ? new Date(r.time).toLocaleString()
              : (k==='studentId'? r.studentId||'未填': r[k]);
            tr.appendChild(td);
          });
        const tdB = document.createElement('td');
        tdB.textContent = r.bmi;
        tr.appendChild(tdB);
        const tdS = document.createElement('td');
        tdS.innerHTML = `${info.icon} ${r.status}`;
        tr.appendChild(tdS);
        tbody.appendChild(tr);

        const card = document.createElement('div');
        card.className = `history-card ${info.cls}`;
        card.innerHTML = `
          <p>時間：${new Date(r.time).toLocaleString()}</p>
          <p>姓名：${r.name}</p>
          <p>學號：${r.studentId||'未填'}</p>
          <p>性別：${r.gender}</p>
          <p>身高：${r.height} cm</p>
          <p>體重：${r.weight} kg</p>
          <p>${info.icon} ${r.status} (BMI：${r.bmi})</p>
        `;
        cards.appendChild(card);
      });
    }
  })();
     const form = document.getElementById('bmiForm');
    form.addEventListener('submit', function(evt) {
    evt.preventDefault();  // 暫停表單送出

    grecaptcha.ready(() => {
      grecaptcha.execute('6Ld09HwrAAAAAAqcZ8qCHNZVEdAswqrleNze9oSF', { action: 'submit' })
        .then(token => {
          // 將 token 塞到隱藏欄位
          document.getElementById('recaptchaToken').value = token;
          // 再次觸發表單送出
          form.submit();
        });
    });
  });
  </script>
</body>
</html>
