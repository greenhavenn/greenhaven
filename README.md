<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Tiệm Cầm Đồ Hòa Du</title>
    <link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@400;600;700&family=Playfair+Display:wght@700;900&family=Chonburi&display=swap" rel="stylesheet">
    
    <style>
        body { font-family: 'Be Vietnam Pro', sans-serif; margin: 0; padding: 0; background-color: #8c765c; background-image: repeating-linear-gradient(90deg, #8c765c, #8c765c 40px, #968066 40px, #968066 80px); min-height: 100vh; display: flex; flex-direction: column; align-items: center; padding-bottom: 60px; overflow-x: hidden; touch-action: manipulation; }
        
        .butterfly { position: fixed; font-size: 20px; pointer-events: none; z-index: 9999; animation: fly 1.5s ease-out forwards; }
        @keyframes fly { 0% { transform: translate(0, 0) scale(1); opacity: 1; } 100% { transform: translate(var(--x), var(--y)) scale(0.5); opacity: 0; } }

        .store-awning { width: 100%; max-width: 950px; height: 50px; background-image: repeating-linear-gradient(90deg, #4a3319, #4a3319 35px, #e6d5b8 35px, #e6d5b8 70px); box-shadow: 0 10px 20px rgba(0,0,0,0.3); border-bottom: 5px solid #362512; position: relative; z-index: 10; }
        .store-awning::after { content: ""; position: absolute; bottom: -12px; left: 0; width: 100%; height: 12px; background-image: radial-gradient(circle at 17.5px 0, #4a3319 17.5px, transparent 18.5px); background-size: 70px 12px; }

        .wood-frame-outer { border: 8px double #362512; background: #f4ebd0; padding: 6px; max-width: 880px; width: 90%; margin-top: -2px; box-shadow: 0 15px 25px rgba(0,0,0,0.25); z-index: 5; }
        .wood-frame-inner { border: 2px solid #5c442c; padding: 20px; text-align: center; background: #fdf8eb; }
        .brand-sub { font-family: 'Playfair Display', serif; font-size: 1.2em; font-weight: 700; letter-spacing: 8px; text-transform: uppercase; color: #5c442c; }
        .brand-main { font-family: 'Chonburi', cursive; font-size: 3.8em; color: #801d1d; margin: 0; text-shadow: 2px 2px 0px #fff; }

        .search-outer-wrapper { width: 900px; max-width: 90%; display: flex; justify-content: flex-end; margin-top: 30px; }
        .search-container { background: #362512; padding: 8px 15px; border-radius: 25px; display: flex; align-items: center; border: 2px solid #5c442c; height: 35px; }
        .search-input { width: 0; opacity: 0; border: none; background: transparent; transition: all 0.4s ease; color: #e6d5b8; outline: none; padding: 0; font-size: 16px; }
        .search-btn { background: transparent; color: #e6d5b8; border: none; cursor: pointer; font-size: 1.1em; }

        .wood-shelf-container { max-width: 900px; width: 90%; margin-top: 10px; border: 14px solid #362512; background-color: #24150b; padding: 25px; box-sizing: border-box; }
        .shelf-title { color: #e6d5b8; text-align: center; font-size: 1.3em; letter-spacing: 3px; margin-bottom: 25px; text-transform: uppercase; border-bottom: 1px dashed #4a3319; padding-bottom: 10px; }
        .shelf-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; align-items: start; }
        
        .shelf-item { position: relative; background: #e8dcbf; border: 3px solid #4a3319; padding: 15px; text-align: center; display: flex; flex-direction: column; align-items: center; justify-content: center; min-height: 150px; text-decoration: none; color: inherit; transition: all 0.4s ease; overflow: hidden; cursor: pointer; box-sizing: border-box; }
        a.shelf-item:active { transform: scale(0.97); }
        a.shelf-item:hover { background: #eedfca; transform: translateY(-5px); }

        .shelf-item.expandable-item { justify-content: flex-start; }
        .shelf-item.expandable-item:hover { background: #eedfca; transform: translateY(-5px); }
        .shelf-item.expanded { grid-column: 1 / -1; background: #fdf8eb; cursor: default; transform: none !important; align-items: center; padding: 30px; }
        
        .new-badge { position: absolute; top: 5px; left: 5px; background: #801d1d; color: #fff; font-size: 0.65em; font-weight: bold; padding: 2px 5px; border-radius: 3px; animation: blink 1.5s infinite; text-transform: uppercase; }
        @keyframes blink { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }

        .backstory { display: none; line-height: 1.6; color: #2b1d0f; margin-top: 15px; font-size: 0.95em; text-align: justify; padding: 0 10px; width: 100%; box-sizing: border-box; }
        .backstory p { margin-bottom: 10px; }
        .expanded .backstory { display: block; animation: fadeIn 0.5s ease; }
        
        .btn-link, .btn-story, .close-btn { display: none; margin-top: 15px; padding: 12px 25px; text-decoration: none; border-radius: 5px; text-align: center; font-weight: bold; cursor: pointer; transition: 0.3s; width: 100%; max-width: 300px; }
        .btn-link { background: #801d1d; color: #e6d5b8; border: 2px solid #5c442c; }
        .btn-story { background: #4a6741; color: #e6d5b8; border: 2px solid #2b3d26; }
        .close-btn { background: #5c442c; color: #e6d5b8; border: 2px solid #e6d5b8; margin-top: 10px; }
        .expanded .btn-link, .expanded .btn-story, .expanded .close-btn { display: inline-block; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .item-icon { font-size: 2em; transition: 0.4s ease; }
        .expanded .item-icon { font-size: 4em; margin-bottom: 10px; }
        .item-name { font-size: 0.9em; font-weight: 700; color: #2b1d0f; text-transform: uppercase; margin: 10px 0; transition: 0.4s ease; }
        .expanded .item-name { font-size: 1.5em; color: #801d1d; }
        .item-price { font-size: 0.8em; color: #a62424; border: 1px dashed #a62424; padding: 2px 8px; }
    </style>
</head>
<body>

    <div class="store-awning"></div>
    <div class="wood-frame-outer">
        <div class="wood-frame-inner">
            <div class="brand-sub">Tiệm Cầm Đồ</div>
            <h1 class="brand-main">Hòa Du</h1>
        </div>
    </div>

    <div class="search-outer-wrapper">
        <div class="search-container" id="search-container">
            <button class="search-btn" id="search-btn">🔍</button>
            <input type="text" class="search-input" id="search-input" placeholder="Tìm kỳ vật...">
        </div>
    </div>

    <div class="wood-shelf-container">
        <div class="shelf-title">❖ Niêm Yết Kỳ Vật Thanh Lý Vãng Lai ❖</div>
        <div class="shelf-grid" id="shelf-grid">
            
            <!-- Cơm cúng (Ghim đầu) -->
            <div class="shelf-item expandable-item" id="com-an-item" onclick="expandItem(this, event)">
                <div class="new-badge">New item!</div>
                <div class="item-icon">🍚</div>
                <div class="item-name">Cơm cúng của Nguyễn Huyền An</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221bcOcgaMt5jQLphIMDlGEcpQ6H0HBawZQ%22%5D,%22action%22:%22open%22,%22userId%22:%22110546609047761147298%22,%22resourceKeys%22:%7B%7D%7D&usp=sharing" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1xBN1zFA8dB1UxwZ-7eVHeNnXJUtMJNho4MGqPakAfRE/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'com-an-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <!-- Quạt giấy -->
            <div class="shelf-item expandable-item" id="quat-nguyen-item" onclick="expandItem(this, event)">
                <div class="item-icon">🪭</div>
                <div class="item-name">Quạt giấy của Hoàng Phúc Nguyên</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221ZzWaWDfVX2GN1pbd5LPRiVZ5TwAdQrWi%22%5D,%22action%22:%22open%22,%22userId%22:%22110546609047761147298%22,%22resourceKeys%22:%7B%7D%7D&usp=sharing" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1DWflNTUK3-P1vYfVpU0I426731VpCgkyAqCJv9h_XYA/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'quat-nguyen-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <!-- Thước phim -->
            <div class="shelf-item expandable-item" id="phung-film-item" onclick="expandItem(this, event)">
                <div class="item-icon">🎞️</div>
                <div class="item-name">Thước phim nhỏ tại Thanh Phụng Ban</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221HjD8RWssMUkcEGdma6LVIsq6ElYReKsC%22%5D,%22action%22:%22open%22,%22userId%22:%22110546609047761147298%22,%22resourceKeys%22:%7B%7D%7D&usp=sharing" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1T7Ucnqnom4WvLukyEJxoWE8NpyC273CcuFlr8RGYZtA/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'phung-film-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <!-- Các mục cũ -->
            <div class="shelf-item expandable-item" id="duc-item" onclick="expandItem(this, event)">
                <div class="item-icon">📷</div>
                <div class="item-name">Máy ảnh của Lê Hoài Đức</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221KWwmGsfia3qqHuyxM6nkVVEOkSC8dWyI%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/11aeOmvfSzGgg6AIav2LPoLSxD9C79tbLljgwRLW1p6E/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'duc-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="trac-item" onclick="expandItem(this, event)">
                <div class="item-icon">🎋</div>
                <div class="item-name">Cây tre của Lương Văn Trác</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221SGqzfQA7WF8fzSrfv8rJC2DsY8oY_1Kh%22%5D,%22action%22:%22open%22,%22userId%22:%22110546609047761147298%22,%22resourceKeys%22:%7B%7D%7D&usp=sharing" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/18LEwO7KrQ_jL3NIe2WPN4Mi9E0nYscns1iivH6QNrQc/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'trac-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="duc-sen-item" onclick="expandItem(this, event)">
                <div class="item-icon">🪷</div>
                <div class="item-name">Bông sen của Phan Đình Đước</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221AiwvF12ZdCG8kHORg2Ed7WQ8qACqOO43%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1wkiiPKMuFXSvAPPIGvN-RLOxfeeFoq0KwOB9HDdrmYI/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'duc-sen-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>
            
            <div class="shelf-item expandable-item" id="antoine-item" onclick="expandItem(this, event)">
                <div class="item-icon">📓</div>
                <div class="item-name">Vở ghi của Antoine Vũ</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221N8eRBBCZDPAwebpXN7exYSfZufXBtyTC%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1LEcWJulcAWmqtQ9NtO80fDAotZJAL6W-PWeo2ChdwnA/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'antoine-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="minh-item" onclick="expandItem(this, event)">
                <div class="item-icon">✒️</div>
                <div class="item-name">Bút máy của Trần Gia Minh</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221YO9dSyLyTM-R1AOPaqKmvH0QYkGOTFS4%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1Cx0Lqv1JCJmBFd9bUeH3XF4gm469PdXiC_tlj4YH5_k/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'minh-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="khanh-item" onclick="expandItem(this, event)">
                <div class="item-icon">💍</div>
                <div class="item-name">Nhẫn bạc của Trần Gia Khánh</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221bFKm_Iuf5UUSzXvdgCo9Rzv89_ZqVV-C%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/125dtVRA50wkvss2OPWDm9Eg1jokKs0Zv/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'khanh-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="an-item" onclick="expandItem(this, event)">
                <div class="item-icon">🎣</div>
                <div class="item-name">Cần câu của Lê Phú Ân</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221QqqTNh8vcCaq8mV6xqLAYE1DRqn_eCbK%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1zQNAJDWoZjTwiv9saXOSkU4fdsLn2nFZ/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'an-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="phong-item" onclick="expandItem(this, event)">
                <div class="item-icon">🗝️</div>
                <div class="item-name">Chìa khóa của Đoàn Trường Phong</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221OuRz58yXlkC_M7J9jzxaYqKj1BK4VG1y%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1isATH21ajS_gTLljbFRGl_i-bIlrEdq-/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'phong-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>

            <div class="shelf-item expandable-item" id="chau-item" onclick="expandItem(this, event)">
                <div class="item-icon">✉️</div>
                <div class="item-name">Hòm thư của Phạm Minh Châu</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221CHzExCT58Ju8I5PeSykxQ_cXn9mE6vCe%22%5D,%22action%22:%22open%22%7D" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1MFKJi2NVvsBuTPoQ0EMQXRYeKzR2mJPh/edit?usp=sharing&ouid=110546609047761147298&rtpof=true&sd=true" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'chau-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>
            
            <div class="shelf-item expandable-item" id="khang-item" onclick="expandItem(this, event)">
                <div class="item-icon">🧵</div>
                <div class="item-name">Cuộn chỉ của Trịnh Hữu Khang</div>
                <div class="item-price">Vô Giá</div>
                <div class="backstory">
                    <div style="text-align: center; display: flex; flex-direction: column; align-items: center;">
                        <a href="https://aistudio.google.com/app/prompts?state=%7B%22ids%22:%5B%221JC8xhNdIhIse1n2BYQ3ZKgN_k9Q8xf8m%22%5D,%22action%22:%22open%22,%22userId%22:%22110546609047761147298%22,%22resourceKeys%22:%7B%7D%7D&usp=sharing" target="_blank" class="btn-link" onclick="event.stopPropagation()">Tiếp Cận Kỳ Vật Này</a>
                        <a href="https://docs.google.com/document/d/1avV9mqzLhLBrTQ2a-kI1a2G-yj1cVUXSTOOeNsSTQD8/edit?usp=sharing" target="_blank" class="btn-story" onclick="event.stopPropagation()">Backstory</a>
                        <button class="close-btn" onclick="closeItem(event, 'khang-item')">⟵ Quay lại kệ kỳ vật</button>
                    </div>
                </div>
            </div>
            
        </div>
    </div>

    <script>
        document.addEventListener('click', function(e) {
            for (let i = 0; i < 5; i++) {
                const b = document.createElement('div'); b.innerHTML = '🦋'; b.className = 'butterfly';
                b.style.left = e.clientX + 'px'; b.style.top = e.clientY + 'px';
                b.style.setProperty('--x', (Math.random()-0.5)*400 + 'px');
                b.style.setProperty('--y', (Math.random()-0.5)*400 + 'px');
                document.body.appendChild(b); setTimeout(() => b.remove(), 1500);
            }
        });

        const searchInput = document.getElementById('search-input');
        document.getElementById('search-btn').addEventListener('click', (e) => { e.stopPropagation(); searchInput.style.width = "150px"; searchInput.style.opacity = "1"; searchInput.style.padding = "0 10px"; searchInput.focus(); });
        
        searchInput.addEventListener('input', function() {
            const q = this.value.toLowerCase();
            document.querySelectorAll('.shelf-item').forEach(i => {
                i.style.display = (q === "" || i.querySelector('.item-name').textContent.toLowerCase().includes(q)) ? 'flex' : 'none';
            });
        });

        function expandItem(el, e) {
            if(e.target.tagName.toLowerCase() === 'a' || e.target.classList.contains('close-btn')) return;
            el.classList.add('expanded');
            setTimeout(() => el.scrollIntoView({ behavior: 'smooth', block: 'center' }), 100);
        }

        function closeItem(e, id) { 
            e.stopPropagation(); 
            document.getElementById(id).classList.remove('expanded'); 
        }

        document.addEventListener('click', (e) => {
            if (!document.getElementById('search-container').contains(e.target)) {
                searchInput.style.width = "0"; searchInput.style.opacity = "0"; searchInput.style.padding = "0";
            }
            const items = document.querySelectorAll('.shelf-item');
            items.forEach(item => {
                if (!item.contains(e.target)) item.classList.remove('expanded');
            });
        });
    </script>
</body>
</html>
