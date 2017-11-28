---
title: "aaaSet urządzenia z systemem Windows 10 z usługą Azure AD z ustawień | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak użytkownicy mogą dołączać tooAzure AD za pomocą menu Ustawienia hello."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="896d2-103">Konfigurowanie urządzenia Windows 10 z usługą Azure AD z ustawień</span><span class="sxs-lookup"><span data-stu-id="896d2-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="896d2-104">Jeśli masz już przy użyciu systemu Windows 7 lub Windows 8 i komputera lub urządzenia został uaktualniony tooWindows 10, można dołączyć tooAzure usługi Active Directory (Azure AD) za pośrednictwem hello ustawień menu.</span><span class="sxs-lookup"><span data-stu-id="896d2-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="896d2-105">toojoin tooAzure AD z menu ustawień hello</span><span class="sxs-lookup"><span data-stu-id="896d2-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="896d2-106">Z hello **Start** menu, kliknij przycisk hello **ustawienia** panelu.</span><span class="sxs-lookup"><span data-stu-id="896d2-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="896d2-107">Z **ustawienia**, wybierz pozycję **systemu**->**o**->**usługi Azure AD Join**.</span><span class="sxs-lookup"><span data-stu-id="896d2-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="896d2-108"><center>
   ![Dołącz do usługi Azure AD z menu ustawień hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="896d2-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="896d2-109">Kliknij przycisk **Kontynuuj** w hello Azure AD Join w oknie wiadomości.</span><span class="sxs-lookup"><span data-stu-id="896d2-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="896d2-110"><center>
   ![W oknie wiadomości usługi Azure AD JOIN](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="896d2-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="896d2-111">Podaj poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="896d2-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="896d2-112">To środowisko logowania będzie zawierać wszystkie kroki hello, które są wymagane toocomplete uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="896d2-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="896d2-113">Jeśli należą federacyjnych dzierżawcy, administrator zapewnia środowisko federacyjnego hello jest obsługiwana przez organizację.</span><span class="sxs-lookup"><span data-stu-id="896d2-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="896d2-114"><center>
   ![Podaj poświadczenia logowania](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="896d2-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="896d2-115">Jeśli w organizacji są skonfigurowane uwierzytelnianie wieloskładnikowe Azure łączenia tooAzure AD, podaj hello czynnika przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="896d2-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="896d2-116">Kliknij przycisk **Akceptuj** na powitania **zezwolić tej toobe urządzenia zarządzane** ekranu.</span><span class="sxs-lookup"><span data-stu-id="896d2-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="896d2-117">Powinna zostać wyświetlona wiadomość hello "urządzenie jest teraz tooyour dołączonego do organizacji w usłudze Azure AD".</span><span class="sxs-lookup"><span data-stu-id="896d2-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="896d2-118">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="896d2-118">Additional information</span></span>
* [<span data-ttu-id="896d2-119">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="896d2-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="896d2-120">Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="896d2-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="896d2-121">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="896d2-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="896d2-122">Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="896d2-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

