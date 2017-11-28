---
title: "aaaWork przy użyciu istniejących lokalnych serwerów proxy i Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano sposób toowork przy użyciu istniejących lokalnych serwerów proxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="6c8e6-103">Praca z istniejącym lokalnych serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="6c8e6-104">W tym artykule opisano sposób toowork łączniki serwera Proxy aplikacji usługi Azure Active Directory (Azure AD) tooconfigure z serwerów proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="6c8e6-105">Przewodnik jest przeznaczony dla klientów z sieci środowiskach z istniejących serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="6c8e6-106">Rozpoczniemy analizując te scenariusze wdrażania głównego:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="6c8e6-107">Skonfiguruj toobypass łączniki proxy ruchu wychodzącego sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="6c8e6-108">Skonfiguruj toouse łączniki tooaccess serwera proxy ruchu wychodzącego serwera Proxy aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="6c8e6-109">Aby uzyskać więcej informacji na temat działania łączników, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="6c8e6-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="6c8e6-110">Konfigurowanie serwera proxy ruchu wychodzącego hello</span><span class="sxs-lookup"><span data-stu-id="6c8e6-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="6c8e6-111">Jeśli masz serwera proxy ruchu wychodzącego w danym środowisku, należy użyć konta z serwera proxy ruchu wychodzącego hello tooconfigure odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="6c8e6-112">Ponieważ hello Instalator jest uruchamiany w kontekście hello hello użytkownika, który wykonuje hello instalacji, należy sprawdzić konfigurację hello przy użyciu Microsoft Edge lub innej przeglądarki internetowej.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="6c8e6-113">tooconfigure hello ustawienia serwera proxy w programie Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="6c8e6-114">Przejdź za**ustawienia** > **ustawienia zaawansowane widoku** > **Otwórz ustawienia serwera Proxy** > **ręcznego ustawienia serwera Proxy** .</span><span class="sxs-lookup"><span data-stu-id="6c8e6-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="6c8e6-115">Ustaw **Użyj serwera proxy** za**na**, wybierz pozycję hello **nie używaj powitania serwera proxy dla adresów lokalnych (sieć intranet)** pole wyboru, a następnie zmień hello adres i port tooreflect Serwer proxy lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="6c8e6-116">Wypełnij ustawienia serwera proxy niezbędne hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-116">Fill in hello necessary proxy settings.</span></span>

   ![Okno dialogowe ustawień serwera proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="6c8e6-118">Obejście proxy ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="6c8e6-118">Bypass outbound proxies</span></span>

<span data-ttu-id="6c8e6-119">Łączniki mają podstawowych składników systemu operacyjnego, które żądania wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="6c8e6-120">Te składniki automatycznie próbę toolocate serwera proxy w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="6c8e6-121">Korzystają autowykrywania serwera Proxy sieci Web (WPAD), jeśli jest włączona w środowisku hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="6c8e6-122">składniki systemu operacyjnego Hello próba toolocate serwer proxy przeprowadzając wyszukiwania DNS dla wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="6c8e6-123">Jeśli to rozwiązuje w systemie DNS, żądanie HTTP jest przeprowadzane toohello IP adres wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="6c8e6-124">To żądanie staje się hello skryptu konfiguracji serwera proxy w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="6c8e6-125">Łącznik Hello korzysta z tego tooselect skryptu serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="6c8e6-126">Jednak ruch łącznika może nadal nie powiodło się, ze względu na ustawienia dodatkowe czynności konfiguracyjne na powitania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="6c8e6-127">Można skonfigurować toobypass łącznika hello tooensure serwera proxy sieci lokalnej, używa bezpośrednie połączenie toohello Azure usługi.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="6c8e6-128">Zalecamy takie podejście (Jeśli zasady sieci umożliwia on), ponieważ oznacza, że masz jeden mniej toomaintain konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="6c8e6-129">toodisable użycia serwera proxy ruchu wychodzącego dla łącznika hello, Edytuj plik C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config hello i dodać hello *system.net* sekcji pokazano w tym przykładowym kodzie :</span><span class="sxs-lookup"><span data-stu-id="6c8e6-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="6c8e6-130">tooensure hello aktualizator łącznika usługi będzie również pomija powitania serwera proxy, należy podobne zmiany toohello ApplicationProxyConnectorUpdaterService.exe.config plik znajdujący się w aktualizator łącznika serwera Proxy aplikacji usługi AAD C:\Program Files\Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="6c8e6-131">Należy się kopie toomake hello oryginalnych plików, w razie potrzeby toorevert toohello domyślnych .config plików.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="6c8e6-132">Użyj serwera proxy ruchu wychodzącego hello</span><span class="sxs-lookup"><span data-stu-id="6c8e6-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="6c8e6-133">Niektóre środowiska wymagają wszystkich toogo ruch wychodzący za pośrednictwem serwera proxy ruchu wychodzącego, bez wyjątku.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="6c8e6-134">W związku z tym pomijanie powitania serwera proxy nie jest opcją.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="6c8e6-135">Można skonfigurować hello łącznika ruchu toogo za pośrednictwem serwera proxy ruchu wychodzącego hello, pokazane na powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Konfigurowanie łącznika toogo ruchu za pośrednictwem serwera proxy ruchu wychodzącego tooAzure AD serwera Proxy aplikacji](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="6c8e6-137">W związku z tym o tylko ruchu wychodzącego, jest tooconfigure nie konieczności ruchu przychodzącego dostęp za pośrednictwem zapór.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="6c8e6-138">Krok 1: Skonfiguruj łącznik hello i powiązanych usług toogo za pośrednictwem serwera proxy ruchu wychodzącego hello</span><span class="sxs-lookup"><span data-stu-id="6c8e6-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="6c8e6-139">Objętych wcześniej, jeśli WPAD jest włączona w środowisku hello i prawidłowo skonfigurowany, łącznik hello automatycznie wykryje na powitania serwera proxy ruchu wychodzącego toouse serwera, a następnie spróbuj go.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="6c8e6-140">Jednak jawnie skonfigurować toogo łącznika hello za pośrednictwem serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="6c8e6-141">toodo tak, przeprowadź edycję pliku C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config hello i Dodaj hello *system.net* sekcji pokazano w tym przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="6c8e6-142">Zmień *proxyserver:8080* tooreflect swoją nazwę serwera lokalnego serwera proxy lub adres IP i hello portu, że nasłuchuje na.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="6c8e6-143">Skonfiguruj serwer proxy hello aktualizator łącznika usługi toouse hello dokonując podobne zmiany toohello w następującej lokalizacji C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy łącznika Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="6c8e6-144">Krok 2: Konfigurowanie hello proxy tooallow ruch z hello łącznika i powiązane usługi tooflow za pośrednictwem</span><span class="sxs-lookup"><span data-stu-id="6c8e6-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="6c8e6-145">Istnieją cztery tooconsider aspekty na powitania serwera proxy ruchu wychodzącego:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="6c8e6-146">Reguły ruchu wychodzącego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-146">Proxy outbound rules</span></span>
* <span data-ttu-id="6c8e6-147">Uwierzytelnianie serwera proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-147">Proxy authentication</span></span>
* <span data-ttu-id="6c8e6-148">Porty serwera proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-148">Proxy ports</span></span>
* <span data-ttu-id="6c8e6-149">Inspekcja protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="6c8e6-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="6c8e6-150">Reguły ruchu wychodzącego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-150">Proxy outbound rules</span></span>
<span data-ttu-id="6c8e6-151">Zezwalaj na dostęp toohello następujące punkty końcowe dla dostępu do usługi łącznika:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="6c8e6-152">*. msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="6c8e6-152">*.msappproxy.net</span></span>
* <span data-ttu-id="6c8e6-153">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6c8e6-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="6c8e6-154">Początkowa rejestracji Zezwalaj na następujące punkty końcowe toohello dostępu:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="6c8e6-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="6c8e6-155">login.windows.net</span></span>
* <span data-ttu-id="6c8e6-156">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6c8e6-156">login.microsoftonline.com</span></span>

<span data-ttu-id="6c8e6-157">Jeśli nie umożliwiają nawiązywanie połączeń przez nazwę FQDN, a zamiast tego muszą toospecify zakresy adresów IP, należy użyć tych opcji:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="6c8e6-158">Zezwalaj na dostęp ruchu wychodzącego łącznika hello tooall miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="6c8e6-159">Zezwalaj na powitania łącznik wychodzący dostęp za[zakresy IP centrum danych Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6c8e6-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="6c8e6-160">Hello żądania przy użyciu hello listą zakresów IP centrum danych Azure jest, że jest aktualizowana co tydzień.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="6c8e6-161">Należy tooput procesu w miejscu tooensure odpowiednio aktualizowany reguł dostępu.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="6c8e6-162">Uwierzytelnianie serwera proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-162">Proxy authentication</span></span>

<span data-ttu-id="6c8e6-163">Uwierzytelnianie serwera proxy nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="6c8e6-164">Nasze zalecenie, bieżący jest hello tooallow łącznika toohello anonimowy dostęp do Internetu miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="6c8e6-165">Porty serwera proxy</span><span class="sxs-lookup"><span data-stu-id="6c8e6-165">Proxy ports</span></span>

<span data-ttu-id="6c8e6-166">Łącznik Hello sprawia, że oparte na protokole SSL połączeń wychodzących przy użyciu metody CONNECT hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="6c8e6-167">Ta metoda konfiguruje zasadniczo tunel powitania serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="6c8e6-168">Skonfiguruj tooallow serwera proxy hello tunelowania tooports 443 i 80.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="6c8e6-169">Po uruchomieniu usługi Service Bus przy użyciu protokołu HTTPS używa portu 443.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="6c8e6-170">Domyślnie usługi Service Bus podejmuje próbę bezpośredniego połączenia TCP i powraca tooHTTPS tylko wtedy, gdy bezpośrednie połączenie między zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="6c8e6-171">tooensure hello ruch jest również przesyłany za pośrednictwem serwera proxy ruchu wychodzącego hello usługi Service Bus, upewnij się, że ten łącznik hello nie może połączyć się bezpośrednio z toohello usług Azure porty 9350, 9352 i 5671.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="6c8e6-172">Inspekcja protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="6c8e6-172">SSL inspection</span></span>
<span data-ttu-id="6c8e6-173">Nie należy używać SSL kontroli w przypadku ruchu łącznika hello, ponieważ powoduje problemy w przypadku ruchu łącznika hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="6c8e6-174">Rozwiązywanie problemów z łącznika serwera proxy problemów i problemy z połączeniem usługi</span><span class="sxs-lookup"><span data-stu-id="6c8e6-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="6c8e6-175">Teraz powinien być widoczny cały ruch przepływających przez powitania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="6c8e6-176">Jeśli masz problemy powinny pomóc w hello następujące informacje dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="6c8e6-177">Witaj najlepsze sposób tooidentify i rozwiązywania problemów z łącznością łącznika tootake sieci przechwytywania usługi łącznika hello podczas uruchamiania usługi łącznika hello jest problemy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="6c8e6-178">To stanowić nie lada wyzwanie, więc Przyjrzyjmy się szybkie porady dotyczące przechwytywania i filtrowania śladów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="6c8e6-179">Możesz użyć hello monitorowania dowolnego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="6c8e6-180">Dla celów hello w tym artykule użyliśmy Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="6c8e6-181">Możesz [Pobierz go z Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="6c8e6-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="6c8e6-182">filtry, których używamy w hello następujące sekcje zawierają informacje i przykłady Hello są określone tooNetwork Monitor, ale hello zasady mogą być zastosowane tooany narzędzie do analizy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="6c8e6-183">Przechwytywanie za pomocą Monitora sieci</span><span class="sxs-lookup"><span data-stu-id="6c8e6-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="6c8e6-184">toostart przechwytywania:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-184">toostart a capture:</span></span>

1. <span data-ttu-id="6c8e6-185">Otwórz program Network Monitor i kliknij przycisk **nowe przechwycenia**.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="6c8e6-186">Kliknij przycisk hello **Start** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-186">Click hello **Start** button.</span></span>

   ![Okno Monitora sieci](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="6c8e6-188">Po ukończeniu przechwytywania, kliknij przycisk hello **zatrzymać** tooend przycisk go.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="6c8e6-189">Przechwytywanie ruchu łącznika</span><span class="sxs-lookup"><span data-stu-id="6c8e6-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="6c8e6-190">Do rozwiązywania problemów początkowej, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="6c8e6-191">Z services.msc należy zatrzymać usługę łącznika serwera Proxy aplikacji w usłudze Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="6c8e6-192">Uruchom hello przechwytywania ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-192">Start hello network capture.</span></span>
3. <span data-ttu-id="6c8e6-193">Uruchom usługę łącznika serwera Proxy aplikacji w usłudze Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="6c8e6-194">Zatrzymaj hello przechwytywania ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-194">Stop hello network capture.</span></span>

   ![Usługa Azure łącznika serwera Proxy aplikacji usługi AD w celu aplikację services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="6c8e6-196">Obejrzyj hello żądań z serwera proxy toohello łącznika hello</span><span class="sxs-lookup"><span data-stu-id="6c8e6-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="6c8e6-197">Skoro masz przechwytywania ruchu sieciowego, wszystko jest gotowe toofilter go.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="6c8e6-198">toolooking klucza Hello na powitania śledzenia jest zrozumienie, jak toofilter hello przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="6c8e6-199">Jeden filtr następująco (gdzie 8080 jest port usługi serwera proxy hello):</span><span class="sxs-lookup"><span data-stu-id="6c8e6-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="6c8e6-200">**(protokół http. Żądanie lub http. Odpowiedź) i tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="6c8e6-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="6c8e6-201">Po wprowadzeniu tego filtru w hello **filtru wyświetlania** i zaznacz **Zastosuj**, filtruje ruchu hello przechwycone oparte na powitania filtru.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="6c8e6-202">Witaj poprzedniego filtru zawiera tylko hello żądań i odpowiedzi HTTP z hello port serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="6c8e6-203">Do uruchomienia łącznika, gdy łącznik hello jest toouse skonfigurowany serwer proxy filtr hello czy Pokaż podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Przykład listy filtrowane żądań i odpowiedzi HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="6c8e6-205">Teraz w szczególności szukasz hello CONNECT żądań, które Pokaż komunikacji z serwerem proxy hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="6c8e6-206">Na sukces otrzymasz odpowiedź HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="6c8e6-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="6c8e6-207">Jeśli widzisz innych kodów odpowiedzi, na przykład 407 lub 502 powitania serwera proxy jest wymaganie uwierzytelniania lub nie zezwala na ruch hello innego powodu.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="6c8e6-208">W tym momencie Uwzględnij się z zespołem pomocy technicznej serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="6c8e6-209">Zidentyfikuj nieudanych prób połączenia TCP</span><span class="sxs-lookup"><span data-stu-id="6c8e6-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="6c8e6-210">Hello innych typowy scenariusz, który może Cię zainteresować jest hello łącznika próbuje tooconnect bezpośrednio, ale występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="6c8e6-211">Inny filtr Monitor sieci, która pomaga tooeasily zidentyfikować ten problem jest:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="6c8e6-212">**Właściwość. TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="6c8e6-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="6c8e6-213">Pakiet SYN jest pierwszy pakiet hello wysłanych tooestablish połączenie TCP.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="6c8e6-214">Jeśli ten pakiet nie zwraca odpowiedź, hello SYN jest podjęta ponownie.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="6c8e6-215">Można użyć dowolnego syn ponownie przesłane hello poprzedzających toosee filtru.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="6c8e6-216">Następnie można sprawdzić, czy te syn odpowiada tooany ruch związany z usługą łącznika.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="6c8e6-217">Witaj poniższy przykład przedstawia próba połączenia nie powiodło się tooService magistrali port 9352:</span><span class="sxs-lookup"><span data-stu-id="6c8e6-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Przykład odpowiedzi próby połączenia nie powiodło się](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="6c8e6-219">Jeśli zostanie wyświetlony ekran podobny do hello poprzedzających odpowiedzi łącznika hello próbuje toocommunicate bezpośrednio z hello usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="6c8e6-220">Jeśli oczekujesz hello łącznika toomake bezpośrednich połączeń toohello Azure usługi, to odpowiedź jest jednoznacznie zidentyfikować, że masz problem sieci i zapory.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="6c8e6-221">Jeśli jesteś toouse skonfigurowany serwer proxy tej odpowiedzi może oznaczać, że usługi Service Bus próbuje bezpośrednie połączenie TCP przed przełączeniem tooattempting połączenie za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="6c8e6-222">Analiza śledzenia sieci nie jest dostępne dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="6c8e6-223">Jednak jest przydatnym narzędziem tooget szybkie informacje o to, co dzieje się z sieci.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="6c8e6-224">Jeśli będziesz kontynuować toostruggle z problemów z łącznością łącznika, Utwórz bilet z naszym zespołem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="6c8e6-225">zespół Hello mogą pomóc o dodatkowe informacje o rozwiązywaniu.</span><span class="sxs-lookup"><span data-stu-id="6c8e6-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="6c8e6-226">Aby uzyskać informacje o rozwiązywaniu problemów z łącznika serwera Proxy aplikacji, zobacz [Rozwiązywanie problemów z serwera Proxy aplikacji](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="6c8e6-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c8e6-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c8e6-227">Next steps</span></span>

[<span data-ttu-id="6c8e6-228">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c8e6-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="6c8e6-229">
[Jak toosilently zainstalować hello łącznika serwera Proxy aplikacji w usłudze Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="6c8e6-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
