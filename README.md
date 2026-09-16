# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-16T08:52:33Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.18K | ± 528.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.33K | ± 927.39 | ops/s | 1.2x slower |
| prometheusAdd | 48.42K | ± 221.29 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.28K | ± 842.42 | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 54.81 | ops/s | 9.6x slower |
| simpleclientAdd | 6.02K | ± 141.46 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.00K | ± 119.62 | ops/s | 9.9x slower |
| openTelemetryAdd | 3.86K | ± 881.38 | ops/s | 15x slower |
| openTelemetryIncNoLabels | 3.50K | ± 216.00 | ops/s | 17x slower |
| openTelemetryInc | 3.50K | ± 249.38 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.90K | ± 416.75 | ops/s | **fastest** |
| simpleclient | 4.20K | ± 50.21 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 155.22 | ops/s | 1.6x slower |
| openTelemetryClassic | 723.45 | ± 15.43 | ops/s | 6.8x slower |
| openTelemetryExponential | 557.76 | ± 15.58 | ops/s | 8.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.59K | ± 358.52 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.54K | ± 88.04 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 591.03K | ± 2.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 579.17K | ± 4.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.97K | ± 17.33K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 542.76K | ± 2.03K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44279.840    ± 842.417  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3862.025    ± 881.381  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3497.128    ± 249.383  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3503.095    ± 216.002  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48419.259    ± 221.290  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59180.104    ± 528.391  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51334.536    ± 927.391  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6017.887    ± 141.455  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6162.975     ± 54.807  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5999.300    ± 119.618  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        723.446     ± 15.429  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.763     ± 15.580  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4896.555    ± 416.754  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2997.136    ± 155.217  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4200.637     ± 50.209  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27544.572     ± 88.038  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27594.378    ± 358.516  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     542759.228   ± 2030.076  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546966.353  ± 17325.871  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     579166.651   ± 4377.164  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     591034.719   ± 2181.986  ops/s
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
