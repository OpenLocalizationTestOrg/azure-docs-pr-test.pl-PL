---
title: "aaaUsing usługi Azure DNS z innymi usługami Azure | Dokumentacja firmy Microsoft"
description: "Opis sposobu tooresolve usługi Azure DNS toouse nazw dla innych usług Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Działanie usługi Azure DNS z innymi usługami Azure

Usługa DNS platformy Azure jest hostowanej usługi DNS zarządzania i nazwy rozwiązania. Dzięki temu można toocreate publicznej nazwy DNS dla hello inne aplikacje i usługi wdrożone na platformie Azure. Tworzenie nazwę usługi Azure w domeny niestandardowej jest tak proste, jak dodawanie rekordu hello poprawnego typu usługi.

* Przypadku dynamicznie przydzielone adresy IP należy utworzyć rekord CNAME w systemie DNS tej nazwy DNS toohello mapy Azure utworzony dla Twojej usługi. Standardy usługi DNS uniemożliwić przy użyciu rekordu CNAME dla hello wierzchołku strefy.
* Dla statycznie przydzielone adresy IP, można utworzyć rekord A systemu DNS przy użyciu dowolnej nazwy, w tym *naked domeny* nazwie w wierzchołku strefy hello.

Witaj poniższej tabeli przedstawiono hello obsługiwane typy rekordów, które mogą być używane dla różnych usług Azure. Jak widać z tej tabeli, usługi DNS platformy Azure obsługuje tylko rekordy DNS dla zasobów sieciowych połączonych z Internetem. Usługa DNS platformy Azure nie może służyć do rozpoznawania nazw wewnętrznych adresów prywatnych.

| Usługa platformy Azure | Interfejs sieciowy | Opis |
| --- | --- | --- |
| Application Gateway |[Frontonu publicznego adresu IP](dns-custom-domain.md#public-ip-address) |Można utworzyć rekord DNS A lub CNAME. |
| Moduł równoważenia obciążenia |[Frontonu publicznego adresu IP](dns-custom-domain.md#public-ip-address)  |Można utworzyć rekord DNS A lub CNAME. Moduł równoważenia obciążenia mają adres IPv6 publicznego adresu IP, który jest przypisywany dynamicznie. W związku z tym należy utworzyć rekord CNAME dla adresu IPv6. |
| Traffic Manager |Nazwa publicznego |Można utworzyć tylko rekord CNAME, który mapuje nazwę trafficmanager.net toohello przypisane tooyour profilu usługi Traffic Manager. Aby uzyskać więcej informacji, zobacz [działa jak Menedżera ruchu](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Usługi w chmurze |[Publiczny adres IP](dns-custom-domain.md#public-ip-address) |Dla statycznie przydzielone adresy IP należy utworzyć rekord A systemu DNS. W przypadku dynamicznie przydzielone adresy IP, należy utworzyć rekord CNAME, który mapuje toohello *cloudapp.net* nazwy. Ta reguła ma zastosowanie tooVMs utworzone w portalu klasycznym hello, ponieważ są wdrożone jako usługa w chmurze. Aby uzyskać więcej informacji, zobacz [Konfigurowanie niestandardowej nazwy domeny usług w chmurze](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| App Service | [Zewnętrznym adresem IP](dns-custom-domain.md#app-service-web-apps) |Dla zewnętrznych adresów IP należy utworzyć rekord A systemu DNS. W przeciwnym razie należy utworzyć rekord CNAME, który mapuje nazwę azurewebsites.net toohello. Aby uzyskać więcej informacji, zobacz [mapy tooan nazwy domeny niestandardowej aplikacji Azure](../app-service-web/web-sites-custom-domain-name.md) |
| Maszyny wirtualne usługi Resource Manager |[Publiczny adres IP](dns-custom-domain.md#public-ip-address) |Menedżer zasobów maszyn wirtualnych może mieć publiczny adres IP. Maszyny Wirtualnej przy użyciu adresu publicznego adresu IP może być również za modułem równoważenia obciążenia. Można utworzyć rekord DNS A lub CNAME dla hello publiczny adres. Ta nazwa niestandardowych może być używane toobypass hello VIP modułu równoważenia obciążenia hello. |
| Klasyczne maszyny wirtualne |[Publiczny adres IP](dns-custom-domain.md#public-ip-address) |Klasyczne maszyny wirtualne utworzone za pomocą programu PowerShell lub interfejsu wiersza polecenia można skonfigurować za pomocą dynamicznej lub statycznej (zastrzeżony) wirtualny adres. Można utworzyć rekordu CNAME systemu DNS lub rekord, odpowiednio. |
