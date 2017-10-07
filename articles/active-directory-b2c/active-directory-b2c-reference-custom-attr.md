---
title: "Usługi Azure Active Directory B2C: Atrybuty niestandardowe | Dokumentacja firmy Microsoft"
description: "Jak atrybutów niestandardowych toouse w usłudze Azure Active Directory B2C toocollect informacji o użytkownikach"
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
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="172fa-103">Usługa Azure Active Directory B2C: Użyj niestandardowych atrybutów toocollect informacji o użytkownikach</span><span class="sxs-lookup"><span data-stu-id="172fa-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="172fa-104">Katalogu usługi Azure Active Directory (Azure AD) B2C zawiera zestaw wbudowanych informacji (atrybuty): imię, nazwisko, Miasto, kod pocztowy i innych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="172fa-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="172fa-105">Jednak każda aplikacja dla użytkownika ma unikatowe wymagania, na jakie toogather atrybuty konsumentów.</span><span class="sxs-lookup"><span data-stu-id="172fa-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="172fa-106">Z usługi Azure AD B2C można rozszerzyć hello zestaw atrybutów przechowywanych dla każdego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="172fa-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="172fa-107">Atrybuty niestandardowe można tworzyć na powitania [portalu Azure](https://portal.azure.com/) i używać go w wypełnieniu zasad, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="172fa-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="172fa-108">Może także odczytywać i zapisywać te atrybuty przy użyciu hello [interfejsu API usługi Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="172fa-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="172fa-109">Użyj atrybutów niestandardowych [Azure AD Graph interfejsu API katalogu schematu rozszerzenia](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="172fa-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="172fa-110">Tworzenie niestandardowego atrybutu</span><span class="sxs-lookup"><span data-stu-id="172fa-110">Create a custom attribute</span></span>
1. <span data-ttu-id="172fa-111">[Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="172fa-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="172fa-112">Kliknij przycisk **atrybuty użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="172fa-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="172fa-113">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="172fa-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="172fa-114">Podaj **nazwa** hello atrybutu niestandardowego (na przykład "ShoeSize") i opcjonalnie **opis**.</span><span class="sxs-lookup"><span data-stu-id="172fa-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="172fa-115">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="172fa-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="172fa-116">Tylko Witaj, "String" **— typ danych** jest obecnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="172fa-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="172fa-117">Atrybut niestandardowy Hello jest teraz dostępna w liście hello **atrybuty użytkownika**i do użytku w zasadach tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="172fa-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="172fa-118">Użyj atrybutu niestandardowego w ramach zasad rejestracji</span><span class="sxs-lookup"><span data-stu-id="172fa-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="172fa-119">[Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="172fa-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="172fa-120">Kliknij przycisk **Zasady tworzenia konta**.</span><span class="sxs-lookup"><span data-stu-id="172fa-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="172fa-121">Kliknij przycisk tooopen Twojego zasad rejestracji (na przykład "B2C_1_SiUp") go.</span><span class="sxs-lookup"><span data-stu-id="172fa-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="172fa-122">Kliknij przycisk **Edytuj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="172fa-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="172fa-123">Kliknij przycisk **atrybuty rejestracji** i wybierz hello atrybutu niestandardowego (na przykład "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="172fa-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="172fa-124">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="172fa-124">Click **OK**.</span></span>
5. <span data-ttu-id="172fa-125">Kliknij przycisk **oświadczenia aplikacji** i wybierz hello atrybutu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="172fa-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="172fa-126">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="172fa-126">Click **OK**.</span></span>
6. <span data-ttu-id="172fa-127">Kliknij przycisk **zapisać** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="172fa-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="172fa-128">Można użyć funkcji "Uruchom teraz" hello na powitania zasad tooverify powitania klienta środowisko.</span><span class="sxs-lookup"><span data-stu-id="172fa-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="172fa-129">Powinny teraz zobacz "ShoeSize" hello liście atrybutów zebrane podczas tworzenia konta użytkownika i zobaczyć ją w hello token wysłany tooyour wstecz aplikacji.</span><span class="sxs-lookup"><span data-stu-id="172fa-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="172fa-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="172fa-130">Notes</span></span>
* <span data-ttu-id="172fa-131">Wraz z zasadami tworzenia konta atrybuty niestandardowe można również zasady rejestracji i logowania i profilu edytowanie zasad.</span><span class="sxs-lookup"><span data-stu-id="172fa-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="172fa-132">Jest to znane ograniczenie atrybutów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="172fa-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="172fa-133">Jest tylko utworzyć hello jest używany po raz pierwszy w dowolne zasady, a nie po dodaniu listy toohello **atrybuty użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="172fa-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

