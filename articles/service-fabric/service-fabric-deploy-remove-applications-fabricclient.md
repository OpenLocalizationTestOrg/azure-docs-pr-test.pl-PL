---
title: "aaaAzure wdrożenia aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Użyj hello toodeploy interfejsów API klienta fabricclient z rolą i usunąć aplikacje w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Wdrażanie i usunąć aplikacje przy użyciu klienta fabricclient z rolą
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Program Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [Interfejsy API FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Raz [typu aplikacji zostały opakowane][10], jest ono gotowe do wdrożenia do klastra usługi sieć szkieletowa usług Azure. Wdrożenie obejmuje hello następujące trzy kroki:

1. Przekaż magazynu obrazów toohello pakietu aplikacji hello
2. Rejestracja typu aplikacji hello
3. Tworzenie wystąpienia aplikacji hello

Po wdrożeniu aplikacji i wystąpienie jest uruchomione w klastrze hello, można usunąć wystąpienia aplikacji hello i typem aplikacji. Usuń toocompletely aplikacji z klastra hello obejmuje hello następujące kroki:

1. Usuń (lub usunąć) hello uruchomione wystąpienie aplikacji
2. Wyrejestrowywanie typu aplikacji hello, jeśli nie są już potrzebne
3. Usuwanie pakietu aplikacji hello z magazynu obrazów hello

Jeśli używasz [programu Visual Studio umożliwiające wdrażanie i debugowanie aplikacji](service-fabric-publish-app-remote-cluster.md) na klaster lokalny rozwój hello wszystkich powyższych kroków obsługi automatycznie za pomocą skryptu programu PowerShell.  Skrypt ten znajduje się w hello *skryptów* folderu projekt aplikacji hello. Ten artykuł zawiera tła na tego skryptu czynności, aby można było wykonać hello operacji poza Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Połącz toohello klastra
Łączenie przez utworzenie klastra toohello [klienta fabricclient z rolą](/dotnet/api/system.fabric.fabricclient) wystąpienia przed uruchomieniem dowolnych hello przykłady kodu w tym artykule. Przykłady łączącego tooa lokalnego klastra projektowego zdalnego klastra lub klastra zabezpieczone przy użyciu usługi Azure Active Directory, X509 certyfikatów lub usługi Active Directory systemu Windows, zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). tooconnect toohello lokalnego klastra projektowego, uruchom następujące hello:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Przekaż pakiet aplikacji hello
Załóżmy, że kompilacji i pakietu aplikacji o nazwie *MyApplication* w programie Visual Studio. Domyślnie nazwa typu aplikacji hello wymienione w pliku ApplicationManifest.xml hello jest "MyApplicationType".  Witaj pakiet aplikacji, który zawiera manifest aplikacji konieczne hello, manifestów usługi i pakietów kodu/config/danych, znajduje się w *C:\Users\&lt; nazwa użytkownika&gt;\Documents\Visual 2017\Projects\ w Studio MyApplication\MyApplication\pkg\Debug*.

Przekazywanie pakietu aplikacji hello umieszcza je w lokalizacji, który jest dostępny dla hello wewnętrznych składników usługi Service Fabric. Sieć szkieletowa usług sprawdza, czy pakiet aplikacji hello podczas rejestracji hello pakietu aplikacji hello. Jednak jeśli chcesz pakiet aplikacji hello tooverify lokalnie (tj. przed przekazaniem), użyj hello [ServiceFabricApplicationPackage testu](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) polecenia cmdlet.

Witaj [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) magazynu obrazów klastra toohello pakietu aplikacji hello przekazuje interfejsu API. 

Jeśli pakiet aplikacji hello jest duży i/lub ma wiele plików, możesz [skompresować je](service-fabric-package-apps.md#compress-a-package) i skopiować go toohello magazynu obrazów przy użyciu programu PowerShell. Witaj Kompresja zmniejsza rozmiar hello i hello liczbę plików.

Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.

## <a name="register-hello-application-package"></a>Pakiet aplikacji hello rejestru
Witaj typ i wersja aplikacji zadeklarowane w manifeście aplikacji hello staną się dostępne po zarejestrowaniu pakietu aplikacji hello. Hello system odczytuje przesłany w poprzednim kroku hello pakiet hello, sprawdza, czy pakiet hello przetwarza hello zawartość pakietu i kopiuje hello przetworzyć pakietu tooan wewnętrznego systemu lokalizacji.  

Witaj [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) rejestrów interfejsu API hello typu aplikacji w klastrze hello i udostępnienie jej do wdrożenia.

Witaj [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) interfejsu API zawiera informacje o wszystkich typów aplikacji pomyślnie zarejestrowany. Po zakończeniu rejestracji hello, można użyć tego toodetermine interfejsu API.

## <a name="create-an-application-instance"></a>Utwórz wystąpienie aplikacji
Można utworzyć wystąpienia aplikacji z dowolnego typu aplikacji, który został pomyślnie zarejestrowany za pomocą hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) interfejsu API. nazwy poszczególnych aplikacji Hello musi rozpoczynać się od hello *"fabric:"* schemat i muszą być unikatowe dla każdego wystąpienia aplikacji (w ramach klastra). Wszystkie usługi domyślne zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello są również tworzone.

Dla dowolnej wersji danego typu zarejestrowanej aplikacji można tworzyć wiele wystąpień aplikacji. Każde wystąpienie aplikacji jest uruchamiany w izolacji z katalogu roboczego i zestaw procesów.

toosee, który o nazwie aplikacje i usługi są uruchomione w klastrze hello, uruchom hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) i [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) interfejsów API.

## <a name="create-a-service-instance"></a>Utwórz wystąpienie usługi
Można utworzyć wystąpienia usługi z typem usługi przy użyciu hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) interfejsu API.  Jeśli usługa hello jest zadeklarowany jako domyślna usługa w manifeście aplikacji hello, hello usługi jest utworzona podczas tworzenia wystąpienia klasy aplikacji hello.  Wywoływanie hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) interfejsu API usługi, który już jest utworzone zwróci wyjątek typu FabricException zawierający kod błędu z wartością FabricErrorCode.ServiceAlreadyExists.

## <a name="remove-a-service-instance"></a>Usuń wystąpienia usługi
Jeśli wystąpienie usługi nie jest już potrzebne, można usunąć go z hello uruchomione wystąpienie aplikacji przez wywołanie hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) interfejsu API.  

> [!WARNING]
> Ta operacja jest nieodwracalna i nie można odzyskać stan usługi.

## <a name="remove-an-application-instance"></a>Usuwanie wystąpienia aplikacji
Gdy wystąpienie aplikacji nie jest już potrzebne, można trwale usunąć ją według nazwy przy użyciu hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) interfejsu API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatycznie usuwa wszystkie usługi należące toohello aplikacji, jak również i stałe usunięcie wszystkich stan usługi.

> [!WARNING]
> Ta operacja jest nieodwracalna i nie można odzyskać stan aplikacji.

## <a name="unregister-an-application-type"></a>Wyrejestrowywanie typu aplikacji
W przypadku konkretnej wersji typu aplikacji nie jest potrzebna, należy wyrejestrować tej konkretnej wersji typu aplikacji hello przy użyciu hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) interfejsu API. Wyrejestrowywanie nieużywane wersje aplikacji typów wersjach miejsca do magazynowania używanego przez hello magazynu obrazów. Wersja typu aplikacji można wyrejestrować tak długo, jak przy użyciu wersji tego typu aplikacji hello wystąpienia są tworzone żadne aplikacje i żadnych uaktualnień aplikacji oczekujących odwołują się do tej wersji typu aplikacji hello.

## <a name="remove-an-application-package-from-hello-image-store"></a>Usuwanie pakietu aplikacji ze sklepu obraz powitania
Gdy pakiet aplikacji nie jest potrzebna, należy ją usunąć z toofree magazynu obrazu hello zasobów systemowych przy użyciu hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) interfejsu API.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Element ImageStoreConnectionString wprowadza się ServiceFabricApplicationPackage kopiowania
środowisko zestawu SDK usług sieci szkieletowej Hello ma już hello jest poprawna, skonfigurować ustawienia domyślne. A w razie potrzeby hello element ImageStoreConnectionString dla wszystkich poleceń powinny być zgodne wartość hello tego hello klaster sieci szkieletowej usług. Hello element ImageStoreConnectionString można znaleźć w manifeście klastra hello pobrany przy użyciu hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) i polecenia Get-ImageStoreConnectionStringFromClusterManifest:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Witaj **Get-ImageStoreConnectionStringFromClusterManifest** polecenia cmdlet, będący częścią modułu programu PowerShell zestawu SDK sieci szkieletowej usług hello jest obraz powitania używane tooget przechowywanie parametrów połączenia.  tooimport hello zestawu SDK modułu, uruchom:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


Element ImageStoreConnectionString Hello zostanie znaleziony w manifeście klastra hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Zobacz [zrozumieć parametry połączenia magazynu obrazu hello](service-fabric-image-store-connection-string.md) o dodatkowe informacje o hello image store oraz obraz przechowywanie parametrów połączenia.

### <a name="deploy-large-application-package"></a>Wdrażanie pakietu dużych aplikacji
Problem: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) interfejsu API upłynie limit czasu dla pakietu aplikacji duże (kolejność GB).
Wypróbuj:
- Określ większego limitu czasu dla [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) metody z `timeout` parametru. Domyślnie program hello limitu czasu wynosi 30 minut.
- Sprawdź hello połączenie sieciowe między maszyną źródłową a klastra. Jeśli hello połączenie jest powolne, rozważ użycie maszynę z lepszą połączenia sieciowego.
Jeśli komputer kliencki hello w regionie innym niż klaster hello, należy rozważyć użycie komputerze klienckim w regionie bliżej lub tego samego jako klaster hello.
- Sprawdź, czy osiągnięto ograniczania zewnętrznych. Na przykład gdy hello obrazu magazyn jest skonfigurowany toouse azure magazynu, można ograniczenie przekazywania.

Problem: Pakiet przekazywania została ukończona pomyślnie, ale [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) limitu czasu interfejsu API. Wypróbuj:
- [Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów.
Hello Kompresja zmniejsza rozmiar hello i wykonaj hello liczba plików, który z kolei ogranicza hello ilość ruchu sieciowego i działają w tej sieci szkieletowej usług. Operacja przekazywania Hello może przebiegać wolniej, (zwłaszcza, Jeśli dołączysz hello kompresji czasu), ale rejestrowania i wyrejestrowania typ aplikacji hello są szybsze.
- Określ większego limitu czasu dla [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) interfejsu API za pomocą `timeout` parametru.

### <a name="deploy-application-package-with-many-files"></a>Wdrażanie pakietu aplikacji z wielu plików
Problem: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) limitu czasu dla pakietu aplikacji z wielu plików (kolejność tysięcy).
Wypróbuj:
- [Kompresuj pakietu hello](service-fabric-package-apps.md#compress-a-package) przed skopiowaniem toohello magazynu obrazów. Kompresja Hello zmniejsza hello liczbę plików.
- Określ większego limitu czasu dla [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) z `timeout` parametru.

## <a name="code-example"></a>Przykładowy kod
Hello poniższy przykład umożliwia skopiowanie obrazu sklepu z aplikacjami pakietu toohello, przepisy typ aplikacji hello, tworzy wystąpienie aplikacji, tworzy wystąpienie usługi, usuwa wystąpienie aplikacji hello, un przepisy typ aplikacji hello i Usuwa pakiet aplikacji hello z hello magazynu obrazów.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)

[Wprowadzenie kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)

[Diagnozowanie i rozwiązywanie problemów z usługą sieci szkieletowej usług](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Model aplikacji w sieci szkieletowej usług](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
