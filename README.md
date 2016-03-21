# SQLite 3 database sink

This is a simple custom sink made for spdlog that writes to SQLite database.

```
auto logging = spdlog::create<spdlog::sinks::database_logger_sink>("SQLiteSink","database.db");
```

### SQL Table

spdlog provides *log_msg* object to the custom sink containing 5 main properties.

* logger_name
* level
* time
* thread_id
* formatted (message)

To use this sink, you need to create a table with all 5 columns like so

```
CREATE TABLE "Logs" (
	`Id`	INTEGER PRIMARY KEY AUTOINCREMENT,
	`TimeStamp`	TEXT NOT NULL,
	`Level`	TEXT NOT NULL,
	`Message`	TEXT NOT NULL,
	`LoggerName`	TEXT NOT NULL,
	`ThreadId`	INTEGER NOT NULL
)
```

This sink uses prepared statements thus adds a bit of sql injection safety
