---
title: "aaaScript programowanie akcji z usługą HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize Hadoop clusters z akcji skryptu. Akcja skryptu można dodatkowe oprogramowanie używane tooinstall systemem Hadoop klastra lub toochange hello konfiguracji aplikacji instalowanych w klastrze."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Tworzenie skryptów akcji skryptu dla klastrów usługi HDInsight w systemie Windows
Dowiedz się, jak skrypty toowrite akcji skryptu dla usługi HDInsight. Uzyskać informacji na temat używania skryptów akcji skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md). Aby hello tego samego artykułu zapisywane w klastrach usługi HDInsight opartej na systemie Linux, zobacz [skryptów tworzenie akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Witaj czynnościach w ramach tego dokumentu działa tylko w przypadku klastrów usługi HDInsight opartej na systemie Windows. HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Uzyskać przy użyciu akcji skryptu z klastrów z systemem Linux, zobacz [programowanie akcji z usługą HDInsight (Linux) w skrypcie](hdinsight-hadoop-script-actions-linux.md).
>
>



Akcja skryptu można dodatkowe oprogramowanie używane tooinstall systemem Hadoop klastra lub toochange hello konfiguracji aplikacji instalowanych w klastrze. Akcje skryptu to skrypty, których uruchamianie w węzłach klastra hello w przypadku klastrów usługi HDInsight i są wykonywane po węzłach w klastrze hello Zakończ konfigurację usługi HDInsight. Akcja skryptu jest wykonywane w ramach uprawnień konta administratora systemu i zapewnia pełne prawa dostępu toohello węzłów klastra. Każdy klaster można podać listę skryptu toobe akcje wykonywane w kolejności hello, w którym zostały określone.

> [!NOTE]
> Jeśli wystąpią hello następujący komunikat o błędzie:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello termin "Zapisz HDIFile" nie został rozpoznany jako hello nazwę polecenia cmdlet, funkcji, pliku skryptu lub program wykonywalny. Sprawdź pisownię nazwy hello hello, lub jeśli ścieżki został uwzględniony, sprawdź, czy ścieżka tego hello jest poprawna i spróbuj ponownie.
> Istnieje, ponieważ nie zawiera metody pomocnicze hello.  Zobacz [metody pomocnicze dla niestandardowych skryptów](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Przykładowe skrypty
Do tworzenia klastrów usługi HDInsight w systemie operacyjnym Windows, hello akcji skryptu jest skrypt programu PowerShell systemu Azure. Witaj poniższy skrypt to przykład dla konfigurowania plików konfiguracji lokacji hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

skrypt Hello przyjmuje cztery parametry, nazwa pliku konfiguracji hello, właściwość hello ma toomodify, wartość hello tooset i opis. Na przykład:

    hive-site.xml hive.metastore.client.socket.timeout 90

Te parametry ustawia hello hive.metastore.client.socket.timeout wartość too90 w pliku gałęzi site.xml hello.  Witaj, wartość domyślna to 60 sekund.

Ten przykładowy skrypt można znaleźć w [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

Usługa HDInsight zapewnia kilka skryptów tooinstall dodatkowe składniki w klastrach HDInsight:

| Nazwa | Skrypt |
| --- | --- |
| **Zainstaluj Spark** |https://hdiconfigactions.blob.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1. Zobacz [instalacji i używania platformy Spark w usłudze HDInsight clusters][hdinsight-install-spark]. |
| **Zainstalować język R** |https://hdiconfigactions.blob.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1. Zobacz [instalacji i używania R w klastrach HDInsight][hdinsight-r-scripts]. |
| **Zainstaluj Solr** |https://hdiconfigactions.blob.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1. Zobacz [instalacji i używania Solr w usłudze HDInsight clusters](hdinsight-hadoop-solr-install.md). |
| - **Zainstaluj Giraph** |https://hdiconfigactions.blob.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1. Zobacz [instalacji i używania Giraph w usłudze HDInsight clusters](hdinsight-hadoop-giraph-install.md). |

Akcja skryptu można wdrożyć z hello portalu Azure, programu Azure PowerShell lub przy użyciu hello zestawu .NET SDK usługi HDInsight.  Aby uzyskać więcej informacji, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu][hdinsight-cluster-customize].

> [!NOTE]
> Witaj przykładowe skrypty działa tylko z klastra usługi HDInsight w wersji 3.1 lub nowszy. Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Metody pomocnicze dla niestandardowych skryptów
Metody pomocnicze akcji skryptu są narzędzia, które można użyć podczas pisania skryptów niestandardowych. Te metody są zdefiniowane w [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)i może być uwzględniony w użyciu hello następujące przykładowe skrypty:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Poniżej przedstawiono hello metody pomocnicze, które są udostępniane przez ten skrypt:

| Metoda pomocnika | Opis |
| --- | --- |
| **Zapisz HDIFile** |Pobierz plik z hello określonej lokalizacji tooa identyfikator URI (Uniform Resource) na dysku lokalnym hello skojarzony z hello maszyny Wirtualnej Azure węzła przypisanej toohello klastra. |
| **Rozwiń węzeł HDIZippedFile** |Rozpakuj plik z rozszerzeniem zip. |
| **Wywołanie HDICmdScript** |Uruchom skrypt z cmd.exe. |
| **HDILog zapisu** |Zapisywania danych wyjściowych z niestandardowego skryptu hello używanych w przypadku akcji skryptu. |
| **Get-Services** |Pobierz listę usługi działające na maszynie hello, w którym hello skrypt jest wykonywany. |
| **Get-Service** |O nazwie określonej usługi hello jako dane wejściowe, uzyskać szczegółowe informacje dla określonej usługi (nazwy usługi, przetworzyć identyfikator, stan, itp.) na maszynie hello gdzie hello skrypt jest wykonywany. |
| **Get-HDIServices** |Pobierz listę usług HDInsight działającego na komputerze hello, w którym hello skrypt jest wykonywany. |
| **Get-HDIService** |Przy hello HDInsight usługi nazwy określonej jako dane wejściowe, uzyskać szczegółowe informacje dla określonej usługi (nazwy usługi, przetworzyć identyfikator, stan, itp.) na maszynie hello gdzie hello skrypt jest wykonywany. |
| **Get-ServicesRunning** |Pobierz listę usług, które są uruchomione na komputerze hello, w którym hello skrypt jest wykonywany. |
| **Get-ServiceRunning** |Sprawdź, czy określonej usługi (według nazwy) jest uruchomiony na komputerze hello gdzie hello skrypt jest wykonywany. |
| **Get-HDIServicesRunning** |Pobierz listę usług HDInsight działającego na komputerze hello, w którym hello skrypt jest wykonywany. |
| **Get-HDIServiceRunning** |Sprawdź, czy określonej usługi HDInsight (według nazwy) jest uruchomiony na komputerze hello gdzie hello skrypt jest wykonywany. |
| **Get-HDIHadoopVersion** |Pobierz wersję hello Hadoop zainstalowany na komputerze hello gdzie hello skrypt jest wykonywany. |
| **IsHDIHeadNode testu** |Sprawdź, czy komputer hello gdzie hello skrypt jest wykonywany jest węzła głównego. |
| **IsActiveHDIHeadNode testu** |Sprawdź, czy komputer hello gdzie hello skrypt jest wykonywany jest aktywnego węzła głównego. |
| **IsHDIDataNode testu** |Sprawdź, czy komputer hello gdzie hello skrypt jest wykonywany jest węzeł danych. |
| **Edytuj HDIConfigFile** |Edytuj pliki konfiguracji hello hive-site.xml, core-site.xml, system plików hdfs-site.xml, mapred-site.xml lub yarn-site.xml. |

## <a name="best-practices-for-script-development"></a>Najlepsze rozwiązania dotyczące tworzenia skryptów
Podczas opracowywania niestandardowego skryptu dla klastra usługi HDInsight są kilka tookeep najlepszych praktyk pamiętać:

* Sprawdź, czy wersja Hadoop hello

    HDInsight w wersji 3.1 (Hadoop 2.4) lub nowszym obsługa przy użyciu akcji skryptu tooinstall niestandardowych składników w klastrze. W skrypcie niestandardowe, należy użyć hello **Get HDIHadoopVersion** pomocnika metody toocheck hello Hadoop wersji przed kontynuowaniem wykonywania innych zadań w skrypcie hello.
* Znajdują się stabilne łączy tooscript zasoby

    Upewnij się, wszystkie skrypty hello i innych artefaktów używane w dostosowania hello klastra pozostają dostępne przez cały okres istnienia hello hello klastra i hello wersje tych plików nie należy zmieniać na czas trwania hello użytkowników. Te zasoby są wymagane, jeśli hello ponownym węzłów w klastrze hello jest wymagana. Witaj, najlepszym rozwiązaniem jest toodownload i zarchiwizowanie wszystkich na koncie magazynu, który hello kontrolki użytkownika. Może to być hello domyślne konto magazynu lub dowolnym hello określone w chwili hello wdrożenia klastra dostosowane dodatkowych kont magazynu.
    W hello Spark i R dostosować klastra przykłady podane w dokumentacji hello, na przykład wprowadzono lokalną kopię hello zasobów tego konta magazynu: https://hdiconfigactions.blob.core.windows.net/.
* Upewnij się, że hello klastra dostosowywania skryptu jest idempotentności

    Należy oczekiwać, że hello węzłów klastra usługi HDInsight zostanie odtworzone z obrazu okres istnienia klastra hello. Witaj klastra dostosowania skrypt jest uruchamiany, gdy klaster zostanie odtworzone z obrazu. Ten skrypt musi być idempotentności toobe zaprojektowane w hello sensie, że po ponownej instalacji systemu, skrypt hello powinien zapewnić, że klastra hello jest zwracany toohello dostosowanej sam tuż po hello skryptu dla hello pierwszego uruchomienia podczas hello klastra został początkowo był w stanie utworzony. Na przykład, jeśli skryptu niestandardowego zainstalować aplikację na D:\AppLocation na pierwszym Uruchom, a następnie przy każdym uruchomieniu kolejne, po ponownym, skrypt hello należy sprawdzić, czy aplikacja hello istnieje na powitania D:\AppLocation lokalizacji przed kontynuowaniem z innymi kroki w skrypcie hello.
* Zainstaluj składniki niestandardowe w lokalizacji optymalne hello

    Jeśli węzły klastra są odtworzyć z obrazu, hello C:\ zasobów dysku i dysk systemowy D:\ można ponownie sformatowany, co grozi utratą hello danych i aplikacji, które były zainstalowane na tych dyskach. Może to również nastąpić, jeśli węzeł maszyny wirtualnej platformy Azure (VM), który jest częścią klastra hello ulegnie awarii i zostało zastąpione przez nowy węzeł. Składniki można zainstalować na dysku D:\ hello lub w lokalizacji C:\apps hello na powitania klastra. Wszystkich innych lokalizacji na dysku C:\ hello są zastrzeżone. Określ lokalizację hello gdzie biblioteki lub aplikacje są toobe zainstalowane w hello klastra dostosowywania skryptu.
* Zapewni to wysoką dostępność hello architektury klastra

    HDInsight ma architekturę aktywny / pasywny wysokiej dostępności, w których jednego węzła głównego jest w trybie aktywnym (w którym jest uruchamiana hello usługi HDInsight) i innych hello węzła głównego jest w trybie rezerwy (w którym HDInsight usługi nie działają). węzły Hello przełącznika tryby aktywnym i pasywnym, jeśli usługi HDInsight są przerywane. Akcja skryptu w przypadku usługi tooinstall używane na obu węzłach głównych wysokiej dostępności, należy pamiętać, że tego hello mechanizm pracy awaryjnej usługi HDInsight nie jest tooautomatically może zakończyć się niepowodzeniem przy użyciu tych usług zainstalowane przez użytkownika. Dlatego użytkownik zainstalował usługi na węzłach head HDInsight, które są oczekiwane toobe wysokiej dostępności musisz mieć własne mechanizm pracy awaryjnej w trybie aktywny / pasywny lub być w trybie aktywny / aktywny.

    Akcja skryptu HDInsight polecenie jest uruchamiane na obu węzłach głównych, gdy roli węzła head hello jest określona jako wartość hello *ClusterRoleCollection* parametru. Tak podczas projektowania niestandardowego skryptu, upewnij się, że skrypt jest świadome tego Instalatora. Nie należy uruchamiać na problemy z którym hello tej samej usługi są zainstalowane i uruchomione na obu węzłów head hello i ich przechodzili konkurujących ze sobą. Pamiętaj też, że dane zostały utracone podczas ponownej instalacji systemu, tak oprogramowania zainstalowanych za pomocą akcji skryptu ma toobe odporność toosuch zdarzeń. Aplikacje powinny być zaprojektowane toowork o wysokiej dostępności danych, który będzie rozmieszczona na wielu węzłach. Należy pamiętać, że maksymalnie 1/5 hello węzłów w klastrze mogą można odtworzyć z obrazu na powitania tym samym czasie.
* Konfigurowanie magazynu obiektów Blob platformy Azure toouse niestandardowych składników hello

    Hello niestandardowych składników, które należy zainstalować na węzłach klastra hello może być domyślny toouse konfiguracji magazynu systemu Distributed plików Hadoop (HDFS). Zamiast tego należy zmienić hello toouse konfiguracji magazynu obiektów Blob platformy Azure. Na klastrze odtworzenia z obrazu pobiera sformatowany w systemie plików HDFS hello i zostaną utracone wszystkie dane są przechowywane. Zamiast tego przy użyciu magazynu obiektów Blob platformy Azure zapewnia, że dane są przechowywane.

## <a name="common-usage-patterns"></a>Wspólne wzorce użycia
Ta sekcja zawiera wskazówki dotyczące implementowania niektóre hello typowe wzorce użycia, które możesz napotkać podczas pisania skryptu niestandardowego.

### <a name="configure-environment-variables"></a>Skonfiguruj zmienne środowiskowe
Często w rozwoju akcji skryptu, uważasz, że hello muszą tooset zmiennych środowiskowych. Na przykład najbardziej prawdopodobnym scenariuszem jest podczas pobierania pliku binarnego z witryny zewnętrznej, ją zainstalować w klastrze hello i Dodaj lokalizację hello, gdzie jest zmienna środowiskowa "PATH" tooyour zainstalowanych. powitania po fragment kodu przedstawia sposób tooset zmienne środowiskowe w hello skryptu niestandardowego.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Ta instrukcja ustawia zmienną środowiskową hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello wartość "true", a także ustawia hello zakresu tej zmiennej toobe komputera. W czasie ważne jest, że zmienne środowiskowe są ustawiane w zakresie odpowiedniego hello — komputera lub użytkownika. Zobacz [tutaj] [ 1] Aby uzyskać więcej informacji na temat ustawiania zmiennych środowiskowych.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Gdzie są przechowywane niestandardowe skrypty hello toolocations dostępu
Skrypty używane toocustomize tooeither potrzeb klastra można hello domyślne konto magazynu dla klastra hello lub publicznego kontenera tylko do odczytu na inne konto magazynu. Jeśli skrypt uzyskuje dostęp do zasobów znajdujących się w innym miejscu te czynności toobe w publicznie dostępnym (co najmniej publiczne tylko do odczytu). Na przykład może tooaccess pliku i zapisz go przy użyciu polecenia hello SaveFile HDI.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

W tym przykładzie musisz zapewnić, że kontenera "somecontainer" na koncie magazynu "somestorageaccount" hello jest dostępny publicznie. W przeciwnym razie hello skrypt zgłasza wyjątek nie znaleziono i zakończyć się niepowodzeniem.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Polecenie cmdlet Add-AzureRmHDInsightScriptAction toohello parametry do przekazania
toopass wiele parametrów polecenia cmdlet toohello Dodaj AzureRmHDInsightScriptAction, należy toocontain wartość ciąg hello tooformat wszystkie parametry dla hello skryptu. Na przykład:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

lub

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Zgłoszenie wyjątku dla wdrożenia klastra nie powiodło się
Wtedy, gdy tooget dokładnie powiadomienie faktu hello dostosowywania tego klastra nie powiodła się zgodnie z oczekiwaniami, jest ważne toothrow wyjątek i niepowodzenie hello tworzenia klastra. Na przykład możesz mają tooprocess pliku, jeśli istnieje i obsługę w przypadku błędu hello, gdzie hello plik nie istnieje. Może to zapewnić hello skrypt zakończy pracę bezpiecznie i hello stan klastra hello poprawnie jest znany. Witaj następujący fragment kodu przedstawiono przykładowy sposób tooachieve to:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

W tym fragmencie Jeśli hello plik nie istnieje, jej doprowadziłoby stanu tooa gdzie skryptu hello faktycznie opuszcza bezpiecznie po wydrukowaniu komunikat o błędzie hello i klastra hello osiągnie uruchomiona przy założeniu, że "pomyślnie" ukończyć procesu dostosowywania klastra. Wtedy, gdy toobe dokładnie powiadomienie faktu hello dostosowywania tego klastra zasadniczo nie powiodło się zgodnie z oczekiwaniami ze względu na Brak pliku, jest bardziej odpowiednia toothrow wyjątek i niepowodzenie kroku dostosowania klastra hello. tooachieve to hello następującego fragmentu kodu przykładowej zamiast tego należy użyć.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Lista kontrolna wdrażania akcji skryptu
Poniżej przedstawiono kroki hello Wybraliśmy podczas przygotowywania toodeploy te skrypty:

1. Umieść hello pliki, które zawierają hello niestandardowych skryptów w miejscu, który jest dostępny dla węzłów klastra hello podczas wdrażania. Może to być domyślny hello lub dodatkowych kont magazynu określony w momencie hello wdrożenie klastra lub innych kontenera magazynu publicznie.
2. Dodaj kontroli do skryptów toomake się upewnić, że są one wykonywane idempotently, tak, aby skrypt hello mogą być wykonywane wiele razy na powitania tym samym węźle.
3. Użyj hello **Write-Output** tooSTDOUT tooprint polecenia cmdlet programu Azure PowerShell, a także STDERR. Nie używaj **Write-Host**.
4. Użyj folder plików tymczasowych, takich jak $env: TEMP, tookeep hello pobrany plik używany przez skrypty hello, a następnie wyczyść je po wykonaniu skryptów.
5. Zainstaluj oprogramowanie niestandardowe tylko na D:\ lub C:\apps. Nie należy używać innych lokalizacji na dysku C: hello są one zastrzeżone. Należy pamiętać, że instalowanie plików na dysku C: hello poza folderem C:\apps hello może spowodować błędy instalacji podczas reimages hello węzła.
6. W przypadku hello zostały zmienione ustawienia na poziomie systemu operacyjnego lub plików konfiguracyjnych usługi Hadoop możesz toorestart usługi HDInsight, dzięki czemu użytkownik może wybrać wszystkie ustawienia poziomu systemu operacyjnego, takich jak hello zmienne środowiskowe w hello skryptów.

## <a name="debug-custom-scripts"></a>Debugowanie skryptów niestandardowych
dzienniki błędów skryptu Hello są przechowywane wraz z innymi dane wyjściowe w hello domyślnego konta magazynu określony dla hello klastra podczas jego tworzenia. Witaj dzienniki są przechowywane w tabeli o nazwie hello *u < \cluster-name-fragment >< \time-stamp > setuplog*. Są to dzienniki zagregowane, które rekordy z wszystkich węzłów hello (węzła głównego i węzły procesów roboczych) na które hello skrypt jest uruchamiany w klastrze hello.
Łatwe toocheck hello dzienników jest toouse HDInsight Tools dla programu Visual Studio. Do zainstalowania narzędzia hello, zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**toocheck hello dziennika za pomocą programu Visual Studio**

1. Otwórz program Visual Studio.
2. Kliknij przycisk **widoku**, a następnie kliknij przycisk **Eksploratora serwera**.
3. Kliknij prawym przyciskiem myszy "Azure", kliknij przycisk Połącz za**subskrypcji platformy Microsoft Azure**, a następnie wprowadź swoje poświadczenia.
4. Rozwiń węzeł **magazynu**, rozwiń konto usługi Azure storage hello używany jako domyślny system plików hello, rozwiń węzeł **tabel**, a następnie kliknij dwukrotnie nazwę tabeli hello.

Możesz również zdalnego do toosee węzłów klastra hello zarówno STDOUT i STDERR niestandardowych skryptów. Witaj dzienniki w każdym węźle są określonego węzła tylko toothat i logują się do **C:\HDInsightLogs\DeploymentAgent.log**. Te pliki dziennika rejestrować wszystkie dane wyjściowe z hello niestandardowego skryptu. Przykład fragment dziennika akcji skryptu Spark wygląda następująco:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


W tym dzienniku jest jasne, czy wykonano akcji skryptu Spark hello na powitania maszyny Wirtualnej o nazwie HEADNODE0 i że nie zwrócono wyjątek podczas wykonywania hello.

W zdarzeniu hello, która występuje błąd wykonania dane wyjściowe hello opisujące go również znajduje się w tym pliku dziennika. Witaj informacji dostępnych w tych dziennikach powinna być pomocnych w debugowaniu problemów skryptu, które mogą wystąpić.

## <a name="see-also"></a>Zobacz też
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]
* [Zainstalować i używać platformy Spark w usłudze hdinsight][hdinsight-install-spark]
* [Zainstaluj i użyj języka R w klastrach HDInsight][hdinsight-r-scripts]
* [Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install.md).
* [Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
