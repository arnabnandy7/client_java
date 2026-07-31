# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-31T07:00:35Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 32.00K | ± 96.98 | ops/s | **fastest** |
| prometheusInc | 31.52K | ± 1.02K | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 31.06K | ± 46.18 | ops/s | 1.0x slower |
| prometheusAdd | 29.94K | ± 257.60 | ops/s | 1.1x slower |
| simpleclientInc | 7.84K | ± 78.37 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 7.70K | ± 17.18 | ops/s | 4.2x slower |
| simpleclientAdd | 7.61K | ± 73.58 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 2.56K | ± 206.22 | ops/s | 13x slower |
| openTelemetryInc | 2.49K | ± 352.61 | ops/s | 13x slower |
| openTelemetryAdd | 2.30K | ± 310.95 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.09K | ± 23.55 | ops/s | **fastest** |
| prometheusClassic | 4.82K | ± 2.37K | ops/s | 1.1x slower |
| prometheusNative | 2.09K | ± 551.33 | ops/s | 2.4x slower |
| openTelemetryClassic | 503.65 | ± 37.44 | ops/s | 10x slower |
| openTelemetryExponential | 346.25 | ± 5.30 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 20.65K | ± 113.21 | ops/s | **fastest** |
| openMetricsWriteToNull | 20.64K | ± 108.48 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 327.55K | ± 2.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 325.19K | ± 3.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 302.41K | ± 3.01K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 301.40K | ± 3.19K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      32004.127     ± 96.982  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2295.817    ± 310.949  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2492.251    ± 352.611  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2555.949    ± 206.221  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29941.909    ± 257.602  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31516.632   ± 1023.171  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31063.842     ± 46.182  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7607.127     ± 73.584  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7838.159     ± 78.370  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7702.846     ± 17.183  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        503.651     ± 37.439  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        346.248      ± 5.297  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4816.898   ± 2370.966  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2094.425    ± 551.326  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5086.400     ± 23.545  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      20641.878    ± 108.478  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      20653.756    ± 113.213  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     301403.718   ± 3189.750  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     302412.326   ± 3013.658  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     325188.123   ± 3352.615  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     327545.200   ± 2743.543  ops/s
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
