# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-29T10:13:50Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.69K | ± 994.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.48K | ± 352.87 | ops/s | 1.1x slower |
| prometheusAdd | 51.10K | ± 317.56 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.03K | ± 985.42 | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 47.83 | ops/s | 9.9x slower |
| simpleclientAdd | 6.37K | ± 203.97 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 10.15 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.37K | ± 470.60 | ops/s | 19x slower |
| openTelemetryInc | 3.19K | ± 143.11 | ops/s | 20x slower |
| openTelemetryAdd | 3.17K | ± 454.98 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.75K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 79.32 | ops/s | 1.3x slower |
| prometheusNative | 2.77K | ± 313.87 | ops/s | 2.1x slower |
| openTelemetryClassic | 769.53 | ± 21.86 | ops/s | 7.5x slower |
| openTelemetryExponential | 606.10 | ± 25.49 | ops/s | 9.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.18K | ± 284.62 | ops/s | **fastest** |
| prometheusWriteToNull | 23.86K | ± 728.66 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 510.13K | ± 4.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 507.17K | ± 6.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.27K | ± 4.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.25K | ± 5.49K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48031.530    ± 985.415  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3166.179    ± 454.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3188.440    ± 143.115  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3374.694    ± 470.598  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51102.140    ± 317.558  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64694.699    ± 994.557  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56482.194    ± 352.869  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6369.088    ± 203.968  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6545.102     ± 47.835  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6333.125     ± 10.146  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        769.530     ± 21.857  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        606.098     ± 25.486  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5749.383   ± 1470.794  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2769.978    ± 313.874  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4417.728     ± 79.318  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24183.371    ± 284.619  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23862.706    ± 728.661  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486253.528   ± 5488.608  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489273.145   ± 4457.557  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     507173.609   ± 6647.634  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     510130.999   ± 4889.212  ops/s
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
