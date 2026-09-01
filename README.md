# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-01T08:57:47Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.47K | ± 807.19 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.12K | ± 820.50 | ops/s | 1.2x slower |
| prometheusAdd | 48.41K | ± 63.34 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.17K | ± 263.77 | ops/s | 1.4x slower |
| simpleclientInc | 6.19K | ± 6.68 | ops/s | 9.8x slower |
| simpleclientAdd | 5.98K | ± 213.82 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.88K | ± 64.60 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.94K | ± 1.18K | ops/s | 12x slower |
| openTelemetryAdd | 3.76K | ± 833.05 | ops/s | 16x slower |
| openTelemetryInc | 3.45K | ± 271.43 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.32K | ± 1.54K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 72.03 | ops/s | 1.2x slower |
| prometheusNative | 2.84K | ± 230.28 | ops/s | 1.9x slower |
| openTelemetryClassic | 669.39 | ± 2.28 | ops/s | 8.0x slower |
| openTelemetryExponential | 526.51 | ± 7.62 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.22K | ± 271.66 | ops/s | **fastest** |
| prometheusWriteToNull | 27.19K | ± 248.59 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 557.36K | ± 7.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.43K | ± 3.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 524.17K | ± 7.15K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 518.50K | ± 4.69K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44171.422    ± 263.765  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3761.757    ± 833.051  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3448.213    ± 271.429  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4944.745   ± 1175.528  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48410.255     ± 63.344  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60465.697    ± 807.189  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51118.430    ± 820.496  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5984.427    ± 213.817  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6193.358      ± 6.683  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5875.954     ± 64.603  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        669.390      ± 2.285  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.511      ± 7.622  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5322.721   ± 1543.188  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2835.359    ± 230.282  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4351.253     ± 72.030  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27219.164    ± 271.655  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27186.723    ± 248.589  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     518503.118   ± 4686.203  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     524172.259   ± 7148.983  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548425.891   ± 3435.523  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     557364.532   ± 7403.228  ops/s
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
