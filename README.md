# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-21T06:46:27Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.03K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.62K | ± 385.68 | ops/s | 1.1x slower |
| prometheusAdd | 50.72K | ± 497.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.24K | ± 1.44K | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 36.99 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 10.07 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 216.91 | ops/s | 10x slower |
| openTelemetryAdd | 3.31K | ± 319.96 | ops/s | 20x slower |
| openTelemetryInc | 3.15K | ± 238.16 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.01K | ± 202.83 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.98K | ± 501.10 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 52.31 | ops/s | 1.6x slower |
| prometheusNative | 2.95K | ± 364.17 | ops/s | 2.4x slower |
| openTelemetryClassic | 775.90 | ± 16.83 | ops/s | 9.0x slower |
| openTelemetryExponential | 687.71 | ± 84.79 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.01K | ± 475.67 | ops/s | **fastest** |
| prometheusWriteToNull | 23.95K | ± 339.84 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 504.10K | ± 3.11K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.04K | ± 6.03K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.47K | ± 4.85K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 473.25K | ± 9.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49244.431   ± 1436.890  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3307.192    ± 319.960  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3150.470    ± 238.156  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3012.059    ± 202.834  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50716.207    ± 497.899  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65030.041   ± 1226.806  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56620.337    ± 385.684  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6307.348    ± 216.908  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6536.907     ± 36.988  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6351.230     ± 10.068  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        775.900     ± 16.828  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        687.712     ± 84.792  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6979.790    ± 501.096  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2948.486    ± 364.167  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4386.608     ± 52.314  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24013.193    ± 475.670  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23946.687    ± 339.840  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473248.694   ± 9042.858  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479474.168   ± 4853.031  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496035.658   ± 6029.826  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504104.561   ± 3112.596  ops/s
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
