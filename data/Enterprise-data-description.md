# AI Data Centre Multi-Scale Electrical Load Dataset (2024 & 2026)

## Abstract

This dataset provides two comprehensive, physics-based, multi-scale electrical load profiles for an enterprise-scale artificial intelligence (AI)-driven data centre, covering two independent full years of hourly operation totalling **17,520 hourly records**. The first file covers calendar year 2024 and the second covers calendar year 2026. Both files were constructed using manufacturer-published hardware specifications and standard electrical engineering parameters applied to an identical facility model comprising 500 CPU servers across 13 CPU racks and 100 GPU servers hosting 400 NVIDIA A100 GPUs across 13 GPU racks, served by three power distribution units. The facility configuration reflects a realistic medium-scale AI data centre with a total installed IT capacity of approximately 466 kW peak.

The two files are complementary and cover contrasting operating conditions. The 2024 file represents a cold-climate ambient temperature regime, with temperatures ranging from approximately −5 °C to +40 °C, producing seasonal variation in cooling demand, coefficient of performance, and power usage effectiveness. The 2026 file represents a warm-climate ambient temperature regime, with temperatures consistently between 20 °C and 35 °C, reflecting conditions representative of Gulf region and subtropical data centre environments. Together the two files enable cross-year and cross-climate generalisation studies that neither file alone can support.

The 2026 file contains 49 variables per timestep and provides the most complete reactive power coverage of the two files, with active and reactive power reported at every layer of the electrical hierarchy: CPU fleet, GPU fleet, memory, storage, network interface cards, accessories and fans, top-of-rack switches, rack losses, PDU losses, UPS losses, transformer losses, cable losses, cooling system, lighting, and facility auxiliary loads. The inclusion of reactive power at each electrical layer is a distinguishing characteristic of this file relative to existing public data centre datasets, which typically report active power only. The 2026 file was used in the associated journal publication and is the primary dataset of this submission.

The 2024 file contains 47 variables per timestep and provides extended variable coverage not present in the 2026 file, including per-server active and reactive power for both CPU and GPU servers, per-rack utilisation ratios for CPU and GPU racks, PDU utilisation ratio, apparent power at the facility level in kVA, facility power factor per timestep, and IT subsystem power factor. This extended coverage makes the 2024 file particularly suitable for per-server power modelling, rack capacity planning, and power quality studies.

Physical consistency was verified in both files against four algebraic energy-balance relations: IT load equality, total-loss summation, facility-load balance, and power usage effectiveness computation. All four checks passed across all 8,760 records in each file, with maximum absolute errors below 0.002 kW for power balance checks and below 5.5 × 10⁻⁵ for PUE computation. The mean facility active power is 409.14 kW and the peak facility active power is 723.33 kW in the 2026 file, with a mean PUE of 1.552 and annual energy consumption of approximately 3.584 GWh. The 2024 file reports a mean facility active power of approximately 390 kW, a peak of approximately 600 kW, and a mean PUE of approximately 1.50, with annual energy consumption of approximately 3.41 GWh.

This dataset submission addresses a documented gap in the public data centre research literature, where no existing dataset simultaneously provides rack-level electrical data, PDU and UPS loading profiles, reactive power components, cooling-load coupling, and computational workload variables in an integrated hourly format across multiple years and climate regimes. Both files are released to advance reproducible research in AI data centre load forecasting, multi-scale electrical modelling, workload scheduling, resilience assessment, digital twin development, power quality analysis, and smart grid integration of large-scale digital infrastructure.

---

## Instructions

This submission contains two dataset files covering two independent annual operating cycles of the same enterprise-scale AI-driven data centre facility model. Both datasets were generated using manufacturer-published hardware specifications and standard electrical engineering parameters applied to an identical facility configuration. Together they provide 17,520 hourly records spanning contrasting ambient temperature regimes and workload profiles.

The 2026 dataset was used in the associated journal publication. The 2024 dataset is released as a companion resource with extended variable coverage.

### Files included

| # | Filename | Coverage | Records | Sheet name |
|---|---|---|---|---|
| 1 | `DC_Load_Dataset_500CPU_100GPU_2024_Hourly.xlsx` | Calendar year 2024 | 8,760 | `Full_Dataset` |
| 2 | `DC_Load_Dataset_500CPU_100GPU_2026_Hourly.xlsx` | Calendar year 2026 | 8,760 | `Hourly_PQ_Data` |

### Shared facility configuration (both files)

| Parameter | Value |
|---|---|
| CPU-only servers | 500 |
| GPU servers | 100 |
| GPUs per GPU server | 4 (NVIDIA A100 SXM) |
| Total GPUs | 400 |
| CPU racks | 13 |
| GPU racks | 13 |
| Total racks | 26 |
| PDUs | 3 |
| CPU server idle / peak power | 120 W / 500 W |
| GPU server idle / peak power | 350 W / 2,200 W |
| PSU efficiency | 0.93 |
| PDU efficiency | 0.973 |
| UPS efficiency | 0.96 |
| Transformer efficiency | 0.985 |
| Lighting load | 15 kW |
| BMS and security load | 8 kW |

### Key differences between the two files

| Aspect | 2024 file | 2026 file |
|---|---|---|
| Ambient temperature range | ≈ −5 °C to +40 °C (cold-climate regime) | ≈ 20 °C to 35 °C (warm-climate regime) |
| Number of variables | 47 | 49 |

**Variables present in the 2024 file only**

- Per-server CPU and GPU power (watts)
- Per-rack utilisation ratios (`R_rack_CPU`, `R_rack_GPU`)
- PDU utilisation ratio (`R_PDU`)
- Apparent power `S_facility` (kVA)
- Facility power factor (`PF_facility`, per timestep)
- IT power factor (`PF_IT`)

**Variables present in the 2026 file only**

- Full reactive power coverage at every electrical layer, including memory, storage, NIC, accessories, ToR switches, rack losses, and all infrastructure loss components

**Both files include**

- Active and reactive power at CPU fleet, GPU fleet, IT total, PDU, UPS, transformer, cable, cooling, lighting, and facility levels

---

## Column descriptions — 2026 file (sheet: `Hourly_PQ_Data`)

**Temporal identifiers**

`timestamp`, `year`, `month`, `day`, `hour`, `day_of_week`, `is_weekend`

**Facility configuration (constant)**

`cpu_server_count` (500), `gpu_server_count` (100), `gpus_per_gpu_server` (4)

**Utilisation and environmental variables**

| Variable | Description |
|---|---|
| `cpu_util_cpu_servers` | CPU utilisation of CPU-only servers (0 to 1) |
| `cpu_util_gpu_servers` | CPU utilisation of GPU servers (0 to 1) |
| `gpu_util_gpu_servers` | GPU utilisation of GPU servers (0 to 1) |
| `workload_intensity_gamma` | Normalised workload arrival intensity (0 to 1) |
| `ambient_temp_C` | Ambient temperature (°C) |
| `rack_temp_C` | Average rack inlet temperature (°C) |

**Active and reactive power variables (kW and kVAr pairs)**

| Active / reactive pair | Description |
|---|---|
| `P_CPU_kW` / `Q_CPU_kVAr` | CPU fleet power |
| `P_GPU_kW` / `Q_GPU_kVAr` | GPU fleet power |
| `P_memory_kW` / `Q_memory_kVAr` | Memory subsystem power |
| `P_storage_kW` / `Q_storage_kVAr` | Storage subsystem power |
| `P_NIC_kW` / `Q_NIC_kVAr` | Network interface card power |
| `P_accessories_fans_kW` / `Q_accessories_fans_kVAr` | Accessories and cooling fans |
| `P_ToR_switches_kW` / `Q_ToR_switches_kVAr` | Top-of-rack switch power |
| `P_IT_before_rack_losses_kW` / `Q_IT_before_rack_losses_kVAr` | IT power before rack losses |
| `P_rack_losses_kW` / `Q_rack_losses_kVAr` | Rack conversion and cable losses |
| `P_IT_total_kW` / `Q_IT_total_kW` | Total IT power including rack losses |
| `P_PDU_losses_kW` / `Q_PDU_losses_kVAr` | PDU losses |
| `P_UPS_losses_kW` / `Q_UPS_losses_kVAr` | UPS losses |
| `P_transformer_losses_kW` / `Q_transformer_losses_kVAr` | Transformer losses |
| `P_cable_losses_kW` / `Q_cable_losses_kVAr` | External cable losses |
| `P_cooling_kW` / `Q_cooling_kVAr` | Cooling system power |
| `P_lighting_kW` / `Q_lighting_kVAr` | Lighting load |
| `P_facility_aux_kW` / `Q_facility_aux_kVAr` | BMS and security auxiliary load |

---

## Column descriptions — 2024 file (sheet: `Full_Dataset`)

**Temporal and environmental variables**

`Timestamp`, `Month`, `Day` (name), `Hour`, `T_amb` (°C)

**Utilisation variables**

`u_CPU fleet` (0 to 1), `u_GPU fleet` (0 to 1)

**CPU fleet power**

`P_CPU fleet` (kW), `Q_CPU fleet` (kVAr), `P_CPU/server` (W), `Q_CPU/server` (VAr)

**GPU fleet power**

`P_GPU fleet` (kW), `Q_GPU fleet` (kVAr), `P_GPU/server` (W), `Q_GPU/server` (VAr)

**IT and rack level**

- `P_IT total` (kW), `Q_IT total` (kVAr), `PF_IT`
- `P_rack CPU avg` (kW), `Q_rack CPU avg` (kVAr), `R_rack CPU`
- `P_rack GPU avg` (kW), `Q_rack GPU avg` (kVAr), `R_rack GPU`

**PDU level**

`P_PDU avg` (kW), `Q_PDU avg` (kVAr), `R_PDU`

**Electrical losses**

- `P_PSU loss` (kW), `Q_PSU loss` (kVAr)
- `P_PDU loss` (kW), `Q_PDU loss` (kVAr)
- `P_UPS loss` (kW), `Q_UPS loss` (kVAr)
- `P_XFMR loss` (kW), `Q_XFMR loss` (kVAr)
- `P_cable loss` (kW), `Q_cable loss` (kVAr)
- `P_loss total` (kW), `Q_loss total` (kVAr)

**Cooling**

`COP` (per timestep), `P_cooling` (kW), `Q_cooling` (kVAr)

**Fixed loads**

`P_lighting` (kW), `Q_lighting` (kVAr), `P_BMS/sec` (kW), `Q_BMS/sec` (kVAr)

**Facility level**

`P_facility` (kW), `Q_facility` (kVAr), `S_facility` (kVA), `PF_facility`

---

## Key statistics

| Metric | 2024 file | 2026 file |
|---|---|---|
| Records | 8,760 | 8,760 |
| Mean facility active power | ≈ 390 kW | 409.14 kW |
| Peak facility active power | ≈ 600 kW | 723.33 kW |
| Mean PUE | ≈ 1.50 | 1.552 (range 1.452–1.699) |
| Annual energy | ≈ 3.41 GWh | ≈ 3.584 GWh |
| Missing values | None | None |
| Duplicate timestamps | None | None |