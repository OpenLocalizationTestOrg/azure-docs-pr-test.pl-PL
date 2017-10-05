---
title: "Usługa Azure Active Directory B2C: Dodawanie usług AD FS jako dostawca tożsamości SAML za pomocą zasad niestandardowych"
description: "Artykule na temat konfigurowania usług AD FS 2016 przy użyciu protokołu SAML i zasad niestandardowych"
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
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="7e5de-103">Usługa Azure Active Directory B2C: Dodawanie usług AD FS jako dostawca tożsamości SAML za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="7e5de-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7e5de-104">W tym artykule przedstawiono sposób włączenia logowania użytkowników z usług AD FS konta za pośrednictwem [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7e5de-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e5de-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e5de-105">Prerequisites</span></span>

<span data-ttu-id="7e5de-106">Wykonaj kroki [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="7e5de-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="7e5de-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="7e5de-107">These steps include:</span></span>

1.  <span data-ttu-id="7e5de-108">Tworzenie usług AD FS jednostki uzależnionej zaufania.</span><span class="sxs-lookup"><span data-stu-id="7e5de-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="7e5de-109">Trwa dodawanie certyfikatu usługi AD FS zaufania jednostki uzależnionej do usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7e5de-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="7e5de-110">Dodawanie dostawcy oświadczeń dla zasad.</span><span class="sxs-lookup"><span data-stu-id="7e5de-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="7e5de-111">Rejestrowanie usług AD FS konta oświadczeń dostawcy przebieg użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e5de-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="7e5de-112">Przekazywanie zasady do usługi Azure AD B2C dzierżawy i przetestować go.</span><span class="sxs-lookup"><span data-stu-id="7e5de-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="7e5de-113">Aby utworzyć oświadczeń zaufania jednostki uzależnionej</span><span class="sxs-lookup"><span data-stu-id="7e5de-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="7e5de-114">Aby używać usług AD FS jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy do tworzenia usług AD FS zaufania jednostki uzależnionej dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="7e5de-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="7e5de-115">Aby dodać nowe zaufanie jednostki uzależnionej przy użyciu przystawki Zarządzanie usługami AD FS i należy ręcznie skonfigurować ustawienia, należy wykonać następującą procedurę na serwerze federacyjnym.</span><span class="sxs-lookup"><span data-stu-id="7e5de-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="7e5de-116">Członkostwo w grupie **Administratorzy**, lub równoważnej na komputerze lokalnym jest minimalnym wymaganiem do wykonania tej procedury.</span><span class="sxs-lookup"><span data-stu-id="7e5de-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="7e5de-117">Szczegółowe informacje na temat używania odpowiednich kont i członkostwa w grupach [grupy domyślne w domenie i lokalne](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="7e5de-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="7e5de-118">W Menedżerze serwera kliknij **narzędzia**, a następnie wybierz **zarządzania usług AD FS**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="7e5de-119">Polecenie **Dodawanie zaufania jednostki uzależnionej**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="7e5de-120">![Dodawanie zaufania jednostki uzależnionej](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="7e5de-121">Na **powitalnej** wybierz pozycję **oświadczeń pamiętać** i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="7e5de-122">![Na stronie powitalnej wybierz pamiętać oświadczeń](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="7e5de-123">Na **wybierz źródło danych** kliknij przycisk **ręcznie wprowadź dane jednostki uzależnionej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="7e5de-124">![Wprowadź dane jednostki uzależnionej](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="7e5de-125">Na **Określanie nazwy wyświetlanej** wpisz nazwę w **Nazwa wyświetlana**w obszarze **uwagi** wpisz opis tego zaufania jednostki uzależnionej, a następnie kliknij przycisk **dalej** .</span><span class="sxs-lookup"><span data-stu-id="7e5de-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="7e5de-126">![Określ nazwę wyświetlaną i uwagi](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="7e5de-127">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="7e5de-127">Optional.</span></span> <span data-ttu-id="7e5de-128">Jeśli certyfikat szyfrowania tokenu opcjonalne następnie na **Konfigurowanie certyfikatu** kliknij przycisk **Przeglądaj** zlokalizuj plik certyfikatu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="7e5de-129">![Konfigurowanie certyfikatu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="7e5de-130">Na **Konfigurowanie adresu URL** wybierz pozycję **Włącz obsługę protokołu SAML 2.0 WebSSO** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="7e5de-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="7e5de-131">W obszarze **URL usługi logowania jednokrotnego SAML 2.0 jednostki uzależnionej w strona**, wpisz adres URL punktu końcowego usługi Security (Assertion Markup Language SAML) dla tego zaufania jednostki uzależnionej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="7e5de-132">Aby uzyskać **URL usługi logowania jednokrotnego SAML 2.0 jednostki uzależnionej w strona**, Wklej `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="7e5de-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="7e5de-133">Zamień na nazwę swojej dzierżawy (na przykład contosob2c.onmicrosoft.com) {dzierżawa} i {zasad} Zamień na nazwę zasady rozszerzenia (na przykład B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="7e5de-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="7e5de-134">Nazwa zasady jest dziedziczący signup_or_signin zasady, w tym przypadku jest: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="7e5de-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="7e5de-135">Na przykład adres URL może być: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Jednostki uzależnionej adres URL strony logowania jednokrotnego SAML 2.0 usługi](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="7e5de-137">Na **skonfiguruj identyfikatory** Określ ten sam adres URL co w poprzednim kroku, kliknij przycisk **Dodaj** dodać je do listy, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="7e5de-138">![Jednostki uzależnionej identyfikatorów zaufania](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="7e5de-139">Na **wybierz zasady kontroli dostępu** wybierz zasady, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="7e5de-140">![Wybierz zasady kontroli dostępu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="7e5de-141">Na **gotowe do dodania zaufania** , przejrzyj ustawienia, a następnie kliknij przycisk **dalej** zapisać uzależnionej informacje o zaufaniu.</span><span class="sxs-lookup"><span data-stu-id="7e5de-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="7e5de-142">![Zapisz dane zaufania jednostki uzależnionej strony](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="7e5de-143">Na **Zakończ** kliknij przycisk **Zamknij**, ta czynność spowoduje automatyczne wyświetlenie **Edycja reguł oświadczeń** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7e5de-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="7e5de-144">![Edycja reguł oświadczeń](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="7e5de-145">Kliknij przycisk **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="7e5de-146">![Dodaj nową regułę](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="7e5de-147">W **szablonu reguły oświadczeń**, wybierz pozycję **Wyślij atrybuty LDAP jako oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="7e5de-148">![Wybierz Wyślij atrybuty LDAP jako oświadczeń szablonu reguł](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="7e5de-149">Podaj **nazwy reguły oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="7e5de-150">Dla **magazynu atrybutów** wybierz **usługi Active Directory wybierz** Dodaj następujące oświadczeń, a następnie kliknij przycisk **Zakończ** i **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="7e5de-151">![Właściwości zestawu reguł](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="7e5de-152">W Menedżerze serwera wybierz **zaufania jednostek uzależnionych** , a następnie wybierz jednostkę uzależnioną zaufania utworzony i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="7e5de-153">![Jednostki uzależnionej strony Edytuj właściwości](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="7e5de-154">Okno Właściwości zaufania (pokaz B2C) jednostki uzależnionej strony kliknij jeden **podpisu** i kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="7e5de-155">![Podpis zestawu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="7e5de-156">Dodaj certyfikat podpisu (bez klucza prywatnego plik .cert).</span><span class="sxs-lookup"><span data-stu-id="7e5de-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Dodaj certyfikat podpisu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="7e5de-158">W oknie Właściwości zaufania (pokaz B2C) jednostki uzależnionej strony kliknij **zaawansowane** karcie i zmień **skrótu Secure hash algorithm** do **SHA-1**, kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="7e5de-159">![Wartość skrótu secure hash algorithm SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="7e5de-160">Dodaj klucz aplikacji konto usług AD FS do usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7e5de-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="7e5de-161">Federacja z kontami usług AD FS wymaga klucz tajny klienta konta usług AD FS do relacji zaufania usługi Azure AD B2C w imieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e5de-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="7e5de-162">Należy do przechowywania certyfikatu usług AD FS w dzierżawie usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7e5de-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="7e5de-163">Przejdź do dzierżawy usługi Azure AD B2C i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**</span><span class="sxs-lookup"><span data-stu-id="7e5de-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="7e5de-164">Wybierz **zasad kluczy** Aby wyświetlić dostępne w Twojej dzierżawie kluczy.</span><span class="sxs-lookup"><span data-stu-id="7e5de-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="7e5de-165">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="7e5de-166">Aby uzyskać **opcje**, użyj **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="7e5de-167">Aby uzyskać **nazwa**, użyj `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="7e5de-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="7e5de-168">Prefiks `B2C_1A_` mogą być dodawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7e5de-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="7e5de-169">W przypadku przekazywania pliku ** wybierz plik .pfx certyfikatu z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="7e5de-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="7e5de-170">Uwaga: ten certyfikat (z kluczem prywatnym) powinna być taka sama, wydane i używane dla jednostki uzależnionej usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="7e5de-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="7e5de-171">![Przekazywanie klucza zasad](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="7e5de-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="7e5de-172">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="7e5de-172">Click **Create**</span></span>
8.  <span data-ttu-id="7e5de-173">Upewnij się, że utworzono klucz `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="7e5de-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="7e5de-174">Dodawanie dostawcy oświadczeń w zasadach rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="7e5de-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="7e5de-175">Użytkownikom na logowanie się przy użyciu konta usług AD FS, należy zdefiniować konta usług AD FS jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7e5de-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="7e5de-176">Innymi słowy należy określić punkt końcowy, który komunikuje się usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7e5de-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="7e5de-177">Punkt końcowy zawiera zestaw oświadczeń, które są używane przez usługę Azure AD B2C, aby sprawdzić, czy określony użytkownik jest uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="7e5de-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="7e5de-178">Zdefiniuj usług AD FS jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="7e5de-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="7e5de-179">Otwórz plik zasad rozszerzenia (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="7e5de-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="7e5de-180">Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.</span><span class="sxs-lookup"><span data-stu-id="7e5de-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="7e5de-181">Znajdź `<ClaimsProviders>` sekcji</span><span class="sxs-lookup"><span data-stu-id="7e5de-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="7e5de-182">Dodaj następujący fragment kodu XML w obszarze `ClaimsProviders` elementu i zastępowanie `identityProvider` o systemie DNS (dowolną wartość, która wskazuje domenę) i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="7e5de-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

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

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="7e5de-183">Zarejestruj dostawcę oświadczeń konta usług AD FS do logowania się lub zaloguj się w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="7e5de-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="7e5de-184">W tym momencie dostawcy tożsamości nie został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="7e5de-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="7e5de-185">Jednak nie jest dostępna w żadnym ekrany konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="7e5de-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="7e5de-186">Teraz należy dodać dostawcy tożsamości konta usług AD FS do użytkownika `SignUpOrSignIn` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e5de-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="7e5de-187">Aby było to możliwe, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="7e5de-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="7e5de-188">Następnie możemy zmodyfikować go, uwzględniając dostawcy tożsamości usługi AD FS:</span><span class="sxs-lookup"><span data-stu-id="7e5de-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="7e5de-189">Otwórz plik bazowy tej zasady (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="7e5de-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="7e5de-190">Znajdź `<UserJourneys>` element i skopiuj cała zawartość `<UserJourneys>` węzła.</span><span class="sxs-lookup"><span data-stu-id="7e5de-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="7e5de-191">Otwórz plik rozszerzenia (na przykład TrustFrameworkExtensions.xml) i Znajdź `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="7e5de-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="7e5de-192">Jeśli element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="7e5de-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="7e5de-193">Wklej całą zawartość `<UserJournesy>` węzła, który został skopiowany jako element podrzędny `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="7e5de-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="7e5de-194">Wyświetlany przycisk</span><span class="sxs-lookup"><span data-stu-id="7e5de-194">Display the button</span></span>
<span data-ttu-id="7e5de-195">`<ClaimsProviderSelections>` Element definiuje listę opcje wyboru dostawcy oświadczeń i ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="7e5de-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="7e5de-196">`<ClaimsProviderSelection>`element jest odpowiednikiem przycisku dostawcy tożsamości na stronie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="7e5de-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="7e5de-197">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta usług AD FS, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie.</span><span class="sxs-lookup"><span data-stu-id="7e5de-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="7e5de-198">Aby dodać ten element:</span><span class="sxs-lookup"><span data-stu-id="7e5de-198">To add this element:</span></span>

1.  <span data-ttu-id="7e5de-199">Znajdź `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="7e5de-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="7e5de-200">Zlokalizuj `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="7e5de-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="7e5de-201">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="7e5de-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="7e5de-202">Połącz przycisku akcji</span><span class="sxs-lookup"><span data-stu-id="7e5de-202">Link the button to an action</span></span>

<span data-ttu-id="7e5de-203">Teraz, gdy masz przycisku w miejscu, należy połączyć je z akcją.</span><span class="sxs-lookup"><span data-stu-id="7e5de-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="7e5de-204">Akcja, w tym przypadku jest dla usługi Azure AD B2C do komunikowania się z konta usług AD FS otrzymujących token.</span><span class="sxs-lookup"><span data-stu-id="7e5de-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="7e5de-205">Połączyć przycisku akcji przez łączenie techniczne profilu dla dostawcy oświadczeń konta usług AD FS:</span><span class="sxs-lookup"><span data-stu-id="7e5de-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="7e5de-206">Znajdź `<OrchestrationStep>` zawierającą `Order="2"` w `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="7e5de-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="7e5de-207">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="7e5de-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="7e5de-208">Upewnij się, `Id` ma taką samą wartość jak `TargetClaimsExchangeId` w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7e5de-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="7e5de-209">Upewnij się, `TechnicalProfileReferenceId` ustawiono techniczne profilu utworzonego wcześniej (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="7e5de-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="7e5de-210">Przekaż zasady dla Twojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="7e5de-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="7e5de-211">W [portalu Azure](https://portal.azure.com), przejdź do [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), a następnie otwórz **usługi Azure AD B2C** bloku.</span><span class="sxs-lookup"><span data-stu-id="7e5de-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="7e5de-212">Wybierz **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="7e5de-213">Otwórz **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="7e5de-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="7e5de-214">Wybierz **przekazywać zasady**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="7e5de-215">Sprawdź **zastąpić zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="7e5de-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="7e5de-216">**Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji</span><span class="sxs-lookup"><span data-stu-id="7e5de-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="7e5de-217">Testowanie zasad niestandardowych przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="7e5de-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="7e5de-218">Otwórz **ustawienia usługi Azure AD B2C** i przejdź do **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="7e5de-219">Otwórz **B2C_1A_signup_signin**, jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="7e5de-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="7e5de-220">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="7e5de-221">Można będzie zalogować się przy użyciu konta usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="7e5de-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="7e5de-222">[Opcjonalnie] Zarejestruj dostawcę oświadczeń konta usług AD FS do edycji profilu użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="7e5de-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="7e5de-223">Można również dodać dostawcy tożsamości konta usług AD FS do użytkownika `ProfileEdit` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e5de-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="7e5de-224">Aby było to możliwe, możemy Powtórz ostatnie dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="7e5de-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="7e5de-225">Wyświetlany przycisk</span><span class="sxs-lookup"><span data-stu-id="7e5de-225">Display the button</span></span>
1.  <span data-ttu-id="7e5de-226">Otwórz plik rozszerzenia zasad (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7e5de-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="7e5de-227">Znajdź `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="7e5de-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="7e5de-228">Zlokalizuj `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="7e5de-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="7e5de-229">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="7e5de-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="7e5de-230">Połącz przycisku akcji</span><span class="sxs-lookup"><span data-stu-id="7e5de-230">Link the button to an action</span></span>
1.  <span data-ttu-id="7e5de-231">Znajdź `<OrchestrationStep>` zawierającą `Order="2"` w `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="7e5de-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="7e5de-232">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="7e5de-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="7e5de-233">Testowanie zasad niestandardowych edycji profilu przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="7e5de-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="7e5de-234">Otwórz **ustawienia usługi Azure AD B2C** i przejdź do **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="7e5de-235">Otwórz **B2C_1A_ProfileEdit**, jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="7e5de-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="7e5de-236">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="7e5de-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="7e5de-237">Można będzie zalogować się przy użyciu konta usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="7e5de-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="7e5de-238">Pobierz pliki pełną zasad</span><span class="sxs-lookup"><span data-stu-id="7e5de-238">Download the complete policy files</span></span>
<span data-ttu-id="7e5de-239">Opcjonalnie: Zaleca się tworzenie scenariusz przy użyciu własnych zasad niestandardowych, które przeprowadzenie pliki po zakończeniu wprowadzenie do zasad niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="7e5de-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="7e5de-240">Pliki przykładowe zasady jedynie do celów referencyjnych</span><span class="sxs-lookup"><span data-stu-id="7e5de-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
