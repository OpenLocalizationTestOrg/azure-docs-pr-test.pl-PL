---
title: "aaaHow toouse Azure API Management z wewnętrznej sieci wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i konfigurowanie usługi Azure API Management w wewnętrznej sieci wirtualnej."
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
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Przy użyciu usługi Azure API Management z wewnętrznej sieci wirtualnej
Sieci wirtualne Azure (sieci wirtualne) zarządzanie interfejsami API umożliwiają zarządzanie interfejsów API nie jest dostępna na powitania Internet. Połączenia hello toomake dostępne są różne technologie sieci VPN i zarządzanie interfejsami API może zostać wdrożony w dwóch trybach głównego wewnątrz hello sieci Wirtualnej:
* Zewnętrzne
* wewnętrzny

## <a name="overview"> </a>Omówienie
Po wdrożeniu usługi API Management w trybie sieci wewnętrznej wirtualnym wszystkich hello punktów końcowych usługi (bramy, portalu dla deweloperów, portal wydawcy, bezpośrednie zarządzanie i Git) są widoczne tylko w sieci wirtualnej, która umożliwia kontrolę dostępu do. Żaden z punktów końcowych usługi hello nie jest zarejestrowany na powitania publiczny serwer DNS.

Za pomocą interfejsu API zarządzania w trybie wewnętrzny można osiągnąć następujące scenariusze hello
* Bezpiecznie należy interfejsów API hostowanych w prywatnej dostępny centrum danych przez 3 strony poza za pomocą połączeń lokacja-lokacja lub sieci VPN usługi ExpressRoute.
* Włącz scenariuszach chmur hybrydowych dzięki uwidocznieniu działania sieci opartej na chmurze interfejsów API i interfejsów API lokalnego za pośrednictwem wspólnego bramy.
* Zarządzanie swoje interfejsy API hostowany w wielu lokalizacjach geograficznych przy użyciu jeden punkt końcowy bramy. 

## <a name="enable-vpn"></a>Tworzenie zarządzanie interfejsami API w sieci wewnętrznej wirtualnej
Witaj usługi Zarządzanie interfejsami API w sieci wewnętrznej wirtualnej jest hostowany za wewnętrzny Balancer(ILB) obciążenia. Adres IP hello ILB Hello jest hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) zakresu.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Włącz połączenie sieci Wirtualnej przy użyciu portalu Azure
Najpierw utworzyć usługi Zarządzanie interfejsami API hello, wykonując kroki hello [utworzyć zarządzanie interfejsami API usługi][Create API Management service]. Następnie Konfiguracja interfejsu API zarządzania toobe wdrożone w ramach sieci wirtualnej.

![Menu konfigurowania APIM w wewnętrznej sieci wirtualnej][api-management-using-internal-vnet-menu]

Po pomyślnym zainicjowaniu wdrażania hello, hello wewnętrznego wirtualnego adresu IP usługi powinny być widoczne na pulpicie nawigacyjnym hello.

![Pulpit nawigacyjny zarządzania interfejsu API z wewnętrznej sieci Wirtualnej skonfigurowane][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Włącz połączenie sieci Wirtualnej przy użyciu poleceń cmdlet programu Powershell
Można również włączyć łączność sieci Wirtualnej przy użyciu poleceń cmdlet programu PowerShell hello.

* **Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet hello [AzureRmApiManagement nowy](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate Azure API Management w sieci Wirtualnej i skonfiguruj go toouse hello wewnętrzna sieć wirtualna typu.

* **Wdrażanie istniejącej usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet hello [AzureRmApiManagementDeployment aktualizacji](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove istniejącej usługi Azure API Management w sieci wirtualnej i skonfiguruj go toouse Wewnętrzny typ sieci Wirtualnej.

## <a name="apim-dns-configuration"></a>Konfiguracja DNS
Korzystając z interfejsu API zarządzania w trybie sieci zewnętrznych wirtualnym, DNS jest zarządzana przez platformę Azure. Tryb sieci wewnętrznej wirtualny należy toomanage własne DNS.

> [!NOTE]
> Zarządzanie interfejsami API usługi nie będzie nasłuchiwać toorequests pochodzących z adresami IP. Tylko odpowiadały toohello toorequests nazwa hosta skonfigurowana na jego punktów końcowych usługi (w tym bramy, portalu dla deweloperów wydawcy portalu, bezpośrednie zarządzanie punktu końcowego i git).

### <a name="access-on-default-host-names"></a>Dostęp do nazw hosta domyślnego:
Podczas tworzenia usługi Zarządzanie interfejsami API w chmurze publicznej Azure, na przykład o nazwie "contoso", hello następujące punkty końcowe usługi są domyślnie skonfigurowane.

>   Bramy / serwera Proxy - contoso.azure api.net

> Portal wydawcy i portalu dla deweloperów - contoso.portal.azure api.net

> Punkt końcowy zarządzania bezpośredniego - contoso.management.azure api.net

>   GIT - contoso.scm.azure api.net

tooaccess tych punktów końcowych usługi Zarządzanie interfejsami API można utworzyć maszyny wirtualnej w sieci wirtualnej toohello podłączone podsieci, w której jest wdrażane zarządzanie interfejsami API. Zakładając, że hello wewnętrznego wirtualnego adresu IP dla usługi jest 10.0.0.5, możesz zrobić hello mapowania pliku hostów (% SystemDrive%\drivers\etc\hosts) w następujący sposób:

> 10.0.0.5 contoso.azure-api.net

> 10.0.0.5 contoso.portal.azure-api.net

> 10.0.0.5 contoso.management.azure-api.net

> 10.0.0.5 contoso.scm.azure-api.net

Następnie są dostępne wszystkie punkty końcowe usługi hello hello tworzenia maszyny wirtualnej. Jeśli używany jest serwer niestandardowe DNS w sieci wirtualnej, można również utworzyć rekordy A DNS i uzyskiwać dostęp do tych punktów końcowych z dowolnego miejsca w sieci wirtualnej. 

### <a name="access-on-custom-domain-names"></a>Dostęp do niestandardowych nazw domen:
Jeśli nie chcesz hello tooaccess usługi API Management z hello domyślne nazwy hosta, należy skonfigurować niestandardowe nazwy domen dla wszystkich usług punktów końcowych podobnie jak poniżej

![Skonfigurowanie domeny niestandardowej dla interfejsu API zarządzania][api-management-custom-domain-name]

Następnie można utworzyć rekordu w sieci serwer DNS tooaccess te punkty końcowe, które są dostępne jedynie z sieci wirtualnej.

## <a name="related-content"></a>Związane z zawartością
* [Typowe problemy z konfiguracją sieci podczas konfigurowania APIM w sieci Wirtualnej][Common Network Configuration Issues]
* [Często zadawane pytania dotyczące sieci wirtualnej](../virtual-network/virtual-networks-faq.md)
* [Tworzenie rekord w systemie DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
