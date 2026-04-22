# 车流监控系统

## 项目简介

基于 Web 的车流监控可视化系统，支持实时车辆位置显示、车牌查询、通行历史查询、统计分析等功能。

## 功能特性

### 1. 地图可视化 (800×600)
- ✅ 出入口位置标注（东、南、西、北）
- ✅ 检查站位置标注（检查站1-6）
- ✅ 道路路径绘制（带方向箭头）
- ✅ 实时车辆位置显示
- ✅ 路径拥堵程度颜色标注：
  - 🟢 一级（0-3辆）- 绿色
  - 🟡 二级（4-6辆）- 黄色
  - 🔴 三级（7-9辆）- 红色

### 2. 实时监控面板
- 在线车辆数统计
- 出入口/检查站/路段数量统计
- 实时车辆列表（点击可定位）
- 自动刷新（3秒间隔）

### 3. 车牌查询
- 车辆详情查询（入站信息、位置、速度）
- 通行历史查询（分页显示）
- 历史记录表格（入站/出站/时间/速度/费用）

### 4. 统计信息
- 按车牌统计（自定义指标）
- 按出入口统计（进入/离开车辆数）
- 全部出入口统计汇总

## 技术栈

- HTML5 + CSS3 + JavaScript (ES5)
- HTML5 Canvas 地图绘制
- 纯前端实现，无外部依赖

## 使用说明

### 启动步骤

1. **启动模拟服务端**
   ```
   双击运行: 模拟服务端v0.1/模拟服务端.exe
   服务地址: http://127.0.0.1:12345
   ```

2. **打开监控页面**
   ```
   方式1: 直接双击 index.html 用浏览器打开
   方式2: 使用本地服务器
     python -m http.server 8080
     然后访问 http://localhost:8080
   ```

### API 接口

| 接口 | 方法 | 说明 |
|------|------|------|
| /getEntries | GET | 获取出入口列表 |
| /getCheckpoints | GET | 获取检查站列表 |
| /getVehiclePositions | GET | 获取实时车辆位置 |
| /getVehicleDetail?no=xxx | GET | 获取车辆详情 |
| /getVehiclesHistory?no=xxx&page=n | GET | 获取通行历史（分页） |
| /getStatisticsByVehicle?no=xxx | GET | 按车牌统计 |
| /getStatisticsByEntry?no=xxx | GET | 按出入口统计 |

## 数据格式

### 出入口 Entry
```json
{
  "No": "E-E",
  "Name": "东出入口",
  "Position": {"Pos_X": 800, "Pos_Y": 200},
  "Start": {"Pos_X": 600, "Pos_Y": 200},
  "End": {"Pos_X": 800, "Pos_Y": 200}
}
```

### 检查站 CheckPoint
```json
{
  "No": "C-1",
  "Name": "检查站1",
  "Position": {"Pos_X": 300, "Pos_Y": 500},
  "Start": {"Pos_X": 200, "Pos_Y": 400},
  "End": {"Pos_X": 400, "Pos_Y": 500}
}
```

### 车辆位置 VehiclePosition
```json
{
  "No": "V-3",
  "Position": {"Pos_X": 172, "Pos_Y": 486}
}
```

### 车辆详情 VehicleDetail
```json
{
  "No": "V-3",
  "EnterName": "西出入口",
  "EnterNo": "E-W",
  "EnterTime": "/Date(1776855975702+0800)/",
  "Position": {"Pos_X": 172, "Pos_Y": 486},
  "Speed": 86
}
```

### 通行记录 VehicleHistory
```json
{
  "VehicleNo": "V-3",
  "EnterName": "东出入口",
  "EnterNo": "E-E",
  "EnterTime": "/Date(...)/",
  "ExitName": "南出入口",
  "ExitNo": "E-S",
  "ExitTime": "/Date(...)/",
  "Speed": 97,
  "Charge": 16.94
}
```

### 出入口统计 Total
```json
{
  "Enter": 4,
  "Exit": 1
}
```

## 文件结构

```
车流监控系统/
├── index.html      # 主页面（单文件应用）
└── README.md       # 项目说明
```

## 浏览器兼容性

- Chrome 60+
- Edge 79+
- Firefox 60+
- Safari 12+

## 注意事项

1. 系统需要连接模拟服务端才能获取实时数据
2. 模拟服务端默认监听 127.0.0.1:12345
3. 页面使用 XMLHttpRequest 进行跨域请求，需要浏览器允许本地文件访问或部署到服务器
4. 建议将页面部署到本地服务器以获得最佳体验

## 作者

大作业项目 - 车流监控系统
