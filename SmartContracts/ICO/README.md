# ORX ICO Contract

* Solidity version: `0.5.8`
* This contract uses the OpenZepellin's `SafeMath` library
* This contract uses a custom `admined` contract features
  * The administration is managed by user levels
    * 0 is a normal user
    * 1 is basic admin
    * 2 is a master admin
  * The master admin is set to the `0x7a3a57c620fA468b304b5d1826CDcDe28E2b2b98` on deployment
  * Only a master admin can add other admins
* This ICO contract have no time deadline
* The total tokens amount to distribute is: 420.000.000 tokens
* This contract is designed to work with 7 tranches in total:
  * 1st: 52.500.000 at 40% bonus
  * 2nd: 52.500.000 at 35% bonus
  * 3rd: 52.500.000 at 30% bonus
  * 4th: 52.500.000 at 20% bonus
  * 5th: 52.500.000 at 10% bonus
  * 6th: 52.500.000 at 5% bonus
  * 7th: 31.500.000 at 0% bonus
* The base rate is 1 ETH = 2941 tokens
* The soft cap is set to 3.000.000 tokens
  * Once soft cap is reached, beneficiary can progressively retrieve collected funds
* The contract allow admins to manually distribute tokens to enable non Ethereum blockchain contributions
* Refunds are available directly on contract
  * Only to ETH contributors
  * Once soft cap is reached
* Direct contributions to the contract are allowed through fallback function
* ICO contract functions:
```
    contract admined {
        mapping(address => uint8) public level;
        function adminshipLevel(address _newAdmin, uint8 _level) onlyAdmin(2) public;
        event AdminshipUpdated(address _newAdmin, uint8 _level);
    }

    contract ICO {
        //state related
        State public state;
        //time related
        uint256 public SaleStartTime;
        uint256 public completedAt;
        //token related
        ERC20Interface public tokenReward;
        //funding related
        uint256 public totalRaised;
        uint256 public totalDistributed;
        uint256 public totalBonusDistributed;
        uint256 public constant rate;
        uint256 public constant trancheSize;
        uint256 public constant hardCap;
        uint256 public constant softCap;
        mapping(address => uint256) public invested;
        mapping(address => uint256) public received;
        //info
        address public owner;
        address payable public beneficiary;
        string public version = '1';
        //functions
        function contribute(address _target, uint256 _value) public payable;
        function checkIfFundingCompleteOrExpired() public;
        function withdrawEth() onlyAdmin(2) public;
        function getRefund() public;
        function finished() public;
        //events for log
        event LogFundingInitialized(address _owner);
        event LogFundingReceived(address _addr, uint _amount, uint _currentTotal);
        event LogContributorsPayout(address _addr, uint _amount);
        event LogBeneficiaryPaid(address _beneficiaryAddress);
        event LogFundingSuccessful(uint _totalRaised);
    }
