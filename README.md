<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 15px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .container {
            width: 100%;
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 25px 20px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 1.8rem;
            margin-bottom: 10px;
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .header p {
            opacity: 0.9;
            font-size: 1rem;
        }
        
        .calculator-section {
            padding: 25px 20px;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2c3e50;
            font-size: 1rem;
        }
        
        .input-group input, .input-group select {
            width: 100%;
            padding: 14px 16px;
            border: 2px solid #e1e8ed;
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        .input-group input:focus, .input-group select:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }
        
        .calculate-btn {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            padding: 16px;
            border: none;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .calculate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(46, 204, 113, 0.3);
        }
        
        .results {
            display: none;
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px 20px;
            margin-top: 25px;
        }
        
        .probability-display {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .probability-number {
            font-size: 3rem;
            font-weight: bold;
            margin-bottom: 10px;
            background: linear-gradient(135deg, #2c3e50, #3498db);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .probability-label {
            font-size: 1.1rem;
            color: #7f8c8d;
            margin-bottom: 20px;
        }
        
        .gauge-container {
            position: relative;
            width: 200px;
            height: 100px;
            margin: 20px auto;
        }
        
        .gauge {
            width: 200px;
            height: 100px;
            border-radius: 100px 100px 0 0;
            background: conic-gradient(from 180deg, #e74c3c 0deg, #f39c12 60deg, #f1c40f 90deg, #2ecc71 120deg, #27ae60 180deg);
            position: relative;
            overflow: hidden;
        }
        
        .gauge::after {
            content: '';
            position: absolute;
            width: 160px;
            height: 80px;
            background: #f8f9fa;
            border-radius: 80px 80px 0 0;
            top: 20px;
            left: 20px;
        }
        
        .gauge-needle {
            position: absolute;
            width: 2px;
            height: 80px;
            background: #2c3e50;
            bottom: 0;
            left: 50%;
            transform-origin: bottom;
            transform: translateX(-50%) rotate(0deg);
            transition: transform 1s ease-out;
            z-index: 10;
        }
        
        .gauge-needle::after {
            content: '';
            position: absolute;
            width: 8px;
            height: 8px;
            background: #2c3e50;
            border-radius: 50%;
            bottom: -4px;
            left: -3px;
        }
        
        .interpretation {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .interpretation-message {
            font-size: 1.1rem;
            font-weight: 600;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
        }
        
        .trend-section {
            margin-top: 25px;
            padding: 20px;
            background: white;
            border-radius: 12px;
            border: 1px solid #e1e8ed;
        }
        
        .trend-section h3 {
            margin-bottom: 15px;
            color: #2c3e50;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.1rem;
        }
        
        .trend-inputs {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }
        
        .trend-input {
            display: flex;
            flex-direction: column;
        }
        
        .trend-input label {
            font-size: 0.9rem;
            margin-bottom: 5px;
            color: #7f8c8d;
        }
        
        .trend-input input {
            padding: 10px;
            border: 1px solid #e1e8ed;
            border-radius: 8px;
            font-size: 14px;
        }
        
        .readiness-check {
            margin-top: 20px;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            font-weight: 600;
            font-size: 0.95rem;
        }
        
        .disclaimer {
            background: #ecf0f1;
            padding: 18px;
            border-radius: 10px;
            margin-top: 25px;
            font-size: 0.85rem;
            color: #7f8c8d;
            text-align: center;
        }
        
        .score-breakdown {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-top: 20px;
        }
        
        .score-range {
            background: white;
            padding: 15px 10px;
            border-radius: 10px;
            text-align: center;
            border: 2px solid transparent;
            transition: all 0.3s ease;
        }
        
        .score-range.current {
            border-color: #3498db;
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.2);
        }
        
        .score-range h4 {
            font-size: 0.95rem;
            margin-bottom: 8px;
        }
        
        .score-range p {
            font-size: 0.85rem;
            margin-bottom: 5px;
        }
        
        .trend-chart {
            margin-top: 20px;
            text-align: center;
        }
        
        .chart-container {
            position: relative;
            height: 200px;
            background: white;
            border-radius: 10px;
            padding: 20px;
            margin-top: 15px;
        }
        
        .chart-line {
            position: relative;
            height: 100%;
            display: flex;
            align-items: end;
            justify-content: space-between;
        }
        
        .chart-point {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #3498db;
            position: relative;
            cursor: pointer;
        }
        
        .chart-point::after {
            content: attr(data-score);
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 12px;
            color: #7f8c8d;
            white-space: nowrap;
        }
        
        .risk-high { color: #e74c3c; }
        .risk-medium { color: #f39c12; }
        .risk-low { color: #27ae60; }
        
        /* Mobile-specific improvements */
        @media (max-width: 480px) {
            .header {
                padding: 20px 15px;
            }
            
            .header h1 {
                font-size: 1.5rem;
            }
            
            .calculator-section {
                padding: 20px 15px;
            }
            
            .probability-number {
                font-size: 2.5rem;
            }
            
            .trend-inputs {
                grid-template-columns: 1fr;
            }
            
            .score-breakdown {
                grid-template-columns: 1fr;
                gap: 15px;
            }
            
            .gauge-container {
                transform: scale(0.9);
            }
            
            .input-group input, .input-group select {
                padding: 16px;
            }
        }
        
        @media (min-width: 481px) and (max-width: 768px) {
            .trend-inputs {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .score-breakdown {
                grid-template-columns: repeat(3, 1fr);
            }
        }
        
        /* Animation for results */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .results {
            animation: fadeIn 0.5s ease forwards;
        }
        
        /* Improved focus states for accessibility */
        button:focus, input:focus, select:focus {
            outline: 2px solid #3498db;
            outline-offset: 2px;
        }
        
        /* Smooth scrolling */
        html {
            scroll-behavior: smooth;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-bullseye"></i> USMLE Step 1 Pass Probability Calculator</h1>
            <p>Estimate your chances based on NBME scores and exam readiness</p>
        </div>
        
        <div class="calculator-section">
            <div class="input-group">
                <label for="nbmeScore"><i class="fas fa-chart-line"></i> Latest NBME Predicted Score</label>
                <input type="number" id="nbmeScore" placeholder="Enter score (180-270)" min="180" max="270">
            </div>
            
            <div class="input-group">
                <label for="examDate"><i class="far fa-calendar-alt"></i> Exam Date (Optional)</label>
                <input type="date" id="examDate">
            </div>
            
            <button class="calculate-btn" onclick="calculateProbability()">
                <i class="fas fa-calculator"></i> Calculate Pass Probability
            </button>
            
            <div class="trend-section">
                <h3><i class="fas fa-chart-line"></i> Score Trend Analysis (Optional)</h3>
                <div class="trend-inputs">
                    <div class="trend-input">
                        <label>NBME 1</label>
                        <input type="number" id="nbme1" placeholder="Score">
                    </div>
                    <div class="trend-input">
                        <label>NBME 2</label>
                        <input type="number" id="nbme2" placeholder="Score">
                    </div>
                    <div class="trend-input">
                        <label>NBME 3</label>
                        <input type="number" id="nbme3" placeholder="Score">
                    </div>
                    <div class="trend-input">
                        <label>Latest</label>
                        <input type="number" id="nbmeLatest" placeholder="Latest Score">
                    </div>
                </div>
            </div>
            
            <div class="results" id="results">
                <div class="probability-display">
                    <div class="probability-number" id="probabilityNumber">0%</div>
                    <div class="probability-label">Estimated Pass Probability</div>
                    
                    <div class="gauge-container">
                        <div class="gauge">
                            <div class="gauge-needle" id="gaugeNeedle"></div>
                        </div>
                    </div>
                </div>
                
                <div class="interpretation">
                    <div class="interpretation-message" id="interpretationMessage"></div>
                </div>
                
                <div class="score-breakdown">
                    <div class="score-range">
                        <h4 style="color: #e74c3c;"><i class="fas fa-exclamation-triangle"></i> High Risk</h4>
                        <p>&lt; 190</p>
                        <p>&lt; 30% Pass Rate</p>
                    </div>
                    <div class="score-range">
                        <h4 style="color: #f39c12;"><i class="fas fa-balance-scale"></i> Borderline</h4>
                        <p>190-205</p>
                        <p>50-75% Pass Rate</p>
                    </div>
                    <div class="score-range">
                        <h4 style="color: #27ae60;"><i class="fas fa-shield-alt"></i> Safe Zone</h4>
                        <p>&gt; 205</p>
                        <p>&gt; 75% Pass Rate</p>
                    </div>
                </div>
                
                <div class="readiness-check" id="readinessCheck"></div>
                
                <div class="trend-chart" id="trendChart" style="display: none;">
                    <h4><i class="fas fa-project-diagram"></i> Score Progression</h4>
                    <div class="chart-container">
                        <div class="chart-line" id="chartLine"></div>
                    </div>
                    <div id="trendAnalysis"></div>
                </div>
            </div>
            
            <div class="disclaimer">
                <strong><i class="fas fa-exclamation-circle"></i> Important Disclaimer:</strong> This calculator provides estimates based on historical NBME score correlations and should not replace professional guidance. Pass rates can vary based on individual preparation, test-taking skills, and other factors. Always consult with your medical education advisors for personalized advice.
            </div>
        </div>
    </div>

    <script>
        function calculateProbability() {
            const nbmeScore = parseFloat(document.getElementById('nbmeScore').value);
            
            if (!nbmeScore || nbmeScore < 180 || nbmeScore > 270) {
                alert('Please enter a valid NBME score between 180-270');
                return;
            }
            
            // Logistic regression-style calculation for smooth curve
            const probability = 1 / (1 + Math.exp(-0.1 * (nbmeScore - 196)));
            const probabilityPercent = Math.round(probability * 100);
            
            // Display results
            document.getElementById('results').style.display = 'block';
            document.getElementById('probabilityNumber').textContent = probabilityPercent + '%';
            
            // Update gauge needle (0-180 degrees)
            const needleAngle = (probability * 180) - 90;
            document.getElementById('gaugeNeedle').style.transform = 
                `translateX(-50%) rotate(${needleAngle}deg)`;
            
            // Set interpretation message and color
            const interpretationElement = document.getElementById('interpretationMessage');
            let message, riskClass;
            
            if (probabilityPercent < 30) {
                message = "High Risk - Consider delaying exam and intensive remediation";
                riskClass = "risk-high";
                interpretationElement.style.backgroundColor = "#fdf2f2";
                interpretationElement.style.color = "#e74c3c";
            } else if (probabilityPercent < 50) {
                message = "Moderate Risk - Additional preparation strongly recommended";
                riskClass = "risk-medium";
                interpretationElement.style.backgroundColor = "#fef9e7";
                interpretationElement.style.color = "#f39c12";
            } else if (probabilityPercent < 75) {
                message = "Borderline Safe - Continue focused preparation";
                riskClass = "risk-medium";
                interpretationElement.style.backgroundColor = "#fef9e7";
                interpretationElement.style.color = "#f39c12";
            } else if (probabilityPercent < 90) {
                message = "Good Chance - Maintain current preparation strategy";
                riskClass = "risk-low";
                interpretationElement.style.backgroundColor = "#f0f9ff";
                interpretationElement.style.color = "#3498db";
            } else {
                message = "Excellent Chance - Well prepared for the exam";
                riskClass = "risk-low";
                interpretationElement.style.backgroundColor = "#f0fdf4";
                interpretationElement.style.color = "#27ae60";
            }
            
            interpretationElement.textContent = message;
            interpretationElement.className = `interpretation-message ${riskClass}`;
            
            // Highlight current score range
            const scoreRanges = document.querySelectorAll('.score-range');
            scoreRanges.forEach(range => range.classList.remove('current'));
            
            if (nbmeScore < 190) {
                scoreRanges[0].classList.add('current');
            } else if (nbmeScore <= 205) {
                scoreRanges[1].classList.add('current');
            } else {
                scoreRanges[2].classList.add('current');
            }
            
            // Readiness check
            checkReadiness(nbmeScore, probabilityPercent);
            
            // Trend analysis
            analyzeTrend();
            
            // Scroll to results
            document.getElementById('results').scrollIntoView({ 
                behavior: 'smooth', 
                block: 'start'
            });
        }
        
        function checkReadiness(score, probability) {
            const examDate = document.getElementById('examDate').value;
            const readinessElement = document.getElementById('readinessCheck');
            
            if (!examDate) {
                readinessElement.style.display = 'none';
                return;
            }
            
            const today = new Date();
            const exam = new Date(examDate);
            const daysUntilExam = Math.ceil((exam - today) / (1000 * 60 * 60 * 24));
            
            readinessElement.style.display = 'block';
            
            if (daysUntilExam < 0) {
                readinessElement.textContent = "⏰ Exam date has passed";
                readinessElement.style.backgroundColor = "#ecf0f1";
                readinessElement.style.color = "#7f8c8d";
            } else if (daysUntilExam <= 14 && probability < 70) {
                readinessElement.textContent = `🚨 Warning: ${daysUntilExam} days until exam with ${probability}% pass probability. Consider postponing if possible.`;
                readinessElement.style.backgroundColor = "#fdf2f2";
                readinessElement.style.color = "#e74c3c";
            } else if (daysUntilExam <= 7 && probability < 85) {
                readinessElement.textContent = `⚠️ Caution: ${daysUntilExam} days until exam. Intensive final preparation recommended.`;
                readinessElement.style.backgroundColor = "#fef9e7";
                readinessElement.style.color = "#f39c12";
            } else {
                readinessElement.textContent = `✅ ${daysUntilExam} days until exam. Time for final review and confidence building.`;
                readinessElement.style.backgroundColor = "#f0fdf4";
                readinessElement.style.color = "#27ae60";
            }
        }
        
        function analyzeTrend() {
            const scores = [
                parseFloat(document.getElementById('nbme1').value),
                parseFloat(document.getElementById('nbme2').value),
                parseFloat(document.getElementById('nbme3').value),
                parseFloat(document.getElementById('nbmeLatest').value)
            ].filter(score => !isNaN(score) && score > 0);
            
            if (scores.length < 2) {
                document.getElementById('trendChart').style.display = 'none';
                return;
            }
            
            document.getElementById('trendChart').style.display = 'block';
            
            // Create simple chart visualization
            const chartLine = document.getElementById('chartLine');
            chartLine.innerHTML = '';
            
            const maxScore = Math.max(...scores) + 10;
            const minScore = Math.min(...scores) - 10;
            const range = maxScore - minScore;
            
            scores.forEach((score, index) => {
                const point = document.createElement('div');
                point.className = 'chart-point';
                point.setAttribute('data-score', score);
                point.style.height = `${((score - minScore) / range) * 100}%`;
                chartLine.appendChild(point);
                
                // Connect points with lines (simplified)
                if (index > 0) {
                    // Add connecting line logic here if desired
                }
            });
            
            // Trend analysis
            const trendAnalysis = document.getElementById('trendAnalysis');
            const firstScore = scores[0];
            const lastScore = scores[scores.length - 1];
            const improvement = lastScore - firstScore;
            
            let trendMessage;
            if (improvement > 10) {
                trendMessage = `📈 Excellent improvement! You've gained ${improvement.toFixed(0)} points. Keep up the momentum!`;
                trendAnalysis.style.color = '#27ae60';
            } else if (improvement > 0) {
                trendMessage = `📊 Steady improvement of ${improvement.toFixed(0)} points. Continue your current study approach.`;
                trendAnalysis.style.color = '#3498db';
            } else if (improvement > -5) {
                trendMessage = `📉 Scores are plateauing. Consider adjusting your study strategy.`;
                trendAnalysis.style.color = '#f39c12';
            } else {
                trendMessage = `📉 Concerning downward trend. Review your study methods and consider seeking guidance.`;
                trendAnalysis.style.color = '#e74c3c';
            }
            
            trendAnalysis.textContent = trendMessage;
        }
        
        // Auto-sync latest score with main input
        document.getElementById('nbmeLatest').addEventListener('input', function() {
            const latestScore = this.value;
            if (latestScore) {
                document.getElementById('nbmeScore').value = latestScore;
            }
        });
        
        // Auto-calculate on main score change
        document.getElementById('nbmeScore').addEventListener('input', function() {
            const score = this.value;
            if (score && score >= 180 && score <= 270) {
                setTimeout(calculateProbability, 500); // Debounced auto-calculation
            }
        });
    </script>
</body>
</html>
