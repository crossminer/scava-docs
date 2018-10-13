When starting the platform, you can pass a configuration file to control the behaviour of the platform:

````Shell
./eclipse -slave -config myconfiguration.properties
````

The configuration file is a typical Java properties file. The properties that can be configured are:

#### `identifier=<your name>` 
The identifier of the node. If not specified, the platform will attempt to use the node's hostname, and if it cannot resolve the hostname, it will generated a random UUID. 

If you plan to multiple instances of the platform on the same machine, you should definitely specify different node identifiers.

#### `log.type=console|file|rolling`
You can specify whether to log output to the console (Log4J's ConsoleAppender), to a particular file without a size limit (Log4J's FileAppender), or to a different file per day (Log4J's DailyRollingFileAppender). If you specify `file` or `rolling`, you must complete the `log.file.path` or `log.rolling.path` property as well. 

If the property is not specified, it will default to the console logger.

#### `log.file.path=<path>`
The path to the file to store the log. E.g. `log.file.path=/tmp/lovelylog.log`

#### `log.rolling.path=<path>`
The path to the file to store the log. This is a Log4J DailyRollingFileAppender that will create separate logs for each 12 hours of the day. The date stamp will be appended to the path provided. E.g.: if you specify `log.rolling.path=/tmp/mylovelylog.log`, it will store files like so: `/tmp/mylovelylog.log.2014-12-17-00` and `/tmp/mylovelylog.log.2014-12-17-12`.

#### `maven_executable=<path>`
The path to where Maven is installed. E.g. `maven_executable=/usr/bin/mvn`

#### `storage_path=<path>`
The path to where files should be stored. E.g. `storage_path=/mnt/ossmeter/`

#### `mongo_hosts`
A comma-separated list of the hosts and ports in a replica set. E.g. `ua002:27017,ua009:27017,ua019:27017,ua020:27017`