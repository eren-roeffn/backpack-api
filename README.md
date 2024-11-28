# **watchdog** 

*A no-nonsense uptime monitor for people who get things done*

## What does it do?
Periodically checks your services and notifies you when they're down. No JavaScript, no animated charts, no nonsense.

## Installation
```bash
# Binary download (Linux)
wget -O watchdog https://watchdog-tools.org/dl/linux-amd64
chmod +x watchdog
sudo mv watchdog /usr/local/bin/

# Or build from source
go get github.com/miller/watchdog
```

## Usage
```bash
# Create monitoring config
cat > services.cfg
web=https://myapp.com timeout=5s
api=https://api.myapp.com/health timeout=3s
db=postgres://localhost:5432 timeout=2s

# Run checks every 30 seconds
watchdog -config services.cfg -interval 30s

# Send alerts to Slack
watchdog -config services.cfg -slack ${SLACK_WEBHOOK}
```

## Alert example
```
[WATCHDOG] Service DOWN
Service: web (https://myapp.com)
Status: Failed 3/3 checks
Last seen: 2024-01-15 14:32:10 UTC
Failed at: 2024-01-15 14:35:22 UTC
```

## Configuration options
```
-config string      Path to config file
-interval duration  Check interval (default 30s)
-timeout duration   Default timeout (default 5s)
-retries int        Consecutive failures before alert (default 3)
-silent             Don't log successful checks
```

## Why I built this
I tried 8 different monitoring tools. All were either too complex, too expensive, or required a PhD to configure. Sometimes you just need to know if your website is responding.

## License
Apache 2.0 - Use it in production, modify it, just don't sue me if it breaks.

*"It just works"*
