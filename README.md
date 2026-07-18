# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-18T06:13:17Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.17K | ± 298.96 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 87.92 | ops/s | 1.2x slower |
| prometheusAdd | 51.47K | ± 88.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.58K | ± 1.23K | ops/s | 1.4x slower |
| simpleclientInc | 6.56K | ± 37.21 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.38K | ± 73.55 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 334.52 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.62K | ± 553.98 | ops/s | 18x slower |
| openTelemetryInc | 3.41K | ± 157.52 | ops/s | 19x slower |
| openTelemetryAdd | 3.15K | ± 273.22 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.56K | ± 2.30K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 74.59 | ops/s | 1.5x slower |
| prometheusNative | 2.78K | ± 300.59 | ops/s | 2.4x slower |
| openTelemetryClassic | 729.00 | ± 24.20 | ops/s | 9.0x slower |
| openTelemetryExponential | 593.81 | ± 29.98 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.56K | ± 585.83 | ops/s | **fastest** |
| prometheusWriteToNull | 23.34K | ± 780.70 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.10K | ± 2.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.85K | ± 3.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.90K | ± 6.86K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.87K | ± 4.31K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48578.186   ± 1230.866  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3152.231    ± 273.219  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3410.667    ± 157.520  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3615.707    ± 553.983  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51472.921     ± 88.380  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66173.737    ± 298.960  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56446.043     ± 87.918  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6237.265    ± 334.520  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6558.241     ± 37.207  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6375.245     ± 73.548  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        728.997     ± 24.204  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        593.814     ± 29.976  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6555.362   ± 2304.185  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2779.039    ± 300.590  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.716     ± 74.589  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23563.663    ± 585.834  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23342.692    ± 780.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463866.516   ± 4310.444  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471899.040   ± 6864.658  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488851.581   ± 3371.199  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490098.406   ± 2902.923  ops/s
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
