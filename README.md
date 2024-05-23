# dvdrental
#ÖDEV 1

1-) film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.

SELECT title, description FROM film;

2-) film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.

SELECT * FROM film
WHERE length > 60 AND length < 75;

3-) film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.

SELECT * FROM film
WHERE rental_rate = 0.99 AND replacement_cost = 12.99 
OR replacement_cost = 28.99;

4-) customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?

SELECT last_name FROM customer
WHERE first_name = 'Mary';

5-) film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.

SELECT * FROM film
WHERE length <= 50 
AND NOT (rental_rate = 2.99 OR rental_rate = 4.99);

#ÖDEV 2

1-)film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız ( BETWEEN - AND yapısını kullanınız.)

SELECT * FROM film WHERE replacement_cost BETWEEN 12.99 AND 16.98; 

2-)actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız. ( IN operatörünü kullanınız.)

SELECT first_name,last_name FROM actor WHERE first_name IN ('Penelope', 'Nick','Ed') ;

3-)film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız. ( IN operatörünü kullanınız.)

SELECT * FROM film WHERE rental_rate IN ('0.99','2.99','4.99') AND replacement_cost IN ('12.99','15.99','28.99'); 

#ÖDEV 3

1)country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.

SELECT country FROM country
WHERE country LIKE 'A%a'

2)country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.
SELECT country FROM country
WHERE country LIKE '_____n';

3)film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.

SELECT title FROM film
WHERE title ILIKE '%T%T%T%T';

4)film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.

SELECT * FROM film
WHERE title LIKE 'C%'AND length > 90 AND rental_rate = 2.99;

#ÖDEV 4

1)film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.

SELECT DISTINCT replacement_cost FROM film;

2)film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?

SELECT COUNT(DISTINCT replacement_cost) FROM film;

3)film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?

SELECT COUNT(*) FROM film 
WHERE title LIKE 'T%' AND rating = 'G';

4)country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?

SELECT COUNT(country) FROM country
WHERE country LIKE '_____';

5)city tablosundaki şehir isimlerinin kaç tanesi 'R' veya r karakteri ile biter?

SELECT COUNT(city) FROM city
WHERE city LIKE 'R%r';


#ödev 5

--1)film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.

SELECT title FROM film
WHERE title LIKE '%n'
ORDER BY length DESC
LIMIT 5;

2)film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi(6,7,8,9,10) sıralayınız.

SELECT * FROM film
WHERE title ILIKE '%N'
ORDER BY length ASC
OFFSET 5LIMIT 5

3)customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.

SELECT * FROM customer
WHERE store_id = '1'
ORDER BY last_name DESC
LIMIT 4;

#ÖDEV 6

1)film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?

SELECT AVG(rental_rate) FROM film;

2)film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?

SELECT COUNT(*) FROM film 
WHERE title LIKE 'C%';

3)film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?

SELECT MAX(length) FROM film 
WHERE rental_rate = 0.99;

4)film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?

SELECT COUNT(DISTINCT(replacement_cost))  FROM film 
WHERE length > 150 ;

#ÖDEV 7
Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

1.film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.
SELECT rating FROM film
GROUP BY rating ;

2.film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.
SELECT replacement_cost , COUNT (*) FROM film
GROUP BY replacement_cost 
HAVING COUNT (*) > 50;

3. customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir? 
SELECT store_id , COUNT(*) FROM customer
GROUP BY store_id ;

4. city tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız.
SELECT country_id,COUNT(*) FROM city
GROUP BY country_id 
ORDER BY COUNT(*) DESC
LIMIT 1;

#ÖDEV 8
1)test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.
CREATE TABLE employer(
	--id INTEGER,
	--name VARCHAR(50),
	--birthday DATE,
	--email VARCHAR(50));

2)Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.
insert into employer (id, name, birthday, email) values (1, 'Gretna', '1980-08-04', 'gbywater0@jiathis.com');
insert into employer (id, name, birthday, email) values (2, 'Haroun', '1987-03-13', 'hhubbucks1@woothemes.com');
insert into employer (id, name, birthday, email) values (3, 'Randolph', '1987-11-14', 'rbearman2@google.it');
insert into employer (id, name, birthday, email) values (4, 'Stafani', '1981-12-19', 'sstapley3@t-online.de');
insert into employer (id, name, birthday, email) values (5, 'Janna', '1990-01-21', 'jolliver4@prnewswire.com');
insert into employer (id, name, birthday, email) values (6, 'Red', '1986-02-18', 'rrottenbury5@nbcnews.com');
insert into employer (id, name, birthday, email) values (7, 'Katinka', '1996-07-22', 'ktsarovic6@live.com');
insert into employer (id, name, birthday, email) values (8, 'Amye', '1987-11-10', 'abrewins7@xinhuanet.com');
insert into employer (id, name, birthday, email) values (9, 'Fey', '1996-05-28', 'fgisby8@usnews.com');
insert into employer (id, name, birthday, email) values (10, 'Marci', '1982-03-26', 'mpinkney9@aboutads.info');
insert into employer (id, name, birthday, email) values (11, 'Kimbell', '1997-07-28', 'klooka@salon.com');
insert into employer (id, name, birthday, email) values (12, 'Carlie', '1986-05-24', 'cpoutressb@wikimedia.org');
insert into employer (id, name, birthday, email) values (13, 'Becka', '1999-04-11', 'bfenbyc@oaic.gov.au');
insert into employer (id, name, birthday, email) values (14, 'Gerladina', '1990-10-01', 'grosendalld@theglobeandmail.com');
insert into employer (id, name, birthday, email) values (15, 'Ev', '1989-11-06', 'emalsere@usatoday.com');
insert into employer (id, name, birthday, email) values (16, 'Dot', '1986-07-05', 'dradagef@hexun.com');
insert into employer (id, name, birthday, email) values (17, 'Helen', '1997-08-02', 'hhaddowg@cornell.edu');
insert into employer (id, name, birthday, email) values (18, 'Leila', '1997-04-27', 'lkinvigh@e-recht24.de');
insert into employer (id, name, birthday, email) values (19, 'Holly', '1996-07-15', 'hklimentyonoki@google.es');
insert into employer (id, name, birthday, email) values (20, 'Palm', '1987-05-24', 'pmacdearmontj@deliciousdays.com');
insert into employer (id, name, birthday, email) values (21, 'Ag', '1984-08-22', 'areecek@nasa.gov');
insert into employer (id, name, birthday, email) values (22, 'Hogan', '1986-04-06', 'hcallaghanl@devhub.com');
insert into employer (id, name, birthday, email) values (23, 'Jarrid', '1987-04-03', 'jnesbym@imageshack.us');
insert into employer (id, name, birthday, email) values (24, 'Packston', '1995-11-04', 'pkenlinn@miibeian.gov.cn');
insert into employer (id, name, birthday, email) values (25, 'Solomon', '1985-03-25', 'swetherso@wisc.edu');
insert into employer (id, name, birthday, email) values (26, 'Mile', '1987-03-23', 'mgrinaughp@tinypic.com');
insert into employer (id, name, birthday, email) values (27, 'Bendite', '1990-06-01', 'bgodarq@webeden.co.uk');
insert into employer (id, name, birthday, email) values (28, 'Alvera', '1991-08-09', 'asimoncellir@bing.com');
insert into employer (id, name, birthday, email) values (29, 'Brana', '1987-03-21', 'btungays@multiply.com');
insert into employer (id, name, birthday, email) values (30, 'Simona', '1980-09-30', 'sdachst@trellian.com');
insert into employer (id, name, birthday, email) values (31, 'Camila', '1999-03-18', 'cbrittoneru@angelfire.com');
insert into employer (id, name, birthday, email) values (32, 'Oswell', '1994-10-25', 'ocorsarv@technorati.com');
insert into employer (id, name, birthday, email) values (33, 'Leodora', '1985-11-14', 'lcharrierw@homestead.com');
insert into employer (id, name, birthday, email) values (34, 'Carmen', '1988-06-04', 'craineyx@bluehost.com');
insert into employer (id, name, birthday, email) values (35, 'Athena', '1983-02-27', 'ashally@businessinsider.com');
insert into employer (id, name, birthday, email) values (36, 'Pren', '2000-05-16', 'pivanisovz@yale.edu');
insert into employer (id, name, birthday, email) values (37, 'Angelina', '1995-04-18', 'atomaszewicz10@toplist.cz');
insert into employer (id, name, birthday, email) values (38, 'Nikita', '1982-08-23', 'ntax11@gnu.org');
insert into employer (id, name, birthday, email) values (39, 'Bevan', '1999-05-18', 'bpablo12@mysql.com');
insert into employer (id, name, birthday, email) values (40, 'Alma', '1988-07-12', 'adaveren13@stanford.edu');
insert into employer (id, name, birthday, email) values (41, 'Guinna', '1998-10-02', 'gzorer14@cafepress.com');
insert into employer (id, name, birthday, email) values (42, 'Guillema', '1999-03-08', 'ggland15@boston.com');
insert into employer (id, name, birthday, email) values (43, 'Evangeline', '1980-11-17', 'escotchbourouge16@squidoo.com');
insert into employer (id, name, birthday, email) values (44, 'Colver', '1989-12-19', 'cdouse17@google.de');
insert into employer (id, name, birthday, email) values (45, 'Reeba', '1989-06-30', 'rduchart18@ucoz.ru');
insert into employer (id, name, birthday, email) values (46, 'Lynette', '1985-01-09', 'lredier19@wikipedia.org');
insert into employer (id, name, birthday, email) values (47, 'Kaleb', '1993-07-25', 'kduxbury1a@webs.com');
insert into employer (id, name, birthday, email) values (48, 'Conrad', '1987-08-10', 'ckenningham1b@unblog.fr');
insert into employer (id, name, birthday, email) values (49, 'Aguie', '1985-09-11', 'abrittoner1c@nsw.gov.au');
insert into employer (id, name, birthday, email) values (50, 'Derril', '1995-05-07', 'dmaslen1d@seesaa.net');

3)Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.

UPDATE employer
SET name = 'Merve'
WHERE id = 10;

UPDATE employer
SET	email = 'merve@gmaiil.com'
WHERE id = 10;

UPDATE employer
SET name = 'Serdar Ortaç',
	birthday = '01.01.1980',
	email = 'serdar@gmail.com'
WHERE id = 1;

UPDATE employer
SET birthday = '22.06.1993'
WHERE id = 8 ;

UPDATE employer
SET name = 'Kıvanç'
WHERE id = 20;

4)Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.
DELETE from employer
WHERE id = 15;

DELETE from employer
WHERE name = 'Fey';


DELETE from employer
WHERE name = 'Dot';

DELETE from employer
WHERE id = 50;

DELETE from employer
WHERE email = 'cdouse17@google.de';

#ÖDEV 9
Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

city tablosu ile country tablosunda bulunan şehir (city) ve ülke (country) isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.

SELECT <sütun_adı>, <sütun_adı> ...
FROM city
INNER JOIN country
ON <city>.<sütun_adı> = <tablo2_adı>.<sütun_adı>;
customer tablosu ile payment tablosunda bulunan payment_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.

customer tablosu ile rental tablosunda bulunan rental_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.

