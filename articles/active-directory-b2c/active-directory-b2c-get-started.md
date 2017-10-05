---
title: "Usługa Azure Active Directory B2C: Tworzenie dzierżawy usługi Azure Active Directory B2C | Dokumentacja firmy Microsoft"
description: "Temat dotyczący sposobu tworzenia dzierżawy usługi Azure Active Directory B2C"
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
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="d2db4-103">Tworzenie dzierżawy usługi Azure Active Directory B2C w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d2db4-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="d2db4-104">Edytowany przez Sipi.</span><span class="sxs-lookup"><span data-stu-id="d2db4-104">Edited by Sipi.</span></span>

<span data-ttu-id="d2db4-105">Ta opcja szybkiego startu ułatwia tworzenie dzierżawy usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="d2db4-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="d2db4-106">Po zakończeniu, masz dzierżawę B2C do użycia na potrzeby rejestrowania aplikacji B2C.</span><span class="sxs-lookup"><span data-stu-id="d2db4-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2db4-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d2db4-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="d2db4-108">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d2db4-108">Log in to Azure</span></span>

<span data-ttu-id="d2db4-109">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2db4-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d2db4-110">Tworzenie dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d2db4-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="d2db4-111">Nie można włączyć funkcji B2C w istniejących dzierżawców.</span><span class="sxs-lookup"><span data-stu-id="d2db4-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="d2db4-112">Musisz utworzyć dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d2db4-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="d2db4-113">Gratulacje, utworzono dzierżawy usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d2db4-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="d2db4-114">Jesteś administratorem globalnym dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="d2db4-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="d2db4-115">W razie potrzeby możesz dodawać innych administratorów globalnych.</span><span class="sxs-lookup"><span data-stu-id="d2db4-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="d2db4-116">Aby przełączyć się do nowej dzierżawy, kliknij przycisk *Zarządzanie nowe łącze dzierżawy*.</span><span class="sxs-lookup"><span data-stu-id="d2db4-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Zarządzanie nowe łącze dzierżawy](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="d2db4-118">Jeśli planujesz używać dzierżawy B2C do aplikacji produkcyjnej, przeczytaj artykuł dotyczący [skali produkcji a dzierżawcy usługi B2C w wersji zapoznawczej](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="d2db4-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="d2db4-119">Istnieją znane problemy podczas usuwania istniejącej dzierżawy B2C i utwórz go ponownie z tą samą nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="d2db4-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="d2db4-120">Musisz utworzyć dzierżawy B2C o nazwie innej domeny.</span><span class="sxs-lookup"><span data-stu-id="d2db4-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="d2db4-121">Link do subskrypcji dzierżawy</span><span class="sxs-lookup"><span data-stu-id="d2db4-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="d2db4-122">Musisz połączyć dzierżawy usługi Azure AD B2C do subskrypcji platformy Azure, aby włączyć wszystkie funkcje B2C i opłacać opłaty za użycie.</span><span class="sxs-lookup"><span data-stu-id="d2db4-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="d2db4-123">Aby dowiedzieć się więcej, przeczytaj [w tym artykule](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="d2db4-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="d2db4-124">Jeśli nie możesz połączyć dzierżawy usługi Azure AD B2C do subskrypcji platformy Azure, niektóre funkcje jest zablokowany, a zostanie wyświetlony komunikat ostrzegawczy ("bez subskrypcji połączone z tej dzierżawy B2C lub na potrzeby subskrypcji uwagi.") w ustawieniach usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="d2db4-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="d2db4-125">Należy wykonać ten krok, przed wysłaniem aplikacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d2db4-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="d2db4-126">Łatwy dostęp do ustawień</span><span class="sxs-lookup"><span data-stu-id="d2db4-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="d2db4-127">Można także przejść do bloku, wprowadzając `Azure AD B2C` w **wyszukiwania zasobów** w górnej części portalu.</span><span class="sxs-lookup"><span data-stu-id="d2db4-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="d2db4-128">Na liście wyników wybierz **usługi Azure AD B2C** B2C blok ustawień dostępu do.</span><span class="sxs-lookup"><span data-stu-id="d2db4-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2db4-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d2db4-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2db4-130">Rejestrowanie aplikacji B2C w dzierżawcy usługi B2C</span><span class="sxs-lookup"><span data-stu-id="d2db4-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
