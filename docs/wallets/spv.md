# 简单支付验证（SPV）

---

## 什么是简单支付验证（SPV）？

简单支付验证（SPV）可以让Decred钱包不必去下载全部的Decred区块账本。SPV模式下运行的钱包只需要下载包含与之相关的交易的完整区块（也就是说：包含钱包地址的交易)。一般情况下， 这意味着下载几十MB的数据，而不是几个GB的数据。这减少了钱包的硬件要求并且大大减少了新钱包初始化的时间。

SPV模式被直接集成到dcrwallet命令行工具中 - Decredition 和 其他官方钱包后台使用的 - 因此所有官方钱包的用户都可以开启简单支付验证（SPV）。

## 为什么SPV模式被加入到了`dcrwallet`中？

运行在SPV模式的钱包对硬件要求极低， 比起下载整个区块账本，磁盘占用和下载要求减少，一个SPV钱包只下载和它有关的交易的区块，并且区块链中剩余其他的区块只下载区块头。因为运行在SPV模式下的钱包的硬件仅验证工作量证明和区块链头部而不是验证区块里的每一笔交易来确保区块内容和区块头一致。

由于这些减少的要求，Decred钱包可以在更广泛的设备上运行 - 特别是移动钱包。通常智能手机和平板的会受到限制诸如CPU功耗，存储或数据流量的限制，并且手机操作系统还限制后台运行程序，这使得运行一个全节点基本不可能。

SPV模式带来的另一个好处就是极大地减少了全新钱包投入使用所需的时间，用户体验得到显著的提升。

## SPV模式如何工作的？

At the start of every block added to the Decred blockchain is 180 bytes of data called the [block header](https://devdocs.decred.org/developer-guides/block-header-specifications/). The block header describes key information about the block including the hash of the block, the Merkle root (the sum of all the transaction hashes in the block), and the nonce calculated by the proof-of-work miners. A predetermined filter is also created for every block, based on the all of the transactions within the block.

When an SPV wallet initializes it will connect to the Decred network using peer-to-peer connections, and it will download the full set of headers and filters. It will then validate the header chain to ensure that the chain and its proof-of-work are valid. Once this is complete, the wallet will use the filters to locally identify which blocks contain owned transactions without uploading any private data to remote nodes. The wallet can then use the peer-to-peer network to download these blocks, scan them for relevant transactions and select these to update personal transaction history and balance.

## How is this different from a "light" wallet?

"Light" wallets such as [Exodus](https://www.exodus.io/) or [Atomic](https://atomicwallet.io/) already bring some of the benefits of an SPV wallet - for example these wallets allow sending and receiving Decred transactions with a minimal start-up time and without downloading the full chain. Light wallets certainly provide a level of convenience but there are often subtle consequences because they depend upon an API provided by a centralized service:

- Light wallets depend on a remote service to watch owned addresses and provide notifications when transactions are received by the addresses. Notifications could be missed or incorrect.

- Users will often be required to upload an extended public key to the central server so it is aware of all of owned addresses, potentially compromising the users' privacy.

- Light wallets do not validate the information they receive by checking the blockchain directly - they have to blindly trust the information provided by the central server.

These concerns do not apply to SPV wallets because they connect directly to the decentralized, peer-to-peer Decred network. They upload no private data to remote nodes and they discover their own transactions by inspecting the blockchain directly.

## Are there any disadvantages?

- SPV does not support voting wallets. Voting wallets have the responsibility to vote on the validity of the last block, and a wallet cannot be sure of the validity unless it fully validates the whole blockchain leading up to that block. It is possible to purchase tickets and allocate the voting rights to a [Voting Service Provider](../proof-of-stake/how-to-stake.md#pos-using-a-voting-service-provider-vsp). Be aware that if a VSP fails to revoke a missed ticket, it is not possible for an SPV wallet to revoke the missed ticket until it has reached the confirmation depth of an expired ticket.

- SPV wallets only download blocks which have transactions related to their owned addresses, which could potentially reveal more information about the wallet than if it downloaded every single block. This only presents a very minor decrease in privacy, but it is a decrease nonetheless. This can be mitigated by downloading blocks from multiple peers so no single peer is able to see the full list of blocks downloaded by a wallet. Even if a passive observer on the network is able to see which blocks are downloaded by a wallet, they are not able to identify which transactions in those blocks are relevant.

- Wallets operating in SPV mode are only able to validate the block headers they download and not the filters. This makes a "false-negative" attack possible, whereby a malicious peer that knows a wallet is waiting for a particular transaction could send the wallet a fake filter which does not include the transaction, resulting in the wallet not downloading the block and so not becoming aware of the transactions existence. This transaction would still be visible to all fully validating nodes and wallets, and it will still appear in the [block explorer](../getting-started/using-the-block-explorer.md). [DCP-0005](https://github.com/decred/dcps/blob/master/dcp-0005/dcp-0005.mediawiki) was activated by a [consensus rule vote](https://docs.decred.org/governance/consensus-rule-voting/overview/) in early 2020, and this enabled adding the hash of the filter into the part of the block header that is PoW validated. As a result, SPV wallets will in future be able to easily check the validity of the filters without having to download their blocks. A "false-positive" scenario is not possible. If a malicious node provides a fake filter which includes a non-existent transaction, the wallet will simply download the full block, compare it to the filter and discover that the filter is not genuine.

## How do I use SPV?

#### `dcrwallet` CLI

To enable SPV mode in `dcrwallet` simply provide the `--spv` flag when starting the process. There is also an optional `--spvconnect` flag which disables DNS seeding and allows you to specify the IP of a full node you wish to sync from. `--spvconnect` can be specified multiple times to sync from multiple peers.

#### Decrediton

When Decrediton is started for the first time, a dedicated screen is displayed during the setup wizard which asks if you would like to enable SPV mode.

If Decrediton has already been used before, it is possible to change to SPV mode through the settings tab. There is also a "SPV Connect" textbox on this tab, which will allow you to specify the IP address of a full node you wish to sync from.
