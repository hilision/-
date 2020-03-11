---
description: 无论怎样新建activity都无法解析
---

# R类解析layout文件报错

升级了AS到最新版，然后写项目的过程中发现，new 一个Activity总是报解析layout文件失败。反复核查引入的R类是否属于该工程（这是一个比较常见的错误），以及xml文件命名以及位置是否准确后。我确认是AS的问题。随即build项目，没有报错。随后重启AS，便一切正常。

