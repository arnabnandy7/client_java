# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-12T08:23:26Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.78K | ± 1.80K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.92K | ± 762.68 | ops/s | 1.1x slower |
| prometheusAdd | 51.02K | ± 602.76 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.07K | ± 1.42K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 92.94 | ops/s | 9.8x slower |
| simpleclientAdd | 6.47K | ± 30.97 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.44K | ± 132.76 | ops/s | 9.9x slower |
| openTelemetryAdd | 3.46K | ± 376.82 | ops/s | 18x slower |
| openTelemetryInc | 3.31K | ± 493.47 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.16K | ± 271.84 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.68K | ± 1.28K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 13.93 | ops/s | 1.7x slower |
| prometheusNative | 3.20K | ± 27.50 | ops/s | 2.4x slower |
| openTelemetryClassic | 780.45 | ± 51.40 | ops/s | 9.8x slower |
| openTelemetryExponential | 643.05 | ± 49.89 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.89K | ± 765.41 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.73K | ± 161.81 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 506.96K | ± 6.23K | ops/s | **fastest** |
| prometheusWriteToNull | 506.51K | ± 13.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 495.66K | ± 3.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.35K | ± 7.50K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49070.165   ± 1422.413  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3464.044    ± 376.821  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3309.915    ± 493.469  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3163.707    ± 271.839  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51016.745    ± 602.759  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63778.127   ± 1800.925  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55924.107    ± 762.678  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6466.517     ± 30.968  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6527.068     ± 92.938  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6443.175    ± 132.760  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        780.448     ± 51.397  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        643.052     ± 49.890  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7682.065   ± 1277.138  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3197.117     ± 27.496  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.417     ± 13.933  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23727.585    ± 161.808  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23892.591    ± 765.411  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486347.850   ± 7495.940  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     495659.334   ± 3557.488  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506960.942   ± 6232.947  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     506508.797  ± 13580.424  ops/s
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
