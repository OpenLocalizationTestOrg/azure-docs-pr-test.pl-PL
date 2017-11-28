---
title: "Usługa Azure Active Directory B2C: Dodawanie usług AD FS jako dostawca tożsamości SAML za pomocą zasad niestandardowych"
description: "Tooarticle instrukcje dotyczące konfigurowania usług AD FS 2016 przy użyciu protokołu SAML i zasad niestandardowych"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="0a427-103">Usługa Azure Active Directory B2C: Dodawanie usług AD FS jako dostawca tożsamości SAML za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="0a427-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="0a427-104">W tym artykule opisano sposób tooenable logowania użytkowników z konta usług AD FS przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0a427-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a427-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a427-105">Prerequisites</span></span>

<span data-ttu-id="0a427-106">Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0a427-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="0a427-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="0a427-107">These steps include:</span></span>

1.  <span data-ttu-id="0a427-108">Tworzenie usług AD FS jednostki uzależnionej zaufania.</span><span class="sxs-lookup"><span data-stu-id="0a427-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="0a427-109">Dodawanie tooAzure certyfikatu usług AD FS zaufania jednostki uzależnionej hello AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0a427-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="0a427-110">Dodawanie zasad tooa dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0a427-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="0a427-111">Konta usług AD FS w usłudze rejestrowania hello oświadczeń przebieg użytkownika tooa dostawcy.</span><span class="sxs-lookup"><span data-stu-id="0a427-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="0a427-112">Przekazywanie hello tooan zasad usługi Azure AD B2C dzierżawy i przetestować go.</span><span class="sxs-lookup"><span data-stu-id="0a427-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="0a427-113">toocreate oświadczeń zaufania jednostki uzależnionej</span><span class="sxs-lookup"><span data-stu-id="0a427-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="0a427-114">toouse usług AD FS jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate usług AD FS zaufania jednostki uzależnionej i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="0a427-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="0a427-115">tooadd nowe uzależnionej zaufania przy użyciu przystawki Zarządzanie FS hello AD i ręcznie skonfigurować ustawienia hello wykonać hello następujące procedury na serwerze federacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0a427-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="0a427-116">Członkostwo w grupie **Administratorzy**, lub równoważnej na komputerze lokalnym hello hello minimalne wymagane toocomplete tej procedury.</span><span class="sxs-lookup"><span data-stu-id="0a427-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="0a427-117">Szczegółowe informacje o używaniu hello odpowiednich kont i członkostwa w grupach [grupy domyślne w domenie i lokalne](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="0a427-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="0a427-118">W Menedżerze serwera kliknij **narzędzia**, a następnie wybierz **zarządzania usług AD FS**.</span><span class="sxs-lookup"><span data-stu-id="0a427-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="0a427-119">Polecenie **Dodawanie zaufania jednostki uzależnionej**.</span><span class="sxs-lookup"><span data-stu-id="0a427-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="0a427-120">![Dodawanie zaufania jednostki uzależnionej](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="0a427-121">Na powitania **powitalnej** wybierz pozycję **oświadczeń pamiętać** i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="0a427-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="0a427-122">![Na stronie powitalnej hello wybierz oświadczeń pamiętać](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="0a427-123">Na powitania **wybierz źródło danych** kliknij przycisk **ręcznie wprowadź dane dotyczące jednostki uzależnionej hello**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0a427-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="0a427-124">![Wprowadź dane dotyczące jednostki uzależnionej hello](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="0a427-125">Na powitania **Określanie nazwy wyświetlanej** wpisz nazwę w **Nazwa wyświetlana**w obszarze **uwagi** wpisz opis tego zaufania jednostki uzależnionej, a następnie kliknij przycisk **dalej** .</span><span class="sxs-lookup"><span data-stu-id="0a427-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="0a427-126">![Określ nazwę wyświetlaną i uwagi](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="0a427-127">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0a427-127">Optional.</span></span> <span data-ttu-id="0a427-128">Jeśli masz certyfikat szyfrowania tokenu opcjonalne następnie na powitania **Konfigurowanie certyfikatu** kliknij przycisk **Przeglądaj** toolocate plik certyfikatu, a następnie kliknij przycisk **dalej** .</span><span class="sxs-lookup"><span data-stu-id="0a427-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="0a427-129">![Konfigurowanie certyfikatu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="0a427-130">Na powitania **Konfigurowanie adresu URL** strona, wybierz hello **Włącz obsługę protokołu SAML 2.0 WebSSO hello** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="0a427-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="0a427-131">W obszarze **URL usługi logowania jednokrotnego SAML 2.0 jednostki uzależnionej w strona**wpisz adres URL punktu końcowego usługi Security (Assertion Markup Language SAML) powitania dla tego zaufania jednostki uzależnionej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0a427-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="0a427-132">Dla hello **URL usługi logowania jednokrotnego SAML 2.0 jednostki uzależnionej w strona**, Wklej hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="0a427-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="0a427-133">Zamień na nazwę swojej dzierżawy (na przykład contosob2c.onmicrosoft.com) {dzierżawa} i {zasad} hello Zamień na nazwę zasady rozszerzenia (na przykład B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="0a427-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="0a427-134">Nazwa zasady Hello jest hello jedną dziedziczący signup_or_signin zasady, w tym przypadku jest: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="0a427-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="0a427-135">Na przykład można hello adresu URL: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="0a427-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Jednostki uzależnionej adres URL strony logowania jednokrotnego SAML 2.0 usługi](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="0a427-137">Na powitania **skonfiguruj identyfikatory** Określ hello tego samego adresu URL jako hello poprzedniego kroku, kliknij przycisk **Dodaj** tooadd ich toohello listy, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0a427-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="0a427-138">![Jednostki uzależnionej identyfikatorów zaufania](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="0a427-139">Na powitania **wybierz zasady kontroli dostępu** wybierz zasady, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0a427-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="0a427-140">![Wybierz zasady kontroli dostępu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="0a427-141">Na powitania **gotowe tooAdd zaufania** , przejrzyj ustawienia hello, a następnie kliknij przycisk **dalej** toosave informacje o zaufaniu jednostki uzależnionej strony.</span><span class="sxs-lookup"><span data-stu-id="0a427-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="0a427-142">![Zapisz dane zaufania jednostki uzależnionej strony](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="0a427-143">Na powitania **Zakończ** kliknij przycisk **Zamknij**, ta czynność spowoduje automatyczne wyświetlenie hello **Edycja reguł oświadczeń** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0a427-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="0a427-144">![Edycja reguł oświadczeń](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="0a427-145">Kliknij przycisk **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="0a427-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="0a427-146">![Dodaj nową regułę](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="0a427-147">W **szablonu reguły oświadczeń**, wybierz pozycję **Wyślij atrybuty LDAP jako oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="0a427-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="0a427-148">![Wybierz Wyślij atrybuty LDAP jako oświadczeń szablonu reguł](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="0a427-149">Podaj **nazwy reguły oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="0a427-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="0a427-150">Dla hello **magazynu atrybutów** wybierz **usługi Active Directory wybierz** Dodaj powitania po oświadczeń, a następnie kliknij przycisk **Zakończ** i **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a427-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="0a427-151">![Właściwości zestawu reguł](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="0a427-152">W Menedżerze serwera wybierz **zaufania jednostek uzależnionych** wybierz hello zaufania jednostki uzależnionej został utworzony i kliknij **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0a427-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="0a427-153">![Jednostki uzależnionej strony Edytuj właściwości](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="0a427-154">Witaj jednej jednostki uzależnionej strony zaufania (pokaz B2C) właściwości kliknij **podpisu** i kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a427-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="0a427-155">![Podpis zestawu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="0a427-156">Dodaj certyfikat podpisu (bez klucza prywatnego plik .cert).</span><span class="sxs-lookup"><span data-stu-id="0a427-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Dodaj certyfikat podpisu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="0a427-158">W oknie Właściwości zaufania (pokaz B2C) jednostki uzależnionej strony powitania kliknij **zaawansowane** karcie i zmień hello **skrótu Secure hash algorithm** za**SHA-1**, kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="0a427-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="0a427-159">![Wartość skrótu secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="0a427-160">Dodaj hello usług AD FS konta aplikacji klucza tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0a427-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="0a427-161">Federacja z kontami usług AD FS wymaga klucza tajnego klienta usług AD FS tootrust konta usługi Azure AD B2C w imieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0a427-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="0a427-162">Należy toostore certyfikatu usług AD FS w dzierżawie usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0a427-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="0a427-163">Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**</span><span class="sxs-lookup"><span data-stu-id="0a427-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="0a427-164">Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="0a427-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="0a427-165">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a427-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="0a427-166">Aby uzyskać **opcje**, użyj **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="0a427-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="0a427-167">Aby uzyskać **nazwa**, użyj `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="0a427-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="0a427-168">Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0a427-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="0a427-169">W hello przekazywania pliku ** wybierz plik .pfx certyfikatu z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="0a427-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="0a427-170">Uwaga: ten certyfikat (z kluczem prywatnym hello) powinna być hello, tej samej, który wystawił i używane dla usług AD FS hello jednostki uzależnionej.</span><span class="sxs-lookup"><span data-stu-id="0a427-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="0a427-171">![Przekazywanie klucza zasad](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="0a427-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="0a427-172">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="0a427-172">Click **Create**</span></span>
8.  <span data-ttu-id="0a427-173">Upewnij się, że utworzono klucz hello `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="0a427-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="0a427-174">Dodawanie dostawcy oświadczeń w zasadach rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="0a427-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="0a427-175">Jeśli chcesz toosign użytkowników przy użyciu konta usług AD FS, musisz mieć konto usług AD FS toodefine jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0a427-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="0a427-176">Innymi słowy należy toospecify punktu końcowego, który komunikuje się usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0a427-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="0a427-177">punkt końcowy Hello zawiera zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a427-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="0a427-178">Zdefiniuj usług AD FS jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="0a427-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="0a427-179">Otwórz plik zasad rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="0a427-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="0a427-180">Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.</span><span class="sxs-lookup"><span data-stu-id="0a427-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="0a427-181">Znajdź hello `<ClaimsProviders>` sekcji</span><span class="sxs-lookup"><span data-stu-id="0a427-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="0a427-182">Dodaj następujące fragment kodu XML w obszarze hello hello `ClaimsProviders` elementu i zastępowanie `identityProvider` o systemie DNS (dowolną wartość, która wskazuje domenę) i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="0a427-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="0a427-183">Zarejestruj hello usług AD FS konta oświadczeń dostawcy tooSign się lub zaloguj się w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="0a427-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="0a427-184">W tym momencie hello dostawcy tożsamości nie został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="0a427-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="0a427-185">Jednak nie jest dostępna w żadnym hello konta-konta/logowania ekranów.</span><span class="sxs-lookup"><span data-stu-id="0a427-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="0a427-186">Teraz należy użytkownik tooyour dostawcy tożsamości konta tooadd hello usług AD FS `SignUpOrSignIn` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a427-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="0a427-187">toomake ją, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="0a427-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="0a427-188">Następnie możemy zmodyfikować go, uwzględniając dostawcy tożsamości usługi AD FS hello:</span><span class="sxs-lookup"><span data-stu-id="0a427-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="0a427-189">Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="0a427-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="0a427-190">Znajdź hello `<UserJourneys>` element kopiowania hello całej zawartości i `<UserJourneys>` węzła.</span><span class="sxs-lookup"><span data-stu-id="0a427-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="0a427-191">Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="0a427-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="0a427-192">Jeśli hello element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="0a427-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="0a427-193">Wklej zawartość całego hello `<UserJournesy>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="0a427-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="0a427-194">Przycisk hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="0a427-194">Display hello button</span></span>
<span data-ttu-id="0a427-195">Witaj `<ClaimsProviderSelections>` element definiuje listę hello opcje wyboru dostawcy oświadczeń i ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="0a427-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="0a427-196">`<ClaimsProviderSelection>`element jest przycisku dostawcy tożsamości analogiczne tooan na stronie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="0a427-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="0a427-197">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta usług AD FS, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0a427-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="0a427-198">tooadd tego elementu:</span><span class="sxs-lookup"><span data-stu-id="0a427-198">tooadd this element:</span></span>

1.  <span data-ttu-id="0a427-199">Znajdź hello `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika hello, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="0a427-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="0a427-200">Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="0a427-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="0a427-201">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="0a427-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="0a427-202">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="0a427-202">Link hello button tooan action</span></span>

<span data-ttu-id="0a427-203">Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji.</span><span class="sxs-lookup"><span data-stu-id="0a427-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="0a427-204">Akcja Hello jest dla usługi Azure AD B2C toocommunicate z tooreceive konta usług AD FS w takim przypadku tokenu.</span><span class="sxs-lookup"><span data-stu-id="0a427-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="0a427-205">Łącze hello tooan Akcja przycisku przez łączenie hello techniczne profilu dla dostawcy oświadczeń konta usług AD FS:</span><span class="sxs-lookup"><span data-stu-id="0a427-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="0a427-206">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="0a427-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="0a427-207">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="0a427-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="0a427-208">Upewnij się, hello `Id` ma takie same wartości jak hello `TargetClaimsExchangeId` w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0a427-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="0a427-209">Upewnij się, `TechnicalProfileReferenceId` ustawiono profil techniczne toohello utworzony wcześniej (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="0a427-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="0a427-210">Przekaż hello zasad tooyour dzierżawy</span><span class="sxs-lookup"><span data-stu-id="0a427-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="0a427-211">W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.</span><span class="sxs-lookup"><span data-stu-id="0a427-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="0a427-212">Wybierz **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="0a427-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="0a427-213">Otwórz hello **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="0a427-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="0a427-214">Wybierz **przekazywać zasady**.</span><span class="sxs-lookup"><span data-stu-id="0a427-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="0a427-215">Sprawdź **zastąpić hello zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="0a427-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="0a427-216">**Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello</span><span class="sxs-lookup"><span data-stu-id="0a427-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="0a427-217">Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="0a427-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="0a427-218">Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="0a427-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="0a427-219">Otwórz **B2C_1A_signup_signin**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="0a427-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="0a427-220">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="0a427-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="0a427-221">Powinno być możliwe toosign za pomocą konta usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="0a427-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="0a427-222">[Opcjonalnie] Zarejestruj przebieg użytkownika edycji tooProfile dostawcy oświadczeń hello usług AD FS konta</span><span class="sxs-lookup"><span data-stu-id="0a427-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="0a427-223">Możesz dostawcy tożsamości konta usług AD FS hello tooadd również użytkownika tooyour `ProfileEdit` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a427-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="0a427-224">toomake ją, powtórz firma Microsoft hello ostatnie dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="0a427-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="0a427-225">Przycisk hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="0a427-225">Display hello button</span></span>
1.  <span data-ttu-id="0a427-226">Otwórz plik rozszerzenia hello zasad (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="0a427-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="0a427-227">Znajdź hello `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika hello, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="0a427-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="0a427-228">Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="0a427-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="0a427-229">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="0a427-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="0a427-230">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="0a427-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="0a427-231">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="0a427-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="0a427-232">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="0a427-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="0a427-233">Testowanie zasad niestandardowych edycji profilu hello przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="0a427-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="0a427-234">Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="0a427-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="0a427-235">Otwórz **B2C_1A_ProfileEdit**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="0a427-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="0a427-236">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="0a427-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="0a427-237">Powinno być możliwe toosign za pomocą konta usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="0a427-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="0a427-238">Pobierz pliki zasad pełną hello</span><span class="sxs-lookup"><span data-stu-id="0a427-238">Download hello complete policy files</span></span>
<span data-ttu-id="0a427-239">Opcjonalnie: Zaleca się kompilacji danego scenariusza przy użyciu własnych niestandardowych zasad plików po zakończeniu hello przeprowadzenie wprowadzenie zasady niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="0a427-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="0a427-240">Pliki przykładowe zasady jedynie do celów referencyjnych</span><span class="sxs-lookup"><span data-stu-id="0a427-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
