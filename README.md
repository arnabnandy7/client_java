# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-04T08:28:59Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.91K | ± 1.98K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 453.02 | ops/s | 1.1x slower |
| prometheusAdd | 51.28K | ± 352.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.71K | ± 781.05 | ops/s | 1.4x slower |
| simpleclientInc | 6.63K | ± 54.69 | ops/s | 9.8x slower |
| simpleclientAdd | 6.46K | ± 10.94 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.45K | ± 134.26 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.61K | ± 767.64 | ops/s | 18x slower |
| openTelemetryAdd | 3.31K | ± 350.46 | ops/s | 20x slower |
| openTelemetryInc | 3.15K | ± 329.94 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.11K | ± 1.57K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 97.78 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 263.47 | ops/s | 1.7x slower |
| openTelemetryClassic | 762.52 | ± 12.23 | ops/s | 6.7x slower |
| openTelemetryExponential | 675.59 | ± 62.37 | ops/s | 7.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.01K | ± 795.45 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.24K | ± 706.62 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 503.46K | ± 7.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.56K | ± 7.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.22K | ± 3.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.24K | ± 3.08K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47707.892    ± 781.053  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3306.170    ± 350.462  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3152.390    ± 329.943  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3614.909    ± 767.637  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51282.284    ± 352.730  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64905.985   ± 1980.590  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56913.780    ± 453.018  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6459.381     ± 10.940  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6628.492     ± 54.686  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6454.084    ± 134.265  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        762.521     ± 12.227  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        675.586     ± 62.371  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5108.653   ± 1572.458  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.683    ± 263.466  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4343.500     ± 97.782  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23236.746    ± 706.619  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24010.503    ± 795.451  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479243.547   ± 3078.262  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482219.443   ± 3602.426  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491558.539   ± 7466.972  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503456.188   ± 7122.952  ops/s
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
