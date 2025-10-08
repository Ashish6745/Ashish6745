<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ashish Pawar - 3D Portfolio</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0a0e27 0%, #1a1d3e 100%);
            overflow-x: hidden;
            color: white;
        }

        #canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            z-index: 1;
        }

        .content-overlay {
            position: relative;
            z-index: 2;
            pointer-events: none;
        }

        .hero-section {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
        }

        h1 {
            font-size: 4rem;
            font-weight: 800;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 1rem;
            animation: fadeInDown 1s ease-out;
        }

        .subtitle {
            font-size: 1.5rem;
            color: #a0aec0;
            margin-bottom: 2rem;
            animation: fadeInUp 1s ease-out 0.3s both;
        }

        .tech-stack {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
            animation: fadeInUp 1s ease-out 0.6s both;
        }

        .tech-badge {
            background: rgba(102, 126, 234, 0.2);
            backdrop-filter: blur(10px);
            padding: 10px 20px;
            border-radius: 25px;
            border: 2px solid rgba(102, 126, 234, 0.3);
            font-weight: 600;
            pointer-events: auto;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .tech-badge:hover {
            background: rgba(102, 126, 234, 0.4);
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
        }

        .cards-section {
            min-height: 100vh;
            padding: 100px 20px;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .project-card {
            background: rgba(26, 29, 62, 0.7);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            border: 2px solid rgba(102, 126, 234, 0.2);
            transition: all 0.4s ease;
            pointer-events: auto;
            cursor: pointer;
        }

        .project-card:hover {
            transform: translateY(-10px);
            border-color: rgba(102, 126, 234, 0.6);
            box-shadow: 0 20px 60px rgba(102, 126, 234, 0.3);
        }

        .project-card h3 {
            color: #667eea;
            font-size: 1.5rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .project-card p {
            color: #a0aec0;
            line-height: 1.6;
            margin-bottom: 15px;
        }

        .project-tags {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 15px;
        }

        .tag {
            background: rgba(102, 126, 234, 0.3);
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.85rem;
            color: #e0e7ff;
        }

        .stats-section {
            padding: 100px 20px;
            text-align: center;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            max-width: 1000px;
            margin: 50px auto;
        }

        .stat-card {
            background: rgba(26, 29, 62, 0.7);
            backdrop-filter: blur(10px);
            padding: 30px;
            border-radius: 15px;
            border: 2px solid rgba(102, 126, 234, 0.2);
            pointer-events: auto;
        }

        .stat-number {
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .stat-label {
            color: #a0aec0;
            margin-top: 10px;
            font-size: 1.1rem;
        }

        .cta-section {
            text-align: center;
            padding: 100px 20px;
        }

        .cta-button {
            display: inline-block;
            padding: 15px 40px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            text-decoration: none;
            border-radius: 50px;
            font-weight: 600;
            font-size: 1.2rem;
            transition: all 0.3s ease;
            pointer-events: auto;
            border: none;
            cursor: pointer;
            margin: 10px;
        }

        .cta-button:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 40px rgba(102, 126, 234, 0.4);
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .scroll-indicator {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            animation: bounce 2s infinite;
            pointer-events: auto;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {
                transform: translateX(-50%) translateY(0);
            }
            40% {
                transform: translateX(-50%) translateY(-10px);
            }
            60% {
                transform: translateX(-50%) translateY(-5px);
            }
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            .subtitle {
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div id="canvas-container"></div>

    <div class="content-overlay">
        <section class="hero-section">
            <h1>ASHISH PAWAR</h1>
            <p class="subtitle">Full-Stack Mobile Developer | Flutter & Node.js Expert</p>
            <div class="tech-stack">
                <span class="tech-badge">📱 Flutter</span>
                <span class="tech-badge">⚡ Node.js</span>
                <span class="tech-badge">🔥 Firebase</span>
                <span class="tech-badge">🎨 Dart</span>
                <span class="tech-badge">💾 MongoDB</span>
            </div>
            <div class="scroll-indicator">
                <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#667eea" stroke-width="2">
                    <path d="M12 5v14M19 12l-7 7-7-7"/>
                </svg>
            </div>
        </section>

        <section class="stats-section">
            <h2 style="font-size: 2.5rem; margin-bottom: 20px;">🚀 Impact & Contributions</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-number">50+</div>
                    <div class="stat-label">Projects Built</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">500+</div>
                    <div class="stat-label">Commits</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">10+</div>
                    <div class="stat-label">Technologies</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">100+</div>
                    <div class="stat-label">Stars Earned</div>
                </div>
            </div>
        </section>

        <section class="cards-section">
            <div class="project-card">
                <h3>📱 Flutter GetX Architecture</h3>
                <p>Production-ready scalable app architecture with advanced state management patterns and clean code principles.</p>
                <div class="project-tags">
                    <span class="tag">Flutter</span>
                    <span class="tag">GetX</span>
                    <span class="tag">Dart</span>
                </div>
            </div>

            <div class="project-card">
                <h3>💬 Real-time Chat App</h3>
                <p>Instant messaging platform with Firebase backend, push notifications, media sharing, and end-to-end encryption.</p>
                <div class="project-tags">
                    <span class="tag">Flutter</span>
                    <span class="tag">Firebase</span>
                    <span class="tag">Real-time</span>
                </div>
            </div>

            <div class="project-card">
                <h3>🔗 URL Shortener API</h3>
                <p>High-performance URL shortening service with analytics dashboard, custom aliases, and QR code generation.</p>
                <div class="project-tags">
                    <span class="tag">Node.js</span>
                    <span class="tag">Express</span>
                    <span class="tag">MongoDB</span>
                </div>
            </div>

            <div class="project-card">
                <h3>📊 Project Management Tool</h3>
                <p>Collaborative workspace with real-time updates, task tracking, team collaboration, and progress analytics.</p>
                <div class="project-tags">
                    <span class="tag">MERN</span>
                    <span class="tag">WebSocket</span>
                    <span class="tag">REST API</span>
                </div>
            </div>

            <div class="project-card">
                <h3>🎨 Portfolio Maker</h3>
                <p>Dynamic portfolio generator with customizable templates, drag-and-drop builder, and instant deployment.</p>
                <div class="project-tags">
                    <span class="tag">Node.js</span>
                    <span class="tag">EJS</span>
                    <span class="tag">Express</span>
                </div>
            </div>

            <div class="project-card">
                <h3>✅ Task Manager Pro</h3>
                <p>Offline-first task management app with cloud sync, priority scheduling, and productivity insights.</p>
                <div class="project-tags">
                    <span class="tag">Flutter</span>
                    <span class="tag">SQLite</span>
                    <span class="tag">Provider</span>
                </div>
            </div>
        </section>

        <section class="cta-section">
            <h2 style="font-size: 2.5rem; margin-bottom: 30px;">Let's Build Something Amazing! 🚀</h2>
            <p style="color: #a0aec0; font-size: 1.2rem; margin-bottom: 40px;">Open for collaborations and exciting projects</p>
            <a href="https://github.com/Ashish6745" class="cta-button" target="_blank">View GitHub</a>
            <a href="https://www.linkedin.com/in/ashish6745" class="cta-button" target="_blank">Connect on LinkedIn</a>
        </section>
    </div>

    <script type="importmap">
        {
            "imports": {
                "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js"
            }
        }
    </script>
    <script type="module">
        import * as THREE from 'three';

        // Scene setup
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        document.getElementById('canvas-container').appendChild(renderer.domElement);

        // Lighting
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
        scene.add(ambientLight);

        const pointLight1 = new THREE.PointLight(0x667eea, 2, 100);
        pointLight1.position.set(10, 10, 10);
        scene.add(pointLight1);

        const pointLight2 = new THREE.PointLight(0x764ba2, 2, 100);
        pointLight2.position.set(-10, -10, 10);
        scene.add(pointLight2);

        // Create floating particles
        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 1000;
        const posArray = new Float32Array(particlesCount * 3);

        for(let i = 0; i < particlesCount * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 100;
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.15,
            color: 0x667eea,
            transparent: true,
            opacity: 0.8
        });

        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        // Create rotating geometric shapes
        const geometry1 = new THREE.TorusKnotGeometry(3, 1, 100, 16);
        const material1 = new THREE.MeshPhongMaterial({
            color: 0x667eea,
            wireframe: true,
            transparent: true,
            opacity: 0.3
        });
        const torusKnot = new THREE.Mesh(geometry1, material1);
        torusKnot.position.set(-15, 0, -20);
        scene.add(torusKnot);

        const geometry2 = new THREE.IcosahedronGeometry(4, 0);
        const material2 = new THREE.MeshPhongMaterial({
            color: 0x764ba2,
            wireframe: true,
            transparent: true,
            opacity: 0.3
        });
        const icosahedron = new THREE.Mesh(geometry2, material2);
        icosahedron.position.set(15, 0, -20);
        scene.add(icosahedron);

        // Create app icons (mobile phones)
        const createPhone = (x, y, z) => {
            const phoneGroup = new THREE.Group();
            
            const screenGeometry = new THREE.BoxGeometry(2, 3, 0.2);
            const screenMaterial = new THREE.MeshPhongMaterial({ color: 0x667eea });
            const screen = new THREE.Mesh(screenGeometry, screenMaterial);
            
            const frameGeometry = new THREE.BoxGeometry(2.2, 3.2, 0.3);
            const frameMaterial = new THREE.MeshPhongMaterial({ color: 0x1a1d3e });
            const frame = new THREE.Mesh(frameGeometry, frameMaterial);
            frame.position.z = -0.05;
            
            phoneGroup.add(screen);
            phoneGroup.add(frame);
            phoneGroup.position.set(x, y, z);
            
            return phoneGroup;
        };

        const phone1 = createPhone(-8, 5, -15);
        const phone2 = createPhone(8, -5, -15);
        const phone3 = createPhone(0, 8, -18);
        scene.add(phone1, phone2, phone3);

        camera.position.z = 30;

        // Mouse interaction
        let mouseX = 0;
        let mouseY = 0;

        document.addEventListener('mousemove', (e) => {
            mouseX = (e.clientX / window.innerWidth) * 2 - 1;
            mouseY = -(e.clientY / window.innerHeight) * 2 + 1;
        });

        // Animation
        let time = 0;
        function animate() {
            requestAnimationFrame(animate);
            time += 0.01;

            // Rotate shapes
            torusKnot.rotation.x += 0.01;
            torusKnot.rotation.y += 0.01;
            
            icosahedron.rotation.x += 0.01;
            icosahedron.rotation.z += 0.01;

            // Animate phones
            phone1.rotation.y = Math.sin(time) * 0.3;
            phone2.rotation.y = Math.cos(time) * 0.3;
            phone3.rotation.x = Math.sin(time * 0.5) * 0.2;

            // Particle animation
            particlesMesh.rotation.y += 0.001;
            particlesMesh.rotation.x += 0.0005;

            // Camera movement based on mouse
            camera.position.x += (mouseX * 5 - camera.position.x) * 0.05;
            camera.position.y += (mouseY * 5 - camera.position.y) * 0.05;
            camera.lookAt(scene.position);

            // Light movement
            pointLight1.position.x = Math.sin(time) * 15;
            pointLight1.position.y = Math.cos(time) * 15;
            
            pointLight2.position.x = Math.cos(time) * 15;
            pointLight2.position.y = Math.sin(time) * 15;

            renderer.render(scene, camera);
        }

        animate();

        // Handle window resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // Scroll effects
        window.addEventListener('scroll', () => {
            const scrollY = window.scrollY;
            camera.position.z = 30 + scrollY * 0.01;
            torusKnot.rotation.z = scrollY * 0.001;
            icosahedron.rotation.z = -scrollY * 0.001;
        });
    </script>
</body>
</html>
