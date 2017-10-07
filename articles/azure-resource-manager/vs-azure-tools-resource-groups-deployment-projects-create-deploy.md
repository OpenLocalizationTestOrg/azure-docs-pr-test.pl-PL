---
title: "projekty grupy zasobów Studio Azure aaaVisual | Dokumentacja firmy Microsoft"
description: "Użyj programu Visual Studio toocreate projektu grupy zasobów platformy Azure i wdrażanie hello tooAzure zasobów."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio
Z programu Visual Studio i hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/), można utworzyć projekt, który wdraża tooAzure Twojego infrastruktury i kodu. Na przykład można zdefiniować hello hosta sieci web, witryny sieci web i bazy danych dla aplikacji i wdrożyć tę infrastrukturę wraz z hello kodu. Można również zdefiniować maszynę wirtualną, usługę Virtual Network i konto usługi Storage, a następnie wdrożyć tę infrastrukturę wraz ze skryptem wykonywanym na maszynie wirtualnej. Witaj **grupy zasobów platformy Azure** projektu wdrażania umożliwia możesz toodeploy wszystkie zasoby potrzebne hello w pojedynczej i powtarzalnej operacji. Aby uzyskać więcej informacji dotyczących wdrażania zasobów i zarządzania nimi, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

Projekty grupy zasobów platformy Azure zawierają szablony JSON Menedżera zasobów Azure, definiujące hello zasobów wdrażanych tooAzure. toolearn o elementach hello hello szablonu usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md). Visual Studio umożliwia możesz tooedit tych szablonów i oferuje narzędzia ułatwiające pracę z szablonami.

Ten artykuł dotyczy wdrażania aplikacji sieci Web i bazy danych SQL Database. Jednak hello kroki są prawie hello w tej samej dla każdego typu zasobu. Równie łatwo możesz wdrożyć maszynę wirtualną i powiązane zasoby. Program Visual Studio zapewnia wiele różnych szablonów początkowych do wdrażania typowych scenariuszy.

W tym artykule przedstawiono program Visual Studio 2017. Jeśli używasz programu Visual Studio 2015 Update 2 i zestawu Microsoft Azure SDK dla programu .NET 2.9 lub Visual Studio 2013 z Azure SDK 2.9 środowiska jest w przeważającej mierze hello takie same. Za pomocą wersji hello Azure SDK w wersji 2.6 lub nowszej; Jednak środowiska hello interfejsu użytkownika mogą być inne niż hello interfejsu użytkownika pokazano, w tym artykule. Zdecydowanie zaleca się zainstalowanie najnowszej wersji hello hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/) przed rozpoczęciem powitalne kroki. 

## <a name="create-azure-resource-group-project"></a>Tworzenie projektu grupy zasobów platformy Azure
W tej procedurze omówiono tworzenie projektu grupy zasobów platformy Azure przy użyciu szablonu **Aplikacja sieci Web i baza danych SQL**.

1. W programie Visual Studio wybierz pozycję **Plik**, **Nowy projekt** i wybierz opcję **C#** lub **Visual Basic**. Wybierz pozycję **Chmura**, a następnie wybierz projekt **Grupa zasobów platformy Azure**.
   
    ![Projekt wdrażania w chmurze](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Wybierz szablon hello, które mają tooAzure toodeploy Menedżera zasobów. Powiadomienia, istnieje wiele różnych opcji oparte na powitania typ projektu chcesz toodeploy. W tym artykule, wybierz hello **aplikacja sieci Web i SQL** szablonu.
   
    ![Wybieranie szablonu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    Szablon Hello jest tylko punktem wyjściowym; Możesz dodawać i usuwać zasoby toofulfill Twojego scenariusza.
   
   > [!NOTE]
   > Program Visual Studio pobiera listę dostępnych szablonów w trybie online. Lista Hello mogą ulec zmianie.
   > 
   > 
   
    Program Visual Studio tworzy projekt wdrożenia grupy zasobów dla aplikacji sieci web hello i bazy danych SQL.
3. toosee utworzoną, poszukać w węźle hello hello projektu wdrożenia.
   
    ![Wyświetlanie węzłów](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Ponieważ Wybraliśmy hello aplikacja sieci Web i szablon SQL, w tym przykładzie widać hello następujące pliki: 
   
   | Nazwa pliku | Opis |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Skrypt programu PowerShell, który wywołuje tooAzure toodeploy poleceń programu PowerShell Menedżera zasobów.<br />**Uwaga** Visual Studio korzysta z tego toodeploy skrypt programu PowerShell szablonu. Wszystkie wprowadzone zmiany skryptu toothis wpływ na wdrożenie w Visual Studio, więc należy uważać. |
   | WebSiteSQLDatabase.json |Witaj szablonu usługi Resource Manager określający infrastrukturę hello, którą chcesz wdrożyć tooAzure i hello parametrów, które można podać podczas wdrażania. Definiuje również hello zależności między zasobami hello w celu Resource Manager wdraża hello zasobów w odpowiedniej kolejności hello. |
   | WebSiteSQLDatabase.parameters.json |Plik parametrów zawierający wartości wymagane przez szablon hello. Należy przekazać parametr wartości toocustomize każdego wdrożenia. |
   
    Wszystkie projekty wdrażania grup zasobów zawierają te podstawowe pliki. Inne projekty mogą zawierać dodatkowe pliki toosupport innych funkcji.

## <a name="customize-hello-resource-manager-template"></a>Dostosowywanie szablonu usługi Resource Manager hello
Aby dostosować projekt wdrożenia, modyfikując szablony JSON hello opisujące hello zasoby, które chcesz toodeploy. JSON to JavaScript Object Notation i jest formatem serializowanych danych, który jest łatwo toowork z. Witaj pliki JSON używają schematu, której odwołuje się u góry hello każdego pliku. Jeśli chcesz toounderstand hello schematu, można pobrać i przeanalizuj go. Witaj schemat określa, jakie elementy są prawidłowe, hello typy i formaty pól, hello możliwe wartości wartości wyliczane itd. toolearn o elementach hello hello szablonu usługi Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).

Otwórz toowork w szablonie, **WebSiteSQLDatabase.json**.

Witaj Visual Studio zawiera Edytor narzędzi tooassist hello o edycji szablonu usługi Resource Manager. Witaj **konspekt pliku JSON** okna umożliwia łatwe toosee hello elementów zdefiniowanych w szablonie.

![wyświetlanie konspektu pliku JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Zaznaczanie elementów hello w konspekcie hello przejście toothat częścią szablonu hello i zaznacza hello odpowiadającego JSON.

![przechodzenie do elementów JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

Można dodać zasobu albo wybór hello **dodawania zasobów** przycisk u góry hello hello okna konspekt pliku JSON lub klikając prawym przyciskiem myszy **zasobów** i wybierając **Dodaj nowy zasób**.

![dodawanie zasobu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

W ramach tego samouczka wybierz pozycję **Konto usługi Storage** i nadaj mu nazwę. Podaj nazwę nie dłuższą niż 11 znaków, zawierającą tylko cyfry i małe litery.

![dodawanie magazynu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Zwróć uwagę, że nie tylko został dodany hello zasobów, ale również parametr hello typu konta magazynu oraz zmienna nazwy hello hello konta magazynu.

![wyświetlanie konspektu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Witaj **storageType** parametr jest wstępnie zdefiniowany wraz z dozwolonymi typami i typem domyślnym. Możesz pozostawić te wartości bez zmian lub edytować je dla danego scenariusza. Jeśli nie chcesz, aby każdy toodeploy **Premium_LRS** konto magazynu przy użyciu tego szablonu, usuń go z hello dozwolone typy. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

Program Visual Studio oferuje również toohelp intellisense zrozumieć właściwości, które są dostępne podczas edytowania szablonu hello. Na przykład tooedit hello właściwości dla planu usługi aplikacji przejdź toohello **HostingPlan** zasobu i Dodaj wartości hello **właściwości**. Należy zauważyć, że narzędzie intellisense zawiera hello dostępne wartości oraz opis tej wartości.

![wyświetlanie funkcji intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

Można ustawić **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Wdrażanie tooAzure projektu grupy zasobów hello
Użytkownik jest teraz gotowy toodeploy projektu. Podczas wdrażania projektu grupy zasobów platformy Azure, możesz go wdrożyć tooan grupy zasobów platformy Azure. Grupa zasobów Hello to logiczne grupowanie zasobów, które współużytkują wspólne cyklu życia.

1. W menu skrótów węzła projektu wdrażania hello hello, wybierz **Wdróż** > **nowy**.
   
    ![Element menu Wdróż, Nowe wdrażanie](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Witaj **wdrażanie tooResource grupy** zostanie wyświetlone okno dialogowe.
   
    ![Wdrażanie tooResource okno dialogowe grupy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. W hello **grupy zasobów** pole listy rozwijanej wybierz istniejącą grupę zasobów lub Utwórz nową. toocreate grupę zasobów, otwórz hello **grupy zasobów** listy rozwijanej pola i wybierz polecenie **Utwórz nowy**.
   
    ![Wdrażanie tooResource okno dialogowe grupy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Witaj **Tworzenie grupy zasobów** zostanie wyświetlone okno dialogowe. Nadaj grupie nazwy i lokalizacji, a następnie wybierz hello **Utwórz** przycisku.
   
    ![Okno dialogowe Tworzenie grupy zasobów](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Edytuj parametry hello hello wdrożenia, wybierając hello **Edytuj parametry** przycisku.
   
    ![Przycisk Edytuj parametry](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Podaj wartości parametrów pusty hello i wybierz hello **zapisać** przycisku. puste parametry Hello są **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, i **databaseName**.
   
    **hostingPlanName** Określa nazwę hello [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **administratorLogin** Określa nazwę użytkownika, powitalne hello administratora serwera SQL. Nie należy używać wspólnych nazw administratorów, takich jak **sa** lub **admin**. 
   
    Witaj **administratorLoginPassword** Określa hasło administratora serwera SQL. Witaj **zapisywanie haseł w postaci zwykłego tekstu w pliku parametrów hello** opcja nie jest bezpieczne; w związku z tym nie należy zaznaczać tej opcji. Ponieważ hello hasła nie jest zapisywany w postaci zwykłego tekstu, należy tooprovide to hasło ponownie podczas wdrażania. 
   
    **databaseName** Określa nazwę hello toocreate bazy danych. 
   
    ![Okno dialogowe Edytowanie parametrów](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Wybierz hello **Wdróż** tooAzure projektu hello toodeploy przycisku. Otwiera konsolę programu PowerShell poza hello wystąpienie programu Visual Studio. Wprowadź hasło administratora programu SQL Server hello w konsoli programu PowerShell powitania po wyświetleniu monitu. **Konsola programu PowerShell może być ukryty za innych elementów lub zminimalizowana na pasku zadań hello.** Wyszukaj tę konsolę, a następnie zaznacz tooprovide hello hasła.
   
   > [!NOTE]
   > Visual Studio może poprosić hello tooinstall poleceń cmdlet programu Azure PowerShell. Należy hello Azure PowerShell polecenia cmdlet toosuccessfully wdrażanie grup zasobów. Jeśli zostanie wyświetlony monit, zainstaluj je.
   > 
   > 
6. Wdrażanie Hello może potrwać kilka minut. W hello **dane wyjściowe** systemu windows, zostanie wyświetlony stan hello hello wdrożenia. Po zakończeniu wdrażania hello ostatnią wiadomość hello wskazuje pomyślne wdrożenie z polecenie podobne do następującego:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. W przeglądarce otwórz hello [portalu Azure](https://portal.azure.com/) i zaloguj się na koncie tooyour. toosee hello grupy zasobów, wybierz opcję **grup zasobów** i wdrożone do grupy zasobów hello.
   
    ![wybieranie grupy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Zostanie wyświetlony wszystkie zasoby hello wdrożone. Zwróć uwagę, że hello nazwę hello konta magazynu nie jest dokładnie należy określić podczas dodawania tego zasobu. Konto magazynu Hello musi być unikatowa. Witaj szablonu automatycznie dodaje ciąg znaków nazwy toohello podane tooprovide unikatową nazwę. 
   
    ![wyświetlanie zasobów](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Zmiany i konieczne tooredeploy projektu, jeśli hello istniejącej grupy zasobów z menu skrótów hello projektu grupy zasobów platformy Azure. Menu skrótów hello, wybierz **Wdróż**, a następnie wybierz grupę zasobów hello wdrożone.
   
    ![wdrożona grupa zasobów platformy Azure](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Wdrażanie kodu przy użyciu infrastruktury
W tym momencie wdrożono infrastrukturę hello aplikacji, ale nie nie wdrożony z projektem hello rzeczywisty kod. W tym artykule opisano, jak toodeploy aplikacji sieci web i bazy danych SQL tabel podczas wdrażania. Jeśli wdrażasz maszynę wirtualną zamiast aplikacji sieci web ma toorun kodu na komputerze hello jako część wdrożenia. Witaj proces wdrażania kodu dla aplikacji sieci web lub konfigurowania maszyny wirtualnej jest niemal hello takie same.

1. Dodaj tooyour projektu rozwiązania Visual Studio. Kliknij prawym przyciskiem myszy rozwiązanie hello, a następnie wybierz **Dodaj** > **nowy projekt**.
   
    ![dodawanie projektu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Dodaj **aplikację sieci Web ASP.NET**. 
   
    ![dodawanie aplikacji sieci Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Wybierz pozycję **MVC**.
   
    ![wybieranie pozycji MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Gdy program Visual Studio utworzy aplikację sieci web, zobaczysz oba projekty w rozwiązaniu hello.
   
    ![wyświetlanie projektów](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Teraz należy toomake się, że projekt grupy zasobów jest świadome hello nowy projekt. Przejdź wstecz projekt grupy zasobów tooyour (AzureResourceGroup1). Kliknij prawym przyciskiem myszy pozycję **Odwołania** i wybierz polecenie **Dodaj odwołanie**.
   
    ![dodawanie odwołania](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Wybierz hello projektu aplikacji sieci web, który został utworzony.
   
    ![dodawanie odwołania](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Dodanie odwołania, połączyć hello projektu aplikacji sieci web projektu toohello zasobów grupy, a automatyczne ustawienie trzech głównych właściwości. Zobacz te właściwości w hello **właściwości** okna hello odwołania.
   
      ![wyświetlanie odwołania](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    właściwości Hello są:
   
   * Witaj **dodatkowe właściwości** zawiera pakiet wdrożeniowy sieci web hello tymczasowej lokalizacji, do której zostanie przypisany toohello usługi Azure Storage. Uwaga hello folder (ExampleApp) i pliku (pakiet.zip). Należy tooknow te wartości ponieważ podać je jako aplikacji hello parametrów podczas wdrażania. 
   * Witaj **Include File Path** zawiera ścieżkę hello, w której zostaje utworzony pakiet hello. Witaj **Include Targets** zawiera polecenie hello, która wykonuje wdrożenia. 
   * Domyślna wartość Hello **kompilacji; Pakiet** umożliwia hello toobuild wdrożenia i utworzyć pakiet wdrożeniowy sieci web (pakiet.zip).  
     
     Nie trzeba profil publikowania jako hello wdrożenie pobiera niezbędne informacje hello z hello właściwości toocreate hello pakietu.
7. Przejdź wstecz tooWebSiteSQLDatabase.json i dodać szablon toohello zasobów.
   
    ![dodawanie zasobu](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Tym razem wybierz pozycję **Web Deploy dla usługi Web Apps**. 
   
    ![dodawanie narzędzia web deploy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Należy ponownie wdrożyć grupie zasobów toohello projektu grupy zasobów. Tym razem występuje kilka nowych parametrów. Nie trzeba wartości tooprovide **_artifactsLocation** lub **_artifactsLocationSasToken** ponieważ Visual Studio automatycznie generuje tych wartości. Jednak masz tooset hello folderu i ścieżki toohello nazwę pliku, który zawiera pakiet wdrożeniowy hello (wyświetlane jako **ExampleAppPackageFolder** i **ExampleAppPackageFileName** w powitania po obrazu ). Podaj wartości hello widać wcześniej w hello właściwości odwołania (**ExampleApp** i **pakiet.zip**).
   
    ![dodawanie narzędzia web deploy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Dla hello **konta magazynu artefaktu**, wybierz hello jedną wdrożonych w tej grupie zasobów.
10. Po zakończeniu wdrażania hello wybierz aplikację sieci web w portalu hello. Wybierz hello adresu URL toobrowse toohello lokacji.
    
     ![przeglądanie lokacji](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Zwróć uwagę, że zostały pomyślnie wdrożone hello domyślna aplikacja ASP.NET.
    
     ![wyświetlanie wdrożonej aplikacji](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn dotyczące zarządzania zasobami za pośrednictwem portalu hello [Using hello Azure toomanage portalu zasobów platformy Azure](resource-group-portal.md).
* toolearn więcej informacji na temat szablonów, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).

