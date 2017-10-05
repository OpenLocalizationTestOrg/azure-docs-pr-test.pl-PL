---
title: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a>Tworzenie i zarządzanie nimi Azure bazy danych MySQL reguł zapory przy użyciu portalu Azure
Reguły zapory poziomu serwera umożliwiają administratorom dostęp do bazy danych Azure MySQL serwera z określonego adresu IP lub zakresu adresów IP. 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a>Tworzenie reguły zapory na poziomie serwera w witrynie Azure Portal

1. W bloku serwera MySQL, w obszarze Ustawienia kliknij pozycję **zabezpieczenia połączeń** aby otworzyć blok połączenia zabezpieczeń bazy danych Azure dla programu MySQL.

   ![Portal Azure — kliknij przycisk Zabezpieczenia połączeń](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Kliknij przycisk **dodać Moje IP** na pasku narzędzi, aby utworzyć regułę przy użyciu adresu IP komputera, jako widocznego w systemie Azure.

   ![Portal Azure — kliknij przycisk Dodaj mój adres IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Zweryfikuj swój adres IP przed zapisaniem konfiguracji. W niektórych sytuacjach adres IP uwzględniony przez Azure portal różni się od adresu IP, używana podczas uzyskiwania dostępu do Internetu i serwery usługi Azure. Dlatego może być konieczne zmiany Start IP i końcowemu adresowi IP, aby funkcja reguły zgodnie z oczekiwaniami.

   Użyj aparatu wyszukiwania lub innego narzędzia online w celu sprawdzenia adresu IP (na przykład, wyszukaj "co to jest adresu IP").

   ![Bing w celu przedstawienia Moje IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Dodaj dodatkowy adres zakresów. W zasadach zapory MySQL bazą danych Azure można określić pojedynczy adres IP lub zakresu adresów. Jeśli chcesz ograniczyć regułę jeden pojedynczy adres IP wpisz ten sam adres w polu Start IP i końcowy adres IP. Otwarcie zapory umożliwia Administratorzy i użytkownicy mogą uzyskać dostępu do dowolnej bazy danych na serwerze MySQL, do których mają prawidłowe poświadczenia.

   ![Portal Azure — reguły zapory ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. Kliknij przycisk **zapisać** na pasku narzędzi, aby zapisać tę regułę zapory poziomu serwera. Poczekaj na potwierdzenie pomyślnego aktualizacji reguł zapory.

   ![Portal Azure — kliknij przycisk Zapisz](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a>Zarządzanie istniejącymi regułami zapory na poziomie serwera przy użyciu witryny Azure Portal
Powtórz kroki, aby zarządzać regułami zapory.
* Aby dodać bieżący komputer, kliknij przycisk **+ Dodaj adres IP Moje**.
* Aby dodać dodatkowe adresy IP, wpisz w **Nazwa reguły**, **START IP**, i **KOŃCOWEMU adresowi IP**.
* Aby zmodyfikować istniejącą regułę, kliknij dowolne pole w regule i wprowadź zmiany.
* Aby usunąć istniejącą regułę, kliknij przycisk wielokropka [...], a następnie kliknij przycisk **usunąć**.
* Kliknij przycisk **Zapisz**, aby zapisać zmiany.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać pomoc w nawiązywania połączenia z bazą danych Azure dla serwera MySQL, [biblioteki połączeń dla bazy danych Azure dla programu MySQL](./concepts-connection-libraries.md)
