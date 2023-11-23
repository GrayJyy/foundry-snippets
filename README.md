# foundry-snippets

>When you need to create a script sol to deploy your contract

enter the `script` and your will get a template like this:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

import {Script} from "forge-std/Script.sol";
import {HelperConfig} from "./HelperConfig.s.sol";

contract Name is Script {
    // HelperConfig public helperConfig;

    constructor() {}

    function run()
        external
        returns (
            /**
             * (Contract contract)
             */
            HelperConfig helperConfig
        )
    {
        helperConfig = new HelperConfig();

        vm.startBroadcast();
        // deploy your contract here...
        vm.stopBroadcast();
    }
}

```

>When you need to create a helperConfig sol to configure your params

enter the `helper` and you will get a template like this(be sure you have set the .env file):

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

import {Script} from "forge-std/Script.sol";

contract HelperConfig is Script {
    error HelperConfig__ChainIdNotSupported();

    struct NetworkConfig {
        uint256 deployerKey;
    }

    uint256 public DEFAULT_ANVIL_PRIVATE_KEY = 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80;
    NetworkConfig public activeNetworkConfig;

    constructor() {
        if (block.chainid == 31337) {
            activeNetworkConfig = getOrCreateAnvilNetworkConfig();
        } else if (block.chainid == 11155111) {
            activeNetworkConfig = getSepoliaNetworkConfig();
        } else {
            revert HelperConfig__ChainIdNotSupported();
        }
    }

    function getOrCreateAnvilNetworkConfig() internal returns (NetworkConfig memory _anvilNetworkConfig) {
        // Check to see if we set an active network config
        if (activeNetworkConfig.deployerKey == DEFAULT_ANVIL_PRIVATE_KEY) {
            return activeNetworkConfig;
        }

        vm.startBroadcast();
        // deploy the mocks...
        vm.stopBroadcast();

        _anvilNetworkConfig = NetworkConfig({deployerKey: DEFAULT_ANVIL_PRIVATE_KEY});
    }

    function getSepoliaNetworkConfig() internal view returns (NetworkConfig memory _sepoliaNotworkConfig) {
        _sepoliaNotworkConfig = NetworkConfig({deployerKey: vm.envUint("PRIVATE_KEY")});
    }
}


```

>When you need to create a test sol to test your contract

enter the `init` and you will get a template like this:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

import {Test, console} from "forge-std/Test.sol";
import {Vm} from "forge-std/Vm.sol";
import {HelperConfig} from "../../script/HelperConfig.s.sol";

contract Name is Test {
    HelperConfig public helperConfig;

    constructor() {}
    function setUp() external {}
}

```

And more code snippets like `test`,`expect emit`,`expect revert`,`prank`,`deal`,`wrap`....

If you have any questions, please let me know directly in the discussion board ---> https://github.com/GrayJyy/foundry-snippets


Now,just enjoy it~~~
