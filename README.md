# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-15T06:26:33Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.04K | ± 328.85 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.66K | ± 397.58 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 432.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.66K | ± 1.26K | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 40.67 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 180.81 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 188.61 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.29K | ± 253.53 | ops/s | 20x slower |
| openTelemetryInc | 3.03K | ± 211.38 | ops/s | 22x slower |
| openTelemetryAdd | 3.00K | ± 191.72 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.04K | ± 1.73K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 59.64 | ops/s | 1.4x slower |
| prometheusNative | 2.65K | ± 112.88 | ops/s | 2.3x slower |
| openTelemetryClassic | 774.13 | ± 21.24 | ops/s | 7.8x slower |
| openTelemetryExponential | 610.96 | ± 25.80 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.79K | ± 891.63 | ops/s | **fastest** |
| prometheusWriteToNull | 23.46K | ± 861.17 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.76K | ± 4.22K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.77K | ± 3.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.26K | ± 3.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.22K | ± 4.52K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48658.070   ± 1260.884  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3003.984    ± 191.717  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3033.245    ± 211.377  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3294.028    ± 253.529  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51290.423    ± 432.017  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66035.522    ± 328.852  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56656.341    ± 397.577  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6219.336    ± 188.614  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6567.266     ± 40.673  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6386.101    ± 180.814  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        774.132     ± 21.244  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        610.961     ± 25.796  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6040.710   ± 1732.052  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2652.598    ± 112.884  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.692     ± 59.637  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23789.478    ± 891.635  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23464.064    ± 861.174  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474215.003   ± 4517.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476260.693   ± 3209.476  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487770.074   ± 3496.531  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495757.555   ± 4216.411  ops/s
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
