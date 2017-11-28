---
title: "aaaHow tooconfigure automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci tooregister urządzeń przyłączonych do domeny systemu Windows automatycznie i w trybie dyskretnym usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="1da52-103">Wprowadzenie do rejestracja urządzeń w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1da52-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="1da52-104">Rejestracja urządzenia w usłudze Azure Active Directory jest hello foundation dla scenariuszy dostępu warunkowego opartego na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="1da52-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="1da52-105">Po zarejestrowaniu urządzenia, rejestracja urządzeń w usłudze Azure Active Directory zapewnia hello urządzenia przy użyciu tożsamości, który jest używany tooauthenticate powitania po zalogowaniu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="1da52-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="1da52-106">urządzenie Hello uwierzytelniony i atrybuty hello hello urządzenia, można następnie tooenforce używane zasady dostępu warunkowego dla aplikacji, które znajdują się w chmurze hello i lokalnych.</span><span class="sxs-lookup"><span data-stu-id="1da52-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="1da52-107">W połączeniu z rozwiązaniem management(MDM) urządzeń przenośnych, takich jak Microsoft Intune, dodatkowe informacje o urządzeniu hello są aktualizowane hello atrybuty urządzenia w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1da52-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="1da52-108">Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="1da52-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="1da52-109">Aby uzyskać więcej informacji dotyczących rejestrowania urządzeń w Microsoft Intune Zobacz rejestrowanie urządzeń do zarządzania w usłudze Intune.</span><span class="sxs-lookup"><span data-stu-id="1da52-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="1da52-110">Scenariusze obsługiwane przez rejestracji Azure Active Directory urządzenia rejestracji usługi Azure Active Directory urządzeń obejmuje obsługę systemu iOS, Android i Windows urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1da52-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="1da52-111">Witaj poszczególne scenariusze wykorzystujące usługę rejestracja urządzeń w usłudze Azure AD mogą mieć bardziej specyficzne wymagania i obsługę platform.</span><span class="sxs-lookup"><span data-stu-id="1da52-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="1da52-112">Te scenariusze są następujące:</span><span class="sxs-lookup"><span data-stu-id="1da52-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="1da52-113">**Dostęp warunkowy dla usługi Office 365 aplikacji w usłudze Microsoft Intune:** Administratorzy IT mogą aprowizować dostępu warunkowego urządzeń zasady toosecure zasobów firmowych, podczas gdy na powitania sam czas dzięki czemu pracownicy przetwarzający informacje na zgodnych urządzeniach tooaccess hello usługi.</span><span class="sxs-lookup"><span data-stu-id="1da52-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="1da52-114">Aby uzyskać więcej informacji, zobacz zasady dostępu warunkowego urządzeń dla usług Office 365.</span><span class="sxs-lookup"><span data-stu-id="1da52-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="1da52-115">**Tooapplications dostępu warunkowego, które są hostowane lokalnie:** zarejestrowane urządzenia można używać z zasadami dostępu dla aplikacji, które są skonfigurowane toouse usług AD FS w systemie Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1da52-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="1da52-116">Aby uzyskać więcej informacji na temat konfigurowania lokalnego dostępu warunkowego, zobacz [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md) (Konfigurowanie lokalnego dostępu warunkowego przy użyciu usługi rejestracji urządzeń w usłudze Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1da52-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="1da52-117">Konfigurowanie usługi Rejestracja urządzeń w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1da52-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="1da52-118">Rejestracja urządzenia toosetup, jest dostępnych kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="1da52-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="1da52-119">Kiedy rejestrować urządzenia przyłączone do tooAzure AD domeny.</span><span class="sxs-lookup"><span data-stu-id="1da52-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="1da52-120">Aby uzyskać więcej informacji na ten temat możesz dodatkowe informacje na temat ustawień usługi Azure AD Join i hello wymaganych dla użytkowników domeny toojoin usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1da52-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="1da52-121">Gdy użytkownicy dodawanie pracy lub szkoły kont tooWindows na osobistych urządzeniach lub tooa zasobów roboczych wymagają rejestracji łączenia urządzeń przenośnych można zarejestrować urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1da52-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="1da52-122">tooensure, musi włączyć rejestrowanie urządzeń w usłudze Azure AD w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1da52-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="1da52-123">Można zarejestrować urządzenia za pomocą automatycznej rejestracji urządzeń dla tradycyjnych komputerów przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="1da52-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="1da52-124">tooensure, należy najpierw pierwszej instalacji programu Azure AD Connect, przed rozpoczęciem pracy z automatycznej rejestracji urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1da52-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="1da52-125">Najnowsze instrukcje, zobacz [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1da52-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="1da52-126">Można również przejrzeć i włączyć lub wyłączyć zarejestrowanych urządzeń w usłudze Azure Active Directory przy użyciu hello portalu administratora.</span><span class="sxs-lookup"><span data-stu-id="1da52-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="1da52-127">Włączanie usługi rejestracji urządzeń usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="1da52-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="1da52-128">**Witaj tooenable usługi rejestracji urządzeń usługi Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="1da52-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="1da52-129">Zaloguj się toohello portalu Microsoft Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1da52-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="1da52-130">W okienku po lewej stronie powitania wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1da52-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="1da52-131">Na karcie katalogu hello wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="1da52-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="1da52-132">Kliknij pozycję **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="1da52-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="1da52-133">Przewiń zbyt**urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="1da52-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="1da52-134">Wybierz wszystkie, aby użytkownicy mogą ZAREJESTROWAĆ swoje urządzenia w usłudze AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="1da52-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="1da52-135">Wybierz maksymalną liczbę hello urządzeń ma tooauthorize dla każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1da52-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="1da52-136">Rejestrowanie Hello usłudze Microsoft Intune lub zarządzania urządzeniami przenośnymi dla usługi Office 365 wymaga rejestracji urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1da52-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="1da52-137">Jeśli skonfigurowano którąś z tych usług **wszystkie** jest zaznaczone i **Brak** jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="1da52-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="1da52-138">Upewnij się, że zostały prawidłowo skonfigurowane i ma hello odpowiednie licencjonowania.</span><span class="sxs-lookup"><span data-stu-id="1da52-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="1da52-139">Domyślnie uwierzytelnianie dwuskładnikowe nie jest włączone dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="1da52-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="1da52-140">Jednak uwierzytelnianie dwuskładnikowe jest zalecane podczas rejestrowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1da52-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="1da52-141">Przed wymaganiem uwierzytelniania dwuskładnikowego dla tej usługi, należy skonfigurować dostawcę uwierzytelniania dwuskładnikowego w usłudze Azure Active Directory i skonfigurować konta użytkowników usługi Multi-Factor Authentication, zobacz Dodawanie usługi Multi-Factor Authentication tooAzure usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="1da52-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="1da52-142">Jeśli korzystasz z usług AD FS w systemie Windows Server 2012 R2, należy skonfigurować moduł uwierzytelniania dwuskładnikowego w usługach AD FS, zobacz Używanie uwierzytelniania wieloskładnikowego z usługami federacyjnymi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1da52-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="1da52-143">Wyświetlanie obiektów urządzeń i zarządzanie nimi w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1da52-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="1da52-144">Z portalu administratora platformy Azure hello można wyświetlać, blokować i odblokowywać urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1da52-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="1da52-145">Urządzenie jest zablokowane przestaną być tooapplications dostępu, które są skonfigurowane tooallow tylko zarejestrowane urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1da52-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="1da52-146">**tooview obiektów urządzeń w usłudze Azure Active Directory i zarządzanie nimi:**</span><span class="sxs-lookup"><span data-stu-id="1da52-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="1da52-147">Zaloguj się na toohello portalu Microsoft Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1da52-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="1da52-148">W okienku po lewej stronie powitania wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1da52-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="1da52-149">Wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="1da52-149">Select your directory.</span></span>

4.  <span data-ttu-id="1da52-150">Wybierz **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="1da52-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="1da52-151">Kliknij przycisk hello użytkownika, dla którego chcesz toosee hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1da52-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="1da52-152">Wybierz **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="1da52-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="1da52-153">Wybierz **zarejestrowanych urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="1da52-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="1da52-154">Teraz można przejrzeć, blokowania lub odblokować zarejestrowane urządzenia hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1da52-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="1da52-155">Karcie hello użytkowników urządzeń z systemem Windows 10, które są lokalne przyłączonych do domeny i automatycznie zarejestrowane nie jest wyświetlana. Użyj toofind polecenia PowerShell Get-MsolDevice hello wszystkich urządzeń organizacji.</span><span class="sxs-lookup"><span data-stu-id="1da52-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1da52-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1da52-156">Next steps</span></span>

<span data-ttu-id="1da52-157">toosetup automatycznego rejestracji urządzenia, zobacz [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="1da52-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


