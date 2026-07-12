# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-12T06:54:10Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.98K | ± 287.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.17K | ± 210.24 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 149.37 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.29K | ± 1.55K | ops/s | 1.3x slower |
| simpleclientAdd | 6.45K | ± 8.49 | ops/s | 10x slower |
| simpleclientInc | 6.41K | ± 93.38 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 25.75 | ops/s | 10x slower |
| openTelemetryAdd | 3.33K | ± 561.35 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.25K | ± 231.74 | ops/s | 20x slower |
| openTelemetryInc | 3.25K | ± 439.29 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.12K | ± 1.62K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 23.14 | ops/s | 1.2x slower |
| prometheusNative | 2.85K | ± 296.74 | ops/s | 1.8x slower |
| openTelemetryClassic | 737.52 | ± 35.30 | ops/s | 6.9x slower |
| openTelemetryExponential | 654.45 | ± 20.37 | ops/s | 7.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.39K | ± 285.28 | ops/s | **fastest** |
| prometheusWriteToNull | 23.28K | ± 668.39 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 511.33K | ± 3.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.90K | ± 4.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.87K | ± 3.41K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 483.86K | ± 6.09K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49291.194   ± 1552.873  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3325.784    ± 561.351  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3245.131    ± 439.287  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3245.745    ± 231.743  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51282.460    ± 149.367  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65976.430    ± 287.482  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57168.338    ± 210.238  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6447.721      ± 8.486  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6411.130     ± 93.385  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6364.702     ± 25.746  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        737.517     ± 35.298  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        654.448     ± 20.371  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5121.774   ± 1622.564  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2846.217    ± 296.744  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4411.374     ± 23.143  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23391.974    ± 285.282  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23277.797    ± 668.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483860.172   ± 6086.678  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485868.761   ± 3408.274  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500900.054   ± 4633.202  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     511331.214   ± 3278.134  ops/s
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
