---
created: 2026-03-10
updated: 2026-03-10
status: 🟥
type: work
tags:
  - ✅/🟨
topics:
  - "[[Monday]]"
  - "[[MetaGuru]]"
  - "[[2026]]"
projectCode: P015
publish: true
---
# 處理一對多與陣列映射 (Array Mapping) 實作範例

本文檔紀錄如何透過資料表 `mapping_field_definition` 設計，來處理來源資料包含子陣列（Master-Detail 明細），並將其轉換為目標系統所需之 JSON 陣列結構。

## 1. 來源資料 (Source JSON)
假設從來源系統收到一筆包含 `lines` 陣列的訂單資料：
```json
{
  "orderId": "ORD-001",
  "customer": "John Doe",
  "data": {
    "lines": [
      { "item_code": "A01", "qty": 2, "price": 100 },
      { "item_code": "B02", "qty": 1, "price": 300 }
    ]
  }
}
```

## 2. 目標資料格式需求 (Target JSON)
經過轉換引擎處理後，拋給目標系統的資料需要長這樣：
```json
{
  "TargetOrderId": "ORD-001",
  "BuyerName": "John Doe",
  "OrderLines": [
    {
      "SkuCode": "A01",
      "Quantity": 2,
      "UnitPrice": 100,
      "LineTotal": 200
    },
    {
      "SkuCode": "B02",
      "Quantity": 1,
      "UnitPrice": 300,
      "LineTotal": 300
    }
  ]
}
```

## 3. 資料表 Mapping 設定
我們在資料表 `mapping_field_definition` 中建立**兩組 Mapping**：一組處理外層（主單），一組處理內層（明細）。

### A. 處理外層的主規則 (`mapping_id`: `Map-Order-Main`)
| mapping_id | target_field | source_field | transform_type | transform_config (JSON) |
| :--- | :--- | :--- | :--- | :--- |
| Map-Order-Main | `TargetOrderId` | `orderId` | `direct` | `NULL` |
| Map-Order-Main | `BuyerName` | `customer` | `direct` | `NULL` |
| **Map-Order-Main** | **`OrderLines`** | **`data.lines`** | **`array_map`** | **`{ "child_mapping_id": "Map-Order-Line" }`** |

> **說明**：外層規則遇到陣列型態時，將 `transform_type` 設為 `array_map`。其工作為：將 `data.lines` 陣列拆開跑迴圈，並將陣列中的每一個元素交給 `child_mapping_id` (即 `Map-Order-Line`) 進行轉換。

### B. 處理內層明細的子規則 (`mapping_id`: `Map-Order-Line`)
子規則處理的對象為「單一明細物件」。此時 `transform_type` 就會使用一般的轉換標籤（例如 `direct`、`concat` 等）。

| mapping_id | target_field | source_field | transform_type | transform_config (JSON) |
| :--- | :--- | :--- | :--- | :--- |
| **Map-Order-Line** | `SkuCode` | `item_code` | **`direct`** | `NULL` |
| **Map-Order-Line** | `Quantity` | `qty` | **`direct`** | `NULL` |
| **Map-Order-Line** | `UnitPrice` | `price` | **`direct`** | `NULL` |
| **Map-Order-Line** | `LineTotal` | `NULL` | **`concat`** | `{ "fields": ["qty", "*", "price"] }` *(公式示意)* |

## 4. 轉換引擎執行邏輯 (C# 虛擬碼概念)
在 C# 程式端，轉換引擎處理 `array_map` 的核心遞迴（或迴圈）邏輯約如下所示：

```csharp
// 1. 處理主單的 OrderLines 欄位
var sourceArray = sourceJson.SelectToken("data.lines") as JArray;
var targetArray = new JArray();

if (sourceArray != null)
{
    // 2. 當遇到 transform_type == "array_map" 時，取得子規則 ID
    // 假設 transform_config = { "child_mapping_id": "Map-Order-Line" }
    string childMappingId = GetConfigValue(transform_config, "child_mapping_id");

    foreach (var sourceItem in sourceArray)
    {
        // 3. 對陣列裡的每一個元素，遞迴呼叫轉換引擎，套用子 Mapping
        JObject mappedItem = Engine.Transform(sourceItem, childMappingId); 
        targetArray.Add(mappedItem);
    }
}

// 4. 最後把轉換完的陣列賦值給目標欄位
targetJson["OrderLines"] = targetArray;
```

## 結論
透過在 `transform_type` 擴充 `array_map` 機制，並將每一層的轉換作業獨立在不同的 `mapping_id` 群組，資料表在儲存 `mapping_field_definition` 時就能維持扁平的關聯設計。
