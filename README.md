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
| `category` | String | `mrt_station` / `thsr_station` / `tra_station` |
| `networkID` | String? | `taipei_mrt` / `kaohsiung_mrt` / `new_taipei_mrt` / `taoyuan_mrt` / `taichung_mrt` / `thsr` / `tra` |
| `lineCodes` | [String]? | 所屬路線代碼陣列，e.g. `["R"]` / `["R", "BL"]` / `null`（台鐵、高鐵無路線代碼） |
| `stationCode` | String? | 官方站碼，e.g. `"R10"` / `"R10;BL12"` / `"6110"` |
| `latitude` | Double | 印章中心緯度 |
| `longitude` | Double | 印章中心經度 |
| `gpsRadiusMeters` | Double | 允許感應的 GPS 半徑（公尺） |
| `isActive` | Bool | 是否啟用 |
| `campaignID` | String? | 活動 ID（`null` 表示一般印章） |
| `stampImageURLs` | [String]? | 印章圖示 URL 陣列 |
| `description` | String? | 簡介文字 |
| `action` | String? | `fogErase`（預設）/ `geofenceUnlock` / `collectionOnly` |
| `unlock` | Object? | 解鎖彈窗，含 `title` / `subtitle?` / `animation?` |

### Stamp ID 命名規則

| 網路 | 前綴 | 範例 ID |
|------|------|---------|
| 臺北捷運 | `tp_` | `tp_R10`、`tp_G08` |
| 高雄捷運 | `ks_` | `ks_R4`、`ks_O5` |
| 新北捷運 | `nt_` | `nt_O01` |
| 桃園捷運 | `ty_` | `ty_A1` |
| 臺中捷運 | `tc_` | `tc_G01` |
| 台灣高鐵 | `thsr_` | `thsr_taipei`、`thsr_taichung` |
| 臺鐵 | `tra_` | `tra_taipei`、`tra_hualien` |

### action 說明

- `fogErase`（預設）：擦除地圖霧 + 加入收集
- `geofenceUnlock`：觸發 Geofence 解鎖 + 加入收集
- `collectionOnly`：僅加入收集，不影響地圖

### 範例（捷運交會站）

```json
{
  "id": "tp_R10",
  "name": "台北車站",
  "category": "mrt_station",
  "networkID": "taipei_mrt",
  "lineCodes": ["R", "BL"],
  "stationCode": "R10;BL12",
  "latitude": 25.047801,
  "longitude": 121.517004,
  "gpsRadiusMeters": 150,
  "isActive": true,
  "campaignID": null,
  "stampImageURLs": [],
  "description": "臺北捷運台北車站（R10）",
  "action": "fogErase",
  "unlock": null
}
```

## 目前印章統計

| 網路 | 站數 | GPS 半徑 |
|------|------|---------|
| 臺鐵 | 221 | 200m |
| 臺北捷運 | 109 | 150m |
| 高雄捷運 | 75 | 150m |
| 新北捷運 | 37 | 150m |
| 桃園捷運 | 22 | 150m |
| 臺中捷運 | 18 | 150m |
| 台灣高鐵 | 12 | 250m |
| **合計** | **494** | |

*站點資料來源：OpenStreetMap（© OpenStreetMap contributors, ODbL）*

## NFC 標籤寫入格式

標籤中儲存 NDEF URL，格式為：

```
https://div-sir.github.io/lumiveil-stamps/s/{stampID}
```

App 會自動附加 `.json` 後綴來取得印章資料。
