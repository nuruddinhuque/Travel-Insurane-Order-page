<!-- Save this as calculator.html -->
<!doctype html>
<html lang="bn">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>NextSure — Travel Insurance Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --dark-bg:#071226; --dark-card:rgba(255,255,255,0.03); --muted:#9fb0c8; --accent:#3b82f6; --success:#10b981; --danger:#ef4444; --warn:#f59e0b; --text:#e6eef6;
      --light-bg:#f4f7fb; --light-card:#ffffff; --muted-light:#000000; --text-light:#0b1220;
    }
    html[data-theme='dark']{ --page-bg:var(--dark-bg); --card-bg:var(--dark-card); --muted-c:var(--muted); --text-c:var(--text); --accent-c:var(--accent); }
    html[data-theme='light']{ --page-bg:var(--light-bg); --card-bg:var(--light-card); --muted-c:var(--muted-light); --text-c:var(--text-light); --accent-c:var(--accent); }

    *{box-sizing:border-box}
    body{font-family:Inter,system-ui,Arial;background:var(--page-bg);color:var(--text-c);margin:0;padding:22px}
    .app{max-width:1100px;margin:0 auto}
    .header{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:18px}
    .brand{display:flex;gap:12px;align-items:center}
    .logo{width:52px;height:52px;border-radius:12px;background:linear-gradient(135deg,var(--accent-c),#7c3aed);display:flex;align-items:center;justify-content:center;font-weight:700;color:#fff}
    h1{margin:0;font-size:18px}
    p.lead{margin:0;color:var(--muted-c);font-size:13px}
    .grid{display:grid;grid-template-columns:1fr 380px;gap:18px}
    .card{background:var(--card-bg);padding:16px;border-radius:12px;border:1px solid rgb(0, 0, 0);box-shadow:0 6px 24px #020617}
    label{display:block;color:var(--muted-c);font-size:13px;margin-top:10px}
    input, select, textarea{width:100%;padding:10px;border-radius:8px;border:1px solid #000000;background:transparent;color:var(--text-c);margin-top:6px}
    .row{display:flex;gap:10px}
    .col{flex:1}
    .btn{padding:10px 14px;border-radius:8px;border:none;cursor:pointer;background:var(--accent-c);color:#fff;font-weight:600}
    .btn.ghost{background:transparent;border:1px solid rgba(0,0,0,0.06);color:var(--text-c)}
    .result{margin-top:12px;padding:12px;border-radius:8px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));color:var(--text-c)}
    .muted{color:var(--muted-c);font-size:13px;margin-top:6px}
    .small{font-size:13px;color:var(--muted-c)}
    .themeRow{display:flex;align-items:center;gap:8px}
    @media (max-width:980px){ .grid{grid-template-columns:1fr} }
  </style>
</head>
<body>
 
    <a href="Index.html"><img src="NextSure logo New.png" width="120" alt="logo"></a>
       

    <div class="grid">
      <!-- LEFT: Calculator -->
      <div class="card" id="calcCard">
        <h3 style="margin:0">Travel Insurance Calculator</h3>
        <p class="small muted">Fill required fields, click Calculate → see price → Continue Order</p>

       

        <label><strong>Plan Insurance Category Plan</strong></label>
        <select id="plan">
          <option value="">Select Plan</option>
          <option>Plan A — Schengen (Worldwide Excl. USA & Canada)</option>
          <option>Plan B — Schengen (Worldwide Incl. USA & Canada)</option>
          <option>Plan A — Non—Schengen (Worldwide Excl. USA & Canada)</option>
          <option>Plan B — Non—Schengen (Worldwide Incl. USA & Canada)</option>
          <option>Plan C — Study (Excl. USA & Canada) Schengen</option>
          <option>Plan D — Study (Incl. USA & Canada) Schengen</option>
          <option>Plan C — Study (Excl. USA & Canada) Non—Schengen</option>
          <option>Plan D — Study (Incl. USA & Canada) Non—Schengen</option>
        </select>

        <div class="row">
          <div class="col">
            <label><strong>Date of Birth</strong></label>
            <input type="date" id="dob" onchange="autoAgeBand()">
          </div>
          <div class="col">
            <label><strong>Age Band</strong></label>
            <select id="age">
              <option>0.5-40</option><option>41-50</option><option>51-65</option><option>66-70</option><option>71-75</option><option>76-79</option><option>80-85</option><option>41-59</option>
            </select>
          </div>
        </div>

        <label><strong>Travel Duration (Days)</strong></label>
        <select id="days">
          <option>1-14</option><option>15-21</option><option>22-28</option><option>29-35</option><option>36-47</option><option>48-60</option><option>61-75</option><option>76-90</option><option>91-120</option><option>121-147</option><option>148-180</option><option>6month</option><option>12month</option>
        </select>

        <div class="row">
          <div class="col">
            <label><strong>Multiplier</strong></label>
            <input type="number" id="multiplier" value="1" step="0.01" min="0.01">
          </div>
          <div class="col">
            <label><strong>Special Offer (%)</strong></label>
            <input type="number" id="adminDiscount" value="0" min="0" max="100">
          </div>
        </div>
        <div style="margin-top:12px;display:flex;gap:8px">
          <button class="btn" onclick="calculate()">Calculate</button>
        </div>
        <div class="result" id="result" style="display:none"></div>
        <div style="margin-top:10px">
          <button class="btn" id="confirmBtn" style="display:none" onclick="confirmOrder()"><a href="Oder.html"> Continue</button></a>
        </div>

      </div>


  <script>
  /* -------------------------
     Full rate object (from your Travel Order test.html)
     ------------------------- */
  const rates = {
    "Plan A — Schengen (Worldwide Excl. USA & Canada)": {
      "0.5-40": {"1-14":1549,"15-21":1614,"22-28":1808,"29-35":2229,"36-47":2553,"48-60":3002,"61-75":3712,"76-90":4438,"91-120":7503,"121-147":9038,"148-180":12557},
      "41-50":  {"1-14":2324,"15-21":2479,"22-28":2767,"29-35":3341,"36-47":3830,"48-60":4537,"61-75":5600,"76-90":6639,"91-120":11330,"121-147":13586,"148-180":18741},
      "51-65":  {"1-14":3124,"15-21":3330,"22-28":3719,"29-35":4491,"36-47":5148,"48-60":6099,"61-75":7528,"76-90":8926 ,"91-120":15230,"121-147":18276,"148-180":25221},
      "66-70":  {"1-14":10164,"15-21":100836,"22-28":12098,"29-35":14617,"36-47":16753,"48-60":19842,"61-75":24498,"76-90":29040},
      "71-75":  {"1-14":17788,"15-21":18962,"22-28":21170,"29-35":25578,"36-47":29318,"48-60":34724,"61-75":42871,"76-90":50820},
      "76-79":  {"1-14":35574,"15-21":37924,"22-28":42340,"29-35":51157,"36-47":58636,"48-60":69448, "61-75":85743, "76-90":101640},
      "80-85":  {"1-14":50820, "15-21":54178,"22-28":60486,"29-35":73080,"36-47":83764,"48-60":99211}
    },
    "Plan B — Schengen (Worldwide Incl. USA & Canada)": {
      "0.5-40":{"1-14":2837,"15-21":3013,"22-28":3406,"29-35":4090,"36-47":4877,"48-60":7856,"61-75":11296,"76-90":13593,"91-120":19150,"121-147":25428,"148-180":33674},
      "41-50":{"1-14":5250,"15-21":5623,"22-28":6516,"29-35":7687,"36-47":9372,"48-60":15228,"61-75":22022,"76-90":26473,"91-120":37486,"121-147":54623,"148-180":66257},
      "51-65":{"1-14":6664,"15-21":7140,"22-28":8272,"29-35":9760,"36-47":11900,"48-60":19338,"61-75":27966,"76-90":33618 ,"91-120":47600,"121-147":63368,"148-180":84134},
      "66-70":{"1-14":21686,"15-21":23233,"22-28":26914,"29-35":31754,"36-47":38722,"48-60":62923,"61-75":90994,"76-90":109390},
      "71-75":{"1-14":37960,"15-21":40659,"22-28":47100,"29-35":55570,"36-47":67763,"48-60":110117,"61-75":159240,"76-90":191431},
      "76-79":{"1-14":75899,"15-21":81318,"22-28":94200,"29-35":111139,"36-47":135528,"48-60":220233,"61-75":318480,"76-90":382863},
      "80-85":{"1-14":108427,"15-21":116168,"22-28":134571,"29-35":158769,"36-47":193611,"48-60":314619}
    },
    "Plan A — Non—Schengen (Worldwide Excl. USA & Canada)": {
      "0.5-40":{"1-14":1239,"15-21":1291,"22-28":1446,"29-35":1783,"36-47":2042,"48-60":2402,"61-75":2970,"76-90":3550,"91-120":6003,"121-147":7230,"148-180":10046},
      "41-50": {"1-14":1860,"15-21":1983,"22-28":2213,"29-35":2673,"36-47":3063,"48-60":3629,"61-75":4480,"76-90":5311 ,"91-120":9063,"121-147":10869,"148-180":14992},
      "51-65": {"1-14":2499,"15-21":2664,"22-28":2976,"29-35":3592,"36-47":4119,"48-60":4879,"61-75":6022,"76-90":7140 ,"91-120":12184,"121-147":14613,"148-180":20326},
      "66-70": {"1-14":8131,"15-21":8668,"22-28":9678,"29-35":11692,"36-47":13402,"48-60":15873,"61-75":19598,"76-90":23232 },
      "71-75": {"1-14":14230,"15-21":15169,"22-28":16937,"29-35":20462,"36-47":23454,"48-60":27779,"61-75":34297,"76-90":40657 },
      "76-79": {"1-14":28460,"15-21":30338,"22-28":33873,"29-35":40924,"36-47":46908,"48-60":55558,"61-75":68592,"76-90":81312 },
      "80-85": {"1-14":40457 ,"15-21":43339,"22-28":48390,"29-35":58463,"36-47":67011,"48-60":79368,}
    },
    "Plan B — Non—Schengen (Worldwide Incl. USA & Canada)": {
      "0.5-40":{"1-14":2269,"15-21":2411,"22-28":2724,"29-35":3271,"36-47":3901,"48-60":6284,"61-75":9037,"76-90":10874,"91-120":15320,"121-147":20341,"148-180":26939},
      "41-50": {"1-14":4200,"15-21":4499,"22-28":5212,"29-35":6149,"36-47":7497,"48-60":12182,"61-75":17910,"76-90":21178},
      "51-65": {"1-14":5331,"15-21":5712,"22-28":6618,"29-35":7808,"36-47":9520,"48-60":15470,"61-75":22371,"76-90":26894},
      "66-70": {"1-14":17349,"15-21":18587,"22-28":21531,"29-35":25402,"36-47":30977,"48-60":50339,"61-75":72796,"76-90":87511},
      "71-75": {"1-14":30360,"15-21":32526,"22-28":37679,"29-35":44454,"36-47":54210,"48-60":88093,"61-75":127392,"76-90":153146},
      "76-79": {"1-14":60720,"15-21":65052,"22-28":75358,"29-35":88910,"36-47":108420,"48-60":176187,"61-75":254784,"76-90":306291},
      "80-85": {"1-14":86742, "15-21":92931,"22-28":107653,"29-35":127013,"36-47":154886,"48-60":251694}
    },
    "Plan C — Study (Excl. USA & Canada) Schengen": {"0.5-40":{"6month":13956,"12month":27912},"41-59":{"6month":21072,"12month":42144}},
    "Plan D — Study (Incl. USA & Canada) Schengen": {"0.5-40":{"6month":22470,"12month":44940},"41-59":{"6month":42498,"12month":84996}},
    "Plan C — Study (Excl. USA & Canada) Non—Schengen": {"0.5-40":{"6month":11166,"12month":22332},"41-59":{"6month":16860,"12month":33720}},
    "Plan D — Study (Incl. USA & Canada) Non—Schengen": {"0.5-40":{"6month":17976,"12month":35952},"41-59":{"6month":34002,"12month":68004}}
  };

  /* -------------------------
     Utility & UI functions
     ------------------------- */
  function _(id){ return document.getElementById(id); }
  function notify(msg){ alert(msg); }

  /* Theme */
  function applySavedTheme(){
    const t = localStorage.getItem('ns_theme') || 'dark';
    document.documentElement.setAttribute('data-theme', t);
    _('themeSelect').value = t;
  }
  

  /* auto age band from dob */
  function autoAgeBand(){
    const dob = _('dob').value; if(!dob) return;
    const b = new Date(dob), now = new Date();
    let age = now.getFullYear() - b.getFullYear();
    const m = now.getMonth() - b.getMonth();
    if(m < 0 || (m === 0 && now.getDate() < b.getDate())) age--;
    let band = '';
    if(age <= 40) band='0.5-40';
    else if(age <= 50) band='41-50';
    else if(age <= 59) band='41-59';
    else if(age <= 65) band='51-65';
    else if(age <= 70) band='66-70';
    else if(age <=75) band='71-75';
    else if(age <=79) band='76-79';
    else band='80-85';
    _('age').value = band;
  }

  /* Calculate price */
  function calculate(){
    const plan = _('plan').value;
    const age = _('age').value;
    const days = _('days').value;
    const dob = _('dob').value;
    
   
    const multiplier = parseFloat(_('multiplier').value || 0);
    const adminDiscount = parseFloat(_('adminDiscount').value || 0);

    if(!plan || !age || !multiplier || !dob || !days){ notify('Please fill Plan, Age Band, Days.'); return; }

    const planKey = Object.keys(rates).find(k => k.trim().toLowerCase() === plan.trim().toLowerCase()) || plan;
    const netRaw = rates[planKey]?.[age]?.[days];

    if(!netRaw){
      _('result').style.display='block';
      _('result').innerHTML = '<strong style="color:#ff9a9a">Rate not available for this combination.</strong>';
      _('confirmBtn').style.display='none';
      return;
    }

    const net = parseFloat(netRaw);
    const vat = net * 0.15;
     const subtotal = net + vat;
     const Discount =  net - (net * (adminDiscount / 100))+vat;

    const discountedNet = net * (adminDiscount / 100)*multiplier;
    

    const total = Discount * multiplier;

    _('result').style.display='block';
    _('result').innerHTML = `

      <div><strong> Net Premium:</strong> ৳${net.toFixed(2)}</div>
      <div><strong> VAT (15%):</strong> ৳${vat.toFixed(2)}</div>
      <div><strong> Gross Premium (incl. VAT):</strong> ৳${subtotal.toFixed(2)}</div
      <div><strong> Special offer:</strong> ৳${discountedNet.toFixed(2)}</div>
      <div><strong> Discount Net</strong> ৳${(Discount.toFixed(2))}</div>
      
   
      <div><strong> Multiplier: </strong> ×${multiplier.toFixed(2)}</div>
      <div style="margin-top:8px;font-size:16px"><strong>Total Payable: ৳${total.toFixed(2)}</div>
    `;
    _('confirmBtn').style.display='inline-block';

    window._lastCalc = {
      company: _('Company').value || '',
      plan, age, days, country: _('countrySearch').value || '', occupation: _('occupation').value || '',
      travelDate: _('travelDate').value || '', dob: _('dob').value || '', contact, multiplier, adminDiscount, net, discountedNet, vat, total
    };
  }



  /* helpers */
  function resetCalc(){
    _('Company').value=''; _('plan').value=''; _('dob').value=''; _('age').value='0.5-40';
    _('days').value='1-14'; _('countrySearch').value=''; _('occupation').value='';
    _('travelDate').value=''; _('contact').value=''; _('multiplier').value='1'; _('adminDiscount').value='0';
    _('result').style.display='none';
    window._lastCalc = null;
  }
  function addDemoOrder(){
    const orders = JSON.parse(localStorage.getItem('orders') || '[]');
    orders.unshift(demo);
    localStorage.setItem('orders', JSON.stringify(orders));
    notify('Demo order added. Admin can view in dashboard.');
  }

  /* save/load admin settings? (not on this page) - admin config is in admin.html */
  /* init */
  document.addEventListener('DOMContentLoaded', ()=>{
    applySavedTheme();
  });

  </script>
</body>
</html>
<!-- Save this as calculator.html -->
<!doctype html>
<html lang="bn">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>NextSure — Travel Insurance Calculator</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --dark-bg:#1b0a48; --dark-card:#ffffffef; --muted:#000000; -webkit-text-color: #dcdbea; --accent:#3b82f6; --success:#10b981; --danger:#ef4444; --warn:#f59e0b; --text:#010000;
      --light-bg:#f4f7fb; --light-card:#ffffff; --muted-light:#000000; --text-light:#0b1220; --h1-color:#000000;
    }
    html[data-theme='dark']{ --page-bg:var(--dark-bg); --card-bg:var(--dark-card); --muted-c:var(--muted); --text-c:var(--text); --accent-c:var(--accent); }
    html[data-theme='light']{ --page-bg:var(--light-bg); --card-bg:var(--light-card); --muted-c:var(--muted-light); --text-c:var(--text-light); --accent-c:var(--accent); }

    *{box-sizing:border-box}
    body{font-family:Inter,system-ui,Arial;background:var(--page-bg);color:#ffffff;margin:0;padding:22px var(--text)color#ffffff;}
    .app{max-width:800px;margin:0 auto}
    .header{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:18px}
    .brand{display:flex;gap:12px;align-items:center}
    .text{color: #000000;}
    .logo{width:52px;height:52px;border-radius:12px;background:linear-gradient(135deg,var(--accent-c),#7c3aed);display:flex;align-items:center;justify-content:center;font-weight:700;color:#dcdbea}
    h1{margin:2px;font-size:18px;}
    p.lead{margin:0;color:var(--muted-c);font-size:13px}
    .grid{display:grid;grid-template-columns:1fr 10px;gap:18px;color: #000000;}
    .card{display: block; background:#dcdbea;padding:16px;border-radius:12px;border:1px solid #0000000d;box-shadow:0 6px 24px #000000}
    label{display:block;color:var(--muted-c);font-size:13px;margin-top:10px}
    input, select, textarea{width:100%;padding:10px;border-radius:8px;border:1px solid #000000;background:transparent;color:var(--text-c);margin-top:6px}
    .row{display:flex;gap:10px}
    .col{flex:1}
    .btn{padding:10px 14px;border-radius:8px;border:none;cursor:pointer;background:var(--accent-c);color:#0dff00;font-weight:600}
    .btn.ghost{background:transparent;border:1px solid #000000;color:var(--text-c)}
    .result{margin-top:12px;padding:12px;border-radius:8px;background:linear-gradient(180deg, #fcf9f9, #00000000);color:var(--text-c)}
    .muted{color:var(--muted-c);font-size:13px;margin-top:6px}
    .small{font-size:13px;color:var(--muted-c)}
    .themeRow{display:flex;align-items:center;gap:8px}
    @media (max-width:980px){ .grid{grid-template-columns:1fr} }
  </style>
</head>
<a href="Oder.html"><img src="NextSure logo New.png" width="120" alt="logo"></a> 
<body>
  <div class="app">
    <div class="header">
      <div class="brand">
        <div class="logo">NI</div>
        
        <div class="text">
          <h1>NextSure — Travel Insurance</h1>
          
          <p class="lead"></p></div>
          
        </div>

        <div class="themeRow small">
           <button class="btn ghost" onclick="location.href='admin.html'">Admin Dashboard</button>
            <label>Theme</label>
          <select id="themeSelect" onchange="changeTheme(this.value)">
            <option value="dark">Dark</option>
            <option value="light">Light</option>
          </select>
          <label style="margin:0 6px 0 0"></label>
        
          </select>
        </div>
      </div>
      <div style="display:flex;gap:10px;align-items:center">
    </div>

    <div class="grid">
      <!-- LEFT: Calculator -->
      <div class="card" id="calcCard"> <h1>NextSure — Travel Insurance</h1>
        
        <p class="small muted">Fill required fields, click Calculate → see price → Confirm & Save & Notify</p>

        <label> <strong>your insurance company</strong> </label>
        <select id="Company">
          <option value="">Select Company</option>
          <option>Bangladesh National Insurance co. ltd</option>
          <option>Prime Insurance co. ltd</option>
          <option>Mercantile Islami Insurance co. ltd</option>
          <option>Sena Insurance co. ltd</option>
        </select>
       
        <label> <strong> Plan Insurance Category Plan</strong></label>
        <select id="plan">
          <option value="">Select Plan</option>
          <option>Plan A — Schengen (Worldwide Excl. USA & Canada)</option>
          <option>Plan B — Schengen (Worldwide Incl. USA & Canada)</option>
          <option>Plan A — Non—Schengen (Worldwide Excl. USA & Canada)</option>
          <option>Plan B — Non—Schengen (Worldwide Incl. USA & Canada)</option>
          <option>Plan C — Study (Excl. USA & Canada) Schengen</option>
          <option>Plan D — Study (Incl. USA & Canada) Schengen</option>
          <option>Plan C — Study (Excl. USA & Canada) Non—Schengen</option>
          <option>Plan D — Study (Incl. USA & Canada) Non—Schengen</option>
        </select>

        <div class="row">
          <div class="col">
            <label><strong>Date of Birth</strong></label>
            <input type="date" id="dob" onchange="autoAgeBand()">
          </div>
          <div class="col">
            <label><strong> Age Band</strong></label>
            <select id="age">
              <option>0.5-40</option><option>41-50</option><option>51-65</option><option>66-70</option><option>71-75</option><option>76-79</option><option>80-85</option><option>41-59</option>
            </select>
          </div>
        </div>

        <label><strong>Travel Duration (Days)</h4></label>
        <select id="days">
          <option>1-14</option><option>15-21</option><option>22-28</option><option>29-35</option><option>36-47</option><option>48-60</option><option>61-75</option><option>76-90</option><option>91-120</option><option>121-147</option><option>148-180</option><option>6month</option><option>12month</option>
        </select>

        <label><strong>Destination Country</h4></label>
        <input list="countries" id="countrySearch" placeholder="Country...">
        <datalist id="countries">
            <option value="Afghanistan">Afghanistan</option>
            <option value="Albania">Albania</option>
            <option value="Algeria">Algeria</option>
            <option value="Andorra">Andorra</option>
            <option value="Angola">Angola</option>
            <option value="Antigua and Barbuda">Antigua and Barbuda</option>
            <option value="Argentina">Argentina</option>
            <option value="Armenia">Armenia</option>
            <option value="Australia">Australia</option>
            <option value="Austria">Austria</option>
            <option value="Azerbaijan">Azerbaijan</option>
            <option value="Bahamas">Bahamas</option>
            <option value="Bahrain">Bahrain</option>
            <option value="Bangladesh">Bangladesh</option>
            <option value="Barbados">Barbados</option>
            <option value="Belarus">Belarus</option>
            <option value="Belgium">Belgium</option>
            <option value="Belize">Belize</option>
            <option value="Benin">Benin</option>
            <option value="Bhutan">Bhutan</option>
            <option value="Bolivia">Bolivia</option>
            <option value="Bosnia and Herzegovina">Bosnia and Herzegovina</option>
            <option value="Botswana">Botswana</option>
            <option value="Brazil">Brazil</option>
            <option value="Brunei">Brunei</option>
            <option value="Bulgaria">Bulgaria</option>
            <option value="Burkina Faso">Burkina Faso</option>
            <option value="Burundi">Burundi</option>
            <option value="Cambodia">Cambodia</option>
            <option value="Cameroon">Cameroon</option>
            <option value="Canada">Canada</option>
            <option value="Chile">Chile</option>
            <option value="China">China</option>
            <option value="Colombia">Colombia</option>
            <option value="Congo">Congo</option>
            <option value="Costa Rica">Costa Rica</option>
            <option value="Croatia">Croatia</option>
            <option value="Cuba">Cuba</option>
            <option value="Cyprus">Cyprus</option>
            <option value="Czech Republic">Czech Republic</option>
            <option value="Denmark">Denmark</option>
            <option value="Dominican Republic">Dominican Republic</option>
            <option value="Ecuador">Ecuador</option>
            <option value="Egypt">Egypt</option>
            <option value="El Salvador">El Salvador</option>
            <option value="Estonia">Estonia</option>
            <option value="Ethiopia">Ethiopia</option>
            <option value="Fiji">Fiji</option>
            <option value="Finland">Finland</option>
            <option value="France">France</option>
            <option value="Gabon">Gabon</option>
            <option value="Gambia">Gambia</option>
            <option value="Georgia">Georgia</option>
            <option value="Germany">Germany</option>
            <option value="Ghana">Ghana</option>
            <option value="Greece">Greece</option>
            <option value="Greenland">Greenland</option>
            <option value="Grenada">Grenada</option>
            <option value="Guatemala">Guatemala</option>
            <option value="Guinea">Guinea</option>
            <option value="Guyana">Guyana</option>
            <option value="Haiti">Haiti</option>
            <option value="Honduras">Honduras</option>
            <option value="Hong Kong">Hong Kong</option>
            <option value="Hungary">Hungary</option>
            <option value="Iceland">Iceland</option>
            <option value="India">India</option>
            <option value="Indonesia">Indonesia</option>
            <option value="Iran">Iran</option>
            <option value="Iraq">Iraq</option>
            <option value="Ireland">Ireland</option>
            <option value="Israel">Israel</option>
            <option value="Italy">Italy</option>
            <option value="Jamaica">Jamaica</option>
            <option value="Japan">Japan</option>
            <option value="Jordan">Jordan</option>
            <option value="Kazakhstan">Kazakhstan</option>
            <option value="Kenya">Kenya</option>
            <option value="Kuwait">Kuwait</option>
            <option value="Kyrgyzstan">Kyrgyzstan</option>
            <option value="Laos">Laos</option>
            <option value="Latvia">Latvia</option>
            <option value="Lebanon">Lebanon</option>
            <option value="Lesotho">Lesotho</option>
            <option value="Liberia">Liberia</option>
            <option value="Libya">Libya</option>
            <option value="Lithuania">Lithuania</option>
            <option value="Luxembourg">Luxembourg</option>
            <option value="Macau">Macau</option>
            <option value="Madagascar">Madagascar</option>
            <option value="Malawi">Malawi</option>
            <option value="Malaysia">Malaysia</option>
            <option value="Maldives">Maldives</option>
            <option value="Mali">Mali</option>
            <option value="Malta">Malta</option>
            <option value="Mauritius">Mauritius</option>
            <option value="Mexico">Mexico</option>
            <option value="Moldova">Moldova</option>
            <option value="Monaco">Monaco</option>
            <option value="Mongolia">Mongolia</option>
            <option value="Montenegro">Montenegro</option>
            <option value="Morocco">Morocco</option>
            <option value="Mozambique">Mozambique</option>
            <option value="Myanmar">Myanmar</option>
            <option value="Namibia">Namibia</option>
            <option value="Nepal">Nepal</option>
            <option value="Netherlands">Netherlands</option>
            <option value="New Zealand">New Zealand</option>
            <option value="Nicaragua">Nicaragua</option>
            <option value="Niger">Niger</option>
            <option value="Nigeria">Nigeria</option>
            <option value="North Korea">North Korea</option>
            <option value="Norway">Norway</option>
            <option value="Oman">Oman</option>
            <option value="Pakistan">Pakistan</option>
            <option value="Palestine">Palestine</option>
            <option value="Panama">Panama</option>
            <option value="Papua New Guinea">Papua New Guinea</option>
            <option value="Paraguay">Paraguay</option>
            <option value="Peru">Peru</option>
            <option value="Philippines">Philippines</option>
            <option value="Poland">Poland</option>
            <option value="Portugal">Portugal</option>
            <option value="Qatar">Qatar</option>
            <option value="Romania">Romania</option>
            <option value="Russia">Russia</option>
            <option value="Rwanda">Rwanda</option>
            <option value="Saudi Arabia">Saudi Arabia</option>
            <option value="Senegal">Senegal</option>
            <option value="Serbia">Serbia</option>
            <option value="Seychelles">Seychelles</option>
            <option value="Sierra Leone">Sierra Leone</option>
            <option value="Singapore">Singapore</option>
            <option value="Slovakia">Slovakia</option>
            <option value="Slovenia">Slovenia</option>
            <option value="Somalia">Somalia</option>
            <option value="South Africa">South Africa</option>
            <option value="South Korea">South Korea</option>
            <option value="Spain">Spain</option>
            <option value="Sri Lanka">Sri Lanka</option>
            <option value="Sudan">Sudan</option>
            <option value="Suriname">Suriname</option>
            <option value="Sweden">Sweden</option>
            <option value="Switzerland">Switzerland</option>
            <option value="Syria">Syria</option>
            <option value="Taiwan">Taiwan</option>
            <option value="Tajikistan">Tajikistan</option>
            <option value="Tanzania">Tanzania</option>
            <option value="Thailand">Thailand</option>
            <option value="Togo">Togo</option>
            <option value="Trinidad and Tobago">Trinidad and Tobago</option>
            <option value="Tunisia">Tunisia</option>
            <option value="Turkey">Turkey</option>
            <option value="Turkmenistan">Turkmenistan</option>
            <option value="Uganda">Uganda</option>
            <option value="Ukraine">Ukraine</option>
            <option value="United Arab Emirates">United Arab Emirates</option>
            <option value="United Kingdom">United Kingdom</option>
            <option value="United States">United States</option>
            <option value="Uruguay">Uruguay</option>
            <option value="Uzbekistan">Uzbekistan</option>
            <option value="Venezuela">Venezuela</option>
            <option value="Vietnam">Vietnam</option>
            <option value="Yemen">Yemen</option>
            <option value="Zambia">Zambia</option>
            <option value="Zimbabwe">Zimbabwe</option>
            <option value="Other">Other</option></datalist>

        <label><strong>Occupation</strong></label>
        <input type="text" id="occupation" placeholder="e.g. Student / Engineer / Business">

        <div class="row">
          <div class="col">
            <label><strong>Travel Date</strong></label>
            <input type="date" id="travelDate">
          </div>
          <div class="col">
            <label><strong>Mobile Number : +88</strong></label>
            <input type="text" id="contact" placeholder="+88XXXXXXXXXX">
          </div>
        </div>

        <div class="row">
          <div class="col">
            <label><strong>Multiplier</strong></label>
            <input type="number" id="multiplier" value="1" step="0.01" min="0.01">
          </div>
          <div class="col">
            <label><strong>Special Offer (%)</strong></label>
            <input type="number" id="adminDiscount" value="0" min="0" max="100">
          </div>
        </div>

        <div style="margin-top:12px;display:flex;gap:8px">
          <button class="btn" onclick="calculate()"><strong>Calculate</strong></button>
          <button class="btn" onclick="resetCalc()"><strong>Clear</strong></button>
        </div>

        <div class="result" id="result" style="display:none"></div>

        <div style="margin-top:10px">
          <button class="btn" id="confirmBtn" style="display:none" onclick="confirmOrder()">Confirm order</button>
        </div>

      </div>

      

  <!-- EmailJS SDK -->
  <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>

  <script>
  /* -------------------------
     Full rate object (from your Travel Order test.html)
     ------------------------- */
  const rates = {
    "Plan A — Schengen (Worldwide Excl. USA & Canada)": {
      "0.5-40": {"1-14":1549,"15-21":1614,"22-28":1808,"29-35":2229,"36-47":2553,"48-60":3002,"61-75":3712,"76-90":4438,"91-120":7503,"121-147":9038,"148-180":12557},
      "41-50":  {"1-14":2324,"15-21":2479,"22-28":2767,"29-35":3341,"36-47":3830,"48-60":4537,"61-75":5600,"76-90":6639,"91-120":11330,"121-147":13586,"148-180":18741},
      "51-65":  {"1-14":3124,"15-21":3330,"22-28":3719,"29-35":4491,"36-47":5148,"48-60":6099,"61-75":7528,"76-90":8926 ,"91-120":15230,"121-147":18276,"148-180":25221},
      "66-70":  {"1-14":10164,"15-21":100836,"22-28":12098,"29-35":14617,"36-47":16753,"48-60":19842,"61-75":24498,"76-90":29040},
      "71-75":  {"1-14":17788,"15-21":18962,"22-28":21170,"29-35":25578,"36-47":29318,"48-60":34724,"61-75":42871,"76-90":50820},
      "76-79":  {"1-14":35574,"15-21":37924,"22-28":42340,"29-35":51157,"36-47":58636,"48-60":69448, "61-75":85743, "76-90":101640},
      "80-85":  {"1-14":50820, "15-21":54178,"22-28":60486,"29-35":73080,"36-47":83764,"48-60":99211}
    },
    "Plan B — Schengen (Worldwide Incl. USA & Canada)": {
      "0.5-40":{"1-14":2837,"15-21":3013,"22-28":3406,"29-35":4090,"36-47":4877,"48-60":7856,"61-75":11296,"76-90":13593,"91-120":19150,"121-147":25428,"148-180":33674},
      "41-50":{"1-14":5250,"15-21":5623,"22-28":6516,"29-35":7687,"36-47":9372,"48-60":15228,"61-75":22022,"76-90":26473,"91-120":37486,"121-147":54623,"148-180":66257},
      "51-65":{"1-14":6664,"15-21":7140,"22-28":8272,"29-35":9760,"36-47":11900,"48-60":19338,"61-75":27966,"76-90":33618 ,"91-120":47600,"121-147":63368,"148-180":84134},
      "66-70":{"1-14":21686,"15-21":23233,"22-28":26914,"29-35":31754,"36-47":38722,"48-60":62923,"61-75":90994,"76-90":109390},
      "71-75":{"1-14":37960,"15-21":40659,"22-28":47100,"29-35":55570,"36-47":67763,"48-60":110117,"61-75":159240,"76-90":191431},
      "76-79":{"1-14":75899,"15-21":81318,"22-28":94200,"29-35":111139,"36-47":135528,"48-60":220233,"61-75":318480,"76-90":382863},
      "80-85":{"1-14":108427,"15-21":116168,"22-28":134571,"29-35":158769,"36-47":193611,"48-60":314619}
    },
    "Plan A — Non—Schengen (Worldwide Excl. USA & Canada)": {
      "0.5-40":{"1-14":1239,"15-21":1291,"22-28":1446,"29-35":1783,"36-47":2042,"48-60":2402,"61-75":2970,"76-90":3550,"91-120":6003,"121-147":7230,"148-180":10046},
      "41-50": {"1-14":1860,"15-21":1983,"22-28":2213,"29-35":2673,"36-47":3063,"48-60":3629,"61-75":4480,"76-90":5311 ,"91-120":9063,"121-147":10869,"148-180":14992},
      "51-65": {"1-14":2499,"15-21":2664,"22-28":2976,"29-35":3592,"36-47":4119,"48-60":4879,"61-75":6022,"76-90":7140 ,"91-120":12184,"121-147":14613,"148-180":20326},
      "66-70": {"1-14":8131,"15-21":8668,"22-28":9678,"29-35":11692,"36-47":13402,"48-60":15873,"61-75":19598,"76-90":23232 },
      "71-75": {"1-14":14230,"15-21":15169,"22-28":16937,"29-35":20462,"36-47":23454,"48-60":27779,"61-75":34297,"76-90":40657 },
      "76-79": {"1-14":28460,"15-21":30338,"22-28":33873,"29-35":40924,"36-47":46908,"48-60":55558,"61-75":68592,"76-90":81312 },
      "80-85": {"1-14":40457 ,"15-21":43339,"22-28":48390,"29-35":58463,"36-47":67011,"48-60":79368,}
    },
    "Plan B — Non—Schengen (Worldwide Incl. USA & Canada)": {
      "0.5-40":{"1-14":2269,"15-21":2411,"22-28":2724,"29-35":3271,"36-47":3901,"48-60":6284,"61-75":9037,"76-90":10874,"91-120":15320,"121-147":20341,"148-180":26939},
      "41-50": {"1-14":4200,"15-21":4499,"22-28":5212,"29-35":6149,"36-47":7497,"48-60":12182,"61-75":17910,"76-90":21178},
      "51-65": {"1-14":5331,"15-21":5712,"22-28":6618,"29-35":7808,"36-47":9520,"48-60":15470,"61-75":22371,"76-90":26894},
      "66-70": {"1-14":17349,"15-21":18587,"22-28":21531,"29-35":25402,"36-47":30977,"48-60":50339,"61-75":72796,"76-90":87511},
      "71-75": {"1-14":30360,"15-21":32526,"22-28":37679,"29-35":44454,"36-47":54210,"48-60":88093,"61-75":127392,"76-90":153146},
      "76-79": {"1-14":60720,"15-21":65052,"22-28":75358,"29-35":88910,"36-47":108420,"48-60":176187,"61-75":254784,"76-90":306291},
      "80-85": {"1-14":86742, "15-21":92931,"22-28":107653,"29-35":127013,"36-47":154886,"48-60":251694}
    },
    "Plan C — Study (Excl. USA & Canada) Schengen": {"0.5-40":{"6month":13956,"12month":27912},"41-59":{"6month":21072,"12month":42144}},
    "Plan D — Study (Incl. USA & Canada) Schengen": {"0.5-40":{"6month":22470,"12month":44940},"41-59":{"6month":42498,"12month":84996}},
    "Plan C — Study (Excl. USA & Canada) Non—Schengen": {"0.5-40":{"6month":11166,"12month":22332},"41-59":{"6month":16860,"12month":33720}},
    "Plan D — Study (Incl. USA & Canada) Non—Schengen": {"0.5-40":{"6month":17976,"12month":35952},"41-59":{"6month":34002,"12month":68004}}
  };

  /* -------------------------
     Utility & UI functions
     ------------------------- */
  function _(id){ return document.getElementById(id); }
  function notify(msg){ alert(msg); }

  /* Theme */
  function applySavedTheme(){
    const t = localStorage.getItem('ns_theme') || 'dark';
    document.documentElement.setAttribute('data-theme', t);
    _('themeSelect').value = t;
  }
  function changeTheme(v){
    localStorage.setItem('ns_theme', v);
    document.documentElement.setAttribute('data-theme', v);
  }

  /* auto age band from dob */
  function autoAgeBand(){
    const dob = _('dob').value; if(!dob) return;
    const b = new Date(dob), now = new Date();
    let age = now.getFullYear() - b.getFullYear();
    const m = now.getMonth() - b.getMonth();
    if(m < 0 || (m === 0 && now.getDate() < b.getDate())) age--;
    let band = '';
    if(age <= 40) band='0.5-40';
    else if(age <= 50) band='41-50';
    else if(age <= 59) band='41-59';
    else if(age <= 65) band='51-65';
    else if(age <= 70) band='66-70';
    else if(age <=75) band='71-75';
    else if(age <=79) band='76-79';
    else band='80-85';
    _('age').value = band;
  }

  /* Calculate price */
  function calculate(){
    const plan = _('plan').value;
    const age = _('age').value;
    const days = _('days').value;
    const contact = _('contact').value.trim();
    const dob = _('dob').value;
    const countries = _('countrySearch').value;
    const occupation = _('occupation').value;
    const Company = _('Company').value;
    const travelDate = _('travelDate').value;
    const multiplier = parseFloat(_('multiplier').value || 1);
    const adminDiscount = parseFloat(_('adminDiscount').value || 0);

    if(!plan || !age || !travelDate || !multiplier|| !occupation|| !countries|| !dob|| !Company || !days || !contact){ notify('Please fill Plan, Age Band, Days and Mobile.'); return; }

    const planKey = Object.keys(rates).find(k => k.trim().toLowerCase() === plan.trim().toLowerCase()) || plan;
    const netRaw = rates[planKey]?.[age]?.[days];

    if(!netRaw){
      _('result').style.display='block';
      _('result').innerHTML = '<strong style="color:#ff9a9a">Rate not available for this combination.</strong>';
      _('confirmBtn').style.display='none';
      return;
    }

    const net = parseFloat(netRaw);
    const vat = net * 0.15;
     const subtotal = net + vat;
     const Discount =  net - (net * (adminDiscount / 100))+vat;

    const discountedNet = net * (adminDiscount / 100)*multiplier;
    

    const total = Discount * multiplier;

    _('result').style.display='block';
    _('result').innerHTML = `

      <div><strong> Net Premium:</strong> ৳${net.toFixed(2)}</div>
      <div><strong> VAT (15%):</strong> ৳${vat.toFixed(2)}</div>
      <div><strong> Gross Premium (incl. VAT):</strong> ৳${subtotal.toFixed(2)}</div
      <div><strong> Special offer:</strong> ৳${discountedNet.toFixed(2)}</div>
      <div><strong> Discount Net</strong> ৳${(Discount.toFixed(2))}</div>
      
   
      <div><strong> Multiplier: </strong> ×${multiplier.toFixed(2)}</div>
      <div style="margin-top:8px;font-size:16px"><strong>Total Payable: ৳${total.toFixed(2)}</div>
    `;
    _('confirmBtn').style.display='inline-block';

    window._lastCalc = {
      company: _('Company').value || '',
      plan, age, days, country: _('countrySearch').value || '', occupation: _('occupation').value || '',
      travelDate: _('travelDate').value || '', dob: _('dob').value || '', contact, multiplier, adminDiscount, net, discountedNet, vat, total
    };
  }
  /* Confirm order -> save & notify */
  function confirmOrder(){
    if(!window._lastCalc){ notify('No calculation to confirm.'); return; }
    const orderId = 'NS' + Date.now().toString().slice(-5)  + Math.floor( Math.random() * 1);
    const order = { orderId, ...window._lastCalc, status: 'Pending', createdAt: new Date().toLocaleString(), };

    const orders = JSON.parse(localStorage.getItem('orders') || '[]');
    orders.unshift(order);
    localStorage.setItem('orders', JSON.stringify(orders));

    notify('Order saved: ' + orderId);

    // Trigger notifications
    sendEmailNotification(order);
    sendSMSWebhook(order);

    // clear UI
    resetCalc();
    _('confirmBtn').style.display='none';
  }

  /* Email notification (EmailJS) - admin must configure via admin dashboard */
  function sendEmailNotification(order){
    const service = localStorage.getItem('emailjs_service') || '';
    const template = localStorage.getItem('emailjs_template') || '';
    const user = localStorage.getItem('emailjs_user') || '';
    const adminEmail = localStorage.getItem('admin_email') || '';
    if(!(service && template && user && adminEmail)){ console.warn('EmailJS not fully configured; skipping email notify'); return; }

    try{ if(window.emailjs && !window.emailjs.__initialized){ emailjs.init(user); window.emailjs.__initialized = true; } }catch(e){ console.warn(e) }

    const templateParams = {
      to_email: adminEmail,
      orderId: order.orderId,
      company: order.company,
      plan: order.plan,
      occupation: order.occupation,
      mobile: order.contact,
      total: Number(order.total).toFixed(2),
      status: order.status,

     DataTransferItem: new Date().toLocaleString('en-GB', { dateStyle: 'medium', timeStyle: 'short' }),


    };

    emailjs.send(service, template, templateParams)
      .then(function(response){ console.log('Email sent', response.status); })
      .catch(function(error){ console.error('EmailJS error', error); });
  }

  /* SMS webhook: frontend POSTs to admin-provided webhook; server must send SMS securely */
  function sendSMSWebhook(order){
    const webhook = localStorage.getItem('sms_webhook') || '';
    if(!webhook){ console.log('No sms webhook configured'); return; }

    const message = `New Order ${order.orderId}: ${order.plan} • ৳${Number(order.total).toFixed(2)} • ${order.contact}`;
    fetch(webhook, {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify({ mobile: localStorage.getItem('admin_mobile') || '', message, order })
    })
    .then(r => { if(!r.ok) throw new Error('Webhook responded ' + r.status); return r.json(); })
    .then(j => console.log('SMS webhook response', j))
    .catch(err => console.warn('SMS webhook error', err));
  }

  /* helpers */
  function resetCalc(){
    _('Company').value=''; _('plan').value=''; _('dob').value=''; _('age').value='0.5-40';
    _('days').value='1-14'; _('countrySearch').value=''; _('occupation').value='';
    _('travelDate').value=''; _('contact').value=''; _('multiplier').value='1'; _('adminDiscount').value='0';
    _('result').style.display='none';
    window._lastCalc = null;
  }

  function addDemo(){
    const demo = {
      orderId:'ORDDEMO'+Date.now().toString().slice(-6),
      company:'Prime Insurance',
      plan:'Plan A — Schengen (Worldwide Excl. USA & Canada)',
      dob:'1990-05-10', age:'0.5-40', days:'1-14', country:'Bangladesh', occupation:'Engineer',
      travelDate:'2025-11-01', contact:'+8801712345678', multiplier:1, adminDiscount:0, net:1549, discountedNet:1549, vat:232.35, total:1781.35, status:'Pending', createdAt:new Date().toISOString()
    };
    const orders = JSON.parse(localStorage.getItem('orders') || '[]');
    orders.unshift(demo);
    localStorage.setItem('orders', JSON.stringify(orders));
    notify('Demo order added. Admin can view in dashboard.');
  }

  /* save/load admin settings? (not on this page) - admin config is in admin.html */
  /* init */
  document.addEventListener('DOMContentLoaded', ()=>{
    applySavedTheme();
  });

  </script>
</body>
</html>
