# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-07T09:48:32Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.03K | ± 223.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 1.35K | ops/s | 1.2x slower |
| prometheusAdd | 51.07K | ± 631.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.71K | ± 1.52K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 49.42 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 23.35 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 380.59 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.59K | ± 147.27 | ops/s | 18x slower |
| openTelemetryAdd | 3.14K | ± 260.04 | ops/s | 21x slower |
| openTelemetryInc | 3.02K | ± 378.02 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.41K | ± 28.47 | ops/s | **fastest** |
| prometheusClassic | 4.31K | ± 526.36 | ops/s | 1.0x slower |
| prometheusNative | 2.97K | ± 178.22 | ops/s | 1.5x slower |
| openTelemetryClassic | 787.10 | ± 27.02 | ops/s | 5.6x slower |
| openTelemetryExponential | 657.99 | ± 13.10 | ops/s | 6.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.94K | ± 1.07K | ops/s | **fastest** |
| prometheusWriteToNull | 23.76K | ± 794.39 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.52K | ± 3.25K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.43K | ± 5.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.32K | ± 3.20K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.50K | ± 6.07K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49705.383   ± 1515.293  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3135.817    ± 260.040  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3023.613    ± 378.022  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3594.588    ± 147.268  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51072.900    ± 631.688  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66029.087    ± 223.517  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56252.619   ± 1352.153  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6215.475    ± 380.586  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.869     ± 49.425  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.143     ± 23.353  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        787.096     ± 27.020  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        657.991     ± 13.101  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4310.565    ± 526.355  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2972.353    ± 178.218  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4414.060     ± 28.471  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23941.939   ± 1067.092  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23763.665    ± 794.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471502.158   ± 6068.174  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479318.666   ± 3202.540  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486432.123   ± 5102.656  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497515.111   ± 3248.244  ops/s
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
