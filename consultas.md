# 📊 Consultas de Negócio para Banco de Dados de Oficina

### ❓ Pergunta de Negócio 1: Quantos carros cada equipe cuidou?
```sql
SELECT COUNT(s.idvehicle) AS qtde_veiculos, t.idTeam 
FROM serviceorders s, teams t  
WHERE s.idTeam = t.idTeam
GROUP BY idteam;

Resultado:

| qtde_veiculos | idTeam |
|---------------|--------|
| 6             | 1      |
| 4             | 2      |
| 5             | 3      |


```
### ❓ Pergunta de Negócio 2: Quais clientes trouxeram algum carro mais de uma vez?
```sql
SELECT c.name, COUNT(v.idVehicle) AS qtde_veiculo
FROM vehicles v, clients c 
WHERE c.idClient = v.idClient	
GROUP BY c.Name
HAVING COUNT(v.idVehicle) > 1;

Resultado:

| name           | qtde_veiculo |
|----------------|--------------|
|Alice Ferreira  | 1            |
|Fernanda Souza  | 2            |
|Mariana Rocha   | 3            |


```
### ❓ Pergunta de Negócio 3: Qual valor das notas nos primeiros 15 dias de janeiro?
```sql
SELECT SUM(totalvalue) AS total, COALESCE(IssueDate, '0') AS date
FROM serviceorders  
WHERE (IssueDate BETWEEN "2025-01-01" AND "2025-01-15")
GROUP BY IssueDate;

Resultado:

| total      | date       |
|------------|------------|
| 2300.00    | 2025-01-01 |
| 0.00       | 2025-01-03 |
| 1200.00    | 2025-01-07 |
| 500.00     | 2025-01-10 |
| 700.00     | 2025-01-15 |
```
### 📈 Pergunta de Negócio 4: Qual a média móvel de 7 dias?
```sql
WITH tbl_patrick (total, date) AS (
    SELECT SUM(totalvalue) AS total, IssueDate AS date
    FROM serviceorders  
    GROUP BY IssueDate
)
SELECT total, date, ROUND(AVG(total)
    OVER (ORDER BY date
    ROWS BETWEEN 6 PRECEDING AND CURRENT ROW), 2) AS moving_average
FROM tbl_patrick  
ORDER BY Date;

Resultado:

| Total      | Date       | Moving Average   |
|------------|------------|------------------|
| 2300.00    | 2025-01-01 | 2300.00          |
| 0.00       | 2025-01-03 | 1150.00          |
| 1200.00    | 2025-01-07 | 1166.67          |
| 500.00     | 2025-01-10 | 1000.00          |
| 700.00     | 2025-01-15 | 940.00           |
| 2550.00    | 2025-01-17 | 1208.33          |
| 400.00     | 2025-01-20 | 1092.86          |
| 1800.00    | 2025-01-22 | 1021.43          |
| 2500.00    | 2025-01-23 | 1378.57          |
| 1900.00    | 2025-01-24 | 1478.57          |
| 400.00     | 2025-01-25 | 1464.29          |
| 550.00     | 2025-01-27 | 1442.86          |

```
### 📈 Pergunta de Negócio 5: Qual a média móvel de 30 dias?
```sql
WITH tbl_patrick (total, date) AS (
    SELECT SUM(totalvalue) AS total, IssueDate AS date
    FROM serviceorders  
    GROUP BY IssueDate
)
SELECT total, date, ROUND(AVG(total)
    OVER (ORDER BY date
    ROWS BETWEEN 29 PRECEDING AND CURRENT ROW), 2) AS moving_average
FROM tbl_patrick  
ORDER BY Date;

Resultado:

| Total      | Date       | Moving Average    |
|------------|------------|-------------------|
| 2300.00    | 2025-01-01 | 2300.00           |
| 0.00       | 2025-01-03 | 1150.00           |
| 1200.00    | 2025-01-07 | 1166.67           |
| 500.00     | 2025-01-10 | 1000.00           |
| 700.00     | 2025-01-15 | 940.00            |
| 2550.00    | 2025-01-17 | 1208.33           |
| 400.00     | 2025-01-20 | 1092.86           |
| 1800.00    | 2025-01-22 | 1181.25           |
| 2500.00    | 2025-01-23 | 1327.78           |
| 1900.00    | 2025-01-24 | 1385.00           |
| 400.00     | 2025-01-25 | 1295.45           |
| 550.00     | 2025-01-27 | 1233.33           |
