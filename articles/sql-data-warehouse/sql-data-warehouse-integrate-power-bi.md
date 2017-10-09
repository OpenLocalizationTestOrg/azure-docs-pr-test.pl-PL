---
title: "aaaUse usługi Power BI z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="44789-103">Użyj usługi Power BI z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="44789-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="44789-104">Podobnie jak w przypadku bazy danych SQL Azure SQL danych magazynu bezpośrednie połączenie umożliwia tooleverage użytkownika zaawansowanych przekazywanie logicznej obok hello możliwości analityczne usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="44789-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="44789-105">Za pomocą bezpośrednich Connect zapytania są wysyłane wstecz tooyour Azure SQL Data Warehouse w czasie rzeczywistym Ci poznać platformę hello danych.</span><span class="sxs-lookup"><span data-stu-id="44789-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="44789-106">To, połączone z hello skali usługi SQL Data Warehouse umożliwia użytkownikom toocreate dynamicznych raportów w minutach przed terabajtów danych.</span><span class="sxs-lookup"><span data-stu-id="44789-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="44789-107">Ponadto wprowadzenie hello hello Otwórz w przycisk usługi Power BI umożliwia użytkownikom toodirectly Połącz usługi Power BI tootheir SQL Data Warehouse bez zbierania informacji z innych części Azure.</span><span class="sxs-lookup"><span data-stu-id="44789-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="44789-108">Podczas używania połączenia bezpośredniego należy Uwaga:</span><span class="sxs-lookup"><span data-stu-id="44789-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="44789-109">Określ nazwę FQDN serwera hello podczas łączenia z (Aby uzyskać więcej informacji zobacz poniżej)</span><span class="sxs-lookup"><span data-stu-id="44789-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="44789-110">Upewnij się, reguły zapory dla bazy danych hello są skonfigurowane za "Zezwalaj na dostęp tooAzure usługi".</span><span class="sxs-lookup"><span data-stu-id="44789-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="44789-111">Wszystkie akcje, takich jak wybierając kolumnę lub Dodawanie filtru bezpośrednio zwrócą hello magazynu danych</span><span class="sxs-lookup"><span data-stu-id="44789-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="44789-112">Kafelki są odświeżane co około 15 minut (w przypadku odświeżania toobe zaplanowane nie są konieczne)</span><span class="sxs-lookup"><span data-stu-id="44789-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="44789-113">Funkcja pytania i odpowiedzi nie jest dostępna dla bezpośrednie łączenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="44789-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="44789-114">Zmiany schematu nie są odczytywane automatycznie</span><span class="sxs-lookup"><span data-stu-id="44789-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="44789-115">Wszystkie zapytania bezpośredniego połączenia limit czasu będzie 2 minuty</span><span class="sxs-lookup"><span data-stu-id="44789-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="44789-116">Te ograniczenia i uwagi może zmienić w dalszym ciągu tooimprove hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="44789-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="44789-117">tooconnect kroki Hello są szczegółowo opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="44789-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="44789-118">Przy użyciu przycisku "Otwórz w usłudze Power BI" hello</span><span class="sxs-lookup"><span data-stu-id="44789-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="44789-119">Witaj najprostszy sposób toomove między magazyn danych SQL i usługi Power BI jest hello Otwórz w usłudze Power BI przycisku.</span><span class="sxs-lookup"><span data-stu-id="44789-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="44789-120">Ten przycisk pozwala tooseamlessly rozpocząć tworzenie nowych pulpitów nawigacyjnych w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="44789-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="44789-121">Rozpoczęto tooget Przejdź tooyour wystąpienie usługi SQL Data Warehouse w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44789-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="44789-122">Kliknij przycisk "Otwórz w usłudze Power BI" hello.</span><span class="sxs-lookup"><span data-stu-id="44789-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="44789-123">Jeśli nie jesteśmy w stanie toosign w bezpośrednio, lub jeśli nie masz konta usługi Power BI, konieczne będzie toosign w.</span><span class="sxs-lookup"><span data-stu-id="44789-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="44789-124">Pojawi się, że wstępne wypełnianie toohello strona połączenia SQL Data Warehouse, hello informacje z usługą SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44789-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="44789-125">Po wprowadzeniu poświadczeń będzie tooyour pełni podłączonej usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44789-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="44789-126">Łączenie za pośrednictwem portalu usługi Power BI hello</span><span class="sxs-lookup"><span data-stu-id="44789-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="44789-127">W dodatku toousing hello Otwórz w usłudze Power BI przycisku użytkownicy mogą łączyć tootheir SQL Data Warehouse za pośrednictwem hello Power BI portalu.</span><span class="sxs-lookup"><span data-stu-id="44789-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="44789-128">Kliknij przycisk "Pobierz dane" u dołu okienka nawigacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="44789-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="44789-129">Wybierz "Bazy danych".</span><span class="sxs-lookup"><span data-stu-id="44789-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="44789-130">Raz na stronie powitania, baz danych, wybierz "Azure SQL Data Warehouse", a następnie kliknij przycisk "Połącz".</span><span class="sxs-lookup"><span data-stu-id="44789-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="44789-131">Wprowadź informacje niezbędne połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="44789-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="44789-132">Nazwa serwera, a nazwa bazy danych znajdują się w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44789-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="44789-133">Nastąpi przekierowanie ponownie się, że nazwa hello wystąpienia zostanie wyświetlona strona głównego toohello usługi Power Bi i po nawiązaniu połączenia z nowego wpisu w obszarze "Zestaw danych".</span><span class="sxs-lookup"><span data-stu-id="44789-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="44789-134">Możesz kliknąć hello nowy zestaw danych tooexplore wszystkie hello tabele i widoki w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="44789-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="44789-135">Wybierając kolumnę wyśle źródła wstecz toohello kwerendy, dynamicznego tworzenia wizualny.</span><span class="sxs-lookup"><span data-stu-id="44789-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="44789-136">Te elementy wizualne mogą być zapisywane w nowy raport i ponownie przypięty tooyour pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="44789-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
