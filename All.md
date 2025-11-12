## Troubleshooting Commands

### Issue: "File not found" errors

```bash
# Check if files exist in private storage
ls -la storage/app/private/uploads/investors/

# Check if files still in public storage
ls -la storage/app/public/uploads/investors/

# Re-run migration
php artisan storage:migrate-investor-files --force

# Check file permissions
ls -la storage/app/private/uploads/investors/9/
```

### Issue: Permission denied errors

```bash
# Fix storage permissions
chmod -R 775 storage/
chown -R www-data:www-data storage/

# For nginx
chown -R nginx:nginx storage/

# Check current permissions
ls -la storage/app/private/
```

### Issue: 403 Forbidden for authorized users

```bash
# Clear all caches
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Rebuild caches
php artisan config:cache
php artisan route:cache

# Verify routes
php artisan route:list --name=file.download

# Check logs for authorization errors
grep "403" storage/logs/laravel.log | tail -n 20
```

### Issue: Routes not found

```bash
# Clear route cache
php artisan route:clear

# Rebuild route cache
php artisan route:cache

# Verify routes exist
php artisan route:list | grep downloadFile

# Check for syntax errors
php artisan route:list | grep ERROR
```

---

## Performance Monitoring

```bash
# Check disk usage
df -h
du -sh storage/app/private/uploads/investors/
du -sh storage/app/public/uploads/investors/

# Monitor PHP processes
ps aux | grep php-fpm
top -bn1 | grep php

# Check memory usage
free -h

# Monitor response times (requires curl)
time curl -I -H "Cookie: laravel_session=your_session" http://your-domain.com/admin/investors/9/files/file.pdf
```

---

## Cleanup Commands (After Verification)

**⚠️ Only run after 24-48 hours of successful operation**

```bash
# Verify all files migrated successfully
diff -r storage/app/public/uploads/investors/ storage/app/private/uploads/investors/

# Remove empty directories from public storage
find storage/app/public/uploads/investors/ -type d -empty -delete

# Remove old public investor files (CAREFUL!)
# Backup first!
tar -czf ~/old_public_files_$(date +%Y%m%d).tar.gz storage/app/public/uploads/investors/
rm -rf storage/app/public/uploads/investors/

# Verify public storage cleaned
ls -la storage/app/public/uploads/
```

---

## Environment-Specific Commands

### Development/Local:

```bash
php artisan serve --host=0.0.0.0 --port=8000
php artisan storage:migrate-investor-files --dry-run
tail -f storage/logs/laravel.log
```

### Staging:

```bash
git pull origin staging
php artisan migrate --force
php artisan storage:migrate-investor-files --dry-run
php artisan config:cache
```

### Production:

```bash
php artisan down
git pull origin main
php artisan migrate --force
php artisan storage:migrate-investor-files --force
php artisan config:cache
php artisan route:cache
php artisan up
```

---

## Quick Reference Table
