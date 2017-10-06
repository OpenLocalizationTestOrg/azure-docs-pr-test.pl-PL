---
title: "Azure Active Directory B2C: Siedziby dostępności & dane regionu | Dokumentacja firmy Microsoft"
description: "Temat dotyczący hello typów dzierżaw usługi Azure Active Directory B2C"
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
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="b6a15-103">Azure Active Directory B2C: Siedziby dostępności & dane regionu</span><span class="sxs-lookup"><span data-stu-id="b6a15-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="b6a15-104">Dostępność w danym regionie i siedziby danych są dwa bardzo różnych zagadnienia dotyczące inaczej tooAzure AD B2C z resztą hello Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a15-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="b6a15-105">W tym artykule opisano hello różnice między te dwa pojęcia, a następnie porównaj sposobów ich zastosowania tooAzure i usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b6a15-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="b6a15-106">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b6a15-106">Summary</span></span>
<span data-ttu-id="b6a15-107">Usługa Azure AD B2C jest **ogólnie dostępna na całym świecie** z opcją hello **danych siedzibę w Stanach Zjednoczonych lub w Europie**.</span><span class="sxs-lookup"><span data-stu-id="b6a15-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="b6a15-108">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="b6a15-108">Concepts</span></span>
* <span data-ttu-id="b6a15-109">**Dostępność w danym regionie** odwołuje się toowhere usługa jest dostępna do użycia.</span><span class="sxs-lookup"><span data-stu-id="b6a15-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="b6a15-110">**Siedziby danych** odwołuje się toowhere użytkownika są przechowywane dane.</span><span class="sxs-lookup"><span data-stu-id="b6a15-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="b6a15-111">Dostępność w danym regionie</span><span class="sxs-lookup"><span data-stu-id="b6a15-111">Region availability</span></span>
<span data-ttu-id="b6a15-112">Usługa Azure AD B2C jest dostępna na całym świecie za pośrednictwem hello Azure chmury publicznej.</span><span class="sxs-lookup"><span data-stu-id="b6a15-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="b6a15-113">To różni się od modelu hello wykonaj większości innych usług platformy Azure, której połączenie z siedziby danych dostępności.</span><span class="sxs-lookup"><span data-stu-id="b6a15-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="b6a15-114">Zawiera przykłady tego, w obu Azure [produktów dostępna w regionie](https://azure.microsoft.com/regions/services/) strony i hello [Kalkulator cen Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="b6a15-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="b6a15-115">Rezydencja danych</span><span class="sxs-lookup"><span data-stu-id="b6a15-115">Data residency</span></span>
<span data-ttu-id="b6a15-116">Usługa Azure AD B2C są przechowywane dane użytkownika w Stanach Zjednoczonych lub w Europie.</span><span class="sxs-lookup"><span data-stu-id="b6a15-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="b6a15-117">Siedziby danych jest określana według kraju/regionu, którego wybrano po [tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6a15-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Zrzut ekranu przedstawiający dzierżawy w wersji zapoznawczej](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="b6a15-119">Dane znajdują się w Stanach Zjednoczonych hello na powitania po krajów i regionów:</span><span class="sxs-lookup"><span data-stu-id="b6a15-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="b6a15-120">Stany Zjednoczone, Kanada, Kostaryka, Republika Dominikańska, Salwador, Gwatemala, Meksyk, Panama, Portoryko i Trynidad</span><span class="sxs-lookup"><span data-stu-id="b6a15-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="b6a15-121">Dane znajdują się w Europie dla powitania po krajów i regionów:</span><span class="sxs-lookup"><span data-stu-id="b6a15-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="b6a15-122">Algierii, Austrii, Azerbejdżanu, Bahrajn, Białorusi, Belgii, Bułgarii, Chorwacji, Cypru, Czechy, Dania, Egiptu, Estonii, Finlandia, Francja, Niemcy, Grecja, Węgierskiej, Islandii, Irlandii, Izrael, Włochy, Jordania, Kazachstanu, Kenii, Kuwejt, Lativa, Liban, Liechtenstein, Lituania, Luksemburg, Macedonia Była Jugosłowiańska Republika, m Alta, Czarnogóry, Maroka, Holandia, Nigerii, Norwegia, Oman, Pakistanu, Polski, Portugalia, Katar, Rumunii, Rosji, Arabia Saudyjska, Serbii, Słowacji, Słowenii, Republika Południowej Afryki, Hiszpanii, Szwecja, Szwajcarii, Tunezji, Turcja, Ukrainy, Zjednoczone Emiraty Arabskie i Zjednoczone Królestwo.</span><span class="sxs-lookup"><span data-stu-id="b6a15-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="b6a15-123">Hello pozostałych krajach znajdują się w proces hello dodawany toohello listy.</span><span class="sxs-lookup"><span data-stu-id="b6a15-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="b6a15-124">Obecnie można nadal używać usługi Azure AD B2C, wybierając żadnego hello krajach powyżej.</span><span class="sxs-lookup"><span data-stu-id="b6a15-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="b6a15-125">Afganistanu, Argentyny, Australii, Brazylia, podrzędnej lokacji, Kolumbii, Ekwadoru, Hongkong SAR, Indie, Indonezji, Iraku, Japonii, Korei, Malezji, Nowa Zelandia, Paragwaju, Peru, Filipiny, Singapur, Sri Lanka, Tajwan, Tajlandii, Urugwaju i Wenezueli.</span><span class="sxs-lookup"><span data-stu-id="b6a15-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="b6a15-126">Dzierżawy w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="b6a15-126">Preview tenant</span></span>
<span data-ttu-id="b6a15-127">Jeśli dzierżawy B2C została utworzona w okresie wersji zapoznawczej usługi Azure AD B2C, istnieje duże prawdopodobieństwo, że Twoje **dzierżawy typu** mówi **dzierżawy w wersji zapoznawczej**.</span><span class="sxs-lookup"><span data-stu-id="b6a15-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="b6a15-128">Jeśli przypadku hello tylko w przypadku projektowania i testowania, a nie dla aplikacji produkcyjnych możesz korzystać dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b6a15-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6a15-129">Brak nie ścieżki migracji z dzierżawy B2C skali produkcji tooa dzierżawy B2C w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="b6a15-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="b6a15-130">Należy pamiętać, że istnieją znane problemy po usunięciu dzierżawy B2C w wersji zapoznawczej i ponownie utwórz dzierżawy B2C produkcji skali z hello tą samą nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="b6a15-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="b6a15-131">Masz toocreate dzierżawę B2C skali produkcji o nazwie innej domeny.</span><span class="sxs-lookup"><span data-stu-id="b6a15-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Zrzut ekranu przedstawiający dzierżawy w wersji zapoznawczej](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
