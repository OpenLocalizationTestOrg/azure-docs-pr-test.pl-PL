---
title: "Automation DSC ciągłego wdrażania z Chocolatey aaaAzure | Dokumentacja firmy Microsoft"
description: "DevOps ciągłe wdrażanie przy użyciu usługi Konfiguracja DSC automatyzacji Azure i Menedżer pakietów Chocolatey.  Przykład pełny szablon JSON ARM i źródła programu PowerShell."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Przykład użycia: TooVirtual ciągłe wdrażanie komputerów przy użyciu usługi Konfiguracja DSC automatyzacji i Chocolatey
W świecie DevOps istnieje wiele tooassist narzędzia z różnych punktach w potoku ciągłej integracji hello.  Konfiguracji usługi Azure Automation pożądanej stanu (DSC) są powitalnej opcje toohello nowe dodawania, korzystających DevOps zespołów.  W tym artykule przedstawiono ustawienia zapasowej ciągłego wdrażania (CD) na komputerze z systemem Windows.  Można z łatwością rozszerzyć hello technika tooinclude dowolną liczbę komputerów z systemem Windows w razie potrzeby hello roli (na przykład witryną sieci web) i z tooadditional występują również ról.

![Ciągłe wdrażanie dla maszyn wirtualnych IaaS](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>Na wysokim poziomie
Jest dość bit przejściem tutaj, ale na szczęście można można podzielić na dwie główne procesy: 

* Pisanie kodu i testowanie go, następnie tworzenia i publikowania pakietów instalacyjnych wersję główną i pomocniczą hello systemu. 
* Tworzenie i zarządzanie nimi maszyn wirtualnych, które będzie zainstalować i wykonywać kod hello pakietów hello.  

Po obu tych procesów core znajdują się w miejscu, jest krótki krok tooautomatically pakiet aktualizacji programu hello działający żadnej określonej maszyny Wirtualnej jako nowe wersje są tworzone i wdrażane.

## <a name="component-overview"></a>Informacje o składniku
Takich jak pakiet menedżerów [stanie get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) są bardzo dobrze znanych Witaj świecie Linux, ale nie tak wiele Witaj świecie systemu Windows.  [Chocolatey](https://chocolatey.org/) jest takie operacją i Scott Hanselman [blogu](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) na powitania tematu jest doskonałym wprowadzenie.  Mówiąc Chocolatey pozwala tooinstall pakietów z centralnym repozytorium pakietów w systemie Windows hello wiersza polecenia.  Można tworzyć i zarządzać własną repozytorium i Chocolatey mogą instalować pakiety z dowolnej liczby repozytoria, które określisz.

Żądany stan konfiguracji (DSC) ([omówienie](https://technet.microsoft.com/library/dn249912.aspx)) jest narzędziem programu PowerShell, które pozwala toodeclare hello konfiguracji maszyny.  Na przykład można powiedzieć "Chcę Chocolatey zainstalowany, I ma zainstalowane usługi IIS, chcę, aby otworzyć port 80, ma wersję 1.0.0 witryny sieci Web zainstalowany."  Witaj DSC lokalny program Configuration Manager (LCM) implementuje tę konfigurację. Serwerem ściągania usługi Konfiguracja DSC przechowuje repozytorium konfiguracji maszyn. Hello LCM na każdej maszynie, sprawdza w okresowo toosee, jeśli jego konfiguracja odpowiada hello przechowywanej konfiguracji. Jego zgłoszenia stanu lub spróbować toobring hello maszyny do dostosowania hello przechowywanej konfiguracji. Można edytować hello przechowywanej konfiguracji na powitania ściągania serwer toocause maszynę lub zbiór toocome maszyny do dostosowania z konfiguracją hello zmienione.

Automatyzacja Azure jest usługą zarządzanej platformie Microsoft Azure, która pozwala tooautomate różne zadania przy użyciu elementów runbook, węzłów, poświadczenia, zasobów i zasoby, takie jak harmonogramów i zmiennych globalnych. Konfiguracja DSC automatyzacji Azure rozszerza ta Automatyzacja możliwości tooinclude DSC środowiska PowerShell narzędzia.  W tym miejscu jest doskonałym [omówienie](automation-dsc-overview.md).

Zasób DSC jest modułu kodu, który ma określonych funkcji, takich jak zarządzanie sieci, w usłudze Active Directory lub programu SQL Server.  Hello Chocolatey zasobów DSC wie jak tooaccess serwer NuGet (między innymi), Pobierz pakiety, zainstalować pakiety i tak dalej.  Istnieją inne zasoby usługi Konfiguracja DSC w hello [galerii programu PowerShell](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Te moduły są zainstalowane na serwerze ściągania usługi Konfiguracja DSC automatyzacji Azure (przez użytkownika) dzięki mogą być używane w konfiguracji.

Szablony Menedżera zasobów zapewnić deklaratywne generowania infrastruktury - np. sieci, podsieci, zabezpieczeń sieci i routingu, obciążenia równoważenia, karty sieciowe, maszyn wirtualnych i tak dalej.  Oto [artykułu](../azure-resource-manager/resource-manager-deployment-model.md) czy porównuje hello modelu wdrażania usługi Resource Manager (deklaratywne) z hello Azure Service Management (ASM lub classic) wdrożenia modelu (imperatywne) i w tym artykule omówiono hello core zasobów dostawców, obliczeń, magazynu i sieci.

Jedną z kluczowych funkcji szablonu usługi Resource Manager jest jej tooinstall możliwość rozszerzenia maszyny Wirtualnej, na powitania maszyny Wirtualnej, zgodnie z jego obsługa została zainicjowana.  Rozszerzenia maszyny Wirtualnej ma określone funkcje takie jak uruchamianie skryptu niestandardowego, instalowanie oprogramowania antywirusowego lub uruchomienie skryptu konfiguracji DSC.  Istnieje wiele typów rozszerzeń maszyny Wirtualnej.

## <a name="quick-trip-around-hello-diagram"></a>Szybkie podróży wokół hello diagramu
Zaczynając od góry hello, wpisz swój kod, kompilacji i testowania, a następnie utworzyć pakiet instalacji.  Chocolatey może obsługiwać różne typy pakietów instalacyjnych, takich jak ZIP MSI, MSU.  I masz hello pełną moc rzeczywista instalacja hello toodo programu PowerShell, jeśli Chocolatey w macierzystym możliwości nie jest dość się tooit.  Pakiet hello należy umieścić w innym dostępny — z repozytorium pakietów.  W tym przykładzie użycie używane folderu publicznego w ramach konta magazynu obiektów blob platformy Azure, ale może być dowolnym miejscu.  Chocolatey natywnie współpracuje z serwerów NuGet i kilka innych metadane pakietów zarządzania.  [W tym artykule](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) opisano opcje hello.  W tym przykładzie użycie używane NuGet.  Plik Nuspec jest metadane dotyczące pakietów.  Hello Nuspec "kompilowania", do jego NuPkg i zapisane na serwerze NuGet.  Podczas konfiguracji żądania pakietu według nazwy i odwołuje się do serwera NuGet, hello Chocolatey zasobów DSC (teraz na powitania maszyny Wirtualnej) grabs hello pakietu i instaluje je automatycznie.  Możesz również poprosić o określonej wersji pakietu.

W hello lewej dolnej części obraz powitania ma szablonu usługi Azure Resource Manager (ARM).  W tym przykładzie użycie hello rozszerzenia maszyny Wirtualnej rejestruje hello maszyny Wirtualnej z serwera ściągania usługi Konfiguracja DSC automatyzacji Azure (czyli serwera ściągania) hello jako węzeł.  Konfiguracja Hello jest przechowywana na serwerze ściągania hello.  W rzeczywistości jest ona przechowywana dwa razy: raz w postaci zwykłego tekstu i po skompilowany jako plik MOF (dla tych, które wiedzieć o takich elementów.)  W portalu hello hello MOF jest "konfiguracja węzła" (w przeciwieństwie toosimply "Konfiguracja").  Jego hello artefaktu, który został skojarzony z węzłem, więc węzeł hello wiedzą, jego konfiguracji.  Szczegóły poniżej przedstawiono, jak tooassign hello węzła toohello konfiguracji węzła.

Prawdopodobnie już robimy bit hello u góry hello lub większość z nich.  Tworzenie hello nuspec, kompilowania i przechowywanie ich w serwerze NuGet jest mała operacją.  I będziesz już zarządzać maszynami wirtualnymi.  Biorąc hello następny krok toocontinuous wdrożenia wymaga konfigurowania serwera ściągania hello (raz), zarejestrowani węzły (raz), tworzenie i przechowywania konfiguracji hello (początkowo).  Następnie pakiety uaktualnienia i wdrożone toohello repozytorium Odśwież hello konfiguracji i konfiguracja węzła na serwerze ściągania hello (Powtórz w razie potrzeby).

Jeśli nie jest uruchamiany z szablonu usługi ARM, który również jest OK.  Brak toohelp poleceń cmdlet przeznaczone PowerShell rejestrowanie maszyn wirtualnych z serwera ściągania hello i wszystkie pozostałe hello. Aby uzyskać więcej informacji, zobacz ten artykuł: [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Krok 1: Skonfigurowanie konta serwera i automatyzacji ściągania hello
Uwierzytelniony wiersza polecenia programu PowerShell (Add-AzureRmAccount): (może zająć kilka minut hello ściągania serwer jest skonfigurowany)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Możesz też zaznaczyć Twoje konto usługi Automatyzacja w każdym hello następujące regiony (alias lokalizacja): wschodnie stany USA 2, południowo-środkowe stany Virginia nam wersji dla instytucji rządowych, Europa Zachodnia, Azja południowo-wschodnia, Japonia Wschodnia, Indie środkowe i Australia Południowo-Wschodnia, Kanada centralnej, Europa Północna, Europa.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Krok 2: Rozszerzenia maszyny Wirtualnej ulepszeń toohello szablon ARM
Szczegóły rejestracji maszyny Wirtualnej (przy użyciu rozszerzenia maszyny Wirtualnej DSC środowiska PowerShell hello) podane w tym [szablonie Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Ten krok rejestruje nowej maszyny Wirtualnej z serwera ściągania hello hello listy węzłów DSC.  Część tej rejestracji jest określenie hello węzła konfiguracji toobe stosowane toohello węzła.  Ta konfiguracja węzła nie ma tooexist jeszcze na serwerze ściągania hello, dlatego jest OK, który krok 4 jest, gdzie jest to wykonywane powitania po raz pierwszy.  Jednak w tym miejscu w kroku 2 należy toohave hello określona nazwa węzła hello i hello Nazwa konfiguracji hello.  W tym przykładzie użycie węzeł hello jest "isvbox" i konfiguracja hello jest "ISVBoxConfig".  Dlatego nazwa konfiguracji węzła hello (określony w DeploymentTemplate.json toobe) jest "ISVBoxConfig.isvbox".  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Krok 3: Dodawanie wymagane serwera ściągania usługi Konfiguracja DSC zasobów toohello
Witaj galerii programu PowerShell jest instrumentowanych tooinstall DSC zasobów na koncie usługi Automatyzacja Azure.  Przejdź toohello zasobów i kliknij przycisk "Wdróż tooAzure automatyzacji" hello.

![Przykład galerii programu PowerShell](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Innej techniki ostatnio dodane toohello Azure Portal umożliwia toopull w nowych modułów lub aktualizację istniejącego modułów. Kliknij hello konta automatyzacji zasobów, hello kafelka zasoby, a na końcu hello modułów kafelka.  ikony galerii przeglądania Hello umożliwia toosee hello listę modułów w galerii hello, przejść do szczegółów i ostatecznie zaimportować na koncie automatyzacji. To jest tookeep doskonały sposób moduły się toodate z tootime czasu. I zależności z innych tooensure modułów, które nie jest niezsynchronizowana sprawdza hello importu funkcji.

Lub brak hello ręcznej metody.  struktury folderów Hello modułu integracji programu PowerShell na komputerze z systemem Windows jest nieco inne niż struktury folderów hello oczekiwany przez hello usługi Automatyzacja Azure.  Wymaga to niewielkiej je ze strony użytkownika.  Ale nie jest trudne i jest wykonywane tylko raz dla zasobów (chyba że chcesz tooupgrade go w przyszłości.)  Aby uzyskać więcej informacji dotyczących tworzenia moduły integracji programu PowerShell, zobacz ten artykuł: [tworzenia moduły integracji dla usługi Automatyzacja Azure](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* Zainstaluj moduł hello potrzebnym na stacji roboczej:
  * Zainstaluj [Windows Management Framework v5](http://aka.ms/wmf5latest) (nie wymagane dla systemu Windows 10)
  * `Install-Module –Name MODULE-NAME`< — chwyty hello modułu na podstawie hello galerii programu PowerShell 
* Kopiuj hello modułu folder z `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa folderu tymczasowego 
* Usuń z folderu głównego hello przykłady i dokumentacja 
* ZIP hello głównego folderu nazewnictwa plików ZIP hello dokładnie takie same hello jako hello folder 
* Umieść plik ZIP hello w dostępny lokalizacji HTTP, takie jak magazyn obiektów blob na koncie magazynu Azure.
* Uruchom to środowiska PowerShell:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

przykład Witaj uwzględnione wykonuje te kroki dla cChoco i xNetworking. Zobacz hello [uwagi](#notes) dla specjalnej obsługi dla cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Krok 4: Dodawanie serwera ściągania toohello hello węzła konfiguracji
Nie ma specjalnych o powitania po raz pierwszy importowania konfiguracji na serwerze ściągania hello i kompilacji.  Wszystkie kolejne import/kompiluje z hello wyglądają tak samo konfiguracji dokładnie hello takie same.  Zawsze aktualizacji pakietu i wymagają toopush go tooproduction wykonaniu tego kroku po sprawdzeniu hello plik konfiguracji jest poprawny — tym hello nowej wersji pakietu.  Poniżej przedstawiono plik konfiguracji hello i programu PowerShell:

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Wynik te czynności w nowej konfiguracji węzła o nazwie "ISVBoxConfig.isvbox" na serwerze ściągania hello.  Nazwa konfiguracji węzła Hello jest tworzone w postaci "configurationName.nodeName".

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Krok 5: Tworzenie i obsługę metadane pakietów
Dla każdego pakietu, który można umieścić w repozytorium pakietów hello należy nuspec, zawierającego jego opis.  Ten plik nuspec musi być skompilowany i przechowywane na serwerze NuGet. Ten proces jest opisany [tutaj](http://docs.nuget.org/create/creating-and-publishing-a-package).  MyGet.org służy jako serwer NuGet.  One sprzedaży tej usługi, ale ma początkowego jednostka SKU, które jest aktualnie wolne.  W NuGet.org znajdują się instrukcje dotyczące instalowania NuGet serwera dla pakietów prywatnych.

## <a name="step-6-tying-it-all-together"></a>Krok 6: Łącząc go wszystkie razem
Za każdym razem wersję przekazuje odpowiedzi na pytania i została zatwierdzona wdrożenia pakietów hello jest tworzony, nuspec nupkg zaktualizowane i wdrożyć serwer NuGet toohello.  Ponadto hello konfiguracji (krok 4 powyżej) musi być zaktualizowany tooagree z hello nowego numeru wersji.  Musi być wysyłane z serwera ściągania toohello i skompilowany.  Od tego momentu jest zapasowych toohello maszyn wirtualnych, które są zależne od tej konfiguracji toopull hello aktualizacji, a następnie zainstaluj go.  Wszystkie te aktualizacje są proste — tylko wiersz lub dwóch programu PowerShell.  W przypadku hello Visual Studio Team Services niektóre z nich są hermetyzowane w zadania kompilacji, które można połączyć ze sobą w kompilacji.  To [artykułu](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery) zawiera więcej szczegółowych informacji.  To [repozytorium GitHub](https://github.com/Microsoft/vso-agent-tasks) szczegóły hello różne zadania dostępne kompilacji.

## <a name="notes"></a>Uwagi
W tym przykładzie użycie rozpoczyna się od maszyny Wirtualnej z ogólny obraz systemu Windows Server 2012 R2 z hello galerii Azure.  Możesz rozpocząć od żadnego obrazu przechowywane, a następnie dostosować stamtąd hello konfiguracji DSC.  Jednak zmiany konfiguracji, który jest rozszerzania obrazu jest trudniejsze niż dynamicznie aktualizowania konfiguracji hello przy użyciu usługi Konfiguracja DSC.

Nie masz toouse szablonu usługi ARM i toouse rozszerzenia maszyny Wirtualnej hello ta technika maszyn wirtualnych.  I maszyny wirtualne nie są toobe na toobe Azure w obszarze Zarządzanie dysku CD.  Wszystko jest niezbędna jest zainstalowany ten Chocolatey i hello LCM skonfigurowane na powitania maszyny Wirtualnej będzie wówczas traktował, gdzie hello ściągania serwer jest.  

Oczywiście po zaktualizowaniu pakietu na maszynie Wirtualnej, który znajduje się w środowisku produkcyjnym należy tootake tej maszyny Wirtualnej poza obrotu podczas instalowania aktualizacji hello.  Jak to zrobić różni.  Na przykład z maszyną Wirtualną za usługą równoważenia obciążenia Azure, możesz dodać, niestandardowe sondowania.  Podczas aktualizowania hello maszyna wirtualna, ma punktu końcowego sondowania hello powrócić 400.  niezbędne toocause dostrajał Hello tej zmiany mogą być wewnątrz konfiguracji, można hello tooswitch dostrajał go utworzyć kopię tooreturning 200 po ukończeniu aktualizacji hello.

Pełne źródło w tym przykładzie użycie znajduje się w [tego projektu programu Visual Studio](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) w witrynie GitHub.

## <a name="related-articles"></a>Pokrewne artykuły
* [Przegląd usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md)
* [Polecenia cmdlet systemu Azure Automation DSC](https://msdn.microsoft.com/library/mt244122.aspx)
* [Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)

