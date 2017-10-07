---
title: aaaLimitations w bazie danych Azure PostgreSQL | Dokumentacja firmy Microsoft
description: "Opis ograniczeń w bazie danych Azure PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="cda57-103">Ograniczenia dotyczące bazy danych platformy Azure dla PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cda57-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="cda57-104">Hello Azure bazy danych dla usługi PostgreSQL znajduje się w publicznej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="cda57-104">hello Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="cda57-105">Witaj poniższych sekcjach opisano pojemności i limity funkcjonalności hello bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="cda57-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="cda57-106">Maksymalne wartości warstwy usługi</span><span class="sxs-lookup"><span data-stu-id="cda57-106">Service Tier Maximums</span></span>
<span data-ttu-id="cda57-107">Bazy danych platformy Azure dla PostgreSQL ma wiele warstw usług, które można wybrać podczas tworzenia serwera.</span><span class="sxs-lookup"><span data-stu-id="cda57-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="cda57-108">Aby uzyskać więcej informacji, zobacz [zrozumieć, co jest dostępne w poszczególnych warstwach usług](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="cda57-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="cda57-109">Jest maksymalna liczba połączeń, jednostek obliczeniowych i magazynu w poszczególnych warstwach usług hello wersji zapoznawczej usługi, następująca:</span><span class="sxs-lookup"><span data-stu-id="cda57-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="cda57-110">**Maksymalna liczba połączeń**</span><span class="sxs-lookup"><span data-stu-id="cda57-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="cda57-111">Podstawowe 50 obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="cda57-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="cda57-112">połączenia o szybkości 50</span><span class="sxs-lookup"><span data-stu-id="cda57-112">50 connections</span></span>    |
| <span data-ttu-id="cda57-113">Podstawowe 100 jednostek obliczeń</span><span class="sxs-lookup"><span data-stu-id="cda57-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="cda57-114">połączenia o szybkości 100</span><span class="sxs-lookup"><span data-stu-id="cda57-114">100 connections</span></span>   |
| <span data-ttu-id="cda57-115">Standardowe jednostki 100 obliczeń</span><span class="sxs-lookup"><span data-stu-id="cda57-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="cda57-116">połączenia o szybkości 200</span><span class="sxs-lookup"><span data-stu-id="cda57-116">200 connections</span></span>   |
| <span data-ttu-id="cda57-117">Standardowa 200 obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="cda57-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="cda57-118">300 połączeń</span><span class="sxs-lookup"><span data-stu-id="cda57-118">300 connections</span></span>   |
| <span data-ttu-id="cda57-119">Standardowa 400 obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="cda57-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="cda57-120">400 połączeń</span><span class="sxs-lookup"><span data-stu-id="cda57-120">400 connections</span></span>   |
| <span data-ttu-id="cda57-121">Standardowa 800 obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="cda57-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="cda57-122">połączenia o szybkości 500</span><span class="sxs-lookup"><span data-stu-id="cda57-122">500 connections</span></span>   |
| <span data-ttu-id="cda57-123">**Obliczeniowe maksymalna liczba jednostek**</span><span class="sxs-lookup"><span data-stu-id="cda57-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="cda57-124">Warstwa Podstawowa usług</span><span class="sxs-lookup"><span data-stu-id="cda57-124">Basic service tier</span></span>         | <span data-ttu-id="cda57-125">100 jednostek obliczeń</span><span class="sxs-lookup"><span data-stu-id="cda57-125">100 Compute Units</span></span> |
| <span data-ttu-id="cda57-126">Warstwa Standardowa usług</span><span class="sxs-lookup"><span data-stu-id="cda57-126">Standard service tier</span></span>      | <span data-ttu-id="cda57-127">800 obliczeniowe jednostki</span><span class="sxs-lookup"><span data-stu-id="cda57-127">800 Compute Units</span></span> |
| <span data-ttu-id="cda57-128">**Maksymalna liczba magazynu**</span><span class="sxs-lookup"><span data-stu-id="cda57-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="cda57-129">Warstwa Podstawowa usług</span><span class="sxs-lookup"><span data-stu-id="cda57-129">Basic service tier</span></span>         | <span data-ttu-id="cda57-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="cda57-130">1 TB</span></span>              |
| <span data-ttu-id="cda57-131">Warstwa Standardowa usług</span><span class="sxs-lookup"><span data-stu-id="cda57-131">Standard service tier</span></span>      | <span data-ttu-id="cda57-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="cda57-132">1 TB</span></span>              |

<span data-ttu-id="cda57-133">Po osiągnięciu zbyt wiele połączeń, może zostać wyświetlony następujący błąd hello:</span><span class="sxs-lookup"><span data-stu-id="cda57-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="cda57-134">Błąd krytyczny: Niestety, jeszcze zbyt wielu klientów</span><span class="sxs-lookup"><span data-stu-id="cda57-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="cda57-135">Ograniczenia funkcjonalności wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="cda57-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="cda57-136">Operacje skalowania</span><span class="sxs-lookup"><span data-stu-id="cda57-136">Scale operations</span></span>
1.  <span data-ttu-id="cda57-137">Dynamiczne skalowanie serwerów w warstwach usług nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cda57-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="cda57-138">Oznacza to przełączaniu między Basic i Standard warstwy usług.</span><span class="sxs-lookup"><span data-stu-id="cda57-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="cda57-139">Dynamiczne zwiększanie na żądanie magazynu na serwerze utworzone wcześniej nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cda57-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="cda57-140">Zmniejszenie rozmiaru magazynu serwera nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="cda57-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="cda57-141">Uaktualniania wersji</span><span class="sxs-lookup"><span data-stu-id="cda57-141">Server version upgrades</span></span>
- <span data-ttu-id="cda57-142">Automatycznej migracji między wersjami aparatu bazy danych głównych nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cda57-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="cda57-143">Zarządzanie subskrypcją</span><span class="sxs-lookup"><span data-stu-id="cda57-143">Subscription management</span></span>
- <span data-ttu-id="cda57-144">Dynamicznie przenoszenie serwerów wstępnie utworzone w subskrypcji i grupy zasobów nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cda57-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="cda57-145">Przywracanie do punktu w czasie</span><span class="sxs-lookup"><span data-stu-id="cda57-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="cda57-146">Przywracanie toodifferent warstwy usług i/lub jednostki obliczeniowe i rozmiaru magazynu nie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="cda57-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="cda57-147">Przywracanie usuniętej serwera nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="cda57-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cda57-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cda57-148">Next steps</span></span>
- <span data-ttu-id="cda57-149">Zrozumienie [co jest dostępne w każdej warstwy cenowej](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="cda57-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="cda57-150">Zrozumienie [obsługiwane wersje PostgreSQL bazy danych](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="cda57-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="cda57-151">Przegląd [jak tooBack zapasowej i przywracania serwera w bazie danych Azure poświęcone PostgreSQL hello portalu Azure](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cda57-151">Review [How tooBack up and Restore a server in Azure Database for PostgreSQL using hello Azure portal](howto-restore-server-portal.md)</span></span>
