# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-05T06:39:56Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 36.64K | ± 832.22 | ops/s | **fastest** |
| codahaleIncNoLabels | 36.05K | ± 2.12K | ops/s | 1.0x slower |
| prometheusInc | 35.46K | ± 593.18 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 34.21K | ± 633.68 | ops/s | 1.1x slower |
| simpleclientInc | 9.24K | ± 112.05 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 9.03K | ± 159.02 | ops/s | 4.1x slower |
| simpleclientAdd | 9.01K | ± 185.97 | ops/s | 4.1x slower |
| openTelemetryAdd | 2.47K | ± 410.15 | ops/s | 15x slower |
| openTelemetryIncNoLabels | 2.17K | ± 294.43 | ops/s | 17x slower |
| openTelemetryInc | 2.09K | ± 319.38 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 6.12K | ± 96.27 | ops/s | **fastest** |
| prometheusClassic | 2.64K | ± 577.65 | ops/s | 2.3x slower |
| prometheusNative | 2.18K | ± 120.52 | ops/s | 2.8x slower |
| openTelemetryClassic | 561.34 | ± 109.29 | ops/s | 11x slower |
| openTelemetryExponential | 383.00 | ± 58.31 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 25.61K | ± 51.20 | ops/s | **fastest** |
| openMetricsWriteToNull | 25.22K | ± 969.27 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 367.49K | ± 3.96K | ops/s | **fastest** |
| prometheusWriteToNull | 361.16K | ± 3.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 346.37K | ± 4.51K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 346.17K | ± 3.13K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      36046.705   ± 2119.901  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2470.442    ± 410.149  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2085.752    ± 319.384  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2172.720    ± 294.428  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36637.755    ± 832.221  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35457.159    ± 593.177  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      34208.824    ± 633.677  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9007.511    ± 185.968  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9243.465    ± 112.048  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9032.521    ± 159.018  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        561.339    ± 109.285  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        382.995     ± 58.312  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2638.233    ± 577.647  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2177.618    ± 120.524  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6117.122     ± 96.271  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      25219.800    ± 969.270  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      25605.219     ± 51.196  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     346174.814   ± 3132.803  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     346373.453   ± 4507.383  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     367494.187   ± 3962.286  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     361155.583   ± 3238.984  ops/s
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
