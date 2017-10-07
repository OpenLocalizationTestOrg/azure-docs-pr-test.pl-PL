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
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="73b71-104">Dostęp do źródła danych w obiektach z aplikacji logiki z bramą dane lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="73b71-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="73b71-105">źródła danych tooaccess lokalnie z aplikacji logiki, skonfiguruj bramę danych lokalnych, używanego przez aplikacje logiki z obsługiwanych łączników.</span><span class="sxs-lookup"><span data-stu-id="73b71-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="73b71-106">Witaj bramy działa jako mostka zapewnia transfer danych szybki i szyfrowanie między źródłami danych lokalnie i aplikacje logiki.</span><span class="sxs-lookup"><span data-stu-id="73b71-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="73b71-107">Brama Hello przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="73b71-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="73b71-108">Cały ruch pochodzi jako bezpieczny ruch wychodzący z hello bramy agenta.</span><span class="sxs-lookup"><span data-stu-id="73b71-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="73b71-109">Dowiedz się więcej o [działanie bramy danych hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="73b71-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="73b71-110">Brama Hello obsługuje źródeł danych toothese połączeń lokalnie:</span><span class="sxs-lookup"><span data-stu-id="73b71-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="73b71-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="73b71-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="73b71-112">DB2</span><span class="sxs-lookup"><span data-stu-id="73b71-112">DB2</span></span>  
*   <span data-ttu-id="73b71-113">System plików</span><span class="sxs-lookup"><span data-stu-id="73b71-113">File System</span></span>
*   <span data-ttu-id="73b71-114">Informix</span><span class="sxs-lookup"><span data-stu-id="73b71-114">Informix</span></span>
*   <span data-ttu-id="73b71-115">MQ</span><span class="sxs-lookup"><span data-stu-id="73b71-115">MQ</span></span>
*   <span data-ttu-id="73b71-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="73b71-116">MySQL</span></span>
*   <span data-ttu-id="73b71-117">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="73b71-117">Oracle Database</span></span>
*   <span data-ttu-id="73b71-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="73b71-118">PostgreSQL</span></span>
*   <span data-ttu-id="73b71-119">Serwer aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="73b71-119">SAP Application Server</span></span> 
*   <span data-ttu-id="73b71-120">Serwer komunikatów SAP</span><span class="sxs-lookup"><span data-stu-id="73b71-120">SAP Message Server</span></span>
*   <span data-ttu-id="73b71-121">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="73b71-121">SharePoint</span></span>
*   <span data-ttu-id="73b71-122">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="73b71-122">SQL Server</span></span>
*   <span data-ttu-id="73b71-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="73b71-123">Teradata</span></span>

<span data-ttu-id="73b71-124">Te kroki pokazują, jak tooset się hello lokalnymi toowork bramy danych z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="73b71-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="73b71-125">Aby uzyskać więcej informacji o obsługiwanych łączników, zobacz [łączniki dla usługi Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="73b71-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="73b71-126">Informacje o sposobie toouse hello bramy z innymi usługami zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="73b71-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="73b71-127">Microsoft Power BI lokalnej bramy danych</span><span class="sxs-lookup"><span data-stu-id="73b71-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="73b71-128">Azure bramy danych lokalnych usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="73b71-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="73b71-129">Brama danych lokalnych Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="73b71-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="73b71-130">Brama danych lokalnych PowerApps firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="73b71-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="73b71-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="73b71-131">Requirements</span></span>

* <span data-ttu-id="73b71-132">Użytkownik musi mieć już [zainstalowana brama danych hello na komputerze lokalnym](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="73b71-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="73b71-133">Po zarejestrowaniu toohello portalu Azure, masz toouse hello tej samej pracy lub szkołą konta, który został użyty zbyt[instalowanie bramy danych lokalne powitania](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="73b71-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="73b71-134">Twoje konto logowania musi mieć również toouse subskrypcji platformy Azure, podczas tworzenia zasobu bramy w portalu Azure hello instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="73b71-135">Instalacji bramy nie może być już żądane przez zasobów Azure bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="73b71-136">Możesz skojarzyć bramy instalacji tooonly jednej bramy Azure zasobu.</span><span class="sxs-lookup"><span data-stu-id="73b71-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="73b71-137">Oświadczenia odbywa się podczas tworzenia zasobu bramy hello, aby instalacja hello jest niedostępne dla innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="73b71-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="73b71-138">Konfigurowanie połączenia bramy danych hello</span><span class="sxs-lookup"><span data-stu-id="73b71-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="73b71-139">1. Instalowanie bramy danych lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="73b71-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="73b71-140">Jeśli nie jest jeszcze wykonaj hello [bramy danych lokalne powitania tooinstall kroki](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="73b71-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="73b71-141">Przed rozpoczęciem powitalne procedurą, upewnij się, zainstalować bramę danych hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="73b71-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="73b71-142">2. Tworzenie zasobu platformy Azure dla bramy danych lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="73b71-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="73b71-143">Po zainstalowaniu bramy hello na komputerze lokalnym, należy utworzyć bramy danych jako zasób w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="73b71-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="73b71-144">Ten krok powoduje również skojarzenie zasobu bramy z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73b71-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="73b71-145">Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="73b71-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="73b71-146">Upewnij się, toouse hello Azure służbowe lub służbowego adresu e-mail użytego tooinstall hello bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="73b71-147">W menu po lewej stronie powitania na platformie Azure, wybierz **nowy** > **integracji przedsiębiorstwa** > **bramy danych lokalnych** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="73b71-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Znajdź "brama lokalna dane"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="73b71-149">Na powitania **Utwórz bramę połączenia** bloku, podaj te szczegóły toocreate zasobu bramy danych:</span><span class="sxs-lookup"><span data-stu-id="73b71-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="73b71-150">**Nazwa**: Wprowadź nazwę dla zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="73b71-151">**Subskrypcja**: Wybierz hello tooassociate subskrypcji platformy Azure z zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="73b71-152">Ta subskrypcja powinna być hello tej samej subskrypcji co aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="73b71-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="73b71-153">Hello Domyślna subskrypcja jest oparta na powitania konto platformy Azure, który został użyty toosign w.</span><span class="sxs-lookup"><span data-stu-id="73b71-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="73b71-154">**Grupa zasobów**: Utwórz grupę zasobów lub wybierz istniejącą grupę zasobów podczas wdrażania zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="73b71-155">Grupy zasobów ułatwiają zarządzanie powiązane zasoby Azure jako kolekcja.</span><span class="sxs-lookup"><span data-stu-id="73b71-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="73b71-156">**Lokalizacja**: Azure ogranicza to toohello lokalizacji tego samego regionu, które zostały wybrane do hello usługi bramy w chmurze podczas [instalacja bramy](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="73b71-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="73b71-157">Upewnij się, że lokalizacja zasobu bramy hello odpowiada lokalizacji usługi w chmurze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="73b71-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="73b71-158">W przeciwnym razie instalacji bramy mogą nie być wyświetlane liście bram hello zainstalowany tooselect możesz w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="73b71-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="73b71-159">Dla zasobu bramy i aplikację logiki, można używać różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="73b71-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="73b71-160">**Nazwa instalacji**: Jeśli instalacji bramy nie została jeszcze wybrana, wybierz hello bramy, która została wcześniej zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="73b71-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="73b71-161">tooadd hello bramy zasobów tooyour pulpitu nawigacyjnego platformy Azure, wybierz **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="73b71-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="73b71-162">Gdy wszystko będzie gotowe, wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="73b71-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="73b71-163">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="73b71-163">For example:</span></span>

    ![Podaj szczegóły toocreate lokalnego centrum danych](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="73b71-165">toofind lub widok bramy danych w dowolnym momencie z hello Azure lewym menu głównego, przejdź zbyt **więcej usług** > **integracji przedsiębiorstwa** > **danych lokalnych Bram**.</span><span class="sxs-lookup"><span data-stu-id="73b71-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Przejdź za "Usługi więcej", "Enterprise integrację", "Bram danych lokalnych"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="73b71-167">3. Połączenie bramy danych lokalnych toohello aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="73b71-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="73b71-168">Teraz, utworzeniu zasobu brama danych i skojarzone z subskrypcją platformy Azure z tego zasobu, należy utworzyć połączenie między centrum danych i aplikacji hello logiki.</span><span class="sxs-lookup"><span data-stu-id="73b71-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="73b71-169">Lokalizacja połączenia bramy musi znajdować się w hello sam region jako aplikację logiki, ale można użyć bramy danych, który istnieje w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="73b71-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="73b71-170">W portalu Azure hello Utwórz lub Otwórz aplikację logiki w Projektancie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="73b71-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="73b71-171">Dodaj łącznik, który obsługuje połączenia lokalnego, takie jak SQL Server.</span><span class="sxs-lookup"><span data-stu-id="73b71-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="73b71-172">Następujące hello kolejności, wybierz **Połącz za pośrednictwem bramy danych lokalnych**, Podaj unikatową nazwę połączenia hello wymagane informacje i wybierz zasób bramy danych hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="73b71-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="73b71-173">Gdy wszystko będzie gotowe, wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="73b71-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="73b71-174">Nazwa połączenia unikatowy pomaga łatwo zidentyfikować to połączenie później, szczególnie w przypadku tworzenia wielu połączeń.</span><span class="sxs-lookup"><span data-stu-id="73b71-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="73b71-175">Jeśli to konieczne, należy również uwzględnić hello kwalifikowaną dla nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="73b71-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Utwórz połączenie między bramą logiki aplikacji i danych](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="73b71-177">Gratulujemy, połączenie bramy jest teraz gotowy do Twojej toouse aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="73b71-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="73b71-178">Edytuj ustawienia połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="73b71-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="73b71-179">Po utworzeniu połączenia bramy aplikacji logiki możesz toolater aktualizacji hello ustawienia dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="73b71-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="73b71-180">połączenie bramy hello toofind:</span><span class="sxs-lookup"><span data-stu-id="73b71-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="73b71-181">W bloku aplikacji logiki hello w obszarze **narzędzi programistycznych**, wybierz pozycję **połączenia interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="73b71-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="73b71-182">Witaj **połączenia interfejsu API** w okienku zostaną wyświetlone wszystkie połączenia interfejsu API skojarzone z aplikacji logiki, w tym połączenia bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Przejdź do aplikacji logiki tooyour, wybierz "Interfejsu API połączeń"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="73b71-184">Lub z hello Azure lewym menu głównego, przejdź zbyt **więcej usług** > **& sieci Web usługi Mobile Services** > **połączenia interfejsu API** w przypadku wszystkich połączeń interfejsu API takie jak połączenia bramy, które są skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73b71-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="73b71-185">Lub na hello Azure lewym menu głównego, przejdź zbyt**wszystkie zasoby** dla wszystkich połączeń interfejsu API, w tym połączenia bramy, które są skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73b71-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="73b71-186">Wybierz połączenie bramy hello tooview lub edycji i wybierz polecenie **połączenia Edytuj interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="73b71-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="73b71-187">Jeśli aktualizacje nie zostały wprowadzone, spróbuj [zatrzymanie i ponowne uruchomienie usługi systemu Windows hello bramy](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="73b71-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="73b71-188">Przełącz lub usunąć zasób lokalną bramy danych</span><span class="sxs-lookup"><span data-stu-id="73b71-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="73b71-189">toocreate zasób różnych bramy skojarzyć bramy z innego zasobu lub usunąć zasobów bramy hello, można usunąć zasobów bramy hello bez wpływu na powitania instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="73b71-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="73b71-190">Z hello Azure lewym menu głównego, przejdź zbyt**wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="73b71-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="73b71-191">Znajdź i zaznacz pozycję zasobu bramy danych.</span><span class="sxs-lookup"><span data-stu-id="73b71-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="73b71-192">Wybierz **bramy danych lokalnych**, a na pasku narzędzi zasobów hello, wybierz pozycję **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="73b71-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="73b71-193">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="73b71-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="73b71-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73b71-194">Next steps</span></span>

* [<span data-ttu-id="73b71-195">Zabezpieczanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="73b71-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="73b71-196">Typowe przykłady i scenariusze dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="73b71-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
