# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-23T04:28:52Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.02K | ± 1.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.96K | ± 1.94K | ops/s | 1.2x slower |
| prometheusAdd | 50.98K | ± 568.96 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.27K | ± 1.06K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 38.61 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.43K | ± 133.54 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 251.46 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.02K | ± 851.83 | ops/s | 16x slower |
| openTelemetryInc | 3.43K | ± 275.90 | ops/s | 19x slower |
| openTelemetryAdd | 3.19K | ± 121.25 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.44K | ± 396.80 | ops/s | **fastest** |
| simpleclient | 4.41K | ± 44.56 | ops/s | 1.0x slower |
| prometheusNative | 3.12K | ± 130.73 | ops/s | 1.4x slower |
| openTelemetryClassic | 772.11 | ± 11.06 | ops/s | 5.7x slower |
| openTelemetryExponential | 703.04 | ± 108.53 | ops/s | 6.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.02K | ± 1.09K | ops/s | **fastest** |
| prometheusWriteToNull | 22.88K | ± 414.77 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.91K | ± 6.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.72K | ± 3.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.01K | ± 2.43K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.11K | ± 3.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49269.925   ± 1058.880  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3188.568    ± 121.246  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3433.950    ± 275.898  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4018.657    ± 851.834  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50975.330    ± 568.955  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65023.242   ± 1075.248  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55963.139   ± 1943.351  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6247.545    ± 251.459  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6560.803     ± 38.608  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6428.036    ± 133.537  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        772.109     ± 11.057  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        703.036    ± 108.525  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4435.928    ± 396.803  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3120.205    ± 130.728  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4413.686     ± 44.559  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23016.224   ± 1093.654  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22884.551    ± 414.768  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484105.818   ± 3151.591  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489012.628   ± 2432.603  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503716.918   ± 3380.072  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509906.812   ± 6178.887  ops/s
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
