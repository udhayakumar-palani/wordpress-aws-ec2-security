# WordPress wp-config.php Hardening

## Hardening Constants

Add before "That's all, stop editing!" in wp-config.php:

```php
// Enforce HTTPS for all WordPress URLs
define('WP_HOME',    'https://[your-domain]');
define('WP_SITEURL', 'https://[your-domain]');

// Remove file editors from wp-admin
define('DISALLOW_FILE_EDIT', true);

// Force SSL for admin logins
define('FORCE_SSL_ADMIN', true);
```

## Effects

| Constant | Security Benefit |
|---|---|
| WP_HOME / WP_SITEURL | Forces HTTPS, prevents mixed content |
| DISALLOW_FILE_EDIT | Closes PHP injection via browser UI |
| FORCE_SSL_ADMIN | Protects admin credentials in transit |

## Location
```
/var/www/html/wp-config.php
```

## Verify
After setting DISALLOW_FILE_EDIT, confirm that Appearance > Theme Editor
and Plugins > Plugin Editor are ABSENT from the wp-admin menu.

## References
- https://developer.wordpress.org/advanced-administration/security/hardening/
- https://developer.wordpress.org/advanced-administration/wordpress/wp-config/
