---
title: "Zarządzanie zasobami za pomocą wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Umożliwia zarządzanie zasobami platformy Azure i grup Azure interfejsu wiersza polecenia (CLI)"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a>Użyj wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [Interfejs wiersza polecenia platformy Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfejs API REST](resource-manager-rest-api.md)
> 
> 

Interfejs wiersza polecenia platformy Azure (Azure CLI) jest jednym z kilku narzędzi można użyć do wdrożenia i zarządzania zasobami za pomocą Menedżera zasobów. W tym artykule przedstawiono typowe sposoby zarządzania zasobami Azure i grup zasobów przy użyciu wiersza polecenia platformy Azure w trybie Menedżera zasobów. Aby dowiedzieć się, jak wdrażanie zasobów za pomocą interfejsu wiersza polecenia, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md). Ogólne dotyczące zasobów platformy Azure i Menedżer zasobów, odwiedź stronę [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

> [!NOTE]
> Do zarządzania zasobami Azure z wiersza polecenia platformy Azure, musisz [instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md), i [logowanie do platformy Azure](../xplat-cli-connect.md) przy użyciu `azure login` polecenia. Upewnij się, że interfejsu wiersza polecenia jest w trybie Menedżera zasobów (Uruchom `azure config mode arm`). Po wykonaniu tych czynności możesz rozpocząć pracę.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Pobieranie grup zasobów i zasoby
### <a name="resource-groups"></a>Grupy zasobów
Aby uzyskać listę wszystkich grup zasobów w Twojej subskrypcji i ich lokalizacje, uruchom następujące polecenie.

    azure group list


### <a name="resources"></a>Zasoby
 Aby wyświetlić listę wszystkich zasobów w grupie, takie jak jedną o nazwie *testRG*, użyj następującego polecenia:

    azure resource list testRG

Aby wyświetlić poszczególnych zasobów w grupie, takie jak maszyny Wirtualnej o nazwie *MyUbuntuVM*, użyj polecenia podobnie do następującej:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Powiadomienie **Microsoft.Compute/virtualMachines** parametru. Ten parametr określa typ zasobu, którego chcesz uzyskać informacje na.

> [!NOTE]
> Korzystając z **zasobów platformy azure** polecenia innych niż **listy** polecenia, należy określić wersję interfejsu API zasobu z **-o** parametru. Jeśli nie wiesz o wersji interfejsu API, zapoznaj się z pliku szablonu i znajdź pole apiVersion zasobu. Aby uzyskać więcej informacji o wersji interfejsu API w Menedżerze zasobów, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).
> 
> 

Podczas wyświetlania szczegółowych informacji w zasobie, często jest przydatne do użycia `--json` parametru. Ten parametr sprawia, że dane wyjściowe bardziej czytelny, ponieważ niektóre wartości są zagnieżdżone struktury lub kolekcji. W poniższym przykładzie pokazano zwracania wyników z **Pokaż** polecenie jako dokument JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Jeśli chcesz, Zapisz dane JSON do pliku przy użyciu &gt; znak Przekieruj dane wyjściowe do pliku. Na przykład:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Tagi
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Zarządzanie zasobami
Aby dodać zasobów, takich jak konta magazynu do grupy zasobów, uruchom polecenie podobne do:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Oprócz określanie wersji interfejsu API zasobu z **-o** parametru, użyj **-p** parametr do przekazania w formacie JSON ciąg z każdego wymaganego lub dodatkowych właściwości.

Aby usunąć istniejący zasób usługi takie jak zasobu maszyny wirtualnej, użyj polecenia podobne do poniższych:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć **przenoszenia zasobów platformy azure** polecenia. Poniższy przykład przedstawia sposób przenoszenia pamięci podręcznej Redis do nowej grupy zasobów. W **-i** parametru, podaj jego rozdzielana przecinkami lista identyfikator zasobu można przenieść.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a>Kontrolowanie dostępu do zasobów
Tworzenie zasad i zarządzania nimi na kontrolowanie dostępu do zasobów platformy Azure, można użyć wiersza polecenia platformy Azure. Aby uzyskać ogólne informacje o definicji zasad oraz przypisywania zasad do zasobów, zobacz [za pomocą zasad zarządzania zasobami i kontrola dostępu](resource-manager-policy.md).

Na przykład zdefiniować następujące zasady odrzucanie wszystkich żądań, w którym lokalizacja nie jest zachodnie stany USA lub północno-środkowe Stany i zapisać go w policy.json pliku definicji zasad:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

Następnie uruchom **utworzenia definicji zasad** polecenia:

    azure policy definition create MyPolicy -p c:\temp\policy.json

To polecenie przedstawia dane wyjściowe podobne do następujących:

    + Utworzenie definicji zasad danych MyPolicy: PolicyName: dane MyPolicy: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    dane: PolicyType: danych niestandardowych: Nazwa wyświetlana: niezdefiniowana danych: Opis: niezdefiniowana danych: klasa PolicyRule: pole = lokalizacji, w = [westus, northcentralus], efekt = Odmów

 Aby przypisać zasad w zakresie ma, użyj **PolicyDefinitionId** zwrócone przez poprzednie polecenie. W poniższym przykładzie ten zakres jest subskrypcji, ale można przejść do grupy zasobów lub pojedynczych zasobów:

    MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### utworzenia przypisania zasad Azure /

Można uzyskać, Zmień lub Usuń definicje zasad przy użyciu **Pokaż definicji zasad**, **zestaw definicji zasad**, i **usunąć definicji zasad** poleceń.

Podobnie można uzyskać, zmienianie lub usuwanie przypisania zasady przy użyciu **Pokaż przypisania zasad**, **zestawie przypisania zasad**, i **Usuń przypisanie zasad** poleceń.

## <a name="export-a-resource-group-as-a-template"></a>Eksportowanie grupy zasobów jako szablon
W przypadku istniejącej grupy zasobów można wyświetlać szablonu usługi Resource Manager dla grupy zasobów. Eksportowanie szablonu oferuje dwie korzyści:

1. Można łatwo automatyzować przyszłych wdrożeń rozwiązania, ponieważ cała infrastruktura jest zdefiniowany w szablonie.
2. Należy zaznajomić się ze składnią szablonu analizując JSON, który reprezentuje rozwiązania.

Przy użyciu wiersza polecenia platformy Azure, możesz wyeksportować szablon, który reprezentuje bieżący stan grupy zasobów, lub Pobierz szablon, który był używany dla danego wdrożenia.

* **Eksportowanie szablonu dla grupy zasobów** — jest to przydatne, gdy wprowadziło zmiany w grupie zasobów i musi pobrać reprezentacja JSON w jego bieżącym stanie. Jednak wygenerowanego szablonu zawiera tylko z minimalnej liczby parametrów i żadnych zmiennych. Większość wartości w szablonie są zakodowane na stałe. Przed wdrożeniem wygenerowanego szablonu, możesz przekonwertować więcej wartości parametrów, można dostosować wdrożenia dla różnych środowisk.
  
    Aby wyeksportować szablon dla grupy zasobów w katalogu lokalnym, uruchom `azure group export` polecenia, jak pokazano w poniższym przykładzie. (Zastępuje katalog lokalny odpowiednie dla danego środowiska systemu operacyjnego).
  
        azure group export testRG ~/azure/templates/
* **Pobierz szablon dla konkretnego wdrożenia** — jest to przydatne, gdy chcesz wyświetlić rzeczywiste szablon, który został użyty do wdrożenia zasobów. Szablon zawiera wszystkie parametry i zmienne zdefiniowane dla oryginalnego wdrożenia. Jednak jeśli ktoś w organizacji wprowadzone zmiany w grupie zasobów poza definicją w szablonie, ten szablon nie zawiera bieżący stan grupy zasobów.
  
    Aby pobrać szablon używany do konkretnego wdrożenia do katalogu lokalnego, uruchom `azure group deployment template download` polecenia. Na przykład:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Eksportowanie szablonu jest w wersji zapoznawczej, a nie wszystkich typów zasobów nie obsługiwało eksportowania szablonu. Podczas próby eksportowania szablonu, może zostać wyświetlony błąd informujący, że niektóre zasoby nie zostały wyeksportowane. Jeśli to konieczne, ręcznie zdefiniować te zasoby do szablonu po pobraniu jej.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe informacje o operacji wdrażania i rozwiązywanie problemów z błędy wdrożenia przy użyciu wiersza polecenia platformy Azure, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
* Jeśli chcesz użyć interfejsu wiersza polecenia do konfigurowania aplikacji lub skryptu dostęp do zasobów, zobacz [użyć wiersza polecenia platformy Azure można utworzyć nazwy głównej usługi dostępu do zasobów](resource-group-authenticate-service-principal-cli.md).
* Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).

