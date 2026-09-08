# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-08T08:29:02Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.58K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.96K | ± 148.02 | ops/s | 1.1x slower |
| prometheusAdd | 51.40K | ± 447.35 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.08K | ± 1.75K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 97.47 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.43K | ± 125.20 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 224.58 | ops/s | 10x slower |
| openTelemetryInc | 3.52K | ± 316.85 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.15K | ± 111.97 | ops/s | 20x slower |
| openTelemetryAdd | 3.06K | ± 226.95 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.77K | ± 738.34 | ops/s | **fastest** |
| simpleclient | 4.38K | ± 18.51 | ops/s | 1.1x slower |
| prometheusNative | 2.74K | ± 347.14 | ops/s | 1.7x slower |
| openTelemetryClassic | 777.66 | ± 40.85 | ops/s | 6.1x slower |
| openTelemetryExponential | 660.93 | ± 79.46 | ops/s | 7.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.64K | ± 768.61 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.41K | ± 261.50 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 475.13K | ± 4.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 474.24K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.14K | ± 4.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 452.27K | ± 6.18K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49080.706   ± 1754.029  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3058.712    ± 226.951  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3517.366    ± 316.853  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3151.570    ± 111.968  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51402.028    ± 447.347  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64579.957   ± 1319.019  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56962.274    ± 148.022  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6308.494    ± 224.583  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6560.950     ± 97.474  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6433.339    ± 125.203  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        777.658     ± 40.849  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        660.927     ± 79.462  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4767.600    ± 738.336  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2738.158    ± 347.135  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4381.929     ± 18.507  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23407.204    ± 261.502  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23643.285    ± 768.612  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459135.889   ± 4229.292  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     452267.614   ± 6178.962  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474243.316   ± 4120.398  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     475125.259   ± 4561.423  ops/s
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
