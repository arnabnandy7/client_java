# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-19T04:23:17Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 69.09K | ± 1.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.14K | ± 2.28K | ops/s | 1.2x slower |
| prometheusAdd | 51.85K | ± 604.39 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 51.31K | ± 1.51K | ops/s | 1.3x slower |
| simpleclientInc | 6.73K | ± 99.88 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.57K | ± 116.77 | ops/s | 11x slower |
| simpleclientAdd | 6.33K | ± 218.11 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.36K | ± 309.47 | ops/s | 21x slower |
| openTelemetryAdd | 3.34K | ± 204.79 | ops/s | 21x slower |
| openTelemetryInc | 3.34K | ± 157.26 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.48K | ± 2.88K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 69.77 | ops/s | 1.7x slower |
| prometheusNative | 2.82K | ± 100.31 | ops/s | 2.7x slower |
| openTelemetryClassic | 800.13 | ± 16.83 | ops/s | 9.4x slower |
| openTelemetryExponential | 693.24 | ± 129.28 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 25.77K | ± 493.62 | ops/s | **fastest** |
| openMetricsWriteToNull | 24.14K | ± 587.42 | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 523.77K | ± 7.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 515.38K | ± 8.81K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.49K | ± 6.34K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 490.33K | ± 6.59K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      51307.835   ± 1514.019  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3341.039    ± 204.793  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3335.992    ± 157.258  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3358.481    ± 309.466  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51845.700    ± 604.394  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69090.803   ± 1408.153  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56144.648   ± 2280.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6331.526    ± 218.110  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6725.539     ± 99.881  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6565.936    ± 116.771  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        800.129     ± 16.829  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        693.241    ± 129.278  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7482.006   ± 2880.340  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2821.813    ± 100.311  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4469.834     ± 69.765  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24138.734    ± 587.420  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      25773.095    ± 493.622  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     490332.940   ± 6594.009  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492491.409   ± 6341.487  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     515382.207   ± 8809.079  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     523773.017   ± 7985.431  ops/s
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
