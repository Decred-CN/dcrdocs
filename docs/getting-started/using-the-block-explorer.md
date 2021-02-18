# <img class="dcr-icon" src="/img/dcr-icons/BlockExplorer.svg" /> 使用区块浏览器

---

## <img class="dcr-icon" src="/img/dcr-icons/Info.svg" /> 总览

在Decred区块链中通过区块浏览器可以查看所有的区块和交易[dcrdata](https://github.com/decred/dcrdata)。

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

选项                   | 解释
---                      | ---
`Number of Transactions` | 标准交易数量 (DCR从一个用户发送到另一个用户)。
`Height`                 | 这个区块在区块链的位置（高度）。
`Block Reward`           | 这个区块铸造出的新DCR的数量。
`Timestamp`              | 区块被矿工挖出并添加到区块链的时间。
`Merkle Root`            | 包含此区块的所有交易的哈希值。
`Stake Root`             | 包含此区块的所有投票交易的哈希值。包含了买票、投票和撤回票。
`VoteBits`               | (1) 区块被POS投票人批准。 (2) 区块被POS投票人否决并且该区块中包含的所有非投票交易以及针对工作量证明矿工和Decred国库的新生成区块奖励均是无效的。
`Final State`            | 票证选择的伪随机数生成器的最终状态。
`Voters`                 | 此区块中成功进行的POS投票的数量，最大值是5。
`Fresh Stake`            | 此区块中购买选票被确认的数量。
`Revocations`            | 投票失败和被撤销的选票数量。
`PoolSize`               | 所有活跃POS选票的总量。
`Difficulty`             | POW网络挖矿难度。
`SBits`                  | 一张POS选票的价格。
`Bits`                   | 区块被挖出时的网络难度的紧凑版本。
`Size`                   | 区块的大小(单位bytes)。
`Version`                | 区块的版本。
`Nonce`                  | 矿工用来打包区块的正确解决方案的值。

## <img class="dcr-icon" src="/img/dcr-icons/Transactions.svg" /> 交易

这个章节列出了所有被矿工挖出包含到此区块的交易。
这些交易按照交易手续费从高到低的顺序被从内存池中选出并打包。
这个区块中的所有交易大概都包括: 标准交易 (点对点传输)，权益证明投票，权益证明购票。
以下各节将讲解每种交易。

---

### 标准交易

标准Decred交易信息说明：

选项              | 解释
---                 | ---
`Size`              | 交易大小（单位bytes）。
`Fee rate`          | 网络手续费（每kB）。
`Received Time`     | 网络确认的时间。
`Mined Time`        | 矿工将交易打包的时间。
`Included in Block` | 包含此交易的区块编号。

注意 `Received Time（接受时间）`, `Mined Time（打包时间）`, and `Included in Block（区块包含）`在矿工验证并包含到decred区块之前是空值，在交易被一个区块确认，交易被认为是完成了。


---

### <img class="dcr-icon" src="/img/dcr-icons/TicketLive.svg" /> 购票交易

购票交易和标准交易有几处不同之处。

注意细微的差别： 这个词`Ticket`出现在发送者钱包地址左侧，然后这个词`SubsidyCommitment`出现在右侧，
This particular user purchased a stake ticket for 8.75411638 DCR and received change in the amount
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
