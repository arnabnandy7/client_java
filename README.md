# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-26T06:57:53Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.69K | ± 483.27 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.53K | ± 455.95 | ops/s | 1.2x slower |
| prometheusAdd | 48.81K | ± 753.55 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.19K | ± 365.47 | ops/s | 1.4x slower |
| simpleclientInc | 6.18K | ± 35.81 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.88K | ± 57.40 | ops/s | 10x slower |
| simpleclientAdd | 5.83K | ± 228.77 | ops/s | 10x slower |
| openTelemetryInc | 4.49K | ± 1.24K | ops/s | 13x slower |
| openTelemetryAdd | 4.07K | ± 868.02 | ops/s | 15x slower |
| openTelemetryIncNoLabels | 3.83K | ± 166.75 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.63K | ± 1.33K | ops/s | **fastest** |
| simpleclient | 4.30K | ± 69.56 | ops/s | 1.3x slower |
| prometheusNative | 2.95K | ± 86.15 | ops/s | 1.9x slower |
| openTelemetryClassic | 731.06 | ± 12.00 | ops/s | 7.7x slower |
| openTelemetryExponential | 562.97 | ± 13.33 | ops/s | 10.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.26K | ± 145.62 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.86K | ± 687.88 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 565.59K | ± 2.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 552.07K | ± 2.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 530.74K | ± 4.83K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 506.77K | ± 5.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44190.467    ± 365.468  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4068.099    ± 868.016  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4492.434   ± 1243.704  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3828.047    ± 166.749  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48810.665    ± 753.548  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59687.441    ± 483.273  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51533.834    ± 455.948  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5825.315    ± 228.766  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6182.082     ± 35.810  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5875.336     ± 57.398  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        731.063     ± 12.003  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.970     ± 13.327  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5625.839   ± 1330.137  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2954.043     ± 86.152  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4296.958     ± 69.564  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26856.012    ± 687.877  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27259.299    ± 145.615  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506767.868   ± 5523.942  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     530743.077   ± 4829.373  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     552069.584   ± 2331.020  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     565587.328   ± 2982.435  ops/s
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
