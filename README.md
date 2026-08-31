# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-31T09:51:23Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.73K | ± 1.54K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.72K | ± 326.31 | ops/s | 1.2x slower |
| prometheusAdd | 51.37K | ± 151.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.28K | ± 243.83 | ops/s | 1.4x slower |
| simpleclientInc | 6.56K | ± 43.89 | ops/s | 10x slower |
| simpleclientAdd | 6.47K | ± 48.83 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 26.62 | ops/s | 10x slower |
| openTelemetryAdd | 3.36K | ± 502.83 | ops/s | 20x slower |
| openTelemetryInc | 3.31K | ± 451.86 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.11K | ± 339.19 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 95.96 | ops/s | 1.1x slower |
| prometheusNative | 3.01K | ± 410.77 | ops/s | 1.7x slower |
| openTelemetryClassic | 766.30 | ± 15.70 | ops/s | 6.6x slower |
| openTelemetryExponential | 568.00 | ± 18.59 | ops/s | 8.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.85K | ± 183.93 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.62K | ± 745.64 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.26K | ± 2.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.34K | ± 4.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.38K | ± 7.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.65K | ± 7.21K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47284.853    ± 243.830  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3356.440    ± 502.830  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3305.115    ± 451.856  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3106.729    ± 339.193  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51365.794    ± 151.895  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65733.742   ± 1535.890  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56715.480    ± 326.315  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6470.778     ± 48.828  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6559.087     ± 43.889  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6358.279     ± 26.618  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        766.299     ± 15.698  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.997     ± 18.589  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5041.833   ± 1480.058  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.282    ± 410.769  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4418.464     ± 95.958  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23615.618    ± 745.642  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23845.514    ± 183.927  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482375.176   ± 7235.676  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481652.794   ± 7212.145  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500343.101   ± 4838.584  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502258.013   ± 2737.372  ops/s
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
