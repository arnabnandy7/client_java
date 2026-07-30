# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-30T06:34:18Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.23K | ± 908.41 | ops/s | **fastest** |
| prometheusNoLabelsInc | 49.78K | ± 2.33K | ops/s | 1.2x slower |
| prometheusAdd | 48.37K | ± 1.25K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.38K | ± 1.42K | ops/s | 1.4x slower |
| openTelemetryInc | 6.16K | ± 92.69 | ops/s | 9.6x slower |
| simpleclientInc | 6.13K | ± 60.77 | ops/s | 9.7x slower |
| simpleclientAdd | 6.10K | ± 44.52 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.04K | ± 208.86 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 5.24K | ± 1.65K | ops/s | 11x slower |
| openTelemetryAdd | 3.41K | ± 146.71 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 800.90 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 111.90 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 259.54 | ops/s | 1.9x slower |
| openTelemetryClassic | 703.24 | ± 5.30 | ops/s | 7.8x slower |
| openTelemetryExponential | 563.04 | ± 19.92 | ops/s | 9.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.36K | ± 249.24 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.29K | ± 126.34 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 585.48K | ± 5.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 565.58K | ± 11.76K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 545.82K | ± 2.98K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 534.51K | ± 3.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42377.577   ± 1424.878  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3410.072    ± 146.708  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6156.091     ± 92.692  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5239.954   ± 1645.400  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48368.480   ± 1248.332  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59232.298    ± 908.409  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      49776.911   ± 2333.694  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6100.354     ± 44.521  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6126.265     ± 60.769  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6036.146    ± 208.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.245      ± 5.301  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.038     ± 19.915  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5469.429    ± 800.897  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2918.887    ± 259.537  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.045    ± 111.895  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27292.974    ± 126.336  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27358.496    ± 249.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     534508.171   ± 3268.929  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     545816.021   ± 2979.816  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     565577.788  ± 11764.649  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     585481.547   ± 5845.528  ops/s
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
