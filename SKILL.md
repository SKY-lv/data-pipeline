# Data Pipeline Agent Skill

> AI-powered ETL and data pipeline automation

## 功能

- **数据抽取** - 数据库/API/文件多源数据抽取
- **数据转换** - 清洗、映射、聚合、验证
- **数据加载** - 支持多种目标存储
- **管道编排** - DAG工作流、依赖管理
- **监控告警** - 数据质量监控、异常告警

## 使用场景

```
用户: 帮我建立一个从MySQL到Snowflake的每日同步管道
Agent: [调用data-pipeline skill配置ETL管道]
```

## 工具函数

### `create_pipeline(config)`

创建数据管道。

**参数:**
```python
{
    "name": "mysql_to_snowflake",
    "source": {
        "type": "mysql",
        "connection": "mysql://...",
        "tables": ["users", "orders"]
    },
    "transform": [
        {"type": "filter", "condition": "status = 'active'"},
        {"type": "map", "field": "created_at", "format": "iso"}
    ],
    "destination": {
        "type": "snowflake",
        "connection": "snowflake://...",
        "schema": "raw"
    },
    "schedule": "0 2 * * *"
}
```

### `run_pipeline(pipeline_id)`

执行管道。

### `monitor_pipeline(pipeline_id)`

监控状态。

### `validate_data(pipeline_id, rules)`

数据质量验证。

## 配置

```json
{
    "connectors": {
        "mysql": {"driver": "pymysql"},
        "postgres": {"driver": "psycopg2"},
        "snowflake": {"driver": "snowflake-connector"},
        "s3": {"driver": "boto3"}
    },
    "orchestrator": "prefect",
    "monitoring": {
        "slack_webhook": "${SLACK_WEBHOOK}",
        "email": "data-team@company.com"
    }
}
```

## 示例

```python
# 创建管道
pipeline = create_pipeline({
    "name": "daily_sync",
    "source": {"type": "mysql", "tables": ["users"]},
    "destination": {"type": "snowflake"},
    "schedule": "0 2 * * *"
})

# 运行
run_pipeline(pipeline['id'])
```

## 安装

```bash
clawhub install SKY-lv/data-pipeline
```

## License

MIT
