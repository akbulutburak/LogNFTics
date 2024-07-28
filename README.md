
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

## Fonksiyonlar







