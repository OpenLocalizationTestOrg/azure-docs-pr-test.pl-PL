---
title: "tooupdate aaaHow usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze tooupdate na platformie Azure. Dowiedz się, jak tooensure dostępności będzie kontynuowana, aktualizacja usługi w chmurze."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>Jak tooupdate usługi w chmurze

Aktualizowanie usługi w chmurze, tym zarówno role i system operacyjny, gościa jest procesem trzech fazach. Po pierwsze hello pliki binarne i pliki konfiguracji hello nowej usługi w chmurze lub wersja systemu operacyjnego, należy przekazać. Następnie Azure rezerwuje zasobów obliczeniowych i sieci dla usługi w chmurze hello na podstawie wymagań hello hello nowej wersji usługi chmury. Na koniec Azure wykonuje stopniowego uaktualnienia tooincrementally aktualizacji hello dzierżawy toohello nowej wersji lub Gość systemu operacyjnego, przy zachowaniu dostępności sieci. W tym artykule omówiono szczegóły hello ten ostatni krok — Witaj uaktualnienia stopniowego.

## <a name="update-an-azure-service"></a>Aktualizacja usługi Azure
Azure organizuje wystąpienia roli w logiczne grupy o nazwie domen uaktualnienia (UD). Domen uaktualnienia (UD) to logiczne zestawy wystąpień roli, które zostały zaktualizowane w grupie.  Aktualizacje platformy Azure w chmurze usługi UD jeden jednocześnie, dzięki czemu wystąpień w innych toocontinue UDs obsługujące ruch.

Witaj domyślna liczba domen uaktualnienia wynosi 5. Dodając atrybut upgradeDomainCount hello w pliku definicji hello usługi (csdef), można określić różne liczby domen uaktualnienia. Aby uzyskać więcej informacji na temat atrybutu upgradeDomainCount hello zobacz [schematu sieć Web](https://msdn.microsoft.com/library/azure/gg557553.aspx) lub [schematu proces roboczy](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Po wykonaniu aktualizacji w miejscu z jednego lub większej liczby ról w usłudze Azure aktualizuje zestawy wystąpień roli, zgodnie z toowhich domeny uaktualnienia toohello, do których należą. Aktualizacje platformy Azure, wszystkich wystąpień hello w danej domenie uaktualnienia — zatrzymywanie, aktualizowanie, przełącza je w tryb online — powrotem przenosi hello dalej domeny. Zatrzymując tylko wystąpień hello w bieżącym hello domena uaktualnienia, Azure upewnia się, że nastąpi aktualizacja z hello najniższe możliwe toohello wpływ usługi. Aby uzyskać więcej informacji, zobacz [jak przebieg aktualizacji hello](#howanupgradeproceeds) dalszej części tego artykułu.

> [!NOTE]
> Podczas terminy hello **aktualizacji** i **uaktualnienia** ma nieco inne znaczenie w kontekście hello Azure, używane zamiennie hello procesów oraz opisy funkcji hello w tym dokumencie.
>
>

Usługi należy zdefiniować co najmniej dwóch wystąpień roli dla tej roli toobe aktualizacji w miejscu bez przestoju. Jeśli usługa hello składa się tylko jedno wystąpienie jedną rolę, usługi będą niedostępne, dopóki hello w miejscu aktualizacji zostało zakończone.

W tym temacie omówiono hello następujących informacji o aktualizacji platformy Azure:

* [Dozwolone zmiany usługi podczas aktualizacji](#AllowedChanges)
* [Jak będzie kontynuowana uaktualnienia](#howanupgradeproceeds)
* [Wycofywanie aktualizacji](#RollbackofanUpdate)
* [Inicjowanie wielu operacji mutating na bieżące wdrożenia.](#multiplemutatingoperations)
* [Rozkład ról domen uaktualnienia](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Dozwolone zmiany usługi podczas aktualizacji
Witaj poniższej tabeli przedstawiono hello dozwolone zmiany usługi tooa podczas aktualizacji:

| Zmiany dozwolone toohosting, usług i ról | Aktualizacja w miejscu | Przemieszczanego (wymiany wirtualnych adresów IP) | Usuń i ponownie wdróż |
| --- | --- | --- | --- |
| Wersja systemu operacyjnego |Tak |Tak |Tak |
| Poziom zaufania platformy .NET |Tak |Tak |Tak |
| Rozmiar maszyny wirtualnej<sup>1</sup> |Tak<sup>2</sup> |Tak |Tak |
| Ustawienia magazynu lokalnego |Zwiększ tylko<sup>2</sup> |Tak |Tak |
| Dodawanie lub usuwanie ról w usłudze |Tak |Tak |Tak |
| Liczba wystąpień określonej roli |Tak |Tak |Tak |
| Liczba lub typ punktów końcowych dla usługi |Tak<sup>2</sup> |Nie |Tak |
| Nazwy i wartości ustawień konfiguracji |Tak |Tak |Tak |
| Wartości (ale nie nazwy) ustawień konfiguracji |Tak |Tak |Tak |
| Dodaj nowe certyfikaty |Tak |Tak |Tak |
| Zmiana istniejących certyfikatów |Tak |Tak |Tak |
| Wdrażanie nowego kodu |Tak |Tak |Tak |

<sup>1</sup> toohello podzbiór dostępne dla usługi w chmurze hello ograniczone zmiany rozmiaru.

<sup>2</sup> wymaga zestawu SDK platformy Azure w wersji 1.5 lub nowszego.

> [!WARNING]
> Zmiana rozmiaru maszyny wirtualnej hello zniszczy danych lokalnych.
>
>

Witaj, następujące elementy nie są obsługiwane podczas aktualizacji:

* Zmiana nazwy hello roli. Usuń, a następnie dodaj rolę hello hello nową nazwę.
* Zmiana hello liczba domen uaktualnienia.
* Zmniejszenie rozmiaru hello hello zasobów lokalnych.

W przypadku wprowadzania inne aktualizacje definicji tooyour usługi, takie jak zmniejszenie hello rozmiar zasobu lokalnego zamiast tego należy wykonać aktualizację wymiany adresów VIP. Aby uzyskać więcej informacji, zobacz [wymiany wdrożenia](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Jak będzie kontynuowana uaktualnienia
Można zdecydować, czy ma tooupdate wszystkie role hello w usłudze lub jedną rolę w usłudze hello. W obu przypadkach wszystkie wystąpienia każdej roli, który jest uaktualniany i toohello pierwszej domeny uaktualnienia należy są zatrzymane, uaktualnione i przywrócony do trybu online. Po ich przywróceniu online, hello wystąpień w drugiej domenie uaktualnienia hello są zatrzymane, uaktualnione i przywrócony do trybu online. Usługi w chmurze może mieć co najwyżej jedno uaktualnienie active naraz. uaktualnienie Hello jest zawsze przeprowadzane przy użyciu najnowszej wersji hello hello usługi w chmurze.

Witaj poniższym diagramie przedstawiono sposób uaktualniania hello będzie kontynuowane w przypadku uaktualniania wszystkich ról hello w usłudze hello:

![Uaktualnij usługę](media/cloud-services-update-azure-service/IC345879.png "uaktualnianie usługi")

Ten dalej diagramie przedstawiono, jak hello aktualizacji będzie kontynuowana, Jeśli uaktualniasz tylko jedną rolę.

![Uaktualnienie roli](media/cloud-services-update-azure-service/IC345880.png "uaktualnienia roli")  

Podczas aktualizacji automatycznych hello Kontroler sieci szkieletowej Azure okresowo ocenia kondycję hello toodetermine usługi chmury hello podczas jego bezpieczne toowalk hello UD dalej. Tej oceny kondycji jest wykonywane na podstawie-role i uwzględnia tylko wystąpienia w najnowszej wersji hello (tj. wystąpień z UDs, które już zostały udał). Sprawdza, czy minimalna liczba wystąpień roli dla każdej roli, zostały osiągnięte zadowalające stanu terminala.

### <a name="role-instance-start-timeout"></a>Limit czasu uruchomienia wystąpienia roli
Witaj kontrolera sieci szkieletowej będzie czekać tooreach wystąpienia każdej roli stanu uruchomiono na 30 minut. Jeśli upływem limitu czasu hello, hello kontrolera sieci szkieletowej będą nadal przejście toohello następne wystąpienie roli.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Wpływ toodrive danych podczas uaktualniania usługi w chmurze

Podczas uaktualniania usługi z wystąpień toomultiple pojedyncze wystąpienie usługi zostanie przeniesiony w dół podczas uaktualniania hello odbywa się ze względu na sposób toohello Azure uaktualnienia usługi. Hello umowę dotyczącą poziomu gwarantujących usługi dostępności usługi ma zastosowanie tylko tooservices, które zostały wdrożone za pomocą więcej niż jedno wystąpienie. Witaj Poniższa lista zawiera opis wpływu każdego scenariusza uaktualniania usługi Azure hello danych na każdym dysku:

|Scenariusz|Dysku c.|Dysk D|Dysk E|
|--------|-------|-------|-------|
|Ponowne uruchomienie maszyny Wirtualnej|Zachowane|Zachowane|Zachowane|
|Ponowne uruchomienie portalu|Zachowane|Zachowane|Zniszczone|
|Portal odtworzenia z obrazu|Zachowane|Zniszczone|Zniszczone|
|Uaktualnienie w miejscu|Zachowane|Zachowane|Zniszczone|
|Węzeł migracji|Zniszczone|Zniszczone|Zniszczone|

Należy pamiętać, że w hello powyżej listy, hello dysku E: reprezentuje hello roli katalogu głównym dysku, nie powinien być ustalony. Zamiast tego należy użyć hello **RoleRoot %** dysku hello toorepresent zmiennej środowiska.

toominimize hello przestoju podczas uaktualniania do jednego wystąpienia usługi, wdrażanie wielu wystąpień usługi toohello przemieszczania serwer i przeprowadzić wymiany wirtualnych adresów IP.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Wycofywanie aktualizacji
Azure zapewnia elastyczność w zarządzaniu usług podczas aktualizacji, co pozwala na zainicjowanie dodatkowe operacje w usłudze, po zaakceptowaniu żądania początkowego aktualizacji hello przez kontroler sieci szkieletowej Azure hello. Wycofywania można wykonać tylko w przypadku aktualizacji (zmiana konfiguracji) lub Trwa uaktualnianie hello **w toku** stanu na powitania wdrożenia. Aktualizacji lub uaktualnieniu jest uważany za toobe trwa tak długo, jak istnieje co najmniej jedno wystąpienie usługi hello, który nie został jeszcze zaktualizowany toohello nowej wersji. tootest zezwolić na wycofanie, sprawdź wartość hello hello RollbackAllowed flagi, zwracane przez [uzyskać wdrożenia](https://msdn.microsoft.com/library/azure/ee460804.aspx) i [pobrać właściwości usługi chmury](https://msdn.microsoft.com/library/azure/ee460806.aspx) operacje, ustawiono tootrue.

> [!NOTE]
> Tylko ułatwia wykrywanie toocall wycofywania na **w miejscu** aktualizacji lub uaktualnienia, ponieważ wymagają uaktualnienia wymiany adresów VIP zastępowanie jeden cały działającego wystąpienia usługi z inną.
>
>

Wycofywanie aktualizacji w toku ma powitania po wpływ na wdrożenie hello:

* Wszystkie wystąpienia roli, które nie zostało jeszcze zaktualizowane lub uaktualnione toohello nowej wersji nie są zaktualizowane lub uaktualnione, ponieważ już uruchomionych wystąpień tych wersji docelowej hello hello usługi.
* Dowolnej roli wystąpienia, który ma już zaktualizowany lub uaktualnionych toohello nowej wersji pakietu usługi hello (\*cspkg) pliku lub hello konfiguracji usługi (\*.cscfg) mają przywróconego toohello wersji sprzed uaktualnienia z pliku (lub oba pliki) te pliki.

Funkcjonalnie odbywa się przez hello następujące funkcje:

* Witaj [wycofywania aktualizacji lub uaktualnienia](https://msdn.microsoft.com/library/azure/hh403977.aspx) operacja, która może być wywoływana dla aktualizacji konfiguracji (wyzwalane przez wywołanie metody [zmiana konfiguracji wdrożenia](https://msdn.microsoft.com/library/azure/ee460809.aspx)) lub uaktualnienia (wyzwalane przez wywołanie metody [ Uaktualnienia wdrożenia](https://msdn.microsoft.com/library/azure/ee460793.aspx)) tak długo, jak istnieje co najmniej jedno wystąpienie usługi hello który nie został jeszcze zaktualizowany toohello nowej wersji.
* Witaj zablokowany element i elementu RollbackAllowed hello, które są zwracane jako część treści odpowiedzi hello hello [uzyskać wdrożenia](https://msdn.microsoft.com/library/azure/ee460804.aspx) i [pobrać właściwości usługi chmury](https://msdn.microsoft.com/library/azure/ee460806.aspx) operacje:

  1. element zablokowany Hello umożliwia toodetect mutating operację można wywołać w ramach danego wdrożenia.
  2. Witaj RollbackAllowed element pozwala toodetect podczas hello [wycofywania aktualizacji lub uaktualnienia](https://msdn.microsoft.com/library/azure/hh403977.aspx) operację można wywołać w danym wdrożeniu.

  W kolejności tooperform wycofanie nie masz toocheck hello zablokowany, a także hello RollbackAllowed elementów. Wystarczy tooconfirm czy RollbackAllowed ustawiono tootrue. Te elementy są zwracane tylko, jeśli te metody są wywoływane przy użyciu hello nagłówek żądania, ustaw za "x-ms-version: 2011-10-01" lub nowszej wersji. Aby uzyskać więcej informacji o nagłówkach przechowywania wersji, zobacz [przechowywanie wersji usługi zarządzania](https://msdn.microsoft.com/library/azure/gg592580.aspx).

Istnieje kilka sytuacji, gdy wycofywania aktualizacji lub uaktualnienie nie jest obsługiwane, są to następujące dane:

* Spadek zużycia zasobów lokalnych — Jeśli hello aktualizacji zwiększa hello zasobów lokalnych roli hello platformy Azure nie zezwala na wycofanie.
* Limity przydziału — Jeśli hello aktualizacja została skali w dół operację, którą użytkownik może już nie mieć wystarczające operacji wycofywania hello toocomplete obliczeniowe przydziału. Każda subskrypcja platformy Azure ma limit przydziału skojarzonych z nim określający hello maksymalna liczba rdzeni, które mogą być używane przez wszystkie usługi hostowanej, które należy toothat subskrypcji. Jeśli wykonania operacji wycofywania aktualizacji danego spowodowałaby subskrypcję za pośrednictwem przydziału, a następnie który wycofanie nie zostaną włączone.
* Sytuacja wyścigu — Jeśli ukończono aktualizowanie początkowej hello, wycofanie nie jest możliwe.

Jest przykładem podczas wycofywania hello aktualizacji mogą być przydatne, jeśli używasz hello [uaktualniania wdrożenia](https://msdn.microsoft.com/library/azure/ee460793.aspx) operacji ręczny tryb toocontrol hello szybkości, jaką usługa hostowana główna tooyour uaktualnienia w miejscu Azure jest wdrażana.

Podczas fazy hello hello uaktualnienia należy wywołać [uaktualniania wdrożenia](https://msdn.microsoft.com/library/azure/ee460793.aspx) w trybie ręcznym i rozpocząć toowalk domen uaktualnienia. Jeśli w pewnym momencie podczas monitorowania hello uaktualnienia, możesz zaznaczyć niektórych wystąpień roli w hello pierwszych uaktualnienia domen, które należy zbadać ma przestać odpowiadać, można wywołać hello [wycofywania aktualizacji lub uaktualnienia](https://msdn.microsoft.com/library/azure/hh403977.aspx) operacji na powitania wdrożenia, które spowoduje pozostawienie niezmienionej hello wystąpienia, które nie ma jeszcze uaktualniona i wycofywania wystąpień, które zostały uaktualnione toohello poprzedniego pakiet usługi i konfiguracji.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Inicjowanie wielu operacji mutating na bieżące wdrożenia.
W niektórych przypadkach może być tooinitiate wiele równoczesnych operacji mutating na bieżące wdrożenia. Na przykład może wykonywać aktualizacji usługi i, gdy aktualizacja jest rozwijane w usłudze, ma toomake niektóre zmiany, np. tooroll Witaj ponownie aktualizacji, zastosuj inną aktualizację lub nawet usuwać hello wdrożenia. Przypadek, w którym może to być konieczne jest, czy uaktualnianie usługi zawiera buggy kodu, co powoduje, że rola uaktualnionego wystąpienia toorepeatedly awarii. W takim przypadku hello Azure kontrolera sieci szkieletowej nie będą mogli toomake postęp stosowania uaktualnić, ponieważ określono za małą liczbę wystąpień w domenie uaktualnionego hello są w dobrej kondycji. Ten stan jest określony tooas *zatrzymane wdrożenia*. Witaj wdrożenia można przylegał wycofywanie hello aktualizacji lub stosowania aktualizacji świeże w górnej części hello awarii jednego.

Po otrzymaniu przez kontroler sieci szkieletowej Azure hello hello żądania początkowego tooupdate lub Uaktualnij program hello usługi można uruchomić kolejnych operacji mutacja. Oznacza to, że nie masz toowait dla toocomplete początkowej operacji hello przed rozpoczęciem inna operacja mutating.

Inicjowanie drugiej operacji aktualizacji, podczas pierwszej aktualizacji hello jest wykonywana będzie wykonywać operacji wycofywania toohello podobne. Jeśli aktualizacja drugi hello jest w trybie automatycznym, pierwsza domena uaktualnienia hello zostaną uaktualnione natychmiast, prawdopodobnie wiodące tooinstances z wielu domen uaktualnienia w trybie offline na powitania sam punkt w czasie.

Witaj mutacja operacje są następujące: [zmiany konfiguracji wdrożenia](https://msdn.microsoft.com/library/azure/ee460809.aspx), [uaktualniania wdrożenia](https://msdn.microsoft.com/library/azure/ee460793.aspx), [stan wdrożenia aktualizacji](https://msdn.microsoft.com/library/azure/ee460808.aspx), [usunąć Wdrożenie](https://msdn.microsoft.com/library/azure/ee460815.aspx), i [wycofywania aktualizacji lub uaktualnieniu](https://msdn.microsoft.com/library/azure/hh403977.aspx).

Dwie operacje [uzyskać wdrożenia](https://msdn.microsoft.com/library/azure/ee460804.aspx) i [pobrać właściwości usługi chmury](https://msdn.microsoft.com/library/azure/ee460806.aspx), zwróć hello zablokowany Flaga, która może być toodetermine zbadane, czy mutating operację można wywołać w ramach danego wdrożenia.

W kolejności toocall hello wersji tych metod, która zwraca flagę zablokowany hello, musisz ustawić nagłówek żądania za "x-ms-version: 2011-10-01" lub nowszego. Aby uzyskać więcej informacji o nagłówkach przechowywania wersji, zobacz [przechowywanie wersji usługi zarządzania](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Rozkład ról domen uaktualnienia
Azure równomiernie rozdziela wystąpień roli dla pewnej liczby domen uaktualnienia, które można skonfigurować jako część pliku definicji (csdef) hello usługi. Maksymalna liczba domen uaktualnienia Hello jest 20 i hello domyślna to 5. Aby uzyskać więcej informacji o sposobie toomodify hello pliku definicji usługi, zobacz [schematu definicji usługi Azure (pliki csdef pliku)](cloud-services-model-and-package.md#csdef).

Na przykład jeśli rola użytkownika ma dziesięć wystąpień, domyślnie każdej z domen zawiera dwa wystąpienia. Jeśli rola użytkownika ma 14 wystąpień cztery hello domen uaktualnienia zawiera trzy wystąpienia i piątej domeny zawiera dwa.

Domen uaktualnienia są oznaczone symbolem liczony od zera indeks: hello pierwszej domeny uaktualnienia ma identyfikator równy 0, a druga domena uaktualnienia hello ma identyfikator równy 1 i tak dalej.

Witaj Poniższy diagram przedstawia rozkład usługi niż zawiera dwie role po usługi hello definiuje dwie domeny uaktualnienia. Hello jest uruchomiona osiem wystąpień roli sieci web hello i dziewięć wystąpienia hello roli procesu roboczego.

![Dystrybucji domen uaktualnienia](media/cloud-services-update-azure-service/IC345533.png "dystrybucji domen uaktualnienia")

> [!NOTE]
> Należy pamiętać, że Azure kontroluje sposób przydzielania wystąpień domen uaktualnienia. Nie jest możliwe toospecify, które wystąpienia są przydzielane toowhich domeny.
>
>

## <a name="next-steps"></a>Następne kroki
[W jaki sposób tooManage usług w chmurze](cloud-services-how-to-manage.md)  
[W jaki sposób tooMonitor usług w chmurze](cloud-services-how-to-monitor.md)  
[W jaki sposób tooConfigure usług w chmurze](cloud-services-how-to-configure.md)  
