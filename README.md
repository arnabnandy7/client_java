# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-06T08:21:40Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.06K | ± 2.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.40K | ± 845.90 | ops/s | 1.1x slower |
| prometheusAdd | 47.80K | ± 511.44 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.66K | ± 344.79 | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 69.92 | ops/s | 9.4x slower |
| simpleclientAdd | 5.96K | ± 209.09 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.91K | ± 23.01 | ops/s | 9.8x slower |
| openTelemetryInc | 4.49K | ± 1.44K | ops/s | 13x slower |
| openTelemetryAdd | 3.96K | ± 871.97 | ops/s | 15x slower |
| openTelemetryIncNoLabels | 3.67K | ± 232.97 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.29K | ± 563.08 | ops/s | **fastest** |
| simpleclient | 4.16K | ± 193.80 | ops/s | 1.0x slower |
| prometheusNative | 2.93K | ± 290.13 | ops/s | 1.5x slower |
| openTelemetryClassic | 724.48 | ± 13.65 | ops/s | 5.9x slower |
| openTelemetryExponential | 578.12 | ± 38.94 | ops/s | 7.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.68K | ± 198.92 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.55K | ± 144.13 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 585.22K | ± 5.40K | ops/s | **fastest** |
| prometheusWriteToByteArray | 577.96K | ± 4.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 553.44K | ± 1.54K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 542.20K | ± 4.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44664.469    ± 344.788  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3956.563    ± 871.970  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4494.324   ± 1444.705  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3665.954    ± 232.974  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47798.982    ± 511.444  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58055.803   ± 2336.802  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51404.088    ± 845.903  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5955.729    ± 209.087  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6163.786     ± 69.915  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5908.978     ± 23.010  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        724.477     ± 13.651  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        578.121     ± 38.944  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4293.256    ± 563.076  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2930.987    ± 290.131  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4162.082    ± 193.805  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27553.515    ± 144.132  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27684.634    ± 198.922  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     542195.210   ± 4536.902  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     553439.276   ± 1542.571  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     577960.044   ± 4783.772  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     585216.428   ± 5399.276  ops/s
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
