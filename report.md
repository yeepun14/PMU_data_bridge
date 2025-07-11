# Background
## Gewertz square project
Infrastructure Under Development: A RE100 Microgrid — a fully renewable energy-based power grid — composed entirely of power electronics-interfaced sources such as rooftop solar PV and Battery Energy Storage Systems (BESS). In the event of a power outage within Chulalongkorn University, the microgrid will switch to islanding operation mode, operating independently to ensure high reliability and resilience of the electrical system in the Gewertz square buildings. 

The project involves connecting the microgrid to the main grid, which requires **synchronization** between the two systems. Therefore, it is necessary to **collect data in real time**.

### Grid and Microgrid Synchronization
Grid and Microgrid Synchronization refers to the process of aligning a microgrid's electrical parameters (such as voltage, frequency, and phase angle) with those of the main utility grid to ensure safe and stable operation when connecting or disconnecting.

When a microgrid reconnects to the main grid (after operating in island mode) or shares power in grid-connected mode, the following conditions must match:
- Voltage magnitude
- Frequency
- Phase angle
- Phase sequence

If these don’t match, it can lead to:
- Power surges
- Equipment damage
- Unstable grid operation

## Data Bridging project
This project is designed to bridge data from phasor measurement units (PMUs) to Redpanda. The goal is to **facilitate the transfer and processing** of PMU data in a real-time streaming environment.
### Overview
The data bridging process involves extracting PMU data, transforming it into a suitable format, and then loading it into Redpanda for real-time analytics and processing.

![Image](<https://github.com/user-attachments/assets/3b1ec6a9-7486-485f-ba60-60b3b424247a />)

- ### Phasor measurement Units (PMUs)
A device used to measure the electrical parameters on an electricity grid in **real-time data**. It sends data over the network in IEEE C37.118 format.

- ### Phasor Data Concentrator (PDC)

A device used to measure the electrical parameters on an electricity grid in **real-time data**. It sends data over the network in IEEE C37.118 format.

- ### Redpanda
A high-performance streaming platform that is designed for real-time data processing.

- ### TimescaleDB
A time-series database built on PostgreSQL that is suitable for real-time data ingestion and querying.

- ### Grafana
An open-source platform used for data visualization and monitoring.

# what we did

# result
