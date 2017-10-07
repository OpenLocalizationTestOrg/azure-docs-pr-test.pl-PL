---
title: "aaaUsing tooDev tooPublish skryptów programu Windows PowerShell i środowisk testowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skrypty toouse środowiska Windows PowerShell z programu Visual Studio toopublish środowiska toodevelopment i testowania."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Przy użyciu programu Windows PowerShell skrypty środowiska toopublish toodev i testowania
Podczas tworzenia aplikacji sieci web w programie Visual Studio, można wygenerować skrypt programu Windows PowerShell, na której można nowsze publikowanie hello tooautomate Twojego tooAzure witryny sieci Web jako aplikacji sieci Web w usłudze Azure App Service lub maszynie wirtualnej. Można edytować i rozszerzyć hello skrypt programu Windows PowerShell w toosuit edytora programu Visual Studio hello wymagań lub zintegrować hello skryptu z istniejących kompilacji, testów i skrypty publikowania.

Skrypty te można udostępnić dostosowane wersje (znanej także jako środowiskach programistycznych i testowych) lokacji do użytku tymczasowego. Może na przykład skonfigurować konkretnej wersji witryny sieci Web na maszynie wirtualnej platformy Azure lub na powitania miejsca na toorun witryny sieci Web zestawu testów, występuje błąd, przetestować poprawkę, wersja próbna proponowanej zmiany lub skonfigurować niestandardowe środowisko pokaz lub prezentacji. Po utworzeniu skryptu, który publikuje projektu można odtworzyć identyczne środowisk, ponownie uruchamiając skrypt hello zgodnie z potrzebami lub uruchom skrypt hello z własnych kompilacji toocreate aplikacji sieci web niestandardowego środowiska do testowania.

## <a name="what-you-need"></a>Co jest potrzebne
* Zestaw Azure SDK 2.3 lub nowszej. Zobacz [programu Visual Studio pobiera](http://go.microsoft.com/fwlink/?LinkID=624384) Aby uzyskać więcej informacji.

Nie trzeba hello Azure SDK toogenerate hello skryptów dla projektów sieci web. Ta funkcja jest dla projektów sieci web, nie role sieci web usług w chmurze.

* Program Azure PowerShell 0.7.4 lub nowszym. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.
* [Program Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) lub nowszym.

## <a name="additional-tools"></a>Dodatkowe narzędzia
Dodatkowych narzędzi i zasobów do pracy z programu PowerShell w programie Visual Studio do tworzenia aplikacji platformy Azure są dostępne. Zobacz [narzędzia programu PowerShell dla programu Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Generowanie hello publikowanie skryptów
Możesz wygenerować hello publikowanie skryptów do maszyny wirtualnej, który jest hostem witryny sieci Web, podczas tworzenia nowego projektu wykonując [tych instrukcji](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Możesz również [Generowanie publikowanie skryptów dla aplikacji sieci web w usłudze Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Skrypty, które generuje Visual Studio
Visual Studio generuje folder rozwiązania poziomu o nazwie **PublishScripts** skrypt publikowania dla maszyny wirtualnej lub witryny sieci Web i moduł, który zawiera funkcje, których można używać w hello zawiera dwa pliki programu Windows PowerShell, skrypty. Visual Studio także generuje plik w formacie JSON hello, który określa szczegóły hello hello projektu, który jest wdrażany.

### <a name="windows-powershell-publish-script"></a>Skrypt publikowanie programu Windows PowerShell
Witaj publikowania skryptu zawiera określone publikowania kroki wdrażania tooa witryny sieci Web lub maszyny wirtualnej. Program Visual Studio udostępnia kolorowania rozwoju środowiska Windows PowerShell. Pomoc dla funkcji hello jest dostępne, a można swobodnie edytować funkcji hello w toosuit skryptu hello zmieniających się wymagań.

### <a name="windows-powershell-module"></a>Moduł programu Windows PowerShell
Witaj środowiska Windows PowerShell moduł, który generuje Visual Studio zawiera funkcje, które hello publikowania używa skryptu. Są to funkcje środowiska Azure PowerShell które nie mają zamierzonego toobe zmodyfikowane. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji.

### <a name="json-configuration-file"></a>Plik JSON konfiguracji
Plik JSON Hello jest tworzony w hello **konfiguracje** folderu i zawiera dane konfiguracji, które określa dokładnie które tooAzure toodeploy zasobów. Nazwa Hello hello pliku, który generuje Visual Studio jest projektu name-WAWS-dev.json Jeśli utworzono witrynę sieci Web lub projektu Nazwa-maszyny Wirtualnej — dev.json Jeśli utworzono maszynę wirtualną. Oto przykładowy plik JSON konfiguracji, który jest generowany podczas tworzenia witryny sieci Web. Większość wartości hello nie wymaga wyjaśnień. Nazwa witryny sieci Web Hello jest generowany przez Azure, dlatego mogą być niezgodne nazwę projektu.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Podczas tworzenia maszyny wirtualnej pliku konfiguracji JSON hello wygląda podobnie następujące toohello. Należy pamiętać, że usługa w chmurze jest tworzony jako kontener dla maszyny wirtualnej hello. Maszyna wirtualna Hello zawiera hello zwykle punktów końcowych dostęp w sieci web za pośrednictwem protokołu HTTP i HTTPS, a także punktów końcowych dla narzędzia Web Deploy, który umożliwia publikowanie toohello witryny sieci Web z komputera lokalnego, pulpitu zdalnego i środowiska Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Co się stanie po uruchomieniu hello można edytować hello JSON konfiguracji toochange publikowanie skryptów. Witaj `cloudService` i `virtualMachine` sekcje są wymagane, ale można usunąć hello `databases` sekcji, jeśli nie jest potrzebna. Hello właściwości, które są puste w hello domyślny plik konfiguracji generowany w programie Visual Studio jest opcjonalna. te, które mają wartości w pliku konfiguracyjnym domyślna hello są wymagane.

Jeśli masz witrynę sieci Web, który ma wiele środowisk wdrażania (nazywanych miejscami) zamiast lokacji pojedynczego produkcji na platformie Azure, hello z nazwą miejsca można uwzględnić w nazwie hello hello witryny sieci Web w pliku konfiguracji JSON hello. Na przykład, jeśli masz witrynę sieci Web o nazwie **witryna** z miejscem dla niego o nazwie **test** , a następnie hello identyfikatora URI jest test.cloudapp.net witrynę, ale hello poprawną nazwę toouse w pliku konfiguracyjnym hello jest mysite(test) . Tylko można to zrobić, jeśli hello witryny sieci Web i gniazd już istnieją w Twojej subskrypcji. Jeśli nie istnieją, Utwórz hello witryny sieci Web, uruchamiając skrypt hello bez określania miejsca hello, a następnie utworzyć gniazda hello hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885), a następnie uruchom skrypt hello o nazwie modyfikacji witryny sieci Web hello. Aby uzyskać więcej informacji dotyczących miejsc wdrożenia dla aplikacji sieci web, zobacz [Konfigurowanie środowiska dla aplikacji sieci web w usłudze Azure App Service przejściowe](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Jak toorun hello opublikować skryptów
Jeśli nigdy nie zostało uruchomione przed skrypt programu Windows PowerShell, należy najpierw ustawić hello wykonywania zasad tooenable skrypty toorun. Jest to użytkowników tooprevent funkcji zabezpieczeń, uruchamiania skryptów programu Windows PowerShell, jeśli są one narażone toomalware i wirusami, które obejmują wykonywanie skryptów.

### <a name="run-hello-script"></a>Uruchom skrypt hello
1. Utwórz hello pakietu Narzędzia Web Deploy w dla projektu. Pakiet Web Deploy jest skompresowanego archiwum (pliku .zip), zawierających pliki mają toocopy tooyour witryny sieci Web lub maszyny wirtualnej. Pakiety Web Deploy można tworzyć w programie Visual Studio dla dowolnej aplikacji sieci web.

![Tworzenie sieci Web wdrażanie pakietu](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Aby uzyskać więcej informacji, zobacz [jak: utworzyć pakiet wdrożeniowy sieci Web w programie Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Można również zautomatyzować tworzenie hello pakietu Narzędzia Web Deploy, zgodnie z opisem w sekcji hello **dostosowywanie i rozszerzanie hello publikowanie skryptów** dalszej części tego tematu.

1. W **Eksploratora rozwiązań**, otwórz menu kontekstowe hello hello skryptu, a następnie wybierz **otworzyć za pomocą programu PowerShell ISE**.
2. Jeśli jest to hello na tym komputerze uruchomiono skryptów programu Windows PowerShell po raz pierwszy, Otwórz okno wiersza polecenia z uprawnieniami administratora i hello wpisz następujące polecenie:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Zaloguj przy użyciu następującego polecenia hello tooAzure.

    ```powershell
    Add-AzureAccount
    ```

    Po wyświetleniu monitu podaj nazwę użytkownika i hasło.

    Należy zwrócić uwagę podczas automatyzacji hello skryptu, ta metoda podawania poświadczeń platformy Azure nie będą działać. Zamiast tego należy używać poświadczeń tooprovide pliku .publishsettings hello. Jeden raz, możesz użyć polecenia hello **Get-AzurePublishSettingsFile** toodownload hello pliku z platformy Azure, a następnie użyć **AzurePublishSettingsFile importu** tooimport hello pliku. Aby uzyskać szczegółowe instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

4. (Opcjonalnie) Jeśli chcesz, aby toocreate Azure zasoby, takie jak hello maszyny wirtualnej, bazy danych i witryny sieci Web bez publikowania aplikacji sieci web, użyj hello **WebApplication.ps1 publikowania** z hello **-konfiguracji** pliku konfiguracji JSON toohello wartość argumentu. Ten wiersz polecenia korzysta toodetermine pliku konfiguracji JSON hello które toocreate zasobów. Ponieważ używa ustawień domyślnych hello inne argumenty wiersza polecenia, tworzy hello zasobów, ale nie publikowania aplikacji sieci web. Witaj — opcja pełne zapewnia więcej informacji o tym, co dzieje.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Użyj hello **WebApplication.ps1 publikowania** polecenia, jak pokazano w jednym z hello następujące przykłady tooinvoke hello skrypt i opublikować aplikację sieci web. Jeśli potrzebujesz toooverride hello domyślne ustawienia dla każdego hello inne argumenty, takie jak nazwa subskrypcji hello, publikowanie nazwy pakietu, poświadczenia maszyny wirtualnej lub poświadczenia serwera bazy danych, można określić tych parametrów. Użyj hello **— pełne** opcję toosee więcej informacji na temat postępu hello hello procesu publikowania.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Jeśli tworzysz maszynę wirtualną, polecenie hello wygląda hello. W tym przykładzie przedstawiono również sposób toospecify hello poświadczeń dla wielu baz danych. Hello maszyn wirtualnych utworzonych przez te skrypty hello certyfikat SSL nie pochodzi z zaufanego głównego urzędu. Dlatego należy toouse hello **— AllowUntrusted** opcji.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    skrypt Hello można utworzyć bazy danych, ale nie tworzy serwerów baz danych. Jeśli chcesz toocreate serwera bazy danych, można użyć hello **AzureSqlDatabaseServer nowy** funkcji w hello modułu platformy Azure.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Dostosowywanie i rozszerzanie hello publikowanie skryptów
Można dostosować hello publikowania skryptu i pliku konfiguracji JSON. Witaj funkcji w module środowiska Windows PowerShell hello **AzureWebAppPublishModule.psm1** nie są zamierzone toobe zmodyfikowane. Po prostu toospecify innej bazy danych lub zmienić niektóre właściwości hello hello maszyny wirtualnej, należy edytować plik konfiguracji JSON hello. Chcąc tooextend funkcjonalność hello hello skryptu tooautomate tworzenia i testowania projektu, można zaimplementować klas zastępczych funkcji w **WebApplication.ps1 publikowania**.

tooautomate tworzenia projektu, Dodaj kod, który wywołuje MSBuild zbyt`New-WebDeployPackage` opisane w tym przykładzie kodu. toohello ścieżka Hello polecenie MSBuild różni się w zależności od wersji hello programu Visual Studio został zainstalowany. tooget hello poprawną ścieżkę, możesz użyć funkcji hello **Get-MSBuildCmd**, jak pokazano w poniższym przykładzie.

### <a name="tooautomate-building-your-project"></a>tooautomate tworzenia projektu
1. Dodaj hello `$ProjectFile` parametru w sekcji globalne param hello.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copy — funkcja hello `Get-MSBuildCmd` do pliku skryptu.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Zastąp `New-WebDeployPackage` z hello następujący kod i zastąp symbole zastępcze hello podczas tworzenia wiersza hello `$msbuildCmd`. Ten kod jest dla programu Visual Studio 2015. Jeśli używasz programu Visual Studio 2013, zmień hello **VisualStudioVersion** właściwości poniżej zbyt`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild Twojej aplikacji sieci web, użyj MsBuild.exe. Aby uzyskać pomoc, zobacz MSBuild wiersza polecenia pod adresem: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Wykonanie polecenia kompilacji hello Start

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Wywołaj hello `New-WebDeployPackage` funkcja przed wierszem: `$Config = Read-ConfigFile $Configuration` dla aplikacji sieci web lub `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` dla maszyn wirtualnych.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Wywołanie skryptu hello dostosowane z wiersza polecenia przy użyciu hello przekazywanie `$Project` argumentu, tak jak powitania po przykład wiersza polecenia.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate testowania aplikacji, Dodaj kod zbyt`Test-WebApplication`. Należy się toouncomment hello wierszy w **WebApplication.ps1 publikowania** gdzie te funkcje są wywoływane. Jeśli nie zapewniać implementację, można ręcznie utworzyć projektu za pomocą programu Visual Studio, a następnie uruchom hello Opublikuj tooAzure toopublish skryptu.

## <a name="publishing-function-summary"></a>Podsumowanie funkcji publikowania
tooget pomocy dla funkcji, można użyć w wierszu polecenia programu Windows PowerShell hello, użyj polecenia hello `Get-Help function-name`. Pomoc Hello zawiera parametr pomocy i przykłady. Witaj tego samego tekstu pomocy jest również w plikach źródłowych skryptu hello, **AzureWebAppPublishModule.psm1** i **WebApplication.ps1 publikowania**. skrypt Hello i pomocy są zlokalizowane w języku Visual Studio.

**AzureWebAppPublishModule**

| Nazwa funkcji | Opis |
| --- | --- |
| Dodaj AzureSQLDatabase |Tworzy nową bazę danych Azure SQL. |
| Dodaj AzureSQLDatabases |Tworzy baz danych Azure SQL z hello wartości w pliku konfiguracji JSON hello, który generuje Visual Studio. |
| Dodaj AzureVM |Tworzy maszynę wirtualną platformy Azure i zwraca adres URL hello hello wdrożyć maszyny Wirtualnej. Witaj funkcja konfiguruje hello wymagania wstępne, a następnie wywołania hello **AzureVM nowy** funkcji toocreate (moduł Azure) nowej maszyny wirtualnej. |
| Dodaj AzureVMEndpoints |Dodaje nową maszynę wirtualną tooa wejściowych punktów końcowych i zwraca hello maszynę wirtualną z hello nowy punkt końcowy. |
| Dodaj AzureVMStorage |Tworzy nowe konto magazynu Azure w hello bieżącej subskrypcji. Nazwa Hello hello konta zaczyna się od "devtest", po której następują unikatowy ciąg alfanumeryczny. Funkcja Hello zwraca nazwę hello hello nowe konto magazynu. Należy określić lokalizację i grupę koligacji dla hello nowe konto magazynu. |
| Dodaj AzureWebsite |Tworzy witrynę sieci Web z hello określonej nazwy i lokalizacji. Ta funkcja wymaga hello **AzureWebsite nowy** funkcji w hello modułu platformy Azure. Jeśli subskrypcja hello już nie obejmuje witrynę sieci Web przy użyciu określonej nazwy hello, funkcja ta tworzy hello witryny sieci Web i zwraca obiekt witryny sieci Web. W przeciwnym razie zwraca `$null`. |
| Subskrypcji kopii zapasowej |Zapisuje hello bieżącej subskrypcji platformy Azure w hello `$Script:originalSubscription` zmiennej w zakresie skryptu. Ta funkcja jest zapisywany hello bieżącej subskrypcji platformy Azure (uzyskanych przez `Get-AzureSubscription -Current`) i jego konta magazynu oraz hello subskrypcji, która zostanie zmieniona przez ten skrypt (przechowywana w zmiennej hello `$UserSpecifiedSubscription`), a jego konto magazynu w zakresie skryptu. Zapisując hello wartości można użyć funkcji, takich jak `Restore-Subscription`, toorestore hello oryginalnego bieżącej subskrypcji i magazynu toocurrent stan konta Jeśli hello bieżący stan został zmieniony. |
| Znajdź AzureVM |Pobiera hello określonej maszyny wirtualnej platformy Azure. |
| Format DevTestMessageWithTime |Dołącza wiadomość hello Data i godzina tooa. Ta funkcja jest przeznaczona dla komunikatów zapisanych toohello błąd i pełne strumieni. |
| Get-AzureSQLDatabaseConnectionString |Składana bazy danych Azure SQL tooan tooconnect ciąg połączenia. |
| Get-AzureVMStorage |Zwraca hello nazwę pierwszego konta magazynu hello mających wzorzec nazwy hello "devtest*" (bez uwzględniania wielkości liter) w określonej lokalizacji lub koligacji grupy hello. Jeśli hello "devtest*" hello lokalizacja lub grupa koligacji nie jest zgodna konta magazynu, funkcja hello ignoruje go. Należy określić lokalizację i grupę koligacji. |
| Get-MSDeployCmd |Zwraca narzędzie MsDeploy.exe hello toorun polecenia. |
| Nowe AzureVMEnvironment |Wyszukuje lub tworzy maszynę wirtualną w hello subskrypcji, która odpowiada wartości hello w pliku konfiguracji JSON hello. |
| Publikowanie WebPackage |Używa MsDeploy.exe i sieci web publikowania pakietu. ZIP pliku toodeploy zasobów tooa witryny sieci Web. Ta funkcja nie generuje żadnego wyniku. W przypadku niepowodzenia hello tooMSDeploy.exe wywołanie funkcji hello zgłasza wyjątek. tooget bardziej szczegółowe dane wyjściowe, użyj hello **-Verbose** opcji. |
| Publikowanie WebPackageToVM |Sprawdza, czy hello wartości parametrów, a następnie wywołuje hello **WebPackage publikowania** funkcji. |
| ConfigFile odczytu |Sprawdza poprawność pliku konfiguracji JSON hello i zwraca tablicy skrótów, wybranych wartości. |
| Przywracanie subskrypcji |Resetuje hello bieżącej subskrypcji toohello oryginalnego subskrypcji. |
| AzureModule testu |Zwraca `$true` w przypadku wersji modułu Azure hello zainstalowany 0.7.4 lub nowszym. Zwraca `$false` hello modułu nie jest zainstalowany lub jest starsza wersja. Ta funkcja nie ma parametrów. |
| AzureModuleVersion testu |Zwraca `$true` Jeśli wersja hello hello Azure modułu jest 0.7.4 lub nowszym. Zwraca `$false` hello modułu nie jest zainstalowany lub jest starsza wersja. Ta funkcja nie ma parametrów. |
| HttpsUrl testu |Konwertuje obiekt System.Uri tooa wejściowy adres URL hello. Zwraca `$True` Jeśli bezwzględny adres URL hello i jego schemat jest typu https. Zwraca `$false` hello adres URL jest względny, jego schematu nie HTTPS, czy hello ciąg wejściowy nie może być przekonwertowany tooa adresu URL. |
| Element członkowski testu |Zwraca `$true` Jeśli właściwość lub metoda jest elementem członkowskim obiektu hello. W przeciwnym razie zwraca `$false`. |
| ErrorWithTime zapisu |Zapisuje komunikat o błędzie z prefiksem hello bieżącego czasu. Ta funkcja wymaga hello **Format DevTestMessageWithTime** funkcja tooprepend hello czasu przed zapisaniem strumień błędów toohello wiadomość hello. |
| HostWithTime zapisu |Zapisuje komunikat toohello hosta programu (**Write-Host**) i jest poprzedzony prefiksem hello bieżący czas. efekt Hello zapisywania toohello hosta programu może być różna. Większość programów obsługujących środowiska Windows PowerShell zapisu te komunikaty toostandard danych wyjściowych. |
| VerboseWithTime zapisu |Zapisuje komunikat trybu informacji pełnej prefiksem hello bieżącego czasu. Ponieważ wywołuje **Write-Verbose**, wiadomość hello wyświetla tylko, gdy hello skrypt jest uruchamiany z hello **pełne** parametru lub gdy hello **VerbosePreference** jest preferencji Ustaw zbyt**Kontynuuj**. |

**Publikowanie aplikacji sieci Web**

| Nazwa funkcji | Opis |
| --- | --- |
| Nowe AzureWebApplicationEnvironment |Tworzy zasobów platformy Azure, takich jak witryny sieci Web lub maszyny wirtualnej. |
| Nowe WebDeployPackage |Ta funkcja nie jest zaimplementowana. Można dodać polecenia w tej funkcji toobuild projektu. |
| Publikowanie AzureWebApplication |Publikuje tooAzure aplikacji sieci web. |
| Publikowanie aplikacji sieci Web |Tworzy i wdraża aplikacje sieci Web, maszyn wirtualnych, baz danych i konta magazynu dla projektu sieci web programu Visual Studio. |
| Test-WebApplication |Ta funkcja nie jest zaimplementowana. Można dodać polecenia w tym tootest funkcji aplikacji. |

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat skryptów środowiska PowerShell, odczytując [skryptów programu Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) zobaczyć inne skrypty programu PowerShell systemu Azure w hello [Centrum skryptów](https://azure.microsoft.com/documentation/scripts/).
