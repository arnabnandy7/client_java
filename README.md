# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-16T06:36:03Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 73.89K | ± 3.40K | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.61K | ± 134.35 | ops/s | 1.1x slower |
| prometheusAdd | 63.13K | ± 901.10 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.69K | ± 179.50 | ops/s | 1.3x slower |
| simpleclientAdd | 7.97K | ± 48.68 | ops/s | 9.3x slower |
| simpleclientInc | 7.75K | ± 152.52 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.60K | ± 3.83 | ops/s | 9.7x slower |
| openTelemetryAdd | 6.39K | ± 77.18 | ops/s | 12x slower |
| openTelemetryInc | 5.75K | ± 1.56K | ops/s | 13x slower |
| openTelemetryIncNoLabels | 4.62K | ± 386.24 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.19K | ± 903.24 | ops/s | **fastest** |
| simpleclient | 5.89K | ± 121.01 | ops/s | 1.1x slower |
| prometheusNative | 3.97K | ± 203.93 | ops/s | 1.6x slower |
| openTelemetryClassic | 899.05 | ± 32.90 | ops/s | 6.9x slower |
| openTelemetryExponential | 706.09 | ± 14.02 | ops/s | 8.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 35.22K | ± 337.08 | ops/s | **fastest** |
| prometheusWriteToNull | 34.83K | ± 825.29 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 701.94K | ± 4.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 684.63K | ± 2.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 661.06K | ± 3.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 644.09K | ± 6.35K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56693.548    ± 179.499  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       6391.944     ± 77.175  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5750.149   ± 1563.689  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4621.030    ± 386.241  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63125.774    ± 901.096  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      73890.505   ± 3404.527  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65605.480    ± 134.350  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7967.155     ± 48.680  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7754.922    ± 152.522  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7599.342      ± 3.829  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        899.055     ± 32.901  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        706.088     ± 14.016  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6188.203    ± 903.242  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3974.219    ± 203.928  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5889.655    ± 121.008  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35218.433    ± 337.085  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34826.358    ± 825.291  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     644091.380   ± 6351.303  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661061.016   ± 3194.235  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     684625.172   ± 2876.979  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     701944.966   ± 4295.261  ops/s
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
