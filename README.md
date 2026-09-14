# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-14T09:07:47Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.72K | ± 188.19 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.44K | ± 1.11K | ops/s | 1.2x slower |
| prometheusAdd | 50.34K | ± 455.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.48K | ± 2.01K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 36.32 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 11.00 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 363.76 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.76K | ± 653.56 | ops/s | 17x slower |
| openTelemetryAdd | 3.33K | ± 376.93 | ops/s | 20x slower |
| openTelemetryInc | 3.10K | ± 321.26 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.95K | ± 2.32K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 36.80 | ops/s | 1.3x slower |
| prometheusNative | 3.15K | ± 98.83 | ops/s | 1.9x slower |
| openTelemetryClassic | 753.98 | ± 13.22 | ops/s | 7.9x slower |
| openTelemetryExponential | 687.87 | ± 41.53 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.50K | ± 391.41 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.46K | ± 536.00 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.91K | ± 3.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.05K | ± 3.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.20K | ± 4.89K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 468.04K | ± 7.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49475.124   ± 2010.729  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3327.732    ± 376.927  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3104.356    ± 321.259  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3755.353    ± 653.562  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50335.884    ± 455.386  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65716.080    ± 188.193  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56437.186   ± 1105.949  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6269.253    ± 363.759  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6569.017     ± 36.316  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6339.743     ± 11.000  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        753.981     ± 13.219  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        687.871     ± 41.535  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5951.656   ± 2317.962  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3146.205     ± 98.831  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.017     ± 36.797  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23455.349    ± 535.995  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24501.174    ± 391.405  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468042.524   ± 7803.954  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474202.021   ± 4894.639  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495050.872   ± 3035.163  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502912.543   ± 3923.847  ops/s
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
