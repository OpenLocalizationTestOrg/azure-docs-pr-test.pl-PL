---
title: "Ustawienia aaaCustom dla środowiska usługi App Service"
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
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="7c495-103">Niestandardowych ustawień konfiguracji środowiska usługi App Service</span><span class="sxs-lookup"><span data-stu-id="7c495-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="7c495-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7c495-104">Overview</span></span>
<span data-ttu-id="7c495-105">Ponieważ środowiska usługi aplikacji są izolowane tooa jednego odbiorcy, istnieją pewne ustawienia konfiguracji, które mogą być stosowane wyłącznie tooApp środowiska usługi.</span><span class="sxs-lookup"><span data-stu-id="7c495-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="7c495-106">Ten artykuł dokumenty hello różnych specjalnego dostosowania, które są dostępne dla środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="7c495-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="7c495-107">Jeśli nie masz środowisko usługi aplikacji, zobacz [jak tooCreate środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="7c495-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="7c495-108">Dostosowywanie środowiska usługi aplikacji może przechowywać przy użyciu tablicy w hello nowe **clusterSettings** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c495-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="7c495-109">Ten atrybut zostanie znaleziony w słownik "Właściwości" hello hello *hostingEnvironments* jednostki usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c495-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="7c495-110">Witaj poniższy fragment skróconej szablonu usługi Resource Manager zawiera hello **clusterSettings** atrybutu:</span><span class="sxs-lookup"><span data-stu-id="7c495-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="7c495-111">Witaj **clusterSettings** atrybut może być uwzględniany w Resource Manager hello tooupdate szablonu środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c495-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="7c495-112">Użyj Eksploratora zasobów Azure tooupdate środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="7c495-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="7c495-113">Alternatywnie można zaktualizować hello środowiska usługi aplikacji przy użyciu [Eksploratora zasobów Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c495-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="7c495-114">W Eksploratorze zasobów Przejdź węzła toohello dla środowiska usługi aplikacji hello (**subskrypcje** > **resourceGroups** > **dostawców**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="7c495-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="7c495-115">Następnie kliknij przycisk hello określonego środowiska usługi aplikacji, które mają tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7c495-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="7c495-116">W okienku po prawej stronie powitania, kliknij przycisk **odczytu/zapisu** w tooallow narzędzi u góry hello interakcyjne edycji w Eksploratorze zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c495-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="7c495-117">Kliknij przycisk hello niebieski **Edytuj** edycji szablonu usługi Resource Manager hello toomake przycisku.</span><span class="sxs-lookup"><span data-stu-id="7c495-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="7c495-118">Przewiń w dół toohello hello prawego okienka.</span><span class="sxs-lookup"><span data-stu-id="7c495-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="7c495-119">Witaj **clusterSettings** atrybut jest bardzo dole hello, gdzie można wprowadzić lub zaktualizować jej wartość.</span><span class="sxs-lookup"><span data-stu-id="7c495-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="7c495-120">Typ (lub kopiowania i wklejania) hello tablicę wartości konfiguracji w hello **clusterSettings** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c495-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="7c495-121">Kliknij zielony hello **PUT** przycisku, który ma znajdujący się u góry hello hello prawym okienku toocommit hello zmiany toohello środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c495-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="7c495-122">Jednak wprowadzane zmiany hello trwa około 30 minut pomnożona przez hello liczba przedniego kończy się hello środowiska usługi aplikacji hello zmiany tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="7c495-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="7c495-123">Na przykład jeśli środowiska usługi aplikacji ma cztery zakończenia frontonu, potrwa około dwie godziny dla toofinish aktualizacji konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="7c495-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="7c495-124">Gdy jest Trwa wprowadzanie zmian w konfiguracji hello, nie ma innych operacji skalowania lub operacje zmiany konfiguracji może mieć miejsce w hello środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c495-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="7c495-125">Wyłączenie protokołu TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="7c495-125">Disable TLS 1.0</span></span>
<span data-ttu-id="7c495-126">Cyklicznego zapytania od klientów, szczególnie w przypadku klientów, którzy mają do czynienia z zgodności PCI inspekcji, jest sposób tooexplicitly wyłączenie protokołu TLS 1.0 dla swoich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c495-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="7c495-127">Protokołu TLS 1.0, można wyłączyć za pomocą następujących hello **clusterSettings** wpis:</span><span class="sxs-lookup"><span data-stu-id="7c495-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="7c495-128">Zmień kolejność użycia mechanizmów szyfrowania TLS</span><span class="sxs-lookup"><span data-stu-id="7c495-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="7c495-129">Następne pytanie od klientów jest Jeśli modyfikują hello lista szyfrów wynegocjowanym przez ich serwer i można to osiągnąć, modyfikując hello **clusterSettings** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="7c495-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="7c495-130">Witaj listę dostępnych mechanizmach szyfrowania można pobrać z [ten artykuł w witrynie MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="7c495-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="7c495-131">Jeśli niepoprawne wartości są ustawiane dla hello mechanizmów szyfrowania, który SChannel nie może zrozumieć, wszystkie server tooyour komunikację TLS może przestaną działać.</span><span class="sxs-lookup"><span data-stu-id="7c495-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="7c495-132">W takim przypadku należy tooremove hello *FrontEndSSLCipherSuiteOrder* wpisu z **clusterSettings** i przesyłanie hello zaktualizowane Menedżera zasobów szablonu toorevert wstecz toohello domyślne szyfrowania Ustawienia pakietu.</span><span class="sxs-lookup"><span data-stu-id="7c495-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="7c495-133">Użyj tej funkcji należy z rozwagą.</span><span class="sxs-lookup"><span data-stu-id="7c495-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="7c495-134">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="7c495-134">Get started</span></span>
<span data-ttu-id="7c495-135">Witryna szablon Menedżera zasobów Azure szybkiego startu Hello zawiera szablonu z hello podstawową definicję dla [tworzenie środowiska usługi aplikacji](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="7c495-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
