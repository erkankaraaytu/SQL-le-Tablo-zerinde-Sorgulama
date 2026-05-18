1. Satış yapılan müşterilerin isimlerini listelemek için gerekli SQL ifadesini yazınız.
SELECT DISTINCT m.Madi, m.Msoyadi
FROM Müşteri m
INNER JOIN Satış s ON m.Mno = s.Mno;

2. Hangi müşteriden hangi aracın alındığını listelemek için gerekli SQL ifadesini yazınız.
SELECT m.Madi, m.Msoyadi, a.Marka, a.Model
FROM Müşteri m
INNER JOIN Alım al ON m.Mno = al.Mno
INNER JOIN Araç a ON al.Aracno = a.Aracno;

3. Her bir müşteriden alınan araçların sayısını listelemek için gerekli SQL ifadesini yazınız.
SELECT m.Madi, m.Msoyadi, COUNT(al.Aracno) AS AlinanAracSayisi
FROM Müşteri m
INNER JOIN Alım al ON m.Mno = al.Mno
GROUP BY m.Mno, m.Madi, m.Msoyadi;

4. Satılan araçların marka ve modelini bulmak için gerekli SQL ifadesini yazınız.
SELECT DISTINCT a.Marka, a.Model
FROM Araç a
INNER JOIN Satış s ON a.Aracno = s.Aracno;

5. Toplam satış ve toplam alım tutarlarını ve bunların farkını bulmak için gerekli SQL
ifadesini yazınız.
SELECT
(SELECT SUM(Sfiyat) FROM Satış) AS ToplamSatis,
(SELECT SUM(Afiyat) FROM Alım) AS ToplamAlim,
((SELECT SUM(Sfiyat) FROM Satış) - (SELECT SUM(Afiyat) FROM Alım)) AS
Fark;

6. Hiç satışı yapılmamış araçları listelemek için gerekli SQL ifadesini yazınız.
SELECT *
FROM Araç
WHERE Aracno NOT IN (SELECT Aracno FROM Satış);

7. Her aracın ortalama satış tutarını bulmak için gerekli SQL ifadesini yazınız.
SELECT a.Marka, a.Model, AVG(s.Sfiyat) AS OrtalamaSatisTutari
FROM Araç a
INNER JOIN Satış s ON a.Aracno = s.Aracno
GROUP BY a.Aracno, a.Marka, a.Model;

8. Alımı ve satışı yapılan tüm araçların marka, model ve alım-satış sayısını listelemek için
gerekli SQL ifadesiniz yazınız.
SELECT a.Marka, a.Model,
(SELECT COUNT(*) FROM Alım WHERE Aracno = a.Aracno) AS AlimSayisi,
(SELECT COUNT(*) FROM Satış WHERE Aracno = a.Aracno) AS SatisSayisi
FROM Araç a
WHERE a.Aracno IN (SELECT Aracno FROM Alım)
AND a.Aracno IN (SELECT Aracno FROM Satış);

9. 20000'den fazla tutara satılan araçları kimlerin hangi aracı aldığını bulmak için gerekli
SQL ifadesini yazınız.
SELECT m.Madi, m.Msoyadi, a.Marka, a.Model, s.Sfiyat
FROM Satış s
INNER JOIN Müşteri m ON s.Mno = m.Mno
INNER JOIN Araç a ON s.Aracno = a.Aracno
WHERE s.Sfiyat > 20000;

10. Tokat'ta bulunan müşterilere satışı yapılan araçları listelemek için gerekli SQL ifadesini
yazınız.
SELECT m.Madi, m.Msoyadi, a.Marka, a.Model
FROM Müşteri m
INNER JOIN Satış s ON m.Mno = s.Mno
INNER JOIN Araç a ON s.Aracno = a.Aracno
WHERE m.Madres LIKE '%Tokat%';
