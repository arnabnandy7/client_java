# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-02T08:20:10Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.13K | ± 1.21K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.98K | ± 761.55 | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 315.92 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.53K | ± 4.68K | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 39.64 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.34K | ± 13.75 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 213.09 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.28K | ± 462.79 | ops/s | 20x slower |
| openTelemetryInc | 3.20K | ± 444.69 | ops/s | 20x slower |
| openTelemetryAdd | 2.93K | ± 264.71 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.44K | ± 2.28K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 58.60 | ops/s | 1.5x slower |
| prometheusNative | 3.10K | ± 263.67 | ops/s | 2.1x slower |
| openTelemetryClassic | 753.01 | ± 28.61 | ops/s | 8.5x slower |
| openTelemetryExponential | 637.55 | ± 33.05 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.79K | ± 493.78 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.78K | ± 624.18 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 508.72K | ± 5.29K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.80K | ± 2.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.34K | ± 3.59K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.93K | ± 3.26K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47532.889   ± 4683.855  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2926.215    ± 264.708  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3198.180    ± 444.686  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3281.017    ± 462.790  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51219.422    ± 315.923  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65132.653   ± 1206.557  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55983.293    ± 761.551  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6325.829    ± 213.089  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6569.137     ± 39.638  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6335.950     ± 13.749  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        753.014     ± 28.605  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        637.547     ± 33.045  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6435.968   ± 2277.197  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3095.951    ± 263.672  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.749     ± 58.600  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23776.582    ± 624.182  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23787.349    ± 493.781  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479932.669   ± 3262.676  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486344.629   ± 3594.151  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500797.500   ± 2493.821  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508721.960   ± 5294.795  ops/s
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
