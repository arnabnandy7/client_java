# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-03T07:19:23Z
- **Commit:** [`f705841`](https://github.com/arnabnandy7/client_java/commit/f70584167d821d79e8270f82f5aa8fc63883c9ac)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.84K | ± 92.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.02K | ± 172.04 | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 102.11 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.53K | ± 2.16K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 35.37 | ops/s | 10x slower |
| simpleclientAdd | 6.56K | ± 7.99 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 34.44 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.34K | ± 558.23 | ops/s | 20x slower |
| openTelemetryAdd | 3.34K | ± 160.34 | ops/s | 20x slower |
| openTelemetryInc | 3.23K | ± 173.69 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.75K | ± 470.51 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 86.23 | ops/s | 1.1x slower |
| prometheusNative | 2.78K | ± 338.64 | ops/s | 1.7x slower |
| openTelemetryClassic | 740.75 | ± 19.69 | ops/s | 6.4x slower |
| openTelemetryExponential | 622.98 | ± 66.72 | ops/s | 7.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.27K | ± 968.06 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.20K | ± 757.24 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.29K | ± 5.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.03K | ± 3.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.26K | ± 2.40K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.72K | ± 1.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49530.614   ± 2164.868  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3335.221    ± 160.336  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3232.496    ± 173.687  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3335.910    ± 558.230  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51599.235    ± 102.113  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65836.310     ± 92.212  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57024.410    ± 172.041  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6555.227      ± 7.992  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.890     ± 35.365  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6386.876     ± 34.435  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        740.754     ± 19.689  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        622.978     ± 66.724  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4752.002    ± 470.508  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2777.200    ± 338.643  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.244     ± 86.226  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23204.186    ± 757.239  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23269.602    ± 968.058  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471724.893   ± 1573.612  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484257.015   ± 2403.923  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493027.572   ± 3118.946  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499287.472   ± 5579.179  ops/s
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
