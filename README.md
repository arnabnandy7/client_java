# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-17T04:25:32Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.55K | ± 30.40 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.82K | ± 1.06K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.07K | ± 1.39K | ops/s | 1.1x slower |
| prometheusAdd | 27.52K | ± 1.39K | ops/s | 1.1x slower |
| simpleclientInc | 6.89K | ± 39.71 | ops/s | 4.6x slower |
| simpleclientAdd | 6.59K | ± 53.78 | ops/s | 4.8x slower |
| simpleclientNoLabelsInc | 6.40K | ± 212.71 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 3.00K | ± 297.77 | ops/s | 11x slower |
| openTelemetryInc | 2.65K | ± 101.63 | ops/s | 12x slower |
| openTelemetryAdd | 2.30K | ± 375.58 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.37K | ± 78.09 | ops/s | **fastest** |
| prometheusClassic | 3.34K | ± 1.84K | ops/s | 1.3x slower |
| prometheusNative | 2.24K | ± 129.39 | ops/s | 2.0x slower |
| openTelemetryClassic | 613.61 | ± 33.04 | ops/s | 7.1x slower |
| openTelemetryExponential | 445.80 | ± 7.97 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.15K | ± 89.53 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.14K | ± 71.94 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.78K | ± 1.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.96K | ± 2.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 292.58K | ± 2.81K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 292.06K | ± 2.01K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29072.888   ± 1390.023  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2298.342    ± 375.576  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2652.175    ± 101.630  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3003.148    ± 297.775  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27523.727   ± 1386.099  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31547.781     ± 30.403  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30818.972   ± 1058.788  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6589.429     ± 53.778  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6893.798     ± 39.706  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6403.079    ± 212.715  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        613.615     ± 33.042  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        445.796      ± 7.966  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3340.888   ± 1838.956  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2239.553    ± 129.389  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4374.913     ± 78.086  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18141.393     ± 71.936  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18145.120     ± 89.535  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     292056.078   ± 2013.569  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     292580.290   ± 2806.253  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313956.011   ± 2922.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318779.509   ± 1970.950  ops/s
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
