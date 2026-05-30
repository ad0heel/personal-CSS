<img width="682" height="1246" alt="image" src="https://github.com/user-attachments/assets/3c8ce720-7717-4f44-9f42-14c2a828759b" />
## Luna Deck
### 正面模版内容
```
<div class="hide-style" style="display: none;">
    <div id="audio">{{audio_for_word}}</div>
    <div id="audio_sentence">{{audio_for_example_sentence}}</div>
</div>

<div class="card-container">
    <div class="word-card" onclick='playAudio("audio")'>
        <div class="ruby-div" id="word">{{ word }}</div>
        <div id="rubyword" class="ruby-div">{{ rubytextHtml }}</div>
    </div>

    <div id="example_sentence" class="example-box" onclick='playAudio("audio_sentence")'>
        {{example_sentence}}
    </div>

    <div id="image" class="screenshot-box">
        {{screenshot}}
    </div>
</div>

<script>
    if (document.getElementById('rubyword').innerHTML.trim().length > 0) {
        document.getElementById('word').style.display = 'none';
    }
    else {
        document.getElementById('rubyword').style.display = 'none';
    }
</script>

<script>
    function playAudio(audioId) {
        var audioDiv = document.getElementById(audioId);
        var audio = audioDiv.getElementsByTagName('*');
        if (audio.length > 0) {
            audio[0].click();
        }
    }
    function checkhide(eid) {
        var emptyDiv = document.getElementById(eid);
        if (emptyDiv && emptyDiv.innerText.trim() === "") {
            emptyDiv.style.display = 'none';
        }
    }
    function checkhide2(eid) {
        var emptyDiv = document.getElementById(eid);
        if (emptyDiv && emptyDiv.children.length == 0) {
            emptyDiv.style.display = 'none';
        }
    }
    checkhide("example_sentence")
    checkhide2("image")
</script>
```
### 背面模版内容
```
<!-- 音訊隱藏區塊 -->
<div class="hide-style" style="display: none;">
    <div id="audio">{{audio_for_word}}</div>
    <div id="audio_sentence">{{audio_for_example_sentence}}</div>
</div>

<div class="card-container">
    <!-- 主單字區塊 -->
    <div class="word-card" onclick='playAudio("audio")'>
        <div class="ruby-div" id="word">{{ word }}</div>
        <div id="rubyword" class="ruby-div">{{ rubytextHtml }}</div>
    </div>

    <!-- 遊戲例句區塊 -->
    <div id="example_sentence" class="example-box" onclick='playAudio("audio_sentence")'>
        {{example_sentence}}
    </div>

    <!-- 遊戲截圖區塊 -->
    <div id="image" class="screenshot-box">
        {{screenshot}}
    </div>

    <!-- 備註區塊 -->
    <div id="remarks" class="remarks-box">
        {{remarks}}
    </div>

    <!-- LunaTranslator 字典頁籤區塊 -->
    <div class="tab-widget">
        <div id="tab_buttons" class="tab-buttons-container"></div>
        <div class="tab-contents-container">
            <div class="tab-content" id="tab_contents"></div>
        </div>
    </div>
</div>

<script>
    if (document.getElementById('rubyword').innerHTML.trim().length > 0) {
        document.getElementById('word').style.display = 'none';
    }
    else {
        document.getElementById('rubyword').style.display = 'none';
    }
</script>

<script>
    function onclickbtn(_id) {
        var tabButtons = document.querySelectorAll('.tab-widget .tab-button');
        var tabPanes = document.querySelectorAll('.tab-widget .tab-pane');
        for (var i = 0; i < tabButtons.length; i++)
            tabButtons[i].classList.remove('active');
        for (var i = 0; i < tabPanes.length; i++)
            tabPanes[i].classList.remove('active');

        document.getElementById('luna_dict_btn_' + _id).classList.add('active');
        document.getElementById('luna_dict_tab_' + _id).classList.add('active');
    }
</script>

<script>
    var dictionaryInfo = {{ dictionaryInfo }};
    var dictionaryContent = {{ dictionaryContent }}
    var htmltabbuttons = ''
    var htmlcontents = ''
    var scriptElementss = []
    var scriptElementsssrc = []
    if (dictionaryInfo.length == 1) {
        document.getElementById('tab_buttons').style.display = 'none'
    }
    for (var iiii = 0; iiii < dictionaryInfo.length; iiii++) {
        htmltabbuttons += '<button type="button" onclick="onclickbtn(\'' + dictionaryInfo[iiii]['dict'] + '\')" id="luna_dict_btn_' + dictionaryInfo[iiii]['dict'] + '" class="tab-button' + (iiii == 0 ? ' active' : '') + '">' + dictionaryInfo[iiii]['name'] + '</button>'

        var tempParent = document.createElement('div');
        tempParent.innerHTML = decodeURIComponent(dictionaryContent[dictionaryInfo[iiii]['dict']]);

        var fragment = document.createElement('div');
        while (tempParent.firstChild) {
            fragment.appendChild(tempParent.firstChild);
        }

        htmlcontents += '<div id="luna_dict_tab_' + dictionaryInfo[iiii]['dict'] + '" class="tab-pane' + (iiii == 0 ? ' active' : '') + '">' + fragment.innerHTML + '</div>'
        var scriptElements = fragment.getElementsByTagName('script');

        for (var jjjj = 0; jjjj < scriptElements.length; jjjj++) {
            scriptElementss.push(scriptElements[jjjj].textContent)
            scriptElementsssrc.push(scriptElements[jjjj].src)
        }
    }
    document.getElementById('tab_buttons').innerHTML = htmltabbuttons
    document.getElementById('tab_contents').innerHTML = htmlcontents
    for (var iiii = 0; iiii < scriptElementss.length; iiii++) {
        eval(scriptElementss[iiii])
        let newScript = document.createElement('script')
        if (scriptElementsssrc[iiii]) {
            newScript.src = scriptElementsssrc[iiii];
            document.head.appendChild(newScript);
        }
    }
</script>

<script>
    function playAudio(audioId) {
        var audioDiv = document.getElementById(audioId);
        var audio = audioDiv.getElementsByTagName('*');
        if (audio.length > 0) {
            audio[0].click();
        }
    }
    function checkhide(eid) {
        var emptyDiv = document.getElementById(eid);
        if (emptyDiv && emptyDiv.innerText.trim() === "") {
            emptyDiv.style.display = 'none';
        }
    }
    function checkhide2(eid) {
        var emptyDiv = document.getElementById(eid);
        if (emptyDiv && emptyDiv.children.length == 0) {
            emptyDiv.style.display = 'none';
        }
    }
    checkhide("example_sentence")
    checkhide2("image")
    checkhide("remarks")
</script>
```
### CSS
```
/* 全域卡片容器調整 */
.card-container {
    max-width: 600px;
    margin: 0 auto;
    padding: 10px;
    font-family: "Helvetica Neue", Helvetica, Arial, "Hiragino Kaku Gothic ProN", "Microsoft JhengHei", sans-serif;
}

/* 主單字區塊優化：放大字體，增加行高與呼吸空間 */
.word-card {
    font-size: 42px;
    font-weight: bold;
    text-align: center;
    margin-top: 15px;
    margin-bottom: 25px;
    line-height: 1.8;
    cursor: pointer;
    transition: opacity 0.2s;
}
.word-card:active {
    opacity: 0.7;
}

/* 內建日文注音的字體與間距微調 */
.word-card ruby {
    ruby-position: over;
}
.word-card rt {
    font-size: 16px;
    font-weight: normal;
    padding-bottom: 4px;
    letter-spacing: 0.05em;
}

.example-box {
    font-size: 20px;
    line-height: 1.8;
    color: #;
    text-align: center;
    background-color: transparent;
    padding: 15px 20px;
    border-radius: 10px;
    margin-bottom: 25px;
    cursor: pointer;
    border-left: none; /* 移除原本的 > 效果 */
    transition: background 0.4s, text-shadow 0.7s ease, color 0.3s ease; 
}
.example-box:hover {
    background-color: transparent; /* 滑鼠移過去也保持背景透明 */
    color: #ffffff; 
    text-shadow: 
        0 0 5px rgba(255, 255, 255, 0.6),  
        0 0 10px #00fff6,                 
        0 0 15px #00fff6;            
     
}/* 遊戲截圖排版 */
.screenshot-box {
    text-align: center;
    margin-bottom: 25px;
}
.screenshot-box img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
}

/* 備註欄位樣式 */
.remarks-box {
    font-size: 16px;
    line-height: 1.6;
    color: #aaaaaa;
    text-align: center;
    margin-bottom: 25px;
    padding: 0 10px;
}

/* LunaTranslator 字典分頁樣式現代化 */
.tab-widget {
    margin-top: 30px;
    border-top: 1px solid #444;
    padding-top: 20px;
}

.tab-buttons-container {
    display: flex;
    justify-content: center;
    gap: 8px;
    flex-wrap: wrap;
    margin-bottom: 15px;
}

/* 頁籤按鈕美化 */
.tab-button {
    background-color: #333;
    color: #ccc;
    border: none;
    padding: 8px 16px;
    font-size: 14px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.2s;
}
.tab-button:hover {
    background-color: #444;
}
.tab-button.active {
    background-color: #00adb5;
    color: #fff;
    font-weight: bold;
}

/* 字典內容框 */
.tab-contents-container {
    background-color: #252525;
    border-radius: 8px;
    padding: 16px;
    text-align: left;
    box-shadow: inset 0 2px 4px rgba(0,0,0,0.2);
}

.tab-pane {
    display: none;
    font-size: 15px;
    line-height: 1.6;
}
.tab-pane.active {
    display: block;
}
```
