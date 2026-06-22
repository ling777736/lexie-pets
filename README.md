# 乐写宠物

> <!DOCTYPE html>
> <html lang="zh-CN">
> <head>
>     <meta charset="UTF-8">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <title>乐写宠物 - 可爱虚拟养成</title>
>     <style>
>         * {
>             margin: 0;
>             padding: 0;
>             box-sizing: border-box;
>             font-family: "Microsoft YaHei", sans-serif;
>         }
>
>         body {
>             background-color: #FFF9E6;
>             min-height: 100vh;
>             display: flex;
>             flex-direction: column;
>             align-items: center;
>             padding: 20px;
>         }
>     
>         .title {
>             font-size: 36px;
>             color: #FFB74D;
>             margin: 20px 0;
>             text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
>         }
>     
>         .status-bar {
>             background-color: #FFE082;
>             padding: 15px 30px;
>             border-radius: 30px;
>             margin-bottom: 20px;
>             display: flex;
>             gap: 30px;
>             box-shadow: 0 4px 8px rgba(0,0,0,0.1);
>         }
>     
>         .status-item {
>             font-size: 18px;
>             font-weight: bold;
>             color: #F57C00;
>         }
>     
>         .container {
>             width: 100%;
>             max-width: 900px;
>             display: flex;
>             flex-direction: column;
>             align-items: center;
>             gap: 20px;
>         }
>     
>         .pets-container {
>             display: flex;
>             flex-wrap: wrap;
>             gap: 30px;
>             justify-content: center;
>         }
>     
>         .pet-card {
>             background: white;
>             width: 280px;
>             padding: 20px;
>             border-radius: 20px;
>             box-shadow: 0 6px 12px rgba(0,0,0,0.1);
>             text-align: center;
>             position: relative;
>         }
>     
>         .pet-avatar {
>             width: 180px;
>             height: 180px;
>             margin: 0 auto;
>             cursor: pointer;
>             transition: transform 0.2s;
>         }
>     
>         .pet-avatar:hover {
>             transform: scale(1.05);
>         }
>     
>         .pet-name {
>             font-size: 22px;
>             color: #FF9800;
>             margin: 10px 0;
>         }
>     
>         .pet-status {
>             font-size: 16px;
>             color: #666;
>             margin-bottom: 8px;
>         }
>     
>         .level-info {
>             font-size: 14px;
>             color: #7B5B14;
>             margin-bottom: 15px;
>             background: #FFF5D6;
>             padding: 6px 10px;
>             border-radius: 12px;
>             display: inline-block;
>         }
>     
>         .btn-group {
>             display: flex;
>             gap: 10px;
>             justify-content: center;
>             margin-bottom: 10px;
>         }
>     
>         .btn {
>             padding: 10px 20px;
>             border: none;
>             border-radius: 30px;
>             font-size: 16px;
>             font-weight: bold;
>             cursor: pointer;
>             transition: all 0.2s;
>         }
>     
>         .feed-btn {
>             background-color: #81C784;
>             color: white;
>         }
>     
>         .pet-btn {
>             background-color: #F06292;
>             color: white;
>         }
>     
>         .adopt-btn {
>             background-color: #FFB74D;
>             color: white;
>             margin-top: 10px;
>         }
>     
>         .shop-btn {
>             background-color: #7986CB;
>             color: white;
>             padding: 12px 30px;
>             font-size: 18px;
>         }
>     
>         .btn:hover {
>             opacity: 0.9;
>             transform: translateY(-2px);
>         }
>     
>         .btn:disabled {
>             background-color: #ccc;
>             cursor: not-allowed;
>             transform: none;
>         }
>     
>         .heart {
>             position: absolute;
>             font-size: 24px;
>             color: #FF4081;
>             animation: heart-float 1s ease-out forwards;
>             pointer-events: none;
>         }
>     
>         @keyframes heart-float {
>             0% { opacity: 1; transform: translateY(0); }
>             100% { opacity: 0; transform: translateY(-50px); }
>         }
>     
>         .speech-bubble {
>             position: absolute;
>             top: -10px;
>             left: 50%;
>             transform: translateX(-50%);
>             background: white;
>             padding: 8px 15px;
>             border-radius: 20px;
>             box-shadow: 0 2px 5px rgba(0,0,0,0.2);
>             font-size: 14px;
>             color: #555;
>             animation: fade-out 2s forwards;
>             white-space: nowrap;
>             z-index: 10;
>         }
>     
>         @keyframes fade-out {
>             0% { opacity: 1; }
>             80% { opacity: 1; }
>             100% { opacity: 0; }
>         }
>     
>         .level-up {
>             position: absolute;
>             top: 50%;
>             left: 50%;
>             transform: translate(-50%, -50%);
>             background: #FFE082;
>             color: #E65100;
>             padding: 12px 24px;
>             border-radius: 20px;
>             font-weight: bold;
>             box-shadow: 0 4px 10px rgba(0,0,0,0.2);
>             animation: levelUpAni 1.5s forwards;
>             z-index: 20;
>         }
>     
>         @keyframes levelUpAni {
>             0% { opacity: 0; scale: 0.5; }
>             50% { opacity: 1; scale: 1.1; }
>             100% { opacity: 0; scale: 1; }
>         }
>     
>         .modal {
>             position: fixed;
>             top: 0;
>             left: 0;
>             width: 100%;
>             height: 100%;
>             background: rgba(0,0,0,0.3);
>             display: none;
>             justify-content: center;
>             align-items: center;
>             z-index: 999;
>         }
>     
>         .modal-content {
>             background: white;
>             padding: 30px;
>             border-radius: 20px;
>             text-align: center;
>             width: 90%;
>             max-width: 400px;
>         }
>     
>         .modal-title {
>             font-size: 24px;
>             color: #FF9800;
>             margin-bottom: 20px;
>         }
>     
>         .shop-item {
>             display: flex;
>             justify-content: space-between;
>             align-items: center;
>             padding: 15px;
>             border-bottom: 1px solid #eee;
>         }
>     
>         .close-modal {
>             margin-top: 20px;
>             background: #FFB74D;
>             color: white;
>         }
>     
>         .select-pet-modal .pet-options {
>             display: flex;
>             gap: 15px;
>             justify-content: center;
>             margin: 20px 0;
>             flex-wrap: wrap;
>         }
>     
>         .pet-option {
>             text-align: center;
>             cursor: pointer;
>             padding: 10px;
>             border-radius: 12px;
>             transition: background 0.2s;
>         }
>     
>         .pet-option:hover {
>             background: #FFF5D6;
>         }
>     
>         .pet-option svg {
>             width: 80px;
>             height: 80px;
>         }
>     </style>
> </head>
> <body>
>     <h1 class="title">🐾 乐写宠物 🐾</h1>
>
>     <div class="status-bar">
>         <div class="status-item">金币：<span id="gold">200</span></div>
>         <div class="status-item">粮食：<span id="food">0</span>袋</div>
>         <div class="status-item">宠物数量：<span id="petCount">0</span>/2</div>
>     </div>
>     
>     <div class="container">
>         <div class="pets-container" id="petsContainer"></div>
>         <button class="btn adopt-btn" id="adoptNewPet" style="display:none;">领养第二只宠物（300金币）</button>
>         <button class="btn shop-btn" id="openShop">🛒 打开商城</button>
>     </div>
>     
>     <!-- 商城 -->
>     <div class="modal" id="shopModal">
>         <div class="modal-content">
>             <h2 class="modal-title">宠物商城</h2>
>             <div class="shop-item">
>                 <span>宠物粮食（20金币/袋）</span>
>                 <button class="btn" id="buyFood">购买</button>
>             </div>
>             <div class="shop-item">
>                 <span>宠物药物（20金币/瓶）</span>
>                 <button class="btn" id="buyMedicine">购买</button>
>             </div>
>             <button class="btn close-modal" id="closeShop">关闭</button>
>         </div>
>     </div>
>     
>     <!-- 首次选宠 -->
>     <div class="modal select-pet-modal" id="selectPetModal">
>         <div class="modal-content">
>             <h2 class="modal-title">选择你的第一只宠物</h2>
>             <div class="pet-options" id="petOptions"></div>
>             <button class="btn close-modal" id="closeSelectModal">取消</button>
>         </div>
>     </div>
>     
>     <script>
>         let gameData = {
>             gold: 200,
>             food: 0,
>             pets: [],
>             maxPets: 2
>         };
>     
>         const petTypes = [
>             { name: "布丁猫", emoji: "🐱", color: "#FFD3B6" },
>             { name: "奶黄狗", emoji: "🐶", color: "#FFEAA7" },
>             { name: "团子兔", emoji: "🐰", color: "#DDA0DD" },
>             { name: "圆圆猪", emoji: "🐷", color: "#FFB6C1" }
>         ];
>     
>         const thanksTexts = [
>             "谢谢你呀～🥰", "主人真好！", "超开心的！", "爱你哟～❤️", "蹭蹭蹭～", "太幸福啦！"
>         ];
>     
>         const goldEl = document.getElementById('gold');
>         const foodEl = document.getElementById('food');
>         const petCountEl = document.getElementById('petCount');
>         const petsContainer = document.getElementById('petsContainer');
>         const adoptNewPetBtn = document.getElementById('adoptNewPet');
>         const shopModal = document.getElementById('shopModal');
>         const selectPetModal = document.getElementById('selectPetModal');
>         const petOptionsEl = document.getElementById('petOptions');
>     
>         // 初始化
>         function initGame() {
>             updateUI();
>             showFirstAdoption();
>             startRandomEvents();
>         }
>     
>         // 界面刷新
>         function updateUI() {
>             goldEl.textContent = gameData.gold;
>             foodEl.textContent = gameData.food;
>             petCountEl.textContent = gameData.pets.length;
>     
>             petsContainer.innerHTML = '';
>             gameData.pets.forEach((pet, i) => {
>                 petsContainer.innerHTML += createPetCard(pet, i);
>             });
>     
>             if (gameData.pets.length === 1) {
>                 adoptNewPetBtn.style.display = 'block';
>                 adoptNewPetBtn.disabled = gameData.gold < 300;
>             } else {
>                 adoptNewPetBtn.style.display = 'none';
>             }
>         }
>     
>         // 宠物卡片
>         function createPetCard(pet, index) {
>             return `
>                 <div class="pet-card">
>                     <div class="pet-avatar" onclick="sayThanks(${index})" style="filter: ${pet.isSick ? 'grayscale(60%)' : 'none'}">
>                         <svg viewBox="0 0 100 100" width="180" height="180">
>                             <circle cx="50" cy="50" r="45" fill="${pet.color}"/>
>                             <text x="50" y="65" font-size: 50" text-anchor="middle">${pet.emoji}</text>
>                         </svg>
>                     </div>
>                     <h3 class="pet-name">${pet.name}</h3>
>                     <p class="pet-status">${pet.isSick ? '😷 生病了，快喂药！' : '😊 健康快乐'}</p>
>                     <div class="level-info">
>                         Lv.${pet.level} | 喂食${pet.feedCount}/${pet.needFeed} | 抚摸${pet.petCount}/${pet.needPet}
>                     </div>
>                     <div class="btn-group">
>                         <button class="btn feed-btn" onclick="feedPet(${index})" ${pet.isSick ? 'disabled' : ''}>🍚 喂养</button>
>                         <button class="btn pet-btn" onclick="petPet(${index})" ${pet.isSick ? 'disabled' : ''}>❤️ 抚摸</button>
>                     </div>
>                     ${pet.isSick ? `<button class="btn" onclick="curePet(${index})">💊 喂药(20金币)</button>` : ''}
>                 </div>
>             `;
>         }
>     
>         // 首次领养选择界面
>         function showFirstAdoption() {
>             if (gameData.pets.length > 0) return;
>             petOptionsEl.innerHTML = '';
>             petTypes.forEach((pet, i) => {
>                 petOptionsEl.innerHTML += `
>                     <div class="pet-option" onclick="chooseFirstPet(${i})">
>                         <svg viewBox="0 0 100 100" width="80" height="80">
>                             <circle cx="50" cy="50" r="45" fill="${pet.color}"/>
>                             <text x="50" y="65" font-size="40" text-anchor="middle">${pet.emoji}</text>
>                         </svg>
>                         <div>${pet.name}</div>
>                     </div>
>                 `;
>             });
>             selectPetModal.style.display = 'flex';
>         }
>     
>         // 选择第一只宠物
>         function chooseFirstPet(index) {
>             const base = petTypes[index];
>             gameData.pets.push({
>                 ...base,
>                 isSick: false,
>                 level: 1,
>                 feedCount: 0,
>                 petCount: 0,
>                 needFeed: 5,
>                 needPet: 20
>             });
>             selectPetModal.style.display = 'none';
>             updateUI();
>         }
>     
>         // 领养第二只
>         function adoptSecondPet() {
>             if (gameData.pets.length >= 2) return alert('最多只能领养2只宠物');
>             if (gameData.gold < 300) return alert('需要300金币才能领养第二只');
>             
>             gameData.gold -= 300;
>             const randomPet = petTypes[Math.floor(Math.random() * petTypes.length)];
>             gameData.pets.push({
>                 ...randomPet,
>                 isSick: false,
>                 level: 1,
>                 feedCount: 0,
>                 petCount: 0,
>                 needFeed: 5,
>                 needPet: 20
>             });
>             updateUI();
>         }
>     
>         // 喂养（必须有粮食）
>         function feedPet(index) {
>             const pet = gameData.pets[index];
>             if (pet.isSick) return;
>             if (gameData.food <= 0) {
>                 alert('未购买粮食，请前往商城购买');
>                 return;
>             }
>     
>             gameData.food--;
>             pet.feedCount++;
>             gameData.gold += 20;
>             createHeartEffect(index);
>             checkLevelUp(index);
>             updateUI();
>         }
>     
>         // 抚摸
>         function petPet(index) {
>             const pet = gameData.pets[index];
>             if (pet.isSick) return;
>             
>             pet.petCount++;
>             gameData.gold += 10;
>             createHeartEffect(index);
>             checkLevelUp(index);
>             updateUI();
>         }
>     
>         // 升级：喂食 AND 抚摸 同时达标
>         function checkLevelUp(index) {
>             const pet = gameData.pets[index];
>             if (pet.feedCount >= pet.needFeed && pet.petCount >= pet.needPet) {
>                 pet.level++;
>                 const reward = Math.min(30 * pet.level, 250);
>                 gameData.gold += reward;
>     
>                 pet.feedCount = 0;
>                 pet.petCount = 0;
>                 pet.needFeed = Math.floor(pet.needFeed * 1.4);
>                 pet.needPet = Math.floor(pet.needPet * 1.4);
>     
>                 showLevelUp(index, reward);
>             }
>         }
>     
>         // 升级动画
>         function showLevelUp(index, reward) {
>             const card = document.querySelectorAll('.pet-card')[index];
>             const tip = document.createElement('div');
>             tip.className = 'level-up';
>             tip.textContent = `升级啦！Lv.${gameData.pets[index].level} +${reward}金币`;
>             card.appendChild(tip);
>             setTimeout(() => tip.remove(), 1500);
>         }
>     
>         // 爱心特效
>         function createHeartEffect(petIndex) {
>             const petCard = document.querySelectorAll('.pet-card')[petIndex];
>             const heart = document.createElement('div');
>             heart.className = 'heart';
>             heart.textContent = '❤️';
>             heart.style.left = Math.random() * 80 + 10 + '%';
>             petCard.appendChild(heart);
>             setTimeout(() => heart.remove(), 1000);
>         }
>     
>         // 点击说话
>         function sayThanks(index) {
>             const petCard = document.querySelectorAll('.pet-card')[index];
>             const bubble = document.createElement('div');
>             bubble.className = 'speech-bubble';
>             bubble.textContent = thanksTexts[Math.floor(Math.random() * thanksTexts.length)];
>             petCard.appendChild(bubble);
>             setTimeout(() => bubble.remove(), 2000);
>         }
>     
>         // 治病
>         function curePet(index) {
>             if (gameData.gold < 20) return alert('金币不足');
>             gameData.gold -= 20;
>             gameData.pets[index].isSick = false;
>             updateUI();
>         }
>     
>         // 随机生病 5~10分钟
>         function startRandomEvents() {
>             const min = 5 * 60 * 1000;
>             const max = 10 * 60 * 1000;
>             setInterval(() => {
>                 gameData.pets.forEach(pet => {
>                     if (!pet.isSick && Math.random() < 0.4) {
>                         pet.isSick = true;
>                     }
>                 });
>                 updateUI();
>             }, min + Math.random() * (max - min));
>         }
>     
>         // 商城
>         document.getElementById('openShop').onclick = () => shopModal.style.display = 'flex';
>         document.getElementById('closeShop').onclick = () => shopModal.style.display = 'none';
>         document.getElementById('buyFood').onclick = () => {
>             if (gameData.gold >= 20) {
>                 gameData.gold -= 20;
>                 gameData.food += 1;
>                 alert('购买粮食成功！');
>                 updateUI();
>             } else alert('金币不足');
>         };
>         document.getElementById('buyMedicine').onclick = () => {
>             if (gameData.gold >= 20) {
>                 gameData.gold -= 20;
>                 alert('购买药物成功！');
>                 updateUI();
>             } else alert('金币不足');
>         };
>     
>         document.getElementById('closeSelectModal').onclick = () => selectPetModal.style.display = 'none';
>         adoptNewPetBtn.onclick = adoptSecondPet;
>     
>         window.onload = initGame;
>     </script>
> </body>
> </html>
