# ⚡ VTB — LTK Tools Auto-Builder

> Automated CI/CD pipeline that builds and serves bleeding-edge Windows binaries of **League Toolkit (LTK)** tools for **Vanilla True Builder**.

[![Build and Release Tools](https://github.com/SEU-USUARIO/SEU-REPO/actions/workflows/build.yml/badge.svg)](https://github.com/SEU-USUARIO/SEU-REPO/actions/workflows/build.yml)
[![Latest Release](https://img.shields.io/github/v/release/SEU-USUARIO/SEU-REPO?label=release&color=blue)](https://github.com/SEU-USUARIO/SEU-REPO/releases/tag/tools-latest)
[![Check Cadence](https://img.shields.io/badge/cron-every%203%20hours-brightgreen)](#how-it-works)

---

## 📖 Overview

**Vanilla True Builder** is designed to be a self-sufficient, frictionless League of Legends mod builder. To work smoothly without forcing users to install Rust, Git, or toolchains locally, this repository automates the upstream build pipeline.

Every 3 hours, a GitHub Actions workflow monitors the upstream **League Toolkit** repositories for new commits. Whenever changes are detected, it freshly compiles and packages standalone Windows `.exe` files into a single bundle: **`tools.zip`**.

---

## 🛠️ Included Tools

| Binary | Source Repository | Description |
| :--- | :--- | :--- |
| **`wadtools.exe`** | [LeagueToolkit/wadtools](https://github.com/LeagueToolkit/wadtools) | Extracts and builds `.wad.client` game archives. |
| **`ritobin.exe`** | [LeagueToolkit/ritobin-tools](https://github.com/LeagueToolkit/ritobin-tools) | Serializes/deserializes League `.bin` property files to text. |

---

## ⚙️ How It Works

```mermaid
graph LR
    A[Cron: Every 3h] --> B[Check Upstream Git SHAs]
    B -->|Has Changes?| C{Diff Check}
    C -->|No Changes| D[Skip / Terminate]
    C -->|New Commits| E[Cargo Build on Windows]
    E --> F[Normalize Names to .exe]
    F --> G[Package tools.zip]
    G --> H[Update Release: tools-latest]
    H --> I[Vanilla True Builder Auto-Update]
