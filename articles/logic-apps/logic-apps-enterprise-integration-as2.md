---
title: "aaaAS2 wiadomości B2B integracji przedsiębiorstwa - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wymiana komunikatów AS2 B2B enterprise integracji z usługą Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Wymiana komunikatów AS2 enterprise integracji z usługą logic apps

Przed przystąpieniem do wymiany wiadomości AS2 dla usługi Azure Logic Apps, należy utworzyć umowy AS2 i przechowywać na koncie integracji tej Umowy. Poniżej przedstawiono procedurę hello toocreate AS2 umowy.

## <a name="before-you-start"></a>Przed rozpoczęciem

Oto hello elementy, które należy:

* [Konta integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md) który został już zdefiniowany i skojarzone z subskrypcją platformy Azure
* Co najmniej dwa [partnerów](logic-apps-enterprise-integration-partners.md) który są już zdefiniowane w ramach konta integracji i skonfigurowane z kwalifikatorem hello AS2 w obszarze **tożsamości firm**

> [!NOTE]
> Podczas tworzenia umowy hello zawartości pliku umowy hello musi odpowiadać typowi umowy hello.    

Po [Tworzenie konta usługi integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md) i [dodać partnerów](logic-apps-enterprise-integration-partners.md), można utworzyć umowy AS2, wykonaj następujące czynności.

## <a name="create-an-as2-agreement"></a>Tworzenie umów AS2

1.  Zaloguj się toohello [portalu Azure](http://portal.azure.com "portalu Azure").  

2.  Wybierz z menu po lewej stronie powitania **więcej usług**. W polu wyszukiwania hello wpisz **integracji** jako filtr. Na liście wyników hello, wybierz **konta integracji**.

    > [!TIP]
    > Jeśli nie widzisz **więcej usług**, najpierw trzeba tooexpand hello menu. U góry hello menu hello zwinięte, zaznacz pole wyboru **Pokaż menu**.

    ![Więcej usług, filtr "integrację", wybierz "Konta integracji"](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. W hello **konta integracji** bloku, który otwiera konta integracji hello wybierz miejsce toocreate hello umowy.
Jeśli nie widzisz kont integracji [utworzyć pierwszy](../logic-apps/logic-apps-enterprise-integration-accounts.md "wszystkiego o konta integracji").  

    ![Wybierz konto integracji hello gdzie toocreate hello umowy](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Wybierz hello **umowy** kafelka. Jeśli nie masz kafelka umowy, najpierw Dodaj hello kafelka.

    ![Wybierz Kafelek "Umów"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. W bloku umów hello, który zostanie otwarty, wybierz **Dodaj**.

    ![Wybierz opcję "Dodaj"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. W obszarze **Dodaj**, wprowadź **nazwa** dla umowy. Aby uzyskać **typ umowy**, wybierz pozycję **AS2**. Wybierz hello **partnera hosta**, **tożsamości hosta**, **partnera gościa**, i **tożsamości gościa** dla umowy.

    ![Podaj szczegóły umowy](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Właściwość | Opis |
    | --- | --- |
    | Nazwa |Nazwa umowy hello |
    | Typ umowy | Powinien być AS2 |
    | Partner hosta |Umowa musi mieć partnera zarówno hosta, jak i gościa. partner hosta Hello reprezentuje hello organizacji, który konfiguruje hello umowy. |
    | Tożsamość hosta |Identyfikator partnera hosta hello |
    | Partner gościa |Umowa musi mieć partnera zarówno hosta, jak i gościa. partner gościa Hello reprezentuje hello organizacja, która jest kontynuowanie współpracy hello hosta partnera. |
    | Tożsamość gościa |Identyfikator partnera gościa hello |
    | Odbierają ustawienia |Te właściwości mają zastosowanie tooall komunikatów odebranych przez umowy. |
    | Wyślij ustawienia |Te właściwości mają zastosowanie tooall komunikatów wysłanych przez umowy. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Skonfiguruj sposób dojść do Porozumienia odebrane wiadomości

Teraz, gdy ustawiono hello umowy właściwości, można skonfigurować sposób identyfikuje niniejszej Umowy oraz obsługi przychodzących komunikatów odebranych od swojego partnera, za pośrednictwem niniejszej Umowy.

1.  W obszarze **Dodaj**, wybierz pozycję **ustawienia odbierania**.
Skonfigurować te właściwości, na podstawie Twojej umowy z partnerem hello, który wymienia wiadomości z Tobą. Opisy właściwości znajdują się w tej sekcji tabela hello.

    ![Skonfiguruj "Otrzymywać ustawienia"](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. Opcjonalnie można zastąpić właściwości hello wiadomości przychodzących, wybierając **zastąpienie właściwości komunikatu**.

3. podpisane wszystkich toobe wiadomości przychodzących toorequire, wybierz **wiadomości powinny być podpisane**. Z hello **certyfikatu** listy, wybierz istniejący [certyfikatu publicznego partnera gościa](../logic-apps/logic-apps-enterprise-integration-certificates.md) sprawdzania poprawności podpisu hello na wiadomości powitania. Lub Utwórz certyfikat hello, jeśli nie masz.

4.  Wybierz wszystkie toobe przychodzących wiadomości zaszyfrowane, toorequire **można zaszyfrować wiadomości**. Z hello **certyfikatu** listy, wybierz istniejący [certyfikatu prywatnego partnera hosta](../logic-apps/logic-apps-enterprise-integration-certificates.md) do odszyfrowywania wiadomości przychodzących. Lub Utwórz certyfikat hello, jeśli nie masz.

5. Wybierz toobe wiadomości toorequire skompresowany, **wiadomości powinna być kompresowane**.

6. Wybierz toosend synchroniczne dyspozycji powiadomienie (MDN) po odebraniu wiadomości **wysyłania MDN**.

7. toosend podpisany MDNs po odebraniu wiadomości, wybierz opcję **wysyłania podpisany MDN**.

8. Wybierz asynchroniczne MDNs po odebraniu wiadomości toosend **Wysyłanie asynchroniczne MDN**.

9. Po zakończeniu upewnij się, że toosave ustawień, wybierając **OK**.

Teraz umowie jest gotowy toohandle przychodzących komunikatów, które są zgodne tooyour wybrane ustawienia.

| Właściwość | Opis |
| --- | --- |
| Zastąpienie właściwości wiadomości |Wskazuje, można zastąpić właściwości w odebranej wiadomości. |
| Komunikat powinien być podpisany |Wymaga toobe wiadomości podpisane cyfrowo. Konfigurowanie hello gościa partnera publiczny certyfikatu do sprawdzenia podpisu.  |
| Komunikat powinien być zaszyfrowany |Wymaga toobe wiadomości zaszyfrowane. Wiadomości zaszyfrowanych przez inne niż są odrzucane. Konfigurowanie prywatnego certyfikatu partnera hello hosta do odszyfrowywania wiadomości powitania.  |
| Komunikat powinien być skompresowany |Wymaga toobe wiadomości skompresowane. Skompresowane inne niż wiadomości są odrzucane. |
| Tekst MDN |Hello domyślne dyspozycji powiadomienia (MDN) toobe toohello wysłane wiadomości nadawcy wiadomości. |
| Wyślij MDN |Wymaga toobe MDNs wysyłane. |
| Wyślij MDN podpisem |Wymaga toobe MDNs podpisany. |
| Algorytm Micznych |Wybierz hello toouse algorytm podpisywania wiadomości. |
| Wysyłanie asynchroniczne MDN | Wymaga toobe wiadomości wysyłane asynchronicznie. |
| ADRES URL | Określ adres URL hello gdzie toosend hello MDNs. |

## <a name="configure-how-your-agreement-sends-messages"></a>Skonfiguruj sposób umowie wysyłania wiadomości

Można skonfigurować sposób identyfikuje niniejszej Umowy oraz obsługi komunikatów wychodzących, wysyłających tooyour partnerów w ramach niniejszej Umowy.

1.  W obszarze **Dodaj**, wybierz pozycję **ustawienia wysyłania**.
Skonfigurować te właściwości, na podstawie Twojej umowy z partnerem hello, który wymienia wiadomości z Tobą. Opisy właściwości znajdują się w tej sekcji tabela hello.

    ![Ustaw właściwości "Wyślij ustawienia" hello](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend podpisanych wiadomości tooyour partnera, wybierz opcję **włączyć podpisywanie komunikatów**. Do podpisywania wiadomości powitania w hello **algorytm Micznych** listy, wybierz opcję hello *certyfikatu prywatnego hosta partnera algorytmu Micznych*. W hello **certyfikatu** listy, wybierz istniejący [certyfikatu prywatnego partnera hosta](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend zaszyfrowane wiadomości toohello partnera, wybierz opcję **włączyć szyfrowanie wiadomości**. Do szyfrowania wiadomości powitania w hello **algorytm szyfrowania** listy, wybierz opcję hello *gościa partnera certyfikatu publicznego algorytmu*.
W hello **certyfikatu** listy, wybierz istniejący [certyfikatu publicznego partnera gościa](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. wiadomości powitania toocompress, wybierz opcję **Włącz kompresję komunikat**.

5. nagłówek content-type hello HTTP toounfold w jednym wierszu, wybierz opcję **nagłówków HTTP ujawniać**.

6. tooreceive synchroniczne MDNs dla hello wysyłane wiadomości, wybierz opcję **MDN żądania**.

7. tooreceive podpisu MDNs wiadomości powitania wysyłane, wybierz opcję **MDN podpisane żądanie**.

8. tooreceive MDNs asynchronicznego dla hello wysyłane wiadomości, wybierz opcję **żądania asynchroniczne MDN**. Jeśli wybierzesz tę opcję, gdy toosend hello MDNs wprowadź adres URL hello.

9. Wybierz toorequire bez odrzucania odbioru, **włączyć NRR**.  

10. toospecify algorytmu format toouse w hello Mikrofon lub logowanie hello wychodzące nagłówki wiadomości powitania AS2 lub MDN, wybierz **format algorytmu SHA2**.  

11. Po zakończeniu upewnij się, że toosave ustawień, wybierając **OK**.

Umowy jest teraz gotowy toohandle wychodzących wiadomości zgodnych ze standardami tooyour wybrane ustawienia.

| Właściwość | Opis |
| --- | --- |
| Włącz podpisywania wiadomości |Wymaga wszystkich wiadomości wysłanych z toobe umowy hello podpisany. |
| Algorytm Micznych |Witaj toouse algorytm podpisywania wiadomości. Konfiguruje hello hosta partnera certyfikatu prywatnego Micznych algorytm podpisywania wiadomości powitania. |
| Certyfikat |Wybierz hello toouse certyfikatu podpisywania wiadomości. Konfiguruje hello hosta partnera prywatnej certyfikat podpisywania wiadomości powitania. |
| Włącz szyfrowanie wiadomości |Wymaga szyfrowania wszystkich wiadomości wysłanych z niniejszej Umowy. Konfiguruje hello gościa partnera certyfikatu publicznego algorytm szyfrowania wiadomości powitania. |
| Algorytm szyfrowania |Witaj toouse algorytmu szyfrowania do szyfrowania wiadomości. Konfiguruje hello gościa partnera publiczny certyfikatu do szyfrowania wiadomości powitania. |
| Certyfikat |wiadomości powitania certyfikatu toouse tooencrypt. Konfiguruje hello gościa partnera prywatny certyfikatu do szyfrowania wiadomości powitania. |
| Włącz kompresję wiadomości |Wymaga kompresji wszystkich wiadomości wysłanych z niniejszej Umowy. |
| Unfold — nagłówki HTTP |Umieszcza nagłówka content-type protokołu HTTP hello na jeden wiersz. |
| Żądanie MDN |Wymaga MDN dla wszystkich wiadomości wysłanych z niniejszej Umowy. |
| Żądanie podpisany MDN |Wymaga wszystkich MDNs, które są wysyłane toothis podpisanej toobe. |
| Żądania asynchroniczne MDN |Wymaga asynchroniczne MDNs toobe wysyłane toothis umowy. |
| ADRES URL |Określ adres URL hello gdzie toosend hello MDNs. |
| Włącz NRR |Wymaga bez odrzucania odbioru (NRR), atrybut komunikacji, który dostarcza dane hello dowodów została odebrana jako problemu. |
| Format algorytmu SHA2 |Wybierz algorytm format toouse hello Mikrofon lub logowanie hello nagłówków wiadomości powitania AS2 lub MDN wychodzących |

## <a name="find-your-created-agreement"></a>Znajdź utworzone umowy

1.  Po zakończeniu ustawienie z właściwości umowę na powitania **Dodaj** bloku, wybierz **OK** toofinish tworzenia umowy i zwracany tooyour bloku konta usługi integracji.

    Nowo dodany umowy teraz pojawia się w sieci **umowy** listy.

2.  Można również wyświetlić umów w przeglądzie konta integracji. W bloku konta integracji, wybierz **omówienie**, a następnie wybierz pozycję hello **umowy** kafelka. 

    ![Wybierz wszystkie umowy tooview kafelka "Umów"](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/as2/). 

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
