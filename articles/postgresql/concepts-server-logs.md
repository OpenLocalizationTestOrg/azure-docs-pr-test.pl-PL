---
title: "Dzienników serwera w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "Generuje dziennikami błędów i kwerendy w bazie danych Azure dla PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 10f6c490a4fdb4c70cb80b035eaebb9d2ad2e699
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Dzienników serwera w bazie danych Azure PostgreSQL 
Bazy danych platformy Azure dla PostgreSQL generuje zapytań i błąd dzienników. Jednak dostęp do dzienników transakcji nie jest obsługiwany. Te dzienniki może służyć do identyfikowania, rozwiązywania, nieoptymalnych wydajności i błędów konfiguracji. Aby uzyskać więcej informacji, zobacz [raportowanie błędów i rejestrowanie](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Dzienniki serwera dostępu
Można wyświetlić listę i Pobierz dzienniki błędów serwera Azure PostgreSQL przy użyciu portalu Azure [interfejsu wiersza polecenia Azure](howto-configure-server-logs-using-cli.md) i interfejsów API REST Azure.

## <a name="log-retention"></a>Przechowywanie dziennika
Można ustawić okresu przechowywania dla dzienniki systemu za pomocą **dziennika\_przechowywania\_okres** parametru skojarzonego z serwerem. Jednostki dla tego parametru jest dni (trzeba potwierdzić). Wartość domyślna to trzy dni. Wartość maksymalna wynosi 7 dni. Należy pamiętać, że serwer musi mieć wystarczającej ilości przydzielone magazynu zawiera pliki dziennika zachowanych.
Pliki dziennika zostaną Obróć co godzinę lub 100MB rozmiar, zależnie od zostanie osiągnięty jako pierwszy.

## <a name="configure-logging-for-azure-postgresql-server"></a>Konfigurowanie rejestrowania dla serwera Azure PostgreSQL
Dla serwera, można włączyć rejestrowanie zapytań i rejestrowania błędów. Dzienniki błędów może zawierać próżni auto, połączenia i punkty kontrolne.

Rejestrowanie zapytań można włączyć dla swojego wystąpienia bazy danych PostgreSQL, ustawiając dwa parametry serwera: dziennika\_instrukcji i dziennika\_min\_czas trwania\_instrukcji.

**Dziennika\_instrukcji** parametr określa instrukcji SQL, które są rejestrowane. Firma Microsoft zaleca ustawienie tego parametru ***wszystkie*** do rejestrowania wszystkich instrukcji; wartość domyślna to none (trzeba potwierdzić).

**Dziennika\_min\_czas trwania\_instrukcji** parametr ustawia limit (w milisekundach) oświadczenia mają być rejestrowane. Wszystkie instrukcje SQL działające dłużej niż ustawienie parametru są rejestrowane. Ten parametr jest wyłączona i domyślnie ustawiany na minus 1 (-1) (wymagana, aby potwierdzić). Włączenie tego parametru mogą być pomocne w śledzeniu zoptymalizowanego zapytania w aplikacji.

**Dziennika\_min\_wiadomości** zezwala na określanie komunikatu poziomy są zapisywane w dzienniku serwera. Wartość domyślna to ostrzeżenie. (wymaga potwierdzenia)

Aby uzyskać więcej informacji na temat tych ustawień, zobacz [raportowanie błędów i rejestrowanie](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) dokumentacji. Do konfiguracji bazy danych Azure szczególnie PostgreSQL parametry serwera, zobacz [dzienniki serwera w bazie danych Azure PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać dostęp do dzienników przy użyciu interfejsu wiersza polecenia interfejsu wiersza polecenia Azure, zobacz [Konfigurowanie i dostępu do dzienników serwera przy użyciu wiersza polecenia platformy Azure](howto-configure-server-logs-using-cli.md)
- Aby uzyskać więcej informacji na parametry serwera, zobacz [dostosować parametry konfiguracji serwera przy użyciu interfejsu wiersza polecenia Azure](howto-configure-server-parameters-using-cli.md).