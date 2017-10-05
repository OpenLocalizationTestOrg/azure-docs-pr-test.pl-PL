---
title: "Użyj usługi Azure Functions do wykonania zadania oczyszczania bazy danych | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Functions można zaplanować zadanie, które łączy się z bazą danych SQL Azure, aby okresowo wyczyszczenia wierszy."
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="e6468-103">Nawiązywanie połączenia z bazy danych SQL Azure za pomocą usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e6468-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="e6468-104">W tym temacie przedstawiono sposób użycia usługi Azure Functions można utworzyć zaplanowane zadanie, które utraciły wierszy w tabeli w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e6468-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="e6468-105">Nowa funkcja C# jest tworzony na podstawie szablonu wyzwalacza czasomierza wstępnie zdefiniowane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e6468-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="e6468-106">Aby zapewnić obsługę tego scenariusza, należy także ustawić parametry połączenia bazy danych jako ustawienie w funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e6468-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="e6468-107">W tym scenariuszu operacja zbiorcza w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e6468-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="e6468-108">Aby funkcja przetworzyć poszczególnych operacji CRUD w tabeli Mobile Apps, zamiast tego należy używać [powiązania Mobile Apps](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="e6468-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6468-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6468-109">Prerequisites</span></span>

+ <span data-ttu-id="e6468-110">W tym temacie funkcja czasomierza wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="e6468-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="e6468-111">Wykonaj kroki w temacie [Tworzenie funkcji platformy Azure, która jest wyzwalany przez czasomierz](functions-create-scheduled-function.md) tworzenia wersji języka C# tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6468-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="e6468-112">W tym temacie przedstawiono polecenie języka Transact-SQL, które wykonuje operację czyszczenia zbiorczego w **SalesOrderHeader** tabeli w bazie danych AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="e6468-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="e6468-113">Aby utworzyć przykładową bazę danych AdventureWorksLT, wykonaj czynności opisane w temacie [tworzenie bazy danych Azure SQL w portalu Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6468-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="e6468-114">Pobieranie informacji o połączeniu</span><span class="sxs-lookup"><span data-stu-id="e6468-114">Get connection information</span></span>

<span data-ttu-id="e6468-115">Należy pobrać parametry połączenia dla bazy danych utworzonej po wykonaniu [tworzenie bazy danych Azure SQL w portalu Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6468-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="e6468-116">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e6468-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="e6468-117">Wybierz **baz danych SQL** z menu po lewej stronie i wybierz bazę danych na **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="e6468-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="e6468-118">Wybierz **Pokaż parametry połączenia bazy danych** i skopiować pełną **ADO.NET** parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="e6468-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Skopiuj parametry połączenia ADO.NET.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="e6468-120">Ustawianie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="e6468-120">Set the connection string</span></span> 

<span data-ttu-id="e6468-121">Aplikacja funkcji obsługuje wykonywanie funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e6468-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="e6468-122">Jest najlepszym rozwiązaniem jest przechowywanie parametrów połączenia i innych informacji poufnych w ustawieniach funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e6468-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="e6468-123">Używanie ustawień aplikacji uniemożliwia przypadkowego ujawnienia parametrów połączenia w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e6468-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="e6468-124">Przejdź do tworzenia aplikacji funkcji [Tworzenie funkcji platformy Azure, która jest wyzwalany przez czasomierz](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="e6468-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="e6468-125">Wybierz **funkcji platformy** > **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e6468-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Ustawienia aplikacji dla aplikacji funkcja.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="e6468-127">Przewiń w dół do **parametry połączenia** i dodaj ciąg połączenia przy użyciu ustawień określonych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="e6468-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Dodaj parametry połączenia w ustawieniach aplikacji funkcji.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="e6468-129">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="e6468-129">Setting</span></span>       | <span data-ttu-id="e6468-130">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="e6468-130">Suggested value</span></span> | <span data-ttu-id="e6468-131">Opis</span><span class="sxs-lookup"><span data-stu-id="e6468-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="e6468-132">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="e6468-132">**Name**</span></span>  |  <span data-ttu-id="e6468-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="e6468-133">sqldb_connection</span></span>  | <span data-ttu-id="e6468-134">Umożliwia dostęp do parametrów połączenia przechowywanych w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6468-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="e6468-135">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="e6468-135">**Value**</span></span> | <span data-ttu-id="e6468-136">Ciąg skopiowany</span><span class="sxs-lookup"><span data-stu-id="e6468-136">Copied string</span></span>  | <span data-ttu-id="e6468-137">Poza parametry połączenia skopiowane w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e6468-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="e6468-138">**Typ**</span><span class="sxs-lookup"><span data-stu-id="e6468-138">**Type**</span></span> | <span data-ttu-id="e6468-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="e6468-139">SQL Database</span></span> | <span data-ttu-id="e6468-140">Użyj domyślnego połączenia bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="e6468-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="e6468-141">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e6468-141">Click **Save**.</span></span>

<span data-ttu-id="e6468-142">Teraz można dodać kod funkcji języka C#, który nawiązuje połączenie z bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="e6468-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="e6468-143">Zaktualizuj kod — funkcja</span><span class="sxs-lookup"><span data-stu-id="e6468-143">Update your function code</span></span>

1. <span data-ttu-id="e6468-144">W funkcji aplikacji wybierz funkcję wyzwalany przez czasomierz.</span><span class="sxs-lookup"><span data-stu-id="e6468-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="e6468-145">Dodaj następujące odwołania do zestawów w górnej części istniejącego kodu funkcji:</span><span class="sxs-lookup"><span data-stu-id="e6468-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="e6468-146">Dodaj następujące `using` instrukcje funkcji:</span><span class="sxs-lookup"><span data-stu-id="e6468-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="e6468-147">Zastąp istniejące **Uruchom** funkcja następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="e6468-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="e6468-148">To przykładowe polecenie aktualizuje **stan** kolumna jest oparta na daty.</span><span class="sxs-lookup"><span data-stu-id="e6468-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="e6468-149">Należy ją zaktualizować 32 wierszy danych.</span><span class="sxs-lookup"><span data-stu-id="e6468-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="e6468-150">Kliknij przycisk **zapisać**, obejrzyj **dzienniki** windows Następna funkcja wykonywania, a następnie zanotuj liczbę wierszy zaktualizowane w **SalesOrderHeader** tabeli.</span><span class="sxs-lookup"><span data-stu-id="e6468-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Wyświetlać dzienniki funkcji.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="e6468-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6468-152">Next steps</span></span>

<span data-ttu-id="e6468-153">Następnie Dowiedz się, jak za pomocą funkcji aplikacji logiki do integracji z innymi usługami.</span><span class="sxs-lookup"><span data-stu-id="e6468-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="e6468-154">Tworzy funkcję, która integruje się z usługą Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e6468-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="e6468-155">Aby uzyskać więcej informacji na temat funkcji zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="e6468-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="e6468-156">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="e6468-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="e6468-157">Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="e6468-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="e6468-158">Testowanie usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e6468-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="e6468-159">Opis różnych narzędzi i technik testowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6468-159">Describes various tools and techniques for testing your functions.</span></span>  
