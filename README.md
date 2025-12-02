<html lang="th">
<head>
    <meta charset="UTF-8">
    <title>A B O Blood Group</title>
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
            font-family: 'Kanit', 'Tahoma', sans-serif;
            letter-spacing: 1.5px;
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
        .char-img {
            width: 68px; height: 68px;
            border-radius: 50%;
            background: #f8ebff;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 36px;
            margin-bottom:0;
            border: 2.5px solid #d3c4ff;
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
        .answer-area {
            border: 2.5px solid #9952f0;    /* ฟ้า/ม่วงสด */
            border-radius: 14px;
            padding: 12px 7px 8px 7px;
            margin: 18px 0 10px 0;
            box-shadow: 0 4px 12px rgba(100,60,200,0.09);
            background: #fcf8ff;
        }
        .answer-area .blood-packs { margin-top:0; margin-bottom:0; }
        .blood-packs { display: flex; flex-wrap: wrap; justify-content: center; gap: 12px; }
        .blood-pack {
            background: #e04e4e;
            border-radius: 11px;
            width: 65px; height: 88px;
            display: flex; flex-direction: column;
            align-items: center; justify-content: center;
            color: #fff; font-size: 24px;
            cursor: pointer; border: 3.3px solid #fff;
            transition: border 0.18s, box-shadow 0.18s;
            box-shadow: 0 2px 7px rgba(220,98,135,0.13);
            position: relative;
        }
        .blood-pack.selected { border: 4px solid #f9c24b; box-shadow: 0 0 0 3px #ffe09a; background: #e83e32; }
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
        .stats-table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0 2px 0;
            font-size: 1em;
        }
        .stats-table th, .stats-table td {
            border: 1.3px solid #a991c9;
            padding: 7px 4px;
            text-align: center;
        }
        .stats-table th {
            background: #ede5f8;
            color: #6542a2;
            font-weight: bold;
        }
        .stats-table td {
            background: #faf6fd;
            color: #553388;
        }
        .table-caption {
            font-weight: bold;
            color: #6532d0;
            font-size: 1.02em;
            margin-top:19px;
            margin-bottom:3px;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@600&display=swap" rel="stylesheet">
</head>
<body>
    <div class="container" id="main-container">
        <h1>A B O Blood Group</h1>
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
    // ตัวการ์ตูน
    const cuteCharacters = [
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="38" rx="21" ry="18" fill="#ffeddd"/><ellipse cx="32" cy="26" rx="18" ry="16" fill="#ffe5c8"/><circle cx="32" cy="23" r="20" fill="#fad2b0"/><ellipse cx="19" cy="21" rx="5" ry="8" fill="#f9ba97"/><ellipse cx="45" cy="21" rx="5" ry="8" fill="#f9ba97"/><ellipse cx="32" cy="29" rx="15" ry="13" fill="#fff7f0"/><ellipse cx="22.5" cy="24.5" rx="2.3" ry="3.1" fill="#fff"/><ellipse cx="41.5" cy="24.5" rx="2.3" ry="3.1" fill="#fff"/><ellipse cx="22.5" cy="25" rx="1.5" ry="2" fill="#773800"/><ellipse cx="41.5" cy="25" rx="1.5" ry="2" fill="#773800"/><ellipse cx="32" cy="31" rx="7" ry="4" fill="#fbd5bc"/><ellipse cx="32" cy="31" rx="3.5" ry="1.8" fill="#f9939d"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="44" rx="18" ry="15" fill="#fffbd8"/><ellipse cx="32" cy="28" rx="17.5" ry="15.8" fill="#fff0c0"/><ellipse cx="32" cy="26" rx="19" ry="16" fill="#ffd67a"/><circle cx="32" cy="21" r="16" fill="#ffe2a7"/><ellipse cx="17" cy="21" rx="4.5" ry="7" fill="#f5d48d"/><ellipse cx="47" cy="21" rx="4.5" ry="7" fill="#f5d48d"/><ellipse cx="32" cy="32" rx="13" ry="10" fill="#fff8db"/><ellipse cx="23" cy="25.7" rx="2" ry="3" fill="#fff"/><ellipse cx="41" cy="25.7" rx="2" ry="3" fill="#fff"/><ellipse cx="23" cy="26" rx="1.2" ry="1.7" fill="#905e08"/><ellipse cx="41" cy="26" rx="1.2" ry="1.7" fill="#905e08"/><ellipse cx="32" cy="33" rx="6" ry="2.5" fill="#ffdce4"/><ellipse cx="32" cy="33" rx="2.4" ry="0.9" fill="#ff90ab"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="44" rx="18" ry="15" fill="#e7f7ff"/><ellipse cx="32" cy="28" rx="17.5" ry="14.8" fill="#d6ebf8"/><ellipse cx="32" cy="25" rx="19" ry="15" fill="#99d5f6"/><ellipse cx="32" cy="17" rx="17" ry="11" fill="#43bcf1"/><ellipse cx="17" cy="21" rx="4.5" ry="7" fill="#bfd7ed"/><ellipse cx="47" cy="21" rx="4.5" ry="7" fill="#bfd7ed"/><ellipse cx="32" cy="31" rx="13" ry="9" fill="#edfbff"/><ellipse cx="23" cy="23.5" rx="2.1" ry="2.8" fill="#fff"/><ellipse cx="41" cy="23.5" rx="2.1" ry="2.8" fill="#fff"/><ellipse cx="23" cy="24" rx="1" ry="1.5" fill="#27759f"/><ellipse cx="41" cy="24" rx="1" ry="1.5" fill="#27759f"/><ellipse cx="32" cy="34" rx="5.5" ry="2" fill="#ffc1a5"/><ellipse cx="32" cy="34" rx="1.8" ry="0.7" fill="#fb97a3"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="40" rx="18" ry="13" fill="#e8ffd7"/><ellipse cx="32" cy="28" rx="15.5" ry="13.8" fill="#e5ffd1"/><ellipse cx="32" cy="25" rx="18.5" ry="13" fill="#a7ee96"/><ellipse cx="32" cy="17" rx="16" ry="10" fill="#6ed93f"/><ellipse cx="17" cy="21" rx="4" ry="6.5" fill="#d2e3c6"/><ellipse cx="47" cy="21" rx="4" ry="6.5" fill="#d2e3c6"/><ellipse cx="32" cy="31" rx="13" ry="8" fill="#f8ffec"/><ellipse cx="23" cy="23.5" rx="1.9" ry="2.6" fill="#fff"/><ellipse cx="41" cy="23.5" rx="1.9" ry="2.6" fill="#fff"/><ellipse cx="23" cy="24" rx="1" ry="1.4" fill="#5b962a"/><ellipse cx="41" cy="24" rx="1" ry="1.4" fill="#5b962a"/><ellipse cx="32" cy="34" rx="5.5" ry="2" fill="#ffc1ef"/><ellipse cx="32" cy="34" rx="1.8" ry="0.6" fill="#ff86bc"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="44" rx="18" ry="14" fill="#ffe5f5"/><ellipse cx="32" cy="28" rx="17.5" ry="15.5" fill="#ffdbe9"/><ellipse cx="32" cy="23" rx="19" ry="15" fill="#f394bc"/><ellipse cx="32" cy="18" rx="15" ry="8" fill="#f18eb1"/><ellipse cx="17" cy="20" rx="4.2" ry="7.2" fill="#facae3"/><ellipse cx="47" cy="20" rx="4.2" ry="7.2" fill="#facae3"/><ellipse cx="32" cy="33" rx="11.5" ry="10.5" fill="#fff8fd"/><ellipse cx="23" cy="25.2" rx="2" ry="2.9" fill="#fff"/><ellipse cx="41" cy="25.2" rx="2" ry="2.9" fill="#fff"/><ellipse cx="23" cy="25.5" rx="1.2" ry="1.5" fill="#f76dac"/><ellipse cx="41" cy="25.5" rx="1.2" ry="1.5" fill="#f76dac"/><ellipse cx="32" cy="35" rx="4" ry="1.7" fill="#ffccd2"/><ellipse cx="32" cy="35" rx="1.5" ry="0.7" fill="#ff7c90"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="44" rx="18" ry="14" fill="#eed0ff"/><ellipse cx="32" cy="30" rx="18" ry="15" fill="#e3c3fd"/><ellipse cx="32" cy="23" rx="18" ry="14" fill="#b193fc"/><ellipse cx="32" cy="20" rx="14" ry="6" fill="#9f74fc"/><ellipse cx="18" cy="22" rx="4" ry="5.5" fill="#cabcf6"/><ellipse cx="46" cy="22" rx="4" ry="5.5" fill="#cabcf6"/><ellipse cx="32" cy="31" rx="10" ry="9" fill="#f6f0ff"/><ellipse cx="24" cy="24" rx="1.9" ry="2.4" fill="#fff"/><ellipse cx="40" cy="24" rx="1.9" ry="2.4" fill="#fff"/><ellipse cx="24" cy="24.3" rx="1.1" ry="1.2" fill="#5c46a4"/><ellipse cx="40" cy="24.3" rx="1.1" ry="1.2" fill="#5c46a4"/><ellipse cx="32" cy="33" rx="2.3" ry="0.9" fill="#8681b5"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="45" rx="16" ry="10" fill="#fbefff"/><ellipse cx="32" cy="29" rx="15.5" ry="13.3" fill="#f4c7e5"/><ellipse cx="32" cy="22" rx="15" ry="13" fill="#c376ae"/><ellipse cx="32" cy="16" rx="12" ry="4" fill="#ab1e85"/><rect x="24" y="11" width="16" height="5" rx="2.5" fill="#ffb4e4"/><ellipse cx="18" cy="20" rx="4.2" ry="6.1" fill="#e7afd6"/><ellipse cx="46" cy="20" rx="4.2" ry="6.1" fill="#e7afd6"/><ellipse cx="32" cy="33" rx="11" ry="9.8" fill="#feeffa"/><ellipse cx="24" cy="23" rx="1.9" ry="2.2" fill="#fff"/><ellipse cx="40" cy="23" rx="1.9" ry="2.2" fill="#fff"/><ellipse cx="24" cy="24" rx="1.2" ry="1.4" fill="#a12c7c"/><ellipse cx="40" cy="24" rx="1.2" ry="1.4" fill="#a12c7c"/><ellipse cx="32" cy="35" rx="4" ry="1.5" fill="#eba6d2"/><ellipse cx="32" cy="35" rx="1.3" ry="0.7" fill="#e066be"/></svg>`,
    `<svg width="64" height="64" viewBox="0 0 64 64"><ellipse cx="32" cy="43" rx="17" ry="13" fill="#dbeeff"/><ellipse cx="32" cy="28" rx="17" ry="14" fill="#a6e1fa"/><ellipse cx="32" cy="21" rx="16" ry="13" fill="#539fd3"/><ellipse cx="32" cy="15" rx="12" ry="3.5" fill="#376f99"/><ellipse cx="33" cy="11" rx="2" ry="2.7" fill="#262e69"/><ellipse cx="18" cy="20" rx="4" ry="5.4" fill="#aad1ea"/><ellipse cx="46" cy="20" rx="4" ry="5.4" fill="#aad1ea"/><ellipse cx="32" cy="31" rx="11.3" ry="9.5" fill="#eaf7ff"/><ellipse cx="24.2" cy="24" rx="2.0" ry="2.3" fill="#fff"/><ellipse cx="40.2" cy="24" rx="2.0" ry="2.3" fill="#fff"/><ellipse cx="24.2" cy="24.7" rx="1" ry="1.2" fill="#275b97"/><ellipse cx="40.2" cy="24.7" rx="1" ry="1.2" fill="#275b97"/><ellipse cx="32" cy="34" rx="2.5" ry="1" fill="#90abd7"/></svg>`
    ];
    const nicknames = [
        "น้องออม", "ปั้นหยา", "ติ๊ดตี่", "ซันนี่", "ปอปลา", "มีค่าร์", "เบบี๋", "นุ่มนิ่ม", "มิลค์กี้", "ตังค์ตังค์",
        "ช็อคโก้", "ไอติม", "มิกิ", "โมโม่", "อั่งเปา", "แซนด์", "ภูริ", "ต้นกล้า", "ภูผา", "เติ้ล", "ข้าวปั้น", "ข้าวเหนียว"
    ];
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
    function getLabQuestions10() {
        let result = [];
        for (let i = 0; i < 10; i++) {
            let receiverBlood = bloodTypes[Math.floor(Math.random() * bloodTypes.length)];
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
        avatarIndex: 0,
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
        // บันทึกสถิติ
        stats: {
            lab: [],
            delivery: []
        }
    };
    function resetPools() {
        state.avatarIndex = 0;
        state.avatarPool = [];
        state.nicknamePool = shuffle([...nicknames]);
        state.parentCombos = shuffle(allParentCombinations());
    }
    function getNextCharacterHTML() {
        const html = cuteCharacters[state.avatarIndex % cuteCharacters.length];
        state.avatarIndex++;
        return `<span class="char-img">${html}</span>`;
    }
    function getNextNick() {
        if (state.nicknamePool.length === 0) {
            state.nicknamePool = shuffle([...nicknames]);
        }
        return state.nicknamePool.pop();
    }
    function shuffle(a){
        let arr = a.slice();
        for(let i=arr.length-1;i>0;i--){
            const j = Math.floor(Math.random()*(i+1));
            [arr[i],arr[j]]=[arr[j],arr[i]];
        }
        return arr;
    }
    function pad(num) { return num < 10 ? '0'+num : num; }
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
        // reset stats
        state.stats = { lab: [], delivery: [] };
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
        state.stats.lab = [];
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
        state.stats.delivery = [];
        renderDeliveryLevel();
    }
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
        let charHtmlA = getNextCharacterHTML();
        let charHtmlB = getNextCharacterHTML();
        let nickA = getNextNick();
        let nickB = getNextNick();
        document.querySelector("#game-area").innerHTML = `
        <div class="fade-in">
            <div style="text-align:center; color:#5a299c; margin-bottom:16px;">
                🏥 สถานการณ์ <b>ห้องปฏิบัติการ</b>: ข้อที่ ${state.labLevel+1} / ${state.totalLabQ}
            </div>
            <div class="avatar-row">
                <div class="avatar">
                    ${charHtmlA}
                    <div class="blood-type">?</div>
                    <div class="nickname">${nickA}</div>
                    <div style="font-size:13px;color:#888; margin-top:2px;">ผู้ให้เลือด</div>
                </div>
                <span style="font-size:48px;">➡️</span>
                <div class="avatar">
                    ${charHtmlB}
                    <div class="blood-type">${q.receiverBlood}</div>
                    <div class="nickname">${nickB}</div>
                    <div style="font-size:13px;color:#888; margin-top:2px;">ผู้รับเลือด</div>
                </div>
            </div>
            <div style="text-align:center; color:#642bf1; font-size:18px;margin-bottom:11px;">
                <b>${nickB}</b> (หมู่เลือด <b>${q.receiverBlood}</b>) ต้องการเลือด<br>
                เลือกหมู่เลือดของ <b>ผู้ให้เลือด</b> ที่ให้ได้ (เลือกได้มากกว่า 1 อัน)
            </div>
            <div class="answer-area">
                <div class="blood-packs" id="blood-packs">
                    ${bloodTypes.map(type=>`
                    <div class="blood-pack" data-type="${type}">
                        <span>🩸</span>
                        <span class="blood-pack-label">${type}</span>
                    </div>`).join('')}
                </div>
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
        // บันทึกสถิติ
        let labStats = state.stats.lab;
        let qN = state.labLevel;
        // เวลาเริ่มของข้อนี้ (หรือรอบใหม่ถ้ายังไม่มี)
        if (!labStats[qN]) labStats[qN] = { trys: 0, correct: false };
        labStats[qN].trys++;
        const correct = selectedTypes.join(',') === correctSorted.join(',');
        if(correct){
            labStats[qN].correct = true;
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
        let dadChar = getNextCharacterHTML();
        let momChar = getNextCharacterHTML();
        let kidChar = getNextCharacterHTML();
        let dadNick = getNextNick();
        let momNick = getNextNick();
        let kidNick = getNextNick();
        document.querySelector("#game-area").innerHTML = `
        <div class="fade-in">
            <div style="text-align:center; color:#3d6a95; margin-bottom:16px;">
                👶 สถานการณ์ <b>ห้องคลอด</b>: ข้อที่ ${state.deliveryLevel+1} / ${state.totalDeliveryQ}
            </div>
            <div class="avatar-row" style="justify-content: space-around;">
                <div class="avatar">
                    ${dadChar}
                    <div class="blood-type">${dadBlood}</div>
                    <div class="nickname">${dadNick}<div style="font-size:12px;color:#999;">คุณพ่อ</div></div>
                </div>
                <div class="avatar">
                    ${momChar}
                    <div class="blood-type">${momBlood}</div>
                    <div class="nickname">${momNick}<div style="font-size:12px;color:#999;">คุณแม่</div></div>
                </div>
            </div>
            <div style="text-align:center; color:#6235ab; font-size:18px;margin-bottom:8px;">
                <b>ลูกของ ${dadNick} กับ ${momNick}</b> จะมีหมู่เลือดเป็นอะไรได้บ้าง?<br>
                <span style="font-size:15px;color:#956;">เลือกหมู่เลือดที่ <b>เป็นไปได้</b> ว่าลูกจะได้รับ</span>
            </div>
            <div class="answer-area">
                <div class="blood-packs" id="blood-packs-delivery">
                    ${bloodTypes.map(type=>`
                    <div class="blood-pack" data-type="${type}">
                        <span>🩸</span>
                        <span class="blood-pack-label">${type}</span>
                    </div>`).join('')}
                </div>
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
        let deliveryStats = state.stats.delivery;
        let qN = state.deliveryLevel;
        if (!deliveryStats[qN]) deliveryStats[qN] = { trys: 0, correct: false };
        deliveryStats[qN].trys++;
        if(selectedTypes.length==0){
            document.getElementById('delivery-result').innerHTML =
                `<span style="color:#d0453b;">โปรดเลือกอย่างน้อย 1 หมู่เลือดก่อนค่ะ</span>
                <button class="btn next-btn" onclick="checkDeliveryAnswer('${a}');">ตรวจคำตอบ</button>`;
            return;
        }
        if(selectedTypes.join(',') === correctSorted.join(',')){
            deliveryStats[qN].correct = true;
            document.getElementById('delivery-result').innerHTML =
                `<span style="color:#22ab60;">✅ ถูกต้อง!</span> <button class="btn next-btn" onclick="nextDeliveryLevel();">ไปด่านถัดไป</button>`;
        }else{
            document.getElementById('delivery-result').innerHTML =
                `<span style="color:#d0453b;">❌ ยังไม่ถูกต้อง โปรดลองใหม่ค่ะ</span>
                <button class="btn next-btn" onclick="checkDeliveryAnswer('${a}');">ตรวจคำตอบ</button>`;
        }
    }
    function nextDeliveryLevel() {
        state.deliveryLevel++;
        state.currentCombo = state.deliveryQuestions[state.deliveryLevel] || null;
        renderDeliveryLevel();
    }
    function showResultSummary() {
        let elapsed = Math.round((state.endTime-state.startTime)/1000);
        // วิเคราะห์ stats
        let labStats = state.stats.lab;
        let deliveryStats = state.stats.delivery;
        let labCorrect = labStats.filter(x=>x&&x.correct).length;
        let labTries = labStats.reduce((sum,x)=>(x&&x.trys)?sum+x.trys:sum,0);
        let deliveryCorrect = deliveryStats.filter(x=>x&&x.correct).length;
        let deliveryTries = deliveryStats.reduce((sum,x)=>(x&&x.trys)?sum+x.trys:sum,0);

        let text = `<div class="result fade-in">
            🏆 <b>${escapeHTML(state.userName)}</b><br>
            <div style="margin:10px 0;">ใช้เวลาเล่นทั้งหมด: <b style="color:#5a29c9;font-size:1.2em">${formatTime(elapsed)}</b></div>
            <div class="table-caption">สถิติห้องปฏิบัติการ</div>
            <table class="stats-table">
                <tr><th>ข้อ</th><th>หมู่เลือดผู้รับ</th><th>ตอบถูก</th><th>จำนวนครั้ง</th></tr>
                ${state.labQuestions.map((q,i)=>`
                <tr>
                    <td>${i+1}</td>
                    <td>${q.receiverBlood}</td>
                    <td style="color:${labStats[i]&&labStats[i].correct?'#19b847':'#f02525'}">${labStats[i]&&labStats[i].correct?'✔️':'✘'}</td>
                    <td>${labStats[i]?labStats[i].trys:0}</td>
                </tr>
                `).join('')}
            </table>
            <div style="font-size:95%;">รวมตอบถูก ${labCorrect}/${state.labQuestions.length} | เฉลี่ย <b>${labTries}</b> ครั้ง</div>
            <div class="table-caption">สถิติห้องคลอด</div>
            <table class="stats-table">
                <tr><th>ข้อ</th><th>พ่อ</th><th>แม่</th><th>ตอบถูก</th><th>จำนวนครั้ง</th></tr>
                ${state.deliveryQuestions.map((q,i)=>`
                <tr>
                    <td>${i+1}</td>
                    <td>${q[0]}</td>
                    <td>${q[1]}</td>
                    <td style="color:${deliveryStats[i]&&deliveryStats[i].correct?'#19b847':'#f02525'}">${deliveryStats[i]&&deliveryStats[i].correct?'✔️':'✘'}</td>
                    <td>${deliveryStats[i]?deliveryStats[i].trys:0}</td>
                </tr>
                `).join('')}
            </table>
            <div style="font-size:95%;">รวมตอบถูก ${deliveryCorrect}/${state.deliveryQuestions.length} | เฉลี่ย <b>${deliveryTries}</b> ครั้ง</div>
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
        let msg = `ฉัน (${state.userName}) เพิ่งผ่านเกม A B O Blood Group ครบทุกด่าน ใช้เวลา ${formatTime(elapsed)}!\nดูสถิติได้ในหน้าสรุป มาเล่นกันเถอะ! 🩸`;
        if (navigator.share) {
            navigator.share({
                title: 'A B O Blood Group',
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
