# Mulesoft Tracing Module Integration
Tracing module enables you to enhance your logs by adding, removing, and clearing all variables from the logging context for a given Mule event. It also enables you to modify the correlation ID during flow execution.
# Uses Of Tracing Module
* Clear all the logging variables from the event logging context.
* Remove a logging variable from logging context.
* Set logging variables to logging context.
* Modify the correlation ID during flow execution
# MDC logging
MDC Logging: Mapped Diagnostic Context (MDC) enriches logging and improves tracking by providing more context or information in the logs for the current Mule event. By default, Mule logs two MDC entries: processor, which shows the location of the current event, and event, which shows the correlation ID of the event.  Open the log4j.xml file and Replace ```[processor: %X{processorPath}; event: %X{correlationId}] ``` with ```[%MDC]```.

# Console logging
For Console logging, We have to add Console appenders under Appenders tag. Also we have to add appender reference to AsyncLogger
```
<?xml version="1.0" encoding="utf-8"?>
<Configuration>
<Appenders>
        <RollingFile name="file" fileName="${sys:mule.home}${sys:file.separator}logs${sys:file.separator}mulesoft-tracing-module-integration.log"
                 filePattern="${sys:mule.home}${sys:file.separator}logs${sys:file.separator}mulesoft-tracing-module-integration-%i.log">
        <PatternLayout pattern="%-5p %d [%t] [%MDC] %c: %m%n"/>
            <SizeBasedTriggeringPolicy size="10 MB"/>
            <DefaultRolloverStrategy max="10"/>
        </RollingFile>
       <Console name="Console" target="SYSTEM_OUT">
          <PatternLayout pattern="%-5p %d [%t] [%MDC] %c: %m%n"/>
        </Console>
    </Appenders>
<Loggers>
        <!-- Http Logger shows wire traffic on DEBUG -->
        <!--AsyncLogger name="org.mule.service.http.impl.service.HttpMessageLogger" level="DEBUG"/-->
        <AsyncLogger name="org.mule.service.http" level="WARN"/>
        <AsyncLogger name="org.mule.extension.http" level="WARN"/>
<!-- Mule logger -->
        <AsyncLogger name="org.mule.runtime.core.internal.processor.LoggerMessageProcessor" level="INFO"/>
<AsyncRoot level="INFO">
            <AppenderRef ref="file"/>
          <AppenderRef ref="Console"/>
        </AsyncRoot>
</Loggers>
</Configuration>
```

# Steps to run application
 * Clone the repo
 * Run the application
 * Hit the below curl and verify the logs. 
 ```bash
curl --location --request POST 'http://localhost:8081/trace' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orderId": 548102842,
    "customerId": "ARG-12934",
    "items": [
        "CP-123",
        "CP-452"
    ]
}'
```
 
