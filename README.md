# First-Year-FInal
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>My Academic Result</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Roboto', sans-serif;
    }

    body {
      margin: 0;
      padding: 0;
      background: #f9f9f9;
      color: #333;
    }

    header {
      background-color: #007BFF;
      color: white;
      padding: 1rem;
      text-align: center;
    }

    .logo {
      font-size: 1.5rem;
      font-weight: bold;
    }

    .container {
      max-width: 600px;
      margin: 2rem auto;
      padding: 1rem;
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }

    .login {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    input[type="password"], input[type="text"] {
      padding: 0.75rem;
      border: 1px solid #ccc;
      border-radius: 8px;
    }

    button {
      padding: 0.75rem;
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    .hidden {
      display: none;
    }

    .result-card {
      background: #e9f5ff;
      padding: 1rem;
      border-radius: 12px;
      margin-top: 1rem;
    }

    .subject-list {
      list-style: none;
      padding: 0;
    }

    .subject-list li {
      padding: 0.5rem 0;
      border-bottom: 1px solid #ccc;
    }

    @media (max-width: 600px) {
      .container {
        margin: 1rem;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="logo">1st year final Result</div>
  </header>

  <div class="container">
    <!-- Password Protection -->
    <div id="loginScreen" class="login">
      <input type="password" id="password" placeholder="Enter Password" />
      <button onclick="checkPassword()">Login</button>
    </div>

    <!-- Main Content -->
    <div id="mainContent" class="hidden">
      <input type="text" id="searchId" placeholder="Enter Roll Number / ID" />
      <button onclick="searchResult()">Search</button>

      <div id="resultArea" class="result-card hidden"></div>
    </div>
  </div>

  <script>
    const correctPassword = "1903"; // Change this to your own password

    const results = {
      "6934": {
        name: "Siamun Salah Uddin",
        subjects: {
          Bangla: 82,
          Math: 85,
          English: 82,
          Physics: 86,
          Chemistry: 78,
          Biology: 92,
          ICT: 86
        },
        total: 591,
        percentage: 84.43,
        gpa: 5.00
      },
      "1002": {
        name: "Bob Smith",
        subjects: {
          Math: 75,
          English: 82,
          Science: 88
        },
        total: 245,
        percentage: 81.67,
        gpa: 3.8
      }
    };

    function checkPassword() {
      const input = document.getElementById("password").value;
      if (input === correctPassword) {
        document.getElementById("loginScreen").classList.add("hidden");
        document.getElementById("mainContent").classList.remove("hidden");
      } else {
        alert("Incorrect password!");
      }
    }

    function searchResult() {
      const id = document.getElementById("searchId").value.trim();
      const result = results[id];
      const area = document.getElementById("resultArea");

      if (result) {
        const subjectsHtml = Object.entries(result.subjects)
          .map(([subject, mark]) => `<li>${subject}: ${mark}</li>`)
          .join("");

        area.innerHTML = `
          <h3>${result.name} (ID: ${id})</h3>
          <ul class="subject-list">
            ${subjectsHtml}
          </ul>
          <p><strong>Total:</strong> ${result.total}</p>
          <p><strong>Percentage:</strong> ${result.percentage}%</p>
          <p><strong>GPA:</strong> ${result.gpa}</p>
        `;
        area.classList.remove("hidden");
      } else {
        area.innerHTML = `<p>No result found for ID: ${id}</p>`;
        area.classList.remove("hidden");
      }
    }
  </script>
</body>
</html>
