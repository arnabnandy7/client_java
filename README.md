# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-24T06:45:58Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.32K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.83K | ± 849.38 | ops/s | 1.2x slower |
| prometheusAdd | 47.75K | ± 685.36 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.26K | ± 227.90 | ops/s | 1.4x slower |
| simpleclientInc | 6.20K | ± 83.49 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.86K | ± 95.05 | ops/s | 10x slower |
| simpleclientAdd | 5.80K | ± 233.42 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.45K | ± 1.49K | ops/s | 14x slower |
| openTelemetryInc | 4.12K | ± 959.38 | ops/s | 15x slower |
| openTelemetryAdd | 3.31K | ± 136.36 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.23K | ± 3.29K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 29.40 | ops/s | 1.4x slower |
| prometheusNative | 3.05K | ± 296.93 | ops/s | 2.0x slower |
| openTelemetryClassic | 720.39 | ± 15.20 | ops/s | 8.6x slower |
| openTelemetryExponential | 569.56 | ± 11.45 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.48K | ± 307.22 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.87K | ± 850.02 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 570.46K | ± 3.44K | ops/s | **fastest** |
| prometheusWriteToNull | 568.49K | ± 19.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.39K | ± 6.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 533.03K | ± 6.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44258.859    ± 227.897  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3310.906    ± 136.357  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4115.016    ± 959.378  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4446.731   ± 1494.928  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47754.870    ± 685.360  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60320.552   ± 1099.799  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51827.001    ± 849.381  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5801.627    ± 233.424  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6199.196     ± 83.489  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5864.036     ± 95.048  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        720.387     ± 15.202  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.559     ± 11.455  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6229.984   ± 3288.252  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3054.724    ± 296.932  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4377.993     ± 29.403  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26866.296    ± 850.023  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27483.967    ± 307.220  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     533029.193   ± 6281.025  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543390.301   ± 6894.133  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     570464.519   ± 3439.628  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     568488.946  ± 19098.249  ops/s
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
