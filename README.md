# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-13T07:04:27Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.41K | ± 1.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 152.36 | ops/s | 1.1x slower |
| prometheusAdd | 51.35K | ± 306.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.08K | ± 1.06K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 23.97 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.43K | ± 145.95 | ops/s | 10x slower |
| simpleclientAdd | 5.95K | ± 375.57 | ops/s | 11x slower |
| openTelemetryInc | 3.28K | ± 190.92 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.10K | ± 26.38 | ops/s | 21x slower |
| openTelemetryAdd | 3.10K | ± 30.63 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.54K | ± 944.01 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 11.64 | ops/s | 1.5x slower |
| prometheusNative | 3.02K | ± 318.63 | ops/s | 2.2x slower |
| openTelemetryClassic | 771.89 | ± 18.99 | ops/s | 8.5x slower |
| openTelemetryExponential | 589.91 | ± 48.02 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.52K | ± 363.84 | ops/s | **fastest** |
| prometheusWriteToNull | 24.26K | ± 668.82 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.01K | ± 5.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.54K | ± 2.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.01K | ± 2.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.46K | ± 4.72K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49077.249   ± 1061.458  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3098.508     ± 30.632  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3280.346    ± 190.921  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3099.490     ± 26.384  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51354.625    ± 306.446  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64410.048   ± 1045.525  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57079.628    ± 152.360  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5946.204    ± 375.568  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.246     ± 23.975  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6429.853    ± 145.948  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        771.887     ± 18.993  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        589.908     ± 48.023  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6536.320    ± 944.013  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3020.198    ± 318.625  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4371.490     ± 11.635  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24518.823    ± 363.842  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24261.616    ± 668.822  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480463.518   ± 4721.099  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485013.040   ± 2131.922  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495544.961   ± 2778.465  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503006.122   ± 5557.077  ops/s
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
