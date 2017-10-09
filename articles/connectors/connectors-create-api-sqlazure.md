---
title: "Łącznik usługi Azure SQL Database hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznika usługi Azure SQL Database z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Rozpoczynanie pracy z łącznika usługi Azure SQL Database hello
Za pomocą łącznika usługi Azure SQL Database hello, tworzyć przepływy pracy dla organizacji zarządzających danych w tabelach. 

Z bazy danych SQL można:

* Tworzenie przepływu pracy przez dodanie nowej bazy danych klientów tooa klientów lub aktualizowanie zamówienia w bazie danych zamówienia.
* Użyj akcji tooget wiersz danych, wstawić nowy wiersz, a nawet usuwać. Na przykład gdy zostaje utworzony rekord w Dynamics CRM Online (wyzwalacz), następnie wstawienia wiersza w bazie danych SQL Azure (działanie). 

W tym temacie pokazano, jak toouse hello łącznika bazy danych SQL w aplikacji logiki, a także list hello akcje.

toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Połącz tooAzure bazy danych SQL
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi. Połączenie stanowi połączenie między aplikacji logiki i innej usługi. Na przykład tooSQL tooconnect bazy danych, należy najpierw utworzyć bazę danych SQL *połączenia*. toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, którą jest nawiązywane zwykle jest używana. Tak w bazie danych SQL, wprowadź połączenie hello toocreate poświadczenia bazy danych SQL. 

#### <a name="create-hello-connection"></a>Utwórz połączenie hello
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Użyć wyzwalacza
Ten łącznik nie ma żadnych wyzwalaczy. Użyj innych wyzwalaczy toostart hello aplikacji logiki, takie jak wyzwalacz cyklu wyzwalacza HTTP elementu Webhook, wyzwalaczy dostępny z innych łączników i inne. [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przykładowego.

## <a name="use-an-action"></a>Za pomocą akcji
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Wybierz znak plus hello. Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Wybierz **Dodaj akcję**.
3. W polu tekstowym hello wpisz "sql" tooget listę wszystkich hello dostępne akcje.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. W tym przykładzie wybierz **SQL Server — wiersz Get**. Jeśli połączenie już istnieje, a następnie wybierz hello **nazwy tabeli** z listy rozwijanej hello listy, a następnie wprowadź hello **identyfikator wiersza** ma tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia. [Utwórz połączenie hello](connectors-create-api-sqlazure.md#create-the-connection) w tym temacie opisano te właściwości. 
   
   > [!NOTE]
   > W tym przykładzie zostanie zwrócona wiersz z tabeli. toosee hello dane w tym wierszu, Dodaj inną akcję, która tworzy plik za pomocą hello pola z tabeli hello. Na przykład dodać akcję OneDrive, która używa hello imię i nazwisko pola toocreate nowy plik w hello konta magazynu w chmurze. 
   > 
   > 
5. **Zapisz** zmiany (lewym górnym rogu paska narzędzi hello). Aplikację logiki jest zapisywana i automatycznie włączone.

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/sql/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).

