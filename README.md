# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-02T06:53:09Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.63K | ± 2.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.86K | ± 358.96 | ops/s | 1.1x slower |
| prometheusAdd | 51.18K | ± 431.27 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.11K | ± 1.12K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 8.28 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.34K | ± 6.70 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 178.67 | ops/s | 10x slower |
| openTelemetryInc | 3.42K | ± 368.05 | ops/s | 19x slower |
| openTelemetryAdd | 3.32K | ± 269.51 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.08K | ± 212.14 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.48K | ± 1.10K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 37.05 | ops/s | 1.5x slower |
| prometheusNative | 3.21K | ± 93.85 | ops/s | 2.0x slower |
| openTelemetryClassic | 738.17 | ± 30.28 | ops/s | 8.8x slower |
| openTelemetryExponential | 634.56 | ± 44.20 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.64K | ± 1.09K | ops/s | **fastest** |
| prometheusWriteToNull | 23.35K | ± 510.54 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.47K | ± 7.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.16K | ± 6.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.02K | ± 3.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.80K | ± 6.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48112.111   ± 1115.698  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3322.387    ± 269.507  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3421.913    ± 368.054  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3075.026    ± 212.140  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51180.235    ± 431.265  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63631.450   ± 2038.576  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56857.829    ± 358.961  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6328.062    ± 178.672  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.230      ± 8.285  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6339.327      ± 6.702  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        738.167     ± 30.277  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        634.563     ± 44.200  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6481.652   ± 1100.157  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3211.303     ± 93.852  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4438.018     ± 37.051  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23639.641   ± 1094.156  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23350.749    ± 510.541  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473803.258   ± 6466.883  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482017.131   ± 3468.967  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496157.222   ± 6282.880  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502471.260   ± 7531.589  ops/s
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
