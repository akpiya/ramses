# Modificaitons of Sink-Sink Interactions

update_sink_hold(ilevel) ignores the following capabilities that update_sink(ilevel) implemenets:
- Overlapping sinks requiring merging
- Ignore non `direct_force_sink` parameters
- Ignore special calculations for periodic boundaries
- Gradient descent - Barzilai&Borwein-like