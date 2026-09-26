# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-26T08:46:12Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.10K | ± 1.82K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.84K | ± 2.32K | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 283.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.13K | ± 1.60K | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 42.53 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.30K | ± 107.88 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 209.25 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.18K | ± 207.87 | ops/s | 20x slower |
| openTelemetryInc | 3.14K | ± 361.55 | ops/s | 21x slower |
| openTelemetryAdd | 3.06K | ± 198.52 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 32.28 | ops/s | 1.2x slower |
| prometheusNative | 2.84K | ± 350.27 | ops/s | 1.9x slower |
| openTelemetryClassic | 758.88 | ± 6.88 | ops/s | 7.0x slower |
| openTelemetryExponential | 654.68 | ± 50.11 | ops/s | 8.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.60K | ± 871.14 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.02K | ± 588.91 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 500.03K | ± 6.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.45K | ± 2.45K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.33K | ± 3.66K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.58K | ± 5.21K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48128.103   ± 1599.252  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3062.053    ± 198.521  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3135.743    ± 361.552  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3180.485    ± 207.868  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51350.693    ± 283.021  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65095.618   ± 1816.696  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54843.237   ± 2317.515  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6225.861    ± 209.251  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6597.793     ± 42.533  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6296.216    ± 107.876  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        758.876      ± 6.885  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        654.683     ± 50.114  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5342.399   ± 1417.783  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2836.070    ± 350.275  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4482.148     ± 32.285  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23021.871    ± 588.913  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23599.184    ± 871.142  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469580.021   ± 5210.458  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483325.904   ± 3659.405  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493448.513   ± 2445.801  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500026.057   ± 6498.275  ops/s
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
