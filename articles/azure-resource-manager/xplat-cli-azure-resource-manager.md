---
title: "aaaManage zasobów przy użyciu interfejsu wiersza polecenia Azure hello | Dokumentacja firmy Microsoft"
description: "Użyj hello toomanage Azure interfejsu wiersza polecenia (CLI) Azure zasobów i grup"
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [Interfejs wiersza polecenia platformy Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Interfejs API REST](resource-manager-rest-api.md)
> 
> 

Witaj interfejsu wiersza polecenia platformy Azure (Azure CLI) jest jednym z kilku narzędzi można użyć toodeploy i zarządzanie zasobami za pomocą Menedżera zasobów. W tym artykule przedstawiono typowe sposoby toomanage Azure zasobów i grup zasobów za pomocą interfejsu wiersza polecenia Azure hello w trybie Menedżera zasobów. Uzyskać informacji o używaniu hello CLI toodeploy zasobów, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md). Ogólne dotyczące zasobów platformy Azure i Menedżer zasobów, odwiedź stronę hello [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

> [!NOTE]
> toomanage Azure zasoby z hello wiersza polecenia platformy Azure, należy za[zainstalować hello Azure CLI](../cli-install-nodejs.md), i [Zaloguj tooAzure](../xplat-cli-connect.md) przy użyciu hello `azure login` polecenia. Utwórz hello się, że interfejs wiersza polecenia jest w trybie Menedżera zasobów (Uruchom `azure config mode arm`). Po wykonaniu tych czynności możesz toogo gotowe.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Pobieranie grup zasobów i zasoby
### <a name="resource-groups"></a>Grupy zasobów
tooget listę wszystkich grup zasobów w Twojej subskrypcji i ich lokalizacje, uruchom to polecenie.

    azure group list


### <a name="resources"></a>Zasoby
 nazwy wszystkich zasobów w grupie, takie jak jeden z toolist *testRG*, użyj następującego polecenia hello:

    azure resource list testRG

tooview poszczególnych zasobów w ramach grupy hello, np. maszyna wirtualna o nazwie *MyUbuntuVM*, użyj polecenia takie jak następujące hello:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Powiadomienie hello **Microsoft.Compute/virtualMachines** parametru. Ten parametr wskazuje typ hello hello zasób, którego chcesz uzyskać informacje na.

> [!NOTE]
> Korzystając z hello **zasobów platformy azure** polecenia niż hello **listy** polecenia, należy określić hello interfejsu API w wersji hello zasobu z hello **-o** parametru. Jeśli nie wiesz o wersji interfejsu API hello, zapoznaj się hello pliku szablonu i znajdź pole apiVersion hello hello zasobów. Aby uzyskać więcej informacji o wersji interfejsu API w Menedżerze zasobów, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).
> 
> 

Podczas wyświetlania szczegółowych informacji w zasobie, często jest przydatne toouse hello `--json` parametru. Ten parametr sprawia, że dane wyjściowe hello bardziej czytelny, ponieważ niektóre wartości są zagnieżdżone struktury lub kolekcji. Witaj poniższym przykładzie pokazano zwracająca wyniki hello hello **Pokaż** polecenie jako dokument JSON.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Jeśli chcesz, Zapisz toofile danych JSON hello przy użyciu hello &gt; pliku tooa wyjściowego hello toodirect znaków. Na przykład:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Tagi
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Zarządzanie zasobami
tooadd zasobów, takich jak grupy zasobów tooa konta magazynu, uruchom polecenie podobne do:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Ponadto toospecifying hello wersja interfejsu API hello zasobu z hello **-o** parametru, użyj hello **-p** parametru toopass w formacie JSON ciąg z każdego wymaganego lub dodatkowych właściwości.

toodelete istniejącego zasobu, takie jak zasobu maszyny wirtualnej, należy użyć polecenia takie jak następujące hello:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello **przenoszenia zasobów platformy azure** polecenia. powitania po przykładzie pokazano, jak toomove pamięci podręcznej Redis tooa nową grupę zasobów. W hello **-i** parametru zawierają identyfikator zasobu hello toomove listę rozdzielaną przecinkami.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Kontrola dostępu tooresources
Można użyć hello toocreate wiersza polecenia platformy Azure i zarządzanie zasobami tooAzure dostępu toocontrol zasad. Aby uzyskać ogólne informacje o definicji zasad i przypisywanie tooresources zasad, zobacz [używają zasad toomanage zasobów i kontroli dostępu](resource-manager-policy.md).

Na przykład zdefiniować następujące zasady toodeny hello wszystkie żądania, w którym lokalizacja nie jest zachodnie stany USA lub północno-środkowe Stany i zapisać go policy.json pliku definicji zasad toohello:

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

Następnie uruchom hello **utworzenia definicji zasad** polecenia:

    azure policy definition create MyPolicy -p c:\temp\policy.json

To polecenie przedstawia dane wyjściowe podobne toohello poniżej:

    + Utworzenie definicji zasad danych MyPolicy: PolicyName: dane MyPolicy: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    dane: PolicyType: danych niestandardowych: Nazwa wyświetlana: niezdefiniowana danych: Opis: niezdefiniowana danych: klasa PolicyRule: pole = lokalizacji, w = [westus, northcentralus], efekt = Odmów

 tooassign zasad w zakresie hello ma, użyj hello **PolicyDefinitionId** zwrócony z hello poprzednie polecenie. W hello poniższy przykład ten zakres jest hello subskrypcji, ale można określić zakres grupy tooresource lub pojedynczych zasobów:

    MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### utworzenia przypisania zasad Azure /

Można uzyskać, Zmień lub Usuń definicje zasad przy użyciu hello **Pokaż definicji zasad**, **zestaw definicji zasad**, i **usunąć definicji zasad** poleceń.

Podobnie można uzyskać, zmienianie lub usuwanie przypisania zasady przy użyciu hello **Pokaż przypisania zasad**, **zestawie przypisania zasad**, i **Usuń przypisanie zasad** poleceń .

## <a name="export-a-resource-group-as-a-template"></a>Eksportowanie grupy zasobów jako szablon
W przypadku istniejącej grupy zasobów można wyświetlać hello szablonu usługi Resource Manager dla grupy zasobów hello. Eksportowanie szablonu hello oferuje dwie korzyści:

1. Można łatwo automatyzować przyszłych wdrożeń hello rozwiązania, ponieważ wszystkie infrastruktury hello jest zdefiniowany w szablonie hello.
2. Należy zaznajomić o składni szablonu analizując hello JSON, który reprezentuje rozwiązania.

Przy użyciu hello wiersza polecenia platformy Azure, możesz wyeksportować szablon, który reprezentuje hello bieżący stan grupy zasobów, lub Pobierz szablon hello, które było używane dla konkretnego wdrożenia.

* **Eksportowanie szablonu powitania dla grupy zasobów** — jest to przydatne, gdy wprowadzone grupy zasobów tooa zmiany i konieczne tooretrieve hello reprezentacja JSON swojego bieżącego stanu. Jednak hello wygenerowanego szablonu zawiera tylko z minimalnej liczby parametrów i żadnych zmiennych. Większość wartości hello w szablonie hello są zakodowane na stałe. Przed wdrożeniem hello wygenerowany szablonu, warto zapoznać się z tooconvert więcej wartości hello do parametrów, można dostosować hello wdrożenia dla różnych środowisk.
  
    tooexport hello szablonu dla zasobu grupy tooa katalogiem lokalnym, uruchom hello `azure group export` polecenia, jak pokazano w hello poniższy przykład. (Zastępuje katalog lokalny odpowiednie dla danego środowiska systemu operacyjnego).
  
        azure group export testRG ~/azure/templates/
* **Pobierz szablon powitania dla konkretnego wdrożenia** — jest to przydatne, gdy będziesz potrzebować tooview hello rzeczywiste szablon, który został toodeploy używane zasoby. Szablon Hello zawiera wszystkie parametry i zmienne zdefiniowane dla hello oryginalnego wdrożenia. Jednak jeśli ktoś w organizacji grupę zasobów toohello zmiany poza definicji hello w szablonie hello, ten szablon nie zawiera bieżący stan hello hello grupy zasobów.
  
    toodownload hello szablon używany do konkretnego wdrożenia tooa katalogiem lokalnym, uruchom hello `azure group deployment template download` polecenia. Na przykład:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Eksportowanie szablonu jest w wersji zapoznawczej, a nie wszystkich typów zasobów nie obsługiwało eksportowania szablonu. Podczas próby tooexport szablonu, może zostać wyświetlony błąd informujący, że niektóre zasoby nie zostały wyeksportowane. Jeśli to konieczne, ręcznie zdefiniować te zasoby do szablonu po pobraniu jej.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Szczegóły tooget operacje wdrażania i rozwiązywania problemów wdrożenia z hello wiersza polecenia platformy Azure, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
* Toouse hello CLI tooset aplikacji lub skryptu tooaccess zasobów, zobacz [toocreate wiersza polecenia platformy Azure Użyj nazwy głównej usługi zasobów tooaccess](resource-group-authenticate-service-principal-cli.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

