---
title: "Zabezpieczenia klastra usługi sieć szkieletowa: role klient | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano Witaj dwie role klienta i uprawnienia hello dostarczone toohello ról."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Kontrola dostępu oparta na rolach dla klientów sieci szkieletowej usług
Sieć szkieletowa usług Azure obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług: administratora i użytkownika. Kontrola dostępu umożliwia hello klastra administrator toolimit dostępu toocertain klastra operacje dla różnych grup użytkowników, co klaster hello bardziej bezpieczne.  

**Administratorzy** mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Domyślnie **użytkowników** może zawierać tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.

Witaj dwie role klient (administratora i klient) określa się w czasie hello tworzenia klastra, podając oddzielne certyfikaty dla każdego. Zobacz [zabezpieczeń klastra sieci szkieletowej usług](service-fabric-cluster-security.md) szczegółowe informacje na temat konfigurowania bezpiecznej klastra sieci szkieletowej usług.

## <a name="default-access-control-settings"></a>Domyślne ustawienia kontroli dostępu
Typ kontroli dostępu administratora Hello ma pełny dostęp tooall powitania klienta fabricclient z rolą interfejsów API. Może wykonywać wszystkie odczyty i zapisy na klaster sieci szkieletowej usług hello, w tym hello następujące operacje:

### <a name="application-and-service-operations"></a>Operacje usług i aplikacji
* **CreateService**: Tworzenie usługi                             
* **CreateServiceFromTemplate**: tworzenie za pomocą szablonu usługi                             
* **Funkcji updateservice modułu**: Usługa aktualizacji                             
* **DeleteService**: usuwanie usługi                             
* **ProvisionApplicationType**: aprowizacji typu aplikacji                             
* **Operacji CreateApplication**: tworzenie aplikacji                               
* **Funkcji deleteapplication modułu**: usuwanie aplikacji                             
* **UpgradeApplication**: uruchomienie lub przerywania uaktualnienia aplikacji                             
* **UnprovisionApplicationType**: aplikacji typu wstrzymania obsługi administracyjnej.                             
* **MoveNextUpgradeDomain**: wznawianie uaktualniania aplikacji z domeną jawne aktualizacji                             
* **ReportUpgradeHealth**: wznawianie uaktualniania aplikacji z hello Bieżący postęp uaktualniania                             
* **ReportHealth**: raportowania kondycji                             
* **PredeployPackageToNode**: przedwdrożeniowe interfejsu API                            
* **CodePackageControl**: ponowne uruchamianie pakiety kodu                             
* **RecoverPartition**: odzyskiwanie partycji                             
* **RecoverPartitions**: odzyskiwanie partycji                             
* **RecoverServicePartitions**: odzyskiwanie partycji usługi                             
* **RecoverSystemPartitions**: odzyskiwanie partycji usług systemowych                             

### <a name="cluster-operations"></a>Działanie klastra
* **ProvisionFabric**: MSI i/lub klastra manifestu inicjowania obsługi administracyjnej                             
* **UpgradeFabric**: uruchomienie uaktualnienia klastra                             
* **UnprovisionFabric**: MSI i/lub klastra manifestu wstrzymania obsługi administracyjnej                         
* **MoveNextFabricUpgradeDomain**: wznawianie uaktualniania klastra z domeną jawne aktualizacji                             
* **ReportFabricUpgradeHealth**: wznawianie uaktualniania klastra z hello Bieżący postęp uaktualniania                             
* **StartInfrastructureTask**: Uruchamianie zadań infrastruktury                             
* **FinishInfrastructureTask**: Kończenie zadań infrastruktury                             
* **InvokeInfrastructureCommand**: infrastruktury zadań zarządzania poleceń                              
* **ActivateNode**: aktywowanie węzła                             
* **DeactivateNode**: dezaktywacji węzła                             
* **DeactivateNodesBatch**: dezaktywowanie wiele węzłów                             
* **RemoveNodeDeactivations**: Przywracanie dezaktywacji na wielu węzłach                             
* **GetNodeDeactivationStatus**: Sprawdzanie stanu dezaktywację.                             
* **NodeStateRemoved**: raportowania stanu węzła usunięte                             
* **ReportFault**: raportowanie błędów                             
* **Operację FileContent**: obraz transfer plików klienta magazynu (toocluster zewnętrznych)                             
* **FileDownload**: obraz magazynu klienta pliku pobierania inicjowania (toocluster zewnętrznych)                             
* **InternalList**: obraz magazynu klienta pliku listy operacji (wewnętrzny)                             
* **Usuń**: Operacja usuwania klienta magazynu obrazu                              
* **Przekaż**: operacja przekazywania klienta magazynu obrazu                             
* **NodeControl**: uruchamianie, zatrzymywanie i ponowne uruchamianie węzłów                             
* **MoveReplicaControl**: przenoszenie replik z jednego węzła tooanother                             

### <a name="miscellaneous-operations"></a>Inne operacje
* **Polecenie ping**: klient polecenia ping                             
* **Zapytanie**: wszystkie zapytania dozwolone
* **NameExists**: sprawdza istnienie identyfikatora URI nazewnictwa                             

Typ kontroli dostępu użytkownika Hello jest domyślnie ograniczony toohello następujące operacje: 

* **EnumerateSubnames**: nazewnictwa URI — wyliczenie                             
* **EnumerateProperties**: nazw właściwości — wyliczenie                             
* **PropertyReadBatch**: operacje odczytu dla nazw właściwości                             
* **GetServiceDescription**: long sondowania usługi powiadomień i odczytywanie ich opisy usług                             
* **ResolveService**: Rozpoznawanie usługi opartej na zgodne                             
* **ResolveNameOwner**: rozpoznawanie nazw właściciela identyfikatora URI                             
* **ResolvePartition**: rozpoznawania usług systemowych                             
* **ServiceNotifications**: powiadomień usługi oparty na zdarzeniach                             
* **GetUpgradeStatus**: sondowanie statusu uaktualnienia aplikacji                             
* **GetFabricUpgradeStatus**: sondowanie statusu uaktualnienia klastra                             
* **InvokeInfrastructureQuery**: badania infrastruktury zadań                             
* **Lista**: operacja listy plików klienta magazynu obrazu                             
* **Funkcji resetpartitionload modułu**: resetowanie obciążenia dla jednostki trybu failover                             
* **Toggleverboseserviceplacementhealthreporting modułu**: przełączanie raportowania kondycji umieszczania pełne usługi                             

Kontrola dostępu administratora Hello ma również toohello dostępu powyższej operacji.

## <a name="changing-default-settings-for-client-roles"></a>Zmiana ustawień domyślnych dla ról klienta
W pliku manifestu klastra hello musisz podać klienta toohello możliwości administratora w razie potrzeby. Można zmienić wartości domyślne hello toohello przechodzi **ustawienia sieci szkieletowej** opcję podczas [Tworzenie klastra](service-fabric-cluster-creation-via-portal.md)i zapewnianie hello poprzedzające ustawienia hello **nazwa**, **admin**, **użytkownika**, i **wartość** pól.

## <a name="next-steps"></a>Następne kroki
[Zabezpieczenia klastra sieci szkieletowej usług](service-fabric-cluster-security.md)

[Tworzenie klastra sieci szkieletowej usług](service-fabric-cluster-creation-via-portal.md)

