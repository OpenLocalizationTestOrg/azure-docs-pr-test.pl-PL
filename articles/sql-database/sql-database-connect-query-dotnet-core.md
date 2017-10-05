---
title: "Korzystanie z platformy .NET Core do wykonywania zapytań w usłudze Azure SQL Database | Microsoft Docs"
description: "W tym temacie przedstawiono sposób wykorzystania platformy .NET Core do utworzenia programu, który nawiązuje połączenie z bazą danych Azure SQL Database i wykonuje zapytania za pomocą instrukcji języka Transact-SQL."
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
ms.openlocfilehash: 046322624d3b89bb983acee863534256fee94b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-core-c-to-query-an-azure-sql-database"></a><span data-ttu-id="73082-103">Korzystanie z platformy .NET Core (C#) do wykonywania zapytań w bazie danych Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="73082-103">Use .NET Core (C#) to query an Azure SQL database</span></span>

<span data-ttu-id="73082-104">W tym przewodniku Szybki start pokazano, jak używać platformy [.NET Core](https://www.microsoft.com/net/) w systemach operacyjnych Windows/Linux/macOS w celu utworzenia programu w języku C# służącego do nawiązywania połączenia z bazą danych Azure SQL Database, a następnie, korzystając z instrukcji Transact-SQL, wysyłać zapytania o dane.</span><span class="sxs-lookup"><span data-stu-id="73082-104">This quick start tutorial demonstrates how to use [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS to create a C# program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73082-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="73082-105">Prerequisites</span></span>

<span data-ttu-id="73082-106">Aby ukończyć ten samouczek Szybki start, upewnij się, że dysponujesz następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="73082-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="73082-107">Baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="73082-107">An Azure SQL database.</span></span> <span data-ttu-id="73082-108">Ten przewodnik Szybki start używa zasobów utworzonych w jednym z poniższych przewodników Szybki start:</span><span class="sxs-lookup"><span data-stu-id="73082-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="73082-109">Tworzenie bazy danych — portal</span><span class="sxs-lookup"><span data-stu-id="73082-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="73082-110">Tworzenie bazy danych — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="73082-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="73082-111">Tworzenie bazy danych — PowerShell</span><span class="sxs-lookup"><span data-stu-id="73082-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="73082-112">[Reguła zapory poziomu serwera](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) dla publicznego adresu IP komputera, który będzie używany w tym samouczku Szybki start.</span><span class="sxs-lookup"><span data-stu-id="73082-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="73082-113">W systemie operacyjnym zainstalowano platformę [.NET Core](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="73082-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="73082-114">Informacje o połączeniu z serwerem SQL</span><span class="sxs-lookup"><span data-stu-id="73082-114">SQL server connection information</span></span>

<span data-ttu-id="73082-115">Uzyskaj parametry połączenia potrzebne do nawiązania połączenia z bazą danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="73082-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="73082-116">W następnych procedurach będą potrzebne w pełni kwalifikowana nazwa serwera, nazwa bazy danych i informacje logowania.</span><span class="sxs-lookup"><span data-stu-id="73082-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="73082-117">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="73082-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="73082-118">Wybierz opcję **Bazy danych SQL** z menu po lewej stronie, a następnie kliknij bazę danych na stronie **Bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="73082-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="73082-119">Na stronie **Przegląd** bazy danych zweryfikuj w pełni kwalifikowaną nazwę serwera, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="73082-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="73082-120">Możesz umieścić kursor na nazwie serwera w celu wywołania opcji **Kliknij, aby skopiować**.</span><span class="sxs-lookup"><span data-stu-id="73082-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![nazwa-serwera](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="73082-122">Jeśli nie pamiętasz informacji logowania dla serwera Azure SQL Database, przejdź do strony serwera SQL Database, aby wyświetlić nazwę administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="73082-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="73082-123">W razie potrzeby zresetuj hasło.</span><span class="sxs-lookup"><span data-stu-id="73082-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="73082-124">Kliknij pozycję **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="73082-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="73082-125">Sprawdź pełne parametry połączenia sterownika **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="73082-125">Review the complete **ADO.NET** connection string.</span></span>

    ![Parametry połączenia sterownika ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="73082-127">W przypadku publicznego adresu IP komputera, na którym jest wykonywany ten samouczek, niezbędne jest posiadanie reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="73082-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="73082-128">Jeśli pracujesz na innym komputerze lub masz inny publiczny adres IP, utwórz [regułę zapory poziomu serwera przy użyciu portalu Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="73082-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="73082-129">Tworzenie nowego projektu .NET</span><span class="sxs-lookup"><span data-stu-id="73082-129">Create a new .NET project</span></span>

1. <span data-ttu-id="73082-130">Otwórz wiersz polecenia i utwórz folder o nazwie *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="73082-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="73082-131">Przejdź do utworzonego folderu i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="73082-131">Navigate to the folder you created and run the following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="73082-132">Otwórz plik ***sqltest.csproj*** w ulubionym edytorze tekstów i dodaj pozycję System.Data.SqlClient jako zależność, używając następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="73082-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using the following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="73082-133">Wstawianie kodu zapytania bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="73082-133">Insert code to query SQL database</span></span>

1. <span data-ttu-id="73082-134">W środowisku projektowym lub ulubionym edytorze tekstów utwórz nowy plik o nazwie **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="73082-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="73082-135">Zastąp jego zawartość następującym kodem i dodaj odpowiednie wartości dla serwera, bazy danych, użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="73082-135">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="73082-136">Uruchamianie kodu</span><span class="sxs-lookup"><span data-stu-id="73082-136">Run the code</span></span>

1. <span data-ttu-id="73082-137">W wierszu polecenia uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="73082-137">At the command prompt, run the following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="73082-138">Sprawdź, czy zostało zwróconych 20 pierwszych wierszy, a następnie zamknij okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73082-138">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="73082-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73082-139">Next steps</span></span>

- <span data-ttu-id="73082-140">[Rozpoczynanie pracy z platformą .NET Core w systemie Windows/Linux/macOS przy użyciu wiersza polecenia](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="73082-140">[Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="73082-141">Dowiedz się, jak [uzyskać połączenie i wykonywać zapytania bazy danych Azure SQL przy użyciu platformy .NET i programu Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="73082-141">Learn how to [connect and query an Azure SQL database using the .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="73082-142">Dowiedz się, jak [zaprojektować pierwszą bazę danych Azure SQL przy użyciu narzędzia SSMS](sql-database-design-first-database.md) lub [zaprojektować pierwszą bazę danych Azure SQL przy użyciu platformy .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="73082-142">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="73082-143">Aby uzyskać więcej informacji na temat platformy .NET, zobacz [.NET documentation](https://docs.microsoft.com/dotnet/) (Dokumentacja platformy .NET).</span><span class="sxs-lookup"><span data-stu-id="73082-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
