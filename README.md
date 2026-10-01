# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-01T09:59:59Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.65K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 53.88K | ± 1.55K | ops/s | 1.2x slower |
| prometheusAdd | 50.38K | ± 1.78K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.86K | ± 516.46 | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 33.90 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.37K | ± 25.53 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 404.79 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.45K | ± 397.57 | ops/s | 19x slower |
| openTelemetryAdd | 3.18K | ± 344.54 | ops/s | 20x slower |
| openTelemetryInc | 3.10K | ± 355.96 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.49K | ± 593.18 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 60.70 | ops/s | 1.0x slower |
| prometheusNative | 2.76K | ± 349.05 | ops/s | 1.6x slower |
| openTelemetryClassic | 776.40 | ± 25.33 | ops/s | 5.8x slower |
| openTelemetryExponential | 659.77 | ± 79.88 | ops/s | 6.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.28K | ± 760.00 | ops/s | **fastest** |
| prometheusWriteToNull | 23.15K | ± 977.62 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.49K | ± 5.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.88K | ± 6.98K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.55K | ± 3.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.04K | ± 5.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49858.469    ± 516.464  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3184.693    ± 344.545  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3103.291    ± 355.955  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3454.134    ± 397.570  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50381.306   ± 1776.714  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64649.842   ± 1098.712  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      53880.137   ± 1553.344  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6202.931    ± 404.787  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6529.952     ± 33.903  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6368.139     ± 25.527  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        776.400     ± 25.332  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        659.769     ± 79.878  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4487.847    ± 593.185  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2760.299    ± 349.053  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.667     ± 60.697  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23275.962    ± 760.004  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23152.724    ± 977.617  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471042.138   ± 5465.346  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482550.184   ± 3569.699  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494883.046   ± 6978.605  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499488.857   ± 5751.062  ops/s
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
