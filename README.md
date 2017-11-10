# Multiownable

[![Build Status](https://travis-ci.org/bitclave/Multiownable.svg?branch=master)](https://travis-ci.org/bitclave/Multiownable)
[![Coverage Status](https://coveralls.io/repos/github/bitclave/Multiownable/badge.svg)](https://coveralls.io/github/bitclave/Multiownable)

BitClave implementation of Multiownable contract as improvement to OpenZeppelin Ownable contract

# Installation

1. Install [truffle](http://truffleframework.com) globally with `npm install -g truffle`
2. Install [testrpc](https://github.com/ethereumjs/testrpc) globally with `npm install -g ethereumjs-testrpc`
3. Install local packages with `npm install`
4. Run tests with `killall -9 node; npm test; killall -9 node;`

On macOS you also need to install watchman: `brew install watchman`

# Features

1. Simple usage: add modifiers `onlyAnyOwner` and `onlyManyOwners`
1. Support multiple pending operations
2. Allows owners to cancel pending operations
2. Reset all pending operations on ownership transfering

# Example of multisig wallet

```solidity
contract SimplestMultiWallet is Multiownable {

    function transferTo(address to, uint256 amount) onlyManyOwners {
        to.transfer(amount);
    }
    
}
```

# Example of multisig wallet with ERC20 tokens support

```solidity
contract SimplestTokensMultiWallet is Multiownable {

    function transferTo(address to, uint256 amount) onlyManyOwners {
        to.transfer(amount);
    }
    
    function transferTokensTo(address token, address to, uint256 amount) onlyManyOwners {
        ERC20(token).transfer(to, amount);
    }
    
}
```
