---
title: "Azure AD Connect: Opis Aprowizacją deklaratywną | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono hello deklaratywne inicjowania obsługi administracyjnej model konfiguracji w programie Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Synchronizacja programu Azure AD Connect: opis Aprowizacją deklaratywną
W tym temacie wyjaśniono hello model konfiguracji w programie Azure AD Connect. Hello model jest nazywany Aprowizacją deklaratywną i pozwala toomake z łatwością zmiana konfiguracji. Wiele czynności opisanych w tym temacie są zaawansowane i nie jest wymagane dla większości scenariuszy.

## <a name="overview"></a>Omówienie
Aprowizacja deklaratywna przetwarzania przychodzących z katalogu źródłowego połączone obiekty i określa, jak przekształcone hello obiektów i atrybutów z celu tooa źródła. Obiekt jest przetwarzane w potoku synchronizacji i potoku hello jest hello takie same dla reguł ruchu przychodzącego i wychodzącego. Reguła ruchu przychodzącego pochodzi z metaverse łącznika miejsca toohello i Reguła ruchu wychodzącego jest z przestrzeni łącznika tooa metaverse hello.

![Potok synchronizacji](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

potok Hello ma kilka różnych modułach. Każdy z nich jest odpowiedzialny za jednej koncepcji w obiekt synchronizacji.

![Potok synchronizacji](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Źródło, hello obiektu źródłowego
* [Zakres](#scope), odnajduje wszystkie reguły synchronizacji, które znajdują się w zakresie
* [Dołącz](#join), określa relację między obszar łączników i metaverse
* [Przekształć](#transform), jak atrybuty powinny zostać przekształcone powoduje obliczenie i przepływu
* [Pierwszeństwo](#precedence), rozwiązuje konflikt wkładów atrybutu
* Obiekt docelowy hello obiektu docelowego

## <a name="scope"></a>Zakres
Moduł zakresu Hello jest szacowania obiektu i określa hello reguł, które znajdują się w zakresie i powinny być uwzględnione w hello przetwarzania. W zależności od wartości atrybutów hello w obiekcie hello reguły synchronizacji różnych są obliczane toobe w zakresie. Na przykład wyłączony użytkownik z nie skrzynek pocztowych programu Exchange mają inne reguły niż włączonego użytkownika z skrzynki pocztowej.  
![Zakres](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

zakres Hello jest zdefiniowany jako grupy i klauzul. klauzule Hello są wewnątrz grupy. Logiczne i jest używany podczas komunikacji między wszystkie klauzule w grupie. Na przykład (działu IT i kraju = = Dania). Logiczne lub jest używana między grupami.

![Zakres](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
zakres Hello na tej ilustracji są odczytywane jako (działu IT i kraju = = Dania) lub (kraju = Szwecja). Jeśli zarówno grupy 1 lub 2 jest obliczane tootrue, reguła hello jest w zakresie.

Moduł zakresu Hello obsługuje hello następujące operacje.

| Operacja | Opis |
| --- | --- |
| RÓWNOŚCI, NOTEQUAL |Porównaj ciąg, który ocenia, czy wartość jest równa toohello wartości w atrybucie hello. W przypadku atrybutów wielowartościowych Zobacz ISIN i ISNOTIN. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Porównaj ciąg, który ocenia, czy wartość jest poniżej wartości hello w atrybucie hello. |
| ZAWIERA, NOTCONTAINS |Porównaj ciąg, który ocenia, czy wartość znajduje się gdzieś wewnątrz wartości w atrybucie hello. |
| STARTSWITH, NOTSTARTSWITH |Porównaj ciąg, który ocenia, czy wartość jest hello początku hello wartości w atrybucie hello. |
| ENDSWITH, NOTENDSWITH |Porównaj ciąg, który ocenia, czy wartość jest w końcu hello hello wartości w atrybucie hello. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Porównaj ciąg, który ocenia, czy wartość jest większa niż hello wartości w atrybucie hello. |
| ISNULL, ISNOTNULL |Ocenia, jeśli jest obecny atrybut hello z hello obiektu. Jeśli atrybut hello nie jest obecny i dlatego wartość null, reguły hello jest w zakresie. |
| ISIN, ISNOTIN |Ocenia, czy wartość hello jest obecny w atrybucie hello zdefiniowane. Ta operacja jest odmianą wielowartościowe hello równości i NOTEQUAL. Atrybut Hello powinien toobe atrybutów wielowartościowych i jeśli wartość hello znajdują się w wartości atrybutu hello, następnie reguły hello znajduje się w zakresie. |
| ISBITSET, ISNOTBITSET |Ocenia, jeśli ustawiono bit konkretnego. Na przykład może być używane tooevaluate hello bitów toosee kontroli konta użytkownika, jeśli użytkownik jest włączone lub wyłączone. |
| ISMEMBEROF, ISNOTMEMBEROF |wartość Hello powinna zawierać nazwa Wyróżniająca grupy tooa w hello przestrzeni łącznika. Jeśli obiekt hello jest członkiem grupy hello określone, reguła hello jest w zakresie. |

## <a name="join"></a>Join
Moduł sprzężenia Hello w potoku synchronizacji hello jest odpowiedzialny za znajdowanie hello relacji między obiekt hello w źródle hello i obiektu w celu hello. W przychodzącej regule ta relacja będzie obiektu w przestrzeni łącznika, znajdowanie obiektu tooan relacji w magazynie metaverse hello.  
![Dołącz między cs i mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
Celem Hello jest toosee, jeśli obiekt już istnieje w magazynie metaverse hello, utworzone przez innego łącznika, powinna być skojarzona z. Na przykład w zasobie konta użytkownika hello lasu z lasem kont hello powinien być połączony z użytkownikiem hello z lasu zasobów hello.

Sprzężenia są używane przede wszystkim na reguł ruchu przychodzącego toojoin łącznika miejsca obiekty razem toohello tego samego obiektu metaverse.

sprzężenia Hello są definiowane jako co najmniej jedną grupę. W grupie masz klauzul. Logiczne i jest używany podczas komunikacji między wszystkie klauzule w grupie. Logiczne lub jest używana między grupami. Hello grupy są przetwarzane w kolejności od top toobottom. Po jednej grupie ma dokładnie jedno dopasowanie z obiektem w celu hello są oceniane żadnych reguł sprzężenia. Jeśli zero lub więcej niż jeden obiekt zostanie znaleziony, przetwarzanie będzie kontynuowane toohello następnej grupy reguł. Z tego powodu hello zasady powinny zostać utworzone w kolejności hello najbardziej jawne pierwszy i bardziej rozmytego na końcu hello.  
![Dołącz do definicji](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
sprzężenia Hello na tej ilustracji są przetwarzane z najwyższym toobottom. Pierwszy potok synchronizacji hello widzi, jeśli istnieje dopasowanie na identyfikator pracownika. Jeśli nie widzi hello drugą regułę, jeśli hello nazwa konta może być obiektów hello toojoin używane razem. Jeśli nie jest dopasowanie albo, hello trzeci i końcowa reguła jest bardziej rozmytego dopasowanie przy użyciu hello nazwy użytkownika.

Witaj zostały ocenione wszystkie reguły sprzężenia, jeśli ma dokładnie jedno dopasowanie, **typu łącza** na powitania **opis** strona jest używana. Jeśli ta opcja jest ustawiona zbyt**udostępniania**, a następnie tworzony jest nowy obiekt w celu hello.  
![Zapewnianie lub sprzężenia](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Obiekt powinien mieć tylko jedną regułę synchronizacji jednego z regułami sprzężenia w zakresie. Jeśli istnieje wiele reguł synchronizacji których sprzężenie jest zdefiniowana, występuje błąd. Pierwszeństwo nie jest używane tooresolve sprzężenia konfliktów. Obiekt musi mieć reguły sprzężenia w zakresie tooflow atrybutów z hello tym samym kierunku ruchu przychodzącego/wychodzącego. Jeśli potrzebujesz tooflow atrybutów ruchu przychodzącego i wychodzącego toohello sam obiekt, muszą mieć ruchu przychodzącego i regułę synchronizacji ruchu wychodzącego z sprzężenia.

Wychodzące sprzężenia ma specjalnego zachowania w przypadku próby tooprovision przestrzeni łącznika docelowego obiektu tooa. Atrybut Hello DN jest używane toofirst wstecznego sprzężenia. Jeśli istnieje już obiekt w przestrzeni łącznika docelowy hello hello tej samej nazwy domeny, hello, które są połączone obiekty.

Moduł sprzężenia Hello tylko oceny po po nową regułę synchronizacji wchodzi w zakres. Jeśli została przyłączona do obiektu, nie jest odłączania nawet wtedy, gdy kryteria dołączania hello nie jest spełniony. Jeśli chcesz toodisjoin obiektu hello reguły synchronizacji, który dołączył obiektów hello musi się znaleźć poza zakresem.

### <a name="metaverse-delete"></a>Usuń metaverse
Obiektu metaverse pozostaje tak długo, jak istnieje jedna reguła synchronizacji w zakresie z **typu łącza** ustawić także**udostępniania** lub **StickyJoin**. StickyJoin jest używany podczas łącznika nie jest dozwolona tooprovision nowy obiektu toohello metaverse, jednak podczas dołączył, musi ono zostać usunięte w źródle hello przed usunięciem obiektu metaverse hello.

Po usunięciu obiektu metaverse wszystkie obiekty skojarzone z reguła synchronizacji ruchu wychodzącego oznaczone do **udostępniania** są oznaczone do usunięcia.

## <a name="transformations"></a>Przekształcenia
przekształcenia Hello są używane toodefine jak element docelowy toohello źródła hello powinien przepływ atrybutów. Witaj przepływów może mieć jedną z następujących hello **przepływ typów**: bezpośrednie, stałej lub wyrażenia. Bezpośrednie przepływu, przepływy jako wartość atrybutu-jest nie dodatkowe przekształceń. Witaj zestawy wartości stałej określona wartość. W wyrażeniu hello deklaratywne inicjowania obsługi administracyjnej wyrażenia języka tooexpress jak powinny być hello transformacji. Witaj szczegółów dla hello wyrażenia języka można znaleźć w hello [opis deklaratywne inicjowania obsługi language wyrażenie](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) tematu.

![Zapewnianie lub sprzężenia](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Hello **Zastosuj raz** wyboru definiuje hello ten atrybut powinien można ustawić tylko podczas tworzenia obiektu hello. Na przykład ta konfiguracja może być używane tooset początkowe hasło dla nowego obiektu użytkownika.

### <a name="merging-attribute-values"></a>Scalanie wartości atrybutów
W przepływów atrybutów hello ma toodetermine ustawienie, atrybuty wielowartościowe powinny zostać scalone z kilku różnych łączników. Witaj, wartość domyślna to **aktualizacji**, co oznacza tej reguły synchronizacji hello o najwyższym priorytecie powinno win.

![Scal typów](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Istnieje również **scalania** i **MergeCaseInsensitive**. Te opcje umożliwiają toomerge wartości z różnych źródeł. Na przykład może być używane toomerge atrybut elementu członkowskiego lub proxyAddresses hello z kilku różnych lasach. Tej opcji wszystkie synchronizacji zasad w zakresie dla obiekt, należy użyć hello sam scalania typu. Nie można zdefiniować **aktualizacji** z jeden łącznik i **scalania** z innej. Jeśli spróbujesz, wystąpi błąd.

Witaj różnica między **scalania** i **MergeCaseInsensitive** jest sposób tooprocess zduplikowane wartości atrybutu. Aparat synchronizacji Hello zapewnia, że zduplikowane wartości nie są wstawiane do atrybutu docelowego hello. Z **MergeCaseInsensitive**, zduplikowane wartości z tylko różnicą w przypadku, gdy nie będą obecne toobe. Na przykład użytkownik nie powinien być widoczny zarówno "SMTP:bob@contoso.com"i"smtp:bob@contoso.com" w hello atrybut target. **Scal** tylko przegląda hello dokładne wartości oraz wielu wartości w przypadku, gdy tylko różnią się w przypadku mogą być dostępne.

Witaj opcja **Zastąp** jest identyczny hello **aktualizacji**, ale nie jest on używany.

### <a name="control-hello-attribute-flow-process"></a>Procesu przepływu atrybutu hello kontroli
Kiedy wiele reguł synchronizacji ruchu przychodzącego są skonfigurowane toocontribute toohello sam atrybut metaverse, a następnie pierwszeństwo jest wygrał użytkownik hello toodetermine używane. Reguła synchronizacji Hello o najwyższy priorytet (najmniejsza wartość liczbowa) będzie toocontribute hello wartość. Witaj, które same odbywa się w reguł dla ruchu wychodzącego. Reguła synchronizacji Hello o najwyższym priorytecie wins i współtworzenia hello wartość toohello połączonego katalogu.

W niektórych przypadkach zamiast współtworzenia wartość, reguła synchronizacji hello należy określić zachowanie inne zasady. Istnieją pewne specjalne literałów używane dla tego przypadku.

Dla reguł synchronizacji ruchu przychodzącego hello literału **NULL** mogą być używane tooindicate czy przepływu hello ma toocontribute nie wartości. Inna reguła o niższym priorytecie może przyczynić się wartość. Jeśli żadna reguła przyczyniły się wartość, atrybut metaverse hello jest usuwany. Wychodzące reguły Jeśli **NULL** jest końcowej hello po przetworzeniu wszystkich reguł synchronizacji, a następnie hello wartość zostanie usunięta w hello połączonego katalogu.

Witaj literału **AuthoritativeNull** przypomina zbyt**NULL** , ale z hello różnicą, że żadne reguły niższy priorytet może przyczynić się wartość.

Przepływ atrybutu można również użyć **IgnoreThisFlow**. Jest podobne tooNULL w hello sensie, że wskazuje nic nie toocontribute. Witaj różnica polega na tym, że nie usuwa już istniejącą wartość w celu hello. Jest tak przepływ atrybutów hello nigdy nie było dostępne.

Oto przykład:

W *limit tooAD - hybrydowym programu Exchange użytkownika* można znaleźć następującego przepływu hello:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
To wyrażenie powinno zostać odczytany jako: Jeśli skrzynka pocztowa użytkownika hello znajduje się w usłudze Azure AD, następnie przepływu atrybutu hello z tooAD usługi Azure AD. Jeśli nie, nie przepływać cokolwiek wstecz tooActive katalogu. W takim przypadku go zachowa hello istniejącą wartość w usłudze AD.

### <a name="importedvalue"></a>ImportedValue
Funkcja Hello ImportedValue różni się od innych funkcji, ponieważ nazwa atrybutu hello musi być ujęta w cudzysłów, a nie w nawiasy kwadratowe:  
`ImportedValue("proxyAddresses")`.

Zwykle podczas synchronizacji atrybutu używa hello oczekiwanej wartości, nawet jeśli nie zostaną wyeksportowane jeszcze lub błąd podczas eksportowania ("top wieża hello"). Synchronizacji ruchu przychodzącego przyjęto założenie, że atrybut, który nie jeszcze osiągnięto połączonego katalogu ostatecznie osiągnie on. W niektórych przypadkach należy tooonly zsynchronizować wartość, która została potwierdzona przez hello połączonego katalogu (hologram i różnicowe zaimportować wieża").

Przykładem tej funkcji można znaleźć w hello out-of-box reguły synchronizacji *w z usługi Active Directory — typowe użytkownika z programu Exchange*. W programie Exchange hybrydowych wartość hello dodawane przez program Exchange online tylko powinna zostać zsynchronizowana gdy zostało potwierdzone, zostały pomyślnie wyeksportowane wartość hello:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Priorytet
Przy próbie kilka reguł synchronizacji toocontribute hello sam element docelowy toohello wartość atrybutu, wartość priorytetu hello wygrał użytkownik hello toodetermine używane. Reguła Hello o najwyższym priorytecie, najmniejsza wartość liczbowa będzie atrybut hello toocontribute konflikt.

![Scal typów](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Ta kolejność może być używane toodefine dokładniejsze atrybutu przepływów małego podzbioru obiektów. Na przykład hello out z — pole — zasady upewnij się, że atrybutów z włączonym kontem (**AccountEnabled użytkownika**) mają priorytet z innych kont.

Można zdefiniować priorytet między łączników. Która umożliwia łączniki wartościami lepsze toocontribute danych najpierw.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Wiele obiektów z hello tej samej przestrzeni łącznika
Jeśli masz wiele obiektów w hello łącznik sam obszar toohello dołączonego do obiektu metaverse tego samego priorytetu musi zostać dostosowana. Jeśli niektóre obiekty znajdują się w zakresie z hello sama synchronizacja reguły, a następnie hello aparatu synchronizacji nie jest toodetermine stanie pierwszeństwo. Jest niejednoznaczny obiekt źródłowy, który powinien współtworzenia hello wartość toohello metaverse. Ta konfiguracja został zgłoszony jako niejednoznaczny, nawet jeśli atrybuty hello w źródle hello mają hello tę samą wartość.  
![Wiele obiektów przyłączone toohello tego samego obiektu mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

W tym scenariuszu należy toochange hello zakresu reguł synchronizacji hello więc hello obiekty źródła synchronizacji różnych zasad w zakresie. Umożliwiające toodefine inny priorytet.  
![Wiele obiektów przyłączone toohello tego samego obiektu mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello język wyrażeń w [opis deklaratywne inicjowania obsługi administracyjnej wyrażenia](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Zobacz, jak deklaratywne inicjowania obsługi administracyjnej jest używane out-of-box w [opis hello domyślnej konfiguracji](active-directory-aadconnectsync-understanding-default-configuration.md).
* Zobacz, jak zmienić przy użyciu aprowizacją deklaratywną w toomake praktyczny [jak toomake toohello zmiany domyślną konfigurację](active-directory-aadconnectsync-change-the-configuration.md).
* Kontynuować tooread użytkowników i kontaktów współdziałania w [opis użytkowników i kontaktów](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

**Tematy odwołań**

* [Synchronizacja programu Azure AD Connect: odwołanie do funkcji](active-directory-aadconnectsync-functions-reference.md)
