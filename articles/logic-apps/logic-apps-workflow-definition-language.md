---
title: "aaaWorkflow języka definicji schematu - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Definiuje przepływy pracy na podstawie hello przepływu pracy definicji schematu dla usługi Azure Logic Apps"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Schemat języka definicji przepływu pracy dla usługi Azure Logic Apps

Definicji przepływu pracy zawiera logikę rzeczywiste hello, która jest wykonywana w ramach aplikacji logiki. Ta definicja zawiera jeden lub więcej wyzwalaczy, które uruchamiają aplikację logiki hello i co najmniej jednej akcji dla tootake aplikacji logiki hello.  
  
## <a name="basic-workflow-definition-structure"></a>Struktura definicji podstawowy przepływ pracy

Oto hello podstawowa struktura definicji przepływu pracy:  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Witaj [interfejsu API REST zarządzania przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows) dokumentacja zawiera informacje na temat toocreate i Zarządzaj przepływami pracy aplikacji logiki.
  
|Nazwa elementu|Wymagane|Opis|  
|------------------|--------------|-----------------|  
|$schema|Nie|Określa lokalizację hello hello pliku schematu JSON, który opisuje hello wersji języka definicji hello. Tej lokalizacji jest wymagany, gdy odwołanie definicję zewnętrznie. Dla tego dokumentu lokalizacja hello jest: <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|Nie|Określa wersję definicji hello. Podczas wdrażania przy użyciu hello definicji przepływu pracy, można użyć tej wartości toomake się, że definicja prawo hello jest używany.|  
|parameters|Nie|Określa, że parametry używane tooinput danych do definicji hello. Można określić maksymalnie 50 parametrów.|  
|Wyzwalacze|Nie|Określa informacje hello wyzwalaczy, które inicjują hello przepływu pracy. Można określić maksymalnie 10 wyzwalaczy.|  
|Akcje|Nie|Określa akcje, które są przyjmowane, gdy przepływ hello jest wykonywana. Można zdefiniować maksymalnie 250 akcji.|  
|dane wyjściowe|Nie|Określa informacje o zasobie hello wdrożone. Można określić maksymalnie 10 danych wyjściowych.|  
  
## <a name="parameters"></a>Parametry

W tej sekcji określa wszystkie parametry hello, które są używane w definicji przepływu pracy hello w czasie wdrażania. Wszystkie parametry musi zostać zadeklarowany w tej sekcji, przed ich użyciem w innych częściach hello definicji.  
  
Witaj poniższy przykład przedstawia hello struktura definicji parametru:  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Nazwa elementu|Wymagane|Opis|  
|------------------|--------------|-----------------|  
|type|Tak|**Typ**: ciąg <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "string"}` <p> **Specyfikacja**:`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Typ**: securestring <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "securestring"}}` <p> **Specyfikacja**:`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Typ**: int <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "int"}}` <p> **Specyfikacja**:`"parameters": {"parameter1": {"value" : 5}}` <p> **Typ**: wartość logiczna <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "bool"}}` <p> **Specyfikacja**:`"parameters": {"parameter1": { "value": true }}` <p> **Typ**: tablicy <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "array"}}` <p> **Specyfikacja**:`"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Typ**: obiekt <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "object"}}` <p> **Specyfikacja**:`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Typ**: secureobject <p> **Deklaracja**:`"parameters": {"parameter1": {"type": "object"}}` <p> **Specyfikacja**:`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Uwaga:** hello `securestring` i `secureobject` typy nie są zwracane w `GET` operacji. Haseł, kluczy i kluczy tajnych należy użyć tego typu.|  
|Wartość domyślna|Nie|Określa hello wartości domyślnej dla parametru hello, gdy nie określono wartości w czasie hello hello zasób został utworzony.|  
|allowedValues|Nie|Określa tablicę dozwolonych wartości dla parametru hello.|  
|Metadane|Nie|Określa dodatkowe informacje dotyczące parametru hello, na przykład czytelny opis lub danych czasu projektowania używana przez Visual Studio lub innych narzędzi.|  
  
Ten przykład przedstawia, jak można użyć parametru części treści hello akcji:  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 Można również użyć parametrów w danych wyjściowych.  
  
## <a name="triggers-and-actions"></a>Wyzwalacze i akcje  

Wyzwalacze i akcje Określ hello wywołania, które mogą zostać użyte podczas wykonywania przepływu pracy. Aby uzyskać szczegółowe informacje o tej sekcji, zobacz [działania przepływu pracy i wyzwalaczy](logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>dane wyjściowe  

Dane wyjściowe określ informacje, które mogą być zwracane z przepływu pracy Uruchom. Na przykład jeśli masz określonego stanu lub wartość ma tootrack przy każdym uruchomieniu, można uwzględnić czy dane w hello Uruchom danych wyjściowych. dane Hello pojawia się w hello interfejsu API REST zarządzania dla tego przebiegu i zarządzania hello interfejsu użytkownika dla tego uruchomienia w hello portalu Azure. Te dane wyjściowe tooother systemami zewnętrznymi takich jak usługi Power BI może również przepływać do tworzenia pulpitów nawigacyjnych. Dane wyjściowe są *nie* używane toorespond tooincoming żądań na powitania interfejsu API REST usługi. żądanie przychodzące tooan toorespond przy użyciu hello `response` typ akcji, Oto przykład:
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Nazwa elementu|Wymagane|Opis|  
|------------------|--------------|-----------------|  
|klucz1|Tak|Określa identyfikator klucza hello hello danych wyjściowych. Zastąp **klucz1** o nazwie, które mają toouse tooidentify hello w danych wyjściowych.|  
|wartość|Tak|Określa wartość hello hello danych wyjściowych.|  
|type|Tak|Określa typ hello hello wartość, która została określona. Typy możliwe wartości to: <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>Wyrażenia  

Wartości JSON w definicji hello mogą być literał lub można je wyrażeń, które są oceniane po definicji hello jest używany. Na przykład:  
  
```json
"name": "value"
```

 lub  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Niektóre wyrażenia pobrać wartości z akcji środowiska uruchomieniowego, które może nie istnieć na początku hello hello wykonywania. Można użyć **funkcje** toohelp pobrać niektóre z tych wartości.  
  
Wyrażenia mogą występować w dowolnym miejscu w wartości ciągu JSON i zawsze powoduje inną wartość JSON. Gdy wartość JSON toobe określone wyrażenie, treść wyrażenia hello hello jest wyodrębniany przez usunięcie znaku hello (@). Jeśli wymagane jest literałem, która rozpoczyna się od @, że ciąg musi być wpisywany z użyciem@. Witaj poniższych przykładach pokazano, jak są analizowane wyrażenia.  
  
|Wartość JSON|wynik|  
|----------------|------------|  
|"Parametry"|Witaj znaków "parameters" są zwracane.|  
|"parametry [1]"|zwracane są Hello znaków "parametry [1]".|  
|"@@"|Ciąg 1 znaku, który zawiera "@" jest zwracany.|  
|" @"|Ciąg znaków 2, który zawiera "@" jest zwracany.|  
  
Z *ciągu interpolacji*, wyrażenia może również zostać wyświetlony wewnątrz ciągów, których wyrażenia są ujęte w `@{ ... }`. Na przykład: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

wynik Hello jest zawsze ciąg, co sprawia, że ta funkcja toohello podobne `concat` funkcji. Załóżmy, że określono `myNumber` jako `42` i `myString` jako `sampleString`:  
  
|Wartość JSON|wynik|  
|----------------|------------|  
|"@parameters(mójCiąg)"|Zwraca `sampleString` jako ciąg.|  
|"@{parameters('myString')}"|Zwraca `sampleString` jako ciąg.|  
|"@parameters(myNumber)"|Zwraca `42` jako *numer*.|  
|"@{parameters('myNumber')}"|Zwraca `42` jako *ciąg*.|  
|"Odpowiedź brzmi: @{parameters('myNumber')}"|Zwraca hello ciąg `Answer is: 42`.|  
|"@concat(" Odpowiedź brzmi: ", string(parameters('myNumber')))"|Zwraca ciąg hello`Answer is: 42`|  
|"Odpowiedź brzmi: @@ {parameters('myNumber')}"|Zwraca hello ciąg `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>Operatory  

Operatory są hello znaki, których można używać wewnątrz wyrażenia lub funkcji. 
  
|Operator|Opis|  
|--------------|-----------------|  
|.|operator kropki Hello umożliwia tooreference właściwości obiektu|  
|?|operator zapytania Hello umożliwia odwołanie właściwości obiektu bez błędów czasu wykonywania o wartości null. Na przykład można użyć tego wyrażenia toohandle null wyzwolenia dane wyjściowe: <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|Witaj pojedynczego cudzysłowu jest hello tylko sposób toowrap literałów ciągów znaków. Nie można użyć podwójnych cudzysłowów wewnątrz wyrażenia, ponieważ ta znaki interpunkcyjne powoduje konflikt z hello JSON oferty, która opakowuje hello całego wyrażenia.|  
|[]|nawiasy kwadratowe Hello mogą być używane tooget wartość z zakresu od tablicy o określonym indeksie. Na przykład, jeśli akcja, która przekazuje `range(0,10)`w toohello `forEach` funkcji, można używać tej funkcji tooget elementów limit tablic:  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Funkcje  

Można także wywoływać funkcje w wyrażeniach. Witaj poniższej tabeli przedstawiono funkcje hello, których można użyć w wyrażeniu.  
  
|wyrażenie|Ocena|  
|----------------|----------------|  
|"@function("Witaj")"|Wywołania hello funkcja członkowska hello definicji z literałem hello Hello jako hello pierwszego parametru.|  
|"@function("Jest chłodnych!")"|Wywołuje hello funkcja członkowska hello definicji z literałem hello "jest chłodnej!" jako pierwszego parametru hello|  
|"@function.prop1 ()"|Wartość właściwości prop1 hello hello hello zwraca `myfunction` członkiem hello definicji.|  
|"@function.Prop1 ("Witaj")"|Wywołania hello funkcja członkowska hello definicji z literałem powitania "Hello" jako hello pierwszy parametr i zwraca hello prop1 właściwość hello obiektu.|  
|"@function(parameters('Hello'))"|Wartość parametru Hello hello i przekazuje hello wartość toofunction|  
  
### <a name="referencing-functions"></a>Odwołanie do funkcji  

Możesz użyć tych danych wyjściowych tooreference funkcji z innych działań w aplikacji logiki hello lub wartości przekazane podczas tworzenia aplikacji logiki hello. Na przykład możesz odwoływać się do danych hello w jednym kroku toouse go w innym.  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|parameters|Zwraca wartość parametru, który jest zdefiniowany w definicji hello. <p>`parameters('password')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: parametr <p> **Opis elementu**: wymagane. Nazwa Hello hello parametru wartości, których chcesz.|  
|Akcja|Umożliwia tooderive wyrażenie jego wartość z inną nazwę w formacie JSON i pary wartości lub dane wyjściowe hello hello bieżącego czasu wykonywania akcji. Właściwość Hello reprezentowany przez propertyPath w hello poniższy przykład jest opcjonalna. Jeśli nie określono propertyPath, odwołanie hello jest toohello akcji całego obiektu. Tej funkcji można używać tylko wewnątrz czy — do warunków akcji. <p>`action().outputs.body.propertyPath`|  
|Akcje|Umożliwia tooderive wyrażenie jego wartość z inną nazwę w formacie JSON i pary wartości lub dane wyjściowe hello hello czasu wykonywania akcji. Wyrażenia te jawnie deklarować, że jedno działanie zależy od innej akcji. Właściwość Hello reprezentowany przez propertyPath w hello poniższy przykład jest opcjonalna. Jeśli nie określono propertyPath, odwołanie hello jest toohello akcji całego obiektu. Można użyć albo tego elementu lub hello warunki zależności toospecify elementu, ale nie ma potrzeby toouse zarówno dla hello tego samego zasobu zależnego. <p>`actions('myAction').outputs.body.propertyPath` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Nazwa akcji <p> **Opis elementu**: wymagane. Nazwa Hello akcji hello wartości, których chcesz. <p> Dostępne właściwości w obiekcie akcji hello są: <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Zobacz hello [interfejsu API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850646) szczegółowe informacje na temat tych właściwości.|
|Wyzwalacz|Umożliwia tooderive wyrażenie jego wartość z inną nazwę w formacie JSON i pary wartości lub dane wyjściowe hello hello czasu wykonywania wyzwalacza. Właściwość Hello reprezentowany przez propertyPath w hello poniższy przykład jest opcjonalna. Jeśli nie określono propertyPath, odwołanie hello jest toohello wyzwalacza całego obiektu. <p>`trigger().outputs.body.propertyPath` <p>Funkcja hello wewnątrz tego wyzwalacza danych wejściowych zwraca elementy wyjściowe hello hello poprzednie wykonanie. Jednak gdy jest używany wewnątrz spełnienie warunku wyzwalacza, hello `trigger` funkcja zwraca dane wyjściowe hello hello bieżącego wykonywania. <p> Dostępne właściwości w obiekcie wyzwalacza hello są: <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Zobacz hello [interfejsu API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850644) szczegółowe informacje na temat tych właściwości.|
|actionOutputs|Ta funkcja jest skrócona forma funkcji`actions('actionName').outputs` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Nazwa akcji <p> **Opis elementu**: wymagane. Nazwa Hello akcji hello wartości, których chcesz.|  
|actionBody i treści|Te funkcje są skrócona forma funkcji`actions('actionName').outputs.body` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Nazwa akcji <p> **Opis elementu**: wymagane. Nazwa Hello akcji hello wartości, których chcesz.|  
|triggerOutputs|Ta funkcja jest skrócona forma funkcji`trigger().outputs`|  
|triggerBody|Ta funkcja jest skrócona forma funkcji`trigger().outputs.body`|  
|Element|Użyta wewnątrz powtarzających się akcja, funkcja zwraca hello element w tablicy powitania dla tej iteracji hello akcji. Na przykład jeśli akcja, która jest uruchamiana dla każdego elementu tablicy wiadomości, należy użyć następującej składni: <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Kolekcja funkcji  

Funkcje te działają na kolekcje i zazwyczaj stosowane tooArrays, ciągi i czasami słowników.  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|zawiera|Zwraca wartość PRAWDA, jeśli słownik zawiera listę kluczy, zawiera wartość lub ciąg zawiera podciąg. Na przykład, funkcja zwraca `true`: <p>`contains('abacaba','aca')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: W kolekcji <p> **Opis elementu**: wymagane. Witaj toosearch kolekcji w ciągu. <p> **Liczba parametrów**: 2 <p> **Nazwa**: obiekt Find <p> **Opis elementu**: wymagane. Witaj toofind obiektu wewnątrz hello **w kolekcji**.|  
|długość|Zwraca hello liczba elementów w tablicy lub ciągu. Na przykład, funkcja zwraca `3`:  <p>`length('abc')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji <p> **Opis elementu**: wymagane. Kolekcja powitania dla o długości hello tooget.|  
|pusty|Zwraca wartość PRAWDA, jeśli obiekt, tablicy lub ciągu jest pusty. Na przykład, funkcja zwraca `true`: <p>`empty('')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji <p> **Opis elementu**: wymagane. Witaj toocheck kolekcji, jeśli jest pusty.|  
|część wspólną|Zwraca pojedynczą tablicę lub obiekt, który zawiera wspólne elementy między tablicami lub obiektów przekazany. Na przykład, funkcja zwraca `[1, 2]`: <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>Witaj parametrów funkcji hello może być zestaw obiektów lub zestaw tablic (nie kombinację obu). Jeśli występują dwa obiekty o hello takie same nazwy, hello ostatni obiekt o tej nazwie zostanie wyświetlony w obiekcie końcowego hello. <p> **Liczba parametrów**: 1...*n* <p> **Nazwa**: kolekcji*n* <p> **Opis elementu**: wymagane. Witaj tooevaluate kolekcji. Obiekt musi być we wszystkich zbiorach przekazano tooappear w wyniku hello.|  
|Unii|Zwraca pojedynczą tablicę lub obiektu z wszystkich elementów hello przekazywane w tablicy lub obiektu toothis funkcji. Na przykład, funkcja zwraca `[1, 2, 3, 10, 101]`: <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>Witaj parametrów funkcji hello może być zestaw obiektów lub zestaw tablic (nie kombinacja jego). Jeśli występują dwa obiekty o hello takie same nazwy w hello ostateczne dane wyjściowe, hello ostatni obiekt o tej nazwie pojawi się w obiekcie końcowego hello. <p> **Liczba parametrów**: 1...*n* <p> **Nazwa**: kolekcji*n* <p> **Opis elementu**: wymagane. Witaj tooevaluate kolekcji. Obiekt, który pojawia się w dowolnej kolekcji hello pojawia się również w wyniku hello.|  
|pierwszy|Zwraca hello pierwszego elementu w tablicy hello lub przekazany ciąg. Na przykład, funkcja zwraca `0`: <p>`first([0,2,3])` <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji <p> **Opis elementu**: wymagane. Witaj tootake hello pierwszy obiekt kolekcji z.|  
|ostatni|Zwraca hello ostatniego elementu w tablicy hello lub przekazany ciąg. Na przykład, funkcja zwraca `3`: <p>`last('0123')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji <p> **Opis elementu**: wymagane. Witaj tootake hello ostatni obiekt kolekcji z.|  
|podejmij|Zwraca pierwsze hello **liczba** przekazano elementów z hello tablicy lub ciągu. Na przykład, funkcja zwraca `[1, 2]`:  <p>`take([1, 2, 3, 4], 2)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji <p> **Opis elementu**: wymagane. Hello kolekcji, z którym tootake hello najpierw **liczba** obiektów. <p> **Liczba parametrów**: 2 <p> **Nazwa**: liczba <p> **Opis elementu**: wymagane. Liczba obiektów tootake z hello Hello **kolekcji**. Musi być dodatnią liczbą całkowitą.|  
|Pomiń|Zwraca hello elementów w tablicy hello, zaczynając od indeksu **liczba**. Na przykład, funkcja zwraca `[3, 4]`: <p>`skip([1, 2 ,3 ,4], 2)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji <p> **Opis elementu**: wymagane. najpierw Hello hello tooskip kolekcji **liczba** obiektów z. <p> **Liczba parametrów**: 2 <p> **Nazwa**: liczba <p> **Opis elementu**: wymagane. Liczba obiektów tooremove z przodu hello Hello **kolekcji**. Musi być dodatnią liczbą całkowitą.|  
|join|Zwraca ciąg z każdym elementem tablicy przyłączone ogranicznikiem, na przykład zwraca `"1,2,3,4"`:<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: kolekcji<br /><br /> **Opis elementu**: wymagane. elementy toojoin kolekcji Hello z.<br /><br /> **Liczba parametrów**: 2<br /><br /> **Nazwa**: ogranicznika<br /><br /> **Opis elementu**: wymagane. ciąg Hello toodelimit elementy z.|  
  
### <a name="string-functions"></a>Funkcje ciągów

następujące funkcje tylko Hello zastosować toostrings. Umożliwia także niektóre funkcje kolekcji ciągów.  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|concat|Łączy ze sobą dowolną liczbę ciągów. Na przykład, jeśli parametr 1 jest `p1`, funkcja zwraca `somevalue-p1-somevalue`: <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Liczba parametrów**: 1...*n* <p> **Nazwa**: ciąg*n* <p> **Opis elementu**: wymagane. Witaj toocombine ciągi w jeden ciąg.|  
|substring|Zwraca podzbiór znaków z ciągu. Na przykład, funkcja zwraca `abc`: <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello, z których hello jest pobierany podciąg. <p> **Liczba parametrów**: 2 <p> **Nazwa**: indeks początkowy <p> **Opis elementu**: wymagane. Indeks Hello gdzie podciąg hello rozpoczyna się w parametrze 1. <p> **Liczba parametrów**: 3 <p> **Nazwa**: długość <p> **Opis elementu**: wymagane. Długość Hello hello podciąg.|  
|Zamień|Zamienia ciąg dany ciąg znaków. Na przykład, funkcja zwraca `hello new string`: <p>`replace('hello old string', 'old', 'new')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello, który jest przeszukiwany parametru 2 i aktualizowane z parametrem 3, gdy parametr 2 znajduje się w parametrze 1. <p> **Liczba parametrów**: 2 <p> **Nazwa**: stary ciąg <p> **Opis elementu**: wymagane. tooreplace ciąg Hello z parametrem 3, w przypadku odnalezienia pasującego w parametrze 1 <p> **Liczba parametrów**: 3 <p> **Nazwa**: nowe parametry <p> **Opis elementu**: wymagane. Witaj ciąg znaków ciąg hello tooreplace używanych w parametrze 2 po znalezieniu dopasowania w parametrze 1.|  
|Identyfikator GUID|Ta funkcja generuje ciąg globalnie unikatowy (identyfikator globalny GUID). Na przykład ta funkcja może wygenerować tego identyfikatora GUID:`c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Specyfikator formatu jednej, która wskazuje [jak tooformat hello wartość tego identyfikatora Guid](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). Parametr formatu Hello może być "N", "D", "B", "P" lub "X". Jeśli format nie jest podany, "D" jest używany.|  
|toLower|Konwertuje toolowercase ciągu. Na przykład, funkcja zwraca `two by two is four`: <p>`toLower('Two by Two is Four')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj ciąg tooconvert toolower wielkości liter. Jeśli znak w ciągu hello nie ma odpowiednika małe litery, znak hello jest dołączony niezmieniona na powitania zwrócony ciąg.|  
|toUpper|Konwertuje toouppercase ciągu. Na przykład, funkcja zwraca `TWO BY TWO IS FOUR`: <p>`toUpper('Two by Two is Four')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj ciąg tooconvert tooupper wielkości liter. Jeśli znak w ciągu hello nie ma odpowiednika wielkie litery, znak hello jest dołączony niezmieniona na powitania zwrócony ciąg.|  
|indexOf|Znajdź insensitively hello indeks wartości w przypadku ciągu. Na przykład, funkcja zwraca `7`: <p>`indexof('hello, world.', 'world')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello, który może zawierać wartości hello. <p> **Liczba parametrów**: 2 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj wartość toosearch hello indeks.|  
|lastIndexOf|Znajdź insensitively hello ostatniego indeks wartości w przypadku ciągu. Na przykład, funkcja zwraca `3`: <p>`lastindexof('foofoo', 'foo')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello, który może zawierać wartości hello. <p> **Liczba parametrów**: 2 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj wartość toosearch hello indeks.|  
|StartsWith|Sprawdza, czy ciąg hello rozpoczyna się od liter wartość insensitively. Na przykład, funkcja zwraca `true`: <p>`startswith('hello, world', 'hello')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello, który może zawierać wartości hello. <p> **Liczba parametrów**: 2 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg hello wartość Hello może rozpoczynać się od.|  
|EndsWith|Sprawdza, czy ciąg hello kończy się wyrazem przypadku wartość insensitively. Na przykład, funkcja zwraca `true`: <p>`endswith('hello, world', 'world')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello, który może zawierać wartości hello. <p> **Liczba parametrów**: 2 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg hello wartości Hello mogą kończyć się.|  
|split|Dzieli ciąg hello za pomocą separatora. Na przykład, funkcja zwraca `["a", "b", "c"]`: <p>`split('a;b;c',';')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg Hello podzielonej. <p> **Liczba parametrów**: 2 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Hello separator.|  
  
### <a name="logical-functions"></a>Funkcje logiczne  

Funkcje te są przydatne w warunkach i mogą być używane tooevaluate każdy rodzaj logiki.  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|równa się|Zwraca wartość PRAWDA, jeśli dwie wartości są równe. Na przykład, jeśli parameter1 someValue, funkcja zwraca `true`: <p>`equals(parameters('parameter1'), 'someValue')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: obiekt o 1 <p> **Opis elementu**: wymagane. Witaj toocompare obiektu zbyt**2 obiektu**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: obiekt 2 <p> **Opis elementu**: wymagane. Witaj toocompare obiektu zbyt**1 obiektu**.|  
|mniej|Zwraca wartość PRAWDA, jeśli pierwszy argument hello jest mniejsza niż hello drugi. Uwaga: wartości może być tylko typu integer, float lub ciąg. Na przykład, funkcja zwraca `true`: <p>`less(10,100)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: obiekt o 1 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest mniejszy niż **2 obiektu**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: obiekt 2 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest większy niż **1 obiektu**.|  
|lessOrEquals|Zwraca wartość PRAWDA, jeśli pierwszy argument hello jest mniejsza niż lub równa toohello drugi. Uwaga: wartości może być tylko typu integer, float lub ciąg. Na przykład, funkcja zwraca `true`: <p>`lessOrEquals(10,10)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: obiekt o 1 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest mniejsza lub równa zbyt**2 obiektu**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: obiekt 2 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest większa niż lub równa zbyt**1 obiektu**.|  
|większa|Zwraca wartość PRAWDA, jeśli pierwszy argument hello jest większa niż hello drugi. Uwaga: wartości może być tylko typu integer, float lub ciąg. Na przykład, funkcja zwraca `false`:  <p>`greater(10,10)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: obiekt o 1 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest większy niż **2 obiektu**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: obiekt 2 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest mniejszy niż **1 obiektu**.|  
|greaterOrEquals|Zwraca wartość PRAWDA, jeśli pierwszy argument hello jest większy lub równy toohello drugi. Uwaga: wartości może być tylko typu integer, float lub ciąg. Na przykład, funkcja zwraca `false`: <p>`greaterOrEquals(10,100)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: obiekt o 1 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest większa niż lub równa zbyt**2 obiektu**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: obiekt 2 <p> **Opis elementu**: wymagane. Witaj toocheck obiektu, jeśli jest mniejsza lub równa zbyt**1 obiektu**.|  
|i|Zwraca wartość true, jeśli oba parametry mają wartość true. Oba argumenty muszą toobe wartości logiczne. Na przykład, funkcja zwraca `false`: <p>`and(greater(1,10),equals(0,0))` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość logiczna 1 <p> **Opis elementu**: wymagane. Witaj pierwszego argumentu, który musi być `true`. <p> **Liczba parametrów**: 2 <p> **Nazwa**: wartość logiczna 2 <p> **Opis elementu**: wymagane. drugi argument Hello musi być `true`.|  
|lub|Zwraca wartość true, jeśli parametr ma wartość true. Oba argumenty muszą toobe wartości logiczne. Na przykład, funkcja zwraca `true`: <p>`or(greater(1,10),equals(0,0))` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość logiczna 1 <p> **Opis elementu**: wymagane. Witaj pierwszego argumentu, który może być `true`. <p> **Liczba parametrów**: 2 <p> **Nazwa**: wartość logiczna 2 <p> **Opis elementu**: wymagane. drugi argument Hello może być `true`.|  
|nie|Zwraca wartość PRAWDA, jeśli parametry hello są `false`. Oba argumenty muszą toobe wartości logiczne. Na przykład, funkcja zwraca `true`: <p>`not(contains('200 Success','Fail'))` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość logiczna <p> **Opis elementu**: zwraca wartość true, jeśli parametry hello są `false`. Oba argumenty muszą toobe wartości logiczne. Ta funkcja zwraca `true`:`not(contains('200 Success','Fail'))`|  
|Jeśli|Zwraca określoną wartość, według tego, czy wyrażenie hello spowodowało `true` lub `false`.  Na przykład, funkcja zwraca `"yes"`: <p>`if(equals(1, 1), 'yes', 'no')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wyrażenie <p> **Opis elementu**: wymagane. Wartość logiczna, która określa, które wyrażenie hello wartości powinna zostać zwrócona. <p> **Liczba parametrów**: 2 <p> **Nazwa**: True <p> **Opis elementu**: wymagane. Witaj tooreturn wartość, jeśli wyrażenie hello jest `true`. <p> **Liczba parametrów**: 3 <p> **Nazwa**: False <p> **Opis elementu**: wymagane. Witaj tooreturn wartość, jeśli wyrażenie hello jest `false`.|  
  
### <a name="conversion-functions"></a>Funkcje konwersji  

Funkcje te są używane tooconvert między poszczególnymi hello natywnych typów w języku hello:  
  
- Ciąg  
  
- Liczba całkowita  
  
- Float  
  
- Wartość logiczna  
  
- Tablice  
  
- słowników  

-   Formularze  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|int|Konwertuj hello parametru tooan całkowitą. Na przykład funkcja zwraca 100 jako liczbę zamiast ciągu: <p>`int('100')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość <p> **Opis elementu**: wymagane. wartość Hello przekonwertowanego tooan liczby całkowitej.|  
|Ciąg|Konwertuj ciąg tooa parametru hello. Na przykład, funkcja zwraca `'10'`: <p>`string(10)` <p>Możesz również przekonwertować ciąg tooa obiektu. Na przykład, jeśli hello `myPar` parametr jest obiekt z jedną właściwość `abc : xyz`, a następnie ta funkcja zwraca `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość <p> **Opis elementu**: wymagane. Witaj oznacza to wartość ciągu tooa przekonwertowany.|  
|JSON|Przekonwertować wartość typu JSON hello parametru tooa i jest hello przeciwne z `string()`. Na przykład, funkcja zwraca `[1,2,3]` jako tablica zamiast ciągu: <p>`json('[1,2,3]')` <p>Podobnie można konwertować obiekt tooan ciągu. Na przykład, funkcja zwraca `{ "abc" : "xyz" }`: <p>`json('{"abc" : "xyz"}')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj ciąg znaków wartości typu macierzystego tooa przekonwertowany. <p>Witaj `json()` funkcja obsługuje za dane wejściowe XML. Na przykład hello wartości parametru: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>przekonwertowana toothis JSON jest: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|Float|Konwertuj liczba zmiennoprzecinkowa tooa hello parametr argumentu. Na przykład, funkcja zwraca `10.333`: <p>`float('10.333')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość <p> **Opis elementu**: wymagane. Witaj wartość oznacza to liczba zmiennoprzecinkowa tooa przekonwertowany.|  
|wartość logiczna|Konwertuj hello tooa parametru typu Boolean. Na przykład, funkcja zwraca `false`: <p>`bool(0)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość <p> **Opis elementu**: wymagane. wartość przekonwertowanego tooa Hello boolean.|  
|połączenie|Zwraca pierwszy obiekt zerowy hello w argumentach hello przekazany. **Uwaga**: pusty ciąg nie jest zerowa. Na przykład, jeśli nie zdefiniowano parametrów 1 i 2, funkcja zwraca `fallback`:  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Liczba parametrów**: 1...*n* <p> **Nazwa**: obiekt*n* <p> **Opis elementu**: wymagane. Witaj toocheck obiektów dla wartości null.|  
|Base64|Zwraca hello base64 reprezentację ciągu wejściowego hello. Na przykład, funkcja zwraca `c29tZSBzdHJpbmc=`: <p>`base64('some string')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: String 1 <p> **Opis elementu**: wymagane. tooencode ciąg Hello do reprezentacji base64.|  
|base64ToBinary|Zwraca wartość binarna reprezentacja ciągu w kodowaniu base64. Na przykład, funkcja zwraca hello binarna reprezentacja `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg kodowany w formacie Hello base64.|  
|base64ToString|Zwraca reprezentację ciągu based64 zakodowany ciąg. Na przykład, funkcja zwraca `some string`: <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. ciąg kodowany w formacie Hello base64.|  
|Binarne|Zwraca wartość binarna reprezentacja wartości.  Na przykład, ta funkcja zwraca to binarna reprezentacja `some string`: <p>`binary('some string')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość <p> **Opis elementu**: wymagane. wartość Hello toobinary przekonwertowany.|  
|dataUriToBinary|Zwraca wartość binarna reprezentacja identyfikatora URI danych. Na przykład, funkcja zwraca hello binarna reprezentacja `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. dane Hello reprezentację toobinary tooconvert identyfikatora URI.|  
|dataUriToString|Zwraca reprezentację ciągu identyfikatora URI danych. Na przykład, funkcja zwraca `some string`: <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg<p> **Opis elementu**: wymagane. dane Hello reprezentację tooString tooconvert identyfikatora URI.|  
|dataUri|Zwraca identyfikator URI wartości danych. Na przykład, funkcja zwraca identyfikator URI danych `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`: <p>`dataUri('some string')` <p> **Liczba parametrów**: 1<p> **Nazwa**: wartość<p> **Opis elementu**: wymagane. Witaj wartość tooconvert toodata identyfikatora URI.|  
|decodeBase64|Zwraca reprezentację ciągu wejściowego based64 w ciągu. Na przykład, funkcja zwraca `some string`: <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: zwraca reprezentację ciągu wejściowego based64 w ciągu.|  
|encodeuricomponent —|Ciąg hello specjalne adres URL, który jest przekazywany w. Na przykład, funkcja zwraca `You+Are%3ACool%2FAwesome`: <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj ciąg znaków tooescape niezabezpieczony adres URL z.|  
|decodeuricomponent —|Ciąg hello UN-URL-specjalne, który jest przekazywany w. Na przykład, funkcja zwraca `You Are:Cool/Awesome`: <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj toodecode hello niezabezpieczony adres URL znaków z.|  
|decodeDataUri|Zwraca wartość binarna reprezentacja danych wejściowych w postaci ciągu identyfikatora URI. Na przykład, funkcja zwraca hello binarna reprezentacja `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. Witaj dataURI toodecode do reprezentacja binarna.|  
|uriComponent|Zwraca identyfikator URI zakodowany reprezentację wartości. Na przykład, funkcja zwraca `You+Are%3ACool%2FAwesome`: <p>`uriComponent('You Are:Cool/Awesome')` <p> **Liczba parametrów**: 1<p> **Nazwa**: ciąg <p> **Opis elementu**: wymagane. toobe ciąg Hello zakodowany identyfikator URI.|  
|uriComponentToBinary|Zwraca ciąg kodowany w formacie to binarna reprezentacja identyfikatora URI. Na przykład, ta funkcja zwraca to binarna reprezentacja `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: ciąg<p> **Opis elementu**: wymagane. ciąg kodowany w formacie Hello identyfikatora URI.|  
|uriComponentToString|Zwraca ciąg kodowany w formacie reprezentację ciągu identyfikatora URI. Na przykład, funkcja zwraca `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Liczba parametrów**: 1<p> **Nazwa**: ciąg<p> **Opis elementu**: wymagane. ciąg kodowany w formacie Hello identyfikatora URI.|  
|xml|Zwraca reprezentację XML hello wartość. Na przykład, funkcja zwraca XML zawartości reprezentowany przez `'\<name>Alan\</name>'`: <p>`xml('\<name>Alan\</name>')` <p>Witaj `xml()` funkcja obsługuje obiekt JSON za dane wejściowe. Na przykład Witaj parametru `{ "abc": "xyz" }` jest tooXML przekonwertowanego zawartości:`\<abc>xyz\</abc>` <p> **Liczba parametrów**: 1<p> **Nazwa**: wartość<p> **Opis elementu**: wymagane. Witaj tooXML tooconvert wartość.|  
|wyrażenie XPath|Zwraca tablicę węzłów XML pasujących wyrażenie xpath hello wartości, która daje w wyniku hello wyrażenie xpath. <p> **Przykład 1** <p>Załóżmy hello wartość parametru `p1` jest reprezentację ciągu tego kodu XML: <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Ten kod:`xpath(xml(parameters('p1'), '/lab/robot/name')` <p>Zwraca <p>`[ <name>R1</name>, <name>R2</name> ]` <p>Podczas tego kodu: <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>Zwraca <p>`13` <p> <p> **Przykład 2** <p>Podany hello po zawartość XML: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Ten kod:`@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>lub ten kod: <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>Zwraca <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>I ten kod:`@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>Zwraca <p>``xyz`` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Xml <p> **Opis elementu**: wymagane. Witaj XML, na które tooevaluate hello XPath wyrażenia. <p> **Liczba parametrów**: 2 <p> **Nazwa**: XPath <p> **Opis elementu**: wymagane. Witaj tooevaluate wyrażenie XPath.|  
|Tablica|Konwertuj hello parametru tooan tablicy. Na przykład, funkcja zwraca `["abc"]`: <p>`array('abc')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: wartość <p> **Opis elementu**: wymagane. wartość Hello przekonwertowanego tooan tablicy.|
|createArray|Tworzy tablicę z hello parametrów. Na przykład, funkcja zwraca `["a", "c"]`: <p>`createArray('a', 'c')` <p> **Liczba parametrów**: 1...*n* <p> **Nazwa**: wszystkie*n* <p> **Opis elementu**: wymagane. Witaj toocombine wartości w tablicy.|
|triggerFormDataValue|Zwraca pojedynczą wartość pasujących do nazwy klucza hello z danych formularza lub wyzwalacza postać zakodowanych danych wyjściowych.  Jeśli dostępnych jest wiele dopasowuje je spowoduje błąd.  Na przykład zwróci następujące hello `bar`:`triggerFormDataValue('foo')`<br /><br />**Liczba parametrów**: 1<br /><br />**Nazwa**: Nazwa klucza<br /><br />**Opis elementu**: wymagane. Witaj nazwa klucza hello formularza danych wartości tooreturn.|
|triggerFormDataMultiValues|Zwraca tablicę wartości pasujących do nazwy klucza hello z danych formularza lub wyzwalacza postać zakodowanych danych wyjściowych.  Na przykład zwróci następujące hello `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Liczba parametrów**: 1<br /><br />**Nazwa**: Nazwa klucza<br /><br />**Opis elementu**: wymagane. Nazwa klucza Hello danych formularza hello wartości tooreturn.|
|triggerMultipartBody|Zwraca hello treści stanowi część wieloczęściowych danych wyjściowych hello wyzwalacza.<br /><br />**Liczba parametrów**: 1<br /><br />**Nazwa**: indeks<br /><br />**Opis elementu**: wymagane. Indeks Hello hello tooretrieve części.|
|formDataValue|Zwraca pojedynczą wartość pasujących do nazwy klucza hello z danych formularza lub wynik akcji zakodowane w formularzu.  Jeśli dostępnych jest wiele dopasowuje je spowoduje błąd.  Na przykład zwróci następujące hello `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Liczba parametrów**: 1<br /><br />**Nazwa**: Nazwa akcji<br /><br />**Opis elementu**: wymagane. Nazwa Hello hello akcji z danych formularza lub postać zakodowanych odpowiedzi.<br /><br />**Liczba parametrów**: 2<br /><br />**Nazwa**: Nazwa klucza<br /><br />**Opis elementu**: wymagane. Witaj nazwa klucza hello formularza danych wartości tooreturn.|
|formDataMultiValues|Zwraca tablicę pasujących do nazwy klucza hello z danych formularza lub wynik akcji postać zakodowanych wartości.  Na przykład zwróci następujące hello `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Liczba parametrów**: 1<br /><br />**Nazwa**: Nazwa akcji<br /><br />**Opis elementu**: wymagane. Nazwa Hello hello akcji z danych formularza lub postać zakodowanych odpowiedzi.<br /><br />**Liczba parametrów**: 2<br /><br />**Nazwa**: Nazwa klucza<br /><br />**Opis elementu**: wymagane. Nazwa klucza Hello danych formularza hello wartości tooreturn.|
|multipartBody|Zwraca hello treść część wieloczęściowych danych wyjściowych akcji.<br /><br />**Liczba parametrów**: 1<br /><br />**Nazwa**: Nazwa akcji<br /><br />**Opis elementu**: wymagane. Nazwa Hello hello akcji za pomocą wieloczęściowej wiadomości odpowiedzi.<br /><br />**Liczba parametrów**: 2<br /><br />**Nazwa**: indeks<br /><br />**Opis elementu**: wymagane. Indeks Hello hello tooretrieve części.|

### <a name="math-functions"></a>Funkcje matematyczne  

Te funkcje mogą być używane dla obu typów liczb: **liczb całkowitych** i **przesunięty**.  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|Dodaj|Zwraca wynik hello Dodawanie hello dwóch liczb. Na przykład, funkcja zwraca `20.333`: <p>`add(10,10.333)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Summand 1 <p> **Opis elementu**: wymagane. Witaj tooadd numer zbyt**Summand 2**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: Summand 2 <p> **Opis elementu**: wymagane. Witaj tooadd numer zbyt**Summand 1**.|  
|Sub|Zwraca wynik hello odjęcie dwóch liczb. Na przykład, funkcja zwraca `-0.333`: <p>`sub(10,10.333)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Minuend <p> **Opis elementu**: wymagane. Witaj number, który **Subtrahend** zostanie usunięty z. <p> **Liczba parametrów**: 2 <p> **Nazwa**: Subtrahend <p> **Opis elementu**: wymagane. Witaj numer tooremove z hello **Minuend**.|  
|mul|Zwraca wynik hello pomnożenie hello dwóch liczb. Na przykład, funkcja zwraca `103.33`: <p>`mul(10,10.333)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Multiplicand 1 <p> **Opis elementu**: wymagane. Witaj numer toomultiply **Multiplicand 2** z. <p> **Liczba parametrów**: 2 <p> **Nazwa**: Multiplicand 2 <p> **Opis elementu**: wymagane. Witaj numer toomultiply **Multiplicand 1** z.|  
|DIV|Zwraca wynik powitania po podzieleniu hello dwóch liczb. Na przykład, funkcja zwraca `1.0333`: <p>`div(10.333,10)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: dzielna <p> **Opis elementu**: wymagane. Witaj numer toodivide przez hello **dzielnik**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: dzielnik. <p> **Opis elementu**: wymagane. Liczba hello toodivide Hello **dzielna** przez.|  
|mod|Zwraca hello resztę po podzieleniu hello dwóch liczb (modulo). Na przykład, funkcja zwraca `2`: <p>`mod(10,4)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: dzielna <p> **Opis elementu**: wymagane. Witaj numer toodivide przez hello **dzielnik**. <p> **Liczba parametrów**: 2 <p> **Nazwa**: dzielnik. <p> **Opis elementu**: wymagane. Liczba hello toodivide Hello **dzielna** przez. Po dzielenia hello pozostałej hello jest zajęta.|  
|min.|Istnieją dwa różne wzorce wywoływania tej funkcji. <p>W tym miejscu `min` pobiera tablicę, i zwraca funkcja hello `0`: <p>`min([0,1,2])` <p>Alternatywnie, może to trwać rozdzielaną przecinkami listę wartości, a także zwraca `0`: <p>`min(0,1,2)` <p> **Uwaga**: wszystkie wartości muszą być liczbami, więc jeśli parametr hello jest tablicą, hello tablica ma tooonly mają numery. <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji lub wartość <p> **Opis elementu**: wymagane. Albo tablica wartości minimalnej wartości toofind hello lub hello pierwsza wartość zestawu. <p> **Liczba parametrów**: 2...*n* <p> **Nazwa**: wartość*n* <p> **Opis elementu**: opcjonalne. Jeśli wartość jest pierwszym parametrem hello, przekazuj dodatkowe wartości i hello minimum wszystkich wartości przekazanych są zwracane.|  
|Maksymalna|Istnieją dwa różne wzorce wywoływania tej funkcji. <p>W tym miejscu `max` pobiera tablicę, i zwraca funkcja hello `2`: <p>`max([0,1,2])` <p>Alternatywnie, może to trwać rozdzielaną przecinkami listę wartości, a także zwraca `2`: <p>`max(0,1,2)` <p> **Uwaga**: wszystkie wartości muszą być liczbami, więc jeśli parametr hello jest tablicą, hello tablica ma tooonly mają numery. <p> **Liczba parametrów**: 1 <p> **Nazwa**: kolekcji lub wartość <p> **Opis elementu**: wymagane. Albo tablica wartości toofind hello maksymalną wartość lub hello pierwsza wartość zestawu. <p> **Liczba parametrów**: 2...*n* <p> **Nazwa**: wartość*n* <p> **Opis elementu**: opcjonalne. Jeśli wartość jest pierwszym parametrem hello, przekazuj dodatkowe wartości i hello maksimum wszystkich wartości przekazanych są zwracane.|  
|Zakres|Generuje tablicę liczby całkowite począwszy od pewną liczbę. Należy zdefiniować długość hello hello zwrócił tablicę. <p>Na przykład, funkcja zwraca `[3,4,5,6]`: <p>`range(3,4)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: indeks początkowy <p> **Opis elementu**: wymagane. Witaj pierwszej liczby całkowitej w tablicy hello. <p> **Liczba parametrów**: 2 <p> **Nazwa**: liczba <p> **Opis elementu**: wymagane. Ta wartość jest liczbą hello liczb całkowitych w tablicy hello.|  
|RAND|Generuje losowe hello jako liczba całkowita określony zakres (włącznie tylko na końcu pierwszego). Na przykład, ta funkcja może zwrócić albo `0` lub "1": <p>`rand(0,2)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: minimalna <p> **Opis elementu**: wymagane. Witaj najniższy liczba całkowita, która może być zwracany. <p> **Liczba parametrów**: 2 <p> **Nazwa**: maksymalna <p> **Opis elementu**: wymagane. Ta wartość jest hello najbliższej liczby całkowitej po hello największą liczbę całkowitą, która może zostać zwrócone.|  
  
### <a name="date-functions"></a>Funkcje daty  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|utcnow|Zwraca hello bieżącą sygnaturę czasową jako ciąg, na przykład: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|addSeconds|Dodaje liczby całkowitej określającej liczbę sekund: tooa sygnatury czasowej ciągu przekazany. Witaj liczbę sekund, może być liczbą dodatnią lub ujemną. Domyślnie hello wynik jest ciągiem w ISO 8601 formatu ("e"), ile specyfikator formatu. Na przykład: `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: znacznik czasu <p> **Opis elementu**: wymagane. Ciąg, który zawiera hello czasu. <p> **Liczba parametrów**: 2 <p> **Nazwa**: sekund <p> **Opis elementu**: wymagane. Liczba Hello tooadd sekund. Może być ujemna toosubtract sekund. <p> **Liczba parametrów**: 3 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|addminutes|Dodaje liczby całkowitej określającej liczbę minut: tooa sygnatury czasowej ciągu przekazany. Witaj liczbę minut, może być liczbą dodatnią lub ujemną. Domyślnie hello wynik jest ciągiem w ISO 8601 formatu ("e"), ile specyfikator formatu. Na przykład: `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: znacznik czasu <p> **Opis elementu**: wymagane. Ciąg, który zawiera hello czasu. <p> **Liczba parametrów**: 2 <p> **Nazwa**: minut <p> **Opis elementu**: wymagane. Liczba Hello tooadd minut. Może być ujemna toosubtract minut. <p> **Liczba parametrów**: 3 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|addhours|Dodaje całkowitą liczbę godzin: tooa sygnatury czasowej ciągu przekazany. Witaj liczbę godzin może być liczbą dodatnią lub ujemną. Domyślnie hello wynik jest ciągiem w ISO 8601 formatu ("e"), ile specyfikator formatu. Na przykład: `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: znacznik czasu <p> **Opis elementu**: wymagane. Ciąg, który zawiera hello czasu. <p> **Liczba parametrów**: 2 <p> **Nazwa**: godziny <p> **Opis elementu**: wymagane. Liczba Hello tooadd godzin. Może być ujemna toosubtract godzin. <p> **Liczba parametrów**: 3 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|addDays|Dodaje liczby całkowitej określającej liczbę dni: tooa sygnatury czasowej ciągu przekazany. Witaj liczbę dni, może być liczbą dodatnią lub ujemną. Domyślnie hello wynik jest ciągiem w ISO 8601 formatu ("e"), ile specyfikator formatu. Na przykład: `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Liczba parametrów**: 1 <p> **Nazwa**: znacznik czasu <p> **Opis elementu**: wymagane. Ciąg, który zawiera hello czasu. <p> **Liczba parametrów**: 2 <p> **Nazwa**: dni <p> **Opis elementu**: wymagane. Liczba Hello tooadd dni. Może być ujemna toosubtract dni. <p> **Liczba parametrów**: 3 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|FormatDateTime|Zwraca ciąg w formacie daty. Domyślnie hello wynik jest ciągiem w ISO 8601 formatu ("e"), ile specyfikator formatu. Na przykład: `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Liczba parametrów**: 1 <p> **Nazwa**: Data <p> **Opis elementu**: wymagane. Ciąg, który zawiera hello datę. <p> **Liczba parametrów**: 2 <p> **Nazwa**: Format <p> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|startOfHour|Zwraca hello początek hello godzinę tooa ciąg timestamp przekazany. Na przykład `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.<br /><br />**Liczba parametrów**: 2<br /><br /> **Nazwa**: Format<br /><br /> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").|  
|startOfDay|Zwraca hello początek hello dzień tooa ciąg timestamp przekazany. Na przykład `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.<br /><br />**Liczba parametrów**: 2<br /><br /> **Nazwa**: Format<br /><br /> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").| 
|startOfMonth|Zwraca hello początek hello miesiąca tooa ciąg timestamp przekazany. Na przykład `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.<br /><br />**Liczba parametrów**: 2<br /><br /> **Nazwa**: Format<br /><br /> **Opis elementu**: opcjonalne. Albo [pojedynczy znak specyfikator formatu](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) lub [wzorzec formatu niestandardowego](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) wskazujące, jak tooformat hello wartość sygnatura czasowa. Jeśli format nie jest określona, używany jest format hello ISO 8601 ("o").| 
|DayOfWeek|Zwraca hello dzień tygodnia składnika sygnaturę czasową ciągu.  Niedziela wynosi 0, od poniedziałku 1 i tak dalej. Na przykład `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.| 
|DayOfMonth|Zwraca hello dzień miesiąca składnika sygnaturę czasową ciągu. Na przykład `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.| 
|Dzieńroku|Zwraca hello dzień roku składnika sygnaturę czasową ciągu. Na przykład `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.| 
|znaczniki osi|Zwraca hello znaczników właściwości ciągu sygnatury czasowej. Na przykład `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Liczba parametrów**: 1<br /><br /> **Nazwa**: znacznik czasu<br /><br /> **Opis elementu**: wymagane. Jest to ciąg, który zawiera hello czasu.| 
  
### <a name="workflow-functions"></a>Funkcje przepływu pracy  

Te funkcje pomocne w uzyskaniu informacji na temat hello przepływu pracy, sama w czasie wykonywania.  
  
|Nazwa funkcji|Opis|  
|-------------------|-----------------|  
|listCallbackUrl|Zwraca ciąg toocall tooinvoke hello wyzwalacza lub akcji. <p> **Uwaga**: tej funkcji można używać tylko w **httpWebhook** i **apiConnectionWebhook**nie w **ręczne**, **cyklu**, **http**, lub **apiConnection**. <p>Na przykład Witaj `listCallbackUrl()` funkcja zwraca: <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|przepływ pracy|Ta funkcja udostępnia wszystkie szczegóły hello hello przepływu pracy się w czasie wykonywania hello. <p> Dostępne właściwości w obiekcie przepływu pracy hello są: <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> Witaj wartość hello `run` właściwość jest obiekt z następującymi właściwościami: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Zobacz hello [interfejsu API Rest](http://go.microsoft.com/fwlink/p/?LinkID=525617) szczegółowe informacje na temat tych właściwości.<p> Na przykład tooget hello nazwę hello bieżącego uruchomienia, użyj hello `"@workflow().run.name"` wyrażenia. |

## <a name="next-steps"></a>Następne kroki

[Wyzwalacze i akcje przepływu pracy](logic-apps-workflow-actions-triggers.md)
