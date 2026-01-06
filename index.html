<!DOCTYPE html>

<html>
    <head>
        <title>Cursor Crusader</title>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    </head>
    <body style="margin:0; padding:0; background:black;">
        <canvas id="canvas" width="1200" height="700" style="border:1px solid white;" tabindex="1"></canvas>

        <script>
            /*
             *Matthew Fuchs
             *Cursor crusader is a game where you need to avoid projectiles shot by enemies and click when near them to deal damage, you collect shards to upgrade and they are dropped from enemies
             */
            var canvas = document.getElementById("canvas");
            var ctx = canvas.getContext("2d");
            var mouseXPos = 0;
            var mouseYPos = 0;
            var mouseLeftDown = false;
            var playerMaxHealth = 10;
            var playerHealth = 10;
            var shards = 100;
            var totalShardsCollected = 0;

            var totalPrestiges = 0;
            var prestigePoints = 0;
            var prestiged = false;

            var MIN_WAVE = 1;
            var MAX_WAVE = 26;

            var wave = 1;
            var selectedWave = 1;
            var waveInProgress = false;
            var waveCooldown = 2000;
            var lastWaveEnd = 0;
            var waveBudget = 0;
            var maxWaveBudget = 5;


            var gameScreen = "menu";
            var highestWave = 1;
            var selectedWave = 1;
            // arena init
            var arenaX = 275;
            var arenaY = 25;
            var arenaSize = 650;
            var arenaOpen = false;
            //enemies init
            var enemies = [];
            var enemyProjectiles = [];
            var lastEnemySpawn = 0;
            var enemySpawnInterval = 5000; // 5 seconds
            var playerHitInterval = 1000;
            var boss = null;
            var bossActive = false;
            var bossProjectiles = [];
            var bossLazers = [];
            var FINAL_BOSS_WAVE = 25;
            var finalBossDefeated = false;

            // === UPGRADE VALUES ===
            var damageLevel = 0;
            var healthLevel = 0;
            var speedLevel = 0;
            var rangeLevel = 0;
            var sizeLevel = 0;
            var UPGRADE_COST = 100;

            // Base costs
            var speedCost = 5;
            var rangeCost = 5;
            var sizeCost = 5;
            var damageCost = 10;
            var healthCost = 10;

            var dashUnlocked = false;
            var dashLevel = 1;          // upgrades
            var dashCooldown = 4000;
            var dashStrength = 0.25;

            var dashLastUsed = -Infinity;
            var dashActive = false;
            var dashDuration = 120;

            var dashEquipped = false;

            class bossEnemy {
                constructor(x, y, radius, health, bulletDamage, bulletSpeed, bulletQuantity, bulletCooldown, bulletRotationSpeed,
                        lazerDamage, lazerQuantity, lazerRotationSpeed, phases, colour, shardDrop) {

                    this.x = x;
                    this.y = y;
                    this.radius = radius;

                    this.maxHealth = health;
                    this.health = health;

                    this.bulletDamage = bulletDamage;
                    this.bulletSpeed = bulletSpeed;
                    this.bulletQuantity = bulletQuantity;
                    this.bulletCooldown = bulletCooldown;
                    this.bulletRotationSpeed = bulletRotationSpeed;

                    this.lazerDamage = lazerDamage;
                    this.lazerQuantity = lazerQuantity;
                    this.lazerRotationSpeed = lazerRotationSpeed;

                    this.phases = phases;
                    this.currentPhase = 1;
                    this.phaseHP = this.maxHealth / this.phases;

                    this.colour = colour;
                    this.shardDrop = shardDrop;

                    this.lastShot = 0;
                    this.lastLazerShot = 0;
                    this.lazerCooldown = 3000;
                    this.lazerBaseAngle = 0;
                    this.lazerAngle = 0;
                    this.lazerAngle = 0;
                    this.lazerTimer = 0;


                    this.lazerActiveTime = 90;    // DAMAGE ON (frames)
                    this.lazerDisabledTime = 120;  // DAMAGE OFF + fading (frames)

                    this.lazerCycleTime = this.lazerActiveTime + this.lazerDisabledTime;

                    this.lazersSpawned = false;

                }

                draw() {
                    ctx.fillStyle = this.colour;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                    ctx.fill();

                    this.drawHealthBar();
                }

                drawHealthBar() { //draw the health bar at the top of the screen with lines for phases
                    var barWidth = 400;
                    var barHeight = 15;
                    var x = canvas.width / 2 - barWidth / 2;
                    var y = 40;

                    ctx.fillStyle = "red";
                    ctx.fillRect(x, y, barWidth, barHeight);

                    ctx.fillStyle = "lime";
                    ctx.fillRect(x, y, barWidth * (this.health / this.maxHealth), barHeight);

                    // phase lines
                    ctx.strokeStyle = "white";
                    for (var i = 1; i < this.phases; i++) {
                        var lineX = x + (barWidth * (i / this.phases));
                        ctx.beginPath();
                        ctx.moveTo(lineX, y);
                        ctx.lineTo(lineX, y + barHeight);
                        ctx.stroke();
                    }
                }

                update() { //update the phases if the boss gets lowk enough
                    this.checkPhase();

                    if (this.currentPhase === 1)
                        this.phase1();
                    if (this.currentPhase === 2)
                        this.phase2();
                    if (this.currentPhase >= 3)
                        this.phase3();
                }

                checkPhase() { //check the phases for the attaco 
                    var newPhase = Math.floor((this.maxHealth - this.health) / this.phaseHP) + 1;

                    if (newPhase > this.currentPhase && newPhase <= this.phases) {
                        this.currentPhase = newPhase;
                        this.onPhaseChange();
                    }
                }

                onPhaseChange() {
                    // scald the stats per phase
                    this.bulletDamage *= 1.1;
                    this.bulletSpeed *= 1.03;
                    this.bulletRotationSpeed *= 1.02;

                    this.lazerDamage *= 1.05;
                    this.lazerRotationSpeed *= 1.02;

                    this.bulletQuantity += 1;
                    this.lazerQuantity += 1;
                }

                phase1() {
                    this.shootBullets();
                }

                phase2() {
                    this.shootBullets();
                }

                phase3() {
                    this.shootBullets();

                    if (!this.lazersSpawned) {
                        this.spawnLazers();
                        this.lazersSpawned = true;
                    }
                }

                shootBullets() {
                    if (Date.now() - this.lastShot < this.bulletCooldown)
                        return;

                    this.lastShot = Date.now();

                    var angleStep = (Math.PI * 2) / this.bulletQuantity;

                    for (var i = 0; i < this.bulletQuantity; i++) {
                        var angle = i * angleStep;

                        bossProjectiles[bossProjectiles.length] = {
                            x: this.x,
                            y: this.y,
                            vx: Math.cos(angle) * this.bulletSpeed,
                            vy: Math.sin(angle) * this.bulletSpeed,
                            radius: 6,
                            damage: this.bulletDamage,
                            colour: "violet"
                        };
                    }
                }

                spawnLazers() {
                    bossLazers = [];

                    var angleStep = (Math.PI * 2) / this.lazerQuantity;

                    for (var i = 0; i < this.lazerQuantity; i++) {
                        bossLazers[bossLazers.length] = {
                            offset: i * angleStep
                        };
                    }
                }

            }


            function updateBossProjectiles() {
                for (var i = bossProjectiles.length - 1; i >= 0; i--) {
                    var p = bossProjectiles[i];

                    p.x += p.vx;
                    p.y += p.vy;

                    if (
                            p.x < arenaX || p.x > arenaX + arenaSize ||
                            p.y < arenaY || p.y > arenaY + arenaSize
                            ) {
                        bossProjectiles.splice(i, 1);
                        continue;
                    }

                    if (circleCollision(p.x, p.y, p.radius, dot.x, dot.y, dot.radius)) {
                        playerHealth -= p.damage;
                        playerHealthBar.set(playerHealth);
                        bossProjectiles.splice(i, 1);

                        if (playerHealth <= 0)
                            gameScreen = "lose";
                    }
                }
            }
            function drawBossProjectiles() {
                for (var i = 0; i < bossProjectiles.length; i++) {
                    var p = bossProjectiles[i];
                    ctx.fillStyle = p.colour;
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                    ctx.fill();
                }
            }


            function updateBossLazers() {
                if (!bossActive || boss === null || gameScreen !== "arena1")
                    return;

                // continuous rotation
                boss.lazerAngle += boss.lazerRotationSpeed;

                // advance timer
                boss.lazerTimer++;
                if (boss.lazerTimer >= boss.lazerCycleTime) {
                    boss.lazerTimer = 0;
                }

                var damageActive = boss.lazerTimer < boss.lazerActiveTime;

                // collision only while active
                if (!damageActive)
                    return;

                for (var i = 0; i < bossLazers.length; i++) {
                    var lazer = bossLazers[i];
                    var angle = boss.lazerAngle + lazer.offset;

                    var dx = Math.cos(angle);
                    var dy = Math.sin(angle);

                    var px = dot.x - boss.x;
                    var py = dot.y - boss.y;

                    var proj = px * dx + py * dy;
                    var dist = Math.abs(px * dy - py * dx);

                    if (proj > 0 && proj < 1000 && dist < 6) {
                        playerHealth -= boss.lazerDamage;
                        playerHealthBar.set(playerHealth);

                        if (playerHealth <= 0)
                            gameScreen = "lose";
                    }
                }
            }


            function drawBossLazers() {
                if (!bossActive || boss === null || gameScreen !== "arena1")
                    return;

                var alpha = 1;

                // fade during disabled time
                if (boss.lazerTimer > boss.lazerActiveTime) {
                    var fadeProgress =
                            (boss.lazerTimer - boss.lazerActiveTime) / boss.lazerDisabledTime;
                    alpha = 1 - fadeProgress;
                }

                ctx.strokeStyle = "rgba(120, 0, 200," + alpha + ")";
                ctx.lineWidth = 6;

                for (var i = 0; i < bossLazers.length; i++) {
                    var lazer = bossLazers[i];
                    var angle = boss.lazerAngle + lazer.offset;

                    ctx.beginPath();
                    ctx.moveTo(boss.x, boss.y);
                    ctx.lineTo(
                            boss.x + Math.cos(angle) * 1000,
                            boss.y + Math.sin(angle) * 1000
                            );
                    ctx.stroke();
                }
            }







            // Dot class
            class Dot {
                constructor(x, y, radius, colour, arenaX, arenaY, arenaSize) {
                    this.x = x;
                    this.y = y;
                    this.radius = radius;
                    this.colour = colour;
                    this.arenaX = arenaX;
                    this.arenaY = arenaY;
                    this.arenaSize = arenaSize;
                    this.targetX = x;
                    this.targetY = y;
                    this.ease = 0.01;
                    this.baseEase = this.ease;
                    this.baseRadius = this.radius;
                    this.baseAttackMaxRadius = this.attackMaxRadius;

                    this.attackHitSet = new Set();

                    this.isAttacking = false;
                    this.attackRadius = 0;
                    this.attackMaxRadius = this.radius * (5 / 3);
                    this.attackColour = "yellow";
                    this.attackDamage = 1;
                    this.hasHitThisClick = false;



                }

                setTarget(x, y) {
                    this.targetX = x;
                    this.targetY = y;
                }
                applyUpgrades() {
                    this.ease = this.baseEase + speedLevel * 0.003;
                    this.radius = this.baseRadius + sizeLevel * 2;
                    this.attackMaxRadius = this.radius * (5 / 3) + rangeLevel * 5;
                }

                attack() {
                    // start attack
                    this.isAttacking = true;
                    this.attackRadius = this.radius;
                    this.attackMaxRadius = this.radius * (5 / 3);
                }

                update() {
                    // move toward target
                    this.x += (this.targetX - this.x) * this.ease;
                    this.y += (this.targetY - this.y) * this.ease;

                    // keep inside arena
                    var minX = this.arenaX + this.radius;
                    var minY = this.arenaY + this.radius;
                    var maxX = this.arenaX + this.arenaSize - this.radius;
                    var maxY = this.arenaY + this.arenaSize - this.radius;

                    if (this.x < minX + this.radius / 5)
                        this.x = minX + this.radius / 5;
                    if (this.y < minY + this.radius / 5)
                        this.y = minY + this.radius / 5;
                    if (this.x > maxX - this.radius / 5)
                        this.x = maxX - this.radius / 5;
                    if (this.y > maxY - this.radius / 5)
                        this.y = maxY - this.radius / 5;

                    // handle attack growth
                    if (this.isAttacking) {
                        this.attackRadius += (this.attackMaxRadius - this.attackRadius) * 0.2;

                        if (this.attackRadius >= this.attackMaxRadius * 0.99) {
                            this.isAttacking = false;
                        }
                    }
                }

                draw(ctx) {
                    // draw the dot
                    ctx.fillStyle = this.colour;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                    ctx.fill();

                    // draw attack if active
                    if (this.isAttacking) {
                        ctx.strokeStyle = this.attackColour;
                        ctx.lineWidth = 2;
                        ctx.beginPath();
                        ctx.arc(this.x, this.y, this.attackRadius, 0, Math.PI * 2);
                        ctx.stroke();
                    }
                }

                tryClick(mouseLeftDown) {

                    if (mouseLeftDown) { //if left mouse down then it attacks
                        this.attack();
                        this.isAttacking = true;
                        this.attackRadius = 0;
                        this.attackHitSet.clear();

                        return true;
                    }
                    return false;
                }
            }


            // Button class (simple)
            class Button { //for most of this button class https://www.youtube.com/watch?v=cGg6A-U9q3E i learned from watching this youtube video
                constructor(text, x, y, width, height, fillColour, textColour, xOffset, onClick) {
                    this.text = text;
                    this.x = x;
                    this.y = y;
                    this.width = width;
                    this.height = height;
                    this.fillColour = fillColour;
                    this.textColour = textColour;
                    this.xOffset = xOffset !== undefined ? xOffset : 0;
                    if (typeof onClick === "function") {
                        this.onClick = onClick;
                    } else {
                        this.onClick = function () { };
                    }
                    this.hover = false;
                }
                draw(ctx, mouseX, mouseY) {
                    ctx.fillStyle = this.fillColour;
                    ctx.fillRect(this.x, this.y, this.width, this.height);

                    ctx.fillStyle = this.textColour;
                    ctx.font = "25px Courier";
                    ctx.fillText(this.text, this.x + this.xOffset, this.y + this.height / 2 + 5);

                    if (mouseX > this.x && mouseX < this.x + this.width &&
                            mouseY > this.y && mouseY < this.y + this.height) {
                        this.hover = true;
                        ctx.strokeStyle = "yellow";
                        ctx.lineWidth = 3;
                        ctx.strokeRect(this.x, this.y, this.width, this.height);
                    } else {
                        this.hover = false;
                    }
                }
                handleClick(mouseX, mouseY, mouseLeftDown) { // handle mouse input
                    if (this.hover && mouseLeftDown) {
                        this.onClick();
                        return true;
                    }
                    return false;
                }
            }
            class SimpleUpgradeButton {
                constructor(text, x, y, onClick) {
                    this.text = text;
                    this.x = x;
                    this.y = y;
                    this.w = 220;
                    this.h = 60;
                    this.onClick = onClick;
                    this.hover = false;
                }

                draw(ctx, mx, my) {
                    this.hover =
                            mx > this.x && mx < this.x + this.w &&
                            my > this.y && my < this.y + this.h;

                    ctx.fillStyle = this.hover ? "#333" : "#222";
                    ctx.fillRect(this.x, this.y, this.w, this.h);

                    ctx.strokeStyle = "white";
                    ctx.lineWidth = 2;
                    ctx.strokeRect(this.x, this.y, this.w, this.h);

                    ctx.fillStyle = "white";
                    ctx.font = "20px Courier";
                    ctx.fillText(this.text, this.x + 15, this.y + 38);
                }

                handleClick(mx, my, click) {
                    if (this.hover && click) {
                        this.onClick();
                        return true;
                    }
                    return false;
                }
            }

            class Enemy {
                constructor(config) {
                    this.x = config.x;
                    this.y = config.y;

                    this.size = config.size;
                    this.health = config.health;
                    this.maxHealth = config.health;

                    this.damage = config.damage;
                    this.speed = config.speed;

                    this.colour = config.colour;
                    this.bulletSpeed = config.bulletSpeed;
                    this.shootCooldown = config.shootCooldown;
                    this.lastShotTime = Date.now();
                    this.lazerBaseAngle = 0;


                    this.weight = config.weight;

                    this.shardsDrop = config.shardsDrop;

                }

                update(targetX, targetY) {


                    // Move toward target
                    var dx = targetX - this.x;
                    var dy = targetY - this.y;
                    var dist = Math.sqrt(dx * dx + dy * dy);

                    if (dist > 0) {
                        this.x += (dx / dist) * this.speed;
                        this.y += (dy / dist) * this.speed;
                    }


                    // Shooting  
                    if (Date.now() - this.lastShotTime >= this.shootCooldown) {
                        this.shoot(targetX, targetY);
                        this.lastShotTime = Date.now();
                    }

                }

                shoot(tx, ty) {
                    var dx = tx - this.x;
                    var dy = ty - this.y;
                    var dist = Math.sqrt(dx * dx + dy * dy);

                    var vx = 0;
                    var vy = 0;
                    if (dist > 0) {
                        vx = (dx / dist) * this.bulletSpeed;
                        vy = (dy / dist) * this.bulletSpeed;
                    }

                    enemyProjectiles[enemyProjectiles.length] = {
                        x: this.x,
                        y: this.y,
                        vx: vx,
                        vy: vy,
                        radius: 5,
                        colour: "white"
                    };
                }

                draw(ctx) {
                    ctx.fillStyle = this.colour;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                    ctx.fill();

                    // health bar
                    ctx.fillStyle = "green";
                    ctx.fillRect(
                            this.x - this.size,
                            this.y - this.size - 8,
                            (this.health / this.maxHealth) * (this.size * 2),
                            4
                            );
                }
            }
            function updateProjectiles() {
                for (var i = enemyProjectiles.length - 1; i >= 0; i--) {
                    var projectileVar = enemyProjectiles[i];
                    projectileVar.x += projectileVar.vx;
                    projectileVar.y += projectileVar.vy;
                    if (projectileVar.x < arenaX || projectileVar.x > arenaX + arenaSize || projectileVar.y < arenaY || projectileVar.y > arenaY + arenaSize) {
                        enemyProjectiles.splice(i, 1);
                        continue;
                    }
                    if (circleCollision(projectileVar.x, projectileVar.y, projectileVar.radius, dot.x, dot.y, dot.radius)) {
                        playerHealth -= 1;
                        playerHealthBar.set(playerHealth);
                        enemyProjectiles.splice(i, 1);
                        if (playerHealth <= 0) {
                            gameScreen = "lose";
                        }
                    }
                }
            }
            function circleCollision(x1, y1, r1, x2, y2, r2) {
                var dx = x2 - x1;
                var dy = y2 - y1;
                var distance = Math.sqrt(dx * dx + dy * dy);
                return distance < r1 + r2;
            }

            function drawProjectiles() {
                for (var i = 0; i < enemyProjectiles.length; i++) {
                    var projectileVar = enemyProjectiles[i];
                    ctx.fillStyle = projectileVar.colour;
                    ctx.beginPath();
                    ctx.arc(projectileVar.x, projectileVar.y, projectileVar.radius, 0, Math.PI * 2);
                    ctx.fill();
                }
            }
            class Bar {
                constructor(x, y, width, height, maxValue, colour) {
                    this.x = x;
                    this.y = y;
                    this.w = width;
                    this.h = height;
                    this.maxValue = maxValue;
                    this.value = maxValue;
                    this.colour = colour;
                    this.borderColour = "rgba(255,255,255,0.8)";
                    this.bgColour = "rgba(0,0,0,0.3)";
                }

                set(value) {
                    this.value = Math.max(0, Math.min(value, this.maxValue));
                }

                draw(ctx) {
                    // background
                    ctx.fillStyle = this.bgColour;
                    ctx.fillRect(this.x, this.y, this.w, this.h);
                    // bar value
                    var percent = this.value / this.maxValue;
                    ctx.fillStyle = this.colour;
                    ctx.fillRect(this.x, this.y, this.w * percent, this.h);
                    // border
                    ctx.lineWidth = 3;
                    ctx.strokeStyle = this.borderColour;
                    ctx.strokeRect(this.x, this.y, this.w, this.h);
                }
            }







            var dot = new Dot(600, 350, 25, "white", arenaX, arenaY, arenaSize);
            var startButton = new Button("Start", 550, 360, 100, 50, "white", "black", 10, function () {
                gameScreen = "arena1";

                updateSelectableWave();
                wave = selectedWave;
                waveInProgress = false;
                lastWaveEnd = 0;

                playerMaxHealth = 10 + healthLevel * 2;
                playerHealth = playerMaxHealth;
                playerHealthBar.maxValue = playerMaxHealth;
                playerHealthBar.set(playerHealth);

                arenaOpen = false;
            });

            var backButton = new Button("Back", 10, 10, 75, 25, "white", "black", 10, function () {
                gameScreen = "menu";
                arenaOpen = false;
            });
            var upgradesBackButton = new Button("Back", 10, 10, 75, 25, "white", "black", 10, function () {
                if (!prestiged) {
                    gameScreen = "mainUpgradesUnprestiged";
                } else {
                    gameScreen = "mainUpgradesPrestiged";
                }
            });
            var upgradeButton = new Button("Upgrades", 540, 550, 100, 50, "white", "black", 10, function () {
                if (!prestiged) {
                    gameScreen = "mainUpgradesUnprestiged";
                } else {
                    gameScreen = "mainUpgradesPrestiged";
                }
            });

            var mainHealthUpgradesButton = new Button("Health", 180, 220, 260, 90, "white", "black", 70, function () {
                gameScreen = "healthUpgrades";
            });
            var mainDamageUpgradesButton = new Button("Damage", 470, 220, 260, 90, "white", "black", 65, function () {
                gameScreen = "damageUpgrades";
            });

            var mainSpeedUpgradesButton = new Button("Speed", 760, 220, 260, 90, "white", "black", 75, function () {
                gameScreen = "speedUpgrades";
            });

            var mainRangeUpgradesButton = new Button("Range", 180, 350, 260, 90, "white", "black", 75, function () {
                gameScreen = "rangeUpgrades";
            });

            var mainSizeUpgradesButton = new Button("Size", 470, 350, 260, 90, "white", "black", 85, function () {
                gameScreen = "sizeUpgrades";
            });

            var mainPrestigeUpgradesButton = new Button("Prestige", 760, 350, 260, 90, "white", "black", 55, function () {
                gameScreen = "prestigeUpgrades";
            });
            var prestigeButton = new Button("Prestige?", 760, 350, 260, 90, "white", "black", 55, function () {
                if (totalShardsCollected < 1000000)
                    return;

                prestiged = true;
                prestigePoints += Math.floor(totalShardsCollected / 1000000);

                // RESET PROGRESSION
                shards = 0;
                wave = 1;
                selectedWave = 1;

                damageLevel = 0;
                healthLevel = 0;
                speedLevel = 0;
                rangeLevel = 0;
                sizeLevel = 0;


                resetWaveState();
                gameScreen = "mainUpgradesPrestiged";
            });



            var losePlayAgainButton = new Button("Play Again", 500, 350, 200, 60, "white", "black", 25, function () {
                restartGame();
            });
            var loseUpgradesButton = new Button("Upgrades", 500, 420, 200, 60, "white", "black", 35, function () {
                if (!prestiged) {
                    gameScreen = "mainUpgradesUnprestiged";
                } else {
                    gameScreen = "mainUpgradesPrestiged";
                }
            });
            var loseSettingsButton = new Button("Settings", 500, 490, 200, 60, "white", "black", 35, function () {

            });
            var loseMenuButton = new Button("Menu", 500, 560, 200, 60, "white", "black", 55, function () {
                resetWaveState();
                gameScreen = "menu";
            });
            var waveDownButton = new Button("Wave -", 450, 470, 120, 40, "gray", "white", 20, function () {
                selectedWave--;
                updateSelectableWave();
            });

            var waveUpButton = new Button("Wave +", 600, 470, 120, 40, "gray", "white", 28, function () {
                selectedWave++;
                updateSelectableWave();
            });
            var dmgButtons = [
                new Button("DMG %", 350, 200, 150, 80, "white", "black", 25, function () {
                    buyDamageUpgrade("percent");
                }),
                new Button("FLAT", 525, 200, 150, 80, "white", "black", 35, function () {
                    buyDamageUpgrade("flat");
                }),
                new Button("MULTI", 700, 200, 150, 80, "white", "black", 25, function () {
                    buyDamageUpgrade("multi");
                })
            ];
            var damageUpgradeButton = new SimpleUpgradeButton("+1 Damage (100)", 490, 260, function () {
                if (shards < UPGRADE_COST)
                    return;

                shards -= UPGRADE_COST;
                dot.baseDamage += 1;
            });


            var healthUpgradeButton = new SimpleUpgradeButton("+1 Health (100)", 490, 260, function () {
                if (shards < UPGRADE_COST)
                    return;

                shards -= UPGRADE_COST;
                dot.maxHealth += 1;
                playerHealth += 1;
                playerHealthBar.set(dot.maxHealth);
            });




            var easingUpgradeButton = new SimpleUpgradeButton("+0.005 Speed (100)", 490, 260, function () {
                if (shards < UPGRADE_COST)
                    return;

                shards -= UPGRADE_COST;
                dot.baseEase += 0.005;
            });


            var sizeUpgradeButton = new SimpleUpgradeButton("-0.5 Size (100)", 490, 260, function () {
                if (shards < UPGRADE_COST)
                    return;

                shards -= UPGRADE_COST;
                dot.radius = Math.max(5, dot.radius - 0.5);
            });


            var rangeUpgradeButton = new SimpleUpgradeButton("+1 Range (100)", 490, 260, function () {
                if (shards < UPGRADE_COST)
                    return;

                shards -= UPGRADE_COST;
                dot.attackRadius += 1;
            });




            var playerHealthBar = new Bar(950, 25, 150, 10, playerMaxHealth, "green");
            function init() {
                canvas.addEventListener("mousemove", function (evt) {
                    var rect = canvas.getBoundingClientRect();
                    mouseXPos = evt.clientX - rect.left;
                    mouseYPos = evt.clientY - rect.top;
                });
                canvas.addEventListener("mousedown", function (evt) {
                    if (evt.button === 0) {
                        mouseLeftDown = true;
                    }
                });
                canvas.addEventListener("mouseup", function (evt) {
                    if (evt.button === 0) {
                        mouseLeftDown = false;
                    }
                });



            }

            function solidRect(x, y, w, h, colour) {
                ctx.fillStyle = colour;
                ctx.beginPath();
                ctx.fillRect(x, y, w, h);
            }
            function drawMediumText(text, x, y, colour) {
                ctx.fillStyle = colour;
                ctx.font = "25px Courier";
                ctx.fillText(text, x, y);
            }
            function drawLargeText(text, x, y, colour) {
                ctx.fillStyle = colour;
                ctx.font = "35px Courier";
                ctx.fillText(text, x, y);
            }
            function arenaRect(x, y, width, height, colour, thickness) {
                ctx.strokeStyle = colour;
                ctx.lineWidth = thickness;
                ctx.beginPath();
                ctx.strokeRect(x, y, width, height);
                ctx.stroke();
            }
            function restartGame() {
                // Reset player
                playerHealth = playerMaxHealth;
                playerHealthBar.set(playerMaxHealth);

                // Reset arena position
                dot.x = 600;
                dot.y = 350;
                dot.setTarget(600, 350);

                // Reset enemies + bullets
                enemies = [];
                enemyProjectiles = [];


                // wave = selectedWave; (arena mode will handle this cleanly)

                waveInProgress = false;
                waveBudget = 5;
                lastWaveEnd = 0;

                gameScreen = "arena1";
            }


            function spawnEnemy(baseConfig) {
                var spawnX = arenaX + baseConfig.size + Math.random() * (arenaSize - baseConfig.size * 2);
                var spawnY = arenaY + baseConfig.size + Math.random() * (arenaSize - baseConfig.size * 2);

                var enemyConfig = cloneEnemyConfig(baseConfig, spawnX, spawnY);
                enemies[enemies.length] = new Enemy(enemyConfig);
            }


            function cloneEnemyConfig(base, x, y) {
                return {
                    x: x,
                    y: y,
                    size: base.size,
                    health: base.health,
                    damage: base.damage,
                    speed: base.speed,
                    colour: base.colour,
                    bulletSpeed: base.bulletSpeed,
                    shootCooldown: base.shootRate,
                    weight: base.weight,
                    shardsDrop: base.shardsDrop
                };
            }

            var basicEnemy = {
                size: 20,
                health: 3,
                damage: 1,
                speed: 0.3,
                colour: "red",
                bulletSpeed: 2,
                shootRate: 2000,
                weight: 1,
                shardsDrop: 1
            };
            var sniperEnemy = {
                size: 18,
                health: 2,
                damage: 1.5,
                speed: 0.2,
                colour: "orange",
                bulletSpeed: 3,
                shootRate: 2500,
                weight: 2,
                shardsDrop: 1
            };
            var heavyEnemy = {
                size: 35,
                health: 5,
                damage: 1,
                speed: 0.1,
                colour: "blue",
                bulletSpeed: 1,
                shootRate: 2000,
                weight: 3,
                shardsDrop: 2
            };

            /**
             * Start wave function 
             */
            function startWave() {
                waveInProgress = true;
                waveBudget = calculateWaveBudget(wave);

                var budget = waveBudget;

                while (budget > 0) {
                    var spawned = false;

                    if (wave < 5) { // if the budget is enough then the enemy will spawn
                        if (budget >= basicEnemy.weight) {
                            spawnEnemy(basicEnemy);
                            budget -= basicEnemy.weight;
                            spawned = true;
                        }

                    } else if (wave < 10) {
                        if (budget >= sniperEnemy.weight) {
                            spawnEnemy(sniperEnemy);
                            budget -= sniperEnemy.weight;
                            spawned = true;
                        } else if (budget >= basicEnemy.weight) {
                            spawnEnemy(basicEnemy);
                            budget -= basicEnemy.weight;
                            spawned = true;
                        }

                    } else if (wave < 525 {
                        if (budget >= sniperEnemy.weight) {
                            spawnEnemy(sniperEnemy);
                            budget -= sniperEnemy.weight;
                            spawned = true;
                        }
                        if(budget >= heavyEnemy.weight){
                            spawnEnemy(heavyEnemy);
                            budget -= heavyEnemy.weight;
                            spawned = true;
                    }

                    if (!spawned) {
                        break;
                    }
                }
            }


            /**
             * reset wave state so when you lose or leave it resets to default 
             */
            function resetWaveState() {
                waveInProgress = false;
                lastWaveEnd = 0;
                waveBudget = 0;

                enemies = [];
                enemyProjectiles = [];
                bossProjectiles = [];
                bossLazers = [];

                boss = null;
                bossActive = false;
                finalBossDefeated = false;
            }

            function calculateWaveBudget(wave) {
                // Simple, predictable scaling
                return Math.min(4 + wave * 2, maxWaveBudget);
            }

            /**
             * sets the minimum to be at least 1 and the new highest will be 5 less than your highest
             */
            function getMaxSelectableWave() {
                var max = highestWaveReached - 5;

                if (max < 1)
                    max = 1;
                if (max > 20)
                    max = 20;

                return max;
            }

            function updateSelectableWave() {
                var minAllowed = 1;
                var maxAllowed = getMaxSelectableWave();

                selectedWave = Math.min(Math.max(selectedWave, minAllowed), maxAllowed);
            }

            function endGame() {
                if (wave >= 250 && totalPrestiges >= 1) {
                    gameScreen === "endGame";
                }
            }

//draw
            function draw() {
                var currentTime = Date.now(); //getting the time in milliseconds
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                if (gameScreen === "menu") {
                    drawLargeText("Welcome to Cursor Crusader", 350, 233, "white");
                    drawMediumText("Avoid projectiles and click on the enemies", 320, 260, "white");
                    startButton.draw(ctx, mouseXPos, mouseYPos);
                    if (startButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    // Buttons for choosing wave
                    waveDownButton.draw(ctx, mouseXPos, mouseYPos);
                    waveUpButton.draw(ctx, mouseXPos, mouseYPos);
                    if (waveDownButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (waveUpButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    upgradeButton.draw(ctx, mouseXPos, mouseYPos);
                    if (upgradeButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }


                    // Text showing the selected wave
                    ctx.fillStyle = "white";
                    ctx.font = "28px Courier";
                    ctx.fillText("Starting Wave: " + selectedWave, 460, 350);
                } else if (gameScreen === "arena1") {

                    if (!arenaOpen) {
                        arenaOpen = true;

                        dot.x = 600;
                        dot.y = 350;
                        dot.setTarget(600, 350);

                        enemies = [];
                        enemyProjectiles = [];
                        wave = selectedWave;

                        if (lastWaveEnd === 0) {
                            lastWaveEnd = Date.now();
                        }
                    }




                    if (wave === FINAL_BOSS_WAVE && !bossActive && !waveInProgress && boss === null && !finalBossDefeated) {
                        boss = new bossEnemy(600, 500, 60, 25, 0.5, 2.5, 8, 2000, 0.5, 0.25, 5, 0.001, 4, "purple", 200);
                        //x, y, radius, health, bulletDamage, bulletSpeed, bulletQuantity, bulletCooldown, bulletRotationSpeed, lazerDamage, lazerQuantity, lazerRotationSpeed, phases, colour, shardDrop
                        bossActive = true;
                        waveInProgress = true;
                    }



                    //Wave system
                    // Start normal wave
                    if (!waveInProgress && !bossActive && wave < FINAL_BOSS_WAVE && Date.now() - lastWaveEnd > waveCooldown) {
                        startWave();
                    }

                    if (waveInProgress && enemies.length === 0 && !bossActive) {
                        waveInProgress = false;
                        wave++;
                        lastWaveEnd = Date.now();
                    }
                    dot.applyUpgrades();

                    playerHealthBar.draw(ctx);

                    if (bossActive && boss !== null) {
                        boss.update();
                        boss.draw(ctx);
                        updateBossProjectiles();
                        updateBossLazers();

                        drawBossProjectiles();
                        drawBossLazers();


                        // Player damage to boss
                        if (dot.isAttacking && !dot.attackHitSet.has(boss) && circleCollision(dot.x, dot.y, dot.attackRadius, boss.x, boss.y, boss.radius)) {

                            boss.health -= dot.attackDamage;
                            dot.attackHitSet.add(boss);
                        }

                        
                        
                        // Boss death
                        if (boss.health <= 0) {
                            shards += boss.shardDrop;
                            totalShardsCollected += boss.shardDrop;

                            bossProjectiles = [];
                            bossLazers = [];

                            boss = null;
                            bossActive = false;
                            waveInProgress = false;

                            finalBossDefeated = true;
                            gameScreen = "endGame";
                        }









                    }
                    if (!bossActive) {// if the boss is not active then the enemies will spawn normally
                        for (var i = enemies.length - 1; i >= 0; i--) {
                            var enemyVar = enemies[i];
                            enemyVar.update(dot.x, dot.y);
                            enemyVar.draw(ctx);

                            if (dot.isAttacking && !dot.attackHitSet.has(enemyVar) && circleCollision(dot.x, dot.y, dot.attackRadius, enemyVar.x, enemyVar.y, enemyVar.size)) {

                                enemyVar.health -= dot.attackDamage;
                                dot.attackHitSet.add(enemyVar);

                                if (enemyVar.health <= 0) {
                                    var scale = Math.sqrt(wave) + (wave * 0.2);
                                    var gain = Math.floor(enemyVar.shardsDrop * scale);
                                    shards += gain;
                                    totalShardsCollected += gain;


                                    enemies.splice(i, 1);
                                }
                            }
                        }
                    }





                    // Bullets
                    updateProjectiles();
                    drawProjectiles();

                    arenaRect(arenaX, arenaY, arenaSize, arenaSize, "white", 10);
                    backButton.draw(ctx, mouseXPos, mouseYPos);
                    if (backButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (dot.tryClick(mouseLeftDown)) {
                        mouseLeftDown = false;
                    }


                    dot.setTarget(mouseXPos, mouseYPos);
                    dot.update();
                    dot.draw(ctx);
                    drawMediumText("Shards: " + shards, 950, 200, "cyan");
                    drawMediumText("Wave: " + wave, 950, 230, "white");
                } else if (gameScreen === "lose") {
                    drawLargeText("You Lose!", 520, 250, "red");
                    losePlayAgainButton.draw(ctx, mouseXPos, mouseYPos);
                    loseUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    loseSettingsButton.draw(ctx, mouseXPos, mouseYPos);
                    loseMenuButton.draw(ctx, mouseXPos, mouseYPos);
                    if (losePlayAgainButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown))
                        mouseLeftDown = false;
                    if (loseUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown))
                        mouseLeftDown = false;
                    if (loseSettingsButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown))
                        mouseLeftDown = false;
                    if (loseMenuButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown))
                        mouseLeftDown = false;
                } else if (gameScreen === "mainUpgradesUnprestiged") {

                    drawLargeText("Upgrades", 520, 80, "white");
                    drawMediumText("Shards: " + shards, 520, 130, "red");

                    mainDamageUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainHealthUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainSpeedUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainRangeUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainSizeUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    backButton.draw(ctx, mouseXPos, mouseYPos);
                    prestigeButton.draw(ctx, mouseXPos, mouseYPos);


                    if (mainDamageUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainHealthUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainSpeedUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainRangeUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainSizeUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (backButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (prestigeButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
//setting up the menud for upgrading
                } else if (gameScreen === "mainUpgradesPrestiged") {

                    drawLargeText("Upgrades", 520, 80, "white");
                    drawMediumText("Shards: " + shards, 520, 130, "red");

                    mainDamageUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainHealthUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainSpeedUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainRangeUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainSizeUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    mainPrestigeUpgradesButton.draw(ctx, mouseXPos, mouseYPos);
                    backButton.draw(ctx, mouseXPos, mouseYPos);
                    if (mainDamageUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (backButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainHealthUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainSpeedUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainRangeUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    if (mainSizeUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }

                    if (mainPrestigeUpgradesButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                } else if (gameScreen === "healthUpgrades") {
                    drawLargeText("Health Upgrades", 450, 100, "white");
                    healthUpgradeButton.draw(ctx, mouseXPos, mouseYPos);
                    if (healthUpgradeButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }

                    upgradesBackButton.draw(ctx, mouseXPos, mouseYPos);
                    if (upgradesBackButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }

                } else if (gameScreen === "damageUpgrades") {

                    drawLargeText("Damage Upgrades", 450, 100, "white");
                    damageUpgradeButton.draw(ctx, mouseXPos, mouseYPos);
                    if (damageUpgradeButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }



                    upgradesBackButton.draw(ctx, mouseXPos, mouseYPos);
                    if (upgradesBackButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                } else if (gameScreen === "speedUpgrades") {
                    easingUpgradeButton.draw(ctx, mouseXPos, mouseYPos);


                    if (easingUpgradeButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }

                    drawLargeText("Speed Upgrades", 450, 100, "white");
                    upgradesBackButton.draw(ctx, mouseXPos, mouseYPos);
                    if (upgradesBackButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                } else if (gameScreen === "rangeUpgrades") {
                    radiusUpgradeButton.draw(ctx, mouseXPos, mouseYPos);
                    if (radiusUpgradeButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }

                    drawLargeText("Range Upgrades", 450, 100, "white");
                    upgradesBackButton.draw(ctx, mouseXPos, mouseYPos);
                    if (upgradesBackButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                } else if (gameScreen === "sizeUpgrades") {
                    drawMediumText("Size Level: " + sizeLevel, 450, 230, "white");
                    drawLargeText("Size Upgrades", 450, 100, "white");
                    upgradesBackButton.draw(ctx, mouseXPos, mouseYPos);
                    if (upgradesBackButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                    }
                    //} else if (gameScreen === "prestigeUpgrades") {
                    //  drawMediumText("Prestige points: " + prestigePoints, 450, 230, "white");
                    // drawLargeText("Prestige Upgrades", 450, 100, "white");
                    // upgradesBackButton.draw(ctx, mouseXPos, mouseYPos);
                    // if (upgradesBackButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                    //     mouseLeftDown = false;
                    // }
                } else if (gameScreen === "endGame") {
                    drawLargeText("YOU WIN!", 520, 250, "lime");
                    drawMediumText("Final Wave: " + FINAL_BOSS_WAVE, 520, 300, "white");
                    drawMediumText("Total Shards: " + totalShardsCollected, 520, 340, "cyan");

                    loseMenuButton.draw(ctx, mouseXPos, mouseYPos);
                    if (loseMenuButton.handleClick(mouseXPos, mouseYPos, mouseLeftDown)) {
                        mouseLeftDown = false;
                        resetWaveState();
                        finalBossDefeated = false;
                        gameScreen = "menu";
                    }
                }







                window.requestAnimationFrame(draw);
            }

            init();
            draw();

        </script> 
    </body>
</html>
