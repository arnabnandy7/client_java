# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-02T04:36:14Z
- **Commit:** [`f705841`](https://github.com/arnabnandy7/client_java/commit/f70584167d821d79e8270f82f5aa8fc63883c9ac)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 27.27K | ± 784.22 | ops/s | **fastest** |
| prometheusNoLabelsInc | 26.65K | ± 195.54 | ops/s | 1.0x slower |
| prometheusInc | 26.53K | ± 49.65 | ops/s | 1.0x slower |
| prometheusAdd | 25.31K | ± 1.25K | ops/s | 1.1x slower |
| simpleclientInc | 6.75K | ± 83.09 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 6.60K | ± 22.73 | ops/s | 4.1x slower |
| simpleclientAdd | 6.46K | ± 117.84 | ops/s | 4.2x slower |
| openTelemetryIncNoLabels | 2.30K | ± 124.68 | ops/s | 12x slower |
| openTelemetryAdd | 2.29K | ± 171.60 | ops/s | 12x slower |
| openTelemetryInc | 2.08K | ± 224.58 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.34K | ± 25.27 | ops/s | **fastest** |
| prometheusClassic | 2.64K | ± 410.42 | ops/s | 1.6x slower |
| prometheusNative | 1.89K | ± 242.83 | ops/s | 2.3x slower |
| openTelemetryClassic | 449.67 | ± 22.13 | ops/s | 9.6x slower |
| openTelemetryExponential | 338.51 | ± 21.72 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 17.91K | ± 62.95 | ops/s | **fastest** |
| prometheusWriteToNull | 17.90K | ± 40.17 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 297.18K | ± 1.90K | ops/s | **fastest** |
| prometheusWriteToNull | 289.43K | ± 12.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 282.61K | ± 2.86K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 281.35K | ± 1.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27270.200    ± 784.223  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2292.042    ± 171.602  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2083.380    ± 224.577  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2302.666    ± 124.681  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25310.477   ± 1247.661  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26532.751     ± 49.646  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26650.098    ± 195.537  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6458.825    ± 117.841  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6751.081     ± 83.089  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6600.880     ± 22.731  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        449.670     ± 22.127  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        338.507     ± 21.722  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2641.491    ± 410.419  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1885.616    ± 242.834  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4335.271     ± 25.267  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17913.330     ± 62.945  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17904.662     ± 40.172  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     282609.400   ± 2861.337  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     281349.747   ± 1605.035  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     297178.702   ± 1895.975  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     289432.536  ± 12123.144  ops/s
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
