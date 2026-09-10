# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-10T08:32:14Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.55K | ± 1.50K | ops/s | **fastest** |
| codahaleIncNoLabels | 29.73K | ± 696.50 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 29.57K | ± 864.43 | ops/s | 1.0x slower |
| prometheusAdd | 28.45K | ± 94.95 | ops/s | 1.1x slower |
| simpleclientInc | 6.81K | ± 72.18 | ops/s | 4.5x slower |
| simpleclientAdd | 6.67K | ± 58.72 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.49K | ± 294.78 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 2.81K | ± 215.61 | ops/s | 11x slower |
| openTelemetryInc | 2.53K | ± 205.51 | ops/s | 12x slower |
| openTelemetryAdd | 2.51K | ± 252.77 | ops/s | 12x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 35.66 | ops/s | **fastest** |
| prometheusClassic | 2.89K | ± 364.11 | ops/s | 1.6x slower |
| prometheusNative | 2.33K | ± 295.18 | ops/s | 1.9x slower |
| openTelemetryClassic | 568.05 | ± 25.31 | ops/s | 7.9x slower |
| openTelemetryExponential | 431.68 | ± 13.98 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 18.32K | ± 56.20 | ops/s | **fastest** |
| prometheusWriteToNull | 18.26K | ± 139.61 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 322.30K | ± 1.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 319.83K | ± 1.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 298.48K | ± 2.09K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.14K | ± 1.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29733.132    ± 696.497  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2506.892    ± 252.770  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2532.914    ± 205.513  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2810.955    ± 215.609  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28447.744     ± 94.946  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30550.777   ± 1499.375  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29568.776    ± 864.432  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6669.172     ± 58.722  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6810.935     ± 72.176  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6485.705    ± 294.778  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        568.051     ± 25.309  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        431.677     ± 13.978  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2888.680    ± 364.107  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2332.776    ± 295.182  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4498.322     ± 35.663  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18323.397     ± 56.199  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18259.674    ± 139.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295140.973   ± 1597.381  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298482.518   ± 2089.402  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     319829.538   ± 1200.318  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     322301.288   ± 1957.747  ops/s
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
