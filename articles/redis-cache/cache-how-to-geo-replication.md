---
title: "aaaHow tooconfigure — replikacja geograficzna dla pamięci podręcznej Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooreplicate pamięć podręczna Redis Azure wystąpień w regionach geograficznych."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>Jak tooconfigure — replikacja geograficzna dla pamięci podręcznej Redis Azure

Replikacja geograficzna udostępnia mechanizm do konsolidacji dwa wystąpienia pamięci podręcznej Redis Azure warstwy Premium. Jedna pamięć podręczna jest wyznaczony jako hello głównej połączonego pamięci podręcznej i hello innych jako hello dodatkowej połączonego pamięci podręcznej. Hello pamięci podręcznej połączonego dodatkowej staje się tylko do odczytu i jest zapisany toohello głównej pamięci podręcznej danych replikowane toohello dodatkowej połączonego pamięci podręcznej. Ta funkcja może być używana tooreplicate pamięci podręcznej w regionach platformy Azure. Ten artykuł zawiera przewodnik tooconfiguring — replikacja geograficzna dla swoich wystąpień pamięci podręcznej Redis Azure warstwy Premium.

## <a name="geo-replication-prerequisites"></a>Replikacja geograficzna wymagania wstępne

muszą być spełnione tooconfigure — replikacja geograficzna między dwoma pamięci podręcznych hello następujące wymagania wstępne:

- Zarówno pamięci podręcznej musi być [warstwy Premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.
- Zarówno pamięci podręcznej musi być w hello tej samej subskrypcji platformy Azure.
- Hello dodatkowej połączonego pamięci podręcznej musi być albo hello samej cen warstwy lub większy warstwy cenowej niż hello głównej połączonego pamięci podręcznej.
- Jeśli klaster włączone hello głównej połączonego pamięci podręcznej, hello pamięci podręcznej połączonego dodatkowej musi mieć klaster włączyć hello takiej samej liczby odłamków jak hello głównej połączonego pamięci podręcznej.
- Zarówno pamięci podręcznych muszą zostać utworzone i uruchomione.
- Trwałości nie mogą być włączone na obu pamięci podręcznej.
- Replikacja geograficzna między pamięci podręcznych w hello jest obsługiwana w tej samej sieci Wirtualnej. Replikacja geograficzna między pamięci podręcznych w różnych sieci wirtualnych jest również obsługiwane, tak długo, jak Witaj dwie sieci wirtualne są skonfigurowane w taki sposób, że zasobów w sieci wirtualnych hello stanie tooreach wzajemnie za pośrednictwem połączeń TCP.

Po skonfigurowaniu replikacji geograficznej hello, obowiązują następujące ograniczenia tooyour pary połączonego pamięci podręcznej:

- Hello dodatkowej połączonego pamięci podręcznej jest tylko do odczytu. można odczytać z niego, ale nie można zapisać tooit żadnych danych. 
- Wszystkie dane sprzed w pamięci podręcznej połączonego dodatkowej hello hello łącze zostało dodane zostaną usunięte. Hello — replikacja geograficzna następnie usunięciu jednak hello zreplikowane dane pozostaną w pamięci podręcznej połączonego dodatkowej hello.
- Nie można zainicjować [operacji skalowania](cache-how-to-scale.md) na obu pamięci podręcznej lub [zmiany liczby hello odłamków](cache-how-to-premium-clustering.md) Jeśli hello pamięci podręcznej ma włączoną funkcją klastrowania.
- Nie można włączyć trwałości na obu pamięci podręcznej.
- Można użyć [wyeksportować](cache-how-to-import-export-data.md#export) z albo pamięcią podręczną, ale możesz tylko [importu](cache-how-to-import-export-data.md#import) do głównej hello połączone pamięci podręcznej.
- Nie można usunąć połączonej pamięci podręcznej lub hello grupę zasobów zawierającą je, przed usunięciem hello łącze replikacji geograficznej. Aby uzyskać więcej informacji, zobacz [Dlaczego operacji hello nie po toodelete Moje połączonego pamięci podręcznej?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Witaj dwie pamięci podręcznych znajdują się w różnych regionach, kosztów wyjście sieci zostanie zastosowana toohello dane replikowane w regionach toohello dodatkowej połączonego pamięci podręcznej. Aby uzyskać więcej informacji, zobacz [ile ma koszt tooreplicate dane w regionach platformy Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- Jest nie automatycznej pracy awaryjnej toohello dodatkowej połączonego pamięci podręcznej, jeśli hello głównej pamięci podręcznej (i jego repliką) przestaną działać. W aplikacjach klienckich toofailover kolejności będzie potrzebny toomanually Usuń hello — replikacja geograficzna łącze i punkt powitania klienta aplikacji toohello pamięci podręcznej, który był wcześniej hello dodatkowej połączonego pamięci podręcznej. Aby uzyskać więcej informacji, zobacz [awarii pamięci podręcznej połączonego dodatkowej toohello działanie?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Dodaj łącze — replikacja geograficzna

1. toolink dwóch premium buforuje ze sobą za replikację geograficzną, kliknij przycisk **— replikacja geograficzna** z menu zasobów hello pamięci podręcznej hello pełnić rolę hello głównej połączone pamięci podręcznej, a następnie kliknij **łącza replikacji pamięci podręcznej Dodaj**z hello **— replikacja geograficzna** bloku.

    ![Dodaj łącze](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Kliknij nazwę hello hello potrzeby dodatkowej pamięci podręcznej z hello **zgodne pamięci podręcznych** listy. Jeśli żądany pamięci podręcznej nie jest wyświetlane na liście hello, upewnij się, że hello [wymagania wstępne — replikacja geograficzna](#geo-replication-prerequisites) dla żądanego hello dodatkowej pamięci podręcznej są spełnione. pamięci podręczne hello toofilter według regionu, kliknij odpowiedni region hello w toodisplay mapy hello tylko te buforuje w hello **zgodne pamięci podręcznych** listy.

    ![Replikacja geograficzna zgodne pamięci podręczne](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    Można także zainicjować hello łączenie za pomocą menu kontekstowe hello procesu lub Wyświetl szczegóły hello dodatkowej pamięci podręcznej.

    ![Menu kontekstowe — replikacja geograficzna](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Kliknij przycisk **łącze** toolink Witaj dwie pamięci podręcznych ze sobą i rozpocząć proces replikacji hello.

    ![Pamięci podręczne łącza](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. Można wyświetlić postęp procesu replikacji hello hello na powitania **— replikacja geograficzna** bloku.

    ![Łączenie stanu](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    Można również wyświetlić hello łączenie stanu na powitania **omówienie** bloku dla obu hello głównej i dodatkowej pamięci podręcznych.

    ![Stan pamięci podręcznej](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Po zakończeniu procesu replikacji hello hello **Link stanu** zmiany zbyt**zakończyło się pomyślnie**.

    ![Stan pamięci podręcznej](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Podczas procesu łączenia hello hello głównej połączonego pamięci podręcznej pozostaje dostępna do użycia, ale hello dodatkowej połączonego pamięci podręcznej jest niedostępny do momentu ukończenia hello łączenie procesu.

## <a name="remove-a-geo-replication-link"></a>Usuń łącze — replikacja geograficzna

1. Kliknij łącze hello tooremove między dwa pamięci podręcznych i Zatrzymaj replikację geograficzną, **odłączyć pamięci podręcznych** z hello **— replikacja geograficzna** bloku.
    
    ![Rozłącz pamięci podręczne](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Po zakończeniu procesu rozłączanie hello hello dodatkowej pamięci podręcznej jest dostępny dla obu odczytuje i zapisuje.

>[!NOTE]
>Usunięcie łącza hello — replikacja geograficzna hello zreplikowanych danych z hello głównej połączonego pamięci podręcznej pozostaje w pamięci podręcznej dodatkowej hello.
>
>

## <a name="geo-replication-faq"></a>Replikacja geograficzna — często zadawane pytania

- [Replikacja geograficzna można używać z pamięci podręcznej warstwy standardowa lub Basic?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [Moje pamięci podręcznej jest dostępny do użycia podczas łączenia hello lub odłączanie procesu?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [Czy można połączyć więcej niż dwa pamięci podręcznych razem?](#can-i-link-more-than-two-caches-together)
- [Czy można połączyć dwóch pamięci podręczne z różnych subskrypcji platformy Azure?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [Czy można połączyć dwóch buforów o różnych rozmiarach?](#can-i-link-two-caches-with-different-sizes)
- [Replikacja geograficzna można używać z włączoną funkcją klastrowania?](#can-i-use-geo-replication-with-clustering-enabled)
- [Replikacja geograficzna można używać z mojej pamięci podręcznych w sieci Wirtualnej?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [Można użyć programu PowerShell lub interfejsu wiersza polecenia Azure toomanage — replikacja geograficzna?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [Ile kosztuje tooreplicate dane w regionach platformy Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [Dlaczego operacji hello nie po toodelete Moje połączonego pamięci podręcznej?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [Jakie region Użyj mojej dodatkowej pamięci podręcznej połączonego](#what-region-should-i-use-for-my-secondary-linked-cache)
- [Jak działa awarii toohello dodatkowej połączonego pamięci podręcznej?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>Replikacja geograficzna można używać z pamięci podręcznej warstwy standardowa lub Basic?

Nie, replikacja geograficzna dostępnej tylko dla pamięci podręcznej warstwy Premium.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>Moje pamięci podręcznej jest dostępny do użycia podczas łączenia hello lub odłączanie procesu?

- Łączący dwa pamięci podręcznych za replikację geograficzną, hello głównej połączonego pamięci podręcznej pozostaje dostępna do użycia, ale hello dodatkowej połączonego bufor nie jest dostępny, aż do zakończenia hello łączenie procesu.
- Podczas usuwania hello — replikacja geograficzna łącza między dwoma pamięci podręcznych, zarówno pamięci podręcznych pozostają dostępne do użycia.

### <a name="can-i-link-more-than-two-caches-together"></a>Czy można połączyć więcej niż dwa pamięci podręcznych razem?

Nie, używając — replikacja geograficzna można połączyć tylko dwa pamięci podręcznych razem.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>Czy można połączyć dwóch pamięci podręczne z różnych subskrypcji platformy Azure?

Pamięci podręcznych, nie musi być w hello tej samej subskrypcji platformy Azure.

### <a name="can-i-link-two-caches-with-different-sizes"></a>Czy można połączyć dwóch buforów o różnych rozmiarach?

Tak, tak długo, jak połączonych hello dodatkowej pamięci podręcznej jest większy niż hello głównej połączonego pamięci podręcznej.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>Replikacja geograficzna można używać z włączoną funkcją klastrowania?

Tak, ile zarówno pamięci podręcznych mają hello tę samą liczbę fragmentów.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>Replikacja geograficzna można używać z mojej pamięci podręcznych w sieci Wirtualnej?

Tak, replikacja geograficzna pamięci podręcznych w sieci wirtualnych są obsługiwane. 

- Replikacja geograficzna między pamięci podręcznych w hello jest obsługiwana w tej samej sieci Wirtualnej.
- Replikacja geograficzna między pamięci podręcznych w różnych sieci wirtualnych jest również obsługiwane, tak długo, jak Witaj dwie sieci wirtualne są skonfigurowane w taki sposób, że zasobów w sieci wirtualnych hello stanie tooreach wzajemnie za pośrednictwem połączeń TCP.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>Można użyć programu PowerShell lub interfejsu wiersza polecenia Azure toomanage — replikacja geograficzna?

W tym momencie, którymi można zarządzać tylko przy użyciu — replikacja geograficzna hello portalu Azure.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>Ile kosztuje tooreplicate dane w regionach platformy Azure?

Używając — replikacja geograficzna, dane z pamięci podręcznej połączonego głównej hello jest replikowanych toohello dodatkowej połączone w pamięci podręcznej. Jeśli hello dwa połączone pamięci podręcznych znajdują się w hello tego samego regionu Azure, bez żadnych opłat hello transferu danych nie istnieje. Jeśli hello dwa połączone pamięci podręcznych znajdują się w różnych regionach platformy Azure, hello opłat transfer danych — replikacja geograficzna hello kosztów przepustowości replikacji tego toohello danych innego regionu systemu Azure. Aby uzyskać więcej informacji, zobacz [szczegóły cennika przepustowości](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>Dlaczego operacji hello nie po toodelete Moje połączonego pamięci podręcznej?

Gdy dwa pamięci podręcznych są połączone ze sobą, nie można usunąć pamięci podręcznej lub hello grupę zasobów zawierającą je przed usunięciem hello łącze replikacji geograficznej. Przy próbie toodelete hello zasobów grupy, która zawiera jedną lub obie hello połączona pamięci podręcznych, hello inne zasoby w grupie zasobów hello są usuwane, ale pozostaje hello grupy zasobów w hello `deleting` stanu i wszystkie połączone pamięci podręcznych w grupie zasobów hello pozostają w hello `running` stanu. toocomplete hello usunięcie grupy zasobów hello i hello połączone pamięci podręcznych w niej łącza hello — replikacja geograficzna podziału, zgodnie z opisem w [Usuń łącze replikacji geograficznej](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>Jakie region Użyj mojej dodatkowej pamięci podręcznej połączonego

Ogólnie rzecz biorąc, zaleca się dla Twojego tooexist pamięci podręcznej w hello sam region platformy Azure jako aplikacja hello, który uzyskuje dostęp do jej. Jeśli aplikacja ma regionu podstawowego i rezerwowej, pamięci podręcznych podstawowych i pomocniczych powinna istnieć w tym samym regionach. Aby uzyskać więcej informacji na temat sparowanego regionów, zobacz [najlepszych rozwiązań — regiony platformy Azure sparowanym](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>Jak działa awarii toohello dodatkowej połączonego pamięci podręcznej?

W hello początkowa wersja — replikacja geograficzna pamięć podręczna Redis Azure nie obsługuje automatycznej pracy awaryjnej w regionach platformy Azure. Replikacja geograficzna jest używany głównie w przypadku odzyskiwania po awarii. W przypadku odzyskiwania distater klientów należy wyświetlić hello całego stosu aplikacji w regionie kopii zapasowej w skoordynowany sposób zamiast umożliwienie poszczególnych składników aplikacji podjęcie decyzji dotyczącej tooswitch tootheir wykonywanie kopii zapasowych na ich własnych. Jest to szczególnie istotne tooRedis. Jedną z kluczowych zalet Redis hello jest magazynem bardzo małe opóźnienia. Jeśli Redis używany przez aplikacji nie powiedzie się w innym regionie Azure tooa, ale warstwie obliczeniowej hello nie, hello dodane wokół czas podróży mają zauważalnego wpływu na wydajność. Z tego powodu chcielibyśmy tooavoid niepowodzenie Redis za pośrednictwem automatycznie powodu tootransient problemów dotyczących dostępności.

Obecnie tooinitiate hello przejścia w tryb failover należy hello tooremove — replikacja geograficzna łącze w hello portalu Azure, a następnie zmień punktu końcowego połączenia powitania klienta pamięci podręcznej Redis hello hello głównej pamięci podręcznej połączonego toohello (dawniej połączone) pomocniczej pamięci podręcznej. Gdy powitalne dwóch pamięci podręcznych są usunąć skojarzenia, repliki hello staje się zwykły zapisu i odczytu pamięci podręcznej ponownie i akceptuje żądania bezpośrednio od klientów pamięci podręcznej Redis.


## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o hello [warstwy pamięci podręcznej Redis Azure Premium](cache-premium-tier-intro.md).

