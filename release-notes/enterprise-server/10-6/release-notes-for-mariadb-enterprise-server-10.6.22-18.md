# Release Notes for MariaDB Enterprise Server 10.6.22-18

MariaDB Enterprise Server 10.6.22-18 is a maintenance release of [MariaDB Enterprise Server](https://app.gitbook.com/o/diTpXxF5WsbHqTReoBsS/s/SsmexDFPv2xG2OTyO5yV/) 10.6. This release includes a variety of fixes.

MariaDB Enterprise Server 10.6.22-18 was released on 11 Jun 2025.

## Fixed Security Vulnerabilities <a href="#fixed-security-vulnerabilities" id="fixed-security-vulnerabilities"></a>

| **CVE (with** [**cve.org**](https://cve.org/) **link)**                        | **CVSS base score** |
| ------------------------------------------------------------------------------ | ------------------- |
| [CVE-2025-30693](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2025-30693) | 5.5                 |
| [CVE-2023-52969](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-52969) | 4.9                 |
| [CVE-2023-52970](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-52970) | 4.9                 |

## Changes in Storage Engines <a href="#changes-in-storage-engines" id="changes-in-storage-engines"></a>

* This release incorporates MariaDB ColumnStore engine version 23.10.4.

## Notable changes <a href="#notable-changes" id="notable-changes"></a>

* New user variable, analyze\_max\_length, default value 4G. Any field that is bigger than this value in bytes will be ignored by ANALYZE TABLE PERSISTENT to not collect statistics for long char/varchars unless it is specified in FOR COLUMNS(). (MENT-2301)
* SBOM now includes 'license' and 'copyright' information, improving security compliance and dependency tracking. (MENT-2311)
* MariaDB effectively running as root CAP\_DAC\_OVERRIDE ([MDEV-36229](https://jira.mariadb.org/browse/MDEV-36229))
* my\_getopt compares option names case sensitively ([MDEV-27126](https://jira.mariadb.org/browse/MDEV-27126))
* [Galera](https://app.gitbook.com/o/diTpXxF5WsbHqTReoBsS/s/3VYeeVGUV4AMqrA3zwy7/) updated to 26.4.22
* Support has been added for Oracle Linux 8 and 9

## Issues Fixed <a href="#issues-fixed" id="issues-fixed"></a>

### Can result in data loss <a href="#can-result-in-data-loss" id="can-result-in-data-loss"></a>

* Assertion InnoDB searching row in wrong partition for multiple system versioned DELETE with same timestamp and same multistatement transaction ([MDEV-36115](https://jira.mariadb.org/browse/MDEV-36115))

### Can result in hang or crash <a href="#can-result-in-hang-or-crash" id="can-result-in-hang-or-crash"></a>

* Incorrect error handling on DDL with FULLTEXT INDEX ([MDEV-36061](https://jira.mariadb.org/browse/MDEV-36061))
* ALTER TABLE…SEQUENCE does not work correctly with InnoDB ([MDEV-36038](https://jira.mariadb.org/browse/MDEV-36038))
* Race conditions between ALTER TABLE or OPTIMIZE TABLE and the purge of transaction history were fixed. ([MDEV-36122](https://jira.mariadb.org/browse/MDEV-36122))
* Server aborts while deleting the record in spatial index ([MDEV-35420](https://jira.mariadb.org/browse/MDEV-35420))
* The server could crash when an UPDATE is about to commit concurrently with a CREATE INDEX that includes VIRTUAL columns ([MDEV-36281](https://jira.mariadb.org/browse/MDEV-36281))
* Upgrades fail on Windows ([MDEV-36128](https://jira.mariadb.org/browse/MDEV-36128))
* ASAN errors in dict\_sys\_t::load\_table / get\_foreign\_key\_info after failing to load a table ([MDEV-33167](https://jira.mariadb.org/browse/MDEV-33167))
* ALTER TABLE…DROP COLUMN after a failed ALTER TABLE…DROP COLUMN could lead to a server crash ([MDEV-36236](https://jira.mariadb.org/browse/MDEV-36236))
* Field pointer may be uninitialized in fill\_record ([MDEV-36181](https://jira.mariadb.org/browse/MDEV-36181))
* A primary server could crash when a semi-sync connection is stopped, if the primary previously disabled semi-sync replication while the connection was already up (and \`rpl\_semi\_sync\_master\_wait\_no\_slave=0\`). ([MDEV-36359](https://jira.mariadb.org/browse/MDEV-36359))
* Incorrect undo logging for indexes on virtual columns whose index ID does not fit in 32 bits ([MDEV-36613](https://jira.mariadb.org/browse/MDEV-36613))
* With wsrep\_ignore\_apply\_errors = 0, the node crashes due to assertion thd->is\_error() failed in Sql\_cmd\_dml::prepare(), shown in the logs ([MDEV-35946](https://jira.mariadb.org/browse/MDEV-35946))
* In some cases, if there are MDL locks (for example, when LOCK TABLE is executed), a node could get stuck in the system thread due to incorrect handling of metadata locks (MDL) in server code when a transaction was BF aborted. ([MDEV-35941](https://jira.mariadb.org/browse/MDEV-35941))
* Regression after the fix for [MDEV-31413](https://jira.mariadb.org/browse/MDEV-31413) - sometimes the server crashes with an assertion in wsrep::transaction::before\_rollback(), for example when using OPTIMIZE TABLE on an ARIA table with wsrep\_osu\_method=RSU. ([MDEV-32631](https://jira.mariadb.org/browse/MDEV-32631))
* SST failure occurs when gtid\_strict\_mode is enabled under high load, such as OLTP load is active on the primary node. A typical symptom of this error is the presence of the diagnostic "\[ERROR] mariadbd: Error writing file 'binlog'", in the debug version it is also possible to crash on assertion in the wsrep::transaction::before\_rollback() function with the message "Assertion \`state() == s\_executing || state() == s\_preparing || state() == s\_prepared || state() == s\_must\_abort || state() == s\_aborting || state() == s\_cert\_failed || state() == s\_must\_replay' failed". ([MDEV-34891](https://jira.mariadb.org/browse/MDEV-34891))
* In Galera, creating sequence with a small cache leads to signal 6 error: \[ERROR] WSREP: FSM: no such a transition REPLICATING -> COMMITTED. ([MDEV-33850](https://jira.mariadb.org/browse/MDEV-33850))
* Under high load wsrep internal thread may terminate due to memory pressure conditions, but this is not a crash, however in debug version user may encounter assertion in wsrep\_to\_isolation\_begin() function with following message: "int wsrep\_to\_isolation\_begin(THD\*, const char\*, const char\*, const TABLE\_LIST\*, const Alter\_info\*, const key\_array\*, const HA\_CREATE\_INFO\*): Assertion \`(0)' failed." ([MDEV-36116](https://jira.mariadb.org/browse/MDEV-36116))
* Assertion \`commit\_trx' failed in innobase\_commit() (ha\_innodb.cc). An INSERT with sql\_log\_bin=0 is still replicated in Galera (per [MDEV-7205](https://jira.mariadb.org/browse/MDEV-7205)), despite binary logging being disabled. This results in a partial binlog bypass, requiring a two-phase commit (2PC). During 2PC, the INSERT is first prepared (entering the PREPARED state in InnoDB), and on commit, the new assertion from [MDEV-24035](https://jira.mariadb.org/browse/MDEV-24035) fails, causing a crash with "Assertion 'commit\_trx' failed" in logs. ([MDEV-35658](https://jira.mariadb.org/browse/MDEV-35658))
* When a sequence is used and inserts run in parallel on multiple Galera nodes, a transaction may be aborted after passing certification. If it then attempts to roll back, the binlog statement cache—which includes reserved sequence values—may be written prematurely. This causes a crash with the diagnostic "WSREP: FSM: no such a transition REPLICATING -> COMMITTED" in the logs, as the transaction is supposed to replay and only write to the binlog during the final commit. ([MDEV-33589](https://jira.mariadb.org/browse/MDEV-33589))
* A Galera node may hang due to improper mutex handling: a thread held lock\_sys.wait\_mutex while triggering a streaming replication rollback, which also tried to acquire THD::LOCK\_thd\_kill, leading to incorrect mutex usage. In debug versions, this leads to diagnostics like "safe\_mutex: Found wrong usage of mutex 'wait\_mutex' and 'LOCK\_thd\_data'", but in both debug and release versions, there is some probability that the node may hang. ([MDEV-36509](https://jira.mariadb.org/browse/MDEV-36509))
* corruption when query cache cannot allocate block ([MDEV-34075](https://jira.mariadb.org/browse/MDEV-34075))
* Stack looping and SIGSEGV in Item\_args::walk\_args on UPDATE ([MDEV-31647](https://jira.mariadb.org/browse/MDEV-31647))
* Server crash in find\_field\_in\_tables, Assertion \`name' failed in find\_field\_in\_table\_ref ([MDEV-25012](https://jira.mariadb.org/browse/MDEV-25012))
* Long server\_audit\_file\_path causes buffer overflow ([MDEV-36245](https://jira.mariadb.org/browse/MDEV-36245))
* Server crash when inserting from derived table containing insert target table ([MDEV-32086](https://jira.mariadb.org/browse/MDEV-32086))

### Can result in unexpected behaviour <a href="#can-result-in-unexpected-behaviour" id="can-result-in-unexpected-behaviour"></a>

* CREATE INDEX fails to heal a FOREIGN KEY constraint ([MDEV-35962](https://jira.mariadb.org/browse/MDEV-35962))
* Doublewrite recovery of innodb\_checksum\_algorithm=full\_crc32 page\_compressed pages does not work ([MDEV-36180](https://jira.mariadb.org/browse/MDEV-36180))
* Segfault on concurrent ALTER and SELECT for partitioned table ([MDEV-31122](https://jira.mariadb.org/browse/MDEV-31122))
* ST\_PointFromWKB ignores SRID argument and always creates the POINT with 0 for it's SRID ([MDEV-32619](https://jira.mariadb.org/browse/MDEV-32619))
* mariadb-dump used wrong quoting character ([MDEV-36268](https://jira.mariadb.org/browse/MDEV-36268))
* After a corrupted table on one node triggers the cluster to vote to evict a node that failed a transaction, the current master can’t commit any more and hangs. ([MDEV-34998](https://jira.mariadb.org/browse/MDEV-34998), MENT-2081)
* [MDEV-32157](https://jira.mariadb.org/browse/MDEV-32157) intended to fix spider wrapper so that it is case insensitive, among other things. However that fix was incomplete, as the udf spider\_direct\_sql may still require case sensitivity. [MDEV-35807](https://jira.mariadb.org/browse/MDEV-35807) fixes this. ([MDEV-35807](https://jira.mariadb.org/browse/MDEV-35807))
* Creating partitioned tables is disallowed when wsrep\_osu\_method=TOI and wsrep\_strict\_ddl=ON, preventing alteration or deletion of partitioned tables. ([MDEV-27861](https://jira.mariadb.org/browse/MDEV-27861))
* Attempting to create a CONNECT engine table results in "non-InnoDB sequences in Galera cluster" error message in logs due to an incorrect engine check. ([MDEV-35748](https://jira.mariadb.org/browse/MDEV-35748))
* innodb\_snapshot\_isolation=1 gives error for not committed row changes ([MDEV-36639](https://jira.mariadb.org/browse/MDEV-36639))
* Aria engine: log initialization failed (MENT-2235)
* MariaDB Backup returns with an error like "Error on file ./test/t1#P#p513.MYD open during \`test\`.\`t1\` table copy for partitioned MyISAM tables when running out of file handles (MENT-2089)
* User without any privileges to a sequence can read from it and modify it via column default ([MDEV-36413](https://jira.mariadb.org/browse/MDEV-36413))
* User has unauthorized access to a sequence through a view with security invoker ([MDEV-36380](https://jira.mariadb.org/browse/MDEV-36380))

### Unexpected results <a href="#unexpected-results" id="unexpected-results"></a>

* The untested ha\_spider::index\_first\_internal constructs broken queries ([MDEV-36324](https://jira.mariadb.org/browse/MDEV-36324))
* Wrong results from tables with a single record and an aggregate ([MDEV-35238](https://jira.mariadb.org/browse/MDEV-35238))
* Unexpected error 1264 'Out of Range Value for Column' when inserting into ... select ... from a spider table ([MDEV-35874](https://jira.mariadb.org/browse/MDEV-35874))
* group by handler missing constant fields when selecting from a view ([MDEV-36307](https://jira.mariadb.org/browse/MDEV-36307))
* Tests calling the udf spider\_copy\_tables fail with --view-protocol ([MDEV-36335](https://jira.mariadb.org/browse/MDEV-36335))

### Related to performance <a href="#related-to-performance" id="related-to-performance"></a>

* dict\_stats\_fetch\_from\_ps() unnecessarily holds exclusive dict\_sys.latch ([MDEV-35436](https://jira.mariadb.org/browse/MDEV-35436))
* Stall and crash when page cleaner fails to generate free pages during Async flush ([MDEV-36226](https://jira.mariadb.org/browse/MDEV-36226))

## Changelog <a href="#changelog" id="changelog"></a>

For the complete list of changes in this release, see the [changelog](changelog-for-mariadb-enterprise-server-10.6.22-18.md).

## Platforms <a href="#platforms" id="platforms"></a>

In alignment to the [enterprise lifecycle](../enterprise-server-lifecycle.md), MariaDB Enterprise Server 10.6.22-18 is provided for:

* AlmaLinux 8 (x86\_64, ARM64)
* AlmaLinux 9 (x86\_64, ARM64)
* Debian 11 (x86\_64, ARM64)
* Debian 12 (x86\_64, ARM64)
* Microsoft Windows (x86\_64) (MariaDB Enterprise Cluster excluded)
* Oracle Linux 8 (x86\_64, ARM64)
* Oracle Linux 9 (x86\_64, ARM64)
* Red Hat Enterprise Linux 8 (x86\_64, ARM64)
* Red Hat Enterprise Linux 9 (x86\_64, ARM64, PPC64LE)
* Rocky Linux 8 (x86\_64, ARM64)
* Rocky Linux 9 (x86\_64, ARM64)
* SUSE Linux Enterprise Server 12 (x86\_64)
* SUSE Linux Enterprise Server 15 (x86\_64, ARM64)
* Ubuntu 20.04 (x86\_64, ARM64)
* Ubuntu 22.04 (x86\_64, ARM64)
* Ubuntu 24.04 (x86\_64, ARM64)
* Red Hat UBI 8 (x86\_64, ARM64)
  * Red Hat UBI 8 is part of the Enterprise Server Docker Image. It does not support MariaDB Enterprise Cluster (Galera) or MariaDB ColumnStore.

Some components of MariaDB Enterprise Server are supported on a subset of platforms. See [MariaDB Engineering Policies](https://mariadb.com/engineering-policies) for details.

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
