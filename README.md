# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-25T06:39:31Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.05K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 237.12 | ops/s | 1.1x slower |
| prometheusAdd | 51.13K | ± 437.80 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.42K | ± 1.07K | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 39.80 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.30K | ± 62.02 | ops/s | 10x slower |
| simpleclientAdd | 6.06K | ± 362.08 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.54K | ± 502.70 | ops/s | 18x slower |
| openTelemetryAdd | 3.11K | ± 343.31 | ops/s | 21x slower |
| openTelemetryInc | 2.96K | ± 277.23 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.99K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 88.50 | ops/s | 1.4x slower |
| prometheusNative | 2.89K | ± 306.97 | ops/s | 2.1x slower |
| openTelemetryClassic | 762.94 | ± 23.37 | ops/s | 7.9x slower |
| openTelemetryExponential | 608.73 | ± 60.64 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.06K | ± 533.60 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.66K | ± 418.35 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 507.11K | ± 2.25K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.72K | ± 3.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.56K | ± 3.03K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 487.09K | ± 1.94K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49421.471   ± 1066.727  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3106.139    ± 343.306  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2963.024    ± 277.232  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3539.460    ± 502.699  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51127.477    ± 437.798  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65048.832   ± 1244.998  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57077.371    ± 237.122  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6055.748    ± 362.082  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6539.128     ± 39.796  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6300.284     ± 62.025  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        762.936     ± 23.372  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        608.727     ± 60.639  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5990.363   ± 1340.076  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2888.922    ± 306.966  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4373.995     ± 88.500  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23661.745    ± 418.355  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24060.333    ± 533.605  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487094.273   ± 1944.866  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488560.057   ± 3033.863  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493716.719   ± 3036.818  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     507110.704   ± 2252.198  ops/s
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
