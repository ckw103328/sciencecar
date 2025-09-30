<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>賽車大比拼</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Comic Sans MS', 'Arial Rounded MT Bold', sans-serif;
            background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #333;
        }
        
        .container {
            max-width: 700px;
            width: 100%;
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 25px;
            padding: 30px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            border: 8px solid #ffcc00;
            position: relative;
            overflow: hidden;
        }
        
        .container::before {
            content: "";
            position: absolute;
            top: -10px;
            left: -10px;
            right: -10px;
            bottom: -10px;
            background: linear-gradient(45deg, #ff9a9e, #fad0c4, #fad0c4, #a1c4fd);
            z-index: -1;
            border-radius: 30px;
        }
        
        h1 {
            text-align: center;
            color: #ff6b6b;
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 3px 3px 0 #ffcc00;
            letter-spacing: 1px;
        }
        
        .subtitle {
            text-align: center;
            color: #4d96ff;
            font-size: 1.2rem;
            margin-bottom: 30px;
            font-weight: bold;
        }
        
        .car-display {
            text-align: center;
            margin: 20px 0;
        }
        
        .car-icon {
            font-size: 5rem;
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .slopes-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            gap: 20px;
            margin: 25px 0;
        }
        
        .slope-card {
            background: linear-gradient(to bottom, #e6f7ff, #ffffff);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border: 4px solid #4d96ff;
            transition: transform 0.3s;
            flex: 1;
            min-width: 180px;
        }
        
        .slope-card:hover {
            transform: translateY(-5px);
        }
        
        .slope-header {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .slope-icon {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .slope-title {
            font-size: 1.4rem;
            color: #ff6b6b;
            font-weight: bold;
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 10px;
        }
        
        label {
            font-weight: bold;
            color: #4d96ff;
            margin-bottom: 8px;
            font-size: 1rem;
            text-align: center;
        }
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: 3px solid #ffcc00;
            border-radius: 15px;
            font-size: 1.2rem;
            text-align: center;
            font-family: 'Comic Sans MS', sans-serif;
            transition: all 0.3s;
        }
        
        input:focus {
            outline: none;
            border-color: #ff6b6b;
            box-shadow: 0 0 0 3px rgba(255, 107, 107, 0.3);
        }
        
        .button-container {
            text-align: center;
            margin: 30px 0 20px;
        }
        
        button {
            background: linear-gradient(to bottom, #ff6b6b, #ff5252);
            color: white;
            border: none;
            border-radius: 50px;
            padding: 15px 40px;
            font-size: 1.4rem;
            cursor: pointer;
            font-weight: bold;
            box-shadow: 0 5px 0 #ff4040;
            transition: all 0.2s;
            font-family: 'Comic Sans MS', sans-serif;
        }
        
        button:hover {
            transform: translateY(3px);
            box-shadow: 0 2px 0 #ff4040;
        }
        
        button:active {
            transform: translateY(5px);
            box-shadow: none;
        }
        
        .results {
            background: linear-gradient(to bottom, #e6f7ff, #ffffff);
            border-radius: 20px;
            padding: 25px;
            margin-top: 25px;
            border: 4px dashed #4d96ff;
            display: none;
        }
        
        .result-title {
            text-align: center;
            color: #ff6b6b;
            font-size: 1.8rem;
            margin-bottom: 20px;
            text-shadow: 1px 1px 0 #ffcc00;
        }
        
        .ranking-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .rank-card {
            flex: 1;
            min-width: 150px;
            background: white;
            border-radius: 15px;
            padding: 15px;
            text-align: center;
            border: 3px solid #ffcc00;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }
        
        .rank-1 {
            border-color: gold;
            background: #fff9c4;
            order: 1;
        }
        
        .rank-2 {
            border-color: silver;
            background: #f5f5f5;
            order: 2;
        }
        
        .rank-3 {
            border-color: #cd7f32;
            background: #ffe0b2;
            order: 3;
        }
        
        .rank-medal {
            font-size: 2rem;
            margin-bottom: 10px;
        }
        
        .rank-title {
            font-weight: bold;
            color: #4d96ff;
            margin-bottom: 5px;
        }
        
        .rank-distance {
            font-size: 1.5rem;
            color: #ff6b6b;
            font-weight: bold;
        }
        
        .summary {
            background-color: #fff9c4;
            border-radius: 15px;
            padding: 15px;
            margin-top: 20px;
            border: 3px solid #ffcc00;
            text-align: center;
        }
        
        .summary-title {
            font-weight: bold;
            color: #ff6b6b;
            font-size: 1.3rem;
            margin-bottom: 10px;
        }
        
        .summary-text {
            font-size: 1.1rem;
            color: #4d96ff;
        }
        
        .encouragement {
            text-align: center;
            font-size: 1.5rem;
            color: #ff6b6b;
            margin-top: 20px;
            font-weight: bold;
            padding: 15px;
            background-color: #fff9c4;
            border-radius: 15px;
            border: 3px solid #ffcc00;
        }
        
        .cloud {
            position: absolute;
            background: white;
            border-radius: 50%;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            z-index: -1;
        }
        
        .cloud-1 {
            width: 100px;
            height: 40px;
            top: 10%;
            left: 5%;
            opacity: 0.7;
        }
        
        .cloud-2 {
            width: 150px;
            height: 60px;
            bottom: 10%;
            right: 5%;
            opacity: 0.8;
        }
        
        .cloud-3 {
            width: 80px;
            height: 30px;
            top: 20%;
            right: 10%;
            opacity: 0.6;
        }
        
        @media (max-width: 768px) {
            .slopes-container {
                flex-direction: column;
            }
            
            .ranking-container {
                flex-direction: column;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .car-icon {
                font-size: 4rem;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            .slope-card {
                padding: 15px;
            }
            
            button {
                padding: 12px 30px;
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="cloud cloud-1"></div>
    <div class="cloud cloud-2"></div>
    <div class="cloud cloud-3"></div>
    
    <div class="container">
        <h1>賽車大比拼 🏎️</h1>
        <p class="subtitle">記錄你的賽車在不同賽道上滑行的距離，看看哪個賽道最厲害！</p>
        
        <div class="car-display">
            <div class="car-icon">🚗</div>
        </div>
        
        <div class="slopes-container">
            <div class="slope-card">
                <div class="slope-header">
                    <div class="slope-icon">🏁 🟥</div>
                    <div class="slope-title">紅色賽道</div>
                </div>
                <div class="input-group">
                    <label for="slope1">距離 (inch):</label>
                    <input type="number" id="slope1" min="0" placeholder="輸入距離">
                </div>
            </div>
            
            <div class="slope-card">
                <div class="slope-header">
                    <div class="slope-icon">🏁 🟩</div>
                    <div class="slope-title">綠色賽道 2</div>
                </div>
                <div class="input-group">
                    <label for="slope2">距離 (inch):</label>
                    <input type="number" id="slope2" min="0" placeholder="輸入距離">
                </div>
            </div>
            
            <div class="slope-card">
                <div class="slope-header">
                    <div class="slope-icon">🏁 ⬛ </div>
                    <div class="slope-title">黑色賽道 3</div>
                </div>
                <div class="input-group">
                    <label for="slope3">距離 (inch):</label>
                    <input type="number" id="slope3" min="0" placeholder="輸入距離">
                </div>
            </div>
        </div>
        
        <div class="button-container">
            <button id="calculate-btn">計算結果！</button>
        </div>
        
        <div class="results" id="results">
            <div class="result-title">賽道排名 🏆</div>
            
            <div class="ranking-container" id="ranking-container">
                <!-- 排名卡片將由JavaScript動態生成 -->
            </div>
            
            <div class="summary" id="summary">
                <!-- 摘要將由JavaScript動態生成 -->
            </div>
            
            <div class="encouragement" id="encouragement"></div>
        </div>
    </div>

    <script>
        document.getElementById('calculate-btn').addEventListener('click', function() {
            // 獲取輸入值
            const slope1 = parseFloat(document.getElementById('slope1').value) || 0;
            const slope2 = parseFloat(document.getElementById('slope2').value) || 0;
            const slope3 = parseFloat(document.getElementById('slope3').value) || 0;
            
            // 創建斜坡數據數組
            const slopes = [
                { name: "紅色賽道", distance: slope1, icon: "📐" },
                { name: "綠色賽道", distance: slope2, icon: "📐" },
                { name: "黑色賽道", distance: slope3, icon: "📐" }
            ];
            
            // 按距離排序（從大到小）
            slopes.sort((a, b) => b.distance - a.distance);
            
            // 更新排名顯示
            const rankingContainer = document.getElementById('ranking-container');
            rankingContainer.innerHTML = '';
            
            slopes.forEach((slope, index) => {
                const rankCard = document.createElement('div');
                rankCard.className = `rank-card rank-${index+1}`;
                
                let medal = "";
                if (index === 0) medal = "🥇";
                else if (index === 1) medal = "🥈";
                else if (index === 2) medal = "🥉";
                
                rankCard.innerHTML = `
                    <div class="rank-medal">${medal}</div>
                    <div class="rank-title">${slope.name}</div>
                    <div class="rank-distance">${slope.distance.toFixed(1)} inch</div>
                `;
                
                rankingContainer.appendChild(rankCard);
            });
            
            // 更新摘要
            const summary = document.getElementById('summary');
            if (slopes[0].distance > 0) {
                summary.innerHTML = `
                    <div class="summary-title">結果摘要</div>
                    <div class="summary-text">
                        <strong>${slopes[0].name}</strong> 讓車子走得最遠！<br>
                        <strong>${slopes[2].name}</strong> 讓車子走得最近。
                    </div>
                `;
            } else {
                summary.innerHTML = `
                    <div class="summary-title">結果摘要</div>
                    <div class="summary-text">請輸入距離來開始記錄！</div>
                `;
            }
            
            // 顯示鼓勵訊息
            const encouragement = document.getElementById('encouragement');
            if (slopes[0].distance === 0) {
                encouragement.textContent = "請輸入距離來開始記錄！";
            } else if (slopes[0].distance < 50) {
                encouragement.textContent = "做得好！繼續嘗試讓車子滑得更遠！🚗";
            } else if (slopes[0].distance < 100) {
                encouragement.textContent = "太棒了！你的賽車滑得很遠呢！🎉";
            } else {
                encouragement.textContent = "哇！你的賽車是超級冠軍！🏆";
            }
            
            // 顯示結果區域
            document.getElementById('results').style.display = 'block';
            
            // 添加一點動畫效果
            const rankCards = document.querySelectorAll('.rank-card');
            rankCards.forEach((card, index) => {
                card.style.opacity = '0';
                card.style.transform = 'translateY(20px)';
                
                setTimeout(() => {
                    card.style.transition = 'all 0.5s ease';
                    card.style.opacity = '1';
                    card.style.transform = 'translateY(0)';
                }, index * 200);
            });
        });
    </script>
</body>
</html>
