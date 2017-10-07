---
title: "aaaCreate, link, usunąć lub przenieść konta integracji w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Sposób integracji toocreate konta, a następnie połącz go tooyour logic apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>Co to jest konto integracji?

Konta integracji umożliwia aplikacjom integracji przedsiębiorstwa artefaktów toomanage, w tym schematów, map, certyfikaty, partnerzy i umów. Dowolną aplikację integracji, które możesz utworzyć używa tooaccess konta integracji tych schematów, map, certyfikaty i tak dalej.

## <a name="create-an-integration-account"></a>Tworzenie konta usługi integracji

1.  Zaloguj się toohello [portalu Azure](http://portal.azure.com "portalu Azure"). Wybierz z menu po lewej stronie powitania **więcej usług**.

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. W polu wyszukiwania hello wpisz "Integracja" filtru. Na liście wyników hello, wybierz **konta integracji**.

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. U góry hello hello strony, wybierz **Dodaj**.

    ![Wybierz opcję Dodaj](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Nadaj nazwę swojego konta integracji i wybierz hello subskrypcji platformy Azure, które mają toouse. Możesz utworzyć nową **grupy zasobów** lub wybierz istniejącą grupę zasobów. Następnie wybierz **lokalizacji** dla Twojego konta integracji hostingu i **warstwy cenowej**. 

    Gdy wszystko jest gotowe, wybierz pozycję **Utwórz**.

    ![Podaj szczegóły konta integracji](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure udostępnia konta integracji w lokalizacji hello wybrany powinno zakończyć się w ciągu 1 minuty.

5. Odśwież stronę hello. Widzisz konta integracji na liście.

    ![Pojawi się nowego konta integracji](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Następnie połącz konto integracji hello za ten zostanie utworzony tooyour aplikacji logiki. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Łączenie aplikacji logiki tooa konta integracji

toogive aplikacje logiki dostępu toomaps, schematów, umów oraz pozostałych artefaktów na koncie integracji aplikacji logiki tooyour konta integracji hello łącza.

### <a name="prerequisites"></a>Wymagania wstępne

* Konta integracji
* Aplikacji logiki

> [!NOTE] 
> Upewnij się, że integracja aplikacji logiki i konta znajdują się w hello *tej samej lokalizacji platformy Azure* przed rozpoczęciem.


1. W hello portalu Azure wybierz aplikację logiki i sprawdź lokalizację aplikację logiki.

    ![Wybierz aplikację logiki, sprawdź lokalizację](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. W obszarze **ustawienia**, wybierz pozycję **konta integracji**.

    ![Wybierz opcję "Konto Integration"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. Z hello **wybierz konto integracji** listy, wybierz hello integracji konta toolink tooyour logiki aplikacji. Wybierz toofinish połączeń, **zapisać**.

    ![Wybierz konto integracji](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Otrzymasz powiadomienie, które pokazuje integracją konta jest tooyour połączonej aplikacji logiki, a wszystkie artefakty na koncie integracji są teraz dostępne tooyour aplikacji logiki.

    ![Aplikację logiki jest połączony tooyour konta integracji](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Teraz, Twoje konto integracji jest tooyour połączonej aplikacji logiki, można użyć łączników hello B2B w aplikacjach logiki. Niektóre typowe łączniki B2B obejmują sprawdzanie poprawności kodu XML i pliku prostego kodowania/dekodowania.  

## <a name="delete-your-integration-account"></a>Usuwanie konta integracji

1. Wybierz **więcej usług**.

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. W polu wyszukiwania hello wpisz "Integracja" filtru. Na liście wyników hello, wybierz **konta integracji**.

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Wybierz konto integracji hello, które mają toodelete.

    ![Wybierz toodelete konta integracji](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. W hello menu wybierz **usunąć**.

    ![Wybierz pozycję "Delete"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Potwierdź konto integracji hello choice toodelete.

## <a name="move-your-integration-account"></a>Przenoszenie konta integracji

toomove integracji tooanother konta Azure subskrypcji lub grupy zasobów, wykonaj następujące kroki.

> [!IMPORTANT]
> Należy zaktualizować wszystkie skrypty toouse hello nowy zasób identyfikatory po przeniesieniu konta integracji.

1. Wybierz **więcej usług**.

    ![Wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. W polu wyszukiwania hello wpisz "Integracja" filtru. Na liście wyników hello, wybierz **konta integracji**.

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Wybierz konto integracji hello, które mają toomove. W obszarze **ustawienia**, wybierz **właściwości**.

    ![Wybierz toomove konta integracji. W obszarze Ustawienia wybierz polecenie Właściwości](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Zmień hello grupy zasobów lub subskrypcji platformy Azure, który został skojarzony z Twoim kontem integracji.

    ![Wybierz opcję Zmień grupę zasobów lub zmiany subskrypcji](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej na temat umów](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  

