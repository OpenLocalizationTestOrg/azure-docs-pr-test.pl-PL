---
title: "aaaEDIFACT wiadomości B2B integracji przedsiębiorstwa - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "EDIFACT wymiany wiadomości w formacie EDI B2B enterprise integracji z usługą Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Komunikaty Exchange EDIFACT enterprise integracji z usługą logic apps

Przed przystąpieniem do wymiany wiadomości EDIFACT dla usługi Azure Logic Apps, należy utworzyć umowy EDIFACT i przechowywać na koncie integracji tej Umowy. Poniżej przedstawiono procedurę hello toocreate umowy EDIFACT.

> [!NOTE]
> Ta strona obejmuje funkcje EDIFACT hello Azure Logic Apps. Aby uzyskać więcej informacji, zobacz [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* [Konta integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure  
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) które już zostały zdefiniowane w ramach konta integracji

> [!NOTE]
> Podczas tworzenia umowy, zawartość hello w wiadomości powitania, które odbierać lub wysyłać tooand od partnera hello musi odpowiadać typowi umowy hello.

Po [Tworzenie konta usługi integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md) i [dodać partnerów](logic-apps-enterprise-integration-partners.md), można utworzyć umowy EDIFACT, wykonując następujące kroki.

## <a name="create-an-edifact-agreement"></a>Tworzenie umów EDIFACT 

1.  Zaloguj się toohello [portalu Azure](http://portal.azure.com "portalu Azure"). Wybierz z menu po lewej stronie powitania **więcej usług**.

    > [!TIP]
    > Jeśli nie widzisz **więcej usług**, najpierw trzeba tooexpand hello menu. U góry hello menu hello zwinięte, zaznacz pole wyboru **Pokaż menu**.

    ![W lewym menu wybierz pozycję "Więcej usług"](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. W polu wyszukiwania hello wpisz "Integracja" filtru. Na liście wyników hello, wybierz **konta integracji**.

    ![Odfiltruj "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. W hello **konta integracji** bloku, który otwiera konta integracji hello wybierz miejsce toocreate hello umowy.
Jeśli nie widzisz kont integracji [utworzyć pierwszy](../logic-apps/logic-apps-enterprise-integration-accounts.md "wszystkiego o konta integracji").  

    ![Wybierz konto integracji, gdzie toocreate hello umowy](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Wybierz hello **umowy** kafelka. Jeśli nie masz kafelka umowy, najpierw Dodaj hello kafelka.   

    ![Wybierz Kafelek "Umów"](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. W bloku umów hello, który zostanie otwarty, wybierz **Dodaj**.

    ![Wybierz opcję "Dodaj"](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. W obszarze **Dodaj**, wprowadź **nazwa** dla umowy. Aby uzyskać **typ umowy**, wybierz pozycję **EDIFACT**. Wybierz hello **partnera hosta**, **tożsamości hosta**, **partnera gościa**, i **tożsamości gościa** dla umowy.

    ![Podaj szczegóły umowy](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Właściwość | Opis |
    | --- | --- |
    | Nazwa |Nazwa umowy hello |
    | Typ umowy | Powinien być EDIFACT |
    | Partner hosta |Umowa musi mieć partnera zarówno hosta, jak i gościa. partner hosta Hello reprezentuje hello organizacji, który konfiguruje hello umowy. |
    | Tożsamość hosta |Identyfikator partnera hosta hello |
    | Partner gościa |Umowa musi mieć partnera zarówno hosta, jak i gościa. partner gościa Hello reprezentuje hello organizacja, która jest kontynuowanie współpracy hello hosta partnera. |
    | Tożsamość gościa |Identyfikator partnera gościa hello |
    | Odbierają ustawienia |Te właściwości mają zastosowanie tooall komunikatów odebranych przez umowy. |
    | Wyślij ustawienia |Te właściwości mają zastosowanie tooall komunikatów wysłanych przez umowy. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Skonfiguruj sposób dojść do Porozumienia odebrane wiadomości

Teraz, gdy ustawiono hello umowy właściwości, można skonfigurować sposób identyfikuje niniejszej Umowy oraz obsługi przychodzących komunikatów odebranych od swojego partnera, za pośrednictwem niniejszej Umowy.

1.  W obszarze **Dodaj**, wybierz pozycję **ustawienia odbierania**.
Skonfigurować te właściwości, na podstawie Twojej umowy z partnerem hello, który wymienia wiadomości z Tobą. Opis właściwości Zobacz hello tabelach w tej sekcji.

    **Odbierają ustawienia** jest podzielona na następujące sekcje: identyfikatory, potwierdzenia, schematów, numery kontroli, weryfikacji i ustawienia wewnętrzne.

    ![Skonfiguruj "Otrzymywać ustawienia"](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Po zakończeniu upewnij się, że toosave ustawień, wybierając **OK**.

Teraz umowie jest gotowy toohandle przychodzących komunikatów, które są zgodne tooyour wybrane ustawienia.

### <a name="identifiers"></a>Identyfikatory

| Właściwość | Opis |
| --- | --- |
| UNB6.1 (hasło odbiorcy odwołanie) |Wprowadź wartość alfanumeryczne z zakresu od 1 do 14 znaków. |
| UNB6.2 (kwalifikator odbiorcy odwołanie) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i maksymalnie dwóch znaków. |

### <a name="acknowledgments"></a>Potwierdzenia

| Właściwość | Opis |
| --- | --- |
| Potwierdzenie odbioru komunikatu (CONTRL) |Zaznacz to pole wyboru tooreturn techniczne nadawcy wymiany toohello potwierdzenia (CONTRL). Potwierdzenie Hello są wysyłane nadawcy wymiany toohello oparte na powitania ustawienia wysyłania hello umowy. |
| Potwierdzenia (CONTRL) |Wybierz tooreturn tego pola wyboru, wysłania nadawcy wymiany toohello oparte na powitania ustawienia wysyłania umowy hello funkcjonalności (CONTRL) potwierdzającej toohello wymiany nadawcy hello potwierdzenia. |

### <a name="schemas"></a>Schematy

| Właściwość | Opis |
| --- | --- |
| UNH2.1 (TYP) |Wybierz typ zestawu transakcji. |
| UNH2.2 (WERSJA) |Wprowadź numer wersji wiadomość hello. (Minimalna, jeden znak; maksymalna, trzy znaki). |
| UNH2.3 (WERSJA) |Wprowadź numer wersji wiadomość hello. (Minimalna, jeden znak; maksymalna, trzy znaki). |
| UNH2.5 (SKOJARZONY KOD PRZYPISANEJ) |Wprowadź kod hello przypisane. (Maksymalnie sześć znaków. Musi być alfanumeryczny). |
| UNG2.1 (IDENTYFIKATOR NADAWCY APLIKACJI) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i 35 znaków. |
| UNG2.2 (KWALIFIKATOR KODU NADAWCY APLIKACJI) |Wprowadź wartość alfanumeryczne z maksymalnie cztery znaki. |
| SCHEMAT |Wybierz hello wcześniej przekazany schematu ma toouse z Twojego konta skojarzone integracji. |

### <a name="control-numbers"></a>Numery kontroli
| Właściwość | Opis |
| --- | --- |
| Nie zezwalaj na duplikaty Interchange numer formantu |zduplikowane wymianę tooblock, wybierz tę właściwość. Zaznaczenie hello akcji dekodowania EDIFACT sprawdza, czy hello wymiany kontroli numer (UNB5) wymiany hello odebranych nie być zgodny z wcześniej przetworzonych wymiany kontroli. W przypadku wykrycia dopasowanie hello wymiany nie został przetworzony. |
| Sprawdź pod kątem zduplikowanych elementów UNB5 co (dni) |Jeśli została wybrana opcja numery kontroli zduplikowane wymiany toodisallow, można określić hello liczbę dni, kiedy tooperform hello sprawdzać, zapewniając hello odpowiednią wartość dla tego ustawienia. |
| Nie zezwalaj na duplikaty numerów kontrolnych grupy |Wybierz tę właściwość, tooblock wymiany z grupy zduplikowane numery kontroli (UNG5). |
| Nie zezwalaj na duplikaty numerów kontrolnych zestawu transakcji |tooblock wymiany numerami zduplikowaną transakcję zestaw formantu (UNH1), wybierz opcję tej właściwości. |
| Numer formantu EDIFACT potwierdzenia |toodesignate hello transakcji ustawić numery do użycia w potwierdzenia, wprowadź wartość sufiksu prefiks hello oraz zakres numerów odwołania. |

### <a name="validations"></a>Sprawdzanie poprawności

Po zakończeniu każdego wiersza weryfikacji innego automatycznie jest dodawany. Jeśli nie określisz żadnych reguł sprawdzania poprawności używa wiersza "Default" hello.

| Właściwość | Opis |
| --- | --- |
| Typ komunikatu |Wybierz typ wiadomości powitania EDI. |
| Sprawdzanie poprawności EDI |Sprawdzają poprawność EDI typy danych zdefiniowane przez schemat hello EDI właściwości, ograniczenia długości danych puste elementy i końcowe separatorów. |
| Rozszerzonej weryfikacji |Jeśli nie jest typem danych hello EDI, znajduje się na powitania danych elementu wymaganie sprawdzania poprawności i dozwolone powtarzania, wyliczenia i dane weryfikacji długości elementu (min/max). |
| Zezwalaj na wiodących/kończących wartości zerowe |Zachowaj wszystkie dodatkowe początkowe lub końcowe zero i miejsce znaków. Nie, usuń te znaki. |
| TRIM wiodących/kończących wartości zerowe |Usuń wiodących lub końcowych zero i spacje. |
| Końcowy znak separatora zasad |Generowanie końcowe separatorów. <p>Wybierz **niedozwolone** ograniczniki końcowe tooprohibit i separatory w hello Odebrano wymiany. Jeśli wymiany hello końcowe ograniczniki i separatorów, wymiany hello jest zadeklarowana nie prawidłowy. <p>Wybierz **opcjonalnie** tooaccept wymiany z lub bez końcowych ograniczniki i separatorów. <p>Wybierz **obowiązkowe** podczas wymiany hello Odebrano musi mieć końcowe ograniczniki i separatorów. |

### <a name="internal-settings"></a>Ustawienia wewnętrzne

| Właściwość | Opis |
| --- | --- |
| Utwórz puste tagi XML, jeśli dozwolone są separatory kończące |Wybierz obejmują tego pola wyboru toohave hello wymiany nadawcy puste tagi XML dla końcowe separatorów. |
| Rozdziel wymianę na zestawy transakcji — zawieś zestawy transakcji w przypadku błędu|Analizuje każdą transakcję, ustaw w wymiany do innego dokumentu XML, stosując hello odpowiednie koperty toohello transakcji zestawu. Wstrzymaj tylko zestawy transakcji hello, Niepowodzenie weryfikacji. |
| Rozdziel wymianę na zestawy transakcji — zawieś wymianę w przypadku błędu|Analizuje każdą transakcję, ustaw w wymiany do innego dokumentu XML przez zastosowanie odpowiednich koperty hello. Zawiesić hello całego wymiany, gdy jeden lub więcej zestawów transakcji w wymiany hello weryfikacji nie powiedzie się. | 
| Zachowaj wymiany — wstrzymanie zestawy transakcji w przypadku błędu |Pozostawia wymiany hello niezmienione, tworzy dokument XML hello całego wsadowej operacji wymiany. Wstrzymaj tylko zestawy transakcji hello, Niepowodzenie weryfikacji, pozostawiając tooprocess Ustawia wszystkie inne transakcji. |
| Zachowaj wymianę — zawieś wymianę w przypadku błędu |Pozostawia wymiany hello niezmienione, tworzy dokument XML hello całego wsadowej operacji wymiany. Zawiesić hello całego wymiany, gdy jeden lub więcej zestawów transakcji w wymiany hello weryfikacji nie powiedzie się. |

## <a name="configure-how-your-agreement-sends-messages"></a>Skonfiguruj sposób umowie wysyłania wiadomości

Można skonfigurować sposób identyfikuje niniejszej Umowy oraz obsługi komunikatów wychodzących, wysyłających tooyour partnerów w ramach niniejszej Umowy.

1.  W obszarze **Dodaj**, wybierz pozycję **ustawienia wysyłania**.
Skonfigurować te właściwości, na podstawie Twojej umowy z partnerem, który wymienia wiadomości z Tobą. Opis właściwości Zobacz hello tabelach w tej sekcji.

    **Wyślij ustawienia** jest podzielona na następujące sekcje: identyfikatory, potwierdzenia, schematów, koperty, zestawów znaków i separatorów, numery kontroli i sprawdzanie poprawności.

    ![Skonfiguruj "Wyślij ustawienia"](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Po zakończeniu upewnij się, że toosave ustawień, wybierając **OK**.

Umowy jest teraz gotowy toohandle wychodzących wiadomości zgodnych ze standardami tooyour wybrane ustawienia.

### <a name="identifiers"></a>Identyfikatory

| Właściwość | Opis |
| --- | --- |
| UNB1.2 (składnia wersja) |Wybierz wartość z zakresu od **1** i **4**. |
| UNB2.3 (adres routingu odwrotnego nadawcy) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i 14 znaków. |
| UNB3.3 (adres routingu odwrotnego odbiorcy) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i 14 znaków. |
| UNB6.1 (hasło odbiorcy odwołanie) |Wprowadź wartość alfanumeryczne z co najmniej jedną i maksymalnie 14 znaków. |
| UNB6.2 (kwalifikator odbiorcy odwołanie) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i maksymalnie dwóch znaków. |
| UNB7 (identyfikator aplikacji odwołanie) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i 14 znaków |

### <a name="acknowledgment"></a>Potwierdzenia
| Właściwość | Opis |
| --- | --- |
| Potwierdzenie odbioru komunikatu (CONTRL) |Zaznacz to pole wyboru, jeśli partnera hello hostowanej oczekuje tooreceive techniczne potwierdzenia (CONTRL). To ustawienie określa, że partnera hello hostowanych, który wysyła wiadomość hello, żądanie potwierdzenia hello gościa partnera. |
| Potwierdzenia (CONTRL) |Zaznacz to pole wyboru, jeśli partnera hello hostowanej oczekuje tooreceive funkcjonalności potwierdzenia (CONTRL). To ustawienie określa, że partnera hello hostowanych, który wysyła wiadomość hello, żądanie potwierdzenia hello gościa partnera. |
| Generuj pętlę SG1/SG4 dla zaakceptowanych zestawów transakcji |Jeśli została wybrana opcja toorequest potwierdzenia funkcjonalności, wybierz generowania tooforce wyboru pętle grupę SG1/BL4 w funkcjonalności potwierdzenia CONTRL dla zestawów zaakceptowane transakcji. |

### <a name="schemas"></a>Schematy
| Właściwość | Opis |
| --- | --- |
| UNH2.1 (TYP) |Wybierz typ zestawu transakcji. |
| UNH2.2 (WERSJA) |Wprowadź numer wersji wiadomość hello. |
| UNH2.3 (WERSJA) |Wprowadź numer wersji wiadomość hello. |
| SCHEMAT |Wybierz hello toouse schematu. Schematy znajdują się na koncie integracji. tooaccess Twojego schematów najpierw połączyć aplikację logiki tooyour konta integracji. |

### <a name="envelopes"></a>Kopert
| Właściwość | Opis |
| --- | --- |
| UNB8 (przetwarzania kodu priorytet) |Wprowadź wartość alfabetycznej, który nie jest więcej niż jeden znak. |
| UNB10 (Umowa komunikacji) |Wprowadź wartość alfanumeryczne z co najmniej jeden znak i maksymalnie 40 znaków. |
| UNB11 (Test wskaźnik) |Wybierz jest tooindicate tego pola wyboru, która hello wymiany wygenerowane dane testowe |
| Zastosuj segment UNA (porada ciągu usługi) |Zaznacz to pole wyboru toogenerate segment UNA dla toobe wymiany hello wysyłane. |
| Zastosuj segmenty UNG (nagłówek grupy funkcji) |Wybierz ten toocreate wyboru Grupowanie segmentów w nagłówku grupy funkcjonalnej hello w partnerze gościa toohello wiadomości powitania. Hello są następujące wartości używane toocreate hello UNG segmentów: <p>Aby uzyskać **UNG1**, wprowadź wartość alfanumeryczne z co najmniej jeden znak i maksymalnie sześć znaków. <p>Aby uzyskać **UNG2.1**, wprowadź wartość alfanumeryczne z co najmniej jeden znak i 35 znaków. <p>Aby uzyskać **UNG2.2**, wprowadź wartość alfanumeryczne z maksymalnie cztery znaki. <p>Aby uzyskać **UNG3.1**, wprowadź wartość alfanumeryczne z co najmniej jeden znak i 35 znaków. <p>Aby uzyskać **UNG3.2**, wprowadź wartość alfanumeryczne z maksymalnie cztery znaki. <p>Aby uzyskać **UNG6**, wprowadź wartość alfanumeryczne z co najmniej jedną i maksymalnie trzy znaki. <p>Aby uzyskać **UNG7.1**, wprowadź wartość alfanumeryczne z co najmniej jeden znak i maksymalnie trzy znaki. <p>Aby uzyskać **UNG7.2**, wprowadź wartość alfanumeryczne z co najmniej jeden znak i maksymalnie trzy znaki. <p>Aby uzyskać **UNG7.3**, wprowadź wartość alfanumeryczne z co najmniej 1 znak i 6 znaków. <p>Aby uzyskać **UNG8**, wprowadź wartość alfanumeryczne z co najmniej jeden znak i 14 znaków. |

### <a name="character-sets-and-separators"></a>Zestawy znaków i separatory

Inne niż zestaw znaków hello, można wprowadzić inny zestaw toobe ograniczniki używane dla każdego typu komunikatu. Jeśli nie określono zestaw znaków dla schematu danej wiadomości, domyślny zestaw znaków hello jest używany.

| Właściwość | Opis |
| --- | --- |
| UNB1.1 (identyfikator systemowy) |Wybierz hello znak EDIFACT ustawić toobe zastosowane na powitania wychodzące wymiany. |
| Schemat |Wybierz schemat z listy rozwijanej hello. Po wykonaniu każdego wiersza, jest automatycznie dodawany nowy wiersz. Wybrany schemat hello separatorów wybierz hello ustawić, które mają toouse oparte na powitania po opisy separatora. |
| Typ danych wejściowych |Wybierz typ danych wejściowych z listy rozwijanej hello. |
| Separator składnika |elementy danych tooseparate, wprowadź jeden znak. |
| Separator elementów danych |tooseparate proste danych elementów w obrębie elementów danych, wprowadź jeden znak. |
| Terminator segmentu |tooindicate hello końca segmentu EDI, wprowadź jeden znak. |
| Sufiks |Wybierz hello znak, który jest używany z hello identyfikator segmentu. Jeśli możesz wyznaczyć sufiks, a następnie hello segmentu terminatora danych elementu może być pusta. Terminator segmentu hello jest puste, należy wyznaczyć sufiks. |

### <a name="control-numbers"></a>Numery kontroli
| Właściwość | Opis |
| --- | --- |
| UNB5 (numer formantu wymiany) |Wprowadź prefiks, zakres wartości hello wymiany Kontrola numeru i sufiks. Wartości te są używane toogenerate wychodzących wymiany. Witaj prefiksu i sufiksu są opcjonalne, gdy wymagany jest numer kontroli hello. Witaj kontroli numer jest zwiększany dla każdego nowego komunikatu; Witaj prefiksu i sufiksu pozostają hello tego samego. |
| UNG5 (numer formantu grupy) |Wprowadź prefiks, zakres wartości hello wymiany Kontrola numeru i sufiks. Te wartości są używane toogenerate hello grupy kontroli numer. Witaj prefiksu i sufiksu są opcjonalne, gdy wymagany jest numer kontroli hello. numer formantu Hello jest zwiększany dla każdej nowej wiadomości, aż do osiągnięcia maksymalnej wartości hello; Witaj prefiksu i sufiksu pozostają hello tego samego. |
| UNH1 (numer nagłówka wiadomości) |Wprowadź prefiks, zakres wartości hello wymiany Kontrola numeru i sufiks. Te wartości są używane numer odwołania nagłówka wiadomości powitania toogenerate. Witaj prefiksu i sufiksu są opcjonalne, gdy wymagany jest numer odwołania hello. Witaj numer jest zwiększany dla każdego nowego komunikatu; Witaj prefiksu i sufiksu pozostają hello tego samego. |

### <a name="validations"></a>Sprawdzanie poprawności

Po zakończeniu każdego wiersza weryfikacji innego automatycznie jest dodawany. Jeśli nie określisz żadnych reguł sprawdzania poprawności używa wiersza "Default" hello.

| Właściwość | Opis |
| --- | --- |
| Typ komunikatu |Wybierz typ wiadomości powitania EDI. |
| Sprawdzanie poprawności EDI |Sprawdzają poprawność EDI typy danych zdefiniowane właściwości EDI hello hello schematu, ograniczenia długości danych puste elementy i końcowe separatorów. |
| Rozszerzonej weryfikacji |Jeśli nie jest typem danych hello EDI, znajduje się na powitania danych elementu wymaganie sprawdzania poprawności i dozwolone powtarzania, wyliczenia i dane weryfikacji długości elementu (min/max). |
| Zezwalaj na wiodących/kończących wartości zerowe |Zachowaj wszystkie dodatkowe początkowe lub końcowe zero i miejsce znaków. Nie, usuń te znaki. |
| TRIM wiodących/kończących wartości zerowe |Usuń początkowe lub końcowe zero znaków. |
| Końcowy znak separatora zasad |Generowanie końcowe separatorów. <p>Wybierz **niedozwolone** ograniczniki końcowe tooprohibit i separatory w hello wysyłane wymiany. Jeśli wymiany hello końcowe ograniczniki i separatorów, wymiany hello jest zadeklarowana nie prawidłowy. <p>Wybierz **opcjonalnie** toosend wymiany z lub bez końcowych ograniczniki i separatorów. <p>Wybierz **obowiązkowe** Jeśli hello wysyłane wymiany musi mieć końcowe ograniczniki i separatorów. |

## <a name="find-your-created-agreement"></a>Znajdź utworzone umowy

1.  Po zakończeniu ustawienie z właściwości umowę na powitania **Dodaj** bloku, wybierz **OK** toofinish tworzenia umowy i zwracany tooyour bloku konta usługi integracji.

    Nowo dodany umowy teraz pojawia się w sieci **umowy** listy.

2.  Można również wyświetlić umów w przeglądzie konta integracji. W bloku konta integracji, wybierz **omówienie**, a następnie wybierz pozycję hello **umowy** kafelka. 

    ![Wybierz wszystkie umowy tooview kafelka "Umów"](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Plik struktury Swagger widoku
Szczegóły programu Swagger hello tooview hello EDIFACT łącznika, zobacz [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>Dowiedz się więcej
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  

