# Linux Server Commands Reference

## Service Management
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl status nginx
sudo systemctl enable nginx

## Log Analysis
sudo journalctl -u nginx --since "5 minutes ago"
sudo tail -f /var/log/nginx/error.log
sudo tail -f /var/log/nginx/access.log

## Port Management
sudo ss -tlnp | grep :80
sudo lsof -i :80
sudo netstat -tlnp | grep :80

## Permission Management
ls -la /var/www/myapp/
chmod 644 filename
chmod 755 directory
chown -R user:group /path

## Process Management
ps aux | grep nginx
top -bn1
kill -9 PID

## Nginx Configuration
sudo nginx -t
sudo nginx -s reload
cat /etc/nginx/sites-available/myapp
ls /etc/nginx/sites-enabled/
