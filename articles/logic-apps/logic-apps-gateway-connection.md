---
title: "aaaAccess źródeł danych na lokalnym dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Konfigurowanie bramy danych lokalne powitania dostępu do źródeł danych w obiektach z aplikacji logiki"
keywords: "dostęp do danych lokalnych, transfer danych, szyfrowania, źródła danych"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Dostęp do źródła danych w obiektach z aplikacji logiki z bramą dane lokalne powitania

źródła danych tooaccess lokalnie z aplikacji logiki, skonfiguruj bramę danych lokalnych, używanego przez aplikacje logiki z obsługiwanych łączników. Witaj bramy działa jako mostka zapewnia transfer danych szybki i szyfrowanie między źródłami danych lokalnie i aplikacje logiki. Brama Hello przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą hello Azure Service Bus. Cały ruch pochodzi jako bezpieczny ruch wychodzący z hello bramy agenta. Dowiedz się więcej o [działanie bramy danych hello](logic-apps-gateway-install.md#gateway-cloud-service). 

Brama Hello obsługuje źródeł danych toothese połączeń lokalnie:

*   BizTalk Server 2016
*   DB2  
*   System plików
*   Informix
*   MQ
*   MySQL
*   Baza danych Oracle
*   PostgreSQL
*   Serwer aplikacji SAP 
*   Serwer komunikatów SAP
*   Sharepoint
*   Oprogramowanie SQL Server
*   Teradata

Te kroki pokazują, jak tooset się hello lokalnymi toowork bramy danych z aplikacji logiki. Aby uzyskać więcej informacji o obsługiwanych łączników, zobacz [łączniki dla usługi Azure Logic Apps](../connectors/apis-list.md). 

Informacje o sposobie toouse hello bramy z innymi usługami zobacz następujące artykuły:

*   [Microsoft Power BI lokalnej bramy danych](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure bramy danych lokalnych usług Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Brama danych lokalnych Flow firmy Microsoft](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Brama danych lokalnych PowerApps firmy Microsoft](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Wymagania

* Użytkownik musi mieć już [zainstalowana brama danych hello na komputerze lokalnym](logic-apps-gateway-install.md).

* Po zarejestrowaniu toohello portalu Azure, masz toouse hello tej samej pracy lub szkołą konta, który został użyty zbyt[instalowanie bramy danych lokalne powitania](logic-apps-gateway-install.md#requirements). Twoje konto logowania musi mieć również toouse subskrypcji platformy Azure, podczas tworzenia zasobu bramy w portalu Azure hello instalacji bramy.

* Instalacji bramy nie może być już żądane przez zasobów Azure bramy. Możesz skojarzyć bramy instalacji tooonly jednej bramy Azure zasobu. Oświadczenia odbywa się podczas tworzenia zasobu bramy hello, aby instalacja hello jest niedostępne dla innych zasobów.

## <a name="set-up-hello-data-gateway-connection"></a>Konfigurowanie połączenia bramy danych hello

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Instalowanie bramy danych lokalne powitania

Jeśli nie jest jeszcze wykonaj hello [bramy danych lokalne powitania tooinstall kroki](logic-apps-gateway-install.md). Przed rozpoczęciem powitalne procedurą, upewnij się, zainstalować bramę danych hello na komputerze lokalnym.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Tworzenie zasobu platformy Azure dla bramy danych lokalne powitania

Po zainstalowaniu bramy hello na komputerze lokalnym, należy utworzyć bramy danych jako zasób w systemie Azure. Ten krok powoduje również skojarzenie zasobu bramy z subskrypcją platformy Azure.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure"). Upewnij się, toouse hello Azure służbowe lub służbowego adresu e-mail użytego tooinstall hello bramy.

2. W menu po lewej stronie powitania na platformie Azure, wybierz **nowy** > **integracji przedsiębiorstwa** > **bramy danych lokalnych** w sposób pokazany poniżej:

   ![Znajdź "brama lokalna dane"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Na powitania **Utwórz bramę połączenia** bloku, podaj te szczegóły toocreate zasobu bramy danych:

    * **Nazwa**: Wprowadź nazwę dla zasobu bramy. 

    * **Subskrypcja**: Wybierz hello tooassociate subskrypcji platformy Azure z zasobu bramy. 
    Ta subskrypcja powinna być hello tej samej subskrypcji co aplikację logiki.
   
      Hello Domyślna subskrypcja jest oparta na powitania konto platformy Azure, który został użyty toosign w.

    * **Grupa zasobów**: Utwórz grupę zasobów lub wybierz istniejącą grupę zasobów podczas wdrażania zasobu bramy. 
    Grupy zasobów ułatwiają zarządzanie powiązane zasoby Azure jako kolekcja.

    * **Lokalizacja**: Azure ogranicza to toohello lokalizacji tego samego regionu, które zostały wybrane do hello usługi bramy w chmurze podczas [instalacja bramy](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Upewnij się, że lokalizacja zasobu bramy hello odpowiada lokalizacji usługi w chmurze bramy hello. W przeciwnym razie instalacji bramy mogą nie być wyświetlane liście bram hello zainstalowany tooselect możesz w następnym kroku hello.
      > 
      > Dla zasobu bramy i aplikację logiki, można używać różnych regionach.

    * **Nazwa instalacji**: Jeśli instalacji bramy nie została jeszcze wybrana, wybierz hello bramy, która została wcześniej zainstalowana. 

    tooadd hello bramy zasobów tooyour pulpitu nawigacyjnego platformy Azure, wybierz **toodashboard numeru Pin**. 
    Gdy wszystko będzie gotowe, wybierz pozycję **Utwórz**.

    Na przykład:

    ![Podaj szczegóły toocreate lokalnego centrum danych](./media/logic-apps-gateway-connection/createblade.png)

    toofind lub widok bramy danych w dowolnym momencie z hello Azure lewym menu głównego, przejdź zbyt **więcej usług** > **integracji przedsiębiorstwa** > **danych lokalnych Bram**.

    ![Przejdź za "Usługi więcej", "Enterprise integrację", "Bram danych lokalnych"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Połączenie bramy danych lokalnych toohello aplikacji logiki

Teraz, utworzeniu zasobu brama danych i skojarzone z subskrypcją platformy Azure z tego zasobu, należy utworzyć połączenie między centrum danych i aplikacji hello logiki.

> [!NOTE]
> Lokalizacja połączenia bramy musi znajdować się w hello sam region jako aplikację logiki, ale można użyć bramy danych, który istnieje w innym regionie.

1. W portalu Azure hello Utwórz lub Otwórz aplikację logiki w Projektancie aplikacji logiki.

2. Dodaj łącznik, który obsługuje połączenia lokalnego, takie jak SQL Server.

3. Następujące hello kolejności, wybierz **Połącz za pośrednictwem bramy danych lokalnych**, Podaj unikatową nazwę połączenia hello wymagane informacje i wybierz zasób bramy danych hello, które mają toouse. Gdy wszystko będzie gotowe, wybierz pozycję **Utwórz**.

   > [!TIP]
   > Nazwa połączenia unikatowy pomaga łatwo zidentyfikować to połączenie później, szczególnie w przypadku tworzenia wielu połączeń. Jeśli to konieczne, należy również uwzględnić hello kwalifikowaną dla nazwy użytkownika. 

   ![Utwórz połączenie między bramą logiki aplikacji i danych](./media/logic-apps-gateway-connection/blankconnection.png)

Gratulujemy, połączenie bramy jest teraz gotowy do Twojej toouse aplikacji logiki.

## <a name="edit-your-gateway-connection-settings"></a>Edytuj ustawienia połączenia bramy

Po utworzeniu połączenia bramy aplikacji logiki możesz toolater aktualizacji hello ustawienia dla tego połączenia.

1. połączenie bramy hello toofind:

   * W bloku aplikacji logiki hello w obszarze **narzędzi programistycznych**, wybierz pozycję **połączenia interfejsu API**. 
   
     Witaj **połączenia interfejsu API** w okienku zostaną wyświetlone wszystkie połączenia interfejsu API skojarzone z aplikacji logiki, w tym połączenia bramy.

     ![Przejdź do aplikacji logiki tooyour, wybierz "Interfejsu API połączeń"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Lub z hello Azure lewym menu głównego, przejdź zbyt **więcej usług** > **& sieci Web usługi Mobile Services** > **połączenia interfejsu API** w przypadku wszystkich połączeń interfejsu API takie jak połączenia bramy, które są skojarzone z subskrypcją platformy Azure. 

   * Lub na hello Azure lewym menu głównego, przejdź zbyt**wszystkie zasoby** dla wszystkich połączeń interfejsu API, w tym połączenia bramy, które są skojarzone z subskrypcją platformy Azure.

2. Wybierz połączenie bramy hello tooview lub edycji i wybierz polecenie **połączenia Edytuj interfejsu API**.

   > [!TIP]
   > Jeśli aktualizacje nie zostały wprowadzone, spróbuj [zatrzymanie i ponowne uruchomienie usługi systemu Windows hello bramy](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Przełącz lub usunąć zasób lokalną bramy danych

toocreate zasób różnych bramy skojarzyć bramy z innego zasobu lub usunąć zasobów bramy hello, można usunąć zasobów bramy hello bez wpływu na powitania instalacji bramy. 

1. Z hello Azure lewym menu głównego, przejdź zbyt**wszystkie zasoby**. 
2. Znajdź i zaznacz pozycję zasobu bramy danych.
3. Wybierz **bramy danych lokalnych**, a na pasku narzędzi zasobów hello, wybierz pozycję **usunąć**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Często zadawane pytania

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Następne kroki

* [Zabezpieczanie aplikacji logiki](./logic-apps-securing-a-logic-app.md)
* [Typowe przykłady i scenariusze dla usługi logic apps](./logic-apps-examples-and-scenarios.md)
