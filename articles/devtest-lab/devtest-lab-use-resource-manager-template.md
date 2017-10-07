---
title: "aaaView i szablon maszyny wirtualnej usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello szablonu usługi Azure Resource Manager z toocreate maszyny wirtualnej innych maszyn wirtualnych"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Użyj szablonu usługi Azure Resource Manager maszynę wirtualną

Podczas tworzenia maszyny wirtualnej (VM) w usłudze DevTest Labs za pośrednictwem hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), możesz wyświetlić szablonu usługi Azure Resource Manager hello przed zapisaniem hello maszyny Wirtualnej. Witaj szablonu mogą być następnie użyta jako toocreate podstawy więcej maszyn wirtualnych laboratorium o hello tych samych ustawień.

W tym artykule opisano, jak tooview hello szablonu usługi Resource Manager, podczas tworzenia maszyny Wirtualnej i w jaki sposób toodeploy jego nowsze tworzenie tooautomate hello tej samej maszyny Wirtualnej.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Wielu maszyn wirtualnych i szablony Menedżera zasobów maszyn wirtualnych na jednym
Istnieją dwa sposoby toocreate maszyny wirtualne w usłudze DevTest Labs przy użyciu szablonu usługi Resource Manager: udostępnianie zasobów Microsoft.DevTestLab/labs/virtualmachines hello lub udostępnić hello Microsoft.Commpute/virtualmachines zasobów. Każda jest używane w różnych scenariuszach i wymagają różnych uprawnień.

- Szablony Menedżera zasobów, korzystających z typu zasobu Microsoft.DevTestLab/labs/virtualmachines (podaną we właściwości "zasobu" hello, w szablonie hello) można udostępnić laboratorium poszczególnych maszyn wirtualnych. Każda maszyna wirtualna następnie jest wyświetlany jako jeden element na liście hello DevTest Labs maszyn wirtualnych:

   ![Lista maszyn wirtualnych jako pojedyncze elementy na liście hello DevTest Labs maszyny wirtualne](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Ten typ szablonu usługi Resource Manager można udostępnić za pośrednictwem hello polecenia programu PowerShell usługi Azure **AzureRmResourceGroupDeployment nowy** lub za pomocą polecenia interfejsu wiersza polecenia Azure hello **Utwórz wdrożenie grupy az** . Wymagane uprawnienia administratora tak użytkowników, którzy są przypisani z rolą użytkownika DevTest Labs nie można wykonać wdrożenia hello. 

- Szablony Menedżera zasobów, korzystających z typu zasobu Microsoft.Compute/virtualmachines umożliwia obsługę wielu maszyn wirtualnych jako jednym środowisku na liście hello DevTest Labs maszyn wirtualnych:

   ![Lista maszyn wirtualnych jako pojedyncze elementy na liście hello DevTest Labs maszyny wirtualne](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Maszyny wirtualne w tym samym środowisku, które mogą być zarządzane wspólnie powitalne i udziału hello sam cykl życia. Użytkownicy z przypisaną z rolą użytkownika DevTest Labs utworzyć środowiska przy użyciu tych szablonów, jak długo hello administrator skonfigurował laboratorium hello w ten sposób.

Hello dalszej części tego artykułu opisano szablony Menedżera zasobów, używające Mirosoft.DevTestLab/labs/virtualmachines. Są one używane przez tworzenie maszyny Wirtualnej laboratorium tooautomate Administratorzy laboratorium (na przykład claimable VMs) lub generowania złotego obrazu (na przykład obraz fabryka).

[Najlepsze rozwiązania dotyczące tworzenia szablonów usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) oferuje wiele toohelp wskazówki i sugestie dotyczące tworzenia szablonów usługi Azure Resource Manager, które są toouse niezawodne i łatwe.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Wyświetlanie i zapisać szablon usługi Resource Manager maszynę wirtualną
1. Wykonaj czynności hello [tworzenie pierwszej maszyny Wirtualnej w laboratorium](devtest-lab-create-first-vm.md) toobegin tworzenia maszyny wirtualnej.
1. Wprowadź informacje wymagane powitania dla maszyny wirtualnej, a następnie dodaj wszelkie artefakty dla tej maszyny Wirtualnej.
1. U dołu hello hello Konfiguruj ustawienia okna, wybierz **szablon ARM widoku**.

   ![Szablon ARM przycisk](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Skopiuj i Zapisz toouse szablonu usługi Resource Manager hello nowsze toocreate inną maszynę wirtualną.

   ![Toosave szablon Menedżera zasobów do późniejszego użycia](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Po zapisaniu szablonu usługi Resource Manager hello, musisz zaktualizować hello sekcji parametrów szablonu hello przed jego użyciem. Można utworzyć parameter.json, który dostosowuje tylko hello parametrów, poza hello rzeczywiste szablonu usługi Resource Manager. 

![Dostosowywanie ma parametrów przy użyciu pliku JSON](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Wdrażanie usługi Resource Manager toocreate szablonu maszyny Wirtualnej
Po zapisać szablon usługi Resource Manager i dostosować go do swoich potrzeb można użyć tooautomate tworzenia maszyny Wirtualnej. [Wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) w tym artykule opisano sposób toouse programu Azure PowerShell z toodeploy szablonów usługi Resource Manager tooAzure Twojego zasobów. [Wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i interfejsu wiersza polecenia Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) w tym artykule opisano sposób toouse wiersza polecenia platformy Azure z toodeploy szablony Menedżera zasobów tooAzure Twojego zasobów.

> [!NOTE]
> Tylko użytkownik z uprawnieniami właściciela laboratorium można utworzyć maszyny wirtualne z szablonem usługi Resource Manager przy użyciu programu Azure PowerShell. Jeśli chcesz tooautomate tworzenia maszyny Wirtualnej przy użyciu szablonu usługi Resource Manager i tylko mają uprawnienia użytkowników, możesz użyć hello [ **tworzenia maszyny wirtualnej laboratorium az** w hello interfejsu wiersza polecenia polecenie](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[utworzyć środowiska wielu maszyn wirtualnych z szablonami usługi Resource Manager](devtest-lab-create-environment-from-arm.md).
* Poznaj więcej szablonów usługi Resource Manager szybki start DevTest Labs automatyzacji z hello [publicznego repozytorium DevTest Labs GitHub](https://github.com/Azure/azure-quickstart-templates).
