<!DOCTYPE html>
<html lang="pt-BR" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aura Beauty | Alta Cosmética & Cuidados Com a Pele</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Playfair Display & Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        aura: {
                            rose: '#E8C5C8',       // Rose Gold Suave
                            gold: '#D4A373',       // Rose Gold Dourado / Accent
                            nude: '#FDF8F5',       // Fundo Nude Claro
                            sand: '#F4ECE6',       // Areia Suave / Cards
                            deep: '#2D2325',       // Vinho/Grafite Profundo para Textos
                            blush: '#F3D2C1',      // Blush Rosado
                            muted: '#8C7A6B'       // Texto Secundário
                        }
                    },
                    fontFamily: {
                        serif: ['Playfair Display', 'serif'],
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDF8F5;
            color: #2D2325;
        }
        .font-serif-title {
            font-family: 'Playfair Display', serif;
        }
        /* Utilitários de Scrollbar */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        /* Vidro Rose Gold */
        .glass-aura {
            background: rgba(253, 248, 245, 0.88);
            backdrop-filter: blur(14px);
            border: 1px solid rgba(232, 197, 200, 0.3);
        }
        /* Efeito Glow Rose */
        .rose-glow {
            box-shadow: 0 0 25px rgba(232, 197, 200, 0.35);
        }
    </style>
</head>
<body class="relative min-h-screen flex flex-col justify-between overflow-x-hidden selection:bg-aura-rose selection:text-aura-deep">

    <!-- Notificação Toast -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-24 opacity-0 transition-all duration-500 ease-out bg-aura-deep text-aura-nude px-6 py-4 rounded-2xl shadow-2xl flex items-center space-x-4 border border-aura-rose/40 pointer-events-none">
        <div id="toast-icon" class="text-aura-rose text-2xl"><i class="fas fa-sparkles"></i></div>
        <div>
            <h4 id="toast-title" class="font-serif-title font-semibold text-sm text-aura-rose">Aura Beauty</h4>
            <p id="toast-message" class="text-xs text-aura-nude/80">Item adicionado ao seu carrinho!</p>
        </div>
    </div>

    <!-- Banner Superior Promocional -->
    <div class="bg-aura-deep text-aura-rose text-[11px] py-2.5 text-center tracking-widest uppercase font-medium border-b border-aura-rose/20 flex items-center justify-center space-x-2">
        <i class="fas fa-sparkles text-aura-gold text-xs"></i>
        <span>Frete Grátis em compras acima de R$ 250 • Use o cupom <strong class="text-white underline">AURA10</strong> para 10% OFF</span>
        <i class="fas fa-sparkles text-aura-gold text-xs"></i>
    </div>

    <!-- Header / Navegação Principal (Fixo) -->
    <header class="sticky top-0 z-40 bg-aura-nude/90 backdrop-blur-md border-b border-aura-rose/20 transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                
                <!-- Logo Aura Beauty -->
                <a href="#home" class="flex items-center space-x-3 group">
                    <div class="w-10 h-10 rounded-full border border-aura-rose flex items-center justify-center bg-aura-sand text-aura-gold group-hover:scale-105 transition-transform duration-300 shadow-sm">
                        <i class="fas fa-gem text-base"></i>
                    </div>
                    <div class="flex flex-col">
                        <span class="font-serif-title text-2xl md:text-3xl font-bold tracking-wider text-aura-deep group-hover:text-aura-gold transition-colors">AURA</span>
                        <span class="text-[9px] tracking-[0.3em] text-aura-muted font-medium uppercase -mt-1">Beauty Lab</span>
                    </div>
                </a>

                <!-- Nav Links (Desktop) -->
                <nav class="hidden lg:flex space-x-8 font-medium text-xs tracking-widest uppercase text-aura-deep">
                    <a href="#home" class="hover:text-aura-gold transition-colors py-2">Início</a>
                    <a href="#products" onclick="filterCategory('serums')" class="hover:text-aura-gold transition-colors py-2">Séruns</a>
                    <a href="#products" onclick="filterCategory('elixirs')" class="hover:text-aura-gold transition-colors py-2">Elixires</a>
                    <a href="#quiz-section" class="hover:text-aura-gold transition-colors py-2 flex items-center text-aura-gold font-semibold">
                        <i class="fas fa-magic mr-1.5"></i> Quiz da Rotina
                    </a>
                    <a href="#about" class="hover:text-aura-gold transition-colors py-2">Sobre</a>
                    <a href="#reviews" class="hover:text-aura-gold transition-colors py-2">Depoimentos</a>
                </nav>

                <!-- Ações e Ícones -->
                <div class="flex items-center space-x-5">
                    
                    <!-- Busca Rápida com Autocomplete -->
                    <div class="relative hidden sm:block">
                        <div class="relative">
                            <input type="text" id="search-input" onkeyup="handleSearch()" placeholder="Buscar produtos ou ativos..." 
                                class="w-44 md:w-60 bg-aura-sand/80 border border-aura-rose/40 rounded-full py-1.5 pl-9 pr-4 text-xs focus:outline-none focus:ring-1 focus:ring-aura-gold focus:w-64 transition-all duration-300 text-aura-deep placeholder-aura-muted/70">
                            <i class="fas fa-search absolute left-3 top-2.5 text-xs text-aura-muted"></i>
                        </div>
                        <!-- Dropdown Autocomplete -->
                        <div id="search-results" class="hidden absolute top-full left-0 right-0 mt-2 bg-aura-nude rounded-2xl shadow-2xl border border-aura-rose/30 max-h-80 overflow-y-auto z-50 p-2"></div>
                    </div>

                    <!-- Favoritos / Wishlist -->
                    <button onclick="toggleWishlistDrawer()" class="relative p-2 text-aura-deep hover:text-aura-gold transition-colors" title="Lista de Desejos">
                        <i class="far fa-heart text-xl"></i>
                        <span id="wishlist-badge" class="absolute top-0 right-0 bg-aura-gold text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold opacity-0 transition-opacity">0</span>
                    </button>

                    <!-- Carrinho -->
                    <button onclick="toggleCartDrawer()" class="relative p-2 text-aura-deep hover:text-aura-gold transition-colors" title="Carrinho de Compras">
                        <i class="fas fa-shopping-bag text-xl"></i>
                        <span id="cart-badge" class="absolute top-0 right-0 bg-aura-deep text-aura-rose text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold border border-aura-rose/40">0</span>
                    </button>

                    <!-- Menu Mobile Toggle -->
                    <button onclick="toggleMobileMenu()" class="lg:hidden p-2 text-aura-deep focus:outline-none">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Menu Mobile Dropdown -->
        <div id="mobile-menu" class="hidden lg:hidden bg-aura-nude border-b border-aura-rose/20 px-6 pt-3 pb-6 space-y-3 shadow-xl">
            <div class="relative mb-3 sm:hidden">
                <input type="text" id="search-input-mobile" onkeyup="handleSearchMobile()" placeholder="Buscar produtos ou ativos..." 
                    class="w-full bg-aura-sand border border-aura-rose/40 rounded-full py-2 pl-9 pr-4 text-xs focus:outline-none">
                <i class="fas fa-search absolute left-3 top-3 text-xs text-aura-muted"></i>
                <div id="search-results-mobile" class="hidden absolute top-full left-0 right-0 mt-1 bg-aura-nude rounded-xl shadow-xl border border-aura-rose/20 max-h-60 overflow-y-auto z-50 p-2"></div>
            </div>
            <a href="#home" onclick="toggleMobileMenu()" class="block py-2 text-aura-deep font-serif-title text-sm border-b border-aura-sand">Início</a>
            <a href="#products" onclick="filterCategory('serums'); toggleMobileMenu()" class="block py-2 text-aura-deep font-serif-title text-sm border-b border-aura-sand">Séruns</a>
            <a href="#products" onclick="filterCategory('elixirs'); toggleMobileMenu()" class="block py-2 text-aura-deep font-serif-title text-sm border-b border-aura-sand">Elixires</a>
            <a href="#quiz-section" onclick="toggleMobileMenu()" class="block py-2 text-aura-gold font-serif-title text-sm border-b border-aura-sand">✨ Quiz de Rotina</a>
            <a href="#about" onclick="toggleMobileMenu()" class="block py-2 text-aura-deep font-serif-title text-sm border-b border-aura-sand">Sobre Nós</a>
            <a href="#reviews" onclick="toggleMobileMenu()" class="block py-2 text-aura-deep font-serif-title text-sm">Depoimentos</a>
        </div>
    </header>

    <main class="flex-grow">
        <!-- Hero Section -->
        <section id="home" class="relative bg-gradient-to-b from-aura-sand via-aura-nude to-aura-nude py-20 lg:py-32 overflow-hidden">
            <div class="absolute -top-32 -right-32 w-96 h-96 bg-aura-rose/20 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute bottom-0 left-0 w-80 h-80 bg-aura-blush/20 rounded-full blur-3xl pointer-events-none"></div>

            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                    
                    <div class="space-y-6 text-center lg:text-left">
                        <div class="inline-flex items-center space-x-2 bg-aura-rose/20 backdrop-blur-md border border-aura-rose/40 rounded-full px-4 py-1.5 shadow-sm">
                            <i class="fas fa-sparkles text-aura-gold text-xs"></i>
                            <span class="text-[11px] font-medium tracking-widest uppercase text-aura-deep">Alta Cosmética Botânica e Biotecnologia</span>
                        </div>
                        
                        <h1 class="font-serif-title text-4xl sm:text-5xl lg:text-6xl font-bold leading-tight text-aura-deep">
                            A luz interior refletida na sua <span class="italic text-aura-gold">pele de seda</span>.
                        </h1>
                        
                        <p class="text-sm sm:text-base text-aura-muted font-light max-w-xl mx-auto lg:mx-0 leading-relaxed">
                            Formulados com ativos biotecnológicos raros e óleos essenciais nobres. Descubra a sinergia perfeita para uma beleza radiante, jovem e atemporal.
                        </p>
                        
                        <div class="flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-4 pt-4">
                            <a href="#products" class="w-full sm:w-auto bg-aura-deep text-aura-rose px-8 py-4 rounded-full font-medium text-xs tracking-widest uppercase hover:bg-aura-gold hover:text-white transition-all duration-300 shadow-xl rose-glow text-center">
                                Explorar Coleção
                            </a>
                            <a href="#quiz-section" class="w-full sm:w-auto border border-aura-rose text-aura-deep px-8 py-4 rounded-full font-medium text-xs tracking-widest uppercase hover:bg-aura-rose/20 transition-all duration-300 text-center flex items-center justify-center">
                                <i class="fas fa-sparkles mr-2 text-aura-gold"></i> Descobrir Sua Rotina
                            </a>
                        </div>
                    </div>

                    <!-- Imagem Hero com Moldura Rose Gold -->
                    <div class="relative flex justify-center">
                        <div class="relative w-80 h-[460px] sm:w-[380px] sm:h-[520px] rounded-t-full border-2 border-aura-rose/60 p-3 shadow-2xl bg-white/40 backdrop-blur-sm">
                            <div class="w-full h-full rounded-t-full overflow-hidden relative">
                                <img src="https://images.unsplash.com/photo-1608248597260-6521e8e1218a?auto=format&fit=crop&w=800&q=80" alt="Aura Beauty Sérum" class="w-full h-full object-cover transform hover:scale-105 transition-transform duration-700">
                                <div class="absolute inset-0 bg-gradient-to-t from-aura-deep/40 via-transparent to-transparent"></div>
                            </div>
                        </div>

                        <!-- Badge Flutuante -->
                        <div class="absolute -bottom-4 -left-2 sm:left-6 bg-white/95 text-aura-deep p-4 rounded-2xl shadow-2xl border border-aura-rose/40 flex items-center space-x-3 max-w-xs">
                            <div class="w-10 h-10 rounded-full bg-aura-sand text-aura-gold flex items-center justify-center flex-shrink-0">
                                <i class="fas fa-droplet text-sm"></i>
                            </div>
                            <div>
                                <p class="text-xs font-serif-title font-bold">100% Vegano & Sustentável</p>
                                <p class="text-[10px] text-aura-muted">Ativos botânicos concentrados.</p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
        </section>

        <!-- Selos de Qualidade -->
        <section class="py-10 bg-aura-sand/60 border-y border-aura-rose/20">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
                    <div class="p-4 rounded-2xl hover:bg-white/60 transition-colors">
                        <i class="fas fa-leaf text-2xl text-aura-gold mb-2"></i>
                        <h4 class="font-serif-title font-bold text-xs uppercase text-aura-deep">Ingredientes Limpos</h4>
                        <p class="text-[11px] text-aura-muted mt-1">Sem parabenos ou sulfatos</p>
                    </div>
                    <div class="p-4 rounded-2xl hover:bg-white/60 transition-colors">
                        <i class="fas fa-paw text-2xl text-aura-gold mb-2"></i>
                        <h4 class="font-serif-title font-bold text-xs uppercase text-aura-deep">Cruelty-Free</h4>
                        <p class="text-[11px] text-aura-muted mt-1">Livre de testes em animais</p>
                    </div>
                    <div class="p-4 rounded-2xl hover:bg-white/60 transition-colors">
                        <i class="fas fa-vial text-2xl text-aura-gold mb-2"></i>
                        <h4 class="font-serif-title font-bold text-xs uppercase text-aura-deep">Dermatologicamente Testado</h4>
                        <p class="text-[11px] text-aura-muted mt-1">Eficácia comprovada</p>
                    </div>
                    <div class="p-4 rounded-2xl hover:bg-white/60 transition-colors">
                        <i class="fas fa-recycle text-2xl text-aura-gold mb-2"></i>
                        <h4 class="font-serif-title font-bold text-xs uppercase text-aura-deep">Embalagem Eco-Luxo</h4>
                        <p class="text-[11px] text-aura-muted mt-1">Vidro e materiais recicláveis</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Vitrine de Produtos -->
        <section id="products" class="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row md:items-end justify-between mb-12">
                <div>
                    <span class="text-xs font-serif-title uppercase tracking-widest text-aura-gold font-bold">Cuidados Exclusivos</span>
                    <h2 class="font-serif-title text-3xl md:text-4xl text-aura-deep mt-1">Coleção de Alta Cosmética</h2>
                </div>

                <!-- Filtros por Categoria -->
                <div class="flex items-center space-x-2 overflow-x-auto no-scrollbar pt-4 md:pt-0">
                    <button onclick="filterCategory('all')" class="cat-btn active border border-aura-deep bg-aura-deep text-white px-5 py-2 rounded-full text-xs font-medium uppercase tracking-wider whitespace-nowrap transition-all">Todos</button>
                    <button onclick="filterCategory('serums')" class="cat-btn border border-aura-rose/50 bg-white text-aura-deep hover:border-aura-deep px-5 py-2 rounded-full text-xs font-medium uppercase tracking-wider whitespace-nowrap transition-all">Séruns</button>
                    <button onclick="filterCategory('elixirs')" class="cat-btn border border-aura-rose/50 bg-white text-aura-deep hover:border-aura-deep px-5 py-2 rounded-full text-xs font-medium uppercase tracking-wider whitespace-nowrap transition-all">Elixires</button>
                    <button onclick="filterCategory('masks')" class="cat-btn border border-aura-rose/50 bg-white text-aura-deep hover:border-aura-deep px-5 py-2 rounded-full text-xs font-medium uppercase tracking-wider whitespace-nowrap transition-all">Máscaras</button>
                    <button onclick="filterCategory('cleansing')" class="cat-btn border border-aura-rose/50 bg-white text-aura-deep hover:border-aura-deep px-5 py-2 rounded-full text-xs font-medium uppercase tracking-wider whitespace-nowrap transition-all">Limpeza</button>
                </div>
            </div>

            <!-- Filtros Secundários e Ordenação -->
            <div class="flex flex-wrap items-center justify-between gap-4 mb-8 bg-aura-sand/40 p-4 rounded-2xl border border-aura-rose/20">
                <div class="flex flex-wrap items-center gap-2">
                    <span class="text-xs font-semibold text-aura-deep/80 mr-1">Propriedades:</span>
                    <button onclick="toggleTag('Luminosidade')" class="tag-btn text-[11px] bg-white border border-aura-rose/30 px-3 py-1 rounded-full hover:bg-aura-rose/20 transition-colors">✨ Luminosidade</button>
                    <button onclick="toggleTag('Rejuvenescimento')" class="tag-btn text-[11px] bg-white border border-aura-rose/30 px-3 py-1 rounded-full hover:bg-aura-rose/20 transition-colors">🌿 Anti-idade</button>
                    <button onclick="toggleTag('Hidratação')" class="tag-btn text-[11px] bg-white border border-aura-rose/30 px-3 py-1 rounded-full hover:bg-aura-rose/20 transition-colors">💧 Hidratação Profunda</button>
                    <button onclick="resetFilters()" class="text-[11px] text-aura-gold underline ml-2 font-medium">Limpar Filtros</button>
                </div>

                <div class="flex items-center space-x-2">
                    <label for="sort-select" class="text-xs font-semibold text-aura-deep/80">Ordenar:</label>
                    <select id="sort-select" onchange="sortProducts()" class="bg-white border border-aura-rose/40 rounded-xl text-xs py-1.5 px-3 focus:outline-none text-aura-deep">
                        <option value="popular">Mais Desejados</option>
                        <option value="price-low">Menor Preço</option>
                        <option value="price-high">Maior Preço</option>
                        <option value="rating">Melhor Avaliados</option>
                    </select>
                </div>
            </div>

            <!-- Grid de Produtos -->
            <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Injetado por JS -->
            </div>
        </section>

        <!-- Quiz "Descubra sua Rotina" -->
        <section id="quiz-section" class="py-20 bg-aura-deep text-aura-nude relative overflow-hidden">
            <div class="absolute -top-40 -left-40 w-96 h-96 bg-aura-rose/10 rounded-full blur-3xl pointer-events-none"></div>

            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center relative z-10">
                <span class="text-xs font-serif-title uppercase tracking-widest text-aura-rose font-bold">Diagnóstico Personalizado</span>
                <h2 class="font-serif-title text-3xl md:text-4xl text-white mt-1 mb-3">Descubra sua Rotina Ideal</h2>
                <p class="text-xs sm:text-sm text-aura-nude/70 max-w-lg mx-auto mb-10">Responda a 3 perguntas rápidas para encontrar a combinação de alta cosmética sob medida para sua pele.</p>

                <!-- Quiz Card Container -->
                <div class="bg-white/5 backdrop-blur-md rounded-3xl p-6 sm:p-12 border border-aura-rose/30 shadow-2xl relative">
                    
                    <!-- Barra de Progresso -->
                    <div class="w-full bg-aura-deep h-1.5 rounded-full mb-10 overflow-hidden border border-aura-rose/20">
                        <div id="quiz-progress" class="bg-gradient-to-r from-aura-rose to-aura-gold h-full w-1/3 transition-all duration-500"></div>
                    </div>

                    <!-- Etapa 1 -->
                    <div id="quiz-step-1" class="quiz-step">
                        <h3 class="font-serif-title text-lg font-semibold mb-6 text-aura-rose">1. Como sua pele reage ao longo do dia?</h3>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                            <button onclick="selectQuizOption(1, 'seca')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left flex items-center space-x-3">
                                <span class="text-lg">🌾</span> <span>Fica ressecada e repuxando com facilidade</span>
                            </button>
                            <button onclick="selectQuizOption(1, 'oleosa')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left flex items-center space-x-3">
                                <span class="text-lg">✨</span> <span>Apresenta oleosidade e brilho excessivo</span>
                            </button>
                            <button onclick="selectQuizOption(1, 'mista')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left flex items-center space-x-3">
                                <span class="text-lg">☯️</span> <span>Brilho na zona T e normal nas demais áreas</span>
                            </button>
                            <button onclick="selectQuizOption(1, 'sensivel')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left flex items-center space-x-3">
                                <span class="text-lg">🌸</span> <span>Reage com vermelhidão e sensibilidade</span>
                            </button>
                        </div>
                    </div>

                    <!-- Etapa 2 -->
                    <div id="quiz-step-2" class="quiz-step hidden">
                        <h3 class="font-serif-title text-lg font-semibold mb-6 text-aura-rose">2. Qual é o seu objetivo principal de cuidado?</h3>
                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                            <button onclick="selectQuizOption(2, 'Rejuvenescimento')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left">
                                <div class="text-aura-rose text-base mb-1"><i class="fas fa-hourglass-half"></i></div>
                                <strong>Anti-idade & Firmeza</strong>
                                <p class="text-[10px] text-aura-nude/60 mt-1">Suavizar linhas e estimular colágeno</p>
                            </button>
                            <button onclick="selectQuizOption(2, 'Luminosidade')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left">
                                <div class="text-aura-rose text-base mb-1"><i class="fas fa-sun"></i></div>
                                <strong>Luminosidade & Glow</strong>
                                <p class="text-[10px] text-aura-nude/60 mt-1">Unificar tom e resgatar o brilho</p>
                            </button>
                            <button onclick="selectQuizOption(2, 'Hidratação')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs text-left">
                                <div class="text-aura-rose text-base mb-1"><i class="fas fa-droplet"></i></div>
                                <strong>Hidratação Profunda</strong>
                                <p class="text-[10px] text-aura-nude/60 mt-1">Nutrição celular e barreira cutânea</p>
                            </button>
                        </div>
                    </div>

                    <!-- Etapa 3 -->
                    <div id="quiz-step-3" class="quiz-step hidden">
                        <h3 class="font-serif-title text-lg font-semibold mb-6 text-aura-rose">3. Qual textura você mais aprecia na pele?</h3>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-w-md mx-auto">
                            <button onclick="selectQuizOption(3, 'fluida')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs">
                                💧 Sérum Aquoso de Rápida Absorção
                            </button>
                            <button onclick="selectQuizOption(3, 'oleo')" class="p-4 border border-aura-rose/30 rounded-2xl hover:border-aura-rose hover:bg-aura-rose/10 transition-all font-medium text-xs">
                                ✨ Elixir Seco e Nutritivo
                            </button>
                        </div>
                    </div>

                    <!-- Resultado -->
                    <div id="quiz-result" class="hidden">
                        <div class="text-aura-gold text-4xl mb-2"><i class="fas fa-award"></i></div>
                        <h3 class="font-serif-title text-2xl font-bold mb-2 text-white">Sua Rotina Personalizada</h3>
                        <p class="text-xs text-aura-nude/80 mb-8">Esta é a combinação de alta performance indicada para as necessidades da sua pele:</p>
                        
                        <div id="quiz-recommendations" class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6 text-left">
                            <!-- Injetado por JS -->
                        </div>

                        <button onclick="resetQuiz()" class="text-xs text-aura-rose underline font-medium uppercase tracking-widest">Refazer Teste</button>
                    </div>

                </div>
            </div>
        </section>

        <!-- Sobre Aura Beauty -->
        <section id="about" class="py-20 bg-aura-nude border-y border-aura-rose/20 relative">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                    
                    <div class="relative">
                        <div class="rounded-3xl overflow-hidden border-2 border-aura-rose/40 shadow-2xl">
                            <img src="https://images.unsplash.com/photo-1540555700478-4be289fbecef?auto=format&fit=crop&w=800&q=80" alt="Laboratório Aura Beauty" class="w-full h-[400px] object-cover">
                        </div>
                        <div class="absolute -bottom-6 -right-6 bg-aura-deep text-aura-rose p-6 rounded-3xl border border-aura-rose/30 shadow-2xl hidden sm:block max-w-xs">
                            <p class="font-serif-title italic text-sm">"Inovação botânica aliada à pureza dos ingredientes nobres."</p>
                        </div>
                    </div>

                    <div class="space-y-6">
                        <span class="text-xs font-serif-title uppercase tracking-widest text-aura-gold font-bold">Nossa Essência</span>
                        <h2 class="font-serif-title text-3xl sm:text-4xl text-aura-deep">Ciência, Cuidado & Sofisticação</h2>
                        <p class="text-xs sm:text-sm text-aura-muted leading-relaxed">
                            A Aura Beauty nasceu da fusão entre a riqueza da botânica de luxo e a biotecnologia dermatológica avançada. Nossas fórmulas são desenvolvidas para elevar o seu autocuidado diário a um ritual de conexão e bem-estar.
                        </p>
                        <p class="text-xs sm:text-sm text-aura-muted leading-relaxed">
                            Priorizamos extratos puros, prensados a frio e sem diluição sintética, garantindo máxima eficácia, absorção rápida e fragrâncias naturais sutis.
                        </p>

                        <div class="grid grid-cols-3 gap-4 pt-4 border-t border-aura-rose/20">
                            <div>
                                <h4 class="font-serif-title font-bold text-lg text-aura-deep">100%</h4>
                                <p class="text-[10px] text-aura-muted uppercase tracking-wider">Ativos Puros</p>
                            </div>
                            <div>
                                <h4 class="font-serif-title font-bold text-lg text-aura-deep">0%</h4>
                                <p class="text-[10px] text-aura-muted uppercase tracking-wider">Toxinas e Sulfatos</p>
                            </div>
                            <div>
                                <h4 class="font-serif-title font-bold text-lg text-aura-deep">Eco</h4>
                                <p class="text-[10px] text-aura-muted uppercase tracking-wider">Frascos Recicláveis</p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
        </section>

        <!-- Depoimentos -->
        <section id="reviews" class="py-20 bg-aura-sand/40">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
                <span class="text-xs font-serif-title uppercase tracking-widest text-aura-gold font-bold">Comentários de Clientes</span>
                <h2 class="font-serif-title text-3xl md:text-4xl text-aura-deep mt-1 mb-12">O que Dizem Sobre Nós</h2>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 text-left">
                    <div class="p-8 rounded-3xl bg-aura-nude border border-aura-rose/20 shadow-sm relative">
                        <div class="flex text-aura-gold text-xs mb-4">
                            <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>
                        <p class="text-xs sm:text-sm text-aura-deep/80 italic mb-6 leading-relaxed">"O Sérum Iluminador Aura Rose mudou completamente a textura da minha pele. O toque é macio e a luminosidade natural dura o dia todo."</p>
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-full bg-aura-rose text-aura-deep font-serif-title font-bold flex items-center justify-center text-xs">MA</div>
                            <div>
                                <h5 class="text-xs font-serif-title font-bold text-aura-deep">Mariana Almeida</h5>
                                <span class="text-[10px] text-aura-muted">Cliente Verificada • São Paulo</span>
                            </div>
                        </div>
                    </div>

                    <div class="p-8 rounded-3xl bg-aura-nude border border-aura-rose/20 shadow-sm relative">
                        <div class="flex text-aura-gold text-xs mb-4">
                            <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>
                        <p class="text-xs sm:text-sm text-aura-deep/80 italic mb-6 leading-relaxed">"Textura leve, perfume sutil incrível e embalagem impecável. Foi a melhor compra de skincare do ano para minha rotina de luxo."</p>
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-full bg-aura-blush text-aura-deep font-serif-title font-bold flex items-center justify-center text-xs">CS</div>
                            <div>
                                <h5 class="text-xs font-serif-title font-bold text-aura-deep">Camila Silva</h5>
                                <span class="text-[10px] text-aura-muted">Cliente Verificada • Rio de Janeiro</span>
                            </div>
                        </div>
                    </div>

                    <div class="p-8 rounded-3xl bg-aura-nude border border-aura-rose/20 shadow-sm relative">
                        <div class="flex text-aura-gold text-xs mb-4">
                            <i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i><i class="fas fa-star"></i>
                        </div>
                        <p class="text-xs sm:text-sm text-aura-deep/80 italic mb-6 leading-relaxed">"Fiz o quiz e segui a recomendação da linha de elixires. Minha pele sensível adorou, sem nenhuma irritação e com alta hidratação."</p>
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 rounded-full bg-aura-gold text-white font-serif-title font-bold flex items-center justify-center text-xs">BR</div>
                            <div>
                                <h5 class="text-xs font-serif-title font-bold text-aura-deep">Beatriz Ribeiro</h5>
                                <span class="text-[10px] text-aura-muted">Cliente Verificada • Curitiba</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="bg-aura-deep text-aura-nude pt-20 pb-10 border-t border-aura-rose/30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-12 pb-16 border-b border-aura-rose/20">
                
                <!-- Coluna Marca -->
                <div class="space-y-4">
                    <div class="flex items-center space-x-2">
                        <i class="fas fa-gem text-aura-rose text-xl"></i>
                        <span class="font-serif-title text-2xl font-bold tracking-wider text-white">AURA</span>
                    </div>
                    <p class="text-xs text-aura-nude/70 leading-relaxed">
                        Alta cosmética de luxo desenvolvida para realçar sua beleza natural com biotecnologia e sofisticação.
                    </p>
                    <div class="flex space-x-4 pt-2">
                        <a href="#" class="text-aura-rose hover:text-aura-gold transition-colors text-base"><i class="fab fa-instagram"></i></a>
                        <a href="#" class="text-aura-rose hover:text-aura-gold transition-colors text-base"><i class="fab fa-pinterest"></i></a>
                        <a href="#" class="text-aura-rose hover:text-aura-gold transition-colors text-base"><i class="fab fa-tiktok"></i></a>
                    </div>
                </div>

                <!-- Links Rápidos -->
                <div>
                    <h4 class="font-serif-title text-xs font-bold uppercase tracking-widest text-aura-rose mb-4">Navegação</h4>
                    <ul class="space-y-2 text-xs text-aura-nude/80">
                        <li><a href="#products" onclick="filterCategory('serums')" class="hover:underline hover:text-aura-rose">Séruns Especiais</a></li>
                        <li><a href="#products" onclick="filterCategory('elixirs')" class="hover:underline hover:text-aura-rose">Elixires Raros</a></li>
                        <li><a href="#products" onclick="filterCategory('masks')" class="hover:underline hover:text-aura-rose">Máscaras Faciais</a></li>
                        <li><a href="#quiz-section" class="hover:underline hover:text-aura-rose">Quiz de Rotina</a></li>
                        <li><a href="#about" class="hover:underline hover:text-aura-rose">Sobre Nós</a></li>
                    </ul>
                </div>

                <!-- Suporte -->
                <div>
                    <h4 class="font-serif-title text-xs font-bold uppercase tracking-widest text-aura-rose mb-4">Atendimento</h4>
                    <ul class="space-y-2 text-xs text-aura-nude/80">
                        <li><a href="#" class="hover:underline">Central de Ajuda</a></li>
                        <li><a href="#" class="hover:underline">Rastrear Pedido</a></li>
                        <li><a href="#" class="hover:underline">Trocas e Devoluções</a></li>
                        <li><a href="#" class="hover:underline">Política de Privacidade</a></li>
                    </ul>
                </div>

                <!-- Newsletter -->
                <div>
                    <h4 class="font-serif-title text-xs font-bold uppercase tracking-widest text-aura-rose mb-4">Clube VIP</h4>
                    <p class="text-xs text-aura-nude/70 mb-3">Receba convites para lançamentos exclusivos e 10% de desconto no primeiro pedido.</p>
                    <form onsubmit="handleNewsletter(event)" class="space-y-2">
                        <input type="email" id="newsletter-email" required placeholder="Seu e-mail de preferência" 
                            class="w-full bg-white/10 border border-aura-rose/30 rounded-xl px-3 py-2.5 text-xs text-white placeholder-white/40 focus:outline-none focus:ring-1 focus:ring-aura-rose">
                        <button type="submit" class="w-full bg-aura-rose text-aura-deep font-medium py-2.5 rounded-xl text-xs uppercase tracking-wider hover:bg-aura-gold hover:text-white transition-colors">
                            Inscrever-se
                        </button>
                    </form>
                </div>

            </div>

            <div class="pt-8 flex flex-col sm:flex-row items-center justify-between text-xs text-aura-nude/50 space-y-4 sm:space-y-0">
                <p>&copy; 2026 Aura Beauty. Todos os direitos reservados.</p>
                <div class="flex items-center space-x-4 text-base">
                    <i class="fab fa-cc-visa" title="Visa"></i>
                    <i class="fab fa-cc-mastercard" title="Mastercard"></i>
                    <i class="fas fa-qrcode" title="Pix"></i>
                </div>
            </div>
        </div>
    </footer>

    <!-- MODAL QUICK VIEW -->
    <div id="quickview-modal" class="fixed inset-0 z-50 hidden overflow-y-auto bg-black/60 backdrop-blur-md flex items-center justify-center p-4">
        <div class="bg-aura-nude w-full max-w-3xl rounded-3xl overflow-hidden shadow-2xl relative border border-aura-rose/40 animate-fade-in">
            <button onclick="closeQuickView()" class="absolute top-4 right-4 z-10 w-9 h-9 bg-aura-sand rounded-full flex items-center justify-center text-aura-deep hover:bg-aura-rose transition-colors">
                <i class="fas fa-times"></i>
            </button>
            <div id="quickview-content" class="grid grid-cols-1 md:grid-cols-2">
                <!-- Conteúdo por JS -->
            </div>
        </div>
    </div>

    <!-- DRAWER: CARRINHO -->
    <div id="cart-drawer" class="fixed inset-0 z-50 pointer-events-none">
        <div id="cart-overlay" onclick="toggleCartDrawer()" class="absolute inset-0 bg-black/50 opacity-0 transition-opacity duration-300 pointer-events-none"></div>
        <div id="cart-panel" class="absolute top-0 right-0 h-full w-full max-w-md bg-aura-nude shadow-2xl transform translate-x-full transition-transform duration-300 pointer-events-auto flex flex-col justify-between">
            
            <div class="p-6 border-b border-aura-rose/20 flex items-center justify-between bg-aura-sand/40">
                <div class="flex items-center space-x-3">
                    <i class="fas fa-shopping-bag text-aura-gold text-lg"></i>
                    <h3 class="font-serif-title font-bold text-lg text-aura-deep">Seu Carrinho Aura</h3>
                </div>
                <button onclick="toggleCartDrawer()" class="text-aura-muted hover:text-aura-deep p-2">
                    <i class="fas fa-times"></i>
                </button>
            </div>

            <!-- Barra de Progresso de Frete Grátis -->
            <div class="bg-aura-deep text-aura-nude p-4 text-xs border-b border-aura-rose/20">
                <div class="flex justify-between font-medium mb-1.5" id="shipping-text">
                    <span>Faltam R$ 250,00 para Frete Grátis</span>
                </div>
                <div class="w-full bg-white/20 h-1.5 rounded-full overflow-hidden">
                    <div id="shipping-bar" class="bg-aura-rose h-full w-0 transition-all duration-300"></div>
                </div>
            </div>

            <!-- Lista de Itens do Carrinho -->
            <div id="cart-items" class="flex-grow overflow-y-auto p-6 space-y-4">
                <!-- Injetado por JS -->
            </div>

            <!-- Cupom & Checkout -->
            <div class="p-6 border-t border-aura-rose/20 bg-aura-sand/30 space-y-4">
                <div class="flex space-x-2">
                    <input type="text" id="coupon-input" placeholder="Cupom (ex: AURA10)" class="bg-white border border-aura-rose/40 rounded-xl px-3 py-2 text-xs w-full focus:outline-none uppercase">
                    <button onclick="applyCoupon()" class="bg-aura-deep text-aura-rose px-4 py-2 rounded-xl text-xs font-bold uppercase">Aplicar</button>
                </div>

                <div class="space-y-1.5 text-xs">
                    <div class="flex justify-between text-aura-muted">
                        <span>Subtotal</span>
                        <span id="cart-subtotal">R$ 0,00</span>
                    </div>
                    <div id="discount-row" class="flex justify-between text-aura-gold hidden font-semibold">
                        <span>Desconto (10%)</span>
                        <span id="cart-discount">-R$ 0,00</span>
                    </div>
                    <div class="flex justify-between text-base font-serif-title font-bold text-aura-deep pt-2 border-t border-aura-rose/20">
                        <span>Total</span>
                        <span id="cart-total">R$ 0,00</span>
                    </div>
                </div>

                <button onclick="checkout()" class="w-full bg-aura-deep text-aura-rose py-4 rounded-full font-bold text-xs tracking-widest uppercase hover:bg-aura-gold hover:text-white transition-colors shadow-lg rose-glow">
                    Finalizar Pedido
                </button>
            </div>

        </div>
    </div>

    <!-- DRAWER: WISHLIST -->
    <div id="wishlist-drawer" class="fixed inset-0 z-50 pointer-events-none">
        <div id="wishlist-overlay" onclick="toggleWishlistDrawer()" class="absolute inset-0 bg-black/50 opacity-0 transition-opacity duration-300 pointer-events-none"></div>
        <div id="wishlist-panel" class="absolute top-0 right-0 h-full w-full max-w-md bg-aura-nude shadow-2xl transform translate-x-full transition-transform duration-300 pointer-events-auto flex flex-col justify-between">
            <div class="p-6 border-b border-aura-rose/20 flex items-center justify-between bg-aura-sand/40">
                <div class="flex items-center space-x-3">
                    <i class="fas fa-heart text-aura-gold text-lg"></i>
                    <h3 class="font-serif-title font-bold text-lg text-aura-deep">Sua Lista de Desejos</h3>
                </div>
                <button onclick="toggleWishlistDrawer()" class="text-aura-muted hover:text-aura-deep p-2">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div id="wishlist-items" class="flex-grow overflow-y-auto p-6 space-y-4">
                <!-- Injetado por JS -->
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // Banco de Dados de Produtos
        const products = [
            {
                id: 1,
                name: "Sérum Iluminador Aura Rose",
                category: "serums",
                price: 189.00,
                oldPrice: 220.00,
                rating: 5.0,
                reviews: 128,
                image: "https://images.unsplash.com/photo-1620916566398-39f1143ab7be?auto=format&fit=crop&w=600&q=80",
                tags: ["Luminosidade", "Rejuvenescimento"],
                skinType: "Todos os tipos de pele",
                ingredients: "Vitamina C Estabilizada 15%, Ácido Hialurônico e Extrato de Rosa Mosqueta.",
                description: "Sérum concentrado de alta absorção que uniforme o tom, devolve o brilho radiante natural e combate radicais livres.",
                badge: "Mais Vendido"
            },
            {
                id: 2,
                name: "Elixir Nutritivo Cristalino",
                category: "elixirs",
                price: 215.00,
                oldPrice: null,
                rating: 4.9,
                reviews: 94,
                image: "https://images.unsplash.com/photo-1631729371254-42c2892f0e6e?auto=format&fit=crop&w=600&q=80",
                tags: ["Hidratação", "Luminosidade"],
                skinType: "Pele Seca e Mista",
                ingredients: "Óleo Secco de Azeitona Squalane, Óleo de Semente de Camélia e Esqualano Vegetal.",
                description: "Toque aveludado que repõe lipídios essenciais sem engordurar, proporcionando toque sedoso duradouro.",
                badge: "Destaque"
            },
            {
                id: 3,
                name: "Máscara de Argila Rosa & Quartzo",
                category: "masks",
                price: 139.00,
                oldPrice: 160.00,
                rating: 4.8,
                reviews: 72,
                image: "https://images.unsplash.com/photo-1567928257065-2650d0353018?auto=format&fit=crop&w=600&q=80",
                tags: ["Rejuvenescimento"],
                skinType: "Pele Mista e Oleosa",
                ingredients: "Argila Rosa Francesa, Pó de Quartzo Rosa e Extrato de Camomila.",
                description: "Detox suave que desobstrui poros, acalma a pele e restaura o viço natural em apenas 10 minutos.",
                badge: null
            },
            {
                id: 4,
                name: "Cleansing Balm Botânico Nude",
                category: "cleansing",
                price: 125.00,
                oldPrice: null,
                rating: 4.9,
                reviews: 105,
                image: "https://images.unsplash.com/photo-1556228720-195a672e8a03?auto=format&fit=crop&w=600&q=80",
                tags: ["Hidratação"],
                skinType: "Todos os tipos",
                ingredients: "Manteiga de Karité, Óleo de Girassol Orgânico e Vitamina E.",
                description: "Bálsamo de limpeza que derrete a maquiagem e impurezas sem agredir a barreira de proteção cutânea.",
                badge: "Novo"
            },
            {
                id: 5,
                name: "Óleo Facial Seco Dourado",
                category: "elixirs",
                price: 198.00,
                oldPrice: 230.00,
                rating: 5.0,
                reviews: 61,
                image: "https://images.unsplash.com/photo-1608248543803-ba4f8c70ae0b?auto=format&fit=crop&w=600&q=80",
                tags: ["Luminosidade"],
                skinType: "Rosto e Colo",
                ingredients: "Óleo de Jojoba, Partículas Iluminadoras de Mica e Óleo de Argan.",
                description: "Proporciona um acabamento iluminado bronze-dourado sutil enquanto nutre intensamente a pele.",
                badge: null
            },
            {
                id: 6,
                name: "Sérum Anti-idade Niacinamida + Bakuchiol",
                category: "serums",
                price: 229.00,
                oldPrice: null,
                rating: 4.9,
                reviews: 83,
                image: "https://images.unsplash.com/photo-1617897903246-719242758050?auto=format&fit=crop&w=600&q=80",
                tags: ["Rejuvenescimento", "Hidratação"],
                skinType: "Pele Madura ou Sensível",
                ingredients: "Bakuchiol 2% (Retinol Vegetal), Niacinamida 5% e Peptídeos.",
                description: "Renovação celular potente sem irritação. Reduz linhas finas e uniformiza a textura do rosto.",
                badge: "Alta Eficácia"
            }
        ];

        // Estado Global
        let cart = [];
        let wishlist = [];
        let activeCategory = 'all';
        let activeTags = [];
        let isCouponApplied = false;
        let quizAnswers = {};

        // Inicialização
        document.addEventListener('DOMContentLoaded', () => {
            renderProducts();
            updateCartUI();
            updateWishlistUI();
        });

        // Toast de Notificação
        function showToast(message, title = "Aura Beauty", icon = "fa-sparkles") {
            const toast = document.getElementById('toast');
            document.getElementById('toast-title').innerText = title;
            document.getElementById('toast-message').innerText = message;
            document.getElementById('toast-icon').innerHTML = `<i class="fas ${icon}"></i>`;
            
            toast.classList.remove('translate-y-24', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 3200);
        }

        // Renderização do Grid de Produtos
        function renderProducts(itemsToRender = getFilteredProducts()) {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = '';

            if (itemsToRender.length === 0) {
                grid.innerHTML = `
                    <div class="col-span-full text-center py-16">
                        <i class="fas fa-gem text-4xl text-aura-rose mb-3"></i>
                        <p class="text-aura-muted font-serif-title text-sm">Nenhum produto encontrado com os filtros selecionados.</p>
                    </div>
                `;
                return;
            }

            itemsToRender.forEach(product => {
                const isWish = wishlist.some(item => item.id === product.id);
                const card = document.createElement('div');
                card.className = "group bg-aura-nude rounded-3xl p-5 border border-aura-rose/20 shadow-sm hover:shadow-2xl hover:border-aura-rose/60 transition-all duration-500 flex flex-col justify-between relative overflow-hidden";
                
                card.innerHTML = `
                    ${product.badge ? `<span class="absolute top-7 left-7 z-10 bg-aura-deep text-aura-rose text-[9px] font-bold px-3 py-1 rounded-full uppercase tracking-widest border border-aura-rose/30">${product.badge}</span>` : ''}
                    
                    <button onclick="toggleWishlist(${product.id})" class="absolute top-7 right-7 z-10 w-9 h-9 bg-white/80 backdrop-blur-sm rounded-full flex items-center justify-center text-aura-deep hover:text-aura-rose transition-colors shadow-md">
                        <i class="${isWish ? 'fas text-aura-rose' : 'far'} fa-heart"></i>
                    </button>

                    <div>
                        <!-- Imagem -->
                        <div class="relative h-64 w-full rounded-2xl overflow-hidden bg-aura-sand/50 mb-5 cursor-pointer" onclick="openQuickView(${product.id})">
                            <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover group-hover:scale-108 transition-transform duration-700">
                            <div class="absolute inset-0 bg-aura-deep/10 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
                                <span class="bg-white/90 backdrop-blur-md text-aura-deep text-xs font-semibold px-4 py-2 rounded-full shadow-lg transform translate-y-2 group-hover:translate-y-0 transition-transform">
                                    <i class="fas fa-eye mr-1.5 text-aura-gold"></i> Visualização Rápida
                                </span>
                            </div>
                        </div>

                        <!-- Avaliação -->
                        <div class="flex items-center space-x-1 text-aura-gold text-xs mb-1">
                            <i class="fas fa-star"></i>
                            <span class="font-bold text-aura-deep ml-1">${product.rating}</span>
                            <span class="text-aura-muted text-[11px]">(${product.reviews})</span>
                        </div>

                        <h3 class="font-serif-title font-bold text-sm text-aura-deep line-clamp-1 group-hover:text-aura-gold transition-colors cursor-pointer" onclick="openQuickView(${product.id})">${product.name}</h3>
                        <p class="text-xs text-aura-muted line-clamp-2 mt-1.5 leading-relaxed font-light">${product.description}</p>
                    </div>

                    <div class="mt-5 pt-4 border-t border-aura-rose/20 flex items-center justify-between">
                        <div>
                            <span class="font-serif-title font-bold text-base text-aura-deep">R$ ${product.price.toFixed(2).replace('.', ',')}</span>
                            ${product.oldPrice ? `<span class="text-xs text-aura-muted/60 line-through ml-1">R$ ${product.oldPrice.toFixed(2).replace('.', ',')}</span>` : ''}
                        </div>

                        <button onclick="addToCart(${product.id})" class="bg-aura-deep text-aura-rose hover:bg-aura-gold hover:text-white p-3 rounded-full transition-all duration-300 shadow-md" title="Adicionar ao Carrinho">
                            <i class="fas fa-plus text-xs"></i>
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        // Filtros e Seleção
        function getFilteredProducts() {
            return products.filter(product => {
                const matchCategory = activeCategory === 'all' || product.category === activeCategory;
                const matchTags = activeTags.length === 0 || activeTags.every(tag => product.tags.includes(tag));
                return matchCategory && matchTags;
            });
        }

        function filterCategory(category) {
            activeCategory = category;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                btn.classList.remove('bg-aura-deep', 'text-white');
                btn.classList.add('bg-white', 'text-aura-deep');
            });
            event.target.classList.remove('bg-white', 'text-aura-deep');
            event.target.classList.add('bg-aura-deep', 'text-white');

            renderProducts();
        }

        function toggleTag(tag) {
            const index = activeTags.indexOf(tag);
            if (index > -1) {
                activeTags.splice(index, 1);
                event.target.classList.remove('bg-aura-rose/30', 'font-bold');
            } else {
                activeTags.push(tag);
                event.target.classList.add('bg-aura-rose/30', 'font-bold');
            }
            renderProducts();
        }

        function resetFilters() {
            activeCategory = 'all';
            activeTags = [];
            document.querySelectorAll('.tag-btn').forEach(btn => btn.classList.remove('bg-aura-rose/30', 'font-bold'));
            renderProducts();
        }

        function sortProducts() {
            const val = document.getElementById('sort-select').value;
            let list = [...getFilteredProducts()];

            if (val === 'price-low') list.sort((a, b) => a.price - b.price);
            else if (val === 'price-high') list.sort((a, b) => b.price - a.price);
            else if (val === 'rating') list.sort((a, b) => b.rating - a.rating);
            else list.sort((a, b) => b.reviews - a.reviews);

            renderProducts(list);
        }

        // Busca com Autocomplete
        function handleSearch() {
            const query = document.getElementById('search-input').value.toLowerCase();
            const resultsBox = document.getElementById('search-results');

            if (query.length < 2) {
                resultsBox.classList.add('hidden');
                return;
            }

            const matches = products.filter(p => p.name.toLowerCase().includes(query) || p.ingredients.toLowerCase().includes(query));
            
            if (matches.length > 0) {
                resultsBox.innerHTML = matches.map(p => `
                    <div onclick="openQuickView(${p.id})" class="flex items-center space-x-3 p-2.5 hover:bg-aura-sand/60 rounded-xl cursor-pointer transition-colors">
                        <img src="${p.image}" class="w-10 h-10 rounded-lg object-cover">
                        <div>
                            <h5 class="text-xs font-serif-title font-bold text-aura-deep">${p.name}</h5>
                            <span class="text-[10px] text-aura-gold font-semibold">R$ ${p.price.toFixed(2).replace('.', ',')}</span>
                        </div>
                    </div>
                `).join('');
                resultsBox.classList.remove('hidden');
            } else {
                resultsBox.innerHTML = `<div class="p-3 text-xs text-aura-muted text-center">Nenhum produto encontrado.</div>`;
                resultsBox.classList.remove('hidden');
            }
        }

        function handleSearchMobile() {
            const query = document.getElementById('search-input-mobile').value.toLowerCase();
            const resultsBox = document.getElementById('search-results-mobile');

            if (query.length < 2) {
                resultsBox.classList.add('hidden');
                return;
            }

            const matches = products.filter(p => p.name.toLowerCase().includes(query));
            
            if (matches.length > 0) {
                resultsBox.innerHTML = matches.map(p => `
                    <div onclick="openQuickView(${p.id}); toggleMobileMenu();" class="flex items-center space-x-3 p-2 hover:bg-aura-sand rounded-lg cursor-pointer">
                        <img src="${p.image}" class="w-8 h-8 rounded object-cover">
                        <span class="text-xs font-serif-title text-aura-deep">${p.name}</span>
                    </div>
                `).join('');
                resultsBox.classList.remove('hidden');
            } else {
                resultsBox.classList.add('hidden');
            }
        }

        // Modal Quick View
        function openQuickView(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            const modal = document.getElementById('quickview-modal');
            const container = document.getElementById('quickview-content');

            container.innerHTML = `
                <div class="h-80 md:h-full bg-aura-sand/50 relative">
                    <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover">
                </div>
                <div class="p-6 md:p-8 flex flex-col justify-between space-y-4">
                    <div>
                        <span class="text-[10px] font-bold tracking-widest text-aura-gold uppercase">Aura Beauty Lab</span>
                        <h3 class="font-serif-title text-2xl font-bold text-aura-deep mt-1">${product.name}</h3>
                        
                        <div class="flex items-center space-x-2 text-aura-gold text-xs my-2">
                            <i class="fas fa-star"></i>
                            <span class="font-bold text-aura-deep">${product.rating}</span>
                            <span class="text-aura-muted">(${product.reviews} avaliações)</span>
                        </div>

                        <div class="my-3">
                            <span class="text-xl font-serif-title font-bold text-aura-deep">R$ ${product.price.toFixed(2).replace('.', ',')}</span>
                            ${product.oldPrice ? `<span class="text-sm text-aura-muted line-through ml-2">R$ ${product.oldPrice.toFixed(2).replace('.', ',')}</span>` : ''}
                        </div>

                        <p class="text-xs text-aura-muted leading-relaxed mb-4">${product.description}</p>

                        <div class="space-y-2 text-xs border-t border-aura-rose/20 pt-3">
                            <p><strong class="text-aura-deep">Tipo de Pele:</strong> ${product.skinType}</p>
                            <p><strong class="text-aura-deep">Ativos Principais:</strong> ${product.ingredients}</p>
                        </div>
                    </div>

                    <div class="pt-4 border-t border-aura-rose/20 flex items-center space-x-3">
                        <button onclick="addToCart(${product.id}); closeQuickView();" class="flex-grow bg-aura-deep text-aura-rose py-3.5 rounded-full font-bold text-xs tracking-widest uppercase hover:bg-aura-gold hover:text-white transition-colors shadow-lg">
                            Adicionar ao Carrinho
                        </button>
                    </div>
                </div>
            `;

            modal.classList.remove('hidden');
        }

        function closeQuickView() {
            document.getElementById('quickview-modal').classList.add('hidden');
        }

        // Drawers
        function toggleCartDrawer() {
            const panel = document.getElementById('cart-panel');
            const overlay = document.getElementById('cart-overlay');
            const isOpen = !panel.classList.contains('translate-x-full');

            if (isOpen) {
                panel.classList.add('translate-x-full');
                overlay.classList.add('opacity-0', 'pointer-events-none');
            } else {
                panel.classList.remove('translate-x-full');
                overlay.classList.remove('opacity-0', 'pointer-events-none');
            }
        }

        function toggleWishlistDrawer() {
            const panel = document.getElementById('wishlist-panel');
            const overlay = document.getElementById('wishlist-overlay');
            const isOpen = !panel.classList.contains('translate-x-full');

            if (isOpen) {
                panel.classList.add('translate-x-full');
                overlay.classList.add('opacity-0', 'pointer-events-none');
            } else {
                panel.classList.remove('translate-x-full');
                overlay.classList.remove('opacity-0', 'pointer-events-none');
            }
        }

        // Operações de Carrinho
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existing = cart.find(item => item.id === productId);

            if (existing) {
                existing.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }

            updateCartUI();
            showToast(`${product.name} foi adicionado ao seu carrinho!`);
        }

        function updateQuantity(productId, delta) {
            const item = cart.find(i => i.id === productId);
            if (!item) return;

            item.quantity += delta;
            if (item.quantity <= 0) {
                cart = cart.filter(i => i.id !== productId);
            }

            updateCartUI();
        }

        function applyCoupon() {
            const code = document.getElementById('coupon-input').value.trim().toUpperCase();
            if (code === 'AURA10') {
                isCouponApplied = true;
                showToast("Cupom AURA10 aplicado (10% OFF)!", "Desconto Especial");
                updateCartUI();
            } else {
                showToast("Cupom inválido. Experimente 'AURA10'", "Erro", "fa-exclamation-circle");
            }
        }

        function updateCartUI() {
            const cartItemsContainer = document.getElementById('cart-items');
            const cartBadge = document.getElementById('cart-badge');
            const cartSubtotal = document.getElementById('cart-subtotal');
            const cartDiscount = document.getElementById('cart-discount');
            const discountRow = document.getElementById('discount-row');
            const cartTotal = document.getElementById('cart-total');
            const shippingText = document.getElementById('shipping-text');
            const shippingBar = document.getElementById('shipping-bar');

            const totalItems = cart.reduce((sum, i) => sum + i.quantity, 0);
            cartBadge.innerText = totalItems;

            if (cart.length === 0) {
                cartItemsContainer.innerHTML = `
                    <div class="text-center py-16 text-aura-muted">
                        <i class="fas fa-shopping-bag text-4xl mb-3 text-aura-rose/50"></i>
                        <p class="text-xs font-serif-title">Seu carrinho está vazio.</p>
                    </div>
                `;
                cartSubtotal.innerText = "R$ 0,00";
                cartTotal.innerText = "R$ 0,00";
                shippingBar.style.width = "0%";
                shippingText.innerText = "Faltam R$ 250,00 para Frete Grátis";
                return;
            }

            cartItemsContainer.innerHTML = cart.map(item => `
                <div class="flex items-center space-x-3 p-3 bg-aura-sand/40 rounded-2xl border border-aura-rose/20">
                    <img src="${item.image}" class="w-14 h-14 rounded-xl object-cover">
                    <div class="flex-grow">
                        <h4 class="text-xs font-serif-title font-bold text-aura-deep line-clamp-1">${item.name}</h4>
                        <span class="text-xs text-aura-gold font-semibold">R$ ${item.price.toFixed(2).replace('.', ',')}</span>
                        <div class="flex items-center space-x-2 mt-2">
                            <button onclick="updateQuantity(${item.id}, -1)" class="w-5 h-5 bg-white rounded-full flex items-center justify-center text-xs text-aura-deep">-</button>
                            <span class="text-xs font-bold px-1">${item.quantity}</span>
                            <button onclick="updateQuantity(${item.id}, 1)" class="w-5 h-5 bg-white rounded-full flex items-center justify-center text-xs text-aura-deep">+</button>
                        </div>
                    </div>
                    <button onclick="updateQuantity(${item.id}, -${item.quantity})" class="text-aura-muted hover:text-red-400 text-xs p-1">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
            `).join('');

            const subtotal = cart.reduce((sum, i) => sum + (i.price * i.quantity), 0);
            let discount = 0;

            if (isCouponApplied) {
                discount = subtotal * 0.10;
                discountRow.classList.remove('hidden');
                cartDiscount.innerText = `-R$ ${discount.toFixed(2).replace('.', ',')}`;
            }

            const total = subtotal - discount;
            cartSubtotal.innerText = `R$ ${subtotal.toFixed(2).replace('.', ',')}`;
            cartTotal.innerText = `R$ ${total.toFixed(2).replace('.', ',')}`;

            // Frete
            const threshold = 250;
            const progress = Math.min((subtotal / threshold) * 100, 100);
            shippingBar.style.width = `${progress}%`;

            if (subtotal >= threshold) {
                shippingText.innerHTML = `<span class="text-aura-rose font-bold">✨ Parabéns! Você ganhou Frete Grátis!</span>`;
            } else {
                const diff = threshold - subtotal;
                shippingText.innerText = `Faltam R$ ${diff.toFixed(2).replace('.', ',')} para Frete Grátis`;
            }
        }

        // Operações de Wishlist
        function toggleWishlist(productId) {
            const product = products.find(p => p.id === productId);
            const index = wishlist.findIndex(item => item.id === productId);

            if (index > -1) {
                wishlist.splice(index, 1);
                showToast(`Removido dos Favoritos`, "Aura");
            } else {
                wishlist.push(product);
                showToast(`Salvo na sua Lista de Desejos!`, "Aura Wishlist", "fa-heart");
            }

            updateWishlistUI();
            renderProducts();
        }

        function updateWishlistUI() {
            const badge = document.getElementById('wishlist-badge');
            const itemsContainer = document.getElementById('wishlist-items');

            badge.innerText = wishlist.length;
            badge.style.opacity = wishlist.length > 0 ? "1" : "0";

            if (wishlist.length === 0) {
                itemsContainer.innerHTML = `
                    <div class="text-center py-16 text-aura-muted">
                        <i class="far fa-heart text-4xl mb-3 text-aura-rose/50"></i>
                        <p class="text-xs font-serif-title">Sua lista de desejos está vazia.</p>
                    </div>
                `;
                return;
            }

            itemsContainer.innerHTML = wishlist.map(item => `
                <div class="flex items-center space-x-3 p-3 bg-aura-sand/40 rounded-2xl border border-aura-rose/20">
                    <img src="${item.image}" class="w-14 h-14 rounded-xl object-cover">
                    <div class="flex-grow">
                        <h4 class="text-xs font-serif-title font-bold text-aura-deep line-clamp-1">${item.name}</h4>
                        <span class="text-xs text-aura-gold font-semibold">R$ ${item.price.toFixed(2).replace('.', ',')}</span>
                    </div>
                    <button onclick="addToCart(${item.id})" class="bg-aura-deep text-aura-rose px-3 py-1.5 rounded-full text-[10px] font-bold uppercase">
                        Mover
                    </button>
                </div>
            `).join('');
        }

        // Lógica do Quiz
        function selectQuizOption(step, option) {
            quizAnswers[`step${step}`] = option;
            document.getElementById(`quiz-step-${step}`).classList.add('hidden');

            const progressEl = document.getElementById('quiz-progress');

            if (step === 1) {
                progressEl.style.width = '66%';
                document.getElementById('quiz-step-2').classList.remove('hidden');
            } else if (step === 2) {
                progressEl.style.width = '100%';
                document.getElementById('quiz-step-3').classList.remove('hidden');
            } else if (step === 3) {
                showQuizResults();
            }
        }

        function showQuizResults() {
            document.getElementById('quiz-step-3').classList.add('hidden');
            const resultEl = document.getElementById('quiz-result');
            const recsContainer = document.getElementById('quiz-recommendations');

            const matched = products.filter(p => p.tags.includes(quizAnswers.step2) || p.category === 'serums').slice(0, 2);

            recsContainer.innerHTML = matched.map(p => `
                <div class="p-4 bg-white/10 rounded-2xl border border-aura-rose/30 flex items-center space-x-3 text-left">
                    <img src="${p.image}" class="w-16 h-16 rounded-xl object-cover">
                    <div>
                        <h4 class="text-xs font-serif-title font-bold text-white">${p.name}</h4>
                        <span class="text-xs text-aura-rose font-semibold">R$ ${p.price.toFixed(2).replace('.', ',')}</span>
                        <button onclick="addToCart(${p.id})" class="mt-2 block bg-aura-rose text-aura-deep px-3 py-1 rounded-full text-[10px] font-bold uppercase">
                            Adicionar
                        </button>
                    </div>
                </div>
            `).join('');

            resultEl.classList.remove('hidden');
        }

        function resetQuiz() {
            quizAnswers = {};
            document.getElementById('quiz-progress').style.width = '33%';
            document.getElementById('quiz-result').classList.add('hidden');
            document.getElementById('quiz-step-1').classList.remove('hidden');
        }

        // Checkout Simulado
        function checkout() {
            if (cart.length === 0) {
                showToast("Adicione produtos antes de finalizar!", "Atenção", "fa-exclamation-circle");
                return;
            }
            showToast("Conectando ao ambiente de pagamento seguro...", "Aura Checkout", "fa-spinner animate-spin");
            setTimeout(() => {
                cart = [];
                updateCartUI();
                toggleCartDrawer();
                showToast("Pedido efetuado com sucesso! Um e-mail de confirmação foi enviado.", "Compra Concluída", "fa-check-circle");
            }, 2200);
        }

        function handleNewsletter(e) {
            e.preventDefault();
            const input = document.getElementById('newsletter-email');
            if (input.value) {
                showToast("Obrigado por se inscrever no Clube VIP Aura!", "Bem-vinda(o)", "fa-envelope");
                input.value = '';
            }
        }

        function toggleMobileMenu() {
            document.getElementById('mobile-menu').classList.toggle('hidden');
        }
    </script>
</body>
</html>
