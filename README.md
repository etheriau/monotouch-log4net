monotouch-log4net
====================

Finally, Apache log4net made to run on MonoTouch iOS. It's a work in progress, alpha quality code base. Please help me by reporting and fixing bugs!

Because MonoTouch doesn't support System.Configuration, you must use a plain xml configuration file, and include it as a bundled resource. The file watch feature is also removed. Lastly, the following appenders are working.

### ConsoleAppender

Logs to Xamarin Studio application output when debugging. Also logs to Apple System Log, but only at the 'Warning' level), so they show up in the [device console](http://developer.apple.com/library/ios/qa/qa1747/_index.html).

    <appender name="ConsoleAppender" type="log4net.Appender.ConsoleAppender">
        <layout type="log4net.Layout.PatternLayout">
            <conversionPattern value="%date [%thread] %-5level %logger - %message%newline" />
        </layout>
    </appender>

### FileAppender

Logs to the application caches directory. Log file can be [downloaded](http://developer.apple.com/library/ios/recipes/xcode_help-devices_organizer/articles/copy_app_data_from_sandbox.html#//apple_ref/doc/uid/TP40010392-CH14-SW1) using the Xcode Organizer.

    <appender name="FileAppender" type="log4net.Appender.FileAppender">
        <file value="log/log-file.txt" />
        <appendToFile value="true" />
        <layout type="log4net.Layout.PatternLayout">
            <conversionPattern value="%date [%thread] %-5level %logger - %message%newline" />
        </layout>
    </appender>

### RollingFileAppender

Logs to the application caches directory. Log files can be downloaded using the Xcode Organizer.

    <appender name="RollingFileAppender" type="log4net.Appender.RollingFileAppender">
        <file value="log/log-file.txt" />
        <appendToFile value="true" />
        <rollingStyle value="Size" />
        <maxSizeRollBackups value="10" />
        <maximumFileSize value="100KB" />
        <staticLogFileName value="true" />
        <layout type="log4net.Layout.PatternLayout">
            <conversionPattern value="%date [%thread] %-5level %logger - %message%newline" />
        </layout>
    </appender>

### LocalSyslogAppender

Logs to [Apple System Log](http://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/LoggingErrorsAndWarnings.html) with the corresponding levels. Unfortunately, ASL will filter out 'INFO' and 'DEBUG' level entries. Therefore only use this appender for severity of 'WARN' and above.

    <appender name="syslog" type="log4net.Appender.LocalSyslogAppender">
        <facility value="Local6" />
        <identity value="MyApp" />
        <layout type="log4net.Layout.PatternLayout">
            <conversionPattern value="%date [%thread] %-5level %logger - %message%newline" />
        </layout>
    </appender>

