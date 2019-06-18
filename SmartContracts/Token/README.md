# ORX TOKEN

ORX is a custom ERC20 standard token built for the Ethereum Blockchain.

* Solidity version: `0.5.8`
* Name: `Orionix`
* Symbol: `ORX`
* Initial Supply: `600.000.000`
* Decimals: `18`
* This contract uses the OpenZepellin's ``SafeMath`` library

# How the contract works

* On deployment the ``owner`` of the contract is set to ``0xA0c6f96035d0FA5F44D781060F84A0Bc6B8D87Ee``.

* The initial supply is sent to the ``0xA0c6f96035d0FA5F44D781060F84A0Bc6B8D87Ee`` on deployment.

* Comply with the ERC20 Standard and implement the following interface:
    
    ```
    contract ERC20TokenInterface {
        function balanceOf(address _owner) public view returns(uint256 value);
        function transfer(address _to, uint256 _value) public returns(bool success);
        function transferFrom(address _from, address _to, uint256 _value) public returns(bool success);
        function approve(address _spender, uint256 _value) public returns(bool success);
        function allowance(address _owner, address _spender) public view returns(uint256 remaining);
    }

* This contract extends the ERC20 standard using a ``Owned`` contract.
* This contract extends the ERC20 standard using a ``burnTokens()`` function.
  * Only the ``owner`` is allowed to burn tonkens from its own wallet.
  * The ``burnTokens()`` function can be limited using the ``supplyLock()`` modifier.
