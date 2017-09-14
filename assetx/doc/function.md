ASSETXCOIN Token Smart Contract: Functional Requirements

This document summarizes functional requirements for ASSETXCOIN Token Smart Contract.

0. Introduction

ASSETXCOIN Token Smart Contract is an ERC-20 compliant Ethereum smart contract that manages ASSETXCOIN Tokens - lightweight cryptocurrency whose units represents shares in Blockchain Capital investment fund. The following sections of this document describe functional requirements for Blockchain Capital Token Smart Contract.

1. Use Cases

This sections describes use cases for ASSETXCOIN Token Smart Contract. Related use cases are grouped into following functional.

1.1. ERC-20 Functional Block

This functional block contains use cases required by ERC-20 standard.

1.1.1. ERC-20:TotalSupply

Actors: User, Smart Contract

Goal: User wants to know how many tokens are currently in circulation

Main Flow:

User calls constant method on Smart Contract
Smart Contract returns to User total number of tokens in circulation
1.1.2. ERC-20:BalanceOf

Actors: User, Smart Contract

Goal: User wants to know how many tokens are currently belonging to the owner of certain address

Main Flow:

User calls constant method on Smart Contract providing the following information as method parameters: address to get number of tokens currently belonging to the owner of
Smart Contract returns to User number of tokens currently belonging to the owner of given address
1.1.3. ERC-20:Transfer

Actors: User, Smart Contract

Goal: User wants to transfer some of his tokens to the owner of certain address

Main Flow:

User calls method on Smart Contract providing the following information as method parameters: address to transfer tokens to the owner of and number of tokens to transfer
Token transfers are not currently frozen
User is not central bank
There are enough tokens currently belonging to User
Destination address is not central bank address
Smart Contract transfers requested number of tokens from User to the owner of given address
Some tokens actually did change hands during the transfer, i.e. destination address was not the same as User's own address and number of tokens transferred is greater than zero
Smart Contract logs tokens transfer event with the following information: address tokens were transferred from the owner of, address tokens were transferred to the owner of, and number of tokens transferred
Smart Contract returns success indicator to User
Exceptional Flow #1:

Same as in Main Flow
Token transfers are currently frozen
Smart Contract returns error indicator to User
Exceptional Flow #2:

Same as in Main Flow
Same as in Main Flow
User is central bank
Number of tokens currently in circulation plus number of tokens to transfer is not greater than maximum allowed number of tokens in circulation
Destination address in not central bank address
Smart Contract creates as many new tokens as many tokens are to be transferred
Smart Contract transfers newly created tokens to the owner of given address
Some tokens were actually created, i.e. number of tokens created is greater than zero
Smart Contract logs tokens transfer event with the following information: central bank address as source address, address tokens were transferred to the owner of, and number of tokens transferred
Smart Contract returns success indicator to User
Exceptional Flow #3:

Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #2
Number of tokens currently in circulation plus number of tokens to transfer is greater than maximum allowed number of tokens in circulation
Smart Contract returns error indicator to User
Exceptional Flow #4:

Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #2
Same as in Exceptional Flow #2
Destination address in central bank address
Smart Contract returns success indicator to User
Exceptional Flow #5:

Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #2
Same as in Exceptional Flow #2
Same as in Exceptional Flow #2
Same as in Exceptional Flow #2
Same as in Exceptional Flow #2
No tokens were actually created, i.e. number of tokens created is zero
Smart Contract returns success indicator to User
Exceptional Flow #6:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
There is not enough tokens currently belonging to User
Smart Contract returns error indicator to User
Exceptional Flow #7:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Destination address is central bank address
Smart Contract destroys as many tokens belonging to User as many tokens are to be transferred
Some tokens actually were destroyed, i.e. number of tokens destroyed is greater than zero
Smart Contract logs tokens transfer event with the following information: User address as source address, central bank address as destination address, and number of tokens destroyed
Smart Contract returns success indicator to User
Exceptional Flow #8:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #7
Same as in Exceptional Flow #7
No tokens were actually destroyed, i.e. number of tokens destroyed is zero
Smart Contract returns success indicator to User
Exceptional Flow 9:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
No tokens actually did change hands during the transfer, i.e. destination address was User's own address, or number of tokens transferred was zero
Smart Contract returns success indicator to User
1.1.4. ERC-20:TransferFrom

Actors: User, Smart Contract

Goal: User wants to transfer some of the tokens currently belonging to the owner of certain source address to the owner of certain destination address

Main Flow:

User calls method on Smart Contract providing the following information as method parameters: source address, destination address, and number of tokens to transfer
Token transfers are not currently frozen
User is currently allowed to transfer requested number of tokens from the owner of source address
Source address is not central bank address
There are enough tokens currently belonging to the owner of source address
Destination address is not central bank address
Smart Contract transfers requested number of tokens from the owner of source address to the owner of destination address
Smart Contract decreases by the number of tokens transferred the number of tokens User is allowed to transfer from the owner of source address
Some tokens actually did change hands during the transfer, i.e. destination address was not the same as source address and number of tokens transferred was greater than zero
Smart Contract logs token transfer event with the following information: source address, destination address, and number of tokens transferred
Smart Contract returns success indicator to User
Exceptional Flow #1:

Same as in Main Flow
Token transfers are currently frozen
Smart Contract returns error indicator to User
Exceptional Flow #2:

Same as in Main Flow
Same as in Main Flow
User is not currently allowed to transfer requested number of tokens from the owner of source address
Smart Contract returns error indicator to User
Exceptional flow #3:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Source address is central bank address
Number of tokens currently in circulation plus number of tokens to transfer is not greater than maximum allowed number of tokens in circulation
Destination address is not central bank address
Smart Contract creates as many new tokens as many tokens are to be transferred
Smart Contract transfers newly created tokens to the owner of given address
Smart Contract decreases by the number of tokens created the number of tokens User is allowed to transfer from the owner of source address
Some tokens were actually created, i.e. number of tokens created is greater than zero
Smart Contract logs token transfer event with the following information: source address, destination address, and number of tokens transferred
Smart Contract returns success indicator to User
Exceptional Flow #4:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #3
Number of tokens currently in circulation plus number of tokens to transfer is greater than maximum allowed number of tokens in circulation
Smart Contract returns error indicator to User
Exceptional Flow #5:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #3
Same as in Exceptional Flow #3
Destination address is central bank address
Smart Contract returns success indicator to User
Exceptional Flow #6:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #3
Same as in Exceptional Flow #3
Same as in Exceptional Flow #3
Same as in Exceptional Flow #3
Same as in Exceptional Flow #3
Same as in Exceptional Flow #3
No tokens were actually created, i.e. number of tokens created is zero
Smart Contract returns success indicator to User
Exceptional Flow #7:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
There are not enough tokens currently belonging to the owner of source address
Smart Contract returns error indicator to User
Exceptional Flow #8:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Destination address is central bank address
Smart Contract destroys as many tokens belonging to User as many tokens are to be transferred
Smart Contract decreases by the number of tokens destroyed the number of tokens User is allowed to transfer from the owner of source address
Some tokens actually were destroyed, i.e. number of tokens destroyed is greater than zero
Smart Contract logs tokens transfer event with the following information: source address, destination address, and number of tokens destroyed
Smart Contract returns success indicator to User
Exceptional Flow #9:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Exceptional Flow #8
Same as in Exceptional Flow #8
Same as in Exceptional Flow #8
No tokens were actually destroyed, i.e. number of tokens destroyed is zero
Smart Contract returns success indicator to User
Exceptional Flow #10:

Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
Same as in Main Flow
same as in Main Flow
same as in Main Flow
same as in Main Flow
No tokens actually did change hands during the transfer, i.e. destination address was the same as source address or number of tokens transferred was zero
Smart Contract returns success indicator to User
1.1.5. ERC-20:Approve

Actors: User, Smart Contract

Goal: User wants to set how many tokens belonging to User the owner of certain address is allowed to transfer

Main Flow:

User calls method on Smart Contract providing the following information as method parameters: address to allow the owner of to transfer tokens belonging to *User and number of tokens to allow transfer of
Smart Contract set the number of tokens belonging to User the owner of given address is allowed to transfer
Smart Contract logs token transfer approval event with the following information: User's address, address the owner of was allowed to transfer tokens belonging to User, and number of tokens the transfer was allowed of
Smart Contract returns success indicator to User
1.1.6. ERC-20:Allowance

Actors: User, Smart Contract

Goal: User wants to know how many tokens belonging to the owner of certain source address the owner of certain spender address is currently allowed to transfer

Main Flow:

User calls constant method on Smart Contract providing the following information as method parameters: source address and spender address
Smart Contract returns to User the number of tokens belonging to the owner of source address the owner of spender address is currently allowed to transfer
1.2. Administration Functional Block

This functional block contains use cases related to smart contract administration.

1.2.1. Administration:Deploy

Actors: User, Smart Contract

Goal: User wants to deploy Smart Contract with certain central bank address

Main Flow:

User deploys Smart Contract providing the following information as constructor arguments: central bank address
Smart Contract remember given central bank address
1.2.2. Administration:Freeze

Actors: User, Smart Contract

Goal: User wants to freeze token transfers

Main Flow:

User calls method on Smart Contract
User is the owner of Smart Contract
Token transfers are not currently frozen
Smart Contract freezes token transfer
Smart Contract logs token transfers freeze event
Exceptional Flow #1:

Same as in Main Flow
User is not the owner of Smart Contract
*Smart Contract cancels transaction
Exceptional Flow #2:

Same as in Main Flow
Same as in Main Flow
Token transfers are currently frozen
Smart Contract does nothing
1.2.3. Administration:Unfreeze

Actors: User, Smart Contract

Goal: User wants to unfreeze token transfers

Main Flow:

User calls method on Smart Contract
User is the owner of Smart Contract
Token transfers are currently frozen
Smart Contract unfreezes token transfer
Smart Contract logs token transfers unfreeze event
Exceptional Flow #1:

Same as in Main Flow
User is not the owner of Smart Contract
*Smart Contract cancels transaction
Exceptional Flow #2:

Same as in Main Flow
Same as in Main Flow
Token transfers are not currently frozen
Smart Contract does nothing
2. Limits

The following limits are established:

Limit	Value
Maximum number of tokens in circulation	2^256-1
