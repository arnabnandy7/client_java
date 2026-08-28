# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-28T15:34:19Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.02K | ± 345.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.87K | ± 281.67 | ops/s | 1.2x slower |
| prometheusAdd | 51.31K | ± 268.79 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.19K | ± 1.48K | ops/s | 1.3x slower |
| simpleclientInc | 6.52K | ± 160.36 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 38.91 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 26.80 | ops/s | 10x slower |
| openTelemetryAdd | 3.30K | ± 166.95 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.17K | ± 170.43 | ops/s | 21x slower |
| openTelemetryInc | 3.05K | ± 227.32 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.05K | ± 1.64K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 74.92 | ops/s | 1.6x slower |
| prometheusNative | 3.14K | ± 137.38 | ops/s | 2.2x slower |
| openTelemetryClassic | 767.07 | ± 32.40 | ops/s | 9.2x slower |
| openTelemetryExponential | 651.37 | ± 69.69 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.72K | ± 97.07 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.50K | ± 423.76 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.75K | ± 4.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.40K | ± 5.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.13K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.47K | ± 4.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49190.150   ± 1478.885  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3304.217    ± 166.953  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3053.012    ± 227.315  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3165.221    ± 170.434  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51307.254    ± 268.790  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66022.732    ± 345.517  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56868.829    ± 281.672  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6481.280     ± 38.914  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6520.996    ± 160.363  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6364.832     ± 26.796  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        767.074     ± 32.400  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        651.374     ± 69.689  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7053.763   ± 1635.014  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3144.284    ± 137.379  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4414.176     ± 74.923  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23495.715    ± 423.760  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23723.575     ± 97.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476473.522   ± 4319.589  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487127.956   ± 3093.422  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496402.715   ± 5442.194  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502749.455   ± 4583.672  ops/s
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
