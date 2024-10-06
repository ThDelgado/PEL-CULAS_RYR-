CREATE TABLE peliculas(
id_pelicula SERIAL PRIMARY KEY,
pelicula VARCHAR(500) NOT NULL,
estreno  INTEGER NOT NULL,
director VARCHAR(300) NOT NULL
);

CREATE TABLE reparto(
id_reparto SERIAL PRIMARY KEY,
id_pelicula INTEGER NOT NULL,
actor VARCHAR(300) NOT NULL, 
FOREIGN KEY (id_pelicula) REFERENCES peliculas(id_pelicula)
);



SELECT * FROM peliculas;
SELECT * FROM reparto;

--Listar todos los actores que aparecen en la película "Titanic", indicando el título de la película, año de estreno, director y todo el reparto. 
SELECT p.pelicula, p.estreno, p.director, r.actor
FROM peliculas p
JOIN reparto r ON p.id_pelicula = r.id_pelicula
WHERE p.pelicula = 'Titanic';

--Listar los 10 directores más populares, indicando su nombre y cuántas películas aparecen en el top 100.   
SELECT * FROM  peliculas;

SELECT director,  COUNT(id_pelicula) AS popular FROM peliculas
WHERE id_pelicula IN(SELECT id_pelicula FROM peliculas ORDER BY id_pelicula LIMIT 100)
GROUP BY director
ORDER BY popular DESC
LIMIT 10;


--Indicar cuántos actores distintos hay. 
SELECT * FROM reparto;

SELECT COUNT(DISTINCT actor) AS num_actores_distintos  FROM reparto; 


--Indicar las películas estrenadas entre los años 1990 y 1999 (ambos incluidos), ordenadas por título de manera ascendente.  
SELECT * FROM peliculas;
SELECT pelicula, estreno  FROM peliculas 
WHERE estreno BETWEEN 1990 AND 1999 
ORDER BY pelicula ASC; 

--Listar los actores de la película más nueva.  
SELECT * FROM reparto;
SELECT * FROM peliculas;

SELECT r.actor FROM reparto r 
JOIN peliculas p ON r.id_pelicula = p.id_pelicula 
WHERE p.estreno = (SELECT MAX(estreno) FROM peliculas); 

--Inserte los datos de una nueva película solo en memoria, y otra película en el disco duro.  
  
BEGIN;
INSERT INTO peliculas ( pelicula,estreno, director) VALUES ('Nueva Película', 2024, 'Nuevo Director'); 

ROLLBACK; 


BEGIN;
INSERT INTO peliculas ( pelicula,estreno, director) VALUES ('Nueva Película', 2024, 'Nuevo Director'); 

COMMIT; 


--actualice 5 directores utilizando ROLLBACK.  

BEGIN; 

UPDATE peliculas SET director = 'Nuevo Director 1' WHERE id_pelicula =1; 
UPDATE peliculas SET director = 'Nuevo Director 2' WHERE id_pelicula =2; 
UPDATE peliculas SET director = 'Nuevo Director 3' WHERE id_pelicula =3; 
UPDATE peliculas SET director = 'Nuevo Director 4' WHERE id_pelicula =4; 
UPDATE peliculas SET director = 'Nuevo Director 5' WHERE id_pelicula =5; 
  

ROLLBACK;


--Inserte 3 actores a la película “Rambo” utilizando SAVEPOINT  

BEGIN;
SAVEPOINT sp1;
INSERT INTO reparto(id_pelicula,actor)VALUES
((SELECT id_pelicula FROM peliculas WHERE pelicula = 'Rambo'), 'Actor 1'),
((SELECT id_pelicula FROM peliculas WHERE pelicula = 'Rambo'), 'Actor 2'),
((SELECT id_pelicula FROM peliculas WHERE pelicula = 'Rambo'), 'Actor 3');
ROLLBACK;

--Inserte 2 actores para cada película estrenada el 2001.  
BEGIN;

INSERT INTO reparto (id_pelicula, actor) VALUES
((SELECT id_pelicula FROM peliculas WHERE estreno = 2001 LIMIT 1),'Actor 1'),
((SELECT id_pelicula FROM peliculas WHERE estreno = 2001 LIMIT 1), 'Actor 2');

ROLLBACK;


--Inserte 2 actores para cada película estrenada el 2001.  


BEGIN;

UPDATE peliculas SET pelicula = 'Donkey Kong' WHERE pelicula = 'king Kong';

ROLLBACK;




