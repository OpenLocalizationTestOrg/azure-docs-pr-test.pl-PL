---
title: "poziom zgodności modelu aaaData w usług Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Opis poziomu zgodności modelu tabelarycznego."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="c1d18-103">Poziom zgodności dla modele tabelaryczne usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="c1d18-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="c1d18-104">*Poziom zgodności* odwołuje się zachowań określonych toorelease hello aparatu usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="c1d18-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="c1d18-105">Poziom zgodności toohello zmiany zwykle pokrywa się z główne wersje programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c1d18-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="c1d18-106">Te zmiany są również zaimplementowane w usług Azure Analysis Services toomaintain parzystości między obu platform.</span><span class="sxs-lookup"><span data-stu-id="c1d18-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="c1d18-107">Zmiany poziomu zgodności dotyczy również funkcje dostępne w Twojej modeli tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="c1d18-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="c1d18-108">Na przykład zapytania bezpośredniego i metadanych tabelarycznych obiektów mają implementacje różne w zależności od poziomu zgodności hello.</span><span class="sxs-lookup"><span data-stu-id="c1d18-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="c1d18-109">Azure Analysis Services obsługuje modeli tabelarycznych przy hello 1200 i 1400 poziomy zgodności.</span><span class="sxs-lookup"><span data-stu-id="c1d18-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="c1d18-110">poziom zgodności najnowszych Hello jest 1400.</span><span class="sxs-lookup"><span data-stu-id="c1d18-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="c1d18-111">Ten poziom pokrywa się z usługami analizy serwera SQL w 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c1d18-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="c1d18-112">Główne funkcje na poziomie zgodności 1400 hello:</span><span class="sxs-lookup"><span data-stu-id="c1d18-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="c1d18-113">Nowa infrastruktura dla połączenia danych, a następnie zaimportuj do modeli tabelarycznych z obsługą TOMASZ interfejsów API i skryptów TMSL.</span><span class="sxs-lookup"><span data-stu-id="c1d18-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="c1d18-114">Ta nowa funkcja umożliwia obsługę dodatkowych źródeł danych takich jak magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1d18-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="c1d18-115">Przekształcenia danych i możliwości mashup danych za pomocą wyrażenia pobieranie danych i M.</span><span class="sxs-lookup"><span data-stu-id="c1d18-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="c1d18-116">Środki obsługuje właściwości wiersze szczegółów za pomocą wyrażenia języka DAX.</span><span class="sxs-lookup"><span data-stu-id="c1d18-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="c1d18-117">Ta właściwość umożliwia klienta narzędzi, takich jak Microsoft Excel toodrill dół toodetailed dane zagregowane raportu.</span><span class="sxs-lookup"><span data-stu-id="c1d18-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="c1d18-118">Na przykład przy przeglądaniu łączna sprzedaż dla regionu i miesiąc, można wyświetlić szczegółów zamówienia hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="c1d18-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="c1d18-119">Zabezpieczenia na poziomie obiektu dla tabel i kolumn nazwy dodatkowo toohello danych w nich.</span><span class="sxs-lookup"><span data-stu-id="c1d18-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="c1d18-120">Rozszerzona obsługa niewyrównane hierarchie.</span><span class="sxs-lookup"><span data-stu-id="c1d18-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="c1d18-121">Wydajność i udoskonalenia funkcji monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c1d18-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="c1d18-122">Ustaw poziom zgodności</span><span class="sxs-lookup"><span data-stu-id="c1d18-122">Set compatibility level</span></span> 
 <span data-ttu-id="c1d18-123">Podczas tworzenia nowego projektu modelu tabelarycznego programu SSDT, można określić poziom zgodności hello na powitania **Projektant modelu tabelarycznego** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c1d18-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="c1d18-125">W przypadku wybrania hello **nie pokazuj ponownie tego komunikatu** opcja, poziom zgodności hello określony jako domyślny hello użycie wszystkich kolejnych projektów.</span><span class="sxs-lookup"><span data-stu-id="c1d18-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="c1d18-126">Można zmienić poziom zgodności domyślne hello programu SSDT w **narzędzia** > **opcje**.</span><span class="sxs-lookup"><span data-stu-id="c1d18-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="c1d18-127">tooupgrade istniejącego projektu modelu tabelarycznego programu SSDT, zestaw hello **poziom zgodności** właściwości w modelu hello **właściwości** okna.</span><span class="sxs-lookup"><span data-stu-id="c1d18-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="c1d18-128">Zachowaj w uwadze, uaktualnienie hello poziom zgodności jest nieodwracalne.</span><span class="sxs-lookup"><span data-stu-id="c1d18-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="c1d18-129">Sprawdź poziom zgodności bazy danych modelu tabelarycznego w programie SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="c1d18-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="c1d18-130">W programie SSMS, kliknij prawym przyciskiem myszy nazwę bazy danych hello > **właściwości** > **poziom zgodności**.</span><span class="sxs-lookup"><span data-stu-id="c1d18-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="c1d18-131">Sprawdź obsługiwany poziom zgodności dla serwera w programie SSMS</span><span class="sxs-lookup"><span data-stu-id="c1d18-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="c1d18-132">W programie SSMS, kliknij prawym przyciskiem myszy nazwę serwera hello > **właściwości** > **obsługiwany poziom zgodności**.</span><span class="sxs-lookup"><span data-stu-id="c1d18-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="c1d18-133">Ta właściwość określa hello najwyższy poziom zgodności bazy danych, które zostanie uruchomione na serwerze hello (z wyjątkiem wersji zapoznawczej).</span><span class="sxs-lookup"><span data-stu-id="c1d18-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="c1d18-134">Nie można zmienić poziomu zgodności Hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c1d18-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c1d18-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1d18-135">Next steps</span></span>
  <span data-ttu-id="c1d18-136">[Tworzenie modelu w portalu Azure](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="c1d18-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="c1d18-137">Zarządzanie usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="c1d18-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
