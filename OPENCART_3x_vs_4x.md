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
