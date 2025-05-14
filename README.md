from zipfile import ZipFile
import os

# Re-creating the base directory after code execution environment reset
base_dir = "/mnt/data/you_are_not_alone_website"
os.makedirs(base_dir, exist_ok=True)

# HTML content
index_html = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>You Are Not Alone</title>
    <link rel="stylesheet" href="style.css">
    <script defer src="script.js"></script>
</head>
<body>
    <div class="sidebar">
        <h2>Explore</h2>
        <ul>
            <li><a href="#citations">APA Citations</a></li>
            <li><a href="#books">Books</a></li>
            <li><a href="#messages">Kind Messages</a></li>
            <li><a href="#counselor">Talk to Someone</a></li>
        </ul>
    </div>
    <div class="main-content">
        <h1>Welcome to <em>You Are Not Alone</em></h1>
        <div class="survey">
            <h2>How Are You Feeling Today?</h2>
            <button class="emoji">😢</button>
            <button class="emoji">😐</button>
            <button class="emoji">😊</button>
        </div>
        <div class="quote-box">
            <h3>Daily Motivation</h3>
            <p id="quote">Your feelings are valid</p>
            <button onclick="newQuote()">New Quote</button>
        </div>
        <div class="reward-center">
            <h3>Reward Center</h3>
            <p>Keep coming back to earn badges!</p>
        </div>
        <div id="citations" class="section">
            <h3>APA Citations</h3>
            <p>Serrano-Ibanez, E. R., et al. (2018)...</p>
            <p>Wildes, J. E., et al. (2010)...</p>
            <p>Mian, N. D., et al. (2025)...</p>
            <p>Kraft, L., et al. (2023)...</p>
        </div>
        <div id="books" class="section">
            <h3>Books for Kids</h3>
            <ul>
                <li>"Ruby Finds a Worry" by Tom Percival</li>
                <li>"My Many Colored Days" by Dr. Seuss</li>
            </ul>
        </div>
        <div id="messages" class="section">
            <h3>Kind Messages</h3>
            <p>“You are enough.”</p>
            <p>“It’s okay to ask for help.”</p>
        </div>
        <div id="counselor" class="section">
            <h3>Need to Talk?</h3>
            <p><a href="https://www.betterhelp.com" target="_blank">Find a Counselor</a></p>
        </div>
    </div>
</body>
</html>
"""

# CSS content
style_css = """
body {
    font-family: 'Comic Sans MS', cursive, sans-serif;
    background-color: #f0f8ff;
    margin: 0;
    display: flex;
}
.sidebar {
    width: 220px;
    background-color: #add8e6;
    padding: 20px;
    height: 100vh;
    position: fixed;
}
.sidebar h2 {
    color: #333;
}
.sidebar ul {
    list-style-type: none;
    padding: 0;
}
.sidebar li {
    margin: 10px 0;
}
.sidebar a {
    color: #000;
    text-decoration: none;
}
.main-content {
    margin-left: 240px;
    padding: 20px;
}
.emoji {
    font-size: 2em;
    margin: 5px;
}
.quote-box, .reward-center {
    margin-top: 20px;
    background-color: #fff8dc;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}
.section {
    margin-top: 30px;
}
"""

# JavaScript content
script_js = """
function newQuote() {
    const quotes = [
        "Your feelings are valid",
        "You are enough",
        "Don’t be so hard on yourself",
        "It’s okay to reach out for help",
        "Fill your mind with mindfulness"
    ];
    const quoteBox = document.getElementById("quote");
    const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
    quoteBox.textContent = randomQuote;
}
"""

# Write files to the directory
with open(os.path.join(base_dir, "index.html"), "w") as f:
    f.write(index_html)

with open(os.path.join(base_dir, "style.css"), "w") as f:
    f.write(style_css)

with open(os.path.join(base_dir, "script.js"), "w") as f:
    f.write(script_js)

# Create a zip file of the directory
zip_path = "/mnt/data/you_are_not_alone_website.zip"
with ZipFile(zip_path, 'w') as zipf:
    for root, dirs, files in os.walk(base_dir):
        for file in files:
            file_path = os.path.join(root, file)
            arcname = os.path.relpath(file_path, base_dir)
            zipf.write(file_path, arcname)

zip_path
