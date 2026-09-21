# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-21T09:11:25Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.41K | ± 425.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.86K | ± 434.51 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 431.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.43K | ± 2.02K | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 42.46 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.43K | ± 131.70 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 234.10 | ops/s | 10x slower |
| openTelemetryInc | 3.26K | ± 246.08 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.15K | ± 162.89 | ops/s | 21x slower |
| openTelemetryAdd | 2.77K | ± 82.75 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.41K | ± 885.50 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 58.51 | ops/s | 1.5x slower |
| prometheusNative | 3.03K | ± 257.41 | ops/s | 2.1x slower |
| openTelemetryClassic | 788.43 | ± 30.23 | ops/s | 8.1x slower |
| openTelemetryExponential | 670.47 | ± 111.85 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.62K | ± 438.92 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.58K | ± 464.64 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 500.96K | ± 3.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.54K | ± 3.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.08K | ± 8.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 469.67K | ± 7.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48429.347   ± 2017.986  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2770.757     ± 82.747  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3257.431    ± 246.078  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3147.576    ± 162.890  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51292.693    ± 431.841  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65406.989    ± 425.394  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56861.424    ± 434.509  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6234.497    ± 234.101  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6565.092     ± 42.458  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6425.084    ± 131.702  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        788.426     ± 30.231  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        670.466    ± 111.848  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6406.653    ± 885.496  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3026.637    ± 257.411  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.051     ± 58.509  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23583.338    ± 464.640  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23615.749    ± 438.917  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469674.183   ± 7469.870  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477081.460   ± 8220.747  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499542.842   ± 3412.652  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500960.674   ± 3370.668  ops/s
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
