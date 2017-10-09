---
title: "Integracja aaaContinuous w VS Team Services za pomocą projekty grupy zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak projekty tooset się ciągłej integracji w programie Visual Studio Team Services za pomocą wdrożenia grupy zasobów platformy Azure w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Ciągła integracja w programie Visual Studio Team Services za pomocą projekty wdrażania grup zasobów platformy Azure
toodeploy szablonu platformy Azure, możesz wykonać zadania w różnych etapach: tworzenie testu, tooAzure kopiowania (zwane również "Tymczasowości") i wdrażania szablonu. Istnieją dwa sposoby toodeploy szablony tooVisual Studio Team Services (VS Team Services). Obie metody Podaj hello takie same wyniki, dlatego wybierz hello jedną, która najlepiej pasuje do przepływu pracy.

1. Dodaj definicję kompilacji tooyour jednego kroku, która uruchamia skrypt programu PowerShell hello, który znajduje się w projekcie wdrożenia grupy zasobów platformy Azure hello (wdrażanie AzureResourceGroup.ps1). skrypt Hello kopiuje artefaktów, a następnie wdraża hello szablonu.
2. Dodaj wiele VS Team Services kroki procesu kompilacji, każda z nich zrealizowane etapu.

W tym artykule przedstawiono obie opcje. Pierwsza opcja Hello ma korzystać hello przy użyciu hello używany ten sam skrypt przez deweloperów w programie Visual Studio i zapewnienia spójności w całym cyklu życia hello. Druga opcja Hello oferuje skrypt wbudowany wygodne toohello alternatywnych. Obu procedurach założono, że masz już Projekt wdrożenia programu Visual Studio w wersji programu VS Team Services.

## <a name="copy-artifacts-tooazure"></a>Kopiowanie artefaktów tooAzure
Niezależnie od scenariusza hello Jeśli masz wszelkie artefakty, które są wymagane do wdrożenia szablonu musi nadać toothem dostępu do usługi Azure Resource Manager. Tych artefaktów może zawierać pliki takie jak:

* Zagnieżdżone szablony
* Konfiguracja i skryptów DSC
* Pliki binarne aplikacji

### <a name="nested-templates-and-configuration-scripts"></a>Zagnieżdżone szablony i skrypty do konfiguracji
Jeśli używasz szablony hello zapewniane przez program Visual Studio (lub skompilowanej za pomocą wstawki kodu programu Visual Studio) hello skrypt programu PowerShell nie tylko przygotuje artefakty hello, również parameterizes hello URI hello zasobów dla różnych wdrożeń. skrypt Hello, a następnie kopiuje hello artefakty tooa bezpiecznego kontenera na platformie Azure, tworzy token SaS dla kontenera i następnie przekazuje informację na toohello szablonu wdrożenia. Zobacz [Utwórz wdrożenie szablonu](https://msdn.microsoft.com/library/azure/dn790564.aspx) zagnieżdżonych toolearn więcej informacji o szablonach.  Przy użyciu zadań w programie VS Team Services, musisz wybrać hello odpowiednich zadań do wdrożenia szablonu i w razie potrzeby należy podać wartości parametrów z hello przemieszczania krok toohello szablonu wdrożenia.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Konfigurowanie ciągłego wdrażania w programie VS Team Services
toocall hello skrypt programu PowerShell w wersji programu VS Team Services, potrzebne tooupdate definicję kompilacji. Krótko mówiąc kroki hello są: 

1. Edytuj hello definicji kompilacji.
2. Konfigurowanie autoryzacji Azure w wersji programu VS Team Services.
3. Dodawanie kroku kompilacji programu Azure PowerShell, który odwołuje się do skryptu programu PowerShell hello w projekcie wdrożenia grupy zasobów platformy Azure hello.
4. Ustaw wartość hello hello *- ArtifactsStagingDirectory* toowork parametru z projektem wbudowane VS Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Szczegółowy przewodnik dotyczący opcję 1
Witaj poniższych procedur umożliwia przeprowadzenie hello kroki niezbędne tooconfigure ciągłe wdrażanie w VS Team Services za pomocą jednego zadania, które uruchamia skrypt programu PowerShell hello w projekcie. 

1. Edytowanie definicji kompilacji programu VS Team Services i dodać kroku kompilacji programu Azure PowerShell. Wybierz hello definicję kompilacji w obszarze hello **definicje kompilacji** kategorii, a następnie wybierz hello **Edytuj** łącza.
   
   ![Edytowanie definicji kompilacji][0]
2. Dodaj nową **programu Azure PowerShell** definicji kompilacji toohello kroku kompilacji, a następnie wybierz pozycję hello **Dodaj krok kompilacji...** Dodaj...
   
   ![Dodawanie kroku kompilacji][1]
3. Wybierz hello **zadań Wdróż** kategorii, wybierz hello **programu Azure PowerShell** zadań, a następnie wybierz pozycję jego **Dodaj** przycisku.
   
   ![Dodawanie zadań][2]
4. Wybierz hello **programu Azure PowerShell** kroku kompilacji, a następnie wypełnij jego wartości.
   
   1. Jeśli masz już punkt końcowy usługi Azure dodane tooVS Team Services, wybierz subskrypcję hello w hello **subskrypcji Azure** pole listy rozwijanej, a następnie pomiń toohello następnej sekcji. 
      
      Jeśli nie masz punkt końcowy usługi Azure w wersji programu VS Team Services, należy tooadd jeden. W tej podsekcji przeprowadza użytkownika przez proces hello. Jeśli konto Azure korzysta z konta Microsoft (na przykład usługi Hotmail), należy wykonać następujące kroki tooget hello uwierzytelnianie nazwy głównej usługi.
   2. Wybierz hello **Zarządzaj** link dalej toohello **subskrypcji Azure** pole listy rozwijanej.
      
      ![Zarządzać subskrypcjami platformy Azure][3]
   3. Wybierz **Azure** w hello **nowy punkt końcowy usługi** pole listy rozwijanej.
      
      ![Nowy punkt końcowy usługi][4]
   4. W hello **dodawania subskrypcji platformy Azure** okno dialogowe, wybierz opcję hello **nazwy głównej usługi** opcji.
      
      ![Opcja głównej usługi][5]
   5. Dodaj toohello informacje o Twojej subskrypcji platformy Azure **dodawania subskrypcji platformy Azure** okno dialogowe. Należy hello tooprovide następujące elementy:
      
      * Identyfikator subskrypcji
      * Nazwa subskrypcji
      * Identyfikator nazwy głównej usługi
      * Klucz nazwy głównej usługi
      * Identyfikator dzierżawy
   6. Dodaj nazwę użytkownika toohello wybór **subskrypcji** pole Nazwa. Ta wartość jest wyświetlana w dalszej części hello **subskrypcji Azure** listy rozwijanej w VS Team Services. 
   7. Jeśli nie znasz identyfikator subskrypcji platformy Azure, można użyć jednej z następującego polecenia tooretrieve hello go.
      
      Dla skryptów programu PowerShell użyj polecenia:
      
      `Get-AzureRmSubscription`
      
      W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:
      
      `azure account show`
   8. tooget Identyfikatora nazwy głównej usługi klucz nazwy głównej usługi i identyfikator dzierżawy, wykonaj procedurę hello w [aplikacji usługi Active Directory Utwórz i nazwę główną usługi za pomocą portalu](resource-group-create-service-principal-portal.md) lub [uwierzytelniania z nazwy głównej usługi Usługa Azure Resource Manager](resource-group-authenticate-service-principal.md).
   9. Dodaj hello toohello wartości Identyfikatora nazwy głównej usługi, klucz nazwy głównej usługi i identyfikator dzierżawcy **dodawania subskrypcji platformy Azure** okna dialogowego polu, a następnie wybierz pozycję hello **OK** przycisku.
      
      Masz teraz hello toorun prawidłowe nazwy głównej usługi toouse skrypt programu PowerShell systemu Azure.
5. Edytowanie definicji kompilacji hello i wybierz polecenie hello **programu Azure PowerShell** kroku kompilacji. Wybierz subskrypcję hello w hello **subskrypcji Azure** pole listy rozwijanej. (Hello subskrypcji nie jest wyświetlana, jeśli hello **Odśwież** przycisku Dalej hello **Zarządzaj** łącza.) 
   
   ![Skonfiguruj zadania kompilacji programu Azure PowerShell][8]
6. Podaj toohello ścieżka skryptu PowerShell AzureResourceGroup.ps1 wdrażania. toodo, wybierz toohello dalej przycisk wielokropka (...) hello **ścieżka skryptu** wybierz skrypt programu PowerShell Wdróż AzureResourceGroup.ps1 toohello w hello **skryptów** folderu projektu, zaznacz go, a następnie wybierz hello **OK** przycisku.    
   
   ![Wybierz ścieżkę tooscript][9]
7. Po wybraniu skryptu hello hello ścieżki toohello skrypt aktualizacji, dzięki czemu jest uruchamiany z hello Build.StagingDirectory (hello na tym samym katalogu który *ArtifactsLocation* ma ustawioną wartość). Można to zrobić przez dodanie "$(Build.StagingDirectory)/" toohello początku hello ścieżka skryptu.
   
    ![Edytuj tooscript ścieżki][10]
8. W hello **argumenty skryptu** wprowadź hello następujące parametry (w jednym wierszu). Po uruchomieniu skryptu hello w programie Visual Studio widać, jak używa VS hello parametrów w hello **dane wyjściowe** okna. Służy to jako punktu wyjścia do ustawiania wartości parametrów hello w Twojej kroku kompilacji.
   
   | Parametr | Opis |
   | --- | --- |
   | -ResourceGroupLocation |Witaj wartość lokalizacji geograficznej, gdzie hello zasobów znajduje się grupa, takich jak **eastus** lub **wschodnie stany USA**. (Dodaj apostrofy, jeśli jest spacja w nazwie hello). Zobacz [regiony platformy Azure](https://azure.microsoft.com/en-us/regions/) Aby uzyskać więcej informacji. |
   | -ResourceGroupName |Hello Nazwa grupy zasobów hello użyty dla tego wdrożenia. |
   | -UploadArtifacts |Tego parametru, jeśli jest obecny, określa, że artefakty wymagające toobe przekazana tooAzure z hello systemu lokalnego. Wystarczy tooset tego przełącznika Jeśli artefakty dodatkowe, które mają toostage za pomocą skryptu PowerShell hello (na przykład skrypty do konfiguracji lub zagnieżdżone szablony) wymaga wdrożenia szablonu. |
   | -StorageAccountName |Hello nazwa konta magazynu hello używana toostage artefaktów dla tego wdrożenia. Ten parametr jest używany tylko, jeśli są przemieszczania artefakty do wdrożenia. Jeśli ten parametr zostanie podany, nowe konto magazynu jest tworzony, jeśli skrypt hello nie został utworzony podczas poprzedniego wdrożenia. Jeśli określono parametr hello, konta magazynu hello musi już istnieć. |
   | -StorageAccountResourceGroupName |Hello Nazwa grupy zasobów hello skojarzone z kontem magazynu hello. Ten parametr jest wymagany tylko wtedy, gdy Podaj wartość dla parametru StorageAccountName hello. |
   | -TemplateFile |Witaj ścieżki toohello szablonu pliku w projekcie wdrożenia grupy zasobów platformy Azure hello. elastyczność tooenhance, użyj ścieżki dla tego parametru, który jest względny toohello lokalizacja hello skrypt programu PowerShell, a nie ścieżką bezwzględną. |
   | -TemplateParametersFile |Witaj ścieżki toohello parametry pliku w projekcie wdrożenia grupy zasobów platformy Azure hello. elastyczność tooenhance, użyj ścieżki dla tego parametru, który jest względny toohello lokalizacja hello skrypt programu PowerShell, a nie ścieżką bezwzględną. |
   | -ArtifactStagingDirectory |Ten parametr umożliwia skrypt programu PowerShell hello znany hello folder, z którym powinny zostać skopiowane pliki binarne hello projektu. Ta wartość zastępuje hello wartość domyślna używana przez hello skrypt programu PowerShell. Użyć wersji programu VS Team Services, ustaw wartość hello: $(Build.StagingDirectory) - ArtifactStagingDirectory |
   
   Oto przykładowy skrypt argumentów (podzielone dla czytelności wiersz):
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Po zakończeniu hello **argumenty skryptu** pole powinno przypominać hello następującej listy:
   
   ![Argumenty skryptu][11]
9. Po dodaniu hello wszystkie wymagane elementy toohello kroku kompilacji programu Azure PowerShell, wybierz hello **kolejki** kompilacji projektu hello toobuild przycisku. Witaj **kompilacji** ekranie zostaną wyświetlone dane wyjściowe hello hello skrypt programu PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Szczegółowy przewodnik dotyczący opcja 2
Witaj poniższych procedur umożliwia przeprowadzenie hello kroki niezbędne tooconfigure ciągłe wdrażanie w VS Team Services za pomocą wbudowanych zadań hello.

1. Edytowanie programu VS Team Services kompilacji definicji tooadd dwa nowe kroki procesu kompilacji. Wybierz hello definicję kompilacji w obszarze hello **definicje kompilacji** kategorii, a następnie wybierz hello **Edytuj** łącza.
   
   ![Edytowanie definicji kompilacji][12]
2. Dodaj hello nowej definicji kompilacji toohello przy użyciu hello kroki procesu kompilacji **Dodaj krok kompilacji...** Dodaj...
   
   ![Dodawanie kroku kompilacji][13]
3. Wybierz hello **Wdróż** kategorii zadań, wybierz hello **Azure File Copy** zadań, a następnie wybierz pozycję jego **Dodaj** przycisku.
   
   ![Dodaj zadanie kopiowania plików na platformę Azure][14]
4. Wybierz hello **wdrożenie grupy zasobów Azure** zadań, a następnie wybierz jego **Dodaj** przycisk, a następnie **Zamknij** hello **katalogu zadania**.
   
   ![Zadanie wdrażania dodać grupy zasobów platformy Azure][15]
5. Wybierz hello **Azure File Copy** zadań i podać jego wartości.
   
   Jeśli masz już punkt końcowy usługi Azure dodane tooVS Team Services, wybierz subskrypcję hello w hello **subskrypcji Azure** pole listy rozwijanej. Jeśli nie masz subskrypcji, zobacz [opcję 1](#detailed-walkthrough-for-option-1) instrukcje dotyczące konfigurowania co w usłudze VS Team Services.
   
   * Źródło — wprowadź **$(Build.StagingDirectory)**
   * Typ połączenia Azure - wybierz **usługi Azure Resource Manager**
   * Subskrypcja platformy Azure RM - hello Wybierz subskrypcję dla konta magazynu hello ma toouse w hello **subskrypcji Azure** pole listy rozwijanej. Witaj subskrypcji nie jest wyświetlana, jeśli hello **Odśwież** przycisku Dalej hello **Zarządzaj** łącza.
   * Typ docelowy — wybierz **obiektów Blob platformy Azure**
   * Menedżer zasobów konta magazynu — wybierz magazyn hello konto ma chcieliby toouse do przemieszczania artefaktów
   * Nazwa kontenera — wprowadź nazwę hello kontenera hello chcesz toouse dla przemieszczania; go może być dowolną nazwę prawidłowego kontenera, ale użyj jednej definicji kompilacji dedykowanych toothis
   
   Wartości danych wyjściowych hello:
   
   * Wprowadź kontenera magazynu URI - **artifactsLocation**
   * Token sygnatury dostępu Współdzielonego kontenera magazynu — wprowadź **artifactsLocationSasToken**
   
   ![Skonfiguruj zadania kopiowania plików na platformę Azure][16]
6. Wybierz hello **wdrożenie grupy zasobów Azure** kroku kompilacji, a następnie wypełnij jego wartości.
   
   * Typ połączenia Azure - wybierz **usługi Azure Resource Manager**
   * Subskrypcja platformy Azure RM - hello Wybierz subskrypcję do wdrożenia w hello **subskrypcji Azure** pole listy rozwijanej. Zwykle będzie używać tej samej subskrypcji hello w poprzednim kroku hello
   * Akcja — wybierz **tworzenia lub aktualizacji grupy zasobów**
   * Grupa zasobów — wybierz grupę zasobów lub wprowadź nazwę hello nową grupę zasobów dla wdrożenia hello
   * Lokalizacja — wybierz hello lokalizacja grupy zasobów hello
   * Szablon — wprowadź hello ścieżka i nazwa hello szablonu toobe wdrożone dołączanie **$(Build.StagingDirectory)**, na przykład: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Parametry szablonu — wprowadź hello ścieżka i nazwa hello toobe parametry używane, dołączanie **$(Build.StagingDirectory)**, na przykład: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Zastąp parametrów szablonu — wprowadź lub skopiuj i Wklej hello następującego kodu:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Skonfiguruj zadania wdrażania grupy zasobów platformy Azure][17]
7. Po dodaniu wszystkie elementy wymagane hello zapisać definicję kompilacji hello i wybrać **nowej kompilacji w kolejce** u góry hello.

## <a name="next-steps"></a>Następne kroki
Odczyt [Omówienie usługi Azure Resource Manager](azure-resource-manager/resource-group-overview.md) toolearn więcej informacji na temat usługi Azure Resource Manager i grup zasobów platformy Azure.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
