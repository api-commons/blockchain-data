# Blockchain Data

The common on-chain data vocabulary -- blocks, transactions, addresses and their balances, and tokens -- distilled from the node, indexer and explorer APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Blockchain, Ethereum, Solana, Bitcoin, Web3, Smart Contracts, Blockchain Infrastructure, Blockchain Data in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| block | 47 | 43 |  | blocks 35, block 24 |
| transaction | 43 | 41 | hash 68%, block_number 54%, created_at 54% | transactions 23, tx 21, txs 9 |
| token | 67 | 62 | name 66%, symbol 58% | tokens 57, token 22, erc20 3 |

Cohort: 374 providers with harvested OpenAPI, 109 crosswalks. Of the providers exposing a block: 17% create, 79% list, 66% fetch, 2% update, 4% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Transactions agree on hash, block_number and created_at; from reaches 32%, because UTXO chains have inputs and outputs rather than a sender.
- Tokens agree on name and symbol; decimals reaches 43% and the contract address 41% -- spelled address, token_address or mint depending on the chain.
- Blocks share number, hash and created_at at 44-46%, just under core: the market splits between raw node RPC (height, hash, time) and indexers that reshape them.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The context is blockchain-data, because api-commons/blockchain already holds a standard.
- One vocabulary across chains: number for block height and slot, hash for transaction hash, txid and signature, with chain as a common field.
- Auth tokens (POST /auth/tokens, /oauth/token) are kept out of token with a never-under qualifier.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
