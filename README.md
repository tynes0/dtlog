# dtlog

**dtlog** is a lightweight, high-performance, and thread-safe logging library for C++ applications. It is designed to be easy to integrate, featuring console coloring, robust file logging with rotation support, and a flexible formatting system.

## Features

* **Thread-Safe:** Built-in mutex protection ensures safe logging from multiple threads.
* **High Performance:** Uses buffered C-style I/O (`fwrite`) for console output and standard streams for file operations.
* **Sink Architecture:** flexible design allowing logging to multiple targets (Console, File, Rotating File) simultaneously.
* **Log Rotation:** Includes `rotating_file_sink` to prevent disk overflow by automatically managing log file sizes and backups.
* **Cross-Platform:** Supports Windows (WinAPI) and Linux/macOS (ANSI colors) out of the box.
* **Custom Formatting:** Highly customizable log patterns (e.g., `[%R] [%L]: %V`).
* **Modern C++:** Utilizes C++17 features like `std::filesystem` for reliable file management.

## Requirements

* **C++ Standard:** C++17 or later (Required for `std::filesystem`).
* **Compiler:** GCC, Clang, or MSVC.

## Installation

`dtlog` is straightforward to integrate. It consists of a header file and a source file.

1.  Copy `dtlog.h` and `dtlog.cpp` into your project's source directory.
2.  Include `dtlog.h` in your code.
3.  Compile `dtlog.cpp` along with your project files.

## Quick Start

Here is a simple example of how to use the default logger (which logs to the console):

```cpp
#include "dtlog.h"

int main() {
    // Create a logger instance with a name
    dtlog::logger log("App");

    // Log messages with different levels
    log.info("Application started successfully.");
    log.warning("Memory usage is at 75%.");
    log.error("Connection to database failed.");
    
    // Support for formatting arguments
    int errorCode = 404;
    log.error("Failed to fetch resource. Error code: {}", errorCode);

    return 0;
}
```

## Advanced Usage

### Logging to Files (Log Rotation)

You can attach multiple "sinks" to a logger. The `rotating_file_sink` is perfect for production environments as it manages file sizes automatically to prevent disk overflow.

```cpp
#include "dtlog.h"

int main() {
    dtlog::logger log("Server");

    // 1. Create a rotating file sink
    // Arguments: filename, max_size (in bytes), max_backup_files
    // Example: 5MB limit, keep 3 backup files
    auto fileSink = std::make_shared<dtlog::rotating_file_sink>("logs/server.log", 5 * 1024 * 1024, 3);
    
    // 2. Add the sink to the logger
    log.add_sink(fileSink);

    // Now logs will go to both Console (default) and File
    log.info("This message goes to both console and the rotating log file.");

    return 0;
}
```

### Customizing the Log Pattern

You can customize how the log messages are formatted using `set_pattern`.

```cpp
dtlog::logger log("MyLogger");

// Set custom pattern: [Time] [Level] [LoggerName]: Message
log.set_pattern("[%T] [%L] [%N]: %V%n");

log.info("Custom formatted message");
// Output: [info] [MyLogger]: Custom formatted message
```

#### Supported Pattern Flags

| Flag | Description                       | Example                          |
|:-----|:----------------------------------|:---------------------------------|
| `%V` | The actual log message            | "System started"                 |
| `%N` | Logger name                       | "App"                            |
| `%L` | Log level                         | "info", "error"                  |
| `%n` | Newline                           | `\n`                             |
| `%R` | Full date and time representation | "Sunday January 1 2023 12:00:00" |
| `%D` | Short date (MM/DD/YY)             | "01/01/23"                       |
| `%T` | ISO 8601 Time (HH:MM:SS)          | "14:30:05"                       |
| `%Y` | Year (4 digits)                   | "2023"                           |
| `%C` | Year (2 digits)                   | "23"                             |
| `%B` | Full month name                   | "January"                        |
| `%m` | Month (01-12)                     | "01"                             |
| `%A` | Full weekday name                 | "Sunday"                         |
| `%d` | Day of month (01-31)              | "01"                             |
| `%H` | Hour (24-hour format)             | "14"                             |
| `%h` | Hour (12-hour format)             | "02"                             |
| `%M` | Minute                            | "30"                             |
| `%S` | Second                            | "05"                             |
| `%F` | AM/PM designation                 | "PM"                             |
| `%x` | 12-hour clock time with AM/PM     | "02:30:05 PM"                    |
| `%X` | HH:MM time (24-hour)              | "14:30"                          |
| `%%` | The literal '%' character         | "%"                              |

## Log Levels

The library supports the following log levels (ordered by severity):

1.  `trace`
2.  `info`
3.  `debug`
4.  `warning`
5.  `error`
6.  `critical`
7.  `none`

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Author

* **GitHub:** [tynes0](https://github.com/tynes0)
* **Email:** cihanbilgihan@gmail.com 
* For contributions, bug reports, or other inquiries, feel free to contact the author.
