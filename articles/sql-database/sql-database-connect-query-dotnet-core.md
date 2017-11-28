---
title: aaaUse .NET Core tooquery bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "W tym temacie przedstawiono sposób toouse .NET Core toocreate program, który łączy tooan bazy danych SQL Azure i zapytania za pomocą instrukcji języka Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="caa44-103">Użyj tooquery .NET Core (C#) bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="caa44-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="caa44-104">Tego samouczka szybkiego startu przedstawia sposób toouse [.NET Core](https://www.microsoft.com/net/) na Windows/Linux/macOS toocreate C# program tooconnect tooan Azure SQL bazy danych, a następnie użyć danych tooquery instrukcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="caa44-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caa44-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="caa44-105">Prerequisites</span></span>

<span data-ttu-id="caa44-106">toocomplete tym szybki start samouczka, upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="caa44-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="caa44-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="caa44-107">An Azure SQL database.</span></span> <span data-ttu-id="caa44-108">To szybki start używa zasobów hello tworzony w jednej z tych Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="caa44-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="caa44-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="caa44-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="caa44-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="caa44-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="caa44-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="caa44-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="caa44-112">A [regułę zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla hello publiczny adres IP komputera hello, możesz użyć w tym samouczku szybki start.</span><span class="sxs-lookup"><span data-stu-id="caa44-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="caa44-113">W systemie operacyjnym zainstalowano platformę [.NET Core](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="caa44-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="caa44-114">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="caa44-114">SQL server connection information</span></span>

<span data-ttu-id="caa44-115">Pobierz hello połączenia potrzebnych tooconnect toohello usługa Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="caa44-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="caa44-116">Konieczne będzie hello pełni kwalifikowaną nazwę serwera, nazwa bazy danych i informacji o logowaniu w hello kolejnych procedur.</span><span class="sxs-lookup"><span data-stu-id="caa44-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="caa44-117">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="caa44-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="caa44-118">Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.</span><span class="sxs-lookup"><span data-stu-id="caa44-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="caa44-119">Na powitania **omówienie** stron dla bazy danych, przejrzyj hello w pełni kwalifikowana nazwa serwera, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="caa44-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="caa44-120">Ustawieniu kursora toobring nazwy serwera hello zapasowej hello **kliknij toocopy** opcji.</span><span class="sxs-lookup"><span data-stu-id="caa44-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="caa44-122">Jeśli użytkownik zapomni swoje informacje logowania serwera bazy danych SQL Azure, przejdź toohello bazy danych SQL strony tooview powitania serwera nazwa administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="caa44-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="caa44-123">Jeśli to konieczne, można zresetować hasła hello.</span><span class="sxs-lookup"><span data-stu-id="caa44-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="caa44-124">Kliknij pozycję **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="caa44-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="caa44-125">Przejrzyj hello pełną **ADO.NET** parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="caa44-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Parametry połączenia sterownika ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="caa44-127">W przypadku hello publiczny adres IP komputera hello, na którym jest wykonywana w tym samouczku, musi mieć reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="caa44-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="caa44-128">Jeśli na innym komputerze lub inny publiczny adres IP, należy utworzyć [reguły zapory poziomu serwera przy użyciu hello portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="caa44-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="caa44-129">Tworzenie nowego projektu .NET</span><span class="sxs-lookup"><span data-stu-id="caa44-129">Create a new .NET project</span></span>

1. <span data-ttu-id="caa44-130">Otwórz wiersz polecenia i utwórz folder o nazwie *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="caa44-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="caa44-131">Przejdź toohello folder utworzony i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="caa44-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="caa44-132">Otwórz ***sqltest.csproj*** o w ulubionym edytorze tekstów i Dodaj System.Data.SqlClient jako zależność przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="caa44-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="caa44-133">Wstaw baza danych SQL tooquery kodu</span><span class="sxs-lookup"><span data-stu-id="caa44-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="caa44-134">W środowisku projektowym lub ulubionym edytorze tekstów utwórz nowy plik o nazwie **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="caa44-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="caa44-135">Zamień zawartość hello hello następujący kod i dodaj odpowiednie wartości powitania serwera, bazy danych, użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="caa44-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="caa44-136">Uruchamianie hello kodu</span><span class="sxs-lookup"><span data-stu-id="caa44-136">Run hello code</span></span>

1. <span data-ttu-id="caa44-137">W wierszu polecenia hello uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="caa44-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="caa44-138">Sprawdź, czy górnych wierszy 20 hello są zwracane, a następnie zamknij okno aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="caa44-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="caa44-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="caa44-139">Next steps</span></span>

- <span data-ttu-id="caa44-140">[Rozpoczynanie pracy z platformą .NET Core na Windows/Linux/macOS przy użyciu wiersza polecenia hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="caa44-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="caa44-141">Dowiedz się, jak za[połączenia i wykonywać zapytania bazy danych Azure SQL przy użyciu hello .NET framework i Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="caa44-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="caa44-142">Dowiedz się, jak za[projektowania pierwszą bazę danych Azure SQL przy użyciu narzędzia SSMS](sql-database-design-first-database.md) lub [projektowania pierwszą bazę danych Azure SQL przy użyciu platformy .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="caa44-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="caa44-143">Aby uzyskać więcej informacji na temat platformy .NET, zobacz [.NET documentation](https://docs.microsoft.com/dotnet/) (Dokumentacja platformy .NET).</span><span class="sxs-lookup"><span data-stu-id="caa44-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
