// SPDX-License-Identifier: MIT
pragma solidity ^0.8.22;

import { IOApp, ILayerZeroEndpointV2 } from "./interfaces/IOApp.sol";
import { OAppSender } from "./OAppSender.sol";
// @dev import the origin so its exposed to OApp implementers
import { OAppReceiver, Origin } from "./OAppReceiver.sol";

abstract contract OApp is IOApp, OAppSender, OAppReceiver {
    constructor(address _endpoint, address _owner) {
        _transferOwnership(_owner);
        endpoint = ILayerZeroEndpointV2(_endpoint);
    }

    function oAppVersion() public pure virtual returns (uint64 senderVersion, uint64 receiverVersion) {
        senderVersion = SENDER_VERSION;
        receiverVersion = RECEIVER_VERSION;
    }
}
