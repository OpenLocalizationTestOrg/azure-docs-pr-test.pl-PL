---
title: "aaaManage zasobów danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Artykuł Hello prezentuje sposób widoczność toocontrol i własności zasobów danych zarejestrowane w wykazie danych Azure."
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
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="e6e86-103">Zarządzać zasobami danych w wykazie danych Azure</span><span class="sxs-lookup"><span data-stu-id="e6e86-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="e6e86-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e6e86-104">Introduction</span></span>
<span data-ttu-id="e6e86-105">Azure Data Catalog jest przeznaczona dla źródła danych odnajdywania, dzięki czemu można łatwo odnaleźć i zrozumieć hello źródeł danych muszą tooperform analizy i podejmować decyzje.</span><span class="sxs-lookup"><span data-stu-id="e6e86-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="e6e86-106">Te możliwości odnajdywania należy hello największy wpływ, gdy inni użytkownicy można odnaleźć i zrozumieć hello szerokiej gamy dostępnych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="e6e86-107">Z tych elementów na uwadze hello domyślne zachowanie usługi Data Catalog jest dla wszystkich zarejestrowanych danych źródeł toobe widoczne tooand wykrywalny przez wszystkich użytkowników wykazu.</span><span class="sxs-lookup"><span data-stu-id="e6e86-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="e6e86-108">Wykaz danych nie zapewnia dostępu toohello samych danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="e6e86-109">Dostęp do danych jest kontrolowany przez właściciela hello hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="e6e86-110">Data Catalog można odnajdywania źródeł danych i wyświetlić metadane hello źródeł toohello powiązane, które są zarejestrowane w wykazie hello.</span><span class="sxs-lookup"><span data-stu-id="e6e86-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="e6e86-111">Może się zdarzyć, jednak gdzie źródeł danych tylko powinna być widoczna toospecific użytkowników lub toomembers określonych grup.</span><span class="sxs-lookup"><span data-stu-id="e6e86-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="e6e86-112">W takich sytuacjach użytkownicy mogą przejąć na własność zasobów danych zarejestrowanych w wykazie hello i następnie ustawić widoczność hello hello zasobów, których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="e6e86-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e86-113">Hello funkcji opisanych w tym artykule jest dostępna tylko w hello Standard Edition usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="e6e86-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="e6e86-114">Witaj bezpłatna wersja nie udostępnia możliwości własności i ograniczanie widoczności zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="e6e86-115">Zarządzanie własności zasobów danych</span><span class="sxs-lookup"><span data-stu-id="e6e86-115">Manage ownership of data assets</span></span>
<span data-ttu-id="e6e86-116">Domyślnie nieposiadanej są zasobów danych, które są zarejestrowane w wykazie danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="e6e86-117">Każdy użytkownik posiadający uprawnienia tooaccess hello katalogu mogą odnaleźć i Adnotuj tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e6e86-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="e6e86-118">Użytkownicy mogą przejąć na własność zasobów danych go i następnie ograniczyć widoczność hello zasoby hello, w których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="e6e86-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="e6e86-119">Gdy zasobu danych w katalogu danych jest właścicielem, tylko użytkownicy, którzy są autoryzowane przez właścicieli hello mogą odnaleźć hello zasobów i wyświetlić jej metadane i tylko właściciele hello można usunąć zasobów hello z katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e6e86-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e86-120">Własność w wykazie danych ma wpływ na powitania metadane są przechowywane w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e6e86-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="e6e86-121">Własność nie przyznaje wszystkie uprawnienia na powitania źródła danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="e6e86-122">Przejmowanie na własność</span><span class="sxs-lookup"><span data-stu-id="e6e86-122">Take ownership</span></span>
<span data-ttu-id="e6e86-123">Użytkownicy mogą przejąć prawo własności zasobów danych, wybierając hello **Przejmij na własność** opcji w portalu wykazu danych hello.</span><span class="sxs-lookup"><span data-stu-id="e6e86-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="e6e86-124">Żadne specjalne uprawnienia są wymagane tootake własności zasobów danych go.</span><span class="sxs-lookup"><span data-stu-id="e6e86-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="e6e86-125">Każdy użytkownik może przejąć na własność zasobów danych go.</span><span class="sxs-lookup"><span data-stu-id="e6e86-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="e6e86-126">Dodaj właścicieli i współwłaścicieli</span><span class="sxs-lookup"><span data-stu-id="e6e86-126">Add owners and co-owners</span></span>
<span data-ttu-id="e6e86-127">Jeśli ma już właściciela zasobów danych, innych użytkowników nie wystarczy przejąć na własność.</span><span class="sxs-lookup"><span data-stu-id="e6e86-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="e6e86-128">Muszą zostać dodane jako współwłaściciele przez istniejące właściciela.</span><span class="sxs-lookup"><span data-stu-id="e6e86-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="e6e86-129">Wszelkie właściciela można dodać dodatkowych użytkowników lub grup zabezpieczeń jako współwłaściciele.</span><span class="sxs-lookup"><span data-stu-id="e6e86-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e86-130">Jego jest najlepszym toohave praktyki co najmniej dwóch osób jako właściciele dla żadnego należące do zasobów danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="e6e86-131">Usuń właścicieli</span><span class="sxs-lookup"><span data-stu-id="e6e86-131">Remove owners</span></span>
<span data-ttu-id="e6e86-132">Podobnie jak wszelkie właściciel zasobu może dodawać współwłaścicieli, wszelkie właściciel zasobu można usunąć wszelkie współwłaściciel.</span><span class="sxs-lookup"><span data-stu-id="e6e86-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="e6e86-133">Właściciel zasobu, która usuwa go lub siebie jako właściciela nie może dłużej zarządzać hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="e6e86-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="e6e86-134">Jeśli właściciel zasobu hello usuwa go lub siebie jako właściciela, nie ma żadnych wspólnej właścicieli zasobów hello przywraca tooan bez właściciela stanu.</span><span class="sxs-lookup"><span data-stu-id="e6e86-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="e6e86-135">Widoczność formantu</span><span class="sxs-lookup"><span data-stu-id="e6e86-135">Control visibility</span></span>
<span data-ttu-id="e6e86-136">Właścicieli zasobu danych można ustawić widoczność hello hello zasobów danych, których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="e6e86-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="e6e86-137">widoczność toorestrict jako domyślny hello, w przypadku, gdy wszystkie usługi Data Catalog użytkownicy mogą odnajdować i widoku hello zasobów danych, właściciel zasobu hello przełączać hello ustawienie widoczności z **wszyscy** zbyt**właściciele i następujący użytkownicy** we właściwościach hello hello trwałego.</span><span class="sxs-lookup"><span data-stu-id="e6e86-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="e6e86-138">Następnie można dodać właścicieli, konkretnych użytkowników i grup zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e6e86-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e86-139">Jeśli to możliwe, należy przydzielić uprawnienia własności i widoczność zasobów grup toosecurity i nie tooindividual użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e6e86-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="e6e86-140">Administratorzy katalogu</span><span class="sxs-lookup"><span data-stu-id="e6e86-140">Catalog administrators</span></span>
<span data-ttu-id="e6e86-141">Administratorzy katalogu danych są niejawnie współwłaściciele wszystkich zasobów w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e6e86-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="e6e86-142">Właściciele zawartości nie można usunąć widoczność administratorów, a administratorzy mogą zarządzać własności i widoczności dla wszystkich zasobów danych w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e6e86-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="e6e86-143">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e6e86-143">Summary</span></span>
<span data-ttu-id="e6e86-144">Hello Data Catalog crowdsourcing toometadata i dane zasobów odnajdowania modelu pozwala wszystkich toocontribute użytkownicy wykazu i odnajdywanie.</span><span class="sxs-lookup"><span data-stu-id="e6e86-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="e6e86-145">Witaj Standard Edition usługi Data Catalog jest przeznaczona dla własności i zarządzania widoczność hello toolimit oraz korzystanie z zasobów określonych danych.</span><span class="sxs-lookup"><span data-stu-id="e6e86-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
