---
title: "Bazy danych platformy Azure dla reguł zapory serwera MySQL | Dokumentacja firmy Microsoft"
description: "Opisuje reguły zapory bazy danych Azure, aby serwer MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 7456cef7a5da665ee3d70df64265b8186a79f9b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a>Bazy danych platformy Azure dla reguł zapory serwera MySQL
Zapory uniemożliwić dostęp do serwera bazy danych do chwili określenia komputery, które ma uprawnienia. Zapora udziela dostępu do serwera, na podstawie źródłowego adresu IP dla każdego żądania.

Aby skonfigurować zaporę, należy utworzyć reguły zapory określające zakresy dopuszczalnych adresów IP. Można tworzyć reguły zapory na poziomie serwera.

**Reguły zapory:** reguły te umożliwiają klientom dostęp do całej bazy danych Azure, aby serwer MySQL, oznacza to, że wszystkie bazy danych w tym samym serwerze logicznym. Reguły zapory poziomu serwera można skonfigurować za pomocą portalu Azure lub przy użyciu poleceń wiersza polecenia platformy Azure. Aby utworzyć reguły zapory poziomu serwera, musi być właściciela subskrypcji lub współautorem subskrypcji.

## <a name="firewall-overview"></a>Omówienie zapory
Wszelki dostęp do bazy danych Azure bazy danych MySQL serwera jest zablokowany przez zaporę domyślnie. Aby rozpocząć korzystanie z serwera z innego komputera, należy określić co najmniej jedną regułę zapory poziomu serwera, aby umożliwić dostęp do serwera. Użyj reguł zapory do określenia IP zakresów adresów z Internetu, aby umożliwić. Dostęp do witryny portalu Azure, sama nie ma wpływu na reguły zapory.

Próby nawiązania połączenia z Internetem i Azure musi najpierw przejść przez zaporę przed dotarciem Azure bazy danych dla bazy danych MySQL, jak pokazano na poniższym diagramie:

![Przykładowy przepływ działania zapory](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a>Łączenie się z Internetu
Reguły zapory na poziomie serwera dotyczą wszystkich baz danych w bazie danych Azure dla serwera MySQL.

Jeśli adres IP żądania należy do jednego z zakresów określonych w regułach zapory na poziomie serwera, ustanawiane jest połączenie.

Jeśli adres IP żądania nie jest w zakresie określony w żadnym z reguły zapory poziomu serwera lub na poziomie bazy danych, żądanie połączenia zakończy się niepowodzeniem.

## <a name="programmatically-managing-firewall-rules"></a>Programowe zarządzanie regułami zapory
Oprócz portalu Azure można zarządzać reguły zapory, programowo przy użyciu wiersza polecenia platformy Azure. Zobacz też [tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure](./howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-the-database-firewall"></a>Rozwiązywanie problemów z zaporą bazy danych
Podczas dostępu do bazy danych Microsoft Azure dla usługi serwera MySQL nie działają zgodnie z oczekiwaniami, należy rozważyć następujące kwestie:

* **Zmiany na liście dozwolonych nie zostały uwzględnione jeszcze:** może być jak opóźnienie 5 minutową zmienia się z bazą danych Azure konfiguracji zapory serwera MySQL zaczęły obowiązywać.

* **Nazwa logowania nie jest autoryzowany lub niepoprawne hasło było używane:** nazwy logowania nie ma uprawnień w bazie danych Azure MySQL serwera lub hasło jest niepoprawne, odmowa połączenia z bazą danych Azure dla serwera MySQL. Utworzenie ustawień zapory zapewnia klientom jedynie możliwość próby nawiązania połączenia z serwerem, ale każdy klient musi podać niezbędne poświadczenia zabezpieczeń.

* **Dynamiczny adres IP:** jeśli używane jest połączenie internetowe za pomocą dynamicznego adresowania IP i występują problemy z przejściem przez zaporę, można wypróbować jedno z poniższych rozwiązań:

* Zakres adresów IP, które są przypisane do komputerów klienckich łączących się z bazą danych Azure dla serwera MySQL poproś o usługodawcy internetowego (ISP), a następnie Dodaj zakres adresów IP reguły zapory.

* Pobierz statyczne adresy IP dla komputerów klienckich, a następnie dodaj te adresy IP jako reguły zapory.

## <a name="next-steps"></a>Następne kroki

[Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure](./howto-manage-firewall-using-portal.md)
[tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure](./howto-manage-firewall-using-cli.md)
