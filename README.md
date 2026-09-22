# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-22T08:55:32Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.57K | ± 3.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.81K | ± 1.03K | ops/s | 1.1x slower |
| prometheusAdd | 62.72K | ± 1.33K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.19K | ± 439.89 | ops/s | 1.3x slower |
| simpleclientInc | 8.00K | ± 123.52 | ops/s | 9.4x slower |
| simpleclientAdd | 7.82K | ± 41.74 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.77K | ± 257.68 | ops/s | 9.7x slower |
| openTelemetryInc | 6.18K | ± 1.49K | ops/s | 12x slower |
| openTelemetryAdd | 6.08K | ± 993.39 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.96K | ± 332.24 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.64K | ± 1.37K | ops/s | **fastest** |
| simpleclient | 5.43K | ± 16.38 | ops/s | 1.2x slower |
| prometheusNative | 3.82K | ± 284.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 952.48 | ± 14.83 | ops/s | 7.0x slower |
| openTelemetryExponential | 721.71 | ± 16.39 | ops/s | 9.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 35.48K | ± 416.35 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.00K | ± 398.53 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 704.39K | ± 7.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 687.92K | ± 5.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 658.65K | ± 4.71K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 650.87K | ± 4.88K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57186.185    ± 439.891  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       6077.097    ± 993.390  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6177.293   ± 1489.708  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4960.759    ± 332.237  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62721.511   ± 1328.601  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75573.348   ± 3568.977  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66813.690   ± 1030.221  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7817.426     ± 41.739  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7999.692    ± 123.515  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7773.474    ± 257.684  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        952.476     ± 14.831  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        721.708     ± 16.392  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6635.076   ± 1373.401  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3822.430    ± 284.636  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5431.434     ± 16.380  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35003.449    ± 398.529  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35476.123    ± 416.354  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     650873.356   ± 4875.835  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     658645.406   ± 4711.791  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     687919.227   ± 5087.779  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     704386.098   ± 7822.792  ops/s
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
