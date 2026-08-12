# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-12T05:32:28Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.32K | ± 563.85 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.02K | ± 156.80 | ops/s | 1.1x slower |
| prometheusAdd | 51.47K | ± 291.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.18K | ± 1.51K | ops/s | 1.3x slower |
| simpleclientInc | 6.48K | ± 150.52 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 37.64 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 186.42 | ops/s | 10x slower |
| openTelemetryInc | 3.34K | ± 153.32 | ops/s | 20x slower |
| openTelemetryAdd | 3.32K | ± 362.05 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.11K | ± 92.98 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.76K | ± 2.33K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 55.60 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 388.08 | ops/s | 2.0x slower |
| openTelemetryClassic | 783.68 | ± 30.94 | ops/s | 7.4x slower |
| openTelemetryExponential | 717.00 | ± 77.72 | ops/s | 8.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.07K | ± 327.36 | ops/s | **fastest** |
| prometheusWriteToNull | 23.42K | ± 171.63 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 500.17K | ± 4.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.52K | ± 4.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.53K | ± 4.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.08K | ± 3.43K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50178.683   ± 1514.656  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3317.290    ± 362.054  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3343.224    ± 153.315  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3110.906     ± 92.985  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51473.179    ± 291.454  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65315.671    ± 563.849  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57020.944    ± 156.803  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6319.411    ± 186.424  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6483.529    ± 150.522  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6357.550     ± 37.639  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        783.685     ± 30.938  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        717.001     ± 77.724  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5761.120   ± 2327.971  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2817.638    ± 388.076  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4402.382     ± 55.604  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24072.170    ± 327.358  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23421.784    ± 171.627  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481080.003   ± 3434.796  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485533.233   ± 4878.399  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494523.622   ± 4882.373  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500169.502   ± 4154.651  ops/s
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
