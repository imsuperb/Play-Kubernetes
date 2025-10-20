# playApp
_The most useful web app to play with Kubernetes!_

## Features ###
With playApp you can do the following:

📦 Get system information: `/sys` \
💲 Get environment variables: `/env` \
📝 Inspect HTTP request headers: `/headers` \
⏳ Simulate custom HTTP status and delay: `/response` \
💥 Simulate system failure: `/crash` \
🔄️ Experiment with deployment strategies: `/version` \
💬 Exercise logging strategies: `/log` \
⚙️ Experiment with Kubernetes probes: `/healthz` \
🗄️ Interact with SQL databases (MySQL, PostgreSQL, Oracle): `/sql` \
🍃 Interact with MongoDB: `/mongodb` \
💾 Inspect files in mounted volumes/configs: `/cat` \
📊 Simulate and scrape Prometheus metrics: `/metrics` \
🛡️ ToDo app simulator: `/tasks`

... and much more!

## Run in Docker
```bash
docker run --rm --name playApp -p 5000:5000 imsuperb/playApp:latest
```

## Run in Kubernetes
```bash
helm repo add imsuperb https://imsuperb.github.io/charts && helm repo update imsuperb
```
```bash
helm upgrade --install playApp imsuperb/playApp \
   --namespace playApp \
   --create-namespace
```
```bash
kubectl -n playApp port-forward svc/playApp 5000:5000
```
## Configuration
Default configuration [config.py](./config.py) can be overwritten using environment variables:

| Environment Variable | Default Value | Description |
|---------------------|---------------|-------------|
| `PLAYAPP_VERSION` | `v1.0.0` | Application version string. Useful for testing various deployment strategies. |
| `PLAYAPP_SECRET_KEY` | `secret` | Secret key for session management and security. |
| `PLAYAPP_DEBUG` | `false` | Enable debug mode. Set to `1`, `true`, `yes`, or `on` to enable. |
| `PLAYAPP_HOST` | `0.0.0.0` | Server host address to bind to. |
| `PLAYAPP_PORT` | `5000` | Server port number. |
| `PLAYAPP_DB_URL` | `sqlite:///playApp.db` | Database connection string. MySQL and PostgreSQL are tested and supported. Example: `postgresql://playApp:playApp@localhost:5432/playApp` |
| `PLAYAPP_DB_ECHO` | `false` | Enable SQLAlchemy query logging for debugging database operations. |
| `PLAYAPP_DB_OPTIONS` | `{}` | Additional SQLAlchemy engine options as a JSON string. Example: `'{"pool_timeout": 5,"connect_args": {"sslmode": "require"}}'` |
| `PLAYAPP_MONGO_URI` | `mongodb://localhost:27017` | MongoDB connection URI. |
| `PLAYAPP_MONGO_DB` | `playApp` | MongoDB database name. |
| `PLAYAPP_MONGO_COLLECTION` | `Requests` | MongoDB collection used by `/mongodb` endpoint. |
| `PLAYAPP_MONGO_SERVER_SELECTION_TIMEOUT_MS` | `500` | MongoDB server selection timeout in milliseconds. |
| `PLAYAPP_MONGO_CLIENT_OPTIONS` | `{}` | Additional MongoClient options as a JSON string. |
