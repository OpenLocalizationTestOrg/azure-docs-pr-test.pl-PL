---
title: "aaaCreate i zarządzania nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a>Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu hello portalu Azure
Reguły zapory poziomu serwera Włącz tooaccess administratorów bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP. 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Utworzyć regułę zapory poziomu serwera w hello portalu Azure

1. W bloku serwera MySQL hello, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** tooopen hello zabezpieczenia połączeń bloku hello Azure bazy danych MySQL.

   ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Kliknij przycisk **dodać Moje IP** na powitania narzędzi toocreate reguły hello adresu IP komputera, ponieważ postrzegane przez hello systemu Azure.

   ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Zweryfikuj swój adres IP przed zapisaniem konfiguracji hello. W niektórych sytuacjach adres IP hello uwzględniony przez Azure portal różni się od hello adres IP używany podczas uzyskiwania dostępu do hello internet i serwerach Azure. Dlatego może być konieczne toochange hello Start adresów IP i końcowemu adresowi IP toomake hello funkcja reguły zgodnie z oczekiwaniami.

   Użyj aparatu wyszukiwania lub inne narzędzia online toocheck adresu IP (na przykład, wyszukaj "co to jest adresu IP").

   ![Bing w celu przedstawienia Moje IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Dodaj dodatkowy adres zakresów. W zasadach hello hello Azure bazy danych MySQL zapory można określić pojedynczy adres IP lub zakresu adresów. Jeśli chcesz toolimit hello reguły tooone pojedynczy adres IP, typ hello sam adres w polu hello Start IP i końcowy adres IP. Otwarcie zapory hello umożliwia administratorom i użytkownikom tooaccess wszystkie bazy danych na powitania MySQL serwera toowhich mają prawidłowe poświadczenia.

   ![Portal Azure — reguły zapory ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Kliknij przycisk **zapisać** na hello toosave narzędzi tę regułę zapory poziomu serwera. Poczekaj, aż hello potwierdzenie, że reguły zapory toohello aktualizacji hello zakończyła się pomyślnie.

   ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a>Zarządzanie istniejącej reguły zapory poziomu serwera za pomocą hello portalu Azure
Powtórz reguły zapory hello hello kroki toomanage.
* tooadd hello bieżącego komputera, kliknij przycisk **+ Dodaj adres IP Moje**.
* tooadd dodatkowe adresy IP, wpisz w hello **Nazwa reguły**, **START IP**, i **KOŃCOWEMU adresowi IP**.
* toomodify istniejącą regułę, kliknij polach hello w regule hello i modyfikować.
* toodelete istniejącą regułę, kliknij przycisk wielokropka hello [...], a następnie kliknij przycisk **usunąć**.
* Kliknij przycisk **zapisać** toosave hello zmiany.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać pomoc w łączenie tooan Azure bazy danych MySQL serwera, zobacz [biblioteki połączeń dla bazy danych Azure dla programu MySQL](./concepts-connection-libraries.md)
