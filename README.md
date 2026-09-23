# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-23T08:57:37Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.81K | ± 93.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.20K | ± 972.75 | ops/s | 1.2x slower |
| prometheusAdd | 51.42K | ± 104.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.33K | ± 1.31K | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 74.10 | ops/s | 9.9x slower |
| simpleclientAdd | 6.39K | ± 109.76 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 32.07 | ops/s | 10x slower |
| openTelemetryAdd | 3.52K | ± 498.19 | ops/s | 19x slower |
| openTelemetryInc | 3.24K | ± 182.83 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.16K | ± 279.57 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.84K | ± 1.63K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 19.08 | ops/s | 1.3x slower |
| prometheusNative | 3.08K | ± 148.24 | ops/s | 1.9x slower |
| openTelemetryClassic | 771.31 | ± 30.96 | ops/s | 7.6x slower |
| openTelemetryExponential | 643.31 | ± 89.64 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.87K | ± 793.02 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.80K | ± 376.15 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.15K | ± 4.66K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.97K | ± 3.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.07K | ± 2.70K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.21K | ± 6.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49326.372   ± 1306.879  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3523.339    ± 498.189  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3244.883    ± 182.828  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3155.172    ± 279.575  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51422.806    ± 104.294  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65814.043     ± 93.523  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56198.511    ± 972.753  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6391.936    ± 109.763  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6618.777     ± 74.099  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6371.820     ± 32.069  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        771.311     ± 30.963  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        643.306     ± 89.636  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5835.928   ± 1631.011  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3075.383    ± 148.235  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4386.388     ± 19.079  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23796.219    ± 376.149  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23871.240    ± 793.017  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468208.525   ± 6380.340  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484073.754   ± 2700.158  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492969.437   ± 3440.224  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494147.431   ± 4664.819  ops/s
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
