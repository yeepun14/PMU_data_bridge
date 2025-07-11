# background
## Gewertz square project
Infrastructure Under Development: A RE100 Microgrid — a fully renewable energy-based power grid — composed entirely of power electronics-interfaced sources such as rooftop solar PV and Battery Energy Storage Systems (BESS). In the event of a power outage within Chulalongkorn University, the microgrid will switch to islanding operation mode, operating independently to ensure high reliability and resilience of the electrical system in the Gewertz square buildings. 

This project is designed to bridge data from phasor measurement units (PMUs) to Redpanda. The goal is to **facilitate the transfer and processing** of PMU data in a real-time streaming environment.
### Overview
The data bridging process involves extracting PMU data, transforming it into a suitable format, and then loading it into Redpanda for real-time analytics and processing.

![Image](<https://github.com/user-attachments/assets/3b1ec6a9-7486-485f-ba60-60b3b424247a />)

- ### Phasor measurement Units
A device used to measure the electrical parameters on an electricity grid in **real-time data**. It sends data over the network in IEEE C37.118 format.

- ### PDC (Phasor Data Concentrator)

A device used to measure the electrical parameters on an electricity grid in **real-time data**. It sends data over the network in IEEE C37.118 format.

- ### Redpanda
A high-performance streaming platform that is designed for real-time data processing.

- ### TimescaleDB
A time-series database built on PostgreSQL that is suitable for real-time data ingestion and querying.

# what we did

# result
