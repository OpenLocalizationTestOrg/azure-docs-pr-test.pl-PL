---
title: "aaaAzure bazy danych dla reguł zapory serwera MySQL | Dokumentacja firmy Microsoft"
description: "Opisuje reguły zapory bazy danych Azure, aby serwer MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1f85310385da947b6c492aa6aa21c1b885c2a97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a>Bazy danych platformy Azure dla reguł zapory serwera MySQL
Zapory uniemożliwiają wszystkich serwera bazy danych tooyour dostępu do chwili określenia komputery, które ma uprawnienia. Zapora Hello przyznaje serwera toohello dostępu oparte na powitania pochodzące z adresu IP dla każdego żądania.

tooconfigure zapory, tworzenie reguł zapory, które określ zakresy adresów IP dopuszczalne. Można tworzyć reguły zapory na poziomie serwera hello.

**Reguły zapory:** reguły te umożliwiają klientom tooaccess całej bazy danych Azure, aby serwer MySQL, oznacza to, że wszystkie hello bazy danych w ramach hello tym samym serwerze logicznym. Reguły zapory poziomu serwera można skonfigurować za pomocą portalu Azure hello lub przy użyciu poleceń wiersza polecenia platformy Azure. reguły zapory poziomu serwera toocreate, musi być hello subskrypcji właścicielem lub współautorem subskrypcji.

## <a name="firewall-overview"></a>Omówienie zapory
Wszystkie bazy danych tooyour dostępu do bazy danych Azure MySQL serwera jest blokowany przez zaporę hello domyślnie. toobegin korzysta z serwera z innego komputera należy toospecify jedną lub więcej poziomu serwera zapory reguły tooenable dostępu tooyour serwera. Użyj toospecify reguły zapory hello zakresów adresów IP, które z hello Internet tooallow. Toohello Access Azure witryny sieci Web portalu sam nie ma wpływu na powitania reguł zapory.

Próby nawiązania połączenia z hello Internet i Azure musi najpierw przejść przez zaporę Windows hello przed dotarciem Azure bazy danych dla bazy danych MySQL, pokazane na powitania po diagramu:

![Przykładowy przepływ działania hello zapory](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Łączenie z hello Internet
Reguły zapory poziomu serwera Zastosuj baz danych tooall hello Azure bazy danych dla serwera MySQL.

Jeśli adres IP hello żądania hello jest w jednej z określonych w regułach zapory poziomu serwera hello zakresach hello, zostanie ustanowione połączenie hello.

Jeśli adres IP hello hello żądania nie jest w hello zakresy określone w żadnym hello poziom bazy danych lub reguły zapory poziomu serwera hello żądanie połączenia zakończy się niepowodzeniem.

## <a name="programmatically-managing-firewall-rules"></a>Programowe zarządzanie regułami zapory
Ponadto toohello portalu Azure, zapory, zasady mogą być zarządzane, programowo przy użyciu wiersza polecenia platformy Azure. Zobacz też [tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure](./howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>Rozwiązywanie problemów dotyczących zapory bazy danych hello
Należy wziąć pod uwagę następujące punkty, gdy toohello dostępu do bazy danych programu Microsoft Azure dla programu MySQL serwera usługi nie działają zgodnie z oczekiwaniami hello:

* **Lista dozwolonych toohello zmiany nie zostały uwzględnione jeszcze:** może być jak opóźnienie 5 minutową zmienia toohello bazy danych platformy Azure dla efektu tootake konfiguracji zapory serwera MySQL.

* **nie ma uprawnień logowania Hello lub niepoprawne hasło było używane:** Jeśli identyfikator logowania nie ma uprawnień na hello Azure bazy danych MySQL serwera lub hello hasło używane jest nieprawidłowa, hello toohello połączenia bazy danych platformy Azure dla odmowa serwer MySQL. Tworzenie ustawień zapory tylko zapewnia klientom tooattempt możliwość łączenia serwera tooyour; Każdy klient musi podać poświadczenia zabezpieczeń wymaganymi hello.

* **Dynamicznego adresu IP:** Jeśli masz kłopot przez zaporę Windows hello ma połączenia internetowego z dynamicznych adresów IP, można Wypróbuj jedną z następujących rozwiązań hello:

* Zapytaj dostawcę usługi internetowego (ISP) dla zakresu adresów IP hello przypisane komputery klienckie tooyour tego dostępu hello Azure bazy danych MySQL serwera, a następnie Dodaj zakres adresów IP hello jako regułę zapory.

* Pobierz statycznych adresów IP zamiast tego dla komputerów klienckich, a następnie dodaj adresy IP hello jako reguły zapory.

## <a name="next-steps"></a>Następne kroki

[Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure hello](./howto-manage-firewall-using-portal.md)
[tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu wiersza polecenia platformy Azure](./howto-manage-firewall-using-cli.md)
