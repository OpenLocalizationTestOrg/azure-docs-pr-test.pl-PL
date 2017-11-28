---
title: "narzędzia sqlcmd SQL Data Warehouse tooAzure aaaConnect | Dokumentacja firmy Microsoft"
description: "Użyj [sqlcmd] [sqlcmd] narzędzie wiersza polecenia tooconnect tooand zapytania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="b8200-103">Połącz tooSQL hurtowni danych przy użyciu narzędzia sqlcmd</span><span class="sxs-lookup"><span data-stu-id="b8200-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8200-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="b8200-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="b8200-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b8200-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="b8200-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8200-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="b8200-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="b8200-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="b8200-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="b8200-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="b8200-109">Użyj [sqlcmd] [ sqlcmd] tooand tooconnect narzędzia wiersza polecenia zapytań usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b8200-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="b8200-110">1. Połączenie</span><span class="sxs-lookup"><span data-stu-id="b8200-110">1. Connect</span></span>
<span data-ttu-id="b8200-111">wprowadzenie tooget [sqlcmd][sqlcmd], otwórz wiersz polecenia hello i wprowadź **sqlcmd** następuje hello parametry połączenia bazy danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b8200-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="b8200-112">Parametry połączenia Hello wymaga hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="b8200-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="b8200-113">**Serwer (-S):** serwera w formie hello `<`nazwy serwera`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="b8200-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="b8200-114">**Baza danych (-d):** nazwa bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b8200-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="b8200-115">**Włącz cytowane identyfikatory (-I):** cytowane identyfikatory musi być wystąpieniem usługi SQL Data Warehouse tooa tooconnect włączone.</span><span class="sxs-lookup"><span data-stu-id="b8200-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="b8200-116">toouse uwierzytelniania programu SQL Server, należy tooadd hello nazwy użytkownika i hasła parametry:</span><span class="sxs-lookup"><span data-stu-id="b8200-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="b8200-117">**Użytkownik (-U):** użytkownik serwera w formie hello `<`użytkownika`>`</span><span class="sxs-lookup"><span data-stu-id="b8200-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="b8200-118">**Hasło (-P):** hasło skojarzone z hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b8200-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="b8200-119">Na przykład ciąg połączenia może wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b8200-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="b8200-120">Azure Active Directory Integrated authentication toouse, należy tooadd hello Azure Active Directory parametry:</span><span class="sxs-lookup"><span data-stu-id="b8200-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="b8200-121">**Uwierzytelnianie usługi Azure Active Directory (-G):** używaj usługi Azure Active Directory do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b8200-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="b8200-122">Na przykład ciąg połączenia może wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b8200-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="b8200-123">Należy zbyt[Włącz uwierzytelnianie usługi Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate przy użyciu usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8200-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="b8200-124">2. Zapytanie</span><span class="sxs-lookup"><span data-stu-id="b8200-124">2. Query</span></span>
<span data-ttu-id="b8200-125">Po połączeniu można wystawiać żadnych obsługiwane instrukcje języka Transact-SQL przed wystąpieniem hello.</span><span class="sxs-lookup"><span data-stu-id="b8200-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="b8200-126">W tym przykładzie zapytania są przesyłane w trybie interaktywnym.</span><span class="sxs-lookup"><span data-stu-id="b8200-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="b8200-127">Pokazują powyższe przykłady dalej sposób wykonywania zapytań w trybie wsadowym przy użyciu opcji -Q hello lub przekazanie w potoku toosqlcmd Twojego SQL.</span><span class="sxs-lookup"><span data-stu-id="b8200-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="b8200-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8200-128">Next steps</span></span>
<span data-ttu-id="b8200-129">Zobacz [dokumentacji narzędzia sqlcmd] [ sqlcmd] więcej informacji o szczegółowe informacje o hello opcje dostępne w przypadku użycia programu sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="b8200-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
