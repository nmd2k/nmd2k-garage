# Nextcloud

Run the docker compose and follow the instruction.

## Backup
Setup backup using borg: https://borgbackup.readthedocs.io/en/stable/usage/general.html#repository-urls

The AIO setup have a backup option itself.

## Notes:

Proxy nginx configuration, add this line:
```
client_body_buffer_size 512k;
proxy_read_timeout 86400s;
client_max_body_size 0;
```

