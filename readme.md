---
title: 選擇題測驗卷網站講義（學生版）.md

---

---
title: 選擇題測驗卷網站講義（學生版）

---

---
title: 選擇題測驗卷網站講義（學生版）
tags: [114程式設計與實習_上學期]

---

# 選擇題測驗卷網站講義（學生版）

學號：415730307　　姓名：許方璞

> **填寫方式**
> 1. 每個學習都要放：**執行截圖**、**三次問 AI 的提示詞**、**最後採用的程式碼**。
> 2. 問 AI 的提示詞請**逐字貼上**自己實際輸入的內容（不要寫摘要），第一次、第二次、第三次依序記錄。
> 3. 程式碼貼在「點開貼上」的收合區塊裡，貼上**你最後真正採用、而且能執行**的版本。

---

## 學習1：產生一個選擇題測驗卷網站

https://cfchen58.synology.me/115/week4/stage1/

**這個階段的目標：** 用 p5.js 做出一個一次顯示一題、四個選項、答完會顯示對錯與總分的測驗網站（題目先寫在程式裡）。
**這個階段會修改的檔案：** index.html、sketch.js

### 執行截圖

![螢幕擷取畫面 2026-10-08 143120](https://hackmd.io/_uploads/B1F8YhEoMx.png)

![螢幕擷取畫面 2026-10-08 143152](https://hackmd.io/_uploads/BkMftnEsMx.png)

[![學習1影片][](https://drive.google.com/file/d/10oKTx-aUwNSyrKZrscGVKi-vtj3x06RE/view?usp=drive_link)](https://drive.google.com/file/d/10oKTx-aUwNSyrKZrscGVKi-vtj3x06RE/view?usp=drive_link)

### 第一次問 AI

```tex!
使用p5.js撰寫一個選擇題網站測驗系統，我已經產生了一個p5.js專案，請把程式碼寫成可以放到sketch.js檔案內，每條指令都需要加上中文註解。測驗系統題目設定為五題，測驗題目的內容為程式設計p5.js簡易指令練習測驗，系統採用全螢幕，使用者答錯時，系統會在正確答案上，加上6a994e背景顏色，該選項要上下跳動，答錯的選項採用780000背景顏色。選擇題選項共有四個，當五題結束後，需要顯示答對的題數每次顯示一個題目薛要有上一題及下一題的按鈕分別在最下方左右邊，整體畫面都要置中對齊
```

### 第二次問 AI

```tex!
使用p5.js撰寫一個選擇題網站測驗系統，我已經產生了一個p5.js專案，請把程式碼寫成可以放到sketch.js檔案內，每條指令都需要加上中文註解。測驗系統題目設定為五題，測驗題目的內容為程式設計p5.js簡易指令練習測驗，系統採用全螢幕，使用者答錯時，系統會在正確答案上，加上6a994e背景顏色，該選項要上下跳動，答錯的選項採用780000背景顏色，使用者答對時，系統會在正確答案上，加上6a994e背景顏色，該選項要上下跳動。選擇題選項共有四個，當五題結束後，需要顯示答對的題數每次顯示一個題目薛要有上一題及下一題的按鈕分別在最下方左右邊，整體畫面都要置中對齊
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習1的程式碼
```javascript=
// 建立五題 p5.js 簡易指令選擇題資料
const quizData = [ // 宣告測驗題目陣列
  { // 建立第一題物件
    question: "在 p5.js 中，哪一個函式只會在程式開始時執行一次？", // 設定第一題題目
    options: ["draw()", "setup()", "start()", "begin()"], // 設定第一題四個選項
    answer: 1 // 設定第一題正確答案為第二個選項
  }, // 結束第一題物件
  { // 建立第二題物件
    question: "在 p5.js 中，哪一個函式會持續重複執行？", // 設定第二題題目
    options: ["setup()", "repeat()", "draw()", "loopStart()"], // 設定第二題四個選項
    answer: 2 // 設定第二題正確答案為第三個選項
  }, // 結束第二題物件
  { // 建立第三題物件
    question: "哪一個 p5.js 指令可以建立畫布？", // 設定第三題題目
    options: ["createCanvas()", "makeCanvas()", "canvasSize()", "newCanvas()"], // 設定第三題四個選項
    answer: 0 // 設定第三題正確答案為第一個選項
  }, // 結束第三題物件
  { // 建立第四題物件
    question: "哪一個 p5.js 指令可以畫出橢圓形？", // 設定第四題題目
    options: ["circle()", "ellipse()", "oval()", "round()"], // 設定第四題四個選項
    answer: 1 // 設定第四題正確答案為第二個選項
  }, // 結束第四題物件
  { // 建立第五題物件
    question: "哪一個 p5.js 指令可以設定畫布背景顏色？", // 設定第五題題目
    options: ["background()", "backColor()", "setBackground()", "canvasColor()"], // 設定第五題四個選項
    answer: 0 // 設定第五題正確答案為第一個選項
  } // 結束第五題物件
]; // 結束測驗題目陣列

let currentQuestion = 0; // 儲存目前顯示的題目編號
let score = 0; // 儲存使用者答對的題數
let quizFinished = false; // 儲存測驗是否已經完成
let selectedAnswers = []; // 儲存每一題使用者選擇的答案
let answeredQuestions = []; // 儲存每一題是否已經作答
let correctAnswers = []; // 儲存每一題是否答對

const correctColor = "#6a994e"; // 設定正確答案背景顏色
const wrongColor = "#780000"; // 設定錯誤答案背景顏色
const normalColor = "#457b9d"; // 設定一般按鈕背景顏色
const backgroundColor = "#f1faee"; // 設定畫面背景顏色
const textColor = "#1d3557"; // 設定主要文字顏色

let layout = {}; // 建立響應式版面資料物件

function setup() { // 建立 p5.js 初始化函式
  createCanvas(windowWidth, windowHeight); // 建立符合視窗大小的畫布
  textAlign(CENTER, CENTER); // 設定文字水平與垂直置中
  rectMode(CENTER); // 設定矩形以中心點作為定位基準
  textFont("Arial"); // 設定使用一般英文字型
  initializeQuiz(); // 初始化測驗資料
  updateLayout(); // 計算響應式版面位置
  tryEnterFullscreen(); // 嘗試進入全螢幕模式
} // 結束 setup 函式

function initializeQuiz() { // 建立初始化測驗資料函式
  currentQuestion = 0; // 將目前題目設定為第一題
  score = 0; // 將分數歸零
  quizFinished = false; // 將測驗狀態設定為未完成
  selectedAnswers = Array(quizData.length).fill(-1); // 初始化每一題的答案為未選擇
  answeredQuestions = Array(quizData.length).fill(false); // 初始化每一題為尚未作答
  correctAnswers = Array(quizData.length).fill(false); // 初始化每一題為尚未判定
} // 結束 initializeQuiz 函式

function tryEnterFullscreen() { // 建立嘗試進入全螢幕函式
  setTimeout(() => { // 延遲執行全螢幕功能
    if (!fullscreen()) { // 判斷目前是否尚未全螢幕
      fullscreen(true); // 將畫面切換到全螢幕
    } // 結束全螢幕判斷
  }, 500); // 設定延遲五百毫秒執行
} // 結束 tryEnterFullscreen 函式

function draw() { // 建立 p5.js 主要繪圖函式
  background(backgroundColor); // 設定畫布背景顏色
  updateLayout(); // 每一幀重新計算響應式版面
  if (quizFinished) { // 判斷測驗是否完成
    drawResultScreen(); // 顯示測驗結果畫面
  } else { // 執行尚未完成測驗的畫面
    drawQuizScreen(); // 顯示題目測驗畫面
  } // 結束測驗狀態判斷
} // 結束 draw 函式

function updateLayout() { // 建立計算響應式版面的函式
  const contentWidth = min(width * 0.86, 900); // 計算主要內容最大寬度
  const optionWidth = min(width * 0.78, 720); // 計算選項按鈕寬度
  const optionHeight = constrain(height * 0.075, 48, 72); // 計算選項按鈕高度
  const optionGap = constrain(height * 0.018, 10, 18); // 計算選項按鈕間距
  layout.centerX = width / 2; // 設定畫面中央水平位置
  layout.contentWidth = contentWidth; // 儲存主要內容寬度
  layout.optionWidth = optionWidth; // 儲存選項按鈕寬度
  layout.optionHeight = optionHeight; // 儲存選項按鈕高度
  layout.optionGap = optionGap; // 儲存選項按鈕間距
  layout.questionY = height * 0.25; // 設定題目文字垂直位置
  layout.firstOptionY = height * 0.43; // 設定第一個選項垂直位置
  layout.navigationY = height - 54; // 設定底部按鈕垂直位置
  layout.navigationWidth = min(width * 0.23, 180); // 設定底部按鈕寬度
  layout.navigationHeight = 48; // 設定底部按鈕高度
} // 結束 updateLayout 函式

function drawQuizScreen() { // 建立繪製測驗畫面的函式
  const question = quizData[currentQuestion]; // 取得目前題目資料
  const answered = answeredQuestions[currentQuestion]; // 取得目前題目的作答狀態

  fill(textColor); // 設定標題文字顏色
  noStroke(); // 移除文字外框
  textSize(constrain(width * 0.045, 26, 48)); // 設定標題文字大小
  text("p5.js 簡易指令練習測驗", layout.centerX, height * 0.07); // 顯示測驗標題

  fill(textColor); // 設定題號文字顏色
  textSize(constrain(width * 0.025, 18, 28)); // 設定題號文字大小
  text(`第 ${currentQuestion + 1} 題／共 ${quizData.length} 題`, layout.centerX, height * 0.14); // 顯示目前題號

  fill(textColor); // 設定題目文字顏色
  textSize(constrain(width * 0.03, 20, 34)); // 設定題目文字大小
  text(question.question, layout.centerX, layout.questionY, layout.contentWidth, 90); // 顯示題目內容

  for (let i = 0; i < question.options.length; i++) { // 逐一處理四個答案選項
    let optionY = layout.firstOptionY + i * (layout.optionHeight + layout.optionGap); // 計算目前選項位置
    let optionColor = normalColor; // 設定選項預設背景顏色
    let bounceY = 0; // 設定選項預設不移動

    if (answered) { // 判斷目前題目是否已經作答
      if (i === question.answer) { // 判斷目前選項是否為正確答案
        optionColor = correctColor; // 將正確答案背景設定為指定綠色
        bounceY = sin(frameCount * 0.16) * 8; // 讓正確答案上下跳動
      } // 結束正確答案判斷

      if (i === selectedAnswers[currentQuestion] && !correctAnswers[currentQuestion]) { // 判斷是否為使用者答錯的選項
        optionColor = wrongColor; // 將錯誤答案背景設定為指定深紅色
      } // 結束錯誤答案判斷
    } // 結束作答狀態判斷

    drawOptionButton(question.options[i], layout.centerX, optionY + bounceY, optionColor); // 繪製目前選項按鈕
  } // 結束四個選項的迴圈

  drawNavigationButtons(); // 繪製底部上一題與下一題按鈕
} // 結束 drawQuizScreen 函式

function drawOptionButton(label, x, y, colorValue) { // 建立繪製選項按鈕函式
  fill(colorValue); // 設定選項按鈕背景顏色
  stroke("#1d3557"); // 設定選項按鈕外框顏色
  strokeWeight(2); // 設定選項按鈕外框粗細
  rect(x, y, layout.optionWidth, layout.optionHeight, 12); // 繪製圓角選項按鈕
  fill("#ffffff"); // 設定選項文字為白色
  noStroke(); // 移除文字外框
  textSize(constrain(width * 0.025, 16, 25)); // 設定選項文字大小
  text(label, x, y, layout.optionWidth * 0.9, layout.optionHeight * 0.8); // 顯示選項文字
} // 結束 drawOptionButton 函式

function drawNavigationButtons() { // 建立繪製底部導覽按鈕函式
  const previousX = layout.navigationWidth / 2 + 24; // 計算上一題按鈕水平位置
  const nextX = width - layout.navigationWidth / 2 - 24; // 計算下一題按鈕水平位置
  const previousDisabled = currentQuestion === 0; // 判斷上一題按鈕是否停用
  const nextDisabled = !answeredQuestions[currentQuestion]; // 判斷下一題按鈕是否停用
  const nextLabel = currentQuestion === quizData.length - 1 ? "完成測驗" : "下一題"; // 設定下一題按鈕文字

  drawNavigationButton("上一題", previousX, layout.navigationY, previousDisabled); // 繪製上一題按鈕
  drawNavigationButton(nextLabel, nextX, layout.navigationY, nextDisabled); // 繪製下一題按鈕
} // 結束 drawNavigationButtons 函式

function drawNavigationButton(label, x, y, disabled) { // 建立繪製導覽按鈕函式
  fill(disabled ? "#a8dadc" : "#1d3557"); // 根據按鈕狀態設定背景顏色
  stroke("#1d3557"); // 設定按鈕外框顏色
  strokeWeight(2); // 設定按鈕外框粗細
  rect(x, y, layout.navigationWidth, layout.navigationHeight, 10); // 繪製導覽按鈕
  fill("#ffffff"); // 設定導覽按鈕文字顏色
  noStroke(); // 移除文字外框
  textSize(constrain(width * 0.021, 15, 22)); // 設定導覽按鈕文字大小
  text(label, x, y); // 顯示導覽按鈕文字
} // 結束 drawNavigationButton 函式

function drawResultScreen() { // 建立繪製結果畫面的函式
  fill(textColor); // 設定結果標題文字顏色
  noStroke(); // 移除文字外框
  textSize(constrain(width * 0.05, 30, 60)); // 設定結果標題文字大小
  text("測驗完成！", layout.centerX, height * 0.28); // 顯示測驗完成文字

  fill(correctColor); // 設定分數文字顏色
  textSize(constrain(width * 0.045, 26, 52)); // 設定分數文字大小
  text(`你答對了 ${score}／${quizData.length} 題`, layout.centerX, height * 0.42); // 顯示使用者答對題數

  fill(textColor); // 設定評語文字顏色
  textSize(constrain(width * 0.027, 18, 30)); // 設定評語文字大小
  if (score === quizData.length) { // 判斷是否全部答對
    text("太棒了！全部答對！", layout.centerX, height * 0.53); // 顯示滿分評語
  } else if (score >= 3) { // 判斷是否答對三題以上
    text("表現很好，繼續練習會更熟悉！", layout.centerX, height * 0.53); // 顯示鼓勵評語
  } else { // 執行未達三題答對的情況
    text("再多練習幾次，就會越來越熟悉！", layout.centerX, height * 0.53); // 顯示練習評語
  } // 結束分數評語判斷

  const restartY = height * 0.68; // 設定重新開始按鈕垂直位置
  fill("#1d3557"); // 設定重新開始按鈕背景顏色
  stroke("#1d3557"); // 設定重新開始按鈕外框顏色
  strokeWeight(2); // 設定重新開始按鈕外框粗細
  rect(layout.centerX, restartY, min(width * 0.35, 260), 58, 10); // 繪製重新開始按鈕
  fill("#ffffff"); // 設定重新開始文字顏色
  noStroke(); // 移除文字外框
  textSize(constrain(width * 0.025, 17, 25)); // 設定重新開始文字大小
  text("重新開始", layout.centerX, restartY); // 顯示重新開始文字
} // 結束 drawResultScreen 函式

function mousePressed() { // 建立滑鼠按下事件函式
  if (quizFinished) { // 判斷測驗是否已經結束
    const restartY = height * 0.68; // 設定重新開始按鈕垂直位置
    if (isInsideButton(mouseX, mouseY, layout.centerX, restartY, min(width * 0.35, 260), 58)) { // 判斷是否點擊重新開始
      initializeQuiz(); // 重新初始化測驗
    } // 結束重新開始判斷
    return; // 結束結果畫面滑鼠事件
  } // 結束測驗完成判斷

  const question = quizData[currentQuestion]; // 取得目前題目資料

  if (!answeredQuestions[currentQuestion]) { // 判斷目前題目是否尚未作答
    for (let i = 0; i < question.options.length; i++) { // 逐一檢查四個選項
      const optionY = layout.firstOptionY + i * (layout.optionHeight + layout.optionGap); // 計算目前選項位置
      if (isInsideButton(mouseX, mouseY, layout.centerX, optionY, layout.optionWidth, layout.optionHeight)) { // 判斷是否點擊目前選項
        selectedAnswers[currentQuestion] = i; // 記錄使用者選擇的選項
        answeredQuestions[currentQuestion] = true; // 記錄目前題目已經作答
        correctAnswers[currentQuestion] = i === question.answer; // 判斷使用者答案是否正確
        if (correctAnswers[currentQuestion]) { // 判斷使用者是否答對
          score++; // 將答對題數增加一題
        } // 結束答對判斷
        break; // 結束選項檢查迴圈
      } // 結束選項點擊判斷
    } // 結束選項檢查迴圈
  } // 結束尚未作答判斷

  const previousX = layout.navigationWidth / 2 + 24; // 計算上一題按鈕水平位置
  const nextX = width - layout.navigationWidth / 2 - 24; // 計算下一題按鈕水平位置

  if (currentQuestion > 0 && isInsideButton(mouseX, mouseY, previousX, layout.navigationY, layout.navigationWidth, layout.navigationHeight)) { // 判斷是否點擊上一題
    currentQuestion--; // 回到上一題
    return; // 結束本次滑鼠事件
  } // 結束上一題判斷

  if (answeredQuestions[currentQuestion] && isInsideButton(mouseX, mouseY, nextX, layout.navigationY, layout.navigationWidth, layout.navigationHeight)) { // 判斷是否點擊下一題或完成測驗
    if (currentQuestion === quizData.length - 1) { // 判斷是否位於最後一題
      quizFinished = true; // 將測驗狀態設定為完成
    } else { // 執行尚未到最後一題的情況
      currentQuestion++; // 前往下一題
    } // 結束最後一題判斷
  } // 結束下一題判斷
} // 結束 mousePressed 函式

function isInsideButton(pointX, pointY, buttonX, buttonY, buttonWidth, buttonHeight) { // 建立判斷座標是否在按鈕內的函式
  const left = buttonX - buttonWidth / 2; // 計算按鈕左邊界
  const right = buttonX + buttonWidth / 2; // 計算按鈕右邊界
  const top = buttonY - buttonHeight / 2; // 計算按鈕上邊界
  const bottom = buttonY + buttonHeight / 2; // 計算按鈕下邊界
  return pointX >= left && pointX <= right && pointY >= top && pointY <= bottom; // 回傳座標是否位於按鈕範圍內
} // 結束 isInsideButton 函式

function keyPressed() { // 建立鍵盤按下事件函式
  if (key === "f" || key === "F") { // 判斷使用者是否按下 F 鍵
    fullscreen(!fullscreen()); // 切換全螢幕狀態
  } // 結束全螢幕切換判斷
} // 結束 keyPressed 函式

function windowResized() { // 建立視窗尺寸改變事件函式
  resizeCanvas(windowWidth, windowHeight); // 重新調整畫布大小
  updateLayout(); // 重新計算響應式版面
} // 結束 windowResized 函式

```
:::


---

## 學習2：網頁設定為響應式網頁

https://cfchen58.synology.me/115/week4/stage2/

**這個階段的目標：** 讓網站在電腦、平板、手機（直向與橫向）都能正常顯示，視窗大小改變時版面自動調整。
**這個階段會修改的檔案：** index.html、sketch.js

### 執行截圖


![螢幕擷取畫面 2026-10-08 144252](https://hackmd.io/_uploads/BJF3jhEjzl.png)
![螢幕擷取畫面 2026-10-08 144314](https://hackmd.io/_uploads/HkJpinEjMe.png)



### 第一次問 AI

```tex!
延續上一個指令，讓網站在電腦、平板、手機（直向與橫向）都能正常顯示，視窗大小改變時版面自動調整
```

### 第二次問 AI

```tex!
延續上一個指令，讓網站在電腦、平板、手機（直向與橫向）都能正常顯示，視窗大小改變時版面自動調整，內容大小自動調整，讓內容不被遮擋，使用者可以完整檢視
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習2的程式碼
```javascript=
// 建立五題 p5.js 簡易指令選擇題資料
const quizData = [ // 宣告測驗題目陣列
  { // 建立第一題資料
    question: "在 p5.js 中，哪一個函式只會在程式開始時執行一次？", // 設定第一題題目
    options: ["draw()", "setup()", "start()", "begin()"], // 設定第一題四個選項
    answer: 1 // 設定第一題正確答案
  }, // 結束第一題資料
  { // 建立第二題資料
    question: "在 p5.js 中，哪一個函式會持續重複執行？", // 設定第二題題目
    options: ["setup()", "repeat()", "draw()", "loopStart()"], // 設定第二題四個選項
    answer: 2 // 設定第二題正確答案
  }, // 結束第二題資料
  { // 建立第三題資料
    question: "哪一個 p5.js 指令可以建立畫布？", // 設定第三題題目
    options: ["createCanvas()", "makeCanvas()", "canvasSize()", "newCanvas()"], // 設定第三題四個選項
    answer: 0 // 設定第三題正確答案
  }, // 結束第三題資料
  { // 建立第四題資料
    question: "哪一個 p5.js 指令可以畫出橢圓形？", // 設定第四題題目
    options: ["circle()", "ellipse()", "oval()", "round()"], // 設定第四題四個選項
    answer: 1 // 設定第四題正確答案
  }, // 結束第四題資料
  { // 建立第五題資料
    question: "哪一個 p5.js 指令可以設定背景顏色？", // 設定第五題題目
    options: ["background()", "backColor()", "setBackground()", "canvasColor()"], // 設定第五題四個選項
    answer: 0 // 設定第五題正確答案
  } // 結束第五題資料
]; // 結束測驗資料陣列

let currentQuestion = 0; // 儲存目前題目索引
let score = 0; // 儲存答對題數
let quizFinished = false; // 儲存測驗完成狀態
let selectedAnswers = []; // 儲存使用者選擇的答案
let answeredQuestions = []; // 儲存每題作答狀態
let correctAnswers = []; // 儲存每題答對狀態
let layout = {}; // 儲存目前版面資料
let lastInputTime = 0; // 儲存上次輸入時間
let lastInputX = -9999; // 儲存上次輸入水平座標
let lastInputY = -9999; // 儲存上次輸入垂直座標

const correctColor = "#6a994e"; // 設定正確答案背景顏色
const wrongColor = "#780000"; // 設定錯誤答案背景顏色
const normalColor = "#457b9d"; // 設定一般按鈕背景顏色
const backgroundColor = "#f1faee"; // 設定畫面背景顏色
const textColor = "#1d3557"; // 設定主要文字顏色
const disabledColor = "#a8dadc"; // 設定停用按鈕背景顏色
const borderColor = "#1d3557"; // 設定按鈕外框顏色

function setup() { // 建立 p5.js 初始化函式
  createCanvas(windowWidth, windowHeight); // 建立符合目前視窗大小的畫布
  pixelDensity(min(window.devicePixelRatio || 1, 2)); // 限制高解析度裝置的像素密度
  textAlign(CENTER, CENTER); // 設定文字水平與垂直置中
  rectMode(CENTER); // 設定矩形以中心點繪製
  textFont("Arial"); // 設定預設字型
  initializeQuiz(); // 初始化測驗資料
  updateLayout(); // 計算初始響應式版面
} // 結束 setup 函式

function initializeQuiz() { // 建立初始化測驗函式
  currentQuestion = 0; // 將目前題目設定為第一題
  score = 0; // 將分數歸零
  quizFinished = false; // 將測驗設定為尚未完成
  selectedAnswers = Array(quizData.length).fill(-1); // 初始化使用者答案
  answeredQuestions = Array(quizData.length).fill(false); // 初始化作答狀態
  correctAnswers = Array(quizData.length).fill(false); // 初始化答對狀態
} // 結束 initializeQuiz 函式

function draw() { // 建立每一幀繪圖函式
  background(backgroundColor); // 設定畫布背景顏色
  updateLayout(); // 每一幀重新計算版面
  if (quizFinished) { // 判斷測驗是否完成
    drawResultScreen(); // 繪製結果畫面
  } else { // 執行測驗尚未完成的情況
    drawQuizScreen(); // 繪製測驗題目畫面
  } // 結束測驗狀態判斷
} // 結束 draw 函式

function updateLayout() { // 建立響應式版面更新函式
  const shortSide = min(width, height); // 取得畫面短邊尺寸
  const longSide = max(width, height); // 取得畫面長邊尺寸
  const isPortrait = height >= width; // 判斷目前是否為直向畫面
  const isPhone = shortSide < 600; // 判斷目前是否為手機尺寸
  const isVeryShort = height < 480; // 判斷畫面是否為超矮橫向畫面
  const useSingleColumn = isPhone && isPortrait; // 判斷是否使用單欄選項
  const safeX = constrain(width * 0.045, 12, 42); // 設定左右安全邊距
  const safeTop = constrain(height * 0.035, 10, 30); // 設定上方安全邊距
  const safeBottom = constrain(height * 0.035, 10, 30); // 設定下方安全邊距
  const contentWidth = min(width - safeX * 2, 960); // 計算主要內容最大寬度
  const titleSize = constrain(shortSide * 0.075, 22, 48); // 計算標題文字大小
  const numberSize = constrain(shortSide * 0.038, 15, 26); // 計算題號文字大小
  const questionSize = constrain(shortSide * 0.052, 18, 34); // 計算題目文字大小
  const optionTextSize = constrain(shortSide * 0.037, 14, 23); // 計算選項文字大小
  const buttonTextSize = constrain(shortSide * 0.034, 14, 22); // 計算按鈕文字大小
  const navigationHeight = constrain(shortSide * 0.105, 42, 58); // 計算導覽按鈕高度
  const navigationWidth = constrain(width * 0.245, 104, 190); // 計算導覽按鈕寬度
  const navigationY = height - safeBottom - navigationHeight / 2; // 計算導覽按鈕垂直位置
  const titleY = safeTop + titleSize * 0.55; // 計算標題垂直位置
  const numberY = titleY + titleSize * 0.9; // 計算題號垂直位置
  const questionY = numberY + numberSize + 12; // 計算題目垂直位置
  const questionHeight = isVeryShort ? 48 : isPhone ? 72 : 88; // 設定題目顯示高度
  const optionStartY = questionY + questionHeight + (isVeryShort ? 8 : 18); // 計算選項起始位置
  const optionGap = constrain(shortSide * 0.022, 7, 18); // 計算選項間距
  const columnCount = useSingleColumn ? 1 : 2; // 設定選項欄數
  const rowCount = ceil(quizData[0].options.length / columnCount); // 計算選項列數
  const columnGap = optionGap; // 設定選項欄間距
  const optionWidth = columnCount === 1 ? contentWidth : (contentWidth - columnGap) / 2; // 計算選項寬度
  const availableHeight = navigationY - navigationHeight / 2 - optionStartY - 14; // 計算選項可用高度
  const idealOptionHeight = isVeryShort ? 42 : isPhone ? 54 : 66; // 設定理想選項高度
  const idealOptionTotalHeight = rowCount * idealOptionHeight + (rowCount - 1) * optionGap; // 計算理想選項總高度
  const heightScale = constrain(availableHeight / max(idealOptionTotalHeight, 1), 0.55, 1); // 計算高度縮放比例
  const optionHeight = max(40, idealOptionHeight * heightScale); // 設定最終選項高度
  const finalOptionGap = max(5, optionGap * heightScale); // 設定最終選項間距
  const finalQuestionSize = max(15, questionSize * min(1, heightScale + 0.12)); // 依可用高度縮放題目字級
  const finalOptionTextSize = max(12, optionTextSize * min(1, heightScale + 0.1)); // 依可用高度縮放選項字級

  layout = { // 建立版面資料物件
    shortSide: shortSide, // 儲存短邊尺寸
    longSide: longSide, // 儲存長邊尺寸
    isPortrait: isPortrait, // 儲存直向狀態
    isPhone: isPhone, // 儲存手機狀態
    isVeryShort: isVeryShort, // 儲存超矮畫面狀態
    safeX: safeX, // 儲存水平安全邊距
    contentWidth: contentWidth, // 儲存主要內容寬度
    centerX: width / 2, // 儲存畫面中央水平位置
    titleSize: titleSize, // 儲存標題文字大小
    numberSize: numberSize, // 儲存題號文字大小
    questionSize: finalQuestionSize, // 儲存最終題目文字大小
    optionTextSize: finalOptionTextSize, // 儲存最終選項文字大小
    buttonTextSize: buttonTextSize, // 儲存按鈕文字大小
    titleY: titleY, // 儲存標題垂直位置
    numberY: numberY, // 儲存題號垂直位置
    questionY: questionY, // 儲存題目垂直位置
    questionHeight: questionHeight, // 儲存題目高度
    optionStartY: optionStartY, // 儲存選項起始位置
    optionWidth: optionWidth, // 儲存選項寬度
    optionHeight: optionHeight, // 儲存選項高度
    optionGap: finalOptionGap, // 儲存選項間距
    columnGap: columnGap, // 儲存欄位間距
    columnCount: columnCount, // 儲存選項欄數
    navigationY: navigationY, // 儲存導覽按鈕垂直位置
    navigationWidth: navigationWidth, // 儲存導覽按鈕寬度
    navigationHeight: navigationHeight // 儲存導覽按鈕高度
  }; // 結束版面資料物件
} // 結束 updateLayout 函式

function drawQuizScreen() { // 建立繪製測驗畫面函式
  const question = quizData[currentQuestion]; // 取得目前題目資料
  const isAnswered = answeredQuestions[currentQuestion]; // 取得目前作答狀態

  fill(textColor); // 設定標題文字顏色
  noStroke(); // 移除文字外框
  textSize(layout.titleSize); // 套用響應式標題字級
  text("p5.js 簡易指令練習測驗", layout.centerX, layout.titleY, layout.contentWidth, layout.titleSize * 1.4); // 顯示標題

  textSize(layout.numberSize); // 套用響應式題號字級
  text(`第 ${currentQuestion + 1} 題／共 ${quizData.length} 題`, layout.centerX, layout.numberY, layout.contentWidth, layout.numberSize * 1.5); // 顯示題號

  textSize(layout.questionSize); // 套用響應式題目字級
  text(question.question, layout.centerX, layout.questionY, layout.contentWidth, layout.questionHeight); // 顯示題目並自動換行

  for (let i = 0; i < question.options.length; i++) { // 逐一處理四個選項
    const position = getOptionPosition(i); // 取得目前選項位置
    let optionColor = normalColor; // 設定選項預設背景顏色
    let bounceOffset = 0; // 設定選項預設跳動距離

    if (isAnswered) { // 判斷目前題目是否已作答
      if (i === question.answer) { // 判斷目前選項是否為正確答案
        optionColor = correctColor; // 將正確答案設定為綠色背景
        bounceOffset = sin(frameCount * 0.16) * min(8, height * 0.012); // 讓正確答案上下跳動
      } // 結束正確答案判斷

      if (i === selectedAnswers[currentQuestion] && !correctAnswers[currentQuestion]) { // 判斷是否為使用者選錯的選項
        optionColor = wrongColor; // 將錯誤選項設定為深紅色背景
      } // 結束錯誤選項判斷
    } // 結束作答狀態判斷

    drawOptionButton(question.options[i], position.x, position.y + bounceOffset, optionColor); // 繪製目前選項
  } // 結束選項迴圈

  drawNavigationButtons(); // 繪製底部導覽按鈕
} // 結束 drawQuizScreen 函式

function getOptionPosition(index) { // 建立取得選項位置函式
  const row = layout.columnCount === 1 ? index : floor(index / layout.columnCount); // 計算選項列數
  const column = layout.columnCount === 1 ? 0 : index % layout.columnCount; // 計算選項欄數
  const totalWidth = layout.columnCount === 1 ? layout.optionWidth : layout.optionWidth * 2 + layout.columnGap; // 計算選項總寬度
  const firstX = layout.centerX - totalWidth / 2 + layout.optionWidth / 2; // 計算第一欄水平位置
  const x = firstX + column * (layout.optionWidth + layout.columnGap); // 計算目前選項水平位置
  const y = layout.optionStartY + layout.optionHeight / 2 + row * (layout.optionHeight + layout.optionGap); // 計算目前選項垂直位置
  return { x: x, y: y }; // 回傳選項座標
} // 結束 getOptionPosition 函式

function drawOptionButton(label, x, y, colorValue) { // 建立繪製選項按鈕函式
  fill(colorValue); // 設定選項背景顏色
  stroke(borderColor); // 設定選項外框顏色
  strokeWeight(2); // 設定選項外框粗細
  rect(x, y, layout.optionWidth, layout.optionHeight, 10); // 繪製圓角選項按鈕
  fill("#ffffff"); // 設定選項文字顏色
  noStroke(); // 移除文字外框
  textSize(layout.optionTextSize); // 設定選項文字大小
  text(label, x, y, layout.optionWidth * 0.88, layout.optionHeight * 0.82); // 顯示選項文字並自動換行
} // 結束 drawOptionButton 函式

function drawNavigationButtons() { // 建立繪製導覽按鈕函式
  const sideMargin = max(10, layout.safeX * 0.65); // 設定導覽按鈕水平安全邊距
  const previousX = sideMargin + layout.navigationWidth / 2; // 計算上一題按鈕水平位置
  const nextX = width - sideMargin - layout.navigationWidth / 2; // 計算下一題按鈕水平位置
  const previousDisabled = currentQuestion === 0; // 判斷上一題是否停用
  const nextDisabled = !answeredQuestions[currentQuestion]; // 判斷下一題是否停用
  const nextLabel = currentQuestion === quizData.length - 1 ? "完成測驗" : "下一題"; // 設定下一題按鈕文字

  drawNavigationButton("上一題", previousX, layout.navigationY, previousDisabled); // 繪製上一題按鈕
  drawNavigationButton(nextLabel, nextX, layout.navigationY, nextDisabled); // 繪製下一題按鈕

  layout.previousButton = { x: previousX, y: layout.navigationY, width: layout.navigationWidth, height: layout.navigationHeight }; // 儲存上一題按鈕位置
  layout.nextButton = { x: nextX, y: layout.navigationY, width: layout.navigationWidth, height: layout.navigationHeight }; // 儲存下一題按鈕位置
} // 結束 drawNavigationButtons 函式

function drawNavigationButton(label, x, y, disabled) { // 建立繪製導覽按鈕函式
  fill(disabled ? disabledColor : borderColor); // 根據按鈕狀態設定背景顏色
  stroke(borderColor); // 設定按鈕外框顏色
  strokeWeight(2); // 設定按鈕外框粗細
  rect(x, y, layout.navigationWidth, layout.navigationHeight, 9); // 繪製導覽按鈕
  fill("#ffffff"); // 設定按鈕文字顏色
  noStroke(); // 移除文字外框
  textSize(layout.buttonTextSize); // 設定導覽文字大小
  text(label, x, y, layout.navigationWidth * 0.88, layout.navigationHeight * 0.75); // 顯示導覽按鈕文字
} // 結束 drawNavigationButton 函式

function drawResultScreen() { // 建立繪製結果畫面函式
  const centerY = height / 2; // 計算畫面中央垂直位置
  const titleSize = constrain(min(width, height) * 0.08, 26, 58); // 計算結果標題字級
  const scoreSize = constrain(min(width, height) * 0.065, 23, 48); // 計算結果分數字級
  const messageSize = constrain(min(width, height) * 0.04, 15, 28); // 計算結果訊息字級
  const compact = height < 520; // 判斷是否為矮畫面
  const titleY = compact ? height * 0.16 : height * 0.25; // 計算結果標題位置
  const scoreY = compact ? height * 0.34 : height * 0.43; // 計算分數位置
  const messageY = compact ? height * 0.5 : height * 0.56; // 計算訊息位置
  const restartY = compact ? height * 0.78 : height * 0.72; // 計算重新開始按鈕位置
  const restartWidth = min(width * 0.58, 280); // 計算重新開始按鈕寬度
  const restartHeight = constrain(min(width, height) * 0.115, 46, 62); // 計算重新開始按鈕高度

  fill(textColor); // 設定標題文字顏色
  noStroke(); // 移除文字外框
  textSize(titleSize); // 套用結果標題字級
  text("測驗完成！", layout.centerX, titleY, width * 0.9, titleSize * 1.5); // 顯示結果標題

  fill(correctColor); // 設定分數文字顏色
  textSize(scoreSize); // 套用結果分數字級
  text(`你答對了 ${score}／${quizData.length} 題`, layout.centerX, scoreY, width * 0.9, scoreSize * 1.5); // 顯示答對題數

  fill(textColor); // 設定評語文字顏色
  textSize(messageSize); // 套用結果訊息字級
  if (score === quizData.length) { // 判斷是否全部答對
    text("太棒了！全部答對！", layout.centerX, messageY, width * 0.88, 60); // 顯示滿分評語
  } else if (score >= 3) { // 判斷是否答對三題以上
    text("表現很好，繼續練習會更熟悉！", layout.centerX, messageY, width * 0.88, 70); // 顯示良好評語
  } else { // 執行答對題數低於三題的情況
    text("再多練習幾次，就會越來越熟悉！", layout.centerX, messageY, width * 0.88, 70); // 顯示鼓勵評語
  } // 結束評語判斷

  fill(borderColor); // 設定重新開始按鈕背景顏色
  stroke(borderColor); // 設定重新開始按鈕外框顏色
  strokeWeight(2); // 設定重新開始按鈕外框粗細
  rect(layout.centerX, restartY, restartWidth, restartHeight, 10); // 繪製重新開始按鈕
  fill("#ffffff"); // 設定重新開始文字顏色
  noStroke(); // 移除重新開始文字外框
  textSize(messageSize); // 設定重新開始文字大小
  text("重新開始", layout.centerX, restartY, restartWidth * 0.85, restartHeight * 0.75); // 顯示重新開始文字
  layout.restartButton = { x: layout.centerX, y: restartY, width: restartWidth, height: restartHeight }; // 儲存重新開始按鈕位置
} // 結束 drawResultScreen 函式

function mousePressed() { // 建立滑鼠按下事件函式
  handleInput(mouseX, mouseY); // 將滑鼠座標交給統一輸入函式
} // 結束 mousePressed 函式

function touchStarted() { // 建立觸控開始事件函式
  if (touches.length > 0) { // 判斷是否存在觸控資料
    handleInput(touches[0].x, touches[0].y); // 將第一個觸控座標交給統一輸入函式
  } // 結束觸控資料判斷
  return false; // 防止瀏覽器產生滑動與重複事件
} // 結束 touchStarted 函式

function handleInput(inputX, inputY) { // 建立滑鼠與觸控共用輸入函式
  const now = millis(); // 取得目前時間
  const inputDistance = dist(inputX, inputY, lastInputX, lastInputY); // 計算輸入座標距離
  if (now - lastInputTime < 400 && inputDistance < 30) { // 判斷是否為重複輸入事件
    return; // 忽略重複輸入
  } // 結束重複輸入判斷

  lastInputTime = now; // 記錄本次輸入時間
  lastInputX = inputX; // 記錄本次輸入水平座標
  lastInputY = inputY; // 記錄本次輸入垂直座標

  if (quizFinished) { // 判斷是否已完成測驗
    const button = layout.restartButton; // 取得重新開始按鈕
    if (button && isInsideButton(inputX, inputY, button.x, button.y, button.width, button.height)) { // 判斷是否點擊重新開始
      initializeQuiz(); // 重新開始測驗
    } // 結束重新開始判斷
    return; // 結束結果畫面輸入處理
  } // 結束測驗完成判斷

  const question = quizData[currentQuestion]; // 取得目前題目資料

  if (!answeredQuestions[currentQuestion]) { // 判斷目前題目是否尚未作答
    for (let i = 0; i < question.options.length; i++) { // 逐一檢查所有答案選項
      const position = getOptionPosition(i); // 取得目前答案位置
      if (isInsideButton(inputX, inputY, position.x, position.y, layout.optionWidth, layout.optionHeight)) { // 判斷是否點擊答案
        selectedAnswers[currentQuestion] = i; // 記錄使用者選擇答案
        answeredQuestions[currentQuestion] = true; // 設定目前題目已作答
        correctAnswers[currentQuestion] = i === question.answer; // 判斷使用者答案是否正確
        if (correctAnswers[currentQuestion]) { // 判斷使用者是否答對
          score++; // 增加答對題數
        } // 結束答對判斷
        return; // 結束本次輸入處理
      } // 結束選項點擊判斷
    } // 結束選項檢查迴圈
  } // 結束尚未作答判斷

  const sideMargin = max(10, layout.safeX * 0.65); // 設定導覽按鈕安全邊距
  const previousX = sideMargin + layout.navigationWidth / 2; // 計算上一題按鈕水平位置
  const nextX = width - sideMargin - layout.navigationWidth / 2; // 計算下一題按鈕水平位置

  if (currentQuestion > 0 && isInsideButton(inputX, inputY, previousX, layout.navigationY, layout.navigationWidth, layout.navigationHeight)) { // 判斷是否點擊上一題
    currentQuestion--; // 回到上一題
    return; // 結束本次輸入處理
  } // 結束上一題判斷

  if (answeredQuestions[currentQuestion] && isInsideButton(inputX, inputY, nextX, layout.navigationY, layout.navigationWidth, layout.navigationHeight)) { // 判斷是否點擊下一題
    if (currentQuestion === quizData.length - 1) { // 判斷是否為最後一題
      quizFinished = true; // 設定測驗已完成
    } else { // 執行尚未到最後一題的情況
      currentQuestion++; // 前往下一題
    } // 結束最後一題判斷
  } // 結束下一題判斷
} // 結束 handleInput 函式

function isInsideButton(pointX, pointY, buttonX, buttonY, buttonWidth, buttonHeight) { // 建立按鈕範圍判斷函式
  const left = buttonX - buttonWidth / 2; // 計算按鈕左邊界
  const right = buttonX + buttonWidth / 2; // 計算按鈕右邊界
  const top = buttonY - buttonHeight / 2; // 計算按鈕上邊界
  const bottom = buttonY + buttonHeight / 2; // 計算按鈕下邊界
  return pointX >= left && pointX <= right && pointY >= top && pointY <= bottom; // 回傳座標是否位於按鈕內
} // 結束 isInsideButton 函式

function keyPressed() { // 建立鍵盤按下事件函式
  if (key === "f" || key === "F") { // 判斷是否按下 F 鍵
    fullscreen(!fullscreen()); // 切換全螢幕狀態
  } // 結束全螢幕切換判斷
} // 結束 keyPressed 函式

function windowResized() { // 建立視窗尺寸改變事件函式
  resizeCanvas(windowWidth, windowHeight); // 重新調整畫布尺寸
  updateLayout(); // 重新計算響應式版面
} // 結束 windowResized 函式

```
:::


---

## 學習3：設定嵌入 Google 字型，網頁文字採用這些字型

https://cfchen58.synology.me/115/week4/stage3/

**這個階段的目標：** 從 Google Fonts 嵌入繁體中文字型，並讓畫布上的題目與選項文字使用這些字型。
**這個階段會修改的檔案：** index.html、sketch.js

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![學習3截圖](請貼上截圖)

### 第一次問 AI

```tex!
延續上一個指令，從 Google Fonts 嵌入繁體中文字型，並讓畫布上的題目與選項文字使用這些字型。
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習3的程式碼
```javascript=
//學習3程式碼所在

```
:::


---

## 學習4：設定題庫並抽題顯示題目網頁（CSV 檔案）

https://cfchen58.synology.me/115/week4/stage4/

**這個階段的目標：** 把題目移到 questions.csv，網站讀取題庫後每次隨機抽出 5 題。
**這個階段會修改的檔案：** index.html、sketch.js、questions.csv

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![學習4截圖](請貼上截圖)

### 第一次問 AI

```tex!
（逐字貼上你第一次問 AI 的提示詞）
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習4的程式碼
```javascript=
//學習4程式碼所在

```
:::


---

## 學習5：利用 Google Sheets 當題庫

https://cfchen58.synology.me/115/week4/stage5/

**這個階段的目標：** 把題庫放在 Google 試算表，網站直接讀取，老師改試算表，網站題目就跟著更新。
**這個階段會修改的檔案：** index.html、sketch.js（questions.csv 當備用題庫）

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![學習5截圖](請貼上截圖)

### 第一次問 AI

```tex!
（逐字貼上你第一次問 AI 的提示詞）
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習5的程式碼
```javascript=
//學習5程式碼所在

```
:::


---

## 我的心得

這五個學習中，哪一個最困難？你是怎麼解決的？（請寫出實際發生的事）

＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿
