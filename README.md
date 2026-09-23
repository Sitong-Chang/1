# Kunshan Cultural Atlas · demo

静态 HTML/CSS/JS 项目，可直接上传 GitHub 仓库根目录，Vercel 使用 Framework Preset: Other，Root Directory: `./`，无需构建命令。

## 数据与限制

- `data/places.geojson`：四个景区的**名称、类别**来自[昆山市人民政府旅游文化页](https://www.ks.gov.cn/kss/lywh/common_tt.shtml)。其中的经纬度是用于原型定位的**近似中心点**，尚未逐点经现场 GPS 或 OSM 核验，不能用于导航。
- 其余三个点（昆曲、奥灶面、锦溪饮食）明确为**示意点**；不指向真实商家或场馆。
- 地图底图使用 OpenStreetMap 瓦片，界面注明 © OpenStreetMap contributors。Leaflet 从 unpkg CDN 加载。网络不可用时显示错误说明。
- `data/routes.json`：团队自建的演示路段图。时间、文化分值、步行负担均为**假设值**，只用于展示不同目标如何改变选路。地图折线为节点间**示意连线**，不沿真实道路；无实时交通、公交班次、坡度、路缘坡道和无障碍认证。
- “舒缓步行”基于演示步行负担选择，绝不作为老人安全、无障碍或轮椅可达承诺。正式版需实地核验道路、休息点、厕所，并接入许可明确的道路路径与交通数据。

## 交互

类别筛选；点击地图或卡片查看地点；收藏；起终点选择；最快、文化探索、舒缓步行三种路线；比较时间、文化分和步行负担；重置。路线使用 Dijkstra 求解：最快按时间，文化探索按 `time - 3 * culture`（每段保证正权重），舒缓步行按 `time + 4 * walking`；同一演示路网可复现、可检查。

## 后续替换数据

实地核验坐标后修改 `places.geojson`；逐路段采样并记录来源后替换 `routes.json`。真实导航需要道路几何、可用的路由服务与交通时刻；不要把当前示意直线当导航。

## 本地运行

```bash
python3 -m http.server 8000 -d kunshan-cultural-map
```

浏览 http://localhost:8000 。不要双击 HTML 以 `file://` 打开，浏览器会限制本地 JSON 读取。
