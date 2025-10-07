# 3-events-new<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>JKS Events and Catering Services</title>
<style>
  body { font-family: Arial,sans-serif; background: #f6f8fa; margin:0; padding:0; color:#2a4c8d; }
  .title-section { text-align:center; margin:25px 0 10px 0; font-size:1.6em; font-weight:700; }
  .display-bar { margin:0 auto 20px auto; border:2px dashed #3399cc; width:85%; padding:18px 0; background:#edf5fa; color:#466676; border-radius:8px; font-size:1.15em; font-weight:600; text-align:center; }
  .menu-bar { display:flex; justify-content:center; gap:60px; margin-bottom:25px; }
  .menu-item { background-color:#468ac9; color:white; padding:14px 50px; border-radius:8px; font-weight:700; cursor:pointer; user-select:none; transition:background-color .3s ease; }
  .menu-item:hover { background-color:#3568a1; }
  .section, .form-section { max-width:930px; margin:0 auto 30px auto; padding:20px; background:white; border-radius:12px; border:2px solid #3399cc; box-shadow:0 2px 12px #a6c6e6aa; }
  .category-list { display:flex; justify-content:space-around; gap:30px; flex-wrap:wrap; margin-bottom:20px; }
  .category-card { border:2px solid #3399cc; border-radius:8px; width:200px; padding:15px; cursor:pointer; font-weight:700; font-size:1.1em; text-align:center; user-select:none; color:#2a4c8d; transition:background-color .3s ease; }
  .category-card:hover { background-color:#3399cc; color:white; }
  .budget { font-size:.9em; margin-top:8px; color:#284067; font-weight:600; }
  .service-grid { display:flex; flex-wrap:wrap; gap:20px; justify-content:center; }
  .service-card { flex: 1 0 200px; background:#f3f4fa; border-radius:8px; border:2px solid #3399cc; padding:15px 10px; text-align:center; font-weight:600; color:#2a4c8d; cursor:pointer; user-select:none; transition:background-color .3s ease; }
  .service-card:hover { background-color:#3399cc; color:white; }
  form { max-width:480px; margin:20px auto 30px auto; padding:20px; border:2px solid #3399cc; border-radius:10px; background-color:#f0f7ff; }
  label { display:block; font-weight:700; margin-bottom:8px; color:#01579b; }
  input[type="text"], input[type="email"], input[type="tel"], textarea, select { width:100%; padding:10px; margin-bottom:16px; border:2px solid #03a9f4; border-radius:6px; font-size:16px; resize:vertical; box-sizing:border-box; }
  input[type="text"]:focus, input[type="email"]:focus, input[type="tel"]:focus, textarea:focus, select:focus { border-color:#0288d1; outline:none; }
  button.submit-btn { width:100%; background-color:#285b88; color:white; padding:14px; border:none; border-radius:8px; cursor:pointer; font-size:1.15em; font-weight:700; transition:background-color .3s ease; }
  button.submit-btn:hover { background-color:#1d416e; }
  button.back-btn { display:block; margin: 0 auto; background:white; color:#0288d1; border:3px solid #03a9f4; border-radius:12px; font-weight:700; padding:12px 50px; cursor:pointer; box-shadow:2px 2px 8px rgba(3,169,244,0.3); transition:background-color .3s ease, color .3s ease; width: max-content; }
  button.back-btn:hover { background-color:#03a9f4; color:white; box-shadow: 2px 2px 12px rgba(3,169,244,0.7); }
  @media (max-width: 950px) {
    .category-list { flex-direction: column; gap: 15px; align-items: center; }
    .service-grid { flex-direction: column; gap: 15px; align-items: center; }
    button.back-btn, button.submit-btn { width: 100%; max-width: 480px; }
  }
</style>
<script>
  let currentFolder = null;
  let currentService = null;

  function showSection(sectionId) {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('packageSection').style.display = 'none';
    document.getElementById('customizedSection').style.display = 'none';
    document.getElementById('premiumSection').style.display = 'none';
    document.getElementById('serviceDisplay').style.display = 'none';
    document.getElementById('contactForm').style.display = 'none';

    if (sectionId === 'packageSection' || sectionId === 'customizedSection' || sectionId === 'premiumSection') {
      document.getElementById(sectionId).style.display = 'block';
      currentFolder = sectionId;
      currentService = null;
    }
    window.scrollTo(0, 0);
  }

  function showServiceDisplay(serviceName) {
    document.getElementById('serviceDisplay').style.display = 'block';
    document.getElementById('contactForm').style.display = 'none';

    const serviceTitle = document.getElementById('serviceTitle');
    serviceTitle.textContent = `Services of ${serviceName}`;

    const servicesGrid = document.getElementById('servicesGrid');
    servicesGrid.innerHTML = '';
    const services = [
      'Decoration', 'Catering', 'Conventions', 'Photography & Videography',
      'Anchor & Actors', 'DJ & Dance & Singers', 'Guest House & Rooms',
      'Chocolate & Cake', 'Games & Entertainment', 'Jewellery',
      'Invitation Cards', 'Vehicles', 'Return Gifts', 'Makeup Artist',
      'Mehandi Artist', 'Clothing & Accessories'
    ];
    services.forEach(s => {
      const div = document.createElement('div');
      div.className = 'service-card';
      div.textContent = s;
      div.onclick = () => showContactForm(s);
      servicesGrid.appendChild(div);
    });
  }

  function showContactForm(serviceName) {
    currentService = serviceName;
    document.getElementById('serviceDisplay').style.display = 'none';
    document.getElementById('contactForm').style.display = 'block';

    document.getElementById('formTitle').textContent = `Contact for ${serviceName}`;
    const budgetDiv = document.getElementById('budgetDiv');
    const capacityDiv = document.getElementById('capacityDiv');
    if (currentFolder === 'customizedSection' || currentFolder === 'packageSection') {
      budgetDiv.style.display = 'block';
      capacityDiv.style.display = 'block';
    } else {
      budgetDiv.style.display = 'none';
      capacityDiv.style.display = 'none';
    }
  }

  function backToFolder() {
    document.getElementById('contactForm').style.display = 'none';
    document.getElementById('serviceDisplay').style.display = 'block';
  }

  function backToMenu() {
    document.getElementById('contactForm').style.display = 'none';
    document.getElementById('serviceDisplay').style.display = 'none';
    document.getElementById('packageSection').style.display = 'none';
    document.getElementById('customizedSection').style.display = 'none';
    document.getElementById('premiumSection').style.display = 'none';
    document.getElementById('mainMenu').style.display = 'block';
    currentFolder = null;
    currentService = null;
  }

  function handleSubmit(event) {
    event.preventDefault();
    const form = event.target;
    const name = form.name.value.trim();
    const email = form.email.value.trim();
    const phone = form.phone.value.trim();
    const message = form.message.value.trim();
    const budget = form.budget ? form.budget.value.trim() : '';
    const capacity = form.capacity ? form.capacity.value.trim() : '';

    if (!name || !email || !phone || !message) {
      alert('Please fill all required fields.');
      return;
    }
    let msgText = `Name: ${name}\nEmail: ${email}\nPhone: ${phone}\nService: ${currentService}\nMessage: ${message}`;
    if (budget) msgText += `\nBudget: ${budget}`;
    if (capacity) msgText += `\nCapacity: ${capacity}`;

    const waURL = `https://wa.me/8977143043?text=${encodeURIComponent(msgText)}`;
    window.open(waURL, '_blank');
    form.reset();
    backToFolder();
  }
</script>
</head>
<body>
  <div class="title-section">JKS Events and Catering Services</div>
  <div class="display-bar">Premium Event & Catering Solutions</div>

  <div id="mainMenu" class="menu-bar">
    <div class="menu-item" onclick="showSection('packageSection')">Package</div>
    <div class="menu-item" onclick="showSection('customizedSection')">Customized</div>
    <div class="menu-item" onclick="showSection('premiumSection')">Premium</div>
  </div>

  <div id="packageSection" class="section" style="display:none;">
    <div class="category-list">
      <div class="category-card" onclick="showServiceDisplay('Silver (50k-160k)')">Silver<br><span class="budget">50,000 - 160,000</span></div>
      <div class="category-card" onclick="showServiceDisplay('Gold (150k-300k)')">Gold<br><span class="budget">150,000 - 300,000</span></div>
      <div class="category-card" onclick="showServiceDisplay('Diamond (500k-5M)')">Diamond<br><span class="budget">500,000 - 5,000,000</span></div>
      <div class="category-card" onclick="showServiceDisplay('Platinum (500k-800k)')">Platinum<br><span class="budget">500,000 - 800,000</span></div>
    </div>
    <button class="back-btn" onclick="backToMenu()">Back to Dashboard</button>
  </div>

  <div id="customizedSection" class="section" style="display:none;">
    <div class="category-list">
      <div class="category-card" onclick="showServiceDisplay('Customized')">All Services <br>(Budget & Capacity)</div>
    </div>
    <button class="back-btn" onclick="backToMenu()">Back to Dashboard</button>
  </div>

  <div id="premiumSection" class="section" style="display:none;">
    <div class="category-list">
      <div class="category-card" onclick="showServiceDisplay('Premium')">All Services (No Budget/Capacity)</div>
    </div>
    <button class="back-btn" onclick="backToMenu()">Back to Dashboard</button>
  </div>

  <div id="serviceDisplay" class="section" style="display:none;">
    <h2 id="serviceTitle" style="text-align:center; margin-bottom: 20px;">Services</h2>
    <div id="servicesGrid" class="service-grid"></div>
    <button class="back-btn" onclick="backToFolder()">Back to Folder</button>
  </div>

  <div id="contactForm" class="form-section" style="display:none;">
    <h2 id="formTitle" style="text-align:center; margin-bottom: 20px;">Contact Form</h2>
    <form onsubmit="handleSubmit(event)">
      <label for="name">Name:</label><input type="text" name="name" id="name" required />
      <label for="email">Email:</label><input type="email" name="email" id="email" required />
      <label for="phone">Phone:</label><input type="tel" name="phone" id="phone" required />
      <label for="message">Message:</label><textarea name="message" id="message" rows="4" required></textarea>
      <div id="budgetDiv" style="margin-bottom: 16px; display:none;">
        <label for="budget">Budget:</label>
        <select name="budget" id="budget" >
          <option value="">Select Budget</option>
          <option value="50,000-100,000">50,000 - 100,000</option>
          <option value="100,001-200,000">100,001 - 200,000</option>
          <option value="200,001-400,000">200,001 - 400,000</option>
          <option value="400,001+">400,001+</option>
        </select>
      </div>
      <div id="capacityDiv" style="margin-bottom: 16px; display:none;">
        <label for="capacity">Capacity:</label>
        <select name="capacity" id="capacity" >
          <option value="">Select Capacity</option>
          <option value="50-100">50 - 100</option>
          <option value="101-200">101 - 200</option>
          <option value="201-500">201 - 500</option>
          <option value="500+">500+</option>
        </select>
      </div>
      <button type="submit" class="submit-btn">Submit via WhatsApp</button>
    </form>
    <button class="back-btn" onclick="backToFolder()">Back to Services</button>
  </div>
</body>
</html>
