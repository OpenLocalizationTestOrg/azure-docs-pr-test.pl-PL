---
title: "Systemy z usługi Azure Logic Apps plików lokalnych tooon aaaConnect | Dokumentacja firmy Microsoft"
description: "Nawiązywanie połączenia tooon lokalnych systemów plików z przepływu pracy aplikacji logiki za pośrednictwem bramy danych lokalne powitania i łącznika systemu plików"
keywords: "systemy plików"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Połącz tooon lokalnych systemów plików z aplikacji logiki z hello łącznika systemu plików

Połączenia hybrydowe chmury jest centralna toologic aplikacji, danych tak toomanage i bezpiecznego dostępu do zasobów lokalnych, aplikacje logiki można użyć bramy danych lokalne powitania. W tym artykule zostanie przedstawiony sposób tooconnect tooan lokalnego systemu plików za pomocą podstawowy scenariusz: Skopiuj plik to jest tooa przekazane tooDropbox udziału plików, a następnie wyślij wiadomość e-mail.

## <a name="prerequisites"></a>Wymagania wstępne

- Instalowanie i konfigurowanie hello najnowszych [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127).
- Instalowanie hello najnowszej bramy danych lokalnych, wersji 1.15.6150.1 lub nowszej. [Połączenie bramy danych lokalnych toohello](http://aka.ms/logicapps-gateway) list hello kroki. Brama Hello musi zostać zainstalowana na maszynie lokalnej, przed kontynuowaniem hello pozostałe kroki hello.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Dodaj wyzwalacza i akcje podłączania tooyour systemu plików

1. Tworzenie aplikacji logiki, a następnie dodaj ten wyzwalacz Dropbox: **utworzenia pliku** 
2. W obszarze hello wyzwalacza, wybierz **następnego kroku** > **Dodaj akcję**. 
3. W polu wyszukiwania hello wpisz `file system` , aby wyświetlić wszystkie obsługiwane akcje hello łącznika systemu plików.

   ![Wyszukiwanie plików łącznika](media/logic-apps-using-file-connector/search-file-connector.png)

2. Wybierz hello **Utwórz plik** akcji i utworzyć systemu plików tooyour połączenia.

   Jeśli nie masz istniejące połączenie, to zostanie wyświetlony monit o toocreate, jeden.

   1. Wybierz **Połącz za pośrednictwem bramy danych lokalnych**. Więcej właściwości są wyświetlane.
   2. Wybierz folder główny dla systemu plików.
      
       > [!NOTE]
       > folder główny Hello jest folderu nadrzędnego głównego hello, który jest używany dla ścieżek względnych dla wszystkich akcji związanych z pliku. Można określić folderu lokalnego na maszynie hello, w której zainstalowano bramę danych lokalne powitania lub hello folder może być udział sieciowy, który hello komputer może uzyskać dostęp.

   3. Wprowadź bramy hello hello nazwy użytkownika i hasła.
   4. Wybierz bramę hello, która została wcześniej zainstalowana.

       ![Skonfiguruj połączenie](media/logic-apps-using-file-connector/create-file.png)

3. Po podaniu wszystkich szczegółów hello wybierz **Utwórz**. 

   Logic Apps konfiguruje i testuje połączenie, upewniając się, czy hello połączenie działa poprawnie. 
   Jeśli połączenie hello jest poprawnie skonfigurowane, zobaczysz opcji dla akcji hello, które wcześniej wybrano. 
   Łącznik programu system plików Hello jest teraz gotowy do użycia.

4. Określ czy toocopy pliki z folderu głównego toohello skrzynki dla udziału plików lokalnych.

   ![Utworzenie pliku](media/logic-apps-using-file-connector/create-file-filled.png)

5. Po pliku hello kopie aplikacji logiki dodać akcję programu Outlook, która wysyła wiadomość e-mail, więc odpowiednich użytkowników wiedzieć o hello nowy plik. Wprowadź hello adresatów, tytuł i treść wiadomości e-mail hello. 

   W hello dynamiczne selektora zawartości można wybrać danych wyjściowych z hello pliku łącznika, dodając więcej szczegółów toohello e-mail.

   ![Wysłanie wiadomości e-mail](media/logic-apps-using-file-connector/send-email.png)

6. Zapisz aplikację logiki. Testowanie aplikacji, przekazując tooDropbox pliku. Hello pliku należy uzyskać udział pliku lokalnego toohello skopiowane, a użytkownik powinien otrzymywać wiadomość e-mail o hello operacji.

   > [!TIP] 
   > Dowiedz się, jak za[Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Gratulacje, masz teraz pracy aplikacji logiki podłączoną tooyour lokalnego systemu plików. Spróbuj eksploracji inne funkcje, które hello oferty łącznika, na przykład:

- Utwórz plik
- Wyświetl listę plików w folderze
- Dołącz plik
- Usuń plik
- Pobierz zawartość pliku
- Pobierz zawartość pliku przy użyciu ścieżki
- Pobierz plik metadanych
- Pobierz metadane pliku przy użyciu ścieżki
- Wyświetl listę plików w folderze głównym
- Plik aktualizacji

## <a name="view-hello-swagger"></a>Widok hello swagger
Zobacz hello [swagger szczegóły](/connectors/fileconnector/). 

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask odpowiedzi na pytania i Dowiedz się, jakie inne usługi Azure Logic Apps robią użytkownicy, odwiedź stronę hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

- [Połącz dane lokalne tooon](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki
- Dowiedz się więcej o [integracji przedsiębiorstwa](../logic-apps/logic-apps-enterprise-integration-overview.md)
