---
title: "Niestandardowe ustawienia dla środowiska usługi App Service"
description: "Niestandardowych ustawień konfiguracji środowiska usługi App Service"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="55671-103">Niestandardowych ustawień konfiguracji środowiska usługi App Service</span><span class="sxs-lookup"><span data-stu-id="55671-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="55671-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="55671-104">Overview</span></span>
<span data-ttu-id="55671-105">Ponieważ środowiska usługi aplikacji są izolowane jednego odbiorcy, istnieją pewne ustawienia konfiguracji, które mogą być stosowane wyłącznie do środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="55671-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="55671-106">W tym artykule opisano różne specjalnego dostosowania, które są dostępne dla środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="55671-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="55671-107">Jeśli nie masz środowisko usługi aplikacji, zobacz [tworzenie środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="55671-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="55671-108">Dostosowywanie środowiska usługi aplikacji może przechowywać przy użyciu tablicy w nowym **clusterSettings** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="55671-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="55671-109">Ten atrybut zostanie znaleziony w słowniku "Właściwości" *hostingEnvironments* jednostki usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55671-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="55671-110">Następujące skróconej Menedżera zasobów szablonu fragment kodu przedstawia **clusterSettings** atrybutu:</span><span class="sxs-lookup"><span data-stu-id="55671-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="55671-111">**ClusterSettings** atrybut może być uwzględniany w szablonie usługi Resource Manager, aby zaktualizować środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55671-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="55671-112">Użyj Eksploratora zasobów Azure, aby zaktualizować środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="55671-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="55671-113">Alternatywnie można zaktualizować środowiska usługi aplikacji przy użyciu [Eksploratora zasobów Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55671-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="55671-114">W Eksploratorze zasobów, przejdź do węzła dla środowiska usługi aplikacji (**subskrypcje** > **resourceGroups** > **dostawców** > **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="55671-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="55671-115">Następnie kliknij przycisk określonego środowiska usługi aplikacji, które chcesz zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="55671-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="55671-116">W okienku po prawej stronie kliknij **odczytu/zapisu** w pasku narzędzi u góry umożliwia interakcyjne edycji w Eksploratorze zasobów.</span><span class="sxs-lookup"><span data-stu-id="55671-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="55671-117">Polecenie **Edytuj** przycisk, aby dokonać edycji szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55671-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="55671-118">Przewiń w dół w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="55671-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="55671-119">**ClusterSettings** atrybut jest u dołu, gdzie można wprowadzić lub zaktualizować jej wartość.</span><span class="sxs-lookup"><span data-stu-id="55671-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="55671-120">Wpisz (lub skopiuj i Wklej) tablica wartości konfiguracji w **clusterSettings** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="55671-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="55671-121">Kliknij zielony **PUT** przycisku, który ma znajdujący się u góry w okienku po prawej stronie można przekazać zmian do środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55671-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="55671-122">Jednak wprowadzane zmiany trwa około 30 minut pomnożona przez liczbę front zakończeń w środowisku usługi aplikacji, aby zmiany zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="55671-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="55671-123">Na przykład jeśli środowiska usługi aplikacji ma cztery zakończenia frontonu, potrwa około dwie godziny na zakończenie aktualizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="55671-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="55671-124">Gdy jest Trwa wprowadzanie zmian w konfiguracji, nie ma innych operacji skalowania lub operacje zmiany konfiguracji może mieć miejsce w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55671-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="55671-125">Wyłączenie protokołu TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="55671-125">Disable TLS 1.0</span></span>
<span data-ttu-id="55671-126">Cyklicznego zapytania od klientów, szczególnie w przypadku klientów, którzy mają do czynienia z zgodności PCI kontroli, jak jawnie wyłączenie protokołu TLS 1.0 dla swoich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55671-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="55671-127">Protokołu TLS 1.0, można wyłączyć za pomocą następujących **clusterSettings** wpis:</span><span class="sxs-lookup"><span data-stu-id="55671-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="55671-128">Zmień kolejność użycia mechanizmów szyfrowania TLS</span><span class="sxs-lookup"><span data-stu-id="55671-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="55671-129">Następne pytanie od klientów jest jeśli one zmodyfikuj listę szyfrów wynegocjowanym przez ich serwer i można to osiągnąć, modyfikując **clusterSettings** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="55671-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="55671-130">Lista dostępnych mechanizmach szyfrowania można pobrać z [ten artykuł w witrynie MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="55671-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="55671-131">Jeśli wartości są ustawiane dla mechanizmów szyfrowania, który SChannel nie może zrozumieć, całą komunikację TLS do serwera mogą przestać działać.</span><span class="sxs-lookup"><span data-stu-id="55671-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="55671-132">W takim przypadku należy usunąć *FrontEndSSLCipherSuiteOrder* wpisu z **clusterSettings** i Prześlij zaktualizowany szablon usługi Resource Manager, aby powrócić do domyślnych ustawień pakietu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="55671-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="55671-133">Użyj tej funkcji należy z rozwagą.</span><span class="sxs-lookup"><span data-stu-id="55671-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="55671-134">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="55671-134">Get started</span></span>
<span data-ttu-id="55671-135">Witryna szablon Menedżera zasobów Azure szybkiego startu zawiera szablon z podstawowej definicji dla [tworzenie środowiska usługi aplikacji](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="55671-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
