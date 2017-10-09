---
title: "aaaSecure zasobów w chmurze z usługą Azure MFA i usług AD FS | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA i usług AD FS w chmurze hello."
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
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="d5526-103">Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS</span><span class="sxs-lookup"><span data-stu-id="d5526-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="d5526-104">Jeśli Twoja organizacja jest Sfederowane przy użyciu usługi Azure Active Directory, należy użyć usługi Azure Multi-Factor Authentication lub zasobów toosecure Active Directory Federation Services (AD FS), które są udostępniane przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5526-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="d5526-105">Hello Użyj następujących procedur toosecure usługi Azure Active Directory zasobów przy użyciu usługi Azure Multi-Factor Authentication lub usług federacyjnych Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5526-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="d5526-106">Zabezpieczanie zasobów usługi Azure AD za pomocą usług AD FS</span><span class="sxs-lookup"><span data-stu-id="d5526-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="d5526-107">toosecure zasób chmury, ustaw reguły oświadczeń Active Directory Federation Services emituje hello multipleauthn oświadczenia, gdy użytkownik wykona pomyślnie weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="d5526-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="d5526-108">Tego oświadczenia są przekazywane tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="d5526-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="d5526-109">Wykonaj tej procedury toowalk hello kroki:</span><span class="sxs-lookup"><span data-stu-id="d5526-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="d5526-110">Otwórz przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="d5526-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="d5526-111">Po lewej stronie powitania, wybierz **zaufania jednostek uzależnionych**.</span><span class="sxs-lookup"><span data-stu-id="d5526-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="d5526-112">Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="d5526-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="d5526-114">Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="d5526-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="d5526-116">Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **przekazuj lub Filtruj oświadczenie przychodzące** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5526-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="d5526-118">Nadaj regule nazwę.</span><span class="sxs-lookup"><span data-stu-id="d5526-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="d5526-119">Wybierz **odwołania do metod uwierzytelniania** hello przychodzące typ oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d5526-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="d5526-120">Wybierz pozycję **Przekazuj wszystkie wartości oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="d5526-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="d5526-121">![Kreator dodawania reguły przekształcania dotyczącej oświadczeń](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="d5526-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="d5526-122">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d5526-122">Click **Finish**.</span></span> <span data-ttu-id="d5526-123">Zamknij konsolę zarządzania FS hello AD.</span><span class="sxs-lookup"><span data-stu-id="d5526-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="d5526-124">Zaufane adresy IP dla użytkowników federacyjnych</span><span class="sxs-lookup"><span data-stu-id="d5526-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="d5526-125">Listę zaufanych adresów IP pozwala administratorom tooby przebiegu weryfikacji dwuetapowej dla określonych adresów IP lub dla użytkowników federacyjnych, mających żądań wysyłanych z we własnej sieci intranet.</span><span class="sxs-lookup"><span data-stu-id="d5526-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="d5526-126">Witaj poniższych sekcjach opisano sposób tooconfigure Azure Multi-Factor Authentication zaufanych adresów IP z użytkowników federacyjnych i obejście weryfikację dwuetapową, jeśli żądanie pochodzi z w intranecie użytkowników federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d5526-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="d5526-127">Jest to osiągane przez skonfigurowanie usług AD FS toouse przekazującego lub filtr szablonem oświadczenia przychodzące z hello typ oświadczenia wewnątrz sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="d5526-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="d5526-128">W tym przykładzie użyto usługi Office 365 w celu pokazania obsługi relacji zaufania jednostek zależnych.</span><span class="sxs-lookup"><span data-stu-id="d5526-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="d5526-129">Konfigurowanie reguł oświadczeń hello usług AD FS</span><span class="sxs-lookup"><span data-stu-id="d5526-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="d5526-130">najpierw Hello potrzebujemy toodo jest tooconfigure oświadczeń hello usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="d5526-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="d5526-131">Utworzenie dwóch reguł oświadczeń, jeden dla hello wewnątrz sieci firmowej oświadczeń, typ i dodatkowe jeden aktualizowania użytkowników zalogowany.</span><span class="sxs-lookup"><span data-stu-id="d5526-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="d5526-132">Otwórz przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="d5526-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="d5526-133">Po lewej stronie powitania, wybierz **zaufania jednostek uzależnionych**.</span><span class="sxs-lookup"><span data-stu-id="d5526-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="d5526-134">Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń...**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="d5526-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="d5526-135">Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę.**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="d5526-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="d5526-136">Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **przekazuj lub Filtruj oświadczenie przychodzące** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5526-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="d5526-137">![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="d5526-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="d5526-138">W hello pole dalej tooClaim Nazwa reguły Nadaj regule nazwę.</span><span class="sxs-lookup"><span data-stu-id="d5526-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="d5526-139">np. WewnSiećFirm.</span><span class="sxs-lookup"><span data-stu-id="d5526-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="d5526-140">Z listy rozwijanej hello, tooIncoming dalej typ oświadczenia, wybierz **wewnątrz sieci firmowej**.</span><span class="sxs-lookup"><span data-stu-id="d5526-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="d5526-141">![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="d5526-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="d5526-142">Kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="d5526-142">Click **Finish**.</span></span>
9. <span data-ttu-id="d5526-143">Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="d5526-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="d5526-144">Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5526-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="d5526-145">W obszarze Nazwa reguły oświadczeń hello: wprowadź *zachowania użytkowników podpisany w*.</span><span class="sxs-lookup"><span data-stu-id="d5526-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="d5526-146">W hello niestandardowe reguły wpisz:</span><span class="sxs-lookup"><span data-stu-id="d5526-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="d5526-148">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d5526-148">Click **Finish**.</span></span>
14. <span data-ttu-id="d5526-149">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="d5526-149">Click **Apply**.</span></span>
15. <span data-ttu-id="d5526-150">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5526-150">Click **Ok**.</span></span>
16. <span data-ttu-id="d5526-151">Zamknij przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="d5526-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="d5526-152">Konfigurowanie zaufanych adresów IP usługi Azure Multi-Factor Authentication dla użytkowników federacyjnych</span><span class="sxs-lookup"><span data-stu-id="d5526-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="d5526-153">Teraz, oświadczenia hello znajdują się w miejscu, można skonfigurować listę zaufanych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d5526-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="d5526-154">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d5526-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d5526-155">Powitania po lewej stronie, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5526-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="d5526-156">W katalogu wybierz katalog hello miejscu tooset zapasowej listę zaufanych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d5526-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="d5526-157">W katalogu wybrano hello, kliknij polecenie **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="d5526-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="d5526-158">W sekcji uwierzytelnianie wieloskładnikowe powitania kliknij **Zarządzaj ustawieniami usługi**.</span><span class="sxs-lookup"><span data-stu-id="d5526-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="d5526-159">Na stronie ustawień usługi hello w obszarze listę zaufanych adresów IP, wybierz **pominąć kilku-factor uwierzytelniania dla żądań od użytkowników federacyjnych w moim intranecie**.</span><span class="sxs-lookup"><span data-stu-id="d5526-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="d5526-161">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d5526-161">Click **save**.</span></span>
8. <span data-ttu-id="d5526-162">Po zastosowaniu aktualizacji powitania kliknij **zamknąć**.</span><span class="sxs-lookup"><span data-stu-id="d5526-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="d5526-163">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="d5526-163">That’s it!</span></span> <span data-ttu-id="d5526-164">W tym momencie użytkowników federacyjnych usługi Office 365 powinien mieć tylko toouse MFA gdy oświadczenie pochodzi z poza hello firmowego intranetu.</span><span class="sxs-lookup"><span data-stu-id="d5526-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
