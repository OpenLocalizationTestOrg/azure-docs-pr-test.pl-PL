---
title: "aaaUsing Elasticsearch jako magazyn śledzenia aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wykorzystania aplikacji usługi Service Fabric toostore Elasticsearch i Kibana, indeksu i wyszukiwania za pomocą śladów aplikacji (Dzienniki)"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Przechowywanie Elasticsearch używany jako śledzenia aplikacji sieci szkieletowej usług
## <a name="introduction"></a>Wprowadzenie
W tym artykule opisano sposób [sieć szkieletowa usług Azure](https://azure.microsoft.com/documentation/services/service-fabric/) aplikacje mogą używać **Elasticsearch** i **Kibana** dla magazynu śledzenia aplikacji, indeksowanie i wyszukiwanie. [Elasticsearch](https://www.elastic.co/guide/index.html) jest open source, rozproszone i skalowalne w czasie rzeczywistym wyszukiwania i analiza mechanizm, który dobrze nadaje się do tego zadania. Można go zainstalować na maszynach wirtualnych Windows i Linux, działają na platformie Microsoft Azure. Elasticsearch wydajnie może przetwarzać *strukturalnych* śladów utworzone przy użyciu technologii, takich jak **funkcji Śledzenie zdarzeń systemu Windows ()**.

ETW jest używany przez usługi sieć szkieletowa środowiska uruchomieniowego toosource informacje diagnostyczne (śladów). Jest to hello ich informacje diagnostyczne, metoda toosource aplikacji sieci szkieletowej usług są zalecane zbyt. Przy użyciu powitalne sam mechanizm umożliwia korelacji między dostarczone przez środowisko uruchomieniowe i aplikacja dostarczona śladów i sprawia, że rozwiązania problemu. Interfejs API rejestrowania obejmują szablony projektów sieci szkieletowej usług w programie Visual Studio (oparte na powitania .NET **EventSource** klasy) który emituje śladów ETW. domyślnie. Ogólne omówienie aplikacji usługi Service Fabric śledzenia przy użyciu funkcji ETW, zobacz [monitorowania i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Witaj śladów tooshow się w Elasticsearch muszą one toobe zarejestrowane w węzłach klastra usługi sieć szkieletowa hello w czasie rzeczywistym (gdy jest uruchomiona aplikacja hello) i wysyłane do punktu końcowego Elasticsearch tooan. Dostępne są dwie główne opcje do przechwytywania śledzenia:

* **W procesie przechwytywania śledzenia**  
  Aplikacja Hello lub dokładnie procesu usługi, jest odpowiedzialny za wysyłanie hello danych diagnostycznych toohello śledzenia magazynu (Elasticsearch).
* **Przechwytywanie śledzenia poza procesem.**  
  Oddzielnym agentem jest przechwytywanie śladów pochodzących z procesu usługi hello lub procesów i wysyłania ich toohello śledzenia magazynu.

Poniżej opisano sposób tooset się Elasticsearch na platformie Azure. omówiono w nim specjaliści hello i wad dla obu opcji przechwytywania i wyjaśniają, jak tooconfigure usługi sieć szkieletowa usług toosend tooElasticsearch danych.

## <a name="set-up-elasticsearch-on-azure"></a>Konfigurowanie Elasticsearch na platformie Azure
Witaj najprostszy sposób tooset hello Elasticsearch usługi na platformie Azure jest za pośrednictwem [ **szablonów usługi Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Zaawansowane [szablon szybkiego startu usługi Azure Resource Manager dla Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) jest dostępna z repozytorium szablonów Szybki Start Azure. Ten szablon używa oddzielny magazyn kont dla jednostki skali (grupy węzłów). Można również udostępniać, klienckim oddzielnie i węzły serwera z różnymi konfiguracjami oraz różne numery dyskach danych dołączonych.

W tym miejscu korzystamy z innego szablonu, nazywane **ES MultiNode** z hello [repozytorium Azure narzędzia diagnostyczne](https://github.com/Azure/azure-diagnostics-tools). Ten szablon jest łatwiejsze toouse i tworzy klaster Elasticsearch zabezpieczone przy użyciu podstawowego uwierzytelniania HTTP. Przed kontynuowaniem pobrać hello repozytorium GitHub tooyour maszyny (przez klonowanie repozytorium hello lub pobieranie pliku zip). Szablon Hello ES MultiNode znajduje się w folderze hello z hello tej samej nazwy.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Przygotowanie toorun maszyny Elasticsearch skrypty instalacyjne
Witaj Najprostszym sposobem toouse hello ES MultiNode szablonu jest za pośrednictwem dostarczonego skryptu programu PowerShell systemu Azure o nazwie `CreateElasticSearchCluster`. toouse ten skrypt należy tooinstall moduły programu PowerShell i narzędzie **openssl**. ostatnie Hello jest niezbędny do utworzenia klastra Elasticsearch kluczem SSH, które mogą być używane tooadminister zdalnie.

`CreateElasticSearchCluster`skrypt jest przeznaczona dla łatwość użycia z szablonem hello ES MultiNode z komputera z systemem Windows. Jest to możliwe toouse hello szablon na komputerze z systemem innym niż Windows, ale w tym scenariuszu wykracza poza zakres tego artykułu hello.

1. Jeśli ich nie zainstalowano już, zainstaluj [ **modułów programu Azure PowerShell**](http://aka.ms/webpi-azps). Po wyświetleniu monitu kliknij przycisk **Uruchom**, następnie **zainstalować**. Program Azure PowerShell 1.3 lub nowszy jest wymagany.
2. Witaj **openssl** narzędzie jest dostępne w dystrybucji hello [ **Git dla systemu Windows**](http://www.git-scm.com/downloads). Jeśli jeszcze tego nie zrobiono, zainstaluj [Git dla systemu Windows](http://www.git-scm.com/downloads) teraz. (opcje instalacji domyślna hello są OK).
3. Przy założeniu, że Git został zainstalowany, ale nie jest uwzględniony w ścieżce systemowej hello, Otwórz okno programu Microsoft Azure PowerShell i uruchom następujące polecenia hello:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Zastąp hello `<Git installation folder>` z lokalizacji Git hello na tym komputerze; domyślnie hello jest **"C:\Program Files\Git"**. Należy zwrócić uwagę średnika hello na początku hello hello pierwszy ścieżki.
4. Upewnij się, że użytkownik jest zalogowany tooAzure (za pośrednictwem [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet) i wybrano hello subskrypcji, która powinna być używana toocreate klastra elastycznej wyszukiwania. Można sprawdzić, czy wybrano poprawną subskrypcję za pomocą `Get-AzureRmContext` i `Get-AzureRmSubscription` polecenia cmdlet.
5. Jeśli jeszcze tego nie zrobiono tego wcześniej, zmień bieżący folder katalogu toohello ES MultiNode hello.

### <a name="run-hello-createelasticsearchcluster-script"></a>Uruchom skrypt CreateElasticSearchCluster hello
Przed uruchomieniem skryptu hello Otwórz hello `azuredeploy-parameters.json` pliku Sprawdź i podaj wartości parametrów skryptu hello. dostępne są następujące parametry Hello:

| Nazwa parametru | Opis |
| --- | --- |
| dnsNameForLoadBalancerIP |Nazwa Hello jest używane toocreate hello widocznego publicznie nazwy DNS dla klastra elastycznej wyszukiwania hello (przez dodanie hello regionu Azure domeny toohello podane nazwy). Na przykład jeśli wartość tego parametru jest "myBigCluster" hello wybrany region platformy Azure to zachodnie stany USA, hello wynikowej nazwy DNS dla klastra hello jest myBigCluster.westus.cloudapp.azure.com. <br /><br />Ta nazwa służy również jako nazwa główna dla wielu artefakty skojarzone z klastrem elastycznej wyszukiwania hello, takich jak nazwy węzła danych. |
| adminUsername |nazwę Hello konta administratora hello Zarządzanie klastrem elastycznej wyszukiwania hello (odpowiadające im klucze SSH wygenerowaniu automatycznie). |
| dataNodeCount |Hello liczba węzłów w klastrze elastycznej wyszukiwania hello. Bieżąca wersja Hello hello skryptu nie rozróżnia między węzłami danych i zapytania. wszystkie węzły odtworzyć obie role. Węzły too3 wartości domyślnych. |
| dataDiskSize |rozmiar Hello dysków danych (w GB) przypisany do każdego węzła danych. Każdy węzeł odbiera 4 dyski danych wyłącznie dedykowanych tooElastic usługi wyszukiwania. |
| Region |Nazwa Hello region platformy Azure, gdzie powinien być zlokalizowany hello elastycznej wyszukiwania klastra. |
| esUserName |Witaj nazwa użytkownika hello użytkownika, która jest skonfigurowana toohave dostępu tooES klastra (podmiotu tooHTTP uwierzytelniania podstawowego). Witaj hasło nie jest częścią pliku parametrów i należy podać podczas `CreateElasticSearchCluster` skrypt zostanie wywołany. |
| vmSizeDataNodes |Witaj rozmiar maszyny wirtualnej platformy Azure dla węzłów klastra elastycznej wyszukiwania. TooStandard_D2 wartości domyślnych. |

Teraz wszystko jest gotowe toorun hello skryptu. Problem hello następujące polecenie:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

gdzie 

| Nazwa parametru skryptu | Opis |
| --- | --- |
| `<es-group-name>` |Nazwa Hello hello grupy zasobów platformy Azure, która będzie zawierać wszystkich zasobów klastra elastycznej wyszukiwania. |
| `<azure-region>` |Nazwa Hello hello region platformy Azure, w którym ma zostać utworzony hello elastycznej wyszukiwania klastra. |
| `<es-password>` |hasło Hello hello elastycznej wyszukiwania użytkownika. |

> [!NOTE]
> Jeśli otrzymasz NullReferenceException z polecenia cmdlet Test-AzureResourceGroup hello pamiętasz toolog na tooAzure (`Add-AzureRmAccount`).
> 
> 

Jeśli wystąpi błąd uruchamiania skryptu hello i określeniu błąd hello spowodowane przez wartość parametru szablonu niewłaściwy, popraw hello parametru plik i ponownie uruchomić skrypt hello nazwę grupy zasobów w innej. Można również wykorzystać hello tej samej nazwy grupy zasobów i mieć skryptu hello oczyszczania hello stary przez dodanie hello `-RemoveExistingResourceGroup` wywołanie skryptu toohello parametru.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Wynik uruchomienia skryptu CreateElasticSearchCluster hello
Po uruchomieniu hello `CreateElasticSearchCluster` skryptu hello następujące główne artefakty zostanie utworzony. W tym przykładzie przyjęto założenie, czy użyto "myBigCluster" jako wartości hello hello `dnsNameForLoadBalancerIP` parametr i hello regionu, w którym utworzono klaster hello jest zachodnie stany USA.

| Artefaktów | Nazwa, lokalizacja i uwagi |
| --- | --- |
| Klucz SSH dla administracji zdalnej |Plik myBigCluster.key (w katalogu hello, z których hello CreateElasticSearchCluster zostało uruchomione). <br /><br />Ten plik klucza może być używane tooconnect toohello admin węzła (za pośrednictwem węzła admin hello) toodata węzłów w klastrze hello. |
| Węzeł administratora |myBigCluster admin.westus.cloudapp.azure.com <br /><br />Dedykowane maszyny Wirtualnej dla zdalnego administrowania klastrami Elasticsearch — Witaj tylko jeden, który zezwala na zewnętrzne połączenia SSH. Jest uruchamiany na powitania tej samej sieci wirtualnej jako wszystkie węzły klastra Elasticsearch hello, ale nie nie uruchomienia wszystkie usługi Elasticsearch. |
| Węzły danych |myBigCluster1... myBigCluster*N* <br /><br />Węzły danych, które są uruchomione usługi Elasticsearch i Kibana. Możesz połączyć za pomocą węzła tooeach SSH, ale tylko za pośrednictwem hello admin węzła. |
| Elasticsearch klastra |http://myBigCluster.westus.cloudapp.Azure.com/ES/ <br /><br />Hello podstawowy punkt końcowy dla klastra Elasticsearch hello (Uwaga hello /es sufiks). Plik jest chroniony przez podstawowego uwierzytelniania HTTP (hello poświadczenia zostały hello określone parametry esUserName/esPassword hello ES MultiNode szablonu). klaster Hello ma również hello head wtyczki zainstalowane (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) dla administracji podstawowy klaster. |
| Usługa Kibana |http://myBigCluster.westus.cloudapp.Azure.com <br /><br />Witaj Kibana usługi skonfigurowano tooshow danych z hello utworzony Elasticsearch klastra. Plik jest chroniony przez hello tych samych poświadczeń uwierzytelniania jako hello klastra samej siebie. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>W trakcie i przechwytywanie śledzenia poza procesem.
Wprowadzeniu hello wspomniano dwa podstawowe sposoby zbierania danych diagnostycznych: w trakcie i poza procesem. Każdy ma mocne i słabe strony.

Zalety hello **w procesie przechwytywania śledzenia** obejmują:

1. *Łatwe konfigurowanie i wdrażanie*
   
   * Konfiguracja Hello zbierania danych diagnostycznych jest tylko część konfiguracji aplikacji hello. Należy zachować łatwe tooalways go "zsynchronizowane" z hello pozostałej części aplikacji hello.
   * Dla każdej aplikacji lub na usługi konfiguracji jest łatwo osiągalny.
   * Zazwyczaj przechwytywania śledzenia poza procesem wymaga oddzielnego wdrażania i konfiguracji agenta diagnostyki hello, zadanie bardzo administracyjne i potencjalne źródła błędów. Technologia określonego agenta Hello często umożliwia tylko jedno wystąpienie agenta hello na maszynę wirtualną (węzeł). Oznacza to tej konfiguracji dla kolekcji hello konfiguracji diagnostycznych hello jest współdzielona przez wszystkie aplikacje i usługi działające na tym węźle.
2. *Elastyczność*
   
   * Aplikacja Hello może wysyłać dane hello wszędzie tam, gdzie musi toogo, tak długo, jak istnieje biblioteki klienckiej, która obsługuje system przechowywania danych hello docelowe. Można dodać nowego wychwytywanie pożądane.
   * Złożone zasady przechwytywania, filtrowania i agregacja danych może być zaimplementowany.
   * Przechwytywanie śledzenia poza procesem często jest ograniczona przez hello sink danych, które hello obsługuje agenta. Niektóre agenci są rozszerzalne.
3. *Uzyskiwanie dostępu do danych aplikacji toointernal i kontekstu*
   
   * Podsystem diagnostycznych Hello uruchomiony proces aplikacji/usługi hello można łatwo rozszerzyć hello śladów z informacje kontekstowe.
   * W podejściu poza procesem hello hello dane należy wysłać tooan agenta za pomocą mechanizmu komunikacji międzyprocesowej takich jak zdarzenia śledzenia systemu Windows. Ten mechanizm można skonfigurować dodatkowe ograniczenia.

Zalety hello **przechwytywania śledzenia poza procesem** obejmują:

1. *Witaj możliwości toomonitor hello aplikacji i zbieranie zrzutów awaryjnych*
   
   * W trakcie śledzenia przechwytywania może się nie powieść, jeśli aplikacja hello nie powiedzie się toostart lub ulegnie awarii. Niezależnego agenta ma znacznie zwiększa prawdopodobieństwo Przechwytywanie istotne informacje dotyczące rozwiązywania problemów.<br /><br />
2. *Dojrzałości, niezawodności i wydajności sprawdzonych*
   
   * Agent opracowane przez dostawcę platformy (na przykład agent programu Microsoft Azure Diagnostics) została toorigorous temat testowania i ograniczania funkcjonalności bitwy.
   * Z śledzenia w procesie przechwytywania należy uważać tooensure wysyłanie danych diagnostycznych z procesu aplikacji hello działania nie zakłócać aplikacji hello głównych zadań lub doprowadzić do problemów chronometrażu lub wydajności. Niezależnie uruchomiony agent jest mniej podatne problemów toothese i specjalnie zaprojektowanego toolimit jego wpływ na hello system.

Jest to możliwe toocombine i korzystać z obu podejść. W rzeczywistości może być hello najlepsze rozwiązanie dla wielu aplikacji.

W tym miejscu użyjemy hello **biblioteki Microsoft.Diagnostic.Listeners** i śledzenia w trakcie hello przechwytywanie danych toosend z klastra Elasticsearch tooan aplikacji sieci szkieletowej usług.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Użyj hello odbiorników biblioteki toosend danych diagnostycznych tooElasticsearch
Biblioteka Microsoft.Diagnostic.Listeners Hello jest częścią PartyCluster przykładowej aplikacji sieci szkieletowej usług. toouse go:

1. Pobierz [próbki PartyCluster hello](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) z usługi GitHub.
2. Skopiuj hello Microsoft.Diagnostics.Listeners i Microsoft.Diagnostics.Listeners.Fabric projektów (całe foldery) z hello PartyCluster próbki toohello rozwiązania folder katalogu aplikacji hello, która ma toosend hello danych tooElasticsearch .
3. Otwórz rozwiązanie docelowy hello, kliknij prawym przyciskiem myszy węzeł rozwiązania hello w hello Eksploratora rozwiązań i wybierz **Dodaj istniejący projekt**. Dodaj hello Microsoft.Diagnostics.Listeners projektu toohello rozwiązania. Powtórz hello takie same dla hello Microsoft.Diagnostics.Listeners.Fabric projektu.
4. Dodaj odwołanie do projektu z usługi projekty toohello dwóch dodano projektów. (Każda usługa, która ma toosend tooElasticsearch danych powinien odwoływać się Microsoft.Diagnostics.EventListeners i Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Projekt zawiera odwołania do tooMicrosoft.Diagnostics.EventListeners i bibliotek Microsoft.Diagnostics.EventListeners.Fabric][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Wersja usługi sieć szkieletowa ogólnej dostępności i pakiet Microsoft.Diagnostics.Tracing Nuget
Aplikacji skompilowanej za pomocą wersji dostępności usługi sieć szkieletowa ogólne (2.0.135 wydane 31 marca 2016) docelowej **.NET Framework 4.5.2**. Ta wersja jest hello najwyższa wersja programu .NET Framework obsługiwane przez platformę Azure w czasie hello wersji hello GA hello. Niestety ta wersja hello framework brakuje niektórych interfejsów API odbiornika danych tego hello Microsoft.Diagnostics.Listeners wymaga biblioteki. Ponieważ EventSource (hello składnik, który podstawą hello rejestrowania interfejsów API w aplikacji sieci szkieletowej) i odbiornika danych są ściśle powiązane, każdy projekt, który korzysta z biblioteki Microsoft.Diagnostics.Listeners hello musi korzystać z alternatywnych implementacji Element EventSource. Ta implementacja jest zapewniana przez hello **pakietu Microsoft.Diagnostics.Tracing Nuget**, utworzone przez firmę Microsoft. Pakiet HELLO jest pełni zgodny z EventSource zawarte w ramach hello, więc zmiany w kodzie nie powinno być konieczne niż zmiany przywoływanego przestrzeni nazw.

toostart przy użyciu implementacji Microsoft.Diagnostics.Tracing hello hello EventSource klasy, wykonaj następujące kroki dla każdego projektu usługi, który wymaga toosend tooElasticsearch danych:

1. Kliknij prawym przyciskiem myszy projekt usługi hello i wybierz polecenie **Zarządzaj pakietami Nuget**.
2. Przełącz toohello nuget.org źródła pakietu (Jeśli nie została jeszcze wybrana) i wyszukaj "**Microsoft.Diagnostics.Tracing**".
3. Zainstaluj hello `Microsoft.Diagnostics.Tracing.EventSource` pakiet (i jego zależności).
4. Otwórz hello **ServiceEventSource.cs** lub **ActorEventSource.cs** pliku w projekcie usługi i Zastąp hello `using System.Diagnostics.Tracing` dyrektywy u góry pliku hello hello `using Microsoft.Diagnostics.Tracing` dyrektywy.

Te czynności nie będzie konieczne raz hello **.NET Framework 4.6** jest obsługiwana przez system Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Podczas tworzenia wystąpienia Elasticsearch odbiornika i konfiguracji
Witaj ostatnim krokiem wysyłanie danych diagnostycznych tooElasticsearch jest toocreate wystąpienia `ElasticSearchListener` i konfigurowanie go z Elasticsearch połączenia danych. odbiornik Hello automatycznie przechwytuje wszystkie zdarzenia wywoływane za pośrednictwem klas źródła zdarzeń zdefiniowanych w projekcie usługi hello. Musi on toobe podczas okresu istnienia hello usługi hello, więc hello najlepiej umieścić toocreate, którego kod inicjujący hello usługi. Oto, jak kod inicjujący hello usługi bezstanowej może wyglądać po hello niezbędne zmiany (dodatki wskazano w komentarzach począwszy `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Dane połączenia Elasticsearch powinno znajdować się w osobnej sekcji w pliku konfiguracji usługi hello (**PackageRoot\Config\Settings.xml**). Witaj nazwę sekcji hello musi odpowiadać toohello przekazana wartość toohello `FabricConfigurationProvider` konstruktora, na przykład:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Witaj wartości `serviceUri`, `userName` i `password` odpowiadają adres punktu końcowego klastra Elasticsearch toohello, Elasticsearch nazwę użytkownika i hasło, odpowiednio. `indexNamePrefix`Witaj prefiksu dla indeksów Elasticsearch; Biblioteka Microsoft.Diagnostics.Listeners Hello tworzy nowy indeks danych raz dziennie.

### <a name="verification"></a>Weryfikacja
Gotowe. Teraz gdy uruchomiona jest usługa hello, rozpoczyna się wysyłanie śladów toohello Elasticsearch usługi, określonego w konfiguracji hello. Sprawdź hello otwarcia, Kibana interfejsu użytkownika skojarzonego z wystąpieniem Elasticsearch docelowej hello. W naszym przykładzie adres strony hello jest http://myBigCluster.westus.cloudapp.azure.com/. Sprawdź, czy indeksy z prefiksem nazwy hello wybrany dla hello `ElasticSearchListener` rzeczywiście zostały utworzone i wypełniane przy użyciu danych wystąpienia.

![Zdarzenia aplikacji PartyCluster przedstawiający Kibana][2]

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat diagnozowania i monitorowanie usługi sieci szkieletowej usług](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
