Example:

https://solodit.cyfrin.io/issues/m-01-staked-assets-can-be-locked-in-lido-due-to-vulnerable-check-in-yieldethstakinglidoprotocoldeposit-code4rena-benddao-benddao-git

### **Checklist for External ERC-20 Tokens** 

When auditing a contract that interacts with an external token (like `externalToken.transfer()`), always investigate these behaviors:

1. **Fee-on-Transfer:** Does the token charge a fee on every transfer? 💸
    - _Risk:_ If you send 100 tokens but only 95 arrive, your contract’s internal accounting (balances) will become out of sync with the actual token balance.
    
2. **Blacklisting:** Does the token have a "blacklist" or "blocklist" feature? 🚫
    - _Risk:_ If the `msg.sender` or the contract itself is blacklisted, the transaction will fail, potentially locking funds or causing a Denial of Service (DoS) for specific users.
    
3. **Revert on Failure:** Does the token call `revert()` on a failed transfer, or does it simply return `false`? ⚠️
    - _Risk:_ Many older tokens (like some implementations of USDT) do not revert on failure. If your contract doesn't check the return value, it might assume the transfer was successful when it actually failed.