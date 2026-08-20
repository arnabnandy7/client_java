# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-20T04:22:25Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.25K | ± 3.25K | ops/s | **fastest** |
| prometheusNoLabelsInc | 65.98K | ± 516.38 | ops/s | 1.1x slower |
| prometheusAdd | 61.76K | ± 734.27 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.11K | ± 618.43 | ops/s | 1.3x slower |
| simpleclientAdd | 7.93K | ± 32.21 | ops/s | 9.5x slower |
| simpleclientInc | 7.80K | ± 175.94 | ops/s | 9.6x slower |
| openTelemetryIncNoLabels | 7.66K | ± 475.60 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 7.61K | ± 64.99 | ops/s | 9.9x slower |
| openTelemetryInc | 5.53K | ± 1.80K | ops/s | 14x slower |
| openTelemetryAdd | 4.91K | ± 1.10K | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.44K | ± 2.73K | ops/s | **fastest** |
| simpleclient | 5.37K | ± 127.46 | ops/s | 1.4x slower |
| prometheusNative | 3.73K | ± 310.30 | ops/s | 2.0x slower |
| openTelemetryClassic | 920.88 | ± 34.52 | ops/s | 8.1x slower |
| openTelemetryExponential | 712.99 | ± 29.78 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 35.45K | ± 173.06 | ops/s | **fastest** |
| prometheusWriteToNull | 35.39K | ± 370.55 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 689.47K | ± 8.62K | ops/s | **fastest** |
| prometheusWriteToNull | 684.49K | ± 31.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 654.13K | ± 5.31K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 640.37K | ± 6.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56114.378    ± 618.431  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4914.949   ± 1102.434  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5534.023   ± 1802.612  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7664.737    ± 475.597  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61755.004    ± 734.271  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75249.166   ± 3248.905  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65979.460    ± 516.378  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7931.720     ± 32.212  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7800.156    ± 175.942  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7607.626     ± 64.986  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        920.884     ± 34.523  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        712.987     ± 29.780  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7436.121   ± 2733.360  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3729.663    ± 310.305  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5371.733    ± 127.459  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35447.822    ± 173.062  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35387.712    ± 370.554  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     640366.354   ± 6099.086  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     654134.592   ± 5314.149  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     689474.618   ± 8616.769  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     684489.819  ± 31945.221  ops/s
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
