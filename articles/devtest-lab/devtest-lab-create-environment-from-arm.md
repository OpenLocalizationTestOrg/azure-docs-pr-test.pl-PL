---
title: "aaaCreate środowiskach wielu maszyn wirtualnych i PaaS zasobów przy użyciu szablonów usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate środowisk wielu maszyn wirtualnych i zasoby PaaS w usłudze Azure DevTest Labs z szablonem usługi Azure Resource Manager"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Tworzenie środowisk wielu maszyn wirtualnych i PaaS zasobów przy użyciu szablonów usługi Azure Resource Manager

Witaj [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) pozwala tooeasily [tworzenie i dodawanie maszyny Wirtualnej laboratorium tooa](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). To działa dobrze w przypadku tworzenia jednej maszyny Wirtualnej w czasie. Jednak hello środowisko zawiera wiele maszyn wirtualnych, każda maszyna wirtualna ma toobe indywidualnie utworzony. W przypadku scenariuszy, takich jak wielowarstwową aplikację sieci Web lub farmy programu SharePoint mechanizm jest tooallow wymagane w celu utworzenia hello wiele maszyn wirtualnych w ramach jednego kroku. Przy użyciu szablonów usługi Azure Resource Manager, można definiować hello infrastrukturze i konfiguracji rozwiązania Azure i wielokrotnie wdrażać wiele maszyn wirtualnych w spójnym stanie. Ta funkcja zapewnia hello następujące korzyści:

- Szablony usługi Azure Resource Manager są ładowane bezpośrednio z Twoim repozytorium kontroli źródła (GitHub lub zespołu usługi Git).
- Po skonfigurowaniu użytkowników można utworzyć środowisko, wybierając szablon usługi Azure Resource Manager z portalu Azure jako współpracujemy z innych typów hello [maszyny Wirtualnej podstawy](./devtest-lab-comparing-vm-base-image-types.md).
- Zasoby platformy Azure PaaS można udostępnić w środowisku z szablonem usługi Azure Resource Manager w tooIaaS dodawania maszyn wirtualnych.
- Koszt Hello środowisk można śledzić w laboratorium hello w tooindividual dodawania maszyn wirtualnych utworzonych przez inne typy zasad.
- PaaS zasoby są tworzone i będą widoczne w koszt śledzenia; jednak maszyna wirtualna automatycznego zamykania nie ma zastosowania tooPaaS zasobów.
- Użytkownicy mają hello tej samej maszyny Wirtualnej kontroli zasad dla środowisk mają dla maszyn wirtualnych z jednego laboratorium.

Dowiedz się więcej o hello wiele [zalet przy użyciu szablonów usługi Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, zaktualizować lub usunąć wszystkie zasoby laboratorium w ramach jednej operacji.

> [!NOTE]
> Gdy używasz szablonu usługi Resource Manager jako toocreate podstawy laboratorium więcej maszyn wirtualnych, istnieją tookeep niektóre różnice pod uwagę w przypadku tworzenia maszyn wirtualnych na wielu lub maszyn wirtualnych na jednym. Użyj maszyny wirtualnej tych różnic bardziej szczegółowo opisano szablonu usługi Azure Resource Manager.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Skonfiguruj repozytoria szablonu usługi Azure Resource Manager

Wśród hello najlepsze rozwiązania z infrastruktury jako kod i konfiguracja jako kod, środowisko szablony mają być zarządzane w kontroli źródła. Azure DevTest Labs następuje takie rozwiązanie i ładuje wszystkie szablony usługi Azure Resource Manager bezpośrednio z repozytoriami GitHub lub VSTS Git. W związku z tym Menedżer zasobów szablony mogą być używane w cyklu całej wersji hello, od środowiska produkcyjnego toohello dla hello testu.

Istnieje kilka reguł toofollow tooorganize szablonów usługi Azure Resource Manager w repozytorium:

- Plik szablonu Hello musi mieć nazwę `azuredeploy.json`. 

    ![Pliki szablonów klucza usługi Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Jeśli chcesz toouse wartości parametrów zdefiniowane w pliku parametrów musi mieć nazwę pliku parametrów hello `azuredeploy.parameters.json`.
- Można używać parametrów hello `_artifactsLocation` i `_artifactsLocationSasToken` tooconstruct hello parametersLink URI wartości, umożliwiając DevTest Labs tooautomatically Zarządzanie zagnieżdżone szablony. Zobacz [jak Azure DevTest Labs ułatwia zagnieżdżonych Menedżera zasobów szablonu wdrożenia dla środowisk testowych](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) Aby uzyskać więcej informacji.
- Metadane może być zdefiniowany toospecify hello wyświetlaną nazwę i opis szablonu. Te metadane musi znajdować się w pliku o nazwie `metadata.json`. Witaj następujący przykładowy plik metadanych ilustruje sposób wyświetlania toospecify hello, nazwę i opis: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Hello następujące kroki prowadzące przez dodawanie laboratorium tooyour repozytorium przy użyciu hello portalu Azure. 

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
1. Z listy hello labs wybierz żądany laboratorium hello.   
1. W bloku hello laboratorium, wybierz **konfiguracji i zasadach**.

    ![Konfiguracja i zasady](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. Z hello **konfiguracji i zasadach** ustawienia z listy wybierz **repozytoria**. Witaj **repozytoria** bloku listy repozytoriów hello, które zostały dodane toohello laboratorium. Repozytorium o nazwie `Public Repo` jest generowane automatycznie dla wszystkich laboratoriów i łączy toohello [repozytorium DevTest Labs GitHub](https://github.com/Azure/azure-devtestlab) zawierający kilku artefaktów maszyny Wirtualnej do użycia.

    ![Publicznego repozytorium](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Wybierz **Dodaj +** tooadd repozytorium szablonu usługi Azure Resource Manager.
1. Gdy hello drugi **repozytoria** zostanie otwarty blok, wprowadź niezbędne informacje hello w następujący sposób:
    - **Nazwa** — wprowadź nazwę repozytorium hello jest używany w laboratorium hello.
    - **Adres URL klonowania Git** — wprowadź adres URL klonowania GIT HTTPS hello z usługi GitHub lub Visual Studio Team Services.  
    - **Gałąź** — wprowadź tooaccess Nazwa gałęzi hello definicji szablonu usługi Azure Resource Manager. 
    - **Osobisty token dostępu** -hello osobisty token dostępu jest używana toosecurely dostępu do repozytorium. Wybierz token z Visual Studio Team Services tooget  **&lt;twoja_nazwa >> Mój profil > Zabezpieczenia > token dostępu publicznego**. tooget Twojego tokenu z serwisu GitHub, wybierz Awatar, a następnie wybierając **Ustawienia > token dostępu publicznego**. 
    - **Ścieżka folderu** — przy użyciu jednej z hello dwa pola wejściowe, wprowadź ścieżkę folderu hello, która rozpoczyna się od ukośnika - i - i jest względna tooyour Git Klonuj URI tooeither definicji artefaktów (pierwsze pole wejściowe) lub szablonem usługi Azure Resource Manager definicje.   
    
        ![Publicznego repozytorium](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Gdy wszystkie pola wymagane hello są wprowadzane i przeszedł pomyślnie weryfikacji hello, wybierz **zapisać**.

Hello Następna sekcja przeprowadzi Cię przez proces tworzenia środowisk z szablonem usługi Azure Resource Manager.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Utwórz środowisko na podstawie szablonu usługi Azure Resource Manager

Repozytorium szablonu usługi Azure Resource Manager został skonfigurowany w laboratorium hello, użytkownicy laboratorium tworzyć środowiska przy użyciu portalu Azure z hello następujące kroki:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
1. Z listy hello labs wybierz żądany laboratorium hello.   
1. W bloku hello laboratorium, wybierz **Dodaj +**.
1. Witaj **wybierz podstawowej** bloku Wyświetla hello obrazy podstawowej korzystania z szablonów usługi Azure Resource Manager hello wyświetlana na początku listy. Wybierz hello żądanego szablonu usługi Azure Resource Manager.

    ![Wybierz podstawowej](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. Na powitania **Dodaj** bloku, wprowadź hello **Nazwa środowiska** wartość. Nazwa środowiska Hello to tooyour wyświetlane użytkownikom w laboratorium hello. pozostałe pola wejściowego Hello są definiowane w szablonie usługi Azure Resource Manager hello. Jeśli wartości domyślne są definiowane w szablonie hello lub hello `azuredeploy.parameter.json` plik jest obecny, wartości domyślne są wyświetlane w tych pól wejściowych. Dla parametrów typu *bezpieczny ciąg*, można użyć kluczy tajnych hello przechowywane w laboratorium hello [magazynie osobistym tajny](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Dodawanie bloku](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Istnieje kilka wartości parametrów, które — nawet wtedy, gdy określono — są wyświetlane jako wartości puste. W związku z tym jeśli użytkownicy przypisać tooparameters tych wartości w szablonie usługi Azure Resource Manager, DevTest Labs nie będą wyświetlane wartości hello; Zamiast tego są wyświetlane puste pola wejściowe, których użytkownicy laboratorium hello muszą tooenter wartości podczas tworzenia środowiska hello.
    > 
    > - GEN UNIKATOWY
    > - GEN - UNIKATOWY — [N]
    > - GEN--PUB-KLUCZA SSH
    > - GEN HASŁA 
 
1. Wybierz **Dodaj** toocreate hello środowiska. środowisko Hello rozpoczyna się natychmiast inicjowania obsługi ze stanem hello wyświetlanie w hello **Moje maszyny wirtualne** listy. Nowa grupa zasobów jest tworzone automatycznie przez tooprovision laboratorium hello wszystkie zasoby hello zdefiniowane w szablonie usługi Azure Resource Manager hello.
1. Po utworzeniu hello środowiska, wybierz środowisko hello w hello **Moje maszyny wirtualne** listę bloku grupy zasobów hello tooopen i Przeglądaj wszystkie zasoby hello udostępniane w środowisku hello.
    
    ![Lista maszyn wirtualnych](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   Można również rozwinąć hello środowiska tooview hello tylko listę maszyn wirtualnych, które są udostępniane w środowisku hello.
    
    ![Lista maszyn wirtualnych](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Kliknij dowolny hello środowisk tooview hello dostępne akcje — takie jak stosowanie artefakty dołączanie dysków z danymi, zmiana czasu automatycznego zamykania i inne.

    ![Akcje środowiska](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Następne kroki
* Po utworzeniu maszyny Wirtualnej, możesz połączyć toohello maszyny Wirtualnej, wybierając **Connect** w bloku hello maszyny Wirtualnej.
* Wyświetlanie i zarządzanie zasobami w środowisku, wybierając środowisko hello hello **Moje maszyny wirtualne** listy w laboratorium. 
* Eksploruj hello [szablonów usługi Azure Resource Manager z galerii szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates)
