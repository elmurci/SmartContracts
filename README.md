Smart Contracts
===================

Compilation of tricks, good practices and cheatsheet for (Solidity) Smart Contracts in Ethereum. 

Sources of the information displayed here are at the bottom of this file.

Feel free to PR and add content!

----------


Good Practices & Tricks
-------------

> - All calls that send to untrusted address should have a gas limit.
> - Balances should be reduced before a send, not after one.
> - Use ```delete``` on arrays to delete all its elements.
> - Initialise storage structs with a single assignment: 
```x = MyStruct({a: 1, b: ```2});
> - If you do not want your contracts to receive ether when called via send, you can add a throwing fallback function: 
```function() { throw; }```.
> - Make your state variables public - the compiler will create getters for you for free.

(Solidity) Cheatsheet
-------------

> **Global Variables:**

> - ```block.blockhash(uint blockNumber) returns (bytes32):``` hash of the given block - only works for 256 most recent blocks
> - ```block.coinbase (address):``` current block miner’s address
> - ```block.difficulty (uint):``` current block difficulty
> - ```block.gaslimit (uint):``` current block gaslimit
> - ```block.number (uint):``` current block number
> - ```block.timestamp (uint):``` current block timestamp
> - ```msg.data (bytes):``` complete calldata
> - ```msg.gas (uint):``` remaining gas
> - ```msg.sender (address):``` sender of the message (current call)
> - ```msg.value (uint):``` number of wei sent with the message
> - ```now (uint):``` current block timestamp (alias for block.timestamp)
> - ```tx.gasprice (uint):``` gas price of the transaction
> - ```tx.origin (address):``` sender of the transaction (full call chain)

> **Scope Variables:**

> - ```this (current contract’s type):``` the current contract, explicitly convertible to address
> - ```super:``` the contract one level higher in the inheritance hierarchy

> **Global Functions:**

> - ```sha3(...) returns (bytes32):``` compute the Ethereum-SHA-3 (KECCAK-256) hash of the (tightly packed) arguments
> - ```sha256(...) returns (bytes32):``` compute the SHA-256 hash of the (tightly packed) arguments
> - ```ripemd160(...) returns (bytes20):``` compute the RIPEMD-160 hash of the (tightly packed) arguments
> - ```ecrecover(bytes32 hash, uint8 v, bytes32 r, bytes32 s) returns (address):``` recover address associated with the public key from elliptic curve signature
> - ```addmod(uint x, uint y, uint k) returns (uint):``` compute (x + y) % k where the addition is performed with arbitrary precision and does not wrap around at 2**256
> - ```mulmod(uint x, uint y, uint k) returns (uint):``` compute (x * y) % k where the multiplication is performed with arbitrary precision and does not wrap around at 2**256
> - ```selfdestruct(address recipient):``` destroy the current contract, sending its funds to the given address
> - ```address.balance (uint256):``` balance of the address in Wei
> - ```address.send(uint256 amount) returns (bool):``` send given amount of Wei to address, returns false on failure

> **Function Visibility Specifiers:**
> 
```function myFunction() <visibility specifier> returns (bool) { 
	return true;
}```

> - ```public:``` visible externally and internally (creates accessor function for storage/state variables)
> - ```private:``` only visible in the current contract
> - ```external:``` only visible externally (only for functions) - i.e. can only be message-called (via this.fun)
> - ```internal:``` only visible internally

> **Modifiers:**

> - ```constant for state variables:``` Disallows assignment (except initialisation), does not occupy storage slot.
> - ```constant for functions:``` Disallows modification of state - this is not enforced yet.
> - ```anonymous for events:``` Does not store event signature as topic.
> - ```indexed for event parameters:``` Stores the parameter as topic.


References
-------------


  [1]:  [b9lab Solidity Cheatsheet](http://https://s3-eu-west-1.amazonaws.com/b9-academy-assets/public/solidity-cheatsheet.pdf)
  
  [2]:  [Peter Vessenes](http://vessenes.com)
