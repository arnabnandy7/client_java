# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-05T08:11:18Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.03K | ± 283.84 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.05K | ± 673.24 | ops/s | 1.2x slower |
| prometheusAdd | 51.24K | ± 578.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.12K | ± 1.27K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 9.13 | ops/s | 10x slower |
| simpleclientAdd | 6.41K | ± 240.05 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.31K | ± 37.57 | ops/s | 10x slower |
| openTelemetryAdd | 3.48K | ± 288.66 | ops/s | 19x slower |
| openTelemetryInc | 3.20K | ± 356.15 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.12K | ± 225.87 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.95K | ± 995.56 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 59.20 | ops/s | 1.3x slower |
| prometheusNative | 3.09K | ± 356.34 | ops/s | 1.9x slower |
| openTelemetryClassic | 738.92 | ± 14.72 | ops/s | 8.1x slower |
| openTelemetryExponential | 738.15 | ± 50.15 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.95K | ± 386.42 | ops/s | **fastest** |
| prometheusWriteToNull | 23.39K | ± 1.47K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 487.29K | ± 4.86K | ops/s | **fastest** |
| prometheusWriteToNull | 486.70K | ± 5.69K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.82K | ± 4.51K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 463.07K | ± 4.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49120.229   ± 1268.243  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3480.310    ± 288.661  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3203.508    ± 356.147  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3115.743    ± 225.875  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51237.411    ± 578.925  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66031.771    ± 283.839  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56045.935    ± 673.237  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6405.293    ± 240.050  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6585.178      ± 9.127  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6306.733     ± 37.567  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        738.920     ± 14.720  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        738.152     ± 50.146  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5951.963    ± 995.559  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3090.714    ± 356.336  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4423.620     ± 59.198  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23946.532    ± 386.421  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23391.595   ± 1472.986  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     463070.042   ± 4658.316  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472822.748   ± 4514.815  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487287.543   ± 4858.874  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486696.377   ± 5693.104  ops/s
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
