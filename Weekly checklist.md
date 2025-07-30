### 📦 Weekly Checklist

| Task                                                               | Server  | Status (✔ / ✖) | Notes                                  |
|--------------------------------------------------------------------|---------|----------------|----------------------------------------|
| Apply updates (`apt update && upgrade`)                            | All     |                |                                        |
| Clean up unused packages (`apt autoremove`)                        | All     |                |                                        |
| Review failed login attempts                                       | All     |                |                                        |
| Check cron job logs (`/var/log/syslog` or `journalctl`)           | All     |                |                                        |
| Backup `/var/www/html` (`tar` or `rsync`)                         | Web     |                |                                        |
| Backup MySQL database (`mysqldump`)                               | DB      |                |                                        |
| Copy backups to remote or S3 (if applicable)                      | Backup  |                |                                        |
| Check firewall rules (UFW)                                        | All     |                |                                        |
| SSL expiration check (`openssl s_client` or browser)              | Web     |                |                                        |
| Report or summarize weekly server health                          | All     |                |                                        |
