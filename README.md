# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-10T05:21:26Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.69K | ± 458.51 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.84K | ± 804.24 | ops/s | 1.2x slower |
| prometheusAdd | 46.84K | ± 1.58K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.60K | ± 1.35K | ops/s | 1.4x slower |
| simpleclientInc | 6.04K | ± 155.59 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.00K | ± 183.74 | ops/s | 10.0x slower |
| simpleclientAdd | 5.84K | ± 314.49 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.66K | ± 1.29K | ops/s | 13x slower |
| openTelemetryInc | 4.66K | ± 1.25K | ops/s | 13x slower |
| openTelemetryAdd | 3.53K | ± 106.02 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.76K | ± 2.70K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 80.65 | ops/s | 1.3x slower |
| prometheusNative | 3.08K | ± 127.62 | ops/s | 1.9x slower |
| openTelemetryClassic | 725.61 | ± 4.58 | ops/s | 7.9x slower |
| openTelemetryExponential | 556.94 | ± 44.18 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.54K | ± 268.64 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.50K | ± 278.95 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 579.55K | ± 3.99K | ops/s | **fastest** |
| prometheusWriteToByteArray | 555.61K | ± 18.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.50K | ± 5.67K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 535.86K | ± 4.67K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43601.083   ± 1351.789  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3528.767    ± 106.016  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4657.327   ± 1254.954  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4659.787   ± 1286.017  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      46842.065   ± 1575.779  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59685.595    ± 458.505  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50840.508    ± 804.236  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5835.483    ± 314.486  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6039.585    ± 155.592  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5997.544    ± 183.739  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        725.609      ± 4.577  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.940     ± 44.184  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5762.397   ± 2698.946  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3083.833    ± 127.615  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4548.544     ± 80.651  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27497.496    ± 278.952  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27540.291    ± 268.644  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535856.536   ± 4669.891  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543497.635   ± 5669.283  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     555611.717  ± 18282.278  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579550.141   ± 3992.790  ops/s
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
