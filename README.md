#  Tynq Scheduler

**distributed cron manager with failover support**

![Go](https://img.shields.io/badge/go-1.22-blue)
![PostgreSQL](https://img.shields.io/badge/db-postgres-informational)
![Redis](https://img.shields.io/badge/queue-redis-red)

## run via docker

```bash
docker run -d -p 9000:9000 \
  -e POSTGRES_URL=postgresql://... \
  -e REDIS_URL=redis://... \
  tynq/tynq-scheduler:latest
```

open dashboard → [localhost:9000](http://localhost:9000)

## create job

```bash
curl -X POST http://localhost:9000/api/jobs \
  -H "Content-Type: application/json" \
  -d '{
    "name": "cleanup-temp",
    "schedule": "0 */6 * * *",
    "command": "bash /scripts/clean.sh",
    "retries": 2
  }'
```

## architecture

```
┌──────────┐     ┌──────────┐
│ worker 1 │───▶ │ worker 2 │───▶ Redis
└──────────┘     └──────────┘
       │                │
       └─────▶ PostgreSQL (state)
```

## highlights

* cluster aware (raft-based)
* job chaining & dependencies
* prometheus metrics `/metrics`
* REST API + web dashboard

docs → [tynq.dev/docs](https://tynq.dev/docs)
community → [discord.gg/tynq](https://discord.gg/tynq)

Apache-2.0 © 2025 [tynq.dev](https://tynq.dev)

# Touch update: 1760682797

# Touch update: 1760682797
