---
title: "Pojęcia dotyczące serwera bazy danych Azure PostgreSQL | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera zagadnienia i wskazówki dotyczące pracy z bazą danych Azure PostgreSQL serwerów."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: c79603a11fa23ad775783157675c07ab67102057
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Bazy danych platformy Azure dla serwerów PostgreSQL
Ten temat zawiera zagadnienia i wskazówki dotyczące pracy z bazą danych Azure PostgreSQL serwerów.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Co to jest Azure bazy danych serwera PostgreSQL?
Baza danych Azure dla serwera PostgreSQL jest centralny punkt administracyjny dla wielu baz danych. Jest tym samym konstrukcja PostgreSQL serwera można zapoznać się z na świecie lokalnych. W szczególności usługa PostgreSQL jest zarządzany, zapewnia gwarancje wydajności, udostępnia dostępu i funkcji na poziomie serwera.

Azure bazy danych programu PostgreSQL serwera:

- Zostanie utworzone w subskrypcji platformy Azure.
- Jest zasobem nadrzędnej dla baz danych.
- Obejmuje przestrzeń nazw dla baz danych.
- To kontener z semantyki silne istnienia — usuwanie serwera i usuwa zawartych baz danych.
- Collocates zasoby w regionie.
- Udostępnia punkt końcowy połączenia dla dostępu do serwera i bazy danych (. postgresql.database.azure.com).
- Określa zakres dla zasad zarządzania, które są stosowane do jej baz danych: logowania, zapory, użytkowników, ról, konfiguracje itd.
- Jest dostępna w różnych wersjach. Aby uzyskać więcej informacji, zobacz [wersji bazy danych obsługiwane PostgreSQL](concepts-supported-versions.md).
- Jest otwarty przez użytkowników. Aby uzyskać więcej informacji, zobacz [PostgreSQL rozszerzenia](concepts-extensions.md).

W ramach Azure bazy danych programu PostgreSQL serwera można utworzyć jedną lub wiele baz danych. Można wybrać opcję utworzenia jednej bazy danych na serwer w celu wykorzystania wszystkich zasobów. Można też utworzyć wiele baz danych, współdzielących zasoby. Cennik strukturalnych na serwer, na podstawie konfiguracji warstwy cenowej obliczeniowe jednostki, Magazyn (GB). Aby uzyskać więcej informacji, zobacz [warstw cenowych](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-postgresql-server"></a>Jak połączyć i uwierzytelniania z bazą danych PostgreSQL serwera Azure?
Następujące elementy zapewnić bezpieczny dostęp do bazy danych.

|||
| :-- | :-- |
| **Uwierzytelnianie i autoryzacja** | Azure bazy danych dla serwera PostgreSQL obsługuje natywnych uwierzytelnianie PostgreSQL. Możesz łączyć i uwierzytelniać się na serwerze z nazwą logowania administratora serwera. |
| **Protokół** | Usługa obsługuje protokół oparta na komunikatach używany przez PostgreSQL. |
| **PROTOKÓŁ TCP/IP** | Protokół jest obsługiwany za pośrednictwem protokołu TCP/IP i za pośrednictwem gniazda domeny systemu Unix. |
| **Zapora** | Aby chronić dane, regułę zapory uniemożliwia dostęp serwer bazy danych lub jej baz danych do chwili określenia komputery, które ma uprawnienia. Zobacz [bazą danych Azure dla reguł zapory serwera PostgreSQL](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Jak zarządzać serwerem?
Baza danych Azure PostgreSQL serwerów można zarządzać za pomocą portalu Azure lub [interfejsu wiersza polecenia Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Następne kroki
- Aby zapoznać się z omówieniem usługi, zobacz [Azure bazy danych PostgreSQL — omówienie](overview.md)
- Aby uzyskać informacje dotyczące określonego zasobu Przydziały i ograniczenia na podstawie Twojej **warstwy usług**, zobacz [warstwy usług](concepts-service-tiers.md)
- Aby uzyskać informacje na połączenie z usługą, zobacz [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md).
