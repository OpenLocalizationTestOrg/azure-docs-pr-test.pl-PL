---
title: "System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzeń do pracy | Dokumentacja firmy Microsoft"
description: "Omówienie wdrażania urządzeń z systemem Windows 10 dla przedsiębiorstw i jak toointegrate w usłudze Azure Active Directory dla hello systemu Windows w chmurze. Różni się znacząco różnych sposobów hello urządzenia można udostępniać oraz używane w przedsiębiorstwie za pomocą hello portalu Azure."
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
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="e6dbd-105">System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="e6dbd-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="e6dbd-106">Windows 10 zapewnia hello tooleverage możliwości usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e6dbd-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e6dbd-107">Można połączyć tooAzure urządzeń z systemem Windows 10 AD, dzięki czemu użytkownicy mogą się zalogować w tooWindows przy użyciu konta usługi Azure AD lub przez dodanie ich identyfikatorów Azure toogain dostępu toobusiness aplikacji i zasobów.</span><span class="sxs-lookup"><span data-stu-id="e6dbd-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Usługa Azure Active Directory z chmurą systemu Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="e6dbd-109">Integrowanie urządzeń z systemem Windows 10 w usłudze Azure Active Directory — Mapa zawartości</span><span class="sxs-lookup"><span data-stu-id="e6dbd-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="e6dbd-110">następujące tematy Hello wgląd w różne możliwości urządzeń z systemem Windows 10 w organizacji.</span><span class="sxs-lookup"><span data-stu-id="e6dbd-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="e6dbd-111">Tematy</span><span class="sxs-lookup"><span data-stu-id="e6dbd-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="e6dbd-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e6dbd-112">Getting started</span></span> |[<span data-ttu-id="e6dbd-113">Przy użyciu urządzeń z systemem Windows 10 w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="e6dbd-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="e6dbd-114">Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="e6dbd-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="e6dbd-115">Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="e6dbd-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="e6dbd-116">Wdrożenie</span><span class="sxs-lookup"><span data-stu-id="e6dbd-116">Deployment</span></span> |[<span data-ttu-id="e6dbd-117">Scenariusze użycia i zagadnienia dotyczące wdrażania dla usługi Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="e6dbd-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="e6dbd-118">Łączenie urządzeń przyłączonych do domeny tooAzure AD, dla systemu Windows 10 napotyka</span><span class="sxs-lookup"><span data-stu-id="e6dbd-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="e6dbd-119">Włączanie Microsoft Passport for work w organizacji hello</span><span class="sxs-lookup"><span data-stu-id="e6dbd-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="e6dbd-120">Włączenie roamingu stanu przedsiębiorstwa w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="e6dbd-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="e6dbd-121">Zadania użytkownika</span><span class="sxs-lookup"><span data-stu-id="e6dbd-121">User tasks</span></span> |[<span data-ttu-id="e6dbd-122">Konfigurowanie nowego urządzenia z systemem Windows 10 z usługą Azure AD podczas instalacji</span><span class="sxs-lookup"><span data-stu-id="e6dbd-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="e6dbd-123">Konfigurowanie urządzenia Windows 10 z usługą Azure AD z menu ustawień hello</span><span class="sxs-lookup"><span data-stu-id="e6dbd-123">Setting up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="e6dbd-124">Sprzęganie osobiste organizacji tooyour urządzenia z systemem Windows 10</span><span class="sxs-lookup"><span data-stu-id="e6dbd-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

