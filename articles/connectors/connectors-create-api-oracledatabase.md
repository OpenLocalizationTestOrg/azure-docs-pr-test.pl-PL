---
title: "Łącznik bazą danych Oracle hello aaaAdd w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj łącznika bazy danych Oracle hello w aplikacji logiki"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Rozpoczynanie pracy z hello bazą danych Oracle łącznika

Za pomocą łącznika bazy danych Oracle hello, możesz utworzyć organizacyjnej przepływów pracy korzystających z danych w istniejącej bazie danych. Ten łącznik można połączyć tooan instalowania lokalną bazą danych Oracle lub maszyny wirtualnej platformy Azure z bazą danych Oracle. Ten łącznik można:

* Tworzenie przepływu pracy przez dodanie nowej bazy danych klientów tooa klientów lub aktualizowanie zamówienia w bazie danych zamówienia.
* Użyj akcji tooget wiersz danych, wstawić nowy wiersz, a nawet usuwać. Na przykład gdy zostaje utworzony rekord w Dynamics CRM Online (wyzwalacz), następnie wstawienia wiersza w bazie danych programu Oracle (działanie). 

W tym temacie pokazano, jak toouse hello łącznik bazy danych Oracle w aplikacji logiki.

## <a name="prerequisites"></a>Wymagania wstępne

* Obsługiwane wersje programu Oracle: 
    * Oracle 9 lub nowszy
    * Oprogramowania klienta Oracle 8.1.7 lub nowszej

* Instalowanie bramy danych lokalne powitania. [Połączenie lokalne tooon dane z aplikacji logiki](../logic-apps/logic-apps-gateway-connection.md) list hello kroki. Brama Hello jest wymagane tooconnect tooan lokalną bazą danych Oracle lub maszynie Wirtualnej platformy Azure z bazy danych Oracle zainstalowane. 

    > [!NOTE]
    > Brama danych lokalne powitania działa jako mostka i udostępnia bezpiecznego transferu danych między lokalnymi danych (który nie znajduje się w chmurze hello) i aplikacje logiki. Witaj, tej samej bramy może być używane z wieloma usługami i wiele źródeł danych. Tak konieczne może być bramy hello tooinstall raz.

* Na komputerze hello, w którym zainstalowano bramę danych lokalne powitania, należy zainstalować powitania klienta Oracle. Należy upewnić się, tooinstall hello dostawca danych programu Oracle 64-bitowego dla platformy .NET z bazy danych Oracle:  

  [64-bitowych ODAC 12c w wersji 4 (12.1.0.2.4) dla systemu Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Jeśli nie zainstalowano klienta Oracle hello, wystąpił błąd występuje, gdy spróbuj toocreate lub użyj hello połączenia. Zobacz hello typowych błędów w tym temacie.


## <a name="add-hello-connector"></a>Dodaj hello łącznika

> [!IMPORTANT]
> Ten łącznik nie ma żadnych wyzwalaczy. Ma ona tylko akcje. Tak podczas tworzenia aplikacji logiki, Dodaj inny toostart wyzwalacza aplikacji logiki, takie jak **harmonogram - cyklu**, lub **żądania / odpowiedzi - odpowiedzi**. 

1. W hello [portalu Azure](https://portal.azure.com), tworzenie aplikacji logiki puste.

2. Na początku hello aplikację logiki, wybierz hello **żądanie / odpowiedź — żądanie** wyzwalacz: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Wybierz pozycję **Zapisz**. Po zapisaniu, adres URL żądania jest generowana automatycznie. 

4. Wybierz **nowy krok**i wybierz **Dodaj akcję**. Wpisz `oracle` toosee hello dostępne akcje: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Dotyczy to również hello najszybszy sposób toosee hello wyzwalacze i Akcje dostępne dla wszystkich łączników. Wpisz część nazwy łącznika hello, takich jak `oracle`. Projektant Hello wymieniono żadne wyzwalacze i wszystkie akcje. 

5. Wybierz jedno z hello działań, takich jak **bazą danych Oracle — wiersz Get**. Wybierz **Połącz za pośrednictwem bramy danych lokalnych**. Wprowadź nazwę serwera Oracle hello, metody uwierzytelniania, nazwy użytkownika, hasło i wybierz hello bramy:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Po nawiązaniu połączenia, wybierz tabelę z listy hello, a następnie wprowadź hello wiersza identyfikator tooyour tabeli. Należy tooknow hello identyfikator toohello tabeli. Jeśli nie znasz, skontaktuj się z administratorem bazy danych Oracle i pobrać dane wyjściowe hello `select * from yourTableName`. Dzięki temu hello informacje umożliwiające identyfikację potrzebne tooproceed.

    W hello poniższy przykład zadanie dane zostały zwrócone z bazy danych zasobów ludzkich: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. W następnym kroku należy można użyć dowolnego z hello toobuild innych łączników przepływ pracy. Jeśli tootest pobieranie danych z bazy danych Oracle, a następnie wyślij do siebie wiadomość e-mail z hello danych Oracle przy użyciu jednej z hello wysłać wiadomości e-mail łączników, takie usługi Office 365 lub Gmail. Używaj tokenów dynamiczne hello z hello Oracle tabeli toobuild hello `Subject` i `Body` Twojego adresu e-mail:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Zapisz** aplikacji logiki, a następnie wybierz **Uruchom**. Zamknij projektanta hello i przyjrzyj się Historia uruchomień hello hello stanu. W przypadku niepowodzenia zaznacz wiersz nie powiodło się wiadomość hello. Otwiera Hello projektanta i programy, które użytkownik, który krok nie powiodło się, a także przedstawiono hello informacje o błędzie. Zakończy się pomyślnie, powinien otrzymywać wiadomość e-mail z informacjami o hello, dodane.


### <a name="workflow-ideas"></a>Koncepcje przepływu pracy

* Mają hasztagiem hello #oracle toomonitor i put tweetów hello w bazie danych, dzięki czemu może być zbadać i używane w innych aplikacjach. W aplikacji logiki, Dodaj hello `Twitter - When a new tweet is posted` wyzwalania, a następnie wprowadź hello **#oracle** hasztagiem. Następnie należy dodać hello `Oracle Database - Insert row` akcji i wybierz tabelę:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* Komunikaty są wysyłane tooa kolejki usługi Service Bus. Mają tooget te komunikaty i umieść je w bazie danych. W aplikacji logiki, Dodaj hello `Service Bus - when a message is received in a queue` wyzwalacza i wybierz hello kolejki. Następnie należy dodać hello `Oracle Database - Insert row` akcji i wybierz tabelę:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Typowe błędy

#### <a name="error-cannot-reach-hello-gateway"></a>**Błąd**: nie można osiągnąć hello bramy

**Przyczyna**: hello lokalnych danych brama nie jest w stanie tooconnect toohello chmury. 

**Środki zaradcze**: Upewnij się, że brama jest uruchomiona na hello na lokalnym komputerze, na którym został zainstalowany i że mogą się łączyć toohello internet.  Zalecamy nie zainstalowanie bramy hello na komputerze, który może zostać wyłączone lub uśpienia. Można również uruchomić ponownie usługi bramy danych lokalne powitania (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Błąd**: Dostawca hello jest używany jest przestarzały: "element System.Data.OracleClient wymaga oprogramowania klienta w wersji version 8.1.7 Oracle lub większą.". Odwiedź stronę [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello oficjalnego dostawcę.

**Przyczyna**: powitania klienta Oracle zestawu SDK nie jest zainstalowany na komputerze hello, gdzie hello lokalnymi brama danych jest uruchomiona.  

**Rozdzielczość**: Pobierz i zainstaluj klienta Oracle hello SDK hello tym samym komputerze co brama danych lokalne powitania.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Błąd**: Tabela "[Nazwa_tabeli]" nie definiuje żadnych kolumn klucza

**Przyczyna**: hello tabela nie ma żadnego klucza podstawowego.  

**Rozdzielczość**: hello łącznika bazy danych programu Oracle wymaga użycia tabelę z kolumną klucza podstawowego.

#### <a name="currently-not-supported"></a>Obecnie nieobsługiwane

* Widoki i procedury składowane 
* Tabeli za pomocą kluczy złożonych
* Zagnieżdżone typy obiektów w tabelach
 
## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/oracle/). 

## <a name="get-some-help"></a>Uzyskaj pomoc

Witaj [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) jest doskonałym umieścić tooask pytania, odpowiedzi na pytania i zobacz, co robią użytkownicy innych Logic Apps. 

Można zwiększyć Logic Apps i łącznikami głosu i przesyłanie pomysłów na [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)i przejrzyj dostępne łączniki hello w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).
