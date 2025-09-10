<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TON CRASH Game</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Orbitron', monospace;
            background: linear-gradient(135deg, #0a0a0a 0%, #1a2a3a 50%, #0d1f2f 100%);
            color: white;
            overflow-x: hidden;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1600px;
            margin: 0 auto;
            position: relative;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            background: rgba(30, 40, 50, 0.9);
            padding: 20px;
            border-radius: 30px;
            border: 2px solid #00aaff;
            backdrop-filter: blur(10px);
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo img {
            height: 50px;
            width: auto;
        }

        .header-center {
            display: flex;
            align-items: center;
            gap: 20px;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
        }

        .nav-button {
            padding: 15px 30px;
            background: rgba(30, 40, 50, 0.9);
            border: 2px solid #00aaff;
            border-radius: 25px;
            color: white;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .nav-button.active {
            background: linear-gradient(45deg, #00aaff, #66ccff);
            color: #000;
            box-shadow: 0 5px 20px rgba(0, 170, 255, 0.4);
        }

        .nav-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 170, 255, 0.3);
        }

        .balance-container {
            display: flex;
            align-items: center;
            gap: 15px;
            background: rgba(30, 40, 50, 0.9);
            padding: 15px 25px;
            border-radius: 30px;
            border: 2px solid #00aaff;
            position: relative;
            overflow: hidden;
        }

        .balance-container::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(0, 170, 255, 0.1), transparent);
            animation: balanceGlow 3s linear infinite;
        }

        @keyframes balanceGlow {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .balance-logo {
            width: 40px;
            height: 40px;
            background: linear-gradient(45deg, #00aaff, #66ccff);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 900;
            font-size: 1.2rem;
            color: #000;
            position: relative;
            z-index: 2;
        }

        .ton-icon {
            width: 24px;
            height: 24px;
        }

        .balance-amount {
            font-size: 1.5rem;
            font-weight: 700;
            position: relative;
            z-index: 2;
            display: flex;
            align-items: center;
            gap: 8px;
            color: white;
        }

        .balance-blurred {
            filter: blur(8px);
            user-select: none;
        }

        .login-overlay {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
        }

        .login-btn {
            background: linear-gradient(45deg, #00dd00, #00ff00);
            color: #000;
            border: none;
            padding: 12px 25px;
            border-radius: 20px;
            font-family: 'Orbitron', monospace;
            font-weight: 900;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(0, 255, 0, 0.3);
            transition: all 0.3s ease;
        }

        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0, 255, 0, 0.5);
        }

        .balance-buttons {
            display: flex;
            gap: 10px;
            margin-top: 10px;
            position: relative;
            z-index: 2;
        }

        .balance-button {
            background: rgba(100, 100, 100, 0.8);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 15px;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .balance-button:hover {
            background: rgba(120, 120, 120, 0.9);
            transform: translateY(-1px);
        }

        .balance-button.withdraw {
            background: rgba(255, 100, 100, 0.8);
            color: white;
            cursor: pointer;
        }

        .balance-button.withdraw:hover {
            background: rgba(255, 120, 120, 0.9);
            transform: translateY(-1px);
        }

        .content-slider {
            position: relative;
            overflow: hidden;
            width: 100%;
        }

        .slider-container {
            display: flex;
            transition: transform 0.5s ease-in-out;
            width: 200%;
        }

        .slide {
            width: 50%;
            flex-shrink: 0;
        }

        .main-content {
            display: grid;
            grid-template-columns: 300px 1fr 350px;
            gap: 30px;
            height: 600px;
        }

        .bonus-content {
            padding: 20px;
            background: rgba(30, 40, 50, 0.9);
            border-radius: 30px;
            border: 2px solid #00aaff;
            margin: 0 auto;
            max-width: 800px;
        }

        .bonus-title {
            text-align: center;
            font-size: 2.5rem;
            font-weight: 900;
            color: white;
            margin-bottom: 30px;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
        }

        .bonus-stages {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 20px;
            margin-bottom: 40px;
        }

        .bonus-stage {
            background: rgba(0, 0, 0, 0.5);
            border: 2px solid rgba(100, 100, 100, 0.3);
            border-radius: 25px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s ease;
            opacity: 0.4;
            position: relative;
            overflow: hidden;
        }

        .bonus-stage.active {
            background: linear-gradient(45deg, rgba(0, 170, 255, 0.2), rgba(0, 170, 255, 0.1));
            border-color: #00aaff;
            opacity: 1;
            box-shadow: 0 0 30px rgba(0, 170, 255, 0.3);
        }

        .bonus-stage.completed {
            background: linear-gradient(45deg, rgba(0, 255, 0, 0.2), rgba(0, 255, 0, 0.1));
            border-color: #00ff00;
            opacity: 1;
        }

        .bonus-stage::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 215, 0, 0.1), transparent);
            animation: bonusGlow 4s linear infinite;
            opacity: 0;
        }

        .bonus-stage.active::before {
            opacity: 1;
        }

        @keyframes bonusGlow {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .bonus-stage-number {
            font-size: 1.5rem;
            font-weight: 900;
            color: white;
            margin-bottom: 10px;
            position: relative;
            z-index: 2;
        }

        .bonus-stage.active .bonus-stage-number {
            color: #ffaa00;
        }

        .bonus-stage.completed .bonus-stage-number {
            color: #00ff00;
        }

        .bonus-percentage {
            font-size: 2rem;
            font-weight: 900;
            margin-bottom: 10px;
            position: relative;
            z-index: 2;
            color: white;
        }

        .bonus-stage.active .bonus-percentage {
            color: #ffaa00;
            text-shadow: 0 0 20px rgba(255, 170, 0, 0.8);
        }

        .bonus-stage.completed .bonus-percentage {
            color: #00ff00;
        }

        .bonus-description {
            font-size: 0.9rem;
            opacity: 0.8;
            position: relative;
            z-index: 2;
            color: white;
        }

        .bonus-info {
            background: rgba(0, 0, 0, 0.7);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 30px;
        }

        .bonus-progress {
            text-align: center;
            margin-bottom: 20px;
        }

        .bonus-progress-text {
            font-size: 1.2rem;
            color: white;
            margin-bottom: 15px;
        }

        .bonus-progress-bar {
            width: 100%;
            height: 10px;
            background: rgba(100, 100, 100, 0.3);
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 15px;
        }

        .bonus-progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #00aaff, #ffaa00);
            border-radius: 10px;
            transition: width 0.3s ease;
        }

        .bonus-stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            text-align: center;
        }

        .bonus-stat {
            background: rgba(0, 170, 255, 0.1);
            padding: 15px;
            border-radius: 15px;
            border: 1px solid rgba(0, 170, 255, 0.3);
        }

        .bonus-stat-value {
            font-size: 1.5rem;
            font-weight: 900;
            color: white;
        }

        .bonus-stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
            margin-top: 5px;
            color: white;
        }

        .online-panel {
            background: rgba(30, 40, 50, 0.9);
            border-radius: 25px;
            border: 2px solid #00aaff;
            padding: 15px;
            backdrop-filter: blur(10px);
            width: 150px;
            height: 80px;
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .online-indicator {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .online-dot {
            width: 12px;
            height: 12px;
            background: #00ff00;
            border-radius: 50%;
            animation: blink 1.5s infinite;
        }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0.3; }
        }

        .online-text {
            font-size: 0.8rem;
            color: white;
            font-weight: 700;
        }

        .online-count {
            font-size: 1.2rem;
            color: white;
            font-weight: 900;
        }

        .players-panel {
            background: rgba(30, 40, 50, 0.9);
            border-radius: 25px;
            border: 2px solid #00aaff;
            padding: 20px;
            backdrop-filter: blur(10px);
        }

        .players-title {
            font-weight: 700;
            margin-bottom: 20px;
            color: white;
            text-align: center;
            font-size: 1.2rem;
        }

        .player-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px;
            margin-bottom: 10px;
            background: rgba(0, 170, 255, 0.1);
            border-radius: 20px;
            border: 1px solid rgba(0, 170, 255, 0.3);
        }

        .player-avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            border: 2px solid #00aaff;
        }

        .player-info {
            flex: 1;
        }

        .player-name {
            font-size: 0.9rem;
            font-weight: 700;
            color: white;
        }

        .player-bet {
            font-size: 0.8rem;
            color: white;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .game-area {
            position: relative;
        }

        .game-canvas {
            background: rgba(30, 40, 50, 0.9);
            border-radius: 35px;
            border: 3px solid #00aaff;
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 170, 255, 0.1) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 170, 255, 0.1) 1px, transparent 1px);
            background-size: 20px 20px;
        }

        .game-canvas::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                radial-gradient(circle at 20% 80%, rgba(0, 170, 255, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(102, 204, 255, 0.05) 0%, transparent 50%);
            animation: backgroundPulse 4s ease-in-out infinite alternate;
        }

        .game-canvas.heartbeat::before {
            animation: heartbeatPulse 0.8s ease-in-out;
        }

        @keyframes backgroundPulse {
            0% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        @keyframes heartbeatPulse {
            0% { 
                opacity: 0.5; 
                transform: scale(1);
            }
            25% { 
                opacity: 0.8; 
                transform: scale(1.02);
            }
            50% { 
                opacity: 1; 
                transform: scale(1.05);
            }
            75% { 
                opacity: 0.8; 
                transform: scale(1.02);
            }
            100% { 
                opacity: 0.5; 
                transform: scale(1);
            }
        }

        .multiplier-display {
            position: absolute;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 4rem;
            font-weight: 900;
            color: white;
            text-shadow: 0 0 30px white;
            z-index: 10;
            transition: all 0.1s ease;
        }

        .multiplier-display.red {
            color: #ff4444;
            text-shadow: 0 0 30px #ff4444;
        }

        .win-display {
            position: absolute;
            top: 120px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 2.5rem;
            font-weight: 900;
            color: #ffaa00;
            text-shadow: 0 0 20px #ffaa00;
            z-index: 11;
            opacity: 0;
            transition: all 0.3s ease;
        }

        .win-display.show {
            opacity: 1;
            animation: winPulse 2s ease-in-out;
        }

        @keyframes winPulse {
            0% { transform: translateX(-50%) scale(0.8); opacity: 0; }
            20% { transform: translateX(-50%) scale(1.2); opacity: 1; }
            80% { transform: translateX(-50%) scale(1); opacity: 1; }
            100% { transform: translateX(-50%) scale(1); opacity: 0; }
        }

        .game-action-button {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            padding: 18px 40px;
            border: none;
            border-radius: 25px;
            font-family: 'Orbitron', monospace;
            font-size: 1.3rem;
            font-weight: 900;
            cursor: pointer;
            transition: all 0.3s ease;
            z-index: 15;
        }

        .game-action-button.bet {
            background: linear-gradient(45deg, #007acc, #0099ff);
            color: white;
            box-shadow: 0 5px 15px rgba(0, 153, 255, 0.4);
        }

        .game-action-button.cashout {
            background: linear-gradient(45deg, #00aaff, #00ddff);
            color: white;
            box-shadow: 0 5px 15px rgba(0, 170, 255, 0.4);
        }

        .game-action-button.cancel {
            background: linear-gradient(45deg, #ff4444, #ff6666);
            color: white;
            box-shadow: 0 5px 15px rgba(255, 68, 68, 0.4);
        }

        .game-action-button.login {
            background: linear-gradient(45deg, #00dd00, #00ff00);
            color: #000;
            box-shadow: 0 5px 15px rgba(0, 255, 0, 0.4);
        }

        .game-action-button:hover {
            transform: translateX(-50%) translateY(-3px);
        }

        .trading-chart {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 5;
        }

        .chart-line {
            stroke: #00aaff;
            stroke-width: 4;
            fill: none;
            filter: drop-shadow(0 0 10px #00aaff);
            transition: stroke 0.3s ease;
        }

        .chart-line.crashed {
            stroke: #ff4444;
            filter: drop-shadow(0 0 10px #ff4444);
        }

        .chart-area {
            fill: url(#gradient);
            opacity: 0.3;
        }

        .game-gif {
            position: absolute;
            width: 120px;
            height: 120px;
            z-index: 8;
            opacity: 0;
            transition: opacity 0.3s ease;
            pointer-events: none;
            border-radius: 15px;
        }

        .game-gif.show {
            opacity: 1;
        }

        .countdown-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 20;
            border-radius: 35px;
        }

        .countdown-number {
            font-size: 8rem;
            font-weight: 900;
            color: #00aaff;
            text-shadow: 0 0 50px #00aaff;
            animation: heartbeat 1s ease-in-out;
        }

        @keyframes heartbeat {
            0% { transform: scale(0.8); opacity: 0.5; }
            50% { transform: scale(1.2); opacity: 1; }
            100% { transform: scale(1); opacity: 1; }
        }

        .game-crashed {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 3rem;
            color: #ff0044;
            font-weight: 900;
            text-shadow: 0 0 30px #ff0044;
            z-index: 15;
            animation: crashPulse 0.5s ease-in-out;
        }

        @keyframes crashPulse {
            0% { transform: translate(-50%, -50%) scale(0); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
            100% { transform: translate(-50%, -50%) scale(1); }
        }

        .betting-panel {
            background: rgba(30, 40, 50, 0.9);
            border-radius: 25px;
            border: 2px solid #00aaff;
            padding: 30px;
            backdrop-filter: blur(10px);
        }

        .game-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: rgba(30, 40, 50, 0.9);
            padding: 20px;
            border-radius: 20px;
            border: 2px solid #00aaff;
            text-align: center;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 900;
            color: white;
        }

        .stat-label {
            margin-top: 5px;
            font-size: 0.9rem;
            color: white;
            opacity: 0.8;
        }

        .history-panel {
            background: rgba(30, 40, 50, 0.9);
            border-radius: 20px;
            border: 2px solid #00aaff;
            padding: 20px;
        }

        .history-title {
            font-weight: 700;
            margin-bottom: 15px;
            color: white;
        }

        .history-list {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .history-item {
            padding: 8px 15px;
            border-radius: 25px;
            font-weight: 700;
            font-size: 0.9rem;
        }

        .history-item.win {
            background: rgba(0, 170, 255, 0.3);
            color: white;
        }

        .history-item.lose {
            background: rgba(255, 68, 68, 0.3);
            color: white;
        }

        .game-history-mini {
            position: absolute;
            top: 20px;
            right: 20px;
            display: flex;
            gap: 10px;
            z-index: 15;
        }

        .mini-result {
            width: 60px;
            height: 40px;
            border-radius: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 900;
            font-size: 0.9rem;
            border: 2px solid;
            animation: slideIn 0.5s ease-out;
        }

        .mini-result.red {
            background: rgba(255, 68, 68, 0.3);
            color: #ff4444;
            border-color: #ff4444;
        }

        .mini-result.orange {
            background: rgba(255, 165, 0, 0.3);
            color: #ffa500;
            border-color: #ffa500;
        }

        .mini-result.white {
            background: rgba(255, 255, 255, 0.3);
            color: #ffffff;
            border-color: #ffffff;
        }

        .mini-result.pending {
            background: rgba(102, 204, 255, 0.3);
            color: #66ccff;
            border-color: #66ccff;
            animation: pulse 1s infinite;
        }

        @keyframes slideIn {
            0% { transform: translateX(100px); opacity: 0; }
            100% { transform: translateX(0); opacity: 1; }
        }

        @keyframes pulse {
            0% { opacity: 0.5; }
            50% { opacity: 1; }
            100% { opacity: 0.5; }
        }

        /* Модальные окна */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }

        .modal-overlay.show {
            opacity: 1;
            visibility: visible;
        }

        .modal {
            background: rgba(30, 40, 50, 0.95);
            border: 3px solid #00aaff;
            border-radius: 35px;
            padding: 40px;
            max-width: 500px;
            width: 90%;
            text-align: center;
            backdrop-filter: blur(15px);
            transform: scale(0.8);
            transition: transform 0.3s ease;
        }

        .modal-overlay.show .modal {
            transform: scale(1);
        }

        .modal h2 {
            color: white;
            margin-bottom: 30px;
            font-size: 2rem;
        }

        .modal-input {
            width: 100%;
            padding: 20px;
            background: rgba(0, 0, 0, 0.7);
            border: 2px solid #00aaff;
            border-radius: 20px;
            color: white;
            font-family: 'Orbitron', monospace;
            font-size: 1.5rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 30px;
        }

        .modal-input:focus {
            outline: none;
            box-shadow: 0 0 20px rgba(0, 170, 255, 0.5);
        }

        .modal-buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
        }

        .modal-btn {
            padding: 15px 30px;
            border: none;
            border-radius: 20px;
            font-family: 'Orbitron', monospace;
            font-weight: 900;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .modal-btn.confirm {
            background: linear-gradient(45deg, #00dd00, #00ff00);
            color: #000;
        }

        .modal-btn.cancel {
            background: linear-gradient(45deg, #ff4444, #ff6666);
            color: white;
        }

        .modal-btn:hover {
            transform: translateY(-2px);
        }

        .deposit-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 30px;
        }

        .deposit-btn {
            padding: 20px;
            background: rgba(0, 170, 255, 0.2);
            border: 2px solid #00aaff;
            border-radius: 20px;
            color: white;
            cursor: pointer;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .deposit-btn:hover {
            background: rgba(0, 170, 255, 0.4);
            transform: translateY(-2px);
        }

        .account-modal {
            max-width: 600px;
        }

        .account-info {
            background: rgba(0, 0, 0, 0.5);
            padding: 20px;
            border-radius: 20px;
            margin-bottom: 30px;
        }

        .account-balance {
            font-size: 2.5rem;
            color: white;
            font-weight: 900;
            margin-bottom: 20px;
        }

        .account-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }

        .last-bets {
            text-align: left;
        }

        .last-bets h3 {
            color: white;
            margin-bottom: 15px;
        }

        .bet-item {
            background: rgba(0, 170, 255, 0.1);
            padding: 12px;
            border-radius: 15px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: white;
        }

        .bet-result.win {
            color: #00ff00;
        }

        .bet-result.lose {
            color: #ff4444;
        }

        /* Модальное окно ставки */
        .bet-modal {
            background: rgba(30, 40, 50, 0.98);
            border: 3px solid #00aaff;
            border-radius: 35px;
            padding: 40px;
            max-width: 400px;
            width: 90%;
            text-align: center;
            backdrop-filter: blur(20px);
            transform: scale(0.8);
            transition: transform 0.3s ease;
        }

        .bet-modal-overlay.show .bet-modal {
            transform: scale(1);
        }

        .bet-amount-input {
            width: 100%;
            padding: 20px;
            background: rgba(0, 0, 0, 0.7);
            border: 2px solid #00aaff;
            border-radius: 20px;
            color: white;
            font-family: 'Orbitron', monospace;
            font-size: 1.8rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 20px;
        }

        .bet-amount-input:focus {
            outline: none;
            box-shadow: 0 0 20px rgba(0, 170, 255, 0.5);
        }

        .quick-bet-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }

        .quick-bet {
            padding: 15px;
            background: rgba(0, 170, 255, 0.2);
            border: 2px solid #00aaff;
            border-radius: 15px;
            color: white;
            cursor: pointer;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
        }

        .quick-bet:hover {
            background: rgba(0, 170, 255, 0.4);
        }

        .auto-cashout-group {
            margin-bottom: 20px;
        }

        .auto-cashout-group label {
            display: block;
            color: white;
            margin-bottom: 10px;
            font-size: 0.9rem;
        }

        .auto-cashout-input {
            width: 100%;
            padding: 15px;
            background: rgba(0, 0, 0, 0.7);
            border: 2px solid #00aaff;
            border-radius: 15px;
            color: white;
            font-family: 'Orbitron', monospace;
            font-size: 1.2rem;
            font-weight: 700;
            text-align: center;
        }

        .auto-cashout-input:focus {
            outline: none;
            box-shadow: 0 0 20px rgba(0, 170, 255, 0.5);
        }

        /* Модальное окно выигрыша */
        .win-modal {
            background: rgba(30, 40, 50, 0.98);
            border: 3px solid #ffaa00;
            border-radius: 35px;
            padding: 50px;
            max-width: 400px;
            width: 90%;
            text-align: center;
            backdrop-filter: blur(20px);
            transform: scale(0.8);
            transition: transform 0.3s ease;
            box-shadow: 0 0 50px rgba(255, 170, 0, 0.5);
        }

        .win-modal-overlay.show .win-modal {
            transform: scale(1);
        }

        .win-modal h2 {
            color: white;
            margin-bottom: 30px;
            font-size: 2.5rem;
            text-shadow: 0 0 20px rgba(255, 170, 0, 0.8);
        }

        .win-modal .modal-btn {
            color: white;
        }

        .win-modal .win-multiplier {
            color: white;
        }

        .win-amount {
            font-size: 4rem;
            font-weight: 900;
            color: #ffaa00;
            text-shadow: 0 0 30px rgba(255, 170, 0, 0.8);
            margin-bottom: 30px;
            animation: goldShine 2s ease-in-out infinite;
        }

        @keyframes goldShine {
            0% { text-shadow: 0 0 30px rgba(255, 170, 0, 0.8); }
            50% { text-shadow: 0 0 50px rgba(255, 215, 0, 1), 0 0 80px rgba(255, 170, 0, 0.6); }
            100% { text-shadow: 0 0 30px rgba(255, 170, 0, 0.8); }
        }

        .win-multiplier {
            font-size: 1.5rem;
            color: white;
            margin-bottom: 30px;
        }

        /* Модальное окно вывода */
        .withdraw-modal {
            background: rgba(30, 40, 50, 0.98);
            border: 3px solid #ff6b6b;
            border-radius: 35px;
            padding: 40px;
            max-width: 500px;
            width: 90%;
            text-align: center;
            backdrop-filter: blur(20px);
            transform: scale(0.8);
            transition: transform 0.3s ease;
        }

        .withdraw-modal-overlay.show .withdraw-modal {
            transform: scale(1);
        }

        .withdraw-input {
            width: 100%;
            padding: 20px;
            background: rgba(0, 0, 0, 0.7);
            border: 2px solid #ff6b6b;
            border-radius: 20px;
            color: white;
            font-family: 'Orbitron', monospace;
            font-size: 1.5rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 20px;
        }

        .withdraw-input:focus {
            outline: none;
            box-shadow: 0 0 20px rgba(255, 107, 107, 0.5);
        }

        .withdraw-info {
            background: rgba(255, 107, 107, 0.1);
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 20px;
            color: white;
            font-size: 0.9rem;
        }

        /* Кнопка смены языка */
        .language-switcher {
            position: fixed;
            bottom: 20px;
            left: 20px;
            background: rgba(30, 40, 50, 0.9);
            border: 2px solid #00aaff;
            border-radius: 20px;
            color: white;
            font-family: 'Orbitron', monospace;
            font-weight: 700;
            padding: 10px 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
            z-index: 1001;
        }

        .language-switcher:hover {
            background: rgba(0, 170, 255, 0.2);
            transform: translateY(-2px);
        }

        .pulse-animation {
            animation: pulseBalance 0.5s ease-in-out;
        }

        @keyframes pulseBalance {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .counting-animation {
            animation: countUp 2s ease-out;
        }

        @keyframes countUp {
            0% { transform: scale(0.8); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; }
            100% { transform: scale(1); opacity: 1; }
        }

        @media (max-width: 1400px) {
            .main-content {
                grid-template-columns: 1fr;
                height: auto;
            }
            
            .game-canvas {
                height: 400px;
            }

            .players-panel {
                order: 2;
            }

            .betting-panel {
                order: 3;
            }

            .online-panel {
                position: relative;
                width: 100%;
                height: auto;
                transform: none;
                margin-bottom: 20px;
            }

            .header-center {
                position: static;
                transform: none;
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                gap: 20px;
                text-align: center;
            }

            .header-center {
                position: static;
                transform: none;
                width: 100%;
                justify-content: center;
            }

            .nav-button {
                padding: 12px 24px;
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo">
                <img src="https://i.postimg.cc/1XymT8ft/sdfv.png" alt="TON CRASH">
            </div>
            
            <!-- Кнопки навигации в центре header -->
            <div class="header-center">
                <button class="nav-button active" id="crashBtn" onclick="switchToSlide(0)" data-lang="crash-game">CRASH</button>
                <button class="nav-button" id="bonusBtn" onclick="switchToSlide(1)" data-lang="bonus">BONUS</button>
            </div>
            
            <div class="balance-container">
                <div class="balance-logo">
                    <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" class="ton-icon">
                </div>
                <div>
                    <div style="font-size: 0.9rem; opacity: 0.8;" data-lang="balance">Баланс</div>
                    <div class="balance-amount" id="balance">
                        <span id="balanceText" class="balance-blurred">1000.00</span>
                        <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" class="ton-icon">
                    </div>
                    <div class="balance-buttons" id="balanceButtons" style="display: none;">
                        <button class="balance-button" onclick="showDepositModal()" data-lang="deposit">ПОПОЛНИТЬ</button>
                        <button class="balance-button withdraw" onclick="showWithdrawModal()" data-lang="withdraw">ВЫВОД СРЕДСТВ</button>
                        <button class="balance-button" onclick="showAccountModal()">:</button>
                    </div>
                </div>
                <div class="login-overlay" id="loginOverlay">
                    <button class="login-btn" onclick="showLoginModal()" data-lang="login">ВОЙТИ</button>
                </div>
            </div>
        </div>

        <div class="content-slider">
            <div class="slider-container" id="sliderContainer">
                <!-- Слайд с игрой -->
                <div class="slide">
                    <div class="main-content">
                        <div class="online-panel">
                            <div class="online-indicator">
                                <div class="online-dot"></div>
                                <span class="online-text" data-lang="online">ОНЛАЙН</span>
                            </div>
                            <div class="online-count" id="onlineCount">127</div>
                        </div>

                        <div class="players-panel">
                            <div class="players-title" data-lang="players-online">Игроки онлайн</div>
                            <div id="playersList"></div>
                        </div>

                        <div class="game-area">
                            <div class="game-canvas" id="gameCanvas">
                                <div class="multiplier-display" id="multiplier">1.00x</div>
                                <div class="win-display" id="winDisplay">+0.00</div>
                                
                                <svg class="trading-chart" id="tradingChart" viewBox="0 0 800 500">
                                    <defs>
                                        <linearGradient id="gradient" x1="0%" y1="0%" x2="0%" y2="100%">
                                            <stop offset="0%" style="stop-color:#00aaff;stop-opacity:0.8" />
                                            <stop offset="100%" style="stop-color:#00aaff;stop-opacity:0" />
                                        </linearGradient>
                                    </defs>
                                    <path class="chart-area" id="chartArea" d=""></path>
                                    <path class="chart-line" id="chartLine" d=""></path>
                                </svg>
                                
                                <img src="" alt="Game Animation" class="game-gif" id="gameGif">
                                <div class="game-history-mini" id="gameHistoryMini"></div>
                                <div class="countdown-overlay" id="countdown" style="display: none;">
                                    <div class="countdown-number" id="countdownNumber">3</div>
                                </div>

                                <!-- Кнопка действия в игре -->
                                <button class="game-action-button login" id="gameActionButton" onclick="showLoginModal()" data-lang="login">ВХОД</button>
                            </div>
                        </div>

                        <div class="betting-panel">
                            <div class="game-stats">
                                <div class="stat-card">
                                    <div class="stat-value" id="totalGames">0</div>
                                    <div class="stat-label" data-lang="total-games">Всего игр</div>
                                </div>
                                <div class="stat-card">
                                    <div class="stat-value" id="winRate">0%</div>
                                    <div class="stat-label" data-lang="win-rate">Процент побед</div>
                                </div>
                            </div>

                            <div class="history-panel">
                                <div class="history-title" data-lang="game-history">История последних игр</div>
                                <div class="history-list" id="historyList"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Слайд с бонусами -->
                <div class="slide">
                    <div class="bonus-content">
                        <div class="bonus-title" data-lang="bonus-system">БОНУСНАЯ СИСТЕМА</div>
                        
                        <div class="bonus-info">
                            <div class="bonus-progress">
                                <div class="bonus-progress-text" id="bonusProgressText" data-lang="stage-progress">Стадия 1 из 5</div>
                                <div class="bonus-progress-bar">
                                    <div class="bonus-progress-fill" id="bonusProgressFill" style="width: 0%"></div>
                                </div>
                            </div>
                            
                            <div class="bonus-stats">
                                <div class="bonus-stat">
                                    <div class="bonus-stat-value" id="totalDeposits">0</div>
                                    <div class="bonus-stat-label" data-lang="total-deposits">Всего пополнений</div>
                                </div>
                                <div class="bonus-stat">
                                    <div class="bonus-stat-value" id="totalBonus">0.00</div>
                                    <div class="bonus-stat-label" data-lang="bonus-received">Получено бонусов</div>
                                </div>
                                <div class="bonus-stat">
                                    <div class="bonus-stat-value" id="nextBonusAmount">100%</div>
                                    <div class="bonus-stat-label" data-lang="next-bonus">Следующий бонус</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="bonus-stages" id="bonusStages">
                            <!-- Стадии бонусов будут добавлены через JavaScript -->
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Кнопка смены языка -->
    <button class="language-switcher" onclick="toggleLanguage()" id="languageSwitcher">RU</button>

    <!-- Модальное окно входа -->
    <div class="modal-overlay" id="loginModal">
        <div class="modal">
            <h2 data-lang="login-title">Вход в игру</h2>
            <input type="text" class="modal-input" id="telegramNick" data-lang-placeholder="enter-nickname" placeholder="Введите ваш ник в Telegram" maxlength="20">
            <div class="modal-buttons">
                <button class="modal-btn confirm" onclick="login()" data-lang="login">ВОЙТИ</button>
                <button class="modal-btn cancel" onclick="closeLoginModal()" data-lang="cancel">ОТМЕНА</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно ставки -->
    <div class="modal-overlay bet-modal-overlay" id="betModal">
        <div class="modal bet-modal">
            <h2 data-lang="place-bet">Сделать ставку</h2>
            <input type="number" class="bet-amount-input" id="betAmountInput" placeholder="0.10" min="0.01" step="0.01">
            
            <div class="quick-bet-grid">
                <button class="quick-bet" onclick="setBetAmountModal(0.1)">
                    0.1 <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" style="width: 16px; height: 16px;">
                </button>
                <button class="quick-bet" onclick="setBetAmountModal(0.5)">
                    0.5 <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" style="width: 16px; height: 16px;">
                </button>
                <button class="quick-bet" onclick="setBetAmountModal(1.0)">
                    1.0 <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" style="width: 16px; height: 16px;">
                </button>
                <button class="quick-bet" onclick="setBetAmountModal(5.0)">
                    5.0 <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" style="width: 16px; height: 16px;">
                </button>
                <button class="quick-bet" onclick="setBetAmountModal(10.0)">
                    10.0 <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" style="width: 16px; height: 16px;">
                </button>
                <button class="quick-bet" onclick="doubleBetModal()">2x</button>
            </div>

            <div class="auto-cashout-group">
                <label for="autoCashoutInput" data-lang="auto-cashout">Авто-кэшаут при (0 = выключен)</label>
                <input type="number" id="autoCashoutInput" class="auto-cashout-input" value="0" min="0" step="0.01" placeholder="0">
            </div>

            <div class="modal-buttons">
                <button class="modal-btn confirm" onclick="confirmBet()" data-lang="place-bet">ПОСТАВИТЬ</button>
                <button class="modal-btn cancel" onclick="closeBetModal()" data-lang="cancel">ОТМЕНА</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно пополнения -->
    <div class="modal-overlay" id="depositModal">
        <div class="modal">
            <h2 data-lang="deposit-balance">Пополнение баланса</h2>
            <div class="deposit-buttons">
                <button class="deposit-btn" onclick="depositCurrency('TON')">
                    <img src="https://files.svgcdn.io/token-branded/ton.png" alt="TON" style="width: 24px; height: 24px;">
                    TON
                </button>
                <button class="deposit-btn" onclick="depositCurrency('USDT')">
                    <img src="https://files.svgcdn.io/token-branded/usdt.png" alt="USDT" style="width: 24px; height: 24px;">
                    USDT
                </button>
            </div>
            <input type="number" class="modal-input" id="depositAmount" data-lang-placeholder="enter-deposit-amount" placeholder="Введите сумму для пополнения" min="1" step="1">
            <div class="modal-buttons">
                <button class="modal-btn confirm" onclick="confirmDeposit()" data-lang="deposit">ПОПОЛНИТЬ</button>
                <button class="modal-btn cancel" onclick="closeDepositModal()" data-lang="cancel">ОТМЕНА</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно вывода -->
    <div class="modal-overlay" id="withdrawModal">
        <div class="modal withdraw-modal">
            <h2 data-lang="withdraw-balance">Вывод средств</h2>
            <div class="withdraw-info">
                <p data-lang="withdraw-info">Минимальная сумма для вывода: 1 TON</p>
                <p data-lang="withdraw-fee">Комиссия сети: 0.02 TON</p>
            </div>
            <input type="text" class="withdraw-input" id="withdrawAddress" data-lang-placeholder="ton-address" placeholder="Введите TON адрес">
            <input type="number" class="modal-input" id="withdrawAmount" data-lang-placeholder="withdraw-amount" placeholder="Введите сумму для вывода" min="1" step="0.01">
            <div class="modal-buttons">
                <button class="modal-btn confirm" onclick="confirmWithdraw()" data-lang="withdraw">ВЫВЕСТИ</button>
                <button class="modal-btn cancel" onclick="closeWithdrawModal()" data-lang="cancel">ОТМЕНА</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно аккаунта -->
    <div class="modal-overlay" id="accountModal">
        <div class="modal account-modal">
            <h2 data-lang="my-account">Мой аккаунт</h2>
            <div class="account-info">
                <div class="account-balance" id="accountBalance">1000.00 TON</div>
                <div class="account-buttons">
                    <button class="modal-btn confirm" onclick="showDepositModal(); closeAccountModal()" data-lang="deposit">ПОПОЛНИТЬ</button>
                    <button class="modal-btn cancel balance-button withdraw" onclick="showWithdrawModal(); closeAccountModal()" data-lang="withdraw">ВЫВОД СРЕДСТВ</button>
                </div>
            </div>
            <div class="last-bets">
                <h3 data-lang="last-bets">Последние 3 ставки:</h3>
                <div id="lastBetsList">
                    <div class="bet-item">
                        <span data-lang="bet-amount">Ставка: 10.5 TON</span>
                        <span class="bet-result win">+15.75 TON</span>
                    </div>
                    <div class="bet-item">
                        <span data-lang="bet-amount">Ставка: 5.0 TON</span>
                        <span class="bet-result lose">-5.0 TON</span>
                    </div>
                    <div class="bet-item">
                        <span data-lang="bet-amount">Ставка: 20.0 TON</span>
                        <span class="bet-result win">+40.0 TON</span>
                    </div>
                </div>
            </div>
            <div class="modal-buttons">
                <button class="modal-btn cancel" onclick="closeAccountModal()" data-lang="close">ЗАКРЫТЬ</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно выигрыша -->
    <div class="modal-overlay win-modal-overlay" id="winModal">
        <div class="modal win-modal">
            <h2 data-lang="win-title">ВЫИГРЫШ!</h2>
            <div class="win-amount" id="winAmountDisplay">+0.00 TON</div>
            <div class="win-multiplier" id="winMultiplierDisplay" data-lang="at-multiplier">при 0.00x</div>
            <div class="modal-buttons">
                <button class="modal-btn confirm" onclick="closeWinModal()" data-lang="great">ОТЛИЧНО!</button>
            </div>
        </div>
    </div>

    <script>
        // Система переводов
        const translations = {
            ru: {
                'balance': 'Баланс',
                'deposit': 'ПОПОЛНИТЬ',
                'withdraw': 'ВЫВОД СРЕДСТВ',
                'login': 'ВОЙТИ',
                'online': 'ОНЛАЙН',
                'players-online': 'Игроки онлайн',
                'total-games': 'Всего игр',
                'win-rate': 'Процент побед',
                'game-history': 'История последних игр',
                'bonus-system': 'БОНУСНАЯ СИСТЕМА',
                'stage-progress': 'Стадия 1 из 5',
                'total-deposits': 'Всего пополнений',
                'bonus-received': 'Получено бонусов',
                'next-bonus': 'Следующий бонус',
                'crash-game': 'CRASH',
                'bonus': 'BONUS',
                'login-title': 'Вход в игру',
                'enter-nickname': 'Введите ваш ник в Telegram',
                'cancel': 'ОТМЕНА',
                'cancel-bet': 'ОТМЕНИТЬ СТАВКУ',
                'place-bet': 'ПОСТАВИТЬ',
                'auto-cashout': 'Авто-кэшаут при (0 = выключен)',
                'deposit-balance': 'Пополнение баланса',
                'withdraw-balance': 'Вывод средств',
                'withdraw-info': 'Минимальная сумма для вывода: 1 TON',
                'withdraw-fee': 'Комиссия сети: 0.02 TON',
                'ton-address': 'Введите TON адрес',
                'withdraw-amount': 'Введите сумму для вывода',
                'enter-deposit-amount': 'Введите сумму для пополнения',
                'my-account': 'Мой аккаунт',
                'last-bets': 'Последние 3 ставки:',
                'bet-amount': 'Ставка:',
                'close': 'ЗАКРЫТЬ',
                'win-title': 'ВЫИГРЫШ!',
                'at-multiplier': 'при',
                'great': 'ОТЛИЧНО!',
                'cashout': 'ЗАБРАТЬ',
                'first-deposit': 'Первое пополнение',
                'second-deposit': 'Второе пополнение',
                'third-deposit': 'Третье пополнение',
                'fourth-deposit': 'Четвертое пополнение',
                'fifth-deposit': 'Пятое пополнение'
            },
            en: {
                'balance': 'Balance',
                'deposit': 'DEPOSIT',
                'withdraw': 'WITHDRAW',
                'login': 'LOGIN',
                'online': 'ONLINE',
                'players-online': 'Online Players',
                'total-games': 'Total Games',
                'win-rate': 'Win Rate',
                'game-history': 'Recent Games History',
                'bonus-system': 'BONUS SYSTEM',
                'stage-progress': 'Stage 1 of 5',
                'total-deposits': 'Total Deposits',
                'bonus-received': 'Bonus Received',
                'next-bonus': 'Next Bonus',
                'crash-game': 'CRASH',
                'bonus': 'BONUS',
                'login-title': 'Login to Game',
                'enter-nickname': 'Enter your Telegram nickname',
                'cancel': 'CANCEL',
                'cancel-bet': 'CANCEL BET',
                'place-bet': 'PLACE BET',
                'auto-cashout': 'Auto-cashout at (0 = disabled)',
                'deposit-balance': 'Deposit Balance',
                'withdraw-balance': 'Withdraw Balance',
                'withdraw-info': 'Minimum withdrawal amount: 1 TON',
                'withdraw-fee': 'Network fee: 0.02 TON',
                'ton-address': 'Enter TON address',
                'withdraw-amount': 'Enter withdrawal amount',
                'enter-deposit-amount': 'Enter deposit amount',
                'my-account': 'My Account',
                'last-bets': 'Last 3 bets:',
                'bet-amount': 'Bet:',
                'close': 'CLOSE',
                'win-title': 'WIN!',
                'at-multiplier': 'at',
                'great': 'GREAT!',
                'cashout': 'CASH OUT',
                'first-deposit': 'First deposit',
                'second-deposit': 'Second deposit',
                'third-deposit': 'Third deposit',
                'fourth-deposit': 'Fourth deposit',
                'fifth-deposit': 'Fifth deposit'
            }
        };

        let currentLanguage = 'ru';

        function toggleLanguage() {
            currentLanguage = currentLanguage === 'ru' ? 'en' : 'ru';
            updateLanguage();
        }

        function updateLanguage() {
            const switcher = document.getElementById('languageSwitcher');
            switcher.textContent = currentLanguage.toUpperCase();

            // Обновляем все элементы с data-lang
            document.querySelectorAll('[data-lang]').forEach(element => {
                const key = element.getAttribute('data-lang');
                if (translations[currentLanguage][key]) {
                    element.textContent = translations[currentLanguage][key];
                }
            });

            // Обновляем плейсхолдеры
            document.querySelectorAll('[data-lang-placeholder]').forEach(element => {
                const key = element.getAttribute('data-lang-placeholder');
                if (translations[currentLanguage][key]) {
                    element.placeholder = translations[currentLanguage][key];
                }
            });

            // Обновляем бонусную систему
            if (game) {
                game.updateBonusDescriptions();
                game.updateBonusDisplay();
            }
        }

        class CrashGame {
            constructor() {
                this.balance = 1000.00;
                this.gameState = 'waiting';
                this.currentMultiplier = 1.00;
                this.betAmount = 0;
                this.hasBet = false;
                this.nextGameBet = false;
                this.nextGameBetAmount = 0;
                this.nextGameAutoCashout = 0;
                this.autoCashout = 0;
                this.gameHistory = [];
                this.miniHistory = [];
                this.totalGames = 0;
                this.wins = 0;
                this.crashPoint = 0;
                this.gameStartTime = 0;
                this.players = [];
                this.gameLoopId = null;
                this.currentGifIndex = 0;
                this.gifChangeInterval = null;
                this.countdownInterval = null;
                this.gameTimeout = null;
                this.chartPoints = [];
                this.baseY = 0;
                this.isCrashed = false;
                this.onlineCount = 127;
                this.isLoggedIn = false;
                this.playerNick = '';
                this.userBets = [];
                this.currentWinAmount = 0;
                
                // Бонусная система
                this.bonusStage = 1;
                this.totalDeposits = 0;
                this.totalBonusReceived = 0;
                this.bonusStages = [
                    { stage: 1, bonus: 100, description: "first-deposit" },
                    { stage: 2, bonus: 50, description: "second-deposit" },
                    { stage: 3, bonus: 10, description: "third-deposit" },
                    { stage: 4, bonus: 10, description: "fourth-deposit" },
                    { stage: 5, bonus: 10, description: "fifth-deposit" }
                ];
                
                // GIF'ы для игрового процесса
                this.gameGifs = [
                    'https://i.postimg.cc/8z9Rz89B/Animated-Ag-ADPls-AAjs4-KUg.gif',
                    'https://i.postimg.cc/KvNFbxKw/Animated-Ag-ADXi0-AAn-Vms-Eg.gif',
                    'https://i.postimg.cc/Jh9CxhgD/Animated-Ag-ADm-Rs-AAs2o-EEs.gif',
                    'https://i.postimg.cc/3wGcKFSN/Animated-Ag-ADERo-AAtixc-Es.gif',
                    'https://i.postimg.cc/W4706DtS/Animated-Ag-ADy-Bk-AAg4-Ei-Eo.gif',
                    'https://i.postimg.cc/Gpw0j9f8/Animated-Ag-ADyxs-AAte-Jk-Us.gif'
                ];
                
                this.initializeGame();
                this.generatePlayers();
                this.startContinuousGame();
                this.startHeartbeatEffect();
                this.startOnlineCounter();
                this.initializeBonusSystem();
            }

            initializeGame() {
                this.updateDisplay();
                this.updateLoginState();
            }

            initializeBonusSystem() {
                this.createBonusStages();
                this.updateBonusDisplay();
            }

            updateBonusDescriptions() {
                this.bonusStages.forEach(stage => {
                    stage.description = translations[currentLanguage][stage.description] || stage.description;
                });
            }

            createBonusStages() {
                const bonusStagesContainer = document.getElementById('bonusStages');
                bonusStagesContainer.innerHTML = '';
                
                this.bonusStages.forEach((stage, index) => {
                    const stageElement = document.createElement('div');
                    stageElement.className = 'bonus-stage';
                    
                    if (this.totalDeposits >= stage.stage) {
                        stageElement.classList.add('completed');
                    } else if (this.totalDeposits + 1 === stage.stage) {
                        stageElement.classList.add('active');
                    }
                    
                    const descriptionKey = Object.keys(translations[currentLanguage]).find(key => 
                        translations[currentLanguage][key] === stage.description
                    );
                    const description = translations[currentLanguage][descriptionKey] || stage.description;
                    
                    stageElement.innerHTML = `
                        <div class="bonus-stage-number">${translations[currentLanguage]['stage-progress'].replace('1 из 5', `${stage.stage}`)}</div>
                        <div class="bonus-percentage">+${stage.bonus}%</div>
                        <div class="bonus-description">${description}</div>
                    `;
                    
                    bonusStagesContainer.appendChild(stageElement);
                });
            }

            updateBonusDisplay() {
                const progressText = document.getElementById('bonusProgressText');
                const progressFill = document.getElementById('bonusProgressFill');
                const totalDepositsEl = document.getElementById('totalDeposits');
                const totalBonusEl = document.getElementById('totalBonus');
                const nextBonusEl = document.getElementById('nextBonusAmount');
                
                progressText.textContent = translations[currentLanguage]['stage-progress'].replace('1', Math.min(this.totalDeposits + 1, 5));
                
                const progressPercent = Math.min((this.totalDeposits / 5) * 100, 100);
                progressFill.style.width = progressPercent + '%';
                
                totalDepositsEl.textContent = this.totalDeposits;
                totalBonusEl.textContent = this.totalBonusReceived.toFixed(2);
                
                const nextStage = this.bonusStages.find(s => s.stage > this.totalDeposits);
                nextBonusEl.textContent = nextStage ? `${nextStage.bonus}%` : 'Max';
                
                this.createBonusStages();
            }

            updateLoginState() {
                const loginOverlay = document.getElementById('loginOverlay');
                const balanceText = document.getElementById('balanceText');
                const balanceButtons = document.getElementById('balanceButtons');
                const gameActionButton = document.getElementById('gameActionButton');

                if (this.isLoggedIn) {
                    loginOverlay.style.display = 'none';
                    balanceText.classList.remove('balance-blurred');
                    balanceButtons.style.display = 'flex';
                    gameActionButton.style.display = 'block';
                    this.updateGameActionButton();
                } else {
                    loginOverlay.style.display = 'block';
                    balanceText.classList.add('balance-blurred');
                    balanceButtons.style.display = 'none';
                    gameActionButton.className = 'game-action-button login';
                    gameActionButton.textContent = translations[currentLanguage]['login'];
                    gameActionButton.onclick = () => showLoginModal();
                }
            }

            updateGameActionButton() {
                if (!this.isLoggedIn) return;
                
                const gameActionButton = document.getElementById('gameActionButton');
                
                if (this.gameState === 'playing' && this.hasBet) {
                    gameActionButton.className = 'game-action-button cashout';
                    gameActionButton.textContent = `${translations[currentLanguage]['cashout']} ${this.currentWinAmount.toFixed(2)} TON`;
                    gameActionButton.onclick = () => this.cashOut();
                    gameActionButton.style.display = 'block';
                } else if (this.nextGameBet) {
                    // Показываем кнопку отмены ставки
                    gameActionButton.className = 'game-action-button cancel';
                    gameActionButton.textContent = translations[currentLanguage]['cancel-bet'];
                    gameActionButton.onclick = () => this.cancelBet();
                    gameActionButton.style.display = 'block';
                } else if (!this.hasBet && !this.nextGameBet) {
                    gameActionButton.className = 'game-action-button bet';
                    gameActionButton.textContent = translations[currentLanguage]['place-bet'];
                    gameActionButton.onclick = () => showBetModal();
                    gameActionButton.style.display = 'block';
                } else {
                    gameActionButton.style.display = 'none';
                }
            }

            // Новая функция для отмены ставки
            cancelBet() {
                if (this.nextGameBet) {
                    // Возвращаем деньги
                    this.balance += this.nextGameBetAmount;
                    
                    // Сбрасываем ставку на следующую игру
                    this.nextGameBet = false;
                    this.nextGameBetAmount = 0;
                    this.nextGameAutoCashout = 0;
                    
                    console.log('Ставка отменена, деньги возвращены');
                    
                    this.updateDisplay();
                    this.updateGameActionButton();
                    
                    // Показываем уведомление
                    const message = currentLanguage === 'ru' ? 'Ставка отменена' : 'Bet cancelled';
                    alert(message);
                }
            }

            login(nickname) {
                this.isLoggedIn = true;
                this.playerNick = nickname;
                this.updateLoginState();
                this.addPlayerToList();
                console.log('Пользователь вошел:', nickname);
            }

            addPlayerToList() {
                // Добавляем игрока в список если его там нет
                const existingPlayer = this.players.find(p => p.name === this.playerNick);
                if (!existingPlayer) {
                    this.players.unshift({
                        name: this.playerNick,
                        avatar: `https://i.pravatar.cc/150?u=${this.playerNick}`,
                        bet: '0.00',
                        isUser: true
                    });
                    if (this.players.length > 8) {
                        this.players.pop();
                    }
                    this.updatePlayersDisplay();
                }
            }

            startOnlineCounter() {
                setInterval(() => {
                    this.onlineCount = Math.floor(Math.random() * 51) + 110;
                    document.getElementById('onlineCount').textContent = this.onlineCount;
                }, 3000);
            }

            startHeartbeatEffect() {
                setInterval(() => {
                    if (Math.random() < 0.1) {
                        const gameCanvas = document.getElementById('gameCanvas');
                        gameCanvas.classList.add('heartbeat');
                        setTimeout(() => {
                            gameCanvas.classList.remove('heartbeat');
                        }, 800);
                    }
                }, 2000);
            }

            startContinuousGame() {
                console.log('Запуск непрерывной игры');
                this.startGameLoop();
            }

            generatePlayers() {
                const names = ['CryptoKing', 'TONMaster', 'RocketMan', 'DiamondHands', 'MoonWalker', 'CoinHunter', 'BlockChainer'];
                const avatars = [
                    'https://i.pravatar.cc/150?img=1',
                    'https://i.pravatar.cc/150?img=2',
                    'https://i.pravatar.cc/150?img=3',
                    'https://i.pravatar.cc/150?img=4',
                    'https://i.pravatar.cc/150?img=5',
                    'https://i.pravatar.cc/150?img=6',
                    'https://i.pravatar.cc/150?img=7'
                ];

                for (let i = 0; i < 7; i++) {
                    this.players.push({
                        name: names[i],
                        avatar: avatars[i],
                        bet: (Math.random() * 10 + 0.1).toFixed(2),
                        potentialWin: 0,
                        isUser: false
                    });
                }
                this.updatePlayersDisplay();
            }

            updatePlayersDisplay() {
                const playersList = document.getElementById('playersList');
                playersList.innerHTML = '';
                
                this.players.forEach(player => {
                    const playerDiv = document.createElement('div');
                    playerDiv.className = 'player-item';
                    
                    let displayBet = player.bet;
                    if (this.gameState === 'playing' && parseFloat(player.bet) > 0) {
                        const potentialWin = (parseFloat(player.bet) * this.currentMultiplier).toFixed(2);
                        displayBet = `${potentialWin} TON`;
                    } else if (parseFloat(player.bet) > 0) {
                        displayBet = `${player.bet} TON`;
                    } else {
                        displayBet = currentLanguage === 'ru' ? 'Ожидает' : 'Waiting';
                    }
                    
                    const youText = currentLanguage === 'ru' ? ' (Вы)' : ' (You)';
                    
                    playerDiv.innerHTML = `
                        <img src="${player.avatar}" alt="${player.name}" class="player-avatar">
                        <div class="player-info">
                            <div class="player-name">${player.name}${player.isUser ? youText : ''}</div>
                            <div class="player-bet">
                                ${displayBet}
                            </div>
                        </div>
                    `;
                    playersList.appendChild(playerDiv);
                });
            }

            startGameLoop() {
                console.log('Начало игрового цикла');
                this.clearAllIntervals();
                this.startCountdown();
            }

            clearAllIntervals() {
                if (this.gameLoopId) {
                    cancelAnimationFrame(this.gameLoopId);
                    this.gameLoopId = null;
                }
                if (this.gifChangeInterval) {
                    clearInterval(this.gifChangeInterval);
                    this.gifChangeInterval = null;
                }
                if (this.countdownInterval) {
                    clearInterval(this.countdownInterval);
                    this.countdownInterval = null;
                }
                if (this.gameTimeout) {
                    clearTimeout(this.gameTimeout);
                    this.gameTimeout = null;
                }
            }

            startCountdown() {
                console.log('Начало обратного отсчета');
                this.gameState = 'countdown';
                const countdown = document.getElementById('countdown');
                const countdownNumber = document.getElementById('countdownNumber');
                
                countdown.style.display = 'flex';
                
                this.addMiniHistoryItem('?', 'pending');
                
                if (this.nextGameBet && this.isLoggedIn) {
                    this.betAmount = this.nextGameBetAmount;
                    this.autoCashout = this.nextGameAutoCashout;
                    this.hasBet = true;
                    this.nextGameBet = false;
                    
                    // Обновляем ставку игрока в списке
                    const userPlayer = this.players.find(p => p.isUser);
                    if (userPlayer) {
                        userPlayer.bet = this.betAmount.toFixed(2);
                    }
                    
                    console.log('Активирована ставка на следующую игру:', this.betAmount);
                }
                
                let count = 3;
                countdownNumber.textContent = count;
                countdownNumber.style.animation = 'heartbeat 1s ease-in-out';

                this.countdownInterval = setInterval(() => {
                    count--;
                    if (count > 0) {
                        countdownNumber.textContent = count;
                        countdownNumber.style.animation = 'none';
                        setTimeout(() => {
                            countdownNumber.style.animation = 'heartbeat 1s ease-in-out';
                        }, 10);
                    } else {
                        clearInterval(this.countdownInterval);
                        this.countdownInterval = null;
                        countdown.style.display = 'none';
                        this.startGame();
                    }
                }, 1000);
            }

            startGame() {
                console.log('Начало игры');
                this.gameState = 'playing';
                this.currentMultiplier = 1.00;
                this.crashPoint = this.generateCrashPoint();
                this.gameStartTime = Date.now();
                this.currentGifIndex = 0;
                this.chartPoints = [];
                this.isCrashed = false;
                this.currentWinAmount = this.hasBet ? this.betAmount : 0;
                
                console.log('Точка краша:', this.crashPoint);
                
                const gameGif = document.getElementById('gameGif');
                gameGif.src = this.gameGifs[this.currentGifIndex];
                gameGif.classList.add('show');
                gameGif.style.left = '50%';
                gameGif.style.top = '150px';
                gameGif.style.transform = 'translateX(-50%)';
                
                this.gifChangeInterval = setInterval(() => {
                    if (this.gameState === 'playing') {
                        this.currentGifIndex = (this.currentGifIndex + 1) % this.gameGifs.length;
                        gameGif.src = this.gameGifs[this.currentGifIndex];
                    }
                }, 1000);
                
                this.updateGameActionButton();
                
                document.getElementById('chartLine').setAttribute('d', '');
                document.getElementById('chartArea').setAttribute('d', '');
                document.getElementById('chartLine').classList.remove('crashed');

                const existingCrash = document.querySelector('.game-crashed');
                if (existingCrash) {
                    existingCrash.remove();
                }

                document.getElementById('multiplier').className = 'multiplier-display';
                document.getElementById('winDisplay').classList.remove('show');

                this.gameLoop();
            }

            generateCrashPoint() {
                const rand = Math.random();
                if (rand < 0.15) return 1.00 + Math.random() * 0.5;
                if (rand < 0.35) return 1.5 + Math.random() * 1.0;
                if (rand < 0.60) return 2.5 + Math.random() * 2.5;
                if (rand < 0.80) return 5.0 + Math.random() * 5.0;
                if (rand < 0.95) return 10.0 + Math.random() * 15.0;
                return 25.0 + Math.random() * 75.0;
            }

            gameLoop() {
                if (this.gameState !== 'playing' && this.gameState !== 'crashed') {
                    console.log('Игровой цикл остановлен, состояние:', this.gameState);
                    return;
                }

                const elapsed = Date.now() - this.gameStartTime;
                
                if (!this.isCrashed) {
                    this.currentMultiplier = 1.00 + Math.pow(elapsed / 1500, 1.1) * 1.2;
                }

                const multiplierElement = document.getElementById('multiplier');
                multiplierElement.textContent = this.currentMultiplier.toFixed(2) + 'x';

                this.updateTradingChart();

                // Обновляем текущий выигрыш если есть ставка
                if (this.hasBet && !this.isCrashed) {
                    this.currentWinAmount = this.betAmount * this.currentMultiplier;
                    this.updateGameActionButton();
                }

                // Обновляем потенциальный выигрыш игроков
                this.updatePlayersDisplay();

                // автокешаут только если значение больше 0
                if (this.hasBet && this.autoCashout > 0 && this.currentMultiplier >= this.autoCashout && !this.isCrashed) {
                    console.log('Авто-кэшаут сработал при:', this.currentMultiplier);
                    this.cashOut();
                    return;
                }

                if (this.currentMultiplier >= this.crashPoint && !this.isCrashed) {
                    console.log('Краш! Множитель:', this.currentMultiplier, 'Точка краша:', this.crashPoint);
                    this.crashGame();
                    return;
                }

                this.gameLoopId = requestAnimationFrame(() => this.gameLoop());
            }

            updateTradingChart() {
                const svg = document.getElementById('tradingChart');
                const svgRect = svg.getBoundingClientRect();
                const width = 800; // viewBox width
                const height = 500; // viewBox height

                const elapsed = Date.now() - this.gameStartTime;
                
                const x = Math.min((elapsed / 15000) * (width - 100), width - 100) + 50;
                
                const multiplierProgress = Math.min((this.currentMultiplier - 1.00) / 19.0, 1.0);
                const smoothProgress = Math.pow(multiplierProgress, 0.4);
                const y = Math.max(height - 50 - (smoothProgress * (height - 150)), 50);
                
                this.chartPoints.push({ x: x, y: y });

                if (this.chartPoints.length > 300) {
                    this.chartPoints.shift();
                }

                let linePath = '';
                let areaPath = '';
                
                if (this.chartPoints.length > 0) {
                    linePath = `M ${this.chartPoints[0].x} ${this.chartPoints[0].y}`;
                    areaPath = `M ${this.chartPoints[0].x} ${height - 50}`;
                    areaPath += ` L ${this.chartPoints[0].x} ${this.chartPoints[0].y}`;
                    
                    for (let i = 1; i < this.chartPoints.length; i++) {
                        linePath += ` L ${this.chartPoints[i].x} ${this.chartPoints[i].y}`;
                        areaPath += ` L ${this.chartPoints[i].x} ${this.chartPoints[i].y}`;
                    }
                    
                    const lastPoint = this.chartPoints[this.chartPoints.length - 1];
                    areaPath += ` L ${lastPoint.x} ${height - 50} Z`;
                }

                document.getElementById('chartLine').setAttribute('d', linePath);
                document.getElementById('chartArea').setAttribute('d', areaPath);
            }

            crashGame() {
                console.log('Игра разбилась при множителе:', this.crashPoint);
                this.gameState = 'crashed';
                this.isCrashed = true;
                
                this.clearAllIntervals();
                
                const gameGif = document.getElementById('gameGif');
                gameGif.classList.remove('show');
                
                document.getElementById('chartLine').classList.add('crashed');
                
                const gameCanvas = document.getElementById('gameCanvas');
                const crashMessage = document.createElement('div');
                crashMessage.className = 'game-crashed';
                crashMessage.textContent = `${currentLanguage === 'ru' ? 'КРАШ!' : 'CRASH!'} ${this.crashPoint.toFixed(2)}x`;
                gameCanvas.appendChild(crashMessage);

                document.getElementById('multiplier').className = 'multiplier-display red';

                this.updateMiniHistoryWithResult(this.crashPoint);

                if (this.hasBet) {
                    const result = {
                        bet: this.betAmount,
                        multiplier: this.crashPoint,
                        result: 'lose',
                        amount: -this.betAmount
                    };
                    this.userBets.unshift(result);
                    if (this.userBets.length > 3) this.userBets.pop();
                    
                    this.gameHistory.push({ multiplier: this.crashPoint, win: false, bet: this.betAmount });
                    this.hasBet = false;
                    this.currentWinAmount = 0;
                    
                    // Сброс ставки игрока
                    const userPlayer = this.players.find(p => p.isUser);
                    if (userPlayer) {
                        userPlayer.bet = '0.00';
                    }
                    
                    console.log('Игрок проиграл ставку:', this.betAmount);
                } else {
                    this.gameHistory.push({ multiplier: this.crashPoint, win: null, bet: 0 });
                }

                this.totalGames++;
                this.updateDisplay();
                this.updateGameActionButton();

                if (this.gameHistory.length > 10) {
                    this.gameHistory = this.gameHistory.slice(-10);
                }

                this.updatePlayersBets();

                console.log('Запуск следующей игры через 3 секунды');
                this.gameTimeout = setTimeout(() => {
                    this.startGameLoop();
                }, 3000);
            }

            addMiniHistoryItem(value, type) {
                const miniHistory = document.getElementById('gameHistoryMini');
                const item = document.createElement('div');
                item.className = `mini-result ${type}`;
                item.textContent = value;
                
                miniHistory.appendChild(item);
                
                while (miniHistory.children.length > 5) {
                    miniHistory.removeChild(miniHistory.firstChild);
                }
            }

            updateMiniHistoryWithResult(multiplier) {
                const miniHistory = document.getElementById('gameHistoryMini');
                const pendingItem = miniHistory.querySelector('.pending');
                
                if (pendingItem) {
                    pendingItem.textContent = multiplier.toFixed(2) + 'x';
                    pendingItem.classList.remove('pending');
                    
                    if (multiplier < 1.5) {
                        pendingItem.classList.add('red');
                    } else if (multiplier < 3.0) {
                        pendingItem.classList.add('orange');
                    } else {
                        pendingItem.classList.add('white');
                    }
                }
            }

            updatePlayersBets() {
                this.players.forEach(player => {
                    if (!player.isUser) {
                        player.bet = (Math.random() * 10 + 0.1).toFixed(2);
                    }
                });
                this.updatePlayersDisplay();
            }

            placeBet(amount, autoCashout) {
                if (!this.isLoggedIn) {
                    showLoginModal();
                    return false;
                }
                
                console.log('Попытка поставить ставку:', amount, 'Состояние игры:', this.gameState);
                
                if (amount <= 0 || amount > this.balance) {
                    alert(currentLanguage === 'ru' ? 'Неверная сумма ставки!' : 'Invalid bet amount!');
                    return false;
                }

                if (this.gameState === 'countdown' || this.gameState === 'waiting' || this.gameState === 'crashed') {
                    if (this.gameState === 'countdown') {
                        // Ставка на текущую игру (пока идет обратный отсчет)
                        this.betAmount = amount;
                        this.balance -= amount;
                        this.hasBet = true;
                        this.currentWinAmount = amount;
                        this.autoCashout = autoCashout || 0;
                        
                        // Обновляем ставку игрока в списке
                        const userPlayer = this.players.find(p => p.isUser);
                        if (userPlayer) {
                            userPlayer.bet = this.betAmount.toFixed(2);
                        }
                        
                        console.log('Ставка на текущую игру принята:', this.betAmount);
                    } else {
                        // Ставка на следующую игру
                        this.nextGameBet = true;
                        this.nextGameBetAmount = amount;
                        this.nextGameAutoCashout = autoCashout || 0;
                        this.balance -= amount;
                        console.log('Ставка на следующую игру зарезервирована:', this.nextGameBetAmount);
                    }
                } else {
                    // Во время игры - ставка на следующую игру
                    this.nextGameBet = true;
                    this.nextGameBetAmount = amount;
                    this.nextGameAutoCashout = autoCashout || 0;
                    this.balance -= amount;
                    console.log('Ставка на следующую игру зарезервирована во время игры:', this.nextGameBetAmount);
                }
                
                this.updateDisplay();
                this.updateGameActionButton();
                this.updatePlayersDisplay();
                return true;
            }

            cashOut() {
                if (!this.isLoggedIn || this.gameState !== 'playing' || !this.hasBet) return;
                
                const winAmount = this.betAmount * this.currentMultiplier;
                this.balance += winAmount;
                
                const result = {
                    bet: this.betAmount,
                    multiplier: this.currentMultiplier,
                    result: 'win',
                    amount: winAmount
                };
                this.userBets.unshift(result);
                if (this.userBets.length > 3) this.userBets.pop();
                
                // Показываем модальное окно выигрыша
                this.showWinModal(winAmount, this.currentMultiplier);
                
                this.gameHistory.push({ 
                    multiplier: this.currentMultiplier, 
                    win: true, 
                    bet: this.betAmount,
                    winAmount: winAmount 
                });
                
                this.wins++;
                
                this.hasBet = false;
                this.betAmount = 0;
                this.currentWinAmount = 0;
                
                // Сброс ставки игрока
                const userPlayer = this.players.find(p => p.isUser);
                if (userPlayer) {
                    userPlayer.bet = '0.00';
                }
                
                console.log('Кэшаут! Выиграно:', winAmount);
                
                document.getElementById('balance').classList.add('pulse-animation');
                setTimeout(() => {
                    document.getElementById('balance').classList.remove('pulse-animation');
                }, 500);
                
                this.updateDisplay();
                this.updateGameActionButton();
                this.updatePlayersDisplay();
            }

            showWinModal(winAmount, multiplier) {
                const winModal = document.getElementById('winModal');
                const winAmountDisplay = document.getElementById('winAmountDisplay');
                const winMultiplierDisplay = document.getElementById('winMultiplierDisplay');
                
                winAmountDisplay.textContent = `+${winAmount.toFixed(2)} TON`;
                winMultiplierDisplay.textContent = `${translations[currentLanguage]['at-multiplier']} ${multiplier.toFixed(2)}x`;
                
                winModal.classList.add('show');
            }

            closeWinModal() {
                const winModal = document.getElementById('winModal');
                winModal.classList.remove('show');
            }

            updateDisplay() {
                const balanceEl = document.getElementById('balanceText');
                balanceEl.textContent = this.balance.toFixed(2);
                
                document.getElementById('totalGames').textContent = this.totalGames;
                document.getElementById('winRate').textContent = this.totalGames > 0 ? 
                    Math.round((this.wins / this.totalGames) * 100) + '%' : '0%';
                
                this.updateHistory();
                
                // Обновляем баланс в модальном окне аккаунта
                const accountBalance = document.getElementById('accountBalance');
                if (accountBalance) {
                    accountBalance.textContent = `${this.balance.toFixed(2)} TON`;
                }
            }

            updateHistory() {
                const historyList = document.getElementById('historyList');
                historyList.innerHTML = '';
                
                this.gameHistory.slice().reverse().forEach(game => {
                    const item = document.createElement('div');
                    item.className = `history-item ${game.win === true ? 'win' : game.win === false ? 'lose' : 'neutral'}`;
                    
                    if (game.win === true) {
                        item.textContent = `${game.multiplier.toFixed(2)}x ✓`;
                    } else if (game.win === false) {
                        item.textContent = `${game.multiplier.toFixed(2)}x ✗`;
                    } else {
                        item.textContent = `${game.multiplier.toFixed(2)}x`;
                        item.style.background = 'rgba(102, 204, 255, 0.2)';
                        item.style.color = '#66ccff';
                    }
                    
                    historyList.appendChild(item);
                });
            }

            updateLastBets() {
                const lastBetsList = document.getElementById('lastBetsList');
                if (lastBetsList && this.userBets.length > 0) {
                    lastBetsList.innerHTML = '';
                    
                    this.userBets.forEach(bet => {
                        const betItem = document.createElement('div');
                        betItem.className = 'bet-item';
                        
                        const resultClass = bet.result === 'win' ? 'win' : 'lose';
                        const resultText = bet.result === 'win' ? 
                            `+${bet.amount.toFixed(2)} TON` : 
                            `${bet.amount.toFixed(2)} TON`;
                        
                        betItem.innerHTML = `
                            <span>${translations[currentLanguage]['bet-amount']} ${bet.bet.toFixed(2)} TON (${bet.multiplier.toFixed(2)}x)</span>
                            <span class="bet-result ${resultClass}">${resultText}</span>
                        `;
                        
                        lastBetsList.appendChild(betItem);
                    });
                }
            }

            deposit(amount) {
                if (!this.isLoggedIn) return;
                
                this.balance += amount;
                this.totalDeposits++;
                
                // Вычисляем бонус
                let bonusPercent = 0;
                if (this.totalDeposits === 1) {
                    bonusPercent = 100;
                } else if (this.totalDeposits === 2) {
                    bonusPercent = 50;
                } else if (this.totalDeposits <= 5) {
                    bonusPercent = 10;
                }
                
                if (bonusPercent > 0) {
                    const bonusAmount = amount * (bonusPercent / 100);
                    this.balance += bonusAmount;
                    this.totalBonusReceived += bonusAmount;
                    
                    const message = currentLanguage === 'ru' ? 
                        `Баланс пополнен на ${amount.toFixed(2)} TON!\nБонус: +${bonusAmount.toFixed(2)} TON (${bonusPercent}%)` :
                        `Balance replenished by ${amount.toFixed(2)} TON!\nBonus: +${bonusAmount.toFixed(2)} TON (${bonusPercent}%)`;
                    alert(message);
                } else {
                    const message = currentLanguage === 'ru' ? 
                        `Баланс пополнен на ${amount.toFixed(2)} TON!` :
                        `Balance replenished by ${amount.toFixed(2)} TON!`;
                    alert(message);
                }
                
                this.updateDisplay();
                this.updateBonusDisplay();
            }

            withdraw(amount, address) {
                if (!this.isLoggedIn) return false;
                
                const minWithdraw = 1;
                const networkFee = 0.02;
                const totalRequired = amount + networkFee;
                
                if (amount < minWithdraw) {
                    const message = currentLanguage === 'ru' ? 
                        `Минимальная сумма для вывода: ${minWithdraw} TON` :
                        `Minimum withdrawal amount: ${minWithdraw} TON`;
                    alert(message);
                    return false;
                }
                
                if (totalRequired > this.balance) {
                    const message = currentLanguage === 'ru' ? 
                        'Недостаточно средств для вывода (включая комиссию сети)' :
                        'Insufficient balance for withdrawal (including network fee)';
                    alert(message);
                    return false;
                }
                
                this.balance -= totalRequired;
                
                const message = currentLanguage === 'ru' ? 
                    `Заявка на вывод ${amount.toFixed(2)} TON отправлена!\nКомиссия сети: ${networkFee} TON\nАдрес: ${address}` :
                    `Withdrawal request for ${amount.toFixed(2)} TON submitted!\nNetwork fee: ${networkFee} TON\nAddress: ${address}`;
                alert(message);
                
                this.updateDisplay();
                return true;
            }
        }

        let game;
        let currentSlide = 0;

        function switchToSlide(slideIndex) {
            const sliderContainer = document.getElementById('sliderContainer');
            const crashBtn = document.getElementById('crashBtn');
            const bonusBtn = document.getElementById('bonusBtn');
            
            currentSlide = slideIndex;
            sliderContainer.style.transform = `translateX(-${slideIndex * 50}%)`;
            
            if (slideIndex === 0) {
                crashBtn.classList.add('active');
                bonusBtn.classList.remove('active');
            } else {
                crashBtn.classList.remove('active');
                bonusBtn.classList.add('active');
            }
        }

        function showLoginModal() {
            const modal = document.getElementById('loginModal');
            const input = document.getElementById('telegramNick');
            
            input.value = '';
            modal.classList.add('show');
            input.focus();
        }

        function closeLoginModal() {
            const modal = document.getElementById('loginModal');
            modal.classList.remove('show');
        }

        function login() {
            const nickname = document.getElementById('telegramNick').value.trim();
            if (nickname.length < 2) {
                const message = currentLanguage === 'ru' ? 'Введите корректный ник!' : 'Enter a valid nickname!';
                alert(message);
                return;
            }
            
            game.login(nickname);
            closeLoginModal();
        }

        function showBetModal() {
            if (!game.isLoggedIn) {
                showLoginModal();
                return;
            }
            
            const modal = document.getElementById('betModal');
            const input = document.getElementById('betAmountInput');
            
            input.value = '0.10';
            modal.classList.add('show');
            input.focus();
        }

        function closeBetModal() {
            const modal = document.getElementById('betModal');
            modal.classList.remove('show');
        }

        function setBetAmountModal(amount) {
            document.getElementById('betAmountInput').value = amount.toFixed(2);
        }

        function doubleBetModal() {
            const current = parseFloat(document.getElementById('betAmountInput').value) || 0;
            const doubled = (current * 2).toFixed(2);
            document.getElementById('betAmountInput').value = doubled;
        }

        function confirmBet() {
            const amount = parseFloat(document.getElementById('betAmountInput').value);
            const autoCashout = parseFloat(document.getElementById('autoCashoutInput').value) || 0;
            
            if (amount && amount > 0 && game.placeBet(amount, autoCashout)) {
                closeBetModal();
            } else {
                const message = currentLanguage === 'ru' ? 'Введите корректную сумму!' : 'Enter a valid amount!';
                alert(message);
            }
        }

        function showDepositModal() {
            if (!game.isLoggedIn) {
                showLoginModal();
                return;
            }
            
            const modal = document.getElementById('depositModal');
            const input = document.getElementById('depositAmount');
            
            input.value = '';
            modal.classList.add('show');
        }

        function closeDepositModal() {
            const modal = document.getElementById('depositModal');
            modal.classList.remove('show');
        }

        function showWithdrawModal() {
            if (!game.isLoggedIn) {
                showLoginModal();
                return;
            }
            
            const modal = document.getElementById('withdrawModal');
            const addressInput = document.getElementById('withdrawAddress');
            const amountInput = document.getElementById('withdrawAmount');
            
            addressInput.value = '';
            amountInput.value = '';
            modal.classList.add('show');
            addressInput.focus();
        }

        function closeWithdrawModal() {
            const modal = document.getElementById('withdrawModal');
            modal.classList.remove('show');
        }

        function confirmWithdraw() {
            const address = document.getElementById('withdrawAddress').value.trim();
            const amount = parseFloat(document.getElementById('withdrawAmount').value);
            
            if (!address) {
                const message = currentLanguage === 'ru' ? 'Введите TON адрес!' : 'Enter TON address!';
                alert(message);
                return;
            }
            
            if (!amount || amount <= 0) {
                const message = currentLanguage === 'ru' ? 'Введите корректную сумму!' : 'Enter a valid amount!';
                alert(message);
                return;
            }
            
            if (game.withdraw(amount, address)) {
                closeWithdrawModal();
            }
        }

        function depositCurrency(currency) {
            console.log('Выбрана валюта для пополнения:', currency);
        }

        function confirmDeposit() {
            const amount = parseFloat(document.getElementById('depositAmount').value);
            if (amount && amount > 0) {
                game.deposit(amount);
                closeDepositModal();
            } else {
                const message = currentLanguage === 'ru' ? 'Введите корректную сумму!' : 'Enter a valid amount!';
                alert(message);
            }
        }

        function showAccountModal() {
            if (!game.isLoggedIn) {
                showLoginModal();
                return;
            }
            
            const modal = document.getElementById('accountModal');
            game.updateLastBets();
            modal.classList.add('show');
        }

        function closeAccountModal() {
            const modal = document.getElementById('accountModal');
            modal.classList.remove('show');
        }

        function closeWinModal() {
            if (game) game.closeWinModal();
        }

        // Закрытие модальных окон по клику вне их
        document.addEventListener('click', function(e) {
            if (e.target.classList.contains('modal-overlay')) {
                e.target.classList.remove('show');
            }
        });

        // Вход по Enter в модальном окне логина
        document.getElementById('telegramNick').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                login();
            }
        });

        // Ставка по Enter в модальном окне ставки
        document.getElementById('betAmountInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                confirmBet();
            }
        });

        // Пополнение по Enter
        document.getElementById('depositAmount').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                confirmDeposit();
            }
        });

        // Вывод по Enter
        document.getElementById('withdrawAmount').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                confirmWithdraw();
            }
        });

        // Инициализация игры
        document.addEventListener('DOMContentLoaded', function() {
            game = new CrashGame();
            updateLanguage();
        });
    </script>
</body>
</html>
