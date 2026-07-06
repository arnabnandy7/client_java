# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-06T08:02:52Z
- **Commit:** [`c29367d`](https://github.com/arnabnandy7/client_java/commit/c29367daf4e6aec49eecf321b8e41553c2e194d5)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.00K | ± 1.36K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.15K | ± 456.70 | ops/s | 1.2x slower |
| prometheusAdd | 48.44K | ± 107.97 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.49K | ± 722.23 | ops/s | 1.3x slower |
| simpleclientInc | 6.11K | ± 75.02 | ops/s | 9.7x slower |
| simpleclientAdd | 5.93K | ± 116.41 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.93K | ± 18.49 | ops/s | 10.0x slower |
| openTelemetryInc | 5.23K | ± 1.17K | ops/s | 11x slower |
| openTelemetryAdd | 4.45K | ± 917.07 | ops/s | 13x slower |
| openTelemetryIncNoLabels | 3.67K | ± 200.83 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.43K | ± 1.56K | ops/s | **fastest** |
| simpleclient | 4.15K | ± 88.95 | ops/s | 1.3x slower |
| prometheusNative | 3.14K | ± 31.56 | ops/s | 1.7x slower |
| openTelemetryClassic | 697.05 | ± 10.97 | ops/s | 7.8x slower |
| openTelemetryExponential | 555.86 | ± 41.92 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.58K | ± 145.33 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.39K | ± 108.60 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 554.06K | ± 5.73K | ops/s | **fastest** |
| prometheusWriteToByteArray | 550.45K | ± 1.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 530.00K | ± 2.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 513.52K | ± 7.26K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44494.622    ± 722.231  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4446.935    ± 917.069  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5226.980   ± 1170.647  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3672.831    ± 200.826  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48439.309    ± 107.969  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59003.743   ± 1355.021  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51145.583    ± 456.700  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5932.936    ± 116.407  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6109.578     ± 75.016  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5925.184     ± 18.486  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.052     ± 10.969  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.863     ± 41.920  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5434.456   ± 1564.377  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3136.686     ± 31.565  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4148.723     ± 88.951  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27390.902    ± 108.598  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27582.262    ± 145.334  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513521.870   ± 7255.516  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     529995.374   ± 2074.990  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     550452.161   ± 1890.041  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     554064.705   ± 5729.820  ops/s
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
