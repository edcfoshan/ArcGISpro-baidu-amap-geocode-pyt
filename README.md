**QQ 交流群：826861025**

# arcgis-baidu-amap-geocode

[English](README_EN.md) | 中文

集成百度地图与高德地图 Web 服务 API 的 **ArcGIS Pro** Python 工具箱（`.pyt`），提供面向中国坐标系的地理编码、POI 检索、逆地理编码、行政区划边界导出和坐标系转换功能。

## 环境要求

| 项目 | 要求 |
|------|------|
| **软件** | ArcGIS Pro **3.0 及以上**（不支持 ArcMap / ArcGIS 10.x） |
| **Python** | 随 ArcGIS Pro 自带（3.x），无需额外安装 |
| **API Key** | 百度地图 Key 和/或高德地图 Key（**必须自行申请并填写**，工具箱无内置 Key） |

> 本工具箱基于 ArcGIS Pro 3.x 的 Python 3 环境开发，在 ArcMap 或 ArcGIS Desktop 10.x 下无法运行。

## 功能概览

| 工具 | 说明 |
|------|------|
| **A_全国行政区划_边界导出** | 省/市/区县级联下拉选择，导出行政区边界面（支持百度/高德双平台） |
| **B_高德 POI 批量采集** | 在指定范围内按关键词或分类采集高德 POI 数据，自动递归拆分高密度区域 |
| **C_百度地点检索3.0** | 百度 POI 批量采集，支持矩形区域检索 |
| **D_地理编码_地名转点坐标** | 输入地址表，按地址字段进行百度/高德地理编码，输出点要素类（支持双平台都要模式） |
| **E_逆地理编码_坐标信息转最近点信息** | 输入点坐标，输出附近 POI 列表（长表格式，每 POI 一行） |
| **F_坐标系转换** | WGS84 / GCJ02(国测局) / BD09(百度) / CGCS2000 之间的批量坐标转换 |

## ❤️ 赞助商

<a href="https://jizhanai.top/register?ref=PBUXGDHTFUAS">
  <img src="./content/sponsors/jizhan-banner.svg" width="100%" alt="极栈：填写邀请码 PBUXGDHTFUAS 减 5 元，点击注册开通" />
</a>

<table>
  <tr>
    <td width="24%" align="center">
      <a href="https://jizhanai.top/register?ref=PBUXGDHTFUAS"><img src="./content/sponsors/jizhan-wordmark.svg" width="180" alt="极栈 jizhanai.top，点击通过邀请链接注册" /></a>
    </td>
    <td>感谢 <a href="https://jizhanai.top/register?ref=PBUXGDHTFUAS"><b>极栈 · jizhanai.top</b></a> 赞助支持本项目！极栈提供 <b>ChatGPT 会员充值</b>服务，支持<b>支付宝支付</b>。选购 <b>ChatGPT 激活码</b>后，按站内指引前往码港兑换。<br><br>通过<a href="https://jizhanai.top/register?ref=PBUXGDHTFUAS">邀请链接注册开通</a>，填写邀请码 <code>PBUXGDHTFUAS</code>，可减 <b>5 元</b>。</td>
  </tr>
</table>

## 安装

1. 克隆或下载本仓库到本地目录
2. 在 ArcGIS Pro 中，打开 **目录** 窗格 → **工具箱** → 右键 → **添加工具箱**，选择 `百度高德Geocode.pyt`
   ![添加工具箱](截图/1添加工具箱.png)
   *在目录窗格中右键"工具箱"，选择"添加工具箱"*
3. 在弹出的文件浏览对话框中，选中 `百度高德Geocode.pyt`，点击确定
   ![选择工具箱文件](截图/2点击工具箱.png)
   *浏览到仓库目录，选中 .pyt 文件后点击确定*
4. 弹出第三方代码运行确认对话框，点击 **是** 允许运行
   ![确认运行](截图/3确定运行.png)
   *点击"是"允许工具箱代码运行*
5. 工具箱添加成功，展开即可看到全部 6 个工具（A~F）
   ![工具列表](截图/4工具列表.png)
   *工具箱包含 6 个地理工具：行政区划导出、POI采集、地理编码、逆地理编码、坐标转换*
6. **首次使用前必须配置 API Key**（见下方）

## 密钥配置（首次使用必读）

工具箱不包含任何 API Key，**必须自行申请并填写后才能使用**。详细配置指南见 [CONFIG.md](CONFIG.md)。

### 填写步骤

1. **申请 Key**
   - 百度：https://lbsyun.baidu.com/apiconsole/key → 创建「服务端」类型应用
   - 高德：https://console.amap.com/dev/key/app → 创建「Web服务」类型应用

2. **找到配置文件** — 在工具箱目录下的 `config/` 文件夹中：
   ```
   arcgis-baidu-amap-geocode/
   └── config/
       ├── baidu_keys.txt    ← 百度 Key 填这里
       └── amap_keys.txt     ← 高德 Key 填这里
   ```

3. **用记事本打开** `baidu_keys.txt` 或 `amap_keys.txt`，内容如下：
   ```
   # 百度地图 API Key 配置文件
   # ……
   # 使用方法：
   #   删除下面行首的 # 号，把 your_baidu_key 替换成你的真实 Key
   #   每行一个 Key，可配多个提高速度
   #
   #your_baidu_key_here
   ```

4. **删除 `#` 号，替换为真实 Key**，例如：
   ```
   AbCdEf1234567890GhIjKlMnOpQrStUv
   ```
   - 每行一个 Key，以 `#` 开头的行为注释
   - 可配置多个 Key 提高并发速度和避免单 Key 配额不足

5. 保存文件，重新运行工具即可

> **按需配置**：只用高德工具只需填 `amap_keys.txt`，只用百度工具只需填 `baidu_keys.txt`。

## 坐标系说明

中国常用的坐标系统及其关系：

| 坐标系 | 别名 | 说明 |
|--------|------|------|
| **WGS84** | EPSG:4326 | 国际标准，GPS 使用 |
| **GCJ-02** | 火星坐标系 | 中国国测局标准，高德、腾讯使用 |
| **BD-09** | 百度坐标系 | 百度地图专用，在 GCJ-02 基础上二次加密 |
| **CGCS2000** | 2000国家大地坐标系 | 中国官方大地基准，与 WGS84 数值近似（本工具按等值处理） |

转换关系：BD-09 → GCJ-02 → WGS84 ↔ CGCS2000

## 并发与速度档位

工具箱提供两个处理速度档位：

- **低（稳定）**：使用 25% 的 Key 理论并发量，适合个人开发者免费配额
- **中（平衡）**：使用 50% 的 Key 理论并发量

并发线程数根据 Key 数量和速度档位自动计算（单个 Key 按 30 QPS 估算）。

## 注意事项

- 输出空间参考统一写为 WGS84 (EPSG:4326)。选择 GCJ-02 输出时，坐标值保留 GCJ-02，但空间参考字段仍为 WGS84
- 高德 POI 批量采集在单区域结果超过 25×触发页数时会自动递归拆分为 4 个子象限继续采集
- 百度 POI 检索 3.0 接口**必须**填写关键词（query），不支持空关键词全量搜索
- 输出 GDB 建议使用 File Geodatabase（以 .gdb 结尾的目录）或勾选"使用临时空间"

## 关注与赞赏

扫码关注「极思G工作室」公众号、加入 QQ 交流群，获取工具更新、交流使用经验：

<img src="./content/求关注-极思G-20261014.png" width="360" alt="关注极思G：公众号与 QQ 交流群" />

如果这些工具对你有帮助，欢迎赞赏支持。赞赏完全自愿，感谢你的支持。

<img src="./content/求赞赏-极思G-20261014.png" width="360" alt="支持极思G：微信赞赏与爱发电" />

## License

[MIT](LICENSE)
