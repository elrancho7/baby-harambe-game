# baby-harambe-game
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Rambe</title>
		<style>
			* { margin: 0; padding: 0; box-sizing: border-box; }
		</style>
	</head>
	<body>
		<div class="container">
			<h1>Hello, World!</h1>
			<p>Start editing to build something amazing.</p>
		</div>
	</body>
</html>
<
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"
		/>
		<title>Baby Harambe's Revenge</title>
		<style>
			body {
			    margin: 0;
			    background: #0a0e14;
			    color: #fff;
			    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
			    text-align: center;
			    touch-action: manipulation;
			    overflow: hidden;
			}
			h1 { font-size: 15px; margin: 3px 0; color: #00ffcc; text-shadow: 0 0 8px rgba(0,255,204,0.4); }
			.ui-panel { display: flex; justify-content: space-around; font-size: 11px; color: #8b949e; background: #161b22; padding: 4px 0; border-bottom: 1px solid #30363d; }
			.ui-panel span { color: #ffd700; font-weight: bold; }
			#boss-alert { font-size: 11px; height: 14px; color: #ff4444; font-weight: bold; margin: 2px 0; }

			#game-container {
			    position: relative;
			    width: 100vw;
			    max-width: 400px;
			    height: 200px;
			    background: radial-gradient(circle, #1a2f23 0%, #0d1a12 100%);
			    margin: 0 auto;
			    border-top: 2px solid #30363d;
			    border-bottom: 2px solid #30363d;
			    overflow: hidden;
			}
			canvas { display: block; width: 100%; height: 100%; }

			/* Smartphone Touch Controls */
			.controls {
			    display: flex;
			    justify-content: space-around;
			    align-items: center;
			    width: 100vw;
			    max-width: 400px;
			    margin: 5px auto;
			    padding: 0 10px;
			    box-sizing: border-box;
			}
			.btn-group {
			    display: flex;
			    flex-direction: column;
			    gap: 4px;
			}
			.control-btn {
			    background: #161b22;
			    color: #fff;
			    border: 2px solid #30363d;
			    font-size: 15px;
			    padding: 6px 14px;
			    border-radius: 8px;
			    cursor: pointer;
			    user-select: none;
			    -webkit-tap-highlight-color: transparent;
			}
			.control-btn:active { background: #30363d; transform: scale(0.95); }
			#throw-btn {
			    background: linear-gradient(135deg, #f0883e 0%, #d16922 100%);
			    border-color: #ffa657;
			    color: #fff;
			    font-weight: bold;
			    font-size: 12px;
			    padding: 14px 10px;
			    border-radius: 50%;
			    box-shadow: 0 4px 10px rgba(240,136,62,0.4);
			}

			/* Shop & Panels */
			.shop-panel {
			    display: flex;
			    justify-content: center;
			    gap: 6px;
			    padding: 0 10px;
			    margin-bottom: 2px;
			}
			.shop-btn {
			    background: #238636;
			    color: #fff;
			    border: none;
			    padding: 4px 7px;
			    font-size: 10px;
			    font-weight: bold;
			    border-radius: 5px;
			    cursor: pointer;
			}
			.shop-btn:active { opacity: 0.8; }

			.leaderboard {
			    font-size: 11px;
			    background: #161b22;
			    width: 100%;
			    max-width: 380px;
			    margin: 3px auto;
			    padding: 4px;
			    border-radius: 6px;
			    border: 1px solid #30363d;
			    color: #8b949e;
			    text-align: left;
			    box-sizing: border-box;
			}
			.leaderboard-title { color: #00ffcc; font-weight: bold; text-align: center; margin-bottom: 2px; }
			.lb-row { display: flex; justify-content: space-between; padding: 1px 6px; }

			#launch-section { padding: 0 10px; }
			.action-btn {
			    display: block;
			    width: 100%;
			    max-width: 380px;
			    margin: 3px auto;
			    padding: 6px;
			    font-size: 12px;
			    font-weight: bold;
			    text-decoration: none;
			    border-radius: 6px;
			    border: none;
			    cursor: pointer;
			    background: #00ffcc;
			    color: #000;
			    box-shadow: 0 0 8px rgba(0,255,204,0.3);
			}
		</style>
	</head>
	<body>
		<h1>🦍 BABY HARAMBE: REVENGE</h1>
		<div class="ui-panel">
			<div>Score: <span id="score">0</span></div>
			<div>Level: <span id="level">1</span></div>
			<div>Banana Coins: <span id="coins">0</span> 🍌</div>
		</div>
		<div id="boss-alert"></div>

		<div id="game-container">
			<canvas id="gameCanvas" width="400" height="200"></canvas>
		</div>

		<!-- Shop & Upgrades -->
		<div class="shop-panel">
			<button class="shop-btn" onclick="upgradeGun('rapid')">
				⚡ Rapid (50 Coins)
			</button>
			<button class="shop-btn" onclick="upgradeGun('spread')">
				💥 Spread (100 Coins)
			</button>
		</div>

		<!-- Leaderboard UI -->
		<div class="leaderboard">
			<div class="leaderboard-title">🏆 TOP DEGEN HIGH SCORES</div>
			<div class="lb-row">
				<span>1. <span id="lb-name-0">Anon</span></span>
				<span id="lb-score-0">0</span>
			</div>
			<div class="lb-row">
				<span>2. <span id="lb-name-1">Anon</span></span>
				<span id="lb-score-1">0</span>
			</div>
			<div class="lb-row">
				<span>3. <span id="lb-name-2">Anon</span></span>
				<span id="lb-score-2">0</span>
			</div>
		</div>

		<!-- On-Screen Touch Controls -->
		<div class="controls">
			<div class="btn-group">
				<button class="control-btn" id="up-btn">⬆️</button>
				<button class="control-btn" id="down-btn">⬇️</button>
			</div>
			<button class="control-btn" id="throw-btn">🍌 THROW</button>
		</div>

		<div id="launch-section">
			<!-- Replace '#' with your actual pump.fun link once deployed -->
			<a id="buy-token-btn" class="action-btn" href="#" target="_blank"
				>Ape $BHARAMBE on Pump.fun</a
			>
		</div>

		<script>
			const canvas = document.getElementById("gameCanvas");
			const ctx = canvas.getContext("2d");

			let score = 0;
			let coins = 0;
			let level = 1;

			// Load or initialize Leaderboard data from localStorage
			let leaderboard = JSON.parse(localStorage.getItem("bharambe_lb")) || [
			    { name: "Harambe", score: 500 },
			    { name: "Satoshi", score: 300 },
			    { name: "Degen", score: 100 }
			];
			updateLeaderboardDisplay();

			let player = { x: 25, y: 70, size: 36 };
			let bananas = [];
			let particles = [];
			let gunLevel = 1; // 1: Normal, 2: Rapid, 3: Spread Shot

			let keepers = [
			    { x: 330, y: 15, speed: 1.3, hp: 1, maxHp: 1, type: "guard", alive: true },
			    { x: 330, y: 80, speed: 1.7, hp: 1, maxHp: 1, type: "guard", alive: true },
			    { x: 330, y: 145, speed: 1.1, hp: 1, maxHp: 1, type: "guard", alive: true }
			];

			let bossActive = false;
			let boss = null;
			let movingUp = false;
			let movingDown = false;
			let gameEnded = false;

			// Touch Listeners for iPhone
			document.getElementById("up-btn").addEventListener("touchstart", (e) => { e.preventDefault(); movingUp = true; });
			document.getElementById("up-btn").addEventListener("touchend", () => { movingUp = false; });
			document.getElementById("down-btn").addEventListener("touchstart", (e) => { e.preventDefault(); movingDown = true; });
			document.getElementById("down-btn").addEventListener("touchend", () => { movingDown = false; });

			document.getElementById("throw-btn").addEventListener("touchstart", (e) => {
			    e.preventDefault();
			    if (!gameEnded) shootBananas();
			});

			function shootBananas() {
			    let speed = gunLevel >= 2 ? 8 : 5.5;
			    bananas.push({ x: player.x + 35, y: player.y + 14, vx: speed, vy: 0 });

			    if (gunLevel >= 3) {
			        bananas.push({ x: player.x + 35, y: player.y + 14, vx: 7, vy: -1.2 });
			        bananas.push({ x: player.x + 35, y: player.y + 14, vx: 7, vy: 1.2 });
			    }
			}

			function upgradeGun(type) {
			    if (type === 'rapid' && gunLevel < 2 && coins >= 50) {
			        coins -= 50;
			        gunLevel = 2;
			        alert("Rapid Fire Gun Unlocked!");
			    } else if (type === 'spread' && gunLevel < 3 && coins >= 100) {
			        coins -= 100;
			        gunLevel = 3;
			        alert("Triple Spread Gun Unlocked!");
			    } else {
			        alert("Not enough Banana Coins or already unlocked!");
			    }
			    document.getElementById("coins").innerText = coins;
			}

			function createExplosion(x, y, isBoss) {
			    let count = isBoss ? 35 : 15;
			    for (let i = 0; i < count; i++) {
			        particles.push({
			            x: x, y: y,
			            vx: (Math.random() - 0.5) * 8,
			            vy: (Math.random() - 0.5) * 8,
			            radius: Math.random() * 4 + 2,
			            color: isBoss ? ['#ffd700', '#ff0000', '#ff8800'][Math.floor(Math.random() * 3)] : ['#ff4400', '#ffbb00', '#fff'][Math.floor(Math.random() * 3)],
			            life: 30
			        });
			    }
			}

			function checkLeaderboard(finalScore) {
			    // Check if score qualifies for top 3
			    let qualifies = leaderboard.some(entry => finalScore > entry.score);
			    if (qualifies || leaderboard.length < 3) {
			        let playerName = prompt("🔥 NEW HIGH SCORE! Enter your Degen username:", "CryptoApe");
			        if (!playerName || playerName.trim() === "") playerName = "Anonymous";

			        leaderboard.push({ name: playerName.trim().substring(0, 10), score: finalScore });
			        leaderboard.sort((a, b) => b.score - a.score);
			        leaderboard = leaderboard.slice(0, 3); // Keep top 3

			        localStorage.setItem("bharambe_lb", JSON.stringify(leaderboard));
			        updateLeaderboardDisplay();
			    }
			}

			function updateLeaderboardDisplay() {
			    for (let i = 0; i < 3; i++) {
			        if (leaderboard[i]) {
			            document.getElementById(`lb-name-${i}`).innerText = leaderboard[i].name;
			            document.getElementById(`lb-score-${i}`).innerText = leaderboard[i].score;
			        } else {
			            document.getElementById(`lb-name-${i}`).innerText = "---";
			            document.getElementById(`lb-score-${i}`).innerText = "0";
			        }
			    }
			}

			function checkMilestones() {
			    if (score >= 250 && level === 1 && !bossActive) {
			        spawnBoss("LEVEL 1 BOSS: CHIEF KEEPER!");
			        level = 2;
			    } else if (score >= 600 && level === 2 && !bossActive) {
			        spawnBoss("LEVEL 2 BOSS: ZOO DIRECTOR!");
			        level = 3;
			    } else if (score >= 1200 && level === 3 && !bossActive) {
			        spawnBoss("FINAL BOSS: THE VETERINARIAN!");
			        level = 4;
			    }
			    document.getElementById("level").innerText = level;
			}

			function spawnBoss(title) {
			    bossActive = true;
			    keepers.forEach(k => k.alive = false);
			    document.getElementById("boss-alert").innerText = `⚠️ ${title} ⚠️`;

			    boss = {
			        x: 320,
			        y: 50,
			        width: 32,
			        height: 42,
			        hp: level * 5,
			        maxHp: level * 5,
			        speed: 1.5 + (level * 0.3)
			    };
			}

			function update() {
			    if (gameEnded) return;

			    if (movingUp && player.y > 5) player.y -= 3.8;
			    if (movingDown && player.y < canvas.height - player.size - 5) player.y += 3.8;

			    bananas.forEach((b, bIndex) => {
			        b.x += b.vx;
			        if (b.vy) b.y += b.vy;

			        if (bossActive && boss) {
			            if (b.x > boss.x && b.x < boss.x + boss.width && b.y > boss.y && b.y < boss.y + boss.height) {
			                bananas.splice(bIndex, 1);
			                boss.hp--;
			                createExplosion(b.x, b.y, false);

			                if (boss.hp <= 0) {
			                    createExplosion(boss.x + 15, boss.y + 20, true);
			                    score += 300;
			                    coins += 50;
			                    bossActive = false;
			                    boss = null;
			                    document.getElementById("boss-alert").innerText = "BOSS DEFEATED! +50 Coins!";
			                    setTimeout(() => { document.getElementById("boss-alert").innerText = ""; }, 3000);

			                    keepers.forEach(k => { k.alive = true; k.y = Math.random() * 130; });
			                }
			            }
			        }

			        keepers.forEach(k => {
			            if (k.alive && b.x > k.x && b.x < k.x + 25 && b.y > k.y && b.y < k.y + 35) {
			                bananas.splice(bIndex, 1);
			                createExplosion(k.x + 12, k.y + 17, false);
			                k.alive = false;
			                score += 50;
			                coins += 10;

			                setTimeout(() => {
			                    if (!bossActive && !gameEnded) {
			                        k.alive = true;
			                        k.y = Math.random() * (canvas.height - 45);
			                    }
			                }, 1500);
			            }
			        });

			        if (b.x > canvas.width || b.y < 0 || b.y > canvas.height) {
			            bananas.splice(bIndex, 1);
			        }
			    });

			    if (!bossActive) {
			        keepers.forEach(k => {
			            if (k.alive) {
			                k.y += k.speed;
			                if (k.y > canvas.height - 40 || k.y < 5) k.speed *= -1;

			                // If keeper crosses paths and hits player, end run & check leaderboard
			                if (Math.abs(k.x - player.x) < 25 && Math.abs(k.y - player.y) < 25) {
			                    gameEnded = true;
			                    document.getElementById("boss-alert").innerText = "GAME OVER! Captured!";
			                    checkLeaderboard(score);
			                }
			            }
			        });
			    }

			    if (bossActive && boss) {
			        boss.y += boss.speed;
			        if (boss.y > canvas.height - 45 || boss.y < 5) boss.speed *= -1;
			    }

			    particles.forEach((p, index) => {
			        p.x += p.vx;
			        p.y += p.vy;
			        p.life--;
			        if (p.life <= 0) particles.splice(index, 1);
			    });

			    checkMilestones();
			    document.getElementById("score").innerText = score;
			    document.getElementById("coins").innerText = coins;
			}

			function draw() {
			    ctx.clearRect(0, 0, canvas.width, canvas.height);

			    // Draw Baby Harambe (Green Beanie)
			    ctx.fillStyle = "#3b7a57";
			    ctx.fillRect(player.x + 8, player.y - 6, 22, 8);
			    ctx.fillStyle = "#4a3319";
			    ctx.fillRect(player.x, player.y + 2, 35, 34);
			    ctx.fillStyle = "#ffcc00";
			    ctx.beginPath();
			    ctx.arc(player.x + 28, player.y + 20, 5, 0, Math.PI * 2);
			    ctx.fill();
			    ctx.font = "12px sans-serif";
			    ctx.fillText("🦍", player.x + 4, player.y + 25);

			    // Draw Bananas
			    ctx.fillStyle = "#ffe600";
			    bananas.forEach(b => {
			        ctx.beginPath();
			        ctx.arc(b.x, b.y, 5, 0, Math.PI * 2);
			        ctx.fill();
			    });

			    // Draw Regular Keepers
			    if (!bossActive) {
			        keepers.forEach(k => {
			            if (k.alive) {
			                ctx.fillStyle = "#1f6feb";
			                ctx.fillRect(k.x, k.y, 25, 35);
			                ctx.font = "12px sans-serif";
			                ctx.fillText("👮", k.x + 2, k.y + 23);
			            }
			        });
			    }

			    // Draw Boss Character
			    if (bossActive && boss) {
			        ctx.fillStyle = "#dc2626";
			        ctx.fillRect(boss.x, boss.y, boss.width, boss.height);
			        ctx.font = "16px sans-serif";
			        ctx.fillText("👹", boss.x + 4, boss.y + 26);

			        ctx.fillStyle = "#333";
			        ctx.fillRect(boss.x - 4, boss.y - 10, 40, 5);
			        ctx.fillStyle = "#22c55e";
			        ctx.fillRect(boss.x - 4, boss.y - 10, (boss.hp / boss.maxHp) * 40, 5);
			    }

			    // Draw Particles
			    particles.forEach(p => {
			        ctx.fillStyle = p.color;
			        ctx.beginPath();
			        ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
			        ctx.fill();
			    });
			}

			function loop() {
			    update();
			    draw();
			    requestAnimationFrame(loop);
			}

			loop();
		</script>
	</body>
</html>
