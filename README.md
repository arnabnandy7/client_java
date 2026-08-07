# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-07T05:49:02Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1021-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.82K | ± 3.33K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.31K | ± 2.34K | ops/s | 1.1x slower |
| prometheusAdd | 48.33K | ± 364.45 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.06K | ± 1.56K | ops/s | 1.4x slower |
| simpleclientInc | 6.21K | ± 108.73 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.90K | ± 3.22 | ops/s | 9.8x slower |
| simpleclientAdd | 5.81K | ± 251.71 | ops/s | 10.0x slower |
| openTelemetryIncNoLabels | 5.22K | ± 1.16K | ops/s | 11x slower |
| openTelemetryInc | 4.43K | ± 1.31K | ops/s | 13x slower |
| openTelemetryAdd | 3.28K | ± 113.32 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 1.58K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 57.06 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 221.80 | ops/s | 1.8x slower |
| openTelemetryClassic | 707.25 | ± 28.81 | ops/s | 7.5x slower |
| openTelemetryExponential | 553.21 | ± 15.86 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.44K | ± 193.94 | ops/s | **fastest** |
| prometheusWriteToNull | 27.37K | ± 298.62 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 566.48K | ± 1.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.06K | ± 2.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.76K | ± 4.94K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 525.81K | ± 2.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42057.604   ± 1563.656  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3284.267    ± 113.315  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4431.103   ± 1311.975  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5215.169   ± 1155.066  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48326.120    ± 364.447  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57821.511   ± 3333.096  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50309.376   ± 2337.443  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5810.580    ± 251.710  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6207.843    ± 108.730  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5897.781      ± 3.221  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.252     ± 28.809  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.212     ± 15.865  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5336.444   ± 1579.717  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2941.037    ± 221.798  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4348.714     ± 57.060  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27435.297    ± 193.944  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27371.200    ± 298.624  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     525813.757   ± 2339.056  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534763.142   ± 4941.728  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549055.248   ± 2673.360  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     566482.532   ± 1531.806  ops/s
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
