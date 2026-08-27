# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-27T14:00:47Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 55.83K | ± 2.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.90K | ± 2.24K | ops/s | 1.1x slower |
| prometheusAdd | 48.48K | ± 1.08K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.15K | ± 243.97 | ops/s | 1.3x slower |
| simpleclientInc | 6.13K | ± 112.58 | ops/s | 9.1x slower |
| simpleclientAdd | 6.02K | ± 274.58 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.86K | ± 55.01 | ops/s | 9.5x slower |
| openTelemetryInc | 4.50K | ± 1.19K | ops/s | 12x slower |
| openTelemetryAdd | 3.98K | ± 851.58 | ops/s | 14x slower |
| openTelemetryIncNoLabels | 3.65K | ± 223.56 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 1.46K | ops/s | **fastest** |
| simpleclient | 4.19K | ± 36.90 | ops/s | 1.3x slower |
| prometheusNative | 2.98K | ± 272.54 | ops/s | 1.8x slower |
| openTelemetryClassic | 726.52 | ± 20.45 | ops/s | 7.6x slower |
| openTelemetryExponential | 553.12 | ± 37.88 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.60K | ± 195.95 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.42K | ± 166.94 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 584.16K | ± 5.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 570.64K | ± 5.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.72K | ± 3.86K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 522.72K | ± 2.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44154.234    ± 243.968  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3981.566    ± 851.581  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4502.772   ± 1192.694  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3647.625    ± 223.564  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48476.059   ± 1081.439  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      55826.070   ± 2681.438  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49895.783   ± 2239.992  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6018.643    ± 274.583  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6126.532    ± 112.582  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5856.897     ± 55.008  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        726.516     ± 20.447  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        553.124     ± 37.877  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5487.551   ± 1464.199  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2979.071    ± 272.541  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4191.017     ± 36.896  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27422.066    ± 166.944  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27595.270    ± 195.949  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522717.628   ± 2679.513  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538715.682   ± 3859.122  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     570636.203   ± 5425.257  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     584157.387   ± 5280.617  ops/s
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
