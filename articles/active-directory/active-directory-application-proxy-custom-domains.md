---
title: "aaaCustom domen w serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zarządzanie domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD, dlatego tego adresu URL hello aplikacji hello jest hello sama niezależnie od tego, gdzie użytkownicy do niego dostęp."
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
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="07a0d-103">Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="07a0d-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="07a0d-104">Podczas publikowania aplikacji za pośrednictwem serwera Proxy usługi Azure Active Directory aplikacji tworzenia zewnętrznego adresu URL dla Twojego toowhen toogo użytkowników, które działają w zdalnie.</span><span class="sxs-lookup"><span data-stu-id="07a0d-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="07a0d-105">Ten adres URL pobiera hello domyślnej domeny *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="07a0d-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="07a0d-106">Na przykład opublikowaniu aplikacji o nazwie kosztów dzierżawy jest o nazwie Contoso, a następnie hello zewnętrzny adres URL będzie https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="07a0d-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="07a0d-107">Jeśli chcesz toouse z własnej nazwy domeny, skonfiguruj niestandardową domenę na potrzeby aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07a0d-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="07a0d-108">Zaleca się skonfigurowanie domeny niestandardowej dla aplikacji, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="07a0d-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="07a0d-109">Oto niektóre z zalet hello domen niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="07a0d-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="07a0d-110">Użytkowników można uzyskać toohello aplikacji hello sam adres URL, czy działają wewnątrz lub na zewnątrz sieci.</span><span class="sxs-lookup"><span data-stu-id="07a0d-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="07a0d-111">Jeśli wszystkie aplikacje mają hello tych samych adresów URL wewnętrznych i zewnętrznych, linki w jednej aplikacji, które wskazują tooanother nadal toowork nawet spoza sieci firmowej hello.</span><span class="sxs-lookup"><span data-stu-id="07a0d-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="07a0d-112">Kontrolowanie znakowanie i tworzyć adresy URL hello ma.</span><span class="sxs-lookup"><span data-stu-id="07a0d-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="07a0d-113">Skonfigurować własną domenę niestandardową</span><span class="sxs-lookup"><span data-stu-id="07a0d-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="07a0d-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07a0d-114">Prerequisites</span></span>

<span data-ttu-id="07a0d-115">Aby skonfigurować domenę niestandardową, upewnij się, że jest możesz hello wymogów przygotowany:</span><span class="sxs-lookup"><span data-stu-id="07a0d-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="07a0d-116">A [tooAzure usługi Active Directory dodać zweryfikowanej domeny](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="07a0d-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="07a0d-117">Niestandardowe certyfikat dla domeny hello w formie hello pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="07a0d-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="07a0d-118">Aplikację lokalną [opublikowana przy użyciu serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="07a0d-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="07a0d-119">Skonfiguruj domenę niestandardową</span><span class="sxs-lookup"><span data-stu-id="07a0d-119">Configure your custom domain</span></span>

<span data-ttu-id="07a0d-120">Jeśli te wymagania trzy gotowy, wykonaj te kroki tooset się domeny niestandardowej:</span><span class="sxs-lookup"><span data-stu-id="07a0d-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="07a0d-121">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07a0d-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="07a0d-122">Przejdź za**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** i wybierz polecenie aplikacji hello ma toomanage.</span><span class="sxs-lookup"><span data-stu-id="07a0d-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="07a0d-123">Wybierz **serwera Proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="07a0d-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="07a0d-124">W polu zewnętrznego adresu URL hello Użyj tooselect listy rozwijanej hello domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="07a0d-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="07a0d-125">Jeśli nie widzisz domeny na liście hello, następnie go nie zostało zweryfikowane jeszcze.</span><span class="sxs-lookup"><span data-stu-id="07a0d-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="07a0d-126">Wybierz **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="07a0d-126">Select **Save**</span></span>
5. <span data-ttu-id="07a0d-127">Witaj **certyfikatu** staje się aktywny pola, które zostało wyłączone.</span><span class="sxs-lookup"><span data-stu-id="07a0d-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="07a0d-128">Zaznaczenie tego pola.</span><span class="sxs-lookup"><span data-stu-id="07a0d-128">Select this field.</span></span> 

   ![Kliknij przycisk tooupload certyfikatu](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="07a0d-130">Jeśli już przekazany certyfikat dla tej domeny, pole certyfikatu hello Wyświetla informacje o certyfikacie hello.</span><span class="sxs-lookup"><span data-stu-id="07a0d-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="07a0d-131">Przekaż certyfikat PFX hello i podaj hasło hello hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="07a0d-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="07a0d-132">Wybierz **zapisać** toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="07a0d-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="07a0d-133">Dodaj [rekord DNS](../dns/dns-operations-recordsets-portal.md) czy przekierowuje hello nowego adresu URL toohello msappproxy.net domeny zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="07a0d-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="07a0d-134">Wystarczy tylko jeden certyfikat tooupload na domenę niestandardową.</span><span class="sxs-lookup"><span data-stu-id="07a0d-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="07a0d-135">Po przekazaniu certyfikatu można hello domeny niestandardowej podczas publikowania nowej aplikacji i nie ma dodatkowych konfiguracji toodo z wyjątkiem rekordu DNS hello.</span><span class="sxs-lookup"><span data-stu-id="07a0d-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="07a0d-136">Zarządzanie certyfikatami</span><span class="sxs-lookup"><span data-stu-id="07a0d-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="07a0d-137">Format certyfikatu</span><span class="sxs-lookup"><span data-stu-id="07a0d-137">Certificate format</span></span>
<span data-ttu-id="07a0d-138">Nie podlega ograniczeniom na powitania certyfikat podpisu metody.</span><span class="sxs-lookup"><span data-stu-id="07a0d-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="07a0d-139">Obsługiwane są wszystkie kryptografii krzywej eliptycznej (ECC), alternatywnej nazwy podmiotu (SAN) i inne popularne typy certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="07a0d-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="07a0d-140">Można użyć certyfikatu symboli wieloznacznych, jak długo symbolu wieloznacznego hello odpowiada hello żądanego zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="07a0d-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="07a0d-141">Można używać certyfikatów z podpisem własnym, jak również.</span><span class="sxs-lookup"><span data-stu-id="07a0d-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="07a0d-142">Jeśli używasz urzędu certyfikacji prywatnej hello punktu dystrybucji list CRL (punkt dystrybucji punktu odwołania certyfikatu) dla certyfikatu hello powinny być publiczne.</span><span class="sxs-lookup"><span data-stu-id="07a0d-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="07a0d-143">Zmiana domeny hello</span><span class="sxs-lookup"><span data-stu-id="07a0d-143">Changing hello domain</span></span>
<span data-ttu-id="07a0d-144">Wszystkie zweryfikowanych domen są wyświetlane na liście rozwijanej zewnętrznego adresu URL hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07a0d-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="07a0d-145">toochange hello domeny, tylko aktualizacji aplikacji hello do pola.</span><span class="sxs-lookup"><span data-stu-id="07a0d-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="07a0d-146">Jeśli hello domeny, nie jest na liście hello [Dodaj go jako zweryfikowanej domeny](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="07a0d-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="07a0d-147">W przypadku wybrania domeny, która nie ma jeszcze certyfikatu skojarzonego wykonaj kroki 5-7 tooadd hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="07a0d-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="07a0d-148">Następnie upewnij się, że aktualizacja hello tooredirect rekordów DNS z hello nowego zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="07a0d-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="07a0d-149">Zarządzanie certyfikatami</span><span class="sxs-lookup"><span data-stu-id="07a0d-149">Certificate management</span></span>
<span data-ttu-id="07a0d-150">Możesz użyć hello, które same certyfikatu dla wielu zastosowań, chyba że aplikacji hello udostępnianie hoście zewnętrznym.</span><span class="sxs-lookup"><span data-stu-id="07a0d-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="07a0d-151">Zostanie wyświetlone ostrzeżenie po wygaśnięciu certyfikatu informujący tooupload innego certyfikatu za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="07a0d-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="07a0d-152">Jeśli hello certyfikat został odwołany, użytkownicy mogą pojawić ostrzeżenie o zabezpieczeniach podczas uzyskiwania dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="07a0d-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="07a0d-153">Nie możemy wykonać sprawdzanie odwołań certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="07a0d-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="07a0d-154">tooupdate hello certyfikat dla danej aplikacji, przejdź toohello aplikacji i wykonaj kroki 5-7 do konfigurowania domeny niestandardowe na tooupload opublikowanych aplikacji nowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="07a0d-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="07a0d-155">W przypadku hello stary certyfikat nie jest używany przez inne aplikacje, zostaną usunięte automatycznie.</span><span class="sxs-lookup"><span data-stu-id="07a0d-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="07a0d-156">Obecnie wszystkie zarządzania certyfikatami jest stronach poszczególnych aplikacji warto toomanage certyfikaty w kontekście hello hello odpowiednie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="07a0d-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="07a0d-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07a0d-157">Next steps</span></span>
* <span data-ttu-id="07a0d-158">[Włącz rejestrację jednokrotną](active-directory-application-proxy-sso-using-kcd.md) tooyour opublikowane aplikacje przy użyciu uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07a0d-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="07a0d-159">[Włącz dostęp warunkowy](active-directory-application-proxy-conditional-access.md) tooyour opublikowane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="07a0d-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="07a0d-160">Dodaj użytkownika domeny niestandardowej nazwy tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="07a0d-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


