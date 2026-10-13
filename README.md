# Real-Time Big Data Pipeline - Marketplace Interaction Analysis

## Overview

This project implements a **real-time Big Data processing pipeline** that simulates and analyzes interactions on an online marketplace inspired by LeBonCoin.

Using **Apache Spark Structured Streaming**, the system processes continuously generated events, performs time-window aggregations, and applies graph algorithms to analyze relationships between users, sellers, and products.

The results are displayed through an interactive dashboard built with **Dash and Cytoscape**.

## Architecture

The pipeline consists of three components:

1. **Data Generator:** Simulates marketplace interactions and sends JSON events through a TCP socket.
2. **Spark Streaming Pipeline:** Processes incoming events, performs aggregations, and computes graph analytics using GraphFrames.
3. **Interactive Dashboard:** Visualizes relationships, network statistics, and influential nodes in near real time.

**Data Flow**

`Event Generator → TCP Socket → PySpark Structured Streaming → GraphFrames → JSON Files → Dash Dashboard`

## Technologies

| Technology | Purpose |
|---|---|
| Python 3.10+ | Application development |
| PySpark 3.5.3 | Distributed stream processing |
| Spark Structured Streaming | Real-time event processing |
| GraphFrames | Graph analytics and PageRank |
| Dash & Cytoscape | Interactive data visualization |
| Pandas | Data manipulation |
| Java 17 / 21 | Spark runtime |

## Key Features

### Real-Time Data Processing

- Continuous event ingestion through a TCP socket.
- Micro-batch processing every 5 seconds.
- Sliding window aggregations (30-second windows, 10-second intervals).
- Watermarking to handle late-arriving events.
- Two concurrent Spark streaming queries.

### Graph Analytics

Marketplace interactions are represented as a graph containing:

- **Nodes:** Users, sellers, and products.
- **Edges:** Likes, views, purchases, and product listings.

GraphFrames is used to calculate:

- **Connected Components:** Identify connected groups within the network.
- **PageRank:** Measure node influence based on graph relationships.

### Interactive Dashboard

The dashboard provides:

- Automatic updates every 5 seconds.
- Interactive network visualization.
- Real-time statistics on users, sellers, products, and connections.
- Top 3 nodes ranked by PageRank.
- Pause and resume functionality.

## Project Structure

```text
Real-Time-BigData-Pipeline/
├── generator/
│   └── producer.py
├── spark/
│   └── pipeline.py
├── dashboard/
│   └── app.py
├── data/
│   └── graph/
│       ├── vertices.json
│       └── edges.json
├── rapport_bigdata.docx
└── README.md
```

## Installation

### Prerequisites

- Python 3.10 or later
- Java 17 or 21
- PySpark 3.5.3

Clone the repository:

```bash
git clone https://github.com/Benji-7810/Real-Time-BigData-Pipeline.git
cd Real-Time-BigData-Pipeline
```

Install dependencies:

```bash
pip install pyspark==3.5.3 graphframes dash dash-cytoscape pandas
```

GraphFrames 0.8.4 is automatically loaded through Spark's package configuration.

**Important:** Use the pip-installed Spark 3.5.3 environment rather than a system installation of Spark 4.x. Ensure that `SPARK_HOME` and `PYTHONPATH` do not reference an incompatible Spark installation.

## Usage

Run the following commands in three separate terminals from the project root.

**Terminal 1 — Start the Data Generator**

```bash
python3 generator/producer.py
```

**Terminal 2 — Start the Spark Pipeline**

```bash
python3 spark/pipeline.py
```

**Terminal 3 — Launch the Dashboard**

```bash
python3 dashboard/app.py
```

Access the dashboard at:

http://localhost:8050

**Note:** The data generator must be started before the Spark pipeline. The first execution may require additional time to download GraphFrames dependencies.

## Results

The application demonstrates an end-to-end streaming architecture combining event generation, real-time processing, graph analytics, and interactive visualization.

It enables users to:

- Monitor simulated marketplace interactions.
- Analyze relationships between users, sellers, and products.
- Identify connected network components.
- Highlight influential nodes using PageRank.
- Explore continuously updated graph data.

## Author

**Benjamin Bey**

Engineering Student in Applied Mathematics and Computer Science at CY Tech.

[GitHub Profile](https://github.com/Benji-7810)
