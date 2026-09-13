# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-13T08:42:36Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.34K | ± 3.67K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.72K | ± 1.31K | ops/s | 1.2x slower |
| prometheusAdd | 50.95K | ± 391.49 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.71K | ± 1.18K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 40.73 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.27K | ± 112.50 | ops/s | 10x slower |
| simpleclientAdd | 6.17K | ± 252.87 | ops/s | 10x slower |
| openTelemetryAdd | 3.37K | ± 65.78 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.07K | ± 250.10 | ops/s | 21x slower |
| openTelemetryInc | 2.80K | ± 196.17 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.62K | ± 665.82 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 42.67 | ops/s | 1.0x slower |
| prometheusNative | 2.80K | ± 327.38 | ops/s | 1.7x slower |
| openTelemetryClassic | 772.91 | ± 20.69 | ops/s | 6.0x slower |
| openTelemetryExponential | 585.53 | ± 13.16 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.99K | ± 896.34 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.26K | ± 664.92 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.77K | ± 7.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.78K | ± 3.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.52K | ± 5.64K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 465.35K | ± 3.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48709.536   ± 1175.456  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3370.584     ± 65.784  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2802.616    ± 196.169  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3073.119    ± 250.098  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50945.687    ± 391.490  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64335.701   ± 3672.215  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55724.988   ± 1307.035  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6169.363    ± 252.874  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6557.154     ± 40.731  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6269.729    ± 112.500  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        772.910     ± 20.685  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        585.534     ± 13.158  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4616.108    ± 665.818  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2796.073    ± 327.384  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.493     ± 42.667  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23255.218    ± 664.919  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23994.679    ± 896.337  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465346.816   ± 3821.873  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471521.028   ± 5635.069  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487784.023   ± 3281.879  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498773.601   ± 7654.853  ops/s
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
