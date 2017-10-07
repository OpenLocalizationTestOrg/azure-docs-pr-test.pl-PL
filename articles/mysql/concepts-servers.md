---
title: "Pojęcia dotyczące aaaServer w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera zagadnienia i wskazówki dotyczące pracy z bazą danych Azure dla serwerów MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Pojęcia dotyczące serwera bazy danych Azure dla programu MySQL
Ten temat zawiera zagadnienia i wskazówki dotyczące pracy z bazą danych Azure dla serwerów MySQL.

## <a name="what-is-an-azure-database-for-mysql-server"></a>Co to jest Azure bazy danych serwera MySQL?

Baza danych Azure MySQL serwera jest centralny punkt administracyjny dla wielu baz danych. Jest hello tego samego konstrukcja serwera MySQL można zapoznać się z Witaj świecie lokalnych. W szczególności hello Azure bazy danych dla usługi MySQL jest zarządzany, zapewnia gwarancje wydajności, udostępnia dostępu i funkcji na poziomie serwera.

Azure bazy danych MySQL serwera:

- Zostanie utworzone w subskrypcji platformy Azure.
- Jest zasobem nadrzędnej hello baz danych.
- Obejmuje przestrzeń nazw dla baz danych.
- To kontener z semantyki silne istnienia — usuwanie serwera i usuwa hello zawartych baz danych.
- Collocates zasoby w regionie.
- Udostępnia punkt końcowy połączenia dla serwera i dostęp do bazy danych.
- Określa zakres powitania dla zasad zarządzania, które są stosowane tooits baz danych: logowania, zapory, użytkowników, ról, konfiguracje itd.
- Jest dostępna w różnych wersjach. Aby uzyskać więcej informacji, zobacz [obsługiwane bazy danych Azure dla wersji bazy danych MySQL](./concepts-supported-versions.md).

Na serwerze usługi Azure Database for MySQL można utworzyć jedną lub wiele baz danych. Opt toocreate pojedynczej bazy danych na serwerze tooutilize wszystkie zasoby hello lub utworzyć wiele baz danych tooshare hello zasobów. Cennik Hello strukturalnych na serwer, na podstawie konfiguracji hello warstwy cenowej obliczeniowe jednostki, Magazyn (GB). Aby uzyskać więcej informacji, zobacz [warstw cenowych](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>Jak połączyć i uwierzytelniania tooan Azure bazy danych MySQL serwera?

Witaj następujące elementy zagwarantować tooyour bezpiecznego dostępu do bazy danych.

|||
| :-- | :-- |
| **Uwierzytelnianie i autoryzacja** | Azure bazy danych MySQL serwera obsługuje natywnych uwierzytelnianie MySQL. Możesz łączyć i tooserver z identyfikator logowania administratora powitania serwera uwierzytelniania. |
| **Protokół** | Usługa Hello obsługuje protokół oparta na komunikatach używany przez MySQL. |
| **PROTOKÓŁ TCP/IP** | Protokół Hello jest obsługiwany za pośrednictwem protokołu TCP/IP i za pośrednictwem gniazda domeny systemu Unix. |
| **Zapora** | toohelp chronić dane, reguła zapory uniemożliwia wszystkich serwera bazy danych tooyour dostępu lub tooits baz danych, do momentu określenia komputery, które ma uprawnienia. Zobacz [bazą danych Azure dla reguł zapory serwera MySQL](./concepts-firewall-rules.md). |
| **PROTOKÓŁ SSL** | Usługa Hello obsługuje wymuszenie połączenia SSL między aplikacjami a serwerem bazy danych.  Zobacz [łączności Konfigurowanie protokołu SSL w Twojej aplikacji toosecurely połączyć tooAzure bazy danych MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Jak zarządzać serwerem?
Można zarządzać Azure bazy danych MySQL serwerów za pomocą hello portalu Azure lub hello wiersza polecenia platformy Azure.

## <a name="next-steps"></a>Następne kroki
- Omówienie usługi hello, zobacz [Azure bazy danych MySQL — omówienie](./overview.md)
- Aby uzyskać informacje dotyczące określonego zasobu Przydziały i ograniczenia na podstawie Twojej **warstwy usług**, zobacz [warstwy usług](./concepts-service-tiers.md)
- Dla informacji na temat łączenia usługi toohello [biblioteki połączeń dla bazy danych Azure dla programu MySQL](./concepts-connection-libraries.md).
