---
title: "Nawiązywanie połączenia systemów plików lokalnych z usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Nawiązywanie połączenia systemów plików lokalnych z przepływu pracy aplikacji logiki za pomocą bramy danych lokalnych i łącznika systemu plików"
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
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a>Nawiązywanie połączenia systemów lokalnych plików z aplikacji logiki w usłudze łącznika systemu plików

Połączenia hybrydowe chmury jest centralnej do aplikacji logiki, więc można zarządzać danymi i bezpieczny dostęp do zasobów lokalnych, aplikacje logiki można użyć bramy danych lokalnych. W tym artykule zostanie przedstawiony sposób nawiązywania połączenia z lokalnego systemu plików ze scenariuszem podstawowe: skopiować plik, który jest przekazywany do usługi Dropbox do udziału plików, a następnie wyślij wiadomość e-mail.

## <a name="prerequisites"></a>Wymagania wstępne

- Instalowanie i Konfigurowanie r [bramy danych lokalnych](https://www.microsoft.com/download/details.aspx?id=53127).
- Zainstaluj najnowszą bramę danych lokalnych, wersji 1.15.6150.1 lub nowszej. [Łączenie się z bramą danych lokalnych](http://aka.ms/logicapps-gateway) zawiera listę czynności. Brama musi zainstalowana na maszynie lokalnej, zanim będzie można kontynuować z pozostałych kroków.

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a>Dodaj wyzwalacza oraz do nawiązywania połączenia z systemu plików

1. Tworzenie aplikacji logiki, a następnie dodaj ten wyzwalacz Dropbox: **utworzenia pliku** 
2. W obszarze wyzwalacza, wybierz **następnego kroku** > **Dodaj akcję**. 
3. W polu wyszukiwania wprowadź `file system` , aby wyświetlić wszystkie obsługiwane akcje dla łącznika systemu plików.

   ![Wyszukiwanie plików łącznika](media/logic-apps-using-file-connector/search-file-connector.png)

2. Wybierz **Utwórz plik** akcji i utworzyć połączenie z systemu plików.

   Nie masz istniejące połączenie, monit o jego utworzenie.

   1. Wybierz **Połącz za pośrednictwem bramy danych lokalnych**. Więcej właściwości są wyświetlane.
   2. Wybierz folder główny dla systemu plików.
      
       > [!NOTE]
       > Folder główny jest folderu nadrzędnego głównego, który jest używany dla ścieżek względnych dla wszystkich akcji związanych z pliku. Można określić lokalny folder na komputerze, na którym zainstalowano bramę danych lokalnych lub może to być udział sieciowy, który ma dostęp maszyna.

   3. Wprowadź nazwę użytkownika i hasło dla bramy.
   4. Wybierz bramę, która została wcześniej zainstalowana.

       ![Skonfiguruj połączenie](media/logic-apps-using-file-connector/create-file.png)

3. Po podaniu wszystkie szczegóły, wybierz **Utwórz**. 

   Logic Apps konfiguruje i testuje połączenie, upewniając się, że połączenie działa poprawnie. 
   Jeśli połączenie jest poprawnie skonfigurowane, zobaczysz opcji dla akcji, która wcześniej została zaznaczona. 
   Łącznik systemu plików jest teraz gotowy do użycia.

4. Określ chcesz skopiować pliki z Dropbox do folderu głównego dla udziału plików lokalnych.

   ![Utworzenie pliku](media/logic-apps-using-file-connector/create-file-filled.png)

5. Po aplikację logiki kopiuje plik, należy dodać akcję programu Outlook, która wysyła wiadomość e-mail, więc odpowiednich użytkowników wiedzieć o nowy plik. Wprowadź adresatów, tytuł i treść wiadomości e-mail. 

   W selektorze zawartości dynamicznej można danych wyjściowych z łącznika plików, dodając więcej szczegółowych informacji do wiadomości e-mail.

   ![Wysłanie wiadomości e-mail](media/logic-apps-using-file-connector/send-email.png)

6. Zapisz aplikację logiki. Testowanie aplikacji, przekazując plik do skrzynki. Plik powinien pobrać skopiowane do udziału pliku lokalnego, a użytkownik powinien otrzymywać wiadomości e-mail dotyczące działania.

   > [!TIP] 
   > Dowiedz się, jak [Monitoruj aplikacje logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Gratulacje, masz teraz pracy aplikacji logiki, który może łączyć się z lokalnego systemu plików. Spróbuj eksploracji inne funkcje, które oferuje łącznika, na przykład:

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

## <a name="view-the-swagger"></a>Wyświetlanie struktury swagger
Zobacz [swagger szczegóły](/connectors/fileconnector/). 

## <a name="get-help"></a>Uzyskiwanie pomocy

Aby zadawać pytania, odpowiadać na nie i patrzeć, co robią inni użytkownicy usługi Azure Logic Apps, odwiedź [forum usługi Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

Aby pomóc w ulepszaniu usługi Azure Logic Apps, przesyłaj pomysły lub głosuj na nie w [witrynie opinii użytkowników usługi Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Następne kroki

- [Połącz się z lokalnymi danymi](../logic-apps/logic-apps-gateway-connection.md) z aplikacji logiki
- Dowiedz się więcej o [integracji przedsiębiorstwa](../logic-apps/logic-apps-enterprise-integration-overview.md)
