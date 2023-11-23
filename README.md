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

enter the `helper` and you will get a template like this:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity  0.8.19;

contract HelperConfig {
    struct NetworkConfig {
        uint256 name;
    }

    uint256 public DEFAULT_ANVIL_PRIVATE_KEY = 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80;

    constructor() {}
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

If you have any questions, please let me know directly in the discussion board...

Now,just enjoy it~~~
