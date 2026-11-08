词忆资源包 · 部署说明
=====================

这个目录里的 15 个 .ciyipack 是词书和离线发音包，manifest.json 是清单。
把它们原样上传到一个静态托管（对象存储 / GitHub Releases / Nginx 都行），
然后在 App 的「设置 → 词书与语音 → 资源来源」里填目录地址即可。

两个硬性要求
------------
1) 必须 HTTPS
   Android 9 起默认禁止明文 HTTP，http:// 的地址会直接下载失败。

2) 必须开 CORS
   App 页面在 WebView 里是 file:// 来源（Origin: null），响应需要带
   Access-Control-Allow-Origin: *
   Nginx 示例：
       add_header Access-Control-Allow-Origin *;
       add_header Access-Control-Allow-Headers Range;
   OSS / COS / GitHub raw 在控制台里打开 CORS 规则即可。

不想搭服务器
------------
把 .ciyipack 文件拷到手机里，在同一个页面点「从文件导入」选择文件，
效果一样，只是要手动拷。

文件清单
--------
book-<id>.ciyipack        每本词书（22 KB – 448 KB）
voice-es-<level>.ciyipack 西语发音包，按 DELE 等级拆（1.75 – 8.24 MB）
manifest.json             版本、大小、sha256、文件名
