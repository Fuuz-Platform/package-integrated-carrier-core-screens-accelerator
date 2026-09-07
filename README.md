# package-integrated-carrier-core-screens-accelerator

**Version:** 0.0.1
**Spec Version:** 2.0.0

---

## Overview

This package installs the core user interface screens for the Integrated Carrier shipping system. It provides the carrier-agnostic shipping screens that work with any carrier registered in the system (FedEx, UPS, or future additions) through the `Integrated Carrier Router` dispatch flow.

---

## Package Contents

```
integrated-carrier-core-screens/
├── manifest.json
├── package-data.json
├── install/                     3 screens (install steps)
└── preinstall/                  3 preinstall verification steps
```

---

## Installed Screens (3)

### Integrated Carrier Shipment Screen

The primary operator-facing shipping workflow screen. Provides:

- **Carrier selection** — Dropdown populated from active `IntegratedCarrier` records
- **Service level selection** — Filtered by selected carrier from `IntegratedCarrierService` records
- **Billing type selection** — Filtered by selected carrier from `IntegratedCarrierBillingType` records
- **Shipment details form** — Origin/destination address entry, package count, weight, dimensions
- **Rate quote** — Triggers the `Integrated Carrier Router` with request type "Rate Quote"; displays returned carrier rates
- **Label generation** — Triggers label generation for the selected service and rate; invokes `Integrated Carrier Print Labels Standard` upon success
- **Void label** — Cancels a previously generated label via the router
- **Shipment history** — Recent `IntegratedCarrierRequest` records for the current session

### Carrier Account Configuration Screen

Administrative screen for managing carrier accounts:

- Create and edit `IntegratedCarrierAccount` records (account number, API credentials, test/production environment toggle)
- Link accounts to `IntegratedCarrierConnectionConfiguration` records
- Test connectivity to carrier API endpoints
- View connection status and last successful API call

### Carrier Management Screen

Administrative screen for managing the carrier registry:

- List of registered `IntegratedCarrier` records with active/inactive status
- `IntegratedCarrierService` management — add/edit available service levels per carrier
- `IntegratedCarrierBillingType` management — configure billing options per carrier
- `IntegratedCarrierRequestFlow` mapping — assign request handler flow IDs to each carrier/request-type combination

---

## Install Process

**Preinstall (3 steps):** Verifies that none of the 3 screen IDs already exist, preventing duplicate installations.

**Install (3 steps):** Creates each screen header and its latest version, then deploys to make it available in the Fuuz application.

---

## Installation

1. Install `package-integrated-carrier-core-schema-accelerator` and `package-integrated-carrier-core-flows-accelerator` first
2. Import this package via Fuuz Package Manager
3. Install carrier-specific packages (FedEx, UPS) to populate carrier/service/billing seed data
4. Assign the Integrated Carrier Shipment Screen to relevant user roles via the Fuuz Role manager
5. Add the screen to the navigation menu for shipping users

---

## Dependencies

- **`package-integrated-carrier-core-schema-accelerator`** — required
- **`package-integrated-carrier-core-flows-accelerator`** — required (screens invoke the router flows)
- At least one carrier package (FedEx or UPS) for seed data to populate carrier dropdowns

---

## Part of the Integrated Carrier Suite

| Package | Description |
|---------|-------------|
| `integrated-carrier-core-schema` | Data models |
| `integrated-carrier-core-flows` | Router and print flows |
| **integrated-carrier-core-screens** (this) | Shipment management screens |
| `integrated-carrier-fedex` | FedEx seed data and label flows |
| `integrated-carrier-ups` | UPS seed data and label flows |
| `integrated-carrier-addon-plex` | Plex ERP integration extension |

---

*Built on the [Fuuz Industrial Operations Platform](https://fuuz.com)*

## Service levels

No service level agreement applies to anything published here. It becomes a supported
deliverable only once it has been implemented by a Fuuz services professional or an
approved Fuuz partner.
