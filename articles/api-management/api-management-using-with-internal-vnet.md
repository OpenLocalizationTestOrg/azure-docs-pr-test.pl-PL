---
title: "Jak używać usługi Azure API Management z wewnętrznej sieci wirtualnej | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie instalacji i konfiguracji usługi Azure API Management w wewnętrznej sieci wirtualnej."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Przy użyciu usługi Azure API Management z wewnętrznej sieci wirtualnej
Sieci wirtualne Azure (sieci wirtualne) zarządzanie interfejsami API umożliwiają zarządzanie interfejsów API nie jest dostępny w Internecie. Liczba technologii sieci VPN są dostępne do nawiązania połączenia i zarządzanie interfejsami API może zostać wdrożony w dwóch trybach głównego w sieci Wirtualnej:
* Zewnętrzne
* wewnętrzny

## <a name="overview"> </a>Omówienie
Zarządzanie interfejsami API jest wdrażana w trybie sieci wewnętrznej wirtualnym, wszystkie punkty końcowe usługi (bramy, portalu dla deweloperów, portal wydawcy, bezpośrednie zarządzanie i Git) są widoczne w sieci wirtualnej, którą kontrolujesz tylko dostęp do. Żaden z punktów końcowych usługi nie jest zarejestrowany na publicznym serwerze DNS.

Za pomocą interfejsu API zarządzania w trybie wewnętrzny można osiągnąć następujące scenariusze
* Bezpiecznie należy interfejsów API hostowanych w prywatnej dostępny centrum danych przez 3 strony poza za pomocą połączeń lokacja-lokacja lub sieci VPN usługi ExpressRoute.
* Włącz scenariuszach chmur hybrydowych dzięki uwidocznieniu działania sieci opartej na chmurze interfejsów API i interfejsów API lokalnego za pośrednictwem wspólnego bramy.
* Zarządzanie swoje interfejsy API hostowany w wielu lokalizacjach geograficznych przy użyciu jeden punkt końcowy bramy. 

## <a name="enable-vpn"></a>Tworzenie zarządzanie interfejsami API w sieci wewnętrznej wirtualnej
Usługa API Management w sieci wewnętrznej wirtualnej jest hostowany za wewnętrzny Balancer(ILB) obciążenia. Adres IP ILB znajduje się w [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) zakresu.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Włącz połączenie sieci Wirtualnej przy użyciu portalu Azure
Najpierw utworzyć usługi Zarządzanie interfejsami API, wykonując kroki [utworzyć zarządzanie interfejsami API usługi][Create API Management service]. Następnie Konfiguracja interfejsu API zarządzania do wdrożenia w ramach sieci wirtualnej.

![Menu konfigurowania APIM w wewnętrznej sieci wirtualnej][api-management-using-internal-vnet-menu]

Po wdrożeniu zakończy się powodzeniem, wewnętrznego wirtualnego adresu IP usługi powinny być widoczne na pulpicie nawigacyjnym.

![Pulpit nawigacyjny zarządzania interfejsu API z wewnętrznej sieci Wirtualnej skonfigurowane][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Włącz połączenie sieci Wirtualnej przy użyciu poleceń cmdlet programu Powershell
Można również włączyć łączność sieci Wirtualnej przy użyciu poleceń cmdlet programu PowerShell.

* **Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet [AzureRmApiManagement nowy](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) utworzenia usługi Azure API Management w sieci Wirtualnej i skonfigurować go do używania typu wewnętrznej sieci Wirtualnej.

* **Wdrażanie istniejącej usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet [AzureRmApiManagementDeployment aktualizacji](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) Aby przenieść istniejącą usługę Azure API Management w sieci wirtualnej i skonfigurować go do używania Wewnętrzny typ sieci Wirtualnej.

## <a name="apim-dns-configuration"></a>Konfiguracja DNS
Korzystając z interfejsu API zarządzania w trybie sieci zewnętrznych wirtualnym, DNS jest zarządzana przez platformę Azure. Dla trybu sieciowego wewnętrznego wirtualnego trzeba zarządzać własną DNS.

> [!NOTE]
> Zarządzanie interfejsami API usługi nie nasłuchiwać żądań przesyłanych na adresy IP. Tylko odpowiada na żądania nazwa hosta skonfigurowana na jego punktów końcowych usługi (w tym bramy, portalu dla deweloperów wydawcy portalu, bezpośrednie zarządzanie punktu końcowego i git).

### <a name="access-on-default-host-names"></a>Dostęp do nazw hosta domyślnego:
Podczas tworzenia usługi Zarządzanie interfejsami API w chmurze publicznej Azure, na przykład o nazwie "contoso", następujące punkty końcowe usługi są domyślnie skonfigurowane.

>   Bramy / serwera Proxy - contoso.azure api.net

> Portal wydawcy i portalu dla deweloperów - contoso.portal.azure api.net

> Punkt końcowy zarządzania bezpośredniego - contoso.management.azure api.net

>   GIT - contoso.scm.azure api.net

Aby uzyskać dostęp do tych punktów końcowych usługi API Management, należy utworzyć maszynę wirtualną w podsieci podłączone do sieci wirtualnej, w której jest wdrażane zarządzanie interfejsami API. Zakładając, że wewnętrznego wirtualnego adresu IP dla usługi jest 10.0.0.5, możesz zrobić hosty pliku mapowania (% SystemDrive%\drivers\etc\hosts) w następujący sposób:

> 10.0.0.5 contoso.azure-api.net

> 10.0.0.5 contoso.portal.azure-api.net

> 10.0.0.5 contoso.management.azure-api.net

> 10.0.0.5 contoso.scm.azure-api.net

Wszystkie punkty końcowe usługi można następnie uzyskać dostęp z maszyny wirtualnej został utworzony. Jeśli używany jest serwer niestandardowe DNS w sieci wirtualnej, można również utworzyć rekordy A DNS i uzyskiwać dostęp do tych punktów końcowych z dowolnego miejsca w sieci wirtualnej. 

### <a name="access-on-custom-domain-names"></a>Dostęp do niestandardowych nazw domen:
Jeśli nie chcesz uzyskać dostęp do usługi API Management z domyślnej nazwy hostów, należy skonfigurować niestandardowe nazwy domen dla wszystkich usług punktów końcowych podobnie jak poniżej

![Skonfigurowanie domeny niestandardowej dla interfejsu API zarządzania][api-management-custom-domain-name]

Następnie można utworzyć rekordów znajdujących się na serwerze DNS, aby dostęp do tych punktów końcowych, które są dostępne jedynie z sieci wirtualnej.

## <a name="related-content"></a>Związane z zawartością
* [Typowe problemy z konfiguracją sieci podczas konfigurowania APIM w sieci Wirtualnej][Common Network Configuration Issues]
* [Często zadawane pytania dotyczące sieci wirtualnej](../virtual-network/virtual-networks-faq.md)
* [Tworzenie rekord w systemie DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
