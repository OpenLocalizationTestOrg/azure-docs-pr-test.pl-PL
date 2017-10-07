---
title: "aaaAzure aplikacji aranżacji poprawki usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Tooautomate aplikacji działających w systemie stosowanie poprawek w klastrze usługi sieć szkieletowa usług."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Poprawka systemu operacyjnego Windows hello w klastrze usługi sieć szkieletowa

Witaj poprawki aranżacji aplikacja jest aplikacji sieci szkieletowej usług Azure, która automatyzuje systemu operacyjnego stosowanie poprawek w klastrze usługi sieć szkieletowa usług Azure bez przestoju.

Aplikacja orchestration poprawki Hello zapewnia następujące hello:

- **Instalacja aktualizacji automatycznych systemu operacyjnego**. Automatycznie pobierania i instalowania aktualizacji systemu operacyjnego. Węzły klastra są ponownie uruchamiane zgodnie z potrzebami bez przestoju klastra.

- **Typu cluster-aware integracji stosowanie poprawek i kondycji**. Podczas stosowania aktualizacji, aplikacja orchestration poprawki hello monitoruje kondycję hello hello węzłów klastra. Węzły klastra są uaktualnionego jeden węzeł lub domeny uaktualnienia pojedynczo. Jeśli kondycji hello klastra hello przestanie działać z powodu toohello proces stosowania poprawek, poprawki jest zatrzymany tooprevent obciążające hello problem.

## <a name="internal-details-of-hello-app"></a>Szczegóły wewnętrznych aplikacji hello

Aplikacja orchestration poprawki Hello składa się z hello następujące składniki podrzędne:

- **Usługa koordynatora**: tej usługi stanowej jest odpowiedzialny za:
    - Koordynowanie zadanie aktualizacji systemu Windows hello na powitania całego klastra.
    - Przechowywanie wyniku hello ukończone operacje usługi Windows Update.
- **Usługa agenta węzła**: tej usługi bezstanowej działa we wszystkich węzłach klastra sieci szkieletowej usług. Witaj, usługa jest odpowiedzialna za:
    - Uruchamianie hello NTService agenta węzła.
    - Monitorowanie hello NTService agenta węzła.
- **Węzeł agenta NTService**: Usługa ta systemu Windows NT jest uruchamiana na wyższym poziomie uprawnień (SYSTEM). Z kolei hello Usługa agenta węzła i hello koordynatorem działać na niższym poziomie uprawnienia (Usługa sieciowa). Usługa Hello jest wykonuje następujące zadania usługi Windows Update na wszystkich węzłach klastra hello hello:
    - Wyłączanie automatycznej aktualizacji systemu Windows w węźle hello.
    - Zgodnie z toohello zasad hello użytkownik udostępnił pobieranie i instalowanie aktualizacji systemu Windows.
    - Ponowne uruchamianie hello maszyny po instalacji usługi Windows Update.
    - Przekazywanie hello wyniki toohello aktualizacje systemu Windows usługi koordynatora.
    - Raporty dotyczące raportowania kondycji, w przypadku, gdy operacja nie powiodła się po wykorzystaniu ponawiania prób.

> [!NOTE]
> Hello poprawki aranżacji aplikacja używa hello sieci szkieletowej usług naprawy Menedżera systemu usługi toodisable lub Włącz hello węzła i sprawdzania kondycji. zadanie naprawy Hello utworzone przez hello poprawki aranżacji aplikacja ścieżki hello postęp aktualizacji systemu Windows dla każdego węzła.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="minimum-supported-service-fabric-runtime-version"></a>Minimalna obsługiwana wersja środowiska uruchomieniowego platformy Service Fabric

#### <a name="azure-clusters"></a>Klastry platformy Azure
Witaj poprawki aranżacji aplikacji musi być uruchamiane na Azure klastrów, które mają wersji środowiska uruchomieniowego platformy Service Fabric w wersji 5.5 lub nowszego.

#### <a name="standalone-on-premises-clusters"></a>Autonomiczny lokalnymi klastrów
Witaj poprawki aranżacji aplikacji musi być uruchamiane na autonomicznych klastrów się v5.6 wersji środowiska uruchomieniowego platformy Service Fabric lub nowszym.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Włącz usługę Menedżer naprawy hello (Jeśli nie jest już uruchomiona)

Witaj poprawki aranżacji aplikacja wymaga hello naprawy Menedżera systemu usługi toobe włączona w klastrze hello.

#### <a name="azure-clusters"></a>Klastry platformy Azure

Azure klastrów w warstwie srebrny trwałości hello ma hello napraw program service manager domyślnie włączone. Azure klastrów w warstwie gold trwałości hello może lub nie mieć hello naprawy Menedżera usługi w zależności od tego, kiedy te klastry zostały utworzone. Azure klastrów w warstwie brązową trwałości hello, domyślnie nie mają hello napraw włączona usługa menedżera. Jeśli usługa hello jest już włączony, widoczny będzie działać w sekcji usług systemu hello hello Service Fabric Explorer.

##### <a name="azure-portal"></a>Azure Portal
Napraw manager z portalu Azure można włączyć w czasie hello konfigurowania klastra. Wybierz `Include Repair Manager` opcję w obszarze `Add on features` w czasie hello konfiguracji klastra.
![Obraz Menedżera naprawy włączenie z portalu Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Szablon usługi Azure Resource Manager
Możesz też użyć hello [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello naprawy Menedżera usługi na nowych i istniejących klastrów sieci szkieletowej usług. Pobierz szablon hello hello klastra, które mają toodeploy. Można użyć hello przykładowych szablonów lub utworzyć niestandardowy szablon usługi Resource Manager. 

tooenable hello naprawy Menedżera usługi przy użyciu [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Najpierw sprawdź, że hello `apiversion` ustawiono zbyt`2017-07-01-preview` dla hello `Microsoft.ServiceFabric/clusters` zasobów, jak pokazano w hello następującego fragmentu. Jeśli jest inny, a następnie należy tooupdate hello `apiVersion` toohello wartość `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Teraz włączyć hello naprawy Menedżera usługi, dodając następujące hello `addonFeatures` sekcji po hello `fabricSettings` sekcji:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Po zaktualizowaniu szablonu klastra wprowadzone zmiany ich zastosowania i umożliwić zakończenie uaktualniania hello. Możesz teraz przeglądać hello naprawy Menedżera systemu usługa jest uruchomiona w klastrze. Jest to `fabric:/System/RepairManagerService` w sekcji usług systemu hello hello Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Autonomiczny lokalnymi klastrów

Można użyć hello [ustawienia konfiguracji dla klastra systemu Windows autonomiczny](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello naprawy Menedżera usługi na nowych i istniejących klastra sieci szkieletowej usług.

Usługa Menedżera naprawy hello tooenable:

1. Najpierw sprawdź, że hello `apiversion` w [konfiguracje klastrów ogólne](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) ustawiono zbyt`04-2017` lub nowszy:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Teraz włączyć naprawy Menedżera usługi, dodając następujące hello `addonFeaturres` sekcji po hello `fabricSettings` sekcji, jak pokazano poniżej:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Zaktualizuj manifeście klastra za pomocą tych zmian, za pomocą hello zaktualizować manifestu klastra [Utwórz nowy klaster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) lub [konfiguracji klastra hello uaktualnienia](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Po hello klastra został uruchomiony z manifestu klastra zaktualizowane, można przeglądać hello naprawy Menedżera systemu usługa jest uruchomiona w klastrze, która jest wywoływana `fabric:/System/RepairManagerService`w obszarze części hello Eksploratora usługi sieć szkieletowa usług systemowych.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Wyłącz automatyczną aktualizację systemu Windows na wszystkich węzłach

Aktualizacje automatyczne systemu Windows może prowadzić utraty tooavailability, ponieważ wiele węzłów klastra można ponownie uruchomić na powitania sam czas. Aplikacja orchestration poprawki Hello, domyślnie toodisable prób hello automatycznej aktualizacji systemu Windows w każdym węźle klastra. Jednak jeśli hello ustawienia są zarządzane przez administratora lub zasad grupy, zaleca się ustawienie hello zasad zbyt "powiadamiania przed pobraniem" jawnie usługi Windows Update.

### <a name="optional-enable-azure-diagnostics"></a>Opcjonalnie: Włącz diagnostyki Azure

Klastry z systemem wersja środowiska uruchomieniowego platformy Service Fabric `5.6.220.9494` i loguje się powyżej Dzienniki aplikacji aranżacji zbieranie poprawki w ramach sieci szkieletowej usług.
Ten krok można pominąć, jeśli klaster jest uruchomiony na wersji środowiska uruchomieniowego platformy Service Fabric `5.6.220.9494` i powyżej.

W przypadku klastrów wersja środowiska uruchomieniowego platformy Service Fabric mniej niż `5.6.220.9494`, dzienniki aplikacji aranżacji poprawki hello są gromadzone lokalnie na każdym z węzłów klastra hello.
Zaleca się skonfigurowanie diagnostyki Azure dzienniki tooupload wszystkie węzły tooa centralnej lokalizacji.

Aby uzyskać informacje na temat włączania diagnostyki Azure, zobacz [zbierania dzienników przy użyciu diagnostyki Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Dzienniki hello poprawki aranżacji aplikacji są generowane na powitania po stałej dostawcy identyfikatory:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

W instrukcji goto szablonu usługi Resource Manager `EtwEventSourceProviderConfiguration` w obszarze `WadCfg` i Dodaj hello następujące wpisy:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Jeśli klaster sieci szkieletowej usług ma wiele typów węzeł, a następnie hello w poprzedniej sekcji, należy dodać do wszystkich hello `WadCfg` sekcje.

## <a name="download-hello-app-package"></a>Pobierz pakiet aplikacji hello

Pobieranie aplikacji hello z hello [pobrać link](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Konfigurowanie aplikacji hello

Witaj zachowanie hello poprawki aranżacji aplikacji może być skonfigurowany toomeet potrzeb. Zastąpić wartości domyślne hello przez przekazywanie parametrów aplikacji hello podczas tworzenia aplikacji lub aktualizacji. Można podać parametry aplikacji, określając `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` lub `New-ServiceFabricApplication` polecenia cmdlet.

|**Parametr**        |**Typ**                          | **Szczegóły**|
|:-|-|-|
|MaxResultsToCache    |Długie                              | Maksymalna liczba wyników aktualizacji systemu Windows, które mają być buforowane. <br>Wartość domyślna to 3000 zakładając, że: <br> -Liczba węzłów to 20. <br> -Liczba aktualizacji pojawia się w węźle miesięcznie wynosi pięć. <br> -Liczba wyników dla operacji może być 10. <br> — Powinny być przechowywane wyniki hello ostatnich trzech miesięcy. |
|TaskApprovalPolicy   |wyliczenia <br> {NodeWise, UpgradeDomainWise}                          |TaskApprovalPolicy wskazuje hello zasady, które jest używane przez aktualizacje systemu Windows tooinstall koordynatorem hello na węzłach klastra usługi sieć szkieletowa hello toobe.<br>                         Dozwolone wartości to: <br>                                                           <b>NodeWise</b>. Windows Update jest zainstalowany jeden węzeł naraz. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update jest zainstalowanych domeny uaktualnienia pojedynczo. (Na powitania maksymalnej, dla usługi Windows Update można przejść wszystkie węzły hello należących do domeny uaktualnienia tooan).
|LogsDiskQuotaInMB   |Długie  <br> (Domyślnie: 1024)               |Maksymalny rozmiar poprawki aplikacji aranżacji loguje MB, co może trwale znajdować się lokalnie w węzłach.
| WUQuery               | Ciąg<br>(Domyślnie: "IsInstalled = 0")                | Zapytanie tooget aktualizacje systemu Windows. Aby uzyskać więcej informacji, zobacz [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)
| InstallWindowsOSOnlyUpdates | wartość logiczna <br> (domyślne: True)                 | Ta flaga umożliwia system operacyjny zainstalowany toobe aktualizacje systemu Windows.            |
| WUOperationTimeOutInMinutes | int <br>(Domyślnie: 90).                   | Określa limit czasu hello do żadnej operacji usługi Windows Update (wyszukiwania lub pobierania lub instalacji). Jeśli operacja hello nie zostało ukończone w ciągu hello określony limit czasu, jest zostało przerwane.       |
| WURescheduleCount     | int <br> (Domyślne: 5).                  | Hello maksymalną liczbę razy hello zmienia harmonogram hello usługi Windows update w przypadku, gdy operacja trwale kończy się niepowodzeniem.          |
| WURescheduleTimeInMinutes | int <br>(Domyślnie: 30). | Interwał powitania, w których hello usługi zmienia harmonogram aktualizacji systemu Windows hello w przypadku, gdy błąd będzie się powtarzać. |
| WUFrequency           | Ciąg rozdzielony przecinkami (domyślne: "Co tydzień, środę, 7:00:00")     | częstotliwość Hello instalacji usługi Windows Update. Witaj format i możliwe wartości to: <br>— Co miesiąc, DD gg, na przykład, co miesiąc, 5, 12: 22:32. <br> — Gg co tydzień i dzień, na przykład, co tydzień, Wtorek, 12:22:32.  <br> -Codziennie, ss, na przykład codziennie, 12:22:32.  <br> -Wskazuje brak, nie można wykonać aktualizacji systemu Windows.  <br><br> Należy pamiętać, że cały czas hello są w formacie UTC.|
| AcceptWindowsUpdateEula | wartość logiczna <br>(Domyślnie: true) | Ustawiając tę flagę aplikacji hello akceptuje hello użytkownika końcowego licencji umowy dla usługi Windows Update w imieniu właściciela hello hello maszyny.              |

> [!TIP]
> Jeśli chcesz od razu toohappen usługi Windows Update, ustaw `WUFrequency` czasu wdrożenia aplikacji toohello względną. Na przykład załóżmy, że ma pięcioma węzłami klastra i plan toodeploy hello aplikacji testów przy około 17:00:00 czasu UTC. Jeśli założono, że wdrożenie lub uaktualniania aplikacji hello ma 30 minut w hello maksymalna, ustaw hello WUFrequency jako "Codziennie, 17:30:00."

## <a name="deploy-hello-app"></a>Wdrażanie aplikacji hello

1. Zakończ wszystkie hello wstępnie wymagane kroki tooprepare hello klastra.
2. Wdróż hello poprawki aranżacji aplikacji, takich jak każda inna aplikacja usługi Service Fabric. Aplikacja hello można wdrożyć przy użyciu programu PowerShell. Wykonaj kroki hello w [Wdróż i usunąć aplikacje przy użyciu programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. tooconfigure aplikacji hello w czasie hello wdrożenia, hello przebiegu `ApplicationParamater` toohello `New-ServiceFabricApplication` polecenia cmdlet. Dla wygody przygotowaliśmy hello skryptu Deploy.ps1 wraz z aplikacji hello. skrypt hello toouse:

    - Połącz klaster sieci szkieletowej usług tooa przy użyciu `Connect-ServiceFabricCluster`.
    - Wykonanie skryptu PowerShell hello Deploy.ps1 hello odpowiednie `ApplicationParameter` wartość.

> [!NOTE]
> Utrzymaj hello hello skrypt i folder aplikacji hello PatchOrchestrationApplication tym samym katalogu.

## <a name="upgrade-hello-app"></a>Uaktualnienie aplikacji hello

tooupgrade istniejącej aplikacji aranżacji poprawki przy użyciu programu PowerShell, wykonaj kroki hello w [uaktualniania aplikacji sieci szkieletowej usług za pomocą programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Usuwanie aplikacji hello

Aplikacja hello tooremove, wykonaj kroki hello w [Wdróż i usunąć aplikacje przy użyciu programu PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Dla wygody przygotowaliśmy hello skryptu Undeploy.ps1 wraz z aplikacji hello. skrypt hello toouse:

  - Połącz klaster sieci szkieletowej usług tooa przy użyciu ```Connect-ServiceFabricCluster```.

  - Uruchom skrypt programu PowerShell hello Undeploy.ps1.

> [!NOTE]
> Utrzymaj hello hello skrypt i folder aplikacji hello PatchOrchestrationApplication tym samym katalogu.

## <a name="view-hello-windows-update-results"></a>Wyświetl wyniki aktualizacji systemu Windows hello

Aplikacja orchestration poprawki Hello uwidacznia interfejsów API REST toodisplay hello historycznymi toohello użytkownika. Przykład Witaj wyniku JSON:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Jeśli aktualizacja nie jest jeszcze zaplanowane, wynik hello JSON jest pusta.

Zaloguj się za toohello tooquery klastra usługi Windows Update wyników. Dowiedz się hello repliki adres podstawowy hello hello koordynatorem i trafień hello URL z przeglądarki hello: http://&lt;IP REPLIKI&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

punkt końcowy REST Hello hello koordynatorem ma portów dynamicznych. toocheck hello dokładny adres URL, zobacz toohello Service Fabric Explorer. Na przykład wyniki hello są dostępne pod adresem `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Obraz końcowy REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Hello zwrotnego serwera proxy jest włączona w klastrze hello, można uzyskać dostępu do adresu URL hello z poza również hello klastra.
Witaj punktu końcowego, który wymaga toobe trafień jest http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

tooenable hello zwrotnego serwera proxy na powitania klastra, wykonaj kroki hello w [odwrotny serwer proxy w sieci szkieletowej usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Po skonfigurowaniu hello zwrotnego serwera proxy, wszystkie usługi micro hello klastra, które ujawniać punkt końcowy HTTP adresowane z poza hello klastra.

## <a name="diagnosticshealth-events"></a>Diagnostyka kondycji zdarzenia

### <a name="collect-patch-orchestration-app-logs"></a>Aplikacja orchestration poprawki zbieranie dzienników

Dzienniki aplikacji aranżacji poprawki są zbierane w ramach dzienników sieci szkieletowej usług z wersji środowiska uruchomieniowego `5.6.220.9494` i powyżej.
W przypadku klastrów wersja środowiska uruchomieniowego platformy Service Fabric mniej niż `5.6.220.9494`, dzienniki mogą być zbierane przy użyciu jednej z następujących metod hello.

#### <a name="locally-on-each-node"></a>Lokalnie na każdym węźle

Dzienniki są gromadzone lokalnie na każdym węźle klastra sieci szkieletowej usług w przypadku wersji środowiska uruchomieniowego usługi sieć szkieletowa usług mniej niż `5.6.220.9494`. Witaj dzienniki hello tooaccess lokalizacji jest \[sieci szkieletowej usług\_instalacji\_dysków\]:\\PatchOrchestrationApplication\\dzienniki.

Na przykład, jeśli usługa sieć szkieletowa jest zainstalowany na dysku D, ścieżka hello jest D:\\PatchOrchestrationApplication\\dzienniki.

#### <a name="central-location"></a>Centralnej lokalizacji

Jeśli diagnostyki Azure jest skonfigurowany jako część wstępnie wymagane kroki, dzienniki hello poprawki aranżacji aplikacji są dostępne w usłudze Azure Storage.

### <a name="health-reports"></a>Raportów o kondycji

Aplikacja orchestration poprawki Hello publikuje również raportów o kondycji względem hello koordynatorem lub hello Usługa agenta węzła w hello w następujących przypadkach:

#### <a name="a-windows-update-operation-failed"></a>Operacja usługi Windows Update, nie powiodła się

W przypadku niepowodzenia operacji usługi Windows Update w węźle raport o kondycji jest generowany przed hello węzła usługi agenta. Szczegóły hello raport o kondycji zawiera nazwy węzła problematyczne hello.

Po pomyślnym węzła problematyczne hello zakończeniu stosowanie poprawek, raport hello są automatycznie usuwane.

#### <a name="hello-node-agent-ntservice-is-down"></a>Witaj NTService agenta węzła nie działa

Jeśli hello NTService agenta węzeł nie działa w węźle, przed hello Usługa agenta węzła generowany jest raport o kondycji poziom ostrzeżeń.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>Usługa Menedżera naprawy Hello nie jest włączona

Jeśli hello naprawy Menedżera usługi nie zostanie znaleziony w klastrze hello, zostanie wygenerowany raport dotyczący kondycji poziom ostrzeżeń hello usługę koordynatora.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

Q. **Dlaczego wyświetlać Mój klastra w stanie błędu, gdy aplikacja orchestration poprawki hello jest uruchomiona?**

A. W procesie instalacji hello aplikacja orchestration poprawki hello wyłącza lub ponownego uruchomienia węzłów, które mogą skutkować tymczasowo kondycji hello klastra hello przechodzi w dół.

Na podstawie hello zasad dla aplikacji hello, albo jeden węzeł może przejść w dół podczas operacji stosowania poprawek *lub* całej domeny uaktualnienia można przestaną działać jednocześnie.

Końca hello hello instalacji usługi Windows Update powitalne węzły są reenabled po ponownym uruchomieniu.

W hello poniższy przykład klaster hello zakończył się, że stan błędu tooan tymczasowo ponieważ dwa węzły zostały w dół i hello MaxPercentageUnhealthNodes zasad zostało naruszone. Błąd Hello jest tymczasowy do momentu hello poprawki operacja jest wykonywana.

![Obraz zła klastra](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Jeśli hello problem będzie się powtarzać, zapoznaj się toohello sekcji rozwiązywania problemów.

Q. **Aplikacja orchestration poprawki jest w stanie ostrzeżenia**

A. Sprawdź toosee, jeśli raport o kondycji zaksięgowany względem aplikacji hello hello główną przyczynę. Zazwyczaj ostrzeżenie hello zawiera szczegółowe informacje o problemie hello. W przypadku przejściowy problem hello aplikacji hello jest oczekiwany Odzyskaj tooauto z tego stanu.

Q. **Co można zrobić, jeśli mojego klastra jest zła i toodo aktualizację pilnych systemu operacyjnego jest potrzebna?**

A. Aplikacja orchestration poprawki Hello nie można zainstalować aktualizacji podczas klastra hello jest zła. Spróbuj toobring klastra tooa dobrej kondycji toounblock hello poprawki aranżacji aplikacji przepływu pracy.

Q. **Dlaczego poprawki w klastrach podąża tak długo toorun?**

A. Hello czas potrzebny aplikacji aranżacji poprawki hello zależy przede wszystkim hello następujące czynniki:

- zasady Hello hello usługę koordynatora. 
  - Witaj domyślne zasady `NodeWise`, powoduje stosowanie poprawek tylko jeden węzeł naraz. Szczególnie w przypadku hello większe klastry, zalecane jest użycie hello `UpgradeDomainWise` tooachieve zasad szybsze poprawki w klastrach.
- Witaj liczba dostępnych do pobrania i zainstalowania aktualizacji. 
- Witaj toodownload Średni czas potrzebny i zainstalować aktualizację, który nie powinien przekraczać po kilku godzinach.
- Witaj wydajności hello maszyny Wirtualnej i przepustowość sieci.

Q. **Dlaczego widzę niektórych aktualizacji w wynikach usługi Windows Update uzyskany za pośrednictwem interfejsu api REST, ale nie w ramach hello historii usługi Windows Update na komputerze?**

A. Niektóre aktualizacje produktu muszą toobe zaewidencjonowany historii odpowiednich aktualizacji/poprawki. Przykład: Usługa Windows Defender aktualizacje nie są wyświetlane w historii usługi Windows Update w systemie Windows Server 2016.

## <a name="disclaimers"></a>Zastrzeżenia

- Aplikacja orchestration poprawki Hello akceptuje hello użytkownika końcowego licencji umowy z usługi Windows Update w imieniu użytkownika hello. Opcjonalnie ustawienie hello, można wyłączyć w konfiguracji hello aplikacji hello.

- Aplikacja orchestration poprawki Hello zbiera dane telemetryczne tootrack użycia i wydajności. dane telemetryczne aplikacji Hello następuje ustawienie hello ustawienia telemetrii hello sieci szkieletowej usług runtime, (która jest domyślnie włączona).

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="a-node-is-not-coming-back-tooup-state"></a>Węzeł jest nie powracające tooup stanu

**węzeł Hello mogła zostać zablokowana na wyłączenie stanu, ponieważ**:

Trwa oczekiwanie na sprawdzenie bezpieczeństwa. tooremedy tej sytuacji, upewnij się, że wystarczającej liczby węzłów są dostępne w dobrej kondycji.

**węzeł Hello mogła zostać zablokowana w stanie wyłączenia, ponieważ**:

- Witaj węzeł został wyłączony ręcznie.
- węzeł Hello został wyłączony z powodu tooan zadania trwającą infrastruktury platformy Azure.
- węzeł Hello zostało wyłączone tymczasowo przez hello poprawki aranżacji aplikacji toopatch hello węzła.

**Hello węzeł może zostać zatrzymane w stanie down ponieważ**:

- węzeł Hello została umieszczona w stanie down ręcznie.
- węzeł Hello jest w trakcie ponownego uruchomienia (które może zostać wyzwolone przez hello poprawki aranżacji aplikacji).
- węzeł Hello jest wyłączony powodu tooa błędny maszyny Wirtualnej lub maszyny lub sieci problemy z połączeniem.

### <a name="updates-were-skipped-on-some-nodes"></a>Aktualizacje zostały pominięte na niektóre węzły

Aplikacja orchestration poprawki Hello próbuje tooinstall zasad systemu Windows update zgodnie z toohello planowaniem mogą. Usługa Hello próbuje toorecover hello węzła i Pomiń hello aktualizacji zgodnie z toohello aplikacji zasad.

W takim przypadku raport dotyczący kondycji poziom ostrzeżeń jest generowany przed hello węzła usługi agenta. wynik Hello aktualizacji systemu Windows zawiera także hello możliwych przyczyn niepowodzenia hello.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>kondycji Hello klastra hello przechodzi tooerror podczas instalacji aktualizacji hello

Błędny usługi Windows update można obniżyć hello kondycji aplikacji lub klastra w określonym węźle lub domena uaktualnienia. Aplikacja orchestration poprawki Hello zaprzestaje wszelkie kolejne operacje usługi Windows Update, dopóki hello klastra jest w dobrej kondycji ponownie.

Administrator musi interweniować i ustalić, dlaczego aplikacja hello lub klastra stał się nieprawidłowy, ponieważ tooWindows aktualizacji.

## <a name="release-notes-"></a>Informacje o wersji:

### <a name="version-110"></a>Wersja 1.1.0
- Publiczny zlecenia

### <a name="version-111"></a>Wersja 1.1.1
- Rozwiązane usterki w SetupEntryPoint z NodeAgentService uniemożliwiający instalacji NodeAgentNTService.

### <a name="version-120-latest"></a>Wersji 1.2.0 (Najnowsza wersja)

- Poprawki błędów wokół systemu ponownie uruchomić przepływ pracy.
- Poprawka błędu podczas tworzenia zadania RM powodu sprawdzenie kondycji toowhich podczas przygotowywania zadań naprawy nie pojawia się zgodnie z oczekiwaniami.
- Zmienione hello tryb uruchamiania usługi windows POANodeSvc z automatycznego toodelayed-auto.
