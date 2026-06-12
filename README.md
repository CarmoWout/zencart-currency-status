# Zen Cart Currency Status Toggle

Implements currency enable/disable (status) functionality for Zen Cart 1.5.7,
following the exact Zen4All Language Status addon pattern.

## Modified files

| File | Description |
|------|-------------|
| `carmo1109/currencies.php` | Admin UI: setstatus action, status column with red/green toggle, status checkbox in new/edit forms |
| `includes/classes/currencies.php` | Storefront: loads only active currencies (WHERE status=1), fallback to DEFAULT_CURRENCY if session currency disabled |
| `includes/functions/functions_general.php` | `zen_currency_exists()` filters on status=1 |
| `carmo1109/includes/languages/english/currencies.php` | EN labels: TABLE_HEADING_CURRENCY_STATUS, ERROR_DEFAULT_CURRENCY_DISABLE |
| `carmo1109/includes/languages/dutch/currencies.php` | NL labels: TABLE_HEADING_CURRENCY_STATUS, ERROR_DEFAULT_CURRENCY_DISABLE |

## Database

The `currencies` table needs a `status` column:

```sql
ALTER TABLE currencies ADD COLUMN status TINYINT(1) NOT NULL DEFAULT 1;
```

## Notes

- Follows Zen4All Language Status pattern from `languages.php`
- Admin listing shows ALL currencies including disabled (for easy toggling)
- Cron exchange rate updates apply to all currencies including disabled ones
- PHP 5.x compatible (uses `isset()` instead of `??` null coalescing)
- ⚠️ Default currency disable protection not yet implemented
