https://solodit.cyfrin.io/issues/h-01-executeisolateliquidate-totalbidamoutavailableliquidity-incorrect-accounting-code4rena-benddao-benddao-git

**Issue:** The BendDAO `YieldEthStakingLido` contract integrates with **Lido Finance** for ETH staking. Lido's withdrawal queue has a strict **Maximum Withdrawal Amount** of **1,000 stETH** per request.

**Vulnerability:** The BendDAO contract allowed users to perform multiple "stakes" on the same NFT position. While it checked that each _individual_ deposit was below the limit, it failed to check if the **total accumulated balance** exceeded 1,000 ETH.

**Impact:** If a user's total stake (initial deposit + rewards) grows beyond 1,000 ETH, any attempt to unstake will trigger a call to Lido for the full amount. Since this exceeds Lido's 1,000 ETH limit, the transaction will **always revert**, effectively locking the user's funds in the protocol. ⛓️

**Recommendation:** Implement a global cap on the total staked amount per position or develop a "batching" logic to split large withdrawals into multiple requests of 1,000 ETH or less.