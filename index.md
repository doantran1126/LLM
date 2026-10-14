# 1. Tạo file index.html từ mã nguồn HTML
html_code = """
<!DOCTYPE html>
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AUREL - Financial Intelligence Platform</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkbg: '#0b0f19',
                        cardbg: '#1e293b',
                        bordercolor: '#334155',
                        primary: '#6366f1',
                        accent: '#38bdf8'
                    }
                }
            }
        }
    </script>
    <style>
        body { background-color: #0b0f19; color: #f8fafc; font-family: 'Inter', system-ui, sans-serif; }
        .glass-card { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 1rem; }
    </style>
</head>
<body class="min-h-screen flex flex-col">
    <nav class="border-b border-slate-800 bg-slate-900/80 backdrop-blur-md sticky top-0 z-50 px-6 py-4 flex justify-between items-center">
        <div class="flex items-center space-x-3">
            <div class="w-10 h-10 rounded-xl bg-indigo-600 flex items-center justify-center font-bold text-xl text-white shadow-lg shadow-indigo-500/30">A</div>
            <div>
                <span class="font-bold text-lg tracking-wide text-white">AUREL</span>
                <span class="text-xs text-indigo-400 block -mt-1">Financial Intelligence</span>
            </div>
        </div>
        <div class="flex items-center space-x-4">
            <span class="px-3 py-1 rounded-full text-xs font-semibold bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                <i class="fa-solid fa-circle text-[8px] mr-1.5 animate-pulse"></i> AI Agent Active
            </span>
        </div>
    </nav>

    <main class="flex-1 max-w-7xl w-full mx-auto p-6 grid grid-cols-1 lg:grid-cols-12 gap-6">
        <div class="lg:col-span-8 space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="glass-card p-5">
                    <p class="text-xs uppercase tracking-wider text-slate-400 font-semibold mb-2">Total Portfolio Value</p>
                    <h3 class="text-2xl font-bold text-white">$124,500.00</h3>
                    <p class="text-xs text-emerald-400 mt-2 font-medium"><i class="fa-solid fa-arrow-trend-up"></i> +12.4% vs last month</p>
                </div>
                <div class="glass-card p-5">
                    <p class="text-xs uppercase tracking-wider text-slate-400 font-semibold mb-2">AI Health & Risk Score</p>
                    <h3 class="text-2xl font-bold text-sky-400">88/100</h3>
                    <p class="text-xs text-slate-400 mt-2">Low Volatility Exposure</p>
                </div>
                <div class="glass-card p-5">
                    <p class="text-xs uppercase tracking-wider text-slate-400 font-semibold mb-2">Monthly Cash Flow</p>
                    <h3 class="text-2xl font-bold text-emerald-400">+$4,250.00</h3>
                    <p class="text-xs text-slate-400 mt-2">Savings Rate: 34%</p>
                </div>
            </div>

            <div class="glass-card p-6">
                <div class="flex justify-between items-center mb-4">
                    <h4 class="font-semibold text-lg text-white">Portfolio Asset Allocation & Forecast</h4>
                </div>
                <div class="h-64">
                    <canvas id="financialChart"></canvas>
                </div>
            </div>
        </div>

        <div class="lg:col-span-4 flex flex-col h-[500px] glass-card overflow-hidden border border-slate-800">
            <div class="p-4 border-b border-slate-800 bg-slate-900/50 flex items-center justify-between">
                <span class="font-semibold text-sm text-white">Financial AI Assistant</span>
                <span class="text-xs text-slate-400">Gemini 3.5 Flash</span>
            </div>
            <div id="chat-box" class="flex-1 p-4 overflow-y-auto space-y-4 text-sm">
                <div class="flex items-start space-x-3">
                    <div class="w-8 h-8 rounded-lg bg-indigo-600/30 border border-indigo-500/40 flex items-center justify-center text-xs font-bold text-indigo-400">AI</div>
                    <div class="bg-slate-800/80 p-3 rounded-2xl rounded-tl-none border border-slate-700/50 text-slate-200">
                        Xin chào! Tôi là trợ lý tài chính AI. Bạn cần hỗ trợ phân tích danh mục hay quản lý rủi ro?
                    </div>
                </div>
            </div>
            <div class="p-4 border-t border-slate-800 bg-slate-900/50">
                <div class="flex items-center space-x-2">
                    <input id="user-input" type="text" placeholder="Hỏi AI..." class="flex-1 bg-slate-800 border border-slate-700 rounded-xl px-4 py-2 text-sm text-white focus:outline-none">
                    <button onclick="sendMessage()" class="bg-indigo-600 hover:bg-indigo-500 text-white p-2 rounded-xl">
                        <i class="fa-solid fa-paper-plane"></i>
                    </button>
                </div>
            </div>
        </div>
    </main>

    <script>
        const ctx = document.getElementById('financialChart').getContext('2d');
        new Chart(ctx, {
            type: 'line',
            data: {
                labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct'],
                datasets: [{
                    label: 'Portfolio Growth ($)',
                    data: [85000, 89000, 92000, 96000, 102000, 108000, 114000, 118000, 121000, 124500],
                    borderColor: '#6366f1',
                    backgroundColor: 'rgba(99, 102, 241, 0.1)',
                    borderWidth: 3,
                    fill: true,
                    tension: 0.4
                }]
            },
            options: { responsive: true, maintainAspectRatio: false }
        });

        function sendMessage() {
            const input = document.getElementById('user-input');
            const chatBox = document.getElementById('chat-box');
            if (!input.value.trim()) return;

            const userMsg = document.createElement('div');
            userMsg.className = 'flex items-start justify-end space-x-3';
            userMsg.innerHTML = `<div class="bg-indigo-600 p-3 rounded-2xl rounded-tr-none text-white">${input.value}</div>`;
            chatBox.appendChild(userMsg);

            const userText = input.value;
            input.value = '';
            chatBox.scrollTop = chatBox.scrollHeight;

            setTimeout(() => {
                const aiMsg = document.createElement('div');
                aiMsg.className = 'flex items-start space-x-3';
                aiMsg.innerHTML = `
                    <div class="w-8 h-8 rounded-lg bg-indigo-600/30 border border-indigo-500/40 flex items-center justify-center text-xs font-bold text-indigo-400">AI</div>
                    <div class="bg-slate-800/80 p-3 rounded-2xl rounded-tl-none border border-slate-700/50 text-slate-200">
                        Đã nhận phản hồi về: "${userText}".
                    </div>
                `;
                chatBox.appendChild(aiMsg);
                chatBox.scrollTop = chatBox.scrollHeight;
            }, 800);
        }
    </script>
</body>
</html>
"""

with open("index.html", "w") as f:
    f.write(html_code)

# 2. Khởi chạy Web Server cục bộ và tạo đường dẫn Live Preview
import portpicker
from google.colab import output

port = portpicker.pick_unused_port()
get_ipython().system_raw(f'python3 -m http.server {port} &')
output.serve_kernel_port_async(port, path='/index.html')
