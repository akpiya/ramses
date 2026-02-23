# Modifications of Sink-Sink Interactions

## Sink Particle Interactions

| Interaction | Location / Details | Addressed |
|-------------|--------------------|-----------|
| **Sink → Gas (gravity)** | `poisson/force_fine.f90` → `f_gas_sink`: Plummer-softened acceleration added to gas cells for `direct_force_sink` sinks | ❌ |
| **Sink mass in Poisson** | `pm/rho_fine.f90`: Cloud particles contribute to `rho` via CIC/TSC (`mp=msink/ncloud_sink_massive` for non-direct-force; `mp=0` for direct-force) | ❌ |
| **Gas → Sink (gravity)** | `pm/synchro_fine.f90` (sync): Cloud particles gather grid gravity; `f_gas_sink` computes gas→sink for direct-force sinks | ❌ |
| **Sink → Gas (accretion)** | `pm/sink_particle.f90` → `accrete_sink`: Removes mass, momentum, energy, passive scalars from `unew` | ❌ |
| **Sink → Gas (AGN feedback)** | `pm/sink_particle.f90` → `accrete_sink`: Thermal energy, momentum kicks, RT photon injection when AGN/rt_AGN enabled | ❌ |
| **Sink → Radiation** | `rt/sink_rt_feedback.f90`: `update_sink_RT_feedback`, `sink_RT_feedback` when `rt_sink=.true.` | ❌ |
| **Refinement** | `pm/rho_fine.f90`: Sink regions refined to `nlevelmax_sink` when `sink_refine=.true.` | ❌ |
| **Sink ↔ Sink (gravity)** | `pm/sink_particle.f90` → `f_sink_sink`: Direct N-body, Plummer softening (4 cells), only for `direct_force_sink` sinks | ✅ |

**update_sink_hold(ilevel)** ignores the following capabilities that update_sink(ilevel) implements:
- Overlapping sinks requiring merging
- Ignore non `direct_force_sink` parameters
- Ignore special calculations for periodic boundaries
- Gradient descent - Barzilai&Borwein-like