# SQL Nedir?

**SQL (Structured Query Language)**, ilişkisel veritabanlarını yönetmek ve onlarla etkileşim kurmak için kullanılan standart bir sorgulama dilidir. Veri ekleme, silme, güncelleme, sorgulama, tablo oluşturma, yetki yönetimi gibi birçok işlemi gerçekleştirmek için kullanılır.

SQL, veri yönetimi dünyasında en yaygın kullanılan dillerden biridir ve MySQL, PostgreSQL, Oracle, SQL Server, SQLite gibi pek çok veritabanı sistemi tarafından desteklenir.

---

# SQL Komut Türleri

SQL komutları genel olarak 5 kategoriye ayrılır:

## 1. DDL (Data Definition Language)

Veritabanı yapısını oluştuma ve değiştirme komutlarıdır. Tablo ve nesne yapısını yönetir.

* `CREATE`
* `ALTER`
* `DROP`
* `TRUNCATE`
* `COMMENT`
* `RENAME`

## 2. DML (Data Manipulation Language)

Tablodaki verileri ekleme, değiştirme, silme gibi veri üzerinde işlem yapar.

* `INSERT`
* `UPDATE`
* `DELETE`
* `CALL`
* `EXPLAIN CALL`
* `LOCK TABLE`

## 3. DCL (Data Control Language)

Kullanıcı yetkilerini yönetir. Yetki ve izin kontrölü yapar.

* `GRANT`
* `REVOKE`
* `DENY`

## 4. TCL (Transaction Control Language)

Veritabanı işlemlerini yönetir. İşlemleri kaydeder veya geri alır. 
Trnsaction = Veritabanlarında yapılan işlemlerin otomatik olarak gerçekleşmesini ve hatalarda geri alınabilmesini sağlayan çalışma mantığıdır.

* `COMMIT`
* `ROLLBACK`
* `SAVEPOINT`

## 5. DQL (Data Query Language)

Veriyi sorgulamak için kullanılır. Veriyi okur/sorgular.

* `SELECT`:

---

# Temel SQL Komut Örnekleri

### SELECT – Veri Sorgulama

```sql
SELECT * FROM employees;
```

### INSERT – Veri Ekleme

```sql
INSERT INTO employees (name, age) VALUES ('Ahmet', 30);
```

### UPDATE – Veri Güncelleme

```sql
UPDATE employees SET age = 31 WHERE name = 'Ahmet';
```

### DELETE – Veri Silme

```sql
DELETE FROM employees WHERE name = 'Ahmet';
```


# Kaynaklar

