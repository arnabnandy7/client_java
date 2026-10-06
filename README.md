# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-06T10:09:42Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.04K | ± 1.37K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.82K | ± 511.59 | ops/s | 1.1x slower |
| prometheusAdd | 51.36K | ± 295.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.29K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientInc | 6.63K | ± 69.85 | ops/s | 9.8x slower |
| simpleclientAdd | 6.46K | ± 16.53 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 30.69 | ops/s | 10x slower |
| openTelemetryInc | 3.38K | ± 425.26 | ops/s | 19x slower |
| openTelemetryAdd | 3.06K | ± 156.10 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.05K | ± 18.45 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.07K | ± 1.53K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 58.84 | ops/s | 1.4x slower |
| prometheusNative | 3.00K | ± 360.53 | ops/s | 2.0x slower |
| openTelemetryClassic | 772.32 | ± 13.07 | ops/s | 7.9x slower |
| openTelemetryExponential | 696.56 | ± 82.73 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.03K | ± 275.69 | ops/s | **fastest** |
| prometheusWriteToNull | 23.56K | ± 702.76 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 501.55K | ± 4.84K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.26K | ± 4.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.66K | ± 4.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.22K | ± 4.01K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48294.095   ± 1502.107  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3059.545    ± 156.102  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3380.842    ± 425.259  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3049.777     ± 18.446  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51362.744    ± 295.839  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65044.784   ± 1369.807  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56818.509    ± 511.590  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6464.342     ± 16.535  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6630.922     ± 69.853  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6365.478     ± 30.685  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        772.322     ± 13.066  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        696.558     ± 82.731  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6065.214   ± 1527.622  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2999.589    ± 360.533  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4385.496     ± 58.843  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24034.236    ± 275.685  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23559.365    ± 702.756  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481223.186   ± 4011.890  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483657.309   ± 4354.641  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495260.179   ± 4790.139  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     501553.469   ± 4839.125  ops/s
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
