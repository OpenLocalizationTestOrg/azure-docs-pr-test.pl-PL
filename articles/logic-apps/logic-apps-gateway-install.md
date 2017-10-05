---
title: Instalowanie bramy danych lokalnych - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Aby uzyskać dostęp do źródła danych na lokalnym, instalowanie bramy danych lokalnych, transfer danych szybki i szyfrowania między źródłami danych lokalnie i logic apps"
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
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="ca183-104">Instalowanie bramy danych lokalnych dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ca183-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="ca183-105">Aplikacje logiki uzyskania dostępu do źródeł danych lokalnie, należy zainstalować i skonfiguruj bramę danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ca183-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="ca183-106">Brama działa jako mostka zapewnia transfer danych szybki i szyfrowania między systemami lokalnymi i aplikacje logiki.</span><span class="sxs-lookup"><span data-stu-id="ca183-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="ca183-107">Brama przekazuje dane z lokalnych źródeł w kanałach zaszyfrowane za pomocą usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ca183-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="ca183-108">Cały ruch pochodzi jako bezpieczny ruch wychodzący z agentem bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="ca183-109">Dowiedz się więcej o [działanie bramy danych](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="ca183-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="ca183-110">Brama obsługuje połączenia z tych źródeł danych na lokalnym:</span><span class="sxs-lookup"><span data-stu-id="ca183-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="ca183-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="ca183-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="ca183-112">DB2</span><span class="sxs-lookup"><span data-stu-id="ca183-112">DB2</span></span>  
*   <span data-ttu-id="ca183-113">System plików</span><span class="sxs-lookup"><span data-stu-id="ca183-113">File System</span></span>
*   <span data-ttu-id="ca183-114">Informix</span><span class="sxs-lookup"><span data-stu-id="ca183-114">Informix</span></span>
*   <span data-ttu-id="ca183-115">MQ</span><span class="sxs-lookup"><span data-stu-id="ca183-115">MQ</span></span>
*   <span data-ttu-id="ca183-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="ca183-116">MySQL</span></span>
*   <span data-ttu-id="ca183-117">Baza danych Oracle</span><span class="sxs-lookup"><span data-stu-id="ca183-117">Oracle Database</span></span>
*   <span data-ttu-id="ca183-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ca183-118">PostgreSQL</span></span>
*   <span data-ttu-id="ca183-119">Serwer aplikacji SAP</span><span class="sxs-lookup"><span data-stu-id="ca183-119">SAP Application Server</span></span> 
*   <span data-ttu-id="ca183-120">Serwer komunikatów SAP</span><span class="sxs-lookup"><span data-stu-id="ca183-120">SAP Message Server</span></span>
*   <span data-ttu-id="ca183-121">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="ca183-121">SharePoint</span></span>
*   <span data-ttu-id="ca183-122">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="ca183-122">SQL Server</span></span>
*   <span data-ttu-id="ca183-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="ca183-123">Teradata</span></span>

<span data-ttu-id="ca183-124">Te kroki pokazują, jak najpierw zainstaluj bramę danych lokalnych przed [skonfigurować połączenie między bramą a aplikacje logiki](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="ca183-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="ca183-125">Aby uzyskać więcej informacji o obsługiwanych łączników, zobacz [łączniki dla usługi Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="ca183-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="ca183-126">Aby uzyskać informacje o sposobie używania bramy z innymi usługami, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="ca183-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="ca183-127">Microsoft Power BI lokalnej bramy danych</span><span class="sxs-lookup"><span data-stu-id="ca183-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="ca183-128">Azure bramy danych lokalnych usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ca183-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="ca183-129">Brama danych lokalnych Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ca183-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="ca183-130">Brama danych lokalnych PowerApps firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ca183-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="ca183-131">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ca183-131">Requirements</span></span>

<span data-ttu-id="ca183-132">**Co najmniej**:</span><span class="sxs-lookup"><span data-stu-id="ca183-132">**Minimum**:</span></span>

* <span data-ttu-id="ca183-133">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="ca183-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="ca183-134">64-bitowej wersji systemu Windows 7 lub Windows Server 2008 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="ca183-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="ca183-135">**Zalecane**:</span><span class="sxs-lookup"><span data-stu-id="ca183-135">**Recommended**:</span></span>

* <span data-ttu-id="ca183-136">8 rdzeni procesora CPU</span><span class="sxs-lookup"><span data-stu-id="ca183-136">8 Core CPU</span></span>
* <span data-ttu-id="ca183-137">8 GB pamięci</span><span class="sxs-lookup"><span data-stu-id="ca183-137">8 GB Memory</span></span>
* <span data-ttu-id="ca183-138">64-bitowej wersji systemu Windows 2012 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="ca183-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="ca183-139">**Ważne uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="ca183-139">**Important considerations**:</span></span>

* <span data-ttu-id="ca183-140">Instalowanie bramy danych lokalnych tylko na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="ca183-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="ca183-141">Nie można zainstalować bramę na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="ca183-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="ca183-142">Nie trzeba zainstalować bramę na tym samym komputerze co źródła danych.</span><span class="sxs-lookup"><span data-stu-id="ca183-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="ca183-143">Aby zminimalizować czas oczekiwania, możesz zainstalować bramę, jak najbliżej ze źródłem danych lub na tym samym komputerze, przy założeniu, że masz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="ca183-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="ca183-144">Nie należy instalować bramy na komputerze, który zostanie wyłączony, przechodzi w stan uśpienia, lub nie łączyć się z Internetem, ponieważ brama nie można uruchomić w tych warunkach.</span><span class="sxs-lookup"><span data-stu-id="ca183-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="ca183-145">Ponadto w sieci bezprzewodowej może pogorszyć wydajność bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="ca183-146">Podczas instalacji, należy się zalogować przy użyciu [konto służbowe](https://docs.microsoft.com/azure/active-directory/sign-up-organization) zarządzanym przez usługę Azure Active Directory (Azure AD), nie konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ca183-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="ca183-147">Należy użyć tego samego konta firmowego lub szkolnego później w portalu Azure, podczas tworzenia i skojarzyć z instalacją bramy zasobów bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="ca183-148">Podczas tworzenia połączenia między aplikację logiki i lokalnego źródła danych, następnie wybierz tego zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="ca183-149">Dlaczego należy używać Praca usługi Azure AD lub konta służbowego?</span><span class="sxs-lookup"><span data-stu-id="ca183-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="ca183-150">Jeśli konta dla oferty usługi Office 365, a nie dostarczył rzeczywiste służbowego adresu e-mail, adresu logowania może wyglądać jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ca183-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="ca183-151">Jeśli masz istniejącą bramę skonfigurowanego z Instalatorem, która jest starsza niż wersja 14.16.6317.4, nie można zmienić lokalizacji bramy sieci, uruchamiając najnowszą wersję Instalatora.</span><span class="sxs-lookup"><span data-stu-id="ca183-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="ca183-152">Jednak można użyć najnowszą wersję Instalatora, aby skonfigurować nową bramę z lokalizacji, w której chcesz zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="ca183-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="ca183-153">Jeśli Instalator bramy, która jest starsza niż wersja 14.16.6317.4, ale nie zostały zainstalowane bramy można jeszcze miejsca, pobranie i użycie najnowszą wersję Instalatora.</span><span class="sxs-lookup"><span data-stu-id="ca183-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="ca183-154">Instalowanie bramy danych</span><span class="sxs-lookup"><span data-stu-id="ca183-154">Install the data gateway</span></span>

1.  <span data-ttu-id="ca183-155">[Pobierz i uruchom Instalator bramy na komputerze lokalnym](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ca183-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="ca183-156">Przeczytaj i zaakceptuj warunki użytkowania i ochrony prywatności.</span><span class="sxs-lookup"><span data-stu-id="ca183-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="ca183-157">Określ ścieżkę na komputerze lokalnym, na którym chcesz zainstalować bramę.</span><span class="sxs-lookup"><span data-stu-id="ca183-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="ca183-158">Po wyświetleniu monitu zaloguj się przy użyciu konta służbowego, nie konta Microsoft Azure pracy.</span><span class="sxs-lookup"><span data-stu-id="ca183-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Zaloguj się przy użyciu pracy Azure lub konta służbowego](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="ca183-160">Teraz zarejestrować zainstalowana brama z [usługi bramy w chmurze](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="ca183-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="ca183-161">Wybierz **zarejestrować nową bramę na tym komputerze**.</span><span class="sxs-lookup"><span data-stu-id="ca183-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="ca183-162">Usługi w chmurze bramy są szyfrowane i przechowywane poświadczenia źródła danych, a szczegóły bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="ca183-163">Usługa również kieruje lokalnie zapytań i ich wyników między aplikację logiki, brama lokalna danych i źródła danych.</span><span class="sxs-lookup"><span data-stu-id="ca183-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="ca183-164">Podaj nazwę dla tej instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="ca183-165">Twórz klucza odzyskiwania, a następnie potwierdź klucz odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ca183-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="ca183-166">Klucz odzyskiwania musi zawierać co najmniej osiem znaków.</span><span class="sxs-lookup"><span data-stu-id="ca183-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="ca183-167">Upewnij się, czy zapisać, a klucz należy przechowywać w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="ca183-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="ca183-168">Należy również ten klucz umożliwia migrację, Przywróć lub Przejmij na istniejącą bramę.</span><span class="sxs-lookup"><span data-stu-id="ca183-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="ca183-169">Aby zmienić domyślny region usługi bramy w chmurze i używane przez instalację bramy usługi Azure Service Bus, wybierz **zmienić regionu**.</span><span class="sxs-lookup"><span data-stu-id="ca183-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Zmiana regionu](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="ca183-171">Domyślnego regionu jest regionu skojarzonego z dzierżawą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca183-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="ca183-172">Otwórz na następne okienko **wybierz Region** aby wybrać inny region.</span><span class="sxs-lookup"><span data-stu-id="ca183-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![Wybierz inny region](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="ca183-174">Na przykład wybierz region, w tym samym jako aplikację logiki, lub wybierz region najbliższy do lokalnego źródła danych, aby ograniczyć czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="ca183-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="ca183-175">Bramy aplikacji logiki i zasobów mogą mieć różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="ca183-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ca183-176">Ten region nie można zmienić po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="ca183-176">You can't change this region after installation.</span></span> <span data-ttu-id="ca183-177">Ten region również określa i ogranicza lokalizacji, w którym można utworzyć zasobów platformy Azure dla bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="ca183-178">Dlatego podczas tworzenia zasobu bramy na platformie Azure, upewnij się, że lokalizacja zasobu zgodny z ustawieniami regionalnymi wybranym podczas instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="ca183-179">Jeśli chcesz później przy użyciu w innym regionie bramy, należy skonfigurować nową bramę.</span><span class="sxs-lookup"><span data-stu-id="ca183-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="ca183-180">Gdy wszystko jest gotowe, wybierz pozycję **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="ca183-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="ca183-181">Teraz wykonaj następujące kroki w portalu Azure, można więc [tworzenie zasobów platformy Azure dla bramy](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="ca183-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="ca183-182">Dowiedz się więcej o [działanie bramy danych](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="ca183-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="ca183-183">Migracja, Przywróć lub Przejmij na istniejącą bramę</span><span class="sxs-lookup"><span data-stu-id="ca183-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="ca183-184">Aby wykonać te zadania, musi mieć klucz odzyskiwania, który został określony podczas instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="ca183-185">Z menu Start komputera, wybierz **bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="ca183-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="ca183-186">Po otwarciu Instalator, zaloguj się przy użyciu tego samego pracy Azure konta służbowego, który był wcześniej używany do instalacji bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="ca183-187">Wybierz **migracji, Przywróć lub Przejmij istniejącą bramę**.</span><span class="sxs-lookup"><span data-stu-id="ca183-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="ca183-188">Podaj nazwę i odzyskiwanie klucza bramy, który chcesz migrować, Przywróć lub Przejmij na.</span><span class="sxs-lookup"><span data-stu-id="ca183-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="ca183-189">Ponownie uruchom bramę</span><span class="sxs-lookup"><span data-stu-id="ca183-189">Restart the gateway</span></span>

<span data-ttu-id="ca183-190">Brama działa jako usługa systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ca183-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="ca183-191">Podobnie jak inne usługi systemu Windows można uruchomić i zatrzymać usługę na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="ca183-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="ca183-192">Można na przykład, otwórz wiersz polecenia z podwyższonym poziomem uprawnień na komputerze, na którym jest uruchomiona brama i uruchamiania obu tych poleceń:</span><span class="sxs-lookup"><span data-stu-id="ca183-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="ca183-193">Aby zatrzymać usługę, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ca183-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="ca183-194">Aby uruchomić usługę, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ca183-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="ca183-195">Konto usługi systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ca183-195">Windows service account</span></span>

<span data-ttu-id="ca183-196">Brama danych lokalnych jest skonfigurowany do użycia `NT SERVICE\PBIEgwService` dla systemu Windows usługi poświadczeń logowania.</span><span class="sxs-lookup"><span data-stu-id="ca183-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="ca183-197">Domyślnie bramy ma prawo "Zaloguj jako usługa" dla komputera, w którym zainstalowano bramę.</span><span class="sxs-lookup"><span data-stu-id="ca183-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="ca183-198">Konto usługi systemu Windows różni się od konto używane do łączenia się z danymi lokalnymi źródeł, a z platformy Azure służbowe konto używane do logowania do usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ca183-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="ca183-199">Konfigurowanie zapory lub serwera proxy</span><span class="sxs-lookup"><span data-stu-id="ca183-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="ca183-200">Brama tworzy wychodzące połączenie [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="ca183-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="ca183-201">Aby podać informacje o serwerze proxy dla bramy, zobacz [Skonfiguruj ustawienia serwera proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="ca183-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="ca183-202">Aby sprawdzić, czy zapory lub serwera proxy, może zablokować połączenia, upewnij się, czy komputer faktycznie można połączyć się z Internetem i [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="ca183-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="ca183-203">Uruchom to polecenie z wiersza polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ca183-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="ca183-204">To polecenie tylko testy, łączności sieciowej i łączności do usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ca183-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="ca183-205">To polecenie nie ma związek z bramy lub bramy usługi w chmurze są szyfrowane i przechowywane poświadczenia i szczegóły bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="ca183-206">Ponadto to polecenie jest tylko dostępne w systemie Windows Server 2012 R2 lub nowszy oraz Windows 8.1 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="ca183-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="ca183-207">We wcześniejszych wersjach systemu operacyjnego można użyć programu Telnet do testowania łączności.</span><span class="sxs-lookup"><span data-stu-id="ca183-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="ca183-208">Dowiedz się więcej o [Azure Service Bus i hybrydowe rozwiązania](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ca183-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="ca183-209">Wyniki powinny wyglądać podobnie do tego przykładu:</span><span class="sxs-lookup"><span data-stu-id="ca183-209">Your results should look similar to this example:</span></span>

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

<span data-ttu-id="ca183-210">Jeśli **TcpTestSucceeded** nie jest ustawiony na **True**, może zostać zablokowany przez zaporę.</span><span class="sxs-lookup"><span data-stu-id="ca183-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="ca183-211">Jeśli chcesz mieć kompleksowe, zamiast **ComputerName** i **portu** wartości z wartości na liście [skonfigurować porty](#configure-ports) w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="ca183-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="ca183-212">Zapora może również zablokować połączeń, które powoduje Azure Service Bus w centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca183-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="ca183-213">W przypadku tego scenariusza należy zatwierdzić (odblokuj) wszystkie adresy IP dla tych centrach danych w danym regionie.</span><span class="sxs-lookup"><span data-stu-id="ca183-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="ca183-214">Dla tych adresów IP [pobrania listy adresów IP platformy Azure w tym miejscu](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="ca183-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="ca183-215">Skonfiguruj porty</span><span class="sxs-lookup"><span data-stu-id="ca183-215">Configure ports</span></span>

<span data-ttu-id="ca183-216">Brama tworzy wychodzące połączenie [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) i komunikuje się portów wychodzących: TCP 443 (ustawienie domyślne), 5671, 5672, 9350 za pośrednictwem 9354.</span><span class="sxs-lookup"><span data-stu-id="ca183-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="ca183-217">Brama nie wymaga portów przychodzących.</span><span class="sxs-lookup"><span data-stu-id="ca183-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="ca183-218">Dowiedz się więcej o [Azure Service Bus i hybrydowe rozwiązania](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ca183-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="ca183-219">NAZWY DOMEN</span><span class="sxs-lookup"><span data-stu-id="ca183-219">DOMAIN NAMES</span></span> | <span data-ttu-id="ca183-220">PORTY WYJŚCIOWE</span><span class="sxs-lookup"><span data-stu-id="ca183-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="ca183-221">OPIS</span><span class="sxs-lookup"><span data-stu-id="ca183-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca183-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="ca183-222">*.analysis.windows.net</span></span> | <span data-ttu-id="ca183-223">443</span><span class="sxs-lookup"><span data-stu-id="ca183-223">443</span></span> | <span data-ttu-id="ca183-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ca183-224">HTTPS</span></span> | 
| <span data-ttu-id="ca183-225">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="ca183-225">*.login.windows.net</span></span> | <span data-ttu-id="ca183-226">443</span><span class="sxs-lookup"><span data-stu-id="ca183-226">443</span></span> | <span data-ttu-id="ca183-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ca183-227">HTTPS</span></span> | 
| <span data-ttu-id="ca183-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ca183-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="ca183-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="ca183-229">5671-5672</span></span> | <span data-ttu-id="ca183-230">Zaawansowane kolejkowania wiadomości protokołu (protokół AMQP)</span><span class="sxs-lookup"><span data-stu-id="ca183-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="ca183-231">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ca183-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="ca183-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="ca183-232">443, 9350-9354</span></span> | <span data-ttu-id="ca183-233">Obiekty nasłuchujące na przekaźnik magistrali usług za pośrednictwem protokołu TCP (wymaga 443 dla tokenu przejęcie kontroli dostępu)</span><span class="sxs-lookup"><span data-stu-id="ca183-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="ca183-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="ca183-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="ca183-235">443</span><span class="sxs-lookup"><span data-stu-id="ca183-235">443</span></span> | <span data-ttu-id="ca183-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ca183-236">HTTPS</span></span> | 
| <span data-ttu-id="ca183-237">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ca183-237">*.core.windows.net</span></span> | <span data-ttu-id="ca183-238">443</span><span class="sxs-lookup"><span data-stu-id="ca183-238">443</span></span> | <span data-ttu-id="ca183-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ca183-239">HTTPS</span></span> | 
| <span data-ttu-id="ca183-240">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ca183-240">login.microsoftonline.com</span></span> | <span data-ttu-id="ca183-241">443</span><span class="sxs-lookup"><span data-stu-id="ca183-241">443</span></span> | <span data-ttu-id="ca183-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="ca183-242">HTTPS</span></span> | 
| <span data-ttu-id="ca183-243">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ca183-243">*.msftncsi.com</span></span> | <span data-ttu-id="ca183-244">443</span><span class="sxs-lookup"><span data-stu-id="ca183-244">443</span></span> | <span data-ttu-id="ca183-245">Używany do sprawdzania łączności z Internetem, gdy brama jest nieosiągalny przez usługę Power BI.</span><span class="sxs-lookup"><span data-stu-id="ca183-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="ca183-246">Jeśli masz zatwierdzić adresów IP zamiast domeny, możesz pobrać i użyć [Microsoft Azure Datacenter IP zakresów listy](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="ca183-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="ca183-247">W niektórych przypadkach połączenia usługi Azure Service Bus są nawiązywane z adresu IP, a nie w pełni kwalifikowanych nazw domen.</span><span class="sxs-lookup"><span data-stu-id="ca183-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="ca183-248">Jak działa bramę danych?</span><span class="sxs-lookup"><span data-stu-id="ca183-248">How does the data gateway work?</span></span>

<span data-ttu-id="ca183-249">Brama danych umożliwia szybkie i bezpieczne komunikację między aplikację logiki, usługi bramy w chmurze i lokalne źródła danych.</span><span class="sxs-lookup"><span data-stu-id="ca183-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![Diagram-for-on-premises-Data-Gateway-Flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="ca183-251">Tak, gdy użytkownik w chmurze współdziała z elementem, który jest podłączony do lokalnego źródła danych:</span><span class="sxs-lookup"><span data-stu-id="ca183-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="ca183-252">Usługa w chmurze bramy tworzy zapytanie, wraz z zaszyfrowane poświadczenia dla źródła danych i wysyła zapytanie do kolejki dla bramy do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="ca183-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="ca183-253">Usługi w chmurze bramy analizuje zapytania i wypychanie żądania do usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ca183-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="ca183-254">Brama danych lokalnych sonduje Azure Service Bus dla żądań oczekujących.</span><span class="sxs-lookup"><span data-stu-id="ca183-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="ca183-255">Bramy pobiera kwerendy odszyfrowuje poświadczenia i nawiązuje połączenie ze źródłem danych przy użyciu tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="ca183-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="ca183-256">Brama wysyła zapytanie do źródła danych do wykonania.</span><span class="sxs-lookup"><span data-stu-id="ca183-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="ca183-257">Wyniki są wysyłane ze źródła danych, wróć do bramy, a następnie do usługi bramy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ca183-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="ca183-258">Usługi w chmurze bramy następnie używa wyników.</span><span class="sxs-lookup"><span data-stu-id="ca183-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="ca183-259">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="ca183-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="ca183-260">Ogólne</span><span class="sxs-lookup"><span data-stu-id="ca183-260">General</span></span>

<span data-ttu-id="ca183-261">**Q**: należy bramy dla źródeł danych w chmurze, np. SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="ca183-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="ca183-262">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="ca183-262">
**A**: No.</span></span> <span data-ttu-id="ca183-263">Brama łączy się tylko źródła danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ca183-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="ca183-264">**Q**: czy bramy musi być zainstalowany na tym samym komputerze jako źródło danych?</span><span class="sxs-lookup"><span data-stu-id="ca183-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="ca183-265">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="ca183-265">
**A**: No.</span></span> <span data-ttu-id="ca183-266">Brama łączy się ze źródłem danych, korzystając z informacji połączenia, który został dostarczony.</span><span class="sxs-lookup"><span data-stu-id="ca183-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="ca183-267">Jako aplikacja klienta, w tym sensie, należy wziąć pod uwagę bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="ca183-268">Bramy wystarczy możliwość nawiązywania nazwę serwera, który został dostarczony.</span><span class="sxs-lookup"><span data-stu-id="ca183-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="ca183-269">**Q**: Dlaczego musi I używać Azure Praca konto służbowe się zalogować?</span><span class="sxs-lookup"><span data-stu-id="ca183-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="ca183-270">
**A**: można używać Praca Azure lub tylko konta służbowego, po zainstalowaniu bramy danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ca183-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="ca183-271">Twoje konto logowania są przechowywane w dzierżawie, który jest zarządzany przez usługę Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca183-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ca183-272">Główna nazwa użytkownika konta usługi Azure AD (UPN) jest zgodna zwykle adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="ca183-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="ca183-273">**Q**: moich poświadczeń przechowywania?</span><span class="sxs-lookup"><span data-stu-id="ca183-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="ca183-274">
**A**: poświadczenia dla źródła danych są szyfrowane i przechowywane w usłudze w chmurze bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="ca183-275">Poświadczenia są odszyfrowywane w bramie danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ca183-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="ca183-276">**Q**: istnieją wszelkie wymagania dotyczące przepustowości sieci?</span><span class="sxs-lookup"><span data-stu-id="ca183-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="ca183-277">
**A**: zaleca się, że połączenie sieciowe ma dobrej przepływności.</span><span class="sxs-lookup"><span data-stu-id="ca183-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="ca183-278">Każde środowisko jest inne, a ilość danych wysyłanych ma wpływ na wyniki.</span><span class="sxs-lookup"><span data-stu-id="ca183-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="ca183-279">Użycie usługi ExpressRoute może pomóc do zapewnienia poziomu przepływności między lokalnymi i centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca183-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="ca183-280">Można użyć aplikacji Azure szybkości testowanie narzędzia innej firmy by zmierzyć przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="ca183-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="ca183-281">**Q**: co to jest czas oczekiwania na wykonywanie zapytań do źródła danych z bramy?</span><span class="sxs-lookup"><span data-stu-id="ca183-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="ca183-282">Co to jest najlepszym architektura?</span><span class="sxs-lookup"><span data-stu-id="ca183-282">What is the best architecture?</span></span> <br/><span data-ttu-id="ca183-283">
**A**: do zmniejszenia opóźnienia sieci, należy zainstalować bramę maksymalnie zbliżony źródła danych, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="ca183-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="ca183-284">Po zainstalowaniu bramy w źródle danych rzeczywistych, to zbliżeniowe minimalizuje opóźnienie wprowadzane.</span><span class="sxs-lookup"><span data-stu-id="ca183-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="ca183-285">Rozważ zbyt centrach danych.</span><span class="sxs-lookup"><span data-stu-id="ca183-285">Consider the datacenters too.</span></span> <span data-ttu-id="ca183-286">Na przykład jeśli usługa używa datacenter zachodnie stany USA, a masz programu SQL Server w maszynie Wirtualnej platformy Azure, maszyny Wirtualnej Azure należy w zachodnie stany USA zbyt.</span><span class="sxs-lookup"><span data-stu-id="ca183-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="ca183-287">Ta bliskości zmniejsza opóźnienia i pozwala uniknąć opłaty za wyjście na maszynie Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="ca183-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="ca183-288">**Q**: jak są wyniki odsyłane do chmury?</span><span class="sxs-lookup"><span data-stu-id="ca183-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="ca183-289">
**A**: wyniki są wysyłane za pośrednictwem usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ca183-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="ca183-290">**Q**: istnieją wszystkie połączenia przychodzące do bramy w chmurze?</span><span class="sxs-lookup"><span data-stu-id="ca183-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="ca183-291">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="ca183-291">
**A**: No.</span></span> <span data-ttu-id="ca183-292">Brama korzysta z połączenia wychodzące do usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ca183-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="ca183-293">**Q**: co zrobić, jeśli zablokowanie połączeń wychodzących?</span><span class="sxs-lookup"><span data-stu-id="ca183-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="ca183-294">Co trzeba otworzyć?</span><span class="sxs-lookup"><span data-stu-id="ca183-294">What do I need to open?</span></span> <br/><span data-ttu-id="ca183-295">
**A**: Zobacz porty i hostów, które używa bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="ca183-296">**Q**: co to jest rzeczywiste usługi systemu Windows o nazwie?</span><span class="sxs-lookup"><span data-stu-id="ca183-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="ca183-297">
**A**: usług w bramie jest nazywany Usługa bramy Power BI Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ca183-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="ca183-298">**Q**: można uruchomić bramy usługi systemu Windows przy użyciu konta usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca183-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="ca183-299">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="ca183-299">
**A**: No.</span></span> <span data-ttu-id="ca183-300">Usługa systemu Windows muszą mieć prawidłowe konto systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ca183-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="ca183-301">Domyślnie usługa jest uruchamiana z identyfikatorem SID usługi NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="ca183-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="ca183-302">Wysoka dostępność i odzyskiwanie po awarii</span><span class="sxs-lookup"><span data-stu-id="ca183-302">High availability and disaster recovery</span></span>

<span data-ttu-id="ca183-303">**Q**: jakie opcje są dostępne dla odzyskiwania po awarii?</span><span class="sxs-lookup"><span data-stu-id="ca183-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="ca183-304">
**A**: klucz odzyskiwania służy do przywracania, lub Przenieś bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="ca183-305">Po zainstalowaniu bramy, należy określić klucz odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ca183-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="ca183-306">**Q**: co to jest korzyść klucz odzyskiwania?</span><span class="sxs-lookup"><span data-stu-id="ca183-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="ca183-307">
**A**: klucz odzyskiwania pozwala przeprowadzić migrację lub odzyskiwanie po awarii ustawienia bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="ca183-308">**Q**: czy jest planowane umożliwiających realizację scenariuszy wysokiej dostępności z bramą?</span><span class="sxs-lookup"><span data-stu-id="ca183-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="ca183-309">
**A**: tych scenariuszy znajdują się na plan, ale nie mamy jeszcze osi czasu.</span><span class="sxs-lookup"><span data-stu-id="ca183-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ca183-310">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ca183-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="ca183-311">**Q**: jak wyświetlić co zapytania są wysyłane do lokalnego źródła danych?</span><span class="sxs-lookup"><span data-stu-id="ca183-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="ca183-312">
**A**: można włączyć funkcja śledzenia zapytań, który zawiera zapytania, które są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="ca183-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="ca183-313">Pamiętaj, aby zmienić zapytania śledzenia wstecz do oryginalnej wartości po zakończeniu rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="ca183-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="ca183-314">Jeśli pozostanie włączona funkcja śledzenia zapytań tworzy większe dzienniki.</span><span class="sxs-lookup"><span data-stu-id="ca183-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="ca183-315">Można też przyjrzeć się narzędzia, które ma źródła danych śledzenia zapytań.</span><span class="sxs-lookup"><span data-stu-id="ca183-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="ca183-316">Na przykład można użyć zdarzeń rozszerzonych lub profilera SQL dla programu SQL Server i usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="ca183-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="ca183-317">**Q**: gdzie są dzienniki bramy?</span><span class="sxs-lookup"><span data-stu-id="ca183-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="ca183-318">
**A**: Zobacz narzędzia w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="ca183-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="ca183-319">Aktualizowanie do najnowszej wersji</span><span class="sxs-lookup"><span data-stu-id="ca183-319">Update to the latest version</span></span>

<span data-ttu-id="ca183-320">Wiele problemów można powierzchni, gdy wersja bramy stanie się nieaktualna.</span><span class="sxs-lookup"><span data-stu-id="ca183-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="ca183-321">Dobrym rozwiązaniem ogólne upewnij się, że używasz najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ca183-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="ca183-322">Brama nie były aktualizowane przez miesiąc lub dłużej, może być zaleca się zainstalowanie najnowszej wersji bramy i zobacz, czy można odtworzyć problem.</span><span class="sxs-lookup"><span data-stu-id="ca183-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="ca183-323">Błąd: Nie można dodać użytkownika do grupy.</span><span class="sxs-lookup"><span data-stu-id="ca183-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="ca183-324">(Użytkownicy dzienników wydajności PBIEgwService-2147463168)</span><span class="sxs-lookup"><span data-stu-id="ca183-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="ca183-325">Ten błąd może pobrać, Jeśli spróbujesz zainstalować bramę na kontrolerze domeny, który nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="ca183-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="ca183-326">Upewnij się, że wdrożyć bramę na komputerze, na którym nie jest kontrolerem domeny.</span><span class="sxs-lookup"><span data-stu-id="ca183-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="ca183-327">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="ca183-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="ca183-328">Zbieranie dzienników z configurer bramy</span><span class="sxs-lookup"><span data-stu-id="ca183-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="ca183-329">Można zbierać kilka dzienniki bramy.</span><span class="sxs-lookup"><span data-stu-id="ca183-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="ca183-330">Zawsze uruchamiaj z dziennikami!</span><span class="sxs-lookup"><span data-stu-id="ca183-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="ca183-331">Dzienniki Instalatora</span><span class="sxs-lookup"><span data-stu-id="ca183-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="ca183-332">Dzienniki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ca183-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="ca183-333">Dzienniki usługi bramy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="ca183-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="ca183-334">Dzienniki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ca183-334">Event logs</span></span>

<span data-ttu-id="ca183-335">Można znaleźć w dziennikach brama zarządzania danymi i PowerBIGateway w obszarze **Dzienniki aplikacji i usług**.</span><span class="sxs-lookup"><span data-stu-id="ca183-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="ca183-336">Śledzenie fiddler</span><span class="sxs-lookup"><span data-stu-id="ca183-336">Fiddler Trace</span></span>

<span data-ttu-id="ca183-337">[Fiddler](http://www.telerik.com/fiddler) to bezpłatne narzędzie ze strony firmy Telerik, który monitoruje ruch HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca183-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="ca183-338">Widać tego ruchu z usługi Power BI z komputera klienta.</span><span class="sxs-lookup"><span data-stu-id="ca183-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="ca183-339">Ta usługa mogą być wyświetlane błędy oraz inne powiązane informacje.</span><span class="sxs-lookup"><span data-stu-id="ca183-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca183-340">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca183-340">Next steps</span></span>
    
* [<span data-ttu-id="ca183-341">Połącz się z lokalnymi danymi z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ca183-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="ca183-342">Funkcje integracji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="ca183-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="ca183-343">Łączniki dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="ca183-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
