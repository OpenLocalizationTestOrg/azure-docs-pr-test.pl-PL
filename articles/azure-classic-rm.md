---
title: "tryby wdrażania (klasyczne) Manager i zarządzania usługami aaaResource | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello różnice między Resource Manager i klasycznych modeli wdrażania."
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Modele wdrażania Azure
Witaj platformy Azure jest w stanie przejścia.  Czy są nowe tooAzure lub używany był on lat, jest ważne toounderstand niektóre zmiany klucza hello jest czynione platformy toohello podczas ten proces przejścia.

Wszystkie zasoby platformy Azure obsługuje jeden lub oba hello następujące modele wdrażania:

* **Menedżer zasobów:** jest hello najnowsze model wdrożenia dla zasobów platformy Azure. Najwięcej zasobów nowszej obsługują już ten model wdrażania i po pewnym czasie zostaną wszystkie zasoby.   
* **Klasycznym:** ten model jest obsługiwany przez większość istniejących zasobów Azure dzisiaj. Dodano nowe zasoby tooAzure nie obsługuje tego modelu.

dokumentacji Hello każdej usługi, która modele on szczegółowe zasobów platformy Azure mogą być tworzone z.

## <a name="why-does-this-matter"></a>Dlaczego ta sprawa?
Ma znaczenia dla hello z następujących powodów:

* funkcji platformy Azure Hello różnią się w tych dwóch modeli.  Na przykład można utworzyć zasoby utworzone przy użyciu modelu wdrażania usługi Resource Manager hello (lub po prostu Resource Manager) z [szablonów usługi Azure Resource Manager](azure-resource-manager/resource-group-overview.md#template-deployment), a nie zasoby utworzone za pomocą hello klasycznego modelu wdrożenia.
* Witaj funkcji poszczególnych zasobów platformy Azure lub zachowania mogą się różnić między dwa modele hello lub istnieje tylko w jednym modelu lub hello innych.  Na przykład równoważeniem obciążenia ruchu na maszyny wirtualne utworzone za pomocą klasycznego modelu wdrożenia hello jest *niejawne* ponieważ maszyny wirtualne są członkami usługi w chmurze platformy Azure i obciążenia jest automatycznie równoważone wirtualnego maszyny w ramach usługi w chmurze. Maszyny wirtualne utworzone za pomocą Menedżera zasobów nie są elementami członkowskimi usługi w chmurze i oddzielne zasoby usługi równoważenia obciążenia Azure muszą być *jawnie* utworzony tooload równoważenie ruchu między wieloma maszynami wirtualnymi.  
* Sposób tworzenia, konfigurowania i zarządzania zasobami Azure różni się od tych dwóch modeli.
* Zasoby utworzone przy użyciu jednego modelu wdrażania niekoniecznie nie może współpracować z utworzonych przy użyciu modelu wdrażania różnych zasobów. Na przykład utworzone za pomocą jednego modelu wdrażania maszyn wirtualnych platformy Azure może być tylko tooAzure połączone sieci wirtualne utworzone za pomocą hello tym samym modelu wdrażania.    

Bazowy wszystkich modeli wdrażania hello jest interfejs programowania aplikacji (API) dla każdego zasobu.  Brak [interfejs API Menedżera zasobów](https://msdn.microsoft.com/library/azure/dn948464.aspx) dla modelu wdrażania usługi Resource Manager hello i [interfejs API zarządzania usługami](https://msdn.microsoft.com/library/azure/ee460799.aspx) dla hello klasycznego modelu wdrożenia. Programiści mogą pisać kod toointeract z poniższych interfejsów API *bezpośrednio*.  

Informatycy, zwykle interakcji z poniższych interfejsów API *pośrednio* przy użyciu graficznego portalu w przeglądarce sieci web, przy użyciu programu Azure PowerShell polecenia cmdlet na komputerze z systemem Windows lub za pomocą hello Azure interfejsu wiersza polecenia (CLI) albo Komputer z systemem Windows, OS X i Linux. Wszystkie te trzy pośrednie metody używane przez hello specjalista IT bezpośrednią interakcję z hello interfejsów API. Oznacza to, że w przypadku nowych funkcji wprowadzonych toohello Azure platforma lub zasobów, jest zawsze bezpośrednio dostępne za pośrednictwem interfejsu API hello najpierw hello pośrednich metod uzyskania obsługę hello nowych zasobów i funkcji, gdy zostanie udostępniona hello interfejsu API.  

Hello w poniższych rozdziałach opisano zasobów jak Azure są konfigurowane za pomocą metody pośrednie hello trzech za pomocą hello różne modele wdrażania.

## <a name="portals"></a>Portale
Platforma Azure ma dwa portale:

* **[Azure portal](https://manage.windowsazure.com):** Jeśli obecnie używasz Azure przez pewien czas, używane tego portalu. Jest używana toocreate i skonfigurować starszych zasobów platformy Azure, które obsługują hello klasycznego modelu wdrażania. Nie można go używać toocreate lub skonfigurować zasoby, które obsługują tylko usługi Resource Manager. 
* **[Portal Azure w wersji zapoznawczej](https://azure.microsoft.com/overview/preview-portal/):** Jeśli używasz nowszej zasobów platformy Azure, prawdopodobnie używane tego portalu. Można go toocreate używane i skonfigurować niektóre zasoby platformy Azure. Zostanie ostatecznie toocreate może być oraz skonfigurować wszystkie zasoby platformy Azure z nim. Dla niektórych zasobów, które obsługują obu modeli wdrażania można toocreate używane ten portal i skonfigurować przy użyciu modelu wdrażania, albo zasób. 

Niektórych zasobów i funkcji tylko może można tworzyć i konfigurować w jednym portalu lub hello innych. Niektórych zasobów lub funkcji (jeszcze) nie można utworzyć lub skonfigurowany w obu portalu i może być konfigurowany tylko przy użyciu programu PowerShell, hello interfejsu wiersza polecenia lub oba. Hello dokumentacji dla każdego zasobu Azure zawiera szczegóły dotyczące metody, które mogą być tworzone z. 

## <a name="powershell"></a>PowerShell
Z [PowerShell](/powershell/azureps-cmdlets-docs) można użyć wiersza polecenia lub autora toocreate skryptów i skonfigurować zasoby platformy Azure z komputerem z systemem Windows.  Poszczególne zasoby platformy Azure mają [poleceń cmdlet Menedżera zasobów](/powershell/azure/overview), [poleceń cmdlet do zarządzania usługi](/powershell/azure/overview?view=azuresmps-3.7.0), lub obie.  Niektórych zasobów i funkcji mogą być tworzone tylko i/lub skonfigurowana przy użyciu programu PowerShell lub hello interfejsu wiersza polecenia. W zależności od zasobów hello, korzystając z polecenia cmdlet programu PowerShell Menedżera zasobów może mieć dwie opcje dotyczące tworzenia i konfigurowania zasobów platformy Azure:

* **Tylko polecenia cmdlet programu PowerShell:** można tworzyć i konfigurować poszczególnych zasobów platformy Azure oddzielnie, używając polecenia cmdlet powitania dla każdego zasobu. Można to zrobić przy użyciu wiersza polecenia lub przez dołączenie wielu poleceń skryptu programu PowerShell, który można przechowywać i wersji.
* **Polecenia cmdlet programu PowerShell z szablonem usługi Azure Resource Manager:** można użyć programu PowerShell toocreate Azure zasobów przy użyciu szablonu usługi Azure Resource Manager. Szablony mogą być zapisane i numerów wersji. Dowiedz się więcej, odczytując hello [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md) artykułu. Kilka [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) dla typowych rozwiązań, które można pobrać i zmodyfikować za istnieje.

## <a name="cli"></a>Interfejs wiersza polecenia
Można utworzyć i skonfigurować zasoby platformy Azure z komputerów z systemem Windows, OS X i Linux przy użyciu hello interfejsu wiersza polecenia.  Witaj odczytu [hello instalowanie interfejsu wiersza polecenia Azure](cli-install-nodejs.md) hello tooinstall artykułu interfejs wiersza polecenia w systemie operacyjnym wyboru. Podobnie jak programu PowerShell, są inne polecenia, które muszą zostać zastosowane w zależności od tego, czy tworzysz zasobów przy użyciu [Resource Manager](xplat-cli-azure-resource-manager.md) lub hello [klasyczny (Zarządzanie usługą)](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) modele wdrażania.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [Resource Manager](azure-resource-manager/resource-group-overview.md).
* Zrozumienie sposobu zbyt[szablony projektów](best-practices-resource-manager-design-templates.md).

