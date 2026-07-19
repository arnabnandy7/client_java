# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-19T06:48:05Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 70.19K | ± 375.35 | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.93K | ± 588.55 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 59.88K | ± 5.19K | ops/s | 1.2x slower |
| prometheusAdd | 58.54K | ± 138.47 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 11.45K | ± 32.35 | ops/s | 6.1x slower |
| simpleclientInc | 11.27K | ± 134.53 | ops/s | 6.2x slower |
| simpleclientAdd | 10.72K | ± 195.03 | ops/s | 6.5x slower |
| openTelemetryIncNoLabels | 7.07K | ± 1.20K | ops/s | 9.9x slower |
| openTelemetryInc | 5.58K | ± 16.90 | ops/s | 13x slower |
| openTelemetryAdd | 5.05K | ± 26.92 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 9.22K | ± 2.41K | ops/s | **fastest** |
| simpleclient | 7.19K | ± 89.71 | ops/s | 1.3x slower |
| prometheusNative | 5.66K | ± 171.12 | ops/s | 1.6x slower |
| openTelemetryClassic | 985.96 | ± 27.79 | ops/s | 9.3x slower |
| openTelemetryExponential | 788.18 | ± 12.67 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 34.24K | ± 98.27 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.22K | ± 74.73 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 803.58K | ± 17.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 738.21K | ± 8.70K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 701.33K | ± 56.44K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 679.21K | ± 19.36K | ops/s | 1.2x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      59880.540   ± 5190.953  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5051.544     ± 26.916  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5578.292     ± 16.895  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7070.909   ± 1204.291  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58537.012    ± 138.468  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      70189.599    ± 375.351  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67929.682    ± 588.549  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10718.763    ± 195.028  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11270.526    ± 134.526  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11446.728     ± 32.349  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        985.959     ± 27.794  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        788.185     ± 12.669  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9216.340   ± 2412.982  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5664.840    ± 171.121  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7188.113     ± 89.708  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34223.924     ± 74.726  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34238.307     ± 98.266  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     701333.027  ± 56438.053  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     679209.862  ± 19364.476  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     738214.584   ± 8698.615  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     803576.692  ± 17910.598  ops/s
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
