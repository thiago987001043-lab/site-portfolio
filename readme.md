<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Thiago Santana | Senior-Level Front-End Developer Portfolio</title>

    <style>
        /* --- CORE CONFIG & DESIGN SYSTEM (TAILWIND SEMANTICS) --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            scroll-behavior: smooth;
        }

        :root {
            --primary: #3b82f6;       /* Tailwind blue-500 */
            --secondary: #60a5fa;     /* Tailwind blue-400 */
            --bg-main: #030712;       /* Tailwind gray-950 */
            --bg-gradient: #0b1528;
            --text-main: #f9fafb;     /* Tailwind gray-50 */
            --text-muted: #9ca3af;    /* Tailwind gray-400 */
            --card-bg: rgba(17, 24, 39, 0.4);
            --card-border: rgba(255, 255, 255, 0.05);
            --nav-bg: rgba(3, 7, 18, 0.6);
            --circle-color: rgba(59, 130, 246, 0.12);
            --footer-bg: #030712;
            --shadow-glow: rgba(59, 130, 246, 0.15);
        }

        body.light-theme {
            --bg-main: #ffffff;
            --bg-gradient: #f0f7ff;   /* Fundo interativo azul claro suave */
            --text-main: #0f172a;     /* Tailwind slate-900 */
            --text-muted: #475569;    /* Tailwind slate-600 */
            --card-bg: rgba(255, 255, 255, 0.7);
            --card-border: rgba(59, 130, 246, 0.15);
            --nav-bg: rgba(255, 255, 255, 0.7);
            --circle-color: rgba(59, 130, 246, 0.18);
            --footer-bg: #f8fafc;
            --shadow-glow: rgba(59, 130, 246, 0.08);
        }

        body {
            background: linear-gradient(135deg, var(--bg-main), var(--bg-gradient));
            color: var(--text-main);
            overflow-x: hidden;
            line-height: 1.6;
            transition: background 0.6s ease, color 0.6s ease;
            perspective: 1000px; /* Habilita o ambiente de renderização 3D no site */
        }

        /* --- CONTROLES DE INTERFACE --- */
        .theme-toggle {
            position: fixed;
            top: 25px;
            right: 25px;
            z-index: 1000;
            background: var(--nav-bg);
            border: 1px solid var(--card-border);
            color: var(--text-main);
            padding: 12px 20px;
            border-radius: 50px;
            cursor: pointer;
            backdrop-filter: blur(12px);
            font-weight: 600;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 10px 25px -5px rgba(0,0,0,0.1);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .theme-toggle:hover {
            transform: translateY(-2px);
            border-color: var(--primary);
            box-shadow: 0 0 15px var(--shadow-glow);
        }

        /* --- ENGINE GRÁFICA DE FUNDO (INTERACTIVE PARALLAX) --- */
        .bg-engine {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: 0;
            pointer-events: none;
        }

        .blur-sphere {
            position: absolute;
            border-radius: 50%;
            background: var(--circle-color);
            filter: blur(40px);
            transition: transform 0.15s ease-out, background 0.6s ease;
            will-change: transform;
        }

        .blur-sphere:nth-child(1) { width: 450px; height: 450px; top: -10%; left: -5%; }
        .blur-sphere:nth-child(2) { width: 350px; height: 350px; bottom: 5%; right: -5%; }
        .blur-sphere:nth-child(3) { width: 250px; height: 250px; top: 45%; left: 35%; }

        /* --- HEADER & NAVIGATION --- */
        header {
            width: 100%;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 24px;
            position: relative;
        }

        nav {
            position: absolute;
            top: 25px;
            z-index: 10;
            display: flex;
            gap: 24px;
            background: var(--nav-bg);
            padding: 12px 36px;
            border-radius: 50px;
            backdrop-filter: blur(12px);
            border: 1px solid var(--card-border);
            transition: all 0.5s ease;
        }

        nav a {
            color: var(--text-muted);
            text-decoration: none;
            font-weight: 500;
            transition: 0.3s;
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

        nav a:hover { color: var(--primary); }

        .hero {
            position: relative;
            z-index: 2;
            max-width: 850px;
            transform-style: preserve-3d;
        }

        .hero h1 {
            font-size: 4.5rem;
            font-weight: 800;
            color: transparent;
            background: linear-gradient(to right, #3b82f6, #60a5fa, #93c5fd);
            background-clip: text;
            -webkit-background-clip: text;
            margin-bottom: 12px;
            letter-spacing: -1px;
        }

        .hero h2 {
            font-size: 1.75rem;
            color: var(--text-main);
            margin-bottom: 24px;
            font-weight: 500;
            letter-spacing: -0.5px;
        }

        .hero p {
            font-size: 1.15rem;
            color: var(--text-muted);
            margin-bottom: 40px;
            max-width: 650px;
            margin-left: auto;
            margin-right: auto;
        }

        /* --- INTERACTIVE BUTTONS --- */
        .btn-container {
            display: flex;
            justify-content: center;
            gap: 16px;
            flex-wrap: wrap;
        }

        .btn-premium {
            padding: 14px 36px;
            border-radius: 12px;
            text-decoration: none;
            font-weight: 600;
            font-size: 0.95rem;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 2px solid var(--primary);
            color: #ffffff;
            background: var(--primary);
            box-shadow: 0 4px 14px var(--shadow-glow);
        }

        .btn-premium:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px var(--shadow-glow);
            filter: brightness(1.1);
        }
        
        .btn-premium-outline {
            background: transparent;
            color: var(--text-main);
            border-color: var(--card-border);
            box-shadow: none;
        }
        .btn-premium-outline:hover {
            border-color: var(--primary);
            background: rgba(59, 130, 246, 0.05);
            color: var(--primary);
        }

        /* --- SECTIONS ARCHITECTURE --- */
        section { padding: 120px 10%; position: relative; z-index: 2; }
        
        .section-title {
            font-size: 2.5rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 60px;
            color: var(--text-main);
            letter-spacing: -0.5px;
        }

        .section-title span {
            color: var(--primary);
        }

        /* --- 3D INTERACTIVE CARDS ARCHITECTURE --- */
        .matrix-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 32px;
            max-width: 1100px;
            margin: 0 auto;
        }

        .card-3d-wrapper {
            perspective: 1000px; /* Garante que o efeito 3D aconteça individualmente por card */
        }

        .card-3d {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            padding: 35px;
            border-radius: 16px;
            backdrop-filter: blur(16px);
            transform-style: preserve-3d; /* Permite que subelementos flutuem em eixos Z diferentes */
            transition: border-color 0.4s ease, box-shadow 0.4s ease, background 0.4s ease;
            height: 100%;
        }

        .card-3d:hover {
            border-color: var(--primary);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.12), 0 0 25px var(--shadow-glow);
        }

        /* Elementos saltando para fora do card no efeito 3D */
        .card-3d h3 {
            margin-bottom: 16px;
            color: var(--text-main);
            font-size: 1.4rem;
            font-weight: 600;
            transform: translateZ(30px); /* Projeta o título para frente em 3D */
            transition: transform 0.2s ease;
        }

        .card-3d p {
            color: var(--text-muted);
            font-size: 0.95rem;
            transform: translateZ(15px); /* Projeta o texto levemente para frente */
            transition: transform 0.2s ease;
        }

        /* Destaque Sênior: React + Tailwind Combinados */
        .card-premium-highlight {
            border: 1px solid rgba(59, 130, 246, 0.4);
            background: linear-gradient(145deg, rgba(17, 24, 39, 0.6), rgba(59, 130, 246, 0.05));
        }
        body.light-theme .card-premium-highlight {
            background: linear-gradient(145deg, #ffffff, rgba(59, 130, 246, 0.08));
        }

        .card-premium-highlight h3 {
            color: #3b82f6;
        }

        /* Tag custom para indicar tecnologia em estudo */
        .tag-learning {
            display: inline-block;
            padding: 4px 10px;
            border-radius: 30px;
            font-size: 0.75rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            background: rgba(59, 130, 246, 0.15);
            color: var(--primary);
            margin-bottom: 16px;
            transform: translateZ(20px);
        }

        /* --- PROJETOS & LINKS --- */
        .project-card { display: flex; flex-direction: column; justify-content: space-between; }
        .project-links {
            margin-top: 24px;
            display: inline-block;
            color: var(--primary);
            text-decoration: none;
            font-weight: 600;
            font-size: 0.9rem;
            transform: translateZ(25px);
            transition: 0.3s;
        }
        .project-links:hover { filter: brightness(1.2); padding-left: 4px; }

        /* --- CONTACT & FOOTER --- */
        .contact { text-align: center; }
        .contact p { margin: 24px 0; font-size: 1.25rem; font-weight: 500; }
        .contact a { color: var(--primary); text-decoration: none; transition: 0.3s; }
        .contact a:hover { filter: brightness(1.2); }

        footer {
            text-align: center;
            padding: 40px;
            color: var(--text-muted);
            font-size: 0.9rem;
            background: var(--footer-bg);
            border-top: 1px solid var(--card-border);
            position: relative;
            z-index: 2;
        }

        /* --- ANIMATION ENGINE (SCROLL ON REVEAL) --- */
        .scroll-interactive {
            opacity: 0;
            transform: translateY(60px) scale(0.96);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .scroll-interactive.active {
            opacity: 1;
            transform: translateY(0) scale(1);
        }

        /* --- RESPONSIVIDADE ADAPTATIVA --- */
        @media (max-width: 768px) {
            nav { display: none; }
            .theme-toggle { top: 20px; right: 20px; padding: 10px 14px; font-size: 0.75rem; }
            .hero h1 { font-size: 2.8rem; }
            .hero h2 { font-size: 1.35rem; }
            section { padding: 80px 6%; }
        }
    </style>
</head>
<body>

    <button class="theme-toggle" id="themeEngineBtn">
        <span id="themeIcon">☀️</span> <span id="themeText">Modo Claro</span>
    </button>

    <div class="bg-engine">
        <div class="blur-sphere" id="sphere1"></div>
        <div class="blur-sphere" id="sphere2"></div>
        <div class="blur-sphere" id="sphere3"></div>
    </div>

    <header id="inicio">
        <nav>
            <a href="#habilidades">Core Stack</a>
            <a href="#estudos">Próxima Stack</a>
            <a href="#projetos">Repositórios</a>
            <a href="#contato">Conectar</a>
        </nav>

        <div class="hero">
            <h1>Thiago Santana</h1>
            <h2>Software Developer | Front-End Architect</h2>
            <p>
                Programador Front-End júnior em busca de oportunidades de estágio, tenho dedicação ao 
                aprendizado contínuo, foco em desenvolvimento web moderno e estou sempre buscando aprimorar meus códigos,
                criando interfaces responsivas, profissionais e funcionais.
            </p>
            <div class="btn-container">
                <a href="#projetos" class="btn-premium btn-premium-outline">Explorar Projetos</a>
                <a href="#contato" class="btn-premium">Iniciar Conversa</a>
            </div>
        </div>
    </header>

    <main>
        <section class="scroll-interactive" id="habilidades">
            <h2 class="section-title">Core <span>Stack & Conhecimentos</span></h2>
            <div class="matrix-grid">
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <h3>HTML5 Semântico</h3>
                        <p>Estruturas de alta performance baseadas em SEO avançado, acessibilidade (WAI-ARIA) e layouts limpos.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <h3>CSS3 Avançado</h3>
                        <p>Arquitetura visual fluida usando Flexbox, Grid Layout, variáveis nativas e animações fluidas de UI.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <h3>JavaScript ES6+</h3>
                        <p>Domínio de lógica assíncrona, Promises, manipulação eficiente da DOM e consumo otimizado de APIs.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <h3>Git & Git Flow</h3>
                        <p>Gestão profissional de ramificações, versionamento seguro e controle de entregas contínuas.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="scroll-interactive" id="estudos">
            <h2 class="section-title">Engenharia em <span>Evolução</span></h2>
            <div class="matrix-grid">
                <div class="card-3d-wrapper" style="grid-column: span calc(auto-fit); min-width: 100%;">
                    <div class="card-3d card-premium-highlight">
                        <span class="tag-learning">Professional Focus</span>
                        <h3>⚛️ React + 🎨 Tailwind CSS</h3>
                        <p>Arquitetando Aplicações de Página Única (SPAs) baseadas em componentes purificados, gerenciamento ágil de estado e estilização utilitária atomizada via Tailwind para máxima velocidade de renderização e design impecável.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <span class="tag-learning">Learning</span>
                        <h3>💙 TypeScript</h3>
                        <p>Adicionando tipagem estática e segurança em escala ao JavaScript, prevenindo erros estruturais em tempo de compilação.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <span class="tag-learning">Learning</span>
                        <h3>💚 Node.js + { } JSON</h3>
                        <p>Desenvolvendo microsserviços rápidos, tratamento profissional e troca estruturada de fluxos de dados via objetos JSON.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <span class="tag-learning">Learning</span>
                        <h3>☕ Java (OOP)</h3>
                        <p>Fundamentação em Programação Orientada a Objetos robusta, padrões de projeto corporativos e regras sólidas de back-end.</p>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d">
                        <span class="tag-learning">Learning</span>
                        <h3>🗄️ MySQL & SQLite</h3>
                        <p>Modelagem relacional de dados, otimização de queries estruturadas em SQL e integração segura de motores de banco de dados.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="scroll-interactive" id="projetos">
            <h2 class="section-title">Sistemas <span>Desenvolvidos</span></h2>
            <div class="matrix-grid">
                <div class="card-3d-wrapper">
                    <div class="card-3d project-card">
                        <div>
                            <h3>Responsive Enterprise Hub</h3>
                            <p>Interface corporativa fluida desenvolvida para validar a consistência em diferentes resoluções mobile e desktop.</p>
                        </div>
                        <a href="https://github.com/thiago987001043-lab" target="_blank" class="project-links">Acessar Repositório →</a>
                    </div>
                </div>
                <div class="card-3d-wrapper">
                    <div class="card-3d project-card">
                        <div>
                            <h3>React Web Application</h3>
                            <p>Ambiente ativo em desenvolvimento combinando componentes funcionais do React com estruturação de dados em tempo real.</p>
                        </div>
                        <a href="https://github.com/thiago987001043-lab" target="_blank" class="project-links">Acompanhar Progresso →</a>
                    </div>
                </div>
            </div>
        </section>

        <section class="contact scroll-interactive" id="contato">
            <h2 class="section-title">Conectar com o <span>Engenheiro</span></h2>
            <p>Disponível para ingressar em times de alta performance e atuar em desafios escaláveis.</p>
            <p>📧 Direct Mail: <a href="mailto:thiago987001043@gmail.com">thiago987001043@gmail.com</a></p>
            <p>💻 Version Control: <a href="https://github.com/thiago987001043-lab" target="_blank">github.com/thiago987001043-lab</a></p>
            <br>
            <a href="mailto:thiago987001043@gmail.com" class="btn-premium" style="display: inline-flex; align-items: center; gap: 10px; justify-content: center;">
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="transition: transform 0.3s ease;">
        <rect width="20" height="16" x="2" y="4" rx="2"/>
        <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
    </svg>
    Disparar E-mail
</a>
        </section>
    </main>

    <footer>
        <p>© 2026 Thiago Santana de Sá Filho • Enterprise Front-End Developer</p>
    </footer>

    <script>
        /* --- 1. THEME TOGGLE ENGINE --- */
        const themeEngineBtn = document.getElementById('themeEngineBtn');
        const themeIcon = document.getElementById('themeIcon');
        const themeText = document.getElementById('themeText');

        themeEngineBtn.addEventListener('click', () => {
            document.body.classList.toggle('light-theme');
            if (document.body.classList.contains('light-theme')) {
                themeIcon.textContent = '🌙';
                themeText.textContent = 'Modo Escuro';
            } else {
                themeIcon.textContent = '☀️';
                themeText.textContent = 'Modo Claro';
            }
        });

        /* --- 2. 3D INTERACTIVE TILT MATH ENGINE (REQUISITO SÊNIOR) --- */
        const cards = document.querySelectorAll('.card-3d');

        cards.forEach(card => {
            card.addEventListener('mousemove', (e) => {
                const cardRect = card.getBoundingClientRect();
                const cardWidth = cardRect.width;
                const cardHeight = cardRect.height;
                
                // Encontra a posição do mouse em relação ao centro do card
                const mouseX = e.clientX - cardRect.left - cardWidth / 2;
                const mouseY = e.clientY - cardRect.top - cardHeight / 2;
                
                // Calcula os graus de rotação (máximo de 15 graus para elegância profissional)
                const rotateX = -(mouseY / cardHeight / 2) * 20;
                const rotateY = (mouseX / cardWidth / 2) * 20;
                
                card.style.transform = `rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateY(-5px)`;
            });

            card.addEventListener('mouseleave', () => {
                // Reseta a orientação do card perfeitamente de volta para a posição original
                card.style.transform = `rotateX(0deg) rotateY(0deg) translateY(0)`;
            });
        });

        /* --- 3. BACKGROUND FLUID PARALLAX SCROLL INTERACTION --- */
        const s1 = document.getElementById('sphere1');
        const s2 = document.getElementById('sphere2');
        const s3 = document.getElementById('sphere3');

        window.addEventListener('scroll', () => {
            const currentScroll = window.scrollY;
            
            // Física de translação assimétrica nos eixos das esferas de fundo 3D
            s1.style.transform = `translate(${currentScroll * 0.15}px, ${currentScroll * 0.3}px)`;
            s2.style.transform = `translate(${currentScroll * -0.1}px, ${currentScroll * -0.15}px)`;
            s3.style.transform = `translateY(${currentScroll * 0.08}px) scale(${1 + currentScroll * 0.0003})`;
        });

        /* --- 4. SCROLL INTERACTIVE OBSERVER (APARECER AO ROLAR) --- */
        const interactiveSections = document.querySelectorAll('.scroll-interactive');

        const scrollObserver = new IntersectionObserver((entries) => {
            entries.forEach((entry) => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                }
            });
        }, {
            threshold: 0.1
        });

        interactiveSections.forEach(section => {
            scrollObserver.observe(section);
        });
    </script>

</body>
</html> 
