<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trang Spam Nội Dung</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #000000;
            color: #ffffff;
            text-align: center;
            padding: 20px;
        }
        #content {
            font-size: 24px;
            margin-top: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #ff0000;
            color: white;
            border: none;
            border-radius: 15px;
        }
        #search-bar {
            padding: 10px;
            font-size: 16px;
            width: 80%;
            margin-top: 20px;
            background-color: #333333;
            color: white;
            border: 1px solid #444444;
            border-radius: 5px;
        }
        .input-container {
            display: flex;
            justify-content: center;
            align-items: center;
        }
        #spam-btn {
            margin-left: 10px;
            display: none;
        }
        .color-picker {
            margin-top: 20px;
        }
        .color-box {
            width: 12px;
            height: 12px;
            display: inline-block;
            margin: 3px;
            cursor: pointer;
            border-radius: 50%;
        }
        h1, p {
            color: #ffffff;
        }
        #random-box {
            margin-top: 20px;
            width: 100px;
            height: 100px;
            background-color: #333333;
            color: #ffffff;
            display: inline-block;
            line-height: 100px;
            font-size: 18px;
            border-radius: 5px;
        }

        #color-notification {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #333333;
            padding: 20px;
            border-radius: 5px;
            z-index: 1000;
        }

        #color-notification button {
            background: none;
            color: white;
            border: none;
            font-size: 20px;
            cursor: pointer;
            float: right;
        }

        #qcuong-name {
            font-size: 28px;
            display: inline-flex;
            align-items: center;
        }

        #qcuong-name i {
            color: #34b7f1;
            font-size: 20px;
            margin-left: 10px;
        }

        #spam-count-container {
            margin-top: 20px;
        }

        #spam-count-input {
            padding: 10px;
            font-size: 16px;
            width: 50px;
            background-color: #333333;
            color: white;
            border: 1px solid #444444;
            border-radius: 5px;
        }

        #spam-box {
            width: 80%;
            height: 150px;
            margin-top: 20px;
            padding: 10px;
            border-radius: 10px;
            overflow: hidden;
            font-size: 16px;
            text-align: left;
            position: relative;
            border: 5px solid transparent;
            background-image: linear-gradient(white, white), radial-gradient(circle, red, orange, yellow, green, cyan, blue, violet);
            background-origin: border-box;
            background-clip: content-box, border-box;
            animation: rainbow 4s linear infinite;
        }

        @keyframes rainbow {
            0% { background-position: 0 0; }
            100% { background-position: 400% 0; }
        }

        @keyframes redBorderAnimation {
            0% { border-color: red; border-top-color: transparent; }
            25% { border-color: transparent; border-right-color: red; }
            50% { border-color: transparent; border-bottom-color: red; }
            75% { border-color: transparent; border-left-color: red; }
            100% { border-color: red; border-top-color: transparent; }
        }

        #spam-box {
            animation: redBorderAnimation 4s linear infinite;
            border-width: 5px;
        }

        /* Thêm phần bản quyền và thông tin liên hệ */
        #footer {
            background-color: #333333;
            color: white;
            padding: 20px;
            margin-top: 40px;
            text-align: center;
        }

        #footer a {
            color: #ff5733;
            text-decoration: none;
        }

        #footer a:hover {
            text-decoration: underline;
        }

    </style>
</head>
<body>
    <h1>Trang Spam Nội Dung</h1>
    <p>Nhập nội dung cần spam và nhấn vào nút "Spam" để spam nội dung đó.</p>
    
    <div id="qcuong-name">
        <span>qcuong</span>
        <i class="fas fa-check-circle"></i>
    </div>

    <div class="input-container">
        <input type="text" id="search-bar" placeholder="Bạn muốn đặt spam gì nào?" oninput="toggleSpamButton()">
        <button id="spam-btn" onclick="spamContent()">Spam</button>
    </div>

    <div id="spam-box"></div>

    <div class="color-picker">
        <button onclick="showColorPicker()">Chọn Màu</button>
    </div>

    <div id="color-notification">
        <button onclick="closeColorPicker()">X</button>
        <h3>Danh Sách Màu:</h3>
        <div id="colors-list"></div>
    </div>

    <div id="random-box"></div>

    <div id="spam-count-container">
        <label for="spam-count-input">Số lần spam:</label>
        <input type="number" id="spam-count-input" value="10" min="1" max="100" onchange="updateSpamCount()">
    </div>

    <div id="footer">
        <p>&copy; 2024 Trang Spam Nội Dung. Tất cả các quyền được bảo lưu.</p>
        <p>Liên Hệ:quoccuong01082009@gamil.com</a></p>
    </div>

    <script>
        let selectedColor = "#ff0000"; 
        let spamCount = 10;

        function toggleSpamButton() {
            let searchInput = document.getElementById("search-bar").value;
            let spamButton = document.getElementById("spam-btn");

            if (searchInput.trim() !== "") {
                spamButton.style.display = "inline-block";
            } else {
                spamButton.style.display = "none";
            }
        }

        function spamContent() {
            let contentDiv = document.getElementById("spam-box");
            let searchInput = document.getElementById("search-bar").value;

            if (searchInput === "") {
                alert("Vui lòng nhập nội dung để spam!");
                return;
            }

            contentDiv.innerHTML = "";

            for (let i = 0; i < spamCount; i++) {
                let span = document.createElement('div');
                span.style.color = selectedColor;
                span.innerHTML = searchInput;

                contentDiv.appendChild(span);
            }
        }

        function showColorPicker() {
            let colorNotification = document.getElementById("color-notification");
            let colorsList = document.getElementById("colors-list");

            const colors = [
                "#FF5733", "#33FF57", "#5733FF", "#FF33A1", "#A1FF33",
                "#33A1FF", "#FF8133", "#8133FF", "#33FFFC", "#F433FF",
                "#FFC733", "#33FF73", "#73FF33", "#FF5733", "#FF33B8",
                "#B8FF33", "#33B8FF", "#B833FF", "#FFB833", "#33FFB8"
            ];

            colorsList.innerHTML = "";

            colors.forEach(function(color) {
                let colorDiv = document.createElement("div");
                colorDiv.className = "color-box";
                colorDiv.style.backgroundColor = color;
                colorDiv.onclick = function() {
                    selectedColor = color;
                    colorNotification.style.display = "none";
                    alert("Đã chọn màu: " + color);
                };
                colorsList.appendChild(colorDiv);
            });

            colorNotification.style.display = "block";
        }

        function closeColorPicker() {
            document.getElementById("color-notification").style.display = "none";
        }

        function updateSpamCount() {
            spamCount = document.getElementById("spam-count-input").value;
        }
    </script>
</body>
</html>
