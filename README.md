# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-25T08:53:08Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.47K | ± 3.59K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.01K | ± 816.35 | ops/s | 1.1x slower |
| prometheusAdd | 51.48K | ± 292.01 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.92K | ± 969.96 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 6.10 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.33K | ± 12.93 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 176.36 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.33K | ± 271.29 | ops/s | 19x slower |
| openTelemetryInc | 3.29K | ± 149.38 | ops/s | 19x slower |
| openTelemetryAdd | 3.21K | ± 261.00 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.16K | ± 1.25K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 49.53 | ops/s | 1.4x slower |
| prometheusNative | 2.86K | ± 295.27 | ops/s | 2.2x slower |
| openTelemetryClassic | 729.83 | ± 15.98 | ops/s | 8.4x slower |
| openTelemetryExponential | 621.86 | ± 57.19 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.71K | ± 864.49 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.57K | ± 1.20K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 515.99K | ± 7.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 510.16K | ± 2.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 490.26K | ± 1.62K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 487.38K | ± 1.01K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47920.209    ± 969.959  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3205.241    ± 261.000  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3291.318    ± 149.378  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3332.168    ± 271.290  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51478.191    ± 292.011  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63467.269   ± 3593.292  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56008.366    ± 816.347  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6217.588    ± 176.364  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6582.698      ± 6.100  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6334.994     ± 12.927  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        729.830     ± 15.985  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        621.861     ± 57.191  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6160.705   ± 1250.141  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2861.328    ± 295.273  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4387.246     ± 49.529  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23565.291   ± 1200.578  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23707.477    ± 864.487  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487378.275   ± 1007.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490258.485   ± 1616.758  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     510163.804   ± 2824.998  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515991.088   ± 7075.461  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
