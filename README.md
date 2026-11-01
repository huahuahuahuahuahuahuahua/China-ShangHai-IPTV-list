[上海联通增强播放列表](IPTV_Enhanced_change.m3u)
上海IPTV组播和时移地址，最新更新三家运营商
已经包含最新CCTV-5,6,8 HD

## 增强播放列表的节目单与台标

通用版 `IPTV_Enhanced_change.m3u` 和 Kodi 专用版 `IPTV_Enhanced_change_kodi.m3u` 均使用 [plsy1 的多天 XMLTV 节目单](https://raw.githubusercontent.com/plsy1/epg/main/e/seven-days.xml.gz)，地址已写入文件头的 `x-tvg-url`。

根据 2026-11-01 下载的节目单重新核对了全部 95 个频道：

- 72 个频道的 `tvg-id` 已对齐新 XMLTV 的数字 `channel id`，`tvg-name` 使用该频道的一个有效 `display-name`。例如 CCTV5 对应 `tvg-id="108"`、`tvg-name="CCTV5"`。
- `CETV1`、`CETV2`、中国教育四套分别对应新节目单的中国教育1、2、4，ID 为 `70`、`71`、`72`。
- 相比旧节目单，新增哈哈炫动、生活时尚、茶频道、嘉佳卡通和教育四套的关联；欢笑剧场、四川卫视、海南卫视、家庭理财在本次新源中没有明确对应频道，已移除旧 EPG 标识。
- 未找到明确对应频道的条目保留直播，不强行关联相似频道。频道显示名称保持本次切换前的名称。
- 95 个频道均添加 `tvg-logo`。图标使用 [fanmingming/live](https://github.com/fanmingming/live) 图标库的 GitHub Raw 链接；感谢原图标库维护者。
- 本次切换不改变直播地址、频道顺序、台标或回看参数。

播放器支持 `tvg-id` 时，应优先按频道 ID 匹配节目单。如果播放器没有读取 M3U 内的节目单地址，请手动设置为上面的地址并刷新节目单和播放列表。如果曾在客户端显式填写旧 EPG URL，也需要清空该项或改为新地址。

本次下载的 CCTV5 数据涉及 2026-10-25 至 2026-11-02。以央视体育官方排程核对 10 月 31 日、11 月 1 日、11 月 2 日，节目名称和起止时间全部一致的条数分别为 14/18、18/19、25/25；历史赛事仍有时段差异，未来排程也可能调整。该源是第三方整理的 XMLTV，不是央视直接提供的 XMLTV；其他频道仅核对了标识映射，未逐条验证内容准确性。

### Kodi / IPTV Simple Client

Kodi 用户请订阅 [Kodi 专用播放列表](https://raw.githubusercontent.com/huahuahuahuahuahuahuahua/China-ShangHai-IPTV-list/refs/heads/master/IPTV_Enhanced_change_kodi.m3u)。它保留同样的 95 个频道、直播 URL、EPG 映射和台标，并在每个频道的 `#EXTINF` 行写入：

```text
catchup="append" catchup-source="&playseek={utc:YmdHMS}-{utcend:YmdHMS}"
```

每频道回看参数可避开 IPTV Simple Client 21.11.0 对文件头 `catchup-source` 默认值的继承问题；时间占位符使用 Kodi 支持的格式，`&` 用于追加到已有查询参数的直播 URL。

- 在 IPTV Simple Client 的当前实例中保持“启用回放”打开。
- “请求格式字符串”可以留空，频道自己的 `catchup-source` 会提供模板。
- 回放窗口时间按运营商实际保留天数设置；设为 5 天不会使服务器额外保存录像。
- EPG URL 可以留空，由播放列表文件头的 `x-tvg-url` 提供；也可以显式填写新地址 <https://raw.githubusercontent.com/plsy1/epg/main/e/seven-days.xml.gz>。不要继续保留旧源地址。
- 保存订阅后重新加载客户端；如启用了播放列表缓存，确认已经读取 Kodi 专用文件。
- 节目单频道 ID 已随新源更新。如果仍显示旧指南，重新加载播放列表后，在 Kodi 的 PVR 与直播电视设置中清除指南数据并重新获取。
- 要在指南中显示多天历史节目，还需调整 Kodi 的“设置 → PVR 与直播电视 → 指南 → 显示的过去日数”。

回看请求已验证能从运营商服务器获得 HLS 播放列表，完整视频播放仍需在 Kodi 上验证。

以下 23 个频道未指定节目单 ID，以免关联到错误频道：

| 原因 | 频道 |
| --- | --- |
| 本次节目单未找到明确对应频道 | 新闻综合HD、都市频道HD、东方影视HD、第一财经HD、五星体育HD、欢笑剧场4K、上海教育HD、CGTN、风云足球HD、央视台球HD、兵器科技HD、世界地理HD、女性时尚HD、高尔夫网球HD、怀旧剧场HD、风云剧场HD、第一剧场HD、风云音乐HD、央视文化精品HD、四川卫视、海南卫视、早期教育HD、家庭理财 |

名称对应不代表已经验证直播可播放，也不代表 4K 版本与普通版本一定同播。当前直播地址属于运营商内网，需要在相应网络环境使用。节目单和台标均依赖第三方服务，后续覆盖和内容可能变化。
