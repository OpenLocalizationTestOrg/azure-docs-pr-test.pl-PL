---
title: "aaaIssuer nazwy i klucza wystawcy usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooretrieve nazwy wystawcy i klucza wystawcy dla usługi Service Bus lub kontroli dostępu (ACS) w usługach BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="5eb10-104">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="5eb10-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="5eb10-105">Azure usługi BizTalk Services używa hello Nazwa wystawcy magistrali usługi i klucza wystawcy i hello Nazwa wystawcy kontroli dostępu i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5eb10-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="5eb10-106">W szczególności:</span><span class="sxs-lookup"><span data-stu-id="5eb10-106">Specifically:</span></span>

| <span data-ttu-id="5eb10-107">Zadanie</span><span class="sxs-lookup"><span data-stu-id="5eb10-107">Task</span></span> | <span data-ttu-id="5eb10-108">Która nazwa wystawcy i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="5eb10-109">Wdrażanie aplikacji w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5eb10-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="5eb10-110">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="5eb10-111">Konfigurowanie hello Azure Portal usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="5eb10-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="5eb10-112">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="5eb10-113">Tworzenie LOB przekaźników z hello BizTalk karty usług w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5eb10-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="5eb10-114">Nazwa wystawcy magistrali usługi i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="5eb10-115">W tym temacie wymieniono hello kroki tooretrieve hello Nazwa wystawcy i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5eb10-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="5eb10-116">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="5eb10-117">Hello Nazwa wystawcy kontroli dostępu i klucz wystawcy, są używane przez następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5eb10-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="5eb10-118">Aplikacja usługi BizTalk Azure utworzone w programie Visual Studio: toosuccessfully wdrażania aplikacji usługi BizTalk w Visual Studio tooAzure, należy wprowadzić hello Nazwa wystawcy kontroli dostępu i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5eb10-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="5eb10-119">Portal usługi BizTalk Azure Hello: podczas tworzenia usługi BizTalk i otwórz hello Portal usługi BizTalk, nazwę wystawcy kontroli dostępu i klucza wystawcy, są automatycznie rejestrowane wdrożeń z hello takie same wartości kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5eb10-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="5eb10-120">Pobierz hello Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="5eb10-121">Nazwa wystawcy i klucza wystawcy wartości hello ACS toouse uwierzytelniania i get, hello ogólne kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="5eb10-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="5eb10-122">Zainstaluj hello [poleceń cmdlet programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="5eb10-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="5eb10-123">Dodaj konto platformy Azure:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="5eb10-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="5eb10-124">Zwraca nazwę Twojej subskrypcji:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="5eb10-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="5eb10-125">Wybierz subskrypcję:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="5eb10-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="5eb10-126">Tworzenie nowej przestrzeni nazw:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="5eb10-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="5eb10-127">Przykład:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="5eb10-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="5eb10-128">Po utworzeniu przestrzeni nazw hello nowych usług ACS, (co może potrwać kilka minut), wartości nazwy wystawcy i klucza wystawcy hello są wymienione w ciągu połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="5eb10-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="5eb10-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="5eb10-129">toosummarize:</span></span>  
<span data-ttu-id="5eb10-130">Nazwa wystawcy = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="5eb10-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="5eb10-131">Klucz wystawcy = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="5eb10-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="5eb10-132">Więcej informacji na temat hello [AzureSBNamespace nowy](https://msdn.microsoft.com/library/dn495165.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5eb10-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="5eb10-133">Nazwa wystawcy magistrali usługi i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="5eb10-134">Nazwa wystawcy magistrali usługi i klucza wystawcy, są używane przez usługi karty BizTalk.</span><span class="sxs-lookup"><span data-stu-id="5eb10-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="5eb10-135">W projekcie usługi BizTalk Services w programie Visual Studio używasz hello usług karty BizTalk tooconnect tooan lokalnego — biznesowych (LOB) systemu.</span><span class="sxs-lookup"><span data-stu-id="5eb10-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="5eb10-136">tooconnect, Utwórz hello LOB przekazywania i wprowadź swoje dane systemu LOB.</span><span class="sxs-lookup"><span data-stu-id="5eb10-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="5eb10-137">W ten sposób można także wprowadzić hello Nazwa wystawcy magistrali usługi i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5eb10-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="5eb10-138">Witaj tooretrieve Nazwa wystawcy magistrali usługi i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5eb10-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="5eb10-139">Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="5eb10-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="5eb10-140">Wybierz w okienku nawigacji po lewej stronie powitania **usługi Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="5eb10-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="5eb10-141">Wybierz obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="5eb10-141">Select your namespace.</span></span> <span data-ttu-id="5eb10-142">Na pasku zadań hello, wybierz **informacje o połączeniu**.</span><span class="sxs-lookup"><span data-stu-id="5eb10-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="5eb10-143">Spowoduje to wyświetlenie hello **domyślne wystawcy** (Nazwa wystawcy) i **domyślny klucz** (klucza wystawcy).</span><span class="sxs-lookup"><span data-stu-id="5eb10-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="5eb10-144">Można skopiować wartości.</span><span class="sxs-lookup"><span data-stu-id="5eb10-144">Their values can be copied.</span></span>  

<span data-ttu-id="5eb10-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="5eb10-145">toosummarize:</span></span>  
<span data-ttu-id="5eb10-146">Nazwa wystawcy = wystawcy domyślne</span><span class="sxs-lookup"><span data-stu-id="5eb10-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="5eb10-147">Klucz wystawcy domyślny klucz =</span><span class="sxs-lookup"><span data-stu-id="5eb10-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="5eb10-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5eb10-148">Next</span></span>
<span data-ttu-id="5eb10-149">Dodatkowe tematy usługi BizTalk Azure:</span><span class="sxs-lookup"><span data-stu-id="5eb10-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="5eb10-150">Instalowanie hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="5eb10-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="5eb10-151">Samouczki: Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="5eb10-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="5eb10-152">Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="5eb10-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="5eb10-153">Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="5eb10-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="5eb10-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5eb10-154">See Also</span></span>
* [<span data-ttu-id="5eb10-155">Porady: Użyj usługi Zarządzanie ACS tooConfigure tożsamości usługi</span><span class="sxs-lookup"><span data-stu-id="5eb10-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="5eb10-156">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="5eb10-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="5eb10-157">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="5eb10-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="5eb10-158">BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)</span><span class="sxs-lookup"><span data-stu-id="5eb10-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="5eb10-159">BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)</span><span class="sxs-lookup"><span data-stu-id="5eb10-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="5eb10-160">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="5eb10-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="5eb10-161">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="5eb10-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

