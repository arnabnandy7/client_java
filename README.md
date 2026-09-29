# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-29T09:35:43Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.57K | ± 53.82 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.64K | ± 976.65 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.66K | ± 934.22 | ops/s | 1.1x slower |
| prometheusAdd | 28.13K | ± 615.17 | ops/s | 1.1x slower |
| simpleclientInc | 6.68K | ± 93.55 | ops/s | 4.7x slower |
| simpleclientAdd | 6.67K | ± 32.67 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.44K | ± 215.11 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 2.77K | ± 349.36 | ops/s | 11x slower |
| openTelemetryInc | 2.62K | ± 146.02 | ops/s | 12x slower |
| openTelemetryAdd | 2.28K | ± 242.87 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.48K | ± 13.85 | ops/s | **fastest** |
| prometheusClassic | 3.15K | ± 634.67 | ops/s | 1.4x slower |
| prometheusNative | 2.04K | ± 59.22 | ops/s | 2.2x slower |
| openTelemetryClassic | 636.72 | ± 65.50 | ops/s | 7.0x slower |
| openTelemetryExponential | 469.61 | ± 27.04 | ops/s | 9.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.31K | ± 91.42 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.28K | ± 73.61 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 324.83K | ± 1.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 322.36K | ± 1.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 301.29K | ± 2.26K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 299.00K | ± 1.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29659.304    ± 934.215  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2275.011    ± 242.872  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2620.490    ± 146.020  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2772.470    ± 349.361  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28128.490    ± 615.171  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31565.588     ± 53.815  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30643.853    ± 976.646  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6666.646     ± 32.671  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6678.662     ± 93.548  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6435.088    ± 215.115  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        636.720     ± 65.495  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        469.613     ± 27.036  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3149.723    ± 634.669  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2035.292     ± 59.216  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4483.617     ± 13.854  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18280.430     ± 73.606  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18307.746     ± 91.417  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     301286.626   ± 2257.057  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298999.089   ± 1790.845  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     322364.433   ± 1522.260  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     324825.831   ± 1864.557  ops/s
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
