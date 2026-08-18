# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-18T04:20:59Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.31K | ± 1.06K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.37K | ± 709.36 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 91.24 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.13K | ± 526.64 | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 55.36 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 24.27 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 355.19 | ops/s | 11x slower |
| openTelemetryInc | 3.35K | ± 173.15 | ops/s | 20x slower |
| openTelemetryAdd | 3.25K | ± 182.91 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.11K | ± 160.42 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.69K | ± 2.31K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 57.25 | ops/s | 1.5x slower |
| prometheusNative | 2.89K | ± 334.45 | ops/s | 2.3x slower |
| openTelemetryClassic | 753.51 | ± 9.05 | ops/s | 8.9x slower |
| openTelemetryExponential | 607.23 | ± 76.30 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.11K | ± 1.13K | ops/s | **fastest** |
| openMetricsWriteToNull | 23.99K | ± 413.62 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.52K | ± 4.10K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.67K | ± 3.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.19K | ± 5.84K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 461.04K | ± 3.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47129.024    ± 526.640  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3253.754    ± 182.906  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3348.253    ± 173.146  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3105.835    ± 160.419  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51433.170     ± 91.236  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66309.863   ± 1063.048  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56373.836    ± 709.357  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6231.481    ± 355.186  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.496     ± 55.362  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6372.468     ± 24.267  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        753.512      ± 9.049  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        607.229     ± 76.303  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6690.015   ± 2309.235  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2887.649    ± 334.454  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4441.620     ± 57.248  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23987.001    ± 413.618  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24111.828   ± 1133.692  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461035.876   ± 3543.144  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468185.940   ± 5840.055  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484667.910   ± 3955.248  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494517.900   ± 4101.143  ops/s
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
