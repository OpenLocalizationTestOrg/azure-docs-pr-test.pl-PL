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
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Bazy danych platformy Azure dla reguł zapory serwera PostgreSQL
Zapory uniemożliwiają wszystkich serwera bazy danych tooyour dostępu do chwili określenia komputery, które ma uprawnienia. Zapora Hello przyznaje serwera toohello dostępu oparte na powitania pochodzące z adresu IP dla każdego żądania.
tooconfigure zapory, tworzenie reguł zapory, które określ zakresy adresów IP dopuszczalne. Można tworzyć reguły zapory na poziomie serwera hello.

**Reguły zapory:** te reguły włączyć tooaccess klientów całej bazy danych Azure PostgreSQL serwera, oznacza to, że wszystkie hello bazy danych w ramach hello tym samym serwerze logicznym. Reguły zapory poziomu serwera można skonfigurować za pomocą portalu Azure hello lub przy użyciu poleceń wiersza polecenia platformy Azure. reguły zapory poziomu serwera toocreate, musi być hello subskrypcji właścicielem lub współautorem subskrypcji.

## <a name="firewall-overview"></a>Omówienie zapory
Wszystkie bazy danych tooyour dostępu do bazy danych Azure PostgreSQL serwera jest blokowany przez zaporę hello domyślnie. toobegin korzysta z serwera z innego komputera należy toospecify jedną lub więcej poziomu serwera zapory reguły tooenable dostępu tooyour serwera. Użyj toospecify reguły zapory hello zakresów adresów IP, które z hello Internet tooallow. Toohello Access Azure witryny sieci Web portalu sam nie ma wpływu na powitania reguł zapory.
Próby nawiązania połączenia z hello Internet i Azure musi najpierw przejść przez zaporę Windows hello przed może nawiązać połączenie z bazą danych PostgreSQL, pokazane na powitania po diagramu:

![Przykładowy przepływ działania hello zapory](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Łączenie z hello Internet
Reguły zapory poziomu serwera Zastosuj hello Azure bazy danych dla serwera PostgreSQL tooall baz danych. Jeśli adres IP hello żądania hello jest w jednej z określonych w regułach zapory poziomu serwera hello zakresach hello, zostanie ustanowione połączenie hello.
Jeśli adres IP hello hello żądania nie jest w hello zakresy określone w żadnym hello poziom bazy danych lub reguły zapory poziomu serwera hello żądanie połączenia zakończy się niepowodzeniem.
Na przykład jeśli aplikacja łączy się z sterownik JDBC dla PostgreSQL, mogą wystąpić ten błąd podjęciem próby wykonania tooconnect hello Zapora blokuje hello połączenia.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: błąd krytyczny: nie pg\_hba.conf wpis dla hosta: "123.45.67.890" użytkownika "adminuser", bazy danych "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Programowe zarządzanie regułami zapory
Ponadto toohello portalu Azure, zapory, zasady mogą być zarządzane, programowo przy użyciu wiersza polecenia platformy Azure.
Zobacz też [tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure](howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Rozwiązywanie problemów dotyczących zapory bazy danych hello
Należy wziąć pod uwagę następujące punkty, gdy toohello dostępu do bazy danych programu Microsoft Azure dla usługi serwera PostgreSQL nie działają zgodnie z oczekiwaniami hello:

* **Lista dozwolonych toohello zmiany nie zostały uwzględnione jeszcze:** może być jak opóźnienie 5 minutową zmienia toohello bazy danych platformy Azure dla efektu tootake konfiguracji zapory serwera PostgreSQL.

* **nie ma uprawnień logowania Hello lub niepoprawne hasło było używane:** Jeśli identyfikator logowania nie ma uprawnień na powitania bazy danych Azure, PostgreSQL serwera lub hello hasło używane jest nieprawidłowa, hello toohello połączenia bazy danych Azure jest PostgreSQL serwera Odmowa dostępu. Tworzenie ustawień zapory tylko zapewnia klientom tooattempt możliwość łączenia serwera tooyour; Każdy klient musi podać poświadczenia zabezpieczeń wymaganymi hello.

Na przykład za pomocą klienta JDBC hello następujący błąd może pojawić się.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: błąd krytyczny: nie można przeprowadzić uwierzytelniania hasła dla użytkownika "nazwa_użytkownika"

* **Dynamicznego adresu IP:** Jeśli masz kłopot przez zaporę Windows hello ma połączenia internetowego z dynamicznych adresów IP, można Wypróbuj jedną z następujących rozwiązań hello:

* Zapytaj dostawcę usługi internetowego (ISP) dla zakresu adresów IP hello przypisane komputery klienckie tooyour hello tego dostępu do bazy danych Azure PostgreSQL serwera, a następnie Dodaj zakres adresów IP hello jako regułę zapory.

* Pobierz statycznych adresów IP zamiast tego dla komputerów klienckich, a następnie dodaj adresy IP hello jako reguły zapory.

## <a name="next-steps"></a>Następne kroki
W przypadku artykułów na temat tworzenia reguł zapory serwera i na poziomie bazy danych zobacz:
* [Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu hello portalu Azure](howto-manage-firewall-using-portal.md)
* [Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu wiersza polecenia platformy Azure](howto-manage-firewall-using-cli.md)