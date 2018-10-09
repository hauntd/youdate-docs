### Upgrade

YouDate upgrade process is simple:
  
1. Replace the `application` folder with the new `application` folder (don't forget: `application/runtime` must be writable).
2. Replace the `content/themes/youdate` directory with the new `content/themes/youdate` directory.

Then open your website or visit administration area. Application will install database structure updates (if any) and notify you in administration area.

#### Upgrade to 1.2+

You need to add an additional cron command to run queued jobs.
 
See [Cron commands](./cron.md) for more information.
