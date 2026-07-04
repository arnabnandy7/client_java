# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-04T07:11:55Z
- **Commit:** [`c29367d`](https://github.com/arnabnandy7/client_java/commit/c29367daf4e6aec49eecf321b8e41553c2e194d5)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.79K | ± 134.08 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.04K | ± 1.21K | ops/s | 1.2x slower |
| prometheusAdd | 50.71K | ± 656.94 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.20K | ± 135.75 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 93.45 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.27K | ± 89.86 | ops/s | 10x slower |
| simpleclientAdd | 6.14K | ± 244.72 | ops/s | 11x slower |
| openTelemetryInc | 3.44K | ± 443.21 | ops/s | 19x slower |
| openTelemetryAdd | 3.26K | ± 476.80 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.15K | ± 270.49 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.77K | ± 1.22K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 60.34 | ops/s | 1.3x slower |
| prometheusNative | 2.96K | ± 335.25 | ops/s | 1.9x slower |
| openTelemetryClassic | 790.09 | ± 39.66 | ops/s | 7.3x slower |
| openTelemetryExponential | 618.08 | ± 75.04 | ops/s | 9.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.06K | ± 780.23 | ops/s | **fastest** |
| prometheusWriteToNull | 22.92K | ± 587.98 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 500.09K | ± 3.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.51K | ± 3.64K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.17K | ± 2.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.34K | ± 3.06K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49197.820    ± 135.754  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3259.305    ± 476.801  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3440.990    ± 443.211  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3152.230    ± 270.488  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50707.479    ± 656.937  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65791.317    ± 134.081  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56039.634   ± 1205.303  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6137.059    ± 244.716  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6580.075     ± 93.449  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6268.405     ± 89.860  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        790.089     ± 39.657  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        618.077     ± 75.039  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5770.257   ± 1219.740  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2959.713    ± 335.255  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4464.448     ± 60.339  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24057.316    ± 780.226  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22924.250    ± 587.978  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477341.764   ± 3062.264  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483173.471   ± 2100.679  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499505.166   ± 3644.158  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500088.347   ± 3045.785  ops/s
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
