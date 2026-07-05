# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-05T07:31:08Z
- **Commit:** [`c29367d`](https://github.com/arnabnandy7/client_java/commit/c29367daf4e6aec49eecf321b8e41553c2e194d5)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.13K | ± 259.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.92K | ± 345.45 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 511.36 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.94K | ± 874.81 | ops/s | 1.4x slower |
| simpleclientInc | 6.65K | ± 102.11 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.33K | ± 17.66 | ops/s | 10x slower |
| simpleclientAdd | 6.08K | ± 305.22 | ops/s | 11x slower |
| openTelemetryInc | 3.21K | ± 188.97 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.20K | ± 127.46 | ops/s | 21x slower |
| openTelemetryAdd | 3.14K | ± 239.81 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.05K | ± 1.43K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 91.35 | ops/s | 1.1x slower |
| prometheusNative | 3.00K | ± 284.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 759.61 | ± 46.42 | ops/s | 6.6x slower |
| openTelemetryExponential | 596.74 | ± 35.07 | ops/s | 8.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.95K | ± 170.33 | ops/s | **fastest** |
| prometheusWriteToNull | 22.82K | ± 216.27 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 501.73K | ± 4.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.51K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.53K | ± 3.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.95K | ± 3.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46937.666    ± 874.812  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3135.478    ± 239.807  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3205.780    ± 188.974  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3200.582    ± 127.463  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51275.259    ± 511.359  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66126.118    ± 259.031  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56915.661    ± 345.454  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6076.671    ± 305.222  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6648.627    ± 102.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6328.558     ± 17.656  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        759.606     ± 46.417  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        596.739     ± 35.069  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5045.262   ± 1429.535  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2996.863    ± 284.639  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.411     ± 91.350  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23950.485    ± 170.332  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22822.106    ± 216.267  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474948.720   ± 3378.923  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481530.596   ± 3729.267  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494505.497   ± 5273.505  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     501728.963   ± 3998.668  ops/s
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
