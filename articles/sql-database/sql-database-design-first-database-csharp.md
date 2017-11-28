---
title: aaaDesign Twojego pierwszego bazy danych SQL Azure - C# | Dokumentacja firmy Microsoft
description: "Dowiedz się toodesign pierwszą bazę danych Azure SQL i połącz tooit za pomocą programu C# za pomocą ADO.NET."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="afb6d-103">Projekt bazy danych Azure SQL i Połącz z C & #x23; i ADO.NET</span><span class="sxs-lookup"><span data-stu-id="afb6d-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="afb6d-104">Baza danych SQL Azure to relacyjnej bazy danych — jako a usługa (DBaaS) w hello Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="afb6d-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="afb6d-105">Z tego samouczka dowiesz się, jak toouse hello portalu Azure i ADO.NET z programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="afb6d-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="afb6d-106">Utwórz bazę danych w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="afb6d-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="afb6d-107">Skonfiguruj regułę zapory poziomu serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="afb6d-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="afb6d-108">Uzyskuj dostęp do bazy danych toohello ADO.NET i Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afb6d-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="afb6d-109">Tworzenie tabel z ADO.NET</span><span class="sxs-lookup"><span data-stu-id="afb6d-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="afb6d-110">Wstawianie, aktualizowanie i usuwanie danych za pomocą ADO.NET</span><span class="sxs-lookup"><span data-stu-id="afb6d-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="afb6d-111">Zapytania na danych ADO.NET</span><span class="sxs-lookup"><span data-stu-id="afb6d-111">Query data ADO.NET</span></span>

<span data-ttu-id="afb6d-112">Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="afb6d-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afb6d-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afb6d-113">Prerequisites</span></span>

<span data-ttu-id="afb6d-114">Zainstalowany program [Visual Studio Community 2017, Visual Studio Professional 2017 lub Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="afb6d-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="afb6d-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afb6d-115">Next steps</span></span>

<span data-ttu-id="afb6d-116">W tym samouczku przedstawiono bazy danych podstawowych zadań takich jak utworzyć bazę danych i tabele, załadować zapytania na danych i przywrócić hello bazy danych tooa wcześniejszego punktu w czasie.</span><span class="sxs-lookup"><span data-stu-id="afb6d-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="afb6d-117">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="afb6d-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="afb6d-118">Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="afb6d-118">Create a database</span></span>
> * <span data-ttu-id="afb6d-119">Konfigurowanie reguł zapory</span><span class="sxs-lookup"><span data-stu-id="afb6d-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="afb6d-120">Połączenia bazy danych toohello z [i Visual Studio C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="afb6d-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="afb6d-121">Tworzenie tabel</span><span class="sxs-lookup"><span data-stu-id="afb6d-121">Create tables</span></span>
> * <span data-ttu-id="afb6d-122">Wstawianie, aktualizowanie i usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="afb6d-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="afb6d-123">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="afb6d-123">Query data</span></span>

<span data-ttu-id="afb6d-124">Przejdź dalej toolearn samouczka toohello o migracji danych.</span><span class="sxs-lookup"><span data-stu-id="afb6d-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="afb6d-125">Migrowanie tooAzure bazy danych programu SQL Server bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="afb6d-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

