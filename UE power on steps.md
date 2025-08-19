# LTE 初始接入流程筆記

---

## 📶 1. PLMN 與 Cell Selection

- UE 開機後進行網路選擇與小區選擇（PLMN & Cell Selection）。
- 接收並解碼 eNB 廣播的系統資訊（System Information，SI）。
- 根據 SI 內容進行接入條件判斷與設定。

---

## 📡 2. 隨機接入程序（Random Access Procedure）

> 註：原文未具體展示流程圖，但此步驟為 LTE Initial Access 的重要前提。

- UE 執行 Random Access，取得 uplink 資源。
- 這一步是為了爭取 eNB 分配之後的控制通道（如 SRB）與資料承載通道（如 DRB）。

---

## 📤 3. RRC Connection Request + Attach Request

- UE 傳送 RRC Connection Request 與 Attach Request。
- 包含識別碼（如 IMSI）與初始通訊要求。

---

## 🔒 4. 認證與加密建立

- eNB 轉送 Attach Request 給核心網路（如 MME、HSS）。
- 使用者認證成功後，建立 NAS 層與 AS 層的加密通道。

---

## 🌐 5. 建立 Default Bearer

- MME 與 S-GW 為 UE 建立 default bearer。
- 使用 GTP-U（GPRS Tunneling Protocol – User plane）建立用戶資料隧道。

---

## 📩 6. Attach Accept 與 GUTI 指派

- UE 接收到 Attach Accept 與 default bearer 設定資訊。
- 核心網路同時分配 GUTI（Globally Unique Temporary Identifier）以保障使用者隱私。

---

## 🔧 7. RRC Reconfiguration

- eNB 發送 RRC Reconfiguration，建立 SRB1、SRB2、DRB 等承載。
- UE 依據內容調整內部參數與通道配置。
- 設定完成後，eNB 通知 MME：UE 已成功接入，並建立好必要的承載與加密機制。

---



最終建立 dedicated bearer，完成初始接入與可用資料連線。

