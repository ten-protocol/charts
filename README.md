# Ten Node Charts

This README provides an overview of the configuration values for the Ten Node Helm charts.

## Components

The chart deploys the following components:
- **Host Node**: Main interface that connects to L1 network and manages transactions
- **Enclave**: Secure computation environment for private transaction processing
- **EdgelessDB**: SGX-enabled database for secure data storage
- **PostgreSQL**: Database with TLS support for persistent storage

## Values

The following table lists the configurable parameters of the ten node chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `global.imagePullPolicy` | Global image pull policy | `IfNotPresent` |
| `enclave.enabled` | Enable enclave deployment | `true` |
| `enclave.image.repository` | Enclave image repository | `testnetobscuronet.azurecr.io/obscuronet/enclave` |
| `enclave.image.tag` | Enclave image tag | `edb-debug-0.2` |
| `enclave.service.port` | Enclave RPC port | `11001` |
| `enclave.resources.limits.memory` | Enclave memory limit | `5Gi` |
| `host.enabled` | Enable host node deployment | `true` |
| `host.image.repository` | Host image repository | `testnetobscuronet.azurecr.io/obscuronet/host` |
| `host.service.type` | Host service type | `LoadBalancer` |
| `host.ports` | Host service ports | `http:80, ws:81, p2p:10000` |
| `postgresql.enabled` | Enable PostgreSQL | `true` |
| `postgresql.tls.enabled` | Enable PostgreSQL TLS | `true` |
| `edb.enabled` | Enable EdgelessDB | `true` |
| `edb.sqlApiPort` | EdgelessDB SQL API port | `3306` |
| `edb.resources.limits.sgx.intel.com/epc` | SGX EPC memory limit | `10Mi` |
| `config.network.chainid` | Network chain ID | `443` |
| `config.network.batch.interval` | Batch processing interval | `1s` |
| `config.network.rollup.interval` | Rollup interval | `15m0s` |
| `config.network.crosschain.interval` | Cross-chain interval | `6s` |
| `config.host.l1.websocketurl` | L1 websocket URL | `ws://dev-testnet-eth2network.uksouth.cloudapp.azure.com:9000` |
| `config.enclave.simulation` | Enable simulation mode | `false` |
| `config.enclave.enableattestation` | Enable attestation | `true` |

### Critical Configurations

Some important configuration sections include:

1. **Node Identity**
   - Node ID (ETH Address): 
     * Unique identifier for the node in the network
     * Ethereum compatible address format
   - Private Key: `f8624b8465fe9d28ab5cc318aa051dab40349b65a901b00b9cd6758102aac5f9`
     * Used for transaction signing

2. **Network Settings**
   - Chain ID: 443
   - Batch interval: 1s
   - Rollup interval: 15m
   - Cross-chain interval: 6s

3. **Resource Requirements**
   - Host: 2Gi memory
   - Enclave: 5Gi memory
   - EdgelessDB: 10Mi SGX EPC

**Security Note**: 
- The example private key shown above is for demonstration only
- In production, always use unique and secure private keys
- Never commit actual private keys to version control

## Usage

To install the chart with the release name `my-release`:

```sh
helm install my-release ./ten-node
```

To uninstall the chart:

```sh
helm uninstall my-release
```

For more information on configuring the chart, refer to the [Helm documentation](https://helm.sh/docs/).

