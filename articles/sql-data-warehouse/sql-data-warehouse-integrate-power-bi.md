---
title: "Użyj usługi Power BI z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z usługi Power BI z usługą Magazyn danych SQL Azure związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="d002f-103">Użyj usługi Power BI z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="d002f-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="d002f-104">Jako z bazy danych SQL Azure SQL danych magazynu bezpośrednie połączenie umożliwia użytkownikom korzystać z zaawansowanych przekazywanie logicznej obok możliwości analityczne usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="d002f-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="d002f-105">Za pomocą bezpośrednich Connect zapytania są wysyłane do usługi Azure SQL Data Warehouse w czasie rzeczywistym Ci poznać platformę danych.</span><span class="sxs-lookup"><span data-stu-id="d002f-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="d002f-106">Połączone, skali usługi SQL Data Warehouse umożliwia użytkownikom tworzenie dynamicznych raportów w minutach przed terabajtów danych.</span><span class="sxs-lookup"><span data-stu-id="d002f-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="d002f-107">Ponadto wprowadzenie przycisku Otwórz w usłudze Power BI umożliwia użytkownikom bezpośrednio z usługi Power BI bez zbierania informacji z innych części Azure ich SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d002f-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="d002f-108">Podczas używania połączenia bezpośredniego należy Uwaga:</span><span class="sxs-lookup"><span data-stu-id="d002f-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="d002f-109">Określ nazwę FQDN serwera podczas łączenia z (Aby uzyskać więcej informacji zobacz poniżej)</span><span class="sxs-lookup"><span data-stu-id="d002f-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="d002f-110">Upewnij się, że reguły zapory dla bazy danych są skonfigurowane do "Zezwalaj na dostęp do usług platformy Azure".</span><span class="sxs-lookup"><span data-stu-id="d002f-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="d002f-111">Wszystkie akcje, takich jak wybierając kolumnę lub Dodawanie filtru bezpośrednio wysyła kwerendy do magazynu danych</span><span class="sxs-lookup"><span data-stu-id="d002f-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="d002f-112">Kafelki są odświeżane co około 15 minut (odświeżania nie są wymagane do zaplanowania)</span><span class="sxs-lookup"><span data-stu-id="d002f-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="d002f-113">Funkcja pytania i odpowiedzi nie jest dostępna dla bezpośrednie łączenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="d002f-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="d002f-114">Zmiany schematu nie są odczytywane automatycznie</span><span class="sxs-lookup"><span data-stu-id="d002f-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="d002f-115">Wszystkie zapytania bezpośredniego połączenia limit czasu będzie 2 minuty</span><span class="sxs-lookup"><span data-stu-id="d002f-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="d002f-116">Te ograniczenia i uwagi może zmienić będziemy kontynuować proces ulepszania procesy.</span><span class="sxs-lookup"><span data-stu-id="d002f-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="d002f-117">Czynności, aby podłączyć szczegóły są przedstawione poniżej.</span><span class="sxs-lookup"><span data-stu-id="d002f-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="d002f-118">Przy użyciu przycisku "Otwórz w usłudze Power BI"</span><span class="sxs-lookup"><span data-stu-id="d002f-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="d002f-119">Najprostszym sposobem przenoszenia między magazyn danych SQL i usługi Power BI jest otwarty w usłudze Power BI przycisku.</span><span class="sxs-lookup"><span data-stu-id="d002f-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="d002f-120">Ten przycisk pozwala na łatwe rozpocząć tworzenie nowych pulpitów nawigacyjnych w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="d002f-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="d002f-121">Aby rozpocząć przejdź do Twojego wystąpienia usługi SQL Data Warehouse w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d002f-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="d002f-122">Kliknij przycisk „Otwórz w usłudze Power BI”.</span><span class="sxs-lookup"><span data-stu-id="d002f-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="d002f-123">Jeśli nie możemy zalogować Cię bezpośrednio lub jeśli nie masz konta usługi Power BI, należy się zalogować.</span><span class="sxs-lookup"><span data-stu-id="d002f-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="d002f-124">Nastąpi przekierowanie do strony połączenie SQL Data Warehouse przy użyciu informacji z usługą SQL Data Warehouse wstępnie wypełnione.</span><span class="sxs-lookup"><span data-stu-id="d002f-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="d002f-125">Po wprowadzeniu poświadczeń można będzie pełni połączony z usługą SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d002f-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="d002f-126">Łączenie za pośrednictwem portalu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="d002f-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="d002f-127">Oprócz przy użyciu przycisku Otwórz w usłudze Power BI, użytkownicy mogą również łączyć się ich SQL Data Warehouse za pośrednictwem portalu Power BI.</span><span class="sxs-lookup"><span data-stu-id="d002f-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="d002f-128">Kliknij przycisk "Pobierz dane" u dołu okienka nawigacji.</span><span class="sxs-lookup"><span data-stu-id="d002f-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="d002f-129">Wybierz "Bazy danych".</span><span class="sxs-lookup"><span data-stu-id="d002f-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="d002f-130">Raz na stronie baz danych, wybierz "Azure SQL Data Warehouse", a następnie kliknij przycisk "Połącz".</span><span class="sxs-lookup"><span data-stu-id="d002f-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="d002f-131">Wprowadź informacje niezbędne połączenia.</span><span class="sxs-lookup"><span data-stu-id="d002f-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="d002f-132">Nazwa serwera, a nazwa bazy danych można znaleźć w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d002f-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="d002f-133">Zostanie skierowany do strony głównej usługi Power BI, a po nawiązaniu połączenia z nowego wpisu w obszarze "Zestaw danych" pojawi się nazwą wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="d002f-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="d002f-134">Możesz kliknąć na nowy zestaw danych, aby poznać wszystkie tabele i widoki w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d002f-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="d002f-135">Wybierając kolumnę będzie wysyłać zapytanie do źródła, dynamicznego tworzenia wizualny.</span><span class="sxs-lookup"><span data-stu-id="d002f-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="d002f-136">Te elementy wizualne można zapisane w nowy raport i ponownie przypięty do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d002f-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
