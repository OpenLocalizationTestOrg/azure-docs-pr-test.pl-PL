---
title: "Praca z istniejącym lokalnych serwerów proxy i Azure AD | Dokumentacja firmy Microsoft"
description: "Uwzględniono również sposób pracy z istniejących serwerów proxy lokalnymi."
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="88f78-103">Praca z istniejącym lokalnych serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="88f78-104">W tym artykule opisano sposób konfigurowania serwera Proxy aplikacji usługi Azure Active Directory (Azure AD) łączniki do pracy z serwerami serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88f78-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="88f78-105">Przewodnik jest przeznaczony dla klientów z sieci środowiskach z istniejących serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="88f78-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="88f78-106">Rozpoczniemy analizując te scenariusze wdrażania głównego:</span><span class="sxs-lookup"><span data-stu-id="88f78-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="88f78-107">Skonfiguruj konektory w celu obejścia proxy ruchu wychodzącego sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="88f78-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="88f78-108">Skonfiguruj konektory w celu użycia serwera proxy ruchu wychodzącego do serwera Proxy aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88f78-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="88f78-109">Aby uzyskać więcej informacji na temat działania łączników, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="88f78-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="88f78-110">Konfigurowanie serwera proxy ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="88f78-110">Configure the outbound proxy</span></span>

<span data-ttu-id="88f78-111">Jeśli w środowisku serwera proxy ruchu wychodzącego, użyj konta z odpowiednimi uprawnieniami do konfigurowania serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88f78-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="88f78-112">Ponieważ Instalator jest uruchamiany w kontekście użytkownika, który jest podczas instalacji, konfiguracji można sprawdzić za pomocą Microsoft Edge lub innej przeglądarki internetowej.</span><span class="sxs-lookup"><span data-stu-id="88f78-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="88f78-113">Aby skonfigurować ustawienia serwera proxy w programie Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="88f78-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="88f78-114">Przejdź do **ustawienia** > **widoku Zaawansowane ustawienia** > **Otwórz ustawienia serwera Proxy** > **instalacji ręcznej serwera Proxy**.</span><span class="sxs-lookup"><span data-stu-id="88f78-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="88f78-115">Ustaw **Użyj serwera proxy** do **na**, wybierz pozycję **nie używaj serwera proxy dla adresów lokalnych (sieć intranet)** pole wyboru, a następnie zmień adres i port, aby odzwierciedlić serwera proxy w lokalnych.</span><span class="sxs-lookup"><span data-stu-id="88f78-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="88f78-116">Wypełnij ustawienia serwera proxy niezbędne.</span><span class="sxs-lookup"><span data-stu-id="88f78-116">Fill in the necessary proxy settings.</span></span>

   ![Okno dialogowe ustawień serwera proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="88f78-118">Obejście proxy ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="88f78-118">Bypass outbound proxies</span></span>

<span data-ttu-id="88f78-119">Łączniki mają podstawowych składników systemu operacyjnego, które żądania wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88f78-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="88f78-120">Te składniki automatycznie podejmować próby zlokalizowania serwera proxy w sieci.</span><span class="sxs-lookup"><span data-stu-id="88f78-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="88f78-121">Korzystają autowykrywania serwera Proxy sieci Web (WPAD), jeśli jest włączona w środowisku.</span><span class="sxs-lookup"><span data-stu-id="88f78-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="88f78-122">Składniki systemu operacyjnego podejmować próby zlokalizowania serwera proxy przeprowadzając wyszukiwania DNS dla wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="88f78-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="88f78-123">Jeśli to rozwiązuje w systemie DNS do adresu IP dla wpad.dat następnie jest przeprowadzane żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="88f78-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="88f78-124">To żądanie staje się skrypt konfiguracji serwera proxy w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="88f78-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="88f78-125">Łącznik korzysta ten skrypt, aby wybrać serwer proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88f78-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="88f78-126">Jednak ruch łącznika może nadal nie powiodło się, ze względu na dodatkowe ustawienia konfiguracji potrzebne na serwerze proxy.</span><span class="sxs-lookup"><span data-stu-id="88f78-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="88f78-127">Można skonfigurować łącznik, aby pominąć lokalnego serwera proxy do zapewnienia korzysta z bezpośredniego łączności usług Azure.</span><span class="sxs-lookup"><span data-stu-id="88f78-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="88f78-128">Zalecamy takie podejście (Jeśli zasady sieci umożliwia on), ponieważ oznacza, że masz mniej jedną konfigurację do obsługi.</span><span class="sxs-lookup"><span data-stu-id="88f78-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="88f78-129">Aby wyłączyć użycia serwera proxy ruchu wychodzącego dla łącznika, przeprowadź edycję pliku C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config i Dodaj *system.net* sekcji pokazano w tym przykładowym kodzie:</span><span class="sxs-lookup"><span data-stu-id="88f78-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="88f78-130">Aby upewnić się, że aktualizator łącznika usługi również pomija serwera proxy, należy wprowadzić zmianę podobne do pliku ApplicationProxyConnectorUpdaterService.exe.config znajdującym się w aktualizator łącznika serwera Proxy aplikacji usługi AAD C:\Program Files\Microsoft.</span><span class="sxs-lookup"><span data-stu-id="88f78-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="88f78-131">Należy pamiętać o wykonaniu kopii oryginalnych plików, w razie potrzeby można przywrócić w plikach .config domyślne.</span><span class="sxs-lookup"><span data-stu-id="88f78-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="88f78-132">Użyj serwera proxy ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="88f78-132">Use the outbound proxy server</span></span>

<span data-ttu-id="88f78-133">Niektóre środowiska wymagają cały ruch wychodzący do go za pośrednictwem serwera proxy ruchu wychodzącego, bez wyjątku.</span><span class="sxs-lookup"><span data-stu-id="88f78-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="88f78-134">W związku z tym pomijanie serwera proxy nie jest opcją.</span><span class="sxs-lookup"><span data-stu-id="88f78-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="88f78-135">Możesz skonfigurować ruchu łącznika do go za pośrednictwem serwera proxy ruchu wychodzącego, jak pokazano na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="88f78-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Konfigurowanie łącznika ruchu można przejść za pośrednictwem serwera proxy ruchu wychodzącego do serwera Proxy aplikacji usługi Azure AD](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="88f78-137">W wyniku o tylko ruchu wychodzącego, nie istnieje potrzeba aby skonfigurować dostęp przychodzących na zaporach.</span><span class="sxs-lookup"><span data-stu-id="88f78-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="88f78-138">Krok 1: Konfigurowanie łącznika i powiązane usługi, aby przejść za pośrednictwem serwera proxy ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="88f78-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="88f78-139">Objętych wcześniej, jeśli WPAD jest włączona w środowisku i prawidłowo skonfigurowany, łącznik automatycznie odnajdzie serwera proxy ruchu wychodzącego i spróbować go użyć.</span><span class="sxs-lookup"><span data-stu-id="88f78-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="88f78-140">Można jednak jawnie skonfigurować łącznik, aby go za pośrednictwem serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88f78-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="88f78-141">Aby to zrobić, Edytuj plik C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy Connector\ApplicationProxyConnectorService.exe.config i Dodaj *system.net* sekcji pokazano w tym przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="88f78-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="88f78-142">Zmień *proxyserver:8080* w celu uwzględnienia nazwę lokalnego serwera proxy serwera lub adres IP i portu nasłuchiwania na.</span><span class="sxs-lookup"><span data-stu-id="88f78-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="88f78-143">Skonfiguruj usługę aktualizator łącznika, aby serwer proxy jest używany przez wprowadzenie zmiany podobną do następującej lokalizacji C:\Program Files\Microsoft usługi AAD aplikacji serwera Proxy łącznika Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="88f78-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="88f78-144">Krok 2: Konfigurowanie serwera proxy zezwalająca na ruch z łącznika i powiązane usługi przepływają przez</span><span class="sxs-lookup"><span data-stu-id="88f78-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="88f78-145">Istnieją cztery aspektów, które należy wziąć pod uwagę w przypadku serwera proxy ruchu wychodzącego:</span><span class="sxs-lookup"><span data-stu-id="88f78-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="88f78-146">Reguły ruchu wychodzącego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-146">Proxy outbound rules</span></span>
* <span data-ttu-id="88f78-147">Uwierzytelnianie serwera proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-147">Proxy authentication</span></span>
* <span data-ttu-id="88f78-148">Porty serwera proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-148">Proxy ports</span></span>
* <span data-ttu-id="88f78-149">Inspekcja protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="88f78-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="88f78-150">Reguły ruchu wychodzącego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-150">Proxy outbound rules</span></span>
<span data-ttu-id="88f78-151">Zezwalaj na dostęp do następujących punktów końcowych do łącznika usługi:</span><span class="sxs-lookup"><span data-stu-id="88f78-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="88f78-152">*. msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="88f78-152">*.msappproxy.net</span></span>
* <span data-ttu-id="88f78-153">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="88f78-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="88f78-154">Początkowe rejestracyjny można zezwolić na dostęp do następujących punktów końcowych:</span><span class="sxs-lookup"><span data-stu-id="88f78-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="88f78-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="88f78-155">login.windows.net</span></span>
* <span data-ttu-id="88f78-156">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="88f78-156">login.microsoftonline.com</span></span>

<span data-ttu-id="88f78-157">Jeśli nie umożliwiają nawiązywanie połączeń przez nazwę FQDN, a zamiast tego określ zakresy adresów IP, korzystać z tych opcji:</span><span class="sxs-lookup"><span data-stu-id="88f78-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="88f78-158">Zezwalaj na dostęp ruchu wychodzącego łącznika do wszystkich miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="88f78-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="88f78-159">Zezwalaj na dostęp ruchu wychodzącego łącznika do [zakresy IP centrum danych Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="88f78-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="88f78-160">Wyzwanie z listy zakresów IP centrum danych Azure jest, że jest aktualizowana co tydzień.</span><span class="sxs-lookup"><span data-stu-id="88f78-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="88f78-161">Należy umieścić procesu w celu zapewnienia odpowiednio aktualizowany reguł dostępu.</span><span class="sxs-lookup"><span data-stu-id="88f78-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="88f78-162">Uwierzytelnianie serwera proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-162">Proxy authentication</span></span>

<span data-ttu-id="88f78-163">Uwierzytelnianie serwera proxy nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="88f78-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="88f78-164">Nasze zalecenie, bieżący jest zezwala na dostęp anonimowy łącznika do Internetu miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="88f78-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="88f78-165">Porty serwera proxy</span><span class="sxs-lookup"><span data-stu-id="88f78-165">Proxy ports</span></span>

<span data-ttu-id="88f78-166">Łącznik sprawia, że oparte na protokole SSL połączeń wychodzących przy użyciu metody CONNECT.</span><span class="sxs-lookup"><span data-stu-id="88f78-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="88f78-167">Ta metoda powoduje ustawienie zasadniczo tunelu za pośrednictwem serwera proxy ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88f78-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="88f78-168">Konfiguracja serwera proxy, aby umożliwić tunelowania na porty 443 i 80.</span><span class="sxs-lookup"><span data-stu-id="88f78-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="88f78-169">Po uruchomieniu usługi Service Bus przy użyciu protokołu HTTPS używa portu 443.</span><span class="sxs-lookup"><span data-stu-id="88f78-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="88f78-170">Domyślnie usługi Service Bus podejmuje próbę bezpośredniego połączenia TCP i powraca do HTTPS tylko wtedy, gdy bezpośrednie połączenie między zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="88f78-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="88f78-171">Aby upewnić się, że ruch usługi Service Bus jest również przesyłany za pośrednictwem serwera proxy ruchu wychodzącego, upewnij się, że łącznik nie może nawiązać bezpośrednie usług platformy Azure dla porty 9350, 9352 i 5671.</span><span class="sxs-lookup"><span data-stu-id="88f78-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="88f78-172">Inspekcja protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="88f78-172">SSL inspection</span></span>
<span data-ttu-id="88f78-173">Nie należy używać protokołu SSL inspekcji dla ruchu łącznika, ponieważ powoduje problemy w przypadku ruchu łącznika.</span><span class="sxs-lookup"><span data-stu-id="88f78-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="88f78-174">Rozwiązywanie problemów z łącznika serwera proxy problemów i problemy z połączeniem usługi</span><span class="sxs-lookup"><span data-stu-id="88f78-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="88f78-175">Teraz powinien być widoczny cały ruch przepływających przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="88f78-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="88f78-176">Jeśli masz problemy powinny pomóc następujące informacje dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="88f78-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="88f78-177">Najlepszym sposobem na identyfikowanie i rozwiązywanie problemów z łącznością łącznika jest przechwytywanie sieci na usługę łącznika podczas uruchamiania usługi łącznika.</span><span class="sxs-lookup"><span data-stu-id="88f78-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="88f78-178">To stanowić nie lada wyzwanie, więc Przyjrzyjmy się szybkie porady dotyczące przechwytywania i filtrowania śladów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="88f78-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="88f78-179">Można użyć narzędzia monitorowania wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88f78-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="88f78-180">Do celów tego artykułu użyliśmy Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="88f78-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="88f78-181">Możesz [Pobierz go z Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="88f78-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="88f78-182">Przykłady i filtry, których używamy w poniższych sekcjach są specyficzne dla monitora sieci, ale zasady mogą być stosowane do dowolnego narzędzia do analizy.</span><span class="sxs-lookup"><span data-stu-id="88f78-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="88f78-183">Przechwytywanie za pomocą Monitora sieci</span><span class="sxs-lookup"><span data-stu-id="88f78-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="88f78-184">Aby uruchomić przechwytywania:</span><span class="sxs-lookup"><span data-stu-id="88f78-184">To start a capture:</span></span>

1. <span data-ttu-id="88f78-185">Otwórz program Network Monitor i kliknij przycisk **nowe przechwycenia**.</span><span class="sxs-lookup"><span data-stu-id="88f78-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="88f78-186">Kliknij przycisk **Start** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88f78-186">Click the **Start** button.</span></span>

   ![Okno Monitora sieci](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="88f78-188">Po ukończeniu przechwytywania, kliknij przycisk **zatrzymać** przycisk, aby ją zakończyć.</span><span class="sxs-lookup"><span data-stu-id="88f78-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="88f78-189">Przechwytywanie ruchu łącznika</span><span class="sxs-lookup"><span data-stu-id="88f78-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="88f78-190">Do rozwiązywania problemów początkowej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="88f78-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="88f78-191">Z services.msc należy zatrzymać usługę łącznika serwera Proxy aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88f78-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="88f78-192">Uruchom przechwytywania ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="88f78-192">Start the network capture.</span></span>
3. <span data-ttu-id="88f78-193">Uruchom usługę łącznika serwera Proxy aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88f78-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="88f78-194">Zatrzymaj przechwytywania ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="88f78-194">Stop the network capture.</span></span>

   ![Usługa Azure łącznika serwera Proxy aplikacji usługi AD w celu aplikację services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="88f78-196">Przyjrzyj się z serwerem proxy żądania z łącznika</span><span class="sxs-lookup"><span data-stu-id="88f78-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="88f78-197">Skoro masz przechwytywania ruchu sieciowego, możesz go filtrować.</span><span class="sxs-lookup"><span data-stu-id="88f78-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="88f78-198">Klucz do analizowania śledzenia jest zrozumienie sposobu filtru przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="88f78-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="88f78-199">Jeden filtr następująco (gdzie 8080 jest port usługi serwera proxy):</span><span class="sxs-lookup"><span data-stu-id="88f78-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="88f78-200">**(protokół http. Żądanie lub http. Odpowiedź) i tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="88f78-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="88f78-201">Po wprowadzeniu tego filtru w **filtru wyświetlania** i zaznacz **Zastosuj**, filtruje przechwycony ruch na podstawie filtru.</span><span class="sxs-lookup"><span data-stu-id="88f78-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="88f78-202">Poprzednie filtru zawiera po prostu żądań i odpowiedzi HTTP z port serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="88f78-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="88f78-203">Do uruchomienia łącznika, gdy łącznik jest skonfigurowany do używania serwera proxy filtr będzie Pokaż mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="88f78-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Przykład listy filtrowane żądań i odpowiedzi HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="88f78-205">Teraz w szczególności szukasz żądania połączenia, które Pokaż komunikacji z serwerem proxy.</span><span class="sxs-lookup"><span data-stu-id="88f78-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="88f78-206">Na sukces otrzymasz odpowiedź HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="88f78-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="88f78-207">Jeśli widzisz innych kodów odpowiedzi, na przykład 407 lub 502, serwer proxy jest wymaganie uwierzytelniania lub nie zezwala na ruch innego powodu.</span><span class="sxs-lookup"><span data-stu-id="88f78-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="88f78-208">W tym momencie Uwzględnij się z zespołem pomocy technicznej serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="88f78-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="88f78-209">Zidentyfikuj nieudanych prób połączenia TCP</span><span class="sxs-lookup"><span data-stu-id="88f78-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="88f78-210">Typowy scenariusz, który może Cię zainteresować jest łącznik próbuje nawiązać połączenie bezpośrednio, ale występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="88f78-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="88f78-211">Inny filtr Monitor sieci, która pomaga łatwo zidentyfikować ten problem jest:</span><span class="sxs-lookup"><span data-stu-id="88f78-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="88f78-212">**Właściwość. TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="88f78-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="88f78-213">Pakiet SYN jest pierwszy pakiet wysyłany do nawiązywania połączeń TCP.</span><span class="sxs-lookup"><span data-stu-id="88f78-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="88f78-214">Jeśli ten pakiet nie zwraca odpowiedź, SYN jest podjęta ponownie.</span><span class="sxs-lookup"><span data-stu-id="88f78-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="88f78-215">Można użyć poprzedniego filtru, aby wyświetlić wszystkie syn ponownie przesłane.</span><span class="sxs-lookup"><span data-stu-id="88f78-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="88f78-216">Następnie można sprawdzić, czy te syn odpowiadają żadnych ruch związany z usługą łącznika.</span><span class="sxs-lookup"><span data-stu-id="88f78-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="88f78-217">W poniższym przykładzie przedstawiono portu usługi Service Bus 9352 próba połączenia nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="88f78-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Przykład odpowiedzi próby połączenia nie powiodło się](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="88f78-219">Jeśli zostanie wyświetlony ekran podobny do poprzedniej odpowiedzi łącznika próbuje komunikują się bezpośrednio z usługi Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="88f78-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="88f78-220">Jeśli łącznik, aby nawiązywać połączenia bezpośrednio z usług Azure, ta odpowiedź jest jednoznacznie zidentyfikować, że masz problem sieci i zapory.</span><span class="sxs-lookup"><span data-stu-id="88f78-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="88f78-221">Jeśli są skonfigurowane do korzystania z serwera proxy, tej odpowiedzi może oznaczać, że usługi Service Bus próbuje bezpośrednie połączenie TCP przed przełączeniem do próba połączenia za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="88f78-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="88f78-222">Analiza śledzenia sieci nie jest dostępne dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="88f78-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="88f78-223">Jednak jest przydatnym narzędziem, aby uzyskać szybki dowiedzieć się, co dzieje się z sieci.</span><span class="sxs-lookup"><span data-stu-id="88f78-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="88f78-224">Jeśli nadal mieć trudności z problemów z łącznością łącznika, Utwórz bilet z naszym zespołem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="88f78-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="88f78-225">Zespół może pomóc dalszego rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="88f78-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="88f78-226">Aby uzyskać informacje o rozwiązywaniu problemów z łącznika serwera Proxy aplikacji, zobacz [Rozwiązywanie problemów z serwera Proxy aplikacji](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="88f78-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88f78-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88f78-227">Next steps</span></span>

[<span data-ttu-id="88f78-228">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88f78-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="88f78-229">
[Jak zainstalować łącznik serwera Proxy aplikacji Azure AD w trybie dyskretnym](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="88f78-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
