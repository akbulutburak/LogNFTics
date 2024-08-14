
# LogNFTX Smart Contract


This project includes a Solidity smart contract called LogNFTics, designed for logistics management using NFTs (ERC721). The contract has been deployed on the Scroll Sepolia Testnet.

## Prerequisites

Before you begin, ensure the following requirements are met:

-MetaMask or another Ethereum wallet configured for Scroll Sepolia Testnet

## Contract Address

- **Contract Address:**: 0x50Bd0Fd6Ca70D4c887f0783Ac8E83A66Ca53B609 -https://sepolia.scrollscan.com/token/0x50bd0fd6ca70d4c887f0783ac8e83a66ca53b609
- **Creator Address:**: 0x2A98F7CBb27f38ff5dAa62D83CE43a7ECe81c3CB

## Data Structures

```solidity
uint256 id;               // Shipment ID
    string origin;        // Origin of the shipment
    string destination;   // Destination of the shipment
    string status;        // Status of the shipment
    uint256 timestamp;    // Timestamp
    string sender;        // Sender
    string receiver;      // Receiver
    uint256 weight;       // Weight
    string dimensions;    // Dimensions
    string additionalInfo;// Additional information

Functions
createShipment: Creates a new shipment and mints it as an NFT
function createShipment(
    string memory _origin, 
    string memory _destination, 
    string memory _sender, 
    string memory _receiver, 
    uint256 _weight, 
    string memory _dimensions, 
    string memory _additionalInfo
) public onlyOwner {
    shipmentCounter++;
    shipments[shipmentCounter] = Shipment(shipmentCounter, _origin, _destination, "Created", block.timestamp, _sender, _receiver, _weight, _dimensions, _additionalInfo);
    _mint(msg.sender, shipmentCounter); // NFT mintleme
    emit ShipmentCreated(shipmentCounter, _origin, _destination, block.timestamp, _sender, _receiver, _weight, _dimensions, _additionalInfo);
}

updateShipmentStatus: Updates the status of a specified shipment.

function updateShipmentStatus(uint256 _id, string memory _status) public onlyOwner {
    require(shipments[_id].id != 0, "Shipment does not exist");
    shipments[_id].status = _status;
    shipments[_id].timestamp = block.timestamp;
    emit ShipmentStatusUpdated(_id, _status, block.timestamp);
}

updateShipmentDetails: Updates the details of a specified shipment.

function updateShipmentDetails(
    uint256 _id, 
    string memory _sender, 
    string memory _receiver, 
    uint256 _weight, 
    string memory _dimensions, 
    string memory _additionalInfo
) public onlyOwner {
    require(shipments[_id].id != 0, "Shipment does not exist");
    shipments[_id].sender = _sender;
    shipments[_id].receiver = _receiver;
    shipments[_id].weight = _weight;
    shipments[_id].dimensions = _dimensions;
    shipments[_id].additionalInfo = _additionalInfo;
    emit ShipmentDetailsUpdated(_id, _sender, _receiver, _weight, _dimensions, _additionalInfo);
}

getShipment: Returns the information of a specified shipment.

function getShipment(uint256 _id) public view returns (Shipment memory) {
    require(shipments[_id].id != 0, "Shipment does not exist");
    return shipments[_id];
}

changeManager: Changes the owner of the contract..
function changeManager(address newManager) public onlyOwner {
    transferOwnership(newManager);
}
Usage
LogNFTics.createShipment("Ankara", "Istanbul", "Sender", "Receiver", 100, "10x10x10", "Additional information");
LogNFTics.updateShipmentStatus(1, "In Transit");
LogNFTics.updateShipmentDetails(1, "New Sender", "New Receiver", 120, "15x15x15", "New additional information");
LogNFTics.getShipment(1);
LogNFTics.changeManager("0xNewOwnerAddress");
