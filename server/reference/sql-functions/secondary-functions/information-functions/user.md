# USER

## Syntax

```
USER()
```

## Description

Returns the current MariaDB user name and host name, given when authenticating to MariaDB, as a string in the utf8 [character set](../../../data-types/string-data-types/character-sets/).

Note that the value of USER() may differ from the value of [CURRENT\_USER()](current_user.md), which is the user used to authenticate the current client. [CURRENT\_ROLE()](current_role.md) returns the current active role.

`SYSTEM_USER()` and, prior to [MariaDB 11.7](https://app.gitbook.com/s/aEnK0ZXmUbJzqQrTjFyb/mariadb-community-server-release-notes/old-releases/mariadb-11-7-rolling-releases/what-is-mariadb-117), [SESSION\_USER](session_user.md), are synonyms for `USER()`.

Statements using the `USER()` function or one of its synonyms are not [safe for statement level replication](../../../../ha-and-performance/standard-replication/unsafe-statements-for-statement-based-replication.md).

## Examples

```
shell> mysql --user="anonymous"

SELECT USER(),CURRENT_USER();
+---------------------+----------------+
| USER()              | CURRENT_USER() |
+---------------------+----------------+
| anonymous@localhost | @localhost     |
+---------------------+----------------+
```

To select only the IP address, use [SUBSTRING\_INDEX()](../../string-functions/substring_index.md),

```
SELECT SUBSTRING_INDEX(USER(), '@', -1);
+----------------------------------+
| SUBSTRING_INDEX(USER(), '@', -1) |
+----------------------------------+
| 192.168.0.101                    |
+----------------------------------+
```

## See Also

* [CURRENT\_USER()](current_user.md)

<sub>_This page is licensed: GPLv2, originally from_</sub> [<sub>_fill\_help\_tables.sql_</sub>](https://github.com/MariaDB/server/blob/main/scripts/fill_help_tables.sql)

{% @marketo/form formId="4316" %}
