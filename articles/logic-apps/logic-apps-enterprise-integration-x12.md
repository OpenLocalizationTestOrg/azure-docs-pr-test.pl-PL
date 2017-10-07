---
title: "aaaX12 wiadomości B2B integracji przedsiębiorstwa - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Exchange X12 wiadomości w formacie EDI B2B enterprise integracji z usługą Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Komunikaty programu Exchange X12 enterprise integracji z usługą logic apps

Przed przystąpieniem do wymiany X12 wiadomości dla usługi Azure Logic Apps, należy utworzyć X12 umowy i przechowywać na koncie integracji tej Umowy. Poniżej przedstawiono procedurę hello toocreate jako X12 umowy.

> [!NOTE]
> Ta strona obejmuje funkcje hello X12 dla usługi Azure Logic Apps. Aby uzyskać więcej informacji, zobacz [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* [Konta integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure
* Co najmniej dwa [partnerów](../logic-apps/logic-apps-enterprise-integration-partners.md) które są zdefiniowane w ramach konta integracji i skonfigurowano hello X12 identyfikator w obszarze **tożsamości firm**    
* Wymaganą [schematu](../logic-apps/logic-apps-enterprise-integration-schemas.md) o przekazywaniu tooyour [konta integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Po [Tworzenie konta usługi integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md), [dodać partnerów](logic-apps-enterprise-integration-partners.md)i mieć [schematu](../logic-apps/logic-apps-enterprise-integration-schemas.md) czy chcesz toouse, możesz utworzyć X12 umowy, wykonując następujące kroki.

## <a name="create-an-x12-agreement"></a>Utwórz X12 umowy

1.  Zaloguj się toohello [portalu Azure](http://portal.azure.com "portalu Azure"). Wybierz z menu po lewej stronie powitania **więcej usług**. 

    > [!TIP]
    > Jeśli nie widzisz **więcej usług**, najpierw trzeba tooexpand hello menu. U góry hello menu hello zwinięte, zaznacz pole wyboru **Pokaż menu**.

    ![W lewym menu wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  W polu wyszukiwania hello wpisz "Integracja" jako filtr. Na liście wyników hello, wybierz **konta integracji**.  

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. W hello **konta integracji** bloku, który otwiera konta integracji hello wybierz miejsce tooadd hello umowy.
Jeśli nie widzisz kont integracji [utworzyć pierwszy](../logic-apps/logic-apps-enterprise-integration-accounts.md "wszystkiego o konta integracji").

    ![Wybierz konto integracji, gdzie toocreate hello umowy](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Wybierz **omówienie**, a następnie wybierz pozycję hello **umowy** kafelka. Jeśli nie masz kafelka umowy, najpierw Dodaj hello kafelka. 

    ![Wybierz Kafelek "Umów"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. W bloku umów hello, który zostanie otwarty, wybierz **Dodaj**.

    ![Wybierz opcję "Dodaj"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. W obszarze **Dodaj**, wprowadź **nazwa** dla umowy. Wybierz typ umowy hello, **X12**. Wybierz hello **partnera hosta**, **tożsamości hosta**, **partnera gościa**, i **tożsamości gościa** dla umowy. Więcej szczegółów właściwości Zobacz tabelę hello w tym kroku.

    ![Podaj szczegóły umowy](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Właściwość | Opis |
    | --- | --- |
    | Nazwa |Nazwa umowy hello |
    | Typ umowy | Powinien być X12 |
    | Partner hosta |Umowa musi mieć partnera zarówno hosta, jak i gościa. partner hosta Hello reprezentuje hello organizacji, który konfiguruje hello umowy. |
    | Tożsamość hosta |Identyfikator partnera hosta hello |
    | Partner gościa |Umowa musi mieć partnera zarówno hosta, jak i gościa. partner gościa Hello reprezentuje hello organizacja, która jest kontynuowanie współpracy hello hosta partnera. |
    | Tożsamość gościa |Identyfikator partnera gościa hello |
    | Odbierają ustawienia |Te właściwości mają zastosowanie tooall komunikatów odebranych przez umowy. |
    | Wyślij ustawienia |Te właściwości mają zastosowanie tooall komunikatów wysłanych przez umowy. |  

  > [!NOTE]
  > Rozdzielczość X12 zależy od dopasowania hello kwalifikator nadawcy i identyfikator i hello odbiornika kwalifikator i zdefiniowany w wiadomości przychodzących i hello partner identyfikator umowy. Zmiany tych wartości dla partnera, zaktualizuj za hello umowy.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Skonfiguruj sposób dojść do Porozumienia odebrane wiadomości

Teraz, gdy ustawiono hello umowy właściwości, można skonfigurować sposób identyfikuje niniejszej Umowy oraz obsługi przychodzących komunikatów odebranych od swojego partnera, za pośrednictwem niniejszej Umowy.

1.  W obszarze **Dodaj**, wybierz pozycję **ustawienia odbierania**.
Skonfigurować te właściwości, na podstawie Twojej umowy z partnerem hello, który wymienia wiadomości z Tobą. Opis właściwości Zobacz hello tabelach w tej sekcji.

    **Odbierają ustawienia** jest podzielona na następujące sekcje: identyfikatory, potwierdzenia, schematów, koperty, numery kontroli, sprawdzanie poprawności i ustawienia wewnętrzne.

2. Po zakończeniu upewnij się, że toosave ustawień, wybierając **OK**.

Teraz umowie jest gotowy toohandle przychodzących komunikatów, które są zgodne tooyour wybrane ustawienia.

### <a name="identifiers"></a>Identyfikatory

![Identyfikator właściwości.](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Właściwość | Opis |
| --- | --- |
| ISA1 (autoryzacji kwalifikator) |Wybierz wartość kwalifikatora autoryzacji hello z listy rozwijanej hello. |
| ISA2 |Opcjonalny. Wprowadź wartość informacji o autoryzacji. Jeśli wprowadzona dla ISA1 wartość hello jest inne niż 00, wprowadź co najmniej jeden znak alfanumeryczny oraz maksymalnie 10. |
| ISA3 (kwalifikator zabezpieczeń) |Wybierz wartość kwalifikatora zabezpieczeń hello z listy rozwijanej hello. |
| ISA4 |Opcjonalny. Wprowadź wartość informacji zabezpieczeń hello. Jeśli wprowadzona dla ISA3 wartość hello jest inne niż 00, wprowadź co najmniej jeden znak alfanumeryczny oraz maksymalnie 10. |

### <a name="acknowledgment"></a>Potwierdzenia

![Ustaw właściwości potwierdzenia](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Właściwość | Opis |
| --- | --- |
| Oczekiwano TA1 |Zwraca nadawcy wymiany toohello potwierdzenia techniczne |
| Oczekiwano FA |Zwraca nadawcy wymiany toohello funkcjonalności potwierdzenia. Następnie wybierz czy potwierdzenia hello 997 lub 999 na podstawie wersji schematu hello |
| Obejmują AK2/IK2 pętli |Włącza generowanie pętle AK2 w funkcjonalności potwierdzenia dla zestawów zaakceptowane transakcji |

### <a name="schemas"></a>Schematy

Wybierz opcję schematu dla każdego typu transakcji (ST1) i aplikację Sender (GS2). odbieranie Hello potoku rozkłada hello komunikat przychodzący odpowiadającą wartości powitania dla ST1 i GS2 w hello komunikat przychodzący z hello wartości, ustawiony w tym miejscu i schematu hello wiadomości przychodzącej hello ze schematem hello określonego w tym miejscu.

![Wybierz opcję schematu](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Właściwość | Opis |
| --- | --- |
| Wersja |Wybierz wersję hello X12 |
| Typ transakcji (ST01) |Wybierz typ transakcji hello |
| Nadawca aplikacji (GS02) |Wybierz aplikację sender hello |
| Schemat |Wybierz plik schematu hello ma toouse. Schematy są dodawane tooyour integracji konta. |

> [!NOTE]
> Skonfiguruj wymagane hello [schematu](../logic-apps/logic-apps-enterprise-integration-schemas.md) czyli przekazane tooyour [konta integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Kopert

![Określ separatora hello w zestawie transakcji: Wybierz identyfikator Standard lub Separator powtórzenia](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Właściwość | Opis |
| --- | --- |
| Użycie ISA11 |Określa toouse separatora hello w zestawie transakcji: <p>Wybierz **standardowy identyfikator** toouse a kropki (.) dla notacji dziesiętnej, zamiast notacji dziesiętnej hello hello przychodzącego dokumentu w hello EDI odbierania potoku. <p>Wybierz **separatora powtarzania** toospecify hello separatora dla wystąpień powtórzony element proste danych lub strukturą danych powtórzony. Na przykład zwykle hello karatach (^) jest używany jako separator powtarzania hello. Schematy HIPAA można używać tylko karatach hello. |

### <a name="control-numbers"></a>Numery kontroli

![Wybierz sposób toohandle kontroli duplikaty numerów](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Właściwość | Opis |
| --- | --- |
| Nie zezwalaj na duplikaty Interchange numer formantu |Blokowanie wymianę zduplikowane. Sprawdza, czy hello wymiany kontroli numer (ISA13) hello Odebrano wymiany formantu. W przypadku wykrycia dopasowanie hello odbierania potoku nie przetworzył hello wymiany. Można określić hello liczbę dni na potrzeby sprawdzania hello, zapewniając wartość *Sprawdź, czy zduplikowany ISA13 co (dni)*. |
| Nie zezwalaj na duplikaty numerów kontrolnych grupy |Blok wymiany z numerami kontroli zduplikowanej grupie. |
| Nie zezwalaj na duplikaty numerów kontrolnych zestawu transakcji |Blok wymiany z numerami kontroli zestaw zduplikowaną transakcję. |

### <a name="validations"></a>Sprawdzanie poprawności

![Ustaw właściwości sprawdzania poprawności odebranej wiadomości](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Po zakończeniu każdego wiersza weryfikacji innego automatycznie jest dodawany. Jeśli nie określisz żadnych reguł sprawdzania poprawności używa wiersza "Default" hello.

| Właściwość | Opis |
| --- | --- |
| Typ komunikatu |Wybierz typ wiadomości powitania EDI. |
| Sprawdzanie poprawności EDI |Sprawdzają poprawność EDI typy danych zdefiniowane przez schemat hello EDI właściwości, ograniczenia długości danych puste elementy i końcowe separatorów. |
| Rozszerzonej weryfikacji |Jeśli nie jest typem danych hello EDI, znajduje się na powitania danych elementu wymaganie sprawdzania poprawności i dozwolone powtarzania, wyliczenia i dane weryfikacji długości elementu (min/max). |
| Zezwalaj na wiodących/kończących wartości zerowe |Zachowaj wszystkie dodatkowe początkowe lub końcowe zero i miejsce znaków. Nie, usuń te znaki. |
| TRIM wiodących/kończących wartości zerowe |Usuń wiodących lub końcowych zero i spacje. |
| Końcowy znak separatora zasad |Generowanie końcowe separatorów. <p>Wybierz **niedozwolone** ograniczniki końcowe tooprohibit i separatory w hello Odebrano wymiany. Jeśli wymiany hello końcowe ograniczniki i separatorów, wymiany hello jest zadeklarowana nie prawidłowy. <p>Wybierz **opcjonalnie** tooaccept wymiany z lub bez końcowych ograniczniki i separatorów. <p>Wybierz **obowiązkowe** podczas wymiany hello musi mieć końcowe ograniczniki i separatorów. |

### <a name="internal-settings"></a>Ustawienia wewnętrzne

![Wybierz ustawienia wewnętrzne](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Właściwość | Opis |
| --- | --- |
| Konwertuj domniemanych format dziesiętny "Nn" tooa 10 numerycznych wartości podstawowej |Konwertuje liczbę EDI, określonego w formacie hello "Nn" na wartość liczbową base-10 |
| Utwórz puste tagi XML, jeśli dozwolone są separatory kończące |Wybierz obejmują tego pola wyboru toohave hello wymiany nadawcy puste tagi XML dla końcowe separatorów. |
| Rozdziel wymianę na zestawy transakcji — zawieś zestawy transakcji w przypadku błędu|Analizuje każdą transakcję, ustaw w wymiany do innego dokumentu XML, stosując hello odpowiednie koperty toohello transakcji zestawu. Wstrzymuje tylko transakcje hello, gdzie hello uwierzytelnienie nie powiedzie się. |
| Rozdziel wymianę na zestawy transakcji — zawieś wymianę w przypadku błędu|Analizuje każdą transakcję, ustaw w wymiany do innego dokumentu XML przez zastosowanie odpowiednich koperty hello. Wstrzymuje całego wymiany, gdy jeden lub więcej zestawów transakcji w wymiany hello niepowodzenie sprawdzania poprawności. | 
| Zachowaj wymiany — wstrzymanie zestawy transakcji w przypadku błędu |Pozostawia wymiany hello niezmienione, tworzy dokument XML hello całego wsadowej operacji wymiany. Wstrzymuje tylko zestawy transakcji hello, Niepowodzenie weryfikacji, pozostawiając tooprocess wszystkie inne zestawy transakcji. |
| Zachowaj wymianę — zawieś wymianę w przypadku błędu |Pozostawia wymiany hello niezmienione, tworzy dokument XML hello całego wsadowej operacji wymiany. Wstrzymuje wymiany całego hello gdy jeden lub więcej zestawów transakcji w wymiany hello weryfikacji nie powiedzie się. |

## <a name="configure-how-your-agreement-sends-messages"></a>Skonfiguruj sposób umowie wysyłania wiadomości

Można skonfigurować sposób identyfikuje niniejszej Umowy oraz obsługi komunikatów wychodzących, wysyłających partnera tooyour za pośrednictwem niniejszej Umowy.

1.  W obszarze **Dodaj**, wybierz pozycję **ustawienia wysyłania**.
Skonfigurować te właściwości, na podstawie Twojej umowy z partnerem, który wymienia wiadomości z Tobą. Opis właściwości Zobacz hello tabelach w tej sekcji.

    **Wyślij ustawienia** jest podzielona na następujące sekcje: identyfikatory, potwierdzenia, schematów, koperty, zestawów znaków i separatorów, numery kontroli i sprawdzania poprawności.

2. Po zakończeniu upewnij się, że toosave ustawień, wybierając **OK**.

Umowy jest teraz gotowy toohandle wychodzących wiadomości zgodnych ze standardami tooyour wybrane ustawienia.

### <a name="identifiers"></a>Identyfikatory

![Identyfikator właściwości.](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Właściwość | Opis |
| --- | --- |
| Kwalifikator autoryzacji (ISA1) |Wybierz wartość kwalifikatora autoryzacji hello z listy rozwijanej hello. |
| ISA2 |Wprowadź wartość informacji o autoryzacji. Jeśli ta wartość jest równa 00, wprowadź co najmniej jeden znak alfanumeryczny oraz maksymalnie 10. |
| Kwalifikator zabezpieczeń (ISA3) |Wybierz wartość kwalifikatora zabezpieczeń hello z listy rozwijanej hello. |
| ISA4 |Wprowadź wartość informacji zabezpieczeń hello. Jeśli ta wartość jest równa 00 hello (ISA4) wartość pola tekstowego, wprowadź co najmniej jedną wartość alfanumeryczne i maksymalnie 10. |

### <a name="acknowledgment"></a>Potwierdzenia

![Ustaw właściwości potwierdzenia](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Właściwość | Opis |
| --- | --- |
| Oczekiwano TA1 |Zwróć nadawcy wymiany toohello techniczne potwierdzenia (TA1). To ustawienie określa tej hello partnera hosta, który wysyła żądania wiadomość hello potwierdzenia od partnera gościa hello hello umowy. Oczekiwano te potwierdzenia przez partnera hosta hello na podstawie ustawień odbierania hello hello umowy. |
| Oczekiwano FA |Zwróć nadawcy wymiany toohello funkcjonalności potwierdzenia (FA). Wybierz, czy hello 997 lub 999 potwierdzeń, oparte na wersji schematu hello, którym pracujesz z. Oczekiwano te potwierdzenia przez partnera hosta hello na podstawie ustawień odbierania hello hello umowy. |
| FA wersji |Wybierz wersję hello FA |

### <a name="schemas"></a>Schematy

![Wybierz toouse schematu](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Właściwość | Opis |
| --- | --- |
| Wersja |Wybierz wersję hello X12 |
| Typ transakcji (ST01) |Wybierz typ transakcji hello |
| SCHEMAT |Wybierz hello toouse schematu. Schematy znajdują się na koncie integracji. Jeśli najpierw wybrać schematu automatycznie konfiguruje wersji i transakcji typu  |

> [!NOTE]
> Skonfiguruj wymagane hello [schematu](../logic-apps/logic-apps-enterprise-integration-schemas.md) czyli przekazane tooyour [konta integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Kopert

![Określ separatora hello w zestawie transakcji: Wybierz identyfikator Standard lub Separator powtórzenia](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Właściwość | Opis |
| --- | --- |
| Użycie ISA11 |Określa toouse separatora hello w zestawie transakcji: <p>Wybierz **standardowy identyfikator** toouse a kropki (.) dla notacji dziesiętnej, zamiast notacji dziesiętnej hello hello przychodzącego dokumentu w hello EDI odbierania potoku. <p>Wybierz **separatora powtarzania** toospecify hello separatora dla wystąpień powtórzony element proste danych lub strukturą danych powtórzony. Na przykład zwykle hello karatach (^) jest używany jako separator powtarzania hello. Schematy HIPAA można używać tylko karatach hello. |

### <a name="control-numbers"></a>Numery kontroli

![Określ właściwości formantu](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Właściwość | Opis |
| --- | --- |
| Numer wersji formantu (ISA12) |Wybierz wersję hello hello X12 standardowe |
| Użycie wskaźnika (ISA15) |Wybierz kontekst hello wymiany.  wartości Hello są informacji i danych produkcyjnych lub dane testowe |
| Schemat |Generuje hello GS i segmentów ST wymiany kodowany w formacie X12 wysyła toohello wysyłania potoku |
| GS1 |Opcjonalne, wybierz wartość hello funkcjonalny kod z listy rozwijanej hello |
| GS2 |Opcjonalne, nadawca aplikacji |
| GS3 |Opcjonalne, odbiornika aplikacji |
| GS4 |Opcjonalne, wybierz opcję CCYYMMDD lub rrmmdd |
| GS5 |Opcjonalnie wybierz hh: mm, HHMMSS albo HHMMSSdd |
| GS7 |Opcjonalne, wybierz wartość dla właściwej agencji hello z listy rozwijanej hello |
| GS8 |Opcjonalne, wersja hello dokumentu |
| Interchange numer formantu (ISA13) |Wymagane, wprowadź numer formantu wymiany hello zakresu wartości. Wprowadź wartość liczbową z zakresu od 1 i maksymalnie 999999999 |
| Numer grupy kontroli (GS06) |Wymagane, wprowadź numer kontroli grupy hello zakres numerów. Wprowadź wartość liczbową z zakresu od 1 i maksymalnie 999999999 |
| Numer kontroli zestawu transakcji (ST02) |Wymagane, wprowadź zakres numerów hello formantu ustawić transakcji. Wprowadź zakres wartości liczbowych z co najmniej 1 i maksymalnie 999999999 |
| Prefiks |Opcjonalne, które są przeznaczone dla zakresu hello numerów kontroli zestawu transakcji używanych w potwierdzeniu. Wprowadź wartość liczbową dla hello środkowej dwóch pól i wartości alfanumeryczne (w razie potrzeby) dla pól hello prefiksu i sufiksu. pola środkowej Hello są wymagane i zawierają hello wartości minimalna i maksymalna hello Kontrola numeru |
| Sufiks |Opcjonalne, które są przeznaczone dla zakresu hello numerów kontroli zestawu transakcji używanych w potwierdzeniu. Wprowadź wartość liczbową dla hello środkowej dwóch pól i wartości alfanumeryczne (w razie potrzeby) dla pól hello prefiksu i sufiksu. pola środkowej Hello są wymagane i zawierają hello wartości minimalna i maksymalna hello Kontrola numeru |

### <a name="character-sets-and-separators"></a>Zestawy znaków i separatory

Inne niż zestaw znaków hello, można wprowadzić inny zestaw ograniczniki dla każdego typu komunikatu. Jeśli zestaw znaków nie jest określona dla schematu danej wiadomości, domyślny zestaw znaków hello jest używany.

![Określ ograniczniki typów wiadomości](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Właściwość | Opis |
| --- | --- |
| Toobe zestaw znaków używany |toovalidate hello właściwości, wybierz opcję hello X12 zestaw znaków. Opcje Hello są Basic, rozszerzone i UTF8. |
| Schemat |Wybierz schemat z listy rozwijanej hello. Po wykonaniu każdego wiersza, jest automatycznie dodawany nowy wiersz. Wybrany schemat hello separatorów wybierz hello ustawić, które mają toouse oparte na powitania po opisy separatora. |
| Typ danych wejściowych |Wybierz typ danych wejściowych z listy rozwijanej hello. |
| Separator składnika |elementy danych tooseparate, wprowadź jeden znak. |
| Separator elementów danych |tooseparate proste danych elementów w obrębie elementów danych, wprowadź jeden znak. |
| Znak zastępczy |Wpisz znak zastępczy używany do zastępowania znaków separatora wszystkich danych ładunku hello podczas generowania wiadomości powitania X12 ruchu wychodzącego. |
| Terminator segmentu |tooindicate hello końca segmentu EDI, wprowadź jeden znak. |
| Sufiks |Wybierz hello znak, który jest używany z hello identyfikator segmentu. Jeśli możesz wyznaczyć sufiks, a następnie hello segmentu terminatora danych elementu może być pusta. Terminator segmentu hello jest puste, należy wyznaczyć sufiks. |

> [!TIP]
> tooprovide wartości znaków specjalnych, edytowanie umowy hello w formacie JSON i podaj wartość ASCII hello hello znak specjalny.

### <a name="validation"></a>Walidacja

![Ustaw właściwości sprawdzania poprawności do wysyłania wiadomości](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Po zakończeniu każdego wiersza weryfikacji innego automatycznie jest dodawany. Jeśli nie określisz żadnych reguł sprawdzania poprawności używa wiersza "Default" hello.

| Właściwość | Opis |
| --- | --- |
| Typ komunikatu |Wybierz typ wiadomości powitania EDI. |
| Sprawdzanie poprawności EDI |Sprawdzają poprawność EDI typy danych zdefiniowane przez schemat hello EDI właściwości, ograniczenia długości danych puste elementy i końcowe separatorów. |
| Rozszerzonej weryfikacji |Jeśli nie jest typem danych hello EDI, znajduje się na powitania danych elementu wymaganie sprawdzania poprawności i dozwolone powtarzania, wyliczenia i dane weryfikacji długości elementu (min/max). |
| Zezwalaj na wiodących/kończących wartości zerowe |Zachowaj wszystkie dodatkowe początkowe lub końcowe zero i miejsce znaków. Nie, usuń te znaki. |
| TRIM wiodących/kończących wartości zerowe |Usuń początkowe lub końcowe zero znaków. |
| Końcowy znak separatora zasad |Generowanie końcowe separatorów. <p>Wybierz **niedozwolone** ograniczniki końcowe tooprohibit i separatory w hello wysyłane wymiany. Jeśli wymiany hello końcowe ograniczniki i separatorów, wymiany hello jest zadeklarowana nie prawidłowy. <p>Wybierz **opcjonalnie** toosend wymiany z lub bez końcowych ograniczniki i separatorów. <p>Wybierz **obowiązkowe** Jeśli hello wysyłane wymiany musi mieć końcowe ograniczniki i separatorów. |

## <a name="find-your-created-agreement"></a>Znajdź utworzone umowy

1.  Po zakończeniu ustawienie z właściwości umowę na powitania **Dodaj** bloku, wybierz **OK** toofinish tworzenia umowy i zwracany tooyour bloku konta usługi integracji.

    Nowo dodany umowy teraz pojawia się w sieci **umowy** listy.

2.  Można również wyświetlić umów w przeglądzie konta integracji. W bloku konta integracji, wybierz **omówienie**, a następnie wybierz pozycję hello **umowy** kafelka.

    ![Wybierz wszystkie umowy tooview kafelka "Umów"](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/x12/). 

## <a name="learn-more"></a>Dowiedz się więcej
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  

