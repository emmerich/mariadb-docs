# MariaDB Java Client 1.1.1 Changelog

{% include "../../../../.gitbook/includes/latest-java.md" %}

[Download](https://downloads.mariadb.org/client-java/1.1.1/) | [Release Notes](../../1.1/mariadb-java-client-111-release-notes.md) | **Changelog** |[Java Client Overview](https://github.com/mariadb-corporation/docs-release-notes/blob/test/en/about-the-mariadb-java-client/README.md)

**Release date:** 01 Mar 2013

For the highlights of this release, see the [release notes](../../1.1/mariadb-java-client-111-release-notes.md).

The revision number links will take you to the revision's page on Launchpad. On Launchpad you can view more details of the revision and view diffs of the code modified in that revision.

* [Revision #414](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/414)\
  Wed 2013-02-27 23:17:31 +0100
  * [CONJ-27](https://jira.mariadb.org/browse/CONJ-27) : Implement tcpAbortiveClose option, for "hard" socket closing.
  * If set, client will abort connection in a way that TCP connection does not enter usual TCP\_WAIT state upon close, and free local port. This option can be handy in situation where connections are created and destroyed in rapid succession and new connection can't be created because of port shortage.
* [Revision #413](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/413)\
  Wed 2013-02-27 23:00:07 +0100
  * Removed unused classes.
* [Revision #412](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/412)\
  Mon 2013-02-18 15:21:03 +0100
  * Fix test warning
* [Revision #411](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/411)\
  Mon 2013-02-18 15:20:40 +0100
  * Small refactoring : remove yet another unnecessary level of abstraction - MySQLQueryFactory. Use MySQLQuery directory
* [Revision #410](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/410)\
  Thu 2013-02-14 22:32:33 +0100
  * [CONJ-25](https://jira.mariadb.org/browse/CONJ-25) : Close open streaming result sets, when closing connection.
  * Prior to this patch a connection would hang during close(), if streaming result set was not fully read.
* [Revision #409](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/409)\
  Wed 2013-02-13 23:05:29 +0100
  * [CONJ-24](https://jira.mariadb.org/browse/CONJ-24) - first() is not legal to use with streaming result set, throw exception if it used
* [Revision #408](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/408)\
  Wed 2013-02-13 17:28:01 +0100
  * Refactor code for getGeneratedKeys() - remove unnecessary classes.
* [Revision #407](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/407)\
  Wed 2013-02-13 11:05:14 +0100
  * [CONJ-23](https://jira.mariadb.org/browse/CONJ-23) : JVM does not exit if statement timeout is used.
  * The reason is that timer thread does not exit. The fix is to Use Timer constructor that marks timer thread a daemon.
* [Revision #406](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/406)\
  Tue 2013-02-12 22:30:04 +0100
  * Do not generate javadoc during the build (no reason for it,as long as we implement standard JDBC interfaces)
* [Revision #405](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/405)\
  Tue 2013-02-12 22:29:01 +0100
  * Use arrays rather than lists to represent resultset metadata and cached result set row, for array are more efficient (faster element access, less space)
* [Revision #404](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/404)\
  Tue 2013-02-12 15:56:23 +0100
  * Implement lazy parsing of result set metadata. Avoid calling expensive String constructors unless necessary.
* [Revision #403](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/403)\
  Mon 2013-02-11 20:11:51 +0100
  * Remove unportable IPV6 test (requires working dual stack and 5.5)
* [Revision #402](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/402)\
  Thu 2013-02-07 23:13:02 +0100
  * Speed up Connection.getWarnings() - avoid unnicessary "show warnings", if last statement did not produce any warnings.
* [Revision #401](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/401)\
  Sun 2013-02-03 21:39:59 +0100
  * [CONJ-20](https://jira.mariadb.org/browse/CONJ-20) Ensure that getObject() returns byte array for CHAR BINARY.
  * Also make sure that getColumnType,getColumnClassName,getColumnTypeName return values indicating binary type for fixed binary type
* [Revision #400](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/400)\
  Sun 2013-02-03 00:32:30 +0100
  * [CONJ-17](https://jira.mariadb.org/browse/CONJ-17) : ResultSetMetaData.getColumnName() returned empty string for special cases, where result set column was not a column from any table. For example, column name returned by ResultRSetMetaData.getColumnName(1) for the query " select count(\*) from table" would be empty string ""
  * The fix is to return column label (called "virtual column name" here [text-protocol.html#packet-Protocol::ColumnDefinition](https://dev.mysql.com/doc/internals/en/text-protocol.html#packet-Protocol::ColumnDefinition)) instead of "".
* [Revision #399](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/399)\
  Sat 2013-02-02 22:04:50 +0100
  * [CONJ-19](https://jira.mariadb.org/browse/CONJ-19) : DatabaseMetaData.getColumns() handled MySQL YEAR datatype as SMALLINT. Fixed to return DATE by default and SMALLINT only n case yearIsDateType=false is set
* [Revision #398](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/398)\
  Sat 2013-02-02 14:37:34 +0100
  * Fix test case
* [Revision #397](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/397)\
  Sat 2013-02-02 14:37:14 +0100
  * [CONJ-15](https://jira.mariadb.org/browse/CONJ-15) - DatabaseMedataData.getColumns() returned incorrect value in "COLUMN\_SIZE" column for character data.
  * Fix is to use I\_S.COLUMNS.CHARACTER\_MAXIMUM\_LENGTH instead of I\_IS.COLUMNS.CHARACTER\_OCTET\_LENGTH to calculate COLUMN\_SIZE
  * Also, return COLUMN\_SIZE for temporal datatypes instead of NULL.
* [Revision #396](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/396)\
  Sat 2013-02-02 13:35:04 +0100
  * [CONJ-16](https://jira.mariadb.org/browse/CONJ-16) : Introduced nullCatalogMeansCurrent parameter, compatibly to ConnectorJ.
  * There are applications that depend on ConnectorJ default behavior, even if this behavior deviates from standard.
* [Revision #395](https://bazaar.launchpad.net/~maria-captains/mariadb-java-client/trunk/revision/395)\
  Thu 2013-01-17 23:34:26 +0100
  * CONJ14 - Fix MySQLStatement to return -1 from getUpdateCount() and null from getResultSet() in case there are no more results.

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formid="4316" formId="4316" %}
