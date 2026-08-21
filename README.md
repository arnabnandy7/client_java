# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-21T04:28:43Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.86K | ± 456.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.81K | ± 303.61 | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 323.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.89K | ± 1.30K | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 83.01 | ops/s | 10.0x slower |
| simpleclientAdd | 6.45K | ± 15.90 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 237.15 | ops/s | 10x slower |
| openTelemetryAdd | 3.39K | ± 509.22 | ops/s | 19x slower |
| openTelemetryInc | 3.30K | ± 497.75 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.17K | ± 230.84 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.76K | ± 293.18 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 29.29 | ops/s | 1.1x slower |
| prometheusNative | 3.22K | ± 108.00 | ops/s | 1.5x slower |
| openTelemetryClassic | 776.03 | ± 50.09 | ops/s | 6.1x slower |
| openTelemetryExponential | 584.25 | ± 51.31 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.49K | ± 541.39 | ops/s | **fastest** |
| openMetricsWriteToNull | 24.36K | ± 545.87 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 508.42K | ± 2.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.51K | ± 4.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.34K | ± 3.01K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.27K | ± 7.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48885.389   ± 1298.518  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3392.223    ± 509.223  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3302.533    ± 497.748  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3170.728    ± 230.835  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51355.057    ± 323.880  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65858.603    ± 456.519  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56811.009    ± 303.608  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6451.873     ± 15.902  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6600.453     ± 83.010  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6360.070    ± 237.149  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        776.027     ± 50.093  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        584.246     ± 51.312  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4758.904    ± 293.181  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3218.776    ± 108.004  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4384.281     ± 29.294  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24356.219    ± 545.872  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24491.224    ± 541.391  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475274.812   ± 7696.174  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485343.557   ± 3013.385  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503505.785   ± 4578.656  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508420.886   ± 2121.738  ops/s
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
