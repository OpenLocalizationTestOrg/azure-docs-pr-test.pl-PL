---
title: "Pomocy technicznej platformy Azure Resource Manager dla usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Przy użyciu programu powershell dla usługi równoważenia obciążenia z usługi Azure Resource Manager. Za pomocą szablonów usługi równoważenia obciążenia"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Za pomocą techniczną platformy Azure Resource Manager z usługą równoważenia obciążenia Azure

Usługa Azure Resource Manager to struktura preferowane dla usług Azure. Moduł równoważenia obciążenia Azure mogą być zarządzane przy użyciu usługi Azure Resource Manager na podstawie interfejsów API i narzędzia.

## <a name="concepts"></a>Pojęcia

Usługa Resource Manager modułu równoważenia obciążenia Azure zawiera następujące zasoby podrzędne:

* Konfiguracja IP frontonu — modułu równoważenia obciążenia może zawierać co najmniej jeden adres IP frontonu, znanej także jako wirtualnych adresów IP (VIP). Te adresy IP są używane podczas transferu danych przychodzących.
* Pula adresów zaplecza — są to adresy IP skojarzone z maszyny wirtualnej sieci karta sieciowa (NIC) na które będą przesyłane obciążenia.
* Reguły równoważenia obciążenia — właściwości reguły mapuje IP danego frontonu i kombinacja portu do zbioru adresów IP zaplecza i portu kombinacji. Moduł równoważenia obciążenia może mieć różne reguły równoważenia obciążenia. Każda reguła zawiera kombinację adresu IP frontonu i portu oraz adresu IP zaplecza i portu, które są powiązane z maszynami wirtualnymi.
* Sond — sond włączyć do śledzenia kondycji wystąpień maszyn wirtualnych. W przypadku niepowodzenia sondy kondycji wystąpienie maszyny Wirtualnej zostanie wykluczony z cyklu automatycznie.
* Reguły NAT ruchu przychodzącego — Definiowanie ruch przychodzący przepływających przez na wierzch reguł NAT zakończenie IP i dystrybuowane do IP zaplecza.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Szablony szybkiego startu

Usługa Azure Resource Manager pozwala inicjować obsługę aplikacji za pomocą deklaratywnych szablonów. W pojedynczym szablonie możesz wdrożyć wiele usług wraz z ich zależnościami. Za pomocą tego samego szablonu możesz wdrażać aplikację na każdym etapie jej cyklu życia.

Szablony mogą zawierać definicji dla maszyn wirtualnych, sieci wirtualne zestawów dostępności, interfejsów sieciowych (NIC), konta magazynu, usługi równoważenia obciążenia, grup zabezpieczeń sieci i publicznych adresów IP. Przy użyciu szablonów można tworzyć wszystko, czego potrzebujesz złożonych aplikacji. Plik szablonu może służyć do zarządzania zawartością system kontroli wersji i współpracy.

[Dowiedz się więcej na temat szablonów](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Dowiedz się więcej o zasoby sieciowe](../virtual-network/resource-groups-networking.md)

Szablony szybkiego startu przy użyciu usługi równoważenia obciążenia Azure można znaleźć w [repozytorium GitHub](https://github.com/Azure/azure-quickstart-templates) hosting zestaw szablonów społeczności wygenerowany.

Przykłady szablonów:

* [2 maszyny wirtualne w moduł równoważenia obciążenia i reguły równoważenia obciążenia](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 maszyn wirtualnych w sieci Wirtualnej przy użyciu reguł wewnętrzny moduł równoważenia obciążenia i moduł równoważenia obciążenia](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 maszyny wirtualne w moduł równoważenia obciążenia i skonfigurować reguły NAT na równoważeniem obciążenia](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Konfigurowanie usługi równoważenia obciążenia Azure za pomocą programu PowerShell lub interfejsu wiersza polecenia

Wprowadzenie do poleceń cmdlet, narzędzi wiersza polecenia i interfejsów API REST usługi Azure Resource Manager

* [Polecenia cmdlet systemu Azure Networking](https://msdn.microsoft.com/library/azure/mt163510.aspx) może służyć do tworzenia modułu równoważenia obciążenia.
* [Jak utworzyć usługę równoważenia obciążenia przy użyciu usługi Azure Resource Manager](load-balancer-get-started-ilb-arm-ps.md)
* [Przy użyciu interfejsu wiersza polecenia platformy Azure w usłudze zarządzania zasobami Azure](../xplat-cli-azure-resource-manager.md)
* [Interfejsy API REST usługi równoważenia obciążenia](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Następne kroki

Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.

Dowiedz się, jak zarządzać [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md). Jest to ważne w przypadku, gdy aplikacja musi podtrzymywania połączenia dla serwerów za modułem równoważenia obciążenia.
