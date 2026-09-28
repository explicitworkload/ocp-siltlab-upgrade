# OCP SiltLab 4.18 — Upgrade & Operator Configuration

This repository contains ImageSetConfiguration manifests for upgrading a disconnected (air-gapped) Red Hat OpenShift Container Platform cluster and its Day-2 operators.

## Cluster Upgrade Path

| Stage | From | To | Channel |
|-------|------|----|---------|
| 1 — Current z-stream upgrade | 4.18.17 | **4.18.19** | `stable-4.18` |
| 2 — Minor version upgrade | 4.18.19 | **4.19.20** | `stable-4.19` |
| 3 — Minor version upgrade | 4.19.20 | **4.20.5** | `stable-4.20` |

All 34 cluster operators are running **4.18.19**, Available, and not Degraded.

## Installed Operators

### Cluster Operators (v4.18.19)

All cluster operators report `AVAILABLE=True`, `PROGRESSING=False`, `DEGRADED=False`:

| Operator | Since |
|----------|-------|
| authentication | 8h |
| baremetal | 436d |
| cloud-controller-manager | 436d |
| cloud-credential | 436d |
| cluster-autoscaler | 436d |
| config-operator | 436d |
| console | 100d |
| control-plane-machine-set | 436d |
| csi-snapshot-controller | 436d |
| dns | 8h |
| etcd | 436d |
| image-registry | 29d |
| ingress | 436d |
| insights | 436d |
| kube-apiserver | 436d |
| kube-controller-manager | 436d |
| kube-scheduler | 436d |
| kube-storage-version-migrator | 436d |
| machine-api | 436d |
| machine-approver | 436d |
| machine-config | 436d |
| marketplace | 436d |
| monitoring | 15d |
| network | 436d |
| node-tuning | 436d |
| olm | 436d |
| openshift-apiserver | 8h |
| openshift-controller-manager | 8h |
| openshift-samples | 436d |
| operator-lifecycle-manager | 436d |
| operator-lifecycle-manager-catalog | 436d |
| operator-lifecycle-manager-packageserver | 30h |
| service-ca | 436d |
| storage | 436d |

### Day-2 Operators (OLM-managed)

| Operator | Namespace | Version | Status |
|----------|-----------|---------|--------|
| GPU Operator (NVIDIA) | nvidia-gpu-operator | — | Succeeded |
| Kubernetes NMState | openshift-nmstate | 4.18.0-202606101320 | Succeeded |
| OpenShift Virtualization | openshift-cnv | — | Succeeded |
| LVM Storage | openshift-storage | — | Succeeded |
| Node Feature Discovery | openshift-nfd | 4.18.0-202506230505 | Succeeded |
| Open Data Hub | openshift-operators | — | Succeeded |
| OpenShift GitOps | openshift-gitops-operator | 1.16.2 | Pending |
| OpenShift Pipelines | openshift-operators | 1.18.1 | Succeeded |
| OpenShift Virtualization (HCO) | openshift-cnv | — | Succeeded |
| Red Hat Build of Keycloak | keycloak | — | Succeeded |
| Red Hat OpenShift AI (RHODS) | redhat-ods-operator | 2.19.1 | Succeeded |
| OpenShift Serverless | openshift-serverless | 1.36.1 | Succeeded |
| OpenShift Service Mesh | openshift-operators | 2.6.11 | Pending |

## ImageSetConfiguration Manifests

### Stage 1 — 4.18 → 4.19

- **[isc-1-platform.yaml](isc-1-platform.yaml)** — Platform images for OCP 4.18.19 and 4.19.20.
- **[isc-1-operators.yaml](isc-1-operators.yaml)** — Operator catalogs from v4.19 indexes.

### Stage 2 — 4.19 → 4.20

- **[isc-2-platform.yaml](isc-2-platform.yaml)** — Platform images for OCP 4.19.20 and 4.20.5.
- **[isc-2-operators.yaml](isc-2-operators.yaml)** — Operator catalogs from v4.20 indexes.

All operator manifests mirror the following packages with explicit channel pinning:

**Red Hat Operators** (`redhat-operator-index`):

| Package | Channel |
|---------|---------|
| `kubernetes-nmstate-operator` | `stable` |
| `kubevirt-hyperconverged` | `stable` |
| `lvms-operator` | `stable-4.19` / `stable-4.20` |
| `nfd` | `stable` |
| `openshift-gitops-operator` | `latest` |
| `openshift-pipelines-operator-rh` | `latest` |
| `rhbk-operator` | `stable-v26.6` |
| `rhods-operator` (OpenShift AI) | `stable-3.5` |
| `serverless-operator` | `stable` |
| `servicemeshoperator` | `stable` |

**Certified Operators** (`certified-operator-index`):

| Package | Channels |
|---------|----------|
| `gpu-operator-certified` | `v26.7`, `v26.3` |
