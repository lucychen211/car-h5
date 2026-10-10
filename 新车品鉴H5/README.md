# 新车品鉴邀约 H5 · 使用说明

**交付文件只有一个：`index.html`**（约 70KB）
双击就能在电脑上预览；上传到 GitHub Pages 后，手机用 https 链接打开。

---

## 一、怎么改内容

### 1. 改门店信息 / 活动日期（最常用）

打开 `index.html`，拉到**最底部 `<script>` 的开头**，找到这一段：

```js
var CONFIG = {
  shop:        '赣州鑫迪比亚迪 4S 店',
  address:     '江西省赣州市章贡区开发区金岭西路 168 号',
  addressFull: '赣州鑫迪比亚迪 4S 店 · 江西省赣州市章贡区开发区金岭西路 168 号',
  phone:       '0797-88866699',
  phoneHref:   '07978886699',

  eventDate:      '2026 年 10 月 18 日（周日）',
  eventDateShort: '10 月 18 日',
  eventStart:     '09:00',
  eventTime:      '09:00 - 17:00',
  validRange:     '2026.10.18 - 2026.10.20',

  countdownTarget: '2026-10-18T09:00:00+08:00',
  mapUrl: 'https://uri.amap.com/marker?position=114.9351,25.8312&name=...'
};
```

**改这一处，封面、引言页、礼遇页、报名页、门店页里所有对应文字和按钮链接会一起变**，不用一页页去找。

- `phoneHref` 只能填**纯数字**（点「一键拨号」实际拨出的号码）
- `countdownTarget` 是倒计时截止时刻，格式 `年-月-日T时:分:秒+08:00`
- `mapUrl` 的 `position` 填门店真实经纬度（**经度,纬度**），直接用高德地图搜门店→分享→复制坐标即可

### 2. 改某一页的文案

在编辑器里搜索页面注释，例如搜 **`第 3 页`**、**`第 4 页`**，
就能定位到那一段，直接改中文即可，样式不用动。

七个页面依次是：封面 → 活动引言 → 车型亮点 → 活动流程 → 到店礼遇 → 在线报名 → 门店信息。

### 3. 更换门店二维码

二维码已经**内嵌进 `index.html` 了**（base64 编码，所以整个作品仍然只有一个文件，
不需要额外的图片文件，上传到 GitHub 也不会丢图）。

要换成别的二维码，两种办法：

**办法 A（推荐，免转换）** —— 把第 7 页那段 `<button class="qr" …>` 里直接换成外链图片：

```html
<button class="qr" type="button" id="qrBtn" aria-label="点击放大二维码">
  <img id="qrImg" src="https://你的图床/新二维码.png" alt="门店企业微信二维码">
  <span class="qr-zoom">点击放大</span>
</button>
```

**办法 B（仍保持单文件）** —— 把新二维码转成 base64 再替换 `src` 里
`data:image/png;base64,` 后面那一长串。可以搜「在线图片转 base64」，
把转换结果整段粘进去即可。

> 二维码建议用**方图、白底、分辨率 300px 以上**，扫起来最稳。
> 页面里的二维码点击后会**全屏放大**，方便对方扫码。

### 4. 换成真实车图

搜 **`车辆插画`**，把那一整段 `<svg> … </svg>` 替换成：

```html
<img src="车图.jpg" alt="宋 PLUS DM-i 2026 款" style="width:100%;border-radius:16px">
```

建议车图宽度 **1200px 左右、横向**，避免手机打开模糊。
（现在用的是矢量插画，所以任何屏幕都不糊、不变形。）

### 5. 增删背景装饰元素

页面里的绿色装饰（叶子 / 圆环 / 波浪 / 能量节点 / 圆点矩阵 / 叶枝）
统一定义在 `<body>` 开头那个 **`<svg width="0" height="0">` 图形库**里，
每页再用一行 `<use>` 调用，例如：

```html
<svg class="deco deco-soft drift" style="top:9%;left:-24px;width:126px">
  <use href="#d-branch"/>
</svg>
```

- **想删掉某个装饰** → 把那一整行 `<svg class="deco" …>…</svg>` 删掉即可
- **想挪位置 / 改大小** → 改 `style` 里的 `top / left / right / bottom / width`
  （用百分比最省事，比如 `top:10%` `width:120px`）
- **想改深浅** → class 换成 `deco-soft`（最淡）/ `deco-mid` / `deco-ring`
- **想加动效** → 加上 `drift`（上下浮动）、`drift2`（反向浮动）、
  `sway`（左右摇摆）、`spin`（缓慢旋转），可叠加
- **想要新的装饰形状** → 在图形库里照着原来的 `<symbol>` 复制一份，
  改 `id`，再在页面里 `<use href="#你的新id"/>` 调用

底色里的**绿色圆点网格**是 `.page::after` 里的第一层背景，想调密度就改
`background-size:18px 18px` 那个数字。

---

## 二、发布到 GitHub Pages（拿到永久 https 链接）

### 准备
没有 GitHub 账号就先在 https://github.com/signup 注册一个（免费）。

### 方法 A：网页上传（最简单，不用装任何软件）

1. 登录 GitHub → 右上角 **`+`** → **New repository**
2. 仓库名填 `car-h5`（或任意英文名），选 **Public**，**不要**勾 Add README
   → 点 **Create repository**
3. 在新仓库页面点 **uploading an existing file**
4. 把 `index.html` 拖进去 → 点 **Commit changes**
5. 点仓库的 **Settings** → 左侧 **Pages**
6. **Source** 选 `Deploy from a branch`，**Branch** 选 `main` + `/ (root)` → **Save**
7. 等 1～2 分钟刷新页面，顶部会出现网址：

   ```
   https://你的用户名.github.io/car-h5/
   ```

这就是永久 https 链接，手机、微信里都能直接打开。

### 方法 B：命令行推送（以后改动用这个更快）

```bash
cd 本文件夹
git init
git add index.html
git commit -m "新车品鉴邀约H5"
git branch -M main
git remote add origin https://github.com/你的用户名/car-h5.git
git push -u origin main
```

之后每次改完 `index.html`，只要：

```bash
git add index.html && git commit -m "更新" && git push
```

等 1 分钟左右刷新链接就是新版。

---

## 三、手机打不开时的排查

| 现象 | 原因 / 解决 |
|---|---|
| 微信里点开显示"已停止访问" | 微信对外链有限制。换成**手机自带浏览器**打开，或在微信里点右上角「···」→ 在浏览器打开 |
| 直接在文件管理器点 html 打不开 | 手机不能直接开本地 html。必须先上传拿到 https 链接 |
| 打开是白屏 | 检查刚才 Commit 的是不是 `index.html` 这个文件名（大小写敏感） |
| 链接 404 | Pages 还在构建，等 1～2 分钟刷新；或 Branch 选错了（应是 `main` + `/root`） |

---

## 四、这份作品对应了作业要求里的哪些"易忽略细节"

- **封面**：文字放在深色半透明遮罩条上，不压在车身上；有「上滑了解更多」引导；车图是矢量绘制，任意屏幕不糊不变形
- **引言页**：短句分段，写"客户能得到什么"，不堆参数；带实时倒计时
- **亮点页**：5 个卖点全部转成客户利益（如"起步安静顺滑，越堵越省油"），不写参数；明确标注 2026 新款
- **流程页**：每段都写"您能得到什么"；写明**试驾必须携带本人有效驾驶证**；标注"名额有限，建议提前报名"
- **礼遇页**：标注活动**有效期**、订车礼「限量」；底部免责小字"以门店现场解释为准"
- **报名页**：只 4 个字段；**提交成功提示** + "顾问会尽快联系您"；**一键拨号 + 一键导航**；隐私提示
- **尾页**：地图导航入口、**返回顶部**按钮、分享引导、**门店企业微信二维码可点击全屏放大**（小屏也能扫）
- **全局**：背景音乐**一键关闭**按钮、页码圆点、滚动进度条、手机端适配（滚动吸附翻页）、各页实测无内容溢出；绿色装饰元素（落叶 / 圆环 / 波浪 / 能量节点 / 点阵）带轻微浮动动效
