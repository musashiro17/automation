<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Stage 1 Form</title>
</head>
<body>
  <h2>Stage 1: User Info</h2>
  <form id="stage1Form" action="https://musashiro17.app.n8n.cloud/webhook-test/provision/stage1" method="POST">
    <label>Proposed Alias:</label>
    <input type="text" name="proposedAlias" value="john.doe" required><br><br>

    <label>Manager Email:</label>
    <input type="email" name="managerEmail" value="tmanager@sistosocompany.onmicrosoft.com" required><br><br>

    <label>Department:</label>
    <input type="text" name="department" value="IT" required><br><br>

    <label>Location:</label>
    <input type="text" name="location" value="HQ" required><br><br>

    <!-- Hidden fields -->
    <input type="hidden" name="csrf" value="vn1OCCArNpwoqwEi8lBa">
    <input type="hidden" name="hp" value="">
    
    <button type="submit">Submit Stage 1</button>
  </form>

  <script>
document.getElementById("stage1Form").addEventListener("submit", function(e) {
  e.preventDefault();

  function generateCSRF(length = 20) {
    const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    let token = '';
    for (let i = 0; i < length; i++) {
      token += chars.charAt(Math.floor(Math.random() * chars.length));
    }
    return token;
  }

  const payload = {
    csrf: generateCSRF(),
    hp: "",
    proposedAlias: document.getElementById("proposedAlias").value,
    managerEmail: document.getElementById("managerEmail").value,
    department: document.getElementById("department").value,
    location: document.getElementById("location").value
  };

  // Send to Stage 1 webhook
  fetch("https://musashiro17.app.n8n.cloud/webhook-test/provision/stage1", {
    method: "POST",
    headers: {"Content-Type": "application/json"},
    body: JSON.stringify(payload)
  })
  .then(response => response.json())
  .then(data => {
    // Save Stage 1 data in localStorage for Stage 2
    localStorage.setItem("stage1Data", JSON.stringify(payload));

    // Redirect to Stage 2 form page
    window.location.href = "";
  })
  .catch(err => alert("Error submitting form"));
});
</script>
</body>
</html>
