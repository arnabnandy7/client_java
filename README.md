# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-04T06:39:54Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.56K | ± 425.96 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.65K | ± 853.26 | ops/s | 1.2x slower |
| prometheusAdd | 47.98K | ± 216.28 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.02K | ± 96.31 | ops/s | 1.4x slower |
| simpleclientInc | 6.13K | ± 58.08 | ops/s | 9.7x slower |
| simpleclientAdd | 5.92K | ± 428.17 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.88K | ± 12.38 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.66K | ± 1.64K | ops/s | 11x slower |
| openTelemetryAdd | 4.53K | ± 890.18 | ops/s | 13x slower |
| openTelemetryInc | 3.57K | ± 263.43 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.01K | ± 1.79K | ops/s | **fastest** |
| simpleclient | 4.19K | ± 56.35 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 222.73 | ops/s | 1.7x slower |
| openTelemetryClassic | 737.09 | ± 34.40 | ops/s | 6.8x slower |
| openTelemetryExponential | 555.76 | ± 7.53 | ops/s | 9.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.31K | ± 168.94 | ops/s | **fastest** |
| prometheusWriteToNull | 27.27K | ± 172.07 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 582.49K | ± 13.47K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.29K | ± 8.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.41K | ± 2.53K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 528.58K | ± 11.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44020.625     ± 96.313  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4526.047    ± 890.182  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3571.981    ± 263.430  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5664.312   ± 1638.011  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47976.355    ± 216.280  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59555.661    ± 425.960  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51648.895    ± 853.257  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5923.096    ± 428.171  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6126.594     ± 58.084  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5883.879     ± 12.382  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        737.090     ± 34.397  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.759      ± 7.530  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5011.957   ± 1793.593  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2922.928    ± 222.731  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4185.349     ± 56.346  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27307.222    ± 168.942  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27270.679    ± 172.073  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528583.709  ± 11323.797  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546407.876   ± 2525.720  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568287.785   ± 8748.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     582486.123  ± 13469.029  ops/s
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
