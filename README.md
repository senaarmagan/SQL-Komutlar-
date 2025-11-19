# SQL Nedir?

**SQL (Structured Query Language)**, ilişkisel veritabanlarını yönetmek ve onlarla etkileşim kurmak için kullanılan standart bir sorgulama dilidir. Veri ekleme, silme, güncelleme, sorgulama, tablo oluşturma, yetki yönetimi gibi birçok işlemi gerçekleştirmek için kullanılır.

SQL, veri yönetimi dünyasında en yaygın kullanılan dillerden biridir ve MySQL, PostgreSQL, Oracle, SQL Server, SQLite gibi pek çok veritabanı sistemi tarafından desteklenir.

---

# SQL Komut Türleri

SQL komutları genel olarak 5 kategoriye ayrılır:

## 1. DDL (Data Definition Language)

Veritabanı yapısını oluştuma ve değiştirme komutlarıdır. Tablo ve nesne yapısını yönetir.

 `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `COMMENT`, `RENAME`

## 2. DML (Data Manipulation Language)

Tablodaki verileri ekleme, değiştirme, silme gibi veri üzerinde işlem yapar.

 `INSERT`, `UPDATE`, `DELETE`, `CALL`, `EXPLAIN CALL`, `LOCK TABLE`

## 3. DCL (Data Control Language)

Kullanıcı yetkilerini yönetir. Yetki ve izin kontrölü yapar.

 `GRANT`, `REVOKE`, `DENY`

## 4. TCL (Transaction Control Language)

Veritabanı işlemlerini yönetir. İşlemleri kaydeder veya geri alır. 

Transaction = Veritabanlarında yapılan işlemlerin otomatik olarak gerçekleşmesini ve hatalarda geri alınabilmesini sağlayan çalışma mantığıdır.

 `COMMIT`, `ROLLBACK`, `SAVEPOINT`

## 5. DQL (Data Query Language)

Veriyi sorgulamak için kullanılır. Veriyi okur/sorgular.

`SELECT`:

---

# Temel SQL Komut Örnekleri

### DQL - SELECT 
Bir tablodan verinin seçilmesine yarar.

```sql
SELECT * FROM employees;
```
### DML - INSERT 
Yeni kayıt ekler. Eksik kalanlara varsayılan değer atanır(NULL veya DEFAULT)

```sql
INSERT INTO employees (name, age) VALUES ('Ahmet', 30);
```
### DML - UPDATE 
Mevcut veriyi günceller. Eğer WHERE komutu kullanılmadığında hepsini günceller. 

```sql
UPDATE employees SET age = 31 WHERE name = 'Ahmet';
```
### DML - DELETE 
Mevcut kaydı siler. Sadece belirtilen kayıtları siler.

```sql
DELETE FROM employees WHERE name = 'Ahmet';
```
### DML - CALL 

```sql

```
### DML - EXPLAIN CALL 

```sql

```
### DML - LOCK TABLE

```sql

```
### DDL - CREATE 
Tablo oluşturur.

```sql
CREATE TABLE emplooyes(
              id INT PrimaryKEY,
              name VarCHAR(100),
              salary DECIMAL(10,2),
              depertmant_id INT);
```
### DDL - ALTER 
Kolon ekleme / silme / değiştirme / güncelleştirme yapar.

```sql
ALTER TABLE employees ADD birthdate DATE;
ALTER TABLE employees DROP COLUMN birthdate;
ALTER TABLE employees MODIFY salary DECIMAL(10,2);
```
### DDL - DROP
Bir tabloyu tamamen kalıcı olarak siler. 

```sql
DROP TABLE emplooyes;
```
### DDL - TRUNCATE 
Tabloyu boşaltır. Geri alınamaz fakat tablonun içindeki verileri siler tablo yapısını korur.

```sql
TRUNCATE TABLE employees;
```
### DDL - RENAME 
Tablonun adını değiştirir.

```sql
RENAME TABLE employees TO staff;
```
### DDL - COMMENT 

```sql

```
### DCL - GRANT
Kullanıcılara yetki verir. Güvenlik için kullanılır.

```sql
GRANT SELECT, INSERT ON employees TO user1;
```
### DCL - REVOKE
Yetkileri geri alır. Kullanıcı erişimi kaybeder.

```sql
REVOKE INSERT ON employees TO user1;
```
### DCL - DENY

```sql

```
### TCL - COMMIT
Yapılan değişiklikleri kalıcı hale getirir. Transaction onaylanır. Değişiklikler geri alınamaz.

```sql
COMMIT;
```
### TCL - ROLLBACK
Değişiklikleri geri alır. Commit yapılmamış tüm işlemler geri döner.

```sql
ROLLBACK;
```
### TCL - SAVEPOINT
Ara kontrol noktası oluşturur. ROLLBACK işlemini daha küçük bölümlere ayırır.

```sql
SAVEPOINT sp1;
```
### TCL - SET TRANSACTION

```sql

```
### TCL - SET CONSTRAINT

```sql

```
















# Kaynaklar

