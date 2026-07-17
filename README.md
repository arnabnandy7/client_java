# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-17T06:38:56Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| codahaleIncNoLabels | 26.62K | ± 1.79K | ops/s | **fastest** |
| prometheusNoLabelsInc | 26.62K | ± 598.47 | ops/s | 1.0x slower |
| prometheusInc | 26.52K | ± 177.11 | ops/s | 1.0x slower |
| prometheusAdd | 25.87K | ± 220.59 | ops/s | 1.0x slower |
| simpleclientInc | 6.81K | ± 57.10 | ops/s | 3.9x slower |
| simpleclientAdd | 6.69K | ± 147.54 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 6.66K | ± 31.25 | ops/s | 4.0x slower |
| openTelemetryIncNoLabels | 2.30K | ± 101.10 | ops/s | 12x slower |
| openTelemetryAdd | 2.27K | ± 286.38 | ops/s | 12x slower |
| openTelemetryInc | 2.21K | ± 111.36 | ops/s | 12x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.41K | ± 37.81 | ops/s | **fastest** |
| prometheusClassic | 2.68K | ± 277.52 | ops/s | 1.6x slower |
| prometheusNative | 2.21K | ± 99.40 | ops/s | 2.0x slower |
| openTelemetryClassic | 442.51 | ± 13.04 | ops/s | 10.0x slower |
| openTelemetryExponential | 332.03 | ± 6.97 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.11K | ± 50.54 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.10K | ± 118.78 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 292.25K | ± 2.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 289.71K | ± 1.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 275.23K | ± 1.03K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 271.53K | ± 1.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26621.677   ± 1794.654  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2272.665    ± 286.376  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2210.301    ± 111.358  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2296.066    ± 101.097  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25871.450    ± 220.590  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26523.153    ± 177.106  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26616.161    ± 598.466  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6693.537    ± 147.538  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6811.294     ± 57.103  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6663.359     ± 31.254  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        442.511     ± 13.041  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        332.030      ± 6.971  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2684.259    ± 277.515  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2212.159     ± 99.401  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4414.858     ± 37.810  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18095.332    ± 118.781  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18106.077     ± 50.544  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     271525.040   ± 1298.590  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     275229.952   ± 1029.539  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     289713.018   ± 1161.054  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     292250.751   ± 2971.738  ops/s
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
