<!--
Used in:
sql-database-performance-guidance.md  
sql-database-resource-limits.md
sql-database-service-tiers.md  
-->

### <a name="basic-service-tier"></a>Warstwa Podstawowa usług
| **Poziom wydajności** | **Podstawowa** |
| --- | :---: |
| Maksymalna liczba jednostek DTU | 5 |
| Maksymalny rozmiar bazy danych* |2 GB|
| Maksymalna pojemność magazynu OLTP w pamięci |Nie dotyczy |
| Maksymalna liczba równoczesnych procesów roboczych (liczba żądań) |30 |
| Maksymalna liczba współbieżnych logowań |30 |
| Maksymalna liczba współbieżnych sesji |300 |
|||

### <a name="standard-service-tier"></a>Warstwa Standardowa usług
| **Poziom wydajności** | **S0** | **S1** | **S2** | **S3** |
| --- |---:| ---:|---:|---:|---:|
| Maksymalna liczba jednostek DTU | 10 | 20 | 50 | 100 |
| Maksymalny rozmiar bazy danych* | 250 GB| 250 GB | 250 GB | 250 GB |
| Maksymalna pojemność magazynu OLTP w pamięci | Nie dotyczy | Nie dotyczy | Nie dotyczy | Nie dotyczy |
| Maksymalna liczba równoczesnych procesów roboczych (liczba żądań)| 60 | 90 | 120 | 200 |
| Maksymalna liczba współbieżnych logowań | 60 | 90 | 120 | 200 |
| Maksymalna liczba współbieżnych sesji |600 | 900 | 1200 | 2400 |
||||||

### <a name="premium-service-tier"></a>Warstwa Premium usług 
| **Poziom wydajności** | **P1** | **P2** | **P4** | **P6** | **P11** | **P15** | 
| --- |---:|---:|---:|---:|---:|---:|
| Maksymalna liczba jednostek DTU | 125 | 250 | 500 | 1000 | 1750 | 4000 |
| Maksymalny rozmiar bazy danych* | 500 GB | 500 GB | 500 GB | 500 GB | 4 TB | 4 TB |
| Maksymalna pojemność magazynu OLTP w pamięci | 1 GB | 2 GB | 4 GB | 8 GB | 14 GB | 32 GB |
| Maksymalna liczba równoczesnych procesów roboczych (liczba żądań)| 200 | 400 | 800 | 1600 | 2400 | 6400 |
| Maksymalna liczba współbieżnych logowań | 200 | 400| 800| 1600| 2400| 6400 |
| Maksymalna liczba współbieżnych sesji | 30000| 30000| 30000| 30000| 30000| 30000 |
|||||||

### <a name="premium-rs-service-tier"></a>Warstwy usług RS — wersja Premium 
| **Poziom wydajności** | **PRS1** | **PRS2** | **PRS4** | **PRS6** |
| --- |---:|---:|---:|---:|---:|---:|
| Maksymalna liczba jednostek DTU | 125 | 250 | 500 | 1000 |
| Maksymalny rozmiar bazy danych* | 500 GB | 500 GB | 500 GB | 500 GB |
| Maksymalna pojemność magazynu OLTP w pamięci | 1 GB | 2 GB | 4 GB | 8 GB |
| Maksymalna liczba równoczesnych procesów roboczych (liczba żądań)| 200 | 400 | 800 | 1600 |
| Maksymalna liczba współbieżnych logowań | 200 | 400| 800| 1600|
| Maksymalna liczba współbieżnych sesji | 30000| 30000| 30000| 30000|
|||||||

\* Maksymalny rozmiar bazy danych oznacza maksymalny rozmiar danych w bazie danych. 