<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agente de Inteligência de Mercado | M.ROSCOE</title>
    
    <!-- Google Fonts: Inter (Estética Looker Studio) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
    
    <!-- Lucide Icons -->
    <script src="https://cdn.jsdelivr.net/npm/lucide@0.468.0/dist/umd/lucide.min.js" onerror="var t=document.createElement('script');t.src='https://unpkg.com/lucide@0.468.0/dist/umd/lucide.min.js';document.head.appendChild(t);"></script>
    <script>window.safeIcons=function(){try{if(window.lucide&&lucide.createIcons)lucide.createIcons();}catch(e){}};window.addEventListener("load",function(){window.safeIcons();});</script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        mcharcoal: '#1A1A1A',
                        morange: '#EE7D26',
                        morangedark: '#D66914',
                        morangelight: '#F59B4E',
                        morangebg: '#FFF4EC',
                        mgreen: '#0F9D58',
                        mamber: '#F59E0B',
                        mred: '#D93025',
                        mbg: '#F4F6F9',
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #F4F6F9;
            color: #1E293B;
            font-family: 'Inter', sans-serif;
            -webkit-font-smoothing: antialiased;
        }

        /* Looker Studio Card Shadow & Border */
        .looker-card {
            background: #FFFFFF;
            border: 1px solid #E2E8F0;
            border-radius: 8px;
            box-shadow: 0 1px 2px 0 rgba(26, 26, 26, 0.04);
            transition: box-shadow 0.2s ease, border-color 0.2s ease;
        }

        .looker-card:hover {
            box-shadow: 0 4px 12px -2px rgba(238, 125, 38, 0.10);
        }

        /* Custom Scrollbar for Tables */
        .custom-scrollbar::-webkit-scrollbar {
            height: 8px;
            width: 8px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #F1F5F9;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #CBD5E1;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94A3B8;
        }

        /* Looker Studio Dropdown Control */
        .looker-control {
            background-color: #FFFFFF;
            border: 1px solid #CBD5E1;
            border-radius: 6px;
            transition: all 0.15s ease;
        }
        .looker-control:focus-within, .looker-control:hover {
            border-color: #EE7D26;
            box-shadow: 0 0 0 2px rgba(238, 125, 38, 0.15);
        }

        /* Tab Indicator */
        .tab-active {
            color: #EE7D26;
            border-bottom: 2px solid #EE7D26;
            background-color: #FFF4EC;
        }
        .tab-inactive {
            color: #64748B;
            border-bottom: 2px solid transparent;
        }
        .tab-inactive:hover {
            color: #1A1A1A;
            background-color: #F8FAFC;
        }

        /* Inline Agendor Status Select Pills */
        .agendor-select-add {
            background-color: #FFF4EC;
            color: #B85309;
            border-color: #F59B4E;
        }
        .agendor-select-added {
            background-color: #ECFDF5;
            color: #065F46;
            border-color: #6EE7B7;
        }
        .agendor-select-discard {
            background-color: #F8FAFC;
            color: #5F6368;
            border-color: #CBD5E1;
        }

        /* Modal Backdrop */
        .modal-backdrop {
            background-color: rgba(26, 26, 26, 0.58);
            backdrop-filter: blur(2px);
        }

        /* Mobile Scroll Snap Carousel & Hide Scrollbar */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }

        @media (max-width: 767px) {
            body {
                padding-bottom: 68px; /* Espaço para a Bottom Nav Bar fixa no celular */
            }
            .mobile-kpi-carousel {
                display: flex;
                overflow-x: auto;
                scroll-snap-type: x mandatory;
                gap: 0.75rem;
                padding-bottom: 4px;
            }
            .mobile-kpi-carousel > div {
                min-width: 82%;
                max-width: 82%;
                scroll-snap-align: start;
                flex-shrink: 0;
            }
            .mobile-bottom-sheet {
                align-items: flex-end !important;
                padding: 0 !important;
            }
            .mobile-bottom-sheet > div {
                border-bottom-left-radius: 0 !important;
                border-bottom-right-radius: 0 !important;
                max-height: 92vh !important;
            }
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- TOP BAR: Estilo Google Looker Studio Header com Identidade Oficial M.ROSCOE -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-xs">
        <div class="max-w-[1640px] mx-auto px-3 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row md:items-center md:justify-between py-2.5 sm:py-3 gap-2.5 sm:gap-3">
                
                <!-- Brand Logo Vetorial M.ROSCOE & Report Title -->
                <div class="flex items-center justify-between md:justify-start gap-3 sm:gap-4">
                    <div class="flex items-center gap-2.5 sm:gap-4 min-w-0">
                        <!-- Logo oficial M.ROSCOE (imagem enviada pelo usuário, embutida) -->
                        <div class="flex flex-col items-center justify-center px-2 py-1 sm:px-2.5 sm:py-1.5 rounded-lg bg-white border border-slate-200/90 shadow-2xs shrink-0" title="M.ROSCOE Engenharia e Construção">
                            <img src="data:image/png;base64,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" alt="Logo M.ROSCOE" class="h-[34px] sm:h-[44px] w-auto block" style="aspect-ratio:1.581">
                        </div>

                        <div class="h-9 w-px bg-slate-200 hidden sm:block"></div>

                        <div class="min-w-0">
                            <div class="flex flex-wrap items-center gap-1.5 sm:gap-2">
                                <h1 class="text-sm sm:text-xl font-extrabold text-[#1A1A1A] tracking-tight leading-tight truncate">
                                    <span class="sm:hidden">Inteligência de Mercado</span>
                                    <span class="hidden sm:inline">Agente de Inteligência de Mercado</span>
                                </h1>
                                <span class="inline-flex items-center gap-1 text-[10px] sm:text-xs font-bold text-[#EE7D26] bg-[#FFF4EC] border border-[#F59B4E]/60 px-2 py-0.5 rounded-full shrink-0">
                                    <i data-lucide="calendar" class="w-3 h-3"></i>
                                    23/11/2026
                                </span>
                            </div>
                            <div class="text-[11px] sm:text-xs text-slate-500 mt-0.5 flex flex-wrap items-center gap-x-2 gap-y-0.5">
                                <span class="hidden sm:inline font-semibold text-slate-700">Prospecção Privada (&gt; R$ 30 mi)</span>
                                <span class="hidden sm:inline text-slate-300">|</span>
                                <!-- Indicador de Sincronização Online em Tempo Real -->
                                <span id="syncStatusIndicator" class="inline-flex items-center gap-1.5 font-semibold text-emerald-700">
                                    <span id="syncStatusDot" class="w-2 h-2 rounded-full bg-[#0F9D58]"></span>
                                    <span id="syncStatusText">Sincronizado online</span>
                                </span>
                            </div>
                        </div>
                    </div>

                    <!-- Botão Mobile Compacto: Salvar Online -->
                    <button onclick="saveOnlineNow()" class="md:hidden inline-flex items-center gap-1.5 text-xs font-bold text-white bg-[#EE7D26] active:bg-[#D66914] px-3 py-2 rounded-lg shadow-xs shrink-0 cursor-pointer" title="Salvar alterações online sem criar cópias">
                        <i data-lucide="cloud-upload" class="w-3.5 h-3.5"></i>
                        <span>Salvar</span>
                    </button>
                </div>

                <!-- Right Controls (Desktop & Tablet): Salvar Online, Copiar Link, Sobrescrever Local, CSV & Reset -->
                <div class="hidden md:flex flex-wrap items-center justify-end gap-2">
                    <div id="activeFilterBadge" class="hidden items-center gap-1.5 text-xs font-semibold bg-[#FFF4EC] text-[#EE7D26] border border-[#F59B4E] px-2.5 py-1.5 rounded-md">
                        <span class="w-2 h-2 rounded-full bg-[#EE7D26] animate-pulse"></span>
                        <span id="activeFilterCount">Filtros ativos</span>
                    </div>
                    
                    <button onclick="resetAllFilters()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-600 hover:text-[#1A1A1A] bg-slate-100 hover:bg-slate-200/80 px-2.5 py-1.5 rounded-md transition cursor-pointer" title="Limpar filtros da tela">
                        <i data-lucide="filter-x" class="w-3.5 h-3.5"></i>
                        <span>Limpar Filtros</span>
                    </button>

                    <button onclick="resetAgendorStatus()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-600 hover:text-red-700 bg-white hover:bg-red-50 border border-slate-300 hover:border-red-200 px-2.5 py-1.5 rounded-md transition cursor-pointer" title="Voltar ao estado original da planilha">
                        <i data-lucide="rotate-ccw" class="w-3.5 h-3.5"></i>
                        <span>Resetar</span>
                    </button>

                    <button onclick="exportCSV()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#1A1A1A] bg-white hover:bg-slate-50 border border-slate-300 px-2.5 py-1.5 rounded-md shadow-2xs transition cursor-pointer" title="Exportar planilha atualizada em CSV (Excel)">
                        <i data-lucide="file-spreadsheet" class="w-3.5 h-3.5 text-[#0F9D58]"></i>
                        <span>CSV</span>
                    </button>

                    <button onclick="overwriteLocalFile()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-slate-700 bg-white hover:bg-slate-50 border border-slate-300 px-2.5 py-1.5 rounded-md shadow-2xs transition cursor-pointer" title="Sobrescrever o mesmo arquivo .html no computador sem criar cópias">
                        <i data-lucide="file-check-2" class="w-3.5 h-3.5 text-[#EE7D26]"></i>
                        <span>Sobrescrever Local</span>
                    </button>

                    <button onclick="copyShareableLink()" class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#EE7D26] bg-[#FFF4EC] hover:bg-[#FDE6D4] border border-[#F59B4E] px-3 py-1.5 rounded-md transition cursor-pointer" title="Copiar link online já contendo todos os status atualizados">
                        <i data-lucide="share-2" class="w-3.5 h-3.5"></i>
                        <span id="shareLinkBtnText">Copiar Link Atualizado</span>
                    </button>

                    <button onclick="saveOnlineNow()" class="inline-flex items-center gap-1.5 text-xs font-bold text-white bg-[#EE7D26] hover:bg-[#D66914] px-3.5 py-1.5 rounded-md shadow-xs transition cursor-pointer" title="Sincronizar e salvar na versão online sem gerar cópias de arquivo">
                        <i data-lucide="cloud-upload" class="w-3.5 h-3.5"></i>
                        <span>Salvar Online</span>
                    </button>
                </div>
            </div>

            <!-- Navigation Tabs (Desktop Only - no celular usamos a Bottom Bar fixa) -->
            <nav class="hidden md:flex items-center gap-1 -mb-px overflow-x-auto" aria-label="Páginas do Relatório">
                <button id="tabBtnOverview" onclick="switchTab('overview')" class="tab-active flex items-center gap-2 px-4 py-2.5 text-sm font-semibold whitespace-nowrap transition cursor-pointer rounded-t-md">
                    <i data-lucide="layout-dashboard" class="w-4 h-4"></i>
                    <span>1. Oportunidades Ativas &amp; Pipeline</span>
                    <span id="badgeCountOverview" class="ml-1 text-xs bg-[#FDE6D4] text-[#D66914] px-2 py-0.5 rounded-full font-bold">24</span>
                </button>
                <button id="tabBtnDiscarded" onclick="switchTab('discarded')" class="tab-inactive flex items-center gap-2 px-4 py-2.5 text-sm font-semibold whitespace-nowrap transition cursor-pointer rounded-t-md">
                    <i data-lucide="archive" class="w-4 h-4"></i>
                    <span>2. Descartados, Monitorar &amp; Metodologia</span>
                    <span class="ml-1 text-xs bg-slate-200 text-slate-700 px-2 py-0.5 rounded-full font-bold">6</span>
                </button>
            </nav>
        </div>
    </header>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="flex-1 max-w-[1640px] w-full mx-auto px-3 sm:px-6 lg:px-8 py-3.5 sm:py-5">

        <!-- ===================================================================== -->
        <!-- PAGE 1: OPORTUNIDADES ATIVAS & PIPELINE                               -->
        <!-- ===================================================================== -->
        <div id="pageOverview" class="space-y-4 sm:space-y-5">

            <!-- MOBILE FILTER DRAWER TRIGGER BAR (Visível apenas em smartphones) -->
            <div class="md:hidden flex items-center justify-between gap-2">
                <button onclick="toggleMobileFilters()" class="flex-1 looker-card px-3.5 py-2.5 flex items-center justify-between text-xs font-bold text-slate-800 active:bg-slate-50 cursor-pointer">
                    <span class="flex items-center gap-2">
                        <i data-lucide="sliders-horizontal" class="w-4 h-4 text-[#EE7D26]"></i>
                        <span>Filtrar Oportunidades</span>
                        <span id="mobileFilterBadgeCount" class="hidden bg-[#EE7D26] text-white text-[10px] font-extrabold px-1.5 py-0.5 rounded-full">0</span>
                    </span>
                    <i id="mobileFilterChevron" data-lucide="chevron-down" class="w-4 h-4 text-slate-400 transition-transform"></i>
                </button>
                <button onclick="copyShareableLink()" class="looker-card px-3 py-2.5 flex items-center gap-1.5 text-xs font-bold text-[#EE7D26] active:bg-[#FFF4EC] shrink-0 cursor-pointer" title="Compartilhar link atualizado">
                    <i data-lucide="share-2" class="w-4 h-4"></i>
                    <span>Link</span>
                </button>
            </div>

            <!-- LOOKER STUDIO FILTER CONTROL BAR (Retrátil no Mobile, Sempre Aberto no Desktop) -->
            <section id="filterControlSection" class="hidden md:block looker-card p-3.5 bg-white">
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-12 gap-3 items-end">
                    
                    <!-- Control 1: Status Agendor -->
                    <div class="lg:col-span-3">
                        <label for="filterAgendor" class="block text-[11px] font-semibold uppercase tracking-wider text-slate-500 mb-1 flex items-center gap-1">
                            <i data-lucide="check-square" class="w-3 h-3 text-[#EE7D26]"></i> Status Agendor
                        </label>
                        <div class="looker-control relative">
                            <select id="filterAgendor" onchange="applyFilters()" class="w-full appearance-none bg-transparent pl-3 pr-8 py-2 text-xs sm:text-sm font-medium text-slate-800 focus:outline-none cursor-pointer">
                                <option value="ALL">Todos os Status Agendor (24)</option>
                                <option value="Adicionar Oportunidade no Agendor">Adicionar Oportunidade no Agendor</option>
                                <option value="Oportunidade já adicionada no Agendor">Oportunidade já adicionada no Agendor</option>
                                <option value="Desconsiderar oportunidade">Desconsiderar oportunidade</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 text-slate-400 absolute right-2.5 top-1/2 -translate-y-1/2 pointer-events-none"></i>
                        </div>
                    </div>

                    <!-- Control 2: Segmento M.ROSCOE (Todos os 9 oficiais) -->
                    <div class="lg:col-span-3">
                        <label for="filterSegment" class="block text-[11px] font-semibold uppercase tracking-wider text-slate-500 mb-1 flex items-center gap-1">
                            <i data-lucide="factory" class="w-3 h-3 text-[#EE7D26]"></i> Segmento M.ROSCOE
                        </label>
                        <div class="looker-control relative">
                            <select id="filterSegment" onchange="applyFilters()" class="w-full appearance-none bg-transparent pl-3 pr-8 py-2 text-xs sm:text-sm font-medium text-slate-800 focus:outline-none cursor-pointer">
                                <option value="ALL">Todos os 9 Segmentos Oficiais</option>
                                <option value="Siderurgia e metalurgia">Siderurgia e metalurgia</option>
                                <option value="Mineração e fertilizantes">Mineração e fertilizantes</option>
                                <option value="Alimentos e bebidas">Alimentos e bebidas</option>
                                <option value="Indústria cimentícia">Indústria cimentícia</option>
                                <option value="Indústria da transformação">Indústria da transformação</option>
                                <option value="Farmacêutico e químico">Farmacêutico e químico</option>
                                <option value="Papel e celulose">Papel e celulose</option>
                                <option value="Edificações">Edificações</option>
                                <option value="Outras obras">Outras obras</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 text-slate-400 absolute right-2.5 top-1/2 -translate-y-1/2 pointer-events-none"></i>
                        </div>
                    </div>

                    <!-- Control 3: Mês de Captação -->
                    <div class="lg:col-span-2">
                        <label for="filterMonth" class="block text-[11px] font-semibold uppercase tracking-wider text-slate-500 mb-1 flex items-center gap-1">
                            <i data-lucide="calendar-days" class="w-3 h-3 text-[#EE7D26]"></i> Mês de Captação
                        </label>
                        <div class="looker-control relative">
                            <select id="filterMonth" onchange="applyFilters()" class="w-full appearance-none bg-transparent pl-3 pr-8 py-2 text-xs sm:text-sm font-medium text-slate-800 focus:outline-none cursor-pointer">
                                <option value="ALL">Todos os Meses</option>
                                <option value="Mai/2025">Mai/2025</option>
                                <option value="Fev/2026">Fev/2026</option>
                                <option value="Ago/2026">Ago/2026</option>
                                <option value="Set/2026">Set/2026</option>
                                <option value="Out/2026">Out/2026</option>
                                <option value="Nov/2026">Nov/2026</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 text-slate-400 absolute right-2.5 top-1/2 -translate-y-1/2 pointer-events-none"></i>
                        </div>
                    </div>

                    <!-- Control 4: Estado (UF) -->
                    <div class="lg:col-span-2">
                        <label for="filterState" class="block text-[11px] font-semibold uppercase tracking-wider text-slate-500 mb-1 flex items-center gap-1">
                            <i data-lucide="map-pin" class="w-3 h-3 text-[#EE7D26]"></i> Estado (UF)
                        </label>
                        <div class="looker-control relative">
                            <select id="filterState" onchange="applyFilters()" class="w-full appearance-none bg-transparent pl-3 pr-8 py-2 text-xs sm:text-sm font-medium text-slate-800 focus:outline-none cursor-pointer">
                                <option value="ALL">Todos os Estados</option>
                                <option value="MG">MG — Minas Gerais</option>
                                <option value="SP">SP — São Paulo</option>
                                <option value="AM">AM — Amazonas</option>
                                <option value="RS">RS — Rio Grande do Sul</option>
                                <option value="PR">PR — Paraná</option>
                                <option value="SC">SC — Santa Catarina</option>
                                <option value="MS">MS — Mato Grosso do Sul</option>
                                <option value="MT">MT — Mato Grosso</option>
                                <option value="RJ">RJ — Rio de Janeiro</option>
                                <option value="BA/CE">BA / CE — Bahia e Ceará</option>
                                <option value="Não divulgado">Não divulgado</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 text-slate-400 absolute right-2.5 top-1/2 -translate-y-1/2 pointer-events-none"></i>
                        </div>
                    </div>

                    <!-- Control 5: Origem da informação -->
                    <div class="lg:col-span-2">
                        <label for="filterOrigin" class="block text-[11px] font-semibold uppercase tracking-wider text-slate-500 mb-1 flex items-center gap-1">
                            <i data-lucide="inbox" class="w-3 h-3 text-[#EE7D26]"></i> Origem
                        </label>
                        <div class="looker-control relative">
                            <select id="filterOrigin" onchange="applyFilters()" class="w-full appearance-none bg-transparent pl-3 pr-8 py-2 text-xs sm:text-sm font-medium text-slate-800 focus:outline-none cursor-pointer">
                                <option value="ALL">Todas as Origens</option>
                            </select>
                            <i data-lucide="chevron-down" class="w-4 h-4 text-slate-400 absolute right-2.5 top-1/2 -translate-y-1/2 pointer-events-none"></i>
                        </div>
                    </div>

                    <!-- Control 6: Busca Rápida -->
                    <div class="lg:col-span-12 sm:col-span-2">
                        <label for="filterSearch" class="block text-[11px] font-semibold uppercase tracking-wider text-slate-500 mb-1 flex items-center gap-1">
                            <i data-lucide="search" class="w-3 h-3 text-[#EE7D26]"></i> Busca Rápida
                        </label>
                        <div class="looker-control relative flex items-center">
                            <i data-lucide="search" class="w-3.5 h-3.5 text-slate-400 ml-2.5 shrink-0"></i>
                            <input type="text" id="filterSearch" oninput="applyFilters()" placeholder="Empresa, obra, decisor..." class="w-full bg-transparent px-2 py-2 text-xs sm:text-sm text-slate-800 placeholder-slate-400 focus:outline-none">
                            <button id="clearSearchBtn" onclick="clearSearch()" class="hidden mr-2 text-slate-400 hover:text-slate-600 cursor-pointer" title="Limpar busca">
                                <i data-lucide="x" class="w-3.5 h-3.5"></i>
                            </button>
                        </div>
                    </div>

                </div>

                <!-- Mobile Drawer Extra Actions -->
                <div class="md:hidden mt-3 pt-3 border-t border-slate-100 flex items-center justify-between gap-2">
                    <button onclick="resetAllFilters()" class="flex-1 py-2 px-3 rounded-md bg-slate-100 text-slate-700 text-xs font-semibold flex items-center justify-center gap-1.5 cursor-pointer">
                        <i data-lucide="filter-x" class="w-3.5 h-3.5"></i>
                        <span>Limpar Filtros</span>
                    </button>
                    <button onclick="exportCSV()" class="flex-1 py-2 px-3 rounded-md bg-emerald-50 text-emerald-800 border border-emerald-200 text-xs font-semibold flex items-center justify-center gap-1.5 cursor-pointer">
                        <i data-lucide="file-spreadsheet" class="w-3.5 h-3.5"></i>
                        <span>Exportar CSV</span>
                    </button>
                </div>
            </section>

            <!-- SCORECARDS ROW (Carrossel Horizontal Snap no Celular / Grid 5 Colunas no Desktop) -->
            <section id="sectionScorecards">
                <div class="md:hidden flex items-center justify-between mb-1.5 px-0.5">
                    <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Indicadores Executivos</span>
                    <span class="text-[11px] text-slate-400 flex items-center gap-1">Deslize <i data-lucide="arrow-right" class="w-3 h-3"></i></span>
                </div>
                <div class="mobile-kpi-carousel no-scrollbar md:grid md:grid-cols-2 lg:grid-cols-5 md:gap-3.5">
                    
                    <!-- KPI 1: Total de Oportunidades -->
                    <div class="looker-card p-3.5 sm:p-4 border-t-4 border-t-[#1A1A1A] flex flex-col justify-between">
                        <div class="flex items-start justify-between gap-2">
                            <span class="text-xs font-semibold text-slate-500 uppercase tracking-wide">Total de Oportunidades</span>
                            <div class="p-1.5 rounded-md bg-slate-100 text-[#1A1A1A]">
                                <i data-lucide="building-2" class="w-4 h-4"></i>
                            </div>
                        </div>
                        <div class="my-1.5 sm:my-2">
                            <div id="kpiTotalObras" class="text-2xl sm:text-3xl font-bold text-[#1A1A1A] tracking-tight">24 obras</div>
                        </div>
                        <div id="kpiTotalSub" class="text-xs text-slate-500 pt-2 border-t border-slate-100 leading-snug">19 com CAPEX informado (+5 N/D)</div>
                    </div>

                    <!-- KPI 2: CAPEX Total Mapeado -->
                    <div class="looker-card p-3.5 sm:p-4 border-t-4 border-t-[#EE7D26] flex flex-col justify-between">
                        <div class="flex items-start justify-between gap-2">
                            <span class="text-xs font-semibold text-slate-500 uppercase tracking-wide">CAPEX Total Mapeado</span>
                            <div class="p-1.5 rounded-md bg-[#FFF4EC] text-[#EE7D26]">
                                <i data-lucide="banknote" class="w-4 h-4"></i>
                            </div>
                        </div>
                        <div class="my-1.5 sm:my-2">
                            <div id="kpiTotalCapex" class="text-2xl sm:text-3xl font-bold text-[#EE7D26] tracking-tight">R$ 82,99 bi</div>
                        </div>
                        <div id="kpiCapexSub" class="text-xs text-slate-500 pt-2 border-t border-slate-100 leading-snug">R$ 82.990 mi somados na base filtrada</div>
                    </div>

                    <!-- KPI 3: Adicionar no Agendor (Destaque Laranja M.ROSCOE) -->
                    <div class="looker-card p-3.5 sm:p-4 border-t-4 border-t-[#EE7D26] flex flex-col justify-between">
                        <div class="flex items-start justify-between gap-2">
                            <span class="text-xs font-semibold text-slate-500 uppercase tracking-wide">Adicionar no Agendor</span>
                            <div class="p-1.5 rounded-md bg-[#FFF4EC] text-[#EE7D26]">
                                <i data-lucide="plus-circle" class="w-4 h-4"></i>
                            </div>
                        </div>
                        <div class="my-1.5 sm:my-2 flex items-baseline gap-2">
                            <div id="kpiAddCount" class="text-2xl sm:text-3xl font-bold text-[#EE7D26] tracking-tight">16 obras</div>
                        </div>
                        <div id="kpiAddCapex" class="text-xs font-semibold text-[#B85309] bg-[#FFF4EC] px-2 py-1 rounded border border-[#F59B4E]/50">CAPEX: R$ 65,63 bi</div>
                    </div>

                    <!-- KPI 4: Já no Agendor (Verde Esmeralda) -->
                    <div class="looker-card p-3.5 sm:p-4 border-t-4 border-t-[#0F9D58] flex flex-col justify-between">
                        <div class="flex items-start justify-between gap-2">
                            <span class="text-xs font-semibold text-slate-500 uppercase tracking-wide">Já no Agendor</span>
                            <div class="p-1.5 rounded-md bg-emerald-50 text-[#0F9D58]">
                                <i data-lucide="check-circle-2" class="w-4 h-4"></i>
                            </div>
                        </div>
                        <div class="my-1.5 sm:my-2 flex items-baseline gap-2">
                            <div id="kpiAddedCount" class="text-2xl sm:text-3xl font-bold text-[#0F9D58] tracking-tight">6 obras</div>
                        </div>
                        <div id="kpiAddedCapex" class="text-xs font-semibold text-emerald-800 bg-emerald-50/80 px-2 py-1 rounded border border-emerald-200">CAPEX: R$ 13,86 bi</div>
                    </div>

                    <!-- KPI 5: Desconsiderar / Contatos Decisores -->
                    <div class="looker-card p-3.5 sm:p-4 border-t-4 border-t-[#5F6368] flex flex-col justify-between sm:col-span-2 lg:col-span-1">
                        <div class="flex items-start justify-between gap-2">
                            <span class="text-xs font-semibold text-slate-500 uppercase tracking-wide">Desconsiderar / Decisores</span>
                            <div class="p-1.5 rounded-md bg-slate-100 text-[#5F6368]">
                                <i data-lucide="ban" class="w-4 h-4"></i>
                            </div>
                        </div>
                        <div class="my-1.5 sm:my-2 flex items-baseline justify-between gap-2">
                            <div id="kpiDiscardCount" class="text-2xl sm:text-3xl font-bold text-[#5F6368] tracking-tight">2 obras</div>
                            <span id="kpiDecisoresBadge" class="text-xs font-bold text-[#1A1A1A] bg-[#FFF4EC] border border-[#F59B4E]/60 px-2 py-0.5 rounded-full">4 decisores</span>
                        </div>
                        <div id="kpiDiscardSub" class="text-xs text-slate-500 pt-2 border-t border-slate-100 leading-snug truncate" title="Aeroflex, Britânia, Potássio do Brasil">CAPEX desc.: R$ 3,50 bi • 4 contatos nominais</div>
                    </div>

                </div>
            </section>

            <!-- CHARTS ROW (3 INTERACTIVE LOOKER STUDIO WIDGETS) -->
            <section id="sectionCharts" class="grid grid-cols-1 lg:grid-cols-12 gap-4">
                
                <!-- Chart 1: CAPEX e Oportunidades por Segmento M.ROSCOE (Todos os 9 oficiais) -->
                <div class="looker-card p-4 lg:col-span-5 flex flex-col">
                    <div class="flex flex-wrap items-center justify-between gap-2 mb-3">
                        <div>
                            <h2 id="chartSegmentTitle" class="text-sm font-bold text-slate-800">Oportunidades por Segmento Oficial M.ROSCOE (R$ mi)</h2>
                            <p class="text-[11px] text-slate-500">Todos os 9 segmentos oficiais (ordenados por volume)</p>
                        </div>
                        <!-- Looker Studio Metric Switcher -->
                        <div class="inline-flex rounded-md bg-slate-100 p-0.5 border border-slate-200">
                            <button id="btnMetricCapex" onclick="toggleSegmentMetric('capex')" class="px-2.5 py-1 text-[11px] font-semibold rounded bg-[#EE7D26] text-white shadow-xs transition cursor-pointer">
                                Valor (R$ mi)
                            </button>
                            <button id="btnMetricCount" onclick="toggleSegmentMetric('count')" class="px-2.5 py-1 text-[11px] font-semibold rounded text-slate-600 hover:text-slate-900 transition cursor-pointer">
                                Qtd. Obras
                            </button>
                        </div>
                    </div>
                    <div class="relative flex-1 min-h-[260px] sm:min-h-[280px] w-full">
                        <canvas id="chartSegments"></canvas>
                    </div>
                </div>

                <!-- Chart 2: Donut - Status de Triagem Agendor -->
                <div class="looker-card p-4 lg:col-span-3 flex flex-col">
                    <div class="mb-3">
                        <h2 class="text-sm font-bold text-slate-800">Status de Triagem Agendor</h2>
                        <p class="text-[11px] text-slate-500">Decisão comercial em tempo real</p>
                    </div>
                    <div class="relative flex-1 min-h-[185px] flex items-center justify-center">
                        <canvas id="chartAgendor"></canvas>
                    </div>
                    <div class="mt-3 pt-2.5 border-t border-slate-100 space-y-2 text-xs">
                        <div class="flex items-center justify-between gap-2">
                            <span class="flex items-center gap-1.5 font-medium text-slate-700 truncate">
                                <span class="w-2.5 h-2.5 rounded-full bg-[#EE7D26] shrink-0"></span>
                                <span class="truncate">Adicionar no Agendor</span>
                            </span>
                            <span id="legendAgendorAdd" class="font-bold text-slate-900 shrink-0">16 (66,7%)</span>
                        </div>
                        <div class="flex items-center justify-between gap-2">
                            <span class="flex items-center gap-1.5 font-medium text-slate-700 truncate">
                                <span class="w-2.5 h-2.5 rounded-full bg-[#0F9D58] shrink-0"></span>
                                <span class="truncate">Já adicionada no Agendor</span>
                            </span>
                            <span id="legendAgendorAdded" class="font-bold text-slate-900 shrink-0">6 (25,0%)</span>
                        </div>
                        <div class="flex items-center justify-between gap-2">
                            <span class="flex items-center gap-1.5 font-medium text-slate-700 truncate">
                                <span class="w-2.5 h-2.5 rounded-full bg-[#5F6368] shrink-0"></span>
                                <span class="truncate">Desconsiderar</span>
                            </span>
                            <span id="legendAgendorDiscard" class="font-bold text-slate-900 shrink-0">2 (8,3%)</span>
                        </div>
                    </div>
                </div>

                <!-- Chart 3: Oportunidades e CAPEX por Mês (Ago/2026 a Nov/2026) -->
                <div class="looker-card p-4 lg:col-span-4 flex flex-col">
                    <div class="flex items-center justify-between gap-2 mb-3">
                        <div>
                            <h2 class="text-sm font-bold text-slate-800">Oportunidades e CAPEX por Mês</h2>
                            <p class="text-[11px] text-slate-500">Captação de notícias (Mai/2025 a Nov/2026)</p>
                        </div>
                        <span class="text-[11px] font-semibold text-[#EE7D26] bg-[#FFF4EC] px-2 py-0.5 rounded border border-[#F59B4E]/60">Cronológico</span>
                    </div>
                    <div class="relative flex-1 min-h-[260px] sm:min-h-[280px] w-full">
                        <canvas id="chartMonths"></canvas>
                    </div>
                </div>

            </section>

            <!-- OPPORTUNITIES LIST SECTION (Cards Executivos no Mobile + Tabela Completa no Desktop) -->
            <section id="sectionOpportunities" class="looker-card overflow-hidden">
                <div class="p-3.5 sm:p-4 border-b border-slate-200 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-2.5 bg-white">
                    <div>
                        <div class="flex items-center gap-2">
                            <h2 class="text-sm sm:text-base font-bold text-slate-900">Oportunidades Mapeadas &amp; Triagem Agendor</h2>
                            <span id="tableRowCountBadge" class="text-xs font-bold bg-[#FFF4EC] text-[#EE7D26] border border-[#F59B4E]/50 px-2 py-0.5 rounded-full">24 registros</span>
                        </div>
                        <p class="text-xs text-slate-500 mt-0.5">Altere o <strong>Status Agendor</strong> diretamente para sincronizar online ou toque em <strong>Ver Dossiê</strong>.</p>
                    </div>
                    <div class="flex items-center gap-2 text-xs text-slate-500">
                        <span class="shrink-0">Ordenar:</span>
                        <select id="sortSelect" onchange="applyFilters()" class="looker-control w-full sm:w-auto px-2.5 py-1.5 text-xs font-medium text-slate-700 cursor-pointer focus:outline-none">
                            <option value="default">Padrão (ordem da planilha)</option>
                            <option value="agendor">Status Agendor</option>
                            <option value="capex_desc">Maior CAPEX (R$ mi)</option>
                            <option value="capex_asc">Menor CAPEX (R$ mi)</option>
                            <option value="mes_desc">Mês Mais Recente (Nov &rarr; Ago)</option>
                            <option value="empresa_asc">Empresa (A - Z)</option>
                        </select>
                    </div>
                </div>

                <!-- MOBILE EXECUTIVE CARDS LIST (Visível apenas em smartphones < 768px) -->
                <div id="mobileOpportunitiesCards" class="md:hidden p-3 space-y-3 bg-[#F8FAFC]">
                    <!-- Populated dynamically via JS -->
                </div>

                <!-- DESKTOP RESPONSIVE TABLE WRAPPER (Visível apenas >= 768px) -->
                <div class="hidden md:block overflow-x-auto custom-scrollbar">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-50 border-b border-slate-200 text-[11px] font-bold uppercase tracking-wider text-slate-500">
                                <th class="py-3 px-3 w-36 text-left">Origem</th>
                                <th class="py-3 px-3 min-w-[235px]">Status Agendor (Editável)</th>
                                <th class="py-3 px-3 min-w-[190px]">Segmento M.ROSCOE</th>
                                <th class="py-3 px-3 min-w-[175px]">Empresa Contratante</th>
                                <th class="py-3 px-3 min-w-[230px]">Obra / Escopo</th>
                                <th class="py-3 px-3 min-w-[130px] text-right">CAPEX</th>
                                <th class="py-3 px-3 min-w-[95px] text-center">Mês</th>
                                <th class="py-3 px-3 min-w-[145px]">Local / UF</th>
                                <th class="py-3 px-3 min-w-[155px]">Decisor</th>
                                <th class="py-3 px-3 text-center w-28">Ações</th>
                            </tr>
                        </thead>
                        <tbody id="opportunitiesTableBody" class="divide-y divide-slate-100 text-xs sm:text-sm">
                            <!-- Populated dynamically via JS -->
                        </tbody>
                    </table>
                </div>

                <!-- Empty State (when filters return 0 items) -->
                <div id="emptyTableState" class="hidden py-12 px-4 text-center">
                    <div class="inline-flex items-center justify-center w-12 h-12 rounded-full bg-[#FFF4EC] text-[#EE7D26] mb-3">
                        <i data-lucide="search-x" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-sm font-bold text-slate-800">Nenhuma oportunidade encontrada com os filtros atuais</h3>
                    <p class="text-xs text-slate-500 mt-1 max-w-md mx-auto">Remova algum filtro de Status Agendor, Segmento, Mês ou UF para voltar a exibir as oportunidades.</p>
                    <button onclick="resetAllFilters()" class="mt-4 inline-flex items-center gap-1.5 px-3.5 py-2 bg-[#EE7D26] text-white text-xs font-semibold rounded-md hover:bg-[#D66914] transition cursor-pointer">
                        <i data-lucide="filter-x" class="w-3.5 h-3.5"></i>
                        Limpar todos os filtros
                    </button>
                </div>

                <!-- Table Footer -->
                <div class="px-4 py-2.5 bg-slate-50 border-t border-slate-200 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-2 text-[11px] text-slate-500">
                    <div>
                        Fonte: <span class="font-medium text-slate-700">Relatorio_Prospeccao_MRoscoe_2026-11-23.xlsx</span> • Sincronizado na versão online sem criar cópias
                    </div>
                    <div class="flex flex-wrap items-center gap-3">
                        <span class="flex items-center gap-1"><span class="w-2 h-2 rounded-full bg-[#EE7D26]"></span> Adicionar no Agendor</span>
                        <span class="flex items-center gap-1"><span class="w-2 h-2 rounded-full bg-[#0F9D58]"></span> Já adicionada no Agendor</span>
                        <span class="flex items-center gap-1"><span class="w-2 h-2 rounded-full bg-[#5F6368]"></span> Desconsiderar</span>
                    </div>
                </div>
            </section>

        </div>

        <!-- ===================================================================== -->
        <!-- PAGE 2: DESCARTADOS, MONITORAR & METODOLOGIA                          -->
        <!-- ===================================================================== -->
        <div id="pageDiscarded" class="hidden space-y-4 sm:space-y-5">
            
            <!-- Top Summary Banner -->
            <div class="looker-card p-4 bg-white border-l-4 border-l-[#EE7D26] flex flex-col md:flex-row md:items-center md:justify-between gap-4">
                <div>
                    <h2 class="text-sm sm:text-base font-bold text-slate-900">Descartados, Monitorar &amp; Metodologia M.ROSCOE</h2>
                    <p class="text-xs sm:text-sm text-slate-600 mt-1">
                        Registro dos 7 itens analisados na semana de <strong>23/11/2026</strong> filtrados fora do pipeline ativo (obras já contratadas/inauguradas, operações de M&amp;A, editais de P&amp;D ou escopo a confirmar).
                    </p>
                </div>
                <div class="flex items-center gap-2 shrink-0">
                    <span class="px-3 py-1.5 rounded-md bg-[#FFF4EC] text-[#EE7D26] border border-[#F59B4E]/50 text-xs font-bold">
                        7 itens triados
                    </span>
                </div>
            </div>

            <!-- Discarded & Monitor Cards (Mobile) + Table (Desktop) -->
            <section class="looker-card overflow-hidden">
                <div class="p-3.5 sm:p-4 border-b border-slate-200 flex items-center justify-between">
                    <div>
                        <h3 class="text-sm font-bold text-slate-900">Itens Descartados e Monitorados</h3>
                        <p class="text-xs text-slate-500">Histórico de curadoria comercial para evitar retrabalho na prospecção</p>
                    </div>
                </div>

                <!-- Mobile Discarded Cards -->
                <div id="mobileDiscardedCards" class="md:hidden p-3 space-y-3 bg-[#F8FAFC]">
                    <!-- Populated via JS -->
                </div>

                <!-- Desktop Discarded Table -->
                <div class="hidden md:block overflow-x-auto custom-scrollbar">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="bg-slate-50 border-b border-slate-200 text-[11px] font-bold uppercase tracking-wider text-slate-500">
                                <th class="py-3 px-4 w-12 text-center">#</th>
                                <th class="py-3 px-4 min-w-[180px]">Empresa / Entidade</th>
                                <th class="py-3 px-4 min-w-[260px]">Descrição do Projeto / Notícia</th>
                                <th class="py-3 px-4 min-w-[140px]">Localização</th>
                                <th class="py-3 px-4 min-w-[150px]">Valor Mencionado</th>
                                <th class="py-3 px-4 min-w-[210px]">Motivo / Status</th>
                                <th class="py-3 px-4 min-w-[240px]">Parecer Técnico M.ROSCOE</th>
                                <th class="py-3 px-4 text-center w-24">Fonte</th>
                            </tr>
                        </thead>
                        <tbody id="discardedTableBody" class="divide-y divide-slate-100 text-xs sm:text-sm">
                            <!-- Populated via JS -->
                        </tbody>
                    </table>
                </div>
            </section>

            <!-- Notas e Metodologia Cards -->
            <section class="grid grid-cols-1 lg:grid-cols-3 gap-4">
                
                <!-- Card 1: Critérios de Corte -->
                <div class="looker-card p-4 sm:p-5">
                    <div class="flex items-center gap-2.5 mb-3">
                        <div class="p-2 rounded-lg bg-[#FFF4EC] text-[#EE7D26]">
                            <i data-lucide="sliders-horizontal" class="w-5 h-5"></i>
                        </div>
                        <h3 class="text-sm font-bold text-slate-900">Critérios de Corte e Triagem</h3>
                    </div>
                    <ul class="space-y-2.5 text-xs text-slate-600 leading-relaxed">
                        <li class="flex items-start gap-2">
                            <i data-lucide="check-circle-2" class="w-4 h-4 text-[#EE7D26] shrink-0 mt-0.5"></i>
                            <span><strong>Data-base da varredura:</strong> Busca web estruturada e leitura dos e-mails da caixa de prospecção realizadas entre <strong>16 e 23/11/2026</strong>, cobrindo anúncios de maio/2025 a novembro/2026.</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <i data-lucide="check-circle-2" class="w-4 h-4 text-[#EE7D26] shrink-0 mt-0.5"></i>
                            <span><strong>Piso de Investimento (CAPEX):</strong> Obras privadas com investimento estimado superior a <strong>R$ 30 milhões</strong> (ou porte físico equivalente, como galpões &gt; 75 mil m²).</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <i data-lucide="check-circle-2" class="w-4 h-4 text-[#EE7D26] shrink-0 mt-0.5"></i>
                            <span><strong>Natureza do Capital:</strong> Exclusivamente <strong>iniciativa privada</strong> (projetos com participação estatal passam por verificação de regime de contratação).</span>
                        </li>
                    </ul>
                </div>

                <!-- Card 2: Fluxo de Triagem CRM Agendor -->
                <div class="looker-card p-4 sm:p-5">
                    <div class="flex items-center gap-2.5 mb-3">
                        <div class="p-2 rounded-lg bg-[#FFF4EC] text-[#EE7D26]">
                            <i data-lucide="git-branch" class="w-5 h-5"></i>
                        </div>
                        <h3 class="text-sm font-bold text-slate-900">Fluxo de Triagem CRM Agendor</h3>
                    </div>
                    <div class="space-y-2.5 text-xs text-slate-600 leading-relaxed">
                        <div class="p-2.5 rounded-md bg-[#FFF4EC] border border-[#F59B4E]">
                            <div class="font-bold text-[#B85309]">Adicionar Oportunidade no Agendor</div>
                            <p class="mt-0.5">Obras qualificadas com janela de contratação aberta prontas para cadastro e prospecção ativa no CRM.</p>
                        </div>
                        <div class="p-2.5 rounded-md bg-emerald-50/70 border border-emerald-200">
                            <div class="font-bold text-[#065F46]">Oportunidade já adicionada no Agendor</div>
                            <p class="mt-0.5">Negócios já registrados no funil da M.ROSCOE ou em acompanhamento comercial contínuo.</p>
                        </div>
                        <div class="p-2.5 rounded-md bg-slate-100 border border-slate-300">
                            <div class="font-bold text-[#5F6368]">Desconsiderar oportunidade</div>
                            <p class="mt-0.5">Projetos com risco de adiamento/suspensão (ex.: Cedro Mineração) ou fora do perfil técnico imediato.</p>
                        </div>
                    </div>
                </div>

                <!-- Card 3: Taxonomia Oficial & Fontes -->
                <div class="looker-card p-4 sm:p-5">
                    <div class="flex items-center gap-2.5 mb-3">
                        <div class="p-2 rounded-lg bg-[#1A1A1A]/10 text-[#1A1A1A]">
                            <i data-lucide="layers" class="w-5 h-5"></i>
                        </div>
                        <h3 class="text-sm font-bold text-slate-900">9 Segmentos Oficiais &amp; Fontes</h3>
                    </div>
                    <p class="text-xs text-slate-600 mb-3 leading-relaxed">
                        Classificação padronizada M.ROSCOE: <em>Siderurgia e metalurgia, Mineração e fertilizantes, Alimentos e bebidas, Indústria cimentícia, Indústria da transformação, Farmacêutico e químico, Papel e celulose, Edificações e Outras obras.</em>
                    </p>
                    <div class="grid grid-cols-2 gap-2 text-xs">
                        <div class="p-2.5 rounded border border-slate-200 bg-slate-50">
                            <div class="font-bold text-[#1A1A1A]">LinkedIn Sales Nav.</div>
                            <div class="text-[11px] text-slate-500 mt-0.5">Engenharia, CAPEX e Suprimentos</div>
                        </div>
                        <div class="p-2.5 rounded border border-slate-200 bg-slate-50">
                            <div class="font-bold text-[#1A1A1A]">InduXdata</div>
                            <div class="text-[11px] text-slate-500 mt-0.5">Abertura de leads confidenciais</div>
                        </div>
                        <div class="p-2.5 rounded border border-slate-200 bg-slate-50">
                            <div class="font-bold text-[#1A1A1A]">Convisão / ITC</div>
                            <div class="text-[11px] text-slate-500 mt-0.5">Estágio de obra e concorrências</div>
                        </div>
                        <div class="p-2.5 rounded border border-slate-200 bg-slate-50">
                            <div class="font-bold text-[#1A1A1A]">Radar CAPEX / OE</div>
                            <div class="text-[11px] text-slate-500 mt-0.5">Monitoramento setorial contínuo</div>
                        </div>
                    </div>
                </div>

            </section>
        </div>

    </main>

    <!-- ===================================================================== -->
    <!-- MOBILE FIXED BOTTOM NAVIGATION BAR (Navegação Nativa de App)          -->
    <!-- ===================================================================== -->
    <nav class="md:hidden fixed bottom-0 inset-x-0 z-30 bg-white border-t border-slate-200 shadow-[0_-2px_10px_rgba(0,0,0,0.05)]" aria-label="Navegação Mobile">
        <div class="grid grid-cols-4 h-16">
            <button id="mNavOverview" onclick="mobileNavigate('overview')" class="flex flex-col items-center justify-center gap-1 text-[#EE7D26] font-bold text-[10px] cursor-pointer">
                <i data-lucide="layout-dashboard" class="w-4 h-4"></i>
                <span>Visão Geral</span>
            </button>
            <button id="mNavOpportunities" onclick="mobileNavigate('opportunities')" class="flex flex-col items-center justify-center gap-1 text-slate-500 font-semibold text-[10px] cursor-pointer relative">
                <div class="relative">
                    <i data-lucide="building-2" class="w-4 h-4"></i>
                    <span id="mNavOppBadge" class="absolute -top-1.5 -right-3 bg-[#EE7D26] text-white text-[9px] font-extrabold px-1 rounded-full">24</span>
                </div>
                <span>Oportunidades</span>
            </button>
            <button id="mNavCharts" onclick="mobileNavigate('charts')" class="flex flex-col items-center justify-center gap-1 text-slate-500 font-semibold text-[10px] cursor-pointer">
                <i data-lucide="bar-chart-3" class="w-4 h-4"></i>
                <span>Gráficos</span>
            </button>
            <button id="mNavDiscarded" onclick="mobileNavigate('discarded')" class="flex flex-col items-center justify-center gap-1 text-slate-500 font-semibold text-[10px] cursor-pointer relative">
                <div class="relative">
                    <i data-lucide="archive" class="w-4 h-4"></i>
                    <span class="absolute -top-1.5 -right-2.5 bg-slate-600 text-white text-[9px] font-extrabold px-1 rounded-full">6</span>
                </div>
                <span>Descartados</span>
            </button>
        </div>
    </nav>

    <!-- ===================================================================== -->
    <!-- DETAIL MODAL / BOTTOM SHEET (FICHA COMPLETA DA OPORTUNIDADE)          -->
    <!-- ===================================================================== -->
    <div id="detailModal" onclick="closeModalOnBackdrop(event)" class="fixed inset-0 z-50 hidden items-center justify-center p-4 modal-backdrop mobile-bottom-sheet">
        <div class="bg-white rounded-xl shadow-2xl border border-slate-200 max-w-2xl w-full max-h-[90vh] flex flex-col overflow-hidden animate-in fade-in zoom-in-95 duration-150">
            
            <!-- Mobile Bottom Sheet Drag Pill -->
            <div class="md:hidden w-full flex justify-center pt-2 pb-1 bg-slate-50">
                <span class="w-10 h-1 rounded-full bg-slate-300"></span>
            </div>

            <!-- Modal Header -->
            <div class="px-4 sm:px-6 py-3.5 sm:py-4 border-b border-slate-200 flex items-start justify-between gap-3 bg-slate-50">
                <div>
                    <div class="flex flex-wrap items-center gap-2 mb-1">
                        <span id="modalNumBadge" class="text-xs font-bold bg-[#1A1A1A] text-white px-2 py-0.5 rounded">Origem</span>
                        <span id="modalPriorityOrigBadge" class="text-xs font-semibold bg-slate-200 text-slate-700 px-2 py-0.5 rounded">Prioridade A</span>
                        <span id="modalSegmentBadge" class="text-xs font-semibold text-[#EE7D26] bg-[#FFF4EC] border border-[#F59B4E]/50 px-2 py-0.5 rounded">Farmacêutico e químico</span>
                    </div>
                    <h3 id="modalCompanyTitle" class="text-base sm:text-xl font-bold text-slate-900">Aeroflex Indústria de Aerossóis</h3>
                </div>
                <button onclick="closeModal()" class="p-1.5 rounded-lg text-slate-400 hover:text-slate-700 hover:bg-slate-200/70 transition cursor-pointer" title="Fechar">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <!-- Modal Body -->
            <div class="p-4 sm:p-6 overflow-y-auto space-y-4 text-sm">
                
                <!-- Status Agendor Selector inside Modal -->
                <div class="p-3.5 rounded-lg bg-[#FFF4EC] border border-[#F59B4E] flex flex-col sm:flex-row sm:items-center sm:justify-between gap-2">
                    <div>
                        <div class="text-[11px] font-bold uppercase tracking-wider text-[#B85309]">Status de Triagem CRM Agendor</div>
                        <div class="text-xs text-slate-600">Sincronizado automaticamente na versão online</div>
                    </div>
                    <select id="modalAgendorSelect" onchange="handleModalAgendorChange(this.value)" class="px-3 py-2 rounded-md border text-xs font-bold cursor-pointer focus:outline-none">
                        <option value="Adicionar Oportunidade no Agendor">Adicionar Oportunidade no Agendor</option>
                        <option value="Oportunidade já adicionada no Agendor">Oportunidade já adicionada no Agendor</option>
                        <option value="Desconsiderar oportunidade">Desconsiderar oportunidade</option>
                    </select>
                </div>

                <!-- Grid of Metadata -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div class="p-3 rounded-lg bg-slate-50 border border-slate-200/80">
                        <div class="text-[11px] font-semibold uppercase text-slate-400">CAPEX / Porte Informado</div>
                        <div id="modalCapex" class="text-sm font-bold text-slate-900 mt-0.5">R$ 150 milhões</div>
                    </div>
                    <div class="p-3 rounded-lg bg-slate-50 border border-slate-200/80">
                        <div class="text-[11px] font-semibold uppercase text-slate-400">Mês de Captação</div>
                        <div id="modalMonth" class="text-sm font-bold text-[#EE7D26] mt-0.5">Nov/2026</div>
                    </div>
                    <div class="p-3 rounded-lg bg-slate-50 border border-slate-200/80">
                        <div class="text-[11px] font-semibold uppercase text-slate-400">Localização da Obra</div>
                        <div id="modalLocation" class="text-sm font-bold text-slate-900 mt-0.5">São José dos Pinhais (PR)</div>
                    </div>
                    <div class="p-3 rounded-lg bg-slate-50 border border-slate-200/80">
                        <div class="text-[11px] font-semibold uppercase text-slate-400">Cronograma Previsto</div>
                        <div id="modalTimeline" class="text-sm font-medium text-slate-800 mt-0.5">Obras a partir de 2026/27</div>
                    </div>
                </div>

                <!-- Escopo -->
                <div>
                    <div class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Escopo da Obra</div>
                    <p id="modalScope" class="p-3.5 rounded-lg bg-white border border-slate-200 text-slate-800 leading-relaxed text-xs sm:text-sm"></p>
                </div>

                <!-- Contato / Decisor -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div>
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Decisor / Contato Identificado</div>
                        <div id="modalContact" class="p-3 rounded-lg bg-slate-50 border border-slate-200 text-slate-800 font-semibold text-xs"></div>
                    </div>
                    <div>
                        <div class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Fonte e Data da Notícia</div>
                        <div id="modalSourceName" class="p-3 rounded-lg bg-slate-50 border border-slate-200 text-slate-700 text-xs"></div>
                    </div>
                </div>

                <!-- Observações & Inteligência Comercial -->
                <div>
                    <div class="text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Inteligência Comercial &amp; Observações</div>
                    <div id="modalObsBox" class="p-3.5 rounded-lg bg-[#FFF4EC]/80 border border-[#F59B4E] text-xs sm:text-sm text-slate-800 leading-relaxed"></div>
                </div>

            </div>

            <!-- Modal Footer -->
            <div class="px-4 sm:px-6 py-3.5 border-t border-slate-200 bg-slate-50 flex flex-wrap items-center justify-between gap-2">
                <button onclick="copyOpportunitySummary()" class="inline-flex items-center gap-1.5 px-3 py-2 rounded-md border border-slate-300 bg-white hover:bg-slate-100 text-xs font-semibold text-slate-700 transition cursor-pointer">
                    <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                    <span id="copyBtnText">Copiar Resumo</span>
                </button>
                <div class="flex items-center gap-2">
                    <a id="modalSourceLink" href="#" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1.5 px-3.5 py-2 rounded-md bg-[#EE7D26] hover:bg-[#D66914] text-white text-xs font-semibold transition">
                        <span>Abrir Notícia</span>
                        <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                    </a>
                    <button onclick="closeModal()" class="px-3.5 py-2 rounded-md bg-slate-200 hover:bg-slate-300 text-slate-800 text-xs font-semibold transition cursor-pointer">
                        Fechar
                    </button>
                </div>
            </div>

        </div>
    </div>

    <!-- ===================================================================== -->
    <!-- AVISO DISCRETO FLUTUANTE NO CANTO INFERIOR (SYNC TOAST)               -->
    <!-- ===================================================================== -->
    <div id="floatingSaveNotice" class="fixed bottom-20 md:bottom-4 right-3 left-3 md:left-auto md:right-4 z-40 hidden items-center justify-between gap-3 bg-[#1A1A1A] text-white px-4 py-3 rounded-lg shadow-xl border-l-4 border-l-[#EE7D26] md:max-w-md transition-all">
        <div class="flex items-center gap-2.5 min-w-0">
            <div class="p-1.5 rounded-full bg-[#0F9D58]/20 text-[#0F9D58] shrink-0">
                <i data-lucide="cloud-check" class="w-4 h-4"></i>
            </div>
            <div class="text-xs leading-snug">
                <span id="floatingNoticeText">Alterações salvas na versão online sem criar cópias.</span>
            </div>
        </div>
        <button onclick="hideFloatingNotice()" class="text-slate-400 hover:text-white p-1 shrink-0 cursor-pointer" title="Fechar aviso">
            <i data-lucide="x" class="w-3.5 h-3.5"></i>
        </button>
    </div>

    <!-- ===================================================================== -->
    <!-- BLOCO DE ESTADO EMBUTIDO (ATUALIZADO AO SOBRESCREVER LOCAL)           -->
    <!-- ===================================================================== -->
    <script id="saved-state-script" type="application/json">{}</script>

    <!-- ===================================================================== -->
    <!-- JAVASCRIPT: SINCRONIZAÇÃO ONLINE, MOBILE NATIVE UI & CHART.JS         -->
    <!-- ===================================================================== -->
    <script type="module">
        // Integração opcional automática com Firebase Firestore caso o ambiente forneça __firebase_config
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        async function initCloudSyncIfAvailable() {
            try {
                if (typeof __firebase_config === 'undefined' || !__firebase_config) return;
                const firebaseConfig = JSON.parse(__firebase_config);
                if (!firebaseConfig || !firebaseConfig.apiKey) return;

                const appId = typeof __app_id !== 'undefined' ? __app_id : 'mroscoe-inteligencia-mercado';
                const app = initializeApp(firebaseConfig);
                const auth = getAuth(app);
                const db = getFirestore(app);

                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }

                if (!auth.currentUser) return;

                const stateDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'agendor_triagem', 'semana_2026_11_16');
                window._mroscoeCloudDocRef = stateDocRef;
                window._mroscoeSetDoc = setDoc;

                // Escuta atualizações em tempo real na nuvem sem criar cópias
                onSnapshot(stateDocRef, (snapshot) => {
                    if (snapshot.exists()) {
                        const data = snapshot.data();
                        if (data && data.statuses && typeof window.applyCloudStatuses === 'function') {
                            window.applyCloudStatuses(data.statuses, data.updatedAt);
                        }
                    }
                }, (err) => {
                    console.warn('Firestore snapshot fallback para armazenamento online local/URL:', err);
                });
            } catch (err) {
                console.warn('Modo online local/URL ativo:', err);
            }
        }

        initCloudSyncIfAvailable();
    </script>

    <script>
        const STORAGE_KEY = 'mroscoe_agendor_status_2026_11_16_v3';
        const WINDOW_NAME_PREFIX = 'MROSCOE_AGENDOR_STATE:';

        const AGENDOR_OPTIONS = [
            "Adicionar Oportunidade no Agendor",
            "Oportunidade já adicionada no Agendor",
            "Desconsiderar oportunidade"
        ];

        // Códigos compactos para sincronização limpa na URL online (#state=...) sem criar cópias
        const STATUS_TO_CODE = {
            "Adicionar Oportunidade no Agendor": "A",
            "Oportunidade já adicionada no Agendor": "J",
            "Desconsiderar oportunidade": "D"
        };
        const CODE_TO_STATUS = {
            "A": "Adicionar Oportunidade no Agendor",
            "J": "Oportunidade já adicionada no Agendor",
            "D": "Desconsiderar oportunidade"
        };

        // Todos os 9 Segmentos Oficiais M.ROSCOE
        const OFFICIAL_SEGMENTS = [
            "Siderurgia e metalurgia",
            "Mineração e fertilizantes",
            "Alimentos e bebidas",
            "Indústria cimentícia",
            "Indústria da transformação",
            "Farmacêutico e químico",
            "Papel e celulose",
            "Edificações",
            "Outras obras"
        ];

        const MONTH_ORDER = ["Mai/2025", "Fev/2026", "Ago/2026", "Set/2026", "Out/2026", "Nov/2026"];

        // 1. BASE DE DADOS DAS 24 OPORTUNIDADES (Semana de 23/11/2026)
        const baseOpportunities = [
            {
                id: 1,
                numPlanilha: 1,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Aeroflex Indústria de Aerossóis",
                segmento: "Farmacêutico e químico",
                escopo: "Nova fábrica de aerossóis (greenfield) com centro de pesquisa de 1.400 m², apresentada como a maior planta do segmento na América Latina",
                capexNum: 150,
                capexTexto: "R$ 150 mi",
                capexDetalhe: "R$ 150 milhões",
                mes: "Nov/2026",
                fonteTexto: "Ric.com.br (11/11/2026); GMC Online e Paranashop (13/11/2026)",
                cronograma: "Obras a partir de 2026/27; operação prevista em 2027",
                cidade: "São José dos Pinhais (PR) – bairro Campo Largo da Roseira",
                uf: "PR",
                contato: "Marcio Miksza – fundador e CEO",
                temDecisor: true,
                obs: "Notícia muito recente; contratação de construtora provavelmente ainda não definida. Contato inicial pelo CEO ou pela área de engenharia/suprimentos.",
                alerta: false,
                link: "https://ric.com.br/negocios/nova-fabrica-aerossois-investimento-sao-jose-dos-pinhais/"
            },
            {
                id: 2,
                numPlanilha: 2,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "ZTT (grupo chinês)",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica de equipamentos para o setor elétrico (greenfield)",
                capexNum: 110,
                capexTexto: "R$ 110 mi",
                capexDetalhe: "R$ 110 milhões (R$ 30 mi em 2026, R$ 40 mi em 2027, R$ 40 mi em 2028)",
                mes: "Nov/2026",
                fonteTexto: "Metrópoles (06/11/2026)",
                cronograma: "Implantação a partir de dez/2026; operação em 2028",
                cidade: "Três Corações (MG)",
                uf: "MG",
                contato: "Não citado na notícia",
                temDecisor: false,
                obs: "Notícia cita priorização de fornecedores da região. Ótima janela: início de obra em dezembro.",
                alerta: false,
                link: "https://www.metropoles.com/minas-gerais/grupo-chines-anuncia-investimento-de-r-110-milhoes-em-fabrica-no-sul-de-mg"
            },
            {
                id: 3,
                numPlanilha: 3,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Empresa não divulgada (acompanhada pela InduXdata)",
                segmento: "Alimentos e bebidas",
                escopo: "Nova fábrica greenfield de bebidas e lácteos; demandas de engenharia, equipamentos e construção",
                capexNum: 400,
                capexTexto: "R$ 400 mi",
                capexDetalhe: "Acima de R$ 400 milhões",
                mes: "Nov/2026",
                fonteTexto: "BVMI / InduXdata (09/11/2026)",
                cronograma: "Fase pré-construção; datas não divulgadas",
                cidade: "Brasil – local não divulgado",
                uf: "Não divulgado",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Empresa e local só são revelados na plataforma InduXdata. Vale checar o detalhe lá.",
                alerta: false,
                link: "https://bvmi.com.br/nova-fabrica-de-alimentos-e-bebidas/"
            },
            {
                id: 15,
                numPlanilha: 4,
                origem: "Thiago Costa",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Coca-Cola FEMSA Brasil (Coca-Cola SPAL)",
                segmento: "Alimentos e bebidas",
                escopo: "Nova fábrica de bebidas (greenfield), projetada para ~400 milhões de litros/ano, com alta automação; local escolhido após disputa entre cidades do Vale do Paraíba",
                capexNum: 1000,
                capexTexto: "R$ 1.000 mi",
                capexDetalhe: "R$ 1 bilhão (US$ 199 mi)",
                mes: "Nov/2026",
                fonteTexto: "Click Petróleo e Gás (nov/2026); IndustrialInfo; Gazeta SP",
                cronograma: "Início de obras previsto para 2026 segundo notícias anteriores; cronograma atual não divulgado",
                cidade: "Caçapava (SP)",
                uf: "SP",
                contato: "Não divulgado na notícia",
                temDecisor: false,
                obs: "Indicada por e-mail interno (Thiago Costa) em 17/11/2026. Pode ser o projeto de bebidas acima de R$ 400 mi da InduXdata; confirmar na plataforma. Abordar engenharia/suprimentos cedo.",
                alerta: false,
                link: "https://clickpetroleoegas.com.br/apos-disputa-entre-cidades-coca-cola-femsa-escolhe-cacapava-para-fabrica-de-r-1-bilhao-prevista-para-produzir-400-milhoes-de-litros-por-ano-asaf04/"
            },
            {
                id: 16,
                numPlanilha: 5,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Coca-Cola (Uberlândia)",
                segmento: "Alimentos e bebidas",
                escopo: "Nova planta industrial da fábrica 'mais moderna da empresa no mundo': R$ 860 mi na construção da planta, dentro de R$ 1,5 bi até 2030",
                capexNum: 860,
                capexTexto: "R$ 860 mi",
                capexDetalhe: "R$ 860 milhões (planta) / R$ 1,5 bilhão até 2030",
                mes: "Mai/2025",
                fonteTexto: "Gironews (13/05/2025); Diário do Litoral",
                cronograma: "Até 2030; estágio atual da obra não confirmado",
                cidade: "Uberlândia (MG)",
                uf: "MG",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Matéria de 2025; confirmar se a construtora já foi contratada e o cronograma atual.",
                alerta: false,
                link: "https://gironews.com/informacoes-de-fornecedores/coca-cola-deve-investir-r-1-bilhao-em-nova-fabrica-em-sao-paulo/"
            },
            {
                id: 21,
                numPlanilha: 6,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Nestlé",
                segmento: "Alimentos e bebidas",
                escopo: "Nova fábrica de fórmulas infantis e nutrição (linhas Ninho e Nestogeno), dentro de pacote de R$ 7 bi (2025-2028) que inclui ampliações em quatro fábricas",
                capexNum: 600,
                capexTexto: "R$ 600 mi",
                capexDetalhe: "R$ 600 milhões (fábrica nova); pacote total R$ 7 bilhões",
                mes: "Nov/2026",
                fonteTexto: "Portal 6 (16/11/2026)",
                cronograma: "Obras começam em 2027; produção em 2028",
                cidade: "Ituiutaba (MG)",
                uf: "MG",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Janela ideal de relacionamento: obras só em 2027. O pacote inclui ainda Araçatuba (SP, ~R$ 540 mi, nutrição e saúde), Araras (SP, ~R$ 1 bi, cafés solúveis) e Montes Claros (MG, ~R$ 450 mi, cápsulas de café), ampliações brownfield que também cabem no perfil; confirmar escopo civil.",
                alerta: false,
                link: "https://portal6.com.br/2026/11/16/nestle-anuncia-r-7-bilhoes-no-brasil-com-nova-fabrica-nova-e-deve-abrir-cerca-de-2-mil-empregos/"
            },
            {
                id: 22,
                numPlanilha: 7,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "AVS Technology (grupo suíço) – Inclor",
                segmento: "Farmacêutico e químico",
                escopo: "Nova fábrica de soda cáustica, hipoclorito de sódio e ácido clorídrico, em área adquirida com recursos próprios",
                capexNum: 100,
                capexTexto: "R$ 100 mi",
                capexDetalhe: "R$ 100 milhões",
                mes: "Out/2026",
                fonteTexto: "Grupo CIMM (05/10/2026)",
                cronograma: "Início das obras previsto para dez/2026; produção em dez/2027",
                cidade: "Rondonópolis (MT) – Distrito Vetorasso",
                uf: "MT",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Obra começa em semanas; verificar com urgência se a construtora já foi definida.",
                alerta: false,
                link: "https://www.cimm.com.br/portal/noticia/exibir_noticia/27749-grupo-suico-anuncia-investimento-100-milhoes-nova-fabrica"
            },
            {
                id: 23,
                numPlanilha: 8,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Jetour (grupo Chery)",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica de veículos eletrificados (modelos T1 e T2), somando-se a outros R$ 400 mi anunciados no início de 2026",
                capexNum: 400,
                capexTexto: "R$ 400 mi",
                capexDetalhe: "R$ 400 milhões (novo aporte)",
                mes: "Nov/2026",
                fonteTexto: "Brasil 247 (18/11/2026)",
                cronograma: "Anunciada em 18/11/2026; cronograma não divulgado",
                cidade: "Estado do Rio de Janeiro; município será divulgado em março (negociação avançada com Itatiaia)",
                uf: "RJ",
                contato: "Ke Chuandeng – presidente da Jetour International",
                temDecisor: true,
                obs: "Projeto em fase inicial; local ainda indefinido. Acompanhar o anúncio do município em março.",
                alerta: false,
                link: "https://www.brasil247.com/industria/chinesa-jetour-anuncia-fabrica-de-r-400-milhoes-no-rj-e-mira-expansao/"
            },
            {
                id: 24,
                numPlanilha: 9,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Yanmar South America",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica de tratores com capacidade para 7 mil unidades/ano, em terreno três vezes maior que o atual; investimento em três etapas até 2030",
                capexNum: 280,
                capexTexto: "R$ 280 mi",
                capexDetalhe: "R$ 280 milhões (1ª etapa: ~R$ 190 milhões)",
                mes: "Nov/2026",
                fonteTexto: "Click Petróleo e Gás (nov/2026), citando CNN Brasil",
                cronograma: "1ª fase em operação em 2027; conclusão das etapas até 2030",
                cidade: "Indaiatuba (SP)",
                uf: "SP",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Obra em andamento ou iminente. As etapas 2 e 3 (até 2030) são a oportunidade mais provável; verificar quem executa a 1ª fase.",
                alerta: false,
                link: "https://clickpetroleoegas.com.br/yanmar-nova-fabrica-indaiatuba-280-milhoes-rss94/"
            },
            {
                id: 25,
                numPlanilha: 10,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Intelbras",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica 'Intelbras 2' (CFTV e segurança), com 52 mil m² de área construída em terreno de ~670 mil m²",
                capexNum: 200,
                capexTexto: "R$ 200 mi",
                capexDetalhe: "R$ 200 milhões",
                mes: "Ago/2026",
                fonteTexto: "Revista PIM Amazônia (ago/2026)",
                cronograma: "Operação prevista para meados de 2027; preparação do terreno já iniciada",
                cidade: "Manaus (AM) – Polo Industrial",
                uf: "AM",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Notícia de agosto; obra provavelmente já contratada. Útil para acompanhar fases seguintes.",
                alerta: false,
                link: "https://pimamazonia.balponte.com.br/intelbras-fabrica-em-manaus-para-2027/"
            },
            {
                id: 26,
                numPlanilha: 11,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "WEG",
                segmento: "Indústria da transformação",
                escopo: "Fábrica de baterias, com investimento elevado e capacidade prevista dobrada",
                capexNum: 330,
                capexTexto: "R$ 330 mi",
                capexDetalhe: "R$ 330 milhões",
                mes: "Nov/2026",
                fonteTexto: "Radar Capex (nov/2026)",
                cronograma: "Datas não divulgadas na fonte",
                cidade: "Itajaí (SC)",
                uf: "SC",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "A fonte traz só a manchete; localizar a matéria completa para confirmar escopo e cronograma.",
                alerta: false,
                link: "https://radarcapex.com.br/investimentos/"
            },
            {
                id: 4,
                numPlanilha: 12,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade A",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Britânia Eletrodomésticos",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica de ~110 mil m² para ampliar produção de eletrodomésticos de maior porte (linha branca)",
                capexNum: 0,
                capexTexto: "N/D",
                capexDetalhe: "Valor do projeto de 110 mil m² não divulgado (outra matéria cita R$ 130 mi para uma unidade de 75,9 mil m² no mesmo município)",
                mes: "Nov/2026",
                fonteTexto: "Click Petróleo e Gás (nov/2026); Tribuna PR; Gazeta do Povo",
                cronograma: "Entrega prevista para 2028",
                cidade: "Joinville (SC)",
                uf: "SC",
                contato: "Ana Luiza Buffara – vice-presidente",
                temDecisor: true,
                obs: "Pelo porte (110 mil m²), o valor deve superar R$ 30 mi, mas confirmar. Atenção: as notícias divergem sobre área e valor.",
                alerta: false,
                link: "https://clickpetroleoegas.com.br/britania-anuncia-nova-fabrica-de-110-mil-metros-quadrados-em-santa-catarina-e-prepara-uma-das-maiores-expansoes-industriais-de-seus-70-anos-vml97/"
            },
            {
                id: 5,
                numPlanilha: 13,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Oportunidade já adicionada no Agendor",
                empresa: "Condumax Incesa",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica de cabos de média tensão",
                capexNum: 160,
                capexTexto: "R$ 160 mi",
                capexDetalhe: "R$ 160 milhões",
                mes: "Out/2026",
                fonteTexto: "Radar Capex (30/10/2026)",
                cronograma: "Inauguração prevista para 2027",
                cidade: "Olímpia (SP)",
                uf: "SP",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Pode já ter construtora contratada; checar estágio da obra.",
                alerta: false,
                link: "https://radarcapex.com.br/investimentos/"
            },
            {
                id: 6,
                numPlanilha: 14,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Oportunidade já adicionada no Agendor",
                empresa: "Whirlpool",
                segmento: "Indústria da transformação",
                escopo: "Ampliação da fábrica",
                capexNum: 300,
                capexTexto: "R$ 300 mi",
                capexDetalhe: "R$ 300 milhões",
                mes: "Nov/2026",
                fonteTexto: "Radar Capex (05/11/2026)",
                cronograma: "Datas não divulgadas",
                cidade: "Rio Claro (SP)",
                uf: "SP",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Obra brownfield, linha de atuação da M.ROSCOE. Confirmar escopo civil e cronograma.",
                alerta: false,
                link: "https://radarcapex.com.br/investimentos/"
            },
            {
                id: 7,
                numPlanilha: 15,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Oportunidade já adicionada no Agendor",
                empresa: "Tellescom",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica de semicondutores",
                capexNum: 1000,
                capexTexto: "R$ 1.000 mi",
                capexDetalhe: "R$ 1 bilhão (US$ 170 milhões)",
                mes: "Out/2026",
                fonteTexto: "Radar Capex (22/10/2026)",
                cronograma: "Datas não divulgadas",
                cidade: "Cachoeirinha (RS)",
                uf: "RS",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Projeto de alta complexidade (sala limpa). Avaliar aderência técnica.",
                alerta: false,
                link: "https://radarcapex.com.br/investimentos/"
            },
            {
                id: 8,
                numPlanilha: 16,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Oportunidade já adicionada no Agendor",
                empresa: "Fenner (Grupo Michelin)",
                segmento: "Indústria da transformação",
                escopo: "Nova fábrica ~3x maior que a atual, hub da América do Sul",
                capexNum: 0,
                capexTexto: "N/D",
                capexDetalhe: "Centenas de milhões de reais (valor exato não divulgado)",
                mes: "Out/2026",
                fonteTexto: "Radar Capex (21/10/2026)",
                cronograma: "Datas não divulgadas",
                cidade: "Guarulhos (SP)",
                uf: "SP",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Valor estimado acima de R$ 30 mi, a confirmar.",
                alerta: false,
                link: "https://radarcapex.com.br/investimentos/"
            },
            {
                id: 17,
                numPlanilha: 17,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Vale",
                segmento: "Mineração e fertilizantes",
                escopo: "Construção de planta para processar 21,8 milhões de t/ano de minério; previsão de 3.603 contratações na obra",
                capexNum: 0,
                capexTexto: "N/D",
                capexDetalhe: "Valor não informado na fonte",
                mes: "Out/2026",
                fonteTexto: "Click Petróleo e Gás (30/10/2026)",
                cronograma: "Autorização para construir recebida em out/2026; início/fim não divulgados",
                cidade: "Minas Gerais – município não identificado na fonte",
                uf: "MG",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "A matéria original aparece apenas como manchete relacionada; localizar o texto completo antes de abordar. A Vale tem cadastro formal de fornecedores.",
                alerta: false,
                link: "https://clickpetroleoegas.com.br/minas-gerais-mira-r-2486-milhoes-17-projetos-buscam-apoio-da-finep-para-minerais-criticos-e-novas-tecnologias-na-mineracao-asaf04"
            },
            {
                id: 10,
                numPlanilha: 18,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Oportunidade já adicionada no Agendor",
                empresa: "Potássio do Brasil",
                segmento: "Mineração e fertilizantes",
                escopo: "Projeto Potássio Autazes: mina e planta, 2,4 milhões de t/ano",
                capexNum: 12400,
                capexTexto: "R$ 12.400 mi",
                capexDetalhe: "R$ 12,4 bilhões",
                mes: "Set/2026",
                fonteTexto: "Crane Brasil (set/2026); Revista Minérios (ago/2026)",
                cronograma: "Estruturação de engenharia e financiamento até início de 2027; operação prevista em 2028",
                cidade: "Autazes (AM)",
                uf: "AM",
                contato: "Sergio Leite – presidente",
                temDecisor: true,
                obs: "Localização remota, com logística diferenciada. Janela de relacionamento é agora, antes da contratação do EPC.",
                alerta: false,
                link: "https://cranebrasil.com.br/setor-inicia-2026-em-alta-e-preve-ciclo-recorde/"
            },
            {
                id: 11,
                numPlanilha: 19,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Desconsiderar oportunidade",
                empresa: "Galvani",
                segmento: "Mineração e fertilizantes",
                escopo: "Projeto Minério Primário de Irecê (fosfato) e investimentos na planta de Luís Eduardo Magalhães; também projeto em Santa Quitéria (CE, US$ 460 mi, em parceria com a estatal INB)",
                capexNum: 0,
                capexTexto: "N/D",
                capexDetalhe: "Irecê: valor não informado; Santa Quitéria: ~US$ 460 milhões",
                mes: "Out/2026",
                fonteTexto: "Revista O Empreiteiro (out/2026); Brasil Mineral",
                cronograma: "Irecê: conclusão até fim de 2026, operação em 2027",
                cidade: "Irecê e Luís Eduardo Magalhães (BA); Santa Quitéria (CE)",
                uf: "BA/CE",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Irecê está em fase final. Santa Quitéria tem parceria com estatal; verificar se a contratação é privada.",
                alerta: false,
                link: "https://revistaoe.com.br/novos-projetos-mineracao-2026/"
            },
            {
                id: 12,
                numPlanilha: 20,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Oportunidade já adicionada no Agendor",
                empresa: "EuroChem",
                segmento: "Mineração e fertilizantes",
                escopo: "Complexo Serra do Salitre: ampliação para 1 milhão de t/ano de fertilizantes fosfatados",
                capexNum: 0,
                capexTexto: "N/D",
                capexDetalhe: "Valor não informado",
                mes: "Out/2026",
                fonteTexto: "Revista O Empreiteiro (out/2026)",
                cronograma: "Capacidade instalada alvo em 2027",
                cidade: "Serra do Salitre (MG)",
                uf: "MG",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Verificar escopo remanescente de obras civis.",
                alerta: false,
                link: "https://revistaoe.com.br/novos-projetos-mineracao-2026/"
            },
            {
                id: 18,
                numPlanilha: 21,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "CSN Mineração",
                segmento: "Mineração e fertilizantes",
                escopo: "Projeto P15: 16,5 milhões de t/ano de pellet feed na mina Casa de Pedra, mais logística e economia circular (R$ 13,2 bi até 2030)",
                capexNum: 13200,
                capexTexto: "R$ 13.200 mi",
                capexDetalhe: "R$ 13,2 bilhões (programa até 2030)",
                mes: "Set/2026",
                fonteTexto: "Brazil Iron (set/2026)",
                cronograma: "Até 2030",
                cidade: "Congonhas (MG)",
                uf: "MG",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "O valor de R$ 13,2 bi cobre o programa todo, não só o P15. Boa porta de entrada via cadastro de fornecedores.",
                alerta: false,
                link: "https://braziliron.com.br/megatendencias-globais-definem-agenda-da-industria-mineral/"
            },
            {
                id: 14,
                numPlanilha: 22,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade B",
                defaultAgendorStatus: "Desconsiderar oportunidade",
                empresa: "Cedro Mineração",
                segmento: "Mineração e fertilizantes",
                escopo: "Expansão da planta de Mariana: 2 para 5 milhões de t/ano de minério de ferro (pellet feed)",
                capexNum: 3500,
                capexTexto: "R$ 3.500 mi",
                capexDetalhe: "R$ 3,5 bilhões",
                mes: "Ago/2026",
                fonteTexto: "Revista Minérios (ago/2026)",
                cronograma: "Datas não divulgadas",
                cidade: "Mariana (MG)",
                uf: "MG",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "ALERTA: o Brasil Mineral de 06/11/2026 informa que a Cedro suspendeu produção em MG. Risco de adiamento do investimento.",
                alerta: true,
                link: "https://revistaminerios.com.br/principais-projetos-de-mineracao-em-2026/"
            },
            {
                id: 19,
                numPlanilha: 23,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade C",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Bracell",
                segmento: "Papel e celulose",
                escopo: "Nova fábrica de celulose (fibra curta), cerca de 2,8 milhões de t/ano",
                capexNum: 25000,
                capexTexto: "R$ 25.000 mi",
                capexDetalhe: "Até R$ 25 bilhões (US$ 4,5 bi)",
                mes: "Fev/2026",
                fonteTexto: "Times Brasil/CNBC (11/02/2026); Compre Rural",
                cronograma: "Início das obras previsto para 2026",
                cidade: "Bataguassu / Água Clara (MS)",
                uf: "MS",
                contato: "Não divulgado",
                temDecisor: false,
                obs: "Megaprojeto: o pacote principal costuma ir para grandes EPCs. Oportunidade provável em pacotes civis e subempreitadas. Confirmar estágio da contratação.",
                alerta: false,
                link: "https://timesbrasil.com.br/empresas-e-negocios/agro/bracell-fabrica-ms-25-bi-2-8-milhoes-toneladas-ano/"
            },
            {
                id: 20,
                numPlanilha: 24,
                origem: "Agente IA",
                prioridadeOrig: "Prioridade C",
                defaultAgendorStatus: "Adicionar Oportunidade no Agendor",
                empresa: "Arauco – Projeto Sucuriú",
                segmento: "Papel e celulose",
                escopo: "Maior fábrica de celulose do mundo em etapa única (3,5 milhões de t/ano), mais ferrovia de R$ 2,4 bi",
                capexNum: 23000,
                capexTexto: "R$ 23.000 mi",
                capexDetalhe: "US$ 4,6 bilhões (~R$ 23 bi)",
                mes: "Out/2026",
                fonteTexto: "Compre Rural (2026); Times Brasil/CNBC",
                cronograma: "Obras em 81%; operação no 4º tri/2027; pico de ~14 mil trabalhadores",
                cidade: "Inocência (MS)",
                uf: "MS",
                contato: "Arnaldo Milan de Souza – gerente de Pessoas do Projeto Sucuriú (não é contato comercial)",
                temDecisor: false,
                obs: "Obra avançada; as oportunidades tendem a ser pontuais (acabamentos, complementares, ferrovia, manutenção futura).",
                alerta: false,
                link: "https://comprerural.com/arauco-investe-r-23-bilhoes-em-megafabrica-de-celulose-e-obras-chegam-a-81-em-ms/"
            }
        ];

        // 2. BASE DE DADOS DOS 6 ITENS DESCARTADOS & MONITORAR (ABA 2)
        const discardedData = [
            {
                id: 1,
                empresa: "Mahindra",
                descricao: "Fábrica de tratores",
                local: "Dois Irmãos (RS)",
                valor: "R$ 100 mi",
                badge: "Contratação já ocorreu",
                badgeType: "closed",
                parecer: "Conclusão prevista para o 2º sem/2026; etapa de contratação de obra civil já encerrada.",
                link: "https://ndmais.com.br/economia/mahindra-investe-r-100-milhoes-em-nova-fabrica-no-rs/"
            },
            {
                id: 2,
                empresa: "Gás Verde",
                descricao: "Planta de Biometano",
                local: "Pernambuco (PE)",
                valor: "R$ 90,2 mi",
                badge: "Contratação já ocorreu",
                badgeType: "closed",
                parecer: "Obra em fase final com término previsto para dez/2026; janela de prospecção fechada.",
                link: "https://clickpetroleoegas.com.br/empresa-investe-r-902-milhoes-em-nova-fabrica-no-brasil-transforma-lixo-em-combustivel-e-fecha-contratos-para-abastecer-stellantis-e-mondelez-vml97/"
            },
            {
                id: 3,
                empresa: "Zilia Technologies",
                descricao: "Ampliação fábrica de semicondutores (20,5 para 23 mil m²)",
                local: "Atibaia (SP)",
                valor: "R$ 143,3 mi BNDES (plano de R$ 650 mi)",
                badge: "Avaliar manualmente",
                badgeType: "monitor",
                parecer: "Financiamento aprovado; maioria do CAPEX é maquinário, mas há expansão física de 2.500 m² a confirmar.",
                link: "https://radarcapex.com.br/investimentos/"
            },
            {
                id: 4,
                empresa: "CSN Cimentos / Huaxin",
                descricao: "Venda de participação societária",
                local: "Brasil",
                valor: "R$ 12,7 bi",
                badge: "M&A / Não é obra",
                badgeType: "non_construction",
                parecer: "Operação societária (fusão e aquisição) sem anúncio associado de nova planta ou ampliação civil.",
                link: "https://www.em.com.br/colunistas/mineirar/2026/11/7536477-governo-define-27-minerais-estrategicos-e-abre-caminho-para-novos-investim.html"
            },
            {
                id: 5,
                empresa: "Embrapii / GIZ",
                descricao: "Chamada pública para descarbonizar aço e cimento",
                local: "Nacional",
                valor: "R$ 81 mi",
                badge: "Edital P&D",
                badgeType: "non_construction",
                parecer: "Edital de fomento à pesquisa e desenvolvimento tecnológico; não configura obra de engenharia civil.",
                link: "https://clickpetroleoegas.com.br/siderurgicas-e-cimenteiras-do-brasil-terao-ate-r-81-milhoes-para-testar-dentro-das-fabricas-tecnologias-que-cortam-emissoes-de-co%E2%82%82-ctl01/"
            },
            {
                id: 6,
                empresa: "Grupo Alubar",
                descricao: "Fábrica de cabos de aço (Santo Tirso)",
                local: "Portugal",
                valor: "€ 55 mi",
                badge: "Obra no exterior",
                badgeType: "non_construction",
                parecer: "Obra em Portugal; fora do escopo nacional (a M.ROSCOE atua apenas em território brasileiro).",
                link: "https://hrportugal.sapo.pt/alubar-escolhe-santo-tirso-para-a-primeira-fabrica-em-portugal-sao-55-milhoes-e-50-postos-de-trabalho/"
            },
            {
                id: 7,
                empresa: "Kellanova",
                descricao: "Ampliação de unidade industrial",
                local: "São Lourenço do Oeste (SC)",
                valor: "R$ 360 mi",
                badge: "Já inaugurada",
                badgeType: "closed",
                parecer: "Expansão já concluída e inaugurada em 2025; mantida apenas para referência histórica.",
                link: "https://mercadoeconsumo.com.br/19/09/2025/economia/kellanova-dona-da-sucrilhos-amplia-fabrica-em-santa-catarina/"
            }
        ];

        // Global State
        let opportunitiesState = [];
        let segmentMetricMode = 'capex'; // 'capex' | 'count'
        let chartSegmentsInstance = null;
        let chartAgendorInstance = null;
        let chartMonthsInstance = null;
        let currentModalItemId = null;
        let mobileFiltersOpen = false;

        // =========================================================================
        // CAMADA DE SINCRONIZAÇÃO ONLINE SEM CRIAR CÓPIAS (CLOUD + URL HASH + LOCAL)
        // =========================================================================

        function updateSyncIndicator(state, label) {
            const dot = document.getElementById('syncStatusDot');
            const text = document.getElementById('syncStatusText');
            const wrapper = document.getElementById('syncStatusIndicator');
            if (!dot || !text || !wrapper) return;

            text.textContent = label;
            if (state === 'saving') {
                dot.className = 'w-2 h-2 rounded-full bg-[#EE7D26] animate-ping';
                wrapper.className = 'inline-flex items-center gap-1.5 font-semibold text-[#EE7D26]';
            } else {
                dot.className = 'w-2 h-2 rounded-full bg-[#0F9D58]';
                wrapper.className = 'inline-flex items-center gap-1.5 font-semibold text-emerald-700';
            }
        }

        function encodeStateToUrlHash(map) {
            // Formato ultra-compacto: "1:A,2:J,14:D" para manter a URL limpa e compartilhável
            const parts = baseOpportunities.map(item => {
                const status = map[String(item.id)] || item.defaultAgendorStatus;
                const code = STATUS_TO_CODE[status] || 'A';
                return `${item.id}:${code}`;
            });
            return `#agendor=${parts.join(',')}`;
        }

        function decodeStateFromUrlHash() {
            try {
                const hash = window.location.hash || '';
                const match = hash.match(/agendor=([0-9:,AJD]+)/);
                if (!match || !match[1]) return {};
                const result = {};
                match[1].split(',').forEach(pair => {
                    const [idStr, code] = pair.split(':');
                    if (idStr && CODE_TO_STATUS[code]) {
                        result[idStr] = CODE_TO_STATUS[code];
                    }
                });
                return result;
            } catch (e) {
                return {};
            }
        }

        function syncUrlHashWithoutReload(stateMap) {
            try {
                const newHash = encodeStateToUrlHash(stateMap);
                if (window.history && window.history.replaceState) {
                    window.history.replaceState(null, '', newHash);
                } else {
                    window.location.hash = newHash;
                }
            } catch (e) {
                // Ignora se o iframe sandbox bloquear replaceState
            }
        }

        function readEmbeddedState() {
            try {
                const scriptEl = document.getElementById('saved-state-script');
                if (scriptEl && scriptEl.textContent.trim()) {
                    const parsed = JSON.parse(scriptEl.textContent.trim());
                    if (parsed && typeof parsed === 'object') return parsed;
                }
            } catch (e) {}
            return {};
        }

        function readSessionStorageSafe() {
            try {
                const raw = window.localStorage.getItem(STORAGE_KEY);
                if (raw) {
                    const parsed = JSON.parse(raw);
                    if (parsed && typeof parsed === 'object') return parsed;
                }
            } catch (e) {}

            try {
                if (typeof window.name === 'string' && window.name.startsWith(WINDOW_NAME_PREFIX)) {
                    const parsed = JSON.parse(window.name.slice(WINDOW_NAME_PREFIX.length));
                    if (parsed && typeof parsed === 'object') return parsed;
                }
            } catch (e) {}

            return {};
        }

        function writeSessionStorageSafe(stateMap) {
            const serialized = JSON.stringify(stateMap);
            try {
                window.name = WINDOW_NAME_PREFIX + serialized;
            } catch (e) {}
            try {
                window.localStorage.setItem(STORAGE_KEY, serialized);
            } catch (e) {}
        }

        function clearSessionStorageSafe() {
            try {
                if (typeof window.name === 'string' && window.name.startsWith(WINDOW_NAME_PREFIX)) {
                    window.name = '';
                }
            } catch (e) {}
            try {
                window.localStorage.removeItem(STORAGE_KEY);
            } catch (e) {}
        }

        // Recebe atualizações em tempo real da nuvem (quando Firebase está ativo)
        window.applyCloudStatuses = function(cloudStatusesMap) {
            if (!cloudStatusesMap || typeof cloudStatusesMap !== 'object') return;
            let changed = false;
            opportunitiesState.forEach(item => {
                const st = cloudStatusesMap[String(item.id)];
                if (st && AGENDOR_OPTIONS.includes(st) && item.agendorStatus !== st) {
                    item.agendorStatus = st;
                    changed = true;
                }
            });
            if (changed) {
                writeSessionStorageSafe(cloudStatusesMap);
                syncUrlHashWithoutReload(cloudStatusesMap);
                applyFilters();
                updateSyncIndicator('synced', 'Sincronizado na nuvem • Tempo real');
            }
        };

        // Carrega estado combinando: Padrão Planilha -> Embutido -> Sessão/LocalStorage -> Hash da URL Online
        function loadAgendorState() {
            const embeddedMap = readEmbeddedState();
            const sessionMap = readSessionStorageSafe();
            const hashMap = decodeStateFromUrlHash();

            opportunitiesState = baseOpportunities.map(item => {
                const key = String(item.id);
                let resolvedStatus = item.defaultAgendorStatus;

                if (embeddedMap[key] && AGENDOR_OPTIONS.includes(embeddedMap[key])) {
                    resolvedStatus = embeddedMap[key];
                }
                if (sessionMap[key] && AGENDOR_OPTIONS.includes(sessionMap[key])) {
                    resolvedStatus = sessionMap[key];
                }
                if (hashMap[key] && AGENDOR_OPTIONS.includes(hashMap[key])) {
                    resolvedStatus = hashMap[key];
                }

                return {
                    ...item,
                    agendorStatus: resolvedStatus
                };
            });

            const initialMap = {};
            opportunitiesState.forEach(o => { initialMap[String(o.id)] = o.agendorStatus; });
            syncUrlHashWithoutReload(initialMap);
        }

        // Salva automaticamente na nuvem, na URL online e no armazenamento persistente sem criar cópias
        async function persistOnlineState(showToastMessage = false) {
            updateSyncIndicator('saving', 'Salvando online...');
            const mapToSave = {};
            opportunitiesState.forEach(item => {
                mapToSave[String(item.id)] = item.agendorStatus;
            });

            const scriptEl = document.getElementById('saved-state-script');
            if (scriptEl) {
                scriptEl.textContent = JSON.stringify(mapToSave);
            }

            writeSessionStorageSafe(mapToSave);
            syncUrlHashWithoutReload(mapToSave);

            // Grava na nuvem Firestore se disponível
            if (window._mroscoeCloudDocRef && window._mroscoeSetDoc) {
                try {
                    await window._mroscoeSetDoc(window._mroscoeCloudDocRef, {
                        statuses: mapToSave,
                        updatedAt: new Date().toISOString()
                    }, { merge: true });
                } catch (e) {
                    console.warn('Falha ao gravar no Firestore, mantido via URL/LocalStorage:', e);
                }
            }

            const nowStr = new Date().toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' });
            updateSyncIndicator('synced', `Salvo online • ${nowStr}`);

            if (showToastMessage) {
                showFloatingNotice(`Versão online atualizada (${nowStr}) sem criar cópias!`);
            }
        }

        // Botão explícito "Salvar Online"
        function saveOnlineNow() {
            persistOnlineState(true);
        }

        // Copia o link online já contendo todos os status atualizados no hash (#agendor=...)
        function copyShareableLink() {
            persistOnlineState(false);
            const shareUrl = window.location.href;
            const textarea = document.createElement('textarea');
            textarea.value = shareUrl;
            textarea.style.position = 'fixed';
            textarea.style.opacity = '0';
            document.body.appendChild(textarea);
            textarea.select();
            try {
                document.execCommand('copy');
                const btnText = document.getElementById('shareLinkBtnText');
                if (btnText) {
                    btnText.textContent = 'Link Copiado!';
                    setTimeout(() => { btnText.textContent = 'Copiar Link Atualizado'; }, 2200);
                }
                showFloatingNotice('Link online copiado! Quem abrir este link verá os status já atualizados.');
            } catch (e) {
                showFloatingNotice('URL atualizada na barra de endereços com os novos status.');
            }
            document.body.removeChild(textarea);
        }

        // Sobrescreve o arquivo .html local diretamente via File System Access API sem criar cópias
        async function overwriteLocalFile() {
            const stateMap = {};
            opportunitiesState.forEach(item => {
                stateMap[String(item.id)] = item.agendorStatus;
            });
            const jsonState = JSON.stringify(stateMap);

            const liveScript = document.getElementById('saved-state-script');
            if (liveScript) liveScript.textContent = jsonState;

            const clonedDoc = document.documentElement.cloneNode(true);
            const clonedTbody = clonedDoc.querySelector('#opportunitiesTableBody');
            if (clonedTbody) clonedTbody.innerHTML = '';
            const clonedMobileCards = clonedDoc.querySelector('#mobileOpportunitiesCards');
            if (clonedMobileCards) clonedMobileCards.innerHTML = '';
            const clonedDiscardedTbody = clonedDoc.querySelector('#discardedTableBody');
            if (clonedDiscardedTbody) clonedDiscardedTbody.innerHTML = '';
            const clonedNotice = clonedDoc.querySelector('#floatingSaveNotice');
            if (clonedNotice) {
                clonedNotice.classList.add('hidden');
                clonedNotice.classList.remove('flex');
            }
            const clonedModal = clonedDoc.querySelector('#detailModal');
            if (clonedModal) {
                clonedModal.classList.add('hidden');
                clonedModal.classList.remove('flex');
            }

            let clonedStateScript = clonedDoc.querySelector('#saved-state-script');
            if (clonedStateScript) {
                clonedStateScript.textContent = jsonState;
            }

            const fullHtml = '<!DOCTYPE html>\n' + clonedDoc.outerHTML;

            // Tenta sobrescrever diretamente no disco sem criar cópias (Chrome/Edge Desktop)
            if (typeof window.showSaveFilePicker === 'function') {
                try {
                    if (!window._mroscoeFileHandle) {
                        window._mroscoeFileHandle = await window.showSaveFilePicker({
                            suggestedName: 'dashboard_mroscoe.html',
                            types: [{
                                description: 'Arquivo HTML do Dashboard M.ROSCOE',
                                accept: { 'text/html': ['.html'] }
                            }]
                        });
                    }
                    const writable = await window._mroscoeFileHandle.createWritable();
                    await writable.write(fullHtml);
                    await writable.close();
                    showFloatingNotice('Arquivo local sobrescrito diretamente no disco sem criar cópias!');
                    return;
                } catch (err) {
                    if (err && err.name === 'AbortError') return;
                }
            }

            // Fallback caso o navegador não suporte showSaveFilePicker
            const blob = new Blob([fullHtml], { type: 'text/html;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'dashboard_mroscoe.html';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            setTimeout(() => URL.revokeObjectURL(url), 1500);
            showFloatingNotice('Arquivo atualizado salvo.');
        }

        function showFloatingNotice(htmlMessage) {
            const notice = document.getElementById('floatingSaveNotice');
            const textEl = document.getElementById('floatingNoticeText');
            if (!notice || !textEl) return;

            textEl.innerHTML = htmlMessage;
            notice.classList.remove('hidden');
            notice.classList.add('flex');
            window.safeIcons();

            clearTimeout(window._floatingNoticeTimer);
            window._floatingNoticeTimer = setTimeout(() => {
                hideFloatingNotice();
            }, 4500);
        }

        function hideFloatingNotice() {
            const notice = document.getElementById('floatingSaveNotice');
            if (notice) {
                notice.classList.add('hidden');
                notice.classList.remove('flex');
            }
        }

        // Update Agendor status of a specific opportunity
        function updateOpportunityAgendorStatus(id, newStatus) {
            const target = opportunitiesState.find(o => o.id === id);
            if (!target) return;
            target.agendorStatus = newStatus;
            persistOnlineState(true);
            applyFilters();

            if (currentModalItemId === id) {
                const modalSel = document.getElementById('modalAgendorSelect');
                modalSel.value = newStatus;
                modalSel.className = `px-3 py-2 rounded-md border text-xs font-bold cursor-pointer focus:outline-none ${getAgendorSelectClass(newStatus)}`;
            }
        }

        function handleModalAgendorChange(newStatus) {
            if (currentModalItemId !== null) {
                updateOpportunityAgendorStatus(currentModalItemId, newStatus);
            }
        }

        function resetAgendorStatus() {
            clearSessionStorageSafe();
            const scriptEl = document.getElementById('saved-state-script');
            if (scriptEl) scriptEl.textContent = '{}';

            opportunitiesState = baseOpportunities.map(item => ({
                ...item,
                agendorStatus: item.defaultAgendorStatus
            }));

            if (currentModalItemId !== null) {
                const currentItem = opportunitiesState.find(o => o.id === currentModalItemId);
                if (currentItem) {
                    const modalSel = document.getElementById('modalAgendorSelect');
                    modalSel.value = currentItem.agendorStatus;
                    modalSel.className = `px-3 py-2 rounded-md border text-xs font-bold cursor-pointer focus:outline-none ${getAgendorSelectClass(currentItem.agendorStatus)}`;
                }
            }

            persistOnlineState(false);
            applyFilters();
            showFloatingNotice('Status restaurados ao padrão original da planilha de 23/11/2026.');
        }

        // =========================================================================
        // MOBILE NAVIGATION & FILTER DRAWER CONTROLS
        // =========================================================================

        function toggleMobileFilters() {
            mobileFiltersOpen = !mobileFiltersOpen;
            const section = document.getElementById('filterControlSection');
            const chevron = document.getElementById('mobileFilterChevron');
            if (mobileFiltersOpen) {
                section.classList.remove('hidden');
                if (chevron) chevron.style.transform = 'rotate(180deg)';
            } else {
                section.classList.add('hidden');
                if (chevron) chevron.style.transform = 'rotate(0deg)';
            }
        }

        function mobileNavigate(target) {
            const navIds = ['mNavOverview', 'mNavOpportunities', 'mNavCharts', 'mNavDiscarded'];
            navIds.forEach(id => {
                const el = document.getElementById(id);
                if (!el) return;
                el.classList.remove('text-[#EE7D26]', 'font-bold');
                el.classList.add('text-slate-500', 'font-semibold');
            });

            if (target === 'discarded') {
                switchTab('discarded');
                const activeEl = document.getElementById('mNavDiscarded');
                activeEl.classList.add('text-[#EE7D26]', 'font-bold');
                activeEl.classList.remove('text-slate-500', 'font-semibold');
                window.scrollTo({ top: 0, behavior: 'smooth' });
                return;
            }

            switchTab('overview');

            if (target === 'overview') {
                const activeEl = document.getElementById('mNavOverview');
                activeEl.classList.add('text-[#EE7D26]', 'font-bold');
                activeEl.classList.remove('text-slate-500', 'font-semibold');
                window.scrollTo({ top: 0, behavior: 'smooth' });
            } else if (target === 'opportunities') {
                const activeEl = document.getElementById('mNavOpportunities');
                activeEl.classList.add('text-[#EE7D26]', 'font-bold');
                activeEl.classList.remove('text-slate-500', 'font-semibold');
                const sec = document.getElementById('sectionOpportunities');
                if (sec) sec.scrollIntoView({ behavior: 'smooth', block: 'start' });
            } else if (target === 'charts') {
                const activeEl = document.getElementById('mNavCharts');
                activeEl.classList.add('text-[#EE7D26]', 'font-bold');
                activeEl.classList.remove('text-slate-500', 'font-semibold');
                const sec = document.getElementById('sectionCharts');
                if (sec) sec.scrollIntoView({ behavior: 'smooth', block: 'start' });
            }
        }

        // =========================================================================
        // EXPORTAR CSV (EXCEL UTF-8 COM BOM)
        // =========================================================================
        function exportCSV() {
            const headers = [
                "Origem", "Status Agendor", "Prioridade Original", "Segmento M.ROSCOE",
                "Empresa Contratante", "Obra / Escopo", "CAPEX (R$ mi)", "Valor Fonte",
                "Mês Captação", "Cidade / UF", "UF", "Cronograma", "Decisor / Contato",
                "Fonte da Notícia", "Observações M.ROSCOE", "Link"
            ];

            const escapeCsvField = (val) => {
                if (val === null || val === undefined) return '""';
                const str = String(val).replace(/"/g, '""').replace(/\r?\n/g, ' ');
                return `"${str}"`;
            };

            const sortedForExport = [...opportunitiesState].sort((a, b) => a.numPlanilha - b.numPlanilha);

            const rows = sortedForExport.map(item => [
                item.origem, item.agendorStatus, item.prioridadeOrig, item.segmento,
                item.empresa, item.escopo, item.capexNum > 0 ? item.capexNum : "Não divulgado",
                item.capexDetalhe, item.mes, item.cidade, item.uf, item.cronograma,
                item.contato, item.fonteTexto, item.obs, item.link
            ].map(escapeCsvField).join(';'));

            const csvContent = '\uFEFF' + [headers.map(escapeCsvField).join(';'), ...rows].join('\r\n');
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);

            const link = document.createElement('a');
            link.href = url;
            link.download = 'Relatorio_Prospeccao_MRoscoe_Agendor_2026-11-23.csv';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            setTimeout(() => URL.revokeObjectURL(url), 1500);

            showFloatingNotice("Planilha <strong>CSV (Excel)</strong> exportada com sucesso.");
        }

        function getAgendorSelectClass(status) {
            if (status === "Adicionar Oportunidade no Agendor") return "agendor-select-add";
            if (status === "Oportunidade já adicionada no Agendor") return "agendor-select-added";
            return "agendor-select-discard";
        }

        function formatCapexSummary(millions) {
            if (millions === 0) return "R$ 0";
            if (millions >= 1000) {
                const billions = (millions / 1000).toLocaleString('pt-BR', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
                return `R$ ${billions} bi`;
            }
            return `R$ ${millions.toLocaleString('pt-BR')} mi`;
        }

        function switchTab(tabName) {
            const pageOverview = document.getElementById('pageOverview');
            const pageDiscarded = document.getElementById('pageDiscarded');
            const btnOverview = document.getElementById('tabBtnOverview');
            const btnDiscarded = document.getElementById('tabBtnDiscarded');

            if (tabName === 'overview') {
                pageOverview.classList.remove('hidden');
                pageDiscarded.classList.add('hidden');
                btnOverview.className = 'tab-active flex items-center gap-2 px-4 py-2.5 text-sm font-semibold whitespace-nowrap transition cursor-pointer rounded-t-md';
                btnDiscarded.className = 'tab-inactive flex items-center gap-2 px-4 py-2.5 text-sm font-semibold whitespace-nowrap transition cursor-pointer rounded-t-md';
            } else {
                pageOverview.classList.add('hidden');
                pageDiscarded.classList.remove('hidden');
                btnDiscarded.className = 'tab-active flex items-center gap-2 px-4 py-2.5 text-sm font-semibold whitespace-nowrap transition cursor-pointer rounded-t-md';
                btnOverview.className = 'tab-inactive flex items-center gap-2 px-4 py-2.5 text-sm font-semibold whitespace-nowrap transition cursor-pointer rounded-t-md';
            }
        }

        function toggleSegmentMetric(mode) {
            segmentMetricMode = mode;
            const btnCapex = document.getElementById('btnMetricCapex');
            const btnCount = document.getElementById('btnMetricCount');
            const titleEl = document.getElementById('chartSegmentTitle');

            if (mode === 'capex') {
                btnCapex.className = 'px-2.5 py-1 text-[11px] font-semibold rounded bg-[#EE7D26] text-white shadow-xs transition cursor-pointer';
                btnCount.className = 'px-2.5 py-1 text-[11px] font-semibold rounded text-slate-600 hover:text-slate-900 transition cursor-pointer';
                titleEl.textContent = 'Oportunidades por Segmento Oficial M.ROSCOE (R$ mi)';
            } else {
                btnCount.className = 'px-2.5 py-1 text-[11px] font-semibold rounded bg-[#EE7D26] text-white shadow-xs transition cursor-pointer';
                btnCapex.className = 'px-2.5 py-1 text-[11px] font-semibold rounded text-slate-600 hover:text-slate-900 transition cursor-pointer';
                titleEl.textContent = 'Oportunidades por Segmento Oficial M.ROSCOE (Qtd.)';
            }
            applyFilters();
        }

        function clearSearch() {
            document.getElementById('filterSearch').value = '';
            applyFilters();
        }

        function populateOriginFilter() {
            const sel = document.getElementById('filterOrigin');
            if (!sel) return;
            const counts = {};
            baseOpportunities.forEach(o => { counts[o.origem] = (counts[o.origem] || 0) + 1; });
            const names = Object.keys(counts).sort((a, b) => counts[b] - counts[a] || a.localeCompare(b));
            sel.innerHTML = '<option value="ALL">Todas as Origens</option>' +
                names.map(n => `<option value="${n}">${n} (${counts[n]})</option>`).join('');
        }

        function resetAllFilters() {
            document.getElementById('filterAgendor').value = 'ALL';
            document.getElementById('filterSegment').value = 'ALL';
            document.getElementById('filterMonth').value = 'ALL';
            document.getElementById('filterState').value = 'ALL';
            document.getElementById('filterOrigin').value = 'ALL';
            document.getElementById('filterSearch').value = '';
            document.getElementById('sortSelect').value = 'default';
            applyFilters();
        }

        function applyFilters() {
            const agendorVal = document.getElementById('filterAgendor').value;
            const segmentVal = document.getElementById('filterSegment').value;
            const monthVal = document.getElementById('filterMonth').value;
            const stateVal = document.getElementById('filterState').value;
            const originVal = document.getElementById('filterOrigin').value;
            const searchVal = document.getElementById('filterSearch').value.trim().toLowerCase();
            const sortVal = document.getElementById('sortSelect').value;

            const clearBtn = document.getElementById('clearSearchBtn');
            if (searchVal.length > 0) clearBtn.classList.remove('hidden');
            else clearBtn.classList.add('hidden');

            let activeFiltersCount = 0;
            if (agendorVal !== 'ALL') activeFiltersCount++;
            if (segmentVal !== 'ALL') activeFiltersCount++;
            if (monthVal !== 'ALL') activeFiltersCount++;
            if (stateVal !== 'ALL') activeFiltersCount++;
            if (originVal !== 'ALL') activeFiltersCount++;
            if (searchVal !== '') activeFiltersCount++;

            const badgeEl = document.getElementById('activeFilterBadge');
            const badgeCountEl = document.getElementById('activeFilterCount');
            const mobileFilterBadge = document.getElementById('mobileFilterBadgeCount');

            if (activeFiltersCount > 0) {
                badgeEl.classList.remove('hidden');
                badgeEl.classList.add('inline-flex');
                badgeCountEl.textContent = `${activeFiltersCount} filtro${activeFiltersCount > 1 ? 's' : ''} ativo${activeFiltersCount > 1 ? 's' : ''}`;
                if (mobileFilterBadge) {
                    mobileFilterBadge.classList.remove('hidden');
                    mobileFilterBadge.textContent = activeFiltersCount;
                }
            } else {
                badgeEl.classList.add('hidden');
                badgeEl.classList.remove('inline-flex');
                if (mobileFilterBadge) mobileFilterBadge.classList.add('hidden');
            }

            let filtered = opportunitiesState.filter(item => {
                if (agendorVal !== 'ALL' && item.agendorStatus !== agendorVal) return false;
                if (segmentVal !== 'ALL' && item.segmento !== segmentVal) return false;
                if (monthVal !== 'ALL' && item.mes !== monthVal) return false;
                if (stateVal !== 'ALL' && item.uf !== stateVal) return false;
                if (originVal !== 'ALL' && item.origem !== originVal) return false;
                if (searchVal !== '') {
                    const haystack = `${item.empresa} ${item.segmento} ${item.escopo} ${item.cidade} ${item.contato} ${item.obs} ${item.mes} ${item.origem}`.toLowerCase();
                    if (!haystack.includes(searchVal)) return false;
                }
                return true;
            });

            if (sortVal === 'agendor') {
                const rank = {
                    "Adicionar Oportunidade no Agendor": 1,
                    "Oportunidade já adicionada no Agendor": 2,
                    "Desconsiderar oportunidade": 3
                };
                filtered.sort((a, b) => rank[a.agendorStatus] - rank[b.agendorStatus] || a.numPlanilha - b.numPlanilha);
            } else if (sortVal === 'capex_desc') {
                filtered.sort((a, b) => b.capexNum - a.capexNum);
            } else if (sortVal === 'capex_asc') {
                filtered.sort((a, b) => a.capexNum - b.capexNum);
            } else if (sortVal === 'mes_desc') {
                filtered.sort((a, b) => MONTH_ORDER.indexOf(b.mes) - MONTH_ORDER.indexOf(a.mes) || a.numPlanilha - b.numPlanilha);
            } else if (sortVal === 'empresa_asc') {
                filtered.sort((a, b) => a.empresa.localeCompare(b.empresa));
            } else {
                filtered.sort((a, b) => a.numPlanilha - b.numPlanilha);
            }

            updateScorecards(filtered);
            updateCharts(filtered);
            renderOpportunitiesTable(filtered);
            renderMobileOpportunitiesCards(filtered);
        }

        function updateScorecards(data) {
            const totalObras = data.length;
            const comValorCount = data.filter(d => d.capexNum > 0).length;
            const semValorCount = totalObras - comValorCount;
            const sumCapexTotal = data.reduce((acc, d) => acc + d.capexNum, 0);

            const listAdd = data.filter(d => d.agendorStatus === "Adicionar Oportunidade no Agendor");
            const listAdded = data.filter(d => d.agendorStatus === "Oportunidade já adicionada no Agendor");
            const listDiscard = data.filter(d => d.agendorStatus === "Desconsiderar oportunidade");

            const capexAdd = listAdd.reduce((acc, d) => acc + d.capexNum, 0);
            const capexAdded = listAdded.reduce((acc, d) => acc + d.capexNum, 0);
            const capexDiscard = listDiscard.reduce((acc, d) => acc + d.capexNum, 0);

            const decisoresList = data.filter(d => d.temDecisor);

            document.getElementById('kpiTotalObras').textContent = `${totalObras} ${totalObras === 1 ? 'obra' : 'obras'}`;
            document.getElementById('kpiTotalSub').textContent = `${comValorCount} com CAPEX informado (+${semValorCount} N/D)`;
            document.getElementById('badgeCountOverview').textContent = totalObras;
            const mNavOppBadge = document.getElementById('mNavOppBadge');
            if (mNavOppBadge) mNavOppBadge.textContent = totalObras;

            document.getElementById('kpiTotalCapex').textContent = formatCapexSummary(sumCapexTotal);
            document.getElementById('kpiCapexSub').textContent = `R$ ${sumCapexTotal.toLocaleString('pt-BR')} mi somados na base filtrada`;

            document.getElementById('kpiAddCount').textContent = `${listAdd.length} ${listAdd.length === 1 ? 'obra' : 'obras'}`;
            document.getElementById('kpiAddCapex').textContent = `CAPEX: ${formatCapexSummary(capexAdd)}`;

            document.getElementById('kpiAddedCount').textContent = `${listAdded.length} ${listAdded.length === 1 ? 'obra' : 'obras'}`;
            document.getElementById('kpiAddedCapex').textContent = `CAPEX: ${formatCapexSummary(capexAdded)}`;

            document.getElementById('kpiDiscardCount').textContent = `${listDiscard.length} ${listDiscard.length === 1 ? 'obra' : 'obras'}`;
            document.getElementById('kpiDecisoresBadge').textContent = `${decisoresList.length} ${decisoresList.length === 1 ? 'decisor' : 'decisores'}`;
            document.getElementById('kpiDiscardSub').textContent = `CAPEX desc.: ${formatCapexSummary(capexDiscard)} • ${decisoresList.length} contatos nominais`;
            document.getElementById('kpiDiscardSub').title = decisoresList.map(d => `${d.empresa}: ${d.contato}`).join(' | ');
        }

        function updateCharts(data) {
            // CHART 1: TODOS OS 9 SEGMENTOS M.ROSCOE
            const segmentMap = {};
            OFFICIAL_SEGMENTS.forEach(seg => {
                segmentMap[seg] = { capex: 0, count: 0 };
            });

            data.forEach(item => {
                if (segmentMap[item.segmento]) {
                    segmentMap[item.segmento].capex += item.capexNum;
                    segmentMap[item.segmento].count += 1;
                }
            });

            const sortedSegments = [...OFFICIAL_SEGMENTS].sort((a, b) => {
                if (segmentMetricMode === 'capex') {
                    return segmentMap[b].capex - segmentMap[a].capex || segmentMap[b].count - segmentMap[a].count;
                }
                return segmentMap[b].count - segmentMap[a].count || segmentMap[b].capex - segmentMap[a].capex;
            });

            const segLabels = sortedSegments;
            const segValues = sortedSegments.map(s => segmentMetricMode === 'capex' ? segmentMap[s].capex : segmentMap[s].count);
            const segColors = sortedSegments.map(s => {
                const val = segmentMetricMode === 'capex' ? segmentMap[s].capex : segmentMap[s].count;
                return val > 0 ? '#EE7D26' : '#E2E8F0';
            });

            const ctxSeg = document.getElementById('chartSegments').getContext('2d');
            if (chartSegmentsInstance) chartSegmentsInstance.destroy();

            chartSegmentsInstance = new Chart(ctxSeg, {
                type: 'bar',
                data: {
                    labels: segLabels,
                    datasets: [{
                        label: segmentMetricMode === 'capex' ? 'CAPEX (R$ mi)' : 'Qtd. de Obras',
                        data: segValues,
                        backgroundColor: segColors,
                        hoverBackgroundColor: '#D66914',
                        borderRadius: 4,
                        barPercentage: 0.72
                    }]
                },
                options: {
                    indexAxis: 'y',
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            backgroundColor: '#1A1A1A',
                            padding: 10,
                            callbacks: {
                                title: (items) => sortedSegments[items[0].dataIndex],
                                label: function(context) {
                                    const fullSeg = sortedSegments[context.dataIndex];
                                    const info = segmentMap[fullSeg];
                                    if (segmentMetricMode === 'capex') {
                                        return ` CAPEX: R$ ${info.capex.toLocaleString('pt-BR')} mi (${info.count} ${info.count === 1 ? 'obra' : 'obras'})`;
                                    }
                                    return ` ${info.count} ${info.count === 1 ? 'obra' : 'obras'} (CAPEX: R$ ${info.capex.toLocaleString('pt-BR')} mi)`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            grid: { color: '#F1F5F9' },
                            ticks: {
                                font: { size: 10, family: 'Inter' },
                                color: '#64748B',
                                callback: (value) => segmentMetricMode === 'capex' ? `R$ ${value.toLocaleString('pt-BR')}` : value
                            }
                        },
                        y: {
                            grid: { display: false },
                            ticks: {
                                autoSkip: false,
                                font: { size: 11, weight: '500', family: 'Inter' },
                                color: '#334155'
                            }
                        }
                    }
                }
            });

            // CHART 2: STATUS DE TRIAGEM AGENDOR (DONUT)
            const cAdd = data.filter(d => d.agendorStatus === "Adicionar Oportunidade no Agendor").length;
            const cAdded = data.filter(d => d.agendorStatus === "Oportunidade já adicionada no Agendor").length;
            const cDiscard = data.filter(d => d.agendorStatus === "Desconsiderar oportunidade").length;
            const totalAg = cAdd + cAdded + cDiscard;

            const fmtPct = (v) => totalAg > 0 ? ((v / totalAg) * 100).toFixed(1).replace('.', ',') : '0,0';

            document.getElementById('legendAgendorAdd').textContent = `${cAdd} (${fmtPct(cAdd)}%)`;
            document.getElementById('legendAgendorAdded').textContent = `${cAdded} (${fmtPct(cAdded)}%)`;
            document.getElementById('legendAgendorDiscard').textContent = `${cDiscard} (${fmtPct(cDiscard)}%)`;

            const ctxAgendor = document.getElementById('chartAgendor').getContext('2d');
            if (chartAgendorInstance) chartAgendorInstance.destroy();

            chartAgendorInstance = new Chart(ctxAgendor, {
                type: 'doughnut',
                data: {
                    labels: [
                        'Adicionar Oportunidade no Agendor',
                        'Oportunidade já adicionada no Agendor',
                        'Desconsiderar oportunidade'
                    ],
                    datasets: [{
                        data: [cAdd, cAdded, cDiscard],
                        backgroundColor: ['#EE7D26', '#0F9D58', '#5F6368'],
                        borderColor: '#FFFFFF',
                        borderWidth: 3,
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '65%',
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            backgroundColor: '#1A1A1A',
                            padding: 10,
                            callbacks: {
                                label: (context) => ` ${context.raw} ${context.raw === 1 ? 'obra' : 'obras'} (${fmtPct(context.raw)}%)`
                            }
                        }
                    }
                }
            });

            // CHART 3: OPORTUNIDADES E CAPEX POR MÊS
            const monthMap = {};
            MONTH_ORDER.forEach(m => { monthMap[m] = { capex: 0, count: 0 }; });

            data.forEach(item => {
                if (monthMap[item.mes]) {
                    monthMap[item.mes].capex += item.capexNum;
                    monthMap[item.mes].count += 1;
                }
            });

            const monthCapexValues = MONTH_ORDER.map(m => monthMap[m].capex);
            const monthCountValues = MONTH_ORDER.map(m => monthMap[m].count);

            const ctxMonths = document.getElementById('chartMonths').getContext('2d');
            if (chartMonthsInstance) chartMonthsInstance.destroy();

            chartMonthsInstance = new Chart(ctxMonths, {
                type: 'bar',
                data: {
                    labels: MONTH_ORDER,
                    datasets: [
                        {
                            label: 'CAPEX (R$ mi)',
                            data: monthCapexValues,
                            backgroundColor: '#EE7D26',
                            hoverBackgroundColor: '#D66914',
                            borderRadius: 4,
                            yAxisID: 'y',
                            order: 2,
                            barPercentage: 0.52
                        },
                        {
                            label: 'Qtd. de Obras',
                            data: monthCountValues,
                            type: 'line',
                            borderColor: '#1A1A1A',
                            backgroundColor: '#1A1A1A',
                            borderWidth: 2.5,
                            pointRadius: 5,
                            pointHoverRadius: 7,
                            tension: 0.25,
                            yAxisID: 'y1',
                            order: 1
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    interaction: { mode: 'index', intersect: false },
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: { boxWidth: 11, font: { size: 11, family: 'Inter' }, color: '#475569' }
                        },
                        tooltip: {
                            backgroundColor: '#1A1A1A',
                            padding: 10,
                            callbacks: {
                                label: (context) => context.datasetIndex === 0
                                    ? ` CAPEX: R$ ${context.raw.toLocaleString('pt-BR')} mi`
                                    : ` Oportunidades: ${context.raw} ${context.raw === 1 ? 'obra' : 'obras'}`
                            }
                        }
                    },
                    scales: {
                        x: {
                            grid: { display: false },
                            ticks: { font: { size: 11, weight: '600', family: 'Inter' }, color: '#334155' }
                        },
                        y: {
                            type: 'linear',
                            position: 'left',
                            beginAtZero: true,
                            grid: { color: '#F1F5F9' },
                            ticks: {
                                font: { size: 10, family: 'Inter' },
                                color: '#EE7D26',
                                callback: (value) => value >= 1000 ? `R$ ${(value / 1000).toFixed(0)}bi` : `R$ ${value}m`
                            },
                            title: { display: true, text: 'CAPEX (R$ mi)', font: { size: 10, weight: '600' }, color: '#EE7D26' }
                        },
                        y1: {
                            type: 'linear',
                            position: 'right',
                            beginAtZero: true,
                            suggestedMax: 6,
                            grid: { drawOnChartArea: false },
                            ticks: { stepSize: 1, font: { size: 11, family: 'Inter' }, color: '#1A1A1A' },
                            title: { display: true, text: 'Qtd. Obras', font: { size: 10, weight: '600' }, color: '#1A1A1A' }
                        }
                    }
                }
            });
        }

        // Render Mobile Executive Cards (Smartphone < 768px)
        function renderMobileOpportunitiesCards(data) {
            const container = document.getElementById('mobileOpportunitiesCards');
            if (!container) return;

            if (data.length === 0) {
                container.innerHTML = '';
                return;
            }

            container.innerHTML = data.map(item => {
                const selectStyleClass = getAgendorSelectClass(item.agendorStatus);
                const optionsHtml = AGENDOR_OPTIONS.map(opt =>
                    `<option value="${opt}" ${item.agendorStatus === opt ? 'selected' : ''}>${opt}</option>`
                ).join('');

                const capexPill = item.capexNum > 0
                    ? `<span class="text-xs font-extrabold text-[#EE7D26] bg-[#FFF4EC] border border-[#F59B4E]/60 px-2.5 py-1 rounded-md shrink-0">${item.capexTexto}</span>`
                    : `<span class="text-xs font-semibold text-slate-500 bg-slate-100 px-2.5 py-1 rounded-md shrink-0">CAPEX N/D</span>`;

                const alertBanner = item.alerta
                    ? `<div class="mt-2 px-2.5 py-1.5 rounded bg-red-50 border border-red-200 text-[11px] font-bold text-red-700 flex items-center gap-1.5">
                         <i data-lucide="alert-triangle" class="w-3.5 h-3.5 shrink-0"></i>
                         <span>Alerta: Produção suspensa em MG (risco adiamento)</span>
                       </div>`
                    : '';

                const decisorPill = item.temDecisor
                    ? `<div class="mt-2 inline-flex items-center gap-1.5 text-[11px] font-semibold text-[#1A1A1A] bg-[#FFF4EC] border border-[#F59B4E]/50 px-2 py-1 rounded">
                         <i data-lucide="user-check" class="w-3.5 h-3.5 text-[#EE7D26] shrink-0"></i>
                         <span>${item.contato}</span>
                       </div>`
                    : '';

                return `
                    <article class="bg-white rounded-xl border border-slate-200 p-3.5 shadow-2xs">
                        <div class="flex items-start justify-between gap-2">
                            <div class="min-w-0">
                                <div class="flex items-center gap-1.5 text-[10px] font-bold uppercase tracking-wide text-slate-400">
                                    <span class="truncate max-w-[60%]">${item.origem}</span>
                                    <span>•</span>
                                    <span class="text-[#EE7D26] truncate">${item.segmento}</span>
                                </div>
                                <h3 class="text-sm font-extrabold text-slate-900 mt-0.5 leading-snug">${item.empresa}</h3>
                            </div>
                            ${capexPill}
                        </div>

                        <p class="text-xs text-slate-600 mt-2 line-clamp-2 leading-relaxed">${item.escopo}</p>

                        <div class="mt-2.5 flex flex-wrap items-center gap-2 text-[11px] text-slate-600">
                            <span class="inline-flex items-center gap-1 bg-slate-100 px-2 py-0.5 rounded font-medium">
                                <i data-lucide="map-pin" class="w-3 h-3 text-[#EE7D26]"></i>
                                ${item.uf}
                            </span>
                            <span class="inline-flex items-center gap-1 bg-slate-100 px-2 py-0.5 rounded font-medium">
                                <i data-lucide="calendar" class="w-3 h-3 text-slate-500"></i>
                                ${item.mes}
                            </span>
                            <span class="text-slate-400 truncate max-w-[180px]">${item.cidade}</span>
                        </div>

                        ${decisorPill}
                        ${alertBanner}

                        <div class="mt-3 pt-2.5 border-t border-slate-100 flex flex-col gap-2">
                            <select onchange="updateOpportunityAgendorStatus(${item.id}, this.value)" aria-label="Status Agendor de ${item.empresa}" class="w-full px-3 py-2.5 rounded-lg border text-xs font-bold cursor-pointer focus:outline-none ${selectStyleClass}">
                                ${optionsHtml}
                            </select>
                            <button onclick="openOpportunityModal(${item.id})" class="w-full py-2 px-3 rounded-lg bg-slate-100 active:bg-[#EE7D26] active:text-white text-slate-800 text-xs font-bold flex items-center justify-center gap-1.5 transition cursor-pointer">
                                <i data-lucide="file-text" class="w-3.5 h-3.5"></i>
                                <span>Ver Dossiê Completo</span>
                            </button>
                        </div>
                    </article>
                `;
            }).join('');

            window.safeIcons();
        }

        // Render Main Opportunities Table (Desktop >= 768px)
        function originBadge(origem) {
            const o = String(origem || 'Não informada');
            let cls = 'bg-sky-50 text-sky-800 border-sky-200';
            let icon = 'mail';
            if (/^agente/i.test(o)) { cls = 'bg-slate-100 text-slate-700 border-slate-200'; icon = 'bot'; }
            else if (/alert/i.test(o)) { cls = 'bg-amber-50 text-amber-800 border-amber-200'; icon = 'bell'; }
            return `<span class="inline-flex items-center gap-1 px-2 py-1 rounded-md border text-[11px] font-semibold leading-snug ${cls}"><i data-lucide="${icon}" class="w-3 h-3 shrink-0"></i><span>${o}</span></span>`;
        }

        function renderOpportunitiesTable(data) {
            const tbody = document.getElementById('opportunitiesTableBody');
            const emptyState = document.getElementById('emptyTableState');
            const countBadge = document.getElementById('tableRowCountBadge');

            countBadge.textContent = `${data.length} ${data.length === 1 ? 'registro' : 'registros'}`;

            if (data.length === 0) {
                tbody.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');

            tbody.innerHTML = data.map(item => {
                const selectStyleClass = getAgendorSelectClass(item.agendorStatus);

                const optionsHtml = AGENDOR_OPTIONS.map(opt =>
                    `<option value="${opt}" ${item.agendorStatus === opt ? 'selected' : ''}>${opt}</option>`
                ).join('');

                const alertTag = item.alerta
                    ? `<span class="mt-1 inline-flex items-center gap-1 text-[10px] font-bold text-red-700 bg-red-50 border border-red-200 px-1.5 py-0.5 rounded">
                         <i data-lucide="alert-triangle" class="w-3 h-3"></i> Risco adiamento
                       </span>`
                    : '';

                const capexDisplay = item.capexNum > 0
                    ? `<div class="font-bold text-slate-900">${item.capexTexto}</div>
                       <div class="text-[10px] text-slate-400 truncate max-w-[130px]" title="${item.capexDetalhe}">${item.capexDetalhe}</div>`
                    : `<span class="inline-block text-xs font-medium text-slate-400 italic bg-slate-100 px-2 py-0.5 rounded" title="${item.capexDetalhe}">N/D</span>`;

                const contatoDisplay = item.temDecisor
                    ? `<span class="inline-flex items-center gap-1 text-xs font-semibold text-[#1A1A1A] bg-[#FFF4EC] border border-[#F59B4E]/60 px-2 py-0.5 rounded">
                         <i data-lucide="user-check" class="w-3 h-3 text-[#EE7D26] shrink-0"></i> ${item.contato}
                       </span>`
                    : `<span class="text-xs text-slate-400">${item.contato}</span>`;

                return `
                    <tr onclick="openOpportunityModal(${item.id})" class="hover:bg-[#FFF4EC]/60 transition cursor-pointer group">
                        <td class="py-3 px-3 text-left">${originBadge(item.origem)}</td>
                        <td class="py-3 px-3" onclick="event.stopPropagation()">
                            <select onchange="updateOpportunityAgendorStatus(${item.id}, this.value)" aria-label="Status Agendor de ${item.empresa}" class="w-full px-2.5 py-1.5 rounded-md border text-xs font-bold cursor-pointer focus:outline-none transition ${selectStyleClass}">
                                ${optionsHtml}
                            </select>
                        </td>
                        <td class="py-3 px-3">
                            <span class="text-xs font-medium text-slate-700 leading-snug block">${item.segmento}</span>
                        </td>
                        <td class="py-3 px-3">
                            <div class="font-bold text-slate-900 group-hover:text-[#EE7D26] transition">${item.empresa}</div>
                            <div class="text-[10px] text-slate-400 mt-0.5">${item.prioridadeOrig}</div>
                            ${alertTag}
                        </td>
                        <td class="py-3 px-3">
                            <p class="text-xs text-slate-600 line-clamp-2 leading-relaxed" title="${item.escopo}">${item.escopo}</p>
                        </td>
                        <td class="py-3 px-3 text-right whitespace-nowrap">${capexDisplay}</td>
                        <td class="py-3 px-3 text-center whitespace-nowrap">
                            <span class="inline-block text-xs font-semibold text-slate-700 bg-slate-100 px-2 py-0.5 rounded border border-slate-200/80" title="${item.fonteTexto}">
                                ${item.mes}
                            </span>
                        </td>
                        <td class="py-3 px-3">
                            <div class="text-xs font-semibold text-slate-800">${item.cidade}</div>
                            <span class="text-[10px] font-bold uppercase text-slate-400">UF: ${item.uf}</span>
                        </td>
                        <td class="py-3 px-3">${contatoDisplay}</td>
                        <td class="py-3 px-3 text-center whitespace-nowrap" onclick="event.stopPropagation()">
                            <button onclick="openOpportunityModal(${item.id})" class="inline-flex items-center gap-1 px-2.5 py-1.5 rounded-md bg-slate-100 hover:bg-[#EE7D26] text-slate-700 hover:text-white text-xs font-semibold transition cursor-pointer" title="Abrir ficha completa">
                                <i data-lucide="eye" class="w-3.5 h-3.5"></i>
                                <span>Detalhes</span>
                            </button>
                        </td>
                    </tr>
                `;
            }).join('');

            window.safeIcons();
        }

        // Render Discarded & Monitor (Desktop Table + Mobile Cards)
        function renderDiscardedTable() {
            const tbody = document.getElementById('discardedTableBody');
            const mobileContainer = document.getElementById('mobileDiscardedCards');

            const getBadgeStyle = (type) => {
                if (type === 'monitor') return 'bg-amber-50 text-amber-800 border-amber-200';
                if (type === 'closed') return 'bg-slate-100 text-slate-600 border-slate-300';
                if (type === 'non_construction') return 'bg-red-50 text-red-700 border-red-200';
                return 'bg-slate-100 text-slate-700 border-slate-200';
            };

            if (tbody) {
                tbody.innerHTML = discardedData.map(item => `
                    <tr class="hover:bg-slate-50/80 transition">
                        <td class="py-3.5 px-4 text-center font-mono text-xs text-slate-400 font-semibold">${item.id}</td>
                        <td class="py-3.5 px-4 font-bold text-slate-900">${item.empresa}</td>
                        <td class="py-3.5 px-4 text-xs text-slate-700">${item.descricao}</td>
                        <td class="py-3.5 px-4 text-xs font-medium text-slate-700">${item.local}</td>
                        <td class="py-3.5 px-4 text-xs font-bold text-slate-800">${item.valor}</td>
                        <td class="py-3.5 px-4">
                            <span class="inline-flex items-center px-2.5 py-1 rounded-full text-[11px] font-bold border ${getBadgeStyle(item.badgeType)}">
                                ${item.badge}
                            </span>
                        </td>
                        <td class="py-3.5 px-4 text-xs text-slate-600 leading-relaxed">${item.parecer}</td>
                        <td class="py-3.5 px-4 text-center">
                            <a href="${item.link}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1 text-xs font-semibold text-[#EE7D26] hover:text-[#D66914] hover:underline">
                                <span>Link</span>
                                <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                            </a>
                        </td>
                    </tr>
                `).join('');
            }

            if (mobileContainer) {
                mobileContainer.innerHTML = discardedData.map(item => `
                    <article class="bg-white rounded-xl border border-slate-200 p-3.5 shadow-2xs">
                        <div class="flex items-start justify-between gap-2">
                            <div>
                                <span class="inline-flex items-center px-2 py-0.5 rounded-full text-[10px] font-bold border ${getBadgeStyle(item.badgeType)}">
                                    ${item.badge}
                                </span>
                                <h4 class="text-sm font-extrabold text-slate-900 mt-1.5">${item.empresa}</h4>
                            </div>
                            <span class="text-xs font-bold text-slate-700 bg-slate-100 px-2 py-1 rounded shrink-0">${item.valor}</span>
                        </div>
                        <p class="text-xs font-medium text-slate-700 mt-1.5">${item.descricao} • <span class="text-slate-500">${item.local}</span></p>
                        <p class="text-xs text-slate-600 mt-2 p-2.5 rounded-lg bg-slate-50 border border-slate-100 leading-relaxed">${item.parecer}</p>
                        <div class="mt-2.5 flex justify-end">
                            <a href="${item.link}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1 text-xs font-bold text-[#EE7D26]">
                                <span>Ver notícia original</span>
                                <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                            </a>
                        </div>
                    </article>
                `).join('');
            }
        }

        function openOpportunityModal(id) {
            const item = opportunitiesState.find(o => o.id === id);
            if (!item) return;
            currentModalItemId = id;

            document.getElementById('modalNumBadge').textContent = `Origem: ${item.origem}`;
            document.getElementById('modalPriorityOrigBadge').textContent = item.prioridadeOrig;
            document.getElementById('modalSegmentBadge').textContent = item.segmento;
            document.getElementById('modalCompanyTitle').textContent = item.empresa;

            const modalSel = document.getElementById('modalAgendorSelect');
            modalSel.value = item.agendorStatus;
            modalSel.className = `px-3 py-2 rounded-md border text-xs font-bold cursor-pointer focus:outline-none ${getAgendorSelectClass(item.agendorStatus)}`;

            document.getElementById('modalCapex').textContent = item.capexDetalhe;
            document.getElementById('modalMonth').textContent = item.mes;
            document.getElementById('modalLocation').textContent = item.cidade;
            document.getElementById('modalTimeline').textContent = item.cronograma;
            document.getElementById('modalScope').textContent = item.escopo;
            document.getElementById('modalContact').textContent = item.contato;
            document.getElementById('modalSourceName').textContent = item.fonteTexto;
            
            const obsBox = document.getElementById('modalObsBox');
            obsBox.textContent = item.obs;
            if (item.alerta) {
                obsBox.className = 'p-3.5 rounded-lg bg-red-50 border border-red-200 text-xs sm:text-sm text-red-900 font-medium leading-relaxed';
            } else {
                obsBox.className = 'p-3.5 rounded-lg bg-[#FFF4EC]/80 border border-[#F59B4E] text-xs sm:text-sm text-slate-800 leading-relaxed';
            }

            document.getElementById('modalSourceLink').href = item.link;
            document.getElementById('copyBtnText').textContent = 'Copiar Resumo';

            const modal = document.getElementById('detailModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            window.safeIcons();
        }

        function closeModal() {
            currentModalItemId = null;
            const modal = document.getElementById('detailModal');
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        function closeModalOnBackdrop(event) {
            if (event.target.id === 'detailModal') {
                closeModal();
            }
        }

        function copyOpportunitySummary() {
            if (currentModalItemId === null) return;
            const item = opportunitiesState.find(o => o.id === currentModalItemId);
            if (!item) return;

            const text = `[M.ROSCOE Prospecção - Semana 23/11/2026]\nOrigem: ${item.origem} | Status Agendor: ${item.agendorStatus}\nEmpresa: ${item.empresa}\nSegmento: ${item.segmento}\nLocal: ${item.cidade}\nCAPEX: ${item.capexDetalhe} | Mês Captação: ${item.mes}\nCronograma: ${item.cronograma}\nEscopo: ${item.escopo}\nDecisor: ${item.contato}\nObs: ${item.obs}\nFonte (${item.fonteTexto}): ${item.link}`;

            const textarea = document.createElement('textarea');
            textarea.value = text;
            textarea.style.position = 'fixed';
            textarea.style.opacity = '0';
            document.body.appendChild(textarea);
            textarea.select();
            try {
                document.execCommand('copy');
                document.getElementById('copyBtnText').textContent = 'Copiado!';
                setTimeout(() => {
                    document.getElementById('copyBtnText').textContent = 'Copiar Resumo';
                }, 2000);
            } catch (err) {
                console.error('Erro ao copiar', err);
            }
            document.body.removeChild(textarea);
        }

        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape') closeModal();
        });

        window.addEventListener('DOMContentLoaded', () => {
            loadAgendorState();
            populateOriginFilter();
            renderDiscardedTable();
            applyFilters();
            window.safeIcons();
        });
    </script>
</body>
</html>
