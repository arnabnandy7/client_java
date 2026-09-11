# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-11T08:31:26Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusAdd | 34.94K | ± 1.06K | ops/s | **fastest** |
| prometheusNoLabelsInc | 34.92K | ± 1.50K | ops/s | 1.0x slower |
| prometheusInc | 34.87K | ± 665.06 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 34.35K | ± 716.61 | ops/s | 1.0x slower |
| simpleclientInc | 9.12K | ± 100.15 | ops/s | 3.8x slower |
| simpleclientNoLabelsInc | 9.09K | ± 141.84 | ops/s | 3.8x slower |
| simpleclientAdd | 9.00K | ± 125.72 | ops/s | 3.9x slower |
| openTelemetryAdd | 2.37K | ± 272.78 | ops/s | 15x slower |
| openTelemetryIncNoLabels | 2.29K | ± 360.49 | ops/s | 15x slower |
| openTelemetryInc | 2.12K | ± 124.19 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 5.94K | ± 92.74 | ops/s | **fastest** |
| prometheusClassic | 3.71K | ± 1.80K | ops/s | 1.6x slower |
| prometheusNative | 2.08K | ± 152.73 | ops/s | 2.8x slower |
| openTelemetryClassic | 444.08 | ± 50.17 | ops/s | 13x slower |
| openTelemetryExponential | 368.62 | ± 11.75 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.66K | ± 484.08 | ops/s | **fastest** |
| openMetricsWriteToNull | 24.57K | ± 602.42 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 341.54K | ± 3.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 338.27K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 323.02K | ± 4.54K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 317.63K | ± 3.72K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      34349.393    ± 716.606  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2366.949    ± 272.781  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2124.130    ± 124.190  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2288.785    ± 360.489  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      34942.716   ± 1060.071  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      34867.343    ± 665.061  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      34924.880   ± 1500.938  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8998.081    ± 125.718  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9122.852    ± 100.151  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9087.651    ± 141.838  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        444.082     ± 50.168  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        368.617     ± 11.754  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3711.607   ± 1797.231  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2083.712    ± 152.727  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5935.415     ± 92.742  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24567.236    ± 602.424  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24658.263    ± 484.078  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     317628.725   ± 3721.802  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     323024.576   ± 4537.334  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     338274.010   ± 4727.123  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     341544.191   ± 3937.493  ops/s
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
