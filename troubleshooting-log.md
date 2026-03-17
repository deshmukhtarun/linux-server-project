# Troubleshooting Log

## Scenario 1 — Service Failure
**Date:** 17/03/2026
**Problem:** Nginx service stopped — connection refused
**Commands Used:**
- sudo systemctl stop nginx (simulated crash)
- curl http://localhost (confirmed: connection refused)
- sudo systemctl status nginx (confirmed: inactive/dead)
- sudo journalctl -u nginx --since "5 minutes ago" (checked logs)
- sudo systemctl start nginx (resolved)
**Root Cause:** Service stopped — not running
**Resolution:** Restart service using systemctl
**Learning:** Always check systemctl status first before investigating further

---

## Scenario 2 — Port Conflict
**Date:** 17/03/2026
**Problem:** Second service failed to bind port 80
**Commands Used:**
- sudo python3 -m http.server 80 (simulated conflict)
- Error: OSError Errno 98 Address already in use
- sudo ss -tlnp | grep :80 (identified port usage)
- sudo lsof -i :80 (identified owner process)
**Root Cause:** Nginx already holding port 80
**Resolution:** Identified correct owner — no action needed
**Learning:** lsof -i :PORT is fastest way to identify port ownership

---

## Scenario 3 — Permission Denied
**Date:** 17/03/2026
**Problem:** 403 Forbidden on web application
**Commands Used:**
- sudo chmod 000 /var/www/myapp/index.html (simulated)
- curl http://localhost (confirmed: 403 Forbidden)
- ls -la /var/www/myapp/index.html (confirmed: ---------- permissions)
- sudo tail -5 /var/log/nginx/error.log (confirmed: Permission denied)
- sudo chmod 644 /var/www/myapp/index.html (resolved)
**Root Cause:** File permissions set to 000 — no read access
**Resolution:** chmod 644 restores correct web file permissions
**Learning:** Web files = 644, directories = 755, always check error.log first
