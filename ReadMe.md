## Zephyr & ART-PI

### 编译
如果使用 west 工具构建，可先了解 west 工作区的概念，将本仓库按照如下结构放置
```
west-workspace/
│
├── zephyr-artpi/         # .git/    │
│   ├── CMakeLists.txt               │
│   ├── prj.conf                     │  never modified by west
│   ├── src/                         │
│   │   └── main.c                   │
│   └── west.yml         # main manifest with optional import(s) and override(s)
│                                    │
├── modules/
│   └── lib/
│       └── zcbor/       # .git/ project from either the main manifest or some import.
│
└── zephyr/              # .git/ project
    └── west.yml         # This can be partially imported with lower precedence or ignored.
                         # Only the 'manifest-rev' version can be imported.
```
west 命令如下(最终调用 cmake)：
```
west build -b stm32h750_art_pi zephyr-artpi/
```
## 烧录
west 命令如下：
```
west flash
```

>注意：默认在外部 spi flash xip 运行，因此需要提前烧录 boot 到片内 0x08000000 地址处，boot.bin 位于 boards/st/stm32h750_art_pi 目录下

## 调试
west 命令如下：
```
west debug
```