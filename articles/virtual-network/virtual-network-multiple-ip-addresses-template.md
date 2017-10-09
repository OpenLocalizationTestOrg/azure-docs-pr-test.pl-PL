---
title: "aaaMultiple adresów IP dla maszyn wirtualnych platformy Azure — szablon | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszyny wirtualnej za pomocą szablonu usługi Azure Resource Manager."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Przypisz wielu adresów IP maszyn toovirtual przy użyciu szablonu usługi Azure Resource Manager

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

W tym artykule opisano, jak toocreate maszynę wirtualną (VM) do wdrożenia usługi Azure Resource Manager hello modelu przy użyciu szablonu usługi Resource Manager. Nie można przypisać wiele prywatnych i publicznych adresów IP toohello tej samej karty Sieciowej podczas wdrażania maszyny Wirtualnej za pośrednictwem hello klasycznego modelu wdrażania. więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Opis szablonu

Wdrażanie szablonu pozwala tooquickly oraz spójnie utworzenie zasobów platformy Azure o wartości innej konfiguracji. Witaj odczytu [Przewodnik po szablonie usługi Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu, jeśli nie masz doświadczenia w obsłudze szablonów usługi Azure Resource Manager. Witaj [wdrożyć maszynę Wirtualną z wielu adresów IP](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) szablon jest wykorzystywany w tym artykule.

<a name="resources"></a>Wdrażanie szablonu hello tworzy hello następujące zasoby:

|Zasób|Nazwa|Opis|
|---|---|---|
|Interfejs sieciowy|*myNic1*|Hello opisane w sekcji scenariusza hello tego artykułu trzy konfiguracje adresów IP są tworzone i przypisywane toothis karty sieciowej.|
|Publiczny zasobu adresu IP|2 są tworzone: *myPublicIP* i *myPublicIP2*|Te zasoby są przydzielonych statyczne publiczne adresy IP, a toohello *IPConfig 1* i *IPConfig 2* opisany w scenariuszu hello konfiguracje adresów IP.|
|VM|*myVM1*|Standardowe DS3 maszyny Wirtualnej.|
|Sieć wirtualna|*myVNet1*|Sieć wirtualną z jednej podsieci o nazwie *mySubnet*.|
|Konto magazynu|Unikatowy toohello wdrożenia|Konto magazynu.|

<a name="parameters"></a>Podczas wdrażania szablonu hello, musisz określić wartości dla hello następujące parametry:

|Nazwa|Opis|
|---|---|
|adminUsername|Nazwa użytkownika administratora. Witaj username muszą być zgodne z [wymagania Azure username](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Hasło hello hasło administratora musi być zgodne z [wymagania dotyczące hasła Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|Nazwa DNS PublicIPAddressName1. Nazwa DNS Hello rozwiąże tooone hello publicznych adresów IP przypisanych toohello maszyny Wirtualnej. Witaj nazwa musi być unikatowa w obrębie hello Azure region (lokalizacja), możesz utworzyć hello maszyny Wirtualnej w ramach.|
|dnsLabelPrefix1|Nazwa DNS PublicIPAddressName2. Nazwa DNS Hello rozwiąże tooone hello publicznych adresów IP przypisanych toohello maszyny Wirtualnej. Witaj nazwa musi być unikatowa w obrębie hello Azure region (lokalizacja), możesz utworzyć hello maszyny Wirtualnej w ramach.|
|OSVersion|wersja systemu Windows i Linux Hello hello maszyny Wirtualnej. system operacyjny Hello jest całkowicie poprawioną obraz powitania podane wybrana wersja systemu Windows i Linux.|
|imagePublisher|wydawcy obrazu systemu Windows i Linux Hello hello wybrane maszyny Wirtualnej.|
|imageOffer|obraz systemu Windows i Linux Hello hello wybrane maszyny Wirtualnej.|

Każdy z zasobów hello wdrożone przez szablon hello jest skonfigurowany przy użyciu kilku ustawień domyślnych. Można wyświetlić te ustawienia przy użyciu jednej z następujących metod hello:

- **Wyświetlanie szablonu hello w witrynie GitHub:** Jeśli znasz szablony, można wyświetlać ustawienia hello w hello [szablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Wyświetl ustawienia powitania po wdrożeniu:** Jeśli nie masz doświadczenia w obsłudze szablony, można wdrożyć szablonu hello przy użyciu kroków w jednym z hello następujące sekcje i następnie wyświetlić ustawienia powitania po wdrożeniu.

Można użyć hello portalu Azure, programu PowerShell lub hello Azure interfejsu wiersza polecenia (CLI) toodeploy hello szablonu. Wszystkie metody tworzenia hello takiego samego wyniku. toodeploy hello szablonu, pełną hello kroków w jednym z hello następujące sekcje:

## <a name="deploy-using-hello-azure-portal"></a>Wdrażanie przy użyciu hello portalu Azure

Szablon hello toodeploy przy użyciu hello portalu Azure, pełną hello następujące kroki:

1. W razie potrzeby zmodyfikuj szablon hello. Szablon Hello wdraża hello zasoby i ustawienia na liście hello [zasobów](#resources) sekcji tego artykułu. więcej informacji na temat szablonów toolearn i w jaki sposób tooauthor ich, przeczytaj hello [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)artykułu.
2. Wdrażanie szablonu hello z jedną z następujących metod hello:
    - **Wybierz hello szablonu w portalu hello:** pełną hello etapami hello [wdrażanie zasobów z szablonu niestandardowego](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) artykułu. Wybierz szablon istniejące hello o nazwie *101-vm wiele ipconfig*.
    - **Bezpośrednio:** kliknij hello następującego szablonu hello tooopen przycisk bezpośrednio w portalu hello:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Niezależnie od metody hello wybierzesz potrzebne wartości toosupply hello [parametry](#parameters) wymienione wcześniej w tym artykule. Po wdrożeniu hello maszyny Wirtualnej, Połącz toohello maszyny Wirtualnej i dodać hello prywatnego adresu IP adresów toohello systemu operacyjnego została wdrożona, wykonując hello etapami hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.

## <a name="deploy-using-powershell"></a>Wdrażanie przy użyciu programu PowerShell

Szablon hello toodeploy przy użyciu programu PowerShell, pełną hello następujące kroki:

1. Wdróż szablon hello, wykonując kroki hello hello [wdrożyć szablon przy użyciu programu PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) artykułu. Witaj opisano wiele opcji wdrażania szablonu. Jeśli wybierzesz toodeploy przy użyciu hello `-TemplateUri parameter`, hello identyfikatora URI dla tego szablonu jest *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Jeśli wybierzesz toodeploy przy użyciu hello `-TemplateFile` parametru kopiowania zawartości hello hello [pliku szablonu](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) z serwisu GitHub do nowego pliku na tym komputerze. W razie potrzeby zmodyfikuj hello zawartość szablonu. Szablon Hello wdraża hello zasoby i ustawienia na liście hello [zasobów](#resources) sekcji tego artykułu. więcej informacji na temat szablonów toolearn i w jaki sposób tooauthor ich, przeczytaj hello [szablonów Authoring Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)artykułu.

    Niezależnie od wybranej toodeploy hello szablonu przy użyciu opcji hello, należy podać wartości na liście hello wartości parametrów hello [parametry](#parameters) sekcji tego artykułu. Jeśli wybierzesz toosupply parametry, używając pliku parametrów, należy skopiować zawartość hello hello [pliku parametrów](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) z serwisu GitHub do nowego pliku na komputerze. Zmodyfikuj wartości hello hello pliku. Użyj pliku hello utworzony jako wartość hello hello `-TemplateParameterFile` parametru.

    Prawidłowe wartości toodetermine hello OSVersion, ImagePublisher i imageOffer parametrów, pełną hello kroki opisane w temacie hello [Nawigacja i wybierz artykuł obrazów maszyny Wirtualnej systemu Windows](../virtual-machines/windows/cli-ps-findimage.md) artykułu.

    >[!TIP]
    >Jeśli nie masz pewności, czy dnslabelprefix jest dostępny, wprowadź hello `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` toofind polecenia wychodzących. Jeśli jest dostępny, hello polecenie zwróci błąd `True`.

2. Po wdrożeniu hello maszyny Wirtualnej, Połącz toohello maszyny Wirtualnej i dodać hello prywatnego adresu IP adresów toohello systemu operacyjnego została wdrożona, wykonując hello etapami hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.

## <a name="deploy-using-hello-azure-cli"></a>Wdrażanie przy użyciu hello wiersza polecenia platformy Azure

Szablon hello toodeploy przy użyciu hello Azure CLI 1.0, pełną hello następujące kroki:

1. Wdróż szablon hello, wykonując kroki hello hello [wdrażania szablonu z hello Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) artykułu. Witaj opisano wiele opcji wdrażania hello szablonu. Jeśli wybierzesz toodeploy przy użyciu hello `--template-uri` (-f), hello identyfikatora URI dla tego szablonu jest *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Jeśli wybierzesz toodeploy przy użyciu hello `--template-file` (-f) parametru kopiowania zawartości hello hello [pliku szablonu](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) z serwisu GitHub do nowego pliku na tym komputerze. W razie potrzeby zmodyfikuj hello zawartość szablonu. Szablon Hello wdraża hello zasoby i ustawienia na liście hello [zasobów](#resources) sekcji tego artykułu. więcej informacji na temat szablonów toolearn i w jaki sposób tooauthor ich, przeczytaj hello [szablonów Authoring Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)artykułu.

    Niezależnie od wybranej toodeploy hello szablonu przy użyciu opcji hello, należy podać wartości na liście hello wartości parametrów hello [parametry](#parameters) sekcji tego artykułu. Jeśli wybierzesz toosupply parametry, używając pliku parametrów, należy skopiować zawartość hello hello [pliku parametrów](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) z serwisu GitHub do nowego pliku na komputerze. Zmodyfikuj wartości hello hello pliku. Użyj pliku hello utworzony jako wartość hello hello `--parameters-file` (-e) parametru.

    Prawidłowe wartości toodetermine hello OSVersion, ImagePublisher i imageOffer parametrów, pełną hello kroki opisane w temacie hello [Nawigacja i wybierz artykuł obrazów maszyny Wirtualnej systemu Windows](../virtual-machines/windows/cli-ps-findimage.md) artykułu.

2. Po wdrożeniu hello maszyny Wirtualnej, Połącz toohello maszyny Wirtualnej i dodać hello prywatnego adresu IP adresów toohello systemu operacyjnego została wdrożona, wykonując hello etapami hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu. Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
