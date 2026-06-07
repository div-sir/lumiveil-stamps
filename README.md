# lumiveil-stamps

Lumiveil NFC 印章資料庫，透過 GitHub Pages 提供服務。

Base URL: `https://div-sir.github.io/lumiveil-stamps`

## 印章格式

每個印章為一個 JSON 檔案，放置於 `s/` 目錄：

```
https://div-sir.github.io/lumiveil-stamps/s/{stampID}.json
```

### 欄位說明

| 欄位 | 型別 | 說明 |
|------|------|------|
| `id` | String | 唯一識別碼，與檔名相同 |
| `name` | String | 顯示名稱（中文） |
| `category` | String | `mrt_station` / `landmark` / `thsr_station` / `tra_station` |
| `networkID` | String? | `taipei_mrt` / `tokyo_metro` / `thsr` / `tra` |
| `lineCode` | String? | 路線代碼，e.g. `R` / `BL` / `G` |
| `stationCode` | String? | 官方站碼，e.g. `R10` |
| `latitude` | Double | 印章中心緯度 |
| `longitude` | Double | 印章中心經度 |
| `gpsRadiusMeters` | Double | 允許感應的 GPS 半徑（公尺） |
| `isActive` | Bool | 是否啟用 |
| `campaignID` | String? | 活動 ID（`null` 表示一般印章） |
| `stampImageURLs` | [String]? | 印章圖示 URL 陣列（可為空） |
| `description` | String? | 簡介文字 |
| `action` | String? | `fogErase`（預設）/ `geofenceUnlock` / `collectionOnly` |
| `unlock` | Object? | 解鎖彈窗內容，含 `title` / `subtitle?` / `animation?` |

### action 說明

- `fogErase`（預設）：擦除地圖霧 + 加入收集
- `geofenceUnlock`：觸發 Geofence 解鎖 + 加入收集
- `collectionOnly`：僅加入收集，不影響地圖

### 範例

```json
{
  "id": "taipei_main",
  "name": "台北車站",
  "category": "mrt_station",
  "networkID": "taipei_mrt",
  "lineCode": "R",
  "stationCode": "R10",
  "latitude": 25.0478,
  "longitude": 121.5170,
  "gpsRadiusMeters": 200,
  "isActive": true,
  "campaignID": null,
  "stampImageURLs": [],
  "description": "台北捷運樞紐站，淡水信義線 × 板南線交會",
  "action": "fogErase",
  "unlock": null
}
```

## 目前印章清單

### 台北捷運（30 站）

| 站名 | ID | 路線 |
|------|----|------|
| 台北車站 | `taipei_main` | R / BL |
| 台大醫院 | `R_ntu_hospital` | R |
| 中正紀念堂 | `R_cksmemorial` | R |
| 古亭 | `guting` | R / G |
| 台電大樓 | `taipower` | G |
| 公館 | `gongguan` | G |
| 萬隆 | `wanlong` | G |
| 中山 | `R_zhongshan` | R |
| 雙連 | `R_shuanglian` | R |
| 民權西路 | `R_minquan_w` | R / O |
| 圓山 | `R_yuanshan` | R |
| 劍潭 | `R_jiantan` | R |
| 士林 | `R_shilin` | R |
| 西門 | `BL_ximen` | BL |
| 龍山寺 | `BL_longshan` | BL |
| 江子翠 | `BL_jiangzicui` | BL |
| 忠孝新生 | `zhongxiao_xinsheng` | BL / G |
| 忠孝復興 | `zhongxiao_fuxing` | BL |
| 忠孝敦化 | `BL_dunhua` | BL |
| 國父紀念館 | `BL_sunyatsen` | BL |
| 市政府 | `BL_cityhall` | BL |
| 永春 | `BL_yongchun` | BL |
| 後山埤 | `BL_houshandong` | BL |
| 松山 | `G_songshan` | G |
| 南京三民 | `G_nanjing_sanmin` | G |
| 台北小巨蛋 | `G_taipei_arena` | G |
| 南京復興 | `G_nanjing_fuxing` | G |
| 松江南京 | `G_songjiang` | G / O |
| 行天宮 | `G_xingtian` | G |
| 東門 | `G_dongmen` | G |

## NFC 標籤寫入格式

標籤中儲存 NDEF URL，格式為：

```
https://div-sir.github.io/lumiveil-stamps/s/{stampID}
```

App 會自動附加 `.json` 後綴來取得印章資料。
