# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-23T06:50:56Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.58K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.61K | ± 1.59K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.06K | ± 1.54K | ops/s | 1.1x slower |
| prometheusAdd | 28.46K | ± 11.05 | ops/s | 1.1x slower |
| simpleclientInc | 6.79K | ± 179.69 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.54K | ± 212.15 | ops/s | 4.7x slower |
| simpleclientAdd | 6.45K | ± 203.44 | ops/s | 4.7x slower |
| openTelemetryInc | 2.66K | ± 224.11 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 2.66K | ± 137.73 | ops/s | 11x slower |
| openTelemetryAdd | 2.36K | ± 94.93 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 39.74 | ops/s | **fastest** |
| prometheusClassic | 2.84K | ± 481.34 | ops/s | 1.6x slower |
| prometheusNative | 2.18K | ± 183.56 | ops/s | 2.0x slower |
| openTelemetryClassic | 604.86 | ± 20.23 | ops/s | 7.4x slower |
| openTelemetryExponential | 449.41 | ± 12.24 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.10K | ± 218.41 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.07K | ± 190.13 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.01K | ± 1.10K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.69K | ± 1.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 291.67K | ± 2.96K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 291.54K | ± 2.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29064.626   ± 1542.824  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2355.617     ± 94.932  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2663.744    ± 224.110  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2660.661    ± 137.731  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28462.767     ± 11.052  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30580.015   ± 1385.479  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29611.819   ± 1589.168  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6445.617    ± 203.437  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6792.132    ± 179.687  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6538.741    ± 212.150  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        604.861     ± 20.228  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        449.407     ± 12.236  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2844.851    ± 481.337  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2176.607    ± 183.559  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4449.710     ± 39.740  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18071.325    ± 190.134  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18097.260    ± 218.406  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     291673.355   ± 2960.129  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     291538.499   ± 2677.272  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313689.785   ± 1582.687  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318009.661   ± 1104.708  ops/s
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
