---
title: "Nazwa wystawcy i klucza wystawcy usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pobrać Nazwa wystawcy i klucza wystawcy dla usługi Service Bus lub kontroli dostępu (ACS) w usługach BizTalk. MABS, WABS"
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
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="5ad86-104">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="5ad86-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="5ad86-105">Azure usługi BizTalk Services używa nazwy wystawcy magistrali usługi i klucza wystawcy i nazwę wystawcy kontroli dostępu i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5ad86-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="5ad86-106">W szczególności:</span><span class="sxs-lookup"><span data-stu-id="5ad86-106">Specifically:</span></span>

| <span data-ttu-id="5ad86-107">Zadanie</span><span class="sxs-lookup"><span data-stu-id="5ad86-107">Task</span></span> | <span data-ttu-id="5ad86-108">Która nazwa wystawcy i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="5ad86-109">Wdrażanie aplikacji w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ad86-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="5ad86-110">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="5ad86-111">Konfigurowanie portalu Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="5ad86-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="5ad86-112">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="5ad86-113">Tworzenie obiektu LOB przekaźników z usługami karty BizTalk w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ad86-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="5ad86-114">Nazwa wystawcy magistrali usługi i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="5ad86-115">W tym temacie przedstawiono kroki, aby pobrać nazwę wystawcy i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5ad86-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="5ad86-116">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="5ad86-117">Nazwa wystawcy kontroli dostępu i klucz wystawcy, są używane przez następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5ad86-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="5ad86-118">Aplikacja usługi BizTalk Azure utworzone w programie Visual Studio: Aby pomyślnie wdrożyć usługę BizTalk aplikacji w programie Visual Studio na platformie Azure, możesz wprowadzić nazwę wystawcy kontroli dostępu i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5ad86-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="5ad86-119">Portalu Azure usługi BizTalk: Podczas tworzenia usługi BizTalk i otwórz Portal usługi BizTalk, nazwa wystawcy kontroli dostępu, a klucz wystawcy automatycznie zarejestrowanych dla wdrożeń o tej samej wartości kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5ad86-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="5ad86-120">Nazwa wystawcy kontroli dostępu i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="5ad86-121">Do usług ACS jest używany do uwierzytelniania i uzyskać wartości nazwy wystawcy i klucza wystawcy, ogólne kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="5ad86-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="5ad86-122">Zainstaluj [poleceń cmdlet programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="5ad86-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="5ad86-123">Dodaj konto platformy Azure:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="5ad86-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="5ad86-124">Zwraca nazwę Twojej subskrypcji:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="5ad86-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="5ad86-125">Wybierz subskrypcję:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="5ad86-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="5ad86-126">Tworzenie nowej przestrzeni nazw:`new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="5ad86-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="5ad86-127">Przykład:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="5ad86-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="5ad86-128">Po utworzeniu nowej przestrzeni nazw usługi ACS, (co może potrwać kilka minut), wartości Nazwa wystawcy i klucza wystawcy są wymienione w ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="5ad86-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

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

<span data-ttu-id="5ad86-129">Podsumowując:</span><span class="sxs-lookup"><span data-stu-id="5ad86-129">To summarize:</span></span>  
<span data-ttu-id="5ad86-130">Nazwa wystawcy = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="5ad86-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="5ad86-131">Klucz wystawcy = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="5ad86-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="5ad86-132">Więcej na temat [AzureSBNamespace nowy](https://msdn.microsoft.com/library/dn495165.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ad86-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="5ad86-133">Nazwa wystawcy magistrali usługi i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="5ad86-134">Nazwa wystawcy magistrali usługi i klucza wystawcy, są używane przez usługi karty BizTalk.</span><span class="sxs-lookup"><span data-stu-id="5ad86-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="5ad86-135">W projekcie usługi BizTalk Services w programie Visual Studio usługi karty BizTalk są używane do nawiązania połączenia lokalnego systemu — biznesowych (LOB).</span><span class="sxs-lookup"><span data-stu-id="5ad86-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="5ad86-136">Nawiązać połączenie, Utwórz LOB przekazywania i wprowadź szczegóły systemu LOB.</span><span class="sxs-lookup"><span data-stu-id="5ad86-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="5ad86-137">W ten sposób można także wprowadzić nazwy wystawcy magistrali usługi i klucza wystawcy.</span><span class="sxs-lookup"><span data-stu-id="5ad86-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="5ad86-138">Pobieranie nazwy wystawcy magistrali usługi i klucza wystawcy</span><span class="sxs-lookup"><span data-stu-id="5ad86-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="5ad86-139">Zaloguj się do [klasycznej witryny Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="5ad86-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="5ad86-140">W lewym okienku nawigacji, wybierz **usługi Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="5ad86-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="5ad86-141">Wybierz obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="5ad86-141">Select your namespace.</span></span> <span data-ttu-id="5ad86-142">Na pasku zadań wybierz **informacje o połączeniu**.</span><span class="sxs-lookup"><span data-stu-id="5ad86-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="5ad86-143">Spowoduje to wyświetlenie **domyślne wystawcy** (Nazwa wystawcy) i **domyślny klucz** (klucza wystawcy).</span><span class="sxs-lookup"><span data-stu-id="5ad86-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="5ad86-144">Można skopiować wartości.</span><span class="sxs-lookup"><span data-stu-id="5ad86-144">Their values can be copied.</span></span>  

<span data-ttu-id="5ad86-145">Podsumowując:</span><span class="sxs-lookup"><span data-stu-id="5ad86-145">To summarize:</span></span>  
<span data-ttu-id="5ad86-146">Nazwa wystawcy = wystawcy domyślne</span><span class="sxs-lookup"><span data-stu-id="5ad86-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="5ad86-147">Klucz wystawcy domyślny klucz =</span><span class="sxs-lookup"><span data-stu-id="5ad86-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="5ad86-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ad86-148">Next</span></span>
<span data-ttu-id="5ad86-149">Dodatkowe tematy usługi BizTalk Azure:</span><span class="sxs-lookup"><span data-stu-id="5ad86-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="5ad86-150">Instalowanie usług Azure BizTalk SDK</span><span class="sxs-lookup"><span data-stu-id="5ad86-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="5ad86-151">Samouczki: Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="5ad86-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="5ad86-152">Jak rozpocząć pracę z zestawem SDK usługi Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="5ad86-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="5ad86-153">Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="5ad86-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="5ad86-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5ad86-154">See Also</span></span>
* [<span data-ttu-id="5ad86-155">Porady: Konfigurowanie tożsamości usługi za pomocą usługi zarządzania ACS</span><span class="sxs-lookup"><span data-stu-id="5ad86-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="5ad86-156">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="5ad86-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="5ad86-157">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="5ad86-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="5ad86-158">BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)</span><span class="sxs-lookup"><span data-stu-id="5ad86-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="5ad86-159">BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)</span><span class="sxs-lookup"><span data-stu-id="5ad86-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="5ad86-160">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="5ad86-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="5ad86-161">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="5ad86-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

