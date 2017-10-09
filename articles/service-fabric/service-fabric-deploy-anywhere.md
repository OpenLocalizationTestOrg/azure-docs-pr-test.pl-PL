---
title: "Sieć szkieletowa usług Azure aaaCreate klastrów w systemie Windows Server i Linux | Dokumentacja firmy Microsoft"
description: "Uruchom na serwerze z systemem Windows i Linux, co oznacza, możesz klastrów sieci szkieletowej usług będzie możliwe toodeploy i sieci szkieletowej usług aplikacji hosta gdziekolwiek można uruchomić w systemie Windows Server lub Linux."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Tworzenie klastrów sieci szkieletowej usług na serwerze z systemem Windows lub Linux
Klaster sieci szkieletowej usług Azure to zestaw połączonych z siecią maszyn wirtualnych lub fizycznych, w których są wdrożone i zarządzane z mikrousług. Komputer lub maszynę Wirtualną, która jest częścią klastra jest nazywany węzłem klastra. Klastrów można skalować toothousands węzłów. Po dodaniu nowego klastra toohello węzłów sieci szkieletowej usług rebalances replik partycji usługi hello i wystąpień między hello zwiększenie liczby węzłów. Ogólne poprawia wydajność aplikacji i zmniejsza rywalizacji o toomemory dostępu. Jeśli nie są wydajnie używane hello węzłów w klastrze hello, można zmniejszyć hello liczby węzłów w klastrze hello. Sieć szkieletowa usług ponownie rebalances hello replik partycji i wystąpień między hello zmniejszyć liczbę węzłów toomake lepsze wykorzystanie sprzętu hello w każdym węźle.

Sieć szkieletowa usług umożliwia tworzenie hello klastrów sieci szkieletowej usług na dowolnym maszyn wirtualnych lub komputerach z systemem Windows Server lub Linux. Oznacza to, są w stanie toodeploy i uruchamianie aplikacji sieci szkieletowej usług w każdym środowisku, w którym znajduje się zestaw komputerów systemu Windows Server lub Linux, które są połączone ze sobą, można go w infrastrukturze lokalnej, Microsoft Azure lub u innego dostawcy chmury.

## <a name="create-service-fabric-clusters-on-azure"></a>Tworzenie klastrów sieci szkieletowej usług na platformie Azure
Tworzenie klastra na platformie Azure odbywa się za pośrednictwem szablonu modelu zasobów lub hello portalu Azure. Odczyt [tworzenia klastra usługi sieć szkieletowa usług za pomocą szablonu usługi Resource Manager](service-fabric-cluster-creation-via-arm.md) lub [Tworzenie klastra sieci szkieletowej usług z portalu Azure hello](service-fabric-cluster-creation-via-portal.md) Aby uzyskać więcej informacji.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Obsługiwane systemy operacyjne dla klastrów w systemie Azure
Jesteś toocreate stanie klastrów na maszynach wirtualnych z tymi systemami operacyjnymi:

* Windows Server 2012 R2
* Windows Server 2016 
* 16.04 Ubuntu Linux (w publicznej wersji zapoznawczej) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Tworzenie autonomicznej usługi sieć szkieletowa klastrów lokalnymi lub z każdego dostawcy chmury
Sieć szkieletowa usług przewiduje pakietu instalacji możesz toocreate autonomicznej usługi sieć szkieletowa klastrów lokalnymi lub dla dowolnego dostawcy chmury

Więcej informacji na temat konfigurowania sieci szkieletowej usług autonomicznych klastrów w systemie Windows Server, przeczytaj [tworzenia klastra usługi sieć szkieletowa usług dla systemu Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Wszystkie wdrożenia chmury i wdrożeniach lokalnych
Hello procesu tworzenia klastra usługi sieć szkieletowa usług lokalnych jest podobne toohello procesu tworzenia klastra na żadną chmurą dowolnego z zestawem maszyn wirtualnych. Witaj początkowe kroki tooprovision Witaj maszyny wirtualne są regulowane hello dostawcy usług w chmurze lub środowiska lokalnego, którego używasz. Po utworzeniu zestawu maszyn wirtualnych o łączności sieciowej z włączoną między nimi, następnie hello tooset kroki zapasowej hello pakietu sieci szkieletowej usług, ustawienia klastra hello Uruchom hello na utworzenie klastra i edytować skrypty zarządzania są identyczne. Dzięki temu Twojej wiedzy i doświadczenia, obsługi i zarządzania klastrami usługi sieć szkieletowa usług są przeniesieniu po wybraniu tootarget nowego środowiska hostingu.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Korzyści wynikające z tworzenia autonomicznych klastrów sieci szkieletowej usług
* Są wolne toochoose żadnego toohost dostawcy chmury klastra.
* Można uruchomić aplikacji usługi Service Fabric, zapisane raz, w wielu środowiskach hostingu z minimalnym toono zmiany.
* Wiedzę na temat tworzenia aplikacji sieci szkieletowej usług są przenoszone z jednego tooanother środowiska hostingu.
* Środowisko operacyjne uruchamiania i zarządzania sieci szkieletowej usług klastrów wykonuje za pośrednictwem z tooanother jednego środowiska.
* Zasięg szerokie klienta jest niepowiązany, udostępniając ograniczenia środowiska.
* Dodatkową warstwę niezawodności i ochrony przed powszechnie awarie istnieje, ponieważ można przenieść usług hello nad środowiskiem wdrażania tooanother Jeśli centrum danych lub dostawcy usług w chmurze ma niedostępności.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Obsługiwane systemy operacyjne dla autonomicznych klastrów
Jesteś toocreate stanie klastrów na maszynach wirtualnych lub komputerach z tymi systemami operacyjnymi:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (wkrótce)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Zalety klastrów sieci szkieletowej usług na platformie Azure za pośrednictwem klastrów sieci szkieletowej usług autonomiczny utworzony lokalnie
Działające klastry usługi sieć szkieletowa usług Azure udostępnia zalet w porównaniu z hello w trybie lokalnym, więc jeśli nie ma określonych potrzeb, na którym uruchamiasz klastrów, następnie Sugerujemy uruchom je na platformie Azure. Na platformie Azure udostępniamy integracji z innymi usługami, dzięki czemu operacje i zarządzania klastra hello łatwiejsze i bardziej niezawodny i funkcje platformy Azure.

* **Portalu Azure:** portalu Azure umożliwia łatwe toocreate i zarządzania klastrami.
* **Usługa Azure Resource Manager:** użycia usługi Azure Resource Manager umożliwia łatwe zarządzanie wszelkie zasoby używane przez klaster hello jako jednostki i upraszcza śledzenie kosztów i rozliczeń.
* **Klastra sieci szkieletowej usług jako zasób Azure** klastra sieci szkieletowej usług A jest zasobem ARM, więc może ona modelu, jak inne zasoby ARM na platformie Azure.
* **Integracja z infrastrukturą platformy Azure** sieci szkieletowej usług koordynuje z hello podstawowej infrastruktury platformy Azure dla systemu operacyjnego, sieci i innych uaktualnień tooimprove dostępności i niezawodności aplikacji.  
* **Diagnostyka:** na platformie Azure, udostępniamy integracji z diagnostyki Azure i analizy dzienników.
* **Automatyczne skalowanie:** klastrów na platformie Azure, firma Microsoft udostępnia wbudowaną funkcję skalowania automatycznego powodu zestawy skalowania tooVirtual maszyny. W lokalnych i dostępnych w innych środowiskach chmury masz toobuild własne automatyczne skalowanie się funkcji lub ręcznie przy użyciu interfejsów API, które udostępnia usługi sieć szkieletowa hello skalowania klastrów skali.

## <a name="next-steps"></a>Następne kroki

* Tworzenie klastra na maszynach wirtualnych lub komputerach z systemem Windows Server: [tworzenia klastra usługi sieć szkieletowa usług dla systemu Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Tworzenie klastra na maszynach wirtualnych lub komputerach z systemem Linux: [sieci szkieletowej usług w systemie Linux](service-fabric-linux-overview.md)
* Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)

