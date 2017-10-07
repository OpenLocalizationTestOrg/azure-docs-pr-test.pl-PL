---
title: "aaaDeploy zestawu skalowania maszyn wirtualnych za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Wdrażanie zestawów skali maszyny wirtualnej za pomocą szablonu usługi Resource Manager i Visual Studio"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Jak toocreate, zestawu skalowania maszyn wirtualnych, z programem Visual Studio
W tym artykule opisano, jak toodeploy Azure zestawu skalowania maszyn wirtualnych za pomocą programu Visual Studio wdrożenie grupy zasobów.

[Zestawy skalowania maszyny wirtualnej Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) jest toodeploy rozwiązań usługi obliczenia Azure zasobów i zarządzanie kolekcją podobnych maszyn wirtualnych z automatycznego skalowania i równoważenie obciążenia. Można udostępnić i wdrożyć zestawy skalowania maszyny wirtualnej przy użyciu [szablony Menedżera zasobów Azure](https://github.com/Azure/azure-quickstart-templates). Szablony usługi Azure Resource Manager można wdrożyć przy użyciu interfejsu wiersza polecenia Azure, programu PowerShell, REST, a także bezpośrednio z programu Visual Studio. Program Visual Studio oferuje zestaw przykład szablonów, które można wdrożyć w ramach projektu wdrożenia grupy zasobów platformy Azure.

Wdrożenia grupy zasobów platformy Azure są toogroup sposób i opublikować zestawu powiązanych zasobów systemu Azure w ramach operacji pojedynczego wdrożenia. Więcej informacji o nich w tym miejscu: [tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Wymagania wstępne
tooget rozpoczęto wdrażanie zestawy skalowania maszyny wirtualnej w programie Visual Studio, potrzebne są następujące hello:

* Visual Studio 2013 lub nowszy
* Zestaw Azure SDK 2.8 2.7 i 2.9

>[!NOTE]
>W poniższych instrukcjach przyjęto w przypadku korzystania z programu Visual Studio z [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Tworzenie projektu
1. Utwórz nowy projekt w programie Visual Studio, wybierając **pliku | Nowy | Projekt**.
   
    ![Nowy plik][file_new]

2. W obszarze **Visual C# | Chmura**, wybierz **usługi Azure Resource Manager** toocreate projektu wdrażania szablonu usługi Azure Resource Manager.
   
    ![Tworzenie projektu][create_project]

3. Z listy hello szablony wybierz hello Linux lub szablon ustawić skali maszyny wirtualnej systemu Windows.
   
   ![Wybierz szablon][select_Template]

4. Po utworzeniu projektu Zobacz skryptów wdrażania środowiska PowerShell szablonu usługi Azure Resource Manager i pliku parametrów dla hello zestawu skalowania maszyn wirtualnych.
   
    ![Eksplorator rozwiązań][solution_explorer]

## <a name="customize-your-project"></a>Dostosowywanie projektu
Teraz możesz edytować hello toocustomize szablonu reguły równoważenia go na potrzeby aplikacji, takich jak dodawanie właściwości rozszerzenia maszyny Wirtualnej lub edytowanie obciążenia. Domyślnie hello szablony zestawu skali maszyny wirtualnej są skonfigurowane toodeploy hello AzureDiagnostics rozszerzenia, co pozwala na łatwe tooadd reguł skalowania automatycznego. Ponadto wdraża z publicznym adresem IP skonfigurowano reguły NAT ruchu przychodzącego modułu równoważenia obciążenia. 

Moduł równoważenia obciążenia Hello umożliwia nawiązanie połączenia toohello wystąpień maszyn wirtualnych z protokołu SSH (Linux) lub protokołu RDP (system Windows). zakres portów frontonu Hello rozpoczyna się od 50000. Dla systemu linux oznacza to, że jeśli użytkownik SSH tooport 50000, są routingiem tooport 22 z hello pierwsza maszyna wirtualna w hello zestawu skalowania maszyny wirtualnej. Łączenie tooport 50001 jest kierowany tooport 22 z hello drugie maszyny Wirtualnej i tak dalej.

 Tooedit dobrze szablonów z programem Visual Studio jest toouse hello konspekt pliku JSON tooorganize hello parametrów, zmienne i zasobów. Po zrozumieniu hello schematu programu Visual Studio może wskazywać błędy w szablonie przed przystąpieniem do wdrażania.

![Eksplorator JSON][json_explorer]

## <a name="deploy-hello-project"></a>Wdrażanie projektu hello
1. Wdrażanie zasobów hello szablon Menedżera zasobów Azure toocreate hello zestawu skalowania maszyn wirtualnych. Kliknij prawym przyciskiem myszy węzeł projektu hello i wybierz polecenie **Wdróż | Nowe wdrożenie**.
   
    ![Wdrażanie szablonu][5deploy_Template]
    
2. W oknie dialogowym "Wdróż tooResource grupy" hello, wybierz subskrypcję.
   
    ![Wdrażanie szablonu][6deploy_Template]

3. W tym miejscu można utworzyć grupy zasobów platformy Azure toodeploy szablon.
   
    ![Nową grupę zasobów][new_resource]

4. Następnie kliknij przycisk **Edytuj parametry** tooenter parametry przekazywane tooyour szablonu. Podaj hello nazwy użytkownika i hasła dla hello systemu operacyjnego, który jest wymagany toocreate hello wdrożenia. Jeśli nie masz narzędzia programu PowerShell dla programu Visual Studio, zainstalowane, zalecane jest toocheck **zapisywanie haseł** tooavoid ukryte wiersza polecenia programu PowerShell monit, lub użyj [Obsługa keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Edytowanie parametrów][edit_parameters]

5. Teraz kliknij **Wdróż**. Witaj **dane wyjściowe** okno zawiera hello postępu wdrożenia. Należy pamiętać, że akcja hello jest wykonywany hello **AzureResourceGroup.ps1 Wdróż** skryptu.
   
   ![Okno danych wyjściowych][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Eksplorowanie sieci zestawu skali maszyny wirtualnej
Po zakończeniu wdrażania hello, można wyświetlić hello nowego zestawu skalowania maszyn wirtualnych w Visual Studio hello **Eksplorator chmury** (Lista hello odświeżania). Eksplorator chmury umożliwia zarządzanie zasobami Azure w programie Visual Studio podczas tworzenia aplikacji. Można również wyświetlić zestawu skalowania maszyn wirtualnych w hello [portalu Azure](https://portal.azure.com) i [Eksploratora zasobów Azure](https://resources.azure.com/).

![Eksplorator chmury][cloud_explorer]

 Hello portal udostępnia najlepszy sposób hello toovisually zarządzać infrastruktury platformy Azure przy użyciu przeglądarki sieci web, gdy Eksploratora zasobów Azure zapewnia prosty sposób tooexplore i debugowania zasobów platformy Azure, nadanie okna do Witaj, "Wyświetl wystąpienia" i również przedstawiający programu PowerShell polecenia hello zasoby, które jest wyświetlany.

## <a name="next-steps"></a>Następne kroki
Po pomyślnym wdrożeniu zestawy skalowania maszyny wirtualnej za pomocą programu Visual Studio, można dostosować toosuit Twojego projektu wymagań aplikacji. Na przykład skonfigurować automatyczne skalowanie, dodając **Insights** zasobów, dodając infrastruktury tooyour szablonu (na przykład autonomicznych maszyn wirtualnych) lub wdrażanie aplikacji przy użyciu hello niestandardowego rozszerzenia skryptu. Dobrym przykładem szablonów można znaleźć w hello [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) repozytorium GitHub (Wyszukaj "vmss").

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
