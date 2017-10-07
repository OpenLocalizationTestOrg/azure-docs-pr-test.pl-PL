---
title: "Łącznik aaaDropbox w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooDropbox toomanage plików. Można wykonywać różne akcje, takie jak przekazywanie, zaktualizować, Pobierz i usuwania plików skrzynki."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Rozpoczynanie pracy z łącznikiem usługi Dropbox hello
Połącz tooDropbox toomanage plików. Można wykonywać różne akcje, takie jak przekazywanie, zaktualizować, Pobierz i usuwania plików skrzynki.

toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Połącz tooDropbox
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi. Połączenie stanowi połączenie między aplikacji logiki i innej usługi. Na przykład w kolejności tooconnect tooDropbox, należy najpierw Dropbox *połączenia*. toocreate połączenie, będzie potrzebny poświadczenia hello tooprovide tooaccess hello usługi, które mają tooconnect do zwykle jest używana. Tak w przykładzie skrzynki hello będzie potrzebny hello tooyour poświadczenia konta Dropbox w kolejności toocreate hello połączenia tooDropbox. [Dowiedz się więcej na temat połączenia]()

### <a name="create-a-connection-toodropbox"></a>Tworzenie tooDropbox połączenia
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Użyj wyzwalacz skrzynki
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

W tym przykładzie używamy hello **podczas tworzenia pliku** wyzwalacza. W przypadku wystąpienia tego wyzwalacza będzie nazywamy hello **pobieranie plików zawartości przy użyciu ścieżki** skrzynki akcji. 

1. Wprowadź *dropbox* w polu wyszukiwania hello hello Logic Apps designer, a następnie wybierz hello **Dropbox — po utworzeniu pliku** wyzwalacza.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Wybierz folder hello, w której ma zostać tootrack tworzenia pliku. Wybierz... (określone w polu hello czerwony) i przeglądania folderów toohello ma wejściowych tooselect hello wyzwalacza.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Za pomocą akcji skrzynki
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Teraz, gdy hello wyzwalacz został dodany, wykonaj te kroki tooadd akcję, która pobierze zawartość hello nowy plik.

1. Wybierz **+ nowy krok** akcji hello tooadd chcesz tootake podczas tworzenia nowego pliku.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Wybierz **Dodaj akcję**. To pole wyszukiwania hello otwiera gdzie możesz wyszukać dowolną akcję należy chcieliby tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Wprowadź *dropbox* toosearch dla tooDropbox powiązanych działań.  
4. Wybierz **Dropbox - pobrania zawartości pliku przy użyciu ścieżki** jako hello tootake akcji podczas tworzenia nowego pliku w hello wybrany Dropbox folder. zostanie otwarty blok kontroli Hello akcji. Użytkownik będzie zostanie wyświetlony monit o tooauthorize Twojego tooaccess aplikacji logiki usłudze Dropbox konta, jeśli nie zostało zrobione to wcześniej.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Wybierz... (znajdujący się na powitania po prawej stronie powitania **ścieżka pliku** sterowania) i przejdź do ścieżki pliku toohello chcesz toouse. Lub użyj hello **ścieżka pliku** tokenu toospeed się z tworzenia aplikacji logiki.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Zapisz swoją pracę i Utwórz nowy plik w Dropbox tooactivate przepływ pracy.  

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/dropbox/).

## <a name="more-connectors"></a>Więcej łączników
Przejdź wstecz toohello [listy interfejsów API](apis-list.md).
