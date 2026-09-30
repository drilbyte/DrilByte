# DrilByte Network

DrilByte is an EVM-compatible blockchain network powered by **Geth 1.13** and secured with a **Proof-of-Authority (PoA)** consensus model.

This README contains the currently verified network connection details for developers, wallet users, node operators, and ecosystem contributors.


## Network overview

| Property | Value |
| --- | --- |
| Network name | DrilByte |
| Network type | EVM-compatible blockchain |
| Consensus | Proof-of-Authority |
| Execution client | Geth 1.13 |
| Chain ID | `275` |
| Hexadecimal chain ID | `0x113` |
| JSON-RPC endpoint | `https://rpc.drilbyte.com` |
| Block explorer | `https://explorer.drilbyte.com` |
| Native currency | DrilByte (`DRBY`, 18 decimals) |
| Documentation | `https://drilbyte.com/docs` |
| Game | `https://game.drilbyte.com/` |
| Airdrop | `https://dril.drilbyte.com/` |

## Quick links

- [Documentation](https://drilbyte.com/docs)
- [JSON-RPC endpoint](https://rpc.drilbyte.com)
- [Block explorer](https://explorer.drilbyte.com)
- [DrilByte game](https://game.drilbyte.com/)
- [DrilByte Airdrop](https://dril.drilbyte.com/)

## Connect a wallet

Use the following values when adding DrilByte to a compatible EVM wallet:

```text
Network name: DrilByte
RPC URL: https://rpc.drilbyte.com
Chain ID: 275
Currency name: DrilByte
Currency symbol: DRBY
Currency decimals: 18
Block explorer URL: https://explorer.drilbyte.com
```

DrilByte's native currency is **DrilByte (DRBY)** with **18 decimals**.

### Add DrilByte programmatically

```javascript
const drilbyte = {
  chainId: "0x113", // 275 in hexadecimal
  chainName: "DrilByte",
  nativeCurrency: {
    name: "DrilByte",
    symbol: "DRBY",
    decimals: 18,
  },
  rpcUrls: ["https://rpc.drilbyte.com"],
  blockExplorerUrls: ["https://explorer.drilbyte.com"],
};

await window.ethereum.request({
  method: "wallet_addEthereumChain",
  params: [drilbyte],
});
```

## JSON-RPC

DrilByte exposes an HTTPS JSON-RPC endpoint:

```text
https://rpc.drilbyte.com
```

### Verify the chain ID

Run this request to ask the endpoint for its hexadecimal chain ID:

```bash
curl https://rpc.drilbyte.com \
  -H "content-type: application/json" \
  --data '{
    "jsonrpc": "2.0",
    "method": "eth_chainId",
    "params": [],
    "id": 1
  }'
```

The expected result for Chain ID `275` is:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x113"
}
```

### Read the latest block

```bash
curl https://rpc.drilbyte.com \
  -H "content-type: application/json" \
  --data '{
    "jsonrpc": "2.0",
    "method": "eth_blockNumber",
    "params": [],
    "id": 1
  }'
```

The result is returned as a hexadecimal block number.

## Connect with ethers

This example uses ethers v6:

```bash
npm install ethers
```

```javascript
import { JsonRpcProvider } from "ethers";

const provider = new JsonRpcProvider(
  "https://rpc.drilbyte.com",
  {
    chainId: 275,
    name: "drilbyte",
  },
);

const blockNumber = await provider.getBlockNumber();
console.log(`Latest DrilByte block: ${blockNumber}`);
```

## Connect with viem

```bash
npm install viem
```

```javascript
import { createPublicClient, http } from "viem";
import { defineChain } from "viem";

const drilbyte = defineChain({
  id: 275,
  name: "DrilByte",
  nativeCurrency: {
    name: "DrilByte",
    symbol: "DRBY",
    decimals: 18,
  },
  rpcUrls: {
    default: {
      http: ["https://rpc.drilbyte.com"],
    },
  },
  blockExplorers: {
    default: {
      name: "DrilByte Explorer",
      url: "https://explorer.drilbyte.com",
    },
  },
});

const client = createPublicClient({
  chain: drilbyte,
  transport: http(),
});

const blockNumber = await client.getBlockNumber();
console.log(`Latest DrilByte block: ${blockNumber}`);
```

## Connect with web3.js

```bash
npm install web3
```

```javascript
import Web3 from "web3";

const web3 = new Web3("https://rpc.drilbyte.com");

const chainId = await web3.eth.getChainId();
const blockNumber = await web3.eth.getBlockNumber();

console.log({ chainId, blockNumber });
```

## Deploy an EVM contract

DrilByte is EVM-compatible, so applications can use familiar Ethereum development tools such as:

- Hardhat
- Foundry
- Remix
- ethers
- web3.js
- viem
- MetaMask and other EVM wallets

Configure your deployment tool with:

```text
RPC URL: https://rpc.drilbyte.com
Chain ID: 275
```

### Hardhat network configuration

```javascript
export default {
  solidity: "0.8.24",
  networks: {
    drilbyte: {
      url: "https://rpc.drilbyte.com",
      chainId: 275,
      accounts: process.env.DRILBYTE_PRIVATE_KEY
        ? [process.env.DRILBYTE_PRIVATE_KEY]
        : [],
    },
  },
};
```

Never commit private keys, seed phrases, or wallet credentials to GitHub. Use environment variables or a secure secrets manager.

### Foundry configuration

```toml
[profile.default]
src = "src"
out = "out"
libs = ["lib"]

[rpc_endpoints]
drilbyte = "https://rpc.drilbyte.com"
```

Deploy with:

```bash
forge create \
  --rpc-url drilbyte \
  --private-key "$DRILBYTE_PRIVATE_KEY" \
  src/Example.sol:Example
```

## Geth 1.13 and Proof-of-Authority

DrilByte uses **Geth 1.13** as its execution client and **Proof-of-Authority** as its consensus model.

PoA networks use an approved validator set rather than open proof-of-work mining. This makes validator membership, genesis configuration, peer discovery, signing configuration, and key management network-specific.

### Operator information still required

The following values are not included here because they must come from the DrilByte network operator:

- Official genesis file
- Validator addresses and validator admission process
- Bootnodes and static peers
- P2P port
- HTTP API and WebSocket configuration
- Authority or signer configuration
- Node data directory requirements
- Snapshot or state-sync instructions
- Testnet or mainnet designation
- Official node launch command
- Key-generation and key-storage runbook

Do not start a validator or production node using guessed values. Use the approved DrilByte operator runbook for Geth 1.13.

### Check a Geth installation

After installing the approved Geth 1.13 release, verify the binary:

```bash
geth version
```

The reported version should be reviewed against the release approved by the DrilByte operator before joining the network.

## Block explorer

The DrilByte block explorer is available at:

```text
https://explorer.drilbyte.com
```

Use the explorer to inspect network activity, blocks, transactions, accounts, and deployed contracts.

The explorer's API endpoint and contract verification workflow have not been documented here because those details were not provided.

## DrilByte game

The DrilByte game is available at:

```text
https://game.drilbyte.com/
```

The game can be used as an ecosystem application built on or connected to the DrilByte network. Wallet connection, contract addresses, supported assets, and gameplay-specific integration details should be documented by the game project.

## Network values to confirm

Before publishing a final production version of this README, confirm the following values with the DrilByte operator:

| Value | Current status |
| --- | --- |
| Network name | Confirmed: DrilByte |
| RPC URL | Confirmed: `https://rpc.drilbyte.com` |
| Chain ID | Confirmed: `275` / `0x113` |
| Client | Confirmed: Geth 1.13 |
| Consensus | Confirmed: Proof-of-Authority |
| EVM compatibility | Confirmed |
| Block explorer | Confirmed: `https://explorer.drilbyte.com` |
| Native currency name | Confirmed: DrilByte |
| Native currency symbol | Confirmed: `DRBY` |
| Native currency decimals | Confirmed: `18` |
| WebSocket endpoint | TBD |
| Testnet or mainnet status | TBD |
| Genesis file | TBD |
| Bootnodes | TBD |
| Validator runbook | TBD |
| Explorer API | Confirmed: `https://api.drilbyte.com` |

## Security notes

- Never commit private keys, seed phrases, keystore passwords, or RPC credentials.
- Confirm the chain ID before signing transactions.
- Use the HTTPS RPC endpoint in production applications.
- Keep validator and signer keys offline or in an approved secure key-management system.
- Treat any unverified genesis file, bootnode, peer list, or node command as untrusted until confirmed by the network operator.
- Review transaction destinations and chain identity before deploying contracts or transferring assets.

## Contributing

Contributions should be made through the DrilByte GitHub repository using pull requests.

When contributing network documentation:

1. Separate verified facts from operator-provided values.
2. Include the source or owner for network-specific settings.
3. Do not publish secrets or private infrastructure details.
4. Test code examples against the DrilByte RPC endpoint when possible.
5. Keep wallet and node instructions aligned with the approved operator runbook.

## License

The license for the DrilByte network documentation and related repositories has not been specified yet.

Add the official license here before publishing the repository.
