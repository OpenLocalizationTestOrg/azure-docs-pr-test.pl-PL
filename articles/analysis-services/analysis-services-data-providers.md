---
title: "bibliotek aaaClient wymaganych przez połączenie usług analizy tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano bibliotek klienta wymaganych przez klienta aplikacji i narzędzi tooconnect usług Azure Analysis Services"
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="b8098-103">Połączenie usług analizy tooAzure biblioteki klienta</span><span class="sxs-lookup"><span data-stu-id="b8098-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="b8098-104">Biblioteki klienta są niezbędne dla aplikacji klienckich i serwerów usług tooAnalysis tooconnect narzędzia.</span><span class="sxs-lookup"><span data-stu-id="b8098-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="b8098-105">Trzy bibliotek klienckich korzystać z usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b8098-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="b8098-106">ADOMD.NET i Analysis Services Management Objects (AMO) są zarządzanego klienta biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b8098-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="b8098-107">dostawcy OLE DB usług Analysis Services Hello (MSOLAP DLL) jest biblioteka klienta natywnego.</span><span class="sxs-lookup"><span data-stu-id="b8098-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="b8098-108">Zazwyczaj wszystkie trzy są instalowane na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="b8098-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="b8098-109">Azure Analysis Services wymaga hello najnowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="b8098-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="b8098-110">Aplikacji klienta firmy Microsoft, takich jak Power BI Desktop i Excel zainstalować wszystkie trzech klientów biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b8098-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="b8098-111">Jednak w zależności od wersji hello lub częstotliwość aktualizacji bibliotek klienta nie może być najnowsze wersje hello wymagane przez usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b8098-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="b8098-112">Witaj dotyczy toocustom aplikacji lub innych interfejsów, takich jak AsCmd, TOMASZ, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="b8098-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="b8098-113">Te aplikacje wymagają ręcznej instalacji hello bibliotek.</span><span class="sxs-lookup"><span data-stu-id="b8098-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="b8098-114">powitania klienta biblioteki dla ręcznej instalacji znajdują się w pakiety funkcji programu SQL Server jako dystrybucyjnego pakietów.</span><span class="sxs-lookup"><span data-stu-id="b8098-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="b8098-115">Te biblioteki klienta są jednak wiązanej toohello wersja programu SQL Server i nie może być hello najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="b8098-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="b8098-116">Biblioteki klienta dla połączeń klienckich różnią się od tooconnect wymagane dostawców danych ze źródła danych tooa serwera usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b8098-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="b8098-117">toolearn więcej informacji na temat połączenia źródła danych, zobacz [połączenia źródła danych](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="b8098-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="b8098-118">Pobierz najnowsze bibliotek klienckich hello</span><span class="sxs-lookup"><span data-stu-id="b8098-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="b8098-119">Użyj powitania po bibliotek klienta, jeśli w środowisku produkcyjnym i wymagają pełni zwolnione i obsługiwanych wersjach.</span><span class="sxs-lookup"><span data-stu-id="b8098-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="b8098-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="b8098-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="b8098-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="b8098-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="b8098-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="b8098-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="b8098-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="b8098-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="b8098-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8098-124">Next steps</span></span>
<span data-ttu-id="b8098-125">[Połącz przy użyciu programu Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="b8098-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="b8098-126">Łączenie z usługą Power BI</span><span class="sxs-lookup"><span data-stu-id="b8098-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
