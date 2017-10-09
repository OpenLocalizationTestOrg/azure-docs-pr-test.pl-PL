---
title: "aaaArchitecture sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług to platforma systemów rozproszonych używane toobuild skalowalne, niezawodne i łatwo zarządzać aplikacji hello chmury. W tym artykule przedstawiono hello architektury sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Architektura usługi Service Fabric
Sieć szkieletowa usług jest tworzone za podsystemów warstwowego. Te podsystemy Włącz toowrite aplikacje, które są:

* Wysokiej dostępności
* Skalowalność
* Zarządzane
* Konstruowanie

powitania po diagram przedstawia hello głównych podsystemami sieci szkieletowej usług.

![Diagram architektury sieci szkieletowej usług](media/service-fabric-architecture/service-fabric-architecture.png)

W rozproszonym systemie hello toosecurely możliwości komunikacji między węzłami w klastrze jest niezwykle istotne. Na powitania podstawowy stosu hello jest hello transportu podsystemu, który zapewnia bezpiecznej komunikacji między węzłami. Powyżej transportu hello podsystemu leży podsystemu federacyjnego hello, w których klastrów hello różnych węzłów do pojedynczej jednostki (o nazwie klastrów), aby sieci szkieletowej usług można wykrywanie błędów, wykonaj Elekcja wiodące i zapewnić spójne routingu. Podsystem niezawodności Hello, w warstwie ponad podsystemu federacyjnego hello, jest odpowiedzialny za hello niezawodności usługi sieć szkieletowa usług za pomocą mechanizmów replikacji, zarządzanie zasobami i pracy awaryjnej. Podsystem federacyjnego Hello jest również podsystemu hello hosting i aktywacji, który umożliwia zarządzanie hello cyklem życia aplikacji w jednym węźle. podsystemu zarządzania Hello zarządza hello cyklem życia aplikacji i usług. Podsystem zmianę Hello ułatwia deweloperom aplikacji test swoich usług za pomocą symulowane błędy przed i po wdrożeniu środowiska tooproduction aplikacji i usług. Sieć szkieletowa usług umożliwia określenie hello tooresolve lokalizacji usług za pośrednictwem jego podsystemu komunikacji. toodevelopers widoczne modele programowania aplikacji Hello są warstwie ponad te podsystemy razem z narzędziami tooenable modelu aplikacji hello.

## <a name="transport-subsystem"></a>Podsystem transportu
Podsystem transportu Hello implementuje kanał komunikacji datagram point-to-point. Ten kanał jest używana do komunikacji w ramach klastrów sieci szkieletowej usług i komunikacji między klastra sieci szkieletowej usług hello i klientami. Obsługuje ona jednokierunkowe i wzorce komunikacji żądanie odpowiedź, które stanowi podstawę hello wykonania emisji i multiemisji w hello warstwy federacji. Podsystem transportu Hello zabezpiecza komunikację przy użyciu X509 certyfikatów lub zabezpieczenia systemu Windows. Podsystem ten jest używana wewnętrznie przez usługi sieć szkieletowa usług i nie jest dostępny bezpośrednio toodevelopers programowania aplikacji.

## <a name="federation-subsystem"></a>Podsystem federacyjnego
W kolejności tooreason o zestawie węzłów Rozproszony system należy toohave spójne wyświetlanie hello systemu. Podsystem federacyjnego Hello używa podstawowych komunikacji hello udostępniane przez podsystem transportu hello i rzędów oczek hello różnych węzłów w klastrze ujednoliconego pojedynczego może on przyczyny o. Zapewnia podstawowych systemów rozproszonych hello wymagane przez hello innych podsystemów — wykrywanie błędów, wybór wiodące i spójne routingu. Podsystem federacyjnego Hello jest oparty na tabelach skrótów rozproszonej ze spacją tokenu 128-bitowego. Podsystem Hello tworzy topologia pierścienia za pośrednictwem hello węzłów z każdego węzła w pierścień hello są przydzielone podzbiór miejsca tokenu hello własności. Do wykrywania awarii warstwy hello używa mechanizm dzierżawienia na podstawie serca bicie i rozstrzygnięcia. Podsystem federacyjnego Hello gwarantuje również za pośrednictwem skomplikowanych sprzężenia i wyjścia protokołów, które istnieje tylko jeden właściciel tokenu w dowolnym momencie. Zapewnia to wybór wiodące i spójne gwarancje routingu.

## <a name="reliability-subsystem"></a>Podsystem niezawodności
Hello podsystemu niezawodności udostępnia hello mechanizm toomake hello stanu usługi sieć szkieletowa usług wysokiej dostępności przy użyciu hello hello *replikatora*, *menedżera trybu Failover*, i  *Moduł równoważenia zasobów*.

* Witaj replikatora zapewnia zmiany stanu w replice podstawowej usługi hello zostanie automatycznie replikowane toosecondary replik, w zachowaniu spójności między hello podstawowych i pomocniczych replik w zestawie replik usługi. Replikator Hello jest odpowiedzialny za zarządzanie kworum między replikami hello hello zestawu replik. Interakcji z hello trybu failover jednostki tooget hello lista tooreplicate operacji, a agent rekonfiguracji hello zapewnia konfiguracji hello hello zestawu replik. Tej konfiguracji wskazuje, jakie operacje hello repliki należy toobe replikowane. Usługa Service Fabric realizuje replikatora domyślne, nazywany Replikator sieci szkieletowej, które mogą być używane przez hello programowania modelu interfejsu API toomake hello stan usługi wysokiej dostępności i niezawodne.
* Hello menedżera trybu Failover gwarantuje, że podczas dodawania węzłów tooor usunięta z klastra hello, obciążenia hello jest automatycznej redystrybucji dostępnych węzłach hello. W przypadku niepowodzenia węzła w klastrze hello hello klastra automatycznie konfigurację dostępności toomaintain repliki usługi hello.
* Hello Resource Manager umieszcza repliki usługi w domenie awarii w klastrze hello i zapewnia, że wszystkie jednostki trybu failover są operacyjną. Hello Resource Manager również równoważy zasobów usługi na powitania bazowy współużytkowanej puli dystrybucji obciążenia uniform optymalne tooachieve węzłów klastra.

## <a name="management-subsystem"></a>Podsystemu zarządzania
podsystemu zarządzania Hello udostępnia usługi end-to-end i zarządzanie cyklem życia aplikacji. Polecenia cmdlet programu PowerShell i interfejsów API administracyjne pozwalają tooprovision, wdrażanie, poprawki uaktualnienia i anulować aprowizację aplikacji bez utraty dostępności. podsystemu zarządzania Hello wykonuje to za pośrednictwem hello następujących usług.

* **Menedżer klastra**: jest to hello podstawowa usługa, która współdziała z hello menedżera trybu Failover z poziomu aplikacji hello tooplace niezawodności na węzłach hello oparte na ograniczenia umieszczania usług hello. Hello Menedżera zasobów w podsystemie pracy awaryjnej zapewnia, że ograniczenia hello nigdy nie są przerwane. Menedżer klastra Hello zarządza hello cyklem życia aplikacji hello z udostępniania toode-provision. Umożliwia integrację z tooensure Menedżera kondycji hello czy dostępności aplikacji nie jest z punktu widzenia semantycznego kondycji podczas uaktualniania.
* **Menedżer kondycji**: Usługa ta umożliwia monitorowanie kondycji aplikacji, usług i jednostek klastra. Informacje o kondycji, które agregowane w magazynie kondycji scentralizowane hello zgłosić jednostki klastra (na przykład węzłów, usługi partycji i replik). Te informacje o kondycji zawiera migawkę kondycji ogólnej w momencie hello usługi i rozproszone na wielu węzłach w klastrze hello, umożliwiając tootake węzłów wszelkie niezbędne działania korygujące. Kwerenda kondycji interfejsów API umożliwiają zdarzenia kondycji hello tooquery zgłosił toohello kondycji podsystemu. zapytania kondycji Hello interfejsów API zwrócić przechowywania danych pierwotnych kondycji hello przechowywanych w kondycji hello lub hello zagregowane, interpretowane danych kondycji dla obiektu określonego klastra.
* **Obraz magazynu**: ta usługa udostępnia przechowywania i dystrybucji hello plików binarnych aplikacji. Ta usługa udostępnia magazyn plików rozproszonych proste skutkującej przekazane tooand pobrane z aplikacji hello.

## <a name="hosting-subsystem"></a>Podsystem hostingu
Menedżer klastra Hello informuje o hello hosting podsystemu (uruchomione w każdym węźle), który ją serwisuje musi toomanage dla określonego węzła. następnie hosting podsystemu Hello zarządza hello cyklem życia aplikacji hello w tym węźle. Interakcji z hello niezawodność i kondycji składników tooensure czy hello repliki są poprawnie umieszczony i są w dobrej kondycji.

## <a name="communication-subsystem"></a>Podsystem komunikacji
Podsystem ten zapewnia niezawodna obsługa komunikatów w ramach odnajdywania klastra i usługi za pośrednictwem usługi nazewnictwa hello hello. Hello Naming service jest rozpoznawany jako lokalizacja tooa nazwy usługi w klastrze hello i umożliwia użytkownikom toomanage usługi nazwy i właściwości. Przy użyciu usługi nazewnictwa hello klientów może bezpiecznie komunikować się z żadnym węźle tooresolve klastra hello nazwę usługi i pobrać metadanych usługi. Użytkownicy sieci szkieletowej usług za pomocą prostego nazewnictwa klienta interfejsu API, można utworzyć usług i klientów obsługujących rozpoznawania hello bieżącą lokalizację sieciową pomimo dynamiki węzła lub hello ponownie zmiany rozmiaru klastra hello.

## <a name="testability-subsystem"></a>Podsystem testowania
Pola to pakiet narzędzi zaprojektowane specjalnie dla usługi sieci szkieletowej usług w oparciu testowania. Witaj narzędzia let dewelopera łatwo wywołać znaczenie błędów i uruchom tooexercise scenariuszy testu i sprawdzanie poprawności hello wiele stanów i przejść, które usługa może wystąpić w jego okres istnienia w sposób kontrolowanych i bezpiecznych. Pola są także toorun mechanizmu dłużej testy, które można wykonać iterację różne możliwe błędy bez utraty dostępności. Udostępnia środowiska testowego w środowisku produkcyjnym.

