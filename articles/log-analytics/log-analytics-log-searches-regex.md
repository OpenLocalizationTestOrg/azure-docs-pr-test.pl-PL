---
title: "wyrażenia aaaRegular w analizy dzienników OMS dziennika wyszukiwania | Dokumentacja firmy Microsoft"
description: "W analizy dzienników dziennik wyszukiwania toohello hello wyników filtrowania zgodnie z wyrażeniem regularnym tooa służy — słowo kluczowe hello wyrażenia regularnego.  Ten artykuł zawiera składnię hello tych wyrażeń z kilka przykładów."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Za pomocą wyrażeń regularnych toofilter przeszukuje dziennika analizy dzienników

[Zaloguj się wyszukiwanie](log-analytics-log-searches.md) pozwalają tooextract informacji z repozytorium analizy dzienników hello.  [Wyrażenia filtru](log-analytics-search-reference.md#filter-expressions) pozwalają toofilter hello wyniki wyszukiwania hello zgodnie z kryteriami toospecific.  Witaj **RegEx** — słowo kluczowe umożliwia toospecify wyrażenia regularnego dla tego filtru.  

Ten artykuł zawiera szczegółowe informacje o składni wyrażeń regularnych hello używane przez analizy dzienników.

> [!NOTE]
> Wyrażenia regularnego można używać tylko z pól z możliwością wyszukiwania.  Aby uzyskać więcej informacji dotyczących pól z możliwością wyszukiwania, zobacz **typy pól** w [wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>RegEx — słowo kluczowe

Witaj użyj następującej składni toouse hello **RegEx** — słowo kluczowe w polu wyszukiwania dziennika.  Można użyć hello pozostałe sekcje w tym artykule toodetermine hello składni wyrażeń regularnych hello samej siebie.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Na przykład rejestruje toouse alert tooreturn wyrażenia regularnego z typem *ostrzeżenie* lub *błąd*, należy użyć powitania po wyszukiwania dziennika.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Wyniki pasujące częściowo
Należy pamiętać, że wyrażenie regularne hello musi odpowiadać hello cały tekst hello właściwości.  Wyniki pasujące częściowo nie zwróci żadnych rekordów.  Na przykład, jeśli chcesz tooreturn rekordy z komputera o nazwie srv01.contoso.com, czy powitania po wyszukiwania dziennika **nie** zwraca żadnych rekordów.

    Computer=RegEx("srv..")

Jest to spowodowane tylko hello pierwsza część hello nazwy odpowiada wyrażeniu regularnemu hello.  Hello następujące dwa dziennik wyszukiwania zwróci rekordy z tego komputera, ponieważ są zgodne hello całą nazwę.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Znaki
Określ inną znaków.

| Znak | Opis | Przykład | Przykładowe dopasowań |
|:--|:--|:--|:--|
| A | Jedno wystąpienie hello znaku. | Computer=RegEx("SRV01.contoso.com") | SRV01.contoso.com |
| . | Dowolny pojedynczy znak. | Computer=RegEx("SRV...contoso.com") | SRV01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| ? | Zero lub jeden wystąpienie hello znaków. | Komputer = wyrażenie regularne ("Srw01?. "contoso.com") | srv0.contoso.com<br>SRV01.contoso.com |
| * | Zero lub więcej wystąpień hello znaków. | Computer=RegEx("SRV01*.contoso.com") | srv0.contoso.com<br>SRV01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| + | Jedno lub więcej wystąpień hello znaków. | Computer=RegEx("SRV01+.contoso.com") | SRV01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Dopasowuje dowolny pojedynczy znak w nawiasach hello | Computer=RegEx("srv0[123].contoso.com") | SRV01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [**-*z*] | Zgodny z pojedynczym znakiem w zakresie hello.  Może zawierać wiele zakresów. | Computer=RegEx("srv0[1-3].contoso.com") | SRV01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Brak znaków hello w nawiasach hello | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [^**-*z*] | Brak znaków hello hello zakresu. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Zgodne zakres znaków liczbowych. | Computer=RegEx("SRV[01-03].contoso.com") | SRV01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| @ | Dowolny ciąg znaków. | Komputer = wyrażenie regularne ("srv@.contoso.com") | SRV01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Wiele wystąpień znaku
Określ wiele wystąpień określonych znaków.

| Znak | Opis | Przykład | Przykładowe dopasowań |
|:--|:--|:--|:--|
| {n} |  *n*wystąpienia hello znaków. | Computer=RegEx("bW-win-sc01{3}.bwren.Lab") | bW Windows sc0111.bwren.lab |
| {n} |  *n*lub więcej wystąpień hello znaku. | Computer=RegEx("bW-win-sc01{3,}.bwren.Lab") | bW Windows sc0111.bwren.lab<br>bW Windows sc01111.bwren.lab<br>bW Windows sc011111.bwren.lab<br>bW Windows sc0111111.bwren.lab |
| {n, m} |  *n*zbyt*m* wystąpień hello znaku. | Computer=RegEx("bW-win-sc01{3,5}.bwren.Lab") | bW Windows sc0111.bwren.lab<br>bW Windows sc01111.bwren.lab<br>bW Windows sc011111.bwren.lab |


## <a name="logical-expressions"></a>Wyrażenia logiczne
Wybierz z wieloma wartościami.

| Znak | Opis | Przykład | Przykładowe dopasowań |
|:--|:--|:--|:--|
| &#124; | Operatora logicznego OR.  Zwraca wynik, jeśli odpowiada na jedno z tych wyrażeń. | Typ alertu AlertSeverity = = wyrażenie regularne ("ostrzeżenie &#124; Błąd") | Ostrzeżenie<br>Błąd |
| & | Operatora logicznego AND.  Zwraca wynik, jeśli odpowiada na oba wyrażenia | EventData = wyrażenie regularne ("(zabezpieczeń.\* &. \*Powodzenie. \*)") | Inspekcji pomyślnego zabezpieczeń |


## <a name="literals"></a>Literały
Konwersja znaków tooliteral znaki specjalne.  Dotyczy to również znaki, które są dostępne funkcje takie jak wyrażenia tooregular?-\*^\[\]{}\(\)+\|. &.

| Znak | Opis | Przykład | Przykładowe dopasowań |
|:--|:--|:--|:--|
| \\ | Konwertuje znaki specjalne tooa literału. | Status_CF =\\[błąd\\] @<br>Status_CF = błąd\\-@ | [Błąd] Nie można odnaleźć pliku.<br>Nie można odnaleźć pliku błędu. |


## <a name="next-steps"></a>Następne kroki

* Zapoznaj się z [dziennika wyszukiwania](log-analytics-log-searches.md) tooview i analizowanie danych hello analizy dzienników repozytorium.
