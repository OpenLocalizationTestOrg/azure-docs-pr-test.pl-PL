---
title: "Obsługa Menedżera zasobów dla usługi równoważenia obciążenia aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Za pomocą techniczną platformy Azure Resource Manager z usługą równoważenia obciążenia Azure

Usługa Azure Resource Manager jest hello preferowane framework dla usług Azure. Moduł równoważenia obciążenia Azure mogą być zarządzane przy użyciu usługi Azure Resource Manager na podstawie interfejsów API i narzędzia.

## <a name="concepts"></a>Pojęcia

Usługa Resource Manager modułu równoważenia obciążenia Azure zawiera hello następujące zasoby podrzędne:

* Konfiguracja IP frontonu — modułu równoważenia obciążenia może zawierać co najmniej jeden adres IP frontonu, znanej także jako wirtualnych adresów IP (VIP). Te adresy IP stanowią wejściowych hello ruchu.
* Pula adresów zaplecza — są to adresy IP skojarzone z maszyną wirtualną hello sieci karta sieciowa (NIC) będą dystrybuowane toowhich obciążenia.
* Reguły równoważenia obciążenia — właściwości reguły mapowania IP frontonu danego portu kombinacja tooa zbiór adresów IP zaplecza i portu kombinacji. Moduł równoważenia obciążenia może mieć różne reguły równoważenia obciążenia. Każda reguła zawiera kombinację adresu IP frontonu i portu oraz adresu IP zaplecza i portu, które są powiązane z maszynami wirtualnymi.
* Sond — sond Włącz możesz tookeep track hello kondycji wystąpień maszyn wirtualnych. W przypadku niepowodzenia sondy kondycji hello wystąpienia maszyny Wirtualnej zostanie wykluczony z cyklu automatycznie.
* Zasady translacji NAT ruchu przychodzącego — Definiowanie reguł NAT hello ruch przychodzący przepływających przez hello IP frontonu i ponownie rozproszonej toohello zakończenia IP.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Szablony szybkiego startu

Usługa Azure Resource Manager umożliwia tooprovision aplikacji przy użyciu szablonu deklaracyjnego. Pojedynczy szablon umożliwia wdrożenie wielu usług wraz z ich zależnościami. Użyj hello tego samego szablonu toorepeatedly wdrożenia aplikacji podczas każdego etapu cyklu życia aplikacji hello.

Szablony mogą zawierać definicji dla maszyn wirtualnych, sieci wirtualne zestawów dostępności, interfejsów sieciowych (NIC), konta magazynu, usługi równoważenia obciążenia, grup zabezpieczeń sieci i publicznych adresów IP. Przy użyciu szablonów można tworzyć wszystko, czego potrzebujesz złożonych aplikacji. Plik szablonu Hello można sprawdzić w kontroli wersji i współpracy system zarządzania zawartością.

[Dowiedz się więcej na temat szablonów](../azure-resource-manager/resource-manager-template-walkthrough.md)

[Dowiedz się więcej o zasoby sieciowe](../virtual-network/resource-groups-networking.md)

Szablony szybkiego startu przy użyciu usługi równoważenia obciążenia Azure można znaleźć w [repozytorium GitHub](https://github.com/Azure/azure-quickstart-templates) hosting zestaw szablonów społeczności wygenerowany.

Przykłady szablonów:

* [2 maszyny wirtualne w moduł równoważenia obciążenia i reguły równoważenia obciążenia](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 maszyn wirtualnych w sieci Wirtualnej przy użyciu reguł wewnętrzny moduł równoważenia obciążenia i moduł równoważenia obciążenia](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 maszyny wirtualne w moduł równoważenia obciążenia i skonfigurować reguły NAT na powitania równoważeniem obciążenia](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Konfigurowanie usługi równoważenia obciążenia Azure za pomocą programu PowerShell lub interfejsu wiersza polecenia

Wprowadzenie do poleceń cmdlet, narzędzi wiersza polecenia i interfejsów API REST usługi Azure Resource Manager

* [Polecenia cmdlet systemu Azure Networking](https://msdn.microsoft.com/library/azure/mt163510.aspx) mogą być używane toocreate modułu równoważenia obciążenia.
* [Jak toocreate modułu równoważenia obciążenia przy użyciu usługi Azure Resource Manager](load-balancer-get-started-ilb-arm-ps.md)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Resource Management](../xplat-cli-azure-resource-manager.md)
* [Interfejsy API REST usługi równoważenia obciążenia](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Następne kroki

Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.

Dowiedz się, jak toomanage [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md). Jest to ważne w przypadku, gdy aplikacja wymaga połączenia tookeep aktywności dla serwerów za modułem równoważenia obciążenia.
