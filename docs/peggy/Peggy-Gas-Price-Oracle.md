 # Peggy Gas Price Oracle

The document explains the why Peggy need gas price oracle and its implementation.


## Ethereum Gas Fee
Currently, the peggy fee mechanism is fixed which does not account for network volatility and changing gas prices. Due to this, if gas prices spike drastically on ethereum and users unpeg, we are stuck with the deficit between the gas price the user paid, and the gas price that the relayers paid.

## Solution
We develop a gas oracle based on the code of ebrelayer, listening the Ethereum new block and get the new suggeusted gas price, then wrap it into a Cosmos transaction sent to Sifchain. And Sifchain just accept the transaction from admin account, will reject update gas price transaction from other accounts.

For UI, we provide a REST API to get current gas price from sifnoded. 

## Transaction
1. transaction format
sifnodecli tx ethbridge update_gas_price [cosmos-validator-address] [ethereum-block-number] [gas-price]

2. transaction example
sifnodecli tx ethbridge update_gas_price sifvaloper1syavy2npfyt9tcncdtsdzf7kny9lh777dzsqna 100 100 --from=sif --yes

## Future features
1. peg multiple EVM-based chains
We need a map to record the gas price for different blockchains like bsc, etc.

