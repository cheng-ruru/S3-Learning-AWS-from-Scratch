# S3-Learning-AWS-from-Scratch
從零開始學AWS Re：Learning AWS

## 雲端小白試著自己動手架設 AWS S3 靜態網站 LAB，請試著完成以下內容

1. 建立一個 S3 Bucket，命名規則 `awssa-英文名`
2. Bucket 要放在東京區域
3. 上傳物件(檔名：Logo.png)至 S3
4. 驗證圖片是否可開啟
5. 物件 > 將靜態網站Static Websit資料夾內的檔案上傳到剛剛建立好的 Bucket 根目錄
6. 放入Static Website資料夾中四個檔案:index.html、error.html、script.js、style.css
7. 屬性 > 啟用靜態網站託管，並設定索引文件與錯誤文件
8. 許可 > 存取控制清單 (ACL) > 點選 "強制執行的儲存貯體擁有者" > 啟用 ACL
9. 許可 > 解除 "封鎖所有公開存取權"
10. 許可 > 在 "存取控制清單 (ACL)" 點選編輯 > 將 "每個人 (公有存取)" 讀取打開
11. 物件 > 將靜態網站的所有檔案勾選後點選 "動作" > 點選 "使 ACL 設為公有"
12. 屬性 > 測試靜態網站 URL 是否可以顯示
13. 把自己建立的 S3 Bucket 刪除


📌 **注意事項：** 
- S3 Bucket 名稱需 **全球唯一**，請使用 awssa-<你的英文名> 避免重複。
- 在刪除 S3 Bucket 前，請確保 **已清空所有物件**，否則無法刪除。
- 靜態網站 URL 可能需要幾分鐘才能生效，請耐心等待。
---

### ** AWS S3 靜態網站**

對於雲端小白來說，學習如何在 AWS 上搭建 S3 靜態網站是一個入門的重要實踐。本次 LAB 的主要目標是：
1. **熟悉 AWS S3 的基本概念與物件存儲機制**。
2. **理解靜態網站托管的原理，學習如何部署 HTML、CSS、JavaScript 等資源**。
3. **掌握 S3 存取權限管理，確保網站可存取但不造成資安風險**。
4. **學習資源最佳化與管理，避免不必要的資源浪費與安全隱患**。

### **📌為什麼要做這些設定？**

#### 1. **建立 S3 Bucket 並放置靜態網站**
- S3 作為物件存儲服務，允許使用者儲存和存取靜態內容。
- 開啟 **靜態網站託管**，可以讓我們用 S3 提供網頁，而無需建置 Web Server，降低部署成本。

#### 2. **啟用 ACL 來確保存取權限一致，避免存取混亂**
- 在 AWS S3 中，**物件的擁有權可能與 Bucket 擁有權不同**，如果沒有統一管理，可能會導致不同帳戶的物件存取權限不一致，影響網站運行。
- 啟用 **強制執行的儲存貯體擁有者**，確保 **所有上傳的物件都歸 S3 Bucket 擁有者管理**，避免日後存取權限錯亂的問題。

#### 3. **解除封鎖公開存取權，確保網站訪客可以存取靜態內容**
- S3 預設會封鎖所有公開存取，這對一般存儲需求來說是必要的安全保護，但對於靜態網站來說，訪客需要能夠正常讀取網站內容。
- **解除封鎖後**，訪客就能透過網路存取 HTML、CSS、JavaScript 檔案，而無需 AWS 認證。

#### 4. **設定公有讀取權限，讓所有訪客都能存取網站內容**
- 即使解除公開存取，**每個物件仍然需要個別設定公有存取權限**，否則網站的某些資源可能無法讀取，影響用戶體驗。
- 透過 **存取控制清單（ACL）設定 `每個人（公有存取）` 可讀取**，確保網站所有靜態資源可供外部訪問。

#### 5. **將靜態網站的所有檔案設為公有，確保對外訪問可行**
- 使用 `使 ACL 設為公有`，統一將網站所有檔案設定為可公開讀取，避免手動逐一設定帶來的錯誤與困擾。
- 確保 HTML、CSS、JavaScript 等靜態內容可順利載入，確保網站功能完整。

#### 6. **刪除 S3 Bucket，避免未使用的資源持續存在，確保安全與成本控制**
- 在 AWS 上，**所有儲存的物件都會產生成本**，即使只是少量存放，也可能影響長期的預算規劃。
- 刪除不再使用的 S3 Bucket，不僅可節省資源成本，還能避免遺留的存取權限可能帶來的 **未授權存取風險**。

---

### **📌資安考量**

#### 1. **存取控制與權限管理**
- AWS S3 的存取權限預設為私有，這是為了防止未經授權的存取。
- 在開放靜態網站存取時，**應該僅針對公開資料開放權限，而非整個 Bucket**，以避免潛在的資料洩漏風險。

#### 2. **確保 Bucket 擁有權**
- 啟用 **強制執行的儲存貯體擁有者**，可防止物件因擁有權不同而無法控制存取權限，減少權限混亂帶來的資安問題。

#### 3. **限制存取範圍**
- 解除公開存取時，應確保 **僅開放特定物件，而非整個儲存桶**，防止機密資料誤開放，造成敏感資訊外洩。

#### 4. **避免未受控的存儲桶暴露**
- **刪除未使用的 S3 Bucket**，可以降低意外的存取風險，避免攻擊者利用過期存取權限來存取敏感資料。

---

# 【跟著RURU一起實際操作】
### 1. 搜尋並進入 S3 服務
- 在 AWS 管理主控台上方的搜尋輸入框中，輸入 `S3`。
- 在搜尋結果中點擊 `S3`，進入 S3 服務頁面。

![Image](https://github.com/user-attachments/assets/60a5c644-4a2a-4ead-aaa7-d53c6f65b7df)

![Image](https://github.com/user-attachments/assets/646357e9-aae6-49e0-9287-66c305a070ba)

### 2. 建立 S3 Bucket
- 確保 **Bucket 放置區域為東京 (ap-northeast-1)**。
 ![Image](https://github.com/user-attachments/assets/70b92a8b-c6b1-435e-8369-7ae8c6bf127e)
==
![Image](https://github.com/user-attachments/assets/d7b2c3d6-1c80-4bb8-bfe2-afe948ddf080)
- 點擊 `建立儲存貯體` (Create bucket)。
 ![Image](https://github.com/user-attachments/assets/b2c0ec8f-62d2-4a4a-9a94-c53d8df50f6f)
- 在 `儲存貯體名稱` (Bucket name) 欄位輸入： `awssa-<你的英文名>`。
 ![Image](https://github.com/user-attachments/assets/f7fc92aa-5ed8-4966-94a5-7df0b800cb91)

- 按下 `建立` (Create bucket) 按鈕。
 ![Image](https://github.com/user-attachments/assets/44a4379b-75d1-4245-b5d9-df5aee5ef762)

 ![Image](https://github.com/user-attachments/assets/54f4ae7f-6ccb-405b-b61c-f41feba88eb3)


### 3. 上傳物件至 S3
- 進入剛建立的 S3 Bucket。
  ![image](https://github.com/user-attachments/assets/63a78978-2085-4aec-b709-7e6fa50b28c7)

- 點擊 `物件` (Objects) > `上傳` (Upload)。
  ![image](https://github.com/user-attachments/assets/812c51a5-4437-430b-941e-56398c3c5653)

- 選擇一個任意的圖片檔案並上傳。
  ![image](https://github.com/user-attachments/assets/6923c8e4-7d75-41ac-8368-7b38cb4749b3)
  ![image](https://github.com/user-attachments/assets/789bfe4c-cbb4-4aee-a97c-be927887550b)
  ![image](https://github.com/user-attachments/assets/17e1d195-db4f-4c8a-bef6-5de1a724d13f)

- 確認圖片成功上傳。
![image](https://github.com/user-attachments/assets/4be43a92-f504-4e7c-9ac4-3a7c8eeb7e73)

### 4. 驗證圖片是否可開啟
- 在 S3 Bucket 內找到剛剛上傳的圖片。
- 點擊圖片名稱，進入詳細頁面。
  ![image](https://github.com/user-attachments/assets/e88b53ae-6fc6-47bd-8e09-5a161a56511d)
- 右上角點選 `開啟` (Open)，確認已成功看到上傳的圖片。
 ![image](https://github.com/user-attachments/assets/42ab0db7-1311-47fa-a3c5-ff810d9801a2)
 
### 5. 上傳靜態網站檔案=>Static Website資料夾
- 進入剛建立的 S3 Bucket。
- 點擊 物件 (Objects) > 上傳 (Upload)。
- 選擇 **靜態網站資料夾Static Website內的所有檔案**，並上傳到 **Bucket 根目錄**。
   ![image](https://github.com/user-attachments/assets/0fe6ba77-8791-45cc-a61f-618299e99197)
- 確認所有檔案成功上傳。
![image](https://github.com/user-attachments/assets/15fe3866-17a2-468d-aa7e-cbe762a32266)

### 6. 啟用靜態網站託管=>在屬性中設定
- 點擊 屬性 (Properties)。
  ![image](https://github.com/user-attachments/assets/30db6b64-c6ea-489b-9b56-fedc443111be)
- 啟用 靜態網站託管 (Static website hosting)。
  ![image](https://github.com/user-attachments/assets/4a7cfb79-a1fa-44fd-a3b7-ae906288f78c)
  ![image](https://github.com/user-attachments/assets/d44c8e16-dccc-42d2-9401-255125568a16)
- 設定 **索引文件 (Index document)** 和 **錯誤文件 (Error document)**。
  ![image](https://github.com/user-attachments/assets/0213283f-fd41-49f5-a954-7d132dfcebe9)
- 儲存變更。
  ![image](https://github.com/user-attachments/assets/00c2f974-9060-4444-9ffc-3d121ec09339)
  ![image](https://github.com/user-attachments/assets/ecba23d3-341d-40b1-97e2-bf725a5b8b4d)
  ![image](https://github.com/user-attachments/assets/347b5fb3-2d93-4542-8cd3-783820d2bc22)

### 7. 設定 S3 存取權限=>在許可中設定
#### 7.1 啟用 ACL
- 前往 許可 (Permissions) > 存取控制清單 (ACL)。
-  ![image](https://github.com/user-attachments/assets/a0e7b029-e757-4874-913f-e5f93be16e0f)
- 點選 強制執行的儲存貯體擁有者 (Enforced bucket owner) > 啟用 ACL。
 ![image](https://github.com/user-attachments/assets/dc276a18-93a9-4342-8aa8-54046c83bd1b)
  ![image](https://github.com/user-attachments/assets/400fce9a-dafd-4e5a-adb1-1f703537fd0f)

#### 7.2 解除封鎖公開存取
- 前往 許可 (Permissions) > 封鎖所有公開存取權 (Block all public access)。
 ![image](https://github.com/user-attachments/assets/9a6ba904-b5d1-4ba2-86e1-09ed5175ec42)
 ![image](https://github.com/user-attachments/assets/270a0d9d-05ff-4234-a2dd-a77e4ca73328)

- **解除封鎖** 所有公開存取設定。
  ![image](https://github.com/user-attachments/assets/c2ae83b2-adc3-440c-a6dc-77c60867f6fc)
- 儲存變更。

#### 7.3 設定公有讀取權限
- 在 存取控制清單 (ACL) 中點擊 編輯。
  ![image](https://github.com/user-attachments/assets/f7e8c567-e261-4c63-8f5a-19f0a67a900a)

- 找到 每個人 (公有存取) (Everyone (public access))，並 **開啟讀取權限**。
  ![image](https://github.com/user-attachments/assets/b64fd2b0-d1fe-4c54-a016-757fb13a6749)
![image](https://github.com/user-attachments/assets/0bd5c0eb-40ce-4376-9182-5bb0735bedfa)
- 儲存變更。

#### 7.4 使所有物件的 ACL 設為公有
- 在 物件 (Objects) 頁面，勾選所有 **靜態網站檔案**。
  ![image](https://github.com/user-attachments/assets/5eee3b87-cd05-4af1-95de-0441547f9a8c)

- 點擊 動作 (Actions) > 使 ACL 設為公有 (Make public using ACL)。
  ![image](https://github.com/user-attachments/assets/aaf09263-87d8-43d6-8db1-c89658dff92d)

- 確認變更。
  ![image](https://github.com/user-attachments/assets/7264c32d-c0c0-478b-838c-b6fca7a5f9e7)


### 8. 測試靜態網站 URL
- 在 屬性 (Properties) 頁面找到 靜態網站 URL。
  ![image](https://github.com/user-attachments/assets/709fd107-66e4-4089-8833-bdce6fbcc1c4)

- 開啟 URL 並確認網站顯示正常。
![image](https://github.com/user-attachments/assets/066c502f-193c-4fda-bd8e-af4d638ee8ef)
![image](https://github.com/user-attachments/assets/ab394914-6ba7-4f05-84f1-17fe47d4195f)
![image](https://github.com/user-attachments/assets/77da1c6b-45a1-4c5b-bc29-b09e32e3a937)

### 9. 刪除 S3 Bucket
- 確保 Bucket 內 **沒有任何物件**。
  ![image](https://github.com/user-attachments/assets/d9fdfc32-2a02-4a61-affa-1ae75f546dfa)
  ![image](https://github.com/user-attachments/assets/c44f2476-f29a-46bb-a513-171d5a50794b)
  ![image](https://github.com/user-attachments/assets/ba08949c-0edf-406e-988e-b2bbebebedaf)
  ![image](https://github.com/user-attachments/assets/fe3406b3-3db9-4516-9f45-6b4634fb1b30)
  ![image](https://github.com/user-attachments/assets/f5dfd9f8-5ee1-4e22-8f08-ae7df3014d7f)
- 進入 儲存貯體 設定。
- 點擊 刪除儲存貯體 (Delete bucket)。
 ![image](https://github.com/user-attachments/assets/6e2136ae-2798-4af8-9770-da6613d3c3cd)
![image](https://github.com/user-attachments/assets/6fb88599-7604-4358-a309-56a471ff0559)
![image](https://github.com/user-attachments/assets/713be490-2e90-49a6-bf8f-ec42a468c3ae)

- 確認刪除成功。
![image](https://github.com/user-attachments/assets/091541b6-72ee-40fa-a985-5cbd588dd44c)
![image](https://github.com/user-attachments/assets/2b91090f-e225-4527-acac-d0263c4bb2a0)



---
### **📌小結**
本次 LAB 讓雲端新手能夠：

✅ **理解 AWS S3 的基礎概念與靜態網站託管功能**  
✅ **學習如何管理 S3 存取權限，確保安全與公開訪問之間的平衡**  
✅ **學會如何刪除未使用的資源，以降低安全風險與成本**  
✅ **培養雲端安全意識，避免存取權限錯誤帶來的潛在資安問題**  

透過這次練習，你不僅能在 AWS 上快速部署靜態網站，還能學習如何正確管理存取權限與資安設定，為未來的雲端開發做好準備！ 
