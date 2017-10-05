---
title: "Usługi Azure Active Directory B2C: Atrybuty niestandardowe | Dokumentacja firmy Microsoft"
description: "Jak używać atrybutów niestandardowych w usłudze Azure Active Directory B2C do zbierania informacji o użytkownikach"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="a9af2-103">Usługa Azure Active Directory B2C: Wykorzystaj niestandardowe atrybuty do zbierania informacji o użytkownikach</span><span class="sxs-lookup"><span data-stu-id="a9af2-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="a9af2-104">Katalogu usługi Azure Active Directory (Azure AD) B2C zawiera zestaw wbudowanych informacji (atrybuty): imię, nazwisko, Miasto, kod pocztowy i innych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="a9af2-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="a9af2-105">Jednak każda aplikacja dla użytkownika ma unikatowe wymagania na atrybuty, jakie można zebrać konsumentów.</span><span class="sxs-lookup"><span data-stu-id="a9af2-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="a9af2-106">Z usługi Azure AD B2C można rozszerzyć zestaw atrybutów przechowywanych dla każdego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a9af2-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="a9af2-107">Atrybuty niestandardowe można tworzyć na [portalu Azure](https://portal.azure.com/) i używać go w wypełnieniu zasad, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a9af2-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="a9af2-108">Może także odczytywać i zapisywać te atrybuty za pomocą [interfejsu API usługi Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a9af2-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a9af2-109">Użyj atrybutów niestandardowych [Azure AD Graph interfejsu API katalogu schematu rozszerzenia](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9af2-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="a9af2-110">Tworzenie niestandardowego atrybutu</span><span class="sxs-lookup"><span data-stu-id="a9af2-110">Create a custom attribute</span></span>
1. <span data-ttu-id="a9af2-111">[Wykonaj następujące kroki, aby przejść do bloku funkcji B2C w portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="a9af2-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="a9af2-112">Kliknij przycisk **atrybuty użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="a9af2-113">Kliknij pozycję **+Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="a9af2-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a9af2-114">Podaj **nazwa** atrybutu niestandardowego (na przykład "ShoeSize") i opcjonalnie **opis**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="a9af2-115">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a9af2-116">Tylko "String" **— typ danych** jest obecnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="a9af2-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="a9af2-117">Atrybut niestandardowy jest teraz dostępna na liście **atrybuty użytkownika**i do użytku w zasadach tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="a9af2-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="a9af2-118">Użyj atrybutu niestandardowego w ramach zasad rejestracji</span><span class="sxs-lookup"><span data-stu-id="a9af2-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="a9af2-119">[Wykonaj następujące kroki, aby przejść do bloku funkcji B2C w portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="a9af2-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="a9af2-120">Kliknij przycisk **Zasady tworzenia konta**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="a9af2-121">Kliknij zasady rejestracji (na przykład "B2C_1_SiUp"), aby go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="a9af2-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="a9af2-122">Kliknij przycisk **Edytuj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="a9af2-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="a9af2-123">Kliknij przycisk **atrybuty rejestracji** i wybierz atrybutu niestandardowego (na przykład "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="a9af2-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="a9af2-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-124">Click **OK**.</span></span>
5. <span data-ttu-id="a9af2-125">Kliknij przycisk **oświadczenia aplikacji** i wybierz atrybut niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="a9af2-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="a9af2-126">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-126">Click **OK**.</span></span>
6. <span data-ttu-id="a9af2-127">Kliknij przycisk **zapisać** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="a9af2-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="a9af2-128">Za pomocą funkcji "Uruchom teraz" na zasady można sprawdzić w środowisku użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a9af2-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="a9af2-129">Powinny teraz zobacz "ShoeSize" na liście atrybutów zebrane podczas tworzenia konta użytkownika i zobaczyć ją w tokenie wysyłane z powrotem do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9af2-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="a9af2-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a9af2-130">Notes</span></span>
* <span data-ttu-id="a9af2-131">Wraz z zasadami tworzenia konta atrybuty niestandardowe można również zasady rejestracji i logowania i profilu edytowanie zasad.</span><span class="sxs-lookup"><span data-stu-id="a9af2-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="a9af2-132">Jest to znane ograniczenie atrybutów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="a9af2-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="a9af2-133">Jest ona tylko tworzony po raz pierwszy jest używany w żadnych zasad, a nie, po dodaniu go do listy **atrybuty użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a9af2-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

