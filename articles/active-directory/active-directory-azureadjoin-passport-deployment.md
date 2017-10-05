---
title: "Włącz program Microsoft Windows Hello dla firm w Twojej organizacji | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące wdrażania do włączenia Microsoft Passport w Twojej organizacji."
services: active-directory
documentationcenter: 
keywords: "Skonfiguruj Microsoft Passport, Microsoft Windows Hello dla firm wdrożenia"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="36190-104">Włącz program Microsoft Windows Hello dla firm w Twojej organizacji</span><span class="sxs-lookup"><span data-stu-id="36190-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="36190-105">Po [łączenie urządzeń przyłączonych do domeny systemu Windows 10 w usłudze Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), wykonaj następujące czynności, aby włączyć program Microsoft Windows Hello dla firm w Twojej organizacji:</span><span class="sxs-lookup"><span data-stu-id="36190-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="36190-106">Wdrażanie programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="36190-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="36190-107">Skonfiguruj ustawienia zasad</span><span class="sxs-lookup"><span data-stu-id="36190-107">Configure policy settings</span></span>
3. <span data-ttu-id="36190-108">Konfigurowanie profilu certyfikatu</span><span class="sxs-lookup"><span data-stu-id="36190-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="36190-109">Wdrażanie programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="36190-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="36190-110">Aby wdrożyć certyfikaty użytkowników oparte na Windows Hello dla firm kluczy, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="36190-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="36190-111">**System Center Configuration Manager Current Branch** — należy zainstalować wersję 1606 lub większą.</span><span class="sxs-lookup"><span data-stu-id="36190-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="36190-112">Aby uzyskać więcej informacji, zobacz [dokumentacji programu System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) i [blogu zespołu programu System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="36190-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="36190-113">**Infrastruktury kluczy publicznych (PKI)** — Aby włączyć program Microsoft Windows Hello dla firm przy użyciu certyfikatów użytkowników wymaga infrastruktury kluczy publicznych w miejscu.</span><span class="sxs-lookup"><span data-stu-id="36190-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="36190-114">Jeśli nie istnieje lub nie chcesz jej używać w przypadku certyfikatów użytkownika, można wdrożyć nowego kontrolera domeny systemu Windows Server 2016 kompilacji 10551 (lub lepszy) zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="36190-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="36190-115">Wykonaj kroki, aby [Instalowanie repliki kontrolera domeny w istniejącej domenie](https://technet.microsoft.com/library/jj574134.aspx) lub [zainstalować nowy las usługi Active Directory, tworząc nowe środowisko](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="36190-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="36190-116">(Obrazów ISO są dostępne do pobrania na [wymiana nośników Signiant](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="36190-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="36190-117">Skonfiguruj ustawienia zasad</span><span class="sxs-lookup"><span data-stu-id="36190-117">Configure policy settings</span></span>
<span data-ttu-id="36190-118">Aby skonfigurować program Microsoft Windows Hello dla firm ustawień zasad, masz dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="36190-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="36190-119">Zasady grupy w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="36190-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="36190-120">System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="36190-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="36190-121">W oknie Zasady grupy w usłudze Active Directory jest to zalecana metoda skonfigurować program Microsoft Windows Hello dla firm ustawień zasad.</span><span class="sxs-lookup"><span data-stu-id="36190-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="36190-122">Za pomocą programu System Center Configuration Manager jest preferowaną metodą, gdy również używać do wdrażania certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="36190-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="36190-123">Ten scenariusz.</span><span class="sxs-lookup"><span data-stu-id="36190-123">This scenario:</span></span>

* <span data-ttu-id="36190-124">Zapewnia zgodność z nowszej scenariusze wdrażania</span><span class="sxs-lookup"><span data-stu-id="36190-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="36190-125">Wymaga po stronie klienta systemu Windows 10 w wersji 1607 lub lepszej.</span><span class="sxs-lookup"><span data-stu-id="36190-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="36190-126">Konfigurowanie programu Microsoft Windows Hello dla firm za pomocą zasad grupy w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="36190-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="36190-127">**Kroki**:</span><span class="sxs-lookup"><span data-stu-id="36190-127">**Steps**:</span></span>

1. <span data-ttu-id="36190-128">Otwórz Menedżera serwera, a następnie przejdź do **narzędzia** > **Zarządzanie zasadami grupy**.</span><span class="sxs-lookup"><span data-stu-id="36190-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="36190-129">W przystawce Zarządzanie zasadami grupy przejdź do węzeł domeny, która odnosi się do domeny, w której chcesz włączyć usługi Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="36190-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="36190-130">Kliknij prawym przyciskiem myszy **obiektów zasad grupy**i wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="36190-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="36190-131">Nadaj nazwę, na przykład włączyć usługi Windows Hello dla firm z obiektu zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="36190-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="36190-132">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="36190-132">Click **OK**.</span></span>
4. <span data-ttu-id="36190-133">Kliknij prawym przyciskiem myszy nowy obiekt zasad grupy, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="36190-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="36190-134">Przejdź do **Konfiguracja komputera** > **zasady** > **Szablony administracyjne** > **systemu Windows Składniki** > **Windows Hello dla firm**.</span><span class="sxs-lookup"><span data-stu-id="36190-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="36190-135">Kliknij prawym przyciskiem myszy **włączenia usługi Windows Hello dla firm**, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="36190-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="36190-136">Wybierz **włączone** przycisk opcji, a następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="36190-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="36190-137">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="36190-137">Click **OK**.</span></span>
8. <span data-ttu-id="36190-138">Teraz możesz połączyć obiekt zasad grupy do wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="36190-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="36190-139">Aby włączyć te zasady dla wszystkich urządzeń z systemem Windows 10 przyłączonych do domeny w swojej organizacji, należy połączyć zasad grupy do domeny.</span><span class="sxs-lookup"><span data-stu-id="36190-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="36190-140">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36190-140">For example:</span></span>
   * <span data-ttu-id="36190-141">Określonej jednostki organizacyjnej (OU) usługi Active Directory, gdzie będą umieszczane komputery przyłączone do domeny systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="36190-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="36190-142">Grupy zabezpieczeń, która zawiera przyłączonych do domeny komputerów z systemem Windows 10, które będą automatycznie rejestrowane w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="36190-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="36190-143">Konfigurowanie usługi Windows Hello dla firm przy użyciu programu System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="36190-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="36190-144">**Kroki**:</span><span class="sxs-lookup"><span data-stu-id="36190-144">**Steps**:</span></span>

1. <span data-ttu-id="36190-145">Otwórz **System Center Configuration Manager**, a następnie przejdź do **zasoby i zgodność > Ustawienia zgodności > dostęp do zasobów firmy > Windows Hello dla firm profile**.</span><span class="sxs-lookup"><span data-stu-id="36190-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Konfigurowanie systemu Windows Hello dla firm](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="36190-147">Na pasku narzędzi u góry kliknij **tworzenia usługi Windows Hello dla firm profilu**.</span><span class="sxs-lookup"><span data-stu-id="36190-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Konfigurowanie systemu Windows Hello dla firm](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="36190-149">Na **ogólne** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="36190-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie systemu Windows Hello dla firm](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="36190-151">a.</span><span class="sxs-lookup"><span data-stu-id="36190-151">a.</span></span> <span data-ttu-id="36190-152">W **nazwa** tekstowym, wpisz nazwę profilu, na przykład **Mój profil WHfB**.</span><span class="sxs-lookup"><span data-stu-id="36190-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="36190-153">b.</span><span class="sxs-lookup"><span data-stu-id="36190-153">b.</span></span> <span data-ttu-id="36190-154">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="36190-154">Click **Next**.</span></span>
4. <span data-ttu-id="36190-155">Na **obsługiwane platformy** okno dialogowe, wybierz platformy, które będą udostępniane z tym usługi Windows Hello dla firm, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="36190-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Konfigurowanie systemu Windows Hello dla firm](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="36190-157">Na **ustawienia** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="36190-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie systemu Windows Hello dla firm](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="36190-159">a.</span><span class="sxs-lookup"><span data-stu-id="36190-159">a.</span></span> <span data-ttu-id="36190-160">Jako **konfigurowania usługi Windows Hello dla firm**, wybierz pozycję **włączone**.</span><span class="sxs-lookup"><span data-stu-id="36190-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="36190-161">b.</span><span class="sxs-lookup"><span data-stu-id="36190-161">b.</span></span> <span data-ttu-id="36190-162">Jako **używaj (Trusted Platform Module)**, wybierz pozycję **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="36190-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="36190-163">c.</span><span class="sxs-lookup"><span data-stu-id="36190-163">c.</span></span> <span data-ttu-id="36190-164">Jako **metodę uwierzytelniania**, wybierz pozycję **opartego na certyfikatach**.</span><span class="sxs-lookup"><span data-stu-id="36190-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="36190-165">d.</span><span class="sxs-lookup"><span data-stu-id="36190-165">d.</span></span> <span data-ttu-id="36190-166">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="36190-166">Click **Next**.</span></span>
6. <span data-ttu-id="36190-167">Na **Podsumowanie** okna dialogowego, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="36190-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="36190-168">Na **zakończenia** okna dialogowego, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="36190-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="36190-169">Na pasku narzędzi u góry kliknij **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="36190-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![Konfigurowanie systemu Windows Hello dla firm](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="36190-171">Konfigurowanie profilu certyfikatu</span><span class="sxs-lookup"><span data-stu-id="36190-171">Configure the certificate profile</span></span>
<span data-ttu-id="36190-172">Jeśli używasz uwierzytelniania opartego na certyfikatach dla uwierzytelniania lokalnego, należy skonfigurować i wdrożyć profil certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="36190-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="36190-173">To zadanie wymaga skonfigurowania serwera usługi NDES i roli lokacji punktu rejestracji certyfikatu w System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="36190-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="36190-174">Aby uzyskać więcej informacji, zobacz [wymagania wstępne dotyczące profilów certyfikatów w programie Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="36190-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="36190-175">Otwórz **System Center Configuration Manager**, a następnie przejdź do **zasoby i zgodność > Ustawienia zgodności > dostęp do zasobów firmy > Profile certyfikatów**.</span><span class="sxs-lookup"><span data-stu-id="36190-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="36190-176">Wybierz szablon, który zawiera karty inteligentnej logowania rozszerzonego użycia klucza (EKU).</span><span class="sxs-lookup"><span data-stu-id="36190-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="36190-177">Na **rejestracja SCEP** strony profilu certyfikatu, musisz wybrać **Zainstaluj w usłudze Passport for Work w przeciwnym razie Zgłoś błąd** jako **dostawcy magazynu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="36190-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36190-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36190-178">Next steps</span></span>
* [<span data-ttu-id="36190-179">System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="36190-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="36190-180">Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="36190-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="36190-181">Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="36190-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="36190-182">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="36190-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="36190-183">Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="36190-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="36190-184">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="36190-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

