# dtlog Logging Library

## Introduction

The `dtlog` library provides a flexible and customizable logging framework for C++ applications. It offers various log levels, message formatting options, and supports logging to different output destinations such as standard output, standard error, and files.

## Installation

To use the `dtlog` library in your C++ project, follow these steps:

1. Clone the repository from GitHub:
```bash
git clone https://github.com/tynes0/dtlog.git
```
2. Include the necessary header files in your project:

```cpp
#include "dtlog/dtlog.h"
```

3. Build your project with the dtlog library included.

### Header-Only Option
For users who prefer a header-only approach, the dtlog_ho.h file is provided as part of the project.

## Getting Started

The library encompasses various components for logging operations. Among these components are determining log levels, formatting log messages, and directing log messages to different output points. The key components of the library are as follows:

- **formatter:** An auxiliary class used for formatting log messages.
- **date_time_formatter:** An auxiliary class used for formatting date and time information.
- **log_level:** An enum class representing logging levels.
- **logger:** The main class used for managing logging operations.

### formatter Class

The formatter class is used to format log messages according to a specific format template. This class has the following main functions:

- **format:** Constructs a log message based on a given format template and arguments.
- **operator():** Formats log messages using an overloaded function call operator.

### date_time_formatter Class

The date_time_formatter class is used to format date and time information in different formats. Some of the methods provided by this class include:

- **full_weekday_name:** Retrieves the full name of the weekday.
- **full_month_name:** Retrieves the full name of the month.
- **year_2_digits:** Retrieves the last two digits of the year.
- **year_4_digits:** Retrieves the full four digits of the year.
- **date_time_representation:** Retrieves date and time information in a specified format.
- **short_MMDDYY_date:** Retrieves date information in a short format.
- **month:** Retrieves the numerical representation of the month.
- **day_of_month:** Retrieves the day of the month.
- **hours_24_format:** Retrieves the hour information in a 24-hour format.
- **hours_12_format:** Retrieves the hour information in a 12-hour format.
- **minutes:** Retrieves the minute information.
- **seconds:** Retrieves the second information.
- **AM_PM:** Retrieves the hour information in AM/PM format.
- **clock_12_hour:** Retrieves the hour and AM/PM information in a 12-hour format.
- **HHMM_time_24_hour:** Retrieves the hour and minute information in a 24-hour format.
- **ISO8601_time_format:** Retrieves the hour information in ISO 8601 format.

### log_level Enum Class

The log_level enum class is used to specify logging levels. This class includes the following logging levels:

- none: No logging is performed.
- trace: Logging is performed at the trace level.
- info: Logging is performed at the info level.
- debug: Logging is performed at the debug level.
- warning: Logging is performed at the warning level.
- error: Logging is performed at the error level.
- critical: Logging is performed at the critical error level.

  # Logger Class

The logger class is responsible for managing logging operations within an application. It provides essential functionalities for logging messages with different log levels, formatting options, and output destinations.

## Constructors

- `logger(const std::string& log_name = "dtlog", const std::string& pattern = "[%R] %N: %V")`: Constructs a logger with a specified name and log message pattern.

## Public Member Functions

- `void log(log_level level, const std::string& message, _Args&&... args)`: Logs a message with the specified log level.
- `void log_stderr(log_level level, const std::string& message, _Args&&... args)`: Logs a message with the specified log level to stderr.
- `void log_to_file(const std::string& filename, const std::string& message, _Args&&... args)`: Logs a message with the specified log level to a file.
- `void set_name(const std::string& name)`: Sets the name of the logger.
- `std::string get_name() const`: Gets the name of the logger.
- `void set_pattern(const std::string& format)`: Sets the log message pattern.
- `std::string get_pattern() const`: Gets the log message pattern.
- `void trace(const std::string& message, _Args&&... args)`: Logs a trace-level message.
- `void info(const std::string& message, _Args&&... args)`: Logs an info-level message.
- `void debug(const std::string& message, _Args&&... args)`: Logs a debug-level message.
- `void warning(const std::string& message, _Args&&... args)`: Logs a warning-level message.
- `void error(const std::string& message, _Args&&... args)`: Logs an error-level message.
- `void critical(const std::string& message, _Args&&... args)`: Logs a critical-level message.

## Example Usage

Below is an example demonstrating basic usage of the logger class:

```cpp
#include "dtlog/dtlog.h"

int main()
{
    dtlog::logger myLogger;
    myLogger.set_name("MyLogger");
    myLogger.set_pattern("[%R] %N: %V");

    myLogger.info("This is an information message.");
    myLogger.error("An error occurred with code {0}.", 500);

    return 0;
}
```

In this example, a logger named MyLogger is created with a specific log message pattern. Information and error messages are then logged using the info and error functions, respectively.

```cpp
#include "dtlog/dtlog.h"

int main()
 {
    dtlog::logger myLogger;
    myLogger.set_name("MyLogger");
    myLogger.set_pattern("[%R] %N: %V");

    myLogger.trace("This is a trace-level message.");
    myLogger.debug("Debugging information: {1} -> {0}", 10, "Variable x");
    myLogger.warning("Warning: Memory usage is high!");
    myLogger.critical("Critical error: Failed to allocate memory.");

    return 0;
}
```

```cpp
#include "dtlog/dtlog.h"

int main()
{
    dtlog::logger myLogger("ApplicationLog", "[%R] [%L] %V");

    myLogger.info("Starting application...");

    // Simulate some processing
    for (int i = 0; i < 10; ++i)
        myLogger.debug("Processing item {}", i);

    myLogger.info("Application finished.");

    // Log to a file named "app.log"
    myLogger.log_to_file("app.log", "Application finished successfully.");

    return 0;
}
```

## References
**Author:** [https://github.com/tynes0](https://github.com/tynes0)

**Original GitHub Repository:** [https://github.com/tynes0/dtlog](https://github.com/tynes0/dtlog)

**Contact Email:** cihanbilgihan@gmail.com

It is released under the Apache License 2.0. See the LICENSE.

For contributions, bug reports, or other inquiries, feel free to contact the author.
