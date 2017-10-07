---
title: "Łącznik usługi OneDrive hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie hello łącznika usługi OneDrive z parametrami interfejsu API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Rozpoczynanie pracy z łącznikiem usługi OneDrive hello
Łączenie plików, w tym przekazywania, get, Usuń pliki i tooOneDrive toomanage. 

Z usługą OneDrive możesz: 

* Tworzenie przepływu pracy przez zapisanie plików w usłudze OneDrive lub zaktualizować istniejące pliki w usłudze OneDrive. 
* Użyj toostart wyzwalaczy przepływu pracy, jeśli plik jest tworzony lub aktualizowany w aplikacji OneDrive.
* Użyj akcji toocreate pliku, usuń plik i inne. Na przykład po odebraniu nowej usługi Office 365 wiadomości e-mail z załącznikiem (wyzwalacz) Utwórz nowy plik w usłudze OneDrive (działanie).

W tym temacie pokazano, jak toouse hello łącznika usługi OneDrive w aplikacji logiki, a także list hello wyzwalacze i akcje.

toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Połącz tooOneDrive
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi. Połączenie stanowi połączenie między aplikacji logiki i innej usługi. Na przykład tooconnect tooOneDrive, należy najpierw OneDrive *połączenia*. toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, które mają tooconnect do zwykle jest używana. Tak z usługą OneDrive, wprowadź hello poświadczenia tooyour OneDrive konta toocreate hello połączenia.

### <a name="create-hello-connection"></a>Utwórz połączenie hello
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Użyć wyzwalacza
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. Wyzwalacze "sondować" hello usługi interwału i częstotliwość. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. W aplikacji logiki hello wpisz "onedrive" tooget listę hello wyzwalaczy:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Wybierz **modyfikacji pliku**. Jeśli połączenie już istnieje, wybierz opcję tooselect przycisk Pokaż selektora hello folderu.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Jeśli zostanie wyświetlony monit o toosign w, wprowadź znak hello szczegóły toocreate hello połączenia. [Utwórz połączenie hello](connectors-create-api-onedrive.md#create-the-connection) w tym temacie przedstawiono kroki hello. 
   
   > [!NOTE]
   > W tym przykładzie aplikacja logiki hello uruchamiane po pliku w folderze hello, wybranych aktualizacji. wyniki hello toosee tego wyzwalacza, Dodaj inną akcję wysyłanej wiadomości e-mail. Na przykład dodać hello Office 365 Outlook *wysłać wiadomość e-mail* akcję, która wysyła pocztą e-mail, należy po zaktualizowaniu pliku. 

3. Wybierz hello **Edytuj** przycisk i ustaw hello **częstotliwość** i **interwał** wartości. Na przykład, jeśli chcesz toopoll wyzwalacza hello co 15 minut, następnie ustawić hello **częstotliwość** za**minutę**i ustaw hello **interwał** zbyt**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Zapisz** zmiany (lewym górnym rogu paska narzędzi hello). Aplikację logiki jest zapisywana i automatycznie włączone.

## <a name="use-an-action"></a>Za pomocą akcji
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Wybierz znak plus hello. Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Wybierz **Dodaj akcję**.
3. W polu tekstowym hello wpisz "onedrive" tooget listę wszystkich hello dostępne akcje.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. W tym przykładzie wybierz **OneDrive — Utwórz plik**. Jeśli połączenie już istnieje, a następnie wybierz hello **ścieżka folderu** tooput hello pliku, wprowadź hello **nazwę pliku**i wybierz polecenie hello **zawartość pliku** chcesz:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia. [Utwórz połączenie hello](connectors-create-api-onedrive.md#create-the-connection) w tym temacie opisano te właściwości. 
   
   > [!NOTE]
   > W tym przykładzie utworzymy nowy plik w folderze OneDrive. Mogą wykorzystywać dane z innego pliku OneDrive hello toocreate wyzwalacza. Na przykład dodać hello Office 365 Outlook *po odebraniu nowej wiadomości e-mail* wyzwalacza. Następnie dodaj hello OneDrive *Utwórz plik* akcję, która używa hello załączników i pola typu zawartości w ramach ForEach toocreate hello nowy plik w usłudze OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Zapisz** zmiany (lewym górnym rogu paska narzędzi hello). Aplikację logiki jest zapisywana i automatycznie włączone.


## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Więcej łączników
Przejdź wstecz toohello [listy interfejsów API](apis-list.md).
