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

Kullanıcı yetkilerini yönetir. Yetki ve izin kontrolü yapar.

 `GRANT`, `REVOKE`, `DENY`

## 4. TCL (Transaction Control Language)

Veritabanı işlemlerini yönetir. İşlemleri kaydeder veya geri alır. 

Transaction = Veritabanlarında yapılan işlemlerin otomatik olarak gerçekleşmesini ve hatalarda geri alınabilmesini sağlayan çalışma mantığıdır.

 `COMMIT`, `ROLLBACK`, `SAVEPOINT`

## 5. DQL (Data Query Language)

Veriyi sorgulamak için kullanılır. Veriyi okur/sorgular.

`SELECT`

---

# Temel SQL Komut Örnekleri

### DQL - SELECT 
Bir tablodan verinin seçilmesine yarar.

```sql
SELECT * FROM employees; # tüm kolonları gösterir
SELECT column1, column2,... FROM employees; # Sadece istenilen kolonlar gösterilir.
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
              name varchar(100),
              salary decimal(10,2),
              depertmant_id INT);  #yeni tablo oluşturur.
```
```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....; # başka tablodan bazı kolonlar alınarak yeni tablo oluşturur.
```
### DDL - ALTER 
Kolon ekleme / silme / değiştirme / güncelleştirme yapar.

```sql
ALTER TABLE employees ADD birthdate DATE; # yeni kolon ekler
ALTER TABLE employees DROP COLUMN birthdate; # kolonu siler
ALTER TABLE employees MODIFY salary DECIMAL(10,2); # veri tipini değiştirir
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
Bir tabloya veya sütuna açıklama eklemek için kullanılır.

```sql
COMMENT ON TABLE employees IS 'Çalışan bilgilerini tutan tablo'; #Tabloya yorum ekleme
```
```sql
COMMENT ON COLUMN employees.name IS 'Çalışanın adı'; #Sütuna yorum ekleme
SELECT * FROM employees;
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
DENY, bir kullanıcıya veya role belirli bir veritabanı nesnesi üzerindeki bir izni açıkça yasaklamak için kullanılan bir DCL komutudur. GRANT ile verilen izinlerden daha yüksek önceliğe sahiptir ve kullanıcıda ilgili izin olsa bile erişimi engeller.

```sql
DENY SELECT ON employees TO user1; # user1 kullanıcısının employees tablosundan SELECT yapmasını engeller:
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
Bir transaction’ın özelliklerini (örneğin isolation level, read/write modu gibi) başlatılmadan önce tanımlamak için kullanılan bir TCL komutudur.Bu komut, veritabanı işlemlerinin nasıl davranacağını kontrol etmeye yarar.
```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
BEGIN;
SELECT * FROM orders;
COMMIT; # isolation belirleme
```
```sql
SET TRANSACTION READ ONLY;
BEGIN;
SELECT COUNT(*) FROM logs;
COMMIT; # sadece okuma
```
```sql
SET TRANSACTION READ WRITE;
BEGIN;
UPDATE employees SET salary = salary * 1.1;
COMMIT; # sadece yazma
```
### TCL - SET CONSTRAINT
Bir transaction sırasında foreign key veya check constraint gibi kısıtlamaların ne zaman kontrol edileceğini belirlemek için kullanılan bir TCL komutudur. Özellikle PostgreSQL gibi sistemlerde yaygın kullanılır.Kısıtlamalar iki şekilde ayarlanabilir:

DEFERRED → Kısıtlamalar transaction sonuna kadar kontrol edilmez.

IMMEDIATE → Kısıtlamalar her işlemden sonra anında kontrol edilir.
```sql
BEGIN;
SET CONSTRAINTS ALL DEFERRED; # Bu işlemler sırasında FK hatası hemen oluşmaz
UPDATE orders SET customer_id = 999 WHERE id = 1; 
UPDATE customers SET id = 999 WHERE id = 10;
COMMIT; # Tüm kısıtlamaları transaction sonuna erteleme
```
```sql
BEGIN;
SET CONSTRAINTS fk_orders_customer DEFERRED;
UPDATE orders SET customer_id = 200 WHERE id = 5;
COMMIT; # Belirli bir constraint’i DEFERRED yapma
```
```sql
SET CONSTRAINTS ALL IMMEDIATE; # Kısıtlamaları tekrar IMMEDIATE moda alma
# Bu durumda, o anda geçersiz bir veri varsa sistem anında hata verir
```















# Kaynaklar

