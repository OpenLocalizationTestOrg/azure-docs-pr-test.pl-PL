---
title: "Omówienie tworzenia aplikacji bazy danych dla bazy danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Wprowadza zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania kodu aplikacji do łączenia z bazą danych Azure dla programu MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Omówienie tworzenia aplikacji dla bazy danych Azure dla programu MySQL 
W tym artykule omówiono zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania kodu aplikacji do łączenia z bazą danych Azure dla programu MySQL 

> [!TIP]
> Samouczek pokazuje, jak utworzyć serwer, utworzenie zapory na serwerze, wyświetlić właściwości serwera, Utwórz bazę danych, Połącz i zapytań przy użyciu narzędzia workbench i mysql.exe, zobacz [projektowania pierwszą bazę danych MySQL na platformie Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Język i platforma
Dostępne są przykłady kodu dla różnych języków programowania i platform programistycznych. Można znaleźć łącza do przykładów kodu w: [bibliotek łączności używane do łączenia z bazą danych Azure dla programu MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Narzędzia
Wersja ciągu identyfikacyjnego MySQL, zgodne z MySQL popularnych narzędzi do zarządzania takich jak narzędzia Workbench lub MySQL, takich jak mysql.exe, korzysta z bazy danych platformy Azure dla programu MySQL [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)i inne. Do interakcji z usługą baza danych, można użyć portalu Azure, interfejsu wiersza polecenia Azure i interfejsów API REST.

## <a name="resource-limitations"></a>Ograniczenia zasobów
Baza danych MySQL Azure zarządza zasoby dostępne dla serwera przy użyciu dwóch różnych mechanizmów: 
- Zarządzanie zasobami 
- Wymuszanie ograniczeń.

## <a name="security"></a>Bezpieczeństwo
Baza danych MySQL Azure zawiera zasoby dotyczące ograniczanie dostępu, ochrona danych Konfigurowanie użytkowników i ról i monitorowanie działań na bazę danych MySQL.

## <a name="authentication"></a>Authentication
Baza danych MySQL Azure obsługuje uwierzytelnianie serwera użytkowników i nazwy logowania.

## <a name="resiliency"></a>Odporność
Po wystąpieniu błędu przejściowego podczas łączenia z bazą danych MySQL, ponów wywołanie kodu. Firma Microsoft zaleca, użyj logiki ponawiania wycofania logiki, więc, że nie przeciąży bazy danych SQL z wielu klientów jednocześnie ponawianie próby.

- Przykłady kodu: Logika ponawiania próby przykłady kodu, które ilustrują temacie Przykłady w języku wybranym w: [bibliotek łączności używane do łączenia z bazą danych Azure dla programu MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Zarządzanie połączeniami
Połączenia bazy danych są ograniczone zasobów, dlatego zalecamy użycie za pośrednictwem połączenia podczas uzyskiwania dostępu do bazy danych MySQL osiągnąć większą wydajność.
- Dostęp do bazy danych przy użyciu puli połączeń lub połączeń trwałych.
- Dostęp do bazy danych przy użyciu krótkich połączenia życia. 
- Użyj logiki ponawiania próby w aplikacji w punkcie próba połączenia, aby wykryć błędy z powodu równoczesnych połączeń osiągnięto maksymalną dozwoloną. W Logika ponawiania ustawić krótkie opóźnienie i poczekaj losowy czas przed prób dodatkowego połączenia.