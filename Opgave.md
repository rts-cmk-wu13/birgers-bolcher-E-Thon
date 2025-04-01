# Birgers Bolcher
### En SQL og database øvelse til Nodejs
Birger fik en bog om bolcher til sin fødselsdag da han blev 14 år. Siden har han eksperimenteret med fremstilling af mange forskellige bolcher og han har flittigt delt smagsprøver ud til sin familie og venner.

Nu er efterspørgslen blevet så stor, at han vil starte en egentlig produktion.  Birger har foreløbig otte forskellige bolchetyper han vil producere og han har lavet en tabel med navne, farver, smag osv. til sine bolcher.
Birger har ambitioner, så han vil have en webside med sine bolcher.

Det er her du kommer ind i billedet. Du får til opgave at sætte en database op og lave en række forskellige udtræk til visning i konsollen i første omgang - senere på en simpel webside.
Database skal være en MySQL database og udtrækket skal foregå via nodejs.


> Da det hele nu er en øvelse hvor du skal lære og træne SQL, sætte en database op og connecte via nodejs, så er det vigtigt at du løser opgaven slavisk og selvstændigt.
**Det handler ikke om at få løsningen**, for så er det ikke længere en øvelse - men du skal selv finde løsningen ved at læse og prøve dig frem – heri opstår læring som er målet med opgaven.


W3Schools er en rigtig god reference til det du søger i <a href="https://www.w3schools.com/sql" target="_blank">SQL</a>


Forklaring følger også i undervisningen

## Øvelse 1
1.1	Opret en database kaldet birgers_bolcher med én tabel kaldet bolche

*Se Tabeldata.pdf*

1.2	Tabellen skal indeholde de viste felter og data – du bestemmer både feltnavne og datatyper

 ![Birgers Bolcher](./assets/birgers.png)
 *Se Tabeldata.pdf*

## Øvelse 2
Skriv en sql sætning for hver af følgende

2.1	Udskriv alle informationer om alle bolcher.
```SQL
SELECT * FROM Candy
```


2.2	Find og udskriv navnene på alle de røde bolcher.
```SQL
SELECT name FROM Candy
WHERE color="Red"
```


2.3	Find og udskriv navnene på alle de røde og de blå bolcher, i samme SQL udtræk.
```SQL
SELECT name FROM Candy 
WHERE color="Red" OR color="Blue"
```


2.4	Find og udskriv navnene på alle bolcher, der ikke er røde, sorteret alfabetisk.
```SQL
SELECT name FROM Candy 
WHERE NOT color="Red"
ORDER BY name
```


2.5	Find og udskriv navnene på alle bolcher som starter med et “B”.
```SQL
SELECT name FROM Candy
WHERE name LIKE 'B%';
```


2.6	Find og udskriv navene på alle bolcher, hvor der i navnet findes mindst ét “e”.
```SQL
SELECT name FROM Candy 
WHERE name LIKE '%e%';
```


2.7	Find og udskriv navn og vægt på alle bolcher der vejer mindre end 10 gram, sorter stigende efter vægt.
```SQL
SELECT name, weight FROM Candy 
WHERE weight < 10
ORDER BY weight ASC;
```


2.8	Find og udskriv navne på alle bolcher, der vejer mellem 10 og 12 gram (begge tal inklusiv), sorteret alfabetisk og derefter vægt.
```SQL
SELECT name FROM Candy 
WHERE weight >= 10 AND weight <= 12
ORDER BY name,weight;
```

eller 
```SQL
SELECT name FROM Candy 
WHERE weight BETWEEN 10 AND 12
ORDER BY name,weight;
```

2.9	Find og udskriv de tre største (tungeste) bolcher.
```SQL
SELECT * FROM Candy 
ORDER BY weight DESC
LIMIT 3
```

2.10 Udskriv alle informationer om et tilfældigt bolche, udvalgt af systemet (sql).
```SQL
SELECT * FROM Candy ORDER BY RANDOM() LIMIT 1
```

## Øvelse 3
3.1	Normaliser tabellen Bolcher så der dannes ”domænetabeller” til de felter hvor flere bolcher ofte har samme værdi.
> Følgende domænetabeller er lavet:
> - Acidity
> - Strength

> Extra:
> - Color
> - Taste

> Extra extra: 
> - Weight

*Se Tabeldata.pdf*

## Øvelse 4

4.1	Gentag øvelse 2, men nu med inner joins

4.1.1	Udskriv alle informationer om alle bolcher.
```SQL
SELECT Candy.id, Candy.name, Color.name AS color, Weight.name AS weight, Acidity.name AS acidity, Strength.name AS strength, Taste.name AS taste, Candy.commodity_price
FROM Candy
INNER JOIN Color ON Candy.color_id=Color.id
INNER JOIN Weight ON Candy.weight_id=Weight.id
INNER JOIN Acidity ON Candy.acidity_id=Acidity.id
INNER JOIN Strength ON Candy.strength_id=Strength.id
INNER JOIN Taste ON Candy.taste_id=Taste.id
```


4.1.2	Find og udskriv navnene på alle de røde bolcher.
```SQL
SELECT Candy.name FROM Candy
INNER JOIN Color ON Candy.color_id=Color.id
WHERE Color.name="Red"
```


4.1.3	Find og udskriv navnene på alle de røde og de blå bolcher, i samme SQL udtræk.
```SQL
SELECT Candy.name FROM Candy
INNER JOIN Color ON Candy.color_id=Color.id
WHERE Color.name="Red" OR Color.name="Blue"
```


4.1.4	Find og udskriv navnene på alle bolcher, der ikke er røde, sorteret alfabetisk.
```SQL
SELECT Candy.name FROM Candy
INNER JOIN Color ON Candy.color_id=Color.id
WHERE NOT Color.name="Red"
ORDER BY Candy.name
```


4.1.5	Find og udskriv navnene på alle bolcher som starter med et “B”.
```SQL
SELECT Candy.name FROM Candy
WHERE Candy.name LIKE 'B%'
```


4.1.6	Find og udskriv navene på alle bolcher, hvor der i navnet findes mindst ét “e”.
```SQL
SELECT Candy.name FROM Candy 
WHERE Candy.name LIKE '%e%'
```


4.1.7	Find og udskriv navn og vægt på alle bolcher der vejer mindre end 10 gram, sorter stigende efter vægt.
```SQL
SELECT Candy.name, Weight.name AS weight FROM Candy
INNER JOIN Weight ON Candy.weight_id=Weight.id
WHERE Weight.name < 10
ORDER BY Weight.name
```


4.1.8	Find og udskriv navne på alle bolcher, der vejer mellem 10 og 12 gram (begge tal inklusiv), sorteret alfabetisk og derefter vægt.
```SQL
SELECT Candy.name AS name FROM Candy
INNER JOIN Weight ON Candy.weight_id=Weight.id
WHERE Weight.name BETWEEN 10 AND 12
ORDER BY Weight.name
```


4.1.9	Find og udskriv de tre største (tungeste) bolcher.
```SQL
SELECT Candy.id, Candy.name, Color.name AS color, Weight.name AS weight, Acidity.name AS acidity, Strength.name AS strength, Taste.name AS taste, Candy.commodity_price
FROM Candy
INNER JOIN Color ON Candy.color_id=Color.id
INNER JOIN Weight ON Candy.weight_id=Weight.id
INNER JOIN Acidity ON Candy.acidity_id=Acidity.id
INNER JOIN Strength ON Candy.strength_id=Strength.id
INNER JOIN Taste ON Candy.taste_id=Taste.id
ORDER BY Weight.name DESC
LIMIT 3
```

4.1.10 Udskriv alle informationer om et tilfældigt bolche, udvalgt af systemet (sql).
```SQL
SELECT Candy.id, Candy.name, Color.name AS color, Weight.name AS weight, Acidity.name AS acidity, Strength.name AS strength, Taste.name AS taste, Candy.commodity_price
FROM Candy
INNER JOIN Color ON Candy.color_id=Color.id
INNER JOIN Weight ON Candy.weight_id=Weight.id
INNER JOIN Acidity ON Candy.acidity_id=Acidity.id
INNER JOIN Strength ON Candy.strength_id=Strength.id
INNER JOIN Taste ON Candy.taste_id=Taste.id
ORDER BY RANDOM()
LIMIT 1
```

## Øvelse 5
Nettopris for et bolche er råvareprisen plus 250 % (begge uden moms) 

5.1	Udskriv en prisliste med bolchenavn og kilopris henholdsvis med og uden moms
```SQL
SELECT 
    Candy.name, 
    ROUND(((Candy.commodity_price/Weight.name*1000)+((Candy.commodity_price/Weight.name*1000)/100*250)),2) AS netto_price_no_VAT, 
    ROUND((((Candy.commodity_price/Weight.name*1000)+((Candy.commodity_price/Weight.name*1000)/100*250))*1.25),2) AS price_incl_VAT
FROM Candy
INNER JOIN Weight ON Candy.weight_id=Weight.id
```

## Øvelse 6
6.3	Udskriv hvor mange bolscher der vejer under 15 g.
```SQL
SELECT COUNT(*) FROM Candy
INNER JOIN Weight ON Candy.weight_id=Weight.id
WHERE Weight.name < 15
```

6.4	Udskriv hvor mange forskellige forskellige bolcher der er i tabellen
```SQL
SELECT COUNT(*) FROM Candy
```

6.5	Udskriv gennemsnitsprisen per bolche
```SQL
SELECT AVG(Candy.commodity_price) FROM Candy
```

6.6	Udskriv navn og pris på det dyreste og billigste bolche
```SQL
SELECT Candy.name, min(Candy.commodity_price) AS commodity_price FROM Candy
UNION SELECT Candy.name, max(Candy.commodity_price) FROM Candy
```
