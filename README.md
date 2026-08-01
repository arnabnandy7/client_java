# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-01T06:52:25Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.51K | ± 1.35K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.90K | ± 3.29K | ops/s | 1.2x slower |
| prometheusAdd | 50.96K | ± 633.72 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.31K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 53.76 | ops/s | 9.8x slower |
| simpleclientAdd | 6.49K | ± 61.07 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 34.50 | ops/s | 10x slower |
| openTelemetryAdd | 3.49K | ± 612.27 | ops/s | 18x slower |
| openTelemetryInc | 3.20K | ± 588.74 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.06K | ± 141.72 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.66K | ± 1.54K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 17.14 | ops/s | 1.3x slower |
| prometheusNative | 2.92K | ± 259.13 | ops/s | 1.9x slower |
| openTelemetryClassic | 760.68 | ± 63.65 | ops/s | 7.4x slower |
| openTelemetryExponential | 714.27 | ± 37.24 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.67K | ± 813.94 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.41K | ± 1.58K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 511.05K | ± 7.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 508.81K | ± 2.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.35K | ± 1.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.29K | ± 3.92K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48306.304   ± 1497.704  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3487.818    ± 612.268  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3200.495    ± 588.736  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3064.629    ± 141.724  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50955.808    ± 633.719  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64509.793   ± 1352.571  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54897.688   ± 3294.133  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6492.961     ± 61.066  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.620     ± 53.761  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6380.642     ± 34.499  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        760.682     ± 63.650  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        714.269     ± 37.239  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5661.750   ± 1538.361  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2923.914    ± 259.130  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4379.134     ± 17.144  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23413.144   ± 1582.291  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23669.025    ± 813.944  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486286.259   ± 3917.367  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488346.027   ± 1498.966  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     508808.084   ± 2439.522  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     511046.690   ± 7358.134  ops/s
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
