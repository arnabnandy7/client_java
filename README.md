# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-11T05:09:09Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.44K | ± 3.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.26K | ± 5.45K | ops/s | 1.2x slower |
| prometheusAdd | 51.51K | ± 170.86 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.16K | ± 1.47K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 6.39 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 44.71 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 185.04 | ops/s | 10x slower |
| openTelemetryInc | 3.68K | ± 125.97 | ops/s | 18x slower |
| openTelemetryAdd | 3.58K | ± 514.78 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.15K | ± 44.99 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.64K | ± 1.37K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 50.30 | ops/s | 1.3x slower |
| prometheusNative | 2.99K | ± 291.28 | ops/s | 1.9x slower |
| openTelemetryClassic | 758.97 | ± 4.45 | ops/s | 7.4x slower |
| openTelemetryExponential | 617.61 | ± 78.25 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.14K | ± 954.16 | ops/s | **fastest** |
| prometheusWriteToNull | 22.81K | ± 546.38 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.68K | ± 3.66K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.16K | ± 3.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.84K | ± 3.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.80K | ± 2.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49157.934   ± 1473.574  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3576.016    ± 514.782  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3676.471    ± 125.968  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3149.804     ± 44.992  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51507.751    ± 170.863  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64441.888   ± 3550.426  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52255.401   ± 5451.146  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6343.183    ± 185.036  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6586.752      ± 6.395  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.434     ± 44.714  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        758.969      ± 4.451  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        617.613     ± 78.252  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5643.408   ± 1370.053  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2991.865    ± 291.279  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.105     ± 50.296  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23142.145    ± 954.157  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22807.603    ± 546.381  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464799.666   ± 2664.347  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475844.899   ± 3265.613  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485155.682   ± 3658.835  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492678.387   ± 3657.021  ops/s
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
