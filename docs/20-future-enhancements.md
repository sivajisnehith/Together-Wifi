# 20 - Future Enhancements

## Overview
This document outlines planned feature additions, architectural evolution, and technology upgrades for future iterations of Together-Wifi.

---

## 1. Planned Feature Roadmap

### Phase 1: Enhanced Connectivity & Security
- **Automated Enterprise WiFi (Passpoint / Hotspot 2.0):** Enable seamless WPA3 Enterprise authentication without requiring manual SSID connection.
- **VPN / Encrypted Tunneling:** Built-in lightweight WireGuard tunnel to secure user traffic over shared public hotspots.

### Phase 2: Advanced Monetization & Payments
- **Crypto & Web3 Micro-payments:** Enable tokenized micro-payments for international visitors using stablecoins (USDC / USDT).
- **Dynamic Pricing Engine:** AI-driven dynamic pricing based on network speed, time of day, and location demand.

### Phase 3: Analytics & Provider Portal
- **Provider Analytics Dashboard:** Web dashboard offering real-time bandwidth consumption graphs, user retention metrics, and payout history.
- **Bandwidth Shaping & QoS:** Integrations with router firmware (OpenWrt) to dynamically limit bandwidth per user tier.

---

## 2. Infrastructure & Architectural Evolution

- **Kubernetes Migration:** Transition from Docker Compose / AWS ECS Fargate to Kubernetes (AWS EKS) for auto-scaling and service mesh integration (Istio).
- **gRPC Inter-Service Communication:** Replace synchronous REST calls between backend microservices with high-performance gRPC (Protocol Buffers).
- **Global Edge Expansion:** Deploy API Gateway and Redis edge caches across multi-region AWS nodes to serve global travelers with sub-20ms latency.
