---
title: alerty aaaCreating w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Alerty w analizy dzienników zidentyfikować ważne informacje zawarte w repozytorium OMS i aktywne powiadamia użytkownika o problemy lub wywołanie akcji tooattempt toocorrect je.  W tym artykule opisano, jak toocreate regułę alertu i szczegóły hello różne akcje mogą przyjmować."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Praca z reguły alertów w analizy dzienników
Alerty są tworzone przez reguły alertów, które automatycznie uruchamiać dziennik wyszukiwania w regularnych odstępach czasu.  Jeśli hello wyników spełniających kryteria określonego tworzenia rekordu alertu.  Reguła Hello można następnie automatycznie uruchom jedno lub więcej tooproactively akcje powiadamiał hello alertu lub wywołać inny proces.   

W tym artykule opisano hello toocreate procesów i edytowanie reguły alertów za pomocą portalu OMS hello.  Aby uzyskać więcej informacji o różnych ustawień hello i jak tooimplement wymagane logiki, zobacz [opis alertów w analizy dzienników](log-analytics-alerts.md).

>[!NOTE]
> Nie można obecnie Utwórz lub zmodyfikuj regułę alertu za pomocą hello portalu Azure. 

## <a name="create-an-alert-rule"></a>Tworzenie reguły alertu

Wyszukiwanie hello rekordów, które powinny wywoływać hello alert toocreate regułę alertu za pomocą portalu OMS hello rozpoczyna się od utworzenia dziennika.  Witaj **Alert** przycisk będzie dostępny, można tworzyć i konfigurować hello reguły alertów.

>[!NOTE]
> Obecnie można tworzyć maksymalnie 250 reguły alertów w obszarze roboczym pakietu OMS. 

1. Na stronie Przegląd OMS powitania kliknij **wyszukiwania dziennika**.
2. Utwórz nowe zapytanie wyszukiwania dziennika albo wybierz zapisany dziennik wyszukiwania. 
3. Kliknij przycisk **alertu** u góry hello hello strony tooopen hello **Dodaj regułę alertu** ekranu.
4. Skonfiguruj reguły alertu hello, korzystając z informacji w [szczegóły reguły alertów](#details-of-alert-rules) poniżej.
6. Kliknij przycisk **zapisać** toocomplete hello alertu.  Zostanie ona rozpoczęta natychmiast uruchomiona.


## <a name="edit-an-alert-rule"></a>Edytuj regułę alertu
Aby pobrać listę wszystkich reguł alertów hello **alerty** menu analizy dzienników **ustawienia**.  

![Zarządzanie alertami](./media/log-analytics-alerts/configure.png)

1. W hello OMS konsoli wybierz hello **ustawienia** kafelka.
2. Wybierz **alerty**.

W tym widoku można wykonywać wiele akcji.

* Wyłączanie reguły wybierając **poza** tooit dalej.
* Edytuj regułę alertu, klikając tooit dalej ikonę ołówka hello.
* Usuń regułę alertu, klikając hello **X** ikonę tooit dalej. 

## <a name="details-of-alert-rules"></a>Szczegóły reguły alertów
Podczas tworzenia lub edytowania reguły alertu w portalu OMS hello współpracujesz hello **Dodaj regułę alertu** lub **edytowanie reguły alertu** strony.  następujące tabele Hello opisano hello pól na ekranie.

![Reguła alertu](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>Informacji o alertach
Są to ustawienia podstawowe reguły alertu hello i hello alertów, które tworzy.

| Właściwość | Opis |
|:--- |:---|
| Nazwa | Unikatowa nazwa tooidentify hello reguły alertów. Ta nazwa jest objęta alerty utworzona przez zasadę hello.  |
| Opis | Opcjonalny opis reguły alertu hello. |
| Ważność |Ważność alerty utworzone przez tę regułę. |

### <a name="search-query-and-time-window"></a>Wyszukiwanie zapytania i przedziału czasowego
Witaj wyszukiwania zapytania i przedziału czasowego, które zwracają hello rekordów, które są obliczane toodetermine, jeśli wszystkie alerty powinny być tworzone.

| Właściwość | Opis |
|:--- |:---|
| Zapytania wyszukiwania | To zapytanie hello, które będą uruchamiane.  Hello rekordów zwróconych przez to zapytanie będzie używane toodetermine, czy alert jest tworzony.<br><br>Wybierz **Użyj bieżącego zapytania wyszukiwania** toouse hello bieżącego zapytania, lub wybierz istniejący zapisanego wyszukiwania z listy hello.  Składnia zapytania Hello znajduje się w polu tekstowym hello, gdzie możesz ją zmodyfikować, jeśli to konieczne. |
| Przedział czasu |Określa zakres czasu hello hello zapytania.  Witaj zapytanie zwraca tylko te rekordy, które zostały utworzone w tym zakresie hello bieżącego czasu.  Może to być dowolna wartość od 5 minut do 24 godzin.  Powinna być większa niż lub równa toohello częstotliwość alertów.  <br><br> Na przykład hello razem, gdy okno jest ustawione too60 minut, a zapytanie hello jest uruchomione o 13:15:00, zostanie zwrócony tylko rekordy między 12:15:00 a 13:15:00. |

Podając hello przedział czasu dla reguły alertu hello, zostanie wyświetlony numer hello istniejących rekordów, które spełniają kryteria wyszukiwania hello przedział czasu.  To może pomóc w określeniu częstotliwość hello, która zapewni hello liczba wyników, których się oczekuje.

### <a name="schedule"></a>Harmonogram
Określa, jak często hello zapytania wyszukiwania jest uruchamiany.

| Właściwość | Opis |
|:--- |:---|
| Częstotliwość alertów | Określa, jak często hello zapytania powinny być uruchamiane. Może być dowolną wartość z zakresu od 5 minut do 24 godzin. Powinien być równy tooor poniżej hello przedział czasu.  Jeśli wartość hello jest większa niż przedział czasu hello, istnieje ryzyko rekordów jest pominięte.<br><br>Rozważmy na przykład okno czasu 30 minut i częstotliwość 60 minut.  Jeśli zapytanie hello jest uruchamiana 1:00, zwraca rekordów między 12:30 i 1:00 PM.  Witaj następnym będzie uruchamiane zapytanie hello jest 2:00, jeśli zwróci rekordów między 1:30 i 2:00.  Nigdy nie będzie można obliczyć wszystkie rekordy między 1:00 i 1:30. |


### <a name="generate-alert-based-on"></a>Generuj alert, na podstawie
Definiuje hello kryteria, które będzie porównywany hello wyniki hello toodetermine zapytania wyszukiwania jeśli alert mają zostać utworzone.  Te informacje będą różne w zależności od typu hello reguły alertu, który można wybrać.  Możesz też uzyskać szczegółowe informacje hello typów innej reguły alertu z [opis alertów w analizy dzienników](log-analytics-alerts.md).

| Właściwość | Opis |
|:--- |:---|
| Pomijanie alertów | Po włączeniu pomijania reguły alertu hello akcje dla reguły hello są wyłączone dla określona długość czasu, po utworzeniu nowego alertu. Reguła Hello jest nadal uruchomiona i utworzy rekordów alert po spełnieniu kryteriów hello. Jest to tooallow czasu toocorrect hello problem bez uruchamiania zduplikowane akcje. |

#### <a name="number-of-results-alert-rules"></a>Liczba wyników reguły alertów

| Właściwość | Opis |
|:--- |:---|
| Liczba wyników |Alert jest tworzony, jeśli hello liczbę rekordów zwróconych przez zapytanie hello **większe** lub **mniej niż** hello należy podać wartość.  |

#### <a name="metric-measurement-alert-rules"></a>Metryki pomiaru reguły alertów

| Właściwość | Opis |
|:--- |:---|
| Łączna wartość | Wartość progowa, że każda wartość zagregowaną w wynikach hello przekraczać toobe uznane za naruszenia. |
| Na podstawie alertu wyzwalacza | Witaj wielu naruszeń zabezpieczeń dla alertu toobe utworzony.  Można określić **łączna liczba naruszeń** dowolną kombinację naruszeń między hello wyników można ustawić lub **kolejnych naruszeń** toorequire, który hello naruszeń musi występować w kolejnych próbek. |

### <a name="actions"></a>Akcje
Reguły alertów zawsze spowoduje utworzenie [alertów rekordu](#alert-records) gdy osiągnięty jest próg hello.  Można również zdefiniować lub uruchamiać więcej toobe odpowiedzi na przykład wysyłanie wiadomości e-mail lub uruchamianie elementu runbook.



#### <a name="email-actions"></a>Akcje poczty e-mail
Akcje e-mail Wyślij wiadomość e-mail ze szczegółami hello hello tooone alertu lub więcej adresatów.

| Właściwość | Opis |
|:--- |:---|
| Powiadomienie e-mail |Określ **tak** Jeśli chcesz toobe wiadomości e-mail wysyłane po wyzwoleniu alertu hello. |
| Temat |Podmiotu w hello wiadomości e-mail.  Nie można zmodyfikować hello treści wiadomości powitania. |
| Adresaci |Adresy wszystkich adresatów wiadomości e-mail.  Jeśli określono więcej niż jeden adres, a następnie hello oddzielne adresy średnikiem (;). |

#### <a name="webhook-actions"></a>Akcje elementu Webhook
Akcje elementu Webhook pozwalają tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP POST.

| Właściwość | Opis |
|:--- |:---|
| Webhook |Określ **tak** Jeśli toocall elementu webhook po wyzwoleniu alertu hello. |
| Adres URL elementu Webhook |adres URL Hello hello elementu webhook. |
| Uwzględnij niestandardowy ładunek JSON |Wybierz tę opcję, jeśli chcesz, aby tooreplace hello domyślny ładunek z niestandardowy ładunek. |
| Wprowadź niestandardowy ładunek JSON |niestandardowy ładunek Hello hello elementu webhook.  Zobacz poprzedniej sekcji, aby uzyskać szczegółowe informacje. |

#### <a name="runbook-actions"></a>Działania elementu Runbook
Działania elementu Runbook uruchamiania elementu runbook automatyzacji Azure. 

>[!NOTE]
> Musi mieć rozwiązanie Automatyzacja hello zainstalowane w obszarze roboczym dla tego toobe akcji włączone. 


| Właściwość | Opis |
|:--- |:---|
| Element Runbook | Określ **tak** Jeśli chcesz toostart runbook usługi Automatyzacja Azure, po wyzwoleniu alertu hello.  |
| Konto usługi Automation | Określa hello konto automatyzacji elementów runbook są wybierane w.  To konto akcji hello zawiera połączone toohello obszaru roboczego. |
| Wybierz element runbook | Wybierz hello element runbook ma toostart, podczas tworzenia alertu. |
| Uruchom na | Wybierz **Azure** toorun runbook hello w chmurze hello.  Wybierz **hybrydowy proces roboczy** toorun runbook hello na agenta o [hybrydowy proces roboczy elementu Runbook](../automation/automation-hybrid-runbook-worker.md ) zainstalowane.  |




## <a name="next-steps"></a>Następne kroki
* Zainstaluj hello [rozwiązania zarządzania alertami](log-analytics-solution-alert-management.md) alerty tooanalyze utworzone w analizy dzienników oraz alertów zebranych z System Center Operations Manager (SCOM).
* Przeczytaj więcej na temat [dziennika wyszukiwania](log-analytics-log-searches.md) który generowania alertów.
* Zakończenie wskazówki dla [Konfigurowanie webook](log-analytics-alerts-webhooks.md) z reguły alertu.  
* Dowiedz się, jak toowrite [elementy runbook automatyzacji Azure](https://azure.microsoft.com/documentation/services/automation) problemów tooremediate identyfikowana na podstawie alertów.

