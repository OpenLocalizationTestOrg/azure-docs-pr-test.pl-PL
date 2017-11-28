---
title: "Reguły nazewnictwa jednostek fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Opisuje reguły nazewnictwa dla jednostek fabryki danych."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d447bbceb4ab344e011311eaf143b20f0a0400d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="bce0b-103">Fabryka danych Azure - reguły nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="bce0b-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="bce0b-104">W poniższej tabeli przedstawiono reguły nazewnictwa artefaktów fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="bce0b-104">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="bce0b-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bce0b-105">Name</span></span> | <span data-ttu-id="bce0b-106">Unikatowość nazwy</span><span class="sxs-lookup"><span data-stu-id="bce0b-106">Name Uniqueness</span></span> | <span data-ttu-id="bce0b-107">Sprawdzanie poprawności</span><span class="sxs-lookup"><span data-stu-id="bce0b-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="bce0b-108">Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="bce0b-108">Data Factory</span></span> |<span data-ttu-id="bce0b-109">Unikatowe w obrębie platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bce0b-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="bce0b-110">Nazwy jest rozróżniana wielkość liter, czyli `MyDF` i `mydf` odwoływać się do tej samej fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="bce0b-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="bce0b-111">Każdej fabryki danych jest powiązany dokładnie jedną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bce0b-111">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="bce0b-112">Nazwy obiektów muszą zaczynać się literą lub cyfrą i może zawierać tylko litery, cyfry i znak kreski (-).</span><span class="sxs-lookup"><span data-stu-id="bce0b-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="bce0b-113">Każdy znak kreski (-) musi być od razu poprzedzone i następuje literą lub cyfrą.</span><span class="sxs-lookup"><span data-stu-id="bce0b-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="bce0b-114">Następujących po sobie kresek nie są dozwolone w nazwach kontenerów.</span><span class="sxs-lookup"><span data-stu-id="bce0b-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="bce0b-115">Nazwa może być 3 do 63 znaków.</span><span class="sxs-lookup"><span data-stu-id="bce0b-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="bce0b-116">Połączonej usługi/tabel/potoki</span><span class="sxs-lookup"><span data-stu-id="bce0b-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="bce0b-117">Unikatowy o w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="bce0b-117">Unique with in a data factory.</span></span> <span data-ttu-id="bce0b-118">Nazwy jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bce0b-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="bce0b-119">Maksymalna liczba znaków w nazwie tabeli: 260.</span><span class="sxs-lookup"><span data-stu-id="bce0b-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="bce0b-120">Nazwa obiektu musi rozpoczynać się od litery, liczby lub znaku podkreślenia (_).</span><span class="sxs-lookup"><span data-stu-id="bce0b-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="bce0b-121">Następujące znaki nie są dozwolone: ".", "+","?", "/", "<", ">","*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="bce0b-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="bce0b-122">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="bce0b-122">Resource Group</span></span> |<span data-ttu-id="bce0b-123">Unikatowe w obrębie platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bce0b-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="bce0b-124">Nazwy jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bce0b-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="bce0b-125">Maksymalna liczba znaków: 1000.</span><span class="sxs-lookup"><span data-stu-id="bce0b-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="bce0b-126">Nazwa może zawierać litery, cyfry i następujące znaki: "-", "_",","i"."</span><span class="sxs-lookup"><span data-stu-id="bce0b-126">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

