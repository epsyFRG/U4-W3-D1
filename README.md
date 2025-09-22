<!-- Dati -->

INSERT INTO clienti (numero_cliente, nome, cognome, anno_di_nascita, regione_residenza)
VALUES
(1, 'Emiliano', 'Massari', 2003, 'Lazio'),
(2, 'Mario', 'Rossi', 1999, 'Lombardia'),
(3, 'Giovanna', 'Olivieri', 1982, 'Sardegna'),
(4, 'Luigi', 'Verdi', 1982, 'Sicilia');

INSERT INTO prodotti (descrizione, in_produzione, in_commercio, data_attivazione, data_disattivazione)
VALUES
('Computer', TRUE, FALSE, '2017-05-10', NULL),
('Telefono', FALSE, TRUE, '2018-03-15', NULL);

INSERT INTO fornitori (numero_fornitore, denominazione, regione_residenza)
VALUES
(1, 'AFK Store Srl', 'Lazio'),
(2, 'Andrea Galeazzi Spa', 'Lombardia');

INSERT INTO fatture (numero_fattura, tipologia, importo, iva, id_cliente, data_fattura, numero_fornitore)
VALUES
(1, 'Elettronica', 500.00, 20, 1, '2020-04-15', 1),
(2, 'Software', 1500.00, 22, 2, '2021-06-10', 2),
(3, 'Accessori', 800.00, 20, 1, '2021-09-20', 1);

<!-- Query -->

SELECT \* FROM clienti WHERE nome = 'Mario';

SELECT nome, cognome FROM clienti WHERE anno_di_nascita = 1982;

SELECT numero_fattura FROM fatture WHERE iva = 20;

SELECT \* FROM prodotti WHERE EXTRACT(YEAR FROM data_attivazione) = 2017 AND (in_produzione = TRUE OR in_commercio = TRUE);

SELECT f.numero_fattura, f.importo, f.iva, f.data_fattura, c.numero_cliente, c.nome, c.cognome, c.regione_residenza FROM fatture f JOIN clienti c ON f.id_cliente = c.numero_cliente WHERE f.importo < 1000;

SELECT f.numero_fattura, f.importo, f.iva, f.data_fattura, fo.denominazione AS nome_fornitore FROM fatture f JOIN fornitori fo ON f.numero_fornitore = fo.numero_fornitore;

SELECT EXTRACT(YEAR FROM data_fattura) AS anno, COUNT(\*) AS numero_fatture FROM fatture WHERE iva = 20 GROUP BY anno ORDER BY anno;

SELECT EXTRACT(YEAR FROM data_fattura) AS anno, COUNT(\*) AS numero_fatture, SUM(importo) AS somma_importi FROM fatture GROUP BY anno ORDER BY anno;
