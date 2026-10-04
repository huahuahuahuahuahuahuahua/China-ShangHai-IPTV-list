[上海联通增强播放列表](IPTV_Enhanced_change.m3u)
上海IPTV组播和时移地址，最新更新三家运营商
已经包含最新CCTV-5,6,8 HD

## 增强播放列表的节目单与台标

`IPTV_Enhanced_change.m3u` 的节目单地址为 <https://epg.zsdc.eu.org/t.xml.gz>，已写入文件头的 `x-tvg-url`。

根据 2026-10-04 下载的节目单核对了全部 95 个频道：

- 71 个频道添加了与 XMLTV `channel id` 对应的 `tvg-id` 和与 `display-name` 对应的 `tvg-name`。
- 其中 66 个频道的显示名称已修正，包括去除清晰度后缀、统一 CCTV 连字符，以及将中国教育一套、二套分别映射为 `CETV1`、`CETV2`。
- `CCTV-4K` 改为 `CCTV4K`，保留频道身份中的 `4K`；`欢笑剧场4K` 使用节目单已有的显示名称，`tvg-id` 为 `欢笑剧场`。
- 95 个频道均添加 `tvg-logo`。图标使用 [fanmingming/live](https://github.com/fanmingming/live) 图标库的 GitHub Raw 链接；感谢原图标库维护者。
- 直播地址、频道顺序和原有回看参数保持原样。

播放器支持 `tvg-id` 时，应优先按频道 ID 匹配节目单。如果播放器没有读取 M3U 内的节目单地址，请手动设置为上面的地址并刷新节目单和播放列表。

### Kodi / IPTV Simple Client

Kodi 用户请订阅 [Kodi 专用播放列表](https://raw.githubusercontent.com/huahuahuahuahuahuahuahua/China-ShangHai-IPTV-list/refs/heads/master/IPTV_Enhanced_change_kodi.m3u)。它保留同样的 95 个频道、直播 URL、EPG 映射和台标，并在每个频道的 `#EXTINF` 行写入：

```text
catchup="append" catchup-source="&playseek={utc:YmdHMS}-{utcend:YmdHMS}"
```

每频道回看参数可避开 IPTV Simple Client 21.11.0 对文件头 `catchup-source` 默认值的继承问题；时间占位符使用 Kodi 支持的格式，`&` 用于追加到已有查询参数的直播 URL。

- 在 IPTV Simple Client 的当前实例中保持“启用回放”打开。
- “请求格式字符串”可以留空，频道自己的 `catchup-source` 会提供模板。
- 回放窗口时间按运营商实际保留天数设置；设为 5 天不会使服务器额外保存录像。
- EPG URL 可以留空，由播放列表文件头的 `x-tvg-url` 提供，也可以继续显式填写同一个地址。
- 保存订阅后重新加载客户端；如启用了播放列表缓存，确认已经读取 Kodi 专用文件。
- 要在指南中显示多天历史节目，还需调整 Kodi 的“设置 → PVR 与直播电视 → 指南 → 显示的过去日数”。

回看请求已验证能从运营商服务器获得 HLS 播放列表，完整视频播放仍需在 Kodi 上验证。

以下 24 个频道保留原名，未指定节目单 ID，以免关联到错误频道：

| 原因 | 频道 |
| --- | --- |
| 本次节目单未找到明确对应频道 | 新闻综合HD、都市频道HD、东方影视HD、第一财经HD、五星体育HD、哈哈炫动HD、生活时尚HD、茶频道HD、上海教育HD、风云足球HD、央视台球HD、兵器科技HD、世界地理HD、女性时尚HD、高尔夫网球HD、怀旧剧场HD、风云剧场HD、第一剧场HD、风云音乐HD、央视文化精品HD、嘉佳卡通、中国教育-4HD、早期教育HD |
| 需要确认实际频道语言 | CGTN（节目单有 `CGTN英语`，确认直播内容后可映射） |

名称对应不代表已经验证直播可播放，也不代表 4K 版本与普通版本一定同播。当前直播地址属于运营商内网，需要在相应网络环境使用。节目单和台标均依赖第三方服务，后续覆盖和内容可能变化。
