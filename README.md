# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-05T10:07:23Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.58K | ± 901.34 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.25K | ± 181.74 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 220.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.56K | ± 1.46K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 10.26 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 17.91 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 41.08 | ops/s | 10x slower |
| openTelemetryInc | 3.40K | ± 495.47 | ops/s | 20x slower |
| openTelemetryAdd | 3.24K | ± 165.13 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.15K | ± 86.53 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.33K | ± 1.28K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 22.84 | ops/s | 1.4x slower |
| prometheusNative | 3.05K | ± 334.99 | ops/s | 2.1x slower |
| openTelemetryClassic | 779.10 | ± 21.59 | ops/s | 8.1x slower |
| openTelemetryExponential | 609.72 | ± 86.66 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.26K | ± 295.29 | ops/s | **fastest** |
| prometheusWriteToNull | 23.25K | ± 935.93 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.22K | ± 11.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.53K | ± 7.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.70K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.80K | ± 4.02K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48556.481   ± 1459.642  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3235.463    ± 165.125  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3403.920    ± 495.474  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3149.017     ± 86.527  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51353.712    ± 220.290  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66582.590    ± 901.340  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57248.265    ± 181.737  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6455.540     ± 17.910  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6594.226     ± 10.262  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.901     ± 41.083  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        779.099     ± 21.589  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        609.719     ± 86.662  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6334.156   ± 1278.856  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3048.144    ± 334.991  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4413.065     ± 22.839  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23255.562    ± 295.289  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23246.409    ± 935.925  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471803.783   ± 4024.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478699.340   ± 3548.009  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482529.520   ± 7649.837  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492217.522  ± 11973.551  ops/s
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
