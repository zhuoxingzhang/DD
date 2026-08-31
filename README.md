<img src="Artifact/dragon.png" alt="Dragon">

# Introduction

This repository contains the artifacts that supplement our work on **Enter the Dragon’s Dojo: Computing Interview Questions for Human Experts to Classify Database Keys as Meaningful**: the technical paper, the demo video, the online demo and a deployable demo.

The demo interviews a team of human experts about the schema they know. It generates Boolean questions of the form "is this column set a key?", prunes the search space from every answer received, and returns the set of meaningful minimal keys together with an Armstrong relation that satisfies all of them and violates all anti-keys.

# The Eight Strategies

The demo implements a single interview framework with three parameters: an **algorithm family**, a **traversal start** and a **traversal direction**. The start page asks for all three and displays the resulting strategy code, in which T stands for top-down, B for bottom-up, B for breadth-first and D for depth-first.

|                              | breadth-first    | depth-first      |
| ---------------------------- | ---------------- | ---------------- |
| **level-wise (LW)**          | `LW-TB`, `LW-BB` | `LW-TD`, `LW-BD` |
| **dualize-and-advance (DA)** | `DA-TB`, `DA-BB` | `DA-TD`, `DA-BD` |

The level-wise family moves through the lattice of column sets one column at a time. The dualize-and-advance family jumps directly to those column sets whose status is still open, which bounds the number of questions linearly in the size of the border formed by the minimal keys and the maximal anti-keys, rather than in the size of the search space.

# Online Demo

Visit the [website](https://deleted-stats-gratis-land.trycloudflare.com/) to interview for keys online! If the link is not accessible, please report an issue.

# Using the Demo

1. Enter the **attributes** of the table schema, and optionally a domain value per attribute for the Armstrong relation.
2. Optionally enter **predetermined minimal keys**, such as the primary key. The interview skips every question their answers already settle.
3. Choose an **algorithm family**, a **traversal start** and a **traversal direction**.
4. Answer each generated question with **Yes** or **No**. The interview finishes as soon as no column set is left whose status is not implied by the answers received, and it reports the minimal keys, the maximal anti-keys and an Armstrong relation.

# Requirements for Demo Deployment

> 1. Software requirements
>> Java with version 17; Java Spring Boot

# Deploy the Demo on Your PC

1. Download the jar file at `Artifact/keyinterviewtool-0.0.1-SNAPSHOT.jar`
2. `cd` to the directory of the jar file
3. Run:
   ```bash
   java -jar keyinterviewtool-0.0.1-SNAPSHOT.jar
   ```
4. Visit `http://localhost:8080` to start the interview on your PC.

# Experiments

The technical paper reports experiments on the distribution of minimal keys, on the effect of schema size and on real-world data sets. This repository holds the paper, the demo and the video only; the code that runs those experiments, the data sets they read and the recorded results they produce are in the [key-interview](https://github.com/zhuoxingzhang/key-interview) repository, whose README describes how to reproduce each of them and which program writes each reported number.

# Repository Contents

| Path | Contents |
| ---- | -------- |
| `Artifact/Technical Paper 4 DD.pdf` | the technical paper |
| `Artifact/demo video.mp4` | the demo video |
| `Artifact/keyinterviewtool-0.0.1-SNAPSHOT.jar` | the deployable demo, implementing all eight strategies |
| `Artifact/dragon.png`, `Artifact/dragon.pdf` | the figure of the dojo |
