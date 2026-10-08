# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-08T10:45:25Z
- **Commit:** [`d8089b2`](https://github.com/arnabnandy7/client_java/commit/d8089b219004512f136a5e3d6153df74ddfbe748)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1012-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 557.01M | ± 8539.42K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.38M | ± 389.80K | ops/s |
| prometheusLabelValuesInc | 116.84M | ± 2979.18K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.30M | ± 649.47K | ops/s |
| prometheusInc | 64.91K | ± 1.74K | ops/s |
| prometheusNoLabelsInc | 56.84K | ± 799.70 | ops/s |
| prometheusAdd | 49.76K | ± 1.50K | ops/s |
| codahaleIncNoLabels | 49.29K | ± 1.80K | ops/s |
| openTelemetryBoundInc | 37.66K | ± 609.47 | ops/s |
| openTelemetryBoundAdd | 30.91K | ± 1.24K | ops/s |
| openTelemetryIncNoLabels | 22.51K | ± 863.48 | ops/s |
| openTelemetryInc | 18.08K | ± 250.71 | ops/s |
| openTelemetryAdd | 15.44K | ± 246.31 | ops/s |
| simpleclientInc | 6.49K | ± 87.67 | ops/s |
| simpleclientAdd | 6.40K | ± 62.01 | ops/s |
| simpleclientNoLabelsInc | 6.32K | ± 160.75 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.98K | ± 191.12 | ops/s |
| prometheusClassic | 6.69K | ± 814.57 | ops/s |
| prometheusClassicSingleThread | 4.55K | ± 12.79 | ops/s |
| simpleclient | 4.37K | ± 73.14 | ops/s |
| openTelemetryBoundClassic | 4.20K | ± 53.82 | ops/s |
| openTelemetryClassic | 4.18K | ± 940.84 | ops/s |
| prometheusNative | 2.69K | ± 374.74 | ops/s |
| openTelemetryBoundExponential | 1.05K | ± 72.42 | ops/s |
| openTelemetryExponential | 821.12 | ± 61.72 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.76K | ± 566.56 | ops/s |
| openMetricsWriteToNull | 23.11K | ± 950.53 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 494.75K | ± 4.05K | ops/s |
| prometheusWriteToNull | 493.16K | ± 8.10K | ops/s |
| openMetricsWriteToNull | 476.29K | ± 3.61K | ops/s |
| openMetricsWriteToByteArray | 473.47K | ± 9.66K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.051 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.041 | — | — |
| CounterBenchmark.prometheusAdd | 0.074 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.057 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.145 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.148 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.222 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.895 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.231 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.133 | — | — |
| HistogramBenchmark.prometheusClassic | 0.557 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.680 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.641 | — | — |
| HistogramBenchmark.prometheusNative | 335793.400 | — | — |
| HistogramBenchmark.simpleclient | 0.213 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.151 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.147 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49288.241   ± 1798.425  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15441.341    ± 246.308  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      30909.910   ± 1235.093  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37656.896    ± 609.466  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18079.389    ± 250.708  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22513.817    ± 863.481  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49758.923   ± 1501.659  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  557007717.773 ± 8539421.528  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334382044.347 ± 389796.353  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64911.402   ± 1740.927  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  116842081.557 ± 2979183.580  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58301922.887 ± 649466.509  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56839.972    ± 799.700  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6397.530     ± 62.015  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6488.624     ± 87.673  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6323.939    ± 160.748  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4196.190     ± 53.816  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1045.998     ± 72.416  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4178.290    ± 940.837  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        821.124     ± 61.715  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6685.158    ± 814.571  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11980.239    ± 191.120  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4550.638     ± 12.790  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2692.518    ± 374.740  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4371.117     ± 73.142  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23108.321    ± 950.528  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23759.002    ± 566.558  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473465.676   ± 9655.108  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476292.428   ± 3606.801  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494747.815   ± 4049.993  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493156.172   ± 8103.533  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
