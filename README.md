# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-28T06:40:04Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.27K | ± 930.06 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.85K | ± 120.15 | ops/s | 1.1x slower |
| prometheusAdd | 48.65K | ± 950.64 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.22K | ± 1.50K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 51.23 | ops/s | 9.6x slower |
| simpleclientAdd | 5.95K | ± 191.98 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 5.77K | ± 238.06 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.28K | ± 1.37K | ops/s | 11x slower |
| openTelemetryInc | 4.40K | ± 1.13K | ops/s | 13x slower |
| openTelemetryAdd | 3.88K | ± 825.61 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.14K | ± 1.02K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 82.72 | ops/s | 1.2x slower |
| prometheusNative | 2.86K | ± 198.33 | ops/s | 1.8x slower |
| openTelemetryClassic | 699.19 | ± 17.17 | ops/s | 7.4x slower |
| openTelemetryExponential | 521.76 | ± 8.59 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.44K | ± 178.80 | ops/s | **fastest** |
| prometheusWriteToNull | 27.21K | ± 653.11 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 582.65K | ± 2.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 566.62K | ± 7.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 544.35K | ± 9.79K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 531.40K | ± 2.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43223.362   ± 1504.271  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3875.074    ± 825.606  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4396.975   ± 1133.356  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5276.878   ± 1370.406  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48654.429    ± 950.643  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59273.066    ± 930.058  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51849.935    ± 120.148  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5954.519    ± 191.984  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6163.234     ± 51.230  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5769.241    ± 238.056  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.195     ± 17.168  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        521.763      ± 8.592  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5142.346   ± 1015.224  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2862.248    ± 198.329  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4406.053     ± 82.719  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27436.903    ± 178.796  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27213.911    ± 653.109  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531398.227   ± 2418.162  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     544347.547   ± 9788.039  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     566621.106   ± 7520.125  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     582649.790   ± 2028.526  ops/s
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
