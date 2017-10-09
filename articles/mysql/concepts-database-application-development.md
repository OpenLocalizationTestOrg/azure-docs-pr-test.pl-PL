---
title: "Omówienie tworzenia aplikacji aaaDatabase bazy danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Wprowadza zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania aplikacji kod tooconnect tooAzure bazy danych dla programu MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Omówienie tworzenia aplikacji dla bazy danych Azure dla programu MySQL 
W tym artykule omówiono zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania aplikacji kod tooconnect tooAzure bazy danych dla programu MySQL 

> [!TIP]
> Samouczek przedstawiający sposób toocreate serwera, utworzenie zapory na serwerze, wyświetlić właściwości serwera, Utwórz bazę danych, Połącz i zapytań przy użyciu narzędzia workbench i mysql.exe, można zobaczyć [projektowania pierwszą bazę danych MySQL na platformie Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Język i platforma
Dostępne są przykłady kodu dla różnych języków programowania i platform programistycznych. Można skorzystać z łączy toohello przykłady kodu w: [bibliotek łączności używane tooAzure tooconnect bazy danych dla programu MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Narzędzia
Bazy danych platformy Azure dla programu MySQL używa hello MySQL community wersji, zgodnej z programem MySQL popularnych narzędzi do zarządzania takich jak narzędzia Workbench lub MySQL, takich jak mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)i inne. Można również używać hello portalu Azure, interfejsu wiersza polecenia Azure i toointeract interfejsów API REST z hello bazy danych usługi.

## <a name="resource-limitations"></a>Ograniczenia zasobów
Baza danych MySQL Azure zarządza serwer tooa dostępne zasoby hello przy użyciu dwóch różnych mechanizmów: 
- Zarządzanie zasobami 
- Wymuszanie ograniczeń.

## <a name="security"></a>Bezpieczeństwo
Baza danych MySQL Azure zawiera zasoby dotyczące ograniczanie dostępu, ochrona danych Konfigurowanie użytkowników i ról i monitorowanie działań na bazę danych MySQL.

## <a name="authentication"></a>Authentication
Baza danych MySQL Azure obsługuje uwierzytelnianie serwera użytkowników i nazwy logowania.

## <a name="resiliency"></a>Odporność
Po wystąpieniu błędu przejściowego podczas łączenia tooMySQL bazy danych, kod powinien ponów wywołanie hello. Firma Microsoft zaleca użycie logiki ponawiania hello wycofania logiki, tak, że nie przeciąży hello bazy danych SQL z wielu klientów jednocześnie ponawianie próby.

- Przykłady kodu: Logika ponawiania próby przykłady kodu, które ilustrują temacie Przykłady dla języka hello wybranym w: [bibliotek łączności używane tooAzure tooconnect bazy danych dla programu MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Zarządzanie połączeniami
Połączenia bazy danych są ograniczone zasobu, tak więc zaleca się użycie za pośrednictwem połączenia podczas uzyskiwania dostępu do bazy danych MySQL tooachieve lepszą wydajność.
- Hello dostępu do bazy danych przy użyciu puli połączeń lub połączeń trwałych.
- Hello dostępu do bazy danych przy użyciu krótkich połączenia życia. 
- Logika ponawiania użycia w aplikacji w punkcie hello hello próba połączenia, błędy toocatch powodu połączeń tooconcurrent osiągnięto hello maksymalna dozwolona liczba. W hello Logika ponawiania próby, ustawić krótkie opóźnienie i poczekaj losowy czas przed hello prób dodatkowego połączenia.
