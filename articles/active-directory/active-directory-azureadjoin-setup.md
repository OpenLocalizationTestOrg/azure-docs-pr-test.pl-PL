---
title: "aaaSetting funkcję Azure AD Join dla użytkowników | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="e6576-103">Konfigurowanie funkcji Azure AD Join w organizacji</span><span class="sxs-lookup"><span data-stu-id="e6576-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="e6576-104">Przed rozpoczęciem konfigurowania usługi Azure Active Directory Join (Azure AD Join), należy tooeither Synchronizacja katalogu lokalnych użytkowników toohello chmury w górę lub ręcznie utworzyć konta zarządzane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6576-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="e6576-105">Szczegółowe instrukcje synchronizowanie tooAzure użytkowników z lokalnej usługi AD znajdują się w [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e6576-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="e6576-106">toomanually tworzenie i zarządzanie użytkownikami w usłudze Azure AD, można znaleźć za[Zarządzanie użytkownikami w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6576-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="e6576-107">Konfigurowanie rejestracji urządzeń</span><span class="sxs-lookup"><span data-stu-id="e6576-107">Set up device registration</span></span>
1. <span data-ttu-id="e6576-108">Zaloguj się na toohello portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e6576-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="e6576-109">W okienku po lewej stronie powitania wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6576-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="e6576-110">Na powitania **katalogu** , a następnie wybierz katalog.</span><span class="sxs-lookup"><span data-stu-id="e6576-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="e6576-111">Wybierz hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="e6576-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="e6576-112">Przejdź toohello **urządzeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e6576-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="e6576-113">Na powitania **urządzeń** ustaw następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e6576-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="e6576-114">**Maksymalna liczba urządzeń na użytkownika**: Wybierz hello maksymalną liczbę urządzeń, które użytkownik może mieć w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6576-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="e6576-115">Jeśli użytkownik osiągnie ten limit przydziału, nie będą mogli tooadd dodatkowych urządzeń dopóki co najmniej jeden z istniejących urządzeń są usuwane.</span><span class="sxs-lookup"><span data-stu-id="e6576-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="e6576-116">**WYMAGAJ uwierzytelniania WIELOSKŁADNIKOWEGO tooJOIN urządzeń**: Określanie, czy użytkownicy są wymagane tooprovide drugiego uwierzytelniania dwuskładnikowego toojoin ich tooAzure urządzenia AD.</span><span class="sxs-lookup"><span data-stu-id="e6576-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="e6576-117">Aby uzyskać więcej informacji dotyczących usługi Azure Multi-Factor Authentication, zobacz [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="e6576-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="e6576-118">**Użytkownicy mogą AZURE AD JOIN urządzenia**: Wybierz hello użytkowników i grup, które mogą toojoin urządzeń tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e6576-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="e6576-119">**URZĄDZEŃ dołączonych do programu dodatkowych ADMINISTRATORÓW usługi AZURE AD**: Z usługi Azure AD Premium lub hello Enterprise Mobility Suite (EMS), można wybrać użytkowników, którzy mają prawa administratora lokalnego toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e6576-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="e6576-120">Administratorom globalnym i właścicielom urządzeń uprawnienia administratora lokalnego są przyznawane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e6576-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="e6576-121"><center>![Konfigurowanie rejestracji urządzeń](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="e6576-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="e6576-122">Po skonfigurowaniu usługi Azure AD Join dla użytkowników, można połączyć z tooAzure AD za pomocą ich firmowych lub osobistych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e6576-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="e6576-123">Poniżej przedstawiono trzy scenariusze hello można korzystać z tooenable Twojego tooset użytkowników usługi Azure AD Join:</span><span class="sxs-lookup"><span data-stu-id="e6576-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="e6576-124">Użytkownikom dołączenie urządzenia należące do firmy bezpośrednio tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e6576-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="e6576-125">Użytkownicy — przyłączenie do domeny należące do firmy urządzenia toohello lokalnej usługi Active Directory, a następnie rozszerzyć hello urządzenia tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e6576-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="e6576-126">Użytkownikom dodawanie pracy lub szkoły kont tooWindows na urządzeniu osobistym.</span><span class="sxs-lookup"><span data-stu-id="e6576-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="e6576-127">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="e6576-127">Additional information</span></span>
* [<span data-ttu-id="e6576-128">System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="e6576-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="e6576-129">Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="e6576-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="e6576-130">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="e6576-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="e6576-131">Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="e6576-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="e6576-132">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="e6576-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

