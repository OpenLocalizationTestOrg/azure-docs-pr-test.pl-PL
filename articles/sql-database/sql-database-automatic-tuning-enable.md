---
title: "aaaEnable automatycznego dostrajania dla usługi Azure SQL Database | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="97213-103">Włączanie automatycznego dostrajania</span><span class="sxs-lookup"><span data-stu-id="97213-103">Enable automatic tuning</span></span>

<span data-ttu-id="97213-104">Baza danych SQL Azure jest usługą automatycznie zarządzanych danych, która stale monitoruje zapytań i identyfikuje akcji hello wykonanie tooimprove wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="97213-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="97213-105">Możesz przejrzeć zalecenia i ręcznie zastosować je lub pozwól bazy danych SQL Azure automatyczne stosowanie działania naprawcze — jest to nazywane **automatycznego dostrajania tryb**.</span><span class="sxs-lookup"><span data-stu-id="97213-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="97213-106">Dostrajanie automatycznego można włączyć na poziomie bazy danych hello lub powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="97213-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="97213-107">Włączanie automatycznego dostrajania na serwerze</span><span class="sxs-lookup"><span data-stu-id="97213-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="97213-108">tooenable automatycznego dostrajania na serwerze bazy danych SQL Azure, przejdź toohello server na platformie Azure w portalu, a następnie wybierz opcję **automatycznego dostrajania** hello menu.</span><span class="sxs-lookup"><span data-stu-id="97213-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="97213-109">Wybierz hello automatycznego dostrajania opcje tooenable a wybierz **Zastosuj**:</span><span class="sxs-lookup"><span data-stu-id="97213-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Serwer](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="97213-111">Automatycznego dostrajania opcji na serwerze są baz danych tooall zastosowane na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="97213-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="97213-112">Domyślnie wszystkie bazy danych odziedziczyć konfiguracji hello z ich nadrzędnego serwera, ale to zastąpione i określić osobno dla każdej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="97213-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="97213-113">Konfigurowanie automatycznego dostrajania dla bazy danych</span><span class="sxs-lookup"><span data-stu-id="97213-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="97213-114">Hello Azure umożliwia portalu tooindividually możesz określić hello automatycznego dostrajania konfiguracji w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="97213-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="97213-115">Ogólne zalecenie Hello jest toomanage hello automatycznego dostrajania konfiguracji na poziomie serwera tak hello tych samych ustawień konfiguracji mogą być automatycznie stosowane w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="97213-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="97213-116">Konfigurowanie automatycznego dostrajania dla poszczególnych bazy danych, gdy hello bazy danych jest inny, że hello inne, na tym samym serwerze.</span><span class="sxs-lookup"><span data-stu-id="97213-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="97213-117">bazy danych toohello w hello portalu Azure Przejdź tooenable automatycznego dostrajania dla jednej bazy danych, a następnie i wybierz **automatycznego dostrajania**.</span><span class="sxs-lookup"><span data-stu-id="97213-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="97213-118">Można skonfigurować ustawienia hello tooinherit pojedynczej bazy danych z bazy danych hello zaznaczając pole wyboru hello lub hello konfiguracji bazy danych można określić osobno.</span><span class="sxs-lookup"><span data-stu-id="97213-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Database (Baza danych)](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="97213-120">Po wybraniu odpowiedniej konfiguracji, kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="97213-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97213-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97213-121">Next steps</span></span>
* <span data-ttu-id="97213-122">Witaj odczytu [automatycznego dostrajania artykułu](sql-database-automatic-tuning.md) toolearn więcej informacji na temat automatycznego dostrajania i jak go w celu poprawy wydajności.</span><span class="sxs-lookup"><span data-stu-id="97213-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="97213-123">Zobacz [zaleceń](sql-database-advisor.md) omówienie zaleceń wydajności bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="97213-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="97213-124">Zobacz [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) toolearn o wyświetlaniu hello wpływ na wydajność kwerend top.</span><span class="sxs-lookup"><span data-stu-id="97213-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
