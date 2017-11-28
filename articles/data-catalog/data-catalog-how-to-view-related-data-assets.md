---
title: "aaaHow tooview powiązane zasoby danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, w jaki sposób tooview powiązane zasoby danych w usłudze Azure Data Catalog trwałego wybranych danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="e9ea0-103">Jak tooview powiązane zasoby danych w usłudze Azure Data Catalog?</span><span class="sxs-lookup"><span data-stu-id="e9ea0-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="e9ea0-104">Wykaz danych Azure umożliwia tooview danych zasoby pokrewne tooa wybrane dane zasobów i widoku relacji między nimi.</span><span class="sxs-lookup"><span data-stu-id="e9ea0-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="e9ea0-105">Obsługiwane źródła danych</span><span class="sxs-lookup"><span data-stu-id="e9ea0-105">Supported data sources</span></span> 
<span data-ttu-id="e9ea0-106">Podczas rejestrowania zasobów danych z hello następujące źródła danych usługi Azure Data Catalog automatycznie rejestruje metadane dotyczące relacji sprzężenia między hello wybrane zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="e9ea0-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="e9ea0-107">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="e9ea0-107">SQL Server</span></span>
- <span data-ttu-id="e9ea0-108">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e9ea0-108">Azure SQL Database</span></span>
- <span data-ttu-id="e9ea0-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="e9ea0-109">MySQL</span></span>
- <span data-ttu-id="e9ea0-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="e9ea0-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="e9ea0-111">Wyświetlanie powiązanych danych zasobów</span><span class="sxs-lookup"><span data-stu-id="e9ea0-111">View related data assets</span></span>
<span data-ttu-id="e9ea0-112">tooview zasobów danych, które są powiązane tooa wybrany zestaw danych, użyj hello **relacje** karcie pokazane na powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="e9ea0-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure Data Catalog — wyświetlanie powiązanych zasobów danych](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="e9ea0-114">W tym przykładzie są dwie relacje dla hello wybrane **ProductSubcategory** zasobu danych:</span><span class="sxs-lookup"><span data-stu-id="e9ea0-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="e9ea0-115">Kolumna ProductSubcategoryID hello produktu tabeli ma relacji klucza obcego z kolumną ProductSubcategoryID hello wybrane ProductSubcategory tabeli.</span><span class="sxs-lookup"><span data-stu-id="e9ea0-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="e9ea0-116">Kolumna ProductCategoryID hello ProductSubCategory tabeli ma relacji klucza obcego z kolumną ProductCategoryID hello wybrane ProductCategory tabeli.</span><span class="sxs-lookup"><span data-stu-id="e9ea0-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="e9ea0-117">Zwróć uwagę, kierunku hello hello strzałki w widoku drzewa relacji hello.</span><span class="sxs-lookup"><span data-stu-id="e9ea0-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="e9ea0-118">toosee więcej szczegółów, takich jak hello w pełni kwalifikowana nazwa kolumny hello Przesuń hello myszy nad i wyświetlić menu podręczne toohello podobne, po obrazu:</span><span class="sxs-lookup"><span data-stu-id="e9ea0-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure Data Catalog — podręczny relacji](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="e9ea0-120">tooinclude relacje między zasoby, które zostały już zarejestrowane, Zarejestruj ponownie tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e9ea0-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9ea0-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9ea0-121">Next steps</span></span>
- [<span data-ttu-id="e9ea0-122">Jak toomanage zasobów danych</span><span class="sxs-lookup"><span data-stu-id="e9ea0-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
