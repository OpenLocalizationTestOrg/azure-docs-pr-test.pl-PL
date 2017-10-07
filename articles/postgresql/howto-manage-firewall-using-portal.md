---
title: "aaaCreate i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu hello portalu Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a>Tworzenie i zarządzanie bazą danych Azure dla reguł zapory PostgreSQL przy użyciu hello portalu Azure
Reguły zapory poziomu serwera włączyć tooaccess administratorów bazy danych Azure PostgreSQL serwera z określonego adresu IP lub zakresu adresów IP. 

## <a name="prerequisites"></a>Wymagania wstępne
toostep za pośrednictwem tego jak tooguide, potrzebne są:
- Serwer [utworzenia bazy danych Azure dla PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Utworzyć regułę zapory poziomu serwera w hello portalu Azure
1. W bloku serwera PostgreSQL hello, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** tooopen hello zabezpieczenia połączeń bloku hello Azure bazy danych PostgreSQL.

  ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Kliknij przycisk **dodać Moje IP** na powitania narzędzi. Spowoduje to utworzenie reguły automatycznie hello adresu IP komputera, jako postrzegana przez hello systemu Azure.

  ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Zweryfikuj swój adres IP przed zapisaniem konfiguracji hello. W niektórych sytuacjach adres IP hello uwzględniony przez Azure portal różni się od hello adres IP używany podczas uzyskiwania dostępu do hello internet i serwerach Azure. Dlatego może być konieczne toochange hello Start adresów IP i końcowemu adresowi IP toomake hello funkcja reguły zgodnie z oczekiwaniami.
Użyj aparatu wyszukiwania lub inne narzędzia online toocheck własnego adresu IP (na przykład wyszukiwania usługi Bing "co to jest IP Moje").

  ![Co to jest Mój IP wyszukiwania usługi Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Dodaj dodatkowy adres zakresów. W zasadach hello hello Azure bazy danych PostgreSQL zapory można określić pojedynczy adres IP lub zakresu adresów. Jeśli chcesz toolimit hello reguły tooone pojedynczy adres IP, typ hello sam adres w polu hello Start IP i końcowy adres IP. Otwarcie zapory hello umożliwia administratorom i użytkownikom toologin tooany bazy danych na powitania toowhich serwera PostgreSQL mają prawidłowe poświadczenia.

  ![Portal Azure — reguły zapory ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Kliknij przycisk **zapisać** na hello toosave narzędzi tę regułę zapory poziomu serwera. Poczekaj, aż hello potwierdzenie, że reguły zapory toohello aktualizacji hello zakończyła się pomyślnie.

  ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Zarządzanie istniejącej reguły zapory poziomu serwera za pomocą hello portalu Azure
Powtórz reguły zapory hello hello kroki toomanage.
* tooadd hello bieżącego komputera, kliknij przycisk hello zbyt + **dodać Moje IP**. Kliknij przycisk **zapisać** toosave hello zmiany.
* tooadd dodatkowe adresy IP, wpisz w hello nazwę reguły, początkowy adres IP i końcowy adres IP. Kliknij przycisk **zapisać** toosave hello zmiany.
* toomodify istniejącą regułę, kliknij polach hello w regule hello i modyfikować. Kliknij przycisk **zapisać** toosave hello zmiany.
* toodelete istniejącą regułę, kliknij przycisk wielokropka hello [...] i kliknij przycisk Usuń Usuń hello reguły. Kliknij przycisk **zapisać** toosave hello zmiany.

## <a name="next-steps"></a>Następne kroki
- Podobnie można utworzyć skrypty zbyt[tworzenie i zarządzanie bazą danych Azure PostgreSQL reguł zapory przy użyciu wiersza polecenia platformy Azure](howto-manage-firewall-using-cli.md)
- Aby uzyskać pomoc w łączenie tooan Azure bazy danych dla serwera PostgreSQL, [biblioteki połączeń dla bazy danych Azure dla PostgreSQL](concepts-connection-libraries.md)
