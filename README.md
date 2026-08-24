# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-24T04:29:36Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.18K | ± 317.13 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.53K | ± 362.34 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 356.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.77K | ± 1.52K | ops/s | 1.4x slower |
| simpleclientInc | 6.63K | ± 58.20 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.33K | ± 7.68 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 263.39 | ops/s | 11x slower |
| openTelemetryAdd | 3.41K | ± 120.67 | ops/s | 19x slower |
| openTelemetryInc | 3.22K | ± 199.15 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.09K | ± 316.91 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 66.26 | ops/s | **fastest** |
| prometheusClassic | 4.32K | ± 292.20 | ops/s | 1.0x slower |
| prometheusNative | 2.77K | ± 337.20 | ops/s | 1.6x slower |
| openTelemetryClassic | 762.94 | ± 18.82 | ops/s | 5.8x slower |
| openTelemetryExponential | 699.81 | ± 80.63 | ops/s | 6.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.93K | ± 633.00 | ops/s | **fastest** |
| prometheusWriteToNull | 23.63K | ± 1.17K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.03K | ± 6.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.40K | ± 4.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.75K | ± 4.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.53K | ± 2.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48769.418   ± 1517.995  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3409.904    ± 120.668  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3223.561    ± 199.149  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3086.599    ± 316.914  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51346.993    ± 356.393  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66183.544    ± 317.132  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56533.512    ± 362.341  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6264.607    ± 263.394  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6627.724     ± 58.202  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6333.224      ± 7.675  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        762.942     ± 18.821  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        699.812     ± 80.631  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4324.801    ± 292.198  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2766.213    ± 337.196  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4446.599     ± 66.262  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23926.265    ± 633.001  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23631.110   ± 1173.535  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471534.587   ± 2746.618  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476748.794   ± 4012.352  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496404.750   ± 4127.344  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499034.867   ± 6983.952  ops/s
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
