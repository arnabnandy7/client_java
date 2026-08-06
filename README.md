# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-06T06:55:18Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.53K | ± 28.81 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.24K | ± 1.66K | ops/s | 1.0x slower |
| prometheusInc | 30.18K | ± 1.42K | ops/s | 1.0x slower |
| prometheusAdd | 28.43K | ± 38.20 | ops/s | 1.1x slower |
| simpleclientInc | 6.73K | ± 192.72 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.45K | ± 226.55 | ops/s | 4.9x slower |
| simpleclientAdd | 6.43K | ± 190.04 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 2.79K | ± 213.40 | ops/s | 11x slower |
| openTelemetryInc | 2.49K | ± 60.64 | ops/s | 13x slower |
| openTelemetryAdd | 2.17K | ± 400.56 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 41.16 | ops/s | **fastest** |
| prometheusClassic | 2.98K | ± 300.07 | ops/s | 1.5x slower |
| prometheusNative | 2.00K | ± 98.87 | ops/s | 2.2x slower |
| openTelemetryClassic | 594.04 | ± 20.12 | ops/s | 7.5x slower |
| openTelemetryExponential | 433.14 | ± 15.82 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.29K | ± 64.25 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.25K | ± 127.49 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 322.66K | ± 2.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 320.56K | ± 2.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.65K | ± 1.50K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.72K | ± 1.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30239.347   ± 1658.487  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2169.258    ± 400.558  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2491.243     ± 60.639  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2794.003    ± 213.400  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28434.003     ± 38.203  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30175.731   ± 1416.809  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31527.432     ± 28.811  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6427.640    ± 190.043  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6725.417    ± 192.719  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6450.577    ± 226.551  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        594.042     ± 20.121  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        433.137     ± 15.819  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2977.023    ± 300.071  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2001.731     ± 98.867  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.931     ± 41.158  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18246.879    ± 127.487  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18286.475     ± 64.252  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295720.849   ± 1424.341  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296654.011   ± 1504.219  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     320559.910   ± 2476.142  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     322659.423   ± 2681.115  ops/s
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
