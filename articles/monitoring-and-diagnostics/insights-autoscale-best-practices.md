---
title: "aaaBest praktyki dotyczące skalowania automatycznego | Dokumentacja firmy Microsoft"
description: "Wzorce skalowania automatycznego na platformie Azure aplikacje sieci Web, zestawy skalowania maszyny wirtualnej i usługi w chmurze"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Najlepsze rozwiązania dotyczące automatycznego skalowania
Ten artykuł zawiera najlepsze rozwiązania w zakresie tooautoscale na platformie Azure. Azure Monitor skalowania automatycznego ma zastosowanie tylko zbyt[zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/), i [usługi aplikacji — aplikacje sieci Web](https://azure.microsoft.com/services/app-service/web/). Innymi usługami Azure, użyj metod skalowania.

## <a name="autoscale-concepts"></a>Pojęcia dotyczące skalowania automatycznego
* Zasób może mieć tylko *jeden* ustawieniu skalowania automatycznego
* Ustawienia automatycznego skalowania może zawierać jeden lub więcej profilów i każdy profil może mieć co najmniej jedną regułę automatycznego skalowania.
* Ustawienia skalowania automatycznego skaluje wystąpień w poziomie, który jest *limit* przez odpowiednie zwiększenie hello wystąpień i *w* dzięki skróceniu hello liczba wystąpień.
  Ustawienie skalowania automatycznego zawiera maksymalną, minimum i wartości domyślnej wystąpień.
* Zadanie automatycznego skalowania odczytuje zawsze hello skojarzonych metryki tooscale sprawdzając, czy został przekroczony hello skonfigurowanej wartości progowej dla skalowalnego w poziomie lub w skali. Umożliwia wyświetlanie listy metryk tego skalowania automatycznego można skalować przez w [metryki wspólnej Skalowanie automatyczne Azure Monitor](insights-autoscale-common-metrics.md).
* Wszystkie Progi są obliczane na poziomie wystąpienia. Na przykład "skali przez 1 wystąpienie gdy średni Procesora > 80%, gdy liczba wystąpień jest równa 2", oznacza skalowalnego w poziomie, gdy hello średnie wykorzystanie Procesora we wszystkich wystąpieniach jest większa niż 80%.
* Zawsze otrzymywać powiadomienia o niepowodzeniu za pośrednictwem poczty e-mail. W szczególności hello właściciela, współautora i czytników zasobu docelowego hello otrzymywać wiadomości e-mail. Możesz również otrzymać *odzyskiwania* wiadomość e-mail, gdy skalowania automatycznego odzyskiwania po awarii i uruchamia działa prawidłowo.
* Użytkownik może zdecydować się na tooreceive skalowania pomyślnie akcji powiadomienia za pośrednictwem poczty e-mail i elementów webhook.

## <a name="autoscale-best-practices"></a>Najlepsze rozwiązania w zakresie skalowania automatycznego
Użyj hello następujące najlepsze rozwiązania w zakresie, jak używać automatycznego skalowania.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Upewnij się, hello maksymalne i minimalne wartości są różne, a także mieć odpowiedni margines między nimi
Jeśli to ustawienie, które ma co najmniej = 2, maksymalna = 2 i bieżącą liczbę wystąpień hello jest 2, może wystąpić żadnej akcji skalowania. Zachować odpowiedni poziom między liczby wystąpień maksymalne i minimalne hello, które łączą się. Funkcja automatycznego skalowania skaluje zawsze między tymi limitami.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>Ręczne skalowanie jest resetowany przez skalowania automatycznego min i max
Jeśli ręcznie zaktualizuj hello wystąpienia licznika tooa wartość powyżej lub poniżej maksymalnej hello hello aparat skalowania automatycznego automatycznie skaluje wstecz toohello minimalną (Jeśli poniżej) lub hello maksymalną (jeśli powyżej). Na przykład można ustawić zakresu powitania od 3 do 6. Jeśli masz jedno uruchomione wystąpienie aparatu skalowania automatycznego hello skaluje wystąpień too3 po jego następnym uruchomieniu. Podobnie, jego czy skali w 8 wystąpień kopii too6 po jego następnym uruchomieniu.  Ręczne skalowanie jest bardzo tymczasowe, chyba że zresetować hello również reguł skalowania automatycznego.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Zawsze używaj połączenia skalowalnego w poziomie i w skali reguł, które wykonuje wzrostu i zmniejszenie
Jeśli używasz tylko jednej części kombinacja hello skalowania automatycznego skalowania — w tym pojedynczy przy, dopóki hello maksymalnej lub minimalnej, osiągnięto.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>Nie przełączać się między hello portalu Azure i hello klasycznego portalu Azure podczas zarządzania skalowania automatycznego
Dla usług aplikacji (aplikacje sieci Web) i usługi w chmurze Użyj hello toocreate portalu Azure (portal.azure.com) i Zarządzaj ustawieniami automatycznego skalowania. Zestawy skalowania maszyny wirtualnej można użyć programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST toocreate i zarządzaj nimi ustawieniu skalowania automatycznego. Nie przełączać się między hello klasycznego portalu Azure (manage.windowsazure.com) i hello portalu Azure (portal.azure.com) podczas zarządzania konfiguracjami skalowania automatycznego. Witaj klasycznego portalu Azure i jego podstawowym wewnętrznej bazy danych ma ograniczenia. Przenieś skalowania automatycznego toomanage portalu Azure toohello przy użyciu graficznego interfejsu użytkownika. Opcje Hello są skalowania automatycznego hello toouse programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST (za pomocą Eksploratora zasobów Azure).

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Wybierz hello Statystyka odpowiednie dla Twojej metryki diagnostyki
Diagnostyka miar, można wybierać między *średni*, *co najmniej*, *maksymalna* i *całkowita* jako metryki tooscale przez. Statystyka najczęściej Hello jest *średni*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Wybierz progi hello dokładnie dla wszystkich typów metryki
Zaleca się uważnie wybranie innego progi dla skalowalnego w poziomie i skali w sytuacji, w praktyce w oparciu.

Firma Microsoft *nie jest zalecane* Ustawienia skalowania automatycznego, takie jak hello przykłady można podać poniżej hello takie same lub bardzo podobne wartości progowe, a w warunkach:

* Zwiększyć wystąpień 1 Jeśli liczba Liczba wątków < = 600
* Zmniejsz wystąpienia o 1 Jeśli liczba Liczba wątków > = 600

Oto przykład co może prowadzić tooa zachowanie, które mogą być mylące. Należy wziąć pod uwagę powitania po sekwencji.

1. Załóżmy, istnieją 2 toobegin wystąpień z, a następnie hello średnią liczbę wątków dla każdego wystąpienia rozwoju too625.
2. Funkcja automatycznego skalowania skaluje się dodanie 3 wystąpienia.
3. Następnie przyjęto założenie, czy liczba wątków średni hello przez wystąpienie znajduje się too575.
4. Przed skalowania, skalowania automatycznego próbuje tooestimate jakie hello stan końcowy będzie, jeśli jest on skalowany w. Na przykład (bieżąca liczba wystąpień) 575 x 3 = 1,725 / 2 (końcowego liczba wystąpień, gdy skalowany w dół) = 862.5 wątków. Oznacza to, że skalowania automatycznego byłyby tooimmediately skalowalnego w poziomie ponownie nawet po jego skalowania, jeśli hello wątku średnia liczba pozostaje hello tego samego lub nawet objęty niewielkiej ilości. Jednak jeśli jego skalowanie ponownie, powtórz czy hello całego procesu, początkowe tooan nieskończoną pętlę.
5. tooavoid tej sytuacji (określane jako "flapping"), skalowania automatycznego nie obsługuje w dół w ogóle. Zamiast tego pomija i reevaluates hello o tej warunku ponownie wykonuje zadanie hello dalej czasu hello usługi. Można to należy mylić wiele osób, ponieważ funkcja automatycznego skalowania nie pojawi się toowork, gdy liczba wątków średni hello 575.

Szacowanie podczas skalowania w jest zamierzone tooavoid "niestabilny" sytuacji, gdy akcje w skali i skalowalnego w poziomie stale Przejdź i z powrotem. Po wybraniu hello takie same progi dla skalowalnego w poziomie i w należy pamiętać o to zachowanie.

Firma Microsoft zaleca, wybierając odpowiedni poziom między hello skalowalnego w poziomie i w progów. Na przykład należy wziąć pod uwagę powitania po lepsze kombinacja reguły.

* Zwiększyć wystąpień 1 Jeśli liczba procesora CPU Wynoszące % > = 80
* Zmniejsz wystąpienia o 1 Jeśli liczba procesora CPU Wynoszące % < = 60

W takim przypadku  

1. Załóżmy, że istnieją 2 toostart wystąpień z.
2. Jeśli hello średni procent użycia procesora CPU w wystąpieniach przestanie too80, automatycznego skalowania skaluje się dodanie trzeci wystąpienia.
3. Teraz załóżmy przez czas Procesora hello % wypada too60.
4. Jego skalowania automatycznego skalowania w reguły szacuje stan końcowy hello, gdyby tooscale w. Na przykład (bieżąca liczba wystąpień) 60 x 3 = 180 / 2 (końcowego liczba wystąpień, gdy skalowany w dół) = 90. Dlatego skalowania automatycznego nie skali w ponieważ poza tooscale może mieć natychmiast ponownie. Zamiast tego pomija skalowania.
5. Umożliwia sprawdzenie skalowania automatycznego czas następnego Hello toofall too50 nadal hello procesora CPU. Ponownie - szacuje wystąpienia 50 x 3 = 150 / 2 wystąpień = 75, który jest poniżej progu skalowalnego w poziomie hello 80, więc on skalowany w pomyślnie too2 wystąpień.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Zagadnienia dotyczące wartości progowe dla specjalnych metryki skalowania
 Dla specjalnych metryki na przykład metryka długość magazynu lub kolejką usługi Service Bus próg hello jest hello średnią liczbę wiadomości na bieżąca liczba wystąpień. Wybierz uważnie hello wybierz wartość progowa hello ta metryka.

Umożliwia ona zilustrować z tooensure przykład zrozumienie zachowania hello lepiej.

* Zwiększenie wystąpienia według liczby 1, gdy liczba komunikatów kolejki magazynu > = 50
* Zmniejsz wystąpienia według liczby 1 Jeśli liczba komunikatów kolejki magazynu < = 10

Należy wziąć pod uwagę następujące sekwencji hello:

1. Istnieją 2 wystąpienia kolejki magazynu.
2. Zachowaj przesyłanych wiadomości i przeglądając kolejki magazynu hello, łączna liczba hello odczytuje 50. Użytkownik może założenie, że tego skalowania automatycznego powinien rozpocząć akcji skalowania w poziomie. Jednak należy pamiętać, że nadal 50/2 = 25 komunikaty dla każdego wystąpienia. Tak skalowalnych w poziomie nie występuje. Dla pierwszego toohappen skalowalnego w poziomie hello hello łącznej liczbie komunikatów w kolejce magazynu hello powinna być 100.
3. Następnie przyjęto założenie, że hello łącznej liczbie komunikatów osiągnie 100.
4. 3 wystąpienia kolejki magazynu jest dodawany powodu tooa akcji skalowania w poziomie.  Witaj następnej akcji skalowania w poziomie nie nastąpi aż do hello całkowita liczba wiadomości w kolejce hello osiągnie 150, ponieważ 150/3 = 50.
5. Teraz hello liczbę wiadomości w kolejce hello pobiera mniejsze. Z wystąpieniami 3 hello pierwszej skali w akcji spowodowany hello całkowita liczba wiadomości we wszystkich kolejkach sumują too30 ponieważ 30/3 = 10 komunikaty dla każdego wystąpienia, czyli hello w skali próg.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Zagadnienia dotyczące skalowania, gdy wiele profilów skonfigurowanych w ustawieniu skalowania automatycznego
W ustawieniu skalowania automatycznego można wybrać profil domyślny, który jest zawsze stosowane bez jej zależności od harmonogramu lub czasu, lub możesz cyklicznego profil lub określony zakres daty i godziny.

Kiedy usługa skalowania automatycznego przetwarza je, zawsze sprawdzają w hello w następującej kolejności:

1. Stałe profilu daty
2. Cykliczne profilu
3. Domyślny profil ("Always")

Jeśli profil warunek jest spełniony, skalowania automatycznego nie sprawdza hello dalej warunku profilu poniżej. Funkcja automatycznego skalowania przetwarza tylko jeden profil naraz. Oznacza to, jeśli chcesz, aby tooalso obejmują warunek przetwarzania z profilu niższego poziomu, te reguły musi zawierać również w bieżącym profilu hello.

Umożliwia przeglądanie to przykładu:

Obraz powitania poniżej przedstawiono ustawienia skalowania automatycznego profil domyślny minimalny wystąpień = 2 do maksymalnej wystąpień = 10. W tym przykładzie reguły są tooscale skonfigurowanych w poziomie, gdy hello liczba wiadomości w kolejce hello jest większa niż 10 i skali w hello liczba wiadomości w kolejce hello jest mniejsza niż 3. Dlatego teraz hello zasobów można skalować między wystąpieniami 2 do 10.

Ponadto jest profil cyklicznego ustawić od poniedziałku. Ma wartość minimalną wystąpień = 2, a maksymalna wystąpienia = 12. Oznacza to, w poniedziałek, skalowania automatycznego hello pierwszego czasu sprawdza, czy ten stan, jeśli liczba wystąpień hello jest równa 2, skaluje się toohello nowe co najmniej 3. Tak długo, jak skalowania automatycznego nadal toofind (poniedziałek) dopasować ten stan profilu, przetwarza tylko hello na podstawie procesora CPU skalowania w poziomie/w skonfigurowanych reguł dla tego profilu. W tej chwili nie sprawdza długość kolejki hello. Jednak jeśli chcesz także hello kolejki długość warunku toobe zaznaczone, należy uwzględnić te reguły z profil domyślny hello również w profilu od poniedziałku.

Podobnie gdy skalowania automatycznego zmienia profil domyślny toohello Wstecz, najpierw sprawdza, czy zostały spełnione warunki minimalną i maksymalną hello. Jeśli hello liczbę wystąpień w czasie hello jest 12, go skaluje w too10, hello maksymalny dozwolony dla hello profil domyślny.

![Ustawienia skalowania automatycznego](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Zagadnienia dotyczące skalowania, gdy skonfigurowano wiele reguł w profilu
Istnieją przypadki, w których użytkownik może mieć tooset wiele reguł w profilu. Witaj następującego zestawu reguł skalowania automatycznego są używane przy użyciu usługi ustawianą wiele reguł.

Na *skalowanie*, skalowania automatycznego jest uruchamiany, jeśli reguły jest spełniony.
Na *w skali*, wszystkie reguły zostały spełnione toobe wymagają skalowania automatycznego.

tooillustrate, założono, że istnieje hello 4 reguły skalowania automatycznego:

* Jeśli Procesor < 30%, skalowania w 1
* Jeśli pamięci < 50% skali w 1
* Jeśli Procesor > 75%, skalowalnych w poziomie przez 1
* Jeśli pamięci > 75%, skalowalnych w poziomie przez 1

Następnie wykonaj hello występuje:

* Jeśli 76% jest procesora CPU i pamięci to 50%, możemy skalowalnego w poziomie.
* Jeśli procesora CPU wynosi 50% pamięci wynosi 76% możemy skalowalnego w poziomie.

Na hello drugiej strony, jeśli procesora CPU wynosi 25% i pamięci 51% skalowania automatycznego jest **nie** w skali. Tooscale — w porządku procesora CPU musi być 49% 29% i pamięci.

### <a name="always-select-a-safe-default-instance-count"></a>Wybierz zawsze bezpieczne domyślną liczbę wystąpień
ważne skalowania automatycznego skaluje liczba toothat usługi, gdy nie są dostępne metryki jest Hello domyślną liczbę wystąpień. W związku z tym wybierz domyślną liczbę wystąpień, które jest bezpieczne dla obciążeń.

### <a name="configure-autoscale-notifications"></a>Konfigurowanie powiadomień skalowania automatycznego
Skalowania automatycznego powiadamia hello Administratorzy i współautorzy hello zasobów za pośrednictwem poczty e-mail, jeśli wystąpienia któregokolwiek z hello następujące warunki:

* Funkcja automatycznego skalowania usługi nie powiedzie się tootake akcji.
* Metryki nie są dostępne dla automatycznego skalowania usługi toomake decyzji skali.
* Metryki są dostępne (odzyskiwania) ponownie toomake decyzji skali.
  Oprócz powyższych warunków toohello, można skonfigurować adres e-mail lub elementu webhook tooget powiadomienia o akcji skalowania pomyślnie.
  
Umożliwia także dziennik aktywności hello kondycję alertu toomonitor hello skalowania automatycznego aparatu. Poniżej przedstawiono przykłady zbyt[Utwórz Alert dziennika aktywności toomonitor wszystkie operacje aparat skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) lub zbyt[Tworzenie alertów dziennika aktywności toomonitor wszystkie nie powiodło się skalowania automatycznego skalowania w / skalowanie w poziomie operacje na Subskrypcja](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Następne kroki
- [Utwórz Alert dziennika aktywności toomonitor wszystkie operacje aparat skalowania automatycznego na subskrypcję.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Utwórz Alert dziennika aktywności toomonitor wszystkie nie powiodło się skalowania automatycznego skalowania w / skalowanie operacji dla Twojej subskrypcji](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
