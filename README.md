# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-02T09:37:58Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.34K | ± 1.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.37K | ± 168.63 | ops/s | 1.2x slower |
| prometheusAdd | 51.12K | ± 727.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.90K | ± 1.38K | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 48.04 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.33K | ± 10.58 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 329.09 | ops/s | 11x slower |
| openTelemetryAdd | 3.35K | ± 498.72 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.31K | ± 342.06 | ops/s | 20x slower |
| openTelemetryInc | 3.14K | ± 280.20 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.01K | ± 702.02 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 79.25 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 331.67 | ops/s | 2.1x slower |
| openTelemetryClassic | 756.81 | ± 22.48 | ops/s | 7.9x slower |
| openTelemetryExponential | 657.77 | ± 87.84 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.10K | ± 208.80 | ops/s | **fastest** |
| prometheusWriteToNull | 24.01K | ± 592.12 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 493.52K | ± 4.43K | ops/s | **fastest** |
| prometheusWriteToNull | 491.74K | ± 5.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.08K | ± 3.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.28K | ± 2.53K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48900.916   ± 1375.160  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3346.871    ± 498.717  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3144.617    ± 280.203  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3313.130    ± 342.060  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51122.658    ± 727.278  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65343.285   ± 1377.633  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56367.551    ± 168.632  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6194.616    ± 329.090  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6604.473     ± 48.036  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6326.487     ± 10.579  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        756.813     ± 22.478  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        657.769     ± 87.840  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6007.124    ± 702.022  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2819.301    ± 331.667  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.067     ± 79.245  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24096.326    ± 208.797  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24013.383    ± 592.122  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485281.128   ± 2525.098  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487080.710   ± 3524.647  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493517.081   ± 4429.015  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491740.474   ± 5152.615  ops/s
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
