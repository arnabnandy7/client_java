# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-09T05:07:42Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 549.86 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.41K | ± 112.44 | ops/s | 1.2x slower |
| prometheusAdd | 50.95K | ± 602.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.07K | ± 793.93 | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 46.24 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 12.78 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 245.64 | ops/s | 11x slower |
| openTelemetryAdd | 3.50K | ± 206.34 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.37K | ± 476.06 | ops/s | 20x slower |
| openTelemetryInc | 3.34K | ± 22.04 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.56K | ± 521.35 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 40.81 | ops/s | 1.0x slower |
| prometheusNative | 2.96K | ± 279.34 | ops/s | 1.5x slower |
| openTelemetryClassic | 762.80 | ± 22.81 | ops/s | 6.0x slower |
| openTelemetryExponential | 594.33 | ± 28.17 | ops/s | 7.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.18K | ± 553.79 | ops/s | **fastest** |
| prometheusWriteToNull | 23.03K | ± 495.10 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.17K | ± 7.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.88K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.29K | ± 5.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.50K | ± 3.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50074.655    ± 793.926  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3495.211    ± 206.341  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3340.851     ± 22.036  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3369.697    ± 476.064  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50948.876    ± 602.056  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66402.351    ± 549.864  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56410.771    ± 112.438  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6254.791    ± 245.643  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6537.238     ± 46.239  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.720     ± 12.779  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        762.803     ± 22.806  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        594.329     ± 28.166  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4563.369    ± 521.350  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2963.323    ± 279.337  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4356.694     ± 40.809  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24175.137    ± 553.794  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23028.810    ± 495.101  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471502.094   ± 3406.701  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476289.739   ± 5574.378  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491882.162   ± 5267.267  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495167.721   ± 7156.714  ops/s
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
