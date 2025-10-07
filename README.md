[Untitled-1.html](https://github.com/user-attachments/files/22751541/Untitled-1.html)
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ລອຍກະທົງອອນລາຍ</title>
    <style>
        /* --- การตั้งค่าพื้นฐาน --- */
        html, body {
            height: 100%;
            margin: 0;
            overflow: hidden; /* ซ่อน scrollbar */
            font-family: 'Sarabun', sans-serif;
        }

        /* --- พื้นหลัง (แม่น้ำ) --- */
        body {
            /* เทคนิคใหม่: ใช้ background หลายชั้นเพื่อสร้างเอฟเฟกต์น้ำ */
            background-color: #001f3f; /* สีพื้นหลังน้ำเงินเข้ม */
            background-image:
                /* ชั้นที่ 3: แสงระยิบระยับ (เคลื่อนที่เร็วสุด) */
                radial-gradient(circle at 20% 40%, rgba(200, 220, 255, 0.2) 1%, transparent 10%),
                radial-gradient(circle at 80% 70%, rgba(200, 220, 255, 0.2) 1%, transparent 10%),
                /* ชั้นที่ 2: แสงสะท้อนนุ่มนวล (เคลื่อนที่ช้า) */
                radial-gradient(ellipse at 50% 100%, rgba(100, 150, 200, 0.25) 0%, transparent 50%),
                /* ชั้นที่ 1: สีพื้นของน้ำไล่ระดับ */
                linear-gradient(to top, #00284d, #00509e);
            background-size: 400px 400px, 400px 400px, 100% 100%, 100% 100%;
            animation: water-flow 15s linear infinite;
            display: flex;
            flex-direction: column;
        }

        /* --- อนิเมชันการไหลของน้ำ --- */
        @keyframes water-flow {
            from {
                background-position: 0 0, 0 0, 0 0, 0 0;
            }
            to {
                /* ขยับ background แต่ละชั้นด้วยความเร็วและทิศทางที่ต่างกัน */
                background-position: -400px 400px, 400px -400px, 0 0, 0 0;
            }
        }
        
        /* --- พระจันทร์ --- */
        #moon {
            position: absolute;
            top: 5%;
            right: 10%;
            width: 100px;
            height: 100px;
            background-color: #f0e68c; /* สีเหลืองอ่อนๆ คล้ายแสงจันทร์ */
            border-radius: 50%;
            /* สร้างเงาเรืองแสงรอบดวงจันทร์ */
            box-shadow: 
                0 0 20px #f0e68c,
                0 0 40px #f0e68c,
                0 0 60px #ffffff;
            animation: moon-glow 8s ease-in-out infinite alternate;
        }

        @keyframes moon-glow {
            from {
                box-shadow: 
                    0 0 20px #f0e68c,
                    0 0 40px #f0e68c,
                    0 0 60px #ffffff;
            }
            to {
                box-shadow: 
                    0 0 30px #f5efb8,
                    0 0 50px #f5efb8,
                    0 0 80px #ffffff;
            }
        }

        /* --- ส่วนหัว --- */
        header {
            color: white;
            text-align: center;
            padding: 20px;
            text-shadow: 2px 2px 4px #067dc2;
        }

        header h1 {
            margin: 0;
            font-size: 2.5em;
        }

        header p {
            margin: 5px 0 0;
            font-size: 1.2em;
        }

        /* --- พื้นที่สำหรับลอยกระทง --- */
        main {
            flex-grow: 1;
            position: relative;
            /* ไม่ต้องใช้ cursor: pointer ที่นี่แล้ว เพราะจะไปบังคลื่น */
            cursor: pointer;
        }

        /* --- รูปแบบกระทง --- */
        .krathong {
            position: absolute;
            width: 100px;  /* กำหนดขนาดความกว้างของรูปกระทง */
            height: 100px; /* กำหนดขนาดความสูงของรูปกระทง */
            /* เพิ่มเงาเรืองแสงรอบๆ รูปกระทง */
            filter: drop-shadow(0 0 8px #ffdd00) drop-shadow(0 0 15px #ffdd00);
            /* ทำให้ animation วนลูปตลอดไป (infinite) และไม่หยุด (forwards) */
            animation: float-away 25s linear infinite; /* อนิเมชันสำหรับกระทงทั่วไป */
            pointer-events: none; /* ทำให้คลิกทะลุตัวกระทงได้ */
        }

        /* --- อนิเมชันการลอยของกระทง --- */
        @keyframes float-away {
            0% {
                transform: translate(var(--tx-start), 100vh) scale(1) rotate(-10deg);
                opacity: 1;
            }
            50% {
                /* จุดกึ่งกลาง: ให้เคลื่อนที่ไปด้านข้าง */
                transform: translate(var(--tx-mid), 50vh) scale(0.9) rotate(0deg);
            }
            100% {
                /* จุดสิ้นสุด: ลอยไปอีกด้านและจางหายไปเล็กน้อย */
                transform: translate(var(--tx-end), -100px) scale(0.8) rotate(10deg);
                opacity: 0.8;
            }
        }

        /* --- รูปแบบและอนิเมชันสำหรับกระทงของผู้ใช้โดยเฉพาะ --- */
        .user-krathong {
            animation: float-from-click 30s ease-out forwards;
        }

        @keyframes float-from-click {
            0% {
                /* เริ่มต้น ณ จุดที่คลิก, ขนาดเล็กและโปร่งใส */
                transform: scale(0.5);
                opacity: 0;
            }
            10% {
                /* เอฟเฟกต์ "จ๋อม", ขยายใหญ่ขึ้นและปรากฏตัว */
                transform: scale(1.1);
                opacity: 1;
            }
            20% {
                /* หลังจาก "จ๋อม" ให้กลับมาขนาดปกติและลอยนิ่งๆ สักพัก */
                transform: scale(1.0);
                opacity: 1;
            }
            95% {
                /* ก่อนจะถึงจุดสิ้นสุดเล็กน้อย ให้ยังคงมองเห็นชัดเจน */
                opacity: 1;
                transform: scale(0.6) translateY(-95vh) translateX(var(--tx-user-end));
            }
            100% {
                /* ลอยจนพ้นขอบจอด้านบนแล้วค่อยจางหายไป */
                transform: scale(0.5) translateY(-110vh) translateX(var(--tx-user-end));
                opacity: 0;
            }
        }

        /* --- รูปแบบหน้าต่างอธิษฐาน (Modal) --- */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.6);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            /* ซ่อนไว้เป็นค่าเริ่มต้น */
            visibility: hidden;
            opacity: 0;
            transition: visibility 0s 0.3s, opacity 0.3s ease;
        }

        .modal-content {
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            text-align: center;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .modal-content h2 {
            margin-top: 0;
            color: #333;
        }

        .selection-title {
            color: #555;
            margin-bottom: 10px;
            font-size: 0.9em;
        }

        .krathong-selection-container {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 20px;
        }

        .krathong-choice {
            width: 60px;
            height: 60px;
            cursor: pointer;
            border-radius: 8px;
            border: 3px solid transparent;
            transition: transform 0.2s ease, border-color 0.2s ease;
        }
        .krathong-choice:hover { transform: scale(1.1); }
        .krathong-choice.selected { border-color: #007bff; }

        #wish-input {
            width: calc(100% - 20px);
            padding: 10px;
            margin-top: 15px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .modal-buttons button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 0 10px;
        }
    </style>
</head>
<body>

    <div id="moon"></div>

    <header>
        <h1>ລອຍກະທົງອອນລາຍສຳຫຼັບຄົນໂສດ</h1>
        <p>ຄິກເພື່ອລອຍກະທົງ</p>
    </header>

    <main id="river"></main>

    <!-- หน้าต่างสำหรับใส่คำอธิษฐาน -->
    <div id="wish-modal" class="modal-overlay">
        <div class="modal-content">
            <h2>ໃສ່ຄຳອະທິຖານ</h2>
            <p class="selection-title">ເລືອກກະທົງຂອງເຈົ້າ</p>
            <div id="krathong-selection" class="krathong-selection-container"></div>
            <textarea id="wish-input" rows="3" placeholder="ຂໍໃຫ້..."></textarea>
            <div class="modal-buttons">
                <button id="cancel-wish">ຍົກເລິກ</button>
                <button id="submit-wish" style="background-color: #007bff; color: white;">ລອຍກະທົງ</button>
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html> [script.js](https://github.com/user-attachments/files/22751542/script.js)
document.addEventListener('DOMContentLoaded', () => {
    const river = document.getElementById('river');
    const wishModal = document.getElementById('wish-modal');
    const wishInput = document.getElementById('wish-input');
    const submitWishBtn = document.getElementById('submit-wish');
    const cancelWishBtn = document.getElementById('cancel-wish');
    const krathongSelectionContainer = document.getElementById('krathong-selection');

    // --- รูปภาพกระทงสำหรับให้เลือก ---
    const krathongImageSources = [
        'https://www.mcp.ac.th/student/sday/event7.fld/image003.png', // แบบที่ 1 (ดอกไม้รวม)
        'https://www.okusanpix.com/wp-content/uploads/2019/10/b17cfe529740a6e610907c76dbb292ee.png', // แบบที่ 2 (สีชมพู)
        'https://pngbie.com/assets/images/icon/Pngbie-%E0%B8%A0%E0%B8%B2%E0%B8%9E%E0%B8%9F%E0%B8%A3%E0%B8%B5-20221030022923.png'  // แบบที่ 3 (ใบตอง)
    ];
    let selectedKrathongSrc = krathongImageSources[0]; // ตั้งค่าเริ่มต้น

    let lastClickPosition = { x: 0, y: 0 };

    // --- เมื่อคลิกที่แม่น้ำ ---
    river.addEventListener('click', (event) => {
        // เก็บตำแหน่งที่คลิก
        lastClickPosition.x = event.clientX;
        lastClickPosition.y = event.clientY;
        // แสดงหน้าต่างสำหรับอธิษฐาน
        wishModal.style.visibility = 'visible';
        wishModal.style.opacity = 1;
        wishModal.style.transitionDelay = '0s';
        wishInput.focus();
    });

    // --- เมื่อกดยืนยันการอธิษฐาน ---
    submitWishBtn.addEventListener('click', () => {
        // ส่ง flag `isUser: true` เพื่อบอกว่าเป็นกระทงของผู้ใช้
        createKrathong(lastClickPosition.x, lastClickPosition.y, wishInput.value, {
            isUser: true
        });
        hideModal();
    });

    // --- เมื่อกดยกเลิก ---
    cancelWishBtn.addEventListener('click', () => {
        hideModal();
    });

    function hideModal() {
        wishModal.style.visibility = 'hidden';
        wishModal.style.opacity = 0;
        wishModal.style.transitionDelay = '0.3s';
        wishInput.value = ''; // ล้างข้อความในช่องอธิษฐาน
    }

    function createKrathong(x, y, wishText, options = {}) {
        const krathong = document.createElement('img');
        krathong.className = 'krathong';

        if (options.isUser) {
            // --- สำหรับกระทงของผู้ใช้ ---
            krathong.src = selectedKrathongSrc; // ใช้รูปกระทงที่เลือก
            krathong.classList.add('user-krathong');
            // กำหนดตำแหน่งเริ่มต้น ณ จุดที่คลิก
            krathong.style.left = `${x - 50}px`; // 50 คือครึ่งความกว้าง
            krathong.style.top = `${y - 50}px`; // 50 คือครึ่งความสูง
            // กำหนดทิศทางการลอยแนวนอนแบบสุ่ม
            const endX = (Math.random() - 0.5) * 200; // ส่ายไปซ้ายหรือขวา
            krathong.style.setProperty('--tx-user-end', `${endX}px`);

            // ลบกระทงของผู้ใช้ออกเมื่ออนิเมชันจบลง
            krathong.addEventListener('animationend', () => {
                krathong.remove();
            });
        } else {
            // --- สำหรับกระทงทั่วไป (ของคนอื่นและกระทงเริ่มต้น) ---
            // สุ่มกระทงจากทั้งหมดที่มี
            krathong.src = krathongImageSources[Math.floor(Math.random() * krathongImageSources.length)];
            const startX = x - (window.innerWidth / 2);
            const midX = startX + (Math.random() - 0.5) * 200;
            const endX = startX + (Math.random() - 0.5) * 400;

            krathong.style.setProperty('--tx-start', `${startX}px`);
            krathong.style.setProperty('--tx-mid', `${midX}px`);
            krathong.style.setProperty('--tx-end', `${endX}px`);

            if (options.animationDelay) {
                krathong.style.animationDelay = options.animationDelay;
            }
            krathong.style.animationDuration = options.animationDuration || '25s';
        }

        river.appendChild(krathong);

        // --- แสดงคำอธิษฐาน (ถ้ามี) ---
        if (wishText) {
            const wishElement = document.createElement('div');
            wishElement.className = 'wish-text';
            wishElement.innerText = wishText;
            wishElement.style.position = 'absolute';
            wishElement.style.left = `${x}px`;
            wishElement.style.top = `${y - 60}px`; // แสดงเหนือกระทง
            wishElement.style.color = 'white';
            wishElement.style.textShadow = '0 0 5px black';
            wishElement.style.opacity = 0;
            wishElement.style.transition = 'opacity 1s 0.5s'; // ค่อยๆ แสดงขึ้นมา
            river.appendChild(wishElement);

            setTimeout(() => { wishElement.style.opacity = 1; }, 100); //หน่วงเวลาให้แสดงผล
            setTimeout(() => { wishElement.style.opacity = 0; }, 5000); // ค่อยๆ หายไปใน 5 วินาที
            setTimeout(() => { wishElement.remove(); }, 6000);
        }
    }

    // --- สร้างกระทงของคนอื่นแบบสุ่ม ---
    function createRandomKrathong() {
        const randomX = Math.random() * window.innerWidth; // สุ่มตำแหน่งแนวนอน
        const randomDuration = 25 + Math.random() * 15; // สุ่มระยะเวลาลอย 25-40 วินาที

        // ตำแหน่ง Y ไม่จำเป็นแล้ว เพราะ animation จะจัดการให้เริ่มจากด้านล่าง
        createKrathong(randomX, 0, null, {
            animationDuration: `${randomDuration}s`
        });
    }

    // --- สร้างกระทงเริ่มต้นเมื่อเปิดหน้าเว็บ ---
    function initializeKrathongs() {
        const numberOfKrathongs = 15; // จำนวนกระทงเริ่มต้น
        for (let i = 0; i < numberOfKrathongs; i++) {
            const randomX = Math.random() * window.innerWidth;
            const randomDelay = `-${Math.random() * 30}s`; // ทำให้ animation เริ่ม ณ จุดที่ต่างกัน
            const randomDuration = 25 + Math.random() * 15;
            createKrathong(randomX, 0, null, { animationDelay: randomDelay, animationDuration: `${randomDuration}s` });
        }
    }

    // --- สร้างตัวเลือกกระทงในหน้าต่าง Modal ---
    function populateKrathongSelection() {
        krathongImageSources.forEach((src, index) => {
            const img = document.createElement('img');
            img.src = src;
            img.className = 'krathong-choice';
            img.dataset.src = src;

            // ตั้งค่าให้กระทงแรกถูกเลือกเป็นค่าเริ่มต้น
            if (index === 0) {
                img.classList.add('selected');
            }

            img.addEventListener('click', () => {
                // เอา class 'selected' ออกจากอันเก่า
                document.querySelector('.krathong-choice.selected').classList.remove('selected');
                // เพิ่ม class 'selected' ให้อันที่เพิ่งคลิก
                img.classList.add('selected');
                // อัปเดตตัวแปรที่เก็บรูปที่ถูกเลือก
                selectedKrathongSrc = img.dataset.src;
            });
            krathongSelectionContainer.appendChild(img);
        });
    }

    populateKrathongSelection(); // สร้างตัวเลือกกระทง
    initializeKrathongs();       // สร้างกระทงเริ่มต้น
    setInterval(createRandomKrathong, 2000); // ลดเวลาให้กระทงใหม่มาเร็วขึ้น
});
