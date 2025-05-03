
# 🍽️ Lavango Food Delivery

**Lavango Food Delivery** — REST API əsaslı yemək sifarişi sistemidir. Bu backend layihəsi istifadəçilərə restoranları araşdırmaq, menyudan məhsul seçmək, sifariş yaratmaq, ödəniş etmək və sifarişin çatdırılma prosesini izləmək imkanı verir. Sistem həmçinin real-time ödənişlər, kuryer axını və reytinq/rəy funksionallıqlarını dəstəkləyir.

---

## 🛠 Texnologiyalar

- **Java 17**
- **Spring Boot 3.2+**
- **Spring Data JPA + MySQL**
- **Spring Security + JWT**
- **Redis** (Caching)
- **Stripe API** (Real-time ödənişlər)
- **Spring Mail** (Email bildirişləri)
- **ELK Stack** (Elasticsearch + Logstash + Kibana)
- **JUnit 5 & Mockito** (Testing)

---

## 📦 Layihə Strukturu

```bash
src/
├── main/
│   └── java/
│       └── jpaprojects.lavangofooddelivery/
│           ├── config        # Konfiqurasiya (Security, Mail, JWT)
│           ├── controller    # REST API endpoint-ləri
│           ├── convertor     # DTO <-> Entity çevirmələri
│           ├── dtos          # Request və Response DTO-ları
│           ├── entity        # JPA Entity-ləri
│           ├── enums         # Status və rol sabitləri
│           ├── exception     # Custom istisnalar və handlerlər
│           ├── repository    # Spring Data JPA interfeysləri
│           └── service       # Biznes məntiqi
│
├── resources/
│   ├── templates             # Email üçün HTML fayllar
│   ├── application.properties
│   └── logback-spring.xml
```

---

## 👥 Rollar və İcazələr

| Rol       | İmkanlar                                                                |
|-----------|-------------------------------------------------------------------------|
| `ADMIN`   | Restoran və menyu idarəsi, sifarişi kuryerə təyin etmək                |
| `CUSTOMER`| Sifariş vermək, ödəniş etmək, rəy və reytinq yazmaq                    |
| `COURIER` | Təyin olunmuş sifarişin çatdırılma statusunu dəyişmək                  |

---

## 🔑 Əsas Funksionallıqlar

### 🧾 Auth
- Qeydiyyat və JWT token ilə giriş
- Role əsaslı endpoint icazələri

### 🏪 Restoran & Menyu
- Admin restoran və menyu əlavə/yenilə/sil
- Müştəri menyuya baxa və məhsul sifariş edə bilər

### 🛒 Sifariş Prosesi
- Səbətə məhsul əlavə et → sifariş yarat → status izlə
- Statuslar: `CREATED`, `PAID`, `IN_DELIVERY`, `DELIVERED`

### 💳 Ödəniş Sistemi
- Stripe Checkout ilə ödəniş linki yaradılır
- Webhook ilə uğurlu ödəniş backend-də `PAID` statusu ilə qeydə alınır

### 🚚 Çatdırılma
- Admin sifarişi bir `COURIER`-ə təyin edir
- Kuryer statusu dəyişə bilər (`IN_DELIVERY`, `DELIVERED`)

### 🌟 Reytinq və Rəy
- Yalnız `DELIVERED` və `PAID` sifarişlərə rəy yazmaq mümkündür
- Reytinqlər 1–5 arasıdır, restoran üçün orta qiymət hesablanır

### 📨 Email Bildirişləri
- Qeydiyyat, ödəniş təsdiqi, şifrə sıfırlama emailləri

### 🧠 Caching (Redis)
- `GET` sorğular üçün menyu və restoran məlumatları cache-lənir

### 📊 Loglama (ELK)
- JSON formatında loglar Logstash ilə Elasticsearch-a yazılır
- Kibana ilə vizuallaşdırma və analiz

---

## ⚙️ Konfiqurasiya (application.properties)

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/food_ordering_system
spring.datasource.username=root
spring.datasource.password=1234

spring.mail.username=your_email@gmail.com
spring.mail.password=your_email_password

jwt.secret=your_jwt_secret
stripe.secret-key=your_stripe_secret
```

---

## 🚀 Layihəni Başlatmaq

```bash
# 1. GitHub reposunu klonla
git clone https://github.com/JasurEynullayev/food_ordering_system.git
cd lavango-food-delivery

# 2. Maven build
./mvnw clean install

# 3. Backend-i işə sal
./mvnw spring-boot:run
```

---

## 🧪 Testlər

- `Service` sinifləri üçün `Mockito` ilə unit testlər
- `Stripe` və `Mail` üçün integration testlər
- `JUnit 5` istifadə olunur

---

## 📈 Gələcək Planlar

- Admin üçün dashboard paneli
- WebSocket ilə real-time çatdırılma izləmə
- Mobil tətbiq (Flutter)
- Frontend (React) inteqrasiyası

---

## 👤 Əlaqə

> **Jasur Eynullayev**  
> Backend Developer  
> ✉️ jasureynullayev@gmail.com  
> 🔗 [linkedin.com/in/jasureynullayev](https://linkedin.com/in/jasureynullayev)
