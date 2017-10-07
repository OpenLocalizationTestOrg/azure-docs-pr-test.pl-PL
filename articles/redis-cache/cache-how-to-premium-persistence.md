---
title: "Trwałość danych tooconfigure aaaHow dla podręczna Redis Azure Premium"
description: "Dowiedz się, jak tooconfigure i zarządzanie nimi trwałości danych swoich wystąpień pamięci podręcznej Redis Azure warstwy Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>Jak trwałości danych tooconfigure dla podręczna Redis Azure Premium
Pamięć podręczna Redis Azure ma ofert różnych pamięci podręcznej, które zapewniają elastyczność w wyborze hello rozmiar pamięci podręcznej i funkcji, łącznie z funkcji warstwy Premium, takich jak klastrowanie, trwałości i obsługi sieci wirtualnej. W tym artykule opisano, jak trwałości tooconfigure w warstwie premium Azure pamięci podręcznej Redis wystąpienia.

Aby uzyskać informacji o innych funkcjach pamięci podręcznej premium, zobacz [warstwy pamięci podręcznej Redis Azure Premium toohello wprowadzenie](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>Co to jest trwałości danych?
[Trwałość redis](https://redis.io/topics/persistence) pozwala toopersist danych przechowywanych w pamięci podręcznej Redis. Można również wykonać migawki i utworzyć kopię zapasową danych hello, które można załadować w przypadku awarii sprzętu. Jest to bardzo dużą zaletą za pośrednictwem Basic lub warstwy standardowa, gdzie hello wszystkie dane są przechowywane w pamięci i może być utracie danych w przypadku awarii skutkującej węzłów pamięci podręcznej w dół. 

Pamięć podręczna Redis Azure oferuje trwałość Redis przy użyciu hello następujące modele:

* **Trwałość RDB** -trwałości po RDB (bazy danych Redis) jest skonfigurowany, pamięć podręczna Redis Azure migawki pamięci podręcznej Redis hello w pamięci podręcznej Redis toodisk formatu binarnego w oparciu można skonfigurować częstotliwość wykonywania kopii zapasowych będzie się powtarzał. Jeśli krytycznego zdarzenie wystąpi wyłączenie hello podstawowy i repliki w pamięci podręcznej, pamięć podręczna hello jest odtworzone przy użyciu najnowszych migawki hello. Dowiedz się więcej o hello [zalety](https://redis.io/topics/persistence#rdb-advantages) i [wady](https://redis.io/topics/persistence#rdb-disadvantages) o trwałości RDB.
* **Trwałość AOF** -trwałości po AOF (Dołącz tylko plików) jest skonfigurowany, pamięć podręczna Redis Azure jest zapisywany co tooa dziennika operacji zapisu zapisany co najmniej raz na sekundę na konto magazynu Azure. Jeśli krytycznego zdarzenie wystąpi wyłączenie hello podstawowy i repliki w pamięci podręcznej, pamięć podręczna hello jest odtworzone przy użyciu operacji zapisu hello przechowywane. Dowiedz się więcej o hello [zalety](https://redis.io/topics/persistence#aof-advantages) i [wady](https://redis.io/topics/persistence#aof-disadvantages) z AOF trwałości.

Trwałości jest konfigurowana przy użyciu hello **nowa pamięć podręczna Redis** bloku podczas tworzenia pamięci podręcznej i na powitania **zasobów menu** istniejących Premium przechowuje w pamięci podręcznej.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Po wybraniu warstwie cenowej premium kliknij **trwałość Redis**.

![Trwałość redis][redis-cache-persistence]

Witaj w hello następnej sekcji opisano sposób tooconfigure trwałość Redis na nowa pamięć podręczna premium. Po skonfigurowaniu trwałość Redis, kliknij przycisk **Utwórz** toocreate Twojego nowego premium pamięci podręcznej z trwałość Redis.

## <a name="enable-redis-persistence"></a>Włącz trwałość Redis

Redis trwałości jest włączona na powitania **trwałość danych Redis** bloku, wybierając opcję **RDB** lub **AOF** trwałości. Dla nowych pamięci podręcznych ten blok jest dostępny w trakcie procesu tworzenia pamięci podręcznej hello zgodnie z opisem w poprzedniej sekcji hello. Dla istniejącej pamięci podręcznych, hello **trwałość danych Redis** bloku jest dostępny z hello **zasobów menu** dla pamięci podręcznej.

![Ustawienia redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>Konfigurowanie trwałości RDB

tooenable RDB trwałości, kliknij przycisk **RDB**. trwałość RDB toodisable na włączonym uprzednio premium pamięć podręczną, kliknij przycisk **wyłączone**.

![RDB trwałość redis][redis-cache-rdb-persistence]

tooconfigure hello interwał wykonywania kopii zapasowej, wybierz opcję **częstotliwość wykonywania kopii zapasowych** z listy rozwijanej hello. Można także wybrać opcję **15 minut**, **30 minut**, **60 minut**, **6 godzin**, **12 godzin**i **24 godziny**. Ten interwał odlicza w dół po pomyślnym zakończeniu hello poprzedniej operacji tworzenia kopii zapasowej i po jego upływie nową kopię zapasową jest inicjowana.

Kliknij przycisk **konta magazynu** tooselect hello toouse konta magazynu, a następnie wybierz pozycję albo hello **klucza podstawowego** lub **klucza pomocniczego** toouse z hello **magazynu Klucz** listy rozwijanej. Musisz wybrać konto magazynu w hello tego samego regionu hello pamięci podręcznej, a **magazyn w warstwie Premium** konta jest zalecane, ponieważ Magazyn w warstwie premium ma wyższej przepustowości. 

> [!IMPORTANT]
> Podczas ponownego generowania klucza magazynu hello konta trwałości, należy ponownie skonfigurować inny klawisz hello z hello **klucza magazynu** listy rozwijanej.
> 
> 

Kliknij przycisk **OK** toosave hello trwałości konfiguracji.

Witaj następnej kopii zapasowej (lub pierwszej kopii zapasowej dla nowych pamięci podręcznych) jest inicjowana po upływie interwału powitania częstotliwość wykonywania kopii zapasowych.

## <a name="configure-aof-persistence"></a>Konfigurowanie trwałości AOF

tooenable AOF trwałości, kliknij przycisk **AOF**. trwałość AOF toodisable na włączonym uprzednio premium pamięć podręczną, kliknij przycisk **wyłączone**.

![AOF trwałość redis][redis-cache-aof-persistence]

tooconfigure AOF trwałości, określ **pierwsze konto magazynu**. To konto magazynu musi być w hello tego samego regionu hello pamięci podręcznej, a **magazyn w warstwie Premium** konta jest zalecane, ponieważ Magazyn w warstwie premium ma wyższej przepustowości. Opcjonalnie można skonfigurować konto dodatkowego magazynu o nazwie **drugiego konta magazynu**. Jeśli skonfigurowano drugiego konta magazynu, hello zapisy toohello repliki w pamięci podręcznej są zapisywane toothis drugiego konta magazynu. Dla każdego konta skonfigurowanego magazynu, wybierz albo hello **klucza podstawowego** lub **klucza pomocniczego** toouse z hello **klucza magazynu** listy rozwijanej. 

> [!IMPORTANT]
> Podczas ponownego generowania klucza magazynu hello konta trwałości, należy ponownie skonfigurować inny klawisz hello z hello **klucza magazynu** listy rozwijanej.
> 
> 

Po włączeniu trwałości AOF zapisu operacji toohello w pamięci podręcznej są zapisywane toohello wyznaczony konta magazynu (lub konta, jeśli skonfigurowano drugiego konta magazynu). W przypadku poważnej awarii hello czy zajmuje dół zarówno hello podstawowy i repliki pamięci podręcznej, hello przechowywanych AOF dziennik jest używane toorebuild hello w pamięci podręcznej.

## <a name="persistence-faq"></a>Trwałość — często zadawane pytania
Witaj Poniższa lista zawiera toocommonly odpowiedzi zadawane pytania dotyczące pamięci podręcznej Redis Azure trwałości.

* [Można włączyć trwałości na utworzonej wcześniej pamięci podręcznej?](#can-i-enable-persistence-on-a-previously-created-cache)
* [Trwałość AOF i RDB na powitania można włączyć jednocześnie?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Model trwałości, który należy wybrać?](#which-persistence-model-should-i-choose)
* [Co się stanie, jeśli mają I skalować tooa inny rozmiar i przywróceniu kopii zapasowej utworzonej przed hello operacji skalowania?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>Trwałość RDB
* [Częstotliwość wykonywania kopii zapasowych RDB hello można zmienić po utworzeniu pamięci podręcznej hello?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Dlaczego Jeśli częstotliwość wykonywania kopii zapasowych RDB 60 minut istnieje ponad 60 minut między kopii zapasowych?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Co się stanie toohello starych kopii zapasowych RDB podczas tworzenia nowej kopii zapasowej?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>Trwałość AOF
* [Kiedy należy używać drugiego konta magazynu?](#when-should-i-use-a-second-storage-account)
* [Czy AOF trwałości mają wpływ na całym, opóźnienia lub wydajności Moje pamięci podręcznej?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Jak usunąć hello drugiego konta magazynu?](#how-can-i-remove-the-second-storage-account)
* [Co to jest ponownego zapisywania i jak wpływa na mój pamięci podręcznej?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [Co należy oczekiwać podczas skalowania pamięci podręcznej z AOF włączone?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [Sposób organizowania danych AOF w magazynie?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>Można włączyć trwałości na utworzonej wcześniej pamięci podręcznej?
Tak, trwałość Redis można skonfigurować zarówno na tworzenie pamięci podręcznej, jak i na istniejące premium pamięci podręcznych.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>Trwałość AOF i RDB na powitania można włączyć jednocześnie?

Nie można włączyć tylko RDB lub AOF, ale nie oba na powitania tym samym czasie.

### <a name="which-persistence-model-should-i-choose"></a>Model trwałości, który należy wybrać?

Trwałość AOF zapisuje co zapisu tooa dziennika, który ma pewien wpływ na przepustowość, w porównaniu z RDB trwałości, który zapisuje kopie zapasowe oparte na powitania skonfigurowany interwał wykonywania kopii zapasowej z minimalnym wpływem na wydajność. Wybierz AOF trwałości, jeśli z podstawowym celem jest toominimize utraty danych, a może obsłużyć spadek przepustowości dla pamięci podręcznej. Wybierz opcję trwałości RDB, jeśli chcesz toomaintain optymalnej przepływności w pamięci podręcznej, ale nadal chcesz mechanizm odzyskiwania danych.

* Dowiedz się więcej o hello [zalety](https://redis.io/topics/persistence#rdb-advantages) i [wady](https://redis.io/topics/persistence#rdb-disadvantages) o trwałości RDB.
* Dowiedz się więcej o hello [zalety](https://redis.io/topics/persistence#aof-advantages) i [wady](https://redis.io/topics/persistence#aof-disadvantages) z AOF trwałości.

Aby uzyskać więcej informacji o wydajności, korzystając z AOF trwałości, zobacz [AOF jest wpływ trwałości w całym, opóźnienia lub wydajności Moje pamięci podręcznej?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>Co się stanie, jeśli mają I skalować tooa inny rozmiar i przywróceniu kopii zapasowej utworzonej przed hello operacji skalowania?

Zarówno RDB, jak i AOF trwałości:

* Większy rozmiar tooa ma skalowania, nie ma żadnego wpływu.
* Jeśli ma skalować tooa mniejszy rozmiar, i mieć niestandardowej [baz danych](cache-configure.md#databases) ustawienie jest większa niż hello [limit bazy danych](cache-configure.md#databases) dla Twojego nowego rozmiaru danych w tych baz danych nie jest przywrócony. Aby uzyskać więcej informacji, zobacz [jest niestandardowe ustawienie dotyczy podczas skalowania baz danych?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Jeśli ma skalowania tooa mniejszy rozmiar, a nie ma wystarczającej ilości miejsca w hello mniejszy rozmiar toohold wszystkie dane hello z ostatniej kopii zapasowej, klucze hello zostanie wykluczona podczas procesu przywracania hello, zwykle za pomocą hello [allkeys lru](http://redis.io/topics/lru-cache) wykluczenia zasady.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>Częstotliwość wykonywania kopii zapasowych RDB hello można zmienić po utworzeniu pamięci podręcznej hello?
Tak, można zmienić częstotliwość wykonywania kopii zapasowych hello trwałości RDB na powitania **trwałość danych Redis** bloku. Aby uzyskać instrukcje, zobacz [trwałość Redis skonfigurować](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Dlaczego Jeśli częstotliwość wykonywania kopii zapasowych RDB 60 minut istnieje ponad 60 minut między kopii zapasowych?
Nie można uruchomić interwał częstotliwości tworzenia kopii zapasowej trwałości RDB powitania, dopóki hello poprzedniego procesu tworzenia kopii zapasowej zostało ukończone pomyślnie. Częstotliwość wykonywania kopii zapasowych hello wynosi 60 min, trwa proces tworzenia kopii zapasowej toosuccessfully 15 minut, pełną hello następnej kopii zapasowej nie można uruchomić do momentu 75 minut po hello uruchomienie hello poprzedniej kopii zapasowej.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>Co się stanie toohello starych kopii zapasowych RDB podczas tworzenia nowej kopii zapasowej?
Wszystkie kopie zapasowe trwałości RDB z wyjątkiem hello najnowszego są automatycznie usuwane. To usunięcie może się nie powtórzyła natychmiast, ale starsze kopie zapasowe nie są zachowywane przez czas nieograniczony.


### <a name="when-should-i-use-a-second-storage-account"></a>Kiedy należy używać drugiego konta magazynu?

Jeśli uważasz, że masz wyższe niż operacji oczekiwanego zestawu w pamięci podręcznej hello, należy używać drugiego konta magazynu AOF trwałości.  Konfigurowanie konta magazynu pomocniczego hello pomaga upewnić się, że pamięć podręczna nie osiągnąć limity przepustowości magazynu.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>Czy AOF trwałości mają wpływ na całym, opóźnienia lub wydajności Moje pamięci podręcznej?

Trwałości AOF wpływające na przepływność przez około 15 – 20% hello pamięci podręcznej znajduje się poniżej maksymalnego obciążenia (Procesora i serwera załadować zarówno w obszarze 90%). Nie należy opóźnień gdy hello pamięci podręcznej znajduje się w tych granicach. Jednak pamięć podręczna hello osiągną te limity wcześniej z AOF włączone.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Jak usunąć hello drugiego konta magazynu?

Należy usunąć konto magazynu dodatkowej trwałości AOF hello ustawiając hello toobe hello sam jako pierwsze konto magazynu hello drugiego konta magazynu. Aby uzyskać instrukcje, zobacz [AOF Konfigurowanie trwałości](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>Co to jest ponownego zapisywania i jak wpływa na mój pamięci podręcznej?

Gdy plik AOF hello staje się wystarczająco duży, napisz ponownie automatycznie jest umieszczonych w kolejce na powitania pamięci podręcznej. Witaj ponownego zapisywania zmienia rozmiar hello AOF pliku z hello minimalny zbiór potrzebnych operacji toocreate hello bieżącego zestawu danych. Podczas modyfikacji oprogramowania należy wcześniej oczekiwać tooreach ograniczeń wydajności, szczególnie w przypadku pracy z dużymi zestawami danych. Ponownego występować mniej często hello AOF pliku jest większy, ale będzie zająć dużo czasu, gdy nastąpi.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>Co należy oczekiwać podczas skalowania pamięci podręcznej z AOF włączone?

Jeśli plik AOF hello w czasie hello skalowania jest znacznie duży, spodziewać się tootake operacji skalowania hello dłużej niż oczekiwano, ponieważ jej będzie można ponowne załadowanie hello pliku po zakończeniu skalowania.

Aby uzyskać więcej informacji na temat skalowania, zobacz [co się stanie, jeśli mają I skalować tooa inny rozmiar i przywróceniu kopii zapasowej utworzonej przed hello operacji skalowania?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>Sposób organizowania danych AOF w magazynie?

Dane przechowywane w plikach AOF jest podzielony na wiele stronicowe na węzeł tooincrease wydajności zapisywania hello toostorage danych. Witaj poniższej tabeli przedstawiono ile stronicowe obiekty BLOB są używane dla każdej warstwy cenowej:

| Warstwa Premium | Obiekty blob |
|--------------|-------|
| P1           | 4 na niezależnego fragmentu    |
| P2           | 8 za niezależnego fragmentu    |
| P3           | 16 na niezależnego fragmentu   |
| P4           | 20 za niezależnego fragmentu   |

Jeśli klaster jest włączona, każdy identyfikator niezależnego fragmentu w pamięci podręcznej hello ma własny zestaw stronicowe obiekty BLOB, jak wskazano w powyższej tabeli hello. Na przykład P2 pamięci podręcznej z trzech odłamków rozdziela jego pliku AOF między 24 stronicowych obiektów blob (8 obiekty BLOB na niezależnego fragmentu z 3 odłamków).

Po ponownego zapisywania dwa zestawy plików AOF istnieje w magazynie. Ponownego występują w tle hello i Dołącz toohello pierwszego zestawu plików, podczas gdy operacje na zestawie wysłanych toohello pamięci podręcznej podczas ponownego zapisywania hello Dołącz toohello drugi zestaw. Kopii zapasowej są tymczasowo przechowywane podczas ponownego w razie awarii, ale jest usuwany natychmiast, po zakończeniu ponownego zapisywania.


## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak toouse premium więcej pamięci podręcznej funkcji.

* [Wprowadzenie toohello pamięci podręcznej Redis Azure Premium warstwy](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
