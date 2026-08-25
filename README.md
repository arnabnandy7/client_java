# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-25T04:24:46Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.06K | ± 1.29K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.72K | ± 390.83 | ops/s | 1.2x slower |
| prometheusAdd | 47.06K | ± 2.53K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.22K | ± 915.10 | ops/s | 1.4x slower |
| simpleclientInc | 6.19K | ± 9.77 | ops/s | 9.5x slower |
| simpleclientAdd | 6.12K | ± 61.60 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.86K | ± 64.01 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.84K | ± 1.62K | ops/s | 12x slower |
| openTelemetryAdd | 3.97K | ± 907.65 | ops/s | 15x slower |
| openTelemetryInc | 3.78K | ± 186.00 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.56K | ± 2.79K | ops/s | **fastest** |
| simpleclient | 4.08K | ± 186.68 | ops/s | 1.6x slower |
| prometheusNative | 2.99K | ± 154.90 | ops/s | 2.2x slower |
| openTelemetryClassic | 717.78 | ± 17.56 | ops/s | 9.1x slower |
| openTelemetryExponential | 555.51 | ± 40.61 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.63K | ± 156.69 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.29K | ± 317.07 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 580.56K | ± 2.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 558.68K | ± 13.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.23K | ± 11.52K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 528.49K | ± 9.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43216.552    ± 915.100  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3973.967    ± 907.646  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3778.468    ± 185.998  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4839.784   ± 1622.733  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47064.636   ± 2526.440  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59064.445   ± 1286.666  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50719.283    ± 390.835  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6119.970     ± 61.596  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6191.472      ± 9.773  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5857.232     ± 64.010  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.782     ± 17.557  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.505     ± 40.610  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6563.858   ± 2794.732  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2993.876    ± 154.900  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4075.566    ± 186.683  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27292.174    ± 317.073  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27629.031    ± 156.688  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528488.092   ± 9377.512  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538229.865  ± 11521.527  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     558679.252  ± 13174.438  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     580555.819   ± 2314.881  ops/s
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
