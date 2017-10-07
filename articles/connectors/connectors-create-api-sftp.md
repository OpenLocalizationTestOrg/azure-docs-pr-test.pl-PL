---
title: "aaaLearn jak toouse hello SFTP łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz toosend tooSFTP interfejsu API i odbierania plików. Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Rozpoczynanie pracy z hello SFTP łącznika
Użyj hello SFTP łącznika tooaccess toosend konta SFTP uprawnia do plików. Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików.  

toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Połącz tooSFTP
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi. A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.  

### <a name="create-a-connection-toosftp"></a>Tworzenie tooSFTP połączenia
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Użyj wyzwalacz SFTP
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

W tym przykładzie hello **SFTP - podczas dodawania lub modyfikowania pliku** wyzwalacza jest używane tooinitiate przepływu pracy aplikacji logiki, po dodaniu pliku lub zmodyfikowane na serwerze SFTP. Możesz również dodać warunek, który sprawdza hello zawartość pliku nowe lub zmodyfikowane hello i tworzy plik hello tooextract decyzji, jeśli jego zawartość wskazują, że należy wyodrębnić przed użyciem hello zawartość. Na koniec Dodaj akcję tooextract hello zawartość pliku i umieścić w folderze na serwerze SFTP hello hello wyodrębnić zawartość. 

Przykład przedsiębiorstwa można użyć tego wyzwalacza toomonitor folderu SFTP nowych plików, które reprezentują zamówień klienta.  Następnie można użyć akcji łącznika SFTP, takich jak **pobrać zawartość pliku**, zawartość hello tooget hello kolejności dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Dodaj warunek
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Za pomocą akcji SFTP
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Więcej łączników
Przejdź wstecz toohello [listy interfejsów API](apis-list.md).
