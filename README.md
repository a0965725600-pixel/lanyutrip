# lanyutrip
<!DOCTYPE html>
<html lang="zh-TW" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>蘭嶼大學生熱血探索計畫：花蓮出發</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'brand-bg': '#fdfbf7',
                        'brand-surface': '#f3eee3',
                        'brand-primary': '#0f766e',
                        'brand-secondary': '#ccfbf1',
                        'brand-accent': '#ea580c',
                        'text-main': '#374151',
                        'text-light': '#6b7280'
                    }
                }
            }
        }
    </script>
    <style>
        .chart-container { position: relative; width: 100%; max-width: 600px; margin: 0 auto; height: 300px; max-height: 400px; }
        @media (min-width: 768px) { .chart-container { height: 350px; } }
        .loader { border: 3px solid #f3f3f3; border-top: 3px solid #ea580c; border-radius: 50%; width: 20px; height: 20px; animation: spin 1s linear infinite; display: inline-block; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        .day-content { animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="bg-brand-bg text-text-main antialiased">

<nav class="fixed top-0 w-full bg-brand-bg/90 backdrop-blur-md shadow-sm z-50">
        <div class="max-w-6xl mx-auto px-4 h-16 flex justify-between items-center">
            <div class="flex items-center gap-2 cursor-pointer" onclick="window.scrollTo(0,0)">
                <span class="text-2xl">🏝️</span>
                <span class="font-bold text-brand-primary text-lg">蘭嶼熱血計畫</span>
            </div>
            <div class="hidden md:flex space-x-6 font-medium">
                <a href="#transport" class="hover:text-brand-primary transition">交通</a>
                <a href="#itinerary" class="hover:text-brand-primary transition">行程</a>
                <a href="#budget" class="hover:text-brand-primary transition">預算</a>
                <a href="#ai-guide" class="text-brand-accent font-bold">✨ 智慧嚮導</a>
            </div>
        </div>
    </nav>

    <header class="pt-32 pb-16 px-4 text-center border-b border-gray-200">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-4xl md:text-5xl font-extrabold text-brand-primary mb-4">花蓮 ➔ 蘭嶼：青春探索計畫</h1>
            <p class="text-lg text-text-light mb-8">結合 ✨ AI 智慧輔助，為您的跳島之旅提供量身定制的建議與文化導覽。</p>
            <div class="flex justify-center gap-4 text-sm md:text-base">
                <span class="bg-brand-secondary text-brand-primary px-4 py-2 rounded-full font-bold">4天3夜</span>
                <span class="bg-brand-secondary text-brand-primary px-4 py-2 rounded-full font-bold">預算 NT$ 9,500</span>
            </div>
        </div>
    </header>

    <main class="max-w-6xl mx-auto px-4 py-16 space-y-24">

        <section id="transport" class="scroll-mt-24">
            <h2 class="text-3xl font-bold text-brand-primary border-l-4 border-brand-accent pl-4 mb-8">交通路線圖</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-center">
                <div class="bg-white p-8 rounded-3xl shadow-sm border border-gray-100">
                    <div class="text-4xl mb-4">🚆</div>
                    <h3 class="font-bold text-xl mb-2">台鐵南下</h3>
                    <p class="text-text-light text-sm">花蓮車站 ➔ 台東車站<br>建議搭乘普悠瑪或自強 3000</p>
                </div>
                <div class="bg-white p-8 rounded-3xl shadow-sm border border-gray-100">
                    <div class="text-4xl mb-4">🚕</div>
                    <h3 class="font-bold text-xl mb-2">接駁轉乘</h3>
                    <p class="text-text-light text-sm">台東車站 ➔ 富岡漁港<br>計程車約 15-20 分鐘</p>
                </div>
                <div class="bg-brand-primary p-8 rounded-3xl shadow-lg text-white">
                    <div class="text-4xl mb-4 text-brand-secondary">⛴️</div>
                    <h3 class="font-bold text-xl mb-2">跨海航行</h3>
                    <p class="opacity-90 text-sm">富岡漁港 ➔ 蘭嶼開元港<br>航程約 2.5 小時，記得吃暈船藥</p>
                </div>
            </div>
        </section>

        <section id="itinerary" class="scroll-mt-24">
            <div class="flex justify-between items-end mb-8">
                <div>
                    <h2 class="text-3xl font-bold text-brand-primary border-l-4 border-brand-accent pl-4">每日行程規劃</h2>
                </div>
                <button onclick="getItineraryAI()" class="text-xs md:text-sm bg-brand-secondary text-brand-primary px-4 py-2 rounded-full font-bold hover:bg-brand-primary hover:text-white transition">✨ AI 推薦祕境</button>
            </div>

            <div id="itinerary-ai-box" class="hidden mb-6 bg-orange-50 border border-orange-100 p-4 rounded-xl">
                <div class="flex items-center gap-2 mb-1">
                    <div id="iti-loader" class="loader hidden"></div>
                    <span class="font-bold text-brand-accent text-sm">✨ AI 建議：</span>
                </div>
                <p id="iti-ai-text" class="text-sm italic text-gray-700"></p>
            </div>

            <div class="flex flex-col lg:flex-row gap-8">
                <div class="lg:w-1/4 flex lg:flex-col overflow-x-auto gap-2">
                    <button class="tab-btn w-full text-left px-6 py-4 rounded-xl font-bold bg-brand-primary text-white" onclick="switchDay(1, this)">Day 1: 抵達與夕陽</button>
                    <button class="tab-btn w-full text-left px-6 py-4 rounded-xl font-bold bg-white text-text-light border" onclick="switchDay(2, this)">Day 2: 湛藍潛水</button>
                    <button class="tab-btn w-full text-left px-6 py-4 rounded-xl font-bold bg-white text-text-light border" onclick="switchDay(3, this)">Day 3: 傳統文化</button>
                    <button class="tab-btn w-full text-left px-6 py-4 rounded-xl font-bold bg-white text-text-light border" onclick="switchDay(4, this)">Day 4: 伴手禮歸途</button>
                </div>
                <div class="lg:w-3/4 bg-white p-8 rounded-3xl shadow-sm border border-gray-100 min-h-[300px]">
                    <div id="day-1" class="day-content">
                        <h3 class="text-2xl font-bold text-brand-primary mb-4">Day 1：開啟島嶼生活</h3>
                        <ul class="space-y-4 text-text-light">
                            <li class="flex gap-3"><strong>13:00</strong> 抵達開元港，領取機車與入住</li>
                            <li class="flex gap-3"><strong>15:30</strong> 環島認識路況，造訪鱷魚岩</li>
                            <li class="flex gap-3"><strong>17:30</strong> 青青草原看夕陽，享受海風</li>
                        </ul>
                    </div>
                    <div id="day-2" class="day-content hidden">
                        <h3 class="text-2xl font-bold text-brand-primary mb-4">Day 2：擁抱湛藍海洋</h3>
                        <ul class="space-y-4 text-text-light">
                            <li class="flex gap-3"><strong>08:30</strong> 專業浮潛體驗（東清或八代灣）</li>
                            <li class="flex gap-3"><strong>13:30</strong> 野銀冷泉消暑消暑</li>
                            <li class="flex gap-3"><strong>19:00</strong> 夜觀角鴞導覽</li>
                        </ul>
                    </div>
                    <div id="day-3" class="day-content hidden">
                        <h3 class="text-2xl font-bold text-brand-primary mb-4">Day 3：深入達悟文化</h3>
                        <ul class="space-y-4 text-text-light">
                            <li class="flex gap-3"><strong>09:00</strong> 野銀地下屋專業文化導覽</li>
                            <li class="flex gap-3"><strong>14:00</strong> 蘭嶼氣象站攻頂看 360 度海景</li>
                            <li class="flex gap-3"><strong>18:30</strong> 部落風味餐：品嚐飛魚料理</li>
                        </ul>
                    </div>
                    <div id="day-4" class="day-content hidden">
                        <h3 class="text-2xl font-bold text-brand-primary mb-4">Day 4：收藏湛藍回憶</h3>
                        <ul class="space-y-4 text-text-light">
                            <li class="flex gap-3"><strong>09:00</strong> 購買特色伴手禮與明信片</li>
                            <li class="flex gap-3"><strong>11:00</strong> 前往開元港候船</li>
                            <li class="flex gap-3"><strong>15:30</strong> 抵達台東轉乘火車回花蓮</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <section id="budget" class="scroll-mt-24">
            <h2 class="text-3xl font-bold text-brand-primary border-l-4 border-brand-accent pl-4 mb-8">預算花費分析</h2>
            <div class="bg-white p-8 rounded-3xl shadow-sm border border-gray-100 flex flex-col md:flex-row gap-12 items-center">
                <div class="w-full md:w-1/2">
                    <div class="chart-container">
                        <canvas id="budgetChart"></canvas>
                    </div>
                </div>
                <div class="w-full md:w-1/2 space-y-6">
                    <h3 class="text-xl font-bold">✨ AI 預算小管家</h3>
                    <div class="flex gap-2">
                        <input type="number" id="budget-input" placeholder="輸入預算 (例: 8000)" class="flex-1 border p-3 rounded-xl focus:ring-2 focus:ring-brand-primary outline-none">
                        <button onclick="getBudgetAI()" class="bg-brand-primary text-white px-6 py-3 rounded-xl font-bold">分析</button>
                    </div>
                    <div id="budget-ai-box" class="hidden p-4 bg-brand-surface rounded-xl">
                        <div id="bud-loader" class="loader hidden mr-2"></div>
                        <p id="bud-ai-text" class="text-sm font-medium text-brand-primary"></p>
                    </div>
                </div>
            </div>
        </section>

        <section id="ai-guide" class="scroll-mt-24">
            <div class="bg-brand-primary rounded-[3rem] p-8 md:p-16 text-white shadow-2xl">
                <h2 class="text-3xl font-bold mb-4">✨ AI 達悟智慧嚮導</h2>
                <p class="mb-8 opacity-90">想了解達悟語、當地禁忌或推薦美食嗎？</p>
                <div class="flex flex-col md:flex-row gap-4">
                    <input type="text" id="guide-input" placeholder="例如：謝謝的達悟語怎麼說？" class="flex-1 p-4 rounded-2xl text-text-main focus:outline-none focus:ring-4 focus:ring-brand-accent/50">
                    <button onclick="askGuideAI()" class="bg-brand-accent px-8 py-4 rounded-2xl font-bold hover:scale-105 transition">詢問嚮導</button>
                </div>
                <div id="guide-box" class="hidden mt-8 bg-white/10 p-6 rounded-2xl border border-white/20">
                    <div id="guide-loader" class="loader hidden mb-2 border-white/30"></div>
                    <p id="guide-text" class="leading-relaxed"></p>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-brand-surface py-12 text-center text-text-light">
        <p class="font-bold mb-2">願你在蘭嶼找到最純粹的自己</p>
        <p class="text-xs">© 2026 蘭嶼熱血探索計畫 | Powered by Gemini AI</p>
    </footer>

    <script>
        const apiKey = ""; // 請在此填入您的 API Key

        async function fetchGemini(prompt, system = "") {
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            const body = { contents: [{ parts: [{ text: prompt }] }] };
            if (system) body.systemInstruction = { parts: [{ text: system }] };
            
            const resp = await fetch(url, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(body) });
            const data = await resp.json();
            return data.candidates[0].content.parts[0].text;
        }

        function switchDay(day, btn) {
            document.querySelectorAll('.day-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`day-${day}`).classList.remove('hidden');
            document.querySelectorAll('.tab-btn').forEach(b => b.className = 'tab-btn w-full text-left px-6 py-4 rounded-xl font-bold bg-white text-text-light border');
            btn.className = 'tab-btn w-full text-left px-6 py-4 rounded-xl font-bold bg-brand-primary text-white';
        }

        async function getItineraryAI() {
            const box = document.getElementById('itinerary-ai-box');
            const text = document.getElementById('iti-ai-text');
            const loader = document.getElementById('iti-loader');
            box.classList.remove('hidden');
            loader.classList.remove('hidden');
            text.innerText = "正在規劃秘境行程...";
            try {
                text.innerText = await fetchGemini("我是一個大學生，正在規劃蘭嶼四天三夜，請給出一個在地人才知道的熱血秘境建議，50字內，繁體中文。");
            } catch (e) { text.innerText = "AI 暫時休息中，請稍後再試！"; }
            finally { loader.classList.add('hidden'); }
        }

        async function getBudgetAI() {
            const budget = document.getElementById('budget-input').value;
            const box = document.getElementById('budget-ai-box');
            const text = document.getElementById('bud-ai-text');
            const loader = document.getElementById('bud-loader');
            if(!budget) return;
            box.classList.remove('hidden');
            loader.classList.remove('hidden');
            text.innerText = "計算中...";
            try {
                text.innerText = await fetchGemini(`我的預算是 ${budget} 元，要去蘭嶼玩四天，請評價是否足夠並給一個省錢策略。50字內，繁體中文。`);
            } catch (e) { text.innerText = "連線失敗。"; }
            finally { loader.classList.add('hidden'); }
        }

        async function askGuideAI() {
            const input = document.getElementById('guide-input').value;
            const box = document.getElementById('guide-box');
            const text = document.getElementById('guide-text');
            const loader = document.getElementById('guide-loader');
            if(!input) return;
            box.classList.remove('hidden');
            loader.classList.remove('hidden');
            text.innerText = "正在詢問部落耆老...";
            try {
                text.innerText = await fetchGemini(input, "你是一位專業的蘭嶼導覽與文化專家，請用繁體中文尊重且親切地回答問題，如果是達悟語請附上發音參考。");
            } catch (e) { text.innerText = "嚮導出門採飛魚了，請稍後再問。"; }
            finally { loader.classList.add('hidden'); }
        }

        window.onload = () => {
            const ctx = document.getElementById('budgetChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['交通', '住宿', '飲食', '體驗'],
                    datasets: [{
                        data: [3800, 2700, 2000, 1500],
                        backgroundColor: ['#0f766e', '#0ea5e9', '#f59e0b', '#ea580c']
                    }]
                },
                options: { maintainAspectRatio: false, plugins: { legend: { position: 'bottom' } } }
            });
        };
    </script>
</body>
</html>
