---
title: "Przyłączanie urządzenia osobistego do organizacji | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak użytkownicy mogą zarejestrować swoje urządzenia osobiste systemu Windows 10 do sieci firmowej, a zawiera kroki wdrażania w scenariuszu BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="7d8c6-103">Przyłączanie urządzenia osobistego do organizacji</span><span class="sxs-lookup"><span data-stu-id="7d8c6-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="7d8c6-104">Aby przyłączyć urządzenie z systemem Windows 10 do organizacji</span><span class="sxs-lookup"><span data-stu-id="7d8c6-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="7d8c6-105">Z **Start** menu, wybierz opcję **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="7d8c6-106">Wybierz **kont**, a następnie kliknij przycisk **konta**.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="7d8c6-107">Kliknij przycisk **dodać konta służbowego**, a następnie wpisz w Twoim kontem organizacyjnym.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="7d8c6-108">Na stronie logowania dla Twojej organizacji, wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="7d8c6-109">Zostanie wyświetlony monit dla żądania uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="7d8c6-110">(To żądanie jest konfigurowane przez administratora IT).</span><span class="sxs-lookup"><span data-stu-id="7d8c6-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="7d8c6-111">Azure Active Directory (Azure AD), sprawdza, czy urządzenie wymaga rejestracji funkcji zarządzania urządzeniami przenośnymi.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="7d8c6-112">System Windows zarejestrowanie urządzenia w katalogu organizacji w usłudze Azure AD i rejestruje w przystawce Zarządzanie urządzeniami przenośnymi w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="7d8c6-113">Jeśli jesteś użytkownikiem zarządzanych systemu Windows umożliwia przejście do pulpitu za pośrednictwem automatycznego logowania.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="7d8c6-114">W przypadku użytkowników federacyjnych, nastąpi przekierowanie do ekranu logowania systemu Windows o podanie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7d8c6-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="7d8c6-115">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="7d8c6-115">Additional information</span></span>
* [<span data-ttu-id="7d8c6-116">System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy</span><span class="sxs-lookup"><span data-stu-id="7d8c6-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="7d8c6-117">Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="7d8c6-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="7d8c6-118">Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="7d8c6-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="7d8c6-119">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="7d8c6-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="7d8c6-120">Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="7d8c6-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="7d8c6-121">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="7d8c6-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

