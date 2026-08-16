# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-16T04:25:40Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.12K | ± 410.79 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.37K | ± 2.58K | ops/s | 1.2x slower |
| prometheusAdd | 51.00K | ± 709.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.06K | ± 1.65K | ops/s | 1.4x slower |
| simpleclientInc | 6.61K | ± 53.45 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.36K | ± 28.22 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 294.97 | ops/s | 10x slower |
| openTelemetryAdd | 3.55K | ± 442.63 | ops/s | 19x slower |
| openTelemetryInc | 3.35K | ± 411.57 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.12K | ± 164.62 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 66.84 | ops/s | 1.3x slower |
| prometheusNative | 2.75K | ± 271.36 | ops/s | 2.0x slower |
| openTelemetryClassic | 717.38 | ± 27.43 | ops/s | 7.7x slower |
| openTelemetryExponential | 699.14 | ± 62.36 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.66K | ± 664.31 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.17K | ± 1.17K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.65K | ± 5.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.18K | ± 3.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.06K | ± 3.79K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.17K | ± 8.70K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48062.579   ± 1646.017  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3545.365    ± 442.630  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3346.594    ± 411.575  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3123.095    ± 164.624  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51002.982    ± 709.252  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66115.178    ± 410.788  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55367.610   ± 2580.506  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6326.438    ± 294.975  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6612.031     ± 53.449  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6362.556     ± 28.224  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.382     ± 27.429  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        699.141     ± 62.361  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5545.303   ± 1069.256  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2746.261    ± 271.355  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4431.219     ± 66.837  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23167.121   ± 1169.112  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23663.395    ± 664.307  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474171.420   ± 8700.905  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480062.499   ± 3786.128  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490179.172   ± 3257.604  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491653.053   ± 5747.302  ops/s
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
