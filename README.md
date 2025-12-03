# API Testing dengan REST Assured

Proyek ini merupakan implementasi **API Testing** menggunakan **REST Assured** dan **Postman** untuk pengujian RESTful API. Fokus utama adalah testing endpoint CRUD dengan berbagai skenario pengujian.

## Fitur Utama

- **User Management API** (CRUD operations)
- **HTTP Method Testing** (GET, POST, PUT, DELETE)
- **Response Validation** (status code, headers, body)
- **Authentication Testing** (Bearer Token)
- **Data Extraction & Chaining** (response parsing)

## Struktur Project
```text
api-testing-rest-assured/
├── src/
│   └── test/java/com/praktikum/api/
│       ├── UserAPITest.java
│       ├── AuthenticationTest.java
│       └── ChainedRequestTest.java
├── postman/
│   └── API_Testing_Collection.json
├── pom.xml
└── README.md
```

## Tools dan Teknologi

- **Java 21+**
- **Maven** (manajemen dependensi & build)
- **REST Assured 5.3.0** (API testing framework)
- **JUnit 5.9.2** (test runner)
- **Hamcrest** (assertion library)
- **Postman** (manual API testing)
- **ReqRes API** (https://reqres.in) - public testing API

## Cara Menjalankan Test

1. Pastikan **Java 21+** dan **Maven** sudah terinstal.

2. Clone repository:
```bash
git clone https://github.com/naursyy/api-testing-rest-assured.git
```

3. Install dependencies:
```bash
mvn clean install
```

4. Jalankan semua test:
```bash
mvn clean test
```

5. Jalankan test spesifik:
```bash
mvn test -Dtest=UserAPITest
```

## Test Coverage

### 1. GET Request Testing
- ✅ Get single user by ID
- ✅ Get list of users with pagination
- ✅ Validate response schema
- ✅ Validate response time
- ✅ Handle 404 Not Found

### 2. POST Request Testing
- ✅ Create new user
- ✅ Validate created data
- ✅ Test with invalid payload
- ✅ Test required fields validation

### 3. PUT Request Testing
- ✅ Update existing user (full update)
- ✅ Validate updated timestamp
- ✅ Test partial update (PATCH)

### 4. DELETE Request Testing
- ✅ Delete user by ID
- ✅ Validate 204 No Content response
- ✅ Verify deletion

### 5. Authentication Testing
- ✅ Login with valid credentials
- ✅ Login with invalid credentials
- ✅ Bearer token validation
- ✅ Register new user

## Contoh Test Case
```java
@Test
public void testGetSingleUser() {
    given()
        .baseUri("https://reqres.in")
        .basePath("/api/users/2")
    .when()
        .get()
    .then()
        .statusCode(200)
        .body("data.id", equalTo(2))
        .body("data.email", notNullValue())
        .time(lessThan(2000L));
}
```

## Response Status Code

| Status Code | Deskripsi |
|-------------|-----------|
| 200 OK | Request berhasil |
| 201 Created | Resource berhasil dibuat |
| 204 No Content | Berhasil tanpa response body |
| 400 Bad Request | Invalid request payload |
| 401 Unauthorized | Authentication gagal |
| 404 Not Found | Resource tidak ditemukan |

## Assertion Types

| Assertion | Penggunaan |
|-----------|------------|
| `statusCode()` | Validasi HTTP status |
| `body()` | Validasi response body |
| `header()` | Validasi response header |
| `time()` | Validasi response time |
| `contentType()` | Validasi Content-Type |

## Postman Collection

Collection Postman tersedia di folder `postman/` dengan environment variables:
- `base_url`: https://reqres.in
- `user_id`: Dynamic variable
- `token`: Authentication token

Import collection ke Postman untuk manual testing.

## Best Practices

- **Base URI Configuration** → Set di BaseTest untuk reusability
- **Request Specification** → Gunakan untuk common settings
- **Response Specification** → Standardisasi validasi response
- **Data-Driven Testing** → Parameterized tests untuk multiple scenarios
- **Logging** → Enable request/response logging untuk debugging
- **Assertion Library** → Gunakan Hamcrest matchers

## Tips Testing

1. **Test Independence** → Setiap test harus berdiri sendiri
2. **Cleanup** → Hapus test data setelah eksekusi
3. **Meaningful Names** → Gunakan naming convention yang jelas
4. **Positive & Negative** → Test happy path dan edge cases
5. **Performance** → Validate response time < 2 detik

## Troubleshooting

### Connection Timeout
```java
given()
    .config(RestAssured.config()
        .httpClient(HttpClientConfig.httpClientConfig()
            .setParam("http.connection.timeout", 5000)))
```

### SSL Certificate Issues
```java
RestAssured.useRelaxedHTTPSValidation();
```

## Referensi

- [REST Assured Documentation](https://rest-assured.io/)
- [ReqRes API Documentation](https://reqres.in/)
- [Hamcrest Matchers Guide](http://hamcrest.org/JavaHamcrest/)

---

**Politeknik Negeri Cilacap** - Modul Praktikum 8: API Testing dengan Postman dan REST Assured
