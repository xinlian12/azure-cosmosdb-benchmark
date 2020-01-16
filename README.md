# azure core benchmarks

Compares Azure Core Logger with Slf4j Logger.
Specifically we are more interested in perf numbers comparision of slf4j and azure-core-logger
 for the case when the log level for that particular log level is disabled.

## how to run the benchmark app

To run the benchmarks:

Note this benchmark app is intended to be used on Linux or Mac.
If you want to run on windows, you may need to update `log4j.appender.FILE.File=/dev/null` in 
`src/main/resources/log4j.properties` according to windows equivalent.

```bash
mvn clean package
java -jar target/azure-core-benchmarks.jar -wi 2 -i 2 -f 1 -t 100
```

## sample benchmark results

Here is some sample benchmark results. 

Please note that the throughput of 
`logDebug_CheckLevel_DebugIsDisabled_SLF4J` compared to 
`logDebug_CheckLevel_DebugIsDisabled_AzureLogger` is `422586263/5275716` which `80x`.


```bash
# Run complete. Total time: 00:01:03

Benchmark                                                                    Mode  Cnt          Score   Error  Units
AzureCoreLoggerVsSlf4jPerf.logDebug_CheckLevel_DebugIsDisabled_AzureLogger  thrpt    2    5275716.491          ops/s
AzureCoreLoggerVsSlf4jPerf.logDebug_CheckLevel_DebugIsDisabled_SLF4J        thrpt    2  422586263.085          ops/s
AzureCoreLoggerVsSlf4jPerf.logDebug_DebugIsDisabled_AzureLogger             thrpt    2    6725075.646          ops/s
AzureCoreLoggerVsSlf4jPerf.logDebug_DebugIsDisabled_SLF4J                   thrpt    2  396479458.548          ops/s
AzureCoreLoggerVsSlf4jPerf.logInfoWithArgs_InfoIsEnabled_AzureLogger        thrpt    2     139918.885          ops/s
AzureCoreLoggerVsSlf4jPerf.logInfoWithArgs_InfoIsEnabled_SLF4J              thrpt    2     158342.225          ops/s
AzureCoreLoggerVsSlf4jPerf.logInfo_CheckLevel_InfoIsEnabled_AzureLogger     thrpt    2     160737.930          ops/s
AzureCoreLoggerVsSlf4jPerf.logInfo_CheckLevel_InfoIsEnabled_SLF4J           thrpt    2     192539.772          ops/s
AzureCoreLoggerVsSlf4jPerf.logInfo_InfoIsEnabled_AzureLogger                thrpt    2     152298.308          ops/s
AzureCoreLoggerVsSlf4jPerf.logInfo_InfoIsEnabled_sf4j                       thrpt    2     238016.150          ops/s
```

