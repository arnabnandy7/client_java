# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-09T08:36:12Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.37K | ± 777.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.14K | ± 1.32K | ops/s | 1.2x slower |
| prometheusAdd | 47.88K | ± 317.88 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.28K | ± 246.34 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.03K | ± 178.69 | ops/s | 9.8x slower |
| simpleclientInc | 6.00K | ± 212.28 | ops/s | 9.9x slower |
| simpleclientAdd | 5.89K | ± 330.90 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.86K | ± 1.77K | ops/s | 12x slower |
| openTelemetryAdd | 4.60K | ± 872.32 | ops/s | 13x slower |
| openTelemetryInc | 3.83K | ± 109.48 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.42K | ± 647.46 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 36.87 | ops/s | 1.0x slower |
| prometheusNative | 2.78K | ± 116.66 | ops/s | 1.6x slower |
| openTelemetryClassic | 730.34 | ± 26.38 | ops/s | 6.1x slower |
| openTelemetryExponential | 581.13 | ± 7.31 | ops/s | 7.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.39K | ± 211.22 | ops/s | **fastest** |
| prometheusWriteToNull | 26.89K | ± 626.04 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 584.01K | ± 8.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 574.21K | ± 6.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 547.15K | ± 3.25K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 535.77K | ± 4.63K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44275.089    ± 246.338  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4602.570    ± 872.318  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3830.603    ± 109.476  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4863.584   ± 1772.670  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47876.255    ± 317.875  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59374.614    ± 777.657  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51143.902   ± 1319.790  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5889.402    ± 330.903  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       5998.221    ± 212.277  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6032.316    ± 178.691  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        730.343     ± 26.380  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        581.128      ± 7.310  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4423.909    ± 647.457  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2779.707    ± 116.659  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4389.557     ± 36.872  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27390.702    ± 211.217  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      26888.408    ± 626.044  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535767.322   ± 4631.973  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     547148.963   ± 3248.578  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     574210.860   ± 6754.386  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     584013.190   ± 8337.980  ops/s
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
