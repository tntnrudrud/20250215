<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>whomadethis_site?!</title><!-- [변경] 사이트 제목 변경 가능 -->
<style>
    /* 기본 스타일 */
    body {
        margin: 0;
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: black;
        color: white;
        font-family: Arial, sans-serif;
        overflow: hidden;
    }

    #giftBox {
        width: 500px;
        height: 500px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #giftImage {
        max-width: 100%;
        max-height: 100%;
        object-fit: contain;
        display: block;
    }

    #openButton {
        font-size: 20px;
        color: #8A754B;
        background-color: transparent;
        border: 2px solid #8A754B;
        padding: 10px 20px;
        cursor: pointer;
        outline: none;
        transition: background-color 0.3s, color 0.3s, opacity 0.3s;
        margin-top: 20px;
    }
    #openButton:hover {
        box-shadow: 0 0 15px #FFFFFF;
    }
    #openButton:active {
        opacity: 0;
        transition: opacity 0.3s;
    }

    /* 🎁 상자 흔들림 효과 */
    @keyframes shake {
        0% { transform: translateX(0); }
        20% { transform: translateX(-5px); }
        40% { transform: translateX(5px); }
        60% { transform: translateX(-5px); }
        80% { transform: translateX(5px); }
        100% { transform: translateX(0); }
    }

    /* ✨ 메시지 반짝임 효과 */
    @keyframes glow {
        0% { box-shadow: 0 0 10px #ffdd57; }
        50% { box-shadow: 0 0 40px #ffdd57; }
        100% { box-shadow: 0 0 10px #ffdd57; }
    }

    /* 🎈 이미지 애니메이션 (위 → 아래로 계속 흐름) */
    @keyframes fallingObjects {
        0% {
            transform: translateY(-100vh) rotate(0deg);
            opacity: 1;
        }
        100% {
            transform: translateY(100vh) rotate(360deg);
            opacity: 0;
        }
    }

    .fallingImage {
        position: absolute;
        opacity: 0;
        animation: fallingObjects linear infinite;
    }

</style>
</head>
<body>

<div id="title"><h1>To. 대주주 봉지퐁지</h1></div> <!-- [변경] 제목 변경 가능 -->
<div id="giftBox">
    <img id="giftImage" src="box.png" alt="선물 상자">
</div>
<button id="openButton">열어봐</button> 

<!-- 🎈 이미지 컨테이너 -->
<div id="imageContainer"></div>

<script>
    // 원하는 이미지 파일 배열 (여기에 추가하면 랜덤으로 사용됨)
    const imageSources = [
        "1.png",  // 🎈 대신 사용할 이미지 1
        "2.png",  // 🎈 대신 사용할 이미지 2
        "3.png",  // 🎈 대신 사용할 이미지 3
    ];

    function openScreen() {
        const giftImage = document.getElementById('giftImage');
        const openButton = document.getElementById('openButton');
        const title = document.getElementById('title');

        // 🎁 1. 상자 흔들림 효과
        giftImage.style.animation = "shake 0.5s ease-in-out";

        setTimeout(() => {
            // 🎁 2. 상자 열림
            giftImage.src = "box.gif";
        }, 500);

        // 🎁 3. 메시지 등장 + 반짝이는 효과
        setTimeout(() => {
            giftImage.src = "gift1.png";
            giftImage.style.width = "auto";
            giftImage.style.height = "100%";  
            giftImage.style.animation = "glow 1.5s infinite alternate"; // 메시지 반짝이는 효과

            // 🎈 4. 이미지 애니메이션 시작
            startFallingImages();
        }, 2000);

        // 버튼 및 제목 숨기기
        openButton.style.display = 'none';
        title.style.display = 'none';
    }
    
    // 버튼 이벤트 리스너 추가
    document.getElementById('openButton').addEventListener('click', openScreen);

    function startFallingImages() {
        const imageContainer = document.getElementById('imageContainer');

        for (let i = 0; i < 30; i++) {  // 🎈 이미지 개수 증가
            let img = document.createElement('img');
            img.className = 'fallingImage';
            img.src = imageSources[Math.floor(Math.random() * imageSources.length)]; // 랜덤 이미지 선택

            // 🌈 이미지 크기 랜덤 설정
            let size = Math.random() * 50 + 50; // 50px ~ 100px 크기
            img.style.width = `${size}px`;
            img.style.height = `${size}px`;

            // 🏆 이미지 시작 위치 랜덤 설정
            let startX = Math.random() * window.innerWidth; // 화면 가로폭 내 랜덤 위치
            img.style.left = `${startX}px`;

            // 🚀 이미지 애니메이션 속도 및 지연 랜덤 설정
            let duration = Math.random() * 5 + 3; // 3초 ~ 8초 동안 떨어짐
            let delay = Math.random() * 3; // 최대 3초 지연 시작
            img.style.animationDuration = `${duration}s`;
            img.style.animationDelay = `${delay}s`;

            imageContainer.appendChild(img);

            // 🌪 이미지가 사라질 때 제거
            setTimeout(() => {
                img.remove();
            }, (duration + delay) * 1000);
        }

        // 🎈 이미지가 무한 반복되도록 일정 시간마다 생성
        setTimeout(startFallingImages, 3000);
    }

</script>

</body>
</html>
