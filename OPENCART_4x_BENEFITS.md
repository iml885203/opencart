# OpenCart 4.x 升級優勢

## 與 3.x 架構比較

### 後端

| 項目 | 3.x | 4.x |
|------|-----|-----|
| PHP 版本 | 7.x (已 EOL) | **8.0+** |
| Namespace | 無 | **PSR-4 標準** |
| Twig | 1.x | **3.x** |
| SCSS | 無 | **內建編譯** |

### 前端

| 項目 | 3.x | 4.x |
|------|-----|-----|
| jQuery | 3.7.1 (必須) | **移除** |
| Bootstrap | 3.x | **5.x** |
| JavaScript | 全域變數 | **ES Modules** |
| 元件化 | 無 | **Web Components** |

---

## 4.x 前端架構

### ES Modules 模組化

```javascript
// 3.x - 全域變數污染
var cart = { add: function() {...} }
var wishlist = { add: function() {...} }

// 4.x - 模組化引入
import('./common/cart.js');
import('./common/wishlist.js');
import('./checkout/checkout.js');
```

### Web Components 元件化

```html
<!-- 3.x - jQuery 操作 DOM -->
<div id="currency">...</div>
<script>$('#currency').on('click', ...)</script>

<!-- 4.x - 自定義元件 -->
<common-currency></common-currency>
<common-cart></common-cart>
<common-search></common-search>
```

### 元件寫法

```javascript
// 4.x Web Component
import { WebComponent } from '../component.js';

class CommonCart extends WebComponent {
    async connected() {
        // 生命週期：元件載入
        let response = await fetch('index.php?route=checkout/cart.json');
        let data = await response.json();
        this.render(data);
    }

    render(data) {
        this.innerHTML = `...`;
    }
}

customElements.define('common-cart', CommonCart);
```

---

## 4.x 優勢

### 1. 移除 jQuery 依賴

| 優點 | 說明 |
|------|------|
| 減少體積 | jQuery 87KB → 0 |
| 原生 API | 使用標準 `fetch()`, `querySelector()` |
| 效能提升 | 少一層抽象 |

### 2. 模組化管理

| 優點 | 說明 |
|------|------|
| 命名空間隔離 | 不再污染全域 |
| 按需載入 | 動態 `import()` |
| Tree Shaking | 可搭配打包工具優化 |

### 3. 元件化開發

| 優點 | 說明 |
|------|------|
| 可重用 | 元件獨立封裝 |
| 易維護 | 邏輯集中在元件內 |
| 標準 API | Web Components 是瀏覽器原生標準 |

### 4. PHP 8 特性

| 特性 | 好處 |
|------|------|
| Named Arguments | 程式碼可讀性高 |
| Attributes | 取代 Annotations |
| Match Expression | 比 switch 更簡潔 |
| Constructor Promotion | 減少樣板程式碼 |
| JIT 編譯 | 效能提升 |

### 5. PSR-4 Namespace

```php
// 3.x - 無命名空間
class ControllerCatalogProduct extends Controller { }

// 4.x - PSR-4 標準
namespace Opencart\Catalog\Controller\Product;
class Product extends \Opencart\System\Engine\Controller { }
```

---

## SEO 影響

4.x 使用混合渲染架構：

| 內容類型 | 渲染方式 | SEO |
|----------|----------|-----|
| 產品/分類/文章 | SSR (PHP + Twig) | ✅ 友好 |
| 購物車/幣別切換 | CSR (Web Components) | 不影響 |

> 主要內容仍是伺服器端渲染，SEO 不受影響

---

## 擴充性比較

| 功能 | 3.x | 4.x |
|------|-----|-----|
| 新增前端功能 | 改 common.js 或新增 JS 檔 | 建立獨立 Web Component |
| 覆寫元件 | 困難 | 重新定義 Custom Element |
| 前端測試 | 困難 | 元件可獨立測試 |

---

## 升級注意事項

| 項目 | 說明 |
|------|------|
| PHP 版本 | 需升級至 8.0+ |
| 擴充套件 | 3.x 套件不相容，需找 4.x 版本 |
| 主題 | 需重新製作或購買 4.x 主題 |
| 資料庫 | 需執行升級腳本 |

---

## 適用情境

| 情境 | 建議 |
|------|------|
| 新專案 | ✅ 直接用 4.x |
| 3.x 小幅客製 | ⚠️ 評估升級成本 |
| 3.x 大量客製 | ⚠️ 可能需重新開發 |
| 需要最新安全更新 | ✅ 升級 4.x |

---

## 結論

| 面向 | 3.x | 4.x |
|------|-----|-----|
| 前端架構 | ⭐⭐ 過時 | ⭐⭐⭐⭐ 現代化 |
| 安全性 | ⭐⭐ PHP 7 EOL | ⭐⭐⭐⭐ PHP 8 |
| 擴充性 | ⭐⭐ 困難 | ⭐⭐⭐⭐ 元件化 |
| 效能 | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| 長期維護 | ⭐⭐ 停止更新 | ⭐⭐⭐⭐ 持續開發 |

> **建議**：如果必須使用 OpenCart，選擇 4.x 版本。但若追求更現代化的架構，可考慮 Nuxt + Supabase 等方案。
