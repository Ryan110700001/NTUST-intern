I. Introduction
市場背景：室內定位服務（ILBS）市場預估至2020年將達100億美元。由於 GPS 信號無法穿透室內，需尋找替代技術。Wi-Fi 指紋定位因 WLAN 部署廣泛、無需視距測量而成為成本效益最高的方案之一 

指紋定位流程：
  離線階段：在已知參考點（RP）蒐集各 AP RSSI 向量，建立指紋資料庫。
  線上階段：量測當前 RSSI 向量，採用相似度度量（如歐氏距離）與資料庫比對，選出最相鄰 RP 作為位置估計。

本文架構：
  Section II 先進定位技術
  Section III 高效系統部署
  Section IV 未來研究方向
II-A. Basic Fingerprint Localization (基本指紋定位) 
1.確定性方法 (Deterministic Methods)
  核心思想：將線上量測到的 RSSI 向量𝑠與離線階段建立的指紋資料庫中每個參考點（RP）的向量𝑟n計算相似度，選擇最相近的 RP 作為估計位置。
  常用相似度度量：
    歐幾里得距離：∥𝑠−𝑟𝑛∥
    餘弦相似度：s⋅r𝑛/∥𝑠∥∥𝑟𝑛∥
    Tanimoto 相似度
  演算法實例：
    k-NN：取k個最鄰近點投票
    支持向量機 (SVM)、線性判別分析 (LDA)：將 RSSI 特徵映射至分類器空間，提高判別力
  優點：計算複雜度低、實作簡單，不需概率模型訓練
  缺點：對離線資料量需求高，面對環境變化或雜訊時穩健性不足

2.概率性方法 (Probabilistic Methods)
核心思想：視位置𝑥與信號𝑠為隨機變量，建立後驗機率模型𝑃(𝑥|𝑠)或似然模型P(s∣x)，並通過最大後驗 (MAP) 或最大似然估計 (MLE) 確定位置：
```latex
\[
  \arg\max_{x} P(x \mid s)
  \;\Longleftrightarrow\;
  \arg\max_{x} \prod_{l=1}^{L} P\bigl(s_{l}\mid x\bigr)
\]```


典型系統：

Horus：以高斯分佈近似 
𝑃
(
𝑠
𝑙
∣
𝑥
)
P(s 
l
​
 ∣x)，可給出置信區間

Bayesian Network、Expectation-Maximization、Gaussian Process、Conditional Random Field 等

優點：能量化置信度、易與其他傳感器（如慣性、聲音）融合

缺點：需做概率假設（獨立性、噪聲分佈），訓練模型需大量數據且計算複雜

II-B. Exploiting Spatial and Temporal Signal Patterns (利用空間性與時間性信號模式) 
時間性模式 (Temporal Patterns)

Peak-Based Fingerprinting (PWF)

收集用戶行走時的 RSSI 序列，偵測具有預定閾值的峰值，將峰值位置對應至最接近的 AP

適用：AP 安裝於天花板走廊

限制：需精確運動信息；走得太快易漏掃

Walkie-Markie

將整段 RSSI 序列（而非單一峰值）作為走廊指紋，以序列模式比對線上數據

優勢：更抗噪、多路徑效應影響小

適用：狹長走廊空間，有固定行走路徑

空間性模式 (Spatial Patterns)

AP Landmarks (UnLoc / MapCraft)

將特定 AP 的強信號區域視為地標，當線上測量落於地標區時，校正並收窄位置估計

若 AP 部署稀疏，需輔以磁場等其他地標

RSSI Strength Order (HALLWAY)

比較多個 AP 間的信號強度排序（例如 s1 < s2 < s3 與 s1 < s3 < s2），區分不同房間

優勢：減少設備差異與微小波動影響

限制：解析度僅達房間層級

Coverage Intersection

根據離散信號強度級別劃分各 AP 覆蓋扇區，取多 AP 扇區的交集作為目標可能區域

可排除在信號空間分散但高相似度的雜訊點

需先做虛擬 AP 過濾，去除同一實體路由器產生的重複 MAC 
。

II-C. Collaborative Localization Among Mobiles (協作式定位) 
Distance-Based Schemes

Virtual Compass (VC)

結合 Wi-Fi Direct 與 Bluetooth，利用 Vivaldi 演算法建立成對距離網絡，求解相對坐標

透過雙傳感器置信區間融合提升距離精度

局限：仍易受 RF 噪聲影響，未支援絕對定位

Peer-Assisted (PA)

使用手機輸出聲波（Beep）偵測互距，將 Wi-Fi RSSI 初估與距離信息映射為網絡圖，通過旋轉、平移最小化整體歐氏距離確定位置

優勢：高距離精度

缺點：圖形剛性對測量誤差敏感，建圖需同步測距

Centaur

基於貝葉斯網絡的協作定位，不用剛性圖形，對距離噪聲更穩健，但主要聚焦靜態場景

Proximity-Based Schemes

利用 Wi-Fi AP 列表或 Bluetooth 檢測用戶間是否鄰近，作為粗略約束

ZigBee Collaborative Localization (ZCL)

用 ZigBee 做鄰居偵測，再結合運動模型與 Wi-Fi 位置信心度分數，透過分散式算法互校正估計

Encounter-Based (Social-Loc)

根據用戶「相遇／未相遇」事件，過濾或加權候選位置，提高協作定位的可靠性

II-D. Motion-Assisted Localization (動作輔助定位) 
Motion Measurement

使用手機內建 MEMS：

加速度計：檢測步伐振幅

陀螺儀：估算朝向變化

磁力計：參考地磁校正方向

步態偵測流程：

行走檢測：閾值或機器學習

步數計算：峰值檢測、自相關或 FFT

步距估算：基於步頻與身高的線性或高斯模型

Fusion Models

Kalman Filter (KF / EKF / UKF)：適合線性高斯系統，需已知系統模型與噪聲參數

Particle Filter (PF)：透過粒子集近似後驗分佈，能處理非線性與非高斯噪聲

Simplified Probabilistic Models：HMM、CRF 或 Wi-Fi SLAM（GraphSLAM、WiSLAM）等，兼顧準確度與計算成本

裝置位置補償：考慮手機在手中揮動造成的 heading drift，可透過穿戴式裝置或校正算法改善

