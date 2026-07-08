# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-08T06:47:35Z
- **Commit:** [`c29367d`](https://github.com/arnabnandy7/client_java/commit/c29367daf4e6aec49eecf321b8e41553c2e194d5)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.25K | ± 2.20K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.49K | ± 311.47 | ops/s | 1.2x slower |
| prometheusAdd | 48.17K | ± 389.09 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.24K | ± 140.33 | ops/s | 1.3x slower |
| simpleclientInc | 6.10K | ± 29.78 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.89K | ± 14.80 | ops/s | 10x slower |
| simpleclientAdd | 5.84K | ± 319.57 | ops/s | 10x slower |
| openTelemetryInc | 4.21K | ± 1.42K | ops/s | 14x slower |
| openTelemetryIncNoLabels | 3.65K | ± 213.27 | ops/s | 16x slower |
| openTelemetryAdd | 3.23K | ± 99.61 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.06K | ± 1.65K | ops/s | **fastest** |
| simpleclient | 4.53K | ± 58.69 | ops/s | 1.6x slower |
| prometheusNative | 3.06K | ± 193.46 | ops/s | 2.3x slower |
| openTelemetryClassic | 697.07 | ± 28.72 | ops/s | 10x slower |
| openTelemetryExponential | 552.82 | ± 21.48 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.56K | ± 126.87 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.13K | ± 166.73 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 564.35K | ± 4.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.46K | ± 3.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 528.96K | ± 5.71K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 517.19K | ± 5.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44240.880    ± 140.328  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3228.797     ± 99.612  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4212.555   ± 1416.261  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3646.491    ± 213.268  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48169.865    ± 389.089  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59245.574   ± 2199.424  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50493.220    ± 311.471  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5842.695    ± 319.574  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6103.160     ± 29.775  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5888.367     ± 14.804  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.072     ± 28.725  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        552.823     ± 21.484  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7057.811   ± 1648.108  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3059.163    ± 193.461  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4526.064     ± 58.685  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27132.461    ± 166.731  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27563.138    ± 126.870  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     517187.032   ± 5222.234  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     528961.927   ± 5705.996  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548462.808   ± 3153.057  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     564353.002   ± 4353.966  ops/s
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
