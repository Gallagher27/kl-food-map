# 吉隆坡美食地图

这是一个可静态托管的单页 HTML 美食地图。直接上传 `index.html` 到 GitHub Pages、Netlify、Cloudflare Pages 或任意静态网站托管即可访问。

## 当前版本

- 使用 Leaflet 作为轻量交互层，不再加载外部底图瓦片。
- 只保留吉隆坡市区几条主干道的简化线条，提升手机拖动流畅度。
- 支持浏览器实时定位，并按当前位置持续更新到餐厅的大致直线距离。
- 支持 1-5 星个人评价和备注，保存在当前浏览器。
- 支持导入 JSON/CSV 地点清单，支持导出当前数据。
- 每个地点可以配置 Google Maps 链接，点击后跳转查看照片、菜单、营业时间、路线等公开信息。

## 定位说明

定位需要在 HTTPS 页面下使用，GitHub Pages 已满足这个条件。首次点击定位按钮时，浏览器会弹出位置权限请求；如果之前点过拒绝，需要在浏览器地址栏左侧的网站权限里重新允许位置权限。

## 推荐数据格式

JSON:

```json
[
  {
    "id": "wanjo",
    "name": "Nasi Lemak Wanjo Kampung Baru",
    "area": "Kampung Baru",
    "category": "马来",
    "price": "$",
    "googleRating": 4.2,
    "lat": 3.1629,
    "lng": 101.7062,
    "tags": ["椰浆饭", "本地感"],
    "googleMapsUrl": "https://www.google.com/maps/search/?api=1&query=Nasi%20Lemak%20Wanjo%20Kampung%20Baru"
  }
]
```

CSV 表头:

```csv
id,name,area,category,price,googleRating,lat,lng,tags,googleMapsUrl
wanjo,Nasi Lemak Wanjo Kampung Baru,Kampung Baru,马来,$,4.2,3.1629,101.7062,椰浆饭|本地感,https://www.google.com/maps/search/?api=1&query=Nasi%20Lemak%20Wanjo%20Kampung%20Baru
```

## Google Maps 收藏同步判断

个人 Google Maps 收藏列表通常不能被一个普通公开网页直接读取。更稳妥的路径是：

1. 先从 Google Maps 或 Google Takeout 导出/整理为 CSV 或 JSON，再导入本页面。
2. 如果需要自动补全照片、价格、评分、营业信息，用 Google Places API 读取公开地点数据；这需要 Google Cloud API Key、账单配置和配额管理。
3. 如果需要朋友共同编辑星级和备注，需要接一个后端数据库，例如 Supabase、Firebase 或自建接口。纯静态 HTML 只能把评价和备注保存在各自浏览器里。
