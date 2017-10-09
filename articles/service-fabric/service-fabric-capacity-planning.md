---
title: "aaaCapacity planowania dla aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooidentify hello liczba węzłów obliczeniowych wymagane dla aplikacji sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Planowanie wydajności dla aplikacji sieci szkieletowej usług
Ten dokument zawiera jak tooestimate hello ilości zasobów (procesorów CPU, pamięci RAM, Magazyn dyskowy) należy toorun aplikacji sieci szkieletowej usług Azure. Są często z toochange wymagania dotyczące zasobów w czasie. Tworzenie i testowanie usługi, a następnie wymaga większej ilości zasobów, przejdź do środowiska produkcyjnego i rozwoju aplikacji w popularne zwykle wymagają niewielkiej ilości zasobów. Podczas projektowania aplikacji przemyślenie hello długoterminowych wymagań i opcji zezwalających na Twojej usługi tooscale toomeet wysoki popyt.

 Podczas tworzenia klastra usługi sieć szkieletowa zdecyduj, jakie rodzaje maszynach wirtualnych (VM) tworzą hello klastra. Każda maszyna wirtualna jest dostarczany z ograniczoną ilością zasobów w formie hello procesorów CPU (rdzenie i szybkości), przepustowości sieci, pamięci RAM i magazynu danych na dysku. Wraz z rozwojem usługi wraz z upływem czasu, można uaktualnić tooVMs, które oferują większe zasoby i/lub Dodaj więcej klaster tooyour maszyn wirtualnych. hello toodo drugie, użytkownik musi projektowania usługi początkowo, może korzystać z nowych maszyn wirtualnych, które są dodawane dynamicznie toohello klastra.

Niektóre usługi Zarządzanie małego danych toono na powitania maszyn wirtualnych, samodzielnie. Planowanie dla tych usług należy skoncentrować się głównie na wydajność, co oznacza wybranie hello pojemności właściwe procesorów CPU (rdzenie i szybkość) hello maszyn wirtualnych. Ponadto należy rozważyć przepustowość sieci, w tym, jak często występuje transferów sieci oraz jak dużo danych jest przenoszona. Jeśli usługa wymaga tooperform również wraz ze wzrostem użycia usługi, możesz dodać więcej klaster toohello maszyn wirtualnych i zrównoważenia obciążenia hello sieci żądaniami na wszystkich maszynach wirtualnych hello.

Dla usług, które Zarządzanie dużych ilości danych na powitania maszyn wirtualnych planowania pojemności należy skoncentrować się przede wszystkim od rozmiaru. W związku z tym należy rozważyć hello pojemność magazynu pamięci RAM i dysku hello maszyny Wirtualnej. Hello system zarządzania pamięci wirtualnej w systemie Windows sprawia, że wyglądać kodu tooapplication pamięci RAM miejsca na dysku. Ponadto środowisko uruchomieniowe usługi sieć szkieletowa hello zapewnia zachowania tylko gorących danych w pamięci i przenoszenie toodisk zimnych danych hello stronicowanie inteligentne. W związku z tym aplikacjom więcej pamięci niż jest fizycznie dostępna na powitania maszyny Wirtualnej. Po prostu mających więcej pamięci RAM zwiększa wydajność, ponieważ hello maszyny Wirtualnej można przechowywać więcej miejsca w pamięci RAM. Witaj wybrania maszyny Wirtualnej powinny mieć dane hello toostore dostatecznie dużego dysku, które mają na powitania maszyny Wirtualnej. Podobnie hello maszyny Wirtualnej powinny mieć tooprovide wystarczającej ilości pamięci RAM, program hello wydajności, które chcesz. Jeśli dane z usługą rozwoju wraz z upływem czasu, dane można dodać więcej maszyn wirtualnych toohello klastra i partycja hello na wszystkich maszynach wirtualnych hello.

## <a name="determine-how-many-nodes-you-need"></a>Określić liczbę węzłów należy
Partycjonowanie usługi umożliwia tooscale dane z usługą. Aby uzyskać więcej informacji na partycje, zobacz [partycjonowania usługi sieć szkieletowa](service-fabric-concepts-partitioning.md). Każda partycja musi mieścić się w jednej maszyny Wirtualnej, ale wiele partycji (małe) można umieścić na jednej maszynie Wirtualnej. Tak mających więcej partycji małych zapewnia większą elastyczność niż w przypadku kilku większych partycji. rozwiązanie Hello jest, że wiele partycji zwiększa obciążenie sieci szkieletowej usług i nie można wykonać operacje transakcyjne na partycje. Istnieje również więcej potencjalnych ruchu sieciowego, jeśli kod usługi często wymaga tooaccess fragmentów danych, które znajdują się w różnych partycji. Podczas projektowania usługi, należy rozważyć te zalet i wad tooarrive w efektywnej strategii partycjonowania.

Załóżmy, że aplikacja ma jednej usługi stanowej, która ma oczekiwać toogrow tooDB_Size GB w roku rozmiar magazynu. Są ujawniane tooadd więcej aplikacji (i partycje) jako występują wzrostu poza tym roku.  Hello replikacji czynnikiem, (RF), który określa hello liczby replik dla całkowita DB_Size hello wpływa na Twojej usługi. Witaj całkowita DB_Size we wszystkich replik jest hello pomnożona przez DB_Size współczynnik replikacji.  Node_Size reprezentuje miejsca na dysku hello/RAM na węzeł ma toouse dla usługi. Aby uzyskać najlepszą wydajność hello DB_Size powinny mieścić się w pamięci na powitania klastra i Node_Size, który jest wokół hello pamięci RAM powitalne powinna być wybrana maszyna wirtualna. Przydzielając Node_Size, który jest większy niż pojemność pamięci RAM hello są zależne stronicowania hello udostępniane przez środowisko uruchomieniowe usługi sieć szkieletowa hello. W związku z tym wydajności mogą nie być optymalne, jeśli cały danych jest uznawany za toobe gorących (od momentu następnie powitalne danych jest stronicowana We/Wy). Jednak w przypadku wielu usług przypadku gorących tylko część danych hello jest bardziej ekonomiczne rozwiązanie.

Hello liczba węzłów dla maksymalnej wydajności można obliczyć w następujący sposób:

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Konto dla rozwoju
Możesz toocompute hello liczba węzłów, na podstawie hello DB_Size oczekiwanego toogrow Twojej usługi, oprócz toohello DB_Size rozpoczęcia z. Następnie rosnąć hello liczba węzłów, wraz z rozwojem usługi tak, aby nie są przerostu hello liczba węzłów. Ale hello liczby partycji powinny być oparte na powitania liczba węzłów, które są wymagane, gdy używasz usługi na maksymalny wzrost.

Jego jest dobrym toohave niektóre dodatkowe maszyny dostępne w dowolnym momencie, dzięki czemu (na przykład, jeśli kilka maszyn wirtualnych przestaną działać) może obsłużyć ani nagłego nieoczekiwany błąd.  Chociaż hello bardzo pojemności należy określić przy użyciu Twojej oczekiwanej wartości szczytowe, punkt początkowy jest tooreserve kilka dodatkowych maszyn wirtualnych (5 – 10 procent dodatkowe).

Hello poprzedniego zakłada jednej usługi stanowej. Jeśli masz więcej niż jednej usługi stanowej, masz hello tooadd DB_Size skojarzone z hello innych usług na powitania równości. Alternatywnie można obliczyć hello liczba węzłów osobno dla każdej usługi stanowej.  Usługa może być repliki lub partycji, które nie są zrównoważonym. Należy pamiętać, że partycji może mieć więcej danych niż inne. Aby uzyskać więcej informacji na partycje, zobacz [partycjonowania artykuł na temat najlepszych rozwiązań](service-fabric-concepts-partitioning.md). Witaj poprzedniego równości jest jednak partycji i replik niezależny, ponieważ sieć szkieletowa usług gwarantuje, że repliki hello są rozproszone między węzłami hello w optymalny sposób.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Arkusz kalkulacyjny na użytek obliczenie kosztów
Teraz umieśćmy kilka liczb rzeczywistych hello formuły. [Arkusza kalkulacyjnego przykład](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) pokazuje, jak tooplan hello pojemności dla aplikacji, która zawiera trzy typy obiektów danych. Dla każdego obiektu możemy zbliżenie jego rozmiar i obiekty ile oczekujemy toohave. Możemy również wybrać liczby replikami chcemy każdego typu obiektu. Arkusz kalkulacyjny Hello oblicza hello łączną ilość pamięci toobe przechowywane w klastrze hello.

Następnie możemy wprowadź rozmiar maszyny Wirtualnej i miesięcznych kosztów. Oparte na powitania rozmiar maszyny Wirtualnej, arkusz kalkulacyjny hello informuje, że hello minimalną liczbę partycji, należy użyć toosplit Twojego toophysically danych mieści się w węzłach hello. Może chcesz większej liczby partycji tooaccommodate, potrzebne w Twojej aplikacji określonego ruchu obliczeń i sieci. Arkusz kalkulacyjny Hello pokazuje hello liczby partycji, które są zarządzania obiektami profilu użytkownika hello wzrosło z jednego toosix.

Teraz oparte na tych informacji, arkusz kalkulacyjny hello pokazuje, czy fizycznie można pobrać wszystkich danych hello hello potrzeby partycji i replik w klastrze 26 węzła. Jednak ten klaster będzie gęsto zapewniać, dlatego może być niektórych awarii węzła tooaccommodate dodatkowe węzły i uaktualnień. Arkusz kalkulacyjny Hello pokazuje też, że mających więcej niż 57 węzłów nie określa żadnej dodatkowe wartości, ponieważ miałoby węzłami pusty. Ponownie możesz toogo powyżej 57 węzłów mimo to tooaccommodate awarii węzła i uaktualnień. Można dostosować toomatch arkusza kalkulacyjnego hello specyficznych potrzeb Twojej aplikacji.   

![Arkusza kalkulacyjnego w celu obliczenia kosztu][Image1]

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z [partycjonowania usługi sieć szkieletowa usług] [ 10] toolearn więcej informacji na temat partycjonowania usługi.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
