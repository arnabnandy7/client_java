# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-03T08:33:53Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.47K | ± 467.92 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.51K | ± 473.17 | ops/s | 1.2x slower |
| prometheusAdd | 51.07K | ± 351.44 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.18K | ± 7.31K | ops/s | 1.5x slower |
| simpleclientInc | 6.61K | ± 60.87 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.37K | ± 30.41 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 172.44 | ops/s | 10x slower |
| openTelemetryAdd | 3.52K | ± 284.74 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.34K | ± 349.65 | ops/s | 20x slower |
| openTelemetryInc | 2.99K | ± 197.28 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.29K | ± 1.85K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 30.76 | ops/s | 1.7x slower |
| prometheusNative | 2.94K | ± 290.89 | ops/s | 2.5x slower |
| openTelemetryClassic | 747.23 | ± 9.42 | ops/s | 9.8x slower |
| openTelemetryExponential | 703.91 | ± 91.41 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.80K | ± 334.95 | ops/s | **fastest** |
| prometheusWriteToNull | 23.18K | ± 457.19 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.88K | ± 4.66K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.36K | ± 9.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.50K | ± 3.12K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 469.59K | ± 8.95K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43178.453   ± 7314.610  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3519.534    ± 284.736  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2986.836    ± 197.281  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3340.895    ± 349.647  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51072.821    ± 351.440  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65466.124    ± 467.918  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55513.674    ± 473.172  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6331.539    ± 172.443  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6612.754     ± 60.869  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6371.222     ± 30.412  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        747.232      ± 9.418  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        703.911     ± 91.409  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7291.059   ± 1846.939  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2938.558    ± 290.893  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4401.807     ± 30.759  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23804.171    ± 334.948  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23183.131    ± 457.193  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469591.712   ± 8948.020  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475497.717   ± 3118.447  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494362.715   ± 9358.378  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509883.024   ± 4663.081  ops/s
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
