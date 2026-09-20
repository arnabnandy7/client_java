# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-20T08:58:37Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 74.63K | ± 1.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.90K | ± 1.17K | ops/s | 1.2x slower |
| prometheusAdd | 58.96K | ± 834.60 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 53.37K | ± 1.91K | ops/s | 1.4x slower |
| simpleclientAdd | 7.51K | ± 137.62 | ops/s | 9.9x slower |
| simpleclientInc | 7.49K | ± 71.19 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 7.46K | ± 248.87 | ops/s | 10x slower |
| openTelemetryInc | 6.43K | ± 1.47K | ops/s | 12x slower |
| openTelemetryIncNoLabels | 5.95K | ± 1.70K | ops/s | 13x slower |
| openTelemetryAdd | 5.54K | ± 1.08K | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.81K | ± 2.03K | ops/s | **fastest** |
| simpleclient | 5.38K | ± 68.05 | ops/s | 1.5x slower |
| prometheusNative | 3.69K | ± 248.49 | ops/s | 2.1x slower |
| openTelemetryClassic | 886.05 | ± 41.75 | ops/s | 8.8x slower |
| openTelemetryExponential | 702.88 | ± 49.17 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 33.95K | ± 479.73 | ops/s | **fastest** |
| prometheusWriteToNull | 33.53K | ± 717.56 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 657.59K | ± 5.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 638.65K | ± 6.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 615.80K | ± 8.72K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 598.18K | ± 8.01K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      53371.216   ± 1909.405  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5537.305   ± 1084.677  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6429.513   ± 1468.309  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5948.436   ± 1700.647  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58963.720    ± 834.600  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      74629.448   ± 1549.146  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63900.731   ± 1169.169  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7507.894    ± 137.617  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7487.646     ± 71.190  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7457.028    ± 248.872  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        886.050     ± 41.754  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        702.883     ± 49.175  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7812.063   ± 2033.105  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3690.172    ± 248.495  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5384.102     ± 68.046  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      33954.177    ± 479.731  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      33533.206    ± 717.556  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     598176.937   ± 8014.483  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     615804.074   ± 8717.219  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     638650.490   ± 6296.282  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     657586.731   ± 5050.408  ops/s
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
