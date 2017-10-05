---
title: "Zarządzać zasobami danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Artykuł prezentuje sposób kontrolowania widoczności i własności zasobów danych zarejestrowane w usłudze Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="2d5c7-103">Zarządzać zasobami danych w wykazie danych Azure</span><span class="sxs-lookup"><span data-stu-id="2d5c7-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="2d5c7-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2d5c7-104">Introduction</span></span>
<span data-ttu-id="2d5c7-105">Azure Data Catalog jest przeznaczona dla źródła danych odnajdywania, dzięki czemu można łatwo odnaleźć i zrozumieć użycie źródeł danych, które należy wykonywać analizy i podejmować decyzje.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="2d5c7-106">Te możliwości odnajdywania należy największy wpływ, gdy inni użytkownicy mogą odnaleźć i zrozumieć szerokiej gamy dostępnych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="2d5c7-107">Z tych elementów, pamiętając domyślne zachowanie usługi Data Catalog jest dla wszystkich źródeł danych zarejestrowanych były widoczne i wykrywalny przez wszystkich użytkowników w katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="2d5c7-108">Wykaz danych nie uzyskania dostępu do samych danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="2d5c7-109">Dostęp do danych jest kontrolowany przez właściciela źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="2d5c7-110">Data Catalog można odnaleźć źródła danych i wyświetlać metadane dotyczące źródeł, które są zarejestrowane w wykazie.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="2d5c7-111">Mogą wystąpić sytuacje, jednak gdzie źródeł danych tylko powinny być widoczne, dla określonych użytkowników lub do członków określonych grup.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="2d5c7-112">W takich sytuacjach użytkownicy mogą przejąć na własność zasobów danych zarejestrowanych w wykazie i następnie ustawić widoczność zasobów, w których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="2d5c7-113">Funkcje opisane w tym artykule jest dostępna tylko w Standard Edition usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="2d5c7-114">Bezpłatna wersja nie udostępnia możliwości posiadania i ograniczenie widoczność zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="2d5c7-115">Zarządzanie własności zasobów danych</span><span class="sxs-lookup"><span data-stu-id="2d5c7-115">Manage ownership of data assets</span></span>
<span data-ttu-id="2d5c7-116">Domyślnie nieposiadanej są zasobów danych, które są zarejestrowane w wykazie danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="2d5c7-117">Każdy użytkownik z uprawnieniami, aby uzyskać dostęp do katalogu mogą odnaleźć i Adnotuj tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="2d5c7-118">Użytkownicy mogą przejąć na własność zasobów danych go i następnie ograniczyć widoczność zasobów, w których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="2d5c7-119">Gdy zasobu danych w katalogu danych jest właścicielem, tylko użytkownicy uwierzytelnieni właściciele mogą odnaleźć zasobu i wyświetlić jej metadane, a tylko właściciele można usunąć elementu zawartości z katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="2d5c7-120">Własność w wykazie danych dotyczy tylko metadane są przechowywane w katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="2d5c7-121">Własność nie przyznaje wszystkie uprawnienia w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="2d5c7-122">Przejmowanie na własność</span><span class="sxs-lookup"><span data-stu-id="2d5c7-122">Take ownership</span></span>
<span data-ttu-id="2d5c7-123">Użytkownicy mogą przejąć prawo własności zasobów danych, wybierając **Przejmij na własność** opcji w portalu wykazu danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="2d5c7-124">Aby przejąć na własność zasobów danych nieposiadanej są wymagane żadne specjalne uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="2d5c7-125">Każdy użytkownik może przejąć na własność zasobów danych go.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="2d5c7-126">Dodaj właścicieli i współwłaścicieli</span><span class="sxs-lookup"><span data-stu-id="2d5c7-126">Add owners and co-owners</span></span>
<span data-ttu-id="2d5c7-127">Jeśli ma już właściciela zasobów danych, innych użytkowników nie wystarczy przejąć na własność.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="2d5c7-128">Muszą zostać dodane jako współwłaściciele przez istniejące właściciela.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="2d5c7-129">Wszelkie właściciela można dodać dodatkowych użytkowników lub grup zabezpieczeń jako współwłaściciele.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="2d5c7-130">Jest najlepszym rozwiązaniem ma co najmniej dwóch osób jako właściciele żadnych zasobów należących do danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="2d5c7-131">Usuń właścicieli</span><span class="sxs-lookup"><span data-stu-id="2d5c7-131">Remove owners</span></span>
<span data-ttu-id="2d5c7-132">Podobnie jak wszelkie właściciel zasobu może dodawać współwłaścicieli, wszelkie właściciel zasobu można usunąć wszelkie współwłaściciel.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="2d5c7-133">Właściciel zasobu, która usuwa go lub siebie jako właściciela nie może dłużej zarządzać elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="2d5c7-134">Jeśli właściciel zasobu usuwa go lub siebie jako właściciela, nie ma żadnych wspólnej właścicieli zasobu przekształcenia go do stanu.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="2d5c7-135">Widoczność formantu</span><span class="sxs-lookup"><span data-stu-id="2d5c7-135">Control visibility</span></span>
<span data-ttu-id="2d5c7-136">Właściciele danych zasobów można kontrolować widoczność zasobów danych, w których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="2d5c7-137">Aby ograniczyć widoczność jako domyślny, w której wszyscy użytkownicy wykazu danych może odnalezienia i wyświetlenia zasobów danych, właściciel zasobu może zmienić ustawienie widoczności z **wszyscy** do **właściciele i następujący użytkownicy** we właściwościach elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="2d5c7-138">Następnie można dodać właścicieli, konkretnych użytkowników i grup zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="2d5c7-139">Jeśli to możliwe, uprawnienia własności i widoczności zasobu powinny być przypisane do grup zabezpieczeń, a nie do poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="2d5c7-140">Administratorzy katalogu</span><span class="sxs-lookup"><span data-stu-id="2d5c7-140">Catalog administrators</span></span>
<span data-ttu-id="2d5c7-141">Administratorzy katalogu danych są niejawnie współwłaściciele wszystkich zasobów w katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="2d5c7-142">Właściciele zawartości nie można usunąć widoczność administratorów, a administratorzy mogą zarządzać własności i widoczności dla wszystkich zasobów danych w katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="2d5c7-143">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="2d5c7-143">Summary</span></span>
<span data-ttu-id="2d5c7-144">Model crowdsourcingu w postaci usługi Data Catalog do odnajdywania zasobów metadane i dane zezwala wszystkim użytkownikom katalogu przyczyniają się do odnajdywania.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="2d5c7-145">Standard Edition Data Catalog jest przeznaczona dla własności i zarządzania, aby ograniczyć widoczność oraz korzystanie z zasobów określonych danych.</span><span class="sxs-lookup"><span data-stu-id="2d5c7-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
