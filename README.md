# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-17T08:48:58Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.84K | ± 729.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.19K | ± 876.41 | ops/s | 1.2x slower |
| prometheusAdd | 48.24K | ± 642.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.39K | ± 1.34K | ops/s | 1.4x slower |
| simpleclientInc | 6.20K | ± 96.28 | ops/s | 9.8x slower |
| simpleclientAdd | 5.93K | ± 202.05 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.92K | ± 19.33 | ops/s | 10x slower |
| openTelemetryAdd | 3.80K | ± 888.09 | ops/s | 16x slower |
| openTelemetryIncNoLabels | 3.45K | ± 250.25 | ops/s | 18x slower |
| openTelemetryInc | 3.43K | ± 231.89 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.07K | ± 1.04K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 163.68 | ops/s | 1.2x slower |
| prometheusNative | 2.87K | ± 231.06 | ops/s | 1.8x slower |
| openTelemetryClassic | 712.62 | ± 26.78 | ops/s | 7.1x slower |
| openTelemetryExponential | 539.01 | ± 11.17 | ops/s | 9.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.46K | ± 127.91 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.32K | ± 362.80 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 586.71K | ± 6.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 577.28K | ± 7.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 554.63K | ± 5.81K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 537.69K | ± 1.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43389.010   ± 1341.579  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3803.866    ± 888.086  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3434.838    ± 231.894  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3445.110    ± 250.246  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48237.334    ± 642.678  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60836.596    ± 729.694  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51189.659    ± 876.405  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5925.050    ± 202.051  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6195.195     ± 96.282  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5918.516     ± 19.334  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.617     ± 26.785  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.012     ± 11.173  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5068.236   ± 1040.708  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2874.910    ± 231.063  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4350.103    ± 163.684  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27322.665    ± 362.801  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27462.666    ± 127.914  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     537690.395   ± 1936.425  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     554630.728   ± 5810.211  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     577279.820   ± 7525.600  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     586707.379   ± 6140.991  ops/s
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
