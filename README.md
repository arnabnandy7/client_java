# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-14T05:33:09Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.87K | ± 761.22 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.33K | ± 827.34 | ops/s | 1.2x slower |
| prometheusAdd | 48.84K | ± 774.91 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.56K | ± 1.21K | ops/s | 1.4x slower |
| simpleclientInc | 6.18K | ± 125.27 | ops/s | 9.9x slower |
| openTelemetryInc | 6.05K | ± 185.22 | ops/s | 10x slower |
| simpleclientAdd | 5.95K | ± 293.56 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.90K | ± 29.95 | ops/s | 10x slower |
| openTelemetryAdd | 5.21K | ± 28.33 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 3.80K | ± 178.18 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.20K | ± 1.86K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 35.64 | ops/s | 1.4x slower |
| prometheusNative | 2.93K | ± 181.56 | ops/s | 2.1x slower |
| openTelemetryClassic | 727.69 | ± 28.95 | ops/s | 8.5x slower |
| openTelemetryExponential | 536.34 | ± 10.99 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.42K | ± 287.37 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.31K | ± 322.95 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 581.59K | ± 4.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 571.65K | ± 5.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 547.70K | ± 3.77K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 527.85K | ± 8.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43558.635   ± 1213.033  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5208.137     ± 28.334  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6053.727    ± 185.217  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3795.923    ± 178.181  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48838.106    ± 774.911  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60872.037    ± 761.224  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51326.270    ± 827.344  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5953.204    ± 293.561  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6175.942    ± 125.272  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5904.923     ± 29.946  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        727.695     ± 28.954  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.341     ± 10.993  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6201.611   ± 1864.003  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2927.346    ± 181.555  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.874     ± 35.639  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27308.681    ± 322.949  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27419.169    ± 287.373  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527847.722   ± 8717.203  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     547699.105   ± 3774.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     571646.436   ± 5329.859  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581588.777   ± 4324.625  ops/s
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
