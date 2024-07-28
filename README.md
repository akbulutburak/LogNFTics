

# LogNFTics Akıllı Sözleşmesi

Bu proje, lojistik yönetimi için NFT'ler (ERC721) kullanarak tasarlanmış bir Solidity akıllı sözleşmesi olan `LogNFTics` içermektedir. Sözleşme, Scroll Sepolia Testnet üzerinde dağıtılmıştır.

## Ön Koşullar

Başlamadan önce, aşağıdaki gereksinimlerin karşılandığından emin olun:
- Node.js ve npm yüklü
- Truffle veya Hardhat yüklü
- Scroll Sepolia Testnet için yapılandırılmış MetaMask veya başka bir Ethereum cüzdanı

*Sepolia Testnet'teki Sözleşme Adresi*

*Sözleşme adresi:0xb8146569b661676A72Ea0E6c3cAd065b6a52861D *
https://sepolia.scrollscan.com/address/0xb8146569b661676a72ea0e6c3cad065b6a52861d

*Yaratıcı adresi:0x2A98F7CBb27f38ff5dAa62D83CE43a7ECe81c3CB *

*Veri Yapıları*

struct Shipment {
    uint256 id;  // Gönderi Kimliği
    string origin;  // Gönderinin Kökeni
    string destination;  // Gönderinin Hedefi
    string status;  // Gönderinin Durumu
    uint256 timestamp;  // Zaman Damgası
    string sender;  // Gönderici
    string receiver;  // Alıcı
    uint256 weight;  // Ağırlık
    string dimensions;  // Boyutlar
    string additionalInfo;  // Ek Bilgi
}

*Fonksiyonlar*
createShipment(string memory _origin, string memory _destination, string memory _sender, string memory _receiver, uint256 _weight, string memory _dimensions, string memory 
_additionalInfo): Yeni bir gönderi oluşturur ve NFT olarak mint eder.

updateShipmentStatus(uint256 _id, string memory _status): Belirtilen gönderinin durumunu günceller.

updateShipmentDetails(uint256 _id, string memory _sender, string memory _receiver, uint256 _weight, string memory _dimensions, string memory _additionalInfo): Belirtilen gönderinin detaylarını günceller.

getShipment(uint256 _id): Belirtilen gönderinin bilgilerini döner.

changeManager(address newManager): Sözleşme sahibini değiştirir.

#Kullanım
Yeni bir gönderi oluşturmak ve mint etmek için:
LogNFTics.createShipment("Ankara", "İstanbul", "Gönderici", "Alıcı", 100, "10x10x10", "Ek bilgi");

Gönderi Durumunu Güncelleme
LogNFTics.updateShipmentStatus(1, "Yolda");

Gönderi Detaylarını Güncelleme
LogNFTics.updateShipmentDetails(1, "Yeni Gönderici", "Yeni Alıcı", 120, "15x15x15", "Yeni ek bilgi");

Gönderi Bilgilerini Alma
LogNFTics.getShipment(1);

Yöneticiyi Değiştirme
LogNFTics.changeManager("0xYeniSahipAdres");








