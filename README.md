
# PatikaWorkshop

Bu proje, **Patika** tarafından düzenlenen online workshop kapsamında, **Motoko Playground** aracıyla geliştirilmiş basit bir Motoko kodu örneğidir. Proje, temel bir **Phonebook (Telefon Rehberi)** uygulaması içerir ve aşağıdaki işlevleri sunar:

## Projenin Amacı

Patika Workshop eğitimi sırasında katılımcılara Motoko dilinin temel kavramlarını ve **Internet Computer** üzerinde aktör tabanlı uygulamalar geliştirme yöntemlerini öğretmek hedeflenmiştir. Bu kod, Motoko ile hem veri yönetimi hem de mesajlaşma işlevlerini nasıl birleştirebileceğinizi göstermektedir.

---

## Özellikler

1. **Telefon Rehberi Yönetimi**  
   - Kişi bilgilerini kaydedebilir ve sorgulayabilirsiniz.
2. **Mesajlaşma Sistemi**  
   - Telefon numarasına bağlı mesaj gönderimi ve mesaj geçmişini yönetebilirsiniz.

---

## Kullanılan Yapılar ve Fonksiyonlar

### Veritabanı Tipleri

- **`Name`**: Kişi isimlerini ifade eder (`Text`).
- **`Phone`**: Telefon numaralarını temsil eder (`Text`).
- **`Entry`**: Kişinin telefon numarası ve açıklamasını içerir:
  ```motoko
  type Entry = {
      desc : Text;
      phone : Phone
  };
  ```
- **`Message`**: Gönderilen mesajı ve alıcısını tanımlar:
  ```motoko
  type Message = {
      receiver : Text;
      message : Text
  };
  ```

### Haritalar (Maps)

- **`phoneBook`**: Telefon rehberi veritabanını tutar.  
  - **Anahtar (Key)**: `Name`
  - **Değer (Value)**: `Entry`
- **`MessageHistory`**: Mesaj geçmişini tutar.  
  - **Anahtar (Key)**: `Phone` (gönderenin telefon numarası)
  - **Değer (Value)**: `Message`

---

## Metotlar

### 1. Yeni Kişi Ekleme
```motoko
public func insert(name : Name, entry : Entry) : async ();
```
- Rehbere yeni bir kişi ekler.

### 2. Telefon Numarası Sorgulama
```motoko
public query func getPhone(name : Name) : async ?Entry;
```
- Belirli bir isme ait kişi bilgilerini getirir.

### 3. Mesaj Gönderme
```motoko
public func sendMessage(senderPhone : Phone, message : Message) : async ();
```
- Bir telefon numarası üzerinden mesaj gönderimini kaydeder.

### 4. Gönderilen Mesajları Sorgulama
```motoko
public query func getSentMessages(senderPhone : Phone) : async ?Message;
```
- Belirtilen telefon numarasıyla gönderilen son mesajı döndürür.

---

## Örnek Kullanım

- Yeni bir kişi eklemek:
  ```motoko
  await Phonebook.insert("Ahmet", {desc = "İş Arkadaşı", phone = "+905555555555"});
  ```

- Kişi bilgilerini sorgulamak:
  ```motoko
  let contact = await Phonebook.getPhone("Ahmet");
  ```

- Mesaj göndermek:
  ```motoko
  await Phonebook.sendMessage("+905555555555", {receiver = "Mehmet", message = "Merhaba!"});
  ```

- Gönderilen mesajları sorgulamak:
  ```motoko
  let messages = await Phonebook.getSentMessages("+905555555555");
  ```

---

## Teknoloji ve Araçlar

- **Motoko**: Kodlama dili.
- **Motoko Playground**: Kodun çalıştırıldığı geliştirme ortamı.
- **Patika.dev**: Eğitim platformu.

---
