# CIG Factory SLP Locker

This project is a contract that can lock the CIG/ETH Sushi SLP tokens.

The locked tokens will be deposited to the CIG factory.

It's possible to harvest the CIG that they earned.

Additionally, it's possible to set up `stipends`, which are rate-limited
payments of CIG to any address. The payments come from CIG that has been
harvested.

Finally, there is a new withdrawal function that makes it possible to remove
the tokens after a certain period.


### Running the test

Assuming that you have NodeJs installed. After checking out this repo, install all the dependencies.

`$ npm update`

Use hardhat to run test, rename `hardhat.config.js.dist` to `hardhat.config.js` and paste your Alchemy API key in.

To run the test:
```
$ npx hardhat test test/locker.js
```

### Deployment

1. Deploy using your favourite deployment tool. The constructor has 3 arguments:

```solidity
constructor (address _cig, address _slp, uint64 _withdrawAt);
```

`_cig` is the cig token address `0xCB56b52316041A62B6b5D0583DcE4A8AE7a3C629`

`_slp` is the CIG/ETH slp address `0x22b15c7ee1186a7c7cffb2d942e20fc228f6e4ed`

`_withdrawAt` is a future UNIX timestamp, once passed, it will be possible for
the admin to call `withdraw()`

2. After deployment, make sure to verify the contract's source code on Etherscan. 
   Note down the contract's deployment address. 
3. Go to the [CIG/ETH SLP page on Etherscan](https://etherscan.io/address/0x22b15c7ee1186a7c7cffb2d942e20fc228f6e4ed#writeContract#F1) and approve the new contract. In the "spender" field, paste the deployed contract address, in the value field paste in `115792089237316195423570985008687907853269984665640564039457584007913129639935`
4. Go back to the page for this contract on Etherscan. Then use the `lock` function to lock some SLP tokens
3. Optional: Set up a stipend for yourself so that you can call harvest() any time.

