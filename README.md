# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-30T09:36:07Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.29K | ± 1.62K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.08K | ± 976.78 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 60.84K | ± 1.73K | ops/s | 1.1x slower |
| prometheusAdd | 55.41K | ± 1.97K | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 10.99K | ± 283.96 | ops/s | 6.0x slower |
| simpleclientAdd | 10.54K | ± 468.75 | ops/s | 6.3x slower |
| simpleclientInc | 10.39K | ± 247.46 | ops/s | 6.4x slower |
| openTelemetryIncNoLabels | 7.62K | ± 610.55 | ops/s | 8.7x slower |
| openTelemetryInc | 5.81K | ± 587.52 | ops/s | 11x slower |
| openTelemetryAdd | 4.50K | ± 42.80 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 8.95K | ± 1.55K | ops/s | **fastest** |
| simpleclient | 6.71K | ± 129.05 | ops/s | 1.3x slower |
| prometheusNative | 5.28K | ± 174.25 | ops/s | 1.7x slower |
| openTelemetryClassic | 888.14 | ± 18.96 | ops/s | 10x slower |
| openTelemetryExponential | 717.80 | ± 32.70 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 32.68K | ± 1.78K | ops/s | **fastest** |
| openMetricsWriteToNull | 32.42K | ± 610.59 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 751.20K | ± 23.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 728.44K | ± 52.58K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 672.88K | ± 50.95K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 665.02K | ± 10.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      60840.060   ± 1727.671  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4503.326     ± 42.803  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5813.145    ± 587.520  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7615.069    ± 610.546  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      55410.620   ± 1971.817  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66293.527   ± 1622.432  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66078.131    ± 976.776  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10543.833    ± 468.751  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10390.938    ± 247.463  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10994.735    ± 283.960  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        888.145     ± 18.965  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        717.800     ± 32.705  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8947.578   ± 1547.048  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5283.990    ± 174.246  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6712.227    ± 129.052  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32423.510    ± 610.590  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      32678.220   ± 1782.918  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     672879.388  ± 50946.240  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     665023.789  ± 10827.216  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     728444.683  ± 52577.420  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     751196.512  ± 23885.052  ops/s
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
