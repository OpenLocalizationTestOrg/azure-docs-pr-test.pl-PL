---
title: "Włączanie automatycznego dostrajania dla usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Można włączyć automatycznego dostrajania bazy danych SQL Azure łatwe."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="2539e-103">Włączanie automatycznego dostrajania</span><span class="sxs-lookup"><span data-stu-id="2539e-103">Enable automatic tuning</span></span>

<span data-ttu-id="2539e-104">Baza danych SQL Azure jest usługą automatycznie zarządzanych danych, która stale monitoruje zapytań i określa działania, które można wykonać, aby poprawić wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2539e-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies the action that you can perform to improve performance of your workload.</span></span> <span data-ttu-id="2539e-105">Możesz przejrzeć zalecenia i ręcznie zastosować je lub pozwól bazy danych SQL Azure automatyczne stosowanie działania naprawcze — jest to nazywane **automatycznego dostrajania tryb**.</span><span class="sxs-lookup"><span data-stu-id="2539e-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="2539e-106">Dostrajanie automatycznej można włączyć na poziomie bazy danych lub serwera.</span><span class="sxs-lookup"><span data-stu-id="2539e-106">Automatic tuning can be enabled at the server or the database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="2539e-107">Włączanie automatycznego dostrajania na serwerze</span><span class="sxs-lookup"><span data-stu-id="2539e-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="2539e-108">Aby włączyć automatyczne dostrajanie na serwerze bazy danych SQL Azure, przejdź do serwera w portalu Azure, a następnie wybierz **automatycznego dostrajania** w menu.</span><span class="sxs-lookup"><span data-stu-id="2539e-108">To enable automatic tuning on Azure SQL Database server, navigate to the server in Azure portal and then select **Automatic tuning** in the menu.</span></span> <span data-ttu-id="2539e-109">Wybierz opcje automatycznego dostrajania chcesz włączyć, a następnie wybierz **Zastosuj**:</span><span class="sxs-lookup"><span data-stu-id="2539e-109">Select the automatic tuning options you want to enable and select **Apply**:</span></span>

![Serwer](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="2539e-111">Opcje automatycznego dostrajania na serwerze są stosowane do wszystkich baz danych na serwerze.</span><span class="sxs-lookup"><span data-stu-id="2539e-111">Automatic tuning options on server are applied to all databases on the server.</span></span> <span data-ttu-id="2539e-112">Domyślnie wszystkie bazy danych dziedziczy konfiguracji z ich nadrzędnego serwera, ale to zastąpione i określić osobno dla każdej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2539e-112">By default, all databases inherit the configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="2539e-113">Konfigurowanie automatycznego dostrajania dla bazy danych</span><span class="sxs-lookup"><span data-stu-id="2539e-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="2539e-114">Azure portal umożliwia niezależnie Określ automatycznego dostrajania konfiguracji w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2539e-114">The Azure portal enables you to individually specify the automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="2539e-115">Ogólne zaleca się zarządzanie automatycznego dostrajania konfiguracji na poziomie serwera, dlatego te same ustawienia konfiguracji mogą być automatycznie stosowane w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2539e-115">The general recommendation is to manage the automatic tuning configuration at server level so the same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="2539e-116">Konfigurowanie automatycznego dostrajania na poszczególne bazy danych, jeśli baza danych jest inny tego inne, na tym samym serwerze.</span><span class="sxs-lookup"><span data-stu-id="2539e-116">Configure automatic tuning on an individual database if the database is different that others on the same server.</span></span>
>

<span data-ttu-id="2539e-117">Aby włączyć automatycznego dostrajania dla jednej bazy danych, przejdź do bazy danych w portalu Azure wybierz a następnie **automatycznego dostrajania**.</span><span class="sxs-lookup"><span data-stu-id="2539e-117">To enable automatic tuning on a single database, navigate to the database in the Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="2539e-118">Można skonfigurować pojedynczy bazy danych, aby odziedziczyć ustawienia z bazy danych, zaznaczając pole wyboru lub konfiguracji bazy danych można określić osobno.</span><span class="sxs-lookup"><span data-stu-id="2539e-118">You can configure a single database to inherit the settings from the database by selecting the checkbox or you can specify the configuration for a database individually.</span></span>

![Database (Baza danych)](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="2539e-120">Po wybraniu odpowiedniej konfiguracji, kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="2539e-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2539e-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2539e-121">Next steps</span></span>
* <span data-ttu-id="2539e-122">Odczyt [automatycznego dostrajania artykułu](sql-database-automatic-tuning.md) Aby dowiedzieć się więcej na temat automatycznego dostrajania i jak go w celu poprawy wydajności.</span><span class="sxs-lookup"><span data-stu-id="2539e-122">Read the [Automatic tuning article](sql-database-automatic-tuning.md) to learn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="2539e-123">Zobacz [zaleceń](sql-database-advisor.md) omówienie zaleceń wydajności bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2539e-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="2539e-124">Zobacz [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) Aby dowiedzieć się więcej o wyświetlaniu wpływu na wydajność kwerend top.</span><span class="sxs-lookup"><span data-stu-id="2539e-124">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>
