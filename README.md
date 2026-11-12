<!DOCTYPE html>
<html lang="hi" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CryptoPillar Options Terminal (BTC, ETH, XAUT)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkbg: '#0b0f19',
                        cardbg: '#131c2e',
                        bordercolor: '#1e293b',
                        accentgreen: '#10b981',
                        accentred: '#ef4444',
                        accentblue: '#3b82f6'
                    }
                }
            }
        }
    </script>
    <style>
        body { background-color: #0b0f19; color: #f8fafc; font-family: system-ui, -apple-system, sans-serif; }
    </style>
</head>
<body class="min-h-screen p-4 md:p-6">

    <!-- Top Navigation / Coin Selector -->
    <header class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center mb-6 pb-4 border-b border-bordercolor gap-4">
        <div>
            <h1 class="text-2xl font-black tracking-wider text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-emerald-400">
                CRYPTOPILLAR <span class="text-xs px-2 py-0.5 bg-blue-500/20 text-blue-400 rounded-full border border-blue-500/30">OPTIONS TERMINAL</span>
            </h1>
            <p class="text-xs text-slate-400 mt-0.5">Live Institutional Grade Analytics & AI Options Predictions</p>
        </div>

        <!-- Coin Toggles -->
        <div class="flex items-center gap-2 bg-cardbg p-1.5 rounded-xl border border-bordercolor shadow-lg">
            <button onclick="switchCoin('BTC')" id="btn-BTC" class="px-4 py-2 rounded-lg font-bold text-sm transition-all bg-blue-600 text-white shadow">BTC/USD</button>
            <button onclick="switchCoin('ETH')" id="btn-ETH" class="px-4 py-2 rounded-lg font-bold text-sm transition-all text-slate-400 hover:text-white">ETH/USD</button>
            <button onclick="switchCoin('XAUT')" id="btn-XAUT" class="px-4 py-2 rounded-lg font-bold text-sm transition-all text-slate-400 hover:text-white">XAUT (Gold)</button>
        </div>

        <!-- Live Ticker Stats -->
        <div class="flex items-center gap-4 bg-cardbg px-4 py-2 rounded-xl border border-bordercolor">
            <div>
                <div class="text-[10px] text-slate-400 uppercase tracking-wider">Spot Price</div>
                <div id="top-price" class="text-lg font-mono font-bold text-emerald-400">$...</div>
            </div>
            <div class="h-8 w-[1px] bg-bordercolor"></div>
            <div>
                <div class="text-[10px] text-slate-400 uppercase tracking-wider">24h Change</div>
                <div id="top-change" class="text-sm font-mono font-semibold text-emerald-400">+0.00%</div>
            </div>
            <div class="h-8 w-[1px] bg-bordercolor"></div>
            <div>
                <div class="text-[10px] text-slate-400 uppercase tracking-wider">ATM IV / PCR</div>
                <div id="top-iv" class="text-xs font-mono font-semibold text-amber-400">52.4% / 0.88</div>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto grid grid-cols-1 lg:grid-cols-3 gap-6">

        <!-- Left & Center: Charts & AI Predictions -->
        <div class="lg:col-span-2 space-y-6">

            <!-- AI Predictive Intelligence & Macro Event Analyzer -->
            <div class="bg-cardbg rounded-2xl p-5 border border-bordercolor shadow-xl">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-base font-bold flex items-center gap-2">
                        <span class="w-2.5 h-2.5 rounded-full bg-blue-500 animate-pulse"></span>
                        AI Predictive Intelligence & Macro Outlook
                    </h2>
                    <span id="ai-sentiment-badge" class="px-2.5 py-1 text-xs font-bold rounded-md bg-amber-500/20 text-amber-400 border border-amber-500/30">Bearish / Cautious</span>
                </div>

                <!-- Scenario Simulators -->
                <div class="grid grid-cols-3 gap-2 mb-4">
                    <button onclick="setScenario('baseline')" id="scen-baseline" class="p-2.5 text-xs rounded-xl border border-blue-500 bg-blue-500/10 font-semibold text-blue-400 transition-all text-left">
                        <div class="font-bold">1. Current Baseline</div>
                        <div class="text-[10px] opacity-75">Hot CPI / DXY Strength</div>
                    </button>
                    <button onclick="setScenario('hot')" id="scen-hot" class="p-2.5 text-xs rounded-xl border border-bordercolor bg-darkbg font-semibold text-slate-400 hover:border-slate-600 transition-all text-left">
                        <div class="font-bold">2. Hot PPI Shock</div>
                        <div class="text-[10px] opacity-75">Hawkish Fed / Dip Risk</div>
                    </button>
                    <button onclick="setScenario('cool')" id="scen-cool" class="p-2.5 text-xs rounded-xl border border-bordercolor bg-darkbg font-semibold text-slate-400 hover:border-slate-600 transition-all text-left">
                        <div class="font-bold">3. Cool PPI / Rally</div>
                        <div class="text-[10px] opacity-75">Liquidity Rebound</div>
                    </button>
                </div>

                <!-- Probability Bar & Outlook Text -->
                <div class="space-y-3 bg-darkbg p-4 rounded-xl border border-bordercolor">
                    <div class="flex justify-between text-xs font-semibold">
                        <span class="text-emerald-400">Bullish: <span id="prob-bull">30</span>%</span>
                        <span class="text-blue-400">Sideways: <span id="prob-side">25</span>%</span>
                        <span class="text-rose-400">Bearish: <span id="prob-bear">45</span>%</span>
                    </div>
                    <!-- Visual Prob Bar -->
                    <div class="h-2.5 w-full bg-slate-800 rounded-full overflow-hidden flex">
                        <div id="bar-bull" class="bg-emerald-500 transition-all duration-500" style="width: 30%"></div>
                        <div id="bar-side" class="bg-blue-500 transition-all duration-500" style="width: 25%"></div>
                        <div id="bar-bear" class="bg-rose-500 transition-all duration-500" style="width: 45%"></div>
                    </div>
                    <p id="ai-summary-text" class="text-xs text-slate-300 leading-relaxed pt-1">
                        Bitcoin is struggling below $74k resistance amid $1.88B ETF outflows. Options strategy favors defined-risk Bear Put Spreads or selling out-of-the-money call spreads during IV spikes.
                    </p>
                </div>

                <!-- Macro Events & One-Click Setup Loader -->
                <div class="mt-4 flex flex-col sm:flex-row justify-between items-center gap-3 pt-3 border-t border-bordercolor">
                    <div class="text-xs text-slate-400 flex items-center gap-2">
                        <span class="font-semibold text-amber-400">⚠️ Next Event:</span> US PPI & Fed Speeches (Nov 13) — <span class="text-slate-200">IV Crush Warning Active</span>
                    </div>
                    <button onclick="loadAIStrategy()" class="px-4 py-2 bg-gradient-to-r from-blue-600 to-emerald-600 hover:from-blue-500 hover:to-emerald-500 text-white font-bold text-xs rounded-xl shadow-lg transition-all flex items-center gap-2">
                        Load AI Setup to Calculator &rarr;
                    </button>
                </div>
            </div>

            <!-- Price & Forecast Chart Canvas -->
            <div class="bg-cardbg rounded-2xl p-5 border border-bordercolor shadow-xl">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-sm font-bold text-slate-200">15-Min Live Price & AI Forecast Cone</h3>
                    <div class="text-xs font-mono text-slate-400" id="chart-timeframe">Interval: 15m</div>
                </div>
                <div class="relative h-64 w-full">
                    <canvas id="marketChart"></canvas>
                </div>
            </div>

            <!-- Options Chain Quick Select -->
            <div class="bg-cardbg rounded-2xl p-5 border border-bordercolor shadow-xl">
                <h3 class="text-sm font-bold text-slate-200 mb-3">Live Options Chain Snapshot (Click Strike to Trade)</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs font-mono">
                        <thead>
                            <tr class="border-b border-bordercolor text-slate-400">
                                <th class="pb-2">Call IV</th>
                                <th class="pb-2">Call Bid/Ask</th>
                                <th class="pb-2 text-center text-emerald-400 font-bold">STRIKE</th>
                                <th class="pb-2 text-right">Put Bid/Ask</th>
                                <th class="pb-2 text-right">Put IV</th>
                            </tr>
                        </thead>
                        <tbody id="options-chain-body" class="divide-y divide-bordercolor/50">
                            <!-- Populated dynamically via JS -->
                        </tbody>
                    </table>
                </div>
            </div>

        </div>

        <!-- Right Column: Interactive Calculators -->
        <div class="space-y-6">

            <!-- Calculator 1: Lot Sizing & Risk Manager -->
            <div class="bg-cardbg rounded-2xl p-5 border border-bordercolor shadow-xl">
                <h3 class="text-sm font-bold text-slate-200 mb-4 flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-emerald-500"></span> Lot Sizing & Risk Calculator
                </h3>
                <div class="space-y-3 text-xs">
                    <div>
                        <label class="block text-slate-400 mb-1">Total Trading Capital ($)</label>
                        <input type="number" id="calc-capital" value="5000" class="w-full bg-darkbg border border-bordercolor rounded-xl px-3 py-2 font-mono text-white focus:outline-none focus:border-blue-500">
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-slate-400 mb-1">Risk Per Trade (%)</label>
                            <input type="number" id="calc-risk-pct" value="2" class="w-full bg-darkbg border border-bordercolor rounded-xl px-3 py-2 font-mono text-white focus:outline-none focus:border-blue-500">
                        </div>
                        <div>
                            <label class="block text-slate-400 mb-1">Option Premium ($)</label>
                            <input type="number" id="calc-premium" value="350" class="w-full bg-darkbg border border-bordercolor rounded-xl px-3 py-2 font-mono text-white focus:outline-none focus:border-blue-500">
                        </div>
                    </div>
                    <div class="bg-darkbg p-3 rounded-xl border border-bordercolor mt-3 space-y-1.5 font-mono">
                        <div class="flex justify-between text-slate-400">
                            <span>Max Risk Amount:</span>
                            <span id="res-risk-amt" class="text-rose-400 font-bold">$100.00</span>
                        </div>
                        <div class="flex justify-between text-slate-400">
                            <span>Recommended Lots:</span>
                            <span id="res-lots" class="text-emerald-400 font-bold">1 Lot</span>
                        </div>
                    </div>
                    <button onclick="calculateRisk()" class="w-full py-2.5 bg-blue-600 hover:bg-blue-500 text-white font-bold rounded-xl shadow transition-all mt-2">
                        Calculate Risk
                    </button>
                </div>
            </div>

            <!-- Calculator 2: Payoff Simulator -->
            <div class="bg-cardbg rounded-2xl p-5 border border-bordercolor shadow-xl">
                <h3 class="text-sm font-bold text-slate-200 mb-4 flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-blue-500"></span> Options Payoff & PnL Simulator
                </h3>
                <div class="space-y-3 text-xs">
                    <div>
                        <label class="block text-slate-400 mb-1">Selected Strategy Type</label>
                        <select id="payoff-strategy" class="w-full bg-darkbg border border-bordercolor rounded-xl px-3 py-2 text-white focus:outline-none focus:border-blue-500">
                            <option value="long_put">Long Put (Bearish)</option>
                            <option value="long_call">Long Call (Bullish)</option>
                            <option value="bear_put_spread">Bear Put Spread</option>
                        </select>
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-slate-400 mb-1">Strike Price ($)</label>
                            <input type="number" id="payoff-strike" value="70000" class="w-full bg-darkbg border border-bordercolor rounded-xl px-3 py-2 font-mono text-white">
                        </div>
                        <div>
                            <label class="block text-slate-400 mb-1">Net Debit / Cost ($)</label>
                            <input type="number" id="payoff-cost" value="450" class="w-full bg-darkbg border border-bordercolor rounded-xl px-3 py-2 font-mono text-white">
                        </div>
                    </div>
                    <div class="bg-darkbg p-3 rounded-xl border border-bordercolor mt-3 space-y-1.5 font-mono text-xs">
                        <div class="flex justify-between text-slate-400">
                            <span>Max Profit:</span>
                            <span id="res-max-profit" class="text-emerald-400 font-bold">Uncapped</span>
                        </div>
                        <div class="flex justify-between text-slate-400">
                            <span>Max Loss:</span>
                            <span id="res-max-loss" class="text-rose-400 font-bold">$450.00</span>
                        </div>
                        <div class="flex justify-between text-slate-400">
                            <span>Breakeven Expiry:</span>
                            <span id="res-breakeven" class="text-blue-400 font-bold">$69,550</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Quick Guide for Options Trading -->
            <div class="bg-cardbg rounded-2xl p-5 border border-bordercolor shadow-xl">
                <h3 class="text-sm font-bold text-slate-200 mb-2">💡 Quick Scalping Tip</h3>
                <p class="text-xs text-slate-400 leading-relaxed">
                    Options buying mein hamesha event se pehle **IV Crush** ka dhyan rakhein. Jab market direction clear na ho, toh naked buying ke bajay **Spreads** use karein taaki theta decay se bach sakein.
                </p>
            </div>

        </div>

    </main>

    <footer class="max-w-7xl mx-auto text-center mt-12 py-4 border-t border-bordercolor text-xs text-slate-500">
        CryptoPillar Options Terminal &bull; Built for BTC, ETH, and XAUT Options Scalpers
    </footer>

    <!-- JavaScript Logic & Live API Engine -->
    <script>
        let currentCoin = 'BTC';
        let marketChart = null;

        const coinDataConfig = {
            BTC: { price: 71250, change: -1.85, iv: '54.2%', pcr: '0.82', strikes: [68000, 69000, 70000, 71250, 72000, 73000, 74000] },
            ETH: { price: 2680, change: -2.40, iv: '61.5%', pcr: '0.74', strikes: [2500, 2550, 2600, 2680, 2750, 2800, 2900] },
            XAUT: { price: 4095, change: +1.15, iv: '24.8%', pcr: '1.45', strikes: [3950, 4000, 4050, 4095, 4150, 4200, 4250] }
        };

        const aiScenarios = {
            baseline: {
                badge: "Bearish / Cautious", badgeClass: "bg-amber-500/20 text-amber-400 border-amber-500/30",
                bull: 30, side: 25, bear: 45,
                text: "Bitcoin is struggling below $74k resistance amid $1.88B ETF outflows. Options strategy favors defined-risk Bear Put Spreads."
            },
            hot: {
                badge: "High Volatility / Bearish", badgeClass: "bg-rose-500/20 text-rose-400 border-rose-500/30",
                bull: 15, side: 20, bear: 65,
                text: "Hot PPI / Hawkish Fed tone increases probability of a sharp flush toward $65k support. Aggressive Put buying recommended on resistance rejection."
            },
            cool: {
                badge: "Bullish Rebound", badgeClass: "bg-emerald-500/20 text-emerald-400 border-emerald-500/30",
                bull: 55, side: 30, bear: 15,
                text: "Cooler inflation data or safe-haven gold accumulation (XAUT) triggers liquidity rebound. Bull Call Spreads and dips buying have high expectancy."
            }
        };

        function switchCoin(coin) {
            currentCoin = coin;
            ['BTC', 'ETH', 'XAUT'].forEach(c => {
                const btn = document.getElementById(`btn-${c}`);
                if (c === coin) {
                    btn.className = "px-4 py-2 rounded-lg font-bold text-sm transition-all bg-blue-600 text-white shadow";
                } else {
                    btn.className = "px-4 py-2 rounded-lg font-bold text-sm transition-all text-slate-400 hover:text-white";
                }
            });
            updateUI();
            fetchLiveSpot();
        }

        function updateUI() {
            const data = coinDataConfig[currentCoin];
            document.getElementById('top-price').innerText = `$${data.price.toLocaleString()}`;
            const changeEl = document.getElementById('top-change');
            changeEl.innerText = `${data.change >= 0 ? '+' : ''}${data.change}%`;
            changeEl.className = `text-sm font-mono font-semibold ${data.change >= 0 ? 'text-emerald-400' : 'text-rose-400'}`;
            document.getElementById('top-iv').innerText = `${data.iv} / ${data.pcr}`;

            // Render Options Chain
            const tbody = document.getElementById('options-chain-body');
            tbody.innerHTML = '';
            data.strikes.forEach(strike => {
                const isAtm = strike === data.price || Math.abs(strike - data.price) < (data.price * 0.01);
                const tr = document.createElement('tr');
                tr.className = isAtm ? 'bg-blue-500/10 font-bold' : '';
                tr.innerHTML = `
                    <td class="py-2 text-slate-400">${(parseFloat(data.iv) + Math.random()*2).toFixed(1)}%</td>
                    <td class="py-2 text-slate-300">$${(strike * 0.02).toFixed(1)} / $${(strike * 0.023).toFixed(1)}</td>
                    <td class="py-2 text-center text-emerald-400 cursor-pointer hover:underline" onclick="selectStrike(${strike})">${strike} ${isAtm ? '⭐(ATM)' : ''}</td>
                    <td class="py-2 text-right text-slate-300">$${(strike * 0.018).toFixed(1)} / $${(strike * 0.021).toFixed(1)}</td>
                    <td class="py-2 text-right text-slate-400">${(parseFloat(data.iv) - Math.random()*2).toFixed(1)}%</td>
                `;
                tbody.appendChild(tr);
            });

            updateChart();
        }

        function setScenario(scenKey) {
            ['baseline', 'hot', 'cool'].forEach(s => {
                cons
