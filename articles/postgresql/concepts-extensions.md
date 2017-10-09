---
title: rozszerzenia PostgreSQL aaaUsing w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft
description: "W tym artykule opisano hello możliwości tooextend hello funkcji bazy danych dla PostgreSQL przy użyciu rozszerzeń w bazie danych Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Rozszerzenia PostgreSQL w bazie danych PostgreSQL Azure
PostgreSQL zapewnia hello możliwości tooextend hello funkcji bazy danych przy użyciu rozszerzeń. Rozszerzenia umożliwiają wielu powiązanych toobe obiektów SQL powiązane ze sobą w jednym pakiecie i może być załadowany lub usunięte z bazy danych za pomocą jednego polecenia. Po załadowaniu do bazy danych hello rozszerzenia może działać podobnie jak funkcje, które są wbudowane w. Aby uzyskać więcej informacji o rozszerzeniach PostgreSQL, zobacz [pakowania obiektów pokrewnych do rozszerzenia](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-toouse-postgresql-extensions"></a>Jak toouse PostgreSQL rozszerzenia?
Rozszerzenia PostgreSQL wymagają toobe zainstalowane dla bazy danych przed ich użyciem. tooinstall określonego rozszerzenia, uruchom [Tworzenie rozszerzenia](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) polecenie z tooload narzędzie psql hello spakowanych obiektów do bazy danych.

Bazy danych platformy Azure dla PostgreSQL obsługuje klucza rozszerzeń wymienionych w tym miejscu. Inne rozszerzenia poza hello wymienione, nie są obsługiwane. Nie można utworzyć własne rozszerzenie z bazą danych Azure, PostgreSQL usługi.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Rozszerzenia dla PostgreSQL przez bazę danych Azure
Witaj poniższych tabelach listy hello standardowe PostgreSQL rozszerzeń, które są obecnie obsługiwane przez bazę danych Azure dla PostgreSQL. Możesz również uzyskać te informacje, badając pg\_dostępne\_rozszerzenia. 

### <a name="data-types-extensions"></a>Rozszerzenia typów danych

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Miejsce na wpisanie ciągu znaków bez uwzględniania wielkości liter |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Zawiera typ danych do przechowywania zestawy par klucz/wartość |

### <a name="functions-extensions"></a>Funkcje rozszerzeń

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Zawiera kilka funkcji toodetermine podobieństwa i odległość między ciągami. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Udostępnia funkcje i operatory do manipulowania bez null tablice liczb całkowitych. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Udostępnia funkcje kryptograficzne |
| [PG\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Zarządza partycjonowane tabele według czasu lub identyfikator |
| [PG\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Udostępnia funkcje i operatory określania hello podobieństwa alfanumeryczne w oparciu o dopasowanie trigram |
| [Identyfikator UUID ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Generowanie powszechnie unikatowe identyfikatory (UUID) |

### <a name="full-text-search-extensions"></a>Rozszerzenia wyszukiwania pełnotekstowego

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Słownik wyszukiwania tekstu, która usuwa akcentów (znaków diakrytycznych) z lexemes. |

### <a name="index-types-extensions"></a>Rozszerzenia typu indeksu

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [BTree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Udostępnia przykładowy GIN operator klasy, które implementuje B-drzewa, takich jak zachowanie dla określonych typów danych. |
| [BTree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Udostępnia klasy operatora indeksu GiST, które implementuje B-drzewa. |

### <a name="language-extensions"></a>Rozszerzenia językowe

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | PL/pgSQL obciążana procedurach języka |

### <a name="miscellaneous-extensions"></a>Różne rozszerzenia

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [PG\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Zapewnia to badania, co dzieje się w pamięci podręcznej buforu hello udostępniane w czasie rzeczywistym. |
| [PG\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Zapewnia sposób tooload relacji danych do hello buforów w pamięci podręcznej. |
| [PG\_stat\_— instrukcje](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Zapewnia możliwość śledzenia statystyki wykonania wszystkich instrukcji SQL wykonane przez serwer. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Tooaccess danych przechowywanych w zewnętrznych serwerów PostgreSQL używane otoki obcy danych |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Rozszerzenia** | **Opis** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topologii, postgis\_tiger\_geocoder, postgis\_sfcgal | Przestrzenne i geograficzne obiekty PostgreSQL. |
| adres\_standardizer, adres\_standardizer\_danych\_nam | Adres na elementy składowe tooparse używane. Używane toosupport geokodowanie adres normalizacji kroku. |
| [pgrouting](http://pgrouting.org/) | Rozszerza hello PostGIS / PostgreSQL geograficzne bazy danych funkcji routingu tooprovide dane geograficzne. |

## <a name="next-steps"></a>Następne kroki
Nie widzisz rozszerzenia, które chcesz toouse? Prosimy o kontakt. Zagłosuj na istniejących żądań lub utworzyć nowy opinii i oczekiwania w naszym [forum opinii klientów](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
