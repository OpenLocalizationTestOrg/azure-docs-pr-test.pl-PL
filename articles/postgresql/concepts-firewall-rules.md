---
title: "Bazy danych platformy Azure dla reguł zapory serwera PostgreSQL | Dokumentacja firmy Microsoft"
description: "Opisuje reguły zapory bazy danych Azure, aby serwer PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: 7fec71f621ffeff2fc42a5a9464ae9011b2e2fee
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Bazy danych platformy Azure dla reguł zapory serwera PostgreSQL
Azure bazy danych dla serwera PostgreSQL zapory uniemożliwia wszystkich dostęp do serwera bazy danych do chwili określenia komputery, które ma uprawnienia. Zapora udziela dostępu do serwera, na podstawie źródłowego adresu IP dla każdego żądania.
Aby skonfigurować zaporę, należy utworzyć reguły zapory określające zakresy dopuszczalnych adresów IP. Można tworzyć reguły zapory na poziomie serwera.

**Reguły zapory:** te reguły umożliwić klientom dostęp całej bazy danych Azure PostgreSQL serwera, oznacza to, że wszystkie bazy danych w tym samym serwerze logicznym. Reguły zapory poziomu serwera można skonfigurować za pomocą portalu Azure lub przy użyciu poleceń wiersza polecenia platformy Azure. Aby utworzyć reguły zapory poziomu serwera, musi być właściciela subskrypcji lub współautorem subskrypcji.

## <a name="firewall-overview"></a>Omówienie zapory
Wszelki dostęp do bazy danych Azure bazy danych dla serwera PostgreSQL jest zablokowany przez zaporę domyślnie. Aby rozpocząć korzystanie z serwera z innego komputera, należy określić co najmniej jedną regułę zapory poziomu serwera, aby umożliwić dostęp do serwera. Użyj reguł zapory do określenia IP zakresów adresów z Internetu, aby umożliwić. Dostęp do witryny portalu Azure, sama nie ma wpływu na reguły zapory.
Próby nawiązania połączenia z Internetem i Azure musi najpierw przejść przez zaporę przed może nawiązać połączenie z bazą danych PostgreSQL, jak pokazano na poniższym diagramie:

![Przykładowy przepływ działania zapory](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a>Łączenie się z Internetu
Reguły zapory na poziomie serwera dotyczą wszystkich baz danych na tej samej bazy danych Azure, PostgreSQL serwera. Jeśli adres IP żądania należy do jednego z zakresów określonych w regułach zapory na poziomie serwera, ustanawiane jest połączenie.
Jeśli adres IP żądania nie jest w ramach zakresów określonych w żadnej z reguł zapory na poziomie serwera, żądanie połączenia zakończy się niepowodzeniem.
Na przykład jeśli aplikacja łączy się z sterownik JDBC dla PostgreSQL, mogą wystąpić ten błąd próby nawiązania połączenia, gdy Zapora blokuje połączenia.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: błąd krytyczny: nie pg\_hba.conf wpis dla hosta: "123.45.67.890" użytkownika "adminuser", bazy danych "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Programowe zarządzanie regułami zapory
Oprócz portalu Azure można zarządzać reguły zapory, programowo przy użyciu wiersza polecenia platformy Azure.
Zobacz też [tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure](howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-the-database-server-firewall"></a>Rozwiązywanie problemów dotyczących zapory serwera bazy danych
Podczas dostępu do bazy danych Microsoft Azure dla usługi serwera PostgreSQL nie działają zgodnie z oczekiwaniami, należy rozważyć następujące kwestie:

* **Zmiany na liście dozwolonych nie zostały uwzględnione jeszcze:** może być jak opóźnienie 5 minutową zmienia się z bazą danych Azure konfiguracji zapory serwera PostgreSQL zaczęły obowiązywać.

* **Nazwa logowania nie jest autoryzowany lub niepoprawne hasło było używane:** Jeśli nazwa logowania nie ma uprawnień w bazie danych Azure PostgreSQL serwera lub hasło jest niepoprawne, odmowa połączenia z bazą danych Azure PostgreSQL serwera. Tworzenie ustawień zapory tylko zapewnia klientom możliwość nawiązania połączenia z serwerem; Każdy klient nadal należy podać poświadczenia niezbędne zabezpieczeń.

Na przykład za pomocą klienta JDBC, może się pojawić następujący błąd.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: błąd krytyczny: nie można przeprowadzić uwierzytelniania hasła dla użytkownika "nazwa_użytkownika"

* **Dynamiczny adres IP:** jeśli używane jest połączenie internetowe za pomocą dynamicznego adresowania IP i występują problemy z przejściem przez zaporę, można wypróbować jedno z poniższych rozwiązań:

* Zakres adresów IP, które są przypisane do komputerów klienckich łączących się z bazą danych Azure dla serwera PostgreSQL poproś o usługodawcy internetowego (ISP), a następnie Dodaj zakres adresów IP reguły zapory.

* Pobierz statycznych adresów IP zamiast tego dla komputerów klienckich, a następnie dodaj statyczny adres IP reguły zapory.

## <a name="next-steps"></a>Następne kroki
W przypadku artykułów na temat tworzenia reguł zapory na poziomie serwera zobacz:
* [Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu portalu Azure](howto-manage-firewall-using-portal.md).
* [Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu interfejsu wiersza polecenia Azure](howto-manage-firewall-using-cli.md).
