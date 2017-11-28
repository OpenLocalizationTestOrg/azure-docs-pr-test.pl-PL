---
title: "Łączenie wielu domen aaaAzure AD"
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
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="c5661-103">Obsługa wielu domen do federowania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5661-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="c5661-104">Witaj następująca dokumentacja znajdują się wskazówki dotyczące toouse wiele domen najwyższego poziomu i poddomen podczas federowania z domenami usługi Office 365 lub Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5661-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="c5661-105">Obsługa wielu domen najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="c5661-105">Multiple top-level domain support</span></span>
<span data-ttu-id="c5661-106">Federowanie wielu, domeny najwyższego poziomu z usługą Azure AD wymaga dodatkowego skonfigurowania, który nie jest wymagany, gdy federowania z jednej domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="c5661-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="c5661-107">Gdy domeny jest Sfederowane przy użyciu usługi Azure AD, kilka właściwości są ustawiane na powitania domeny na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c5661-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="c5661-108">Jeden z nich ważne jest IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="c5661-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="c5661-109">Jest to identyfikator URI, który jest używany przez usługi Azure AD tooidentify jest skojarzony z domeny hello hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="c5661-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="c5661-110">Witaj identyfikatora URI nie musi tooresolve tooanything, ale musi być prawidłowym identyfikatorem URI.</span><span class="sxs-lookup"><span data-stu-id="c5661-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="c5661-111">Domyślnie usługi Azure AD ustawia wartość toohello identyfikator usługi federacyjnej hello w lokalnej usługi AD FS konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c5661-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="c5661-112">Identyfikator usługi federacyjnej Hello jest identyfikatorem URI, który unikatowo identyfikuje usługi federacyjnej.</span><span class="sxs-lookup"><span data-stu-id="c5661-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="c5661-113">Usługa federacyjna Hello jest wystąpienia usług AD FS tej funkcji jako hello usługi tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="c5661-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="c5661-114">Można wyświetlić IssuerUri za pomocą polecenia programu PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="c5661-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="c5661-116">Problem występuje, gdy chcemy tooadd więcej niż jednej domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="c5661-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="c5661-117">Na przykład, załóżmy, że masz konfiguracji federacji między usługą Azure AD oraz w lokalnym środowisku.</span><span class="sxs-lookup"><span data-stu-id="c5661-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="c5661-118">W tym dokumencie używam bmcontoso.com.  Po dodaniu drugiego najwyższego poziomu domeny, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="c5661-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domeny](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="c5661-120">Gdy firma Microsoft spróbuje tooconvert naszych toobe domeny bmfabrikam.com federacyjnych, możemy komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c5661-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="c5661-121">Witaj przyczyną tego błędu jest, usługa Azure AD ma ograniczenie, które nie zezwala na powitania hello toohave właściwości IssuerUri samą wartość dla więcej niż jedną domenę.</span><span class="sxs-lookup"><span data-stu-id="c5661-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Błąd federacyjnego](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="c5661-123">Parametr SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="c5661-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="c5661-124">tooworkaround, potrzebujemy tooadd różnych IssuerUri, można to zrobić za pomocą hello `-SupportMultipleDomain` parametru.</span><span class="sxs-lookup"><span data-stu-id="c5661-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="c5661-125">Ten parametr jest używany z hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5661-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="c5661-126">Ten parametr umożliwia usługi Azure AD, skonfiguruj hello IssuerUri, dzięki czemu jest on oparty na powitania nazwę domeny hello.</span><span class="sxs-lookup"><span data-stu-id="c5661-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="c5661-127">Są to unikatowy między katalogów w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5661-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="c5661-128">Za pomocą parametru hello umożliwia toocomplete polecenia programu PowerShell hello pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c5661-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="c5661-130">Patrzeć hello ustawienia naszej nowej domeny bmfabrikam.com można wyświetlić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c5661-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="c5661-132">Należy pamiętać, że `-SupportMultipleDomain` hello nie powoduje zmiany innych punktów końcowych, które są nadal skonfigurowane usługi federacyjnej tooour toopoint na adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="c5661-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="c5661-133">Innym czynnikiem który `-SupportMultipleDomain` jest jest ona sprawdza, czy hello AD FS systemu zawiera poprawną wartość wystawcy hello w tokenów wystawionych dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5661-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="c5661-134">Robi to przez pobranie hello domeny część użytkowników hello UPN i to ustawienie jako domeny hello w hello IssuerUri, tj. sufiks https://{upn} / adfs/services/zaufania.</span><span class="sxs-lookup"><span data-stu-id="c5661-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="c5661-135">W związku z tym podczas uwierzytelniania tooAzure AD lub usługi Office 365, element IssuerUri hello w tokenie użytkownika hello jest używane toolocate hello domeny w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5661-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="c5661-136">Jeśli nie można odnaleźć dopasowania, uwierzytelniania hello zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c5661-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="c5661-137">Na przykład, jeśli nazwy UPN użytkownika jest bsimon@bmcontoso.com, element IssuerUri hello hello tokenu usług AD FS problemy zostaną ustawione toohttp://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="c5661-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="c5661-138">To będzie odpowiadała konfiguracji usługi Azure AD hello i uwierzytelniania powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="c5661-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="c5661-139">następujące Hello jest reguły oświadczeń dostosowane hello, który implementuje tę logikę:</span><span class="sxs-lookup"><span data-stu-id="c5661-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="c5661-140">W kolejności toouse hello - SupportMultipleDomain Przełącz podczas próby tooadd nowych lub przekonwertować już dodane domeny, konieczne toohave Instalatora toosupport Twojego zaufania federacyjnego pierwotnie je.</span><span class="sxs-lookup"><span data-stu-id="c5661-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="c5661-141">Jak tooupdate hello zaufania między usługami AD FS a usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5661-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="c5661-142">Jeśli nie uaktualniono konfiguracji hello federacyjnych zaufania między usługami AD FS a wystąpieniem usługi Azure AD, może być konieczne toore-tworzenia tego zaufania.</span><span class="sxs-lookup"><span data-stu-id="c5661-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="c5661-143">To dlatego, gdy została pierwotnie bez hello `-SupportMultipleDomain` parametru hello IssuerUri jest ustawiona z wartością domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="c5661-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="c5661-144">W hello zrzut ekranu poniżej można zauważyć, że hello IssuerUri ustawiono toohttps://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="c5661-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="c5661-145">Teraz tak, jeśli firma Microsoft pomyślnie dodano nową domenę w portalu hello Azure AD, a następnie spróbuj tooconvert za pomocą `Convert-MsolDomaintoFederated -DomainName <your domain>`, uzyskujemy hello następujący błąd.</span><span class="sxs-lookup"><span data-stu-id="c5661-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="c5661-147">Jeśli spróbujesz tooadd hello `-SupportMultipleDomain` przełącznika będzie Otrzymaliśmy hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c5661-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="c5661-149">Po prostu próby toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` na powitania pierwotnej domeny również spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="c5661-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="c5661-151">Wykonaj kroki hello poniżej tooadd dodatkowej domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="c5661-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="c5661-152">Jeśli dodano już domeny i nie użyto hello `-SupportMultipleDomain` start parametru hello prostych kroków, usuwania i aktualizowania domenę oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="c5661-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="c5661-153">Jeśli domeny najwyższego poziomu nie dodano jeszcze można uruchomić z poziomu hello kroki dodawania domeny przy użyciu programu PowerShell Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c5661-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="c5661-154">Użyj hello następujące kroki tooremove hello Online firmy Microsoft zaufania i zaktualizuj domenę oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="c5661-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="c5661-155">Na serwerze federacyjnym usług AD FS Otwórz **Zarządzanie usługami AD FS.**</span><span class="sxs-lookup"><span data-stu-id="c5661-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="c5661-156">Na powitania po lewej stronie rozwiń **relacje zaufania** i **zaufania jednostek uzależnionych**</span><span class="sxs-lookup"><span data-stu-id="c5661-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="c5661-157">Na powitania prawo, usunąć hello **Microsoft Office 365 tożsamość platformy** wpisu.</span><span class="sxs-lookup"><span data-stu-id="c5661-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="c5661-158">![Usuń Online firmy Microsoft](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="c5661-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="c5661-159">Na komputerze, na którym ma [Azure Active Directory modułu dla środowiska Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) zainstalowanym uruchom następujące hello: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="c5661-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="c5661-160">Wprowadź hello użytkownika i hasło administratora globalnego dla domeny usługi Azure AD hello federowania w usłudze</span><span class="sxs-lookup"><span data-stu-id="c5661-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="c5661-161">W programie PowerShell wpisz:`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="c5661-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="c5661-162">W programie PowerShell wpisz `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="c5661-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="c5661-163">Jest to hello pierwotnej domeny.</span><span class="sxs-lookup"><span data-stu-id="c5661-163">This is for hello original domain.</span></span>  <span data-ttu-id="c5661-164">Za pomocą hello powyżej domen, które będzie:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="c5661-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="c5661-165">Użyj hello następujące kroki tooadd hello nowej domeny najwyższego poziomu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5661-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="c5661-166">Na komputerze, na którym ma [Azure Active Directory modułu dla środowiska Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) zainstalowanym uruchom następujące hello: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="c5661-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="c5661-167">Wprowadź hello użytkownika i hasło administratora globalnego dla domeny usługi Azure AD hello federowania w usłudze</span><span class="sxs-lookup"><span data-stu-id="c5661-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="c5661-168">W programie PowerShell wpisz:`Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="c5661-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="c5661-169">W programie PowerShell wpisz:`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="c5661-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="c5661-170">Użyj następujących hello kroki tooadd hello nowej domeny najwyższego poziomu za pomocą usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c5661-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="c5661-171">Uruchamianie usługi Azure AD Connect z pulpitu hello lub menu start</span><span class="sxs-lookup"><span data-stu-id="c5661-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="c5661-172">Wybierz opcję "Dodaj dodatkowe domenowych Azure AD" ![Dodawanie kolejnej domeny usługi Azure AD](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="c5661-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="c5661-173">Wprowadź usługi Azure AD i poświadczeń usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5661-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="c5661-174">Wybierz domenę drugi hello mają tooconfigure dla Federacji.</span><span class="sxs-lookup"><span data-stu-id="c5661-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="c5661-175">![Dodawanie kolejnej domeny usługi Azure AD](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="c5661-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="c5661-176">Kliknij przycisk Instaluj</span><span class="sxs-lookup"><span data-stu-id="c5661-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="c5661-177">Sprawdź hello nowej domeny najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="c5661-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="c5661-178">Za pomocą polecenia programu PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`można wyświetlić hello zaktualizowane IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="c5661-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="c5661-179">Poniższy zrzut ekranu Hello pokazuje ustawienia Federacji hello zostały zaktualizowane na naszych oryginalnego http://bmcontoso.com/adfs/services/trust domeny</span><span class="sxs-lookup"><span data-stu-id="c5661-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="c5661-181">Witaj IssuerUri naszej nowej domeny skonfigurowano toohttps://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="c5661-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="c5661-183">Obsługa domen podrzędnych</span><span class="sxs-lookup"><span data-stu-id="c5661-183">Support for Sub-domains</span></span>
<span data-ttu-id="c5661-184">Podczas dodawania domeny podrzędnej z powodu hello sposób usługi Azure AD obsługiwane domen, a będzie dziedziczyć ustawień hello hello nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="c5661-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="c5661-185">Oznacza to, że hello IssuerUri musi toomatch hello nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="c5661-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="c5661-186">Dlatego umożliwia Powiedz, na przykład, że I bmcontoso.com i następnie dodać corp.bmcontoso.com.  Oznacza to, że ten hello IssuerUri do użytkownika z corp.bmcontoso.com należy toobe **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="c5661-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="c5661-187">Jednak zaimplementowana reguła standardowe hello powyżej dla usługi Azure AD, spowoduje wygenerowanie tokenu z wystawcą jako **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="c5661-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="c5661-188">nie będzie odpowiadała wymaganej wartości hello domeny i uwierzytelnianie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c5661-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="c5661-189">Jak tooenable obsługę poddomen</span><span class="sxs-lookup"><span data-stu-id="c5661-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="c5661-190">W kolejności toowork wokół tego hello usług AD FS dla witryny Microsoft Online zaufanie jednostki uzależnionej musi toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c5661-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="c5661-191">toodo, niestandardowej reguły oświadczeń należy skonfigurować tak, aby taśmy Wyłącz wszelkie poddomen z sufiksem nazwy UPN użytkownika hello podczas konstruowania hello niestandardowej wartości wystawcy.</span><span class="sxs-lookup"><span data-stu-id="c5661-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="c5661-192">Witaj następujące oświadczenie będzie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c5661-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="c5661-193">numer ostatniej Hello w wyrażeniu regularnym hello ustawić hello ile domeny nadrzędnej istnieje w domenie katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="c5661-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="c5661-194">W tym miejscu można mieć bmcontoso.com, niezbędne są dwie domeny nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="c5661-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="c5661-195">Jeśli trzy nadrzędnego domeny zostały zachowane toobe (tj.: corp.bmcontoso.com), następnie numer hello byłby trzy.</span><span class="sxs-lookup"><span data-stu-id="c5661-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="c5661-196">Mogą być wskazywane Eventualy zakresu, zawsze będą dopasowania hello toomatch hello maksymalna liczba domen.</span><span class="sxs-lookup"><span data-stu-id="c5661-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="c5661-197">"{2,3}" będzie odpowiadała dwie domeny toothree (np.: bmfabrikam.com i corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="c5661-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="c5661-198">Użyj następujących hello kroki tooadd domenami podrzędnymi toosupport oświadczenia niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c5661-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="c5661-199">Zarządzanie usługami Otwórz AD FS</span><span class="sxs-lookup"><span data-stu-id="c5661-199">Open AD FS Management</span></span>
2. <span data-ttu-id="c5661-200">Zaufania Microsoft Online RP powitania kliknij prawym przyciskiem myszy i wybierz polecenie reguły Edycja oświadczeń</span><span class="sxs-lookup"><span data-stu-id="c5661-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="c5661-201">Wybierz hello trzeci reguły oświadczeń i Zastąp ![Edycja oświadczeń](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="c5661-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="c5661-202">Zastąp bieżący oświadczeń hello:</span><span class="sxs-lookup"><span data-stu-id="c5661-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Zastąp oświadczeń](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="c5661-204">Kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="c5661-204">Click Ok.</span></span>  <span data-ttu-id="c5661-205">Kliknij przycisk Zastosuj.</span><span class="sxs-lookup"><span data-stu-id="c5661-205">Click Apply.</span></span>  <span data-ttu-id="c5661-206">Kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="c5661-206">Click Ok.</span></span>  <span data-ttu-id="c5661-207">Zamknij przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="c5661-207">Close AD FS Management.</span></span>

