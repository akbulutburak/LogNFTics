
# LogNFTics Akıllı Sözleşmesi

Bu proje, lojistik yönetimi için NFT'ler (ERC721) kullanarak tasarlanmış bir Solidity akıllı sözleşmesi olan `LogNFTics` içermektedir. Sözleşme, Scroll Sepolia Testnet üzerinde dağıtılmıştır.

## Ön Koşullar

Başlamadan önce, aşağıdaki gereksinimlerin karşılandığından emin olun:

- Scroll Sepolia Testnet için yapılandırılmış MetaMask veya başka bir Ethereum cüzdanı

## Sözleşme Adresi

- **Sözleşme Adresi**: [0xb8146569b661676A72Ea0E6c3cAd065b6a52861D](https://sepolia.scrollscan.com/address/0xb8146569b661676a72ea0e6c3cad065b6a52861d)
- **Yaratıcı Adresi**: 0x2A98F7CBb27f38ff5dAa62D83CE43a7ECe81c3CB

## Veri Yapıları

```solidity
struct Shipment {
    uint256 id;           // Gönderi Kimliği
    string origin;        // Gönderinin Kökeni
    string destination;   // Gönderinin Hedefi
    string status;        // Gönderinin Durumu
    uint256 timestamp;    // Zaman Damgası
    string sender;        // Gönderici
    string receiver;      // Alıcı
    uint256 weight;       // Ağırlık
    string dimensions;    // Boyutlar
    string additionalInfo;// Ek Bilgi
}

Fonksiyonlar
createShipment: Yeni bir gönderi oluşturur ve NFT olarak mint eder.
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

updateShipmentStatus: Belirtilen gönderinin durumunu günceller.

function updateShipmentStatus(uint256 _id, string memory _status) public onlyOwner {
    require(shipments[_id].id != 0, "Shipment does not exist");
    shipments[_id].status = _status;
    shipments[_id].timestamp = block.timestamp;
    emit ShipmentStatusUpdated(_id, _status, block.timestamp);
}

updateShipmentDetails: Belirtilen gönderinin detaylarını günceller.

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

getShipment: Belirtilen gönderinin bilgilerini döner.

function getShipment(uint256 _id) public view returns (Shipment memory) {
    require(shipments[_id].id != 0, "Shipment does not exist");
    return shipments[_id];
}

changeManager: Sözleşme sahibini değiştirir.
function changeManager(address newManager) public onlyOwner {
    transferOwnership(newManager);
}
Kullanım
LogNFTics.createShipment("Ankara", "İstanbul", "Gönderici", "Alıcı", 100, "10x10x10", "Ek bilgi");
LogNFTics.updateShipmentStatus(1, "Yolda");
LogNFTics.updateShipmentDetails(1, "Yeni Gönderici", "Yeni Alıcı", 120, "15x15x15", "Yeni ek bilgi");
LogNFTics.getShipment(1);
LogNFTics.changeManager("0xYeniSahipAdres");

