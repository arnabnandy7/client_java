# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-14T06:25:55Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.94K | ± 1.97K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.67K | ± 258.05 | ops/s | 1.1x slower |
| prometheusAdd | 51.38K | ± 183.38 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.42K | ± 1.22K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 61.30 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.38K | ± 20.19 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 341.64 | ops/s | 10x slower |
| openTelemetryInc | 3.39K | ± 288.32 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.16K | ± 260.01 | ops/s | 20x slower |
| openTelemetryAdd | 2.97K | ± 49.48 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.82K | ± 2.39K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 33.43 | ops/s | 1.5x slower |
| prometheusNative | 2.67K | ± 114.63 | ops/s | 2.6x slower |
| openTelemetryClassic | 750.44 | ± 17.37 | ops/s | 9.1x slower |
| openTelemetryExponential | 629.46 | ± 95.30 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.70K | ± 499.92 | ops/s | **fastest** |
| prometheusWriteToNull | 23.50K | ± 440.77 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 504.64K | ± 3.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 502.97K | ± 3.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.04K | ± 3.30K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 475.07K | ± 3.90K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49421.302   ± 1215.700  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2974.335     ± 49.477  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3392.748    ± 288.324  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3162.422    ± 260.013  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51376.734    ± 183.379  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63936.211   ± 1967.128  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56671.576    ± 258.046  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6230.182    ± 341.641  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6647.337     ± 61.301  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6379.705     ± 20.188  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.440     ± 17.370  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        629.462     ± 95.297  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6820.304   ± 2386.649  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2671.614    ± 114.634  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4418.980     ± 33.434  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23704.127    ± 499.921  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23499.438    ± 440.772  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475069.987   ± 3904.267  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479040.627   ± 3297.563  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502967.707   ± 3372.141  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504636.033   ± 3015.367  ops/s
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
