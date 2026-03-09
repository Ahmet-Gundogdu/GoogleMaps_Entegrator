# Google Maps API Key Alma Rehberi

**Proje:** CRM-Backend (Laravel 10)  
**Tarih:** 6 Mart 2026

---

## İçindekiler

1. [Google Cloud Console Hesap Oluşturma](#1-google-cloud-console-hesap-oluşturma)
2. [Yeni Proje Oluşturma](#2-yeni-proje-oluşturma)
3. [Faturalandırma Hesabı Ayarlama](#3-faturalandırma-hesabı-ayarlama)
4. [API'leri Etkinleştirme](#4-apileri-etkinleştirme)
5. [API Key Oluşturma](#5-api-key-oluşturma)
6. [API Key Kısıtlama (Güvenlik)](#6-api-key-kısıtlama-güvenlik)
7. [Laravel Projesine Entegrasyon](#7-laravel-projesine-entegrasyon)
8. [Test Etme](#8-test-etme)
9. [Kotalar ve Fiyatlandırma](#9-kotalar-ve-fiyatlandırma)
10. [Sorun Giderme](#10-sorun-giderme)

---

## 1. Google Cloud Console Hesap Oluşturma

1. Tarayıcınızda [Google Cloud Console](https://console.cloud.google.com/) adresine gidin.
2. Google hesabınızla giriş yapın (Gmail hesabınız yeterlidir).
3. İlk kez giriyorsanız **Hizmet Şartları**'nı kabul edin.
4. Ülke bilgilerinizi seçin ve **Kabul Et ve Devam Et** butonuna tıklayın.

> **Not:** Yeni kullanıcılar için Google Cloud, **90 gün boyunca 300$ ücretsiz kredi** sunmaktadır.

---

## 2. Yeni Proje Oluşturma

1. Cloud Console'da sol üst köşedeki **proje seçici** açılır menüsüne tıklayın.
2. Açılan pencerede **Yeni Proje** butonuna tıklayın.
3. Proje bilgilerini doldurun:
   - **Proje Adı:** `crm-backend` (veya istediğiniz bir isim)
   - **Kuruluş:** Varsa kuruluşunuzu seçin, yoksa "Kuruluş yok" olarak bırakın
   - **Konum:** İsteğe bağlı
4. **Oluştur** butonuna tıklayın.
5. Proje oluşturulduktan sonra, proje seçiciden yeni projenizi seçtiğinizden emin olun.

---

## 3. Faturalandırma Hesabı Ayarlama

> **Önemli:** Google Maps API'lerini kullanabilmek için faturalandırma hesabı **zorunludur**. Ancak aylık 200$'lık ücretsiz kullanım hakkınız vardır.

1. Sol menüden **Faturalandırma** (Billing) seçeneğine gidin.
2. **Faturalandırma Hesabı Bağla** butonuna tıklayın.
3. Yeni bir faturalandırma hesabı oluşturun:
   - Ülke: **Türkiye**
   - Hesap türü: **Bireysel** veya **İş**
   - Ödeme bilgileri: Geçerli bir kredi/banka kartı ekleyin
4. **Gönder ve Faturalandırmayı Etkinleştir** butonuna tıklayın.

### Aylık Ücretsiz Kullanım ($200 Kredi)

| API | Ücretsiz Kullanım Limiti |
|-----|--------------------------|
| Places API (Text Search) | ~5.000 istek/ay |
| Place Details | ~5.000 istek/ay |
| Geocoding API | ~40.000 istek/ay |
| Maps JavaScript API | ~28.000 yükleme/ay |

---

## 4. API'leri Etkinleştirme

Projemiz için aşağıdaki API'lerin etkinleştirilmesi gerekmektedir:

### 4.1 Places API (New) — Zorunlu

1. Sol menüden **API'ler ve Hizmetler** > **Kitaplık** (Library) seçeneğine gidin.
2. Arama çubuğuna **"Places API (New)"** yazın.
3. Sonuçlardan **Places API (New)** seçin.
4. **Etkinleştir** (Enable) butonuna tıklayın.

### 4.2 Geocoding API — Zorunlu

1. Kitaplık sayfasında **"Geocoding API"** arayın.
2. **Geocoding API** seçin ve **Etkinleştir** butonuna tıklayın.

### 4.3 Maps JavaScript API — İsteğe Bağlı (Frontend için)

1. Kitaplık sayfasında **"Maps JavaScript API"** arayın.
2. **Maps JavaScript API** seçin ve **Etkinleştir** butonuna tıklayın.

> **Proje için gerekli API'ler:**
> - **Places API (New):** Text Search ve Place Details için (`places.googleapis.com`)
> - **Geocoding API:** Adres-koordinat dönüşümü için (`maps.googleapis.com`)

---

## 5. API Key Oluşturma

1. Sol menüden **API'ler ve Hizmetler** > **Kimlik Bilgileri** (Credentials) seçeneğine gidin.
2. Üst kısımdaki **+ Kimlik Bilgisi Oluştur** butonuna tıklayın.
3. Açılan menüden **API Anahtarı** (API Key) seçin.
4. API anahtarınız otomatik olarak oluşturulacaktır.
5. Oluşan anahtarı **kopyalayın ve güvenli bir yere kaydedin**.

> **Uyarı:** API Key'i asla herkese açık bir yerde (GitHub, frontend kodu vb.) paylaşmayın!

---

## 6. API Key Kısıtlama (Güvenlik)

Oluşturulan API Key'e kısıtlama eklemek, güvenlik açısından **kritik öneme** sahiptir.

### 6.1 Uygulama Kısıtlamaları

1. **Kimlik Bilgileri** sayfasında oluşturduğunuz API Key'in yanındaki **kalem ikonuna** tıklayın.
2. **Uygulama kısıtlamaları** bölümünde:

   **Backend (Sunucu) kullanımı için:**
   - **IP adresleri** seçin
   - Sunucunuzun IP adresini ekleyin (ör: `185.x.x.x`)
   - Geliştirme ortamı için: `127.0.0.1` ve `::1`

   **Frontend kullanımı için:**
   - **HTTP yönlendiricileri** seçin
   - İzin verilen domain'leri ekleyin (ör: `https://crm.yourdomain.com/*`)

### 6.2 API Kısıtlamaları

1. Aynı düzenleme sayfasında **API kısıtlamaları** bölümüne gidin.
2. **Anahtarı kısıtla** seçin.
3. Sadece ihtiyacınız olan API'leri seçin:
   - ✅ Places API (New)
   - ✅ Geocoding API
   - ✅ Maps JavaScript API (frontend kullanılıyorsa)
4. **Kaydet** butonuna tıklayın.

---

## 7. Laravel Projesine Entegrasyon

### 7.1 `.env` Dosyasına Key Ekleme

Proje kök dizinindeki `.env` dosyasına aşağıdaki satırları ekleyin:

```env
GOOGLE_MAPS_API_KEY=AIzaSy_BURAYA_KENDI_API_KEYINIZI_YAZIN
GOOGLE_MAPS_ENABLED=true
```

### 7.2 Yapılandırma Doğrulama

Projede `config/googlemaps.php` dosyası zaten mevcuttur ve aşağıdaki yapılandırmayı içerir:

```php
return [
    'api_key' => env('GOOGLE_MAPS_API_KEY'),
    'enabled' => env('GOOGLE_MAPS_ENABLED', true),
    'defaults' => [
        'language' => 'tr',
        'region' => 'TR',
        'max_results' => 20,
    ],
    'endpoints' => [
        'places_search' => 'https://places.googleapis.com/v1/places:searchText',
        'place_details' => 'https://places.googleapis.com/v1/places/',
        'geocoding' => 'https://maps.googleapis.com/maps/api/geocode/json',
    ],
    // ...
];
```

### 7.3 API Key Erişimi (Kod İçinde)

```php
// API Key'e erişim
$apiKey = config('googlemaps.api_key');

// Etkinlik kontrolü
$isEnabled = config('googlemaps.enabled');

// Varsayılan dil
$language = config('googlemaps.defaults.language'); // "tr"
```

> **Uyarı:** Kod içinde asla `env('GOOGLE_MAPS_API_KEY')` kullanmayın! Her zaman `config('googlemaps.api_key')` tercih edin.

---

## 8. Test Etme

### 8.1 Terminal ile Hızlı Test

Places API (New) Text Search testi:

```bash
curl -X POST "https://places.googleapis.com/v1/places:searchText" \
  -H "Content-Type: application/json" \
  -H "X-Goog-Api-Key: API_KEYINIZ" \
  -H "X-Goog-FieldMask: places.displayName,places.formattedAddress" \
  -d '{"textQuery": "restoran istanbul kadıköy", "languageCode": "tr"}'
```

Geocoding API testi:

```bash
curl "https://maps.googleapis.com/maps/api/geocode/json?address=Istanbul&key=API_KEYINIZ"
```

### 8.2 Laravel Tinker ile Test

```bash
php artisan tinker
```

```php
$apiKey = config('googlemaps.api_key');
echo "API Key: " . substr($apiKey, 0, 10) . "...";

// Basit bir Geocoding isteği
$response = Http::get('https://maps.googleapis.com/maps/api/geocode/json', [
    'address' => 'Istanbul, Turkey',
    'key' => $apiKey,
]);

echo $response->json()['status']; // "OK" dönmeli
```

### 8.3 Beklenen Başarılı Yanıt

```json
{
  "status": "OK",
  "results": [
    {
      "formatted_address": "İstanbul, Türkiye",
      "geometry": {
        "location": {
          "lat": 41.0082376,
          "lng": 28.9783589
        }
      }
    }
  ]
}
```

---

## 9. Kotalar ve Fiyatlandırma

### 9.1 Fiyatlandırma Tablosu (Mart 2026)

| API | Fiyat (1.000 istek) | Aylık Ücretsiz |
|-----|---------------------|----------------|
| Places Text Search | ~$32 | ~6.250 istek |
| Place Details (Basic) | ~$17 | ~11.765 istek |
| Place Details (Advanced) | ~$40 | ~5.000 istek |
| Geocoding | ~$5 | ~40.000 istek |

> **Not:** Fiyatlar değişkenlik gösterebilir. Güncel fiyatlar için [Google Maps Platform Fiyatlandırma](https://developers.google.com/maps/billing-and-pricing/pricing) sayfasını kontrol edin.

### 9.2 Kota Limitleri Ayarlama

Beklenmedik yüksek faturaları önlemek için kota limitleri ayarlayın:

1. **API'ler ve Hizmetler** > **Kotalar** sayfasına gidin.
2. İlgili API'yi seçin.
3. **Günlük istek limiti** belirleyin (ör: 1.000 istek/gün).
4. **Faturalandırma Uyarıları** oluşturun:
   - **Faturalandırma** > **Bütçeler ve uyarılar** > **Bütçe Oluştur**
   - Aylık bütçe limiti belirleyin (ör: $50)
   - Uyarı eşiklerini ayarlayın (%50, %90, %100)

---

## 10. Sorun Giderme

### Sık Karşılaşılan Hatalar

| Hata | Sebep | Çözüm |
|------|-------|-------|
| `REQUEST_DENIED` | API Key geçersiz veya API etkinleştirilmemiş | API Key'i kontrol edin, ilgili API'nin etkinleştirildiğinden emin olun |
| `OVER_QUERY_LIMIT` | Günlük kota aşıldı | Kota limitlerini artırın veya ertesi gün tekrar deneyin |
| `INVALID_REQUEST` | Geçersiz parametreler | İstek parametrelerini ve formatını kontrol edin |
| `API key not valid` | Yanlış/eksik API Key | `.env` dosyasındaki key'i doğrulayın, `php artisan config:clear` çalıştırın |
| `This API project is not authorized` | API kısıtlaması | API Key kısıtlamalarını kontrol edin |

### Hızlı Kontrol Listesi

```bash
# 1. Config cache temizleme
php artisan config:clear

# 2. API Key'in doğru yüklendiğini kontrol etme
php artisan tinker --execute="echo config('googlemaps.api_key');"

# 3. .env dosyasında key var mı kontrol
grep GOOGLE_MAPS .env
```

### Google Cloud Console'da Hata İzleme

1. **API'ler ve Hizmetler** > **Gösterge Tablosu** (Dashboard) sayfasına gidin.
2. İlgili API'yi seçin.
3. **Metrikler** sekmesinde:
   - İstek sayısı
   - Hata oranı
   - Gecikme süresi grafiklerini inceleyebilirsiniz.

---

## Özet Kontrol Listesi

- [ ] Google Cloud Console hesabı oluşturuldu
- [ ] Yeni proje oluşturuldu
- [ ] Faturalandırma hesabı bağlandı
- [ ] Places API (New) etkinleştirildi
- [ ] Geocoding API etkinleştirildi
- [ ] API Key oluşturuldu
- [ ] API Key kısıtlamaları ayarlandı (IP + API kısıtlaması)
- [ ] `.env` dosyasına `GOOGLE_MAPS_API_KEY` eklendi
- [ ] `GOOGLE_MAPS_ENABLED=true` ayarlandı
- [ ] API Key test edildi ve çalışıyor
- [ ] Kota limitleri ve faturalandırma uyarıları ayarlandı
