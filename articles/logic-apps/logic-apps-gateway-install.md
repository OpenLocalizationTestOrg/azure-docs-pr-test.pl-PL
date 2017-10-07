---
title: "Brama danych lokalnych aaaInstall — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Aby uzyskać dostęp do źródła danych na lokalnym, instalowanie bramy danych lokalnych hello transferu danych szybki i szyfrowania między źródłami danych lokalnie i logic apps"
keywords: "dostęp do danych lokalnych, transfer danych, szyfrowania, źródła danych"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="cca8a-104">Instalowanie bramy danych lokalne powitania dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="cca8a-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="cca8a-105">Aplikacje logiki uzyskania dostępu do źródeł danych lokalnie, należy zainstalować i skonfigurować bramę danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="cca8a-106">Witaj bramy działa jako mostka zapewnia transfer danych szybki i szyfrowania między systemami lokalnymi i aplikacje logiki.</span><span class="sxs-lookup"><span data-stu-id="cca8a-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="cca8a-107">Brama Hello przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cca8a-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="cca8a-108">Cały ruch pochodzi jako bezpieczny ruch wychodzący z hello bramy agenta.</span><span class="sxs-lookup"><span data-stu-id="cca8a-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="cca8a-109">Dowiedz się więcej o [działanie bramy danych hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cca8a-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="cca8a-110">Brama Hello obsługuje źródeł danych toothese połączeń lokalnie:</span><span class="sxs-lookup"><span data-stu-id="cca8a-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="cca8a-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="cca8a-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="cca8a-112">DB2</span><span class="sxs-lookup"><span data-stu-id="cca8a-112">DB2</span></span>  
*   <span data-ttu-id="cca8a-113">System plików</span><span class="sxs-lookup"><span data-stu-id="cca8a-113">File System</span></span>
*   <span data-ttu-id="cca8a-114">Informix</span><span class="sxs-lookup"><span data-stu-id="cca8a-114">Informix</span></span>
*   <span data-ttu-id="cca8a-115">MQ</span><span class="sxs-lookup"><span data-stu-id="cca8a-115">MQ</span></span>
*   <span data-ttu-id="cca8a-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="cca8a-116">MySQL</span></span>
*   <span data-ttu-id="cca8a-117">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="cca8a-117">Oracle Database</span></span>
*   <span data-ttu-id="cca8a-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cca8a-118">PostgreSQL</span></span>
*   <span data-ttu-id="cca8a-119">Serwer aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="cca8a-119">SAP Application Server</span></span> 
*   <span data-ttu-id="cca8a-120">Serwer komunikatów SAP</span><span class="sxs-lookup"><span data-stu-id="cca8a-120">SAP Message Server</span></span>
*   <span data-ttu-id="cca8a-121">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="cca8a-121">SharePoint</span></span>
*   <span data-ttu-id="cca8a-122">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="cca8a-122">SQL Server</span></span>
*   <span data-ttu-id="cca8a-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="cca8a-123">Teradata</span></span>

<span data-ttu-id="cca8a-124">Te kroki pokazują, jak toofirst hello instalacji lokalnej bramy danych przed [skonfigurować połączenie między bramą hello i aplikacje logiki](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="cca8a-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="cca8a-125">Aby uzyskać więcej informacji o obsługiwanych łączników, zobacz [łączniki dla usługi Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="cca8a-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="cca8a-126">Informacje o sposobie toouse hello bramy z innymi usługami zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="cca8a-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="cca8a-127">Microsoft Power BI lokalnej bramy danych</span><span class="sxs-lookup"><span data-stu-id="cca8a-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="cca8a-128">Azure bramy danych lokalnych usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cca8a-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="cca8a-129">Brama danych lokalnych Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="cca8a-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="cca8a-130">Brama danych lokalnych PowerApps firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="cca8a-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="cca8a-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="cca8a-131">Requirements</span></span>

<span data-ttu-id="cca8a-132">**Co najmniej**:</span><span class="sxs-lookup"><span data-stu-id="cca8a-132">**Minimum**:</span></span>

* <span data-ttu-id="cca8a-133">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="cca8a-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="cca8a-134">64-bitowej wersji systemu Windows 7 lub Windows Server 2008 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="cca8a-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="cca8a-135">**Zalecane**:</span><span class="sxs-lookup"><span data-stu-id="cca8a-135">**Recommended**:</span></span>

* <span data-ttu-id="cca8a-136">8 rdzeni procesora CPU</span><span class="sxs-lookup"><span data-stu-id="cca8a-136">8 Core CPU</span></span>
* <span data-ttu-id="cca8a-137">8 GB pamięci</span><span class="sxs-lookup"><span data-stu-id="cca8a-137">8 GB Memory</span></span>
* <span data-ttu-id="cca8a-138">64-bitowej wersji systemu Windows 2012 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="cca8a-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="cca8a-139">**Ważne uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="cca8a-139">**Important considerations**:</span></span>

* <span data-ttu-id="cca8a-140">Instalowanie bramy danych lokalne powitania tylko na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="cca8a-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="cca8a-141">Witaj bramy nie można zainstalować na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="cca8a-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="cca8a-142">Nie masz tooinstall hello bramy na powitania tego samego komputera jako źródła danych.</span><span class="sxs-lookup"><span data-stu-id="cca8a-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="cca8a-143">Opóźnienie toominimize, możesz zainstalować bramę hello jak jako źródło danych możliwe tooyour lub na powitania sam komputera, przy założeniu, że użytkownik ma uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="cca8a-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="cca8a-144">Nie należy instalować na komputerze, który zostanie wyłączony, toosleep czy też nie połączyć toohello Internet, ponieważ hello bramy nie można uruchomić w tych warunkach hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="cca8a-145">Ponadto w sieci bezprzewodowej może pogorszyć wydajność bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="cca8a-146">Podczas instalacji, należy się zalogować przy użyciu [konto służbowe](https://docs.microsoft.com/azure/active-directory/sign-up-organization) zarządzanym przez usługę Azure Active Directory (Azure AD), nie konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cca8a-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="cca8a-147">Masz toouse hello służbowe lub szkolne, konto później w hello Azure portal podczas tworzenia i skojarzyć z instalacją bramy zasobów bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="cca8a-148">Podczas tworzenia połączenia hello między logiki aplikacji i hello lokalnego źródła danych, następnie wybierz tego zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="cca8a-149">Dlaczego należy używać Praca usługi Azure AD lub konta służbowego?</span><span class="sxs-lookup"><span data-stu-id="cca8a-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="cca8a-150">Jeśli konta dla oferty usługi Office 365, a nie dostarczył rzeczywiste służbowego adresu e-mail, adresu logowania może wyglądać jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cca8a-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="cca8a-151">Jeśli masz istniejącą bramę skonfigurowanego z Instalatorem, która jest starsza niż wersja 14.16.6317.4, nie można zmienić lokalizacji bramy sieci przez uruchomione hello najnowszą wersję Instalatora.</span><span class="sxs-lookup"><span data-stu-id="cca8a-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="cca8a-152">Jednak można użyć hello najnowsze Instalator tooset się nową bramę z lokalizacją hello, który chcesz zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="cca8a-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="cca8a-153">Jeśli Instalator bramy, która jest starsza niż wersja 14.16.6317.4, ale nie zostały zainstalowane bramy można jeszcze miejsca, pobranie i użycie hello najnowszą wersję Instalatora.</span><span class="sxs-lookup"><span data-stu-id="cca8a-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="cca8a-154">Instalowanie bramy danych hello</span><span class="sxs-lookup"><span data-stu-id="cca8a-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="cca8a-155">[Pobierz i uruchom Instalatora bramy hello na komputerze lokalnym](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cca8a-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="cca8a-156">Przeczytaj i zaakceptuj postanowienia hello instrukcji użycia i ochrony prywatności.</span><span class="sxs-lookup"><span data-stu-id="cca8a-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="cca8a-157">Określ ścieżkę hello na komputerze lokalnym, w którym ma tooinstall hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="cca8a-158">Po wyświetleniu monitu zaloguj się przy użyciu konta służbowego, nie konta Microsoft Azure pracy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Zaloguj się przy użyciu pracy Azure lub konta służbowego](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="cca8a-160">Zarejestruj teraz zainstalowana brama hello [usługi bramy w chmurze](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cca8a-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="cca8a-161">Wybierz **zarejestrować nową bramę na tym komputerze**.</span><span class="sxs-lookup"><span data-stu-id="cca8a-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="cca8a-162">usługi w chmurze bramy Hello są szyfrowane i przechowywane poświadczenia źródła danych, a szczegóły bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="cca8a-163">Usługa Hello również kieruje zapytań i ich wyników między aplikację logiki, brama danych lokalne powitania i źródła danych lokalnie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="cca8a-164">Podaj nazwę dla tej instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="cca8a-165">Twórz klucza odzyskiwania, a następnie potwierdź klucz odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="cca8a-166">Klucz odzyskiwania musi zawierać co najmniej osiem znaków.</span><span class="sxs-lookup"><span data-stu-id="cca8a-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="cca8a-167">Upewnij się, zapisywanie i hello klucz należy przechowywać w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="cca8a-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="cca8a-168">Należy również ten klucz należy toomigrate, przywracania, lub Przejmij istniejącą bramę.</span><span class="sxs-lookup"><span data-stu-id="cca8a-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="cca8a-169">Wybierz toochange hello domyślnego regionu hello usługi bramy w chmurze i używanych w danej instalacji bramy usługi Azure Service Bus **Region zmiany**.</span><span class="sxs-lookup"><span data-stu-id="cca8a-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Zmiana regionu](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="cca8a-171">Witaj domyślnego regionu jest hello regionu skojarzonego z dzierżawą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cca8a-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="cca8a-172">Otwórz hello na powitania następne okienko **wybierz Region** zbyt wybierz inny region.</span><span class="sxs-lookup"><span data-stu-id="cca8a-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Wybierz inny region](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="cca8a-174">Na przykład użytkownik może wybrać hello tym samym regionie co aplikację logiki lub hello wybierz region najbliższy tooyour lokalne na dane źródło, aby ograniczyć czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="cca8a-175">Bramy aplikacji logiki i zasobów mogą mieć różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="cca8a-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="cca8a-176">Ten region nie można zmienić po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="cca8a-176">You can't change this region after installation.</span></span> <span data-ttu-id="cca8a-177">Ten region również określa i ogranicza lokalizacji hello umożliwiającego utworzenie hello zasobów platformy Azure dla bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="cca8a-178">Dlatego podczas tworzenia zasobu bramy na platformie Azure, upewnij się, czy lokalizacja zasobu hello zgodna hello regionie, który został wybrany podczas instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="cca8a-179">Jeśli chcesz toouse inny region bramy później, należy skonfigurować nową bramę.</span><span class="sxs-lookup"><span data-stu-id="cca8a-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="cca8a-180">Gdy wszystko jest gotowe, wybierz pozycję **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="cca8a-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="cca8a-181">Teraz, można więc, wykonaj następujące kroki w portalu Azure hello [tworzenie zasobów platformy Azure dla bramy](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="cca8a-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="cca8a-182">Dowiedz się więcej o [działanie bramy danych hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cca8a-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="cca8a-183">Migracja, Przywróć lub Przejmij na istniejącą bramę</span><span class="sxs-lookup"><span data-stu-id="cca8a-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="cca8a-184">tooperform te zadania, musi mieć hello klucza odzyskiwania, który został określony podczas hello brama została zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="cca8a-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="cca8a-185">Z menu Start komputera, wybierz **bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="cca8a-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="cca8a-186">Po hello Instalator zostanie otwarta, zaloguj się przy użyciu hello sam Azure pracy lub konta służbowego, który był wcześniej używany tooinstall hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="cca8a-187">Wybierz **migracji, Przywróć lub Przejmij istniejącą bramę**.</span><span class="sxs-lookup"><span data-stu-id="cca8a-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="cca8a-188">Podaj nazwę i odzyskiwania klucz hello bramy hello, który ma być toomigrate, przywracania lub podejmij za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="cca8a-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="cca8a-189">Ponownie uruchom bramę hello</span><span class="sxs-lookup"><span data-stu-id="cca8a-189">Restart hello gateway</span></span>

<span data-ttu-id="cca8a-190">Witaj bramy działa jako usługa systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cca8a-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="cca8a-191">Podobnie jak inne usługi systemu Windows należy uruchomić i zatrzymać usługi hello na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="cca8a-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="cca8a-192">Można na przykład, otwórz wiersz polecenia z podwyższonym poziomem uprawnień na komputerze hello gdzie hello brama jest uruchomiona i uruchom obu tych poleceń:</span><span class="sxs-lookup"><span data-stu-id="cca8a-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="cca8a-193">toostop hello usługi, uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="cca8a-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="cca8a-194">toostart hello usługi, uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="cca8a-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="cca8a-195">Konto usługi systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cca8a-195">Windows service account</span></span>

<span data-ttu-id="cca8a-196">Brama danych lokalne powitania skonfigurowano toouse `NT SERVICE\PBIEgwService` dla systemu Windows hello usługi poświadczeń logowania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="cca8a-197">Domyślnie hello bramy ma prawo "Zaloguj jako usługa" hello maszyny hello zainstalowanym hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="cca8a-198">Konto usługi Windows Hello różni się od hello konto używane do łączenia tooon lokalnych źródeł danych oraz hello Azure pracy lub konto służbowe używane toosign w usługach toocloud.</span><span class="sxs-lookup"><span data-stu-id="cca8a-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="cca8a-199">Konfigurowanie zapory lub serwera proxy</span><span class="sxs-lookup"><span data-stu-id="cca8a-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="cca8a-200">Brama Hello tworzy połączeń wychodzących za [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="cca8a-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="cca8a-201">informacje o serwerze proxy tooprovide bramy, zobacz [Skonfiguruj ustawienia serwera proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="cca8a-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="cca8a-202">toocheck czy zapory lub serwera proxy, może zablokować połączenia, upewnij się, czy komputer faktycznie można łączyć z toohello internet i hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="cca8a-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="cca8a-203">Uruchom to polecenie z wiersza polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cca8a-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="cca8a-204">To polecenie tylko testy, łączności sieciowej i toohello łączność usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cca8a-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="cca8a-205">Dzięki hello polecenia nie ma niczego toodo hello bramy lub hello bramy usługi w chmurze są szyfrowane i przechowywane poświadczenia i szczegóły bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="cca8a-206">Ponadto to polecenie jest tylko dostępne w systemie Windows Server 2012 R2 lub nowszy oraz Windows 8.1 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="cca8a-207">We wcześniejszych wersjach systemu operacyjnego, można użyć programu Telnet zbyt przetestować połączenia.</span><span class="sxs-lookup"><span data-stu-id="cca8a-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="cca8a-208">Dowiedz się więcej o [Azure Service Bus i hybrydowe rozwiązania](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="cca8a-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="cca8a-209">Wyniki powinny wyglądać podobny przykład toothis:</span><span class="sxs-lookup"><span data-stu-id="cca8a-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="cca8a-210">Jeśli **TcpTestSucceeded** nie ustawiono zbyt**True**, może zostać zablokowany przez zaporę.</span><span class="sxs-lookup"><span data-stu-id="cca8a-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="cca8a-211">Jeśli toobe kompleksowe, należy zastąpić hello **ComputerName** i **portu** wartości z wartościami hello wymienione w obszarze [skonfigurować porty](#configure-ports) w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="cca8a-212">Hello Zapora może również blokować połączeń, że powitalne Azure Service Bus udostępnia toohello centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cca8a-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="cca8a-213">W przypadku tego scenariusza należy zatwierdzić (odblokuj) hello wszystkie adresy IP dla tych centrach danych w danym regionie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="cca8a-214">Dla tych adresów IP [get hello Azure listy adresów IP w tym miejscu](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="cca8a-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="cca8a-215">Skonfiguruj porty</span><span class="sxs-lookup"><span data-stu-id="cca8a-215">Configure ports</span></span>

<span data-ttu-id="cca8a-216">Brama Hello tworzy połączeń wychodzących za[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) i komunikuje się portów wychodzących: TCP 443 (ustawienie domyślne), 5671, 5672, 9350 za pośrednictwem 9354.</span><span class="sxs-lookup"><span data-stu-id="cca8a-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="cca8a-217">Witaj bramy nie wymaga portów przychodzących.</span><span class="sxs-lookup"><span data-stu-id="cca8a-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="cca8a-218">Dowiedz się więcej o [Azure Service Bus i hybrydowe rozwiązania](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="cca8a-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="cca8a-219">NAZWY DOMEN</span><span class="sxs-lookup"><span data-stu-id="cca8a-219">DOMAIN NAMES</span></span> | <span data-ttu-id="cca8a-220">PORTY WYJŚCIOWE</span><span class="sxs-lookup"><span data-stu-id="cca8a-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="cca8a-221">OPIS</span><span class="sxs-lookup"><span data-stu-id="cca8a-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cca8a-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="cca8a-222">*.analysis.windows.net</span></span> | <span data-ttu-id="cca8a-223">443</span><span class="sxs-lookup"><span data-stu-id="cca8a-223">443</span></span> | <span data-ttu-id="cca8a-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="cca8a-224">HTTPS</span></span> | 
| <span data-ttu-id="cca8a-225">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="cca8a-225">*.login.windows.net</span></span> | <span data-ttu-id="cca8a-226">443</span><span class="sxs-lookup"><span data-stu-id="cca8a-226">443</span></span> | <span data-ttu-id="cca8a-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="cca8a-227">HTTPS</span></span> | 
| <span data-ttu-id="cca8a-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="cca8a-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="cca8a-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="cca8a-229">5671-5672</span></span> | <span data-ttu-id="cca8a-230">Zaawansowane kolejkowania wiadomości protokołu (protokół AMQP)</span><span class="sxs-lookup"><span data-stu-id="cca8a-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="cca8a-231">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="cca8a-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="cca8a-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="cca8a-232">443, 9350-9354</span></span> | <span data-ttu-id="cca8a-233">Obiekty nasłuchujące na przekaźnik magistrali usług za pośrednictwem protokołu TCP (wymaga 443 dla tokenu przejęcie kontroli dostępu)</span><span class="sxs-lookup"><span data-stu-id="cca8a-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="cca8a-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="cca8a-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="cca8a-235">443</span><span class="sxs-lookup"><span data-stu-id="cca8a-235">443</span></span> | <span data-ttu-id="cca8a-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="cca8a-236">HTTPS</span></span> | 
| <span data-ttu-id="cca8a-237">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="cca8a-237">*.core.windows.net</span></span> | <span data-ttu-id="cca8a-238">443</span><span class="sxs-lookup"><span data-stu-id="cca8a-238">443</span></span> | <span data-ttu-id="cca8a-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="cca8a-239">HTTPS</span></span> | 
| <span data-ttu-id="cca8a-240">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cca8a-240">login.microsoftonline.com</span></span> | <span data-ttu-id="cca8a-241">443</span><span class="sxs-lookup"><span data-stu-id="cca8a-241">443</span></span> | <span data-ttu-id="cca8a-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="cca8a-242">HTTPS</span></span> | 
| <span data-ttu-id="cca8a-243">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="cca8a-243">*.msftncsi.com</span></span> | <span data-ttu-id="cca8a-244">443</span><span class="sxs-lookup"><span data-stu-id="cca8a-244">443</span></span> | <span data-ttu-id="cca8a-245">Połączenie z Internetem tootest należy użyć, gdy brama hello jest nieosiągalny za hello usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="cca8a-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="cca8a-246">Jeśli zamiast domeny hello tooapprove adresów IP, możesz pobrać i użyć hello [Microsoft Azure Datacenter IP zakresów listy](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="cca8a-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="cca8a-247">W niektórych przypadkach hello Azure Service Bus połączenia są nawiązywane z adresu IP, a nie w pełni kwalifikowanych nazw domen.</span><span class="sxs-lookup"><span data-stu-id="cca8a-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="cca8a-248">Jak działa hello bramę danych?</span><span class="sxs-lookup"><span data-stu-id="cca8a-248">How does hello data gateway work?</span></span>

<span data-ttu-id="cca8a-249">Brama danych Hello umożliwia szybkie i bezpieczne komunikację między aplikację logiki, hello usługi bramy w chmurze i lokalne źródła danych.</span><span class="sxs-lookup"><span data-stu-id="cca8a-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![Diagram-for-on-premises-Data-Gateway-Flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="cca8a-251">Dlatego po hello użytkownika w chmurze hello współdziała z elementem, który został podłączony tooyour lokalnego źródła danych:</span><span class="sxs-lookup"><span data-stu-id="cca8a-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="cca8a-252">Hello usługi bramy w chmurze tworzy zapytanie, wraz z hello zaszyfrowane poświadczenia dla źródła danych hello i wysyła hello zapytania toohello kolejki hello tooprocess bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="cca8a-253">Witaj usługi bramy w chmurze analizuje zapytania hello i wypchnięcia toohello żądania hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cca8a-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="cca8a-254">Brama danych lokalne powitania sonduje hello Azure Service Bus dla żądań oczekujących.</span><span class="sxs-lookup"><span data-stu-id="cca8a-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="cca8a-255">bramy Hello pobiera hello zapytania, odszyfrowuje hello poświadczeń i łączy toohello źródła danych z tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cca8a-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="cca8a-256">Brama Hello wysyła źródła danych toohello hello kwerendy do wykonania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="cca8a-257">wyniki Hello są wysyłane z hello źródła danych, brama toohello Wstecz i toohello usługi bramy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cca8a-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="cca8a-258">Witaj usługi bramy w chmurze używa hello wyników.</span><span class="sxs-lookup"><span data-stu-id="cca8a-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="cca8a-259">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="cca8a-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="cca8a-260">Ogólne</span><span class="sxs-lookup"><span data-stu-id="cca8a-260">General</span></span>

<span data-ttu-id="cca8a-261">**Q**: należy bramy dla źródeł danych w chmurze hello, np. SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="cca8a-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="cca8a-262">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-262">
**A**: No.</span></span> <span data-ttu-id="cca8a-263">Brama łączy lokalnych tooon tylko źródła danych.</span><span class="sxs-lookup"><span data-stu-id="cca8a-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="cca8a-264">**Q**: hello bramy ma zainstalowane na powitania sam komputer jako źródło danych hello toobe?</span><span class="sxs-lookup"><span data-stu-id="cca8a-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="cca8a-265">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-265">
**A**: No.</span></span> <span data-ttu-id="cca8a-266">Brama Hello łączy toohello źródła danych przy użyciu informacji o połączeniu hello dostarczony.</span><span class="sxs-lookup"><span data-stu-id="cca8a-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="cca8a-267">Jako aplikacja klienta, w tym sensie, należy wziąć pod uwagę hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="cca8a-268">Witaj bramy wystarczy hello możliwości tooconnect toohello nazwy serwera podany.</span><span class="sxs-lookup"><span data-stu-id="cca8a-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="cca8a-269">**Q**: Dlaczego należy I Użyj Azure pracy lub szkołą toosign konta w?</span><span class="sxs-lookup"><span data-stu-id="cca8a-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="cca8a-270">
**A**: można używać Praca Azure lub tylko konta służbowego, po zainstalowaniu bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="cca8a-271">Twoje konto logowania są przechowywane w dzierżawie, który jest zarządzany przez usługę Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cca8a-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="cca8a-272">Zazwyczaj główna nazwa użytkownika konta usługi Azure AD (UPN) jest zgodna hello adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="cca8a-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="cca8a-273">**Q**: moich poświadczeń przechowywania?</span><span class="sxs-lookup"><span data-stu-id="cca8a-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="cca8a-274">
**A**: poświadczenia powitania dla źródła danych są szyfrowane i przechowywane hello bramy w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cca8a-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="cca8a-275">poświadczenia Hello są odszyfrowywane w bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="cca8a-276">**Q**: istnieją wszelkie wymagania dotyczące przepustowości sieci?</span><span class="sxs-lookup"><span data-stu-id="cca8a-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="cca8a-277">
**A**: zaleca się, że połączenie sieciowe ma dobrej przepływności.</span><span class="sxs-lookup"><span data-stu-id="cca8a-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="cca8a-278">Każde środowisko jest inne, a hello ilość danych wysyłanych dotyczy hello wyników.</span><span class="sxs-lookup"><span data-stu-id="cca8a-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="cca8a-279">Przy użyciu usługi ExpressRoute może pomóc tooguarantee poziomu przepływności między lokalnymi i hello centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cca8a-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="cca8a-280">Możesz użyć hello narzędzia innej firmy Azure szybkości testowanie aplikacji toohelp miernika przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="cca8a-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="cca8a-281">**Q**: co to jest hello opóźnienie dla źródła danych tooa zapytania uruchomionego z bramy hello?</span><span class="sxs-lookup"><span data-stu-id="cca8a-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="cca8a-282">Co to jest architektura najlepsze hello?</span><span class="sxs-lookup"><span data-stu-id="cca8a-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="cca8a-283">
**A**: tooreduce opóźnienia sieci, zainstaluj hello bramy jako źródło danych zamknij toohello, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="cca8a-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="cca8a-284">Po zainstalowaniu bramy hello w źródle danych rzeczywistych hello, to zbliżeniowe minimalizuje opóźnienia hello wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="cca8a-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="cca8a-285">Rozważ zbyt hello centrów danych.</span><span class="sxs-lookup"><span data-stu-id="cca8a-285">Consider hello datacenters too.</span></span> <span data-ttu-id="cca8a-286">Na przykład jeśli usługa używa hello datacenter zachodnie stany USA, a masz programu SQL Server w maszynie Wirtualnej platformy Azure, maszyny Wirtualnej Azure należy w hello zachodnie stany USA zbyt.</span><span class="sxs-lookup"><span data-stu-id="cca8a-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="cca8a-287">Ta bliskości zmniejsza opóźnienia i pozwala uniknąć opłaty za wyjście na powitania maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cca8a-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="cca8a-288">**Q**: w jaki sposób wyniki wysyłane wstecz toohello chmury?</span><span class="sxs-lookup"><span data-stu-id="cca8a-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="cca8a-289">
**A**: wyniki są wysyłane za pośrednictwem hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cca8a-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="cca8a-290">**Q**: czy istnieją bramy toohello wszystkie połączenia przychodzące z chmury hello?</span><span class="sxs-lookup"><span data-stu-id="cca8a-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="cca8a-291">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-291">
**A**: No.</span></span> <span data-ttu-id="cca8a-292">Brama Hello używa połączenia wychodzące tooAzure usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cca8a-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="cca8a-293">**Q**: co zrobić, jeśli zablokowanie połączeń wychodzących?</span><span class="sxs-lookup"><span data-stu-id="cca8a-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="cca8a-294">Czego potrzebuję tooopen?</span><span class="sxs-lookup"><span data-stu-id="cca8a-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="cca8a-295">
**A**: Zobacz hello portów i hostów, które hello używa bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="cca8a-296">**Q**: rzeczywiste usługi Windows hello tzw?</span><span class="sxs-lookup"><span data-stu-id="cca8a-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="cca8a-297">
**A**: W usługach, bramy hello jest nazywany Usługa bramy Power BI Enterprise.</span><span class="sxs-lookup"><span data-stu-id="cca8a-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="cca8a-298">**Q**: można hello usługa systemu Windows bramy uruchomione przy użyciu konta usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cca8a-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="cca8a-299">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="cca8a-299">
**A**: No.</span></span> <span data-ttu-id="cca8a-300">Usługa Windows Hello muszą mieć prawidłowe konto systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cca8a-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="cca8a-301">Domyślnie usługa hello jest uruchamiana z hello SID usługi NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="cca8a-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="cca8a-302">Wysoka dostępność i odzyskiwanie po awarii</span><span class="sxs-lookup"><span data-stu-id="cca8a-302">High availability and disaster recovery</span></span>

<span data-ttu-id="cca8a-303">**Q**: jakie opcje są dostępne dla odzyskiwania po awarii?</span><span class="sxs-lookup"><span data-stu-id="cca8a-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="cca8a-304">
**A**: możesz użyć toorestore klucza odzyskiwania hello lub przenieść bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="cca8a-305">Po zainstalowaniu bramy hello Określ hello klucza odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="cca8a-306">**Q**: co to jest korzyść hello hello klucza odzyskiwania?</span><span class="sxs-lookup"><span data-stu-id="cca8a-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="cca8a-307">
**A**: hello klucza odzyskiwania zawiera toomigrate sposób lub odzyskiwanie po awarii ustawienia bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="cca8a-308">**Q**: czy jest planowane umożliwiających realizację scenariuszy wysokiej dostępności z bramą hello?</span><span class="sxs-lookup"><span data-stu-id="cca8a-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="cca8a-309">
**A**: te scenariusze są na powitania plan, ale nie mamy jeszcze osi czasu.</span><span class="sxs-lookup"><span data-stu-id="cca8a-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cca8a-310">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="cca8a-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="cca8a-311">**Q**: jak zobaczyć, jakie zapytania są wysyłane toohello lokalnego źródła danych?</span><span class="sxs-lookup"><span data-stu-id="cca8a-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="cca8a-312">
**A**: można włączyć funkcja śledzenia zapytań, w tym hello zapytań, które są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="cca8a-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="cca8a-313">Należy pamiętać, zapytania toochange Śledzenie wstecz toohello oryginalnej wartości po zakończeniu rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cca8a-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="cca8a-314">Jeśli pozostanie włączona funkcja śledzenia zapytań tworzy większe dzienniki.</span><span class="sxs-lookup"><span data-stu-id="cca8a-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="cca8a-315">Można też przyjrzeć się narzędzia, które ma źródła danych śledzenia zapytań.</span><span class="sxs-lookup"><span data-stu-id="cca8a-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="cca8a-316">Na przykład można użyć zdarzeń rozszerzonych lub profilera SQL dla programu SQL Server i usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="cca8a-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="cca8a-317">**Q**: gdzie są dzienniki bramy hello?</span><span class="sxs-lookup"><span data-stu-id="cca8a-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="cca8a-318">
**A**: Zobacz narzędzia w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="cca8a-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="cca8a-319">Aktualizacja toohello najnowszej wersji</span><span class="sxs-lookup"><span data-stu-id="cca8a-319">Update toohello latest version</span></span>

<span data-ttu-id="cca8a-320">Wiele problemów można powierzchni, gdy wersja bramy hello staje się nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="cca8a-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="cca8a-321">Dobrym rozwiązaniem ogólne upewnij się, że używasz najnowszej wersji powitania.</span><span class="sxs-lookup"><span data-stu-id="cca8a-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="cca8a-322">Witaj bramy nie były aktualizowane przez miesiąc lub dłużej, może zaleca się zainstalowanie najnowszej wersji bramy hello hello i zobacz, czy można odtworzyć problem hello.</span><span class="sxs-lookup"><span data-stu-id="cca8a-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="cca8a-323">Błąd: Nie tooadd toogroup użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cca8a-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="cca8a-324">(Użytkownicy dzienników wydajności PBIEgwService-2147463168)</span><span class="sxs-lookup"><span data-stu-id="cca8a-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="cca8a-325">Być może ten błąd przy próbie tooinstall hello bramy na kontrolerze domeny, który nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="cca8a-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="cca8a-326">Upewnij się, wdrożenie bramy hello na komputerze, który nie jest kontrolerem domeny.</span><span class="sxs-lookup"><span data-stu-id="cca8a-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="cca8a-327">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="cca8a-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="cca8a-328">Zbieranie dzienników z hello configurer bramy</span><span class="sxs-lookup"><span data-stu-id="cca8a-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="cca8a-329">Można zbierać dzienniki kilka hello bramy.</span><span class="sxs-lookup"><span data-stu-id="cca8a-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="cca8a-330">Zawsze uruchamiaj z dziennikami Witaj!</span><span class="sxs-lookup"><span data-stu-id="cca8a-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="cca8a-331">Dzienniki Instalatora</span><span class="sxs-lookup"><span data-stu-id="cca8a-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="cca8a-332">Dzienniki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="cca8a-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="cca8a-333">Dzienniki usługi bramy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="cca8a-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="cca8a-334">Dzienniki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="cca8a-334">Event logs</span></span>

<span data-ttu-id="cca8a-335">Możesz znaleźć hello dzienniki bramy zarządzania danymi i PowerBIGateway w obszarze **Dzienniki aplikacji i usług**.</span><span class="sxs-lookup"><span data-stu-id="cca8a-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="cca8a-336">Śledzenie fiddler</span><span class="sxs-lookup"><span data-stu-id="cca8a-336">Fiddler Trace</span></span>

<span data-ttu-id="cca8a-337">[Fiddler](http://www.telerik.com/fiddler) to bezpłatne narzędzie ze strony firmy Telerik, który monitoruje ruch HTTP.</span><span class="sxs-lookup"><span data-stu-id="cca8a-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="cca8a-338">Ten ruch z usługi Power BI z komputera klienta hello hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="cca8a-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="cca8a-339">Ta usługa mogą być wyświetlane błędy oraz inne powiązane informacje.</span><span class="sxs-lookup"><span data-stu-id="cca8a-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cca8a-340">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cca8a-340">Next steps</span></span>
    
* [<span data-ttu-id="cca8a-341">Połączenie lokalne tooon dane z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="cca8a-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="cca8a-342">Funkcje integracji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="cca8a-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="cca8a-343">Łączniki dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="cca8a-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
