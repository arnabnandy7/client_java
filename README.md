# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-07T07:34:53Z
- **Commit:** [`c29367d`](https://github.com/arnabnandy7/client_java/commit/c29367daf4e6aec49eecf321b8e41553c2e194d5)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.16K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.24K | ± 887.99 | ops/s | 1.1x slower |
| prometheusAdd | 51.02K | ± 560.20 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.82K | ± 715.72 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 8.94 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.36K | ± 29.84 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 175.02 | ops/s | 10x slower |
| openTelemetryAdd | 3.49K | ± 275.74 | ops/s | 18x slower |
| openTelemetryInc | 3.14K | ± 221.27 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.05K | ± 40.29 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.70K | ± 2.16K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 89.19 | ops/s | 1.5x slower |
| prometheusNative | 3.08K | ± 122.78 | ops/s | 2.2x slower |
| openTelemetryClassic | 750.31 | ± 9.16 | ops/s | 8.9x slower |
| openTelemetryExponential | 605.18 | ± 60.01 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.23K | ± 692.39 | ops/s | **fastest** |
| prometheusWriteToNull | 23.92K | ± 1.01K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 493.53K | ± 5.36K | ops/s | **fastest** |
| prometheusWriteToNull | 493.16K | ± 3.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.76K | ± 2.92K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.05K | ± 5.86K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48820.803    ± 715.718  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3494.869    ± 275.735  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3141.583    ± 221.266  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3046.452     ± 40.290  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51015.596    ± 560.205  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64160.999   ± 1204.981  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56237.830    ± 887.994  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6205.788    ± 175.023  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.373      ± 8.937  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6361.395     ± 29.839  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.307      ± 9.161  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        605.182     ± 60.010  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6696.683   ± 2163.978  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3078.880    ± 122.778  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.521     ± 89.194  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24233.136    ± 692.390  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23917.944   ± 1013.803  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480046.928   ± 5860.849  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483761.258   ± 2922.805  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493529.040   ± 5356.580  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493155.340   ± 3350.708  ops/s
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
