---
title: "Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="f6c76-103">Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6c76-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="f6c76-104">Nazwa domeny może być identyfikator ważne w przypadku wielu zasobów katalogu w ramach:</span><span class="sxs-lookup"><span data-stu-id="f6c76-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="f6c76-105">Użytkownik nazwy lub adresu e-mail użytkownika</span><span class="sxs-lookup"><span data-stu-id="f6c76-105">A user name or email address for a user</span></span>
* <span data-ttu-id="f6c76-106">Adres grupy</span><span class="sxs-lookup"><span data-stu-id="f6c76-106">The address for a group</span></span>
* <span data-ttu-id="f6c76-107">Identyfikator URI aplikacji dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="f6c76-107">The app ID URI for an application</span></span>

<span data-ttu-id="f6c76-108">Zasób w usłudze Azure Active Directory (Azure AD) może zawierać nazwy domeny, która została już zweryfikowana należeć do katalogu, który zawiera zasób.</span><span class="sxs-lookup"><span data-stu-id="f6c76-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="f6c76-109">Tylko administrator globalny może wykonywać zadania zarządzania domeny w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6c76-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6c76-110">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="f6c76-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="f6c76-111">Jak zarządzać nazwy domeny w Centrum administracyjnym usługi Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6c76-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="f6c76-112">Ustaw nazwę domeny głównej dla katalogu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c76-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="f6c76-113">Podczas tworzenia katalogu z początkowej nazwy domeny, takie jak "contoso.onmicrosoft.com", jest również nazwę domeny głównej dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="f6c76-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="f6c76-114">Domena podstawowa jest domyślna nazwa domeny dla nowego użytkownika, podczas tworzenia nowego użytkownika w [klasycznego portalu Azure](https://manage.windowsazure.com/), lub innych portalach, takich jak portalu administracyjnego usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f6c76-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="f6c76-115">Usprawnia to proces dla administratora utworzyć nowych użytkowników w portalu.</span><span class="sxs-lookup"><span data-stu-id="f6c76-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="f6c76-116">Aby zmienić nazwę domeny głównej dla katalogu:</span><span class="sxs-lookup"><span data-stu-id="f6c76-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="f6c76-117">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu konta użytkownika będącego administratorem globalnym katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6c76-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="f6c76-118">Wybierz **usługi Active Directory** na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="f6c76-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="f6c76-119">Otwórz katalog.</span><span class="sxs-lookup"><span data-stu-id="f6c76-119">Open your directory.</span></span>
4. <span data-ttu-id="f6c76-120">Wybierz **domen** kartę.</span><span class="sxs-lookup"><span data-stu-id="f6c76-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="f6c76-121">Wybierz **zmiany podstawowego** przycisk paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="f6c76-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="f6c76-122">Wybierz domenę, w której mają być nowej domeny głównej dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="f6c76-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="f6c76-123">Można zmienić nazwę domeny głównej dla katalogu jako zweryfikowanej domeny niestandardowej, która nie jest zintegrowany.</span><span class="sxs-lookup"><span data-stu-id="f6c76-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="f6c76-124">Zmiana domeny podstawowej dla katalogu nie spowoduje zmiany nazwy użytkownika dla wszystkich istniejących użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f6c76-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="f6c76-125">Dodawanie niestandardowych nazw domen do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c76-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="f6c76-126">Maksymalnie 900 nazw domen niestandardowych można dodać do każdego katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6c76-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="f6c76-127">Proces [Dodawanie dodatkowej niestandardowej nazwy domeny](active-directory-add-domain.md) jest taki sam dla pierwszej nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="f6c76-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="f6c76-128">Dodawanie poddomen domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="f6c76-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="f6c76-129">Jeśli chcesz dodać nazwy domen trzeciego poziomu, takie jak "europe.contoso.com" do katalogu, należy najpierw dodać i zweryfikować domeny drugiego poziomu, np. contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f6c76-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="f6c76-130">Poddomeny zostanie automatycznie zweryfikowane przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6c76-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="f6c76-131">Aby wyświetlić zweryfikowaniu poddomeny, który właśnie został dodany, Odśwież stronę w przeglądarce, która zawiera listę domen w katalogu.</span><span class="sxs-lookup"><span data-stu-id="f6c76-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="f6c76-132">Co robić w przypadku zmiany nazwy domeny niestandardowej rejestratora DNS.</span><span class="sxs-lookup"><span data-stu-id="f6c76-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="f6c76-133">Jeśli zmienisz rejestratora DNS dla nazwy domeny niestandardowej, można korzystać z nazwy domeny niestandardowej z usługą Azure AD, sam bez przerw i dodatkowe zadania konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="f6c76-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="f6c76-134">Jeśli korzystasz z niestandardowej nazwy domeny z usługą Office 365, Intune lub innych usług, które opierają się na niestandardowych nazw domen w usłudze Azure AD, można znaleźć w dokumentacji tych usług.</span><span class="sxs-lookup"><span data-stu-id="f6c76-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="f6c76-135">Usuń niestandardową nazwę domeny</span><span class="sxs-lookup"><span data-stu-id="f6c76-135">Delete a custom domain name</span></span>
<span data-ttu-id="f6c76-136">Czy organizacja już używa tej nazwy domeny, czy należy użyć tej nazwy domeny z inną usługą Azure AD, możesz usunąć niestandardową nazwę domeny z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6c76-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="f6c76-137">Aby usunąć niestandardową nazwę domeny, musi najpierw upewnić, że żaden zasób w katalogu zależą od nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="f6c76-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="f6c76-138">Nie można usunąć nazwy domeny z katalogu, jeśli:</span><span class="sxs-lookup"><span data-stu-id="f6c76-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="f6c76-139">Każdy użytkownik ma nazwę użytkownika, adres e-mail lub adres serwera proxy, który obejmuje nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="f6c76-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="f6c76-140">Każda grupa ma adres e-mail lub adres serwera proxy, która zawiera nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="f6c76-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="f6c76-141">Aplikacje w usługi Azure AD ma identyfikator URI, który obejmuje nazwę domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f6c76-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="f6c76-142">Należy zmienić lub usunąć tych zasobów w katalogu usługi Azure AD, przed usunięciem nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="f6c76-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="f6c76-143">Użyj programu PowerShell lub interfejsu API programu Graph, zarządzanie nazwami domen</span><span class="sxs-lookup"><span data-stu-id="f6c76-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="f6c76-144">Większość zadań zarządzania dla nazwy domeny w usłudze Azure Active Directory można również przeprowadzić przy użyciu PowerShell firmy Microsoft lub programowo przy użyciu interfejsu API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="f6c76-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="f6c76-145">Zarządzanie nazwami domen w usłudze Azure AD przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6c76-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="f6c76-146">Zarządzanie nazwami domen w usłudze Azure AD przy użyciu interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="f6c76-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="f6c76-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6c76-147">Next steps</span></span>
* [<span data-ttu-id="f6c76-148">Więcej informacji na temat nazw domen w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6c76-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="f6c76-149">Zarządzanie niestandardowymi nazwami domen</span><span class="sxs-lookup"><span data-stu-id="f6c76-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

