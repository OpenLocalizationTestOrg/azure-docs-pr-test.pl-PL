---
title: "aaaVisualizing klastra za pomocą Eksploratora usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "Eksploratora usługi sieć szkieletowa jest oparte na sieci web narzędzie do sprawdzania i zarządzanie aplikacjami w chmurze i węzłów w klastrze usługi sieć szkieletowa usług Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer
Eksploratora usługi sieć szkieletowa jest oparte na sieci web narzędzie do sprawdzania i zarządzanie aplikacjami i węzły w klastrze usługi sieć szkieletowa usług Azure. Service Fabric Explorer znajduje się bezpośrednio w klastrze hello, dzięki czemu jest zawsze dostępne, niezależnie od tego, w którym jest uruchomiona klastra.

## <a name="video-tutorial"></a>Samouczek wideo

jak toouse Service Fabric Explorer, obejrzyj toolearn hello po wideo Microsoft Virtual Academy:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Połącz tooService Fabric Explorer
Jeśli zostały wykonane instrukcje hello zbyt[przygotowywanie środowiska projektowego](service-fabric-get-started.md), Service Fabric Explorer można uruchomić w klastrze lokalnym, przechodząc toohttp://localhost:19080 / Explorer.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Zrozumienie hello układu Service Fabric Explorer
Za pomocą Eksploratora usługi sieć szkieletowa można nawigować przy użyciu hello drzewa po lewej stronie powitania. Witaj katalogu głównego drzewa hello pulpit nawigacyjny klastra hello zawiera omówienie klastra, w tym podsumowanie aplikacji i kondycji węzła.

![Pulpit nawigacyjny klastra Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Wyświetl układ hello klastra
Węzły w klastrze usługi sieć szkieletowa usług są umieszczane między dwuwymiarowa siatki domen błędów i uaktualnienia domen. Ten umieszczania gwarantuje, że aplikacje pozostają dostępne w obecności hello awarie sprzętu i uaktualnień aplikacji. Możesz wyświetlić bieżący klaster hello układ przy użyciu mapy klastra hello.

![Mapa klastra Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Wyświetl aplikacje i usługi
Witaj klaster zawiera dwa poddrzewa: jeden dla aplikacji i drugi dla węzłów.

Można użyć toonavigate widoku aplikacji hello za pośrednictwem usługi Service Fabric logicznej hierarchii: aplikacji, usług, partycji i replik.

W poniższym przykładzie hello, hello aplikacji **moja_aplikacja** składa się z dwóch usług **MyStatefulService** i **WebService**. Ponieważ **MyStatefulService** jest obiektem stanowym, zawiera partycji z jednego podstawowego i dwóch replik pomocniczych. Z kolei WebSvcService jest bezstanowych i zawiera pojedyncze wystąpienie.

![Widok aplikacji w narzędziu Service Fabric Explorer][sfx-application-tree]

Na każdym poziomie drzewa hello hello głównego w okienku zostaną wyświetlone odpowiednie informacje o elemencie hello. Można na przykład zobacz hello stan kondycji i wersji określonej usługi.

![Okienko essentials Service Fabric Explorer][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Wyświetlanie węzłów klastra hello
Widok węzła Hello przedstawia hello fizycznego układu hello klastra. Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle. W szczególności widać replik, które są aktualnie uruchomione istnieje.

## <a name="actions"></a>Akcje
Service Fabric Explorer oferuje tooinvoke szybkie akcje na węzłach, aplikacji i usług w ramach klastra.

Na przykład toodelete wystąpienie aplikacji wybierz aplikacji hello z hello drzewa po lewej stronie powitania, a następnie wybierz **akcje** > **Usuń aplikację**.

![Usunięcie aplikacji w narzędziu Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> Można wykonywać hello same akcje, klikając przycisk wielokropka hello następnego elementu tooeach.
>
>

Witaj Poniższa tabela zawiera listę dostępnych dla każdej jednostki akcji hello:

| **Jednostki** | **Akcja** | **Opis** |
| --- | --- | --- |
| Typ aplikacji |Cofnij aprowizację typu |Usunięcie pakietu aplikacji hello z magazynu obrazu klastra hello. Wymaga wszystkie aplikacje tego typu toobe, najpierw usunąć. |
| Aplikacja |Usuń aplikację |Usunięcie aplikacji hello, łącznie z jej usług i ich stan (jeśli istnieje). |
| Usługa |Usuwanie usługi |Usuń usługi hello i jego stan (jeśli istnieje). |
| Węzeł |Activate |Aktywuj hello węzła. |
| Węzeł | Dezaktywuj (Wstrzymaj) | Wstrzymaj węzeł hello w jego bieżącym stanie. Usługi nadal toorun, ale usługi sieć szkieletowa nie aktywnego przenosi niczego na lub wyłącz go, chyba że jest wymagane tooprevent awarii lub niespójność danych. Ta akcja jest zwykle używana tooenable debugowanie usług na tooensure określonego węzła, który nie należy przenosić podczas kontroli. | |
| Węzeł | Dezaktywuj (ponowne uruchomienie) | Bezpieczne przenoszenie wszystkich usług w pamięci wyłącz węzeł i zamknij usług trwałych. Zazwyczaj używany podczas hello procesy hosta lub maszyny toobe konieczność ponownego uruchomienia. | |
| Węzeł | Dezaktywuj (Usuń dane) | Bezpiecznie zamknąć wszystkie usługi uruchomione w węźle powitania po utworzeniu wystarczające zapasowe replik. Zazwyczaj używane do węzła (lub co najmniej jej magazynem) jest przełączana trwale poza Komisji. | |
| Węzeł | Usuń stan węzła | Usuń wiedzy replik węzła z klastra hello. Zazwyczaj używany podczas uznaje nieodwracalny węzeł już nie powiodło się. | |
| Węzeł | Ponowne uruchamianie | Symulację awarii węzła poprzez ponowne uruchomienie węzła hello. Więcej informacji [tutaj](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Ponieważ wiele działań destrukcyjnego, może być zadawane tooconfirm Twojego zamiar przed zakończeniem działania hello.

> [!TIP]
> Wszystkie akcje, które mogą być wykonywane za pomocą Eksploratora usługi sieć szkieletowa można również przeprowadzić za pomocą programu PowerShell lub interfejsu API REST, tooenable automatyzacji.
>
>

Umożliwia także wystąpień aplikacji usługi Service Fabric Explorer toocreate aplikacji danego typu i wersji. Wybierz typ aplikacji hello w widoku drzewa hello, a następnie kliknij przycisk hello **Utwórz wystąpienie aplikacji** łącze następnej wersji toohello chcesz w okienku po prawej stronie powitania.

![Tworzenie wystąpienia aplikacji w narzędziu Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> Obecnie nie mogą być parametryczne wystąpień aplikacji utworzonych za pomocą Eksploratora usługi sieć szkieletowa. Są one tworzone przy użyciu wartości parametrów domyślnych.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Połącz tooa zdalnego klastra sieci szkieletowej usług
Jeśli znasz punktu końcowego hello klastra i masz wystarczające uprawnienia dostępne Service Fabric Explorer z dowolnej przeglądarki. Jest to spowodowane Eksploratora usługi sieć szkieletowa jest po prostu innej usługi, która działa w klastrze hello.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Odnajdywanie punktu końcowego Service Fabric Explorer hello zdalnego klastra
tooreach Service Fabric Explorer, w przypadku danego klastra punktu przeglądarkę, aby:

http://&lt;your klastra endpoint&gt;: 19080/Explorer

W przypadku klastrów Azure hello pełny adres URL jest również dostępna w okienku essentials klastra hello hello portalu Azure.

### <a name="connect-tooa-secure-cluster"></a>Połącz tooa bezpiecznego klastra
Można kontrolować klienta dostępu tooyour klastra sieci szkieletowej usług z certyfikatów lub przy użyciu usługi Azure Active Directory (AAD).

Jeśli tooconnect tooService Eksploratora sieci szkieletowej w klastrze bezpieczny, następnie w zależności od konfiguracji klastra hello można będzie można toopresent wymagany certyfikat klienta lub zaloguj się za pomocą usługi AAD.

## <a name="next-steps"></a>Następne kroki
* [Omówienie testowania](service-fabric-testability-overview.md)
* [Zarządzanie aplikacji usługi Service Fabric w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Wdrażanie aplikacji sieci szkieletowej usług za pomocą programu PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
