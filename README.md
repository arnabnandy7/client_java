# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-03T09:13:32Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 31.95K | ± 222.80 | ops/s | **fastest** |
| prometheusInc | 31.51K | ± 1.01K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 31.03K | ± 220.36 | ops/s | 1.0x slower |
| prometheusAdd | 30.11K | ± 186.41 | ops/s | 1.1x slower |
| simpleclientInc | 7.90K | ± 21.30 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 7.70K | ± 37.13 | ops/s | 4.1x slower |
| simpleclientAdd | 7.54K | ± 145.62 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 2.65K | ± 122.40 | ops/s | 12x slower |
| openTelemetryInc | 2.60K | ± 82.75 | ops/s | 12x slower |
| openTelemetryAdd | 2.16K | ± 218.10 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.05K | ± 45.67 | ops/s | **fastest** |
| prometheusClassic | 2.70K | ± 1.51K | ops/s | 1.9x slower |
| prometheusNative | 2.58K | ± 262.61 | ops/s | 2.0x slower |
| openTelemetryClassic | 486.08 | ± 19.38 | ops/s | 10x slower |
| openTelemetryExponential | 367.16 | ± 15.33 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 20.64K | ± 205.29 | ops/s | **fastest** |
| openMetricsWriteToNull | 20.59K | ± 156.17 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 321.47K | ± 2.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 319.63K | ± 2.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 303.45K | ± 1.38K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 301.14K | ± 1.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31948.712    ± 222.802  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2160.820    ± 218.103  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2601.511     ± 82.751  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2653.070    ± 122.405  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      30110.535    ± 186.408  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31512.918   ± 1011.790  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31028.480    ± 220.357  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7537.125    ± 145.616  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7898.909     ± 21.302  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7704.635     ± 37.130  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        486.077     ± 19.383  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        367.165     ± 15.334  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2700.059   ± 1512.934  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2580.390    ± 262.613  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5050.089     ± 45.671  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      20594.899    ± 156.173  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      20640.276    ± 205.292  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     301135.562   ± 1791.406  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     303445.837   ± 1383.632  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     319626.417   ± 2646.340  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     321471.567   ± 2369.562  ops/s
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
