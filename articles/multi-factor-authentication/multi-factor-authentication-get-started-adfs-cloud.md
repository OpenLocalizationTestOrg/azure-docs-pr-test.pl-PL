---
title: "Zabezpieczanie zasobów w chmurze za pomocą usługi Azure MFA i usług AD FS | Microsoft Docs"
description: "Ta strona dotyczy usługi Azure Multi-Factor Authentication i zawiera informacje umożliwiające rozpoczęcie korzystania z usługi Azure MFA i usług AD FS w chmurze."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="df9a6-103">Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS</span><span class="sxs-lookup"><span data-stu-id="df9a6-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="df9a6-104">Jeśli Twoja organizacja jest sfederowana z użyciem usługi Azure Active Directory, możesz użyć usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services (AD FS) do zabezpieczenia zasobów używanych przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df9a6-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="df9a6-105">Aby zabezpieczyć zasoby usługi Azure Active Directory za pomocą usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services, postępuj zgodnie z poniższymi procedurami.</span><span class="sxs-lookup"><span data-stu-id="df9a6-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="df9a6-106">Zabezpieczanie zasobów usługi Azure AD za pomocą usług AD FS</span><span class="sxs-lookup"><span data-stu-id="df9a6-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="df9a6-107">Aby zabezpieczyć zasób w chmurze, skonfiguruj regułę oświadczeń, tak aby usługi Active Directory Federation Services emitowały oświadczenie multipleauthn, gdy użytkownik pomyślnie przeprowadzi weryfikację dwuetapową.</span><span class="sxs-lookup"><span data-stu-id="df9a6-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="df9a6-108">To oświadczenie jest przekazywane do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df9a6-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="df9a6-109">Wykonaj tę procedurę w celu przejścia przez poszczególne kroki:</span><span class="sxs-lookup"><span data-stu-id="df9a6-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="df9a6-110">Otwórz przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="df9a6-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="df9a6-111">Po lewej stronie wybierz pozycję **Relacje zaufania jednostek zależnych**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="df9a6-112">Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="df9a6-114">Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="df9a6-116">W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Przekazywanie lub filtrowanie oświadczenia przychodzącego**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="df9a6-118">Nadaj regule nazwę.</span><span class="sxs-lookup"><span data-stu-id="df9a6-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="df9a6-119">Wybierz wartość **Odwołania metod uwierzytelniania** jako typ oświadczenia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="df9a6-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="df9a6-120">Wybierz pozycję **Przekazuj wszystkie wartości oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="df9a6-121">![Kreator dodawania reguły przekształcania dotyczącej oświadczeń](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="df9a6-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="df9a6-122">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-122">Click **Finish**.</span></span> <span data-ttu-id="df9a6-123">Zamknij konsolę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="df9a6-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="df9a6-124">Zaufane adresy IP dla użytkowników federacyjnych</span><span class="sxs-lookup"><span data-stu-id="df9a6-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="df9a6-125">Zaufane adresy IP umożliwiają administratorom pomijanie weryfikacji dwuetapowej w przypadku określonych adresów IP lub użytkowników federacyjnych, którzy wysyłają żądania z firmowej sieci intranet.</span><span class="sxs-lookup"><span data-stu-id="df9a6-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="df9a6-126">Poniższe sekcje zawierają instrukcje dotyczące konfigurowania zaufanych adresów IP usługi Azure Multi-Factor Authentication dla użytkowników federacyjnych i pomijania weryfikacji dwuetapowej w przypadku żądań pochodzących od użytkowników federacyjnych z sieci intranet.</span><span class="sxs-lookup"><span data-stu-id="df9a6-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="df9a6-127">Osiąga się to przez skonfigurowanie usług AD FS pod kątem używania szablonu przekazywania lub szablonu filtrowania oświadczeń przychodzących za pomocą typu oświadczeń wewnętrznej sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="df9a6-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="df9a6-128">W tym przykładzie użyto usługi Office 365 w celu pokazania obsługi relacji zaufania jednostek zależnych.</span><span class="sxs-lookup"><span data-stu-id="df9a6-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="df9a6-129">Konfigurowanie reguł oświadczeń usług AD FS</span><span class="sxs-lookup"><span data-stu-id="df9a6-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="df9a6-130">W pierwszej kolejności należy skonfigurować oświadczenia usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="df9a6-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="df9a6-131">Utwórz dwie reguły oświadczeń — jedną dla typu oświadczenia wewnętrznej sieci firmowej, a drugą na potrzeby umożliwienia stałego zalogowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="df9a6-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="df9a6-132">Otwórz przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="df9a6-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="df9a6-133">Po lewej stronie wybierz pozycję **Relacje zaufania jednostek zależnych**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="df9a6-134">Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń...**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="df9a6-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="df9a6-135">Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę.**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="df9a6-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="df9a6-136">W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Przekazywanie lub filtrowanie oświadczenia przychodzącego**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="df9a6-137">![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="df9a6-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="df9a6-138">W polu Nazwa reguły oświadczenia wpisz nazwę reguły,</span><span class="sxs-lookup"><span data-stu-id="df9a6-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="df9a6-139">np. WewnSiećFirm.</span><span class="sxs-lookup"><span data-stu-id="df9a6-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="df9a6-140">Dla pola Typ oświadczenia przychodzącego wybierz z listy rozwijanej pozycję **Wewnątrz sieci firmowej**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="df9a6-141">![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="df9a6-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="df9a6-142">Kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="df9a6-142">Click **Finish**.</span></span>
9. <span data-ttu-id="df9a6-143">Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="df9a6-144">W Kreatorze dodawania reguły przekształcania oświadczeń wybierz z listy rozwijanej pozycję **Wysyłanie oświadczeń przy użyciu reguły niestandardowej**, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="df9a6-145">W polu Nazwa reguły oświadczenia wprowadź tekst *Nie wylogowuj użytkowników*.</span><span class="sxs-lookup"><span data-stu-id="df9a6-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="df9a6-146">W polu Reguła niestandardowa wprowadź kod:</span><span class="sxs-lookup"><span data-stu-id="df9a6-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="df9a6-148">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-148">Click **Finish**.</span></span>
14. <span data-ttu-id="df9a6-149">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-149">Click **Apply**.</span></span>
15. <span data-ttu-id="df9a6-150">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-150">Click **Ok**.</span></span>
16. <span data-ttu-id="df9a6-151">Zamknij przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="df9a6-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="df9a6-152">Konfigurowanie zaufanych adresów IP usługi Azure Multi-Factor Authentication dla użytkowników federacyjnych</span><span class="sxs-lookup"><span data-stu-id="df9a6-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="df9a6-153">Po skonfigurowaniu oświadczeń można przystąpić do konfigurowania zaufanych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="df9a6-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="df9a6-154">Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="df9a6-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="df9a6-155">W obszarze po lewej stronie kliknij pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="df9a6-156">W sekcji Katalog wybierz katalog, w którym chcesz skonfigurować zaufane adresy IP.</span><span class="sxs-lookup"><span data-stu-id="df9a6-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="df9a6-157">W wybranym katalogu kliknij pozycję **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="df9a6-158">W sekcji uwierzytelniania wieloskładnikowego kliknij pozycję **Zarządzaj ustawieniami usługi**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="df9a6-159">Na stronie Ustawienia usługi w obszarze zaufanych adresów IP wybierz pozycję **Pomiń uwierzytelnianie wieloskładnikowe w przypadku żądań od użytkowników federacyjnych w moim intranecie**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="df9a6-161">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-161">Click **save**.</span></span>
8. <span data-ttu-id="df9a6-162">Po zastosowaniu aktualizacji kliknij pozycję **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="df9a6-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="df9a6-163">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="df9a6-163">That’s it!</span></span> <span data-ttu-id="df9a6-164">Od tej pory federacyjni użytkownicy usługi Office 365 muszą używać usługi MFA, tylko jeśli ich oświadczenia pochodzą spoza firmowego intranetu.</span><span class="sxs-lookup"><span data-stu-id="df9a6-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
