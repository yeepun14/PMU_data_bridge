# Background
## Gewertz square project
Infrastructure Under Development: A RE100 Microgrid — a fully renewable energy-based power grid — composed entirely of power electronics-interfaced sources such as rooftop solar PV and Battery Energy Storage Systems (BESS). In the event of a power outage within Chulalongkorn University, the microgrid will switch to islanding operation mode, operating independently to ensure high reliability and resilience of the electrical system in the Gewertz square buildings. 

The project involves connecting the microgrid to the main grid, which requires **synchronization** between the two systems. Therefore, it is necessary to **collect data in real time**.

### Grid and Microgrid Synchronization
Grid and Microgrid Synchronization refers to the process of aligning a microgrid's electrical parameters (such as Voltage, Frequency, and Phase angle) with those of the main utility grid to ensure safe and stable operation when connecting.

When a microgrid reconnects to the main grid (after operating in island mode) or shares power in grid-connected mode, the following conditions must match:
- Voltage magnitude
- Frequency
- Phase angle
- Phase sequence

If these don’t match, it can lead to:
- Power surges
- Equipment damage
- Unstable grid operation

### PMU in Grid–Microgrid Synchronization
Phasor Measurement Units (PMUs) play a key role in ensuring safe and stable synchronization between a microgrid and the main grid. They provide time-synchronized, high-resolution measurements of voltage and current phasors, enabling accurate monitoring and control during grid transitions.

**Key Benefits of PMU Integration**
1. Time-Synchronized Data
PMUs use GPS-based time stamping to provide synchronized phasor data, essential for comparing voltage, frequency, and phase angle between the grid and microgrid.
2. Accurate Parameter Matching
Synchronization requires that voltage, frequency, and phase angle are closely aligned. PMUs enable real-time monitoring to ensure safe connection or reconnection.
3. Fast Fault Detection
With high reporting rates (30–120 samples/second), PMUs detect disturbances faster than traditional SCADA, allowing quicker responses to instability.
4. Support for Inverter Control
PMUs enhance the control of inverter-based microgrids by supporting advanced control strategies such as droop control and virtual synchronous operation.
5. Safe Reconnection & Black Start
PMUs facilitate seamless resynchronization after islanding or blackouts by tracking alignment conditions in real time.

## Data Bridging project
This project is designed to bridge data from phasor measurement units (PMUs) to Redpanda. The goal is to **facilitate the transfer and processing** of PMU data in a real-time streaming environment.

### Overview
The data bridging process involves extracting PMU data, transforming it into a suitable format, and then loading it into Redpanda for real-time analytics and processing.

![Image](<https://github.com/user-attachments/assets/3b1ec6a9-7486-485f-ba60-60b3b424247a />)

### Phasor measurement Units (PMUs)
A device used to measure the electrical parameters on an electricity grid in **real-time data**. It sends data over the network in **IEEE C37.118 format.**

> IEEE C37.118.1: Standard for Synchrophasor Measurements for Power Systems have Total Vector Error (TVE) < 1% in steady state

### Phasor Data Concentrator (PDC)

A system that collects data from multiple PMUs and aggregates it for further processing or transmission.

### Redpanda
A high-performance streaming platform that is designed for real-time data processing.

> **Choose Redpanda because** we need a Kafka-compatible streaming system with high 
durability and performance.
You’re building a system with stream processing, event sourcing, or real-time analytics.

| Feature | Redpanda | MQTT Broker |
| --- | --- | -- |
| *Protocol* | Kafka (binary, high-throughput) | MQTT (lightweight, pub/sub) |
| *Performance goal* | High throughput, high durability | Lightweight, low power use |
|*Use case focus*| Streaming big data | Communicating with many small devices | 
|*Persistence*| Strong durability guarantees| Often memory-based with optional persistence |
| *Client types*| Servers, apps, streaming systems | IoT devices, mobile clients |
| *Connectivity* | Not optimized for mobile/IoT | Built for intermittent, unreliable connections |

### TimescaleDB
A time-series database built on PostgreSQL that is suitable for real-time data ingestion and querying.

### Grafana
An open-source platform used for data visualization and monitoring.

### Lab Synchronization (Synchronous Generator)
Study the control of a synchronous generator connected to the power grid. It focuses on synchronization, real power control via mechanical torque, and reactive power control via field current. Key observations include power-angle characteristics and the V-Curve. The **"Dark Lamp Method"** is used for synchronization (A synchronization method using three lamps. When all go dark at once, the generator's voltage matches the grid — indicating the right moment to connect) ,with safety and proper meter usage emphasized.

Lab Simulation from https://perso.univ-lyon1.fr/charles.joubert/web_anim/simen_Pelton_couplee_1.html

![Synchronized_summary](https://github.com/user-attachments/assets/4ca42d7c-28fe-4d93-92c9-b663df7cb976)

When all three lamps go dark simultaneously, it means the voltage from the generator is **equal** in magnitude, frequency, and phase to the grid. At that exact moment, the voltage difference is nearly zero, so **no current flows through the lamps** (I ≈ 0). This ensures a smooth connection without causing **inrush current, arcing, or mechanical stress**, which can damage the generator or system. Synchronizing at any other time would result in a phase mismatch and potentially large circulating currents.

![Synchronized_Lab](https://github.com/user-attachments/assets/ff1ef94a-3b76-484f-893b-13e09f9b8a23)

When all three lamps go dark simultaneously, it indicates that the voltage magnitude, frequency, and phase match. This is the correct moment to close the breaker and synchronize the generator, ensuring a smooth and safe connection without circulating current or electrical stress.

PMUs relates conceptually. The lab involves phasor-based analysis of voltage, current, and power in synchronous generators. PMUs are designed to measure in real-time. PMUs help monitor synchronization, stability, and power flow in large power systems, exactly the kind of behavior being studied in this experiment.

# What we did
### Weekly Progress Summary
| **Week**   | **Date**                             | **Activity Description**                                                                                                                                                                                       |
|------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Week 0** | 15/05/2025                           | **Orientation**: Provided an overview of the internship program and assigned project topics to each group.                                                                                                     |
| **Week 1** | 28/05/2025                           | **Tutorial Session 1**: Introduction to MQTT Communication and ESP32 Programming.                                                                                                                              |
| **Week 2** | 04/06/2025                           | **Tutorial Session 2**: Covered basic Linux commands, database and dashboard setup, Docker, and API server development.                                                                                        |
| **Week 3** | 11/06/2025                           | **Tutorial Session 3**: Introduction to Git and GitHub for version control, and using Node-RED for workflow automation.                                                                                        |
| **Week 4** | 15/06/2025 – 21/06/2025 | Practiced sending data from **pyPMU** and **randomPMU** to **tinyPDC** and subsequently to **Redpanda**. However, sending real PMU data was not yet successful.                                                |
| **Week 5** | 22/06/2025 – 28/06/2025 | Successfully transmitted data to **Redpanda**, processed it into structured orders, and forwarded it to the **database** and **Grafana** for visualization.                                                   |
| **Week 6** | 29/06/2025 – 05/07/2025 | Utilized real-time data from **gridPMU** and **microgridPMU** to compute active (P) and reactive power (Q). The processed data was then sent to the database and Grafana, including phase plot visualizations. |
| **Week 7** | 06/07/2025 – 12/07/2025 | Conducted data ping testing and completed the written report.                                                                                                            |
| **Week 8** | 13/07/2025 – 19/07/2025 | Prepared final presentation materials.                                                      |
| **Week 9** | 20/07/2025 – 21/07/2025 | **Pitch Day**: Final project presentations and official conclusion of the internship program.   

### Phasor measurement Units (PMUs)
PMUs measure values such as voltage (V), current (I), Frequency, and Phase angle in real time, and transmit the data using the IEEE C37.118 protocol — the primary standard for PMU data. The information is sent as a binary stream in a frame-based format.

From [microgridPMU](databridge/microgridPMU.py)

### Phasor Data Concentrator (PDC)
From [microgridPDC](databridge/microgridPDC.py)

```
ใส่โค้ดที่อยากอธิบาย
```
From [tinyPDC_udp](databridge/tinyPDC_udp.py)

```
ใส่โค้ดที่อยากอธิบาย
```

### Message Queue System
TinyPDC retrieves data → Kafka receives and streams the data → PostgreSQL stores the data for future use.

- **Redpanda**\
A high-throughput, low-latency streaming platform based on a distributed log architecture. It supports real-time data ingestion and processing with strong consistency guarantees, making it suitable for event-driven systems and time-sensitive applications. Its built-in management interface facilitates intuitive data stream monitoring and control, enabling seamless integration within modern data pipelines.

From [docker-compose.yml](/databridge/docker-redpanda/docker-compose.yml) Change localhost to Network ip at port 9092 (Kafka broker)

```
localhost: 9092 # change localhost to Network ip
192.168.38.136: 9092
```
- **Consumer**\
From [docker-compose.yml](/databridge/docker-database/docker-compose.yml)

From [json_comsumer_gridPMU](databridge/json_comsumer_gridPMU.py)

```
ใส่โค้ดที่อยากอธิบาย
```

From [json_consumer_microgridPMU](databridge/json_consumer_microgridPMU.py)

```
ใส่โค้ดที่อยากอธิบาย
```

### Database Integration

### Grafana Dashboard

### System Design
We have divided the system into three separate PCs, each performing specific tasks according to the flowchart:

![Flowchart](https://github.com/user-attachments/assets/b24babc6-0878-498b-a049-43a8d84eabdd)

- **PC 1** collects data from two sources: the Microgrid PMU, which provides measurements of Voltage, Frequency, and Phase Angle, and the Grid PMU, which receives data from the utility grid. This PC functions as a data concentrator, converting raw PMU data into a more readable format and calculating Active power (P), Reactive power (Q), and Apparent power (S) for further analysis.

- **PC 2** is responsible for receiving the processed data from PC 1 (Redpanda). Moreover, it is the connected netwerk IP for PC 1 and PC 3 to collect data.

- **PC 3** stores the received data into a database and displays synchronized measurements through a Grafana Dashboard.

(It is not necessary to follow this design)

# Result
