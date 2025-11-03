# Laravel, Artisan and Tinker

## Command list

```bash

    #  To clear all caches and re-optimizing artisan local server
    php artisan optimize:clear && php artisan optimize && php artisan serve --host=localhost --port=8000
    # 01:07 pm

    date +"%I:%M %p"
    # 01:07 PM

    #  To clear all caches and re-optimizing artisan local server
    php artisan optimize:clear && php artisan optimize && php artisan serve --host=localhost --port=8000


    # 5. Update Laravel on Production Server
    php artisan migrate --force
    php artisan config:clear
    php artisan cache:clear
    php artisan optimize

    php artisan optimize:clear && php artisan optimize  # Production Server | For better performance



    ## Code Quality

    # Laravel Pint (code formatter)
    ./vendor/bin/pint

    # Clear caches
    php artisan cache:clear
    php artisan config:clear
    php artisan route:clear
    php artisan view:clear

    # Optimize for production
    php artisan config:cache
    php artisan route:cache
    php artisan view:cache
```

Using Laravel Schema Builder

```php
    // Get just column names  ✅ ✅ ✅
    Schema::getColumnListing('investor_applications');

    // Get detailed column information
    Schema::getConnection()->getDoctrineSchemaManager()->listTableColumns('investor_applications');

```

Using DB Facade

```php
    // Get column names with types
    DB::getSchemaBuilder()->getColumnListing('investor_applications');

    // More detailed information ✅ ✅ ✅
    DB::select('DESCRIBE investor_applications');
    DB::select('DESCRIBE password_reset_tokens');
```

Raw SQL Queries

```php
    // MySQL
    DB::select('SHOW COLUMNS FROM investor_applications');

    // PostgreSQL
    DB::select('SELECT column_name FROM information_schema.columns WHERE table_name = ?', ['investor_applications']);

    // SQLite
    DB::select('PRAGMA table_info(investor_applications)');
```

Most Practical Approach in Tinker

```php
    // Simple column names
    $columns = Schema::getColumnListing('investor_applications');
    print_r($columns);

    // With detailed info ✅ ✅ ✅
    $detailed = DB::select('DESCRIBE investor_applications');
    print_r($detailed);
```

## For Better Readability

```php
    // Format the output nicely
    collect(Schema::getColumnListing('investor_applications'))
    ->each(fn($column) => echo $column . PHP_EOL);

    // Or with numbering
    collect(Schema::getColumnListing('investor_applications'))->each(fn($column, $index) => echo ($index + 1) . '. ' . $column . PHP_EOL);
```

## Createing Middleware -

```bash
    # Audit System Middleware

    php artisan make:middleware AuditMiddleware
    #   INFO  Middleware [app/Http/Middleware/AuditMiddleware.php] created successfully.

    php artisan make:middleware AdminActionLogger
    #   INFO  Middleware [app/Http/Middleware/AdminActionLogger.php] created successfully.
```

## Testing Commands - Activity Logging System

```bash
    php artisan tinker

    # Test user creation logging
    User::create(['name' => 'Test', 'email' => 'test@example.com', 'password' => bcrypt('password')]);

    ActivityLog::latest()->first();

    # Test helper function
    logActivity('test.event', 'Testing activity log');
    ActivityLog::latest()->first();


    # Clear route cache to apply middleware changes
    php artisan route:clear

    # Clear config cache
    php artisan config:clear

    # Test that the application loads without errors
    php artisan route:list --columns=uri,name,middleware | grep -E "admin|reviewer|investor|project"

    # Combo
    php artisan down && git pull origin main && php artisan cache:clear && php artisan config:clear && php artisan route:clear && php artisan view:clear && php artisan config:cache && php artisan route:cache && php artisan view:cache && php artisan storage:migrate-investor-files --force && php artisan up



    invest-hub]$     php artisan down && git pull origin main && php artisan cache:clear && php artisan config:clear && php artisan route:clear && php artisan view:clear && php artisan config:cache && php artisan route:cache && php artisan view:cache && php artisan storage:migrate-investor-files --force && php artisan up

   INFO  Application is now in maintenance mode.

From github.com:M-Bukhari/abam-investment-hub
 * branch            main       -> FETCH_HEAD
Already up to date.

   INFO  Application cache cleared successfully.


   INFO  Configuration cache cleared successfully.


   INFO  Route cache cleared successfully.


   INFO  Compiled views cleared successfully.


   INFO  Configuration cached successfully.


   INFO  Routes cached successfully.



   INFO  Blade templates cached successfully.

Investor Files Migration Tool
============================

Found 20 investor directories to migrate.

 20/20 [▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓] 100%

Migration Summary
=================
+-------------------+-------+
| Metric            | Count |
+-------------------+-------+
| Total Directories | 20    |
| Total Files Found | 202   |
| Files Migrated    | 202   |
| Errors            | 0     |
+-------------------+-------+

✓ Migration completed successfully!
All investor files are now stored privately and require authentication to access.

   INFO  Application is now live.


    # Combo
    php artisan down && git pull origin main && php artisan cache:clear && php artisan config:clear && php artisan route:clear && php artisan view:clear && php artisan config:cache && php artisan route:cache && php artisan view:cache && php artisan storage:migrate-investor-files --force && php artisan up

```

Queries

```php

```
