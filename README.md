# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-22T06:45:19Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.93K | ± 234.34 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.82K | ± 407.34 | ops/s | 1.2x slower |
| prometheusAdd | 51.39K | ± 160.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.87K | ± 1.89K | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 11.73 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.46K | ± 134.56 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 10.75 | ops/s | 10x slower |
| openTelemetryAdd | 3.29K | ± 256.72 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.24K | ± 452.67 | ops/s | 20x slower |
| openTelemetryInc | 3.16K | ± 433.82 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.57K | ± 1.17K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 42.35 | ops/s | 1.3x slower |
| prometheusNative | 2.78K | ± 293.00 | ops/s | 2.0x slower |
| openTelemetryClassic | 756.13 | ± 5.68 | ops/s | 7.4x slower |
| openTelemetryExponential | 632.41 | ± 54.55 | ops/s | 8.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.54K | ± 763.79 | ops/s | **fastest** |
| prometheusWriteToNull | 23.38K | ± 96.96 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 510.51K | ± 3.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.14K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.24K | ± 3.56K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 483.43K | ± 2.07K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47868.698   ± 1890.550  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3291.242    ± 256.721  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3164.279    ± 433.825  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3242.831    ± 452.673  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51386.971    ± 160.608  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65932.685    ± 234.340  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56815.004    ± 407.342  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6460.815     ± 10.746  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6572.356     ± 11.727  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6463.017    ± 134.558  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        756.126      ± 5.676  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        632.414     ± 54.552  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5572.282   ± 1171.312  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2780.099    ± 293.001  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4343.493     ± 42.355  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24538.619    ± 763.794  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23378.059     ± 96.957  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483426.500   ± 2068.975  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485241.639   ± 3559.573  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500141.999   ± 2604.727  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     510505.279   ± 3521.490  ops/s
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
