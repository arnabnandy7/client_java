# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-15T04:16:35Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 666.40 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.39K | ± 122.94 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 279.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.27K | ± 1.55K | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 84.89 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 10.41 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 217.86 | ops/s | 11x slower |
| openTelemetryInc | 3.46K | ± 447.91 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.16K | ± 479.15 | ops/s | 21x slower |
| openTelemetryAdd | 3.04K | ± 173.02 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.74K | ± 1.36K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 44.65 | ops/s | 1.3x slower |
| prometheusNative | 3.06K | ± 265.08 | ops/s | 1.9x slower |
| openTelemetryClassic | 779.76 | ± 9.02 | ops/s | 7.4x slower |
| openTelemetryExponential | 704.71 | ± 42.92 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.99K | ± 630.11 | ops/s | **fastest** |
| prometheusWriteToNull | 23.93K | ± 552.84 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.28K | ± 4.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.95K | ± 2.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.93K | ± 3.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 460.91K | ± 2.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48273.323   ± 1550.190  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3042.401    ± 173.019  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3455.193    ± 447.911  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3159.048    ± 479.149  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51283.625    ± 279.613  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66404.158    ± 666.402  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56390.074    ± 122.935  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6262.436    ± 217.860  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6598.028     ± 84.894  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6338.984     ± 10.415  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        779.756      ± 9.017  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        704.711     ± 42.924  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5737.516   ± 1361.023  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3058.376    ± 265.078  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.662     ± 44.650  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23986.070    ± 630.112  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23933.921    ± 552.839  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     460908.805   ± 2422.891  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468932.353   ± 3247.015  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481949.496   ± 2466.200  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487282.445   ± 4492.429  ops/s
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
