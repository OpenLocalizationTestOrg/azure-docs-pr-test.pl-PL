---
title: Brama danych lokalnych aaaOn | Dokumentacja firmy Microsoft
description: "Brama lokalnego jest konieczne, jeśli serwer usług Analysis Services na platformie Azure będą łączyć tooon lokalnych źródeł danych."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="59ffb-103">Łączenie tooon lokalnych źródeł danych z lokalnego Azure bramy danych</span><span class="sxs-lookup"><span data-stu-id="59ffb-103">Connecting tooon-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="59ffb-104">Brama danych lokalne powitania działa jako mostka zapewnianie bezpiecznego transferu danych między lokalnych źródeł danych i w chmurze hello serwerów usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="59ffb-104">hello on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in hello cloud.</span></span> <span data-ttu-id="59ffb-105">W tooworking dodanie z wieloma serwerami usług Azure Analysis Services w hello tego samego regionu, hello najnowszą wersję bramy hello współdziała również z usługi Azure Logic Apps, usługi Power BI aplikacje zasilania i Flow firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="59ffb-105">In addition tooworking with multiple Azure Analysis Services servers in hello same region, hello latest version of hello gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="59ffb-106">Można skojarzyć wielu usług w hello tym samym regionie z pojedynczą bramą.</span><span class="sxs-lookup"><span data-stu-id="59ffb-106">You can associate multiple services in hello same region with a single gateway.</span></span> 

 <span data-ttu-id="59ffb-107">Zasób bramy w hello wymaga usług Azure Analysis Services tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="59ffb-107">Azure Analysis Services requires a gateway resource in hello same region.</span></span> <span data-ttu-id="59ffb-108">Na przykład jeśli masz serwery usług Azure Analysis Services w regionie wschodnie stany USA 2 hello należy zasobu bramy w regionie wschodnie stany USA 2 hello.</span><span class="sxs-lookup"><span data-stu-id="59ffb-108">For example, if you have Azure Analysis Services servers in hello East US 2 region, you need a gateway resource in hello East US 2 region.</span></span> <span data-ttu-id="59ffb-109">Wiele serwerów w wschodnie stany USA 2 można użyć hello tą samą bramą.</span><span class="sxs-lookup"><span data-stu-id="59ffb-109">Multiple servers in East US 2 can use hello same gateway.</span></span>

<span data-ttu-id="59ffb-110">Pobieranie konfiguracji z hello bramy hello po raz pierwszy jest procesem czteroczęściową:</span><span class="sxs-lookup"><span data-stu-id="59ffb-110">Getting setup with hello gateway hello first time is a four-part process:</span></span>

- <span data-ttu-id="59ffb-111">**Pobierz i uruchom Instalatora** -tego kroku Usługa bramy są instalowane na komputerze w organizacji.</span><span class="sxs-lookup"><span data-stu-id="59ffb-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="59ffb-112">**Zarejestruj bramę** — w tym kroku określ nazwę i odzyskiwanie klucza bramy i wybierz region, rejestrowanie bramy z hello usługi bramy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="59ffb-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with hello Gateway Cloud Service.</span></span>

- <span data-ttu-id="59ffb-113">**Tworzenie zasobu bramy na platformie Azure** — w tym kroku tworzenia zasobu bramy w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59ffb-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="59ffb-114">**Połącz zasób serwerów bramy tooyour** — po utworzeniu zasobu bramy w ramach subskrypcji, możesz rozpocząć łączenia z tooit serwerów.</span><span class="sxs-lookup"><span data-stu-id="59ffb-114">**Connect your servers tooyour gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers tooit.</span></span>

<span data-ttu-id="59ffb-115">Po utworzeniu zasobu bramy skonfigurowane dla Twojej subskrypcji, można połączyć wiele serwerów i tooit innych usług.</span><span class="sxs-lookup"><span data-stu-id="59ffb-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services tooit.</span></span> <span data-ttu-id="59ffb-116">Tylko muszą tooinstall różnych bramy i Utwórz zasoby dodatkowe bramy, jeśli masz serwery lub innych usług w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="59ffb-116">You only need tooinstall a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="59ffb-117">Zobacz tooget pracę już teraz, [Zainstaluj i skonfiguruj bramę danych lokalnych](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="59ffb-117">tooget started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="59ffb-118"><a name="how-it-works"></a>Jak to działa</span><span class="sxs-lookup"><span data-stu-id="59ffb-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="59ffb-119">Brama Hello zainstalować na komputerze w organizacji działa jako usługa systemu Windows, **bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="59ffb-119">hello gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="59ffb-120">Ta usługa lokalna jest zarejestrowany hello usługi bramy w chmurze za pomocą usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="59ffb-120">This local service is registered with hello Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="59ffb-121">Następnie można utworzyć zasobu bramy usługi bramy w chmurze dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59ffb-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="59ffb-122">Twoje Azure Analysis Services, serwery są następnie połączony tooyour zasobów bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-122">Your Azure Analysis Services servers are then connected tooyour gateway resource.</span></span> <span data-ttu-id="59ffb-123">Gdy modele tooyour tooconnect potrzeby z serwera lokalnego źródła danych do zapytań lub przetwarzania zapytań i danych przepływu traverses hello bramy zasób usługi Azure Service Bus hello Usługa bramy lokalnej lokalnymi danymi i źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="59ffb-123">When models on your server need tooconnect tooyour on-premises data sources for queries or processing, a query and data flow traverses hello gateway resource, Azure Service Bus, hello local on-premises data gateway service, and your data sources.</span></span> 

![Jak to działa](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="59ffb-125">Zapytania i przepływ danych:</span><span class="sxs-lookup"><span data-stu-id="59ffb-125">Queries and data flow:</span></span>

1. <span data-ttu-id="59ffb-126">Zapytanie jest tworzony przez usługi w chmurze hello o hello zaszyfrowane poświadczenia dla źródła danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-126">A query is created by hello cloud service with hello encrypted credentials for hello on-premises data source.</span></span> <span data-ttu-id="59ffb-127">Następnie został wysłany tooa kolejki hello tooprocess bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-127">It's then sent tooa queue for hello gateway tooprocess.</span></span>
2. <span data-ttu-id="59ffb-128">Witaj usługi bramy w chmurze analizuje zapytania hello i wypchnięcia toohello żądania hello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="59ffb-128">hello gateway cloud service analyzes hello query and pushes hello request toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="59ffb-129">Brama danych lokalne powitania sonduje hello Azure Service Bus dla żądań oczekujących.</span><span class="sxs-lookup"><span data-stu-id="59ffb-129">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="59ffb-130">bramy Hello pobiera hello zapytania, odszyfrowuje hello poświadczeń i łączy toohello źródeł danych z tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="59ffb-130">hello gateway gets hello query, decrypts hello credentials, and connects toohello data sources with those credentials.</span></span>
5. <span data-ttu-id="59ffb-131">Brama Hello wysyła źródła danych toohello hello kwerendy do wykonania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-131">hello gateway sends hello query toohello data source for execution.</span></span>
6. <span data-ttu-id="59ffb-132">wyniki Hello są wysyłane z hello źródła danych, brama toohello Wstecz, a następnie na powitania usługi w chmurze, jak i na serwerze.</span><span class="sxs-lookup"><span data-stu-id="59ffb-132">hello results are sent from hello data source, back toohello gateway, and then onto hello cloud service and your server.</span></span>

## <span data-ttu-id="59ffb-133"><a name="windows-service-account"></a>Konta usługi systemu Windows</span><span class="sxs-lookup"><span data-stu-id="59ffb-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="59ffb-134">Hello bramy danych lokalnych jest skonfigurowany toouse *NT SERVICE\PBIEgwService* dla poświadczeń logowania usługi Windows hello.</span><span class="sxs-lookup"><span data-stu-id="59ffb-134">hello on-premises data gateway is configured toouse *NT SERVICE\PBIEgwService* for hello Windows service logon credential.</span></span> <span data-ttu-id="59ffb-135">Domyślnie ma hello prawym końcu Logowanie jako usługa; w kontekście hello hello maszyna bramy hello jest instalowany na.</span><span class="sxs-lookup"><span data-stu-id="59ffb-135">By default, it has hello right of Logon as a service; in hello context of hello machine that you are installing hello gateway on.</span></span> <span data-ttu-id="59ffb-136">To poświadczenie nie jest hello tego samego źródła danych konto używane tooconnect tooon lokalnego lub konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59ffb-136">This credential is not hello same account used tooconnect tooon-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="59ffb-137">Jeśli wystąpią problemy z serwerem proxy powodu tooauthentication, może być toochange hello Windows usługa tooa użytkownika domeny lub zarządzane konto usługi.</span><span class="sxs-lookup"><span data-stu-id="59ffb-137">If you encounter issues with your proxy server due tooauthentication, you may want toochange hello Windows service account tooa domain user or managed service account.</span></span>

## <span data-ttu-id="59ffb-138"><a name="ports"></a>Portów</span><span class="sxs-lookup"><span data-stu-id="59ffb-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="59ffb-139">Brama Hello tworzy tooAzure wychodzące połączenie usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="59ffb-139">hello gateway creates an outbound connection tooAzure Service Bus.</span></span> <span data-ttu-id="59ffb-140">Komunikuje się ona portów wychodzących: TCP 443 (ustawienie domyślne), 5671, 5672, 9350 za pośrednictwem 9354.</span><span class="sxs-lookup"><span data-stu-id="59ffb-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="59ffb-141">Hello bramy nie jest wymagane porty dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="59ffb-141">hello gateway does not require inbound ports.</span></span>

<span data-ttu-id="59ffb-142">Firma Microsoft zaleca dozwolonych adresów IP hello w Twoim regionie danych w zaporze.</span><span class="sxs-lookup"><span data-stu-id="59ffb-142">We recommend you whitelist hello IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="59ffb-143">Możesz pobrać hello [listy Microsoft Azure Datacenter IP](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="59ffb-143">You can download hello [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="59ffb-144">Ta lista jest aktualizowana co tydzień.</span><span class="sxs-lookup"><span data-stu-id="59ffb-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="59ffb-145">Adresy IP Hello hello Azure Datacenter IP liście znajdują się w notacji CIDR.</span><span class="sxs-lookup"><span data-stu-id="59ffb-145">hello IP Addresses listed in hello Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="59ffb-146">Na przykład 10.0.0.0/24 oznacza 10.0.0.0 za pośrednictwem 10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="59ffb-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="59ffb-147">Dowiedz się więcej o hello [notacji CIDR](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="59ffb-147">Learn more about hello [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="59ffb-148">Oto Hello hello w pełni kwalifikowana nazwy domeny używane przez hello bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-148">hello following are hello fully qualified domain names used by hello gateway.</span></span>

| <span data-ttu-id="59ffb-149">Nazwy domen</span><span class="sxs-lookup"><span data-stu-id="59ffb-149">Domain names</span></span> | <span data-ttu-id="59ffb-150">Porty wyjściowe</span><span class="sxs-lookup"><span data-stu-id="59ffb-150">Outbound ports</span></span> | <span data-ttu-id="59ffb-151">Opis</span><span class="sxs-lookup"><span data-stu-id="59ffb-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59ffb-152">*. witrynie powerbi.com</span><span class="sxs-lookup"><span data-stu-id="59ffb-152">*.powerbi.com</span></span> |<span data-ttu-id="59ffb-153">80</span><span class="sxs-lookup"><span data-stu-id="59ffb-153">80</span></span> |<span data-ttu-id="59ffb-154">Instalator hello toodownload HTTP używany.</span><span class="sxs-lookup"><span data-stu-id="59ffb-154">HTTP used toodownload hello installer.</span></span> |
| <span data-ttu-id="59ffb-155">*. witrynie powerbi.com</span><span class="sxs-lookup"><span data-stu-id="59ffb-155">*.powerbi.com</span></span> |<span data-ttu-id="59ffb-156">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-156">443</span></span> |<span data-ttu-id="59ffb-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="59ffb-157">HTTPS</span></span> |
| <span data-ttu-id="59ffb-158">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="59ffb-158">*.analysis.windows.net</span></span> |<span data-ttu-id="59ffb-159">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-159">443</span></span> |<span data-ttu-id="59ffb-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="59ffb-160">HTTPS</span></span> |
| <span data-ttu-id="59ffb-161">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="59ffb-161">*.login.windows.net</span></span> |<span data-ttu-id="59ffb-162">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-162">443</span></span> |<span data-ttu-id="59ffb-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="59ffb-163">HTTPS</span></span> |
| <span data-ttu-id="59ffb-164">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="59ffb-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="59ffb-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="59ffb-165">5671-5672</span></span> |<span data-ttu-id="59ffb-166">Zaawansowane kolejkowania wiadomości protokołu (protokół AMQP)</span><span class="sxs-lookup"><span data-stu-id="59ffb-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="59ffb-167">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="59ffb-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="59ffb-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="59ffb-168">443, 9350-9354</span></span> |<span data-ttu-id="59ffb-169">Obiekty nasłuchujące na przekaźnik magistrali usług za pośrednictwem protokołu TCP (wymaga 443 dla tokenu przejęcie kontroli dostępu)</span><span class="sxs-lookup"><span data-stu-id="59ffb-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="59ffb-170">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="59ffb-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="59ffb-171">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-171">443</span></span> |<span data-ttu-id="59ffb-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="59ffb-172">HTTPS</span></span> |
| <span data-ttu-id="59ffb-173">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="59ffb-173">*.core.windows.net</span></span> |<span data-ttu-id="59ffb-174">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-174">443</span></span> |<span data-ttu-id="59ffb-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="59ffb-175">HTTPS</span></span> |
| <span data-ttu-id="59ffb-176">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="59ffb-176">login.microsoftonline.com</span></span> |<span data-ttu-id="59ffb-177">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-177">443</span></span> |<span data-ttu-id="59ffb-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="59ffb-178">HTTPS</span></span> |
| <span data-ttu-id="59ffb-179">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="59ffb-179">*.msftncsi.com</span></span> |<span data-ttu-id="59ffb-180">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-180">443</span></span> |<span data-ttu-id="59ffb-181">Połączenie z Internetem tootest należy użyć, jeśli brama hello jest nieosiągalny za hello usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="59ffb-181">Used tootest internet connectivity if hello gateway is unreachable by hello Power BI service.</span></span> |
| <span data-ttu-id="59ffb-182">*.microsoftonline p.com</span><span class="sxs-lookup"><span data-stu-id="59ffb-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="59ffb-183">443</span><span class="sxs-lookup"><span data-stu-id="59ffb-183">443</span></span> |<span data-ttu-id="59ffb-184">Używany do uwierzytelniania w zależności od konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="59ffb-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="59ffb-185"><a name="force-https"></a>Wymuszanie komunikację HTTPS z usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="59ffb-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="59ffb-186">Możesz wymusić hello toocommunicate bramy z usługi Azure Service Bus przy użyciu protokołu HTTPS zamiast bezpośredniego TCP; Jednak to tak może znacznie zmniejszyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="59ffb-186">You can force hello gateway toocommunicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="59ffb-187">Można zmodyfikować hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* pliku, zmieniając wartość hello z `AutoDetect` zbyt`Https`.</span><span class="sxs-lookup"><span data-stu-id="59ffb-187">You can modify hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing hello value from `AutoDetect` too`Https`.</span></span> <span data-ttu-id="59ffb-188">Ten plik znajduje się zwykle w *bramy danych lokalnych Files\On C:\Program*.</span><span class="sxs-lookup"><span data-stu-id="59ffb-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="59ffb-189"><a name="faq"></a>Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="59ffb-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="59ffb-190">Ogólne</span><span class="sxs-lookup"><span data-stu-id="59ffb-190">General</span></span>

<span data-ttu-id="59ffb-191">**Q**: należy bramy dla źródeł danych w chmurze hello, takie jak bazy danych SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="59ffb-191">**Q**: Do I need a gateway for data sources in hello cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="59ffb-192">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="59ffb-192">
**A**: No.</span></span> <span data-ttu-id="59ffb-193">Brama łączy lokalnych tooon tylko źródła danych.</span><span class="sxs-lookup"><span data-stu-id="59ffb-193">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="59ffb-194">**Q**: hello bramy ma zainstalowane na powitania sam komputer jako źródło danych hello toobe?</span><span class="sxs-lookup"><span data-stu-id="59ffb-194">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="59ffb-195">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="59ffb-195">
**A**: No.</span></span> <span data-ttu-id="59ffb-196">Brama Hello łączy toohello źródła danych przy użyciu informacji o połączeniu hello dostarczony.</span><span class="sxs-lookup"><span data-stu-id="59ffb-196">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="59ffb-197">Jako aplikacja klienta, w tym sensie, należy wziąć pod uwagę hello bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-197">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="59ffb-198">Witaj bramy wystarczy hello możliwości tooconnect toohello nazwy serwera podany, zwykle na powitania sam sieci.</span><span class="sxs-lookup"><span data-stu-id="59ffb-198">hello gateway just needs hello capability tooconnect toohello server name that was provided, typically on hello same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="59ffb-199">**Q**: Dlaczego muszą toouse służbowego lub szkolnego konta toosign w?</span><span class="sxs-lookup"><span data-stu-id="59ffb-199">**Q**: Why do I need toouse a work or school account toosign in?</span></span> <br/><span data-ttu-id="59ffb-200">
**A**: można używać Praca Azure lub tylko konta służbowego, po zainstalowaniu bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-200">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="59ffb-201">Twoje konto logowania są przechowywane w dzierżawie, który jest zarządzany przez usługę Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59ffb-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="59ffb-202">Zazwyczaj główna nazwa użytkownika konta usługi Azure AD (UPN) jest zgodna hello adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="59ffb-202">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="59ffb-203">**Q**: moich poświadczeń przechowywania?</span><span class="sxs-lookup"><span data-stu-id="59ffb-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="59ffb-204">
**A**: poświadczenia powitania dla źródła danych są szyfrowane i przechowywane w hello usługi bramy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="59ffb-204">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello Gateway Cloud Service.</span></span> <span data-ttu-id="59ffb-205">poświadczenia Hello są odszyfrowywane w bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-205">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="59ffb-206">**Q**: istnieją wszelkie wymagania dotyczące przepustowości sieci?</span><span class="sxs-lookup"><span data-stu-id="59ffb-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="59ffb-207">
**A**: ma zaleca sieci połączenie ma dobrej przepływności.</span><span class="sxs-lookup"><span data-stu-id="59ffb-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="59ffb-208">Każde środowisko jest inne, a hello ilość danych wysyłanych dotyczy hello wyników.</span><span class="sxs-lookup"><span data-stu-id="59ffb-208">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="59ffb-209">Przy użyciu usługi ExpressRoute może pomóc tooguarantee poziomu przepływności między lokalnymi i hello centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59ffb-209">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="59ffb-210">Możesz użyć hello narzędzia innej firmy Azure szybkości testowanie aplikacji toohelp miernika przepustowość sieci.</span><span class="sxs-lookup"><span data-stu-id="59ffb-210">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="59ffb-211">**Q**: co to jest hello opóźnienie dla źródła danych tooa zapytania uruchomionego z bramy hello?</span><span class="sxs-lookup"><span data-stu-id="59ffb-211">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="59ffb-212">Co to jest architektura najlepsze hello?</span><span class="sxs-lookup"><span data-stu-id="59ffb-212">What is hello best architecture?</span></span> <br/><span data-ttu-id="59ffb-213">
**A**: tooreduce opóźnienia sieci, zainstaluj hello bramy jako źródło danych zamknij toohello, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="59ffb-213">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="59ffb-214">Po zainstalowaniu bramy hello w źródle danych rzeczywistych hello, to zbliżeniowe minimalizuje opóźnienia hello wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="59ffb-214">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="59ffb-215">Rozważ zbyt hello centrów danych.</span><span class="sxs-lookup"><span data-stu-id="59ffb-215">Consider hello datacenters too.</span></span> <span data-ttu-id="59ffb-216">Na przykład jeśli usługa używa hello datacenter zachodnie stany USA, a masz programu SQL Server w maszynie Wirtualnej platformy Azure, maszyny Wirtualnej Azure należy w hello zachodnie stany USA zbyt.</span><span class="sxs-lookup"><span data-stu-id="59ffb-216">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="59ffb-217">Ta bliskości zmniejsza opóźnienia i pozwala uniknąć opłaty za wyjście na powitania maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59ffb-217">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="59ffb-218">**Q**: w jaki sposób wyniki wysyłane wstecz toohello chmury?</span><span class="sxs-lookup"><span data-stu-id="59ffb-218">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="59ffb-219">
**A**: wyniki są wysyłane za pośrednictwem hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="59ffb-219">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="59ffb-220">**Q**: czy istnieją bramy toohello wszystkie połączenia przychodzące z chmury hello?</span><span class="sxs-lookup"><span data-stu-id="59ffb-220">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="59ffb-221">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="59ffb-221">
**A**: No.</span></span> <span data-ttu-id="59ffb-222">Brama Hello używa połączenia wychodzące tooAzure usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="59ffb-222">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="59ffb-223">**Q**: co zrobić, jeśli zablokowanie połączeń wychodzących?</span><span class="sxs-lookup"><span data-stu-id="59ffb-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="59ffb-224">Czego potrzebuję tooopen?</span><span class="sxs-lookup"><span data-stu-id="59ffb-224">What do I need tooopen?</span></span> <br/><span data-ttu-id="59ffb-225">
**A**: Zobacz hello portów i hostów, które hello używa bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-225">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="59ffb-226">**Q**: rzeczywiste usługi Windows hello tzw?</span><span class="sxs-lookup"><span data-stu-id="59ffb-226">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="59ffb-227">
**A**: W usługach, bramy hello nosi nazwę lokalną usługę bramy danych.</span><span class="sxs-lookup"><span data-stu-id="59ffb-227">
**A**: In Services, hello gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="59ffb-228">**Q**: można hello usługa systemu Windows bramy uruchomione przy użyciu konta usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59ffb-228">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="59ffb-229">
**A**: nie.</span><span class="sxs-lookup"><span data-stu-id="59ffb-229">
**A**: No.</span></span> <span data-ttu-id="59ffb-230">Usługa Windows Hello muszą mieć prawidłowe konto systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="59ffb-230">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="59ffb-231">Domyślnie usługa hello jest uruchamiana z hello SID usługi NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="59ffb-231">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="59ffb-232"><a name="high-availability"></a>Wysoka dostępność i odzyskiwanie po awarii</span><span class="sxs-lookup"><span data-stu-id="59ffb-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="59ffb-233">**Q**: jakie opcje są dostępne dla odzyskiwania po awarii?</span><span class="sxs-lookup"><span data-stu-id="59ffb-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="59ffb-234">
**A**: możesz użyć toorestore klucza odzyskiwania hello lub przenieść bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-234">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="59ffb-235">Po zainstalowaniu bramy hello Określ hello klucza odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-235">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="59ffb-236">**Q**: co to jest korzyść hello hello klucza odzyskiwania?</span><span class="sxs-lookup"><span data-stu-id="59ffb-236">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="59ffb-237">
**A**: hello klucza odzyskiwania zawiera toomigrate sposób lub odzyskiwanie po awarii ustawienia bramy.</span><span class="sxs-lookup"><span data-stu-id="59ffb-237">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="59ffb-238"><a name="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="59ffb-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="59ffb-239">**Q**: jak zobaczyć, jakie zapytania są wysyłane toohello lokalnego źródła danych?</span><span class="sxs-lookup"><span data-stu-id="59ffb-239">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="59ffb-240">
**A**: można włączyć funkcja śledzenia zapytań, w tym hello zapytań, które są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="59ffb-240">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="59ffb-241">Należy pamiętać, zapytania toochange Śledzenie wstecz toohello oryginalnej wartości po zakończeniu rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="59ffb-241">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="59ffb-242">Jeśli pozostanie włączona funkcja śledzenia zapytań tworzy większe dzienniki.</span><span class="sxs-lookup"><span data-stu-id="59ffb-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="59ffb-243">Można też przyjrzeć się narzędzia, które ma źródła danych śledzenia zapytań.</span><span class="sxs-lookup"><span data-stu-id="59ffb-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="59ffb-244">Na przykład można użyć zdarzeń rozszerzonych lub profilera SQL dla programu SQL Server i usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="59ffb-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="59ffb-245">**Q**: gdzie są dzienniki bramy hello?</span><span class="sxs-lookup"><span data-stu-id="59ffb-245">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="59ffb-246">
**A**: Zobacz dzienniki w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="59ffb-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="59ffb-247"><a name="update"></a>Aktualizacja toohello najnowszej wersji</span><span class="sxs-lookup"><span data-stu-id="59ffb-247"><a name="update"></a>Update toohello latest version</span></span>

<span data-ttu-id="59ffb-248">Wiele problemów można powierzchni, gdy wersja bramy hello staje się nieaktualne.</span><span class="sxs-lookup"><span data-stu-id="59ffb-248">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="59ffb-249">Dobrym rozwiązaniem ogólne upewnij się, że używasz najnowszej wersji powitania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-249">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="59ffb-250">Witaj bramy nie były aktualizowane przez miesiąc lub dłużej, może zaleca się zainstalowanie najnowszej wersji bramy hello hello i zobacz, czy można odtworzyć problem hello.</span><span class="sxs-lookup"><span data-stu-id="59ffb-250">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="59ffb-251">Błąd: Nie tooadd toogroup użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59ffb-251">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="59ffb-252">(Użytkownicy dzienników wydajności PBIEgwService-2147463168)</span><span class="sxs-lookup"><span data-stu-id="59ffb-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="59ffb-253">Być może ten błąd przy próbie tooinstall hello bramy na kontrolerze domeny, który nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="59ffb-253">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="59ffb-254">Upewnij się, wdrożenie bramy hello na komputerze, który nie jest kontrolerem domeny.</span><span class="sxs-lookup"><span data-stu-id="59ffb-254">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="59ffb-255"><a name="logs"></a>Dzienniki</span><span class="sxs-lookup"><span data-stu-id="59ffb-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="59ffb-256">Pliki dziennika są zasobów ważne podczas rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="59ffb-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="59ffb-257">Dzienniki usługi bramy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="59ffb-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="59ffb-258">Dzienniki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="59ffb-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="59ffb-259">Dzienniki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="59ffb-259">Event logs</span></span>

<span data-ttu-id="59ffb-260">Możesz znaleźć hello dzienniki bramy zarządzania danymi i PowerBIGateway w obszarze **Dzienniki aplikacji i usług**.</span><span class="sxs-lookup"><span data-stu-id="59ffb-260">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="59ffb-261"><a name="telemetry"></a>Telemetrii</span><span class="sxs-lookup"><span data-stu-id="59ffb-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="59ffb-262">Dane telemetryczne może służyć do monitorowania i rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="59ffb-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="59ffb-263">Domyślnie</span><span class="sxs-lookup"><span data-stu-id="59ffb-263">By default</span></span>

<span data-ttu-id="59ffb-264">**tooturn na telemetrii**</span><span class="sxs-lookup"><span data-stu-id="59ffb-264">**tooturn on telemetry**</span></span>

1.  <span data-ttu-id="59ffb-265">Sprawdź katalog danych lokalnymi hello klienta bramy na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="59ffb-265">Check hello On-premises data gateway client directory on hello computer.</span></span> <span data-ttu-id="59ffb-266">Zazwyczaj jest **bramy danych %systemdrive%\Program lokalnych Files\On**.</span><span class="sxs-lookup"><span data-stu-id="59ffb-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="59ffb-267">Lub, otwórz konsolę usługi i sprawdź tooexecutable ścieżka hello: właściwość Usługa bramy danych lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="59ffb-267">Or, you can open a Services console and check hello Path tooexecutable: A property of hello On-premises data gateway service.</span></span>
2.  <span data-ttu-id="59ffb-268">W pliku Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config hello z katalogu klienta.</span><span class="sxs-lookup"><span data-stu-id="59ffb-268">In hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="59ffb-269">Zmień hello SendTelemetry ustawienie tootrue.</span><span class="sxs-lookup"><span data-stu-id="59ffb-269">Change hello SendTelemetry setting tootrue.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="59ffb-270">Zapisz zmiany i ponownie uruchom usługę Windows hello: lokalnej usługi bramy danych.</span><span class="sxs-lookup"><span data-stu-id="59ffb-270">Save your changes and restart hello Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="59ffb-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59ffb-271">Next steps</span></span>
* [<span data-ttu-id="59ffb-272">Zarządzanie usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="59ffb-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="59ffb-273">Pobieranie danych z usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="59ffb-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
