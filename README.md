<!DOCTYPE html>
<html lang="cs" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BuildSphere - Minecraft Building Team</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Rajdhani:wght@600;700;800&display=swap" rel="stylesheet">
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        heading: ['Rajdhani', 'sans-serif'],
                    },
                    colors: {
                        primary: '#3b82f6',   // Jasná Modrá
                        secondary: '#f43f5e', // Růžová/Červená
                        accent: '#22d3ee',    // Azurová
                        dark: '#0f172a',
                        darker: '#020617',
                        deepblue: '#0a0d17',
                    }
                }
            }
        }
    </script>

    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>

    <style>
        /* Animace pozadí Hero sekce */
        .hero-bg {
            background-image: linear-gradient(rgba(15, 23, 42, 0.95), rgba(2, 6, 23, 0.99)), url('https://images.unsplash.com/photo-1628286950298-63cb53517861?q=80&w=2574&auto=format&fit=crop'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            animation: pan 60s linear infinite alternate;
        }
        @keyframes pan {
            0% { background-position: 0% 0%; }
            100% { background-position: 100% 100%; }
        }

        /* Dynamické gradienty pro text */
        .text-gradient {
            background: linear-gradient(to right, #3b82f6, #f43f5e, #22d3ee);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Vizuální oddělovač */
        .section-separator {
            @apply h-1 bg-gradient-to-r from-primary via-accent to-secondary w-32 mx-auto my-12 rounded-full shadow-lg shadow-accent/30;
        }

        /* Nová jemná opakující se animace pro stálý "život" */
        .animate-breathe {
            animation: breathe 3s ease-in-out infinite;
        }
        @keyframes breathe {
            0%, 100% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.01); opacity: 0.95; }
        }

        /* Animace pro interakci (jemný zoom + light shake) */
        .hover-effect:hover {
            transform: scale(1.03) translateY(-2px);
            transition: transform 0.3s ease-in-out;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
        }
        .hover-effect {
            transition: all 0.3s ease-in-out;
        }

        /* Skryje scrollbar, ale umožní scroll */
        body::-webkit-scrollbar {
            display: none;
        }
        body {
            -ms-overflow-style: none; /* IE and Edge */
            scrollbar-width: none; /* Firefox */
        }

        /* Pro section reveal animations */
        .fade-in-section {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
            will-change: opacity, transform;
        }
        .fade-in-section.is-visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* Placeholder pro abstraktní pozadí sekce "O nás" */
        .abstract-bg {
            background: radial-gradient(circle at top left, var(--tw-gradient-stops));
            --tw-gradient-stops: #3b82f640, #f43f5e40, #0a0d17;
            min-height: 400px;
            position: relative;
            overflow: hidden;
            border-radius: 1.5rem;
            border: 4px solid;
            border-image: linear-gradient(to bottom right, #3b82f6, #22d3ee, #f43f5e) 1;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
        }
        .abstract-bg::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: repeating-linear-gradient(
                45deg,
                rgba(255,255,255,0.05) 0px,
                rgba(255,255,255,0.05) 1px,
                transparent 1px,
                transparent 5px
            );
            animation: move-pattern 20s linear infinite;
        }
        @keyframes move-pattern {
            0% { transform: translate(0, 0); }
            100% { transform: translate(-50px, -50px); }
        }

    </style>
</head>
<body class="bg-white dark:bg-darker text-gray-800 dark:text-gray-200 transition-colors duration-300" x-data="{ darkMode: true, mobileMenu: false }" :class="{ 'dark': darkMode }">

    <div id="particles-js" class="fixed inset-0 z-0 opacity-20"></div>

    <nav class="fixed w-full z-50 bg-white/80 dark:bg-darker/80 backdrop-blur-lg border-b border-gray-200 dark:border-gray-800 shadow-xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <div class="flex-shrink-0 flex items-center gap-3 cursor-pointer hover-effect" onclick="window.scrollTo(0,0)">
                    <i class="fa-solid fa-gem text-4xl text-accent animate-pulse"></i>
                    <span class="font-heading font-extrabold text-3xl tracking-wider uppercase text-gradient">BuildSphere</span>
                </div>
                
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-8 font-heading font-semibold text-lg">
                        <a href="#about" class="hover:text-accent transition-transform hover-effect">O nás</a>
                        <a href="#specialization" class="hover:text-accent transition-transform hover-effect">Specializace</a>
                        <a href="#projects" class="hover:text-accent transition-transform hover-effect">Projekty</a>
                        <a href="#team" class="hover:text-accent transition-transform hover-effect">Tým</a>
                        <a href="#join" class="hover:text-accent transition-transform hover-effect">Nábor</a>
                    </div>
                </div>

                <div class="hidden md:flex items-center gap-4">
                    <button @click="darkMode = !darkMode" class="p-2 rounded-full hover:bg-gray-700 transition hover-effect">
                        <span x-show="darkMode" class="text-2xl animate-breathe">🌙</span>
                        <span x-show="!darkMode" class="text-2xl animate-breathe">☀️</span>
                    </button>
                    <a href="https://discord.gg/MPV2EKSK" target="_blank" class="bg-primary hover:bg-secondary text-white px-5 py-2 rounded-xl font-heading font-bold transition-transform hover-effect shadow-lg shadow-primary/50 flex items-center gap-2 animate-breathe">
                        <i class="fa-brands fa-discord"></i> Discord
                    </a>
                </div>

                <div class="md:hidden flex items-center gap-4">
                     <button @click="darkMode = !darkMode" class="p-2">
                        <span x-show="darkMode" class="text-2xl animate-breathe">🌙</span>
                        <span x-show="!darkMode" class="text-2xl animate-breathe">☀️</span>
                    </button>
                    <button @click="mobileMenu = !mobileMenu" class="text-3xl text-gray-700 dark:text-gray-300 hover-effect">
                        <i class="fa-solid fa-bars"></i>
                    </button>
                </div>
            </div>
        </div>
        <div x-show="mobileMenu" @click.away="mobileMenu = false" x-transition:enter="duration-200 ease-out" x-transition:leave="duration-150 ease-in" class="md:hidden bg-darker/95 border-b border-gray-800 absolute w-full left-0 shadow-2xl">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3 text-center">
                <a href="#about" @click="mobileMenu = false" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-800 hover:text-accent">O nás</a>
                <a href="#specialization" @click="mobileMenu = false" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-800 hover:text-accent">Specializace</a>
                <a href="#projects" @click="mobileMenu = false" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-800 hover:text-accent">Projekty</a>
                <a href="#team" @click="mobileMenu = false" class="block px-3 py-2 rounded-md text-base font-medium hover:bg-gray-800 hover:text-accent">Tým</a>
                <a href="#join" @click="mobileMenu = false" class="block px-3 py-2 rounded-md text-base font-medium text-accent font-bold hover:bg-gray-800">Nábor</a>
                <a href="https://discord.gg/MPV2EKSK" target="_blank" class="block w-3/4 mx-auto py-2 mt-4 bg-primary text-white rounded-lg font-bold hover:bg-secondary hover-effect">
                    <i class="fa-brands fa-discord mr-2"></i> Discord
                </a>
            </div>
        </div>
    </nav>

    <section class="hero-bg min-h-screen flex items-center justify-center text-center px-4 pt-20 relative z-10">
        <div class="max-w-4xl mx-auto space-y-6 animate-fade-in-up">
            <span class="inline-block py-2 px-4 rounded-full bg-accent/20 text-accent border border-accent/50 text-sm font-semibold uppercase tracking-wider mb-4 shadow-xl transform hover-effect animate-breathe">
                💎 Minecraft Building Team
            </span>
            <h1 class="text-5xl md:text-7xl font-heading font-extrabold text-white leading-tight drop-shadow-2xl">
                Tvoříme legendy. <br>
                Každý blok má svůj <span class="text-gradient">příběh.</span>
            </h1>
            <p class="text-xl text-gray-300 max-w-2xl mx-auto font-light drop-shadow-md">
                Jsme tým BuildSphere. Od detailu k celku, od fantazie k realitě. Tvoříme světy, které vás pohltí.
            </p>
            
            <div class="flex flex-col sm:flex-row gap-4 justify-center mt-8">
                <a href="#specialization" class="px-8 py-4 bg-secondary text-white font-bold rounded-xl hover:bg-red-700 transition shadow-[0_0_25px_rgba(244,63,94,0.5)] hover-effect">
                    🗺️ Naše Služby
                </a>
                <a href="https://discord.gg/MPV2EKSK" class="px-8 py-4 bg-primary/20 backdrop-blur-sm border border-primary text-white font-bold rounded-xl hover:bg-primary/40 transition hover-effect">
                    🤝 Připojit se k nám
                </a>
            </div>
        </div>
    </section>

    <section id="about" class="py-20 bg-gray-50 dark:bg-dark relative z-10 fade-in-section">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-5xl font-heading font-bold mb-4 text-center text-gray-900 dark:text-white">O nás</h2>
            <div class="section-separator"></div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center mt-12">
                <div class="space-y-6 text-gray-600 dark:text-gray-300 leading-relaxed">
                    <p class="text-lg">
                        Jsme tým stavitelů v Minecraftu jménem **Build Sphere**, zrozený z čisté vášně pro detail, architekturu a nekonečné možnosti, které tato hra nabízí.
                    </p>
                    <p class="text-lg">
                        Naše cesta začala inspirací. Sledovali jsme s obdivem práci špičkových týmů z české i globální scény – jména jako **Czech-Agile, BlockWorks nebo Elysium Fire** nám ukázala, kam až lze posunout hranice blokového světa. Viděli jsme jejich preciznost, komplexnost projektů a schopnost vyprávět příběhy skrz bloky. Tato inspirace nás nevedla ke kopírování, ale k vytvoření vlastní, unikátní vize.
                    </p>
                    <h3 class="text-3xl font-heading font-bold mt-10 text-gradient">Naše Mise a Filozofie</h3>
                    <div class="p-6 bg-white dark:bg-darker rounded-xl border border-gray-200 dark:border-gray-800 shadow-md flex items-start gap-4 hover:shadow-xl transition-transform hover-effect">
                        <i class="fa-solid fa-magic text-3xl text-primary mt-1 animate-breathe"></i>
                        <div>
                            <h4 class="font-bold text-xl mb-1 text-gray-900 dark:text-white">Od Detailu k Celku</h4>
                            <p class="text-gray-600 dark:text-gray-400">Věříme, že i ten nejmenší blok má svůj význam. Každý náš projekt – ať už je to masivní server spawn, rozsáhlé RPG město nebo malá dekorace – je promyšlen do posledního detailu.</p>
                        </div>
                    </div>
                    <div class="p-6 bg-white dark:bg-darker rounded-xl border border-gray-200 dark:border-gray-800 shadow-md flex items-start gap-4 hover:shadow-xl transition-transform hover-effect">
                        <i class="fa-solid fa-bolt text-3xl text-secondary mt-1 animate-breathe"></i>
                        <div>
                            <h4 class="font-bold text-xl mb-1 text-gray-900 dark:text-white">Inovace a Posouvání Hranic</h4>
                            <p class="text-gray-600 dark:text-gray-400">Nechceme jen "hezky stavět". Neustále experimentujeme s novými technikami, barevnými paletami a kompozicemi. Specializujeme se na fantasy a středověké projekty obohacené o komplexní terraforming a organické stavby.</p>
                        </div>
                    </div>
                </div>
                
                <div class="abstract-bg relative rounded-3xl shadow-2xl transform rotate-3 scale-105 transition-transform duration-700 border-4 border-primary/50 hover:rotate-0 hover:scale-100 overflow-hidden hover-effect">
                    <div class="absolute inset-0 flex items-center justify-center text-white text-3xl font-bold p-8">
                        <i class="fa-solid fa-cubes text-9xl opacity-75 animate-breathe"></i>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="py-20 bg-white dark:bg-darker border-t border-gray-200 dark:border-gray-800 relative z-10 fade-in-section">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <h2 class="text-5xl font-heading font-bold mb-4 text-center text-gray-900 dark:text-white">Co nás odlišuje?</h2>
            <div class="section-separator"></div>

            <div class="grid md:grid-cols-3 gap-8 mt-12">
                <div class="bg-gray-50 dark:bg-dark p-8 rounded-2xl transition duration-300 border border-transparent hover:border-primary/50 shadow-lg hover:shadow-2xl transform hover-effect">
                    <div class="w-16 h-16 bg-gradient-to-br from-blue-500 to-indigo-600 rounded-lg flex items-center justify-center text-white text-3xl mb-6 animate-breathe">
                        <i class="fa-solid fa-scroll"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-3 text-gray-900 dark:text-white">Vášeň pro Příběh</h3>
                    <p class="text-gray-600 dark:text-gray-400">
                        Naše stavby nejsou jen hromady bloků. Každý kout, ulice nebo věž má svůj příběh, který vtáhne hráče do světa, jenž žije i po odpojení ze serveru.
                    </p>
                </div>

                <div class="bg-gray-50 dark:bg-dark p-8 rounded-2xl transition duration-300 border border-transparent hover:border-secondary/50 shadow-lg hover:shadow-2xl transform hover-effect">
                    <div class="w-16 h-16 bg-gradient-to-br from-pink-500 to-rose-600 rounded-lg flex items-center justify-center text-white text-3xl mb-6 animate-breathe">
                        <i class="fa-solid fa-puzzle-piece"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-3 text-gray-900 dark:text-white">Síla Týmové Práce</h3>
                    <p class="text-gray-600 dark:text-gray-400">
                        Naše největší síla spočívá v kolektivu. Mezi námi není rivalita, ale vzájemná podpora a konstruktivní kritika, která posouvá kvalitu projektů.
                    </p>
                </div>

                <div class="bg-gray-50 dark:bg-dark p-8 rounded-2xl transition duration-300 border border-transparent hover:border-accent/50 shadow-lg hover:shadow-2xl transform hover-effect">
                    <div class="w-16 h-16 bg-gradient-to-br from-accent to-teal-600 rounded-lg flex items-center justify-center text-white text-3xl mb-6 animate-breathe">
                        <i class="fa-solid fa-medal"></i>
                    </div>
                    <h3 class="text-2xl font-bold mb-3 text-gray-900 dark:text-white">Profesionalita v Blocích</h3>
                    <p class="text-gray-600 dark:text-gray-400">
                        Dodržujeme termíny, efektivně komunikujeme a používáme pokročilé nástroje jako WorldEdit, VoxelSniper, Arceon či WorldPainter pro top-tier výsledky.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <section id="specialization" class="py-20 bg-darker relative overflow-hidden z-10 fade-in-section">
        <div class="absolute top-0 left-0 w-full h-full bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] opacity-10"></div>
        
        <div class="max-w-7xl mx-auto px-4 relative z-10 text-center">
            <h2 class="text-5xl font-heading font-bold text-white mb-4">Naše Specializace</h2>
            <div class="section-separator"></div>
            <p class="text-xl text-gray-400 mt-6 mb-12 max-w-2xl mx-auto">
                Naše služby se zaměřují na tvorbu úžasných Minecraft světů. Každý projekt je pro nás jedinečný.
            </p>
            
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="group bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl border border-gray-700 hover:border-primary transition cursor-default shadow-xl transform hover-effect">
                    <div class="text-6xl mb-4 text-primary group-hover:text-accent transition animate-breathe">🏰</div>
                    <h3 class="text-3xl font-bold text-white mb-2 font-heading">Fantasy / Medieval Města</h3>
                    <p class="text-gray-400 mb-4">Detailní města a spawny, které vtáhnou hráče do epických příběhů a dobrodružství.</p>
                </div>

                <div class="group bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl border border-gray-700 hover:border-secondary transition cursor-default shadow-xl transform hover-effect">
                    <div class="text-6xl mb-4 text-secondary group-hover:text-accent transition animate-breathe">🌋</div>
                    <h3 class="text-3xl font-bold text-white mb-2 font-heading">Realistický Terraforming</h3>
                    <p class="text-gray-400 mb-4">Vytváříme ohromující krajiny, hory, údolí a oceány, které vypadají jako skutečné.</p>
                </div>

                <div class="group bg-gradient-to-br from-gray-800 to-gray-900 p-8 rounded-2xl border border-gray-700 hover:border-accent transition cursor-default shadow-xl transform hover-effect">
                    <div class="text-6xl mb-4 text-accent group-hover:text-white transition animate-breathe">🐲</div>
                    <h3 class="text-3xl font-bold text-white mb-2 font-heading">Organické Sochy a Dekorace</h3>
                    <p class="text-gray-400 mb-4">Od draků po epické stromy, naše organické stavby dodají vašemu světu život.</p>
                </div>
            </div>
            <div class="mt-12 text-center">
                <a href="#join" class="inline-block px-10 py-4 bg-secondary text-white font-bold rounded-xl text-lg hover:bg-red-700 transition shadow-lg shadow-secondary/40 hover-effect">
                    ✨ Objednat Zakázkovou Mapu
                </a>
            </div>
        </div>
    </section>

    <section id="projects" class="py-20 bg-gray-50 dark:bg-dark relative z-10 fade-in-section">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <h2 class="text-5xl font-heading font-bold mb-4 text-gray-900 dark:text-white">Spolupracovali jsme</h2>
            <div class="section-separator"></div>
            <p class="text-xl text-gray-600 dark:text-gray-400 mt-6 mb-12 max-w-2xl mx-auto">
                Jsme hrdí na projekty, které jsme realizovali pro naše partnery.
            </p>
            
            <div class="flex flex-wrap justify-center gap-16 items-center">
                <a href="https://www.youtube.com/@rajcepro" target="_blank" class="relative group bg-white dark:bg-darker p-8 rounded-2xl shadow-xl border border-gray-200 dark:border-gray-800 hover:border-primary transition-all duration-300 transform hover-effect">
                    <div class="h-28 w-28 object-contain mx-auto mb-4 rounded-full bg-red-500/10 flex items-center justify-center text-red-500 text-6xl border-4 border-white dark:border-darker animate-breathe">
                        <i class="fa-brands fa-youtube"></i> 
                    </div>
                    <h4 class="font-bold text-2xl text-gray-900 dark:text-white mb-1">Rajče.pro</h4>
                    <span class="text-sm text-gray-500 block mb-2">YouTube / Herní Server</span>
                    <p class="text-lg font-bold text-green-500 animate-pulse">
                        <i class="fa-solid fa-users text-green-400 mr-1"></i> 300+ Hráčů Denně!
                    </p>
                </a>
                
                <a href="https://www.youtube.com/@plej111" target="_blank" class="relative group bg-white dark:bg-darker p-8 rounded-2xl shadow-xl border border-gray-200 dark:border-gray-800 hover:border-secondary transition-all duration-300 transform hover-effect">
                    <div class="h-28 w-28 object-cover mx-auto mb-4 rounded-full border-4 border-white dark:border-darker bg-blue-500/10 flex items-center justify-center text-blue-500 text-6xl animate-breathe">
                         <i class="fa-brands fa-youtube"></i>
                    </div>
                    <h4 class="font-bold text-2xl text-gray-900 dark:text-white mb-1">Plej</h4>
                    <span class="text-sm text-gray-500">YouTube Kanál</span>
                </a>
            </div>
        </div>
    </section>

    <section id="team" class="py-20 bg-deepblue text-white relative z-10 fade-in-section">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <h2 class="text-5xl font-heading font-bold mb-4">Náš Tým</h2>
            <div class="section-separator"></div>
            <p class="text-xl text-gray-400 mt-6 mb-12 max-w-2xl mx-auto">
                Poznejte tvůrce, který stojí za BuildSphere.
            </p>

            <div class="flex justify-center">
                <div class="bg-gray-800 p-8 rounded-2xl shadow-2xl transform hover-effect transition-transform duration-300 border border-gray-700 hover:border-primary max-w-lg">
                    <div class="h-40 w-40 rounded-full bg-gradient-to-br from-primary to-secondary mx-auto flex items-center justify-center text-7xl font-bold text-white mb-6 border-8 border-accent overflow-hidden shadow-xl animate-breathe">
                        👑
                    </div>
                    <h3 class="text-4xl font-heading font-extrabold mb-2 text-gradient">RuzovyKrtek</h3>
                    <p class="text-secondary font-semibold text-xl mb-4">Majitel Všeho</p>
                    <p class="text-gray-400 text-base">
                        Zakladatel a vizionář BuildSphere. Jeho neochvějná vášeň pro Minecraft, smysl pro detail a nekompromisní standardy kvality posouvají náš tým k nekonečným možnostem a vytváření legendárních děl. Je hnací silou každého projektu a garantem originality a preciznosti.
                    </p>
                    <div class="flex justify-center gap-8 mt-8">
                        <a href="https://discord.gg/MPV2EKSK" target="_blank" class="text-gray-400 hover:text-primary transition-colors text-4xl hover-effect">
                            <i class="fa-brands fa-discord"></i>
                        </a>
                        <a href="https://www.youtube.com/@RuzovyKrtek" target="_blank" class="text-gray-400 hover:text-secondary transition-colors text-4xl hover-effect">
                            <i class="fa-brands fa-youtube"></i>
                        </a>
                        <a href="mailto:ruzovykrtekspoluprace@gmail.com" class="text-gray-400 hover:text-accent transition-colors text-4xl hover-effect">
                            <i class="fa-solid fa-envelope"></i>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="join" class="py-20 bg-gradient-to-r from-indigo-900 to-purple-900 text-white text-center px-4 relative z-10 fade-in-section">
        <div class="max-w-3xl mx-auto relative z-10">
            <h2 class="text-5xl font-heading font-bold mb-6">Přidej se k nám!</h2>
            <p class="text-xl text-indigo-100 mb-8 max-w-2xl mx-auto">
                Hledáme nové kreativní stavitele, kteří sdílí naši vášeň pro stavění a chtějí posouvat hranice možného. Máš cit pro detail a chuť tvořit ve skvělém týmu?
            </p>
            
            <div class="bg-white/10 backdrop-blur-md p-8 rounded-2xl border border-white/20 inline-block w-full max-w-lg shadow-2xl">
                <h3 class="text-2xl font-bold mb-6 border-b border-white/20 pb-4">Kontaktujte nás</h3>
                
                <div class="flex flex-col gap-4 text-left">
                    <div class="flex items-center gap-4 bg-black/20 p-4 rounded-lg hover:bg-black/30 transition hover-effect">
                        <i class="fa-solid fa-envelope text-3xl text-pink-400"></i>
                        <div>
                            <p class="text-xs text-gray-300 uppercase">Email</p>
                            <a href="mailto:ruzovykrtekspoluprace@gmail.com" class="font-mono text-lg hover:text-pink-300 transition">ruzovykrtekspoluprace@gmail.com</a>
                        </div>
                    </div>
                    
                    <div class="flex items-center gap-4 bg-black/20 p-4 rounded-lg hover:bg-black/30 transition hover-effect">
                        <i class="fa-brands fa-discord text-3xl text-indigo-400"></i>
                        <div>
                            <p class="text-xs text-gray-300 uppercase">Discord Nick</p>
                            <span class="font-mono text-lg select-all">ruzovykrtek</span>
                        </div>
                    </div>
                </div>

                <div class="mt-8">
                     <a href="https://discord.gg/MPV2EKSK" class="block w-full py-4 bg-secondary hover:bg-red-700 rounded-xl font-bold transition shadow-lg hover-effect">
                        Přejít na náš Discord Server
                    </a>
                </div>
            </div>
        </div>
    </section>

    <footer class="bg-darker border-t border-gray-800 py-12 text-center md:text-left relative z-10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid md:grid-cols-4 gap-8">
                <div class="col-span-1 md:col-span-2">
                    <span class="font-heading font-extrabold text-3xl text-gradient tracking-wider uppercase mb-4 block hover-effect">BuildSphere</span>
                    <p class="text-gray-500 max-w-sm">
                        Specializujeme se na fantasy a středověké projekty obohacené o komplexní terraforming a organické stavby.
                    </p>
                </div>
                
                <div>
                    <h4 class="text-white font-bold mb-4 uppercase text-sm">Navigace</h4>
                    <ul class="space-y-2 text-gray-400 text-sm">
                        <li><a href="#" class="hover:text-primary transition hover-effect">Domů</a></li>
                        <li><a href="#about" class="hover:text-primary transition hover-effect">O nás</a></li>
                        <li><a href="#specialization" class="hover:text-primary transition hover-effect">Služby</a></li>
                        <li><a href="#join" class="hover:text-primary transition hover-effect">Nábor</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-white font-bold mb-4 uppercase text-sm">Sleduj nás</h4>
                    <ul class="space-y-2 text-gray-400 text-sm">
                        <li>
                            <a href="https://discord.gg/MPV2EKSK" target="_blank" class="hover:text-primary transition hover-effect flex items-center gap-2">
                                <i class="fa-brands fa-discord"></i> Discord
                            </a>
                        </li>
                        <li>
                            <a href="https://www.youtube.com/@RuzovyKrtek" target="_blank" class="hover:text-secondary transition hover-effect flex items-center gap-2">
                                <i class="fa-brands fa-youtube"></i> YouTube (RuzovyKrtek)
                            </a>
                        </li>
                        <li>
                            <a href="mailto:ruzovykrtekspoluprace@gmail.com" class="hover:text-accent transition hover-effect flex items-center gap-2">
                                <i class="fa-solid fa-envelope"></i> Email
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-gray-800 mt-12 pt-8 flex flex-col md:flex-row justify-between items-center text-gray-600 text-sm">
                <p>&copy; 2025 BuildSphere. Všechna práva vyhrazena.</p>
                <p class="mt-4 md:mt-0">Design & Code by RuzovyKrtek</p>
            </div>
        </div>
    </footer>

    <script>
        // Inicializace Particles.js
        particlesJS('particles-js', {
            "particles": {
                "number": {
                    "value": 80,
                    "density": {
                        "enable": true,
                        "value_area": 800
                    }
                },
                "color": {
                    "value": "#22d3ee" // Accent color
                },
                "shape": {
                    "type": "circle",
                },
                "opacity": {
                    "value": 0.5,
                    "random": false,
                    "anim": {
                        "enable": false,
                    }
                },
                "size": {
                    "value": 3,
                    "random": true,
                    "anim": {
                        "enable": false,
                    }
                },
                "line_linked": {
                    "enable": true,
                    "distance": 150,
                    "color": "#3b82f6", // Primary color
                    "opacity": 0.4,
                    "width": 1
                },
                "move": {
                    "enable": true,
                    "speed": 1.5,
                    "direction": "none",
                    "random": false,
                    "straight": false,
                    "out_mode": "out",
                    "bounce": false,
                    "attract": {
                        "enable": false,
                        "rotateX": 600,
                        "rotateY": 1200
                    }
                }
            },
            "interactivity": {
                "detect_on": "canvas",
                "events": {
                    "onhover": {
                        "enable": true,
                        "mode": "grab"
                    },
                    "onclick": {
                        "enable": true,
                        "mode": "push"
                    },
                    "resize": true
                },
                "modes": {
                    "grab": {
                        "distance": 140,
                        "line_linked": {
                            "opacity": 1
                        }
                    },
                    "push": {
                        "particles_nb": 4
                    }
                }
            },
            "retina_detect": true
        });

        // Logika pro animaci sekcí při scrollování
        document.addEventListener('DOMContentLoaded', (event) => {
            const sections = document.querySelectorAll('.fade-in-section');

            const options = {
                root: null, // viewport
                rootMargin: '0px 0px -100px 0px', // -100px odspodu (spustí se dřív)
                threshold: 0.1 // 10% sekce je vidět
            };

            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('is-visible');
                        observer.unobserve(entry.target); // Zastaví sledování sekce, jakmile se objeví
                    }
                });
            }, options);

            sections.forEach(section => {
                observer.observe(section);
            });
        });
    </script>

</body>
</html>
