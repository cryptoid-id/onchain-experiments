# onchain-experiments

Onchain experiments and learning notes: contract audits, testnet token
templates, reading RPC and explorers, and safety checklists.

> Safety note: this repository contains public information and my own
> notes only. No private keys, seed phrases, passwords, cookies, or
> verification codes are ever stored here. Experiments use testnet
> wallets and testnet funds.

## Before I sign anything: my checklist

1. Verify the chain. Check the chain ID and network name in the wallet
   before signing; a familiar site on the wrong chain is a red flag.
2. Verify the contract. Read the verified source (Sourcify or the chain
   explorer) instead of trusting a landing page.
3. Check the price in the transaction itself. For a free mint, the value
   must be exactly 0. If a preview shows a price, stop.
4. Read the key functions. Look at mint, withdraw, owner-only functions,
   and any function that can move user funds or change supply.
5. Simulate first. A clean simulation or preview is the gate before any
   broadcast.
6. One broadcast, then verify. Check the result on the explorer
   (ownerOf, balanceOf, receipt status) before doing anything else.

## Reading a chain with raw RPC

Useful read-only calls that need no wallet at all:

- eth_blockNumber: the latest block.
- eth_call with balanceOf(address): a token balance.
- eth_call with ownerOf(tokenId): who owns an NFT.
- eth_getTransactionReceipt: whether a transaction really succeeded.

If a read fails on one public RPC endpoint, try another before concluding
anything; a failed read is not proof that something does not exist.

## Test token template notes

My GIWA Sepolia test tokens (OSCT series) follow a plain ERC20 shape:

- Fixed supply of 1,000,000, minted once to the deployer at deployment.
- No mint function after deployment, no owner withdrawals, nothing that
  can move other people's balances.
- Testnet only: these tokens have no value and are only activity markers.

## Audit notes format

For every contract I review I write down:

- Contract address and chain, and where its source is verified.
- What the contract can do, in plain words.
- What it cannot do, and which functions are owner-only.
- A simple decision: GO, CAUTION, or BLOCK, with the reason.

Updated: 2026-11-11
