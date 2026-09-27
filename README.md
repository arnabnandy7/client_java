# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-27T09:16:29Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.50K | ± 1.55K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 281.15 | ops/s | 1.1x slower |
| prometheusAdd | 50.71K | ± 299.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.93K | ± 1.46K | ops/s | 1.3x slower |
| simpleclientInc | 6.51K | ± 7.12 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 9.03 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 171.05 | ops/s | 10x slower |
| openTelemetryAdd | 3.18K | ± 284.23 | ops/s | 21x slower |
| openTelemetryInc | 3.16K | ± 268.33 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.13K | ± 281.99 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.64K | ± 1.89K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 86.69 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 351.03 | ops/s | 1.9x slower |
| openTelemetryClassic | 770.77 | ± 6.42 | ops/s | 7.3x slower |
| openTelemetryExponential | 606.63 | ± 41.07 | ops/s | 9.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.03K | ± 568.48 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.91K | ± 363.71 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.29K | ± 2.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.25K | ± 2.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.36K | ± 5.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.08K | ± 8.36K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48927.534   ± 1456.010  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3180.653    ± 284.227  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3156.531    ± 268.335  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3129.830    ± 281.992  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50711.138    ± 299.052  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65503.790   ± 1545.131  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57048.379    ± 281.149  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6333.414    ± 171.050  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6513.878      ± 7.121  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6344.060      ± 9.026  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        770.774      ± 6.424  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        606.627     ± 41.073  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5643.308   ± 1888.405  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.916    ± 351.026  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4394.240     ± 86.686  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23911.411    ± 363.712  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24031.213    ± 568.484  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474081.386   ± 8361.294  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480362.862   ± 5618.122  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495250.054   ± 2871.108  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502288.700   ± 2830.126  ops/s
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
