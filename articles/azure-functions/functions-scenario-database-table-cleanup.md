---
title: "tooperform usługi Azure Functions aaaUse czyszczenia bazy danych zadań | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Functions tooschedule zadanie, które łączy tooperiodically bazy danych SQL tooAzure wyczyszczenia wierszy."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Użyj usługi Azure Functions tooconnect tooan bazy danych SQL Azure
W tym temacie pokazano, jak toocreate usługi Azure Functions toouse zaplanowanego zadania, które utraciły wierszy w tabeli w bazie danych SQL Azure. Hello nową C# funkcję jest tworzony na podstawie szablonu wyzwalacza czasomierza wstępnie zdefiniowane w hello portalu Azure. toosupport tego scenariusza, należy także ustawić parametry połączenia bazy danych jako ustawienie w hello funkcji aplikacji. W tym scenariuszu operacja zbiorcza hello w bazie danych. toohave Twojego funkcja procesu poszczególnych operacji CRUD w tabeli Mobile Apps, należy zamiast tego użyć [powiązania Mobile Apps](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Wymagania wstępne

+ W tym temacie funkcja czasomierza wyzwolone. Zakończenie hello kroków w temacie hello [Tworzenie funkcji platformy Azure, która jest wyzwalany przez czasomierz](functions-create-scheduled-function.md) wersji toocreate C# tej funkcji.   

+ W tym temacie przedstawiono polecenie języka Transact-SQL, które wykonuje operację czyszczenia zbiorczego hello **SalesOrderHeader** tabeli hello AdventureWorksLT przykładowej bazy danych. toocreate hello AdventureWorksLT przykładowej bazy danych, pełną hello kroków w temacie hello [tworzenie bazy danych Azure SQL w portalu Azure hello](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Pobieranie informacji o połączeniu

Wymagane parametry połączenia hello tooget dla hello bazy danych utworzonej po wykonaniu [tworzenie bazy danych Azure SQL w portalu Azure hello](../sql-database/sql-database-get-started-portal.md).

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
 
3. Wybierz **baz danych SQL** z menu po lewej stronie powitania i wybierz bazę danych na powitania **baz danych SQL** strony.

4. Wybierz **Pokaż parametry połączenia bazy danych** i hello Kopiuj pełną **ADO.NET** parametry połączenia.

    ![Skopiuj parametry połączenia ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Ustawianie parametrów połączenia hello 

Aplikacja funkcji obsługuje wykonywanie hello funkcji na platformie Azure. Jest najważniejsze parametry połączenia toostore praktyki i innych informacji poufnych, w ustawieniach funkcji aplikacji. Używanie ustawień aplikacji uniemożliwia przypadkowego ujawnienia hello parametry połączenia w kodzie. 

1. Przejdź do tworzenia aplikacji funkcji tooyour [Tworzenie funkcji platformy Azure, która jest wyzwalany przez czasomierz](functions-create-scheduled-function.md).

2. Wybierz **funkcji platformy** > **ustawienia aplikacji**.
   
    ![Ustawienia aplikacji hello funkcji aplikacji.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Przewiń w dół za**parametry połączenia** i dodaj ciąg połączenia przy użyciu ustawień hello określoną w tabeli hello.
   
    ![Dodaj ustawienia połączenia ciąg toohello funkcji aplikacji.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Ustawienie       | Sugerowana wartość | Opis             | 
    | ------------ | ------------------ | --------------------- | 
    | **Nazwa**  |  sqldb_connection  | Używane tooaccess hello przechowywane parametry połączenia w kodzie funkcji.    |
    | **Wartość** | Ciąg skopiowany  | Poza hello parametry połączenia skopiowane w poprzedniej sekcji hello. |
    | **Typ** | SQL Database | Użyj połączenia między hello domyślna baza danych SQL. |   

3. Kliknij pozycję **Zapisz**.

Teraz możesz dodać hello kodu C# funkcja łączącego tooyour bazy danych SQL.

## <a name="update-your-function-code"></a>Zaktualizuj kod — funkcja

1. W funkcji aplikacji wybierz funkcję wyzwalany przez czasomierz hello.
 
3. Dodaj następujące odwołania do zestawów u góry hello hello istniejącego kodu funkcji hello:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Dodaj następujące hello `using` instrukcje toohello funkcji:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Zamień istniejące hello **Uruchom** funkcji z hello następującego kodu:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    To przykładowe polecenie aktualizuje hello **stan** kolumna jest oparta na powitania Data wysyłki. Należy ją zaktualizować 32 wierszy danych.

5. Kliknij przycisk **zapisać**, obejrzyj hello **dzienniki** systemu windows dla hello obok funkcji wykonywania, a następnie należy zwrócić uwagę hello liczba zaktualizowanych w hello **SalesOrderHeader** tabeli.

    ![Wyświetlać dzienniki funkcji hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Następne kroki

Następnie Dowiedz się, jak działa toouse z toointegrate Logic Apps z innymi usługami.

> [!div class="nextstepaction"] 
> [Tworzy funkcję, która integruje się z usługą Logic Apps](functions-twitter-email.md)

Aby uzyskać więcej informacji na temat funkcji zobacz następujące tematy hello:

* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)  
  Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.
* [Testowanie usługi Azure Functions](functions-test-a-function.md)  
  Opis różnych narzędzi i technik testowania funkcji.  
