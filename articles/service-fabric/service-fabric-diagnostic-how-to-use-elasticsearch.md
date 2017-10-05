---
title: "Przy użyciu Elasticsearch jako magazyn śledzenia aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Opis sposobu aplikacji usługi Service Fabric użyciu Elasticsearch i Kibana wyszukiwania za pomocą śladów aplikacji (Dzienniki) i przechowywać indeksu,"
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
ms.openlocfilehash: 2d2ceceea131b41ad1a1735aaa2a859d035ab098
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Przechowywanie Elasticsearch używany jako śledzenia aplikacji sieci szkieletowej usług
## <a name="introduction"></a>Wprowadzenie
W tym artykule opisano sposób [sieć szkieletowa usług Azure](https://azure.microsoft.com/documentation/services/service-fabric/) aplikacje mogą używać **Elasticsearch** i **Kibana** dla magazynu śledzenia aplikacji, indeksowanie i wyszukiwanie. [Elasticsearch](https://www.elastic.co/guide/index.html) jest open source, rozproszone i skalowalne w czasie rzeczywistym wyszukiwania i analiza mechanizm, który dobrze nadaje się do tego zadania. Można go zainstalować na maszynach wirtualnych Windows i Linux, działają na platformie Microsoft Azure. Elasticsearch wydajnie może przetwarzać *strukturalnych* śladów utworzone przy użyciu technologii, takich jak **funkcji Śledzenie zdarzeń systemu Windows ()**.

ETW jest używany przez środowisko uruchomieniowe usługi sieć szkieletowa do źródła informacji diagnostycznych (śladów). Jest zalecana metoda zbyt źródła ich informacje diagnostyczne, aplikacji sieci szkieletowej usług. Ten sam mechanizm umożliwia korelacji między dostarczone przez środowisko uruchomieniowe i aplikacja dostarczona śladów i sprawia, że rozwiązania problemu. Interfejs API rejestrowania obejmują szablony projektów sieci szkieletowej usług w programie Visual Studio (oparte na .NET **EventSource** klasy) który emituje śladów ETW. domyślnie. Ogólne omówienie aplikacji usługi Service Fabric śledzenia przy użyciu funkcji ETW, zobacz [monitorowania i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Dla danych śledzenia w Elasticsearch muszą być zarejestrowane w węzłach klastra sieci szkieletowej usług w czasie rzeczywistym (gdy aplikacja jest uruchomiona) i wysyłane do punktu końcowego Elasticsearch. Dostępne są dwie główne opcje do przechwytywania śledzenia:

* **W procesie przechwytywania śledzenia**  
  Aplikacja lub bardziej precyzyjnie procesu usługi, jest odpowiedzialny za wysyłanie danych diagnostycznych w magazynie śledzenia (Elasticsearch).
* **Przechwytywanie śledzenia poza procesem.**  
  Oddzielnym agentem jest przechwytywanie śladów pochodzących z procesu usługi lub procesów i wysyłania ich do sklepu śledzenia.

Poniżej możemy opisano, jak skonfigurować Elasticsearch na platformie Azure, omówiono w nim zalety i wady obu przechwytywania opcje i wyjaśniono, jak skonfigurować usługę sieci szkieletowej usług w celu wysyłania danych do Elasticsearch.

## <a name="set-up-elasticsearch-on-azure"></a>Konfigurowanie Elasticsearch na platformie Azure
Najbardziej oczywistym sposobem skonfigurowania usługi Elasticsearch na platformie Azure jest za pośrednictwem [ **szablonów usługi Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Zaawansowane [szablon szybkiego startu usługi Azure Resource Manager dla Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) jest dostępna z repozytorium szablonów Szybki Start Azure. Ten szablon używa oddzielny magazyn kont dla jednostki skali (grupy węzłów). Można również udostępniać, klienckim oddzielnie i węzły serwera z różnymi konfiguracjami oraz różne numery dyskach danych dołączonych.

W tym miejscu korzystamy z innego szablonu, nazywane **ES MultiNode** z [repozytorium Azure narzędzia diagnostyczne](https://github.com/Azure/azure-diagnostics-tools). Ten szablon jest łatwiejsza w użyciu, i tworzy klastra Elasticsearch zabezpieczone przy użyciu podstawowego uwierzytelniania HTTP. Przed kontynuowaniem pobierz repozytorium z serwisu GitHub do komputera (przez klonowanie repozytorium lub pobieranie pliku zip). Szablon ES MultiNode znajduje się w folderze o tej samej nazwie.

### <a name="prepare-a-machine-to-run-elasticsearch-installation-scripts"></a>Przygotowanie maszyny do uruchamiania skryptów instalacji Elasticsearch
Najprostszym sposobem, aby użyć szablonu ES MultiNode odbywa się za pośrednictwem dostarczonego skryptu programu PowerShell systemu Azure o nazwie `CreateElasticSearchCluster`. Aby użyć tego skryptu, musisz zainstalować moduły programu PowerShell i narzędzie **openssl**. Drugie jest niezbędny do utworzenia klucza SSH, który może służyć do administrowania klastrem Elasticsearch zdalnie.

`CreateElasticSearchCluster`skrypt jest przeznaczona dla łatwość użycia przy użyciu szablonu ES MultiNode z komputera z systemem Windows. Można użyć szablonu na komputerze z systemem innym niż Windows, ale w tym scenariuszu wykracza poza zakres tego artykułu.

1. Jeśli ich nie zainstalowano już, zainstaluj [ **modułów programu Azure PowerShell**](http://aka.ms/webpi-azps). Po wyświetleniu monitu kliknij przycisk **Uruchom**, następnie **zainstalować**. Program Azure PowerShell 1.3 lub nowszy jest wymagany.
2. **Openssl** narzędzie znajduje się w dystrybucji [ **Git dla systemu Windows**](http://www.git-scm.com/downloads). Jeśli jeszcze tego nie zrobiono, zainstaluj [Git dla systemu Windows](http://www.git-scm.com/downloads) teraz. (Domyślne opcje instalacji są OK).
3. Przy założeniu, że Git został zainstalowany, ale nie jest uwzględniony w ścieżce systemowej, Otwórz okno programu Microsoft Azure PowerShell i uruchom następujące polecenia:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Zastąp `<Git installation folder>` z lokalizacji Git na tym komputerze; wartość domyślna to **"C:\Program Files\Git"**. Należy zwrócić uwagę na początku ścieżki pierwszym znakiem średnika.
4. Upewnij się, że użytkownik jest zalogowany na platformie Azure (za pośrednictwem [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet) i po wybraniu subskrypcji, które mają być używane do tworzenia klastra elastycznej wyszukiwania. Można sprawdzić, czy wybrano poprawną subskrypcję za pomocą `Get-AzureRmContext` i `Get-AzureRmSubscription` polecenia cmdlet.
5. Jeśli jeszcze tego nie zrobiono tego wcześniej, zmień bieżący katalog na folder ES MultiNode.

### <a name="run-the-createelasticsearchcluster-script"></a>Uruchom skrypt CreateElasticSearchCluster
Przed uruchomieniem skryptu Otwórz `azuredeploy-parameters.json` pliku Sprawdź i podaj wartości parametrów skryptu. Dostępne są następujące parametry:

| Nazwa parametru | Opis |
| --- | --- |
| dnsNameForLoadBalancerIP |Nazwa, która służy do tworzenia publicznie widoczna nazwa DNS dla klastra elastycznej wyszukiwania (dołączając do podanej nazwy domeny region platformy Azure). Na przykład jeśli wartość tego parametru jest "myBigCluster", a wybrany region platformy Azure to zachodnie stany USA, wynikowa nazwa DNS dla klastra jest myBigCluster.westus.cloudapp.azure.com. <br /><br />Ta nazwa służy również jako nazwę wiele artefakty skojarzone z klastrem elastycznej wyszukiwania, takie jak bazy danych, nazwy węzła głównego. |
| adminUsername |Nazwa konta administratora do zarządzania klastrem elastycznej wyszukiwania (odpowiadające im klucze SSH wygenerowaniu automatycznie). |
| dataNodeCount |Liczba węzłów w klastrze elastycznej wyszukiwania. Bieżąca wersja skryptu nie rozróżnia między węzłami danych i zapytania. wszystkie węzły odtworzyć obie role. Wartość domyślna to 3 węzłach. |
| dataDiskSize |Rozmiar dysków danych (w GB) przypisany do każdego węzła danych. Każdy węzeł odbiera 4 dyski danych, przeznaczona wyłącznie do usługi wyszukiwania elastycznej. |
| Region |Nazwa regionu Azure, gdzie powinien być zlokalizowany klastra elastycznej wyszukiwania. |
| esUserName |Nazwa użytkownika użytkownik, który jest skonfigurowany do dostępu do klastra ES (zgodnie z uwierzytelniania podstawowego HTTP). Hasło nie jest częścią pliku parametrów i należy podać podczas `CreateElasticSearchCluster` skrypt zostanie wywołany. |
| vmSizeDataNodes |Rozmiar maszyny wirtualnej platformy Azure dla węzłów klastra elastycznej wyszukiwania. Wartość domyślna to Standard_D2. |

Teraz można przystąpić do uruchomienia skryptu. Należy wydać następujące polecenie:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

gdzie 

| Nazwa parametru skryptu | Opis |
| --- | --- |
| `<es-group-name>` |Nazwa grupy zasobów platformy Azure, która będzie zawierać wszystkich zasobów klastra elastycznej wyszukiwania. |
| `<azure-region>` |Nazwa region platformy Azure, w którym ma zostać utworzony klaster elastycznej wyszukiwania. |
| `<es-password>` |Hasło użytkownika elastycznej wyszukiwania. |

> [!NOTE]
> Jeśli otrzymasz NullReferenceException z polecenia cmdlet Test-AzureResourceGroup pamiętasz do logowania się do platformy Azure (`Add-AzureRmAccount`).
> 
> 

Jeśli okaże się, że błąd został spowodowany przez wartość parametru szablonu niewłaściwy wystąpi błąd uruchomienia skryptu, Popraw plik parametru i ponownie uruchom skrypt z nazwą grupy innego zasobu. Można ponownie użyć tej samej nazwy grupy zasobów i mieć skrypt czyszczenia starego przez dodanie `-RemoveExistingResourceGroup` parametr, aby można było wywołać skryptu.

### <a name="result-of-running-the-createelasticsearchcluster-script"></a>Wynik uruchomienia skryptu CreateElasticSearchCluster
Po uruchomieniu `CreateElasticSearchCluster` skryptu następujące główne artefakty zostanie utworzony. W tym przykładzie przyjęto założenie, że użyto "myBigCluster" jako wartości `dnsNameForLoadBalancerIP` parametr i że region, w którym utworzono klaster jest zachodnie stany USA.

| Artefaktów | Nazwa, lokalizacja i uwagi |
| --- | --- |
| Klucz SSH dla administracji zdalnej |Plik myBigCluster.key (w katalogu, z którego zostało uruchomione CreateElasticSearchCluster). <br /><br />Ten plik klucza może służyć do połączenia do węzła administratora i (za pośrednictwem węzła administratora) danych w węzłach klastra. |
| Węzeł administratora |myBigCluster admin.westus.cloudapp.azure.com <br /><br />Dedykowane maszyny Wirtualnej dla zdalnego administrowania klastrami Elasticsearch — tylko jeden, który zezwala na zewnętrzne połączenia SSH. Jest uruchamiany na tej samej sieci wirtualnej wszystkie węzły klastra Elasticsearch, ale nie uruchamia wszystkie usługi Elasticsearch. |
| Węzły danych |myBigCluster1... myBigCluster*N* <br /><br />Węzły danych, które są uruchomione usługi Elasticsearch i Kibana. Możesz połączyć za pośrednictwem protokołu SSH w każdym węźle, ale tylko za pomocą węzła administratora. |
| Elasticsearch klastra |http://myBigCluster.westus.cloudapp.Azure.com/ES/ <br /><br />Podstawowy punkt końcowy dla klastra Elasticsearch (Uwaga sufiks /es). Jest on chroniony podstawowego uwierzytelniania HTTP (poświadczenia zostały określone parametry esUserName/esPassword szablonu ES MultiNode). Klaster ma również nagłówek wtyczki zainstalowane (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) dla administracji podstawowy klaster. |
| Usługa Kibana |http://myBigCluster.westus.cloudapp.Azure.com <br /><br />Usługa Kibana jest skonfigurowana tak, aby wyświetlić dane utworzonego klastra Elasticsearch. Jest on chroniony tych samych poświadczeń uwierzytelniania jako samego klastra. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>W trakcie i przechwytywanie śledzenia poza procesem.
We wprowadzeniu wspomniano dwa podstawowe sposoby zbierania danych diagnostycznych: w trakcie i poza procesem. Każdy ma mocne i słabe strony.

Zalety **w procesie przechwytywania śledzenia** obejmują:

1. *Łatwe konfigurowanie i wdrażanie*
   
   * Konfiguracja zbierania danych diagnostycznych jest tylko część konfiguracji aplikacji. To ułatwia zawsze Zachowuj "synchronizację" z resztą aplikacji.
   * Dla każdej aplikacji lub na usługi konfiguracji jest łatwo osiągalny.
   * Zazwyczaj przechwytywania śledzenia poza procesem wymaga oddzielnego wdrażania i konfiguracji agenta diagnostyki, jest bardzo administracyjne zadania i potencjalne źródła błędów. Technologia określonego agenta umożliwia często tylko jedno wystąpienie agenta dla jednej maszyny wirtualnej (węzeł). Oznacza to tej konfiguracji dla kolekcji Konfiguracja diagnostyczna jest współdzielona przez wszystkie aplikacje i usługi działające na tym węźle.
2. *Elastyczność*
   
   * Aplikacja może wysyłać dane wszędzie tam, gdzie należy przejść, tak długo, jak jest biblioteka klienta, która obsługuje system magazynowania wybranych danych. Można dodać nowego wychwytywanie pożądane.
   * Złożone zasady przechwytywania, filtrowania i agregacja danych może być zaimplementowany.
   * Przechwytywanie śledzenia poza procesem często jest ograniczona przez sink danych, które obsługuje agenta. Niektóre agenci są rozszerzalne.
3. *Dostęp do danych aplikacji wewnętrznych i kontekstu*
   
   * Podsystem diagnostycznych uruchomiony proces aplikacji/usługi można łatwo rozszerzyć śladów z informacje kontekstowe.
   * W ujęciu poza procesem dane należy wysłać do agenta za pomocą mechanizmu komunikacji międzyprocesowej, takich jak zdarzenia śledzenia systemu Windows. Ten mechanizm można skonfigurować dodatkowe ograniczenia.

Zalety **przechwytywania śledzenia poza procesem** obejmują:

1. *Możliwość monitorowania aplikacji i zbieranie zestawy awaryjne*
   
   * W trakcie śledzenia przechwytywania może się nie powieść, jeśli aplikacja nie powiedzie się lub ulega awarii. Niezależnego agenta ma znacznie zwiększa prawdopodobieństwo Przechwytywanie istotne informacje dotyczące rozwiązywania problemów.<br /><br />
2. *Dojrzałości, niezawodności i wydajności sprawdzonych*
   
   * Agent opracowane przez dostawcę platformy (na przykład agent programu Microsoft Azure Diagnostics) została rygorystyczne testowania i ograniczania funkcjonalności bitwy.
   * Z śledzenia w procesie przechwytywania można uważać, aby zapewnić, że działania wysyłanie danych diagnostycznych z procesu aplikacji nie zakłócać głównych zadań aplikacji lub doprowadzić do problemów chronometrażu lub wydajności. Agent niezależnie uruchomiona jest mniej podatne na te problemy i specjalnie z myślą o ograniczyć jej wpływ na system.

Istnieje możliwość łączenia i korzystać z obu podejść. W rzeczywistości może być najlepszym rozwiązaniem dla wielu aplikacji.

W tym miejscu użyjemy **biblioteki Microsoft.Diagnostic.Listeners** i śledzenia w procesie przechwytywania do wysyłania danych z aplikacji do klastra Elasticsearch sieci szkieletowej usług.

## <a name="use-the-listeners-library-to-send-diagnostic-data-to-elasticsearch"></a>Wyślij dane diagnostyczne do Elasticsearch przy użyciu biblioteki obiektów nasłuchujących
Biblioteka Microsoft.Diagnostic.Listeners jest częścią PartyCluster przykładowej aplikacji sieci szkieletowej usług. Aby użyć go:

1. Pobierz [próbki PartyCluster](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) z usługi GitHub.
2. Skopiuj projektów Microsoft.Diagnostics.Listeners i Microsoft.Diagnostics.Listeners.Fabric (całe foldery) z katalog przykładu PartyCluster do folderu rozwiązania aplikacji, która ma wysyłać dane do Elasticsearch.
3. Otwórz rozwiązanie docelowych, kliknij prawym przyciskiem myszy węzeł rozwiązania w Eksploratorze rozwiązań i wybierz **Dodaj istniejący projekt**. Dodaj Microsoft.Diagnostics.Listeners projektu do rozwiązania. Powtórzenie Microsoft.Diagnostics.Listeners.Fabric projektu.
4. Dodaj odwołanie do projektu z projektów z usługi do dwa projekty dodany. (Każda usługa, która ma wysyłać dane do Elasticsearch powinien odwoływać się Microsoft.Diagnostics.EventListeners i Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Odwołania do bibliotek Microsoft.Diagnostics.EventListeners i Microsoft.Diagnostics.EventListeners.Fabric][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Wersja usługi sieć szkieletowa ogólnej dostępności i pakiet Microsoft.Diagnostics.Tracing Nuget
Aplikacji skompilowanej za pomocą wersji dostępności usługi sieć szkieletowa ogólne (2.0.135 wydane 31 marca 2016) docelowej **.NET Framework 4.5.2**. Ta wersja jest najwyższa wersja programu .NET Framework obsługiwane przez platformę Azure w czasie wersja Ogólnodostępna. Niestety ta wersja platformy nie ma niektórych interfejsów API odbiornika danych wymaga biblioteki Microsoft.Diagnostics.Listeners. Ponieważ EventSource (składnik, który stanowi podstawę rejestrowania interfejsów API w sieci szkieletowej aplikacji) i odbiornika danych są ściśle powiązane, każdy projekt, który korzysta z biblioteki Microsoft.Diagnostics.Listeners użyć alternatywnej implementacji obiektu EventSource. Ta implementacja jest zapewniana przez **pakietu Microsoft.Diagnostics.Tracing Nuget**, utworzone przez firmę Microsoft. Pakiet jest pełni zgodny z EventSource zawarte w ramach, więc zmiany w kodzie nie powinno być konieczne niż zmiany przywoływanego przestrzeni nazw.

Aby rozpocząć korzystanie z implementacji Microsoft.Diagnostics.Tracing klasy źródła zdarzeń, wykonaj następujące kroki dla każdego projektu usługi, który należy do wysyłania danych do Elasticsearch:

1. Kliknij prawym przyciskiem myszy projekt usługi i wybierz polecenie **Zarządzaj pakietami Nuget**.
2. Przełącz się do źródła pakietu nuget.org (Jeśli nie została jeszcze wybrana) i wyszukaj "**Microsoft.Diagnostics.Tracing**".
3. Zainstaluj `Microsoft.Diagnostics.Tracing.EventSource` pakiet (i jego zależności).
4. Otwórz **ServiceEventSource.cs** lub **ActorEventSource.cs** pliku w projekcie usługi i Zastąp `using System.Diagnostics.Tracing` dyrektywy u góry pliku z `using Microsoft.Diagnostics.Tracing` dyrektywy.

Te czynności nie będzie konieczne raz **.NET Framework 4.6** jest obsługiwana przez system Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Podczas tworzenia wystąpienia Elasticsearch odbiornika i konfiguracji
Ostatnim krokiem wysyłanie danych diagnostycznych do Elasticsearch jest utworzenie wystąpienia `ElasticSearchListener` i konfigurowanie go z Elasticsearch połączenia danych. Odbiornik automatycznie przechwytuje wszystkie zdarzenia wywoływane za pośrednictwem klas źródła zdarzeń zdefiniowanych w projekcie usługi. Musi to być aktywne przez cały okres istnienia usługi, dlatego najlepszym miejscem, aby go utworzyć w kodzie inicjowania usługi. Oto, jak kod inicjujący usługi bezstanowej może wyglądać po niezbędne zmiany (dodatki wskazano w komentarzach począwszy `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add the following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is the entry point of the service host process.
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

                // The ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name to a .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of the class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that the ElasticSearchListner instance is not garbage-collected prematurely
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

Dane połączenia Elasticsearch powinno znajdować się w osobnej sekcji w pliku konfiguracji usługi (**PackageRoot\Config\Settings.xml**). Nazwa sekcji musi odpowiadać wartości przekazanych do `FabricConfigurationProvider` konstruktora, na przykład:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Wartości `serviceUri`, `userName` i `password` odpowiada adres punktu końcowego klastra Elasticsearch Elasticsearch nazwy użytkownika i hasła, odpowiednio parametry. `indexNamePrefix`jest prefiksem dla indeksów Elasticsearch; Biblioteka Microsoft.Diagnostics.Listeners tworzy nowy indeks danych raz dziennie.

### <a name="verification"></a>Weryfikacja
Gotowe. Teraz gdy uruchomiona jest usługa, rozpoczyna się wysyłanie śladów do usługi Elasticsearch określony w konfiguracji. Możesz sprawdzić, czy to otwarcie interfejsu użytkownika Kibana skojarzony z wystąpieniem Elasticsearch docelowej. W naszym przykładzie adres strony jest http://myBigCluster.westus.cloudapp.azure.com/. Sprawdź, czy indeksy z prefiksem nazwy wybrany dla `ElasticSearchListener` rzeczywiście zostały utworzone i wypełniane przy użyciu danych wystąpienia.

![Zdarzenia aplikacji PartyCluster przedstawiający Kibana][2]

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat diagnozowania i monitorowanie usługi sieci szkieletowej usług](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
