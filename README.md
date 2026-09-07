# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-07T08:33:10Z
- **Commit:** [`79a5990`](https://github.com/arnabnandy7/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.79K | ± 272.40 | ops/s | **fastest** |
| prometheusNoLabelsInc | 63.29K | ± 581.10 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 56.57K | ± 9.16K | ops/s | 1.2x slower |
| prometheusAdd | 56.35K | ± 2.14K | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 10.56K | ± 344.13 | ops/s | 6.2x slower |
| simpleclientInc | 10.51K | ± 147.15 | ops/s | 6.3x slower |
| simpleclientAdd | 10.26K | ± 256.56 | ops/s | 6.4x slower |
| openTelemetryIncNoLabels | 7.47K | ± 1.14K | ops/s | 8.8x slower |
| openTelemetryAdd | 5.25K | ± 958.46 | ops/s | 13x slower |
| openTelemetryInc | 5.22K | ± 215.20 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.37K | ± 1.38K | ops/s | **fastest** |
| simpleclient | 6.69K | ± 21.45 | ops/s | 1.1x slower |
| prometheusNative | 4.73K | ± 287.81 | ops/s | 1.6x slower |
| openTelemetryClassic | 923.24 | ± 16.66 | ops/s | 8.0x slower |
| openTelemetryExponential | 719.42 | ± 14.36 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 32.40K | ± 224.54 | ops/s | **fastest** |
| openMetricsWriteToNull | 32.31K | ± 150.73 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 721.96K | ± 42.96K | ops/s | **fastest** |
| prometheusWriteToNull | 692.54K | ± 21.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 686.80K | ± 13.59K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 666.61K | ± 41.18K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56573.022   ± 9155.778  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5254.143    ± 958.456  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5220.086    ± 215.199  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7474.510   ± 1142.803  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56350.754   ± 2140.911  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65791.314    ± 272.396  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63293.059    ± 581.096  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10263.970    ± 256.558  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10510.291    ± 147.150  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10557.126    ± 344.131  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        923.237     ± 16.664  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        719.423     ± 14.357  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7374.179   ± 1383.782  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4734.374    ± 287.814  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6693.942     ± 21.446  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32313.623    ± 150.730  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      32403.691    ± 224.537  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     666606.046  ± 41181.893  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     686799.967  ± 13586.789  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     721963.069  ± 42961.214  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     692543.541  ± 21556.633  ops/s
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
