---
title: "aaaPlanning migracji zasobów IaaS z klasycznym tooAzure Resource Manager | Dokumentacja firmy Microsoft"
description: "Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 7574122d951119db4991187945739b190ef14995
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager
Podczas usługi Azure Resource Manager oferuje wiele funkcji niesamowite, jest krytyczne tooplan limit toomake przebieg migracji, z którą rzeczy sure bezproblemowe. Poświęcany czas na planowanie sprawdzi, czy nie występują problemy podczas wykonywania działań migracji.

> [!NOTE]
> Hello następujące wskazówki został zespół Advisory klienta usługi Azure hello silnie załadowanie współtworzonej tooby i Praca z klientami w dużych środowiskach Migrowanie architektów rozwiązanie chmury. W związku tego dokumentu będą nadal tooget aktualizowany nowe wzorce sukcesu wyłonić, więc zajrzyj od czasu tootime toosee przypadku żadnych rekomendacji do przedstawienia nowych.

Istnieją cztery fazy ogólny przebieg migracji hello:<br>

![Etapy migracji](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Planowanie

### <a name="technical-considerations-and-tradeoffs"></a>Zagadnienia techniczne i wady i zalety

W zależności od Twojego rozmiar wymagania techniczne, lokalizacji geograficznych i rozwiązań operacyjnych może być tooconsider:

1. Dlaczego wymagane jest Menedżera zasobów Azure dla organizacji?  Co to są hello powodów biznesowych do migracji?
2. Co to są przyczyn technicznych hello Azure Resource Manager?  Jakie (jeżeli istniał) dodatkowymi usługami platformy Azure ma tooleverage?
3. Która aplikacja (lub zestawy maszyn wirtualnych) znajduje się w hello migracji?
4. Jakie scenariusze są obsługiwane przy migracji hello interfejsu API?  Przejrzyj hello [nieobsługiwane funkcje i konfiguracje](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations).
5. Zespołów operacyjnych obsługuje obecnie aplikacji/maszyn wirtualnych w klasycznym i usługi Azure Resource Manager?
6. Jak (Jeśli w ogóle) usługi Azure Resource Manager zmienia wdrożenia maszyn wirtualnych, zarządzania, monitorowania i raportowania procesów?  Skrypty wdrażania zbędna toobe aktualizacji?
7. Co to jest komunikacja hello Planowanie uczestników tooalert (użytkownicy końcowi, właścicieli aplikacji i właścicieli infrastruktury)?
8. W zależności od złożoności hello hello środowiska powinno być okres konserwacji, gdzie aplikacji hello jest niedostępna tooend użytkowników i właścicieli tooapplication?  Jeśli tak, jak długo?
9. Co to jest uczestników tooensure plan szkolenia hello są wiedzę i wykorzystać w usłudze Azure Resource Manager?
10. Co to jest zarządzanie programem hello lub plan zarządzania hello migracji projektu?
11. Co to są termin hello hello migracji usługi Azure Resource Manager i inne powiązane mapy drogowej technologii?  Są one optymalnie wyrównana?

### <a name="patterns-of-success"></a>Wzorce Powodzenie

Klienci pomyślnie szczegółowych planów gdzie hello poprzedniego pytania są omówione, udokumentowanych i postanowieniom.  Sprawdź, czy plany migracji hello szeroko przekazanych toosponsors i uczestników.  Wyposażyć sobie z wiedzą na temat opcji migracji; Zdecydowanie zalecane jest odczytu za pomocą tego dokumentu migracji poniżej.

* [Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj programu PowerShell toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj interfejsu wiersza polecenia toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Narzędzia z migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów społeczności](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Przegląd najbardziej typowych błędów migracji](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Tooavoid problemów

- Błąd tooplan.  kroki technologii Hello tej migracji zostały sprawdzone i wynik hello jest atrybutem wartości prognozowanych.
- Zakładając, że hello API migracji platformy obsługiwanej będzie konta we wszystkich scenariuszach. Witaj odczytu [nieobsługiwane funkcje i konfiguracje](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations) toounderstand jakie scenariusze są obsługiwane.
- Nie ma potencjalnych awarii aplikacji dla użytkowników końcowych.  Planowanie wystarczająco dużego buforu tooadequately Ostrzegaj użytkownicy końcowi czasu aplikacji potencjalnie niedostępny.


## <a name="lab-test"></a>Laboratorium testowego

**Replikowanie środowiska i przeprowadzić migrację testu**
  > [!NOTE]
  > Dokładne replikacji istniejącego środowiska jest wykonywana przy użyciu narzędzia przyczyniły się społeczności, który nie jest oficjalnie obsługiwana przez Microsoft Support. W związku z tym jest **opcjonalne** krok, ale jest hello najlepsze sposób toofind problemów bez używania środowiska produkcyjnego. Jeśli przy użyciu narzędzia przyczyniły się społeczności nie jest opcją, przeczytaj o hello zalecenie przebiegu weryfikacji/Prepare/przerwania poniżej.
  >

  Przeprowadzenie testu laboratorium dokładne scenariusz (obliczeniowych, sieci i magazynu) jest hello najlepsze sposób tooensure płynną migrację. Zapewni:

  - Całkowicie oddzielne laboratorium lub istniejące tootest poza środowiskiem produkcyjnym. Zaleca się całkowicie oddzielne laboratorium, które można poddać migracji wielokrotnie i może zostać zmodyfikowany utraty danych.  Skrypty toocollect/wodzianem metadanych hello rzeczywistych subskrypcje są wymienione poniżej.
  - Należy dobrze toocreate hello laboratorium w oddzielnej subskrypcji. Przyczyna Hello jest hello laboratorium będzie się działo wielokrotnie, czy posiadanie oddzielnego, izolowanego subskrypcji zostanie zmniejsza ryzyko hello czy coś rzeczywistym zostaną przypadkowo usunięte.

  Można to zrobić za pomocą narzędzia AsmMetadataParser hello. [Dowiedz się więcej o tym narzędziu, w tym miejscu](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Wzorce Powodzenie

następujące Hello były problemy wykryte w wielu hello większych migracji. To nie jest kompletną listą i należy zapoznać się toohello [nieobsługiwane funkcje i konfiguracje](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#unsupported-features-and-configurations) uzyskać więcej szczegółowych informacji.  Może lub nie mogą wystąpić następujące problemy techniczne, ale po wykonaniu rozwiązywania tych przed podjęciem próby wykonania migracji zapewnia płynne.

- **Czy przebiegu weryfikacji/Prepare/przerwania** — jest to prawdopodobnie hello Najważniejszy krok tooensure Classic tooAzure Menedżera zasobów migracji Powodzenie. Migracja Hello interfejsu API zawiera trzy główne kroki: Sprawdzanie poprawności, przygotowanie i zatwierdzić. Sprawdzanie poprawności zostanie odczytać stanu hello klasycznego środowiska i zwracanie wyniku wszystkie problemy. Jednak ponieważ niektóre problemy, może istnieć w stosie usługi Azure Resource Manager hello, sprawdzanie poprawności nie będzie przechwytywać wszystko. Hello następnego kroku w procesie migracji, przygotowanie pomoże udostępnianie tych problemów. Przygotowanie będzie przenieść hello metadanych z klasycznym tooAzure Resource Manager, ale zostanie nie zatwierdzania hello przenoszenia i zostanie nie Usuń lub zmień niczego hello Classic po stronie. przebiegu Hello obejmuje przygotowanie hello migracji, a następnie przerywanie (**nie zatwierdzania**) przygotować hello migracji. Celem Hello przebiegu zweryfikować/przygotowanie/przerwania jest toosee wszystkich metadanych hello w stosie usługi Azure Resource Manager hello, ją zbadać (*programowo lub w portalu*), sprawdź, czy wszystko migruje poprawnie i działa za pośrednictwem problemy techniczne.  On również zapewni w pewnym sensie czasem trwania migracji, można odpowiednio zaplanować przestoje.  Sprawdź poprawność/przygotowanie/przerwania nie powoduje żadnych przestojów użytkownika; w związku z tym jest brak tooapplication użycia.
  - Poniższe elementy Hello należy toobe rozwiązanie przed hello przebiegu, ale przebiegu testu będzie również bezpiecznie opróżnić te kroki przygotowania, jeśli zostaną one pominięte. Podczas migracji enterprise znaleźliśmy toobe przebiegu hello przygotowanie do migracji tooensure bezpieczny i nieoceniony sposób.
  - Gdy przygotowanie działa Kontrola hello płaszczyzny (operacje zarządzania platformy Azure) zostanie zablokowana dla hello całej sieci wirtualnej, a więc nie można wprowadzać zmiany metadanych tooVM podczas sprawdzania poprawności/przygotowanie/przerwania.  Ale w przeciwnym razie dowolnej funkcji aplikacji (usług pulpitu zdalnego, maszyna wirtualna użycia, itp.) będzie to miało wpływu.  Użytkownicy hello maszyn wirtualnych nie będą wiedzieli, że tego przebiegu hello jest wykonywana.

- **Express Route obwody i sieci VPN**. Obecnie Express bram trasy z łączami autoryzacji nie można migrować bez przestoju. Aby hello obejście tego problemu, zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne od modelu wdrażania Menedżera zasobów klasycznych toohello hello](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **Rozszerzenia maszyny Wirtualnej** -rozszerzenia maszyny wirtualnej są potencjalnie jedną z największych toomigrating roadblocks hello, działających maszyn wirtualnych. Korygowanie rozszerzeń maszyny Wirtualnej może potrwać zgłaszane 1-2 dni, więc odpowiednio zaplanować.  Działającego agenta platformy Azure jest wymagane tooreport wstecz stan rozszerzenia maszyny Wirtualnej działających maszyn wirtualnych. Jeśli stan hello wróci jako uszkodzony dla uruchomionej maszyny Wirtualnej, spowoduje to zatrzymanie migracji. sam agent Hello nie musi toobe w stanie tooenable migracji, ale jeśli istnieją rozszerzenia na hello maszyny Wirtualnej, następnie zarówno pracy agent AND wychodzące połączenie z Internetem (z systemem DNS), które będą potrzebne dla toomove migracji do przodu.
  - Jeśli serwer DNS tooa łączności zostaną utracone podczas migracji, wszystkie rozszerzenia maszyny Wirtualnej, z wyjątkiem BGInfo wersji 1. \* muszą toofirst usunięte z każdego maszyny Wirtualnej, aby przygotować migrację, a następnie ponownie dodać toohello wstecz maszyny Wirtualnej po migracji usługi Azure Resource Manager.  **Jest to tylko dla maszyn wirtualnych, które są uruchomione.**  Jeśli hello maszyny wirtualne zostały zatrzymane deallocated, rozszerzeń maszyny Wirtualnej nie ma potrzeby toobe usunięte.

  > [!NOTE]
  > Wiele rozszerzeń, takich jak diagnostyki Azure i zabezpieczeń Centrum monitorowania zostanie ponownie się po migracji, więc usunięcie ich nie jest problemem.

  - Ponadto upewnij się, grup zabezpieczeń sieci są ograniczając ruch wychodzący do Internetu. Może to nastąpić w niektórych konfiguracjach grup zabezpieczeń sieci. Ruch wychodzący do Internetu (i DNS) jest wymagany dla rozszerzeń maszyny Wirtualnej toobe migracji tooAzure Menedżera zasobów.
  - Dwie wersje hello rozszerzenie BGInfo istnieją i są nazywane w wersji 1 i 2.  

      - Jeśli hello maszyna wirtualna używa hello rozszerzenie BGInfo wersji 1, można pozostawić to rozszerzenie, ponieważ jest. Migracja Hello interfejsu API pomija tego rozszerzenia. Witaj rozszerzenie BGInfo mogą być dodawane po migracji.
      - Jeśli hello maszyna wirtualna używa hello rozszerzenie wersji 2 BGInfo opartych na formacie JSON, hello maszyny Wirtualnej został utworzony przy użyciu hello portalu Azure. Migracja Hello interfejsu API obejmuje to rozszerzenie w hello migracji tooAzure Resource Manager, pod warunkiem agenta hello działa i wychodzący dostęp do Internetu (i DNS).

  - **Opcja korygowania 1**. Jeśli wiesz, że maszyny wirtualne nie będą miały wychodzącego dostępem do Internetu, działającą usługę DNS i Praca agentów programu Azure na maszynach wirtualnych hello, następnie odinstaluj wszystkie rozszerzenia maszyny Wirtualnej w ramach migracji hello przed Prepare, zainstaluj ponownie hello rozszerzeń maszyny Wirtualnej, po migracji.
  - **Opcja korygowania 2**. Jeśli rozszerzeń maszyny Wirtualnej są zbyt duże z próg wykluczający, inną opcją jest tooshutdown/cofnąć wszystkich maszyn wirtualnych przed migracją. Migrowanie hello cofnięciu przydziału maszyn wirtualnych, a następnie uruchomić je ponownie na powitania po stronie usługi Azure Resource Manager. w tym miejscu Hello korzyścią jest to, że rozszerzenia maszyny Wirtualnej zostanie poddana migracji. Witaj wadą interfejsu jest publicznymi wszystkich wirtualnych adresów IP zostaną utracone (może to być z systemem innym niż starter,) i oczywiście hello maszyn wirtualnych zamknie uniemożliwiający znacznie większy wpływ na pracę aplikacji.

    > [!NOTE]
    > Skonfigurowanie zasad Centrum zabezpieczeń Azure przed hello działających maszyn wirtualnych migrowanych hello zasady zabezpieczeń muszą toobe zatrzymane przed usunięciem rozszerzeń, w przeciwnym razie zabezpieczeń hello rozszerzonego monitorowania zostaną zainstalowane ponownie automatycznie na hello maszyny Wirtualnej po usunięcie go.

- **Zestawy dostępności** — toobe sieć wirtualną (vNet) migracji tooAzure Resource Manager, hello Classic deployment (tj. Usługa w chmurze) w maszynach wirtualnych musi być w jednym zestawie dostępności lub hello maszyn wirtualnych wszystkie nie może być w jakimkolwiek zestawie dostępności. Mając więcej niż jeden zestaw hello w usłudze w chmurze dostępności nie jest zgodny z usługi Azure Resource Manager i zostanie zatrzymany migracji.  Ponadto nie może być niektórych maszyn wirtualnych w zestawie dostępności i niektórych maszyn wirtualnych w zestawie dostępności. tooresolve, będzie konieczne tooremediate lub zamieniać usługi w chmurze.  Planowanie odpowiednio to może zająć dużo czasu.

- **Wdrożenia roli sieć Web/proces roboczy** -usługi w chmurze zawierającego role sieci web i proces roboczy nie może przeprowadzić migracji tooAzure Menedżera zasobów. role sieć web/proces roboczy Hello najpierw należy usunąć z sieci wirtualnej hello, przed rozpoczęciem migracji.  Typowe rozwiązania jest toojust przenoszenia sieci web/proces roboczy roli wystąpień tooa oddzielne klasycznej sieci wirtualnej będącego również obwodu ExpressRoute połączonego tooan lub toomigrate hello kodu toonewer usługi aplikacji PaaS (rozważania wykracza poza zakres tego dokumentu hello). W poprzednim hello ponownie wdrożyć case, Utwórz nową sieć wirtualną w klasycznym, Przenieś/ponownego wdrażania hello sieci web/proces roboczy ról toothat nowej sieci wirtualnej, a następnie usuń hello wdrożeń z siecią wirtualną hello przenoszony. Nie zmian w kodzie wymaganych. nowe Hello [równorzędna sieci wirtualnych](../../virtual-network/virtual-network-peering-overview.md) możliwości mogą być używane toopeer razem hello klasycznego sieci wirtualnej zawierającego role sieć web/proces roboczy hello i innych sieci wirtualnych w hello tego samego regionu Azure, takich jak hello sieci wirtualnej jest migracji (**po ukończeniu migracji sieci wirtualnej, jak połączyć za pomocą sieci wirtualne nie mogą być migrowane**), dlatego dostarczanie hello takie same możliwości bez utraty wydajności i nie kary opóźnienia/przepustowość. Podane dodanie hello [równorzędna sieci wirtualnych](../../virtual-network/virtual-network-peering-overview.md), wdrożenia roli sieć web/proces roboczy teraz łatwo można zminimalizować i blokuje hello tooAzure migracji Menedżera zasobów.

- **Limity przydziału Menedżera zasobów Azure** -regiony platformy Azure mają oddzielne przydziały/limity dla usługi Azure Resource Manager i klasycznym. Mimo że w scenariuszu migracji nowy sprzęt nie jest używane *(Firma Microsoft jest zamiana istniejących maszyn wirtualnych z klasycznym tooAzure Resource Manager)*, limity przydziału Menedżera zasobów Azure nadal potrzebujesz toobe w miejscu z wystarczającą wydajność przed można rozpocząć migrację. Poniżej wymieniono limity głównych hello, który NAS spowodować problemy.  Otwórz limity przydziału obsługi biletów tooraise hello.

    > [!NOTE]
    > Te limity muszą toobe zgłoszonych w hello tego samego regionu, zgodnie z bieżącego środowiska toobe migracji.
    >

    - Interfejsy sieciowe
    - Moduły równoważenia obciążenia
    - Publiczne adresy IP
    - Statyczne publiczne adresy IP
    - Rdzenie
    - Grupy zabezpieczeń sieci
    - Tabele tras

    Można sprawdzić za pomocą następującego polecenia hello najnowszej wersji programu Azure PowerShell hello Twojej bieżącej limity przydziału Menedżera zasobów Azure.

    **Obliczenia bazy danych** *(rdzenie, zestawów dostępności)*

    ```powershell
    Get-AzureRmVMUsage -Location <azure-region>
    ```

    **Sieci** *(sieci wirtualne, statyczne publiczne adresy IP, publiczne adresy IP, grupy zabezpieczeń sieciowych, sieci interfejsów, równoważenia obciążenia, tabele tras)*

    ```powershell
    Get-AzureRmUsage /subscriptions/<subscription-id>/providers/Microsoft.Network/locations/<azure-region> -ApiVersion 2016-03-30 | Format-Table
    ```

    **Magazyn** *(konta magazynu)*

    ```powershell
    Get-AzureRmStorageUsage
    ```

- **Usługa Azure Resource Manager interfejsu API ograniczenie** — Jeśli masz środowisku wystarczająco duży (np. > 400 maszyn wirtualnych w sieci Wirtualnej), może być trafień API domyślne hello ograniczenie dla operacji zapisu (obecnie `1200 writes/hour`) w usłudze Azure Resource Manager. Przed rozpoczęciem migracji, należy podniesieniu tooincrease biletu pomocy technicznej tego limitu dla Twojej subskrypcji.


- **Upłynął limit stanu maszyny Wirtualnej udostępniania** — Jeśli żadnej maszyny Wirtualnej ma stan hello `provisioning timed out`, to toobe musi rozpoznać sprzed migracji. toodo jedynym sposobem Hello jest przestojów przez anulowania obsługi/reprovisioning hello maszyny Wirtualnej (usuwanie, Zachowaj hello dysku i ponownie utwórz hello maszyny Wirtualnej).

- **Stan maszyny Wirtualnej RoleStateUnknown** — Jeżeli migracja zostanie zatrzymany ze względu tooa `role state unknown` błąd wiadomości, sprawdź hello maszyny Wirtualnej przy użyciu portalu hello i upewnij się, jest uruchomiona. Ten błąd zazwyczaj zniknie jego właścicielem (Brak korygowania wymagane), po upływie kilku minut i jest często przejściowego typu często występujące podczas maszyny wirtualnej `start`, `stop`, `restart` operacji. **Zalecana praktyka:** ponów próbę migracji ponownie za kilka minut.

- **Klaster sieci szkieletowej nie istnieje** — w niektórych przypadkach niektórych nie można migrować maszyny wirtualne z różnych powodów nieparzysta. Jest jednym z tych znanych przypadków Jeśli hello maszyna wirtualna została niedawno utworzona (w ramach hello ostatniego tygodnia lub tak) i wystąpiły tooland klastrze platformy Azure, która nie jest jeszcze wyposażony w przypadku obciążeń usługi Azure Resource Manager.  Otrzymasz komunikat o błędzie informujący `fabric cluster does not exist` i hello maszyny Wirtualnej nie można migrować. Oczekiwanie na kilka dni rozwiąże zwykle tego konkretnego problemu jako klastra hello wkrótce zostanie wyświetlony usługi Azure Resource Manager włączone. Jednak jeden natychmiastowego rozwiązania jest zbyt`stop-deallocate` hello maszyny Wirtualnej, następnie do przodu kontynuować migracji i uruchom hello maszyny Wirtualnej Utwórz kopię zapasową w usłudze Azure Resource Manager po zakończeniu migracji.

### <a name="pitfalls-tooavoid"></a>Tooavoid problemów

- Nie używaj skrótów i Pomiń hello przebiegu zweryfikować/przygotowanie/przerwania migracji.
- Większość, jeśli nie, Twoje potencjalnych problemów będzie powierzchni etapach hello zweryfikować/przygotowanie/przerwania.

## <a name="migration"></a>Migracja

### <a name="technical-considerations-and-tradeoffs"></a>Zagadnienia techniczne i wady i zalety

Teraz można przystąpić ponieważ pracowano za pośrednictwem hello znane problemy związane ze środowiskiem.

Hello rzeczywistej migracji można tooconsider:

1. Planowanie i Zaplanuj sieci wirtualnej hello (najmniejszego migracji) z zwiększanie priorytetu.  Witaj najpierw proste sieci wirtualnych i postępu za pomocą hello więcej skomplikowane sieci wirtualnych.
2. Większość klientów będą mieć środowiskach nieprodukcyjnych i produkcji.  Ostatnio planowania produkcji.
3. **(OPCJONALNIE)**  Zaplanować przestój konserwacji, z dużą ilością buforu w przypadku spowodować nieoczekiwane problemy.
4. Komunikować się z i Wyrównaj ją z sieci zespoły pomocy technicznej, w przypadku problemach.

### <a name="patterns-of-success"></a>Wzorce Powodzenie

Witaj wskazówki techniczne z hello _laboratorium testowego_ sekcji należy traktować i skorygowane wcześniejsze tooa rzeczywistych migracji.  Z odpowiednie testy migracji hello jest rzeczywiście niepowiązane ze zdarzeniami.  W przypadku środowisk produkcyjnych może być dodatkowe wsparcie toohave przydatne, np. zaufanych partnera firmy Microsoft lub usług Microsoft Premier.

### <a name="pitfalls-tooavoid"></a>Tooavoid problemów

Nie są w pełni testowania mogą powodować problemy i opóźnienie w hello migracji.  

## <a name="beyond-migration"></a>Po migracji

### <a name="technical-considerations-and-tradeoffs"></a>Zagadnienia techniczne i wady i zalety

Skoro masz usługi Azure Resource Manager zmaksymalizować hello platformy.  Witaj odczytu [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) toofind się o dodatkowe korzyści.

Tooconsider rzeczy:

- Tworzenie pakietów hello migracji z innymi działaniami.  Większość klientów zdecydować się na okno obsługi aplikacji.  Tak, które mogą być toouse tego tooenable przestój innych możliwości usługi Azure Resource Manager, takie jak szyfrowanie i migracji tooManaged dysków.
- Kontroluj hello technicznych i powodów biznesowych do usługi Azure Resource Manager; Włącz hello dodatkowe usługi dostępne tylko w usłudze Azure Resource Manager stosowane tooyour środowiska.
- Modernizacji środowiska z usługami PaaS.

### <a name="patterns-of-success"></a>Wzorce Powodzenie

Być nigdy wykonywane celowo na usług co tooenable chcesz teraz w usłudze Azure Resource Manager.  Wielu klientów Znajdź hello poniżej istotne dla nich środowiska Azure:

- [Kontrola dostępu oparta na rolach](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Szablony usługi Azure Resource Manager dla wdrożenia łatwiejsze i bardziej kontrolowane](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Tagi](../../azure-resource-manager/resource-group-using-tags.md).
- [Formant działania](../../azure-resource-manager/resource-group-audit.md)
- [Zasady zasobów](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Tooavoid problemów

Należy pamiętać o tym, dlaczego uruchomiony przebieg migracji tego Classic tooAzure Menedżera zasobów.  Jakie były oryginalnego powodów biznesowych hello? Czy uzyskania Przyczyna firm hello?


## <a name="next-steps"></a>Następne kroki

* [Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj programu PowerShell toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Użyj interfejsu wiersza polecenia toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Narzędzia z migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów społeczności](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Przegląd najbardziej typowych błędów migracji](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
