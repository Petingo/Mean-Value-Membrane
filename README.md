# Mean-Value Membrane
- An web implementation of http://www.cs.huji.ac.il/~danix/mvclone/
- Demo：https://petingo.me/MVC/
- Source：https://github.com/Petingo/MVC/

![demo](https://github.com/petingo/MVC/raw/master/demo.png)

### 測試圖片
![composite](https://github.com/petingo/MVC/raw/master/composite.png)

### 檔案說明
專案利用 HTML + javascript 完成，其中 pixel 的改動主要依靠 canvas 進行。主要檔案有 `index.html`、`main.js`、`mvc.js`；其中 `index.html` 和 `main.js` 為網頁前端介面與操作邏輯的部分，`mvc.js` 為主要的影像處理演素法實作。

### 處理流程
分別上傳背景圖片和合成圖片以後，先在合成圖片上面標點，標點以後會先將點利用 [atan2()](https://zh.wikipedia.org/wiki/Atan2) 求極坐標進行排序，確保這些邊點是按照順時針方向排列，方便後續操作和計算。排序完成後會利用兩點求一直線的原理計算外框的範圍與「內部像素點」的座標。

接下來開始 render，依照演算法的流程，首先會針對每個內部像素點計算這些點對於邊緣點的 mean-value coordinate（有點類似依照距離和角度計算加權平均的概念），接著對於每個邊緣點、計算它們在來源圖和目標圖中的影像值差距，稱為 difference 值；需要注意的是 RGB 三通到要分別計算。

最後對於每個內部點計算 <img src="/tex/efcf9713ca967107fecdd43b3c921eca.svg?invert_in_darkmode&sanitize=true" align=middle width=164.467347pt height=31.36100879999999pt/>，將目標圖的影像強度 <img src="/tex/ffcbbb391bc04da2d07f7aef493d3e2a.svg?invert_in_darkmode&sanitize=true" align=middle width=30.61077854999999pt height=24.65753399999998pt/> 加上 <img src="/tex/ba413bfad070394bac217a91553c05b8.svg?invert_in_darkmode&sanitize=true" align=middle width=83.96884155pt height=24.65753399999998pt/> 就是最終結果。