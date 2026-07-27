# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-27T07:16:29Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.48K | ± 1.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.52K | ± 299.18 | ops/s | 1.1x slower |
| prometheusAdd | 51.51K | ± 204.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.19K | ± 91.72 | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 38.05 | ops/s | 9.9x slower |
| simpleclientAdd | 6.30K | ± 209.96 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.29K | ± 137.07 | ops/s | 10x slower |
| openTelemetryAdd | 3.29K | ± 233.37 | ops/s | 20x slower |
| openTelemetryInc | 3.27K | ± 404.50 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.10K | ± 183.72 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.12K | ± 1.75K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 32.53 | ops/s | 1.4x slower |
| prometheusNative | 3.00K | ± 340.82 | ops/s | 2.0x slower |
| openTelemetryClassic | 809.72 | ± 25.10 | ops/s | 7.6x slower |
| openTelemetryExponential | 600.65 | ± 68.12 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.24K | ± 1.00K | ops/s | **fastest** |
| openMetricsWriteToNull | 24.15K | ± 568.59 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.78K | ± 4.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.53K | ± 5.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.63K | ± 3.16K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 464.74K | ± 5.09K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50190.098     ± 91.718  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3286.581    ± 233.374  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3270.462    ± 404.498  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3097.502    ± 183.717  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51507.603    ± 204.862  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64482.068   ± 1528.167  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56523.328    ± 299.180  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6296.342    ± 209.959  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6533.914     ± 38.051  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6292.746    ± 137.069  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        809.719     ± 25.095  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        600.652     ± 68.116  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6117.794   ± 1749.118  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2995.525    ± 340.825  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.002     ± 32.532  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24152.970    ± 568.593  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24240.809   ± 1002.712  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464735.995   ± 5085.204  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472629.903   ± 3159.903  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486531.917   ± 5369.563  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499784.124   ± 4610.815  ops/s
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
