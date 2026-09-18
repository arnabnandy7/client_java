# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-18T08:37:40Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.49K | ± 38.77 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.25K | ± 193.28 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.70K | ± 331.83 | ops/s | 1.1x slower |
| prometheusAdd | 27.32K | ± 1.83K | ops/s | 1.2x slower |
| simpleclientInc | 6.91K | ± 23.08 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.49K | ± 280.95 | ops/s | 4.9x slower |
| simpleclientAdd | 6.45K | ± 226.53 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 2.78K | ± 220.64 | ops/s | 11x slower |
| openTelemetryInc | 2.44K | ± 78.43 | ops/s | 13x slower |
| openTelemetryAdd | 2.38K | ± 248.77 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.43K | ± 50.54 | ops/s | **fastest** |
| prometheusClassic | 3.14K | ± 368.89 | ops/s | 1.4x slower |
| prometheusNative | 2.27K | ± 152.73 | ops/s | 2.0x slower |
| openTelemetryClassic | 554.51 | ± 25.39 | ops/s | 8.0x slower |
| openTelemetryExponential | 417.48 | ± 21.93 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.18K | ± 166.96 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.07K | ± 287.20 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.79K | ± 4.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 316.84K | ± 4.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 295.22K | ± 2.97K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 291.70K | ± 3.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29703.736    ± 331.830  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2376.557    ± 248.770  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2444.728     ± 78.434  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2776.168    ± 220.640  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27317.087   ± 1829.176  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31488.856     ± 38.766  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31246.972    ± 193.283  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6445.796    ± 226.534  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6906.381     ± 23.079  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6492.302    ± 280.952  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        554.513     ± 25.391  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        417.480     ± 21.935  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3141.100    ± 368.894  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2266.678    ± 152.735  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.908     ± 50.539  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18068.805    ± 287.197  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18183.975    ± 166.962  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     291695.906   ± 3293.055  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     295221.084   ± 2967.312  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     316837.048   ± 4249.617  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318786.680   ± 4207.350  ops/s
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
