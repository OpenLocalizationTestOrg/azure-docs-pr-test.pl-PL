---
title: "cykl życia aaaApplication w sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano tworzenie, wdrażanie, testowania, uaktualniania, utrzymywaniem i usunięcie aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 08837cca-5aa7-40da-b087-2b657224a097
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 36cd6081010e83cb8226c8f85d1e912ac9eebd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-lifecycle"></a>Cykl życia aplikacji w sieci szkieletowej usług
Ponieważ z innych platform, aplikację na sieć szkieletowa usług Azure zazwyczaj przechodzi przez hello następujące etapy: projekt, programowanie testowania, wdrożenia, uaktualnianie, obsługi i usuwania. Sieć szkieletowa usług przewiduje hello pełnej aplikacji cyklem życia aplikacji w chmurze, od projektowania do wdrażania, zarządzania infrastrukturą i likwidowaniu tooeventual konserwacji najwyższej jakości pomoc techniczną. model usługi Hello umożliwia kilku różnych ról tooparticipate niezależnie w cyklu życia aplikacji hello. Ten artykuł zawiera omówienie hello interfejsów API i jak są używane przez różne role hello w hello etapy cyklu życia aplikacji usługi sieć szkieletowa hello.

Witaj poniższe wideo Microsoft Virtual Academy opisano sposób toomanage cyklu użytkowania Twojej aplikacji:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-application-lifecycle/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="service-model-roles"></a>Usługi ról modelu
role modelu usługi Hello są:

* **Usługa developer**: rozwija moduły i ogólne usług, które może być konieczności zmiany i używany w wielu aplikacji hello tego samego typu lub różnych typów. Na przykład usługi kolejki może służyć do tworzenia aplikacji obsługi biletów (Pomoc techniczna) lub aplikacji handlu elektronicznego (koszyk).
* **Deweloper aplikacji**: tworzy aplikacje integrując zbiór usług toosatisfy niektórych wymagań lub scenariuszy. Na przykład witryną internetową handlu elektronicznego może zintegrować "JSON frontonu usługi bezstanowej," "Usługa Stateful aukcji" i "Usługa Stateful kolejki" toobuild auctioning rozwiązania.
* **Administrator aplikacji**: sprawia, że decyzje dotyczące konfiguracji aplikacji hello (wypełnianie parametrów szablonu konfiguracji hello), wdrożenie (mapowanie zasobów tooavailable) i jakości usług. Na przykład administrator aplikacji decyduje hello języka ustawień regionalnych (angielski dla hello Stanów Zjednoczonych lub japoński w Japonii, na przykład) aplikacji hello. Różne wdrożonej aplikacji może mieć różne ustawienia.
* **Operator**: wdraża aplikacje na podstawie konfiguracji aplikacji hello i wymaganiami określonymi przez administratora aplikacji hello. Na przykład operator przepisy i wdraża aplikację hello i zapewnia, że jest uruchomiona na platformie Azure. Operatory monitorowanie informacji o kondycji i wydajności aplikacji i konserwacja infrastruktury fizycznej hello, zgodnie z potrzebami.

## <a name="develop"></a>Programowanie
1. A *usługi developer* osiąga różnych typów usług przy użyciu hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) lub [niezawodne usługi](service-fabric-reliable-services-introduction.md) model programowania.
2. A *usługi developer* deklaratywnie opisano typy usługi hello opracowane w pliku manifestu usługi składające się z co najmniej jednego pakietu kodu, konfiguracji i danych.
3. *Deweloper aplikacji* utworzy aplikację przy użyciu usługi różnych typów.
4. *Deweloper aplikacji* deklaratywnie opisuje typ aplikacji hello w manifest aplikacji odwołuje się do hello usługi manifesty hello składników usług i odpowiednio zastępowanie i ustawianie różne ustawienia konfiguracji i wdrażania hello usług składowych.

Zobacz [wprowadzenie Reliable Actors](service-fabric-reliable-actors-get-started.md) i [Rozpoczynanie pracy z usługami Reliable Services](service-fabric-reliable-services-quick-start.md) przykłady.

## <a name="deploy"></a>Wdrażanie
1. *Administrator aplikacji* dostosowanie hello aplikacji typu tooa określonej aplikacji wdrożonych toobe tooa klastra sieci szkieletowej usług, podając odpowiednie parametry hello hello **atrybutów ApplicationType**elementu w manifeście aplikacji hello.
2. *Operator* przekazywania hello sklepu z aplikacjami pakietu toohello klastra obrazu przy użyciu hello [ **CopyApplicationPackage** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) lub hello [  **Kopiuj ServiceFabricApplicationPackage** polecenia cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). pakiet aplikacji Hello zawiera manifest aplikacji hello i kolekcji hello usługi pakietów. Sieć szkieletowa usług wdraża aplikacje z pakietu aplikacji hello przechowywane w magazynie obraz powitania, magazynu obiektów blob platformy Azure lub hello usługa systemowa sieci szkieletowej usług.
3. Hello *operator* następnie inicjuje hello typu aplikacji w klastrze docelowym hello z pakietu przekazanej aplikacji hello przy użyciu hello [ **ProvisionApplicationAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **ServiceFabricApplicationType rejestru** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), lub hello [ **udostępnienia aplikacji** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
4. Po zainicjowaniu obsługi administracyjnej aplikacji hello *operator* uruchamia hello aplikacji z parametrami hello dostarczonych przez hello *administrator aplikacji* przy użyciu hello [  **CreateApplicationAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CreateApplicationAsync_System_Fabric_Description_ApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **ServiceFabricApplication nowy** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricapplication), lub hello [ **tworzenie Aplikacja** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/create-an-application).
5. Po wdrożeniu aplikacji hello *operator* hello używa [ **CreateServiceAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_CreateServiceAsync_System_Fabric_Description_ServiceDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Nowy ServiceFabricService** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice), lub hello [ **Utwórz usługę** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/create-a-service) na podstawie toocreate nowych wystąpień usługi dla aplikacji hello typy dostępność usług.
6. Aplikacja Hello jest teraz uruchomiona w klastrze usługi sieć szkieletowa hello.

Zobacz [wdrażania aplikacji](service-fabric-deploy-remove-applications.md) przykłady.

## <a name="test"></a>Testowanie
1. Po wdrożeniu toohello lokalnego klastra projektowego lub klaster testowy *usługi developer* uruchamia hello scenariusza testów wbudowanych trybu failover przy użyciu hello [ **FailoverTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenarioparameters#System_Fabric_Testability_Scenario_FailoverTestScenarioParameters) i [ **FailoverTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenario#System_Fabric_Testability_Scenario_FailoverTestScenario) klas lub hello [ **Invoke ServiceFabricFailoverTestScenario** polecenia cmdlet ](/powershell/module/servicefabric/invoke-servicefabricfailovertestscenario?view=azureservicefabricps). Scenariusz test pracy awaryjnej Hello jest uruchomiona usługa określony za pomocą ważne tooensure przejścia i tryb failover, że są nadal dostępne i działają.
2. Witaj *usługi developer* , a następnie uruchamia hello scenariusza testów wbudowanych chaos przy użyciu hello [ **ChaosTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenarioparameters#System_Fabric_Testability_Scenario_ChaosTestScenarioParameters) i [  **ChaosTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenario#System_Fabric_Testability_Scenario_ChaosTestScenario) klas lub hello [ **Invoke ServiceFabricChaosTestScenario** polecenia cmdlet](/powershell/module/servicefabric/invoke-servicefabricchaostestscenario?view=azureservicefabricps). Scenariusz testów chaos Hello losowo wywołuje wiele węzłów, pakietu kodu i usterek repliki do klastra hello.
3. Hello *usługi developer* [testów komunikacji usług](service-fabric-testability-scenarios-service-communication.md) przez tworzenie scenariuszy testowania, łączące replik podstawowych wokół hello klastra.

Zobacz [toohello wprowadzenie błędów Analysis Service](service-fabric-testability-overview.md) Aby uzyskać więcej informacji.

## <a name="upgrade"></a>Uaktualnienie
1. A *usługi developer* aktualizacji usług składowych hello aplikacji hello wystąpienia i/lub poprawki błędów i udostępnia nową wersję hello manifestu usługi.
2. *Deweloper aplikacji* zastępuje parameterizes ustawienia konfiguracji i wdrażania hello hello spójne usług i udostępnia nową wersję manifest aplikacji hello. Deweloper aplikacji Hello następnie dołącza hello nowe wersje hello usługi manifesty w aplikacji hello i zawiera nową wersję typu aplikacji hello w pakiecie aplikacji zaktualizowane.
3. *Administrator aplikacji* zawiera hello nowa wersja typu aplikacji hello w aplikacji docelowej hello aktualizując hello odpowiednie parametry.
4. *Operator* przekazywania hello zaktualizowaną aplikację pakietu toohello klastra image store z użyciem hello [ **CopyApplicationPackage** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_) lub hello [ **ServiceFabricApplicationPackage kopiowania** polecenia cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). pakiet aplikacji Hello zawiera manifest aplikacji hello i kolekcji hello usługi pakietów.
5. *Operator* przepisy hello nowej wersji aplikacji hello w klastrze docelowym hello przy użyciu hello [ **ProvisionApplicationAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_), hello [ **ServiceFabricApplicationType rejestru** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype), lub hello [ **udostępnienia aplikacji** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
6. *Operator* uaktualnień hello docelowej aplikacji toohello nowej wersji przy użyciu hello [ **UpgradeApplicationAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpgradeApplicationAsync_System_Fabric_Description_ApplicationUpgradeDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Start-ServiceFabricApplicationUpgrade** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationupgrade), lub hello [ **uaktualniania aplikacji** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/upgrade-an-application).
7. *Operator* kontroli hello postęp uaktualnienia za pomocą hello [ **GetApplicationUpgradeProgressAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_GetApplicationUpgradeProgressAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [  **Get-ServiceFabricApplicationUpgrade** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricapplicationupgrade), lub hello [ **uzyskać postęp uaktualniania aplikacji** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/get-the-progress-of-an-application-upgrade1).
8. W razie potrzeby hello *operator* modyfikuje i przywrócenie hello parametry hello bieżącego uaktualniania aplikacji przy użyciu hello [ **UpdateApplicationUpgradeAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpdateApplicationUpgradeAsync_System_Fabric_Description_ApplicationUpgradeUpdateDescription_System_TimeSpan_System_Threading_CancellationToken_), Witaj [ **Update-ServiceFabricApplicationUpgrade** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/update-servicefabricapplicationupgrade), lub hello [ **uaktualniania aplikacji aktualizacji** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/update-an-application-upgrade).
9. W razie potrzeby hello *operator* wycofuje hello bieżącego uaktualniania aplikacji przy użyciu hello [ **RollbackApplicationUpgradeAsync** — metoda](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RollbackApplicationUpgradeAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Start ServiceFabricApplicationRollback** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationrollback), lub hello [ **uaktualniania aplikacji wycofywania** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/rollback-an-application-upgrade).
10. Sieć szkieletowa usług uaktualnia aplikacji docelowej hello uruchomiona w klastrze hello bez utraty dostępności hello dowolnego z jego usług składowych.

Zobacz hello [samouczek uaktualniania aplikacji](service-fabric-application-upgrade-tutorial.md) przykłady.

## <a name="maintain"></a>Obsługa
1. Do uaktualnienia systemu operacyjnego i poprawki usługi sieć szkieletowa interfejsów z hello infrastruktury platformy Azure tooguarantee dostępności wszystkich aplikacji hello uruchomiona w klastrze hello.
2. Dla platformy Service Fabric toohello aktualizacje i poprawki Service Fabric uaktualnia się bez utraty dostępność aplikacji hello uruchomionych w klastrze hello.
3. *Administrator aplikacji* zatwierdza hello dodawania lub usuwania węzłów z klastra po przeanalizowaniu pojemności historyczne dane dotyczące użycia i planowanego przyszłego zapotrzebowania.
4. *Operator* dodaje i usuwa określony przez hello węzłów *administrator aplikacji*.
5. Gdy zostaną dodane nowe węzły, że tooor istniejące węzły są usuwane z klastra hello, Service Fabric automatycznie równoważy hello uruchomionych aplikacji we wszystkich węzłach klastra hello tooachieve optymalnej wydajności.

## <a name="remove"></a>Remove
1. *Operator* można usunąć określonego wystąpienia usług uruchomionych w klastrze hello bez usuwania hello całą aplikację przy użyciu hello [ **DeleteServiceAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_DeleteServiceAsync_System_Fabric_Description_DeleteServiceDescription_System_TimeSpan_System_Threading_CancellationToken_) , hello [ **ServiceFabricService Usuń** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricservice), lub hello [ **usunięcia usługi** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/delete-a-service).  
2. *Operator* można również usunąć wystąpienia aplikacji i wszystkich jego usług przy użyciu hello [ **DeleteApplicationAsync** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_DeleteApplicationAsync_System_Fabric_Description_DeleteApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_), hello [ **Usuń ServiceFabricApplication** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricapplication), lub hello [ **Usuń aplikację** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/delete-an-application).
3. Gdy zatrzymano usług i aplikacji hello hello *operator* można wstrzymał obsługi administracyjnej za pomocą hello typ aplikacji hello [ **UnprovisionApplicationAsync** — metoda](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UnprovisionApplicationAsync_System_String_System_String_System_TimeSpan_System_Threading_CancellationToken_), Witaj [ **Unregister-ServiceFabricApplicationType** polecenia cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype), lub hello [ **wstrzymał obsługi administracyjnej aplikacji** operacji REST](https://docs.microsoft.com/rest/api/servicefabric/unprovision-an-application). Cofanie aprowizacji typu aplikacji hello nie powoduje usunięcia pakietu aplikacji hello z hello magazynu ImageStore. Należy ręcznie usunąć pakiet aplikacji hello.
4. *Operator* pakiet aplikacji hello powoduje usunięcie z hello magazynu ImageStore przy użyciu hello [ **RemoveApplicationPackage** metody](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RemoveApplicationPackage_System_String_System_String_) lub hello [ **Usuń ServiceFabricApplicationPackage** polecenia cmdlet](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps).

Zobacz [wdrażania aplikacji](service-fabric-deploy-remove-applications.md) przykłady.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat tworzenia testowania i zarządzanie aplikacjami platformy Service Fabric i usług, zobacz:

* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Usługi Reliable Services](service-fabric-reliable-services-introduction.md)
* [Wdrażanie aplikacji](service-fabric-deploy-remove-applications.md)
* [Uaktualnianie aplikacji](service-fabric-application-upgrade.md)
* [Omówienie testowania](service-fabric-testability-overview.md)
