# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-08T04:57:54Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 26.58K | ± 46.35 | ops/s | **fastest** |
| codahaleIncNoLabels | 26.58K | ± 561.72 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.38K | ± 334.41 | ops/s | 1.0x slower |
| prometheusAdd | 25.80K | ± 129.46 | ops/s | 1.0x slower |
| simpleclientInc | 6.75K | ± 26.62 | ops/s | 3.9x slower |
| simpleclientNoLabelsInc | 6.56K | ± 52.64 | ops/s | 4.1x slower |
| simpleclientAdd | 6.41K | ± 86.17 | ops/s | 4.1x slower |
| openTelemetryIncNoLabels | 2.48K | ± 202.49 | ops/s | 11x slower |
| openTelemetryInc | 2.35K | ± 204.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.96K | ± 85.24 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.34K | ± 13.81 | ops/s | **fastest** |
| prometheusClassic | 2.48K | ± 830.04 | ops/s | 1.8x slower |
| prometheusNative | 2.30K | ± 263.91 | ops/s | 1.9x slower |
| openTelemetryClassic | 428.27 | ± 9.81 | ops/s | 10x slower |
| openTelemetryExponential | 319.37 | ± 15.93 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 17.96K | ± 47.00 | ops/s | **fastest** |
| openMetricsWriteToNull | 17.93K | ± 35.23 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 303.93K | ± 2.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 301.72K | ± 1.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 283.30K | ± 1.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 281.47K | ± 2.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26577.780    ± 561.724  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1963.889     ± 85.240  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2345.601    ± 204.851  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2479.244    ± 202.494  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25801.418    ± 129.458  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26579.556     ± 46.349  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26382.855    ± 334.411  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6411.707     ± 86.167  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6750.084     ± 26.616  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6560.073     ± 52.643  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        428.266      ± 9.809  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        319.369     ± 15.929  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2475.035    ± 830.040  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2301.214    ± 263.905  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4342.050     ± 13.808  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17932.778     ± 35.228  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17956.628     ± 46.998  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     281466.909   ± 2483.032  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     283303.924   ± 1192.206  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     301720.427   ± 1076.338  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     303930.506   ± 2969.727  ops/s
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
