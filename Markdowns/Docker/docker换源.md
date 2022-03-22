# docker换源.md

右键单击桌面右下角docker的图标 → Settings

    Docker Engine → 在"registry-mirrors"那一栏填入https://registry.docker-cn.com→apply and restart


json

```json
   {
        "registry-mirrors": [
            "https://registry.docker-cn.com",
            "http://hub-mirror.c.163.com",
            "https://kfwkfulq.mirror.aliyuncs.com"
        ],
            "builder": {
            "gc": {
                "defaultKeepStorage": "20GB",
                "enabled": true
            }
        },
        "experimental": false,
        "features": {
            "buildkit": true
        }
    }
```