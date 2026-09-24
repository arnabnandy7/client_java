# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-24T08:49:36Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.19K | ± 1.37K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 317.59 | ops/s | 1.1x slower |
| prometheusAdd | 51.15K | ± 550.15 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.00K | ± 1.74K | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 143.36 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.37K | ± 40.30 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 306.18 | ops/s | 10x slower |
| openTelemetryInc | 3.14K | ± 364.87 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.02K | ± 172.35 | ops/s | 21x slower |
| openTelemetryAdd | 2.97K | ± 371.68 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.38K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 52.29 | ops/s | 1.2x slower |
| prometheusNative | 2.91K | ± 232.64 | ops/s | 1.9x slower |
| openTelemetryClassic | 708.16 | ± 11.29 | ops/s | 7.6x slower |
| openTelemetryExponential | 666.62 | ± 32.68 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.20K | ± 719.31 | ops/s | **fastest** |
| prometheusWriteToNull | 23.20K | ± 476.48 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 514.87K | ± 8.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.93K | ± 2.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.30K | ± 3.07K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 479.83K | ± 5.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48004.393   ± 1744.793  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2968.751    ± 371.679  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3138.670    ± 364.874  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3018.138    ± 172.351  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51151.108    ± 550.152  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64188.079   ± 1369.605  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56775.202    ± 317.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6245.604    ± 306.181  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6460.272    ± 143.357  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6374.548     ± 40.295  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.157     ± 11.292  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        666.620     ± 32.684  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5384.502   ± 1469.573  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2906.446    ± 232.643  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4451.187     ± 52.291  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23198.405    ± 719.310  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23197.393    ± 476.476  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479828.183   ± 5058.433  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488304.397   ± 3073.475  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499929.341   ± 2910.459  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     514874.524   ± 8207.944  ops/s
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
