# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-26T04:31:15Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.58K | ± 39.20 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.23K | ± 254.25 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.51K | ± 1.11K | ops/s | 1.1x slower |
| prometheusAdd | 28.02K | ± 746.71 | ops/s | 1.1x slower |
| simpleclientInc | 6.93K | ± 51.26 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.59K | ± 25.65 | ops/s | 4.8x slower |
| simpleclientAdd | 6.39K | ± 155.71 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 2.69K | ± 42.49 | ops/s | 12x slower |
| openTelemetryInc | 2.64K | ± 83.59 | ops/s | 12x slower |
| openTelemetryAdd | 2.32K | ± 293.14 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.47K | ± 75.61 | ops/s | **fastest** |
| prometheusClassic | 3.31K | ± 125.26 | ops/s | 1.4x slower |
| prometheusNative | 2.38K | ± 169.49 | ops/s | 1.9x slower |
| openTelemetryClassic | 571.63 | ± 20.10 | ops/s | 7.8x slower |
| openTelemetryExponential | 440.33 | ± 13.11 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.24K | ± 68.85 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.19K | ± 191.19 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 326.75K | ± 2.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 323.87K | ± 1.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.54K | ± 1.82K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 298.98K | ± 2.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29510.603   ± 1108.354  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2324.701    ± 293.145  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2644.155     ± 83.590  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2690.936     ± 42.490  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28022.655    ± 746.714  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31578.018     ± 39.204  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31233.530    ± 254.253  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6391.787    ± 155.709  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6926.739     ± 51.258  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6594.338     ± 25.645  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        571.628     ± 20.098  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        440.331     ± 13.106  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3305.497    ± 125.258  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2380.041    ± 169.491  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4473.239     ± 75.610  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18186.055    ± 191.193  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18235.021     ± 68.851  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298978.164   ± 2607.345  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301541.010   ± 1821.857  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     323874.258   ± 1806.781  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     326748.127   ± 2091.017  ops/s
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
