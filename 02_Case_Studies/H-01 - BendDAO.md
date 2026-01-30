https://solodit.cyfrin.io/issues/h-01-executeisolateliquidate-totalbidamoutavailableliquidity-incorrect-accounting-code4rena-benddao-benddao-git

| **Component**   | **What happened?**                                              | **Impact**                                                    |
| --------------- | --------------------------------------------------------------- | ------------------------------------------------------------- |
| **Mathematics** | Added `extraAmount` twice to `availableLiquidity`.              | **Insolvency**: The system "prints" non-existent money. 💸    |
| **Variable**    | Subtracted the total debt from the bid pool (`totalBidAmount`). | **Panic Underflow**: Liquidation transactions fail/revert. 💥 |
| **Economy**     | The calculated Utilization ($U$) became artificially low.       | **Lower interest rates**, hurting yield for depositors. 📉    |
