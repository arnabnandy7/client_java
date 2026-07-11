# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-11T06:38:32Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.24K | ± 3.85K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.71K | ± 415.75 | ops/s | 1.1x slower |
| prometheusAdd | 51.49K | ± 133.62 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 46.15K | ± 1.32K | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 31.67 | ops/s | 9.7x slower |
| simpleclientAdd | 6.47K | ± 20.50 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.33K | ± 50.53 | ops/s | 10.0x slower |
| openTelemetryInc | 3.58K | ± 284.80 | ops/s | 18x slower |
| openTelemetryAdd | 3.52K | ± 180.37 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.30K | ± 25.40 | ops/s | 19x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.04K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.29K | ± 178.45 | ops/s | 1.4x slower |
| prometheusNative | 2.91K | ± 302.66 | ops/s | 2.1x slower |
| openTelemetryClassic | 765.48 | ± 25.67 | ops/s | 7.9x slower |
| openTelemetryExponential | 718.43 | ± 113.14 | ops/s | 8.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.02K | ± 516.94 | ops/s | **fastest** |
| prometheusWriteToNull | 23.29K | ± 446.21 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.39K | ± 5.48K | ops/s | **fastest** |
| prometheusWriteToByteArray | 498.70K | ± 5.00K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.18K | ± 4.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.07K | ± 2.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46151.942   ± 1319.114  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3516.372    ± 180.366  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3578.489    ± 284.797  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3300.419     ± 25.396  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51485.398    ± 133.619  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63236.053   ± 3850.097  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56712.496    ± 415.753  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6466.558     ± 20.503  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6526.625     ± 31.671  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6334.585     ± 50.530  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        765.480     ± 25.669  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        718.432    ± 113.141  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6038.792   ± 1310.683  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2908.851    ± 302.660  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4292.060    ± 178.448  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24024.265    ± 516.941  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23288.404    ± 446.212  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474071.849   ± 2300.607  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481181.212   ± 4265.214  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498702.083   ± 5000.864  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503388.566   ± 5476.939  ops/s
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
