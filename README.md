# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-20T07:05:04Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.60K | ± 454.70 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.06K | ± 536.61 | ops/s | 1.2x slower |
| prometheusAdd | 46.51K | ± 2.80K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.28K | ± 787.81 | ops/s | 1.3x slower |
| simpleclientInc | 6.17K | ± 116.71 | ops/s | 9.7x slower |
| simpleclientAdd | 6.10K | ± 14.51 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.90K | ± 52.33 | ops/s | 10x slower |
| openTelemetryAdd | 4.50K | ± 823.33 | ops/s | 13x slower |
| openTelemetryInc | 3.99K | ± 1.19K | ops/s | 15x slower |
| openTelemetryIncNoLabels | 3.60K | ± 241.40 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.12K | ± 1.76K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 30.80 | ops/s | 1.4x slower |
| prometheusNative | 2.83K | ± 158.01 | ops/s | 2.2x slower |
| openTelemetryClassic | 711.00 | ± 3.97 | ops/s | 8.6x slower |
| openTelemetryExponential | 580.46 | ± 29.70 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.60K | ± 148.81 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.19K | ± 305.27 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 583.45K | ± 5.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 570.62K | ± 3.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 550.60K | ± 5.88K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 535.17K | ± 1.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44279.921    ± 787.813  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4504.888    ± 823.335  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3985.595   ± 1189.261  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3597.659    ± 241.403  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      46506.443   ± 2799.235  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59599.510    ± 454.703  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51060.923    ± 536.608  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6095.494     ± 14.508  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6167.956    ± 116.708  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5900.810     ± 52.326  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        711.004      ± 3.970  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.463     ± 29.698  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6117.988   ± 1760.166  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2829.920    ± 158.011  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4392.875     ± 30.799  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27191.116    ± 305.267  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27596.875    ± 148.811  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535168.703   ± 1625.749  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     550596.061   ± 5882.635  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     570617.640   ± 3134.709  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     583449.017   ± 5812.115  ops/s
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
