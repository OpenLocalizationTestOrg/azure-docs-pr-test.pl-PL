---
title: "Konfigurowanie funkcji Azure AD Join dla użytkowników| Microsoft Docs"
description: "Wyjaśnia, jak administratorzy mogą skonfigurować funkcję Azure AD Join dla katalogu lokalnego i rejestracji urządzeń."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: c37adc2654f7e931fdda22627e4a6ece2789fd86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="2381d-103">Konfigurowanie funkcji Azure AD Join w organizacji</span><span class="sxs-lookup"><span data-stu-id="2381d-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="2381d-104">Przed skonfigurowaniem usługi Azure Active Directory Join (Azure AD Join), należy albo zsynchronizować katalog lokalny użytkowników z chmurą, albo ręcznie utworzyć konta zarządzane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2381d-104">Before you set up Azure Active Directory Join (Azure AD Join), you need to either sync up your on-premises directory of users to the cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="2381d-105">Aby uzyskać szczegółowe instrukcje dotyczące synchronizacji lokalnych użytkowników z usługą Azure AD, zobacz [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="2381d-105">Detailed instructions for syncing your on-premises users to Azure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="2381d-106">Aby ręcznie tworzyć użytkowników w usłudze Azure AD i zarządzać nimi, zobacz [Zarządzanie użytkownikami w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="2381d-106">To manually create and manage users in Azure AD, refer to [User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="2381d-107">Konfigurowanie rejestracji urządzeń</span><span class="sxs-lookup"><span data-stu-id="2381d-107">Set up device registration</span></span>
1. <span data-ttu-id="2381d-108">Zaloguj się w witrynie Azure Portal jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2381d-108">Log on to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="2381d-109">W lewym okienku wybierz pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2381d-109">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="2381d-110">Na karcie **Katalog** wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="2381d-110">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="2381d-111">Wybierz kartę **Konfigurowanie**.</span><span class="sxs-lookup"><span data-stu-id="2381d-111">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="2381d-112">Przejdź do sekcji **Urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="2381d-112">Go to the **Devices** section.</span></span>
6. <span data-ttu-id="2381d-113">Na karcie **Urządzenia** ustaw wartości poniższych elementów:</span><span class="sxs-lookup"><span data-stu-id="2381d-113">On the **devices** tab, set the following:</span></span>  
   * <span data-ttu-id="2381d-114">**MAKSYMALNA LICZBA URZĄDZEŃ PRZYPADAJĄCYCH NA JEDNEGO UŻYTKOWNIKA**: wybierz maksymalną liczbę urządzeń, jaką użytkownik może mieć w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2381d-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select the maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="2381d-115">Jeśli użytkownik osiągnie ten limit przydziału, nie będzie mógł dodać dodatkowych urządzeń dopóki co najmniej jedno z istniejących urządzeń nie zostanie usunięte.</span><span class="sxs-lookup"><span data-stu-id="2381d-115">If a user reaches this quota, they will not be able to add additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="2381d-116">**WYMAGAJ UWIERZYTELNIANIA WIELOSKŁADNIKOWEGO PODCZAS PRZYŁĄCZANIA URZĄDZEŃ**: ustal, czy użytkownicy muszą zapewnić drugi składnik uwierzytelniania w celu przyłączenia urządzenia do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2381d-116">**REQUIRE MULTI-FACTOR AUTH TO JOIN DEVICES**: Set whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="2381d-117">Aby uzyskać więcej informacji o usłudze Azure Multi-Factor Authentication, zobacz [Wprowadzenie do usługi Azure Multi-Factor Authentication w chmurze](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="2381d-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in the cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="2381d-118">**UŻYTKOWNICY MOGĄ PRZYŁĄCZAĆ URZĄDZENIA DO USŁUGI AZURE AD**: wybierz użytkowników i grupy, które mogą przyłączać urządzenia do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2381d-118">**USERS MAY AZURE AD JOIN DEVICES**: Select the users and groups that are allowed to join devices to Azure AD.</span></span>
   * <span data-ttu-id="2381d-119">**DODATKOWI ADMINISTRATORZY URZĄDZEŃ PRZYŁĄCZONYCH DO USŁUGI AZURE AD**: korzystając z usługi Azure AD Premium lub pakietu Enterprise Mobility Suite (EMS), możesz wybrać, którzy użytkownicy mają przyznane uprawnienia administratora lokalnego do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2381d-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or the Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights to the device.</span></span> <span data-ttu-id="2381d-120">Administratorom globalnym i właścicielom urządzeń uprawnienia administratora lokalnego są przyznawane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="2381d-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="2381d-121"><center>![Konfigurowanie rejestracji urządzeń](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="2381d-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="2381d-122">Skonfigurowanie funkcji Azure AD Join dla użytkowników pozwala im łączyć się z usługą Azure AD za pomocą ich urządzeń firmowych lub osobistych.</span><span class="sxs-lookup"><span data-stu-id="2381d-122">After you set up Azure AD Join for your users, they can connect to Azure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="2381d-123">Poniżej przedstawiono trzy możliwe scenariusze postępowania w celu umożliwienia użytkownikom skonfigurowania funkcji Azure AD Join:</span><span class="sxs-lookup"><span data-stu-id="2381d-123">Following are the three scenarios you can use to enable your users to set up Azure AD Join:</span></span>

* <span data-ttu-id="2381d-124">Użytkownicy dołączają urządzenie należące do firmy bezpośrednio do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2381d-124">Users join a company-owned device directly to Azure AD.</span></span>
* <span data-ttu-id="2381d-125">Użytkownicy przyłączają do domeny urządzenia należącego do firmy do lokalnej usługi Active Directory, a następnie rozszerzają urządzenie o usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2381d-125">Users domain-join a company-owned device to the on-premises Active Directory and then extend the device to Azure AD.</span></span>
* <span data-ttu-id="2381d-126">Użytkownicy dodają konta służbowe do systemu Windows na urządzeniu osobistym.</span><span class="sxs-lookup"><span data-stu-id="2381d-126">Users add work or school accounts to Windows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="2381d-127">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="2381d-127">Additional information</span></span>
* [<span data-ttu-id="2381d-128">System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="2381d-128">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="2381d-129">Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="2381d-129">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2381d-130">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2381d-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="2381d-131">Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="2381d-131">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="2381d-132">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2381d-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

