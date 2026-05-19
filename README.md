# n8n Deployment

n8n workflow automation for Studio Mahoney.

## Architecture

- **Host:** ww-node (100.125.75.128)
- **Port:** 5678
- **Public URL:** https://n8n.secure-svr.net
- **Proxy:** nginx on secure-svr.net

## Deployment

```bash
cd ~/Documents/GitHub/n8n/deploy/compose
docker compose up -d
```

## Updating

```bash
cd ~/Documents/GitHub/n8n/deploy/compose
docker compose pull
docker compose up -d
```

## Backup

n8n data is stored in the `n8n_data` Docker volume.

Backup:
```bash
docker run --rm -v n8n_data:/data:ro -v ~/backups/n8n:/backup alpine \
  tar czf /backup/n8n-data-$(date +%Y%m%d-%H%M%S).tar.gz -C /data .
```

Restore:
```bash
docker run --rm -v n8n_data:/data -v ~/backups/n8n:/backup alpine \
  tar xzf /backup/n8n-data-YYYYMMDD-HHMMSS.tar.gz -C /data
```

## Configuration

- Timezone: America/Chicago
- Protocol: HTTPS
- Webhook base: https://n8n.secure-svr.net/

## Related

- **Jira:** SM-20
- **nginx vhost:** `/root/secure-svr.net/nginx/sites-available/n8n.conf` (on secure-svr)
- **Memory:** memory/2026-05-19.md
