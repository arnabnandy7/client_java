# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-30T09:31:12Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.74K | ± 98.34 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.86K | ± 1.21K | ops/s | 1.2x slower |
| prometheusAdd | 51.12K | ± 231.75 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.12K | ± 135.41 | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 44.92 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 18.76 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 376.62 | ops/s | 11x slower |
| openTelemetryAdd | 3.35K | ± 151.06 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.22K | ± 196.33 | ops/s | 20x slower |
| openTelemetryInc | 3.15K | ± 220.54 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.23K | ± 702.82 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 71.95 | ops/s | 1.4x slower |
| prometheusNative | 2.69K | ± 44.87 | ops/s | 2.3x slower |
| openTelemetryClassic | 754.10 | ± 39.96 | ops/s | 8.3x slower |
| openTelemetryExponential | 658.93 | ± 71.90 | ops/s | 9.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.28K | ± 786.84 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.62K | ± 1.16K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.66K | ± 1.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.63K | ± 5.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.67K | ± 1.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.80K | ± 5.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50124.549    ± 135.415  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3353.649    ± 151.062  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3152.754    ± 220.544  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3224.212    ± 196.327  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51123.375    ± 231.752  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65738.466     ± 98.342  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55860.240   ± 1214.100  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6180.810    ± 376.618  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6531.365     ± 44.924  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.812     ± 18.759  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        754.096     ± 39.957  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        658.930     ± 71.896  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6234.225    ± 702.823  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2690.099     ± 44.866  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.350     ± 71.952  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23624.975   ± 1159.625  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24276.167    ± 786.844  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483802.784   ± 5056.336  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488665.808   ± 1624.285  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499633.828   ± 5483.315  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509657.034   ± 1923.811  ops/s
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
