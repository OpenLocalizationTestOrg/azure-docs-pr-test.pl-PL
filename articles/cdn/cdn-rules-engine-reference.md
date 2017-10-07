---
title: "Odwołanie do aparatu reguł aaaAzure CDN | Dokumentacja firmy Microsoft"
description: "Dokumentacja referencyjna dla usługi Azure CDN zasady warunków dopasowania aparatu i funkcje."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Aparat reguł usługi Azure CDN
Ten temat zawiera szczegółowe opisy hello dostępne dopasowanie warunków oraz funkcje dla Azure Content Delivery Network (CDN) [aparatu reguł](cdn-rules-engine.md).

Hello aparatu reguł HTTP jest źródłem końcowego hello toobe zaprojektowana dla określonych typów żądań przetwarzanych przez hello CDN.

**Najczęstsze zastosowania**:

- Zastąpienie lub zdefiniowania zasad niestandardowych pamięci podręcznej.
- Zabezpieczanie lub odrzucanie żądań dla poufnej zawartości.
- Przekieruj żądania.
- Przechowywanie danych dziennika niestandardowego.

## <a name="terminology"></a>Terminologia
Reguła jest definiowana za pomocą hello [ **wyrażenia warunkowe**](cdn-rules-engine-reference-conditional-expressions.md), [ **odpowiada**](cdn-rules-engine-reference-match-conditions.md), i [  **Funkcje**](cdn-rules-engine-reference-features.md). Te elementy zostały wyróżnione na następującej ilustracji hello.

 ![Warunek dopasowania CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Składnia

Hello sposób, w którym będzie traktowany znaki specjalne zmienia się zgodnie z toohow warunek dopasowania lub wartości tekstowe uchwytów funkcji. Dopasowanie warunku lub funkcji mogą interpretować tekst w jednym z hello następujące sposoby:

1. [**Wartości literałów**](#literal-values) 
2. [**Wartości symboli wieloznacznych**](#wildcard-values)
3. [**Wyrażenia regularne**](#regular-expressions)

### <a name="literal-values"></a>Wartości literałów
Tekst, który jest interpretowana jako wartość literału traktują wszystkich znaków specjalnych, z wyjątkiem hello hello % symbolu, w ramach hello wartości, które muszą być zgodne. Innymi słowy, literałem odpowiada za zestaw warunków`\'*'\` tylko będą spełnione, podczas którego dokładnie wartość (np. `\'*'\`) został znaleziony.
 
Symbol procentu jest adresem URL tooindicate używane kodowanie (np. `%20`).

### <a name="wildcard-values"></a>Wartości symboli wieloznacznych
Tekst, który jest interpretowany jako wartość symbolu wieloznacznego przypisze dodatkowych znaczeń toospecial znaków. Witaj w poniższej tabeli opisano interpretacji hello następującego zestawu znaków.

Znak | Opis
----------|------------
\ | Ukośnik odwrotny jest używane tooescape hello znaków określonych w tej tabeli. Należy określić ukośnik odwrotny bezpośrednio przed hello znak specjalny, który powinien być zmienione znaczenie.<br/>Na przykład składni hello specjalne gwiazdkę:`\*`
% | Symbol procentu jest adresem URL tooindicate używane kodowanie (np. `%20`).
* | Znak gwiazdki jest symbol wieloznaczny, który reprezentuje co najmniej jeden znak.
Miejsca | Znak odstępu wskazuje, czy warunek dopasowania muszą zostać spełnione w jednej z określonych hello wartości lub wzorce.
"wartość" | Pojedynczy cudzysłów nie ma specjalnego znaczenia. Jednak jest używany zestaw apostrofy tooindicate, którego wartość powinna być traktowane jako wartość literału. Można w hello następujące sposoby:<br><br/>— Umożliwia toobe warunku dopasowania spełnione przy każdym hello określona wartość dopasowań jakiejkolwiek jego części hello porównania wartości.  Na przykład `'ma'` będzie zgodna z żadną hello następujące parametry: <br/><br/>/Business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/ firm/szablonu. **ma**p<br /><br />— Umożliwia toobe znak specjalny, określony jako literał znaków. Na przykład można określić znak spacji literału umieszczając znak odstępu, w ramach zestawu pojedynczych cudzysłowów (tj. `' '` lub `'sample value'`).<br/>— Umożliwia toobe pustą wartość, określony. Określ wartość pusta, określając zestaw pojedynczych cudzysłowów (np. ").<br /><br/>**Ważne:**<br/>— Jeśli hello określona wartość nie zawiera symboli wieloznacznych, następnie jest automatycznie uważane za wartość literału. Oznacza to, że nie jest konieczne toospecify zestaw apostrofy.<br/>— Jeśli ukośnik odwrotny ucieczki nie innego znaku w tej tabeli, następnie go zostaną zignorowane, kiedy określony w ramach zestawu apostrofy.<br/>-Inny sposób toospecify znaków specjalnych w postaci literału znaku jest tooescape za pomocą ukośnika odwrotnego (np. `\`).

### <a name="regular-expressions"></a>Wyrażenia regularne

Wyrażenia regularne Zdefiniuj wzorzec, który ma zostać wyszukany w wartości tekstowej. Notacja wyrażeń regularnych definiuje określone znaczenie tooa wielu symboli. Witaj poniższej tabeli przedstawiono sposób specjalne znaki są traktowane przez dopasowanie warunków i funkcje, które obsługują wyrażeń regularnych.

Znaki specjalne | Opis
------------------|------------
\ | Witaj znaku ukośnika odwrotnego specjalne hello następującym. Powoduje to, że ten toobe znak traktowane jako wartość literału zamiast przyjmowania na jego znaczenie wyrażenia regularnego. Na przykład składni hello specjalne gwiazdkę:`\*`
% | znaczenie Hello symbol procentu zależy od jego użycia.<br/><br/> `%{HTTPVariable}`: Ta składnia identyfikuje Zmienna HTTP.<br/>`%{HTTPVariable%Pattern}`: Ta składnia używa tooidentify symbol procentu HTTP, zmiennych i jako ogranicznik.<br />`\%`: Anulowanie symbol procentu pozwala toobe używany jako wartość literału lub tooindicate podczas kodowania adresu URL (np. `\%20`).
* | Znak gwiazdki umożliwia hello poprzedzających toobe znak dopasowane zero lub więcej razy. 
Miejsca | Znak odstępu zwykle jest traktowana jako literał znaków. 
"wartość" | Apostrofy są traktowane jako literały. Zestaw apostrofy nie ma specjalnego znaczenia.


## <a name="next-steps"></a>Następne kroki
* [Warunki uzgadniania aparatu reguł](cdn-rules-engine-reference-match-conditions.md)
* [Wyrażenia warunkowe aparatu reguł](cdn-rules-engine-reference-conditional-expressions.md)
* [Funkcje aparatu reguł](cdn-rules-engine-reference-features.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)
* [Omówienie usługi Azure CDN](cdn-overview.md)
