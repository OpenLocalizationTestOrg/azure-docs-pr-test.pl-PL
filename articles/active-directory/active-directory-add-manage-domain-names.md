---
title: "aaaManaging niestandardowych nazw domen w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Pojęcia dotyczące zarządzania i kwestie dotyczące zarządzania domeny niestandardowej w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="50365-103">Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50365-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="50365-104">Nazwa domeny może być identyfikator ważne w przypadku wielu zasobów katalogu w ramach:</span><span class="sxs-lookup"><span data-stu-id="50365-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="50365-105">Użytkownik nazwy lub adresu e-mail użytkownika</span><span class="sxs-lookup"><span data-stu-id="50365-105">A user name or email address for a user</span></span>
* <span data-ttu-id="50365-106">Witaj adres grupy</span><span class="sxs-lookup"><span data-stu-id="50365-106">hello address for a group</span></span>
* <span data-ttu-id="50365-107">Aplikacja Hello identyfikator URI dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="50365-107">hello app ID URI for an application</span></span>

<span data-ttu-id="50365-108">Zasób w usłudze Azure Active Directory (Azure AD) może zawierać nazwy domeny, który jest już sprawdziła toobe należących do katalogu hello zawierającej hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="50365-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="50365-109">Tylko administrator globalny może wykonywać zadania zarządzania domeny w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50365-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50365-110">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="50365-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="50365-111">Aby uzyskać jak toomanage Twojego nazw domen w Centrum administracyjnym hello Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50365-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="50365-112">Nazwa domeny głównej hello zestawu dla katalogu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="50365-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="50365-113">Podczas tworzenia katalogu hello początkową nazwę domeny, takie jak "contoso.onmicrosoft.com", jest również hello podstawowej nazwy domeny dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="50365-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="50365-114">domena podstawowa Hello jest hello domyślna nazwa domeny dla nowego użytkownika, podczas tworzenia nowego użytkownika w hello [klasycznego portalu Azure](https://manage.windowsazure.com/), lub innych portalach, takich jak portal administratora hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="50365-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="50365-115">Usprawnia to proces hello administratora toocreate nowych użytkowników w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="50365-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="50365-116">Nazwa domeny głównej hello toochange dla katalogu:</span><span class="sxs-lookup"><span data-stu-id="50365-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="50365-117">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu konta użytkownika, który jest administratorem globalnym katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50365-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="50365-118">Wybierz **usługi Active Directory** na pasku nawigacyjnym po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="50365-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="50365-119">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="50365-119">Open your directory.</span></span>
4. <span data-ttu-id="50365-120">Wybierz hello **domen** kartę.</span><span class="sxs-lookup"><span data-stu-id="50365-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="50365-121">Wybierz hello **zmiany podstawowego** przycisk na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="50365-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="50365-122">Wybierz domenę hello mają toobe hello nowej domeny głównej dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="50365-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="50365-123">Można zmienić nazwę domeny głównej hello toobe Twojego katalogu zweryfikowanej domeny niestandardowej, która nie jest zintegrowany.</span><span class="sxs-lookup"><span data-stu-id="50365-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="50365-124">Zmiana hello domeny głównej dla katalogu nie zmieni hello nazwy żadnych istniejących użytkowników.</span><span class="sxs-lookup"><span data-stu-id="50365-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="50365-125">Dodaj tooyour nazwy domeny niestandardowej usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="50365-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="50365-126">Możesz dodać too900 domeny niestandardowej nazwy tooeach usługi Azure AD katalogu.</span><span class="sxs-lookup"><span data-stu-id="50365-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="50365-127">Witaj procesu zbyt[Dodawanie dodatkowej niestandardowej nazwy domeny](active-directory-add-domain.md) jest hello takie same dla hello pierwszej niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="50365-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="50365-128">Dodawanie poddomen domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="50365-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="50365-129">Jeśli chcesz tooadd nazwy domen trzeciego poziomu, takie jak katalog tooyour "europe.contoso.com", należy najpierw dodać i sprawdzić, hello domeny drugiego poziomu, np. contoso.com. poddomeny Hello zostanie automatycznie zweryfikowane przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50365-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="50365-130">toosee, który hello poddomeny dodanego została zweryfikowana, Odśwież hello strony w przeglądarce hello, który zawiera listę domen hello w katalogu.</span><span class="sxs-lookup"><span data-stu-id="50365-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="50365-131">Jakie toodo hello DNS rejestratora po zmianie nazwy domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="50365-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="50365-132">Jeśli zmienisz hello DNS rejestratora dla niestandardowej nazwy domeny, możesz kontynuować toouse nazwy domeny niestandardowej z usługą Azure AD, sam bez przerw i dodatkowe zadania konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="50365-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="50365-133">Jeśli korzystasz z niestandardowej nazwy domeny z usługą Office 365, Intune lub innych usług, które opierają się na niestandardowych nazw domen w usłudze Azure AD, zapoznaj się z toohello dokumentacją dla tych usług.</span><span class="sxs-lookup"><span data-stu-id="50365-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="50365-134">Usuń niestandardową nazwę domeny</span><span class="sxs-lookup"><span data-stu-id="50365-134">Delete a custom domain name</span></span>
<span data-ttu-id="50365-135">Czy organizacja już używa tej nazwy domeny, czy należy toouse tej nazwy domeny z inną usługą Azure AD, możesz usunąć niestandardową nazwę domeny z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50365-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="50365-136">toodelete niestandardowej nazwy domeny, należy najpierw upewnić, że żaden zasób w katalogu zależeć hello nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="50365-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="50365-137">Nie można usunąć nazwy domeny z katalogu, jeśli:</span><span class="sxs-lookup"><span data-stu-id="50365-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="50365-138">Każdy użytkownik ma nazwę użytkownika, adres e-mail lub adres serwera proxy, który obejmuje nazwę domeny hello.</span><span class="sxs-lookup"><span data-stu-id="50365-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="50365-139">Każda grupa ma adres e-mail lub adres serwera proxy, który obejmuje nazwę domeny hello.</span><span class="sxs-lookup"><span data-stu-id="50365-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="50365-140">Aplikacje w usługi Azure AD ma identyfikator URI, który obejmuje nazwę domeny hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50365-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="50365-141">Należy zmienić lub usunąć tych zasobów w katalogu usługi Azure AD, przed usunięciem hello niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="50365-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="50365-142">Użyj nazwy domeny toomanage programu PowerShell lub interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="50365-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="50365-143">Większość zadań zarządzania dla nazwy domeny w usłudze Azure Active Directory można również przeprowadzić przy użyciu PowerShell firmy Microsoft lub programowo przy użyciu interfejsu API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="50365-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="50365-144">Przy użyciu programu PowerShell toomanage domen w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="50365-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="50365-145">Przy użyciu nazwy domeny toomanage interfejsu API programu Graph w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="50365-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="50365-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="50365-146">Next steps</span></span>
* [<span data-ttu-id="50365-147">Więcej informacji na temat nazw domen w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="50365-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="50365-148">Zarządzanie niestandardowymi nazwami domen</span><span class="sxs-lookup"><span data-stu-id="50365-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

