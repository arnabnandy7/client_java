# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-22T04:19:19Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.19K | ± 1.50K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.63K | ± 1.65K | ops/s | 1.2x slower |
| prometheusAdd | 50.61K | ± 731.99 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.40K | ± 9.05K | ops/s | 1.5x slower |
| simpleclientInc | 6.56K | ± 36.48 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 15.30 | ops/s | 10x slower |
| simpleclientAdd | 6.08K | ± 58.64 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.60K | ± 1.00K | ops/s | 18x slower |
| openTelemetryInc | 3.29K | ± 177.43 | ops/s | 20x slower |
| openTelemetryAdd | 3.17K | ± 27.04 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.88K | ± 2.64K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 19.80 | ops/s | 1.4x slower |
| prometheusNative | 2.90K | ± 287.12 | ops/s | 2.0x slower |
| openTelemetryClassic | 760.50 | ± 47.46 | ops/s | 7.7x slower |
| openTelemetryExponential | 702.42 | ± 32.72 | ops/s | 8.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.91K | ± 97.97 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.87K | ± 341.54 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 508.94K | ± 9.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.31K | ± 7.46K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.72K | ± 1.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.60K | ± 2.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43399.402   ± 9046.417  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3171.477     ± 27.036  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3286.186    ± 177.426  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3601.708   ± 1000.392  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50607.026    ± 731.986  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65190.156   ± 1498.545  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54633.055   ± 1650.745  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6075.021     ± 58.643  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6556.382     ± 36.480  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6350.764     ± 15.301  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        760.497     ± 47.462  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        702.416     ± 32.715  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5881.897   ± 2643.545  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2902.249    ± 287.124  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4348.241     ± 19.798  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23873.545    ± 341.539  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23905.780     ± 97.973  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484603.854   ± 2396.403  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488716.315   ± 1360.021  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497305.195   ± 7461.892  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508935.899   ± 9242.250  ops/s
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
