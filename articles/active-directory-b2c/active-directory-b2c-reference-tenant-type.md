---
title: "Azure Active Directory B2C: Siedziby dostępności & dane regionu | Dokumentacja firmy Microsoft"
description: "Temat dotyczący typów dzierżaw usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="c7a62-103">Azure Active Directory B2C: Siedziby dostępności & dane regionu</span><span class="sxs-lookup"><span data-stu-id="c7a62-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="c7a62-104">Dostępność w danym regionie i siedziby danych są dwa bardzo różnych zagadnienia dotyczące inaczej usługi Azure AD B2C od pozostałej części Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a62-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="c7a62-105">W tym artykule wyjaśniono różnice między tych dwóch pojęć, a następnie porównaj sposobów ich zastosowania do platformy Azure i usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c7a62-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="c7a62-106">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c7a62-106">Summary</span></span>
<span data-ttu-id="c7a62-107">Usługa Azure AD B2C jest **ogólnie dostępna na całym świecie** z opcją dla **danych siedzibę w Stanach Zjednoczonych lub w Europie**.</span><span class="sxs-lookup"><span data-stu-id="c7a62-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="c7a62-108">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="c7a62-108">Concepts</span></span>
* <span data-ttu-id="c7a62-109">**Dostępność w danym regionie** odwołuje się do kiedy usługa jest dostępna do użycia.</span><span class="sxs-lookup"><span data-stu-id="c7a62-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="c7a62-110">**Siedziby danych** odwołuje się do przechowywania danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7a62-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="c7a62-111">Dostępność w danym regionie</span><span class="sxs-lookup"><span data-stu-id="c7a62-111">Region availability</span></span>
<span data-ttu-id="c7a62-112">Usługa Azure AD B2C jest dostępna na całym świecie za pośrednictwem chmury publicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a62-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="c7a62-113">To różni się od modelu wykonaj większości innych usług platformy Azure, której połączenie z siedziby danych dostępności.</span><span class="sxs-lookup"><span data-stu-id="c7a62-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="c7a62-114">Zawiera przykłady tego, w obu Azure [produktów dostępna w regionie](https://azure.microsoft.com/regions/services/) strony i [Kalkulator cen Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="c7a62-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="c7a62-115">Rezydencja danych</span><span class="sxs-lookup"><span data-stu-id="c7a62-115">Data residency</span></span>
<span data-ttu-id="c7a62-116">Usługa Azure AD B2C są przechowywane dane użytkownika w Stanach Zjednoczonych lub w Europie.</span><span class="sxs-lookup"><span data-stu-id="c7a62-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="c7a62-117">Siedziby danych jest określana według kraju/regionu, którego wybrano po [tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c7a62-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Zrzut ekranu przedstawiający dzierżawy w wersji zapoznawczej](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="c7a62-119">Dane znajdują się w Stanach Zjednoczonych dla następujących krajach/regionach:</span><span class="sxs-lookup"><span data-stu-id="c7a62-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="c7a62-120">Stany Zjednoczone, Kanada, Kostaryka, Republika Dominikańska, Salwador, Gwatemala, Meksyk, Panama, Portoryko i Trynidad</span><span class="sxs-lookup"><span data-stu-id="c7a62-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="c7a62-121">Dane znajdują się w Europie dla następujących krajach/regionach:</span><span class="sxs-lookup"><span data-stu-id="c7a62-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="c7a62-122">Algierii, Austrii, Azerbejdżanu, Bahrajn, Białorusi, Belgii, Bułgarii, Chorwacji, Cypru, Czechy, Dania, Egiptu, Estonii, Finlandia, Francja, Niemcy, Grecja, Węgierskiej, Islandii, Irlandii, Izrael, Włochy, Jordania, Kazachstanu, Kenii, Kuwejt, Lativa, Liban, Liechtenstein, Lituania, Luksemburg, Macedonia Była Jugosłowiańska Republika, m Alta, Czarnogóry, Maroka, Holandia, Nigerii, Norwegia, Oman, Pakistanu, Polski, Portugalia, Katar, Rumunii, Rosji, Arabia Saudyjska, Serbii, Słowacji, Słowenii, Republika Południowej Afryki, Hiszpanii, Szwecja, Szwajcarii, Tunezji, Turcja, Ukrainy, Zjednoczone Emiraty Arabskie i Zjednoczone Królestwo.</span><span class="sxs-lookup"><span data-stu-id="c7a62-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="c7a62-123">Pozostałe krajach/regionach są właśnie dodawany do listy.</span><span class="sxs-lookup"><span data-stu-id="c7a62-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="c7a62-124">Obecnie można nadal używać usługi Azure AD B2C, wybierając żadnego krajach/regionach powyżej.</span><span class="sxs-lookup"><span data-stu-id="c7a62-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="c7a62-125">Afganistanu, Argentyny, Australii, Brazylia, podrzędnej lokacji, Kolumbii, Ekwadoru, Hongkong SAR, Indie, Indonezji, Iraku, Japonii, Korei, Malezji, Nowa Zelandia, Paragwaju, Peru, Filipiny, Singapur, Sri Lanka, Tajwan, Tajlandii, Urugwaju i Wenezueli.</span><span class="sxs-lookup"><span data-stu-id="c7a62-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="c7a62-126">Dzierżawy w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="c7a62-126">Preview tenant</span></span>
<span data-ttu-id="c7a62-127">Jeśli dzierżawy B2C została utworzona w okresie wersji zapoznawczej usługi Azure AD B2C, istnieje duże prawdopodobieństwo, że Twoje **dzierżawy typu** mówi **dzierżawy w wersji zapoznawczej**.</span><span class="sxs-lookup"><span data-stu-id="c7a62-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="c7a62-128">Jeśli jest to możliwe, musi użyć dzierżawy tylko w przypadku projektowania i testowania, a nie dla aplikacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c7a62-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7a62-129">Brak nie ścieżki migracji z dzierżawy B2C w wersji zapoznawczej do dzierżawy B2C skali produkcji.</span><span class="sxs-lookup"><span data-stu-id="c7a62-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="c7a62-130">Należy pamiętać, że istnieją znane problemy podczas usuwania dzierżawy B2C w wersji zapoznawczej i ponownie utwórz dzierżawy B2C produkcji skali, z tą samą nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="c7a62-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="c7a62-131">Należy utworzyć dzierżawy B2C skali produkcji o nazwie innej domeny.</span><span class="sxs-lookup"><span data-stu-id="c7a62-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Zrzut ekranu przedstawiający dzierżawy w wersji zapoznawczej](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
