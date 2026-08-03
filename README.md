# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-03T07:08:50Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.00K | ± 982.94 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 372.81 | ops/s | 1.1x slower |
| prometheusAdd | 50.52K | ± 735.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.85K | ± 1.37K | ops/s | 1.3x slower |
| simpleclientInc | 6.51K | ± 117.03 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.34K | ± 11.94 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 181.83 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.37K | ± 113.28 | ops/s | 19x slower |
| openTelemetryInc | 3.12K | ± 78.24 | ops/s | 21x slower |
| openTelemetryAdd | 3.02K | ± 186.07 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.64K | ± 921.80 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 80.01 | ops/s | 1.5x slower |
| prometheusNative | 2.79K | ± 353.09 | ops/s | 2.4x slower |
| openTelemetryClassic | 776.43 | ± 20.12 | ops/s | 8.6x slower |
| openTelemetryExponential | 621.27 | ± 96.20 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.79K | ± 499.77 | ops/s | **fastest** |
| prometheusWriteToNull | 23.02K | ± 483.99 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.26K | ± 7.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.84K | ± 1.62K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.91K | ± 4.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.65K | ± 2.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48854.472   ± 1374.072  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3015.171    ± 186.074  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3117.630     ± 78.236  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3370.419    ± 113.282  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50522.170    ± 735.041  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64996.362    ± 982.943  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56849.913    ± 372.809  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6297.546    ± 181.828  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6513.632    ± 117.029  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.053     ± 11.942  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        776.426     ± 20.123  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        621.274     ± 96.204  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6639.076    ± 921.797  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2791.833    ± 353.093  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4428.888     ± 80.011  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23794.464    ± 499.770  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23018.481    ± 483.992  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464653.120   ± 2849.065  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471906.975   ± 4894.978  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482840.397   ± 1619.321  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490259.884   ± 7306.360  ops/s
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
