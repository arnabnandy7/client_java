# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-28T09:53:01Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 26.48K | ± 72.66 | ops/s | **fastest** |
| codahaleIncNoLabels | 26.44K | ± 119.19 | ops/s | 1.0x slower |
| prometheusInc | 26.24K | ± 144.91 | ops/s | 1.0x slower |
| prometheusAdd | 24.85K | ± 1.12K | ops/s | 1.1x slower |
| simpleclientInc | 6.63K | ± 25.91 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 6.48K | ± 23.93 | ops/s | 4.1x slower |
| simpleclientAdd | 6.36K | ± 108.81 | ops/s | 4.2x slower |
| openTelemetryInc | 2.59K | ± 297.60 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 2.36K | ± 215.10 | ops/s | 11x slower |
| openTelemetryAdd | 2.23K | ± 104.80 | ops/s | 12x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.32K | ± 67.81 | ops/s | **fastest** |
| prometheusClassic | 2.79K | ± 777.44 | ops/s | 1.5x slower |
| prometheusNative | 1.88K | ± 270.29 | ops/s | 2.3x slower |
| openTelemetryClassic | 459.42 | ± 37.44 | ops/s | 9.4x slower |
| openTelemetryExponential | 338.06 | ± 15.81 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 17.79K | ± 102.16 | ops/s | **fastest** |
| openMetricsWriteToNull | 17.73K | ± 85.07 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 297.25K | ± 1.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 292.65K | ± 2.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 281.81K | ± 2.40K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 279.79K | ± 2.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26436.708    ± 119.192  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2225.818    ± 104.797  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2594.220    ± 297.598  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2359.939    ± 215.097  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      24851.594   ± 1116.784  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26244.699    ± 144.914  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26479.670     ± 72.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6355.333    ± 108.810  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6632.759     ± 25.907  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6482.692     ± 23.933  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        459.422     ± 37.440  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        338.064     ± 15.806  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2794.580    ± 777.443  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1877.805    ± 270.286  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4320.949     ± 67.809  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17726.487     ± 85.071  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17786.478    ± 102.164  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     281813.873   ± 2403.759  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     279788.891   ± 2056.558  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     292645.586   ± 2515.994  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     297247.076   ± 1885.986  ops/s
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
