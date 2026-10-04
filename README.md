# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-04T09:35:59Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 588.97 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.44K | ± 1.07K | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 113.34 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.99K | ± 1.11K | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 27.26 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 38.53 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 34.09 | ops/s | 10x slower |
| openTelemetryAdd | 3.16K | ± 316.20 | ops/s | 21x slower |
| openTelemetryInc | 3.15K | ± 256.02 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.15K | ± 337.33 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.69K | ± 1.53K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 59.77 | ops/s | 1.3x slower |
| prometheusNative | 2.83K | ± 298.04 | ops/s | 2.0x slower |
| openTelemetryClassic | 747.74 | ± 45.62 | ops/s | 7.6x slower |
| openTelemetryExponential | 594.11 | ± 32.99 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.26K | ± 969.80 | ops/s | **fastest** |
| prometheusWriteToNull | 23.00K | ± 1.09K | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.85K | ± 4.04K | ops/s | **fastest** |
| prometheusWriteToByteArray | 509.38K | ± 1.71K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 490.56K | ± 1.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.01K | ± 4.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48992.798   ± 1107.347  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3163.722    ± 316.196  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3153.081    ± 256.025  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3151.637    ± 337.329  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51240.275    ± 113.342  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66417.189    ± 588.967  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56440.539   ± 1072.140  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6475.332     ± 38.528  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6527.695     ± 27.258  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6363.390     ± 34.093  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        747.743     ± 45.617  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        594.114     ± 32.990  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5692.746   ± 1530.797  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2828.260    ± 298.042  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4489.719     ± 59.775  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24257.917    ± 969.795  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22997.228   ± 1086.048  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484006.522   ± 4467.697  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490556.922   ± 1607.246  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509378.461   ± 1710.348  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512854.577   ± 4038.276  ops/s
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
