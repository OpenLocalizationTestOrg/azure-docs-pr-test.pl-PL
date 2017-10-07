---
title: "aaaConfigure hello ról platformy Azure w chmurze usługi z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset Konfigurowanie i konfigurowania ról dla usług w chmurze Azure przy użyciu programu Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Skonfigurować role usługi w chmurze Azure z programem Visual Studio
Usługi w chmurze Azure może mieć co najmniej jednego procesu roboczego lub role sieci web. Dla każdej roli należy toodefine sposób konfigurowania tej roli, a także skonfigurować sposób uruchamiania tej roli. toolearn więcej informacji na temat ról w usługach w chmurze, zobacz film hello [tooAzure wprowadzenie usługi w chmurze](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

Witaj informacje dla usługi w chmurze są przechowywane w hello następujące pliki:

- **ServiceDefinition.csdef** -pliku definicji usługi hello definiuje ustawienia środowiska uruchomieniowego hello tym, jakie role są wymagane usługi w chmurze, punktów końcowych i rozmiar maszyny wirtualnej. Brak hello danych przechowywanych w `ServiceDefinition.csdef` można zmieniać w przypadku roli użytkownika jest uruchomiona.
- **Pliku ServiceConfiguration.cscfg** — plik konfiguracji usługi hello konfiguruje liczbę wystąpień roli są uruchamiane i hello wartości ustawień hello zdefiniowane dla roli. Witaj danych przechowywanych w `ServiceConfiguration.cscfg` można zmienić uruchomionej roli użytkownika.

toostore różne wartości dla ustawień hello kontrolujących sposób uruchamiania roli, można zdefiniować wiele konfiguracji usługi. W przypadku używania konfiguracji innej usługi, dla poszczególnych środowisk wdrażania. Na przykład można ustawić Twojego konta połączenia ciąg toouse hello lokalnego magazynu Azure emulatora magazynu w konfiguracji usługi lokalnej i utwórz inny toouse konfiguracji usługi Azure storage w chmurze hello.

Podczas tworzenia usługi w chmurze platformy Azure w programie Visual Studio, dwie konfiguracje usług są tworzone automatycznie i dodane tooyour projektu platformy Azure:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Konfigurowanie usługi w chmurze Azure
Usługi w chmurze Azure z Eksploratora rozwiązań można skonfigurować w programie Visual Studio, pokazane na powitania następujące kroki:

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **właściwości**.
   
    ![Menu kontekstowe projektu Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Na stronie właściwości projektu hello, wybierz hello **programowanie** kartę. 

    ![Strona właściwości projektu — karta programowanie](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. W hello **konfiguracji usługi** listy, wybierz opcję hello nazwę hello konfiguracji usługi, które mają tooedit. (Toomake zmian konfiguracji usługi hello tooall dla tej roli, zaznacz **wszystkie konfiguracje**.)
   
    > [!IMPORTANT]
    > Jeśli wybierzesz opcję konfiguracji określonej usługi, niektóre właściwości są wyłączone, ponieważ ich można ustawić tylko w przypadku wszystkich konfiguracji. tooedit te właściwości, należy wybrać **wszystkie konfiguracje**.
    > 
    > 
   
    ![Lista konfiguracji usługi dla usługi w chmurze Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Zmień hello liczbę wystąpień roli
wydajność hello tooimprove usługi w chmurze, można zmienić hello liczbę wystąpień roli, które działają na podstawie hello liczby użytkowników lub obciążenia hello oczekiwany dla określonej roli. Oddzielnej maszynie wirtualnej jest tworzony dla każdego wystąpienia roli, gdy usługa w chmurze hello działa na platformie Azure. Ma to wpływ na rozliczenia hello hello wdrożenia tej usługi w chmurze. Aby uzyskać więcej informacji dotyczących rozliczeń, zobacz [zrozumieć rachunku platformy Microsoft Azure](billing/billing-understand-your-bill.md).

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello. W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Wybierz hello **konfiguracji** kartę.

    ![Karta Konfiguracja](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. W hello **konfiguracji usługi** listy, wybierz opcję hello konfiguracji usługi, które mają tooupdate.
   
    ![Konfiguracji usługi na liście](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. W hello **wystąpienia licznika** tekst Wprowadź hello liczbę wystąpień mają toostart dla tej roli. Każde wystąpienie działa na oddzielnej maszynie wirtualnej podczas publikowania tooAzure usługi chmury hello.

    ![Aktualizowanie hello liczba wystąpień](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Zarządzanie parametry połączenia dla konta magazynu
Można dodać, usunąć ani zmodyfikować parametrów połączenia dla konfiguracji usługi. Na przykład może być ciąg połączenia lokalnej konfiguracji usługi lokalnej, która ma wartość `UseDevelopmentStorage=true`. Można także tooconfigure konfiguracji usługi chmury, korzystającej z konta magazynu na platformie Azure.

> [!WARNING]
> Po wprowadzeniu hello Azure klucza informacji o koncie magazynu dla parametrów połączenia konta magazynu, te informacje są przechowywane lokalnie w pliku konfiguracji usługi hello. Jednak ta informacje obecnie nie są przechowywane jako tekst zaszyfrowany.
> 
> 

Za pomocą innej wartości dla każdej konfiguracji usługi, nie ma toouse innymi parametrami połączenia w usłudze w chmurze lub zmodyfikuj kodu podczas publikowania z tooAzure usługi chmury. Możesz użyć tej samej nazwy dla hello parametry połączenia w kodzie i hello wartość jest inny, na podstawie konfiguracji usługi hello, wybranej podczas tworzenia usługi w chmurze lub podczas jego publikowania powitalne.

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello. W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Wybierz hello **ustawienia** kartę.

    ![Karta Ustawienia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. W hello **konfiguracji usługi** listy, wybierz opcję hello konfiguracji usługi, które mają tooupdate.

    ![Konfiguracja usługi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Wybierz tooadd ciąg połączenia **Dodaj ustawienie**.

    ![Dodaj ciąg połączenia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Po dodaniu nowego ustawienia hello listy toohello, należy zaktualizować wiersza hello liście hello hello niezbędne informacje.

    ![Nowe parametry połączenia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nazwa** — wprowadź nazwę hello mają toouse hello ciągu połączenia.
    - **Typ** — wybierz tę opcję **ciąg połączenia** z listy rozwijanej hello.
    - **Wartość** — możesz wprowadzić parametry połączenia hello bezpośrednio do hello **wartość** komórki lub hello wybierz wielokropek (...) toowork w hello **utworzyć parametry połączenia magazynu** okna dialogowego.  

1. W hello **utworzyć parametry połączenia magazynu** okno dialogowe, wybierz opcję **łączyć się przy użyciu**. Następnie wykonaj instrukcje hello opcja hello:

    - **Emulator magazynu Microsoft Azure** — Jeśli ta opcja hello pozostałe ustawienia w oknie dialogowym hello są wyłączone, ponieważ mają one zastosowanie tylko tooAzure. Kliknij przycisk **OK**.
    - **Subskrypcja** — w przypadku wybrania tej opcji, użyj hello listy rozwijanej listy tooeither wybierz i zaloguj się do konta Microsoft, lub Dodawanie konta Microsoft. Wybierz konto platformy Azure subskrypcji i magazynu. Kliknij przycisk **OK**.
    - **Ręcznie wprowadzić poświadczenia** — wprowadź nazwę konta magazynu hello i albo hello klucz podstawowy lub drugiego. Wybierz opcję wyznaczenia **połączenia** (HTTPS jest zalecane dla większości scenariuszy). Kliknij przycisk **OK**.

1. toodelete ciąg połączenia wybierz hello parametry połączenia, a następnie wybierz **Usuń ustawienie**.

1. Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.

## <a name="programmatically-access-a-connection-string"></a>Uzyskania programowego dostępu do parametrów połączenia

Witaj poniższej procedurze pokazano, jak tooprogrammatically uzyskują dostęp do ciągu połączenia przy użyciu języka C#.

1. Dodaj następujące hello przy użyciu dyrektywy tooa C# pliku, gdzie będą toouse hello ustawienia:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Witaj poniższy kod przedstawia przykładowy sposób tooaccess ciąg połączenia. Zastąp hello &lt;ConnectionStringName > symbolu zastępczego hello odpowiednią wartość. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Dodatek toouse niestandardowe ustawienia usługi w chmurze Azure
Ustawienia niestandardowe w pliku konfiguracji usługi hello pozwalają Dodaj nazwę i wartość ciągu dla określonej usługi konfiguracji. Możesz wybrać toouse tego tooconfigure ustawienie to funkcja usługi w chmurze, odczytując wartości hello hello ustawienie i przy użyciu tej logiki hello toocontrol wartości w kodzie. Bez konieczności toorebuild pakietu usługi lub usługi w chmurze jest uruchomiona, można zmienić tych wartości konfiguracji usługi. Powiadomienia o kodzie można sprawdzić podczas zmiany ustawień. Zobacz [RoleEnvironment.Changing zdarzeń](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Można dodać, usunąć ani zmodyfikować własne ustawienia konfiguracji usługi. Może być różne wartości dla tych ciągów w przypadku konfiguracji z innej usługi.

Za pomocą innej wartości dla każdej konfiguracji usługi, nie mają różne ciągi toouse w usłudze w chmurze lub zmodyfikuj kodu podczas publikowania z tooAzure usługi chmury. Możesz użyć tej samej nazwy dla ciąg hello w polu wartość kodu i hello jest inny, na podstawie konfiguracji usługi hello, wybranej podczas tworzenia usługi w chmurze lub podczas jego publikowania powitalne.

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello. W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Wybierz hello **ustawienia** kartę.

    ![Karta Ustawienia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. W hello **konfiguracji usługi** listy, wybierz opcję hello konfiguracji usługi, które mają tooupdate.

    ![Konfiguracji usługi na liście](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd niestandardową wartość ustawienia, wybierz **Dodaj ustawienie**.

    ![Dodaj niestandardową wartość ustawienia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Po dodaniu nowego ustawienia hello listy toohello, należy zaktualizować wiersza hello liście hello hello niezbędne informacje.

    ![Nowe ustawienie niestandardowe](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nazwa** — wprowadź nazwę hello hello ustawienia.
    - **Typ** — wybierz tę opcję **ciąg** z listy rozwijanej hello.
    - **Wartość** — wprowadź wartość hello hello ustawienia. Możesz wprowadzić wartość hello bezpośrednio do hello **wartość** komórki lub hello wybierz wielokropek (...) tooenter hello wartości w hello **Edytowanie ciągu** okna dialogowego.  

1. toodelete niestandardową wartość ustawienia, wybierz ustawienie hello, a następnie wybierz **Usuń ustawienie**.

1. Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.

## <a name="programmatically-access-a-custom-settings-value"></a>Uzyskania programowego dostępu do wartości ustawienia niestandardowego
 
Witaj poniższej procedurze pokazano, jak tooprogrammatically dostępu niestandardową wartość ustawienia przy użyciu języka C#.

1. Dodaj następujące hello przy użyciu dyrektywy tooa C# pliku, gdzie będą toouse hello ustawienia:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Witaj poniższy kod przedstawia przykładowy sposób tooaccess ustawienia niestandardowego. Zastąp hello &lt;SettingName > symbolu zastępczego hello odpowiednią wartość. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Zarządzanie magazynem lokalnym dla każdego wystąpienia roli
Możesz dodać magazyn systemu pliku lokalnego dla każdego wystąpienia roli. Hello danych przechowywanych w pamięci masowej nie jest dostępny przez innych wystąpień roli hello, dla których hello są przechowywane dane lub innych ról.  

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello. W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Wybierz hello **Magazyn lokalny** kartę.

    ![Karta magazynu lokalnego](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. W hello **konfiguracji usługi** listy, upewnij się, że **wszystkie konfiguracje** jest zaznaczona, jak ustawienia magazynu lokalne powitania tooall usługi konfiguracji. Wszelkie inne wartości powoduje wszystkie pola wejściowe hello na stronie powitania wyłączana. 

    ![Konfiguracji usługi na liście](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. Wybierz tooadd wpisem Magazyn lokalny **dodać magazyn lokalny**.

    ![Dodaj magazyn lokalny](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Po dodaniu nowego wpisu magazynu lokalnego hello listy toohello, należy zaktualizować wiersza hello liście hello hello niezbędne informacje.

    ![Nowy wpis w lokalnej pamięci masowej](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Nazwa** — wprowadź nazwę hello mają toouse dla nowego magazynu lokalne powitania.
    - **Rozmiar (MB)** — wprowadź hello rozmiar w MB potrzebnym do nowego magazynu lokalne powitania.
    - **Wyczyść na roli odtworzenia** — wybierz dane hello tooremove tej opcji w hello nowego magazynu lokalnego, podczas odtwarzania hello maszyny wirtualnej dla roli hello.

1. toodelete wpisu magazynu lokalnego, wybierz wpis hello, a następnie wybierz **usunąć magazyn lokalny**.

1. Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.

## <a name="programmatically-accessing-local-storage"></a>Uzyskiwania dostępu do lokalnego magazynu

W tej części przedstawiono sposób tooprogrammatically uzyskiwania dostępu do magazynu lokalnego przy użyciu języka C# zapisując plik tekstowy testu `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Pisanie tekstu toolocal magazynem

Hello następującego kodu przedstawiono przykład sposobu toolocal magazyn plików toowrite tekstu. Zastąp hello &lt;LocalStorageName > symbolu zastępczego hello odpowiednią wartość. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Znajdź plik zapisany toolocal magazynu

tooview hello plik utworzony przez kod hello w poprzedniej sekcji hello, wykonaj następujące kroki:
    
1.  Witaj obszaru powiadomień systemu Windows, kliknij prawym przyciskiem myszy hello Azure ikona i, wybierz z menu kontekstowego hello, **Pokaż interfejs użytkownika emulatora obliczeń**. 

    ![Pokaż emulatora obliczeń platformy Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Wybierz rolę sieci web hello.

    ![Emulator obliczeń platformy Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Na powitania **Microsoft Azure obliczeniowe emulatora** menu, wybierz opcję **narzędzia** > **Otwórz magazyn lokalny**.

    ![Otwórz magazyn lokalny element menu](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Po otwarciu okna Eksploratora Windows hello, wprowadź "MyLocalStorageTest.txt" do hello **wyszukiwania** pola tekstowego, a następnie wybierz **Enter** toostart hello wyszukiwania. 

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o Azure projekty w programie Visual Studio, odczytując [Konfigurowanie projektu platformy Azure](vs-azure-tools-configuring-an-azure-project.md). Więcej informacji na temat schematu usługi w chmurze hello odczytując [odwołanie do schematu](https://msdn.microsoft.com/library/azure/dd179398).

