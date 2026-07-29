# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-29T06:47:42Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 30.35K | ± 1.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.32K | ± 674.32 | ops/s | 1.0x slower |
| prometheusInc | 30.05K | ± 215.98 | ops/s | 1.0x slower |
| prometheusAdd | 29.26K | ± 102.67 | ops/s | 1.0x slower |
| simpleclientInc | 7.63K | ± 37.40 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 7.47K | ± 26.68 | ops/s | 4.1x slower |
| simpleclientAdd | 7.32K | ± 148.00 | ops/s | 4.1x slower |
| openTelemetryAdd | 2.52K | ± 375.08 | ops/s | 12x slower |
| openTelemetryInc | 2.51K | ± 277.69 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 2.50K | ± 306.38 | ops/s | 12x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.82K | ± 56.68 | ops/s | **fastest** |
| prometheusClassic | 2.74K | ± 295.54 | ops/s | 1.8x slower |
| prometheusNative | 2.00K | ± 325.21 | ops/s | 2.4x slower |
| openTelemetryClassic | 456.92 | ± 6.44 | ops/s | 11x slower |
| openTelemetryExponential | 349.81 | ± 10.13 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 20.02K | ± 235.81 | ops/s | **fastest** |
| prometheusWriteToNull | 19.85K | ± 235.10 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 323.81K | ± 6.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 321.25K | ± 2.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 304.62K | ± 5.93K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.83K | ± 3.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30354.802   ± 1202.458  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2515.745    ± 375.083  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2507.909    ± 277.691  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2499.680    ± 306.385  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29261.261    ± 102.673  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30051.024    ± 215.985  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30322.719    ± 674.325  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7315.968    ± 148.004  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7630.984     ± 37.396  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7466.881     ± 26.677  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        456.919      ± 6.440  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        349.807     ± 10.133  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2735.503    ± 295.543  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1996.703    ± 325.214  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4824.696     ± 56.678  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      20022.079    ± 235.806  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      19849.856    ± 235.102  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297830.653   ± 3294.191  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     304619.874   ± 5926.681  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     321253.586   ± 2151.235  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     323811.322   ± 6357.520  ops/s
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
