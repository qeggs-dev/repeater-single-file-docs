# Auto Backup

[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-blue.svg?logo=python)](https://www.python.org/downloads/) [![License: MIT](https://img.shields.io/badge/License-MIT-63b9ff.svg)](https://opensource.org/licenses/MIT)

一个简单的目录自动备份小程序，支持定时任务、多格式压缩的配置管理。

## 功能特性

- 🔄 **定时备份** - 基于Cron表达式的配置备份频率
- 📦 **多格式压缩** - 支持ZIP、TAR、GZ等多种压缩格式
- 📁 **目录结构保留** - 备份时完整保留原始目录结构
- 📝 **日志管理** - 支持日志轮转、压缩和分级输出
- ⚙️ **配置驱动** - 使用JSON文件配置所有参数
- 🚀 **异步调度** - 基于APScheduler的异步任务调度
- 📊 **进度显示** - 实时显示文件压缩进度

## 安装

### 环境要求
- Python 3.11+
- pip包管理器

### 安装步骤

1. 克隆仓库
```bash
git clone https://github.com/qeggs-dev/auto-backup.git
cd auto-backup
```

2. 下载启动器
```bash
git clone https://github.com/qeggs-dev/Sloves_Starter.git
copy Sloves_Starter/Sloves_Starter.py auto-backup/run.py
```

## 快速开始

### 1. 创建配置文件

在`./configs`目录下创建JSON配置文件，例如`backup_config.json`：

```json
{
    "logger": {
        "level": "INFO",
        "file": "./logs/{time:YYYY-MM-DD-HH-MM-SS}.log",
        "rotation": "1 day",
        "retention": "7 days",
        "compression": "tar.gz"
    },
    "tasks": [
        {
            "name": "daily_backup",
            "src": "./data",
            "dst": "./backups",
            "glob": "**/*",
            "time_format": "%Y-%m-%d-%H-%M-%S",
            "suffix": ".zip",
            "compression": "deflated",
            "cron": {
                "hour": "2",
                "minute": "0"
            }
        }
    ],
    "idle_wait": 10
}
```

### 2. 运行程序

```bash
python run.py
```

程序会自动扫描`./configs`目录下的JSON配置文件。如果有多个配置文件，会提示选择使用哪一个。

## 配置说明

### 日志配置 (LoggerConfig)

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| level | string | "INFO" | 日志级别：TRACE/DEBUG/INFO/SUCCESS/WARNING/ERROR/CRITICAL |
| file | string | "./logs/..." | 日志文件路径，支持{time}变量 |
| enqueue | boolean | true | 是否启用异步日志队列 |
| rotation | string | "1 day" | 日志轮转间隔 |
| retention | string | "7 days" | 日志保留时间 |
| encoding | string | "utf-8" | 日志文件编码 |
| compression | string | "tar.gz" | 日志压缩格式 |

### 任务配置 (TaskConfig)

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| name | string | "" | 任务名称 |
| src | string | "./monitor" | 要备份的源目录 |
| dst | string | "./backups" | 备份文件存放目录 |
| glob | string | "*" | 文件匹配模式 |
| time_format | string | "%Y-%m-%d-%H-%M-%S" | 备份文件时间格式 |
| suffix | string | ".zip" | 备份文件后缀 |
| compression | string | "deflated" | 压缩模式：stored/deflated/bzip2/lzma |
| cron | object | {} | Cron表达式配置 |

### Cron配置 (CronConfig)

支持标准的Cron表达式字段：
- year: 年
- month: 月
- day: 日
- week: 周
- day_of_week: 星期几
- hour: 小时
- minute: 分钟
- second: 秒
- start_date: 开始日期
- end_date: 结束日期
- timezone: 时区
- jitter: 随机偏移量(秒)

## 项目结构

```
auto-backup/
├── auto_backup.py              # 主程序入口
├── auto_backup_core/            # 核心模块
│   ├── __init__.py
│   ├── auto_backup.py           # 备份执行类
│   ├── config_models/           # 配置模型
│   │   ├── __init__.py
│   │   ├── config_model.py      # 主配置模型
│   │   ├── logger_configs.py    # 日志配置
│   │   └── task_configs.py      # 任务配置
│   ├── init_logger.py           # 日志初始化
│   └── main.py                  # 核心调度器
└── configs/                     # 配置文件目录
    └── *.json                   # JSON配置文件
```

## 许可证

[MIT License](./LICENSE)