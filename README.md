# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-19T08:34:06Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.70K | ± 554.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.81K | ± 394.90 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.52K | ± 432.30 | ops/s | 1.3x slower |
| prometheusAdd | 50.06K | ± 2.35K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 38.49 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 36.28 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 337.17 | ops/s | 11x slower |
| openTelemetryInc | 3.48K | ± 197.34 | ops/s | 19x slower |
| openTelemetryAdd | 3.20K | ± 399.48 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.07K | ± 57.65 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 14.67 | ops/s | 1.2x slower |
| prometheusNative | 3.15K | ± 42.85 | ops/s | 1.7x slower |
| openTelemetryClassic | 759.81 | ± 14.20 | ops/s | 7.1x slower |
| openTelemetryExponential | 700.47 | ± 62.48 | ops/s | 7.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.12K | ± 361.93 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.42K | ± 250.57 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 500.29K | ± 3.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.80K | ± 6.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.63K | ± 5.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.12K | ± 5.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50516.645    ± 432.298  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3196.995    ± 399.479  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3483.061    ± 197.343  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3071.719     ± 57.652  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50055.259   ± 2351.308  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65702.677    ± 554.295  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56806.486    ± 394.899  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6231.302    ± 337.166  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6606.537     ± 38.490  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.452     ± 36.277  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        759.812     ± 14.202  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        700.472     ± 62.479  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5414.727   ± 1475.486  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3151.134     ± 42.850  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4380.408     ± 14.667  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23424.643    ± 250.566  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24116.086    ± 361.933  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474116.166   ± 5804.070  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476630.269   ± 5806.088  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489798.292   ± 6470.135  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500285.103   ± 3975.632  ops/s
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
