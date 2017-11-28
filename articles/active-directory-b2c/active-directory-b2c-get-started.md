---
title: "Usługa Azure Active Directory B2C: Tworzenie dzierżawy usługi Azure Active Directory B2C | Dokumentacja firmy Microsoft"
description: "Temat dotyczący sposobu dzierżawy usługi Azure Active Directory B2C toocreate"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="fa450-103">Tworzenie dzierżawy usługi Azure Active Directory B2C w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="fa450-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="fa450-104">Edytowany przez Sipi.</span><span class="sxs-lookup"><span data-stu-id="fa450-104">Edited by Sipi.</span></span>

<span data-ttu-id="fa450-105">Ta opcja szybkiego startu ułatwia tworzenie dzierżawy usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="fa450-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="fa450-106">Po zakończeniu, masz toouse dzierżawy B2C do rejestrowania aplikacji B2C.</span><span class="sxs-lookup"><span data-stu-id="fa450-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa450-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa450-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="fa450-108">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="fa450-108">Log in tooAzure</span></span>

<span data-ttu-id="fa450-109">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fa450-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="fa450-110">Tworzenie dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fa450-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="fa450-111">Nie można włączyć funkcji B2C w istniejących dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="fa450-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="fa450-112">Należy toocreate dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fa450-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="fa450-113">Gratulacje, utworzono dzierżawy usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="fa450-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="fa450-114">Jesteś administratorem globalnym dzierżawcy hello.</span><span class="sxs-lookup"><span data-stu-id="fa450-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="fa450-115">W razie potrzeby możesz dodawać innych administratorów globalnych.</span><span class="sxs-lookup"><span data-stu-id="fa450-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="fa450-116">tooyour tooswitch nowej dzierżawy, kliknij przycisk hello *Zarządzanie nowe łącze dzierżawy*.</span><span class="sxs-lookup"><span data-stu-id="fa450-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Zarządzanie nowe łącze dzierżawy](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="fa450-118">Jeśli planujesz toouse dzierżawy B2C do aplikacji produkcyjnej, przeczytaj artykuł hello na [skali produkcji a dzierżawcy usługi B2C w wersji zapoznawczej](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="fa450-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="fa450-119">Istnieją znane problemy podczas usuwania istniejących B2C dzierżawy i utwórz ją ponownie hello tą samą nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="fa450-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="fa450-120">Należy toocreate dzierżawy B2C o nazwie innej domeny.</span><span class="sxs-lookup"><span data-stu-id="fa450-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="fa450-121">Połączyć subskrypcję tooyour dzierżawy</span><span class="sxs-lookup"><span data-stu-id="fa450-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="fa450-122">Należy toolink programu Azure AD B2C dzierżawy wszystkie funkcje B2C tooyour tooenable subskrypcji platformy Azure i opłacać opłaty za użycie.</span><span class="sxs-lookup"><span data-stu-id="fa450-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="fa450-123">toolearn, przeczytaj [w tym artykule](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="fa450-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="fa450-124">Jeśli nie możesz połączyć Twoje tooyour dzierżawy usługi Azure AD B2C subskrypcji platformy Azure, niektóre funkcje jest zablokowany, a zostanie wyświetlony komunikat ostrzegawczy ("bez subskrypcji połączonego toothis B2C dzierżawy lub hello subskrypcji wymaga uwagi.") w ustawieniach hello B2C.</span><span class="sxs-lookup"><span data-stu-id="fa450-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="fa450-125">Należy wykonać ten krok, przed wysłaniem aplikacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="fa450-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="fa450-126">Toosettings łatwy dostęp</span><span class="sxs-lookup"><span data-stu-id="fa450-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="fa450-127">Można także przejść do bloku hello wprowadzając `Azure AD B2C` w **wyszukiwania zasobów** u góry hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="fa450-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="fa450-128">Na liście wyników hello, wybierz **usługi Azure AD B2C** tooaccess hello bloku ustawienia B2C.</span><span class="sxs-lookup"><span data-stu-id="fa450-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa450-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa450-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fa450-130">Rejestrowanie aplikacji B2C w dzierżawcy usługi B2C</span><span class="sxs-lookup"><span data-stu-id="fa450-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
