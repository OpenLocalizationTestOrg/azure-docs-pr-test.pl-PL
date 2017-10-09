---
title: "pojęcia aaaServer w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera zagadnienia i wskazówki dotyczące pracy z bazą danych Azure PostgreSQL serwerów."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Bazy danych platformy Azure dla serwerów PostgreSQL
Ten temat zawiera zagadnienia i wskazówki dotyczące pracy z bazą danych Azure PostgreSQL serwerów.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Co to jest Azure bazy danych serwera PostgreSQL?
Baza danych Azure dla serwera PostgreSQL jest centralny punkt administracyjny dla wielu baz danych. Jest hello tego samego konstrukcja serwera PostgreSQL można zapoznać się z Witaj świecie lokalnych. W szczególności hello PostgreSQL usługi jest zarządzany, zapewnia gwarancje wydajności, udostępnia dostępu i funkcji na poziomie serwera.

Azure bazy danych programu PostgreSQL serwera:

- Zostanie utworzone w subskrypcji platformy Azure.
- Jest zasobem nadrzędnej hello baz danych.
- Obejmuje przestrzeń nazw dla baz danych.
- To kontener z semantyki silne istnienia — usuwanie serwera i usuwa hello zawartych baz danych.
- Collocates zasoby w regionie.
- Udostępnia punkt końcowy połączenia dla dostępu do serwera i bazy danych (. postgresql.database.azure.com).
- Określa zakres powitania dla zasad zarządzania, które są stosowane tooits baz danych: logowania, zapory, użytkowników, ról, konfiguracje itd.
- Jest dostępna w różnych wersjach. Aby uzyskać więcej informacji, zobacz [wersji bazy danych obsługiwane PostgreSQL](concepts-supported-versions.md).
- Jest otwarty przez użytkowników. Aby uzyskać więcej informacji, zobacz [PostgreSQL rozszerzenia](concepts-extensions.md).

W ramach Azure bazy danych programu PostgreSQL serwera można utworzyć jedną lub wiele baz danych. Opt toocreate pojedynczej bazy danych na serwerze tooutilize wszystkie zasoby hello lub utworzyć wiele baz danych tooshare hello zasobów. Cennik Hello strukturalnych na serwer, na podstawie konfiguracji hello warstwy cenowej obliczeniowe jednostki, Magazyn (GB). Aby uzyskać więcej informacji, zobacz [warstw cenowych](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Jak połączyć i uwierzytelniania tooan Azure bazy danych dla serwera PostgreSQL?
Witaj następujące elementy zagwarantować tooyour bezpiecznego dostępu do bazy danych.

|||
| :-- | :-- |
| **Uwierzytelnianie i autoryzacja** | Azure bazy danych dla serwera PostgreSQL obsługuje natywnych uwierzytelnianie PostgreSQL. Możesz łączyć i tooserver z identyfikator logowania administratora powitania serwera uwierzytelniania. |
| **Protokół** | Usługa Hello obsługuje protokół oparta na komunikatach używany przez PostgreSQL. |
| **PROTOKÓŁ TCP/IP** | Protokół Hello jest obsługiwany za pośrednictwem protokołu TCP/IP i za pośrednictwem gniazda domeny systemu Unix. |
| **Zapora** | toohelp chronić dane, reguła zapory uniemożliwia wszystkich serwera bazy danych tooyour dostępu lub tooits baz danych, do momentu określenia komputery, które ma uprawnienia. Zobacz [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Jak zarządzać serwerem?
Baza danych Azure można zarządzać dla hello PostgreSQL serwerów za pomocą portalu Azure lub hello [interfejsu wiersza polecenia Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Następne kroki
- Omówienie usługi hello, zobacz [Azure bazy danych PostgreSQL — omówienie](overview.md)
- Aby uzyskać informacje dotyczące określonego zasobu Przydziały i ograniczenia na podstawie Twojej **warstwy usług**, zobacz [warstwy usług](concepts-service-tiers.md)
- Uzyskać informacji na temat łączenia usługi toohello, zobacz [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md).
