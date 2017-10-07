---
title: "aaaLearn jak toouse hello łącznik FTP w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooFTP toomanage serwera plików. Można wykonywać różne akcje, takie jak przekazywanie, aktualizacji, Pobierz i usuwania plików na serwerze FTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Rozpoczynanie pracy z hello łącznik FTP
Korzystanie ze toomonitor łącznika hello FTP, zarządzanie i utworzyć pliki na serwerze FTP. 

toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Połącz tooFTP
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi. A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.  

### <a name="create-a-connection-tooftp"></a>Tworzenie tooFTP połączenia
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Użyj wyzwalacz FTP
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> Łącznik FTP Hello wymaga się, że serwer FTP, który jest dostępny z Internetu hello i jest skonfigurowany toooperate trybu PASYWNEGO. Ponadto łącznik hello FTP jest **nie jest zgodne z niejawnych FTPS (FTP za pośrednictwem protokołu SSL)**. Witaj łącznik FTP obsługuje tylko jawne FTPS (FTP za pośrednictwem protokołu SSL).  
> 
> 

W tym przykładzie I przedstawia sposób toouse hello **FTP - podczas dodawania lub modyfikowania pliku** wyzwolenia tooinitiate przepływu pracy aplikacji logiki, po dodaniu pliku lub zmodyfikowane na serwerze FTP. Przykład przedsiębiorstwa można użyć tego wyzwalacza toomonitor FTP folder nowych plików, które reprezentują zamówień od klientów.  Można następnie użyć akcji łącznik FTP takich jak **pobrać zawartość pliku** tooget zawartość hello hello kolejności dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.

1. Wprowadź *ftp* w polu wyszukiwania hello hello logiki aplikacji designer wybierz hello **FTP - podczas dodawania lub modyfikowania pliku** wyzwalacza   
   ![Obraz wyzwalacza FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Witaj **podczas dodawania lub modyfikowania pliku** otwiera formantu  
   ![Wyzwalacz FTP — obraz 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Wybierz hello **...**  znajdujący się po prawej stronie powitania hello formantu. Spowoduje to otwarcie formant wyboru hello folderu  
   ![Obraz wyzwalacza FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Wybierz hello  **>**  (Strzałka w prawo), a następnie przejdź do folderu hello toofind mają toomonitor dla nowych lub zmienionych plików. Wybierz hello folder — hello folder jest teraz wyświetlany na powitania **folderu** formantu.  
   ![Obraz wyzwalacza FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

W tym momencie aplikację logiki została skonfigurowana z wyzwalaczy, które rozpocznie się uruchom hello innych wyzwalacze i akcje w przepływie pracy powitania po modyfikacji lub utworzone w określonym folderze FTP hello pliku. 

> [!NOTE]
> Dla logiki aplikacji toobe funkcjonalności musi ona zawierać przynajmniej jeden wyzwalacz i jedną akcję. Wykonaj kroki hello hello następnej sekcji tooadd akcji.  
> 
> 

## <a name="use-a-ftp-action"></a>Za pomocą akcji FTP
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Teraz, wyzwalacz został dodany, wykonaj te kroki tooadd akcję, która pobierze zawartość pliku nowe lub zmodyfikowane hello znalezione przez wyzwalacz hello hello.    

1. Wybierz **+ nowy krok** tooadd hello hello akcji tooget hello zawartość hello pliku na serwerze hello FTP  
2. Wybierz hello **Dodaj akcję** łącza.  
   ![Obraz akcji FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Wprowadź *FTP* tooFTP związane z toosearch dla wszystkich akcji.
4. Wybierz **FTP — pobranie zawartości pliku** jako hello tootake akcji, gdy nowe lub zmodyfikowane pliku znajduje się w folderze hello FTP.      
   ![Obraz akcji FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Witaj **pobrać zawartość pliku** sterowania zostanie otwarta. **Uwaga**: użytkownik będzie zostanie wyświetlony monit o tooauthorize Twojego tooaccess aplikacji logiki konta serwera FTP, jeśli nie zostało zrobione to wcześniej.  
   ![Obraz akcji FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Wybierz hello **pliku** formantu (hello biały znak znajdujący się poniżej **pliku***). W tym miejscu można żadnego hello różne właściwości z pliku nowe lub zmodyfikowane hello na powitania serwera FTP.  
6. Wybierz hello **plików zawartości** opcji.  
   ![Obraz akcji FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. Formant Hello jest aktualizowany, wskazującą, że hello **FTP — pobranie zawartości pliku** akcji uzyskają hello *plików zawartości* hello pliku nowe lub zmodyfikowane na serwerze hello FTP.      
   ![Obraz akcji FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Zapisz swoją pracę, a następnie dodaj plik toohello FTP folderu tootest przepływ pracy.    

W tym momencie aplikacji logiki hello został skonfigurowany z toomonitor wyzwalacza folderu na serwerze FTP i hello inicjowania przepływu pracy, gdy znajdzie się nowy plik lub zmodyfikowany plik na serwerze hello FTP. 

Aplikacja logiki Hello również została skonfigurowana z akcji hello zawartość tooget hello nowych lub zmodyfikowanych plików.

Można teraz dodawać innej akcji, takich jak hello [SQL Server — Wstaw wiersz](connectors-create-api-sqlazure.md) akcji tooinsert hello zawartość hello nowych lub zmodyfikowanych plików do tabeli bazy danych SQL.  

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)

