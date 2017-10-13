---
title: "Informacje o sposobie korzystania z łącznika SFTP w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połączyć z interfejsem API SFTP do wysyłania i odbierania plików. Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików."
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
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a>Rozpoczynanie pracy z łącznikiem SFTP
Użyj konektora SFTP dostępu do konta SFTP do wysyłania i odbierania plików. Można wykonywać różne operacje, takie jak tworzenie, aktualizowanie, Pobierz i usuwania plików.  

Aby użyć [każdy łącznik](apis-list.md), należy najpierw utworzyć aplikację logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-to-sftp"></a>Nawiązać połączenia z użyciem protokołu SFTP
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi. A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.  

### <a name="create-a-connection-to-sftp"></a>Utwórz połączenie z użyciem protokołu SFTP
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Użyj wyzwalacz SFTP
Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

W tym przykładzie **SFTP - podczas dodawania lub modyfikowania pliku** wyzwalacza jest używane do inicjowania przepływu pracy aplikacji logiki, gdy plik zostanie dodany do lub zmodyfikowane na serwerze SFTP. Możesz również dodać warunek, który sprawdza zawartość pliku nowe lub zmodyfikowane i podejmuje decyzję, aby wyodrębnić plik, jeśli jego zawartość wskazują, że należy wyodrębnić przed rozpoczęciem korzystania z zawartości. Na koniec Dodaj akcję w celu wyodrębnienia zawartości pliku i umieścić w folderze na serwerze SFTP wyodrębniona zawartość. 

W przykładzie przedsiębiorstwa może użyć tego wyzwalacza do monitorowania folderu SFTP dla nowych plików, które reprezentują zamówień klienta.  Następnie można użyć akcji łącznika SFTP, takich jak **pobrać zawartość pliku**, aby pobrać zawartość kolejność dla dalszego przetwarzania i przechowywania w bazie danych zamówienia.

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Dodaj warunek
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Za pomocą akcji SFTP
Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Więcej łączników
Wróć do [listy interfejsów API](apis-list.md).