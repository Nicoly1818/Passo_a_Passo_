# Passo_a_Passo_
<!DOCTYPE html>
<html lang="pt-BR" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Coleta e Tratamento de Dados Industriais | Guia Prático</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter & JetBrains Mono para detalhes técnicos -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                    colors: {
                        royal: {
                            50: '#eef4ff',
                            100: '#d9e6ff',
                            200: '#bcd4ff',
                            500: '#2563eb',
                            600: '#1d4ed8',
                            700: '#1e40af',
                            800: '#1e3a8a',
                            900: '#172554',
                            950: '#0f172a',
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Padrão de grade técnica sutil para fundo */
        .bg-tech-grid {
            background-size: 32px 32px;
            background-image: 
                linear-gradient(to right, rgba(30, 58, 138, 0.04) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(30, 58, 138, 0.04) 1px, transparent 1px);
        }

        /* Animação do pulso de dados no simulador Node-RED */
        @keyframes flowPacket {
            0% { left: 0%; opacity: 0; }
            15% { opacity: 1; }
            85% { opacity: 1; }
            100% { left: 100%; opacity: 0; }
        }

        .packet-anim {
            animation: flowPacket 1.6s cubic-bezier(0.4, 0, 0.2, 1) forwards;
        }

        /* Esconder scrollbar na navegação horizontal mobile */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 antialiased selection:bg-royal-600 selection:text-white">

    <!-- Barra de Navegação Fixa no Topo com Indicador de Progresso -->
    <header class="fixed top-0 left-0 right-0 z-50 bg-white/90 backdrop-blur-md border-b border-slate-200/80 shadow-sm">
        <div class="max-w-3xl mx-auto px-4 h-14 flex items-center justify-between gap-3">
            <!-- Identificação discreta -->
            <a href="#secao-1" class="flex items-center gap-2 shrink-0 group">
                <span class="w-7 h-7 rounded-lg bg-royal-800 text-white flex items-center justify-center font-mono text-xs font-bold shadow-sm group-hover:bg-royal-600 transition-colors">
                    IIoT
                </span>
                <span class="text-xs font-bold tracking-tight text-royal-900 hidden sm:inline">
                    Dados Industriais
                </span>
            </a>

            <!-- Links Rápidos para as 6 Etapas -->
            <nav aria-label="Navegação das etapas" class="flex items-center gap-1.5 overflow-x-auto no-scrollbar py-1">
                <a href="#secao-1" data-nav="secao-1" class="nav-pill px-2.5 py-1 rounded-full text-xs font-semibold transition-all bg-royal-800 text-white">1. Início</a>
                <a href="#secao-2" data-nav="secao-2" class="nav-pill px-2.5 py-1 rounded-full text-xs font-semibold text-slate-600 hover:bg-slate-100 transition-all">2. Roteiro</a>
                <a href="#secao-3" data-nav="secao-3" class="nav-pill px-2.5 py-1 rounded-full text-xs font-semibold text-slate-600 hover:bg-slate-100 transition-all">3. Ferramentas</a>
                <a href="#secao-4" data-nav="secao-4" class="nav-pill px-2.5 py-1 rounded-full text-xs font-semibold text-slate-600 hover:bg-slate-100 transition-all">4. Node-RED</a>
                <a href="#secao-5" data-nav="secao-5" class="nav-pill px-2.5 py-1 rounded-full text-xs font-semibold text-slate-600 hover:bg-slate-100 transition-all">5. Excel</a>
                <a href="#secao-6" data-nav="secao-6" class="nav-pill px-2.5 py-1 rounded-full text-xs font-semibold text-slate-600 hover:bg-slate-100 transition-all">6. Créditos</a>
            </nav>
        </div>
        <!-- Barra de Progresso de Leitura -->
        <div class="w-full h-1 bg-slate-100">
            <div id="reading-progress" class="h-full bg-gradient-to-r from-royal-600 to-sky-500 w-0 transition-all duration-150"></div>
        </div>
    </header>

    <!-- Conteúdo Principal Estritamente Vertical (Coluna Única Centralizada) -->
    <main class="pt-14">

        <!-- =====================================================================
             SEÇÃO 1: CAPA / HERO (NÚMERO 1)
             ===================================================================== -->
        <section id="secao-1" class="relative overflow-hidden bg-gradient-to-b from-royal-950 via-royal-900 to-royal-800 text-white py-16 sm:py-24 px-4 sm:px-6">
            <!-- Grade decorativa sutil -->
            <div class="absolute inset-0 opacity-10" style="background-image: radial-gradient(#93c5fd 1px, transparent 1px); background-size: 24px 24px;"></div>
            
            <div class="relative max-w-2xl mx-auto flex flex-col items-start">
                <!-- Número da Etapa + Badge -->
                <div class="flex items-center gap-3 mb-6">
                    <span class="w-9 h-9 rounded-full border-2 border-sky-400/60 bg-royal-800/80 text-sky-300 font-mono font-bold text-sm flex items-center justify-center shadow-inner">
                        1
                    </span>
                    <span class="inline-flex items-center gap-1.5 px-3.5 py-1 rounded-full text-xs font-semibold tracking-wider uppercase bg-sky-500/20 text-sky-200 border border-sky-400/30">
                        <span class="w-1.5 h-1.5 rounded-full bg-sky-400 animate-pulse"></span>
                        Projeto de Extensão
                    </span>
                </div>

                <!-- Título Principal -->
                <h1 class="text-3xl sm:text-5xl font-extrabold tracking-tight leading-tight text-white mb-4">
                    COLETA E TRATAMENTO DE DADOS INDUSTRIAIS
                </h1>

                <!-- Subtítulo em Destaque -->
                <p class="text-lg sm:text-xl font-medium text-sky-200 italic border-l-4 border-sky-400 pl-4 mb-6">
                    Do funcionamento da máquina à análise das informações
                </p>

                <!-- Descrição -->
                <p class="text-slate-200 text-base sm:text-lg leading-relaxed mb-8">
                    Aprenda como captar informações de uma planta industrial e transformá-las em dados para análise. 
                    <strong class="text-white font-semibold">Um guia prático utilizando OPC UA, Node-RED e Excel.</strong>
                </p>

                <!-- Ilustração / Diagrama Visual Estilizado em SVG/HTML -->
                <div class="w-full bg-royal-950/60 border border-royal-700/70 rounded-2xl p-5 sm:p-6 mb-9 shadow-xl backdrop-blur-sm">
                    <div class="text-xs font-mono uppercase tracking-wider text-sky-300/80 mb-4 flex items-center justify-between">
                        <span>Arquitetura do Fluxo Industrial</span>
                        <span class="text-emerald-400 flex items-center gap-1">
                            <span class="w-2 h-2 rounded-full bg-emerald-400"></span> Online
                        </span>
                    </div>
                    
                    <!-- Diagrama SVG Responsivo -->
                    <svg viewBox="0 0 640 170" class="w-full h-auto" role="img" aria-label="Diagrama ilustrando Planta Industrial conectada via OPC UA ao Node-RED e exportada para análise no Excel">
                        <defs>
                            <linearGradient id="lineGrad" x1="0%" y1="0%" x2="100%" y2="0%">
                                <stop offset="0%" stop-color="#38bdf8" />
                                <stop offset="100%" stop-color="#34d399" />
                            </linearGradient>
                        </defs>

                        <!-- Linhas de Conexão -->
                        <line x1="145" y1="85" x2="245" y2="85" stroke="url(#lineGrad)" stroke-width="3" stroke-dasharray="6 4" />
                        <line x1="395" y1="85" x2="495" y2="85" stroke="url(#lineGrad)" stroke-width="3" stroke-dasharray="6 4" />

                        <!-- Nó 1: Planta Industrial & Sensores -->
                        <g transform="translate(15, 25)">
                            <rect width="130" height="120" rx="14" fill="#1e293b" stroke="#38bdf8" stroke-width="1.5" />
                            <!-- Ícone Fábrica/Engrenagem -->
                            <path d="M40 65 V45 L55 55 V45 L70 55 V40 H85 V65 Z" fill="#38bdf8" opacity="0.9"/>
                            <circle cx="92" cy="42" r="5" fill="#34d399" />
                            <text x="65" y="88" text-anchor="middle" fill="#f8fafc" font-family="Inter, sans-serif" font-size="11" font-weight="700">PLANTA &amp; CLP</text>
                            <text x="65" y="104" text-anchor="middle" fill="#94a3b8" font-family="JetBrains Mono, monospace" font-size="9">Sensores / OPC UA</text>
                        </g>

                        <!-- Badge Protocolo -->
                        <g transform="translate(162, 62)">
                            <rect width="66" height="20" rx="10" fill="#0f172a" stroke="#38bdf8" stroke-width="1"/>
                            <text x="33" y="13" text-anchor="middle" fill="#7dd3fc" font-family="JetBrains Mono, monospace" font-size="9" font-weight="600">OPC UA</text>
                        </g>

                        <!-- Nó 2: Node-RED -->
                        <g transform="translate(245, 25)">
                            <rect width="150" height="120" rx="14" fill="#1e293b" stroke="#f87171" stroke-width="1.5" />
                            <!-- Blocos visuais de fluxo -->
                            <rect x="28" y="42" width="26" height="14" rx="4" fill="#60a5fa" />
                            <line x1="54" y1="49" x2="66" y2="49" stroke="#cbd5e1" stroke-width="2" />
                            <rect x="66" y="42" width="26" height="14" rx="4" fill="#fbbf24" />
                            <line x1="92" y1="49" x2="104" y2="49" stroke="#cbd5e1" stroke-width="2" />
                            <rect x="104" y="42" width="22" height="14" rx="4" fill="#34d399" />
                            <text x="75" y="88" text-anchor="middle" fill="#f8fafc" font-family="Inter, sans-serif" font-size="11" font-weight="700">NODE-RED</text>
                            <text x="75" y="104" text-anchor="middle" fill="#94a3b8" font-family="JetBrains Mono, monospace" font-size="9">Coleta &amp; Fluxo CSV</text>
                        </g>

                        <!-- Badge Exportação -->
                        <g transform="translate(412, 62)">
                            <rect width="66" height="20" rx="10" fill="#0f172a" stroke="#34d399" stroke-width="1"/>
                            <text x="33" y="13" text-anchor="middle" fill="#6ee7b7" font-family="JetBrains Mono, monospace" font-size="9" font-weight="600">.CSV</text>
                        </g>

                        <!-- Nó 3: Excel / Análise -->
                        <g transform="translate(495, 25)">
                            <rect width="130" height="120" rx="14" fill="#1e293b" stroke="#34d399" stroke-width="1.5" />
                            <!-- Gráfico de barras -->
                            <rect x="42" y="52" width="10" height="18" rx="2" fill="#34d399" opacity="0.6" />
                            <rect x="58" y="42" width="10" height="28" rx="2" fill="#34d399" opacity="0.85" />
                            <rect x="74" y="34" width="10" height="36" rx="2" fill="#34d399" />
                            <text x="65" y="88" text-anchor="middle" fill="#f8fafc" font-family="Inter, sans-serif" font-size="11" font-weight="700">EXCEL</text>
                            <text x="65" y="104" text-anchor="middle" fill="#94a3b8" font-family="JetBrains Mono, monospace" font-size="9">Tratamento &amp; KPI</text>
                        </g>
                    </svg>
                </div>

                <!-- Botão de Rolagem Suave -->
                <a href="#secao-2" class="w-full sm:w-auto inline-flex items-center justify-center gap-2.5 bg-sky-500 hover:bg-sky-400 text-royal-950 font-bold text-base px-7 py-4 rounded-xl shadow-lg shadow-sky-500/25 transition-all active:scale-[0.98]">
                    <span>Começar o Guia</span>
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
                    </svg>
                </a>
            </div>
        </section>

        <!-- =====================================================================
             SEÇÃO 2: O QUE VOCÊ VAI APRENDER? (NÚMERO 2)
             ===================================================================== -->
        <section id="secao-2" class="bg-tech-grid py-16 sm:py-20 px-4 sm:px-6 border-b border-slate-200">
            <div class="max-w-2xl mx-auto">
                <!-- Cabeçalho da Seção -->
                <div class="flex items-center gap-3.5 mb-8">
                    <span class="w-10 h-10 rounded-full bg-royal-800 text-white font-mono font-bold text-base flex items-center justify-center shadow-md shrink-0">
                        2
                    </span>
                    <div>
                        <span class="text-xs font-mono font-semibold uppercase tracking-wider text-royal-600 block">Visão Geral do Conteúdo</span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-royal-900 tracking-tight">
                            O que você vai aprender?
                        </h2>
                    </div>
                </div>

                <!-- Card com Lista Numerada dos 6 Tópicos -->
                <div class="bg-white rounded-2xl border-2 border-royal-800/15 shadow-lg shadow-slate-200/60 p-6 sm:p-8 mb-6">
                    <ol class="space-y-4">
                        <li class="flex items-center gap-4 p-3.5 rounded-xl bg-royal-50/70 border border-royal-100">
                            <span class="w-8 h-8 rounded-lg bg-royal-800 text-white font-mono font-bold text-sm flex items-center justify-center shrink-0">1</span>
                            <span class="font-bold text-royal-950 text-sm sm:text-base tracking-wide">CONHECENDO AS FERRAMENTAS</span>
                        </li>
                        <li class="flex items-center gap-4 p-3.5 rounded-xl bg-royal-50/70 border border-royal-100">
                            <span class="w-8 h-8 rounded-lg bg-royal-800 text-white font-mono font-bold text-sm flex items-center justify-center shrink-0">2</span>
                            <span class="font-bold text-royal-950 text-sm sm:text-base tracking-wide">PREPARANDO A COLETA DE DADOS</span>
                        </li>
                        <li class="flex items-center gap-4 p-3.5 rounded-xl bg-royal-50/70 border border-royal-100">
                            <span class="w-8 h-8 rounded-lg bg-royal-800 text-white font-mono font-bold text-sm flex items-center justify-center shrink-0">3</span>
                            <span class="font-bold text-royal-950 text-sm sm:text-base tracking-wide">CONFIGURANDO O NODE-RED</span>
                        </li>
                        <li class="flex items-center gap-4 p-3.5 rounded-xl bg-royal-50/70 border border-royal-100">
                            <span class="w-8 h-8 rounded-lg bg-royal-800 text-white font-mono font-bold text-sm flex items-center justify-center shrink-0">4</span>
                            <span class="font-bold text-royal-950 text-sm sm:text-base tracking-wide">REALIZANDO A COLETA</span>
                        </li>
                        <li class="flex items-center gap-4 p-3.5 rounded-xl bg-royal-50/70 border border-royal-100">
                            <span class="w-8 h-8 rounded-lg bg-royal-800 text-white font-mono font-bold text-sm flex items-center justify-center shrink-0">5</span>
                            <span class="font-bold text-royal-950 text-sm sm:text-base tracking-wide">EXPORTANDO OS DADOS</span>
                        </li>
                        <li class="flex items-center gap-4 p-3.5 rounded-xl bg-royal-50/70 border border-royal-100">
                            <span class="w-8 h-8 rounded-lg bg-royal-800 text-white font-mono font-bold text-sm flex items-center justify-center shrink-0">6</span>
                            <span class="font-bold text-royal-950 text-sm sm:text-base tracking-wide">ORGANIZANDO E ANALISANDO NO EXCEL</span>
                        </li>
                    </ol>
                </div>

                <!-- Texto Complementar -->
                <div class="bg-slate-100/90 border-l-4 border-royal-700 rounded-r-xl p-5 text-slate-700 text-sm sm:text-base leading-relaxed">
                    Apresentar, de maneira simples, como coletar informações de equipamentos industriais, organizar os registros e utilizar esses dados para compreender melhor os processos de uma indústria.
                </div>
            </div>
        </section>

        <!-- =====================================================================
             SEÇÃO 3: CONHECENDO AS FERRAMENTAS (NÚMERO 3)
             ===================================================================== -->
        <section id="secao-3" class="bg-white py-16 sm:py-20 px-4 sm:px-6 border-b border-slate-200">
            <div class="max-w-2xl mx-auto">
                <!-- Cabeçalho da Seção -->
                <div class="flex items-center gap-3.5 mb-8">
                    <span class="w-10 h-10 rounded-full bg-royal-800 text-white font-mono font-bold text-base flex items-center justify-center shadow-md shrink-0">
                        3
                    </span>
                    <div>
                        <span class="text-xs font-mono font-semibold uppercase tracking-wider text-royal-600 block">Ecossistema Tecnológico</span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-royal-900 tracking-tight">
                            CONHECENDO AS FERRAMENTAS
                        </h2>
                    </div>
                </div>

                <!-- 4 Cards Verticais Empilhados -->
                <div class="flex flex-col gap-5">
                    
                    <!-- Card 1: PLANTA INDUSTRIAL -->
                    <article class="group bg-slate-50 hover:bg-royal-50/40 border border-slate-200 hover:border-royal-300 rounded-2xl p-6 transition-all shadow-sm">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-xl bg-royal-800 text-white flex items-center justify-center shrink-0 shadow-sm">
                                <!-- Ícone Fábrica / Engrenagem -->
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
                                </svg>
                            </div>
                            <div>
                                <h3 class="text-lg font-extrabold text-royal-900 tracking-tight mb-1.5">
                                    PLANTA INDUSTRIAL
                                </h3>
                                <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                                    É o ambiente onde estão as máquinas, equipamentos e sensores que geram informações durante o funcionamento.
                                </p>
                            </div>
                        </div>
                    </article>

                    <!-- Card 2: OPC UA -->
                    <article class="group bg-slate-50 hover:bg-royal-50/40 border border-slate-200 hover:border-royal-300 rounded-2xl p-6 transition-all shadow-sm">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-xl bg-royal-700 text-white flex items-center justify-center shrink-0 shadow-sm">
                                <!-- Ícone Protocolo / Rede -->
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4" />
                                </svg>
                            </div>
                            <div>
                                <h3 class="text-lg font-extrabold text-royal-900 tracking-tight mb-1.5">
                                    OPC UA
                                </h3>
                                <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                                    É um protocolo de comunicação que permite a troca de informações entre equipamentos industriais e sistemas.
                                </p>
                            </div>
                        </div>
                    </article>

                    <!-- Card 3: NODE-RED -->
                    <article class="group bg-slate-50 hover:bg-royal-50/40 border border-slate-200 hover:border-royal-300 rounded-2xl p-6 transition-all shadow-sm">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-xl bg-rose-700 text-white flex items-center justify-center shrink-0 shadow-sm">
                                <!-- Ícone Fluxo de Nós -->
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h4v4H4V6zm12 8h4v4h-4v-4zM8 8h4a2 2 0 012 2v4a2 2 0 002 2h0" />
                                </svg>
                            </div>
                            <div>
                                <h3 class="text-lg font-extrabold text-royal-900 tracking-tight mb-1.5">
                                    NODE-RED
                                </h3>
                                <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                                    É uma ferramenta visual utilizada para conectar sistemas, receber e organizar dados.
                                </p>
                            </div>
                        </div>
                    </article>

                    <!-- Card 4: EXCEL -->
                    <article class="group bg-slate-50 hover:bg-royal-50/40 border border-slate-200 hover:border-royal-300 rounded-2xl p-6 transition-all shadow-sm">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 rounded-xl bg-emerald-700 text-white flex items-center justify-center shrink-0 shadow-sm">
                                <!-- Ícone Planilha / Dados -->
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M3 10h18M3 14h18m-9-4v8m-7 0h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
                                </svg>
                            </div>
                            <div>
                                <h3 class="text-lg font-extrabold text-royal-900 tracking-tight mb-1.5">
                                    EXCEL
                                </h3>
                                <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                                    Permite armazenar, organizar, tratar e analisar as informações coletadas.
                                </p>
                            </div>
                        </div>
                    </article>

                </div>
            </div>
        </section>

        <!-- =====================================================================
             SEÇÃO 4: COMO COLETAR OS DADOS PELO NODE-RED? (NÚMERO 4)
             ===================================================================== -->
        <section id="secao-4" class="bg-tech-grid py-16 sm:py-20 px-4 sm:px-6 border-b border-slate-200">
            <div class="max-w-2xl mx-auto">
                <!-- Cabeçalho da Seção -->
                <div class="flex items-center gap-3.5 mb-8">
                    <span class="w-10 h-10 rounded-full bg-royal-800 text-white font-mono font-bold text-base flex items-center justify-center shadow-md shrink-0">
                        4
                    </span>
                    <div>
                        <span class="text-xs font-mono font-semibold uppercase tracking-wider text-royal-600 block">Aquisição de Dados</span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-royal-900 tracking-tight">
                            COMO COLETAR OS DADOS PELO NODE-RED?
                        </h2>
                    </div>
                </div>

                <!-- Linha do Tempo Vertical com 5 Passos Numerados -->
                <div class="relative pl-8 sm:pl-10 border-l-2 border-royal-300 space-y-6 mb-10 ml-3">
                    
                    <!-- PASSO 1 -->
                    <div class="relative bg-white rounded-2xl border border-slate-200 p-5 shadow-sm">
                        <span class="absolute -left-[43px] sm:-left-[51px] top-5 w-7 h-7 rounded-full bg-royal-800 text-white font-mono text-xs font-bold flex items-center justify-center ring-4 ring-slate-50">
                            1
                        </span>
                        <h3 class="text-sm sm:text-base font-extrabold text-royal-800 uppercase tracking-wide mb-1">
                            PASSO 1 – ABRA O NODE-RED
                        </h3>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Acesse o Node-RED pelo navegador e abra o fluxo responsável pela coleta de dados.
                        </p>
                    </div>

                    <!-- PASSO 2 -->
                    <div class="relative bg-white rounded-2xl border border-slate-200 p-5 shadow-sm">
                        <span class="absolute -left-[43px] sm:-left-[51px] top-5 w-7 h-7 rounded-full bg-royal-800 text-white font-mono text-xs font-bold flex items-center justify-center ring-4 ring-slate-50">
                            2
                        </span>
                        <h3 class="text-sm sm:text-base font-extrabold text-royal-800 uppercase tracking-wide mb-1">
                            PASSO 2 – CONFIGURE A COMUNICAÇÃO
                        </h3>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Configure o cliente OPC UA com o endereço do servidor (Endpoint) e os NodeIDs das variáveis que deseja monitorar.
                        </p>
                    </div>

                    <!-- PASSO 3 -->
                    <div class="relative bg-white rounded-2xl border border-slate-200 p-5 shadow-sm">
                        <span class="absolute -left-[43px] sm:-left-[51px] top-5 w-7 h-7 rounded-full bg-royal-800 text-white font-mono text-xs font-bold flex items-center justify-center ring-4 ring-slate-50">
                            3
                        </span>
                        <h3 class="text-sm sm:text-base font-extrabold text-royal-800 uppercase tracking-wide mb-1">
                            PASSO 3 – INICIE A COLETA
                        </h3>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Utilize os botões de injeção (Inject) para iniciar as solicitações de leitura das variáveis.
                        </p>
                    </div>

                    <!-- PASSO 4 -->
                    <div class="relative bg-white rounded-2xl border border-slate-200 p-5 shadow-sm">
                        <span class="absolute -left-[43px] sm:-left-[51px] top-5 w-7 h-7 rounded-full bg-royal-800 text-white font-mono text-xs font-bold flex items-center justify-center ring-4 ring-slate-50">
                            4
                        </span>
                        <h3 class="text-sm sm:text-base font-extrabold text-royal-800 uppercase tracking-wide mb-1">
                            PASSO 4 – VERIFIQUE OS RESULTADOS
                        </h3>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Utilize o nó Debug para visualizar os dados recebidos e verificar se a coleta está funcionando.
                        </p>
                    </div>

                    <!-- PASSO 5 -->
                    <div class="relative bg-white rounded-2xl border border-slate-200 p-5 shadow-sm">
                        <span class="absolute -left-[43px] sm:-left-[51px] top-5 w-7 h-7 rounded-full bg-royal-800 text-white font-mono text-xs font-bold flex items-center justify-center ring-4 ring-slate-50">
                            5
                        </span>
                        <h3 class="text-sm sm:text-base font-extrabold text-royal-800 uppercase tracking-wide mb-1">
                            PASSO 5 – GERE O ARQUIVO
                        </h3>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Os dados passam pelos nós de formatação e conversão para CSV e, em seguida, são salvos no computador.
                        </p>
                    </div>

                </div>

                <!-- Diagrama Visual Interativo Simulando um Fluxo do Node-RED -->
                <div class="bg-slate-900 text-white rounded-2xl p-5 sm:p-6 shadow-xl border border-slate-700">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-5 pb-4 border-b border-slate-800">
                        <div>
                            <span class="text-xs font-mono text-sky-400 uppercase tracking-wider block">Simulador Interativo</span>
                            <h3 class="text-base font-bold text-white">Fluxo de Coleta Node-RED</h3>
                        </div>
                        <button id="btn-simular-nodered" type="button" class="inline-flex items-center justify-center gap-2 bg-royal-600 hover:bg-royal-500 active:scale-95 text-white font-semibold text-xs sm:text-sm px-4 py-2.5 rounded-xl shadow-md transition-all cursor-pointer">
                            <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                                <path d="M6.3 2.841A1.5 1.5 0 004 4.11V15.89a1.5 1.5 0 002.3 1.269l9.344-5.89a1.5 1.5 0 000-2.538L6.3 2.84z" />
                            </svg>
                            <span>Simular Injeção</span>
                        </button>
                    </div>

                    <!-- Área do Canvas/Fluxo (Responsivo vertical no mobile, horizontal no sm+) -->
                    <div class="relative bg-slate-950/90 rounded-xl p-4 border border-slate-800 overflow-hidden" style="background-image: radial-gradient(#334155 1px, transparent 1px); background-size: 16px 16px;">
                        
                        <div class="flex flex-col sm:flex-row items-center justify-between gap-3 sm:gap-2 relative z-10">
                            
                            <!-- Nó 1: Inject -->
                            <div id="node-inject" class="w-full sm:w-auto flex items-center justify-between sm:justify-start gap-2 bg-sky-600 border-2 border-sky-400 text-white px-3.5 py-2.5 rounded-lg shadow-md transition-transform">
                                <span class="w-3 h-3 rounded-sm bg-sky-200 inline-block"></span>
                                <span class="font-mono text-xs font-bold">Inject (Leitura)</span>
                                <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                            </div>

                            <!-- Conector 1 -->
                            <div class="h-5 w-0.5 sm:h-0.5 sm:flex-1 bg-slate-600 relative">
                                <div id="packet-1" class="hidden sm:block absolute -top-1.5 w-3.5 h-3.5 rounded-full bg-sky-400 shadow-[0_0_10px_#38bdf8] opacity-0"></div>
                            </div>

                            <!-- Nó 2: OPC UA Client -->
                            <div id="node-opcua" class="w-full sm:w-auto flex items-center justify-between sm:justify-start gap-2 bg-indigo-600 border-2 border-indigo-400 text-white px-3.5 py-2.5 rounded-lg shadow-md transition-transform">
                                <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                                <span class="font-mono text-xs font-bold">OPC UA Client</span>
                                <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                            </div>

                            <!-- Conector 2 -->
                            <div class="h-5 w-0.5 sm:h-0.5 sm:flex-1 bg-slate-600 relative">
                                <div id="packet-2" class="hidden sm:block absolute -top-1.5 w-3.5 h-3.5 rounded-full bg-amber-400 shadow-[0_0_10px_#fbbf24] opacity-0"></div>
                            </div>

                            <!-- Nó 3: Function / CSV -->
                            <div id="node-csv" class="w-full sm:w-auto flex items-center justify-between sm:justify-start gap-2 bg-amber-600 border-2 border-amber-400 text-white px-3.5 py-2.5 rounded-lg shadow-md transition-transform">
                                <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                                <span class="font-mono text-xs font-bold">Function / CSV</span>
                                <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                            </div>

                            <!-- Conector 3 -->
                            <div class="h-5 w-0.5 sm:h-0.5 sm:flex-1 bg-slate-600 relative">
                                <div id="packet-3" class="hidden sm:block absolute -top-1.5 w-3.5 h-3.5 rounded-full bg-emerald-400 shadow-[0_0_10px_#34d399] opacity-0"></div>
                            </div>

                            <!-- Nó 4: Debug & File Write -->
                            <div class="w-full sm:w-auto flex flex-col gap-2">
                                <div id="node-debug" class="flex items-center justify-between sm:justify-start gap-2 bg-emerald-600 border-2 border-emerald-400 text-white px-3 py-1.5 rounded-lg shadow-md transition-transform">
                                    <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                                    <span class="font-mono text-[11px] font-bold">Debug</span>
                                </div>
                                <div id="node-file" class="flex items-center justify-between sm:justify-start gap-2 bg-teal-700 border-2 border-teal-400 text-white px-3 py-1.5 rounded-lg shadow-md transition-transform">
                                    <span class="w-2.5 h-2.5 rounded-full bg-slate-300 border border-slate-700"></span>
                                    <span class="font-mono text-[11px] font-bold">File Write (.csv)</span>
                                </div>
                            </div>
                        </div>

                        <!-- Console de Saída (Debug & CSV Log) -->
                        <div class="mt-4 pt-3 border-t border-slate-800 font-mono text-xs">
                            <div class="flex items-center justify-between text-slate-400 mb-1.5">
                                <span>Painel Debug / Saída CSV:</span>
                                <span id="sim-status" class="text-slate-500">Aguardando injeção...</span>
                            </div>
                            <div id="sim-console" class="bg-black/60 text-emerald-400 p-3 rounded-lg border border-slate-800/80 min-h-[56px] leading-relaxed overflow-x-auto">
                                Clique em "Simular Injeção" acima para disparar a leitura do servidor OPC UA.
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- =====================================================================
             SEÇÃO 5: COMO TRATAR OS DADOS NO EXCEL? (NÚMERO 5)
             ===================================================================== -->
        <section id="secao-5" class="bg-white py-16 sm:py-20 px-4 sm:px-6 border-b border-slate-200">
            <div class="max-w-2xl mx-auto">
                <!-- Cabeçalho da Seção -->
                <div class="flex items-center gap-3.5 mb-8">
                    <span class="w-10 h-10 rounded-full bg-royal-800 text-white font-mono font-bold text-base flex items-center justify-center shadow-md shrink-0">
                        5
                    </span>
                    <div>
                        <span class="text-xs font-mono font-semibold uppercase tracking-wider text-royal-600 block">Tratamento e Inteligência</span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-royal-900 tracking-tight">
                            COMO TRATAR OS DADOS NO EXCEL?
                        </h2>
                    </div>
                </div>

                <!-- Passos Verticais -->
                <div class="space-y-5 mb-10">
                    
                    <!-- PASSO 1 -->
                    <div class="bg-slate-50 rounded-2xl border border-slate-200 p-6 shadow-sm">
                        <div class="flex items-center gap-3 mb-2">
                            <span class="px-2.5 py-0.5 rounded-md bg-royal-800 text-white font-mono text-xs font-bold">01</span>
                            <h3 class="text-base sm:text-lg font-extrabold text-royal-900">
                                PASSO 1 – IMPORTE O ARQUIVO
                            </h3>
                        </div>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Abra o Excel, acesse a guia <strong class="text-slate-800">Dados</strong> e selecione a opção <strong class="text-slate-800">De Texto/CSV</strong>. Localize o arquivo gerado pelo Node-RED.
                        </p>
                    </div>

                    <!-- PASSO 2 -->
                    <div class="bg-slate-50 rounded-2xl border border-slate-200 p-6 shadow-sm">
                        <div class="flex items-center gap-3 mb-2">
                            <span class="px-2.5 py-0.5 rounded-md bg-royal-800 text-white font-mono text-xs font-bold">02</span>
                            <h3 class="text-base sm:text-lg font-extrabold text-royal-900">
                                PASSO 2 – ORGANIZE A PLANILHA
                            </h3>
                        </div>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
                            Verifique se as informações estão separadas em colunas e se possuem títulos. Confira datas, horários e valores.
                        </p>
                    </div>

                    <!-- PASSO 3 -->
                    <div class="bg-slate-50 rounded-2xl border border-slate-200 p-6 shadow-sm">
                        <div class="flex items-center gap-3 mb-2">
                            <span class="px-2.5 py-0.5 rounded-md bg-royal-800 text-white font-mono text-xs font-bold">03</span>
                            <h3 class="text-base sm:text-lg font-extrabold text-royal-900">
                                PASSO 3 – ANALISE AS INFORMAÇÕES
                            </h3>
                        </div>
                        <p class="text-slate-600 text-sm sm:text-base leading-relaxed mb-3">
                            Utilize tabelas dinâmicas, fórmulas e gráficos para observar:
                        </p>
                        <ul class="space-y-2 text-slate-700 text-sm sm:text-base">
                            <li class="flex items-start gap-2.5">
                                <span class="w-1.5 h-1.5 rounded-full bg-royal-600 mt-2 shrink-0"></span>
                                <span>Quantidade de registros;</span>
                            </li>
                            <li class="flex items-start gap-2.5">
                                <span class="w-1.5 h-1.5 rounded-full bg-royal-600 mt-2 shrink-0"></span>
                                <span>Frequência dos estados dos equipamentos;</span>
                            </li>
                            <li class="flex items-start gap-2.5">
                                <span class="w-1.5 h-1.5 rounded-full bg-royal-600 mt-2 shrink-0"></span>
                                <span>Comparação entre valores;</span>
                            </li>
                            <li class="flex items-start gap-2.5">
                                <span class="w-1.5 h-1.5 rounded-full bg-royal-600 mt-2 shrink-0"></span>
                                <span>Tempo de operação, quando houver registros adequados de início e término.</span>
                            </li>
                        </ul>
                    </div>

                </div>

                <!-- Bloco de Destaque: RESULTADO FINAL -->
                <div class="bg-gradient-to-br from-royal-900 to-royal-800 text-white rounded-2xl p-6 sm:p-8 shadow-xl border border-royal-700">
                    <div class="inline-block px-3 py-1 rounded-full bg-sky-400/20 text-sky-300 font-mono text-xs font-bold uppercase tracking-wider mb-4">
                        RESULTADO FINAL
                    </div>

                    <!-- Fluxo Visual -->
                    <div class="flex flex-col sm:flex-row sm:flex-wrap items-center justify-between gap-2.5 bg-royal-950/60 p-4 rounded-xl border border-royal-700/70 mb-5 text-center">
                        <span class="w-full sm:w-auto px-3 py-2 rounded-lg bg-royal-800/90 border border-royal-600 text-xs sm:text-sm font-semibold text-sky-100">
                            Dados coletados
                        </span>
                        <span class="text-sky-400 font-bold text-lg rotate-90 sm:rotate-0">→</span>
                        <span class="w-full sm:w-auto px-3 py-2 rounded-lg bg-royal-800/90 border border-royal-600 text-xs sm:text-sm font-semibold text-sky-100">
                            Dados organizados
                        </span>
                        <span class="text-sky-400 font-bold text-lg rotate-90 sm:rotate-0">→</span>
                        <span class="w-full sm:w-auto px-3 py-2 rounded-lg bg-royal-800/90 border border-royal-600 text-xs sm:text-sm font-semibold text-sky-100">
                            Informações analisadas
                        </span>
                        <span class="text-sky-400 font-bold text-lg rotate-90 sm:rotate-0">→</span>
                        <span class="w-full sm:w-auto px-3 py-2 rounded-lg bg-emerald-600/90 border border-emerald-400 text-xs sm:text-sm font-bold text-white shadow-sm">
                            Resultados apresentados
                        </span>
                    </div>

                    <!-- Frase de Encerramento -->
                    <p class="text-base sm:text-lg font-bold text-sky-200 text-center sm:text-left">
                        Agora você sabe como transformar dados industriais em informações úteis!
                    </p>
                </div>
            </div>
        </section>

        <!-- =====================================================================
             SEÇÃO 6: DA COLETA À INFORMAÇÃO & CRÉDITOS / RODAPÉ (NÚMERO 6)
             ===================================================================== -->
        <section id="secao-6" class="bg-slate-900 text-slate-200 py-16 sm:py-20 px-4 sm:px-6">
            <div class="max-w-2xl mx-auto">
                <!-- Cabeçalho da Seção -->
                <div class="flex items-center gap-3.5 mb-6">
                    <span class="w-10 h-10 rounded-full bg-sky-500 text-royal-950 font-mono font-bold text-base flex items-center justify-center shadow-md shrink-0">
                        6
                    </span>
                    <div>
                        <span class="text-xs font-mono font-semibold uppercase tracking-wider text-sky-400 block">Conclusão & Autoria</span>
                        <h2 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
                            DA COLETA À INFORMAÇÃO
                        </h2>
                    </div>
                </div>

                <!-- Texto Principal -->
                <p class="text-lg sm:text-xl text-slate-300 leading-relaxed mb-10 border-l-4 border-sky-500 pl-4">
                    Os dados industriais podem revelar informações importantes sobre o funcionamento de uma máquina ou processo.
                </p>

                <!-- Card de Créditos Acadêmicos -->
                <div class="bg-slate-800/80 border border-slate-700 rounded-2xl p-6 sm:p-8 shadow-lg">
                    <div class="mb-6">
                        <h3 class="text-xs font-mono font-bold uppercase tracking-wider text-sky-400 mb-3">
                            Desenvolvido por:
                        </h3>
                        <ul class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 text-sm sm:text-base font-medium text-white">
                            <li class="flex items-center gap-2.5 bg-slate-900/60 px-3.5 py-2 rounded-lg border border-slate-700/60">
                                <span class="w-2 h-2 rounded-full bg-sky-400"></span>
                                <span>Amanda de França Beccaria</span>
                            </li>
                            <li class="flex items-center gap-2.5 bg-slate-900/60 px-3.5 py-2 rounded-lg border border-slate-700/60">
                                <span class="w-2 h-2 rounded-full bg-sky-400"></span>
                                <span>Gabriela Yasumura</span>
                            </li>
                            <li class="flex items-center gap-2.5 bg-slate-900/60 px-3.5 py-2 rounded-lg border border-slate-700/60">
                                <span class="w-2 h-2 rounded-full bg-sky-400"></span>
                                <span>Nicoly Rafaeli Branco Moura</span>
                            </li>
                            <li class="flex items-center gap-2.5 bg-slate-900/60 px-3.5 py-2 rounded-lg border border-slate-700/60">
                                <span class="w-2 h-2 rounded-full bg-sky-400"></span>
                                <span>Samyra Muniz</span>
                            </li>
                            <li class="flex items-center gap-2.5 bg-slate-900/60 px-3.5 py-2 rounded-lg border border-slate-700/60 sm:col-span-2">
                                <span class="w-2 h-2 rounded-full bg-sky-400"></span>
                                <span>Vitoria Vilela Freitas</span>
                            </li>
                        </ul>
                    </div>

                    <!-- Instituição / Curso -->
                    <div class="pt-5 border-t border-slate-700/80 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                        <div>
                            <span class="text-xs font-mono uppercase tracking-wider text-slate-400 block mb-1">Instituição / Curso</span>
                            <p class="text-sm sm:text-base font-bold text-white">
                                Engenharia de Controle e Automação – Centro Universitário Senai Armando Arruda Pereira
                            </p>
                        </div>
                        <a href="#secao-1" class="inline-flex items-center justify-center gap-1.5 text-xs font-semibold text-sky-400 hover:text-sky-300 bg-slate-900/80 px-3.5 py-2 rounded-lg border border-slate-700 shrink-0 transition-colors">
                            <span>Voltar ao topo</span>
                            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M5 10l7-7m0 0l7 7m-7-7v18" />
                            </svg>
                        </a>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Scripts de Interatividade: Barra de Progresso, Navegação Ativa e Simulador Node-RED -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // 1. Indicador de Progresso de Leitura Vertical
            const progressBar = document.getElementById('reading-progress');
            const sections = document.querySelectorAll('main section');
            const navPills = document.querySelectorAll('.nav-pill');

            function updateScrollProgress() {
                const scrollTop = window.scrollY;
                const docHeight = document.documentElement.scrollHeight - window.innerHeight;
                const scrollPercent = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0;
                progressBar.style.width = `${Math.min(100, Math.max(0, scrollPercent))}%`;

                // Atualizar pílula de navegação ativa
                let currentId = 'secao-1';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop - 120;
                    if (scrollTop >= sectionTop) {
                        currentId = section.getAttribute('id');
                    }
                });

                navPills.forEach(pill => {
                    if (pill.dataset.nav === currentId) {
                        pill.classList.remove('text-slate-600', 'hover:bg-slate-100');
                        pill.classList.add('bg-royal-800', 'text-white');
                    } else {
                        pill.classList.remove('bg-royal-800', 'text-white');
                        pill.classList.add('text-slate-600', 'hover:bg-slate-100');
                    }
                });
            }

            window.addEventListener('scroll', updateScrollProgress, { passive: true });
            updateScrollProgress();

            // 2. Simulador Interativo do Fluxo Node-RED (Seção 4)
            const btnSimular = document.getElementById('btn-simular-nodered');
            const simConsole = document.getElementById('sim-console');
            const simStatus = document.getElementById('sim-status');
            
            const nodeInject = document.getElementById('node-inject');
            const nodeOpcua = document.getElementById('node-opcua');
            const nodeCsv = document.getElementById('node-csv');
            const nodeDebug = document.getElementById('node-debug');
            const nodeFile = document.getElementById('node-file');

            const packet1 = document.getElementById('packet-1');
            const packet2 = document.getElementById('packet-2');
            const packet3 = document.getElementById('packet-3');

            let isSimulating = false;
            let sampleCounter = 104;

            function pulseNode(el) {
                el.classList.add('scale-105', 'ring-2', 'ring-white');
                setTimeout(() => {
                    el.classList.remove('scale-105', 'ring-2', 'ring-white');
                }, 350);
            }

            function triggerPacket(packetEl) {
                packetEl.classList.remove('packet-anim');
                void packetEl.offsetWidth; // Reflow para reiniciar animação
                packetEl.classList.add('packet-anim');
            }

            btnSimular.addEventListener('click', () => {
                if (isSimulating) return;
                isSimulating = true;
                sampleCounter++;

                const now = new Date();
                const timestamp = now.toLocaleTimeString('pt-BR');
                const dateStr = now.toLocaleDateString('pt-BR');
                const tempValue = (62 + Math.random() * 6).toFixed(1);
                const rpmValue = Math.floor(1440 + Math.random() * 40);

                // Etapa 1: Inject
                simStatus.textContent = '1/4 Injetando solicitação...';
                simStatus.className = 'text-sky-400';
                pulseNode(nodeInject);
                triggerPacket(packet1);
                simConsole.innerHTML = `<span class="text-sky-400">[${timestamp}] Inject:</span> Solicitando leitura dos NodeIDs (ns=2;s=Temp_Motor, ns=2;s=RPM)...`;

                // Etapa 2: OPC UA Client
                setTimeout(() => {
                    simStatus.textContent = '2/4 Lendo servidor OPC UA...';
                    simStatus.className = 'text-indigo-400';
                    pulseNode(nodeOpcua);
                    triggerPacket(packet2);
                    simConsole.innerHTML = `<span class="text-indigo-400">[${timestamp}] OPC UA Client:</span> Payload recebido -> { Temp: ${tempValue}°C, Rotacao: ${rpmValue} RPM, Status: "OPERANDO" }`;
                }, 650);

                // Etapa 3: Function / CSV
                setTimeout(() => {
                    simStatus.textContent = '3/4 Formatando linha CSV...';
                    simStatus.className = 'text-amber-400';
                    pulseNode(nodeCsv);
                    triggerPacket(packet3);
                }, 1300);

                // Etapa 4: Debug & File Write
                setTimeout(() => {
                    simStatus.textContent = '4/4 Salvo em dados_planta.csv!';
                    simStatus.className = 'text-emerald-400 font-semibold';
                    pulseNode(nodeDebug);
                    pulseNode(nodeFile);

                    simConsole.innerHTML = `
                        <div class="text-emerald-400 mb-1">✓ [Debug] Coleta #${sampleCounter} validada com sucesso!</div>
                        <div class="text-slate-300 bg-slate-900 px-2.5 py-1.5 rounded border border-slate-700 text-[11px]">
                            <span class="text-slate-500">dados_planta.csv &gt;</span> ${dateStr};${timestamp};${tempValue};${rpmValue};OPERANDO
                        </div>
                    `;
                    isSimulating = false;
                }, 1950);
            });
        });
    </script>
</body>
</html>
