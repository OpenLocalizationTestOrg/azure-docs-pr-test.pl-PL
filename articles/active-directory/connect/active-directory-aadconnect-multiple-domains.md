---
title: Azure AD Connect wielu domen
description: "W tym dokumencie opisano instalowanie i konfigurowanie wielu domen najwyższego poziomu z usługi Office 365 i Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="8cd62-103">Obsługa wielu domen do federowania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd62-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="8cd62-104">Poniższa dokumentacja zawiera wskazówki dotyczące sposobu używania wielu najwyższego poziomu domen i poddomen podczas federowania w usłudze Office 365 lub domen usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd62-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="8cd62-105">Obsługa wielu domen najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="8cd62-105">Multiple top-level domain support</span></span>
<span data-ttu-id="8cd62-106">Federowanie wielu, domeny najwyższego poziomu z usługą Azure AD wymaga dodatkowego skonfigurowania, który nie jest wymagany, gdy federowania z jednej domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="8cd62-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="8cd62-107">Gdy domeny jest Sfederowane przy użyciu usługi Azure AD, kilka właściwości są ustawiane w domenie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8cd62-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="8cd62-108">Jeden z nich ważne jest IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="8cd62-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="8cd62-109">Jest to identyfikator URI, który jest używany przez usługę Azure AD, aby zidentyfikować domenę, w której token jest skojarzony z.</span><span class="sxs-lookup"><span data-stu-id="8cd62-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="8cd62-110">Identyfikator URI nie musi rozpoznać cokolwiek, ale musi być prawidłowym identyfikatorem URI.</span><span class="sxs-lookup"><span data-stu-id="8cd62-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="8cd62-111">Domyślnie usługi Azure AD ustawia tę wartość Identyfikator usługi federacyjnej w lokalnej usługi AD FS konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8cd62-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="8cd62-112">Identyfikator usługi federacyjnej jest identyfikatorem URI, który unikatowo identyfikuje usługi federacyjnej.</span><span class="sxs-lookup"><span data-stu-id="8cd62-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="8cd62-113">Usługi federacyjnej jest wystąpieniem programu AD FS, która działa jako usługę tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="8cd62-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="8cd62-114">Możesz wyświetlić IssuerUri za pomocą polecenia programu PowerShell `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="8cd62-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="8cd62-116">Problem występuje, gdy chcemy dodać więcej niż jednej domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="8cd62-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="8cd62-117">Na przykład, załóżmy, że masz konfiguracji federacji między usługą Azure AD oraz w lokalnym środowisku.</span><span class="sxs-lookup"><span data-stu-id="8cd62-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="8cd62-118">W tym dokumencie używam bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="8cd62-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="8cd62-119">Po dodaniu drugiego najwyższego poziomu domeny, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="8cd62-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domeny](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="8cd62-121">Gdy firma Microsoft spróbuje przekonwertować naszych domeny bmfabrikam.com federacyjną, możemy komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="8cd62-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="8cd62-122">Przyczyną jest, usługa Azure AD ma ograniczenie, które nie zezwala na właściwość IssuerUri mają taką samą wartość dla więcej niż jedną domenę.</span><span class="sxs-lookup"><span data-stu-id="8cd62-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Błąd federacyjnego](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="8cd62-124">Parametr SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="8cd62-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="8cd62-125">Do rozwiązania, należy dodać inny IssuerUri, można to zrobić za pomocą `-SupportMultipleDomain` parametru.</span><span class="sxs-lookup"><span data-stu-id="8cd62-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="8cd62-126">Ten parametr jest używany z następujących poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8cd62-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="8cd62-127">Ten parametr umożliwia usługi Azure AD, skonfiguruj IssuerUri, dzięki czemu jest on oparty na nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="8cd62-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="8cd62-128">Są to unikatowy między katalogów w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd62-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="8cd62-129">Za pomocą parametru umożliwia polecenia programu PowerShell zakończyć się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="8cd62-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="8cd62-131">Patrzeć ustawienia naszej nowej domeny bmfabrikam.com zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="8cd62-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="8cd62-133">Należy pamiętać, że `-SupportMultipleDomain` nie powoduje zmiany innych punktów końcowych, które są nadal skonfigurowane, aby wskazywał naszej usługi federacyjnej na adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="8cd62-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="8cd62-134">Innym czynnikiem który `-SupportMultipleDomain` jest jest ona sprawdza, czy system usług AD FS zawiera poprawną wartość wystawca w tokenów wystawionych dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd62-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="8cd62-135">Robi to przez pobranie część nazwy UPN użytkowników domeny i to ustawienie jako domeny w IssuerUri, tj. sufiks https://{upn} / adfs/services/zaufania.</span><span class="sxs-lookup"><span data-stu-id="8cd62-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="8cd62-136">W związku z tym podczas uwierzytelniania do usługi Azure AD lub usługi Office 365, element IssuerUri token użytkownika jest używana do lokalizowania domeny w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd62-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="8cd62-137">Jeśli nie można odnaleźć dopasowania, że uwierzytelnianie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8cd62-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="8cd62-138">Na przykład, jeśli nazwy UPN użytkownika jest bsimon@bmcontoso.com, http://bmcontoso.com/adfs/services/trust zostanie ustawiony element IssuerUri problemy tokenu usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="8cd62-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="8cd62-139">To będzie odpowiadała konfiguracji usługi Azure AD i uwierzytelniania powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="8cd62-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="8cd62-140">Poniżej przedstawiono reguły niestandardowe oświadczeń, który implementuje tę logikę:</span><span class="sxs-lookup"><span data-stu-id="8cd62-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="8cd62-141">Aby użyć przełącznika - SupportMultipleDomain, gdy próbuje dodać nowe lub przekonwertować już dodane do domeny, musisz mieć Instalatora z zaufaniem federacyjnym do pierwotnie ich obsługi.</span><span class="sxs-lookup"><span data-stu-id="8cd62-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="8cd62-142">Jak zaktualizować relacji zaufania między usługami AD FS a usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd62-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="8cd62-143">Nie uaktualniono konfiguracji federacyjnych relacji zaufania między usługami AD FS a wystąpieniem usługi Azure AD, należy ponownie utworzyć zaufanie.</span><span class="sxs-lookup"><span data-stu-id="8cd62-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="8cd62-144">To dlatego kiedy została pierwotnie bez `-SupportMultipleDomain` parametru IssuerUri została skonfigurowana z wartością domyślną.</span><span class="sxs-lookup"><span data-stu-id="8cd62-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="8cd62-145">Na poniższym zrzucie ekranu można zauważyć, że IssuerUri ma ustawioną wartość https://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="8cd62-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="8cd62-146">Teraz tak, jeśli firma Microsoft pomyślnie dodano nową domenę w portalu usługi Azure AD, a następnie spróbuj przekonwertować ją przy użyciu `Convert-MsolDomaintoFederated -DomainName <your domain>`, uzyskujemy następujący błąd.</span><span class="sxs-lookup"><span data-stu-id="8cd62-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="8cd62-148">Jeśli próbujesz dodać `-SupportMultipleDomain` przełącznika możemy zostanie wyświetlony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="8cd62-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="8cd62-150">Po prostu próby uruchomienia `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` w domenie oryginalnego również spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="8cd62-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="8cd62-152">Skorzystaj z poniższych czynności, aby dodać dodatkowe domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="8cd62-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="8cd62-153">Jeśli dodano już domeny i nie używa `-SupportMultipleDomain` start parametru prostych kroków, usuwania i aktualizowania domenę oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="8cd62-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="8cd62-154">Jeśli domeny najwyższego poziomu nie dodano jeszcze można uruchomić z poziomu procedury dodawania domeny przy użyciu programu PowerShell Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8cd62-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="8cd62-155">Wykonaj następujące kroki, aby usunąć zaufanie Online firmy Microsoft i zaktualizować domenę oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="8cd62-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="8cd62-156">Na serwerze federacyjnym usług AD FS Otwórz **Zarządzanie usługami AD FS.**</span><span class="sxs-lookup"><span data-stu-id="8cd62-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="8cd62-157">Po lewej stronie rozwiń **relacje zaufania** i **zaufania jednostek uzależnionych**</span><span class="sxs-lookup"><span data-stu-id="8cd62-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="8cd62-158">Po prawej stronie, należy usunąć **Microsoft Office 365 tożsamość platformy** wpisu.</span><span class="sxs-lookup"><span data-stu-id="8cd62-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="8cd62-159">![Usuń Online firmy Microsoft](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="8cd62-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="8cd62-160">Na komputerze, na którym ma [Azure Active Directory modułu dla środowiska Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) zainstalowanym uruchom następujące polecenie: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="8cd62-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="8cd62-161">Wprowadź nazwę użytkownika i hasło administratora globalnego dla domeny usługi Azure AD, które są federowania w usłudze</span><span class="sxs-lookup"><span data-stu-id="8cd62-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="8cd62-162">W programie PowerShell wpisz:`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="8cd62-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="8cd62-163">W programie PowerShell wpisz `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="8cd62-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="8cd62-164">Jest to oryginalna domeny.</span><span class="sxs-lookup"><span data-stu-id="8cd62-164">This is for the original domain.</span></span>  <span data-ttu-id="8cd62-165">Przy użyciu powyższej domeny, które będzie:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="8cd62-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="8cd62-166">Wykonaj następujące kroki, aby dodać nową domenę najwyższego poziomu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd62-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="8cd62-167">Na komputerze, na którym ma [Azure Active Directory modułu dla środowiska Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) zainstalowanym uruchom następujące polecenie: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="8cd62-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="8cd62-168">Wprowadź nazwę użytkownika i hasło administratora globalnego dla domeny usługi Azure AD, które są federowania w usłudze</span><span class="sxs-lookup"><span data-stu-id="8cd62-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="8cd62-169">W programie PowerShell wpisz:`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="8cd62-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="8cd62-170">W programie PowerShell wpisz:`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="8cd62-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="8cd62-171">Wykonaj następujące kroki, aby dodać nową domenę najwyższego poziomu za pomocą usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8cd62-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="8cd62-172">Uruchamianie usługi Azure AD Connect z pulpitu lub menu start</span><span class="sxs-lookup"><span data-stu-id="8cd62-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="8cd62-173">Wybierz opcję "Dodaj dodatkowe domenowych Azure AD" ![Dodawanie kolejnej domeny usługi Azure AD](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="8cd62-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="8cd62-174">Wprowadź usługi Azure AD i poświadczeń usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="8cd62-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="8cd62-175">Wybierz drugiej domeny, który chcesz skonfigurować na potrzeby federacji.</span><span class="sxs-lookup"><span data-stu-id="8cd62-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="8cd62-176">![Dodawanie kolejnej domeny usługi Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="8cd62-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="8cd62-177">Kliknij przycisk Instaluj</span><span class="sxs-lookup"><span data-stu-id="8cd62-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="8cd62-178">Sprawdź nowej domeny najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="8cd62-178">Verify the new top-level domain</span></span>
<span data-ttu-id="8cd62-179">Za pomocą polecenia programu PowerShell `Get-MsolDomainFederationSettings -DomainName <your domain>`można wyświetlić zaktualizowane IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="8cd62-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="8cd62-180">Poniższy zrzut ekranu przedstawia Federacji ustawienia zostały zaktualizowane na naszych oryginalnego http://bmcontoso.com/adfs/services/trust domeny</span><span class="sxs-lookup"><span data-stu-id="8cd62-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="8cd62-182">I IssuerUri naszej nowej domeny została ustawiona jako https://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="8cd62-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="8cd62-184">Obsługa domen podrzędnych</span><span class="sxs-lookup"><span data-stu-id="8cd62-184">Support for Sub-domains</span></span>
<span data-ttu-id="8cd62-185">Po dodaniu domenę podrzędną, ze względu na sposób Azure AD obsługi domen odziedziczy ustawienia elementu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="8cd62-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="8cd62-186">Oznacza to, że IssuerUri musi być zgodna elementów nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="8cd62-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="8cd62-187">Dlatego umożliwia Powiedz, na przykład, że I bmcontoso.com i następnie dodać corp.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="8cd62-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="8cd62-188">Oznacza to, że IssuerUri dla użytkownika z corp.bmcontoso.com musi być **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="8cd62-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="8cd62-189">Jednak standardowa zasada zaimplementowana powyżej dla usługi Azure AD wygeneruje token z wystawcą jako **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="8cd62-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="8cd62-190">nie będzie odpowiadała domeny wymagane wartości, a uwierzytelnianie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8cd62-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="8cd62-191">Jak włączyć obsługę poddomen</span><span class="sxs-lookup"><span data-stu-id="8cd62-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="8cd62-192">Aby obejść ten problem usług AD FS zaufania jednostki uzależnionej dla witryny Microsoft Online musi zostać zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="8cd62-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="8cd62-193">Aby to zrobić, należy skonfigurować niestandardowej reguły oświadczeń tak, aby taśmy Wyłącz wszelkie poddomen z sufiks nazwy UPN użytkownika podczas tworzenia niestandardowej wartości wystawcy.</span><span class="sxs-lookup"><span data-stu-id="8cd62-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="8cd62-194">Następujące oświadczenie będzie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8cd62-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="8cd62-195">Ostatni numer w wyrażeniu regularnym Ustaw liczbę domeny nadrzędnej istnieje w domenie katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="8cd62-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="8cd62-196">W tym miejscu można mieć bmcontoso.com, niezbędne są dwie domeny nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="8cd62-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="8cd62-197">Jeśli trzy nadrzędnego domeny zostały mają być przechowywane (tj.: corp.bmcontoso.com), następnie numer byłby trzy.</span><span class="sxs-lookup"><span data-stu-id="8cd62-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="8cd62-198">Mogą być wskazywane Eventualy zakresu, zawsze będą dopasowania do dopasowania maksymalną liczbę domen.</span><span class="sxs-lookup"><span data-stu-id="8cd62-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="8cd62-199">"{2,3}" będzie odpowiadała dwóch do trzech domenach (np.: bmfabrikam.com i corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="8cd62-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="8cd62-200">Wykonaj następujące kroki, aby dodać niestandardowe oświadczenia do obsługi domenami podrzędnymi.</span><span class="sxs-lookup"><span data-stu-id="8cd62-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="8cd62-201">Zarządzanie usługami Otwórz AD FS</span><span class="sxs-lookup"><span data-stu-id="8cd62-201">Open AD FS Management</span></span>
2. <span data-ttu-id="8cd62-202">Zaufanie RP Online firmy Microsoft kliknij prawym przyciskiem myszy i wybierz polecenie reguły Edycja oświadczeń</span><span class="sxs-lookup"><span data-stu-id="8cd62-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="8cd62-203">Wybierz trzecie reguły oświadczeń i Zastąp ![Edycja oświadczeń](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="8cd62-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="8cd62-204">Zastąp bieżący oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="8cd62-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Zastąp oświadczeń](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="8cd62-206">Kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="8cd62-206">Click Ok.</span></span>  <span data-ttu-id="8cd62-207">Kliknij przycisk Zastosuj.</span><span class="sxs-lookup"><span data-stu-id="8cd62-207">Click Apply.</span></span>  <span data-ttu-id="8cd62-208">Kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="8cd62-208">Click Ok.</span></span>  <span data-ttu-id="8cd62-209">Zamknij przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="8cd62-209">Close AD FS Management.</span></span>

