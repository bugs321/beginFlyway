


Sample commands
#to get list of script going to be applied
flyway info -configFiles=C:\OneSumX\conf\osx_ldm.conf -outputFile=C:\OneSumX_Release\logs\GDM_%date%_%time:~0,2%%time:~3,2%%time:~6,2%.log
#to create a baseline 
flyway baseline -configFiles=C:\OneSumX\conf\osx_ldm.conf -outputFile=C:\OneSumX_Release\logs\GDM_%date%_%time:~0,2%%time:~3,2%%time:~6,2%.log
flyway migrate -configFiles=C:\OneSumX\conf\osx_ldm.conf -outputFile=C:\OneSumX_Release\logs\GDM_%date%_%time:~0,2%%time:~3,2%%time:~6,2%.log

#To deploy only 2 sripts (1.1 and 1.2) from the available list of scripts to be executed then below command is used (add -target=X.X version)
flyway info -configFiles=C:\OneSumX_Release\conf\osx_gdm.conf -outputFile=C:\OneSumX_Release\logs\GDM_%date%_%time:~0,2%%time:~3,2%%time:~6,2%.log -target=1.2

Sample folder structure:

C:.
│   Readme.txt
│
├───conf
│       osx_fsdb.conf
│       osx_gdm.conf
│       osx_ldm.conf
│		osx_gdm_oracle.conf		
│
├───logs
│       GDM_10-01-2021_214311.log
│
└───sql
    │   FSDB1_1__fsdb_table1.sql
    │   FSDB1_2__fsdb_createTable2.sql
    │   FSDB1_3__fsdb_createTable3.sql
    │   GDM1_1__gdm_createTable1.sql
    │   GDM1_2__gdm_createTable2.sql
    │   GDM1_3__gdm_CreateTable3.sql
    │   GDM1_4__gdm_CreateTable3Error.sql
    │   LDM1_1__ldm_table1.sql
    │   LDM1_2__ldm_createTable2.sql
    │   LDM1_3__ldm_createTable3.sql
    │
    └───rollback



Flayway Usage
=============

flyway [options] command

By default, the configuration will be read from conf/flyway.conf.
Options passed from the command-line override the configuration.

Commands
--------
migrate  : Migrates the database
clean    : Drops all objects in the configured schemas
info     : Prints the information about applied, current and pending migrations
validate : Validates the applied migrations against the ones on the classpath
undo     : [teams] Undoes the most recently applied versioned migration
baseline : Baselines an existing database at the baselineVersion
repair   : Repairs the schema history table

Options (Format: -key=value)
-------
driver                       : Fully qualified classname of the JDBC driver
url                          : Jdbc url to use to connect to the database
user                         : User to use to connect to the database
password                     : Password to use to connect to the database
connectRetries               : Maximum number of retries when attempting to connect to the database
initSql                      : SQL statements to run to initialize a new database connection
schemas                      : Comma-separated list of the schemas managed by Flyway
table                        : Name of Flyway's schema history table
locations                    : Classpath locations to scan recursively for migrations
resolvers                    : Comma-separated list of custom MigrationResolvers
skipDefaultResolvers         : Skips default resolvers (jdbc, sql and Spring-jdbc)
sqlMigrationPrefix           : File name prefix for versioned SQL migrations
undoSqlMigrationPrefix       : [teams] File name prefix for undo SQL migrations
repeatableSqlMigrationPrefix : File name prefix for repeatable SQL migrations
sqlMigrationSeparator        : File name separator for SQL migrations
sqlMigrationSuffixes         : Comma-separated list of file name suffixes for SQL migrations
stream                       : [teams] Stream SQL migrations when executing them
batch                        : [teams] Batch SQL statements when executing them
mixed                        : Allow mixing transactional and non-transactional statements
encoding                     : Encoding of SQL migrations
placeholderReplacement       : Whether placeholders should be replaced
placeholders                 : Placeholders to replace in sql migrations
placeholderPrefix            : Prefix of every placeholder
placeholderSuffix            : Suffix of every placeholder
lockRetryCount               : The maximum number of retries when trying to obtain a lock
jdbcProperties               : Properties to pass to the JDBC driver object
installedBy                  : Username that will be recorded in the schema history table
target                       : Target version up to which Flyway should use migrations
cherryPick                   : [teams] Comma separated list of migrations that Flyway should consider when migrating
skipExecutingMigrations      : [teams] Whether Flyway should skip actually executing the contents of the migrations
outOfOrder                   : Allows migrations to be run "out of order"
callbacks                    : Comma-separated list of FlywayCallback classes, or locations to scan for FlywayCallback classes
skipDefaultCallbacks         : Skips default callbacks (sql)
validateOnMigrate            : Validate when running migrate
validateMigrationNaming      : Validate file names of SQL migrations (including callbacks)
ignoreMissingMigrations      : Allow missing migrations when validating
ignoreIgnoredMigrations      : Allow ignored migrations when validating
ignorePendingMigrations      : Allow pending migrations when validating
ignoreFutureMigrations       : Allow future migrations when validating
cleanOnValidationError       : Automatically clean on a validation error
cleanDisabled                : Whether to disable clean
baselineVersion              : Version to tag schema with when executing baseline
baselineDescription          : Description to tag schema with when executing baseline
baselineOnMigrate            : Baseline on migrate against uninitialized non-empty schema
configFiles                  : Comma-separated list of config files to use
configFileEncoding           : Encoding to use when loading the config files
jarDirs                      : Comma-separated list of dirs for Jdbc drivers & Java migrations
createSchemas                : Whether Flyway should attempt to create the schemas specified in the schemas property
dryRunOutput                 : [teams] File where to output the SQL statements of a migration dry run
errorOverrides               : [teams] Rules to override specific SQL states and errors codes
oracle.sqlplus               : [teams] Enable Oracle SQL*Plus command support
licenseKey                   : [teams] Your Flyway license key
color                        : Whether to colorize output. Values: always, never, or auto (default)
outputFile                   : Send output to the specified file alongside the console
outputType                   : Serialise the output in the given format, Values: json

Flags
-----
-X          : Print debug output
-q          : Suppress all output, except for errors and warnings
-n          : Suppress prompting for a user and password
-v          : Print the Flyway version and exit
-?          : Print this usage info and exit
-community  : Run the Flyway Community Edition (default)
-teams      : Run the Flyway Teams Edition

Example
-------
flyway -user=myuser -password=s3cr3t -url=jdbc:h2:mem -placeholders.abc=def migrate

More info at https://flywaydb.org/documentation/commandline
