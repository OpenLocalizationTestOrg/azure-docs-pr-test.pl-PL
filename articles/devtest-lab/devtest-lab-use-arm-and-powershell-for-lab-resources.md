---
title: "aaaCreate lub zmodyfikować labs automatycznie za pomocą szablonów usługi Azure Resource Manager przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak szablonów usługi Azure Resource Manager toouse toocreate programu PowerShell lub zmodyfikować labs automatycznie w laboratorium DevTest lab"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Tworzenie lub modyfikowanie labs automatycznie przy użyciu szablonów usługi Azure Resource Manager i programu PowerShell

DevTest Labs udostępnia wiele szablonów usługi Azure Resource Manager i skryptów programu PowerShell, które pomagają w szybkim i automatyczne tworzenie nowych labs lub zmodyfikować istniejącą labs oraz następnie wdrażania tych zasobów.

W tym artykule opisano informacje pomocne przy użyciu tych szablonów i skryptów tworzenia hello tooautomate, modyfikacji i wdrażania programu labs proces hello. Ten artykuł zawiera także gdzie można znaleźć więcej informacji na temat sposobu toouse PowerShell tooperform niektóre typowe zadania w usłudze DevTest Labs.

## <a name="step-1-gather-your-templates-and-scripts"></a>Krok 1: Zbieranie z szablonów i skryptów
Można znaleźć wstępnie wprowadzone [szablonów usługi Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) i [skryptów programu PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) na naszego publicznego [repozytorium Github](https://github.com/Azure/azure-devtestlab). Używane jako-, lub dostosować je do potrzeb i zapisanie ich w ramach własnego [prywatne repozytorium Git](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Krok 2: Modyfikowanie szablonu usługi Azure Resource Manager
Możesz wykonać kroki hello na [Tworzenie pierwszego szablonu usługi Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) Jeśli nigdy nie utworzono szablonu przed.

Ponadto [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) oferuje wiele toohelp wskazówki i sugestie dotyczące tworzenia szablonów usługi Azure Resource Manager, które są toouse niezawodne i łatwe. Zazwyczaj będzie używać odmianą jednej z metod hello lub przykłady podane i zmodyfikować szablon do własnych potrzeb.

## <a name="step-3-deploy-resources-with-powershell"></a>Krok 3: Wdrażanie zasobów przy użyciu programu PowerShell
Po dostosowaniu z szablonów i skrypty, wykonaj kroki hello niezbędne zbyt[wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). Artykuł Hello zawiera ogólne informacje o korzystaniu z programu Azure PowerShell z toodeploy szablonów usługi Azure Resource Manager tooAzure Twojego zasobów.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Typowe zadania, które można wykonywać w usłudze DevTest labs przy użyciu programu PowerShell
Istnieje wielu innych typowych zadań, które można zautomatyzować za pomocą programu PowerShell. Witaj następujące części dokumentacji hello konspektu tooperform wymagane kroki hello tych zadań.

* [Tworzenie niestandardowego obrazu z pliku VHD za pomocą programu PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Przekaż toolab pliku wirtualnego dysku twardego konto magazynu przy użyciu programu PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Dodaj użytkownika zewnętrznego laboratorium tooa przy użyciu programu PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Tworzenie laboratorium niestandardowej roli zabezpieczeń przy użyciu programu PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak toocreate [prywatne repozytorium Git](devtest-lab-add-artifact-repo.md) którym będą przechowywanie szablony niestandardowe lub skryptów.
* Eksploruj hello [szablonów usługi Azure Resource Manager z galerii szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).
