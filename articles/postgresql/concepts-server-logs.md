---
title: aaaServer w dziennikach w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft
description: "Generuje dziennikami błędów i kwerendy w bazie danych Azure dla PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Dzienników serwera w bazie danych Azure PostgreSQL 
Bazy danych platformy Azure dla PostgreSQL generuje zapytań i błąd dzienników. Dzienniki tootransaction dostępu nie jest obsługiwane. Te dzienniki mogą być używane tooidentify, rozwiązywanie problemów z i naprawić błędy konfiguracji i podrzędna optymalnej wydajności. Aby uzyskać więcej informacji, zobacz [raportowanie błędów i rejestrowanie](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Dzienniki serwera dostępu
Można wyświetlić listę i Pobierz dzienniki błędów serwera Azure PostgreSQL przy użyciu hello portalu Azure, [interfejsu wiersza polecenia Azure](howto-configure-server-logs-using-cli.md) i interfejsów API REST Azure.

## <a name="log-retention"></a>Przechowywanie dziennika
Można ustawić okresu przechowywania hello przy użyciu dzienników systemu **dziennika\_przechowywania\_okres** parametru skojarzonego z serwerem. Witaj jednostki dla tego parametru jest dni (konieczne tooconfirm). Witaj, wartość domyślna to trzy dni. Witaj, wartość maksymalna wynosi 7 dni. Należy pamiętać, że serwer musi mieć wystarczającą ilość hello toocontain Magazyn przydzielony przechowywane pliki dziennika.
pliki dziennika Hello będzie Obróć co godzinę lub 100MB rozmiar, zależności zostanie osiągnięty jako pierwszy.

## <a name="configure-logging-for-azure-postgresql-server"></a>Konfigurowanie rejestrowania dla serwera Azure PostgreSQL
Dla serwera, można włączyć rejestrowanie zapytań i rejestrowania błędów. Dzienniki błędów może zawierać próżni auto, połączenia i punkty kontrolne.

Rejestrowanie zapytań można włączyć dla swojego wystąpienia bazy danych PostgreSQL, ustawiając dwa parametry serwera: dziennika\_instrukcji i dziennika\_min\_czas trwania\_instrukcji.

Witaj **dziennika\_instrukcji** parametr określa instrukcji SQL, które są rejestrowane. Firma Microsoft zaleca ustawienie tego parametru zbyt***wszystkie*** toolog wszystkie instrukcje; wartość domyślna hello jest none (konieczne tooconfirm).

Witaj **dziennika\_min\_czas trwania\_instrukcji** parametr ustawia hello limit w milisekundach toobe instrukcji, rejestrowane. Wszystkie instrukcje SQL działające dłużej niż ustawienie parametru hello są rejestrowane. Ten parametr jest wyłączone i ustawione toominus 1 (-1), domyślnie (potrzeby tooconfirm). Włączenie tego parametru mogą być pomocne w śledzeniu zoptymalizowanego zapytania w aplikacji.

Witaj **dziennika\_min\_wiadomości** pozwala toocontrol poziomów wiadomości, które są zapisywane toohello dziennik serwera. domyślne Hello jest ostrzeżenie. (należy tooconfirm)

Aby uzyskać więcej informacji na temat tych ustawień, zobacz [raportowanie błędów i rejestrowanie](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) dokumentacji. Do konfiguracji bazy danych Azure szczególnie PostgreSQL parametry serwera, zobacz [dzienniki serwera w bazie danych Azure PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Następne kroki
- tooaccess dzienników przy użyciu interfejsu wiersza polecenia interfejsu wiersza polecenia Azure, zobacz [Konfigurowanie i dostępu do dzienników serwera przy użyciu wiersza polecenia platformy Azure](howto-configure-server-logs-using-cli.md)
- Aby uzyskać więcej informacji na parametry serwera, zobacz [dostosować parametry konfiguracji serwera przy użyciu interfejsu wiersza polecenia Azure](howto-configure-server-parameters-using-cli.md).