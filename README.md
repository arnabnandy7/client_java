# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-10T07:30:44Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.04K | ± 318.29 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.71K | ± 375.07 | ops/s | 1.2x slower |
| prometheusAdd | 51.33K | ± 237.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.18K | ± 1.51K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 73.38 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 23.84 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 13.94 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.17K | ± 46.72 | ops/s | 21x slower |
| openTelemetryAdd | 3.17K | ± 422.89 | ops/s | 21x slower |
| openTelemetryInc | 3.15K | ± 266.95 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.72K | ± 683.43 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 121.26 | ops/s | 1.1x slower |
| prometheusNative | 3.17K | ± 79.57 | ops/s | 1.5x slower |
| openTelemetryClassic | 763.81 | ± 29.49 | ops/s | 6.2x slower |
| openTelemetryExponential | 646.69 | ± 72.94 | ops/s | 7.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.46K | ± 115.56 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.25K | ± 721.41 | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.85K | ± 7.04K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.07K | ± 5.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.51K | ± 4.67K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.26K | ± 12.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49176.569   ± 1513.966  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3168.204    ± 422.888  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3152.320    ± 266.954  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3173.760     ± 46.720  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51328.651    ± 237.047  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66042.900    ± 318.286  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56709.883    ± 375.066  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6455.495     ± 23.842  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6545.419     ± 73.381  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6331.832     ± 13.938  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        763.809     ± 29.491  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        646.688     ± 72.942  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4720.581    ± 683.433  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3174.367     ± 79.567  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4351.110    ± 121.256  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23248.937    ± 721.413  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24458.847    ± 115.563  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459261.067  ± 12736.441  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486511.733   ± 4666.360  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492067.358   ± 5900.568  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509848.119   ± 7035.592  ops/s
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
