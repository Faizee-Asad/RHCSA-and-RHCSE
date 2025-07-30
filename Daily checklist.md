### 📅 Daily Checklist

| Task                                                              | Server | Status (✔ / ✖) | Notes / Issues Found                  |
|-------------------------------------------------------------------|--------|----------------|---------------------------------------|
| Check server uptime (`uptime`)                                    | All    |                |                                       |
| Check CPU & RAM usage (`top`, `free -m`)                          | All    |                |                                       |
| Check disk usage (`df -h`)                                        | All    |                |                                       |
| Check Apache/Nginx status (`systemctl status apache2`)           | Web    |                |                                       |
| Check MySQL status (`systemctl status mysql`)                    | DB     |                |                                       |
| Review system logs (`/var/log/syslog`, `auth.log`)               | All    |                |                                       |
| Ping test site/app or use `curl localhost`                       | Web    |                |                                       |
| Confirm no service failure overnight                             | All    |                |                                       |
| Note any login failures (`grep 'Failed' /var/log/auth.log`)      | All    |                |                                       |
| Escalate or fix minor issues (restarts, cleanup)                 | As needed |             |                                       |
