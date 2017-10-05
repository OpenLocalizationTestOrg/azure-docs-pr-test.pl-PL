---
title: "Ogranicz zawartość sieci Azure CDN według kraju | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ograniczyć dostęp do treści Azure CDN przy użyciu funkcji filtrowania Geo."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="c3847-103">Ogranicz zawartość sieci Azure CDN według kraju</span><span class="sxs-lookup"><span data-stu-id="c3847-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="c3847-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c3847-104">Overview</span></span>
<span data-ttu-id="c3847-105">Gdy użytkownik zażąda zawartości, domyślnie, niezależnie od tego, w którym użytkownik wprowadzone tego żądania z obsługiwanej zawartości.</span><span class="sxs-lookup"><span data-stu-id="c3847-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="c3847-106">W niektórych przypadkach można ograniczyć dostęp do zawartości według kraju.</span><span class="sxs-lookup"><span data-stu-id="c3847-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="c3847-107">W tym temacie wyjaśniono, jak używać **filtrowania geograficznie** funkcji, aby skonfigurować usługę, aby umożliwić lub zablokować dostęp według kraju.</span><span class="sxs-lookup"><span data-stu-id="c3847-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3847-108">Produkty Verizon i Akamai mają te same funkcje filtrowania geograficznie, ale ma niewielkie różnice w te numerów kierunkowych krajów obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="c3847-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="c3847-109">Zobacz krok 3 dla łącza do różnic.</span><span class="sxs-lookup"><span data-stu-id="c3847-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="c3847-110">Informacji o kwestiach dotyczących konfigurowania tego typu ograniczeń znajduje się w temacie [zagadnienia](cdn-restrict-access-by-country.md#considerations) sekcji na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="c3847-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Filtrowanie kraju](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="c3847-112">Krok 1: Definiowanie ścieżkę katalogu</span><span class="sxs-lookup"><span data-stu-id="c3847-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="c3847-113">Wybierz punkt końcowy w portalu, a znaleźć kartę filtrowania geograficznie na nawigacji po lewej stronie, aby znaleźć tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="c3847-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="c3847-114">Konfigurując filtr kraju, należy określić ścieżkę względną do lokalizacji, do którego użytkownicy będą dozwolone lub odmowa dostępu.</span><span class="sxs-lookup"><span data-stu-id="c3847-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="c3847-115">Filtrowanie geograficznie można stosować dla wszystkich plików z "/" lub wybrane foldery, określając ścieżki katalogu "/ obrazy /".</span><span class="sxs-lookup"><span data-stu-id="c3847-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="c3847-116">Można także zastosować dla filtrowania geograficznie w pojedynczym pliku przez określenie pliku i pomijając wiodący ukośnik "/ zdjęcia/miasto.png".</span><span class="sxs-lookup"><span data-stu-id="c3847-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="c3847-117">Przykładowy filtr ścieżki katalogu:</span><span class="sxs-lookup"><span data-stu-id="c3847-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="c3847-118">Krok 2: Definiowanie akcji: blokowanie lub zezwalanie na</span><span class="sxs-lookup"><span data-stu-id="c3847-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="c3847-119">**Zablokuj:** użytkowników z określonym krajów nie będą mieli dostępu do zasobów zażąda tej ścieżki cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="c3847-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="c3847-120">Jeśli inne opcje filtrowania kraju zostały skonfigurowane dla tej lokalizacji, następnie wszyscy inni użytkownicy będą mieć dostęp.</span><span class="sxs-lookup"><span data-stu-id="c3847-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="c3847-121">**Zezwalaj na:** tylko użytkowników z określonym krajów będą mieć dostęp do zasobów zażąda tej ścieżki cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="c3847-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="c3847-122">Krok 3: Definiowanie krajów</span><span class="sxs-lookup"><span data-stu-id="c3847-122">Step 3: Define the countries</span></span>
<span data-ttu-id="c3847-123">Wybierz krajów, które chcesz zablokować lub zezwolić dla ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c3847-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="c3847-124">Na przykład reguła blokowania /Photos/Strasburgu/będzie filtrować pliki w tym:</span><span class="sxs-lookup"><span data-stu-id="c3847-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="c3847-125">Kod kraju</span><span class="sxs-lookup"><span data-stu-id="c3847-125">Country codes</span></span>
<span data-ttu-id="c3847-126">**Filtrowania geograficznie** funkcji używa kodów kraju, aby zdefiniować krajów, z których będą dozwolone lub blokowane dla katalogu zabezpieczonych żądanie.</span><span class="sxs-lookup"><span data-stu-id="c3847-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="c3847-127">Można znaleźć numerów kierunkowych w [Azure CDN numerów kierunkowych](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3847-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="c3847-128"><a id="considerations"></a>Zagadnienia dotyczące</span><span class="sxs-lookup"><span data-stu-id="c3847-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="c3847-129">Verizon lub kilka minut z Akamai, zmiany w Twoim kraju filtrowania konfiguracja zaczęła obowiązywać może potrwać do 90 minut.</span><span class="sxs-lookup"><span data-stu-id="c3847-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="c3847-130">Ta funkcja nie obsługuje symboli wieloznacznych (na przykład "*").</span><span class="sxs-lookup"><span data-stu-id="c3847-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="c3847-131">Konfiguracja filtrowania geograficznie skojarzony ze ścieżką względną będzie cyklicznie zastosowanych do tej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c3847-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="c3847-132">Tylko jedna reguła może odnosić się do tej samej ścieżce względnej (nie można utworzyć wiele filtrów kraju, które wskazują na tej samej ścieżce względnej.</span><span class="sxs-lookup"><span data-stu-id="c3847-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="c3847-133">Jednak folder może mieć wiele filtrów kraju.</span><span class="sxs-lookup"><span data-stu-id="c3847-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="c3847-134">Jest to spowodowane cykliczne rodzaj filtry kraju.</span><span class="sxs-lookup"><span data-stu-id="c3847-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="c3847-135">Innymi słowy podfolderze folderu wcześniej skonfigurowane można przypisać filtru innego kraju.</span><span class="sxs-lookup"><span data-stu-id="c3847-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

