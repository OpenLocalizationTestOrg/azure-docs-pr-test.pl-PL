---
title: "tooretain aaaHow stałej wirtualnego adresu IP dla usługi w chmurze platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zmienić nie tooensure, który hello wirtualny adres IP (VIP) usługi w chmurze Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Zachowaj stałej wirtualnego adresu IP dla usługi w chmurze Azure
Po zaktualizowaniu usługi w chmurze, która jest hostowana na platformie Azure, może być konieczne tooensure, która hello wirtualnego adresu IP (VIP) usługi hello nie ulega zmianie. Wiele usług zarządzania domeny używa hello systemu nazw domen (DNS) do rejestracji nazw domen. DNS działa tylko wtedy, gdy pozostaje hello VIP hello takie same. Można użyć hello **Kreator publikowania** w tooensure narzędzi Azure, która hello VIP usługi w chmurze nie ulega zmianie podczas aktualizacji. Aby uzyskać więcej informacji na temat zarządzania domeny DNS toouse usług w chmurze, zobacz [Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Publikowanie usługi w chmurze bez zmieniania ich adresów VIP
Hello VIP usługi w chmurze jest przydzielony wdrażając najpierw go tooAzure w określonym środowisku, takich jak hello środowiska produkcyjnego. Witaj VIP zmiany tylko wtedy, gdy jawnie usunąć wdrożenie hello lub wdrożenie hello jest niejawnie usunięte przez wdrożenie hello aktualizacji procesu. tooretain hello VIP, nie można usuwać wdrożenia, a użytkownik powinien upewnić się, że program Visual Studio nie powoduje usunięcia wdrożenia automatycznie. 

Można określić ustawienia wdrażania w hello **Kreator publikowania**, który obsługuje kilka opcji wdrażania. Można określić świeże wdrożenie lub wdrażanie aktualizacji przyrostowych lub jednocześnie. Oba rodzaje wdrożenia aktualizacji zachować hello VIP. Definicje różnego typu wdrożenia, zobacz [Kreator publikowania aplikacji Azure](vs-azure-tools-publish-azure-application-wizard.md). Ponadto można kontrolować, czy hello poprzedniego wdrożenia usługi w chmurze jest usuwana, jeśli wystąpi błąd. Jeśli ta opcja nie ustawiony prawidłowo, hello wirtualne adresy IP mogą ulec zmianie nieoczekiwanie.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Aktualizowanie usługi w chmurze bez zmieniania ich adresów VIP
1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio. 

2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello projektu. Menu skrótów hello, wybierz **publikowania**.

    ![Menu Publikowanie](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. W hello **publikowanie aplikacji platformy Azure** okno dialogowe, wybierz hello toowhich subskrypcji platformy Azure ma toodeploy. Zarejestruj się, jeśli to konieczne i wybierz pozycję **dalej**.

    ![Publikowanie Azure aplikacji stronę logowania](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. Na powitania **typowe ustawienia** karcie, upewnij się, że nazwa hello toowhich usługi chmury hello jest wdrażany, hello **środowiska**, hello **konfiguracji kompilacji**i hello **Konfiguracji usługi** są wszystkie prawidłowe.

    ![Publikowanie kartę typowe ustawienia aplikacji Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Na powitania **Zaawansowane ustawienia** karcie, upewnij się, że hello **etykieta wdrożenia** i hello **konta magazynu** są poprawne. Sprawdź, że hello **usunąć wdrożenie w przypadku niepowodzenia** pole wyboru jest wyczyszczone, a następnie sprawdź, że hello **aktualizację wdrożenia** pole wyboru jest zaznaczone. Przez wyczyszczenie hello **usunąć wdrożenie w przypadku niepowodzenia** pole wyboru upewnieniu się, że sieci wirtualne adresy IP nie jest utracone, jeśli wystąpi błąd podczas wdrażania. Po wybraniu hello **aktualizację wdrożenia** pole wyboru, należy upewnić wdrożenia nie jest usuwany, a Twoje VIP utratę przy ponownym publikowania aplikacji. 

    ![Publikowanie kartę Zaawansowane ustawienia aplikacji Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther określ w jaki sposób toobe ról hello aktualizacji, zaznacz **ustawienia** dalej zbyt**aktualizację wdrożenia**. Wybierz opcję **aktualizacji przyrostowej** lub **jednoczesne aktualizowanie**i wybierz **OK**. Wybierz **aktualizacji przyrostowej** tooupdate każdego wystąpienia aplikacji, po kolei, tak że hello aplikacji jest zawsze dostępna. Wybierz **jednoczesne aktualizowanie** tooupdate wszystkich wystąpień aplikacji hello — w tym samym czasie. Jednoczesne aktualizowanie jest szybsze, ale z usługą mogą być niedostępne podczas procesu aktualizacji hello. Gdy skończysz, wybierz **dalej**.

    ![Publikowanie strony Ustawienia wdrożenia aplikacji Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. W hello **publikowanie aplikacji platformy Azure** okno dialogowe, wybierz opcję **dalej** do hello **Podsumowanie** zostanie wyświetlona strona. Sprawdź ustawienia, a następnie wybierz **publikowania**.
   
    ![Publikowanie na stronie Podsumowanie aplikacji Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Następne kroki
- [Za pomocą programu Visual Studio Azure Kreator publikowania aplikacji hello](vs-azure-tools-publish-azure-application-wizard.md)

