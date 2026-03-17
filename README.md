# Linux Server Setup & Troubleshooting

## Overview
Hands-on Linux server project — Ubuntu 24.04 + Nginx.
Deployed custom web application and resolved real-world server issues.

## Environment
- OS: Ubuntu 24.04 LTS (WSL2)
- Web Server: Nginx 1.24.0
- Tools: systemctl, journalctl, ss, lsof, chmod, ps, top

## What Was Built
- Configured Nginx virtual host serving custom HTML application
- Set correct file permissions and directory ownership
- Validated configuration before deployment

## Troubleshooting Scenarios Practiced

### Scenario 1 — Service Failure
- Simulated: sudo systemctl stop nginx
- Symptom: curl connection refused
- Investigation: systemctl status + journalctl
- Resolution: systemctl start nginx
- Learning: Always check service logs before assuming hardware failure

### Scenario 2 — Port Conflict
- Simulated: Second service attempting to bind port 80
- Symptom: OSError Errno 98 Address already in use
- Investigation: ss -tlnp + lsof -i :80
- Resolution: Identified owner process — Nginx holding port correctly
- Learning: lsof -i = fastest way to identify port ownership

### Scenario 3 — Permission Denied
- Simulated: chmod 000 on index.html
- Symptom: 403 Forbidden in browser
- Investigation: ls -la + tail /var/log/nginx/error.log
- Resolution: chmod 644 index.html
- Learning: Web files need 644, directories need 755

## Key Commands Reference
- systemctl start/stop/status/reload nginx
- journalctl -u nginx --since "5 minutes ago"
- sudo ss -tlnp | grep :80
- sudo lsof -i :80
- chmod 644 file / chmod 755 directory
- ps aux | grep nginx
- tail -f /var/log/nginx/error.log

## Skills Demonstrated
- Linux service management
- Web server configuration
- Permission management
- Log analysis
- Process monitoring
- Incident identification and resolution
