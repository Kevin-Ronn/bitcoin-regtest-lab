# Bitcoin Regtest Laboratory

A reproducible, Dockerized Bitcoin Core regtest environment for studying Bitcoin transaction validation, UTXOs, signatures, mempool behavior, confirmations, and rejection of invalid transactions.

## Safety

This project uses Bitcoin Core **regtest**. Regtest coins have no monetary value and are isolated from Bitcoin mainnet.

Do not place real Bitcoin keys, wallet data, or credentials in this repository.

## Architecture

```text
                 Docker network
                       |
          +------------+------------+
          |                         |
    Bitcoin Core #1           Bitcoin Core #2
      Alice wallet              Bob wallet
          |                         |
          +------ regtest ----------+
```

## Requirements

- Ubuntu/Linux, macOS, or Windows with Docker
- Docker Engine
- Docker Compose V2

## Start

```bash
git clone https://github.com/Kevin-Ronn/bitcoin-regtest-lab.git
cd bitcoin-regtest-lab
docker compose up -d
docker compose ps
```

Check Bitcoin Core:

```bash
docker exec btc-regtest-node1 bitcoin-cli \
  -regtest \
  -rpcuser=lab \
  -rpcpassword=labpassword \
  getblockchaininfo
```

The output should contain:

```text
"chain": "regtest"
```

## Research direction

The environment is intended for controlled experiments comparing:

- valid versus invalid transactions
- real versus nonexistent TXIDs
- correct versus incorrect transaction outputs
- invalid signatures
- nonexistent UTXOs
- conflicting/double-spend transactions
- mempool acceptance versus block confirmation

The goal is to demonstrate the difference between something that merely **looks like a Bitcoin payment** and something that satisfies Bitcoin's consensus rules.

## Current state

The repository contains the reproducible two-node Docker environment. Local blockchain and wallet state are intentionally excluded through `.gitignore`.
