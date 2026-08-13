# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-13T05:36:27Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.85K | ± 4.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 163.32 | ops/s | 1.1x slower |
| prometheusAdd | 50.83K | ± 649.56 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.21K | ± 1.50K | ops/s | 1.2x slower |
| simpleclientInc | 6.53K | ± 45.21 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.36K | ± 37.00 | ops/s | 9.6x slower |
| simpleclientAdd | 6.21K | ± 168.62 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 3.56K | ± 267.42 | ops/s | 17x slower |
| openTelemetryInc | 3.36K | ± 164.83 | ops/s | 18x slower |
| openTelemetryAdd | 3.17K | ± 162.80 | ops/s | 19x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.44K | ± 2.01K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 39.93 | ops/s | 1.5x slower |
| prometheusNative | 3.04K | ± 274.57 | ops/s | 2.1x slower |
| openTelemetryClassic | 735.05 | ± 27.66 | ops/s | 8.8x slower |
| openTelemetryExponential | 634.75 | ± 72.19 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.85K | ± 1.27K | ops/s | **fastest** |
| openMetricsWriteToNull | 23.31K | ± 587.82 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 511.06K | ± 3.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.12K | ± 5.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 490.68K | ± 1.74K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.48K | ± 2.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49207.514   ± 1496.339  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3170.605    ± 162.803  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3363.134    ± 164.834  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3561.730    ± 267.423  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50828.276    ± 649.561  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60846.696   ± 4381.117  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57052.736    ± 163.320  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6210.783    ± 168.619  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6526.934     ± 45.207  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6361.102     ± 36.998  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        735.049     ± 27.659  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        634.745     ± 72.187  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6442.589   ± 2007.708  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3043.080    ± 274.571  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.984     ± 39.933  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23305.415    ± 587.816  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23847.378   ± 1266.870  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481482.544   ± 2196.745  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490677.361   ± 1739.412  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500122.345   ± 5573.309  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     511061.408   ± 3013.218  ops/s
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
