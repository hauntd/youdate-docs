### Upgrade

YouDate upgrade process is simple:
  
1. Replace the `application` folder with the new `application` folder (don't forget: `application/runtime` must be writable).
2. Replace the `content/themes/youdate` directory with the new `content/themes/youdate` directory.
3. All new YouDate releases come with an updated translations file (`Source/translations-1.9.json`. You may want to import it, but keep in mind that it will overwrite any changes that you've made to existing translations (supported languages only).

Then open your website or visit administration area. Application will install database structure updates (if any) and notify you in administration area.

#### Upgrade to 1.9

1. Follow the upgrade procedure described above. Then you need to import additional SQL dump files (phpMyAdmin, HeidiSQL, Sequel Pro or any other, that support SQL import).
Files to import: 
    * `Source/countries.sql`
    * `Source/geodata.sql`
2. Add this line to your `.env` config file:

```
APP_GEODATA_SOURCE = mysql
```

#### Upgrade to 1.2+

You need to add an additional cron command to run queued jobs.
 
See [Cron commands](./cron.md) for more information.
