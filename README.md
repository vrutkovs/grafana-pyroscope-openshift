# Continuous profiling

Continuous profiling is technique to collect pprofs from processes and aggregate them similar to 
what Prometheus does to metrics. This enables us to find regressions across different versions and 
find inefficient code paths.

## Profiles

Profiles are 

## How does it work?

Most solutions come with two options:
* direct pprof endpoint scraping
* eBPF ✨

Profiles are fetched, labelled and stored in DB. The UI later on allows to filter profiles by labels and time, displaying the flamegraph as result.

eBPF magic allwos to produce profiles without exposing pprof endpoints. Instead the kernel is instructed to record syscals coming from the process - and the app reconstructs which function was 
called using golang runtime metadata.

The downside of eBPF solution is that it can only record the basics - CPU time and memory usage, while golang pprof endpoint can also expose information about created goroutines and time spent 
on blocking I/O.

## Continuous profiling solution

Two market leaders:
* Parca by PolarSignals - Frederic Branczyk's startup
* Grafana Pyroscope

Parca has pioneered the idea, created custom-made DB and UI, while Pyroscope has great integration with Grafana and somewhat better aggregation methods.

## Pyroscope demo

## Parca demo

## What's next?

Most interested in continuous profiling would be performance team, who already record metrics and logs during performance tests. Profiling results would be useful to determine the source of the 
regression up to a particular function and a change in the codepath.
