# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-15T08:53:32Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.77K | ± 1.19K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.80K | ± 783.16 | ops/s | 1.2x slower |
| prometheusAdd | 48.84K | ± 659.35 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.15K | ± 261.28 | ops/s | 1.4x slower |
| simpleclientInc | 6.20K | ± 11.95 | ops/s | 9.6x slower |
| simpleclientAdd | 6.05K | ± 192.92 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.90K | ± 18.80 | ops/s | 10x slower |
| openTelemetryInc | 4.18K | ± 1.26K | ops/s | 14x slower |
| openTelemetryAdd | 3.72K | ± 909.73 | ops/s | 16x slower |
| openTelemetryIncNoLabels | 3.38K | ± 166.38 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.86K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 37.04 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 77.43 | ops/s | 1.7x slower |
| openTelemetryClassic | 683.20 | ± 15.28 | ops/s | 7.8x slower |
| openTelemetryExponential | 533.81 | ± 9.77 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.47K | ± 111.33 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.97K | ± 73.64 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 579.17K | ± 1.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 562.16K | ± 21.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.17K | ± 9.55K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 530.71K | ± 5.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44148.363    ± 261.276  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3723.451    ± 909.734  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4176.492   ± 1261.518  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3380.355    ± 166.376  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48836.614    ± 659.351  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59774.719   ± 1193.131  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51797.156    ± 783.156  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6049.690    ± 192.918  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6195.250     ± 11.952  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5902.374     ± 18.804  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.203     ± 15.280  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.811      ± 9.767  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5361.004   ± 1863.013  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3084.268     ± 77.427  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4342.840     ± 37.040  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26966.304     ± 73.637  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27472.943    ± 111.330  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     530706.601   ± 5740.663  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543169.496   ± 9554.255  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     562164.969  ± 21413.378  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579173.474   ± 1694.327  ops/s
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
