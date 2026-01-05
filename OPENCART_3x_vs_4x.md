# OpenCart 3.x vs 4.x 擴充比較

## 3.x 瓶頸

### 前端架構
| 問題 | 影響 |
|------|------|
| jQuery + 全域變數 | 命名衝突、難以維護 |
| 沒有模組化 | 無法 tree shaking、HTTP 請求多 |
| 沒有 bundle | CSS/JS 未壓縮合併 |
| 硬編碼選擇器 | 改 HTML 容易壞 |

### 付款串接
- 需建立 **7+ 個檔案**（controller, view, model, language × admin/catalog）
- 沒有統一 Payment Interface
- Webhook 處理分散

### 多語系
- **374 個語系檔**需維護
- 沒有 fallback 機制
- 新功能 = 語系檔 × 語言數

### 資料庫
| 問題 | 影響 |
|------|------|
| 沒有 ORM | 手動拼 SQL 字串，易出錯 |
| 沒有 Migration | Schema 變更無版本控制 |
| MyISAM 引擎 | 不支援 Transaction / Foreign Key |
| 大量子查詢 | 單一 SQL 過度複雜，效能差 |

**風險：**
- **SQL Injection**：依賴 `$this->db->escape()` 手動跳脫，漏寫就有漏洞
- **資料不一致**：MyISAM 無 Transaction，寫入中斷會造成髒資料
- **難以重構**：沒有 Migration，多環境部署 Schema 難同步
- **效能瓶頸**：Raw SQL 沒有快取機制，N+1 查詢問題常見

---

## 4.x 改進

### 前端
```
3.x: jQuery 全域變數
4.x: ES Modules + Web Components
```

| 3.x | 4.x |
|-----|-----|
| `var cart = {...}` | `import { cart } from './cart.js'` |
| Bootstrap 3 | Bootstrap 5 |
| 無元件化 | Custom Elements |

### 後端
| 項目 | 3.x | 4.x |
|------|-----|-----|
| PHP | 7.x | 8.0+ |
| Namespace | 無 | PSR-4 |
| SCSS | 無 | 內建編譯 |

---

## 結論

| 需求 | 3.x | 4.x |
|------|-----|-----|
| 簡單客製 | 可行 | 更好 |
| 複雜互動 | 困難 | 元件化支援 |
| 長期維護 | 技術債累積 | 架構較現代 |

**建議**：新專案用 4.x，舊專案評估升級成本
