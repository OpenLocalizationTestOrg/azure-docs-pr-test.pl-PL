---
title: "aaaRestrict zawartości Azure CDN według kraju | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toorestrict dostępu tooyour Azure CDN zawartości przy użyciu funkcji filtrowania Geo."
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
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="c24d4-103">Ogranicz zawartość sieci Azure CDN według kraju</span><span class="sxs-lookup"><span data-stu-id="c24d4-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="c24d4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c24d4-104">Overview</span></span>
<span data-ttu-id="c24d4-105">Gdy użytkownik zażąda zawartości, domyślnie, niezależnie od tego, w którym użytkownik hello wprowadzone tego żądania z obsługiwanej hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="c24d4-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="c24d4-106">W niektórych przypadkach może być toorestrict dostęp do tooyour zawartości według kraju.</span><span class="sxs-lookup"><span data-stu-id="c24d4-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="c24d4-107">W tym temacie opisano sposób toouse hello **filtrowania geograficznie** funkcji w kolejności tooconfigure hello tooallow lub blokowanie dostępu do usługi według kraju.</span><span class="sxs-lookup"><span data-stu-id="c24d4-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c24d4-108">produkty Verizon i Akamai Hello Podaj hello tę samą funkcjonalność filtrowania geograficznie, ale ma niewielkie różnice w te numerów kierunkowych obsługują.</span><span class="sxs-lookup"><span data-stu-id="c24d4-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="c24d4-109">Zobacz krok 3 różnic toohello łącza.</span><span class="sxs-lookup"><span data-stu-id="c24d4-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="c24d4-110">Informacje o kwestiach dotyczących tooconfiguring takiego ograniczenia, temacie hello [zagadnienia dotyczące](cdn-restrict-access-by-country.md#considerations) sekcji na końcu hello hello tematu.</span><span class="sxs-lookup"><span data-stu-id="c24d4-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![Filtrowanie kraju](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="c24d4-112">Krok 1: Definiowanie hello ścieżki katalogu</span><span class="sxs-lookup"><span data-stu-id="c24d4-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="c24d4-113">Wybierz punkt końcowy w portalu hello i znaleźć hello filtrowania geograficznie na karcie toofind nawigacji po lewej stronie powitania tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="c24d4-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="c24d4-114">Konfigurując filtr kraju, należy określić hello ścieżki względnej toohello lokalizacji toowhich użytkowników ma być dozwolony lub zabroniony dostęp.</span><span class="sxs-lookup"><span data-stu-id="c24d4-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="c24d4-115">Filtrowanie geograficznie można stosować dla wszystkich plików z "/" lub wybrane foldery, określając ścieżki katalogu "/ obrazy /".</span><span class="sxs-lookup"><span data-stu-id="c24d4-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="c24d4-116">Można także zastosować filtrowanie geograficznie tooa pojedynczy plik przez określenie pliku hello i pomijając hello ukośnika "/ zdjęcia/miasto.png".</span><span class="sxs-lookup"><span data-stu-id="c24d4-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="c24d4-117">Przykładowy filtr ścieżki katalogu:</span><span class="sxs-lookup"><span data-stu-id="c24d4-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="c24d4-118">Krok 2: Definiowanie akcji hello: blokowanie lub zezwalanie na</span><span class="sxs-lookup"><span data-stu-id="c24d4-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="c24d4-119">**Zablokuj:** użytkownikom hello określony krajów będą odrzucane tooassets dostępu zażąda tej ścieżki cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="c24d4-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="c24d4-120">Jeśli inne opcje filtrowania kraju zostały skonfigurowane dla tej lokalizacji, następnie wszyscy inni użytkownicy będą mieć dostęp.</span><span class="sxs-lookup"><span data-stu-id="c24d4-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="c24d4-121">**Zezwalaj na:** tylko użytkownicy z hello określony krajów może być tooassets dostępu zażąda tej ścieżki cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="c24d4-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="c24d4-122">Krok 3: Definiowanie hello krajach</span><span class="sxs-lookup"><span data-stu-id="c24d4-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="c24d4-123">Wybierz krajach hello mają tooblock, lub zezwolić hello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c24d4-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="c24d4-124">Na przykład hello reguły blokowania /Photos/Strasburgu/będzie filtrować pliki w tym:</span><span class="sxs-lookup"><span data-stu-id="c24d4-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="c24d4-125">Kod kraju</span><span class="sxs-lookup"><span data-stu-id="c24d4-125">Country codes</span></span>
<span data-ttu-id="c24d4-126">Witaj **filtrowania geograficznie** funkcja używa kraju kodów toodefine hello krajach z których będą dozwolone lub zablokowane żądania dla zabezpieczonych katalogu.</span><span class="sxs-lookup"><span data-stu-id="c24d4-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="c24d4-127">Można znaleźć hello numerów kierunkowych w [Azure CDN numerów kierunkowych](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="c24d4-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="c24d4-128"><a id="considerations"></a>Zagadnienia dotyczące</span><span class="sxs-lookup"><span data-stu-id="c24d4-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="c24d4-129">Może potrwać too90 minut Verizon lub kilka minut z Akamai, zmiany tooyour kraju filtrowania konfiguracji tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="c24d4-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="c24d4-130">Ta funkcja nie obsługuje symboli wieloznacznych (na przykład "*").</span><span class="sxs-lookup"><span data-stu-id="c24d4-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="c24d4-131">skojarzony ze ścieżką względną hello konfiguracji filtrowania geograficznie Hello będzie stosowane rekursywnie toothat ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c24d4-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="c24d4-132">Tylko jedna reguła może być zastosowane toohello tej samej ścieżce względnej (nie można utworzyć wiele filtrów kraju toohello tego punktu tej samej ścieżce względnej.</span><span class="sxs-lookup"><span data-stu-id="c24d4-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="c24d4-133">Jednak folder może mieć wiele filtrów kraju.</span><span class="sxs-lookup"><span data-stu-id="c24d4-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="c24d4-134">Jest to powodu toohello cykliczne rodzaj filtry kraju.</span><span class="sxs-lookup"><span data-stu-id="c24d4-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="c24d4-135">Innymi słowy podfolderze folderu wcześniej skonfigurowane można przypisać filtru innego kraju.</span><span class="sxs-lookup"><span data-stu-id="c24d4-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

