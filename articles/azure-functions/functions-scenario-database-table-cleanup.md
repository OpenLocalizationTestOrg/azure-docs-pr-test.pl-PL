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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="d8163-103">Użyj usługi Azure Functions tooconnect tooan bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d8163-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="d8163-104">W tym temacie pokazano, jak toocreate usługi Azure Functions toouse zaplanowanego zadania, które utraciły wierszy w tabeli w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d8163-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="d8163-105">Hello nową C# funkcję jest tworzony na podstawie szablonu wyzwalacza czasomierza wstępnie zdefiniowane w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d8163-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="d8163-106">toosupport tego scenariusza, należy także ustawić parametry połączenia bazy danych jako ustawienie w hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8163-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="d8163-107">W tym scenariuszu operacja zbiorcza hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d8163-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="d8163-108">toohave Twojego funkcja procesu poszczególnych operacji CRUD w tabeli Mobile Apps, należy zamiast tego użyć [powiązania Mobile Apps](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d8163-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8163-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d8163-109">Prerequisites</span></span>

+ <span data-ttu-id="d8163-110">W tym temacie funkcja czasomierza wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="d8163-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="d8163-111">Zakończenie hello kroków w temacie hello [Tworzenie funkcji platformy Azure, która jest wyzwalany przez czasomierz](functions-create-scheduled-function.md) wersji toocreate C# tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d8163-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="d8163-112">W tym temacie przedstawiono polecenie języka Transact-SQL, które wykonuje operację czyszczenia zbiorczego hello **SalesOrderHeader** tabeli hello AdventureWorksLT przykładowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8163-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="d8163-113">toocreate hello AdventureWorksLT przykładowej bazy danych, pełną hello kroków w temacie hello [tworzenie bazy danych Azure SQL w portalu Azure hello](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8163-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="d8163-114">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="d8163-114">Get connection information</span></span>

<span data-ttu-id="d8163-115">Wymagane parametry połączenia hello tooget dla hello bazy danych utworzonej po wykonaniu [tworzenie bazy danych Azure SQL w portalu Azure hello](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8163-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="d8163-116">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8163-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="d8163-117">Wybierz **baz danych SQL** z menu po lewej stronie powitania i wybierz bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="d8163-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="d8163-118">Wybierz **Pokaż parametry połączenia bazy danych** i hello Kopiuj pełną **ADO.NET** parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="d8163-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Skopiuj parametry połączenia ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="d8163-120">Ustawianie parametrów połączenia hello</span><span class="sxs-lookup"><span data-stu-id="d8163-120">Set hello connection string</span></span> 

<span data-ttu-id="d8163-121">Aplikacja funkcji obsługuje wykonywanie hello funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d8163-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="d8163-122">Jest najważniejsze parametry połączenia toostore praktyki i innych informacji poufnych, w ustawieniach funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8163-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="d8163-123">Używanie ustawień aplikacji uniemożliwia przypadkowego ujawnienia hello parametry połączenia w kodzie.</span><span class="sxs-lookup"><span data-stu-id="d8163-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="d8163-124">Przejdź do tworzenia aplikacji funkcji tooyour [Tworzenie funkcji platformy Azure, która jest wyzwalany przez czasomierz](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="d8163-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="d8163-125">Wybierz **funkcji platformy** > **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d8163-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Ustawienia aplikacji hello funkcji aplikacji.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="d8163-127">Przewiń w dół za**parametry połączenia** i dodaj ciąg połączenia przy użyciu ustawień hello określoną w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="d8163-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Dodaj ustawienia połączenia ciąg toohello funkcji aplikacji.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="d8163-129">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="d8163-129">Setting</span></span>       | <span data-ttu-id="d8163-130">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="d8163-130">Suggested value</span></span> | <span data-ttu-id="d8163-131">Opis</span><span class="sxs-lookup"><span data-stu-id="d8163-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="d8163-132">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="d8163-132">**Name**</span></span>  |  <span data-ttu-id="d8163-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="d8163-133">sqldb_connection</span></span>  | <span data-ttu-id="d8163-134">Używane tooaccess hello przechowywane parametry połączenia w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="d8163-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="d8163-135">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="d8163-135">**Value**</span></span> | <span data-ttu-id="d8163-136">Ciąg skopiowany</span><span class="sxs-lookup"><span data-stu-id="d8163-136">Copied string</span></span>  | <span data-ttu-id="d8163-137">Poza hello parametry połączenia skopiowane w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d8163-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="d8163-138">**Typ**</span><span class="sxs-lookup"><span data-stu-id="d8163-138">**Type**</span></span> | <span data-ttu-id="d8163-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="d8163-139">SQL Database</span></span> | <span data-ttu-id="d8163-140">Użyj połączenia między hello domyślna baza danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d8163-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="d8163-141">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d8163-141">Click **Save**.</span></span>

<span data-ttu-id="d8163-142">Teraz możesz dodać hello kodu C# funkcja łączącego tooyour bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d8163-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="d8163-143">Zaktualizuj kod — funkcja</span><span class="sxs-lookup"><span data-stu-id="d8163-143">Update your function code</span></span>

1. <span data-ttu-id="d8163-144">W funkcji aplikacji wybierz funkcję wyzwalany przez czasomierz hello.</span><span class="sxs-lookup"><span data-stu-id="d8163-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="d8163-145">Dodaj następujące odwołania do zestawów u góry hello hello istniejącego kodu funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="d8163-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="d8163-146">Dodaj następujące hello `using` instrukcje toohello funkcji:</span><span class="sxs-lookup"><span data-stu-id="d8163-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="d8163-147">Zamień istniejące hello **Uruchom** funkcji z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d8163-147">Replace hello existing **Run** function with hello following code:</span></span>
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

    <span data-ttu-id="d8163-148">To przykładowe polecenie aktualizuje hello **stan** kolumna jest oparta na powitania Data wysyłki.</span><span class="sxs-lookup"><span data-stu-id="d8163-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="d8163-149">Należy ją zaktualizować 32 wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="d8163-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="d8163-150">Kliknij przycisk **zapisać**, obejrzyj hello **dzienniki** systemu windows dla hello obok funkcji wykonywania, a następnie należy zwrócić uwagę hello liczba zaktualizowanych w hello **SalesOrderHeader** tabeli.</span><span class="sxs-lookup"><span data-stu-id="d8163-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Wyświetlać dzienniki funkcji hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="d8163-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8163-152">Next steps</span></span>

<span data-ttu-id="d8163-153">Następnie Dowiedz się, jak działa toouse z toointegrate Logic Apps z innymi usługami.</span><span class="sxs-lookup"><span data-stu-id="d8163-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="d8163-154">Tworzy funkcję, która integruje się z usługą Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d8163-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="d8163-155">Aby uzyskać więcej informacji na temat funkcji zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="d8163-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="d8163-156">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="d8163-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="d8163-157">Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="d8163-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="d8163-158">Testowanie usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d8163-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="d8163-159">Opis różnych narzędzi i technik testowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="d8163-159">Describes various tools and techniques for testing your functions.</span></span>  
