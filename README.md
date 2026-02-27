# Distributed Gesture Recognition System IEEE Student Workshop | Spring 2026

## Overview
This workshop is an intensive deep dive into Distributed Embedded Systems and Edge-to-Cloud Telemetry. Participants collaborate to build a 20-node sensor grid using STM32 microcontrollers to capture motion data. This data is aggregated by an NVIDIA Jetson Orin Nano and visualized in a real-time Google Colab dashboard, demonstrating the full lifecycle of data from bare-metal hardware to cloud-based analytics.

## Workshop Learning Objectives

* Embedded C (Bare-Metal): Programming ARM Cortex-M MCUs for high-frequency sensor sampling.
* Real-Time DSP: Implementing IIR Low-Pass Filters to stabilize noisy accelerometer/gyroscope signals.
* Serial Protocols: Navigating data ingestion via SPI/I2C in a high-density node environment.
* Edge-to-Cloud Telemetry: Using a Jetson Orin Nano as a gateway to push live data to a cloud dashboard.
* Cloud Analytics: Utilizing Google Colab for real-time visualization of 20 simultaneous data streams.

## System Architecture
1. The Edge Nodes (STM32)
Each participant manages a dedicated sensor node.
Hardware: STM32 + MPU6050 (6-axis IMU).
Task: Implement an IIR Low-Pass Filter in Embedded C to isolate intended gestures from mechanical vibration.
Constraint: No RTOS used—timing is managed via hardware interrupts and timers to ensure a strictly deterministic 100Hz sampling rate.

2. The Gateway (NVIDIA Jetson Orin Nano)
Role: Central Data Hub.
Logic: The Jetson polls all 20 nodes via a shared serial bus, applies a classification model, and acts as a bridge to the cloud.
Networking: Pushes aggregated JSON packets to a cloud-based database (Firebase or Google Sheets API) every 500ms.

3. The Dashboard (Google Colab)
Role: Remote Monitoring & Evaluation.
Workflow: Participants access a shared Colab notebook that pulls live data from the cloud.
Visualization: Uses Matplotlib/Plotly to display a "Heatmap" of the 20 nodes and real-time accuracy metrics for the recognition model.

## Tech Stack
Languages: Embedded C, Python, JavaScript (Web Serial API).
Frameworks: NVIDIA TensorRT (Inference), Pandas/Matplotlib (Visualization).
Hardware: 20x STM32 BluePill/Nucleo, NVIDIA Jetson Orin Nano, MPU6050 IMUs.
Tools: Google Colab, Logic Analyzers, STM32CubeIDE.

## Workshop Roadmap
Node Bring-Up: Hardware initialization and I2C sensor communication.
Signal Conditioning: Calculating filter coefficients and implementing the LPF in C.
Data Bus Integration: Syncing the nodes with the Jetson Gateway.
Cloud Visualization: Authenticating the Colab notebook to view the live gesture dashboard.
