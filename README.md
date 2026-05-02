# Login-app
All websites in one app
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Login App</title>

<style>
* {
    box-sizing: border-box;
}

body {
    font-family: Arial;
    background: linear-gradient(135deg, #4facfe, #00f2fe);
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
}

.container {
    background: white;
    padding: 20px;
    border-radius: 15px;
    width: 90%;
    max-width: 350px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
    animation: fadeIn 0.5s ease;
}

input, button, select {
    width: 100%;
    padding: 12px;
    margin: 10px 0;
    font-size: 16px;
    border-radius: 8px;
}

input {
    border: 1px solid #ccc;
}

button {
    background-color: #4facfe;
    color: white;
    border: none;
    cursor: pointer;
}

button:hover {
    background-color: #3b8edc;
}

.logout {
    background: red;
}

.logo {
    width: 80px;
    display: block;
    margin: 0 auto 10px;
}

@keyframes fadeIn {
    from {opacity: 0; transform: translateY(20px);} 
    to {opacity: 1; transform: translateY(0);} 
}
</style>

<script>

function addLogo(containerId) {
    const container = document.getElementById(containerId);
    const img = document.createElement("img");
    img.src = "imageess.jpg";
    img.className = "logo";
    container.prepend(img);
}

function registerUser(event) {
    event.preventDefault();

    const name = document.getElementById("regName").value.trim();
    const password = document.getElementById("regPassword").value.trim();

    if(name && password) {
        localStorage.setItem("user", JSON.stringify({name, password}));
        alert("Account created! Please login.");
        showLogin();
    }
}

function loginUser(event) {
    event.preventDefault();

    const name = document.getElementById("name").value.trim();
    const password = document.getElementById("password").value.trim();

    const savedUser = JSON.parse(localStorage.getItem("user"));

    if(savedUser && name === savedUser.name && password === savedUser.password) {
        localStorage.setItem("loggedIn", name);
        showApp(name);
    } else {
        alert("Invalid Username or Password ❌");
    }
}

function showLogin() {
    document.getElementById("registerSection").style.display = "none";
    document.getElementById("loginSection").style.display = "block";
    document.getElementById("selectSection").style.display = "none";
}

function showRegister() {
    document.getElementById("loginSection").style.display = "none";
    document.getElementById("registerSection").style.display = "block";
}


function showApp(name) {
    document.getElementById("loginSection").style.display = "none";
    document.getElementById("registerSection").style.display = "none";
    document.getElementById("selectSection").style.display = "block";
    document.getElementById("welcome").innerText = "Welcome, " + name + "!";
}

function logout() {
    localStorage.removeItem("loggedIn");
    showLogin(); // ✅ Go back to login page (no reload)
}

function openWebsite() {
    const url = document.getElementById("websiteSelect").value;
    if(url) {
        window.open(url, "_blank");
    } else {
        alert("Select a website");
    }
}
window.onload = function () {
    addLogo("loginSection");
    addLogo("registerSection");
    addLogo("selectSection");

    const loggedIn = localStorage.getItem("loggedIn");

    if(loggedIn) {
        showApp(loggedIn);
    } else {
        showLogin(); // ✅ Default to login page
    }
};
</script>

</head>

<body>
<div class="container" id="registerSection">
    <h2>Create Account</h2>
    <form onsubmit="registerUser(event)">
        <input type="text" id="regName" placeholder="Username" required>
        <input type="password" id="regPassword" placeholder="Create Password" required>
        <button type="submit">Register</button>
        <button type="button" onclick="showLogin()">Back to Login</button>
    </form>
</div>
<div class="container" id="loginSection" style="display:none;">
    <h2>Login</h2>
    <form onsubmit="loginUser(event)">
        <input type="text" id="name" placeholder="Username" required>
        <input type="password" id="password" placeholder="Password" required>
        <button type="submit">Login</button>
        <button type="button" onclick="showRegister()">Create Account</button>
    </form>
</div>

<div class="container" id="selectSection" style="display:none;">
    <h2 id="welcome">Welcome!</h2>

    <select id="websiteSelect">
        <option value="">--Select Website--</option>
        <option value="https://www.google.com">Google</option>
        <option value="https://www.instagram.com">Instagram</option>
        <option value="https://sites.google.com/cambridge.edu.in/4th-sem--subject-sphere?usp=sharing">Cambridge college notes</option>
        <option value="https://www.facebook.com">Facebook</option>
        <option value="https://www.youtube.com/">YouTube</option>
        <option value="https://chatgpt.com/">ChatGPT</option>
        <option value="https://student.citexams.in/">Cambridge college ERP portal</option>
        <option value="https://hotstar.com">JioHotstar</option>
        <option value="https://docs.google.com/spreadsheets/u/1/d/12j2cTXxuZ0QcFZPF08dNkbqmR3NWJtESq9gq1ns-DzI/htmlview">Assessment sheet</option>
        <option value="https://www.codedpad.com">CodedPad</option>
    </select>

    <button onclick="openWebsite()">Open</button>
    <button class="logout" onclick="logout()">Logout</button>
</div>

</body>
</html>
