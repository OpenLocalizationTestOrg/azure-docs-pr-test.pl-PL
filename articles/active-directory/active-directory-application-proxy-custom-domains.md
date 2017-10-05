---
title: "Domen niestandardowych w serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zarządzanie domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD, aby adres URL aplikacji jest taki sam, niezależnie od tego, gdzie użytkownicy do niego dostęp."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="4c65d-103">Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c65d-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="4c65d-104">Podczas publikowania aplikacji za pośrednictwem serwera Proxy usługi Azure Active Directory aplikacji, możesz utworzyć zewnętrznego adresu URL dla użytkowników, aby przejść do podczas pracy zdalnej.</span><span class="sxs-lookup"><span data-stu-id="4c65d-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="4c65d-105">Ten adres URL pobiera domyślną domenę *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="4c65d-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="4c65d-106">Na przykład jeśli opublikowana aplikacji o nazwie kosztów i dzierżawy jest o nazwie Contoso, zewnętrzny adres URL może być https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="4c65d-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="4c65d-107">Jeśli chcesz korzystać z własnej nazwy domeny, skonfiguruj niestandardową domenę na potrzeby aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c65d-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="4c65d-108">Zaleca się skonfigurowanie domeny niestandardowej dla aplikacji, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="4c65d-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="4c65d-109">Oto niektóre zalety domen niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="4c65d-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="4c65d-110">Użytkownicy przejść do aplikacji z tego samego adresu URL, czy działają wewnątrz lub na zewnątrz sieci.</span><span class="sxs-lookup"><span data-stu-id="4c65d-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="4c65d-111">Jeśli wszystkie aplikacje tego samego wewnętrzne i zewnętrzne adresy URL, linki w jednej aplikacji, które wskazują na inny nadal działać nawet spoza sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="4c65d-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="4c65d-112">Kontrolowanie znakowanie i tworzyć adresy URL.</span><span class="sxs-lookup"><span data-stu-id="4c65d-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="4c65d-113">Skonfigurować własną domenę niestandardową</span><span class="sxs-lookup"><span data-stu-id="4c65d-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4c65d-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c65d-114">Prerequisites</span></span>

<span data-ttu-id="4c65d-115">Przed skonfigurowaniem niestandardową domenę, upewnij się, że masz następujące wymagania przygotowany:</span><span class="sxs-lookup"><span data-stu-id="4c65d-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="4c65d-116">A [zweryfikowaną domeną dodane do usługi Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c65d-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="4c65d-117">Niestandardowe certyfikat dla domeny, w formie pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="4c65d-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="4c65d-118">Aplikację lokalną [opublikowana przy użyciu serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c65d-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="4c65d-119">Skonfiguruj domenę niestandardową</span><span class="sxs-lookup"><span data-stu-id="4c65d-119">Configure your custom domain</span></span>

<span data-ttu-id="4c65d-120">Jeśli te wymagania trzy gotowy, wykonaj następujące kroki, aby skonfigurować domenę niestandardową:</span><span class="sxs-lookup"><span data-stu-id="4c65d-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="4c65d-121">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c65d-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4c65d-122">Przejdź do **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** i wybierz aplikację, którymi chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="4c65d-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="4c65d-123">Wybierz **serwera Proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4c65d-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="4c65d-124">W polu zewnętrzny adres URL użyj listy rozwijanej, aby wybrać domenę niestandardową.</span><span class="sxs-lookup"><span data-stu-id="4c65d-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="4c65d-125">Jeśli nie widzisz domeny na liście, następnie go nie zostało zweryfikowane jeszcze.</span><span class="sxs-lookup"><span data-stu-id="4c65d-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="4c65d-126">Wybierz **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="4c65d-126">Select **Save**</span></span>
5. <span data-ttu-id="4c65d-127">**Certyfikatu** staje się aktywny pola, które zostało wyłączone.</span><span class="sxs-lookup"><span data-stu-id="4c65d-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="4c65d-128">Zaznaczenie tego pola.</span><span class="sxs-lookup"><span data-stu-id="4c65d-128">Select this field.</span></span> 

   ![Kliknij, aby przekazać certyfikat](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="4c65d-130">Jeśli już przekazany certyfikat dla tej domeny, pole certyfikatu Wyświetla informacje o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="4c65d-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="4c65d-131">Przekazywanie certyfikatu PFX, a następnie wprowadź hasło dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4c65d-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="4c65d-132">Wybierz **zapisać** Aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="4c65d-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="4c65d-133">Dodaj [rekord DNS](../dns/dns-operations-recordsets-portal.md) który przekierowuje do domeny msappproxy.net nowego zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4c65d-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="4c65d-134">Należy przekazać jeden certyfikat dla domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="4c65d-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="4c65d-135">Po przekazaniu certyfikatu można domeny niestandardowej podczas publikowania nowej aplikacji co wymaga dodatkowej konfiguracji, z wyjątkiem rekordu DNS.</span><span class="sxs-lookup"><span data-stu-id="4c65d-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="4c65d-136">Zarządzanie certyfikatami</span><span class="sxs-lookup"><span data-stu-id="4c65d-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="4c65d-137">Format certyfikatu</span><span class="sxs-lookup"><span data-stu-id="4c65d-137">Certificate format</span></span>
<span data-ttu-id="4c65d-138">Nie podlega ograniczeniom certyfikat metodach podpisu.</span><span class="sxs-lookup"><span data-stu-id="4c65d-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="4c65d-139">Obsługiwane są wszystkie kryptografii krzywej eliptycznej (ECC), alternatywnej nazwy podmiotu (SAN) i inne popularne typy certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4c65d-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="4c65d-140">Można użyć certyfikatu symboli wieloznacznych, tak długo, jak symbol wieloznaczny odpowiada żądanego zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4c65d-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="4c65d-141">Można używać certyfikatów z podpisem własnym, jak również.</span><span class="sxs-lookup"><span data-stu-id="4c65d-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="4c65d-142">Jeśli używasz urzędu certyfikacji prywatnej CDP (punkt dystrybucji punktu odwołania certyfikatu) dla certyfikatu powinny być publiczne.</span><span class="sxs-lookup"><span data-stu-id="4c65d-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="4c65d-143">Zmiana domeny</span><span class="sxs-lookup"><span data-stu-id="4c65d-143">Changing the domain</span></span>
<span data-ttu-id="4c65d-144">Wszystkie zweryfikowanych domen są wyświetlane na liście rozwijanej zewnętrzny adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c65d-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="4c65d-145">Aby zmienić domeny, aktualizując pola dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c65d-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="4c65d-146">Jeśli chcesz domeny nie ma na liście [Dodaj go jako zweryfikowanej domeny](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c65d-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="4c65d-147">W przypadku wybrania domeny, która nie ma certyfikatu skojarzonego jeszcze, wykonaj kroki 5-7, aby dodać certyfikat.</span><span class="sxs-lookup"><span data-stu-id="4c65d-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="4c65d-148">Następnie upewnij się, że aktualizacja rekordu DNS, aby przekierować z nowego zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4c65d-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="4c65d-149">Zarządzanie certyfikatami</span><span class="sxs-lookup"><span data-stu-id="4c65d-149">Certificate management</span></span>
<span data-ttu-id="4c65d-150">Tego samego certyfikatu można użyć dla wielu zastosowań, chyba że hoście zewnętrznym udostępniać aplikacje.</span><span class="sxs-lookup"><span data-stu-id="4c65d-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="4c65d-151">Zostanie wyświetlone ostrzeżenie po wygaśnięciu certyfikatu informujący, aby przekazać nowy certyfikat za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="4c65d-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="4c65d-152">Jeśli certyfikat jest odwołany, użytkownicy mogą pojawić ostrzeżenie o zabezpieczeniach podczas uzyskiwania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c65d-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="4c65d-153">Nie możemy wykonać sprawdzanie odwołań certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4c65d-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="4c65d-154">Aby zaktualizować certyfikat dla danej aplikacji, przejdź do aplikacji i wykonaj kroki 5-7 do konfigurowania domeny niestandardowe na opublikowanych aplikacji, aby przekazać nowy certyfikat.</span><span class="sxs-lookup"><span data-stu-id="4c65d-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="4c65d-155">W przypadku stary certyfikat nie jest używany przez inne aplikacje, zostaną usunięte automatycznie.</span><span class="sxs-lookup"><span data-stu-id="4c65d-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="4c65d-156">Wszystkie zarządzania certyfikatami jest obecnie stronach poszczególnych aplikacji, należy do zarządzania certyfikatami w kontekście odpowiednie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="4c65d-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c65d-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c65d-157">Next steps</span></span>
* <span data-ttu-id="4c65d-158">[Włącz rejestrację jednokrotną](active-directory-application-proxy-sso-using-kcd.md) do aplikacji opublikowanych przy użyciu uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c65d-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="4c65d-159">[Włącz dostęp warunkowy](active-directory-application-proxy-conditional-access.md) do opublikowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c65d-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="4c65d-160">Dodawanie niestandardowej nazwy domeny do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c65d-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


