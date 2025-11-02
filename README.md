# 🌐 Beacom

**Internet for everyone.**

Beacom is a next-generation ISP platform built from the ground up with modern technology. We're rethinking connectivity for Africa—affordable, reliable, and built on Rust + Kotlin Multiplatform.

---

## 🚀 Vision

Most ISPs are running on legacy infrastructure from the 2000s. Beacom is different:

- **Stage 1:** Virtual ISP (reseller with custom software)
- **Stage 2:** WISP (own the last mile with wireless)
- **Stage 3:** Infrastructure (fibre, data centers, caching)
- **Stage 4:** Full ISP (spectrum, peering, wholesale)

We're not just building an ISP. We're building a **connectivity platform** with hardware, marketplace, and ecosystem plays.

---

## 🏗️ Architecture

### Backend (Rust)
- **gRPC microservices** for inter-service communication
- **Event-sourced billing** for audit trails
- **Real-time RADIUS** authentication and accounting
- **Custom network monitoring** (SNMP, NetFlow, MikroTik/Ubiquiti APIs)
- **ML-powered analytics** (churn prediction, fraud detection)

### Frontend (Kotlin Multiplatform + React)
- **Mobile apps** (iOS + Android) with Compose Multiplatform
- **Web portal** (React + Vite + TypeScript)
- **Admin dashboard** (React + real-time network monitoring)
- **Marketing site** (Next.js 14 for SEO)

---

## 📁 Repository Structure

```
beacom/
├── backend/           # Rust microservices
│   ├── crates/        # Shared libraries
│   ├── services/      # gRPC services (billing, RADIUS, etc.)
│   ├── workers/       # Background jobs
│   └── proto/         # Protocol buffer definitions
│
├── clients/
│   ├── beacom-mobile/ # Kotlin Multiplatform (iOS + Android)
│   ├── beacom-web/    # React user portal
│   ├── beacom-admin/  # React admin dashboard
│   └── beacom-marketing/ # Next.js marketing site
│
├── hardware/          # Hardware specs, firmware, provisioning
├── docs/              # Architecture docs, runbooks
└── infrastructure/    # K8s manifests, terraform, scripts
```

---

## 🛠️ Tech Stack

### Backend
- **Language:** Rust 🦀
- **Framework:** Axum (async web framework)
- **gRPC:** Tonic + Prost
- **Database:** PostgreSQL (transactional), ClickHouse (analytics)
- **Cache:** Redis
- **Queue:** RabbitMQ / NATS
- **Observability:** OpenTelemetry, Prometheus, Grafana
- **Deployment:** Kubernetes, Docker

### Mobile
- **Language:** Kotlin
- **Framework:** Compose Multiplatform
- **Architecture:** Clean Architecture (MVVM)
- **Networking:** Ktor (REST), gRPC-KMP
- **DI:** Koin
- **Database:** SQLDelight
- **Platforms:** iOS, Android

### Web
- **Language:** TypeScript
- **Framework:** React 18, Next.js 14
- **State:** Zustand
- **Styling:** Tailwind CSS
- **API:** REST + gRPC-Web
- **Charts:** Recharts
- **Build:** Vite

---

## 🔑 Key Features

### For Users
- **Real-time usage tracking** with push notifications
- **Flexible bundles** (prepaid, postpaid, pay-as-you-go)
- **One-tap top-ups** via Paystack, Yoco, Ozow
- **Marketplace** (buy airtime, pay bills, purchase vouchers)
- **Hardware management** (configure routers, update firmware)
- **24/7 support** (tickets, live chat, WhatsApp)

### For Admins
- **Live network dashboard** (SNMP monitoring, topology maps)
- **User management** (subscriptions, credits, manual adjustments)
- **Payment reconciliation** (automated + manual)
- **Hardware provisioning** (routers, SIMs, hotspots)
- **Analytics** (churn prediction, revenue forecasting)
- **Audit logs** (every admin action tracked)

### For Ops
- **Automated alerting** (tower down, bandwidth exceeded)
- **RADIUS server** (PPPoE, hotspot, CoA for real-time changes)
- **BGP daemon** (for Stage 4 peering)
- **Spectrum controller** (5G spectrum management)
- **Cache node manager** (Netflix, YouTube content caches)

---

## 🚦 Getting Started

### Prerequisites
- Rust 1.75+
- Kotlin 1.9+
- Node.js 20+
- Docker + Docker Compose
- PostgreSQL 15+
- Redis 7+

### Quick Start (Backend)

```bash
cd backend

# Setup environment
cp .env.example .env

# Start dependencies
docker-compose up -d postgres redis

# Run migrations
./scripts/migrate.sh

# Generate gRPC code from proto files
./scripts/generate-proto.sh

# Run all services (development)
cargo run --bin api-gateway
cargo run --bin billing-engine
cargo run --bin radius-server
```

### Quick Start (Mobile)

```bash
cd clients/beacom-mobile

# Install dependencies
./gradlew build

# Run Android
./gradlew :androidApp:installDebug

# Run iOS
cd iosApp
pod install
open iosApp.xcworkspace
```

### Quick Start (Web)

```bash
cd clients/beacom-web

# Install dependencies
npm install

# Start dev server
npm run dev
```

---

## 📡 Services Overview

| Service | Port | Purpose |
|---------|------|---------|
| api-gateway | 8080 | Public REST/GraphQL API |
| billing-engine | 50051 | gRPC billing logic |
| radius-server | 1812/1813 | RADIUS auth/accounting |
| network-monitor | 50052 | Network health monitoring |
| analytics-engine | 50053 | Data processing + ML |
| notification-service | 50054 | Email/SMS/Push dispatcher |
| webhook-handler | 8081 | Payment gateway webhooks |
| admin-api | 50055 | Internal admin operations |

---

## 🔐 Security

- **JWT authentication** with refresh tokens
- **RBAC** (role-based access control)
- **Encrypted passwords** (Argon2)
- **OTP support** (TOTP, SMS)
- **API rate limiting** (per user, per IP)
- **Audit logs** for all admin actions
- **RADIUS shared secrets** for NAS authentication
- **Payment webhook signature verification**

---

## 🧪 Testing

```bash
# Backend unit tests
cargo test

# Backend integration tests
cargo test --test '*' --features integration

# Backend benchmarks
cargo bench

# Mobile tests
./gradlew test

# Web tests
npm test

# Load tests
cd tests/load_tests
k6 run scenario_1.js
```

---

## 📊 Monitoring

- **Metrics:** Prometheus + Grafana dashboards
- **Tracing:** Jaeger for distributed tracing
- **Logs:** Loki for log aggregation
- **Alerts:** Alertmanager + Telegram/SMS notifications
- **Uptime:** Synthetic monitoring via UptimeRobot

---

## 🌍 Deployment

### Staging
```bash
./scripts/deploy.sh staging
```

### Production
```bash
./scripts/deploy.sh production
```

Kubernetes manifests in `k8s/` directory.

---

## 🛣️ Roadmap

### Q1 2025 - Stage 1: Virtual ISP
- [x] Backend scaffolding
- [x] Mobile app scaffolding
- [ ] Auth system (login, register, JWT)
- [ ] Billing engine (prepaid bundles)
- [ ] Payment integration (Paystack)
- [ ] Usage tracking via partner API
- [ ] Mobile app MVP (iOS + Android)

### Q2 2025 - Stage 2: WISP
- [ ] RADIUS server (PPPoE + hotspot)
- [ ] Real-time usage deduction
- [ ] Bandwidth throttling (CoA)
- [ ] Network monitoring (SNMP)
- [ ] MikroTik integration
- [ ] First 100 customers

### Q3 2025 - Hardware
- [ ] Custom router (OpenWrt-based)
- [ ] Firmware OTA updates
- [ ] Router config via mobile app
- [ ] SIM provisioning system
- [ ] Hotspot device prototype

### Q4 2025 - Marketplace
- [ ] Airtime purchases
- [ ] Bill payments (electricity, water)
- [ ] Voucher sales
- [ ] Partner integrations

### 2026+ - Stage 3/4
- [ ] Fibre deployments
- [ ] Data center co-location
- [ ] Content caching (Netflix, YouTube)
- [ ] BGP peering
- [ ] Spectrum acquisition
- [ ] Wholesale services

---

## 🤝 Contributing

We're not open source (yet), but contributions from the core team follow these guidelines:

1. **Branch naming:** `feature/description`, `fix/description`
2. **Commit messages:** Conventional Commits format
3. **Code review:** All PRs require review
4. **Tests:** All new features must have tests
5. **Documentation:** Update docs for API changes

---

## 📝 License

Proprietary. All rights reserved.

---

## 🙏 Acknowledgments

Built with:
- Rust 🦀
- Kotlin 
- React ⚛️
- Love for SA 🇿🇦

---

## 📞 Contact

- **Website:** beacom.co.za
- **Email:** hello@beacom.co.za
- **Support:** support@beacom.co.za
- **Twitter:** @BeacomZA

---

**Beacom.** Internet for everyone. 🌐✨
