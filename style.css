<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PromptRouter - Multi-Persona Prompt Compiler</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        navy: {
                            900: '#060b19',
                            800: '#0b132b',
                            700: '#1c2541',
                            600: '#2a365c',
                        },
                        mint: {
                            DEFAULT: '#6fffe9',
                            dark: '#5bc0be',
                            glow: 'rgba(111, 255, 233, 0.25)',
                        }
                    }
                }
            }
        }
    </script>
    <!-- Google Font Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;600&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #060b19;
            color: #f4f7f6;
            background-image: 
                radial-gradient(circle at 15% 15%, rgba(28, 37, 65, 0.8) 0%, transparent 40%),
                radial-gradient(circle at 85% 85%, rgba(91, 192, 190, 0.15) 0%, transparent 45%);
            background-attachment: fixed;
        }

        .code-font {
            font-family: 'Fira Code', monospace;
        }

        /* Glassmorphism utility */
        .glass-panel {
            background: rgba(11, 19, 43, 0.7);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(111, 255, 233, 0.12);
        }

        .glass-card {
            background: rgba(28, 37, 65, 0.55);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            transition: all 0.25s ease-in-out;
        }

        .glass-card:hover {
            border-color: rgba(111, 255, 233, 0.3);
            box-shadow: 0 10px 30px -10px rgba(111, 255, 233, 0.15);
        }

        .glow-button {
            background: linear-gradient(135deg, #5bc0be 0%, #6fffe9 100%);
            box-shadow: 0 0 20px rgba(111, 255, 233, 0.3);
            transition: all 0.2s ease;
        }

        .glow-button:hover {
            box-shadow: 0 0 28px rgba(111, 255, 233, 0.5);
            transform: translateY(-1px);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(11, 19, 43, 0.5);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(91, 192, 190, 0.4);
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #6fffe9;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Top Navigation Header -->
    <header class="w-full glass-panel sticky top-0 z-50 border-b border-mint/10 px-6 py-4">
        <div class="max-w-7xl mx-auto flex flex-wrap justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-navy-700 to-mint-dark flex items-center justify-center border border-mint/30 shadow-lg shadow-mint/10">
                    <svg class="w-6 h-6 text-mint" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
                    </svg>
                </div>
                <div>
                    <h1 class="text-xl font-bold tracking-tight text-white flex items-center gap-2">
                        Prompt<span class="text-mint">Router</span>
                        <span class="text-xs font-mono font-normal px-2 py-0.5 rounded bg-mint/10 text-mint border border-mint/20">v2.5 Engine</span>
                    </h1>
                    <p class="text-xs text-gray-400">Intent-Driven Multi-Persona Prompt Compiler</p>
                </div>
            </div>

            <!-- API Configuration & Preset Quick Actions -->
            <div class="flex items-center gap-3 flex-wrap">
                <div class="relative flex items-center">
                    <span class="absolute left-3 text-xs text-mint font-mono">API Key:</span>
                    <input type="password" id="api-key-input" placeholder="Gemini API Key (Optional for live testing)" 
                        class="bg-navy-900/80 border border-navy-600 focus:border-mint text-xs text-white rounded-lg pl-16 pr-3 py-2 w-64 outline-none transition-colors code-font">
                </div>
                <button onclick="toggleGlobalSettings()" class="text-xs bg-navy-700 hover:bg-navy-600 text-gray-300 hover:text-white px-3 py-2 rounded-lg border border-white/10 transition-colors flex items-center gap-1.5">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"/></svg>
                    Settings
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto p-4 sm:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Intent Input & Compiler Controls -->
        <section class="lg:col-span-4 flex flex-col gap-6">
            
            <!-- Raw Intent Input Card -->
            <div class="glass-panel rounded-2xl p-5 shadow-xl flex flex-col gap-4">
                <div class="flex justify-between items-center">
                    <label for="raw-intent" class="text-sm font-semibold text-mint flex items-center gap-2">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/></svg>
                        Raw Goal / Intent
                    </label>
                    <span class="text-xs text-gray-400 font-mono">Single-line input</span>
                </div>

                <textarea id="raw-intent" rows="3" placeholder="e.g. Build a fast search index for customer logs with low memory footprint and high query efficiency..."
                    class="w-full bg-navy-900/90 border border-navy-600 focus:border-mint text-sm text-gray-100 rounded-xl p-3 outline-none resize-none transition-all placeholder-gray-500"></textarea>

                <!-- Sample Intent Chips -->
                <div>
                    <span class="text-xs text-gray-400 block mb-2 font-medium">Quick Preset Intents:</span>
                    <div class="flex flex-wrap gap-1.5">
                        <button onclick="setPresetIntent('Build a high-throughput search index for JSON customer logs')" class="text-xs bg-navy-700/60 hover:bg-navy-600 border border-white/5 hover:border-mint/30 text-gray-300 rounded-lg px-2.5 py-1 transition-all">🔍 Search Index</button>
                        <button onclick="setPresetIntent('Analyze Q3 financial revenue drops and present strategic mitigation steps')" class="text-xs bg-navy-700/60 hover:bg-navy-600 border border-white/5 hover:border-mint/30 text-gray-300 rounded-lg px-2.5 py-1 transition-all">📈 Revenue Analysis</button>
                        <button onclick="setPresetIntent('Design a sci-fi cyberpunk story about an AI detective solving digital crimes')" class="text-xs bg-navy-700/60 hover:bg-navy-600 border border-white/5 hover:border-mint/30 text-gray-300 rounded-lg px-2.5 py-1 transition-all">🌃 Cyberpunk Story</button>
                    </div>
                </div>

                <!-- Target Persona Selector -->
                <div class="mt-2">
                    <label class="text-sm font-semibold text-mint block mb-2">Target Personas (Select 1 to 4):</label>
                    <div class="grid grid-cols-1 gap-2" id="persona-selector">
                        <!-- Populated by JavaScript -->
                    </div>
                </div>

                <!-- Compile Button -->
                <button onclick="compilePrompts()" class="glow-button text-navy-900 font-bold py-3.5 px-4 rounded-xl text-center flex items-center justify-center gap-2 mt-2">
                    <svg class="w-5 h-5 fill-current" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.57l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.57l7-10a1 1 0 011.12-.384z" clip-rule="evenodd"/></button>
                    Compile Multi-Persona Prompts
                </button>
            </div>

            <!-- Pipeline Parameters Drawer (Config Settings) -->
            <div id="settings-panel" class="glass-panel rounded-2xl p-5 shadow-xl hidden flex-col gap-4">
                <h3 class="text-sm font-bold text-mint uppercase tracking-wider">Compiler Engine Guardrails</h3>
                
                <div class="space-y-3 text-xs">
                    <div>
                        <label class="text-gray-300 font-medium block mb-1">Few-Shot Context Style:</label>
                        <select id="fewshot-style" class="w-full bg-navy-900 border border-navy-600 text-gray-200 rounded-lg p-2 outline-none">
                            <option value="strict">Strict Production (Edge Cases + Security)</option>
                            <option value="balanced" selected>Balanced (Standard Input/Output Pairs)</option>
                            <option value="minimal">Minimal (Zero-shot focused)</option>
                        </select>
                    </div>

                    <div>
                        <label class="text-gray-300 font-medium block mb-1">Output Format Constraint:</label>
                        <select id="format-constraint" class="w-full bg-navy-900 border border-navy-600 text-gray-200 rounded-lg p-2 outline-none">
                            <option value="json" selected>Strict Structured JSON Schema</option>
                            <option value="markdown">Executive Markdown Report</option>
                            <option value="code_block">Clean Code Block Only (No Markdown Text)</option>
                        </select>
                    </div>

                    <div class="flex items-center justify-between pt-1">
                        <span class="text-gray-300">Enforce Negative Constraints:</span>
                        <input type="checkbox" id="enforce-negatives" checked class="accent-mint w-4 h-4 rounded">
                    </div>
                </div>
            </div>

        </section>

        <!-- Right Column: Compiled Persona Cards Grid & Live API Inspector -->
        <section class="lg:col-span-8 flex flex-col gap-6">

            <!-- Compilation Status Bar -->
            <div class="glass-panel rounded-2xl px-5 py-3.5 flex flex-wrap justify-between items-center gap-3">
                <div class="flex items-center gap-2 text-xs">
                    <span class="w-2.5 h-2.5 rounded-full bg-mint animate-pulse"></span>
                    <span class="text-gray-300 font-mono" id="engine-status">Engine Ready • Awaiting Intent Compilation</span>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="copyAllCompiled()" class="text-xs bg-navy-700/80 hover:bg-navy-600 text-mint border border-mint/20 px-3 py-1.5 rounded-lg transition-colors flex items-center gap-1 font-mono">
                        <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7v8a2 2 0 002 2h6M8 7V5a2 2 0 012-2h6a2 2 0 012 2v2M8 7H6a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2v-2"/></svg>
                        Copy All Prompts
                    </button>
                </div>
            </div>

            <!-- Dynamic Persona Cards Workspace -->
            <div id="compiled-cards-grid" class="grid grid-cols-1 gap-6">
                <!-- Empty Placeholder State -->
                <div class="glass-panel rounded-2xl p-12 text-center flex flex-col items-center justify-center border-dashed border-navy-600">
                    <div class="w-16 h-16 rounded-full bg-navy-700/50 flex items-center justify-center text-mint mb-4 border border-mint/20">
                        <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"/></svg>
                    </div>
                    <h3 class="text-lg font-bold text-white mb-1">No Prompts Compiled Yet</h3>
                    <p class="text-sm text-gray-400 max-w-md">Enter your raw goal on the left panel, select your target personas, and click 'Compile Multi-Persona Prompts' to construct tailored prompt pipelines.</p>
                </div>
            </div>

        </section>

    </main>

    <!-- Global Toast Alert -->
    <div id="toast" class="fixed bottom-5 right-5 glass-panel border border-mint text-mint text-xs font-mono px-4 py-3 rounded-xl shadow-2xl translate-y-20 opacity-0 transition-all duration-300 z-50 flex items-center gap-2">
        <svg class="w-4 h-4 text-mint" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>
        <span id="toast-message">Notification text</span>
    </div>

    <!-- JavaScript Logic & Engine -->
    <script>
        // Definition of available Persona Profiles
        const PERSONAS = [
            {
                id: 'code_architect',
                name: 'Code Architect & Senior Engineer',
                badge: 'Technical & Production',
                icon: '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>',
                roleDescription: 'Act as a Principal Software Architect and Lead Systems Engineer with 15+ years of experience in high-performance computing.',
                fewShotTemplate: (intent) => `INPUT: "${intent}"\nEXPECTED STRUCTURE: Optimized code algorithm, memory layout considerations, time complexity analysis (Big-O), unit test coverage suite.`,
                constraints: ['Must produce clean, production-ready code with type annotations.', 'Include benchmark assumptions.', 'No hand-waving explanations.']
            },
            {
                id: 'executive_brief',
                name: 'Executive & Strategic Briefing',
                badge: 'Business & Management',
                icon: '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/>',
                roleDescription: 'Act as a Chief Strategy Officer (CSO) and Management Consultant advising C-suite executives.',
                fewShotTemplate: (intent) => `INPUT: "${intent}"\nEXPECTED STRUCTURE: Executive Summary (3 bullets), ROI Projection, Key Risk Assessment Matrix, 30-60-90 Day Execution Roadmap.`,
                constraints: ['Keep high-level focus on strategic ROI and risk.', 'Avoid excessive technical jargon without defining business impact.', 'Include quantifiable metrics.']
            },
            {
                id: 'data_analyst',
                name: 'Data Analytics & Query Specialist',
                badge: 'Data & SQL/Pandas',
                icon: '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4m0 5c0 2.21-3.582 4-8 4s-8-1.79-8-4"/>',
                roleDescription: 'Act as a Lead Data Scientist and Analytics Engineer specializing in SQL, Python Data Analytics, and ETL Pipeline Optimization.',
                fewShotTemplate: (intent) => `INPUT: "${intent}"\nEXPECTED STRUCTURE: Optimized SQL CTE queries, Data Schema assumptions, Pandas data transformation script, Edge case data cleaning rules.`,
                constraints: ['Use standard ANSI SQL or Pandas best practices.', 'Ensure query performance optimization.', 'Handle NULL values and timestamp timezone offsets.']
            },
            {
                id: 'creative_storyteller',
                name: 'Creative Narrative & Visionary',
                badge: 'Story & Engagement',
                icon: '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 4a2 2 0 114 0v1a2 2 0 01-2 2 2 2 0 01-2-2V4zm-6 8a2 2 0 114 0v1a2 2 0 01-2 2 2 2 0 01-2-2v-1zm12 0a2 2 0 114 0v1a2 2 0 01-2 2 2 2 0 01-2-2v-1zM4 18a2 2 0 012-2h12a2 2 0 012 2v1H4v-1z"/>',
                roleDescription: 'Act as a World-Class Narrative Architect, Creative Director, and Speculative Fiction Author.',
                fewShotTemplate: (intent) => `INPUT: "${intent}"\nEXPECTED STRUCTURE: Sensory atmosphere setting, Character arcs, Narrative plot points, Visually evocative sensory details.`,
                constraints: ['Prioritize rich atmosphere and deep emotional resonance.', 'Avoid cliched storytelling tropes.', 'Maintain consistent tone and pacing.']
            }
        ];

        // State Store
        let selectedPersonaIds = ['code_architect', 'executive_brief'];
        let compiledPromptsStore = {};

        // Initialization
        window.onload = function() {
            renderPersonaSelector();
        };

        // Render Persona Selection List
        function renderPersonaSelector() {
            const container = document.getElementById('persona-selector');
            container.innerHTML = PERSONAS.map(p => {
                const isSelected = selectedPersonaIds.includes(p.id);
                return `
                    <div onclick="togglePersonaSelection('${p.id}')" 
                        class="cursor-pointer p-3 rounded-xl border flex items-center justify-between transition-all ${isSelected ? 'bg-navy-700/80 border-mint text-white shadow-md' : 'bg-navy-900/50 border-navy-600 text-gray-400 hover:border-gray-500'}">
                        <div class="flex items-center gap-3">
                            <svg class="w-5 h-5 ${isSelected ? 'text-mint' : 'text-gray-500'}" fill="none" stroke="currentColor" viewBox="0 0 24 24">${p.icon}</svg>
                            <div>
                                <div class="text-xs font-semibold ${isSelected ? 'text-white' : 'text-gray-300'}">${p.name}</div>
                                <div class="text-[10px] text-gray-400 font-mono">${p.badge}</div>
                            </div>
                        </div>
                        <input type="checkbox" ${isSelected ? 'checked' : ''} class="accent-mint w-4 h-4 pointer-events-none">
                    </div>
                `;
            }).join('');
        }

        // Toggle Persona Selection
        function togglePersonaSelection(id) {
            if (selectedPersonaIds.includes(id)) {
                if (selectedPersonaIds.length === 1) {
                    showToast("Please keep at least 1 persona selected.");
                    return;
                }
                selectedPersonaIds = selectedPersonaIds.filter(item => item !== id);
            } else {
                if (selectedPersonaIds.length >= 4) {
                    showToast("Maximum 4 personas can be selected at once.");
                    return;
                }
                selectedPersonaIds.push(id);
            }
            renderPersonaSelector();
        }

        // Set Preset Intent
        function setPresetIntent(text) {
            document.getElementById('raw-intent').value = text;
        }

        // Toggle Settings Panel
        function toggleGlobalSettings() {
            const panel = document.getElementById('settings-panel');
            panel.classList.toggle('hidden');
            panel.classList.toggle('flex');
        }

        // Prompt Compiler Engine Core
        function compilePrompts() {
            const rawIntent = document.getElementById('raw-intent').value.trim();
            if (!rawIntent) {
                showToast("Please enter a raw goal or intent first.");
                return;
            }

            const fewShotStyle = document.getElementById('fewshot-style').value;
            const formatConstraint = document.getElementById('format-constraint').value;
            const enforceNegatives = document.getElementById('enforce-negatives').checked;

            const grid = document.getElementById('compiled-cards-grid');
            grid.innerHTML = '';
            compiledPromptsStore = {};

            // Processing Indicator
            document.getElementById('engine-status').innerText = `Engine Processing • Compiling ${selectedPersonaIds.length} Persona Pipelines...`;

            selectedPersonaIds.forEach(id => {
                const persona = PERSONAS.find(p => p.id === id);
                if (!persona) return;

                // Deconstruct Intent & Build Structured Prompt Pipeline
                const compiledPrompt = buildPersonaPrompt(persona, rawIntent, fewShotStyle, formatConstraint, enforceNegatives);
                compiledPromptsStore[id] = compiledPrompt;

                // Create Result Card Component
                const card = document.createElement('div');
                card.className = "glass-panel rounded-2xl p-5 shadow-xl flex flex-col gap-4 border border-navy-600 hover:border-mint/30 transition-all";
                card.id = `card-${id}`;

                card.innerHTML = `
                    <!-- Card Header -->
                    <div class="flex flex-wrap justify-between items-center gap-2 border-b border-white/10 pb-3">
                        <div class="flex items-center gap-2.5">
                            <span class="p-2 rounded-lg bg-navy-700 text-mint border border-mint/20">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">${persona.icon}</svg>
                            </span>
                            <div>
                                <h3 class="text-sm font-bold text-white">${persona.name}</h3>
                                <span class="text-[10px] font-mono text-mint">${persona.badge}</span>
                            </div>
                        </div>

                        <div class="flex items-center gap-2">
                            <button onclick="copySinglePrompt('${id}')" class="text-xs bg-navy-700 hover:bg-navy-600 text-gray-200 px-2.5 py-1.5 rounded-lg border border-white/10 flex items-center gap-1 font-mono transition-colors">
                                <svg class="w-3.5 h-3.5 text-mint" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7v8a2 2 0 002 2h6M8 7V5a2 2 0 012-2h6a2 2 0 012 2v2M8 7H6a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2v-2"/></svg>
                                Copy Prompt
                            </button>
                            <button onclick="testLiveWithGemini('${id}')" class="text-xs glow-button text-navy-900 font-bold px-3 py-1.5 rounded-lg flex items-center gap-1 transition-all">
                                <svg class="w-3.5 h-3.5 fill-current" viewBox="0 0 20 20"><path d="M10 12a2 2 0 100-4 2 2 0 000 4z"/><path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd"/></svg>
                                Test Live
                            </button>
                        </div>
                    </div>

                    <!-- Compiled Prompt Box -->
                    <div class="relative">
                        <span class="absolute top-2 right-3 text-[10px] font-mono text-gray-500 uppercase">Compiled Prompt String</span>
                        <pre class="w-full bg-navy-900/90 border border-navy-700 rounded-xl p-3.5 text-xs text-gray-200 code-font whitespace-pre-wrap max-h-64 overflow-y-auto leading-relaxed select-all" id="prompt-text-${id}">${escapeHtml(compiledPrompt)}</pre>
                    </div>

                    <!-- Live Gemini Response Output (Hidden initially) -->
                    <div id="live-response-container-${id}" class="hidden flex-col gap-2 pt-2 border-t border-white/5">
                        <div class="flex justify-between items-center text-xs">
                            <span class="text-mint font-mono flex items-center gap-1.5 font-semibold">
                                <span class="w-2 h-2 rounded-full bg-mint animate-ping"></span>
                                Live Gemini Output:
                            </span>
                            <span class="text-[10px] text-gray-400 font-mono" id="response-time-${id}"></span>
                        </div>
                        <div class="bg-navy-900/80 border border-mint/20 rounded-xl p-3.5 text-xs text-gray-100 leading-relaxed overflow-x-auto min-h-[80px]" id="live-output-${id}">
                            <!-- API Output rendered here -->
                        </div>
                    </div>
                `;

                grid.appendChild(card);
            });

            document.getElementById('engine-status').innerText = `Engine Ready • ${selectedPersonaIds.length} Persona Prompts Compiled`;
            showToast("Compilation successful!");
        }

        // Construct Individual Prompt Pipeline String
        function buildPersonaPrompt(persona, intent, fewShotStyle, formatConstraint, enforceNegatives) {
            let prompt = `=== SYSTEM INSTRUCTION & ROLE ===\n${persona.roleDescription}\n\n`;

            prompt += `=== USER INTENT & DECOMPOSITION ===\nPrimary Goal: "${intent}"\nTask Decomposition: Deconstruct the goal into logical execution phases, addressing root requirements and secondary implications.\n\n`;

            if (fewShotStyle !== 'minimal') {
                prompt += `=== FEW-SHOT CONTEXT & EXAMPLES ===\n${persona.fewShotTemplate(intent)}\n\n`;
            }

            prompt += `=== CONSTRAINTS & GUARDRAILS ===\n`;
            persona.constraints.forEach((c, idx) => {
                prompt += `${idx + 1}. ${c}\n`;
            });

            if (enforceNegatives) {
                prompt += `* Negative Constraints: Do NOT introduce hallucinated dependencies. Do NOT use generic placeholder text. Avoid vague summaries.\n`;
            }

            prompt += `\n=== REQUIRED OUTPUT FORMAT ===\n`;
            if (formatConstraint === 'json') {
                prompt += `Respond strictly with a valid JSON object matching this schema:\n{\n  "persona": "${persona.name}",\n  "status": "success",\n  "executiveSummary": "String",\n  "primaryArtifact": "String or Code",\n  "metadata": { "keyTakeaways": ["String"], "confidenceScore": 0.98 }\n}`;
            } else if (formatConstraint === 'markdown') {
                prompt += `Format response as a clean, structured Markdown document with standard Headers (##), Bullet points, and Code blocks where appropriate.`;
            } else {
                prompt += `Provide ONLY the raw execution code or primary output inside a standard syntax-highlighted markdown code block. Include zero introductory or concluding text.`;
            }

            return prompt;
        }

        // Test Live via Gemini API
        async function testLiveWithGemini(personaId) {
            const apiKeyInput = document.getElementById('api-key-input').value.trim();
            const compiledPrompt = compiledPromptsStore[personaId];
            
            if (!compiledPrompt) {
                showToast("Please compile prompts first.");
                return;
            }

            const responseContainer = document.getElementById(`live-response-container-${personaId}`);
            const outputBox = document.getElementById(`live-output-${personaId}`);
            const timeTag = document.getElementById(`response-time-${personaId}`);

            responseContainer.classList.remove('hidden');
            responseContainer.classList.add('flex');
            outputBox.innerHTML = `<div class="flex items-center gap-2 text-gray-400 font-mono"><svg class="w-4 h-4 animate-spin text-mint" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v1m0 14v1m8-8h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707"/></svg> Executing request with gemini-3-flash-preview...</div>`;

            const startTime = Date.now();
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKeyInput}`;

            const payload = {
                contents: [
                    {
                        parts: [
                            { text: compiledPrompt }
                        ]
                    }
                ]
            };

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    const errData = await response.json();
                    throw new Error(errData.error?.message || `HTTP ${response.status} Error`);
                }

                const result = await response.json();
                const elapsedTime = ((Date.now() - startTime) / 1000).toFixed(2);
                timeTag.innerText = `Latency: ${elapsedTime}s`;

                const textOutput = result.candidates?.[0]?.content?.parts?.[0]?.text;

                if (textOutput) {
                    outputBox.innerHTML = `<pre class="whitespace-pre-wrap code-font text-xs text-mint/90 leading-relaxed">${escapeHtml(textOutput)}</pre>`;
                } else {
                    outputBox.innerHTML = `<span class="text-yellow-400">Response received, but no text content found in structure.</span>`;
                }

            } catch (err) {
                console.error("Gemini API Error:", err);
                outputBox.innerHTML = `<span class="text-rose-400 font-mono font-medium">Error: ${escapeHtml(err.message)}</span>`;
                timeTag.innerText = `Failed`;
            }
        }

        // Copy Single Compiled Prompt to Clipboard
        function copySinglePrompt(personaId) {
            const promptText = compiledPromptsStore[personaId];
            if (!promptText) return;

            copyToClipboard(promptText);
            showToast("Copied persona prompt to clipboard!");
        }

        // Copy All Compiled Prompts
        function copyAllCompiled() {
            if (Object.keys(compiledPromptsStore).length === 0) {
                showToast("No compiled prompts to copy.");
                return;
            }

            let combined = "";
            for (const [id, text] of Object.entries(compiledPromptsStore)) {
                const persona = PERSONAS.find(p => p.id === id);
                combined += `================================================\nPERSONA: ${persona ? persona.name : id}\n================================================\n\n${text}\n\n\n`;
            }

            copyToClipboard(combined);
            showToast("Copied ALL persona prompts to clipboard!");
        }

        // Clipboard Helper using execCommand fallback for iFrame compatibility
        function copyToClipboard(text) {
            const textarea = document.createElement('textarea');
            textarea.value = text;
            textarea.style.position = 'fixed';
            textarea.style.opacity = '0';
            document.body.appendChild(textarea);
            textarea.select();
            try {
                document.execCommand('copy');
            } catch (err) {
                console.error('Copy failed', err);
            }
            document.body.removeChild(textarea);
        }

        // Toast Notification Trigger
        function showToast(msg) {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toast-message');
            toastMsg.innerText = msg;
            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        // Helper: Escape HTML special characters
        function escapeHtml(str) {
            return str
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>
