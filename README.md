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
SELECT * FROM film; -- Tüm kolonları gösterir.
SELECT column1, column2,... FROM film; -- Sadece istenilen kolonlar gösterilir.
```
### DML - INSERT 
Yeni kayıt ekler. Eksik kalanlara varsayılan değer atanır(NULL veya DEFAULT)

```sql
INSERT INTO actor(first_name, last_name) VALUES ('Ahmet', 'Veli');
```
### DML - UPDATE 
Mevcut veriyi günceller. Eğer WHERE komutu kullanılmadığında hepsini günceller. 

```sql
UPDATE actor SET first_name='Ayşe' WHERE actor_id=1;
```
### DML - DELETE 
Mevcut kaydı siler. Sadece belirtilen kayıtları siler.

```sql
DELETE FROM film_actor WHERE actor_id=1;
```
### DML - CALL 
Bir veritabanı içinde tanımlanmış stored procedure çalıştırmak için kullanılan DML komutudur.
```sql
CALL update_all_salaries(); -- Parametresiz procedure çağırma
CALL add_employee('Ahmet', 'Yilmaz', 45000);  -- Parametre alan procedure çağırma
```
### DML - EXPLAIN CALL 
Bir stored procedure çalıştırılmadan önce veritabanının bu çağrıyı nasıl işlediğini, hangi planı kullanacağını ve hangi adımların gerçekleşeceğini analiz etmek için kullanılır.
```sql
EXPLAIN CALL update_all_salaries(); -- Bu komut procedure içerisinde yer alan SELECT/UPDATE/INSERT sorgularının yürütme planını döker.
EXPLAIN CALL add_employee('Ahmet', 'Yılmaz', 45000); -- Paramtre alarak bu şekilde çalışabilir.
EXPLAIN ANALYZE CALL update_all_salaries(); -- PostgreSQL gibi sistemlerde bu şekilde çalışır.
```
### DML - LOCK TABLE
Bir tabloyu belirli bir kilit (lock) moduyla kilitleyerek diğer işlemlerin bu tablo üzerinde okuma/yazma yapmasını kontrol eden bir DML komutudur.
Transaction içinde kullanılır ve veri bütünlüğünü korumak için kritik öneme sahiptir.
Kullanım amacı olarak aynı tablo üzerinde çakışan işlemleri engellemek, veri tutarlılığını korumak ve kritik güncelleme işlemleri sırasında diğer kullanıcıların müdahalesini engellemektir.
Bazı veritabanlarında kullanımı değişmektedir.
```sql
LOCK TABLE employees IN SHARE MODE; -- Başkaları tabloyu okuyabilir. Ancak tablo üzerinde UPDATE, DELETE, INSERT yapamaz.
LOCK TABLE employees IN EXCLUSIVE MODE; -- Diğer kullanıcıların tabloya erişimini tamamen engeller.
```
### DDL - CREATE 
Tablo oluşturur.

```sql
CREATE TABLE test_actor(
   actor_id SERIAL PRIMARY KEY,
	  first_name VARCHAR(50),
	  last_name VARCHAR(50),
	  birth_date DATE,
	  active BOOLEAN,
	  height_cm NUMERIC(5,2),
	  notes TEXT
);  # Yeni tablo oluşturur.
```
```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....; -- Başka tablodan bazı kolonlar alınarak yeni tablo oluşturur.
```
### DDL - ALTER 
Kolon ekleme / silme / değiştirme / güncelleştirme yapar.

```sql
ALTER TABLE test_actor ADD COLUMN email VARCHAR(50); -- Yeni sütun ekler.
ALTER TABLE test_actor RENAME COLUMN notes TO remarks; -- Sutün adını değiştirir.
ALTER TABLE test_actor ALTER COLUMN height_cm TYPE DECIMAL(6,2); -- Sütun tipini değiştirir.
ALTER TABLE test_actor DROP COLUMN active; -- Sütunu siler.
```
### DDL - DROP
Bir tabloyu tamamen kalıcı olarak siler. 

```sql
DROP TABLE test_actor;
```
### DDL - TRUNCATE 
Tabloyu boşaltır. Geri alınamaz fakat tablonun içindeki verileri siler tablo yapısını korur.

```sql
TRUNCATE TABLE test_actor;
```
### DDL - RENAME 
Tablonun adını değiştirir.

```sql
RENAME TABLE test_actor TO all_actors;
ALTER TABLE test_actor RENAME TO all_actors; -- PostgreSQL'de bu şekilde çalışır.
```
### DDL - COMMENT 
Bir tabloya veya sütuna açıklama eklemek için kullanılır.

```sql
COMMENT ON TABLE all_actors IS 'Tüm aktörlerin bilgilerini tutan test tablosudur.'; -- Tabloya yorum ekleme.
```
```sql
COMMENT ON COLUMN all_actors.first_name IS 'Aktörün adı'; -- Sütuna yorum ekleme.
```
### DCL - GRANT
Kullanıcılara yetki verir. Güvenlik için kullanılır.

```sql
GRANT SELECT ON TABLE all_actors TO public; -- Tüm kullanıcılara izin verir.
GRANT SELECT, INSERT, UPDATE, DELETE ON TABLE all_actors TO my_user; -- Belirli bir kullanıcıya izin verir. 
GRANT SELECT(first_name, last_name) ON TABLE all_actors TO my_user; -- Sütun bazlı izin verir.
```
```sql
CREATE ROLE actor_reader; -- Rol oluştur.
GRANT SELECT ON TABLE all_actors TO actor_reader; -- Oluşturulan role izin verir.
```
### DCL - REVOKE
Yetkileri geri alır. Kullanıcı erişimi kaybeder.

```sql
REVOKE SELECT ON TABLE all_actors FROM public; -- Daha önce herkese verilen tüm izinler kaldırılır.
REVOKE ALL PRIVILEGES ON TABLE all_actors FROM my_user; -- Kullanıcıya tabloya hiç bir şekilde erişemez.
REVOKE SELECT(first_name, last_name) ON TABLE all_actors FROM my_user; -- Kullanıcı sadece iki sütuna erişemez.
```
### DCL - DENY
DENY, bir kullanıcıya veya role belirli bir veritabanı nesnesi üzerindeki bir izni açıkça yasaklamak için kullanılan bir DCL komutudur. GRANT ile verilen izinlerden daha yüksek önceliğe sahiptir ve kullanıcıda ilgili izin olsa bile erişimi engeller.

```sql
DENY SELECT ON employees TO user1; -- user1 kullanıcısının employees tablosundan SELECT yapmasını engeller. PostgreSQL de DENY komutu yok.
```
### TCL - COMMIT
Yapılan değişiklikleri kalıcı hale getirir. Transaction onaylanır. Değişiklikler geri alınamaz.

```sql
BEGIN;
UPDATE all_actors SET first_name = 'Test' WHERE actor_id = 1;
COMMIT; -- Bir işlem başlatır ve kalıcı hale gelir.
```
### TCL - ROLLBACK
Değişiklikleri geri alır. Commit yapılmamış tüm işlemler geri döner.

```sql
BEGIN;
UPDATE all_actors SET first_name = 'Silinsin' WHERE actor_id = 1;
ROLLBACK; 
```
### TCL - SAVEPOINT
Ara kontrol noktası oluşturur. ROLLBACK işlemini daha küçük bölümlere ayırır.

```sql
BEGIN;
UPDATE all_actors SET height_cm = 180 WHERE actor_id = 1;
SAVEPOINT sp1;     -- Ara nokta oluştur.
UPDATE all_actors SET height_cm = 999 WHERE actor_id = 2;
ROLLBACK TO sp1;   -- 999 değişikliği geri alındı, ilk UPDATE kaldı.
COMMIT;
```
### TCL - SET TRANSACTION
Bir transaction’ın özelliklerini (örneğin isolation level, read/write modu gibi) başlatılmadan önce tanımlamak için kullanılan bir TCL komutudur.Bu komut, veritabanı işlemlerinin nasıl davranacağını kontrol etmeye yarar.
```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
-- işlemler
COMMIT;

```
```sql
BEGIN;
SET TRANSACTION READ ONLY;
SELECT * FROM all_actors;
COMMIT; -- Sadece okuma.
```
### TCL - SET CONSTRAINT
Bir transaction sırasında foreign key veya check constraint gibi kısıtlamaların ne zaman kontrol edileceğini belirlemek için kullanılan bir TCL komutudur. Özellikle PostgreSQL gibi sistemlerde yaygın kullanılır.Kısıtlamalar iki şekilde ayarlanabilir:

DEFERRED → Kısıtlamalar transaction sonuna kadar kontrol edilmez.

IMMEDIATE → Kısıtlamalar her işlemden sonra anında kontrol edilir.
```sql
BEGIN;
SET CONSTRAINTS ALL DEFERRED;
-- Geçici olarak FK hatası verecek işlemler yapılabilir.
COMMIT;   -- Burada constraint kontrol edilir.
```
















# Kaynaklar

