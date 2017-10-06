---
title: "aaaCreate Azure role sieć web i procesu roboczego dla programu PHP | Dokumentacja firmy Microsoft"
description: "Przewodnik toocreating PHP sieci web i proces roboczy role usługi w chmurze Azure i konfigurowanie hello środowiska uruchomieniowego języka PHP."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>Jak toocreate role sieć web i proces roboczy języka PHP
## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób toocreate role sieci web lub procesu roboczego PHP w środowisku programowania Windows wybierz określonej wersji programu PHP z hello "wbudowanych" wersje dostępne, zmienić konfigurację PHP hello Włącz rozszerzenia i ponadto wdrożyć tooAzure. Opisano również sposób tooconfigure sieci web lub procesu roboczego roli toouse środowiska uruchomieniowego języka PHP (z konfiguracji niestandardowej i rozszerzenia) podane.

## <a name="what-are-php-web-and-worker-roles"></a>Co to są role sieć web i proces roboczy PHP?
Platforma Azure udostępnia trzy modele obliczeniowe na potrzeby uruchamiania aplikacji: Azure App Service, maszynach wirtualnych platformy Azure i usługi w chmurze Azure. Wszystkie trzy modele obsługują PHP. Usługi w chmurze, które obejmują role sieć web i proces roboczy, zapewnia *platforma jako usługa (PaaS)*. W ramach usługi w chmurze rola sieć web zapewnia dedykowanych sieci web usług Internet Information Services (IIS) aplikacji frontonu sieci web toohost serwera. Rola proces roboczy można uruchamiać asynchroniczne, długotrwałe lub ciągłe zadania niezależne interakcji z użytkownikiem lub danych wejściowych.

Aby uzyskać więcej informacji o tych opcjach, zobacz [obliczeniowe hosting opcji dostarczanych przez platformę Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Pobierz hello Azure SDK dla języka PHP
Witaj [zestaw Azure SDK for PHP] składa się z kilku składników. W tym artykule będzie korzystać z dwóch z nich: programu Azure PowerShell i hello emulatory platformy Azure. Te dwa składniki można zainstalować za pomocą Instalatora platformy sieci Web firmy Microsoft hello. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Tworzenie projektu usługi w chmurze
pierwszym krokiem Hello tworzenie roli sieci web lub procesu roboczego PHP jest toocreate projektu usługi Azure. projekt usługi Azure służy jako kontener logicznej dla sieci web i proces roboczy ról i zawiera projekt hello [definicji (csdef) usługi] i [konfiguracji usługi (cscfg)] plików.

toocreate nowego projektu usługi Azure, uruchom program Azure PowerShell jako administrator i wykonaj hello następujące polecenie:

    PS C:\>New-AzureServiceProject myProject

To polecenie spowoduje utworzenie nowego katalogu (`myProject`) toowhich można dodać role sieci web i proces roboczy.

## <a name="add-php-web-or-worker-roles"></a>Dodawanie ról PHP sieci web lub procesu roboczego
tooadd projektu tooa roli sieci web PHP, uruchom następujące polecenia w katalogu głównym projektu hello hello:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Dla roli proces roboczy Użyj tego polecenia:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Witaj `roleName` parametr jest opcjonalny. Jeśli zostanie pominięty, będą automatycznie generowane hello nazwy roli. Hello utworzone pierwszego rola sieci web będzie `WebRole1`, hello drugi będzie `WebRole2`i tak dalej. będzie Hello pierwszy roli proces roboczy utworzony `WorkerRole1`, hello drugi będzie `WorkerRole2`i tak dalej.
>
>

## <a name="specify-hello-built-in-php-version"></a>Określ hello wbudowanych wersji PHP
Po dodaniu PHP sieci web lub procesu roboczego roli tooa projektu pliki konfiguracji projektu hello są modyfikowane tak, aby PHP zostanie zainstalowana na każde wystąpienie w sieci web lub procesu roboczego aplikacji po jej wdrożeniu. Wersja hello toosee PHP instalowanego domyślnie, uruchom następujące polecenie hello:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Witaj dane wyjściowe polecenia hello powyżej będzie wyglądała podobnie toowhat są wyświetlane poniżej. W tym przykładzie hello `IsDefault` flaga jest ustawiona zbyt`true` dla programów PHP 5.3.17, i wskazujący będzie hello domyślne PHP wersji.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

Można ustawić hello PHP środowiska wykonawczego w wersji tooany hello wersji PHP, które są wyświetlane. Na przykład tooset wersji PHP hello (dla roli o nazwie hello `roleName`) too5.4.0, hello Użyj następującego polecenia:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Dostępne wersje PHP mogą ulec zmianie w przyszłych hello.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Dostosowywanie hello wbudowanych środowiska uruchomieniowego języka PHP
Masz pełną kontrolę nad hello konfigurację środowiska uruchomieniowego języka PHP hello zainstalowanego wykonanie kroków hello powyżej, w tym modyfikowanie `php.ini` ustawienia i włączania rozszerzeń.

toocustomize hello wbudowanych środowiska uruchomieniowego języka PHP, wykonaj następujące kroki:

1. Dodaj nowy folder o nazwie `php`, toohello `bin` katalogu swojej roli sieci web. Dla roli proces roboczy Dodaj ją toohello roli katalogu głównego.
2. W hello `php` folderu, utworzyć inny folder o nazwie `ext`. Umieszczaj żadnego `.dll` rozszerzenia plików (np. `php_mongo.dll`), które mają tooenable w tym folderze.
3. Dodaj `php.ini` pliku toohello `php` folderu. Włącz wszystkie rozszerzenia niestandardowe i ustaw wszystkie dyrektywy PHP w tym pliku. Na przykład, jeśli potrzebujesz tooturn `display_errors` na i Włącz hello `php_mongo.dll` rozszerzenia, zawartość hello Twojej `php.ini` pliku będzie następujące:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Wszystkie ustawienia, które nie zostanie jawnie ustawiona w hello `php.ini` pliku Podaj zostanie automatycznie można ustawić wartości domyślne tootheir. Jednak należy pamiętać, że można dodać pełnego `php.ini` pliku.
>
>

## <a name="use-your-own-php-runtime"></a>Użyć własnego środowiska uruchomieniowego języka PHP
W niektórych przypadkach, zamiast wybrać wbudowanych środowiska uruchomieniowego języka PHP i skonfigurować go, jak opisano powyżej może być tooprovide własnego środowiska uruchomieniowego języka PHP. Na przykład można użyć tego samego środowiska uruchomieniowego języka PHP w roli sieci web lub procesu roboczego używanego w środowisku projektowania hello. Dzięki temu można łatwiej tooensure aplikacji hello nie spowoduje zmiany zachowania w środowisku produkcyjnym.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Skonfiguruj toouse roli sieci web z własnego środowiska uruchomieniowego języka PHP
tooconfigure toouse roli sieci web środowiska uruchomieniowego języka PHP, które zapewniają, wykonaj następujące kroki:

1. Tworzenie projektu usługi Azure i Dodaj rolę sieci web PHP, jak opisano wcześniej w tym temacie.
2. Utwórz `php` folderu w hello `bin` folderu, który znajduje się w katalogu głównym roli sieci web, a następnie dodaj toohello środowiska uruchomieniowego (wszystkie pliki binarne, pliki konfiguracji, podfoldery itp.) z PHP `php` folderu.
3. (OPCJONALNIE) Jeśli Twojego środowiska uruchomieniowego języka PHP używa hello [Drivers firmy Microsoft dla programów PHP i SQL Server][sqlsrv drivers], konieczne będzie tooconfigure tooinstall roli sieci web [programu SQL Server Native Client 2012] [ sql native client] po zainicjowaniu obsługi administracyjnej. toodo, Dodaj hello [Instalator sqlncli.msi x64] toohello `bin` folderu w katalogu głównym roli sieci web. skryptu uruchomieniowego Hello opisany w następnym kroku hello uruchomi dyskretnej Instalatora hello po udostępnieniu hello roli. Jeśli Twojego środowiska uruchomieniowego języka PHP nie używa hello Drivers firmy Microsoft dla programu PHP dla programu SQL Server, należy usunąć hello następującego wiersza ze skryptu hello pokazano w następnym kroku hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Zdefiniuj zadanie uruchamiania, który konfiguruje [Internet Information Services (IIS)] [ iis.net] toouse Twojego toohandle środowiska uruchomieniowego PHP żądań dotyczących `.php` stron. toodo, otwórz hello `setup_web.cmd` pliku (w hello `bin` pliku katalog główny roli sieci web) w edytorze tekstów i zastąp jego zawartość z hello następujący skrypt:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Dodaj katalog główny aplikacji pliki tooyour roli sieci web firmy. Jest to katalog główny serwera sieci web hello.
6. Publikowanie aplikacji, zgodnie z opisem w hello [opublikować aplikację](#publish-your-application) poniższej sekcji.

> [!NOTE]
> Witaj `download.ps1` skryptu (w hello `bin` folder katalogu głównego roli sieci web hello) można usunąć po wykonaniu kroków hello opisane powyżej, aby przy użyciu własnego środowiska uruchomieniowego języka PHP.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Skonfiguruj toouse roli procesu roboczego własnego środowiska uruchomieniowego języka PHP
tooconfigure toouse roli procesu roboczego środowiska wykonawczego PHP, które zapewniają, wykonaj następujące kroki:

1. Tworzenie projektu usługi Azure i Dodaj rolę procesu roboczego PHP, jak opisano wcześniej w tym temacie.
2. Utwórz `php` folderu w katalogu głównym roli procesu roboczego hello, a następnie dodaj programu PHP toohello środowiska uruchomieniowego (wszystkie pliki binarne, pliki konfiguracji, podfoldery itp.) `php` folderu.
3. (OPCJONALNIE) Jeśli korzysta z Twojego środowiska uruchomieniowego języka PHP [Drivers firmy Microsoft dla programów PHP i SQL Server][sqlsrv drivers], konieczne będzie tooconfigure Twojego tooinstall roli procesu roboczego [programu SQL Server Native Client 2012] [ sql native client] po zainicjowaniu obsługi administracyjnej. toodo, Dodaj hello [Instalator sqlncli.msi x64] roli procesu roboczego toohello katalogu głównego. skryptu uruchomieniowego Hello opisany w następnym kroku hello uruchomi dyskretnej Instalatora hello po udostępnieniu hello roli. Jeśli Twojego środowiska uruchomieniowego języka PHP nie używa hello Drivers firmy Microsoft dla programu PHP dla programu SQL Server, należy usunąć hello następującego wiersza ze skryptu hello pokazano w następnym kroku hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Zdefiniuj zadanie uruchamiania, który dodaje użytkownika `php.exe` zmiennej środowiskowej PATH roli toohello pliku wykonywalnego procesu roboczego po udostępnieniu hello roli. toodo, otwórz hello `setup_worker.cmd` plików (w katalogu głównym roli procesu roboczego hello) w edytorze tekstów i zastąp jego zawartość hello następującego skryptu:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Dodaj katalog główny roli użytkownika aplikacji pliki tooyour procesu roboczego.
6. Publikowanie aplikacji, zgodnie z opisem w hello [opublikować aplikację](#publish-your-application) poniższej sekcji.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Uruchom aplikację w hello emulatory zasobów obliczeniowych i magazynu
Hello Azure emulatory Podaj lokalnego środowiska można przetestować aplikację Azure, przed wdrożeniem toohello chmury. Istnieją pewne różnice między hello emulatorów i hello środowiska platformy Azure. toounderstand to lepsze, zobacz [użyć emulatora magazynu Azure hello do projektowania i testowania](storage/common/storage-use-emulator.md).

Należy pamiętać, że użytkownik musi mieć PHP zainstalowane lokalnie emulatora obliczeń hello toouse. emulator obliczeń Hello będzie używać sieci lokalnej toorun instalacji PHP aplikacji.

wykonanie projektu w emulatory hello toorun hello następujące polecenie z katalogu głównego projektu:

    PS C:\MyProject> Start-AzureEmulator

Zostaną wyświetlone dane wyjściowe podobne toothis:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Widać działanie aplikacji w emulatorze hello przez otwarcie przeglądarki sieci web i przeglądanie toohello lokalny adres wyświetlany w danych wyjściowych hello (`http://127.0.0.1:81` hello przykład danych wyjściowych powyżej).

emulatory hello toostop, wykonanie tego polecenia:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Publikowanie aplikacji
toopublish aplikacji, należy importu toofirst Twojego ustawień publikowania za pomocą hello [AzurePublishSettingsFile importu](https://msdn.microsoft.com/library/azure/dn790370.aspx) polecenia cmdlet. Następnie można opublikować aplikację przy użyciu hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) polecenia cmdlet. Informacje logowania, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka PHP](/develop/php/).

[zestaw Azure SDK for PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definicji (csdef) usługi]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[konfiguracji usługi (cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[Instalator sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
