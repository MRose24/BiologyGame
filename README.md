<html lang="th">
<head>
    <meta charset="UTF-8">
    <title>เกมการให้และรับเลือด วิชาชีววิทยา</title>
    <style>
        body {
            font-family: 'Tahoma', sans-serif;
            background-color: #f5f5fb;
            margin: 0; padding: 0;
        }
        .container {
            width: 90%;
            max-width: 500px;
            margin: 32px auto;
            background: white;
            border-radius: 18px;
            box-shadow: 0 2px 16px rgba(0,0,0,0.06);
            padding: 28px 18px 32px 18px;
            min-height: 500px;
        }
        h1 {
            color: #5c32af;
            text-align: center;
            margin-bottom: 24px;
        }
        .btn {
            color: white;
            background: #6c47c4;
            border: none;
            border-radius: 9px;
            padding: 11px 25px;
            font-size: 18px;
            margin: 7px;
            cursor: pointer;
            transition: background 0.2s;
        }
        .btn:active, .btn.selected { background: #b45aff; }
        .scenarios { display: flex; justify-content: center; margin-bottom: 28px; }
        .scenario-btn {
            background: #baffc9;
            color: #333;
            border: none;
            border-radius: 9px;
            padding: 13px 18px;
            font-size: 16px;
            margin: 0 6px;
            cursor: pointer;
        }
        .scenario-btn.locked {
            background: #e0e0e0;
            color: #aaa;
            cursor: not-allowed;
        }
        .avatar-row {
            display: flex; align-items: center; justify-content: center; gap: 16px; margin-bottom: 18px;
        }
        .avatar {
            display: flex; flex-direction: column; align-items: center;
        }
        .avatar-img {
            width: 64px; height: 64px;
            border-radius: 50%;
            background: #e5eafc;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 36px;
        }
        .blood-type {
            background: #fc8686;
            color: #fff;
            font-size: 17px;
            font-weight: bold;
            padding: 0px 10px;
            border-radius: 8px;
            margin-top: 5px;
        }
        .nickname { font-size: 15px; color: #6e43b3; margin-top: 4px;}
        .blood-packs { display: flex; flex-wrap: wrap; justify-content: center; gap: 12px; margin: 18px 0 10px 0;}
        .blood-pack {
            background: #e04e4e;
            border-radius: 11px;
            width: 65px; height: 88px;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            color: #fff; font-size: 24px;
            cursor: pointer; border: 4px solid transparent;
            transition: border 0.15s;
            box-shadow: 0 2px 7px rgba(220,98,135,0.17);
            position: relative;
        }
        .blood-pack.selected { border: 4px solid #f9c24b;}
        .blood-pack-label {
            font-size: 17px;
            margin-top: 6px;
            background: rgba(255,255,255,0.88);
            color: #d34c53;
            border-radius: 7px;
            padding: 1px 11px 0 11px;
        }
        .result {
            text-align: center; font-size: 1.25em; margin-top: 12px; margin-bottom: 6px;
        }
        .next-btn { margin: 15px auto 0 auto; display: block;}
        .fade-in { animation: fadeIn 0.4s;}
        .timer {
            text-align: right;
            font-size: 1.05em;
            color: #533db7;
            font-weight: bold;
            margin-bottom: 5px;
        }
        .share-btn {
            background: #4a90e2;
            color: #fff;
            border: none;
            border-radius: 7px;
            padding: 10px 18px;
            font-size: 18px;
            cursor: pointer;
            margin: 7px 0 0 0;
        }
        .username-box {
            margin: 0 auto 24px auto;
            text-align: center;
        }
        .username-box input {
            border: 1.4px solid #d4cef5;
            border-radius: 7px;
            padding: 10px 13px;
            font-size: 18px;
            width: 70%;
        }
    </style>
</head>
<body>
    <div class="container" id="main-container">
        <h1>เกมการให้และรับเลือด 🩸</h1>
        <div class="username-box" id="username-box">
            <div style="font-size:19px; color:#4a3299; margin-bottom: 10px;">
                ใส่ชื่อของคุณเพื่อเริ่มเกม
            </div>
            <input type="text" placeholder="ระบุชื่อ (ภาษาไทยหรืออังกฤษ)" id="username-input" maxlength="24">
            <div style="margin-top:15px;">
                <button class="btn" onclick="userSubmitName()">เริ่มเกม</button>
            </div>
        </div>
        <div id="game-ui" style="display:none;">
            <div class="timer" id="timer">เวลา: 0:00</div>
            <div class="scenarios">
                <button class="scenario-btn" id="btn-lab">🏥 ห้องปฏิบัติการ</button>
                <button class="scenario-btn locked" id="btn-delivery">👶 ห้องคลอด</button>
            </div>
            <div id="game-area"></div>
        </div>
    </div>
    <script>
    const nicknames = [
        'มะลิ','ใบชา','น้ำหวาน','ต้นข้าว','ปีโป้','ฟ้าใส','บัวลอย','ไข่มุก',
        'ปังปอนด์','ลูกปลา','น้ำตาล','ภูผา','เปียโน','พีช','สนุก','ขนมปัง'
    ];
    const avatars = ['🐰','🐼','🐻','🐱','🦊','🐶','🦁','🐮','🐷','🐸','🦄','🐯','🐨','🦝', '🐵'];
    const bloodTypes = ['A','B','AB','O'];
    const canDonate = {
        'O': ['O','A','B','AB'],
        'A': ['A','AB'],
        'B': ['B','AB'],
        'AB': ['AB'],
    };
    const possibleChildBlood = {
        'A,A': ['A','O'],
        'A,B': ['A','B','AB','O'],
        'A,AB': ['A','B','AB'],
        'A,O': ['A','O'],
        'B,B': ['B','O'],
        'B,AB': ['A','B','AB'],
        'B,O': ['B','O'],
        'AB,AB': ['A','B','AB'],
        'AB,O': ['A','B'],
        'O,O': ['O'],
    };
    function allParentCombinations() {
        let combos = [];
        for (let i = 0; i < bloodTypes.length; i++) {
            for (let j = i; j < bloodTypes.length; j++) {
                let a = bloodTypes[i], b = bloodTypes[j];
                if(possibleChildBlood.hasOwnProperty(`${a},${b}`))
                    combos.push([a,b]);
            }
        }
        return combos;
    }

    // --- เพิ่มโจทย์ห้องปฏิบัติการ 10 ข้อ (สุ่ม receiverBlood + ซ้ำได้ + สลับ) ---
    function getLabQuestions10() {
        let result = [];
        for (let i = 0; i < 10; i++) {
            // สุ่มหมู่เลือดผู้รับ 1 อัน
            let receiverBlood = bloodTypes[Math.floor(Math.random() * bloodTypes.length)];
            // ตอบถูกต้องคือ ทุกกลุ่มที่สามารถให้ receiver นี้ได้
            let correctDonors = [];
            for (let donor of bloodTypes) {
                if (canDonate[donor].includes(receiverBlood)) correctDonors.push(donor);
            }
            result.push({
                receiverBlood: receiverBlood,
                correctDonors: correctDonors
            });
        }
        return shuffle(result);
    }

    let state = {
        scenario: 'lab',
        labQuestions: [],
        labLevel: 0,
        deliveryUnlocked: false,
        deliveryLevel: 0,
        deliveryQuestions: [],
        totalLabQ: 10,
        totalDeliveryQ: allParentCombinations().length,
        parentCombos: [],
        currentCombo: null,
        avatarPool: [],
        nicknamePool: [],
        userName: '',
        startTime: 0,
        endTime: 0,
        timerRunning: false,
        timerInterval: null,
        elapsedSec: 0,
        finishedLab: false,
        finishedDelivery: false,
    };

    function resetPools() {
        state.avatarPool = shuffle([...avatars]);
        state.nicknamePool = shuffle([...nicknames]);
        state.parentCombos = shuffle(allParentCombinations());
    }

    function shuffle(a){
        let arr = a.slice();
        for(let i=arr.length-1;i>0;i--){
            const j = Math.floor(Math.random()*(i+1));
            [arr[i],arr[j]]=[arr[j],arr[i]];
        }
        return arr;
    }
    function pad(num) {
        return num < 10 ? '0'+num : num;
    }
    function formatTime(secs) {
        return Math.floor(secs/60) + ':' + pad(secs%60);
    }
    function userSubmitName() {
        let name = document.getElementById('username-input').value.trim();
        if(!name) {
            alert('กรุณาระบุชื่อ');
            return;
        }
        state.userName = name;
        document.getElementById('username-box').style.display = "none";
        document.getElementById('game-ui').style.display = "";
        startLabScenario(true);
        state.startTime = Date.now();
        state.endTime = 0;
        state.elapsedSec = 0;
        state.finishedLab = false;
        state.finishedDelivery = false;
        startTimer();
    }
    function startTimer() {
        state.timerRunning = true;
        updateTimer();
        state.timerInterval = setInterval(function() {
            if(state.timerRunning) {
                state.elapsedSec = Math.floor((Date.now() - state.startTime)/1000);
                updateTimer();
            }
        }, 500);
    }
    function stopTimer() {
        state.timerRunning = false;
        clearInterval(state.timerInterval);
        updateTimer();
    }
    function updateTimer() {
        let timerEl = document.getElementById('timer');
        if(timerEl) timerEl.textContent = 'เวลา: ' + formatTime(state.elapsedSec);
    }

    function startLabScenario(isStart = false) {
        state.scenario = 'lab';
        state.labLevel = 0;
        state.finishedLab = false;
        document.getElementById("btn-lab").classList.add('selected');
        document.getElementById("btn-delivery").classList.remove('selected');
        resetPools();
        state.labQuestions = getLabQuestions10();
        renderLabLevel();
    }
    function startDeliveryScenario() {
        state.scenario = 'delivery';
        state.deliveryLevel = 0;
        state.finishedDelivery = false;
        document.getElementById("btn-delivery").classList.add('selected');
        document.getElementById("btn-lab").classList.remove('selected');
        resetPools();
        state.deliveryQuestions = shuffle(state.parentCombos);
        renderDeliveryLevel();
    }
    // ---- ปรับห้องปฏิบัติการ: เลือกหมู่ผู้ให้ได้หลายข้อ ----
    function renderLabLevel() {
        let qN = state.labLevel;
        if (qN >= state.totalLabQ) {
            state.finishedLab = true;
            state.deliveryUnlocked = true;
            document.querySelector("#btn-delivery").classList.remove('locked');
            document.getElementById("btn-lab").classList.add('selected');
            document.querySelector("#game-area").innerHTML = `
                <div class="result fade-in">✅ คุณผ่านการให้และรับเลือดจนครบทุกหมู่!<br>สามารถเข้าเล่น <b>ห้องคลอด</b> ได้แล้วค่ะ 🎉</div>
            `;
            return;
        }
        let q = state.labQuestions[qN];
        // show UI (โจทย์ : ระบุหมู่เลือดของผู้ให้ทั้งหมดที่ให้ผู้รับนี้ได้)
        let avatarA = state.avatarPool.length ? state.avatarPool.pop() : avatars[Math.floor(Math.random()*avatars.length)];
        let avatarB = state.avatarPool.length ? state.avatarPool.pop() : avatars[Math.floor(Math.random()*avatars.length)];
        let nickA = state.nicknamePool.length ? state.nicknamePool.pop() : nicknames[Math.floor(Math.random()*nicknames.length)];
        let nickB = state.nicknamePool.length ? state.nicknamePool.pop() : nicknames[Math.floor(Math.random()*nicknames.length)];
        document.querySelector("#game-area").innerHTML = `
        <div class="fade-in">
            <div style="text-align:center; color:#5a299c; margin-bottom:16px;">
                🏥 สถานการณ์ <b>ห้องปฏิบัติการ</b>: ข้อที่ ${state.labLevel+1} / ${state.totalLabQ}
            </div>
            <div class="avatar-row">
                <div class="avatar">
                    <div class="avatar-img">${avatarA}</div>
                    <div class="blood-type">?</div>
                    <div class="nickname">${nickA}</div>
                    <div style="font-size:13px;color:#888; margin-top:2px;">ผู้ให้เลือด</div>
                </div>
                <span style="font-size:48px;">➡️</span>
                <div class="avatar">
                    <div class="avatar-img">${avatarB}</div>
                    <div class="blood-type">${q.receiverBlood}</div>
                    <div class="nickname">${nickB}</div>
                    <div style="font-size:13px;color:#888; margin-top:2px;">ผู้รับเลือด</div>
                </div>
            </div>
            <div style="text-align:center; color:#642bf1; font-size:18px;margin-bottom:11px;">
                <b>${nickB}</b> (หมู่เลือด <b>${q.receiverBlood}</b>) ต้องการเลือด<br>
                เลือกหมู่เลือดของ <b>ผู้ให้เลือด</b> ที่ให้ได้ (เลือกได้มากกว่า 1 อัน)
            </div>
            <div class="blood-packs" id="blood-packs">
                ${bloodTypes.map(type=>`
                <div class="blood-pack" data-type="${type}">
                    <span>🩸</span>
                    <span class="blood-pack-label">${type}</span>
                </div>`).join('')}
            </div>
            <div id="lab-result" class="result"></div>
        </div>
        `;
        let selected = [];
        document.querySelectorAll('.blood-pack').forEach(pack=>{
            pack.onclick = ()=>{
                let t = pack.getAttribute('data-type');
                pack.classList.toggle('selected');
                if (selected.includes(t)) {
                    selected = selected.filter(x => x!==t);
                } else {
                    selected.push(t);
                }
            };
        });
        document.getElementById('lab-result').innerHTML = `
            <button class="btn next-btn" onclick="checkLabMultiAnswer('${q.correctDonors.join(',')}');">ตรวจคำตอบ</button>
        `;
    }

    function checkLabMultiAnswer(ansStr) {
        let correctTypes = ansStr.split(',');
        let selectedTypes = Array.from(document.querySelectorAll('.blood-pack.selected')).map(x=>x.getAttribute('data-type')).sort();
        let correctSorted = correctTypes.slice().sort();
        if(selectedTypes.length==0){
            document.getElementById('lab-result').innerHTML =
                `<span style="color:#d0453b;">โปรดเลือกอย่างน้อย 1 หมู่เลือดก่อนค่ะ</span>
                <button class="btn next-btn" onclick="checkLabMultiAnswer('${ansStr}');">ตรวจคำตอบ</button>`;
            return;
        }
        if(selectedTypes.join(',') === correctSorted.join(',')){
            document.getElementById('lab-result').innerHTML =
                `<span style="color:#22ab60;">✅ ถูกต้อง!</span> <button class="btn next-btn" onclick="nextLabLevel();">ไปด่านถัดไป</button>`;
        }else{
            document.getElementById('lab-result').innerHTML =
                `<span style="color:#d0453b;">❌ ยังไม่ถูกต้อง โปรดลองใหม่ค่ะ</span>
                <button class="btn next-btn" onclick="checkLabMultiAnswer('${ansStr}');">ตรวจคำตอบ</button>`;
        }
    }
    function nextLabLevel() {
        state.labLevel++;
        renderLabLevel();
    }
    function renderDeliveryLevel() {
        let qN = state.deliveryLevel;
        if (qN >= state.totalDeliveryQ) {
            state.finishedDelivery = true;
            state.endTime = Date.now();
            stopTimer();
            showResultSummary();
            return;
        }
        if(!state.currentCombo) state.currentCombo = state.deliveryQuestions[qN] || ['A','A'];
        let [dadBlood, momBlood] = state.currentCombo;
        let dadAvatar = state.avatarPool.length ? state.avatarPool.pop() : avatars[Math.floor(Math.random()*avatars.length)];
        let momAvatar = state.avatarPool.length ? state.avatarPool.pop() : avatars[Math.floor(Math.random()*avatars.length)];
        let kidAvatar = avatars[Math.floor(Math.random()*avatars.length)];
        let dadNick = state.nicknamePool.length ? state.nicknamePool.pop() : nicknames[Math.floor(Math.random()*nicknames.length)];
        let momNick = state.nicknamePool.length ? state.nicknamePool.pop() : nicknames[Math.floor(Math.random()*nicknames.length)];
        let kidNick = state.nicknamePool.length ? state.nicknamePool.pop() : nicknames[Math.floor(Math.random()*nicknames.length)];
        document.querySelector("#game-area").innerHTML = `
        <div class="fade-in">
            <div style="text-align:center; color:#3d6a95; margin-bottom:16px;">
                👶 สถานการณ์ <b>ห้องคลอด</b>: ข้อที่ ${state.deliveryLevel+1} / ${state.totalDeliveryQ}
            </div>
            <div class="avatar-row" style="justify-content: space-around;">
                <div class="avatar">
                    <div class="avatar-img">${dadAvatar}</div>
                    <div class="blood-type">${dadBlood}</div>
                    <div class="nickname">${dadNick}<div style="font-size:12px;color:#999;">คุณพ่อ</div></div>
                </div>
                <div class="avatar">
                    <div class="avatar-img">${momAvatar}</div>
                    <div class="blood-type">${momBlood}</div>
                    <div class="nickname">${momNick}<div style="font-size:12px;color:#999;">คุณแม่</div></div>
                </div>
            </div>
            <div style="text-align:center; color:#6235ab; font-size:18px;margin-bottom:8px;">
                <b>ลูกของ ${dadNick} กับ ${momNick}</b> จะมีหมู่เลือดเป็นอะไรได้บ้าง?<br>
                <span style="font-size:15px;color:#956;">เลือกหมู่เลือดที่ <b>เป็นไปได้</b> ว่าลูกจะได้รับ</span>
            </div>
            <div class="avatar-row" style="justify-content:center;">
                <div class="avatar">
                    <div class="avatar-img">${kidAvatar}</div>
                    <div style="font-size:14px; color:#aaa;">ลูก</div>
                </div>
            </div>
            <div class="blood-packs" id="blood-packs-delivery">
                ${bloodTypes.map(type=>`
                <div class="blood-pack" data-type="${type}">
                    <span>🩸</span>
                    <span class="blood-pack-label">${type}</span>
                </div>`).join('')}
            </div>
            <div id="delivery-result" class="result"></div>
        </div>
        `;
        let selected = [];
        document.querySelectorAll('.blood-pack').forEach(pack => {
            pack.onclick = ()=>{
                let t = pack.getAttribute('data-type');
                pack.classList.toggle('selected');
                if (selected.includes(t)) {
                    selected = selected.filter(x => x!==t);
                } else {
                    selected.push(t);
                }
            };
        });
        let ans = possibleChildBlood.hasOwnProperty(`${dadBlood},${momBlood}`) ?
            possibleChildBlood[`${dadBlood},${momBlood}`] : possibleChildBlood[`${momBlood},${dadBlood}`];
        document.getElementById('delivery-result').innerHTML = `
            <button class="btn next-btn" onclick="checkDeliveryAnswer('${ans.join(',')}');">ตรวจคำตอบ</button>
        `;
    }
    function checkDeliveryAnswer(a) {
        let correctTypes = a.split(',');
        let selectedTypes = Array.from(document.querySelectorAll('.blood-pack.selected')).map(x=>x.getAttribute('data-type')).sort();
        let correctSorted = correctTypes.slice().sort();
        if(selectedTypes.length==0){
            document.getElementById('delivery-result').innerHTML =
                `<span style="color:#d0453b;">โปรดเลือกอย่างน้อย 1 หมู่เลือดก่อนค่ะ</span>
                <button class="btn next-btn" onclick="checkDeliveryAnswer('${a}');">ตรวจคำตอบ</button>`;
            return;
        }
        if(selectedTypes.join(',') === correctSorted.join(',')){
            document.getElementById('delivery-result').innerHTML =
                `<span style="color:#22ab60;">✅ ถูกต้อง!</span> <button class="btn next-btn" onclick="nextDeliveryLevel();">ไปด่านถัดไป</button>`;
        }else{
            document.getElementById('delivery-result').innerHTML =
                `<span style="color:#d0453b;">❌ ยังไม่ถูกต้อง โปรดลองใหม่ค่ะ</span>
                <button class="btn next-btn" onclick="checkDeliveryAnswer('${a}');">ตรวจคำตอบ</button>`;
        }
    }
    function nextLabLevel() {
        state.labLevel++;
        renderLabLevel();
    }
    function nextDeliveryLevel() {
        state.deliveryLevel++;
        state.currentCombo = state.deliveryQuestions[state.deliveryLevel] || null;
        renderDeliveryLevel();
    }
    function showResultSummary() {
        let elapsed = Math.round((state.endTime-state.startTime)/1000);
        let text = `<div class="result fade-in">
            🏆 <b>${escapeHTML(state.userName)}</b><br>
            <div style="margin:10px 0;">ใช้เวลาเล่นทั้งหมด: <b style="color:#5a29c9;font-size:1.2em">${formatTime(elapsed)}</b></div>
            <button class="share-btn" onclick="shareResult()">แชร์ผลการเล่น</button>
            <div style="margin-top:18px;">
                <button class="btn" onclick="restartGame()">เริ่มใหม่</button>
            </div>
        </div>`;
        document.querySelector("#game-area").innerHTML = text;
    }
    function escapeHTML(txt) {
        return txt.replace(/</g,"&lt;").replace(/>/g,"&gt;");
    }
    function shareResult() {
        let elapsed = Math.round((state.endTime-state.startTime)/1000);
        let msg = `ฉัน (${state.userName}) เพิ่งผ่านเกมการให้และรับเลือดครบทุกด่าน ใช้เวลา ${formatTime(elapsed)}!\nมาเล่นกันเถอะ! 🩸`;
        if (navigator.share) {
            navigator.share({
                title: 'เกมการให้และรับเลือด',
                text: msg,
                url: window.location.href
            }).catch(()=>{});
        } else {
            copyTextToClipboard(msg);
            alert("คัดลอกผลไปยังคลิปบอร์ดแล้ว:\n\n" + msg);
        }
    }
    function copyTextToClipboard(text) {
        let textArea = document.createElement("textarea");
        textArea.value = text;
        document.body.appendChild(textArea);
        textArea.focus();
        textArea.select();
        document.execCommand("copy");
        textArea.remove();
    }
    document.getElementById("btn-lab").onclick = function() {
        if(document.getElementById("btn-lab").classList.contains('selected')) return;
        startLabScenario();
    }
    document.getElementById("btn-delivery").onclick = function() {
        if(!state.deliveryUnlocked) return;
        if(document.getElementById("btn-delivery").classList.contains('selected')) return;
        startDeliveryScenario();
    }
    function restartGame() {
        state.userName = '';
        document.getElementById('username-input').value = "";
        document.getElementById('username-box').style.display = "";
        document.getElementById('game-ui').style.display = "none";
        state.timerRunning = false;
        clearInterval(state.timerInterval);
    }
    window.nextLabLevel = nextLabLevel;
    window.nextDeliveryLevel = nextDeliveryLevel;
    window.checkDeliveryAnswer = checkDeliveryAnswer;
    window.startLabScenario = startLabScenario;
    window.restartGame = restartGame;
    window.shareResult = shareResult;
    window.userSubmitName = userSubmitName;
    window.checkLabMultiAnswer = checkLabMultiAnswer;
    document.getElementById('username-input').addEventListener('keydown',function(e){
        if(e.key==='Enter') userSubmitName();
    });
    </script>
</body>
</html>
