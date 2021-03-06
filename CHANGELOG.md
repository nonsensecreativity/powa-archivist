## 3.1.1 (2017-09-19)

  - Bugfix:
    - Fix unsafe coding with sighup handler (Andreas Seltenreich, Julien
      Rouhaud)
    - Make sure we wait at least powa.frequency between two snapshot (Marc Cousin
      and Julien Rouhaud)
    - Fix win32 portability of compute_powa_frequeny() (Julien Rouhaud)
    - Don't try to read dbentry->tables if it's NULL (Julien Rouhaud)
    - Fix compilation for platform with HAVE_CLOCK_GETTIME (Julien Rouhaud,
      reported by Maxence Ahlouche)
  - Miscellaneous:
    - Add pg10 Compatibility (Julien Rouhaud)
    - Only execute once the powa_stat functions (Julien Rouhaud)

## 3.1.0 (2016-07-29)

  - Fix issue leading to impossibility to stop the worker without shutting down
    the database
  - Fix cluster wide statistics to get fresh values
  - Report PoWA collector activity in pg_stat_activity and process title
  - add a new powa.debug parameter
  - Purge at the same frequency as we coalesce. We just don't do both at the same iteration
  - Fix bloat issue
  - Add + and / operators on powa types to get delta and counters per second
    given two records

## 3.0.1 (2016-02-09)

  - Don't track 2PC related statements, as they're not normalized by
    pg_stat_statements. Upgrade script will do all the needed cleanup.
  - Restore the install_all.sql file to easily setup PoWA.
  - Maintain a cache of pg_database to allow seeing dropped database in the UI.
    See issue https://github.com/powa-team/powa/issues/63
  - Don't try to load PoWA if it's not in shared_preload_libraries

## 3.0.0 (2015-11-06)

Please not that there is not upgrade to switch to this version. You need to
remove the old one and install the new 3.0.0 version.

  - Handle pg_qualtats 0.0.7
  - Sample cluster wide statistics, for relations and functions
  - Fix the powa reset function, and rename it to powa_reset()
  - Add min/max records to improve performance when analyzing big time interval
  - Allow disabling some statistics sampling
  - Handle pg_track_settings extension
  - Add a GUC to ignore some users activity in sampled data

## 2.0.1 (2015-07-27)

  - Handle creation/suppression of supported extensions.
  - Remove the install_all script

## 2.0 (2015-02-06)

Major rework of the extension. PoWA 2 is now only compatible with PostgreSQL
version 9.4 and above. PoWA 2 is also now compatible with external extensions,
such as [pg_qualstats](https://github.com/powa-team/pg_qualstats) or
[pg_stat_kcache](https://github.com/powa-team/pg_stat_kcache). Third-part
extensions can also now be implemented easily.

The UI is also now in a [new repository](https://github.com/powa-team/powa-web),
with more frequent release cycle.

## 1.2.1 (2015-01-16)

No changes in core.

New features and changes in UI :
  - UI is now compatible with mojolicious 5.0 and more
  - UI can now connect to multiple servers, and credentials can be specified for each server
  - Use ISO 8601 timestamp format
  - Add POWA_CONFIG_FILE variable to specify config file location
  - Better charts display on small screens

When upgrading from 1.2:
  - No change on the extension
  - the format of the database section of the powa.conf has changed, to allow multiple servers specification. Please read INSTALL.md for more details about it.

## 1.2 (2014-10-27)

News features and fixes in core :
  - Display more metrics : temporary data, I/O time, average runtime
  - Fix timestamp for snapshots
  - DEALLOCATE and BEGIN statements are now ignored
  - PoWA history tables are now marked as "to be dumped" by pg_dump
  - Improve performance for "per database aggregated stats"

News features and changes in UI :
  - Follow the selected time interval between each page
  - Add a title to each page
  - Display metrics for each query page
  - Move database selector as a menu entry
  - Display human readable metrics
  - Fix empty graph bug

When upgrading from older versions :
  - Upgrade the core with ALTER EXTENSION powa UPDATE.
  - The format of the database section of the powa.conf has changed. The new format is :

     "dbname"   : "powa",
     "host"     : "127.0.0.1",
     "port"     : "5432",

 (instead of one line containing the dbi:Pg connection info)


## 1.1 (2014-08-18)

**POWA is now production ready**

Features:

  - Various UI improvments
  - More documentation
  - New demo mode
  - Plugin support
  - The code is now under the PostgreSQL license
  - New website
  - New logo

Bug fixes:

  - Use a temporary table for unpacked records to avoid unnecessary bloat


## 1.0 (2014-06-13)

**Hello World ! This is the first public release of POWA**

Features:

  - Web UI based on Mojolicious
  - Graph and dynamic charts
  - Packed the code as an extension
  - PL functions

