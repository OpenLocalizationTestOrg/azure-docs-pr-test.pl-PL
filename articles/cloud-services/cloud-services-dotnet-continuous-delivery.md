---
title: "dostarczanie aaaContinuous chmury usługi z programem TFS na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacji w chmurze tooset się ciągłego dostarczania dla platformy Azure. Przykłady kodu dla instrukcji wiersza polecenia programu MSBuild i skryptów programu PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Ciągłego dostarczania dla usług w chmurze na platformie Azure
Witaj procesu opisanego w tym artykule przedstawiono sposób tooset się ciągłego dostarczania dla aplikacji w chmurze Azure. Ten proces umożliwia automatyczne tworzenie pakietów i wdrożyć tooAzure pakietu powitania po każdym ewidencjonowania kodu. Witaj procesu kompilacji pakietu opisane w tym artykule jest równoważne toohello **pakietu** polecenie w programie Visual Studio i kroki publikowania są równoważne toohello **publikowania** polecenia w programie Visual Studio.
Hello artykuł obejmuje hello metody toocreate serwera kompilacji będzie korzystać także z MSBuild instrukcje wiersza polecenia i skryptów programu Windows PowerShell i pokazuje, jak toooptionally Konfigurowanie programu Visual Studio Team Foundation Server - Team Build definicje toouse hello MSBuild poleceń i skryptów programu PowerShell. proces Hello jest można dostosować do własnego środowiska kompilacji i środowisk docelowej platformy Azure.

Można również użyć programu Visual Studio Team Services, wersji programu TFS, która jest hostowana na platformie Azure, toodo to łatwiejsze. 

Przed rozpoczęciem należy opublikować aplikacji z programu Visual Studio.
Zapewni to, czy wszystkie zasoby hello są dostępne i została zainicjowana usiłujące tooautomate hello publikacji procesu.

## <a name="1-configure-hello-build-server"></a>1: Konfigurowanie powitania serwera kompilacji
Przed utworzeniem pakietu Azure przy użyciu programu MSBuild, należy zainstalować hello wymagane oprogramowanie i narzędzi na serwerze kompilacji hello.

Program Visual Studio nie jest wymagane toobe zainstalowane na powitania serwera kompilacji. Toomanage usługi kompilacji programu Team Foundation toouse serwera kompilacji, należy wykonać instrukcje hello hello [usługi kompilacji programu Team Foundation] [ Team Foundation Build Service] dokumentacji.

1. Na serwerze kompilacji hello Zainstaluj hello [.NET Framework 4.5.2][.NET Framework 4.5.2], która obejmuje MSBuild.
2. Zainstaluj najnowsze hello [Azure Authoring Tools dla programu .NET](https://azure.microsoft.com/develop/net/).
3. Zainstaluj hello [biblioteki Azure dla platformy .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Serwer kompilacji pliku Microsoft.WebApplication.targets hello kopiowania z toohello instalacji programu Visual Studio.

   Na komputerze z programem Visual Studio zainstalowany, ten plik znajduje się w katalogu hello C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\14.0\\WebApplications. Należy skopiować toohello tym samym katalogu na powitania serwera kompilacji.
5. Zainstaluj hello [Azure Tools dla programu Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2: Tworzenie pakietu przy użyciu polecenia programu MSBuild
W tej sekcji opisano, jak tooconstruct MSBuild polecenia, który tworzy pakiet Azure. Wykonaj ten krok na powitania kompilacji serwera tooverify czy wszystko jest poprawnie skonfigurowana i czy polecenie MSBuild hello wykonuje, co ma toodo. Można dodać skrypty kompilacji to tooexisting wiersza polecenia na serwerze kompilacji hello lub skorzystać z wiersza polecenia hello w definicji kompilacji TFS, zgodnie z opisem w następnej sekcji hello. Aby uzyskać więcej informacji na temat parametrów wiersza polecenia i MSBuild, zobacz [informacje w wierszu polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Jeśli program Visual Studio jest zainstalowany na serwerze kompilacji hello, Znajdź i wybierz **wiersz polecenia programu Visual Studio** w hello **programu Visual Studio Tools** folderu systemu Windows.

   Jeśli program Visual Studio nie jest zainstalowany na serwerze kompilacji hello, otwórz wiersz polecenia i upewnij się, że MSBuild.exe jest dostępny w ścieżce. Z hello .NET Framework w hello ścieżki % WINDIR % jest zainstalowany program MSBuild\\Microsoft.NET\\Framework\\*wersji*. Na przykład aby dodać zmiennej środowiskowej PATH toohello MSBuild.exe, jeśli masz zainstalowany program .NET Framework 4, wpisz następujące polecenie w wierszu polecenia hello hello:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. W wierszu polecenia hello Przejdź toohello folder zawierający plik projektu platformy Azure, które mają toobuild.
3. Uruchom program MSBuild z hello/target: opcja tak jak hello poniższy przykład publikowania:

       MSBuild /target:Publish

   Tej opcji można stosować skrót /t: publikowania. Opcja /t:Publish Hello w programie MSBuild nie należy mylić z polecenia Opublikuj hello dostępne w programie Visual Studio Jeśli masz hello zainstalowania zestawu Azure SDK. Witaj /t: opcja publikowania tylko kompilacje hello Azure pakietów. Nie wdrażać pakietów hello jak hello polecenia Opublikuj w programie Visual Studio.

   Opcjonalnie można określić nazwę projektu hello jako parametr MSBuild. Jeśli nie zostanie określony, używany jest hello bieżący katalog. Aby uzyskać więcej informacji na temat opcji wiersza polecenia programu MSBuild, zobacz [informacje w wierszu polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Zlokalizuj hello danych wyjściowych. Domyślnie to polecenie tworzy katalog w folderze głównym toohello relacji dla projektu hello, takich jak *ProjectDir*\\bin\\*konfiguracji* \\ App.publish\\. Podczas tworzenia projektu platformy Azure, generowanie dwóch plików, sam plik pakietu hello i hello towarzyszącego pliku konfiguracji:

   * Project.cspkg
   * Element ServiceConfiguration. *TargetProfile*.cscfg

   Domyślnie każdy projekt Azure zawiera jeden usługi konfiguracji pliku (cscfg) lokalne kompilacje (debugowanie) i drugi dla kompilacji chmury (tymczasowym czy produkcyjnym), ale można dodać lub usunąć pliki konfiguracji usługi, zgodnie z potrzebami. Podczas tworzenia pakietu w programie Visual Studio, użytkownik zostanie poproszony które tooinclude pliku konfiguracji usługi obok hello pakietu.
5. Określ plik konfiguracji usługi hello. Podczas tworzenia pakietu przy użyciu programu MSBuild w pliku konfiguracji usługi lokalne powitania znajduje się domyślnie. tooinclude plik konfiguracji innej usługi, ustaw właściwość TargetProfile hello polecenia programu MSBuild, tak jak hello poniższy przykład:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Określ lokalizację hello hello danych wyjściowych. Ustaw ścieżkę hello przy użyciu /p:PublishDir =*katalogu* \\ opcji, w tym hello kończyć się separatorem ukośnik odwrotny, tak jak hello poniższy przykład:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Po utworzone i przetestowane MSBuild odpowiednie polecenie wiersza toobuild projektów i połączyć je w pakiecie Azure, istnieje możliwość dodania skryptów kompilacji tooyour tego wiersza polecenia. Jeśli serwer kompilacji obsługuje skrypty niestandardowe, ten proces będzie zależeć od specyfiki procesu kompilacji niestandardowej. Jeśli używasz TFS jako środowiska kompilacji, a następnie wykonać instrukcje hello hello następnego kroku procesu kompilacji tooyour tooadd hello Azure pakietu kompilacji.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: Tworzenie pakietu za pomocą kompilacji TFS zespołu
Jeśli masz Konfigurowanie kontrolera kompilacji i hello serwer kompilacji Team Foundation Server (TFS), skonfigurować jako maszyna kompilacji TFS, a następnie możesz opcjonalnie skonfigurować automatyczne kompilacji pakietu Azure. Aby uzyskać informacje dotyczące sposobu tooset się i użyj Team Foundation server jako system kompilacji, zobacz [skalowania w poziomie system kompilacji][Scale out your build system]. W szczególności w poniższej procedurze przyjęto, że na serwerze kompilacji zostało skonfigurowane zgodnie z opisem w [Wdróż i skonfiguruj serwer kompilacji][Deploy and configure a build server], i utworzyć projektu zespołowego, należy utworzyć chmury projekt usługi w projekcie zespołowym hello.

tooconfigure TFS toobuild Azure pakietów, wykonaj następujące kroki hello:

1. W programie Visual Studio na komputerze dewelopera na powitania menu Widok wybierz polecenie **Team Explorer**, lub wybierz polecenie Ctrl +\\, Ctrl + M. W oknie programu Team Explorer rozwiń hello **kompilacje** węzła lub wybierz hello **kompilacje** stronie, a następnie wybierz **nową definicję kompilacji**.

   ![Nowa opcja definicji kompilacji][0]
2. Wybierz hello **wyzwalacza** , a następnie określ hello potrzeby warunków, dla której ma zostać hello toobe pakiet utworzony. Na przykład określić **ciągłej integracji** występuje toobuild hello pakietu przy każdym wyboru w kontroli źródła.
3. Wybierz hello **ustawienia źródła** karcie i upewnij się, że folder projektu jest wymieniony w hello **folderu kontroli źródła** kolumny, i jest w stanie hello **Active**.
4. Wybierz hello **kompilacji domyślne** , a następnie w obszarze kontroler kompilacji, sprawdź nazwę hello powitania serwera kompilacji.  Ponadto wybierz opcję hello **folderu odrzuceń następujące toohello danych wyjściowych kompilacji kopiowania** i określ hello żądaną lokalizację docelową.
5. Wybierz hello **procesu** kartę. Na karcie procesu hello, wybierz szablon domyślny hello, w obszarze **kompilacji**, wybierz projekt hello, jeśli nie została jeszcze wybrana, a rozwiń hello **zaawansowane** części hello **kompilacji**części hello siatki.
6. Wybierz **argumenty programu MSBuild**i ustaw odpowiednie argumenty wiersza polecenia programu MSBuild hello zgodnie z opisem w kroku 2. powyżej. Na przykład wprowadź **/t: publikowanie /p:PublishDir =\\\\MójSerwer\\porzuca\\**  toobuild pakietu hello pakietu i skopiuj pliki lokalizacji toohello \\ \\MójSerwer\\porzuca\\:

   ![Argumenty programu MSBuild][2]

   > [!NOTE]
   > Kopiowanie tooa pliki hello udziału umożliwia łatwiejsze toomanually wdrażania pakietów hello na komputerze projektowym.
7. Testowanie hello Powodzenie z kroku kompilacji sprawdzając w projekcie tooyour zmiany lub kolejki nowej kompilacji. Kliknij prawym przyciskiem myszy tooqueue zapasowej nowej kompilacji w programie Team Explorer **wszystkie definicje kompilacji,** , a następnie wybierz **Tworzenie nowej kolejki**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: publikowanie pakietu przy użyciu skryptu programu PowerShell
W tej sekcji opisano, jak tooconstruct skrypt programu Windows PowerShell, która będzie publikować pakiet aplikacji hello chmury output tooAzure przy użyciu parametrów opcjonalnych. Ten skrypt można wywołać po wykonaniu kroku kompilacji hello w Twojej automatyzacji niestandardowej kompilacji. Można również nadać mu z szablonu procesu działania przepływu pracy w Visual Studio TFS Team Build.

1. Zainstaluj hello [poleceń cmdlet programu Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 lub nowszej).
   Podczas fazy instalacji polecenia cmdlet hello należy wybrać tooinstall jako przystawki. Należy zwrócić uwagę, czy tego oficjalnie obsługiwana wersja zastępuje starszej wersji hello oferowane za pośrednictwem portalu CodePlex, chociaż hello poprzednie wersje zostały numerowane 2.x.x.
2. Uruchom program PowerShell Azure przy użyciu hello Start menu lub strony początkowej. Po uruchomieniu w ten sposób hello poleceń cmdlet programu Azure PowerShell zostanie załadowany.
3. W wierszu polecenia programu PowerShell hello, sprawdź, czy polecenia cmdlet programu PowerShell hello są załadowane przez wprowadzenie polecenia częściowe hello `Get-Azure` , a następnie naciskając klawisz hello klawisza Tab do uzupełniania instrukcji.

   Po naciśnięciu klawisza Tab hello wielokrotnie, powinny pojawić różne polecenia programu PowerShell systemu Azure.
4. Sprawdź, czy masz połączenie tooyour subskrypcji platformy Azure przez zaimportowanie informacji o subskrypcji z pliku .publishsettings hello.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Następnie wprowadź polecenie hello

   `Get-AzureSubscription`

   Oznacza to, informacje o Twojej subskrypcji. Sprawdź, czy wszystkie ustawienia są poprawne.
5. Zapisz szablon skryptu hello podana na końcu tego artykułu w folderze skryptów jako c: hello\\skryptów\\WindowsAzure\\**PublishCloudService.ps1**.
6. Przejrzyj sekcję parametry hello hello skryptu. Dodaj lub zmodyfikuj wartości domyślne. Te wartości zawsze może być zastąpiona przez przekazywanie parametrów jawnych.
7. Upewnij się, istnieją usługi w chmurze prawidłowe i kont magazynu utworzonych w ramach subskrypcji, która może być celem hello publikowanie skryptu. Konto magazynu (magazynu obiektów blob) zostanie użyty tooupload i tymczasowe przechowywanie hello wdrożenia pakietu i pliku konfiguracji podczas tworzenia wdrożenia.

   * toocreate nową usługę w chmurze, można wywołać tego skryptu lub użyj hello [portalu Azure](https://portal.azure.com). Nazwa usługi w chmurze Hello będzie służyć jako prefiksu w pełni kwalifikowaną nazwę domeny i dlatego musi być unikatowa.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate nowe konto magazynu, można wywołać tego skryptu lub użyj hello [portalu Azure](https://portal.azure.com). Nazwa konta magazynu Hello będzie służyć jako prefiksu w pełni kwalifikowaną nazwę domeny i dlatego musi być unikatowa. Spróbuj użyć hello takie same nazwy jako usługa w chmurze.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Wywołanie skryptu hello bezpośrednio z programu Azure PowerShell lub okablować się tego skryptu tooyour hosta kompilacji automatyzacji toooccur po hello kompilacji pakietu.

   > [!IMPORTANT]
   > skrypt Hello będzie zawsze usunąć lub zamienić istniejący wdrożeń domyślnie, jeśli ich wykrycia. Jest to niezbędne do włączenia ciągłego dostarczania automatyzacji, jeśli to możliwe nie monitowania użytkownika.
   >
   >

   **Przykładowy scenariusz 1:** toohello ciągłe wdrażanie tymczasowej środowiska usługi:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   To jest zazwyczaj następuje testu weryfikacji i wymiany wirtualnych adresów IP. swap Hello VIP może odbywać się za pośrednictwem hello [portalu Azure](https://portal.azure.com) lub za pomocą polecenia cmdlet hello przenoszenia wdrożenia.

   **Przykładowy scenariusz 2:** środowiska produkcyjnego toohello ciągłego wdrażania usługi dedykowanych testu

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Pulpit zdalny:**

   Włączenie pulpitu zdalnego w projekcie platformy Azure należy tooperform dodatkowe kroki jednorazowe hello tooensure, który jest poprawny certyfikat usługi w chmurze przekazać usługi w chmurze tooall celem tego skryptu.

   Znajdź wartości odcisku palca certyfikatu hello oczekiwany przez poszczególnych ról. Wartości odcisku palca są widoczne w sekcji certyfikaty hello pliku konfiguracji chmury (tj. ServiceConfiguration.Cloud.cscfg). Jest również widoczna w oknie dialogowym Konfiguracja usług pulpitu zdalnego hello w programie Visual Studio, gdy hello Pokaż opcje i widok wybranego certyfikatu.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Przekaż certyfikaty usług pulpitu zdalnego za pomocą następującego polecenia cmdlet skryptu hello krokiem jednorazowej konfiguracji:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Na przykład:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   Alternatywnie można wyeksportować plik certyfikatu PFX hello z kluczem prywatnym i przekazywania certyfikaty tooeach docelowej chmury usługi przy użyciu [portalu Azure](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Uaktualnienie a wdrożenia. Usunięcie wdrożenia —\> nowego wdrożenia**

   skrypt Hello będzie domyślnie wykonywać uaktualniania wdrożenia ($enableDeploymentUpgrade = 1) gdy brak parametru jest przekazano lub nie została jawnie przekazana wartość 1. Dla pojedynczego wystąpienia to zaletą jest mniej czasu niż pełne wdrożenie. Dla wystąpień, które wymagają wysokiej dostępności ma to również zaletą hello pozostawienie niektórych wystąpień uruchomiona, podczas gdy inne uaktualnienia (przejście domenę aktualizacji), a także Twojego adresu VIP, nie zostaną usunięte.

   Wdrożenia uaktualnienia można wyłączyć w skrypcie hello ($enableDeploymentUpgrade = 0) lub przez przekazanie *- enableDeploymentUpgrade 0* jako parametr zmienia delete toofirst zachowanie skryptu wszystkie istniejące wdrożenia i utworzyć nowe wdrożenie.

   > [!IMPORTANT]
   > skrypt Hello będzie zawsze usunąć lub zamienić istniejący wdrożeń domyślnie, jeśli ich wykrycia. Jest to niezbędne do włączenia ciągłego dostarczania automatyzacji, jeśli to możliwe nie monitowania użytkownika / — operator.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: publikowanie pakietu za pomocą kompilacji TFS zespołu
Ten opcjonalny krok łączy TFS Team Build toohello skryptu utworzonego w kroku 4, który obsługuje publikowanie tooAzure kompilacji pakietu hello. Pociąga za sobą modyfikowanie hello szablonu procesu używanego przez definicję kompilacji, wykonywania działań publikowania na końcu hello hello przepływu pracy. Witaj Publikuj działania wykona przekazywanie parametrów z kompilacji hello polecenia programu PowerShell. W danych wyjściowych kompilacji standardowe hello będzie przekazywany w potoku dane wyjściowe hello MSBuild elementów docelowych i opublikuj skryptu.

1. Edytuj hello definicji kompilacji odpowiedzialny za ciągłego wdrażania.
2. Wybierz hello **procesu** kartę.
3. Postępuj zgodnie z [tych instrukcji](http://msdn.microsoft.com/library/dd647551.aspx) tooadd projekt działania hello szablon procesu kompilacji, Pobierz szablon domyślny hello, dodaj go do projektu hello i go zaewidencjonować. Nadaj nazwę nowej, takich jak AzureBuildProcessTemplate szablonu procesu kompilacji hello.
4. Zwraca toohello **procesu** , a następnie użyć **Pokaż szczegóły** tooshow listę szablonów procesu kompilacji dostępne. Wybierz hello **nowy...**  przycisk, a następnie przejdź projektu toohello właśnie dodany i zaewidencjonowane. Znajdź właśnie utworzony szablon hello i wybierz polecenie **OK**.
5. Otwórz hello wybrany szablon procesu do edycji. Możesz otworzyć bezpośrednio w Projektancie przepływów pracy hello lub toowork edytora XML hello z hello XAML.
6. Dodaj następujące listy argumentów nowe jako odrębne pozycje hello argumenty karcie projektanta przepływów pracy hello hello. Wszystkie argumenty powinny posiadać kierunek = w i wpisz = ciąg. Te parametry są parametry używane tooflow z hello definicję kompilacji w przepływie pracy hello, które następnie hello używane toocall get publikowania skryptu.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista argumentów][3]

   powitalne odpowiedniego XAML wygląda następująco:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Dodaj nową sekwencję na końcu hello Uruchom na agenta:

   1. Rozpocznij od dodania toocheck działania Jeśli instrukcji dla prawidłowym plikiem skryptu. Ustaw wartość toothis warunku hello:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. W hello następnie przypadku hello Jeśli instrukcji Dodaj nowe działanie w sekwencji. Publikowanie zestawu hello wyświetlana nazwa too'Start "
   3. Z hello rozpoczęcia publikowania sekwencji nadal zaznaczony Dodaj na następującej liście nowe zmienne jako oddzielne pozycje w karcie Zmienne hello projektanta przepływów pracy. Wszystkie zmienne powinny mieć typ zmiennej = ciągu i zakres = rozpoczęcie publikowania. Te parametry są parametry używane tooflow z hello definicji kompilacji do przepływu pracy, które następnie hello używane toocall get publikowania skryptu.

      * SubscriptionDataFilePath typu String
      * PublishScriptFilePath typu String

        ![Nowe zmienne][4]
   4. Jeśli korzystają z programu TFS 2012 lub starszy, Dodaj działanie ConvertWorkspaceItem początku hello hello nowej sekwencji. Jeśli używasz programu TFS 2013 lub nowszy, Dodaj działanie GetLocalPath początku hello hello nowej sekwencji. Dla ConvertWorkspaceItem, ustaw właściwości hello w następujący sposób: kierunek = ServerToLocal, nazwa wyświetlana = 'Convert opublikować nazwę pliku skryptu', dane wejściowe = "PublishScriptLocation", wynik = "PublishScriptFilePath", obszar roboczy = "Obszar roboczy". Dla działania GetLocalPath, ustaw too'PublishScriptLocation IncomingPath właściwości hello ", a hello too'PublishScriptFilePath wynik". To działanie konwertuje hello ścieżki toohello publikowania skryptu z lokalizacji serwera TFS (jeśli dotyczy) tooa ścieżka standardowe dysku lokalnym.
   5. Jeśli używasz programu TFS 2012 lub wcześniej, Dodaj kolejne działanie ConvertWorkspaceItem na końcu hello hello nowej sekwencji. Kierunek = ServerToLocal, nazwa wyświetlana = "Dokonać konwersji subskrypcji nazwa_pliku", dane wejściowe = "SubscriptionDataFileLocation", wynik = "SubscriptionDataFilePath", obszar roboczy = "Obszar roboczy". Jeśli używasz programu TFS 2013 lub nowszy, Dodaj inny GetLocalPath. IncomingPath = "SubscriptionDataFileLocation", a wynik = "SubscriptionDataFilePath."
   6. Dodawanie działania InvokeProcess na końcu hello hello nowej sekwencji.
      Tego wywołania działania PowerShell.exe z argumentami hello przekazany przez hello definicji kompilacji.

      + Argumenty = String.Format ("-""{0}" "- serviceName {1} - storageAccountName {2} tabelę packageLocation —""{3}" "- cloudConfigLocation""{4}" "- subscriptionDataFile""{5}" "- selectedSubscription {6} pliku-środowiska""{7}" "",  PublishScriptFilePath, ServiceName, StorageAccountName, tabelę PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, Nazwa subskrypcji, środowisko)
      + Nazwa wyświetlana = Execute publikowania skryptu
      + Nazwa pliku = "PowerShell" (zawierają hello oferty)
      + OutputEncoding = System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. W hello **Obsługa standardowego wyjścia** sekcji textbox InvokeProcess, ustaw too'data wartości tekstowe hello ". To dane wyjścia standardowego hello toostore zmiennej.
   8. Dodaj działanie WriteBuildMessage poniżej hello **Obsługa standardowego wyjścia** sekcji. Ustaw hello znaczenie = "Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High" i wiadomość hello = "dane". Dzięki temu hello standardowe dane wyjściowe skryptu zostanie zapisane dane wyjściowe kompilacji toohello.
   9. W hello **obsługi błędów wyjścia** sekcji textbox InvokeProcess, ustaw too'data wartości tekstowe hello ". To dane błąd standardowy hello toostore zmiennej.
   10. Dodaj działanie WriteBuildError poniżej hello **obsługi błędów wyjścia** sekcji. Ustaw wiadomość hello = "dane". Dzięki temu, że błędy standardowe hello skryptu hello zostaną zapisane dane wyjściowe błędów kompilacji toohello.
   11. Popraw błędy wskazywanym przez niebieski znaczniki wykrzyknika. Umieść kursor nad tooget znaczniki wykrzyknika wskazówkę o błędzie hello. Zapisz hello przepływu pracy, aby usunąć błędy.

   wynik końcowy Hello hello opublikować przepływu pracy działania będzie wyglądać następująco w Projektancie hello:

   ![Działania przepływu pracy][5]

   wynik końcowy Hello hello opublikować działań będzie wyglądać następująco w języku XAML przepływu pracy:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Zapisz hello przepływu pracy szablonu procesu dla kompilacji i zaewidencjonuj tego pliku.
9. Edytowanie definicji kompilacji hello (je zamknąć, jeżeli jest już otwarty) i wybierz hello **nowy** przycisku, jeśli nie ma jeszcze hello nowego szablonu na liście hello szablonów procesu.
10. Ustawiania wartości właściwości parametru hello w sekcji różne hello w następujący sposób:

    1. CloudConfigLocation = "c:\\porzuca\\app.publish\\ServiceConfiguration.Cloud.cscfg" *ta wartość jest określana na podstawie: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. Tabelę PackageLocation = "c:\\porzuca\\app.publish\\ContactManager.Azure.cspkg" *ta wartość jest określana na podstawie: (cspkg)($ProjectName) $PublishDir*
    3. PublishScriptLocation = "c:\\skryptów\\WindowsAzure\\PublishCloudService.ps1"
    4. ServiceName = "mycloudservicename" *Użyj hello odpowiednie nazwa usługi w chmurze w tym miejscu*
    5. Środowisko = "Tymczasowe"
    6. StorageAccountName = "mystorageaccountname" *Użyj hello odpowiednie nazwy konta magazynu w tym miejscu*
    7. SubscriptionDataFileLocation = "c:\\skryptów\\WindowsAzure\\Subscription.xml"
    8. Nazwa subskrypcji = "default"

    ![Wartości właściwości parametru][6]
11. Zapisz hello toohello zmiany definicji kompilacji.
12. Kolejka tooexecute kompilacji, zarówno hello kompilacji pakietu i publikowania. Jeśli masz wyzwalacz ustawić tooContinuous integracji wykona to zachowanie na każdym zaewidencjonowania.

### <a name="publishcloudserviceps1-script-template"></a>PublishCloudService.ps1 skrypt szablonu
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Następne kroki
tooenable zdalne debugowanie przy użyciu ciągłego dostarczania, zobacz [Włączanie debugowania zdalnego, korzystając z ciągłego dostarczania toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
