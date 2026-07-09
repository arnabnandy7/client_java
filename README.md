# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-09T07:31:55Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.94K | ± 2.13K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.58K | ± 318.72 | ops/s | 1.1x slower |
| prometheusAdd | 51.23K | ± 324.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.16K | ± 1.83K | ops/s | 1.3x slower |
| simpleclientInc | 6.63K | ± 63.70 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.32K | ± 79.37 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 130.55 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.71K | ± 639.26 | ops/s | 18x slower |
| openTelemetryAdd | 3.36K | ± 357.82 | ops/s | 19x slower |
| openTelemetryInc | 3.31K | ± 362.87 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.15K | ± 1.39K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 82.06 | ops/s | 1.4x slower |
| prometheusNative | 2.67K | ± 275.26 | ops/s | 2.3x slower |
| openTelemetryClassic | 764.56 | ± 22.88 | ops/s | 8.0x slower |
| openTelemetryExponential | 619.85 | ± 72.28 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.82K | ± 530.83 | ops/s | **fastest** |
| prometheusWriteToNull | 23.82K | ± 245.55 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 478.27K | ± 19.92K | ops/s | **fastest** |
| prometheusWriteToNull | 476.86K | ± 11.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.91K | ± 10.41K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 458.95K | ± 9.91K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49163.947   ± 1830.935  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3360.211    ± 357.821  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3312.865    ± 362.872  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3710.348    ± 639.256  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51227.502    ± 324.856  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64938.578   ± 2129.529  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56577.294    ± 318.725  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6228.739    ± 130.549  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6625.160     ± 63.698  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6316.796     ± 79.374  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        764.565     ± 22.882  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        619.846     ± 72.276  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6145.776   ± 1388.657  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2673.604    ± 275.265  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.214     ± 82.056  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23820.391    ± 530.829  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23817.702    ± 245.553  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458946.014   ± 9907.539  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472911.573  ± 10411.205  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478272.686  ± 19920.944  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476858.607  ± 11299.658  ops/s
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
