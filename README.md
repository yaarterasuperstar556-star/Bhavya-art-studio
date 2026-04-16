<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bhavya Art Studio - ArtShare Community</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .navbar {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: 0 2px 20px rgba(0,0,0,0.1);
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .nav-logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #667eea;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .nav-links {
            display: flex;
            gap: 1rem;
            align-items: center;
        }

        .nav-link {
            color: #333;
            text-decoration: none;
            padding: 0.5rem 1rem;
            border-radius: 25px;
            transition: all 0.3s ease;
        }

        .nav-link:hover, .nav-link.active {
            background: #667eea;
            color: white;
        }

        .login-btn {
            background: #667eea;
            color: white;
            border: none;
            padding: 0.7rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            transition: all 0.3s ease;
        }

        .login-btn:hover {
            background: #5a67d8;
            transform: translateY(-2px);
        }

        .main-container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 120px 2rem 2rem;
            min-height: calc(100vh - 140px);
        }

        .section {
            display: none;
        }

        .section.active {
            display: block;
        }

        .section-header {
            text-align: center;
            margin-bottom: 3rem;
        }

        .section-header h1 {
            font-size: 3rem;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 1rem;
        }

        .owner-badge {
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            color: white;
            padding: 0.5rem 1.5rem;
            border-radius: 25px;
            font-weight: bold;
            display: inline-block;
            margin-bottom: 1rem;
            box-shadow: 0 5px 15px rgba(255,107,107,0.3);
        }

        .artwork-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 2rem;
        }

        .artwork-card {
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .artwork-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }

        .artwork-image {
            width: 100%;
            height: 250px;
            object-fit: cover;
            background: #f0f0f0;
        }

        .artwork-info {
            padding: 1.5rem;
        }

        .artwork-title {
            font-size: 1.3rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
            color: #333;
        }

        .artist-name {
            color: #667eea;
            font-weight: 500;
            margin-bottom: 0.5rem;
        }

        .artwork-description {
            color: #666;
            margin-bottom: 1rem;
            line-height: 1.5;
        }

        .artwork-stats {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.9rem;
            color: #888;
        }

        .upload-form {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 3rem;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }

        .upload-area {
            border: 3px dashed #667eea;
            border-radius: 15px;
            padding: 3rem;
            text-align: center;
            margin-bottom: 2rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .upload-area:hover {
            background: #f8f9ff;
        }

        .upload-area i {
            font-size: 3rem;
            color: #667eea;
            margin-bottom: 1rem;
        }

        #artworkFile {
            display: none;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 1rem;
            border: 2px solid #e1e5e9;
            border-radius: 10px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
        }

        .btn {
            width: 100%;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 1rem;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.4);
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 2rem;
            border-radius: 20px;
            width: 90%;
            max-width: 500px;
            position: relative;
            animation: modalSlideIn 0.3s ease;
            max-height: 90vh;
            overflow-y: auto;
        }

        .close {
            position: absolute;
            right: 1.5rem;
            top: 1.5rem;
            font-size: 2rem;
            cursor: pointer;
            color: #999;
        }

        .close:hover {
            color: #333;
        }

        .loading {
            grid-column: 1 / -1;
            text-align: center;
            padding: 3rem;
            color: #666;
            font-size: 1.2rem;
        }

        .profile-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: white;
            padding: 2rem;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        @keyframes modalSlideIn {
            from { opacity: 0; transform: translateY(-50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @media (max-width: 768px) {
            .nav-container {
                flex-direction: column;
                gap: 1rem;
            }
            .artwork-grid {
                grid-template-columns: 1fr;
            }
            .section-header h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar">
        <div class="nav-container">
            <div class="nav-logo">
                <i class="fas fa-palette"></i>
                <span>Bhavya Art Studio</span>
            </div>
            <div class="nav-links" id="navLinks">
                <a href="#" class="nav-link active" onclick="showSection('feed')">Feed</a>
                <a href="#" class="nav-link" onclick="showSection('upload')">Upload</a>
                <a href="#" class="nav-link" onclick="showSection('profile')">Profile</a>
                <button class="login-btn" id="loginBtn">
                    <i class="fas fa-sign-in-alt"></i> Login
                </button>
            </div>
        </div>
    </nav>

    <!-- Auth Modal -->
    <div id="authModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeAuthModal()">&times;</span>
            <div id="loginForm">
                <h2><i class="fas fa-user-lock"></i> Login to Bhavya Art Studio</h2>
                <div class="owner-badge">👑 Owner: Bhavya Art Studio</div>
                <div class="form-group">
                    <input type="email" id="email" placeholder="📧 Email" required>
                </div>
                <div class="form-group">
                    <input type="password" id="password" placeholder="🔒 Password" required>
                </div>
                <button class="btn" onclick="loginUser()">Login</button>
                <p style="text-align: center; margin-top: 1rem;">
                    Don't have an account? <a href="#" onclick="showSignup()" style="color: #667eea; font-weight: bold;">Sign up</a>
                </p>
            </div>
            <div id="signupForm" style="display: none;">
                <h2><i class="fas fa-user-plus"></i> Join Bhavya Art Community</h2>
                <div class="form-group">
                    <input type="text" id="displayName" placeholder="🎨 Display Name" required>
                </div>
                <div class="form-group">
                    <input type="email" id="signupEmail" placeholder="📧 Email" required>
                </div>
                <div class="form-group">
                    <input type="password" id="signupPassword" placeholder="🔒 Password" required>
                </div>
                <button class="btn" onclick="signupUser()">Create Account</button>
                <p style="text-align: center; margin-top: 1rem;">
                    Have an account? <a href="#" onclick="showLogin()" style="color: #667eea; font-weight: bold;">Login</a>
                </p>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <main class="main-container">
        <!-- Feed Section -->
        <section id="feed" class="section active">
            <div class="section-header">
                <h1>🎨 Art Feed</h1>
                <p>Discover amazing artworks from Bhavya Art Community</p>
                <div class="owner-badge">Managed by Bhavya Art Studio</div>
            </div>
            <div class="artwork-grid" id="artworkGrid">
                <div class="loading">
                    <i class="fas fa-spinner fa-spin"></i><br>
                    Loading artworks...
                </div>
            </div>
        </section>

        <!-- Upload Section -->
        <section id="upload" class="section">
            <div class="section-header">
                <h1>📤 Share Your Artwork</h1>
                <p>Upload your creativity to Bhavya Art Community</p>
            </div>
            <form id="uploadForm" class="upload-form">
                <div class="upload-area" id="uploadArea">
                    <i class="fas fa-cloud-upload-alt"></i>
                    <p>Drag & drop your artwork or click to browse</p>
                    <input type="file" id="artworkFile" accept="image/*">
                </div>
                <div class="form-group">
                    <input type="text" id="artworkTitle" placeholder="🎨 Artwork Title" required>
                </div>
                <div class="form-group">
                    <textarea id="artworkDescription" rows="4" placeholder="✍️ Description (optional)"></textarea>
                </div>
                <button type="submit" class="btn">🚀 Share Artwork</button>
            </form>
        </section>

        <!-- Profile Section -->
        <section id="profile" class="section">
            <div class="section-header">
                <h1>👤 Your Profile</h1>
            </div>
            <div id="profileContent">
                <div class="loading">Please login to view your profile</div>
            </div>
        </section>
    </main>

    <script>
        // Global variables
        let currentUser = JSON.parse(localStorage.getItem('currentUser')) || null;
        let artworks = JSON.parse(localStorage.getItem('artworks')) || [];
        let nextId = parseInt(localStorage.getItem('nextId')) || 1;

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateUI();
            loadArtworks();
            initDragDrop();
            document.getElementById('uploadForm').addEventListener('submit', handleUpload);
        });

        // Update UI
        function updateUI() {
            const loginBtn = document.getElementById('loginBtn');
            if (currentUser) {
                loginBtn.innerHTML = `<i class="fas fa-user"></i> ${currentUser.displayName}`;
                loginBtn.onclick = showProfile;
                document.querySelector('.upload-form').style.display = 'block';
            } else {
                loginBtn.innerHTML = `<i class="fas fa-sign-in-alt"></i> Login`;
                loginBtn.onclick = showAuthModal;
                document.querySelector('.upload-form').style.display = 'none';
            }
        }

        // Navigation
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('active');
            });
            document.getElementById(sectionId).classList.add('active');
            event.target.classList.add('active');
            
            if (sectionId === 'feed') loadArtworks();
            if (sectionId === 'profile') loadUserProfile();
        }

        // Auth Modal
        function showAuthModal() {
            document.getElementById('authModal').style.display = 'block';
        }

        function closeAuthModal() {
            document.getElementById('authModal').style.display = 'none';
            showLogin();
        }

        function showSignup() {
            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('signupForm').style.display = 'block';
        }

        function showLogin() {
            document.getElementById('signupForm').style.display = 'none';
            document.getElementById('loginForm').style.display = 'block';
        }

        // Login
        function loginUser() {
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            
            // Demo users (including owner)
            const demoUsers = [
                { email: 'bhavya@bhavyaartstudio.com', password: 'bhavya123', displayName: 'Bhavya Art Studio 👑' },
                { email: 'artist1@example.com', password: '123456', displayName: 'Creative Soul' },
                { email: 'artist2@example.com', password: '123456', displayName: 'Digital Dreamer' }
            ];
            
            const user = demoUsers.find(u => u.email === email && u.password === password);
            if (user) {
                currentUser = user;
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                updateUI();
                closeAuthModal();
                loadUserProfile();
                alert('✅ Welcome to Bhavya Art Studio!');
            } else {
                alert('❌ Invalid email or password');
            }
        }

        // Signup
        function signupUser() {
            const displayName = document.getElementById('displayName').value;
            const email = document.getElementById('signupEmail').value;
            const password = document.getElementById('signupPassword').value;
            
            if (displayName && email && password.length >= 6) {
                currentUser = { displayName, email, password, id: Date.now() };
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                updateUI();
                closeAuthModal();
                alert('🎉 Account created successfully!');
            } else {
