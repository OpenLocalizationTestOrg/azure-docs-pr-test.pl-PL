---
title: "Windows 10 dla przedsiębiorstw: sposoby użycia urządzeń do pracy | Dokumentacja firmy Microsoft"
description: "Omówienie wdrażania urządzeń z systemem Windows 10 dla przedsiębiorstw i sposobu integracji z usługą Azure Active Directory dla chmury systemu Windows. Różni się różne sposoby urządzenia można alokować i używane w przedsiębiorstwie za pomocą portalu Azure."
keywords: "chmury systemu Windows, Windows w usłudze Azure Active Directory urządzenia systemu Windows 10 w Azure, urządzeń z systemem Windows Azure"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="82ecd-105">System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="82ecd-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="82ecd-106">Windows 10 daje możliwość wykorzystać usługę Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82ecd-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="82ecd-107">Urządzeń z systemem Windows 10 można połączyć z usługą Azure AD, dzięki czemu można logowania się do systemu Windows przy użyciu konta usługi Azure AD lub przez dodanie ich identyfikatorów Azure do uzyskiwania dostępu do aplikacji biznesowych i zasobów.</span><span class="sxs-lookup"><span data-stu-id="82ecd-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Usługa Azure Active Directory z chmurą systemu Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="82ecd-109">Integrowanie urządzeń z systemem Windows 10 w usłudze Azure Active Directory — Mapa zawartości</span><span class="sxs-lookup"><span data-stu-id="82ecd-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="82ecd-110">Poniższe tematy zawierają szczegółowe informacje na różne możliwości urządzeń z systemem Windows 10 w organizacji.</span><span class="sxs-lookup"><span data-stu-id="82ecd-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="82ecd-111">Tematy</span><span class="sxs-lookup"><span data-stu-id="82ecd-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="82ecd-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="82ecd-112">Getting started</span></span> |[<span data-ttu-id="82ecd-113">Przy użyciu urządzeń z systemem Windows 10 w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="82ecd-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="82ecd-114">Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="82ecd-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="82ecd-115">Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="82ecd-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="82ecd-116">Wdrożenie</span><span class="sxs-lookup"><span data-stu-id="82ecd-116">Deployment</span></span> |[<span data-ttu-id="82ecd-117">Scenariusze użycia i zagadnienia dotyczące wdrażania dla usługi Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="82ecd-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="82ecd-118">Łączenie urządzeń przyłączonych do domeny do usługi Azure AD w systemie Windows 10 napotyka</span><span class="sxs-lookup"><span data-stu-id="82ecd-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="82ecd-119">Włączanie Microsoft Passport for work w organizacji</span><span class="sxs-lookup"><span data-stu-id="82ecd-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="82ecd-120">Włączenie roamingu stanu przedsiębiorstwa w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="82ecd-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="82ecd-121">Zadania użytkownika</span><span class="sxs-lookup"><span data-stu-id="82ecd-121">User tasks</span></span> |[<span data-ttu-id="82ecd-122">Konfigurowanie nowego urządzenia z systemem Windows 10 z usługą Azure AD podczas instalacji</span><span class="sxs-lookup"><span data-stu-id="82ecd-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="82ecd-123">Konfigurowanie urządzenia Windows 10 z usługą Azure AD z menu ustawień</span><span class="sxs-lookup"><span data-stu-id="82ecd-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="82ecd-124">Dołączenie urządzenia osobistego systemu Windows 10 do organizacji</span><span class="sxs-lookup"><span data-stu-id="82ecd-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

