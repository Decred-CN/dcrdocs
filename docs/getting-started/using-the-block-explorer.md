# <img class="dcr-icon" src="/img/dcr-icons/BlockExplorer.svg" /> 使用区块浏览器

---

## <img class="dcr-icon" src="/img/dcr-icons/Info.svg" /> 总览

在Decred区块链中通过区块浏览器可以查看所有的区块和交易，[dcrdata](https://github.com/decred/dcrdata)。

dcrdata的公共服务可用于以下网络：

- [主网](https://dcrdata.decred.org)
- [测试网](https://testnet.decred.org)

以下是一个有关dcrdata信息快速浏览。

选项         | 解释
---            | ---
`Height（高度）`       | 区块编号。
`Age（块龄）`          | 在多久之前这个块添加到区块链。
`Transactions（交易）` | 这个区块中包含的交易数量。
`Votes（投出选票）`        | 这个区块中包含Voted票数量。
`Fresh Stake（新购选票）`  | 这个区块中包含新购选票数量。
`Size（区块大小）`         | 区块大小(单位：bytes)。

在`Latest Transactions（最近的交易）`下面， 你可以看到通过Decred网络传输的交易ID(txid)和币数量(单位：DCR)。

---

## <img class="dcr-icon" src="/img/dcr-icons/Blocks.svg" /> 区块

区块可以通过搜索它们的区块高度编号来定位，
点击一个主页上的`Height`高度值，或者是他们
`BlockHash` 区块哈希值。 较旧的块将具有较小的区块编号。
区块概述的上半部分显示了有关此区块的相关信息。
这些信息包含： 此区块高度编号、区块哈希值和几个网络关键参数，详细描述如下：

Option                   | Explanation
---                      | ---
`Number of Transactions` | The number of standard transactions (DCR sent from one user to another).
`Height`                 | The height of the blockchain in which this block resides.
`Block Reward`           | The amount of new DCR minted in this block.
`Timestamp`              | The time this block was created by a miner and was included in the blockchain.
`Merkle Root`            | A hash value of all the transaction hashes included in this block.
`Stake Root`             | A hash value of all the stake related transaction hashes in this block. This includes ticket purchases, votes, and ticket revocations.
`VoteBits`               | (1) Block was approved by proof-of-stake voters. (2) Block was vetoed by proof-of-stake voters and all non-stake transactions in the block were invalidated, along with the newly generated block reward for the proof-of-work miner and the Decred Treasury.
`Final State`            | The final state of the pseudo random number generator used for ticket selection.
`Voters`                 | The number of successful proof-of-stake votes cast in this block. The maximum value is 5.
`Fresh Stake`            | The number of stake ticket purchases confirmed in this block.
`Revocations`            | The number of tickets that failed to vote and were revoked.
`PoolSize`               | The total number of active proof-of-stake tickets.
`Difficulty`             | The proof-of-work network difficulty.
`SBits`                  | The price of one proof-of-stake ticket.
`Bits`                   | A compact version of the network difficulty at the time the block was mined.
`Size`                   | The size of the block (in bytes).
`Version`                | The version of the block.
`Nonce`                  | The value used by a miner to find the correct solution for this block.

## <img class="dcr-icon" src="/img/dcr-icons/Transactions.svg" /> 交易

这个章节列出了所有被矿工挖出包含到此区块的交易。
这些交易按照交易手续费从高到低的顺序被从内存池中选出并打包。
这个区块中的所有交易大概都包括: 标准交易 (点对点传输)，权益证明投票，权益证明购票。
以下各节将讲解每种交易。

---

### 标准交易

Here’s the information included in standard Decred transactions.

Option              | Explanation
---                 | ---
`Size`              | The size of the transaction in bytes.
`Fee rate`          | The rate of fees collected by the network (per kB).
`Received Time`     | The time the network confirmed the transaction.
`Mined Time`        | The time a miner included the transaction in a block.
`Included in Block` | The block number that the transaction became a part of.

Note `Received Time`, `Mined Time`, and `Included in Block` will not have a value until a miner validates the transaction and includes it in a Decred block. After being confirmed in a block, the transaction is considered complete.


---

### <img class="dcr-icon" src="/img/dcr-icons/TicketLive.svg" /> 购票交易

For a ticket purchase (stake submission) there are a few differences
from a standard transaction shown.

Note the difference under details: The word `Ticket` appears above the
sender's wallet address on the left, and the words `Subsidy
Commitment` appear on the right. This particular user purchased a
stake ticket for 8.75411638 DCR and received change in the amount
of 7.15994209 DCR. The address listed on the left under `Ticket` is
the address that contains the funds used to purchase this
ticket. The first output on the right is the address that retains
voting rights for this specific ticket. The second output, `Subsidy
Commitment`, is the address where the reward will go. This is not yet
shown by the block explorer at this time. The third and final output
is the address where change for this transaction will be sent.

---

### <img class="dcr-icon" src="/img/dcr-icons/TicketVoted.svg" /> 投票交易

Note the identifying terms in the details section: `Vote`, `Stake
Base`, `Block Commitment`, and `Vote Bits`:

These keywords indicate that this transaction is a vote that was cast
from a proof-of-stake ticket holder. In this particular example, the
user had previously purchased a ticket for 8.99472311 DCR and was
sent 10.82959184 DCR after the vote was cast in this transaction.
