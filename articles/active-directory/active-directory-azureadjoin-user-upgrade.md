---
title: "Konfigurowanie urządzenia Windows 10 z usługą Azure AD z ustawień | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak użytkownicy mogą dołączać do usługi Azure AD za pomocą menu Ustawienia."
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="590a3-103">Konfigurowanie urządzenia Windows 10 z usługą Azure AD z ustawień</span><span class="sxs-lookup"><span data-stu-id="590a3-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="590a3-104">Jeśli korzystasz już z systemem Windows 7 lub Windows 8 i komputera lub urządzenia został uaktualniony do systemu Windows 10, można dołączyć do usługi Azure Active Directory (Azure AD), za pomocą menu Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="590a3-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="590a3-105">Aby przyłączyć się do usługi Azure AD z menu ustawień</span><span class="sxs-lookup"><span data-stu-id="590a3-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="590a3-106">Z **Start** menu, kliknij przycisk **ustawienia** panelu.</span><span class="sxs-lookup"><span data-stu-id="590a3-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="590a3-107">Z **ustawienia**, wybierz pozycję **systemu**->**o**->**usługi Azure AD Join**.</span><span class="sxs-lookup"><span data-stu-id="590a3-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="590a3-108"><center>
   ![Dołącz do usługi Azure AD z menu ustawień](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="590a3-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="590a3-109">Kliknij przycisk **Kontynuuj** w oknie wiadomości Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="590a3-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="590a3-110"><center>
   ![W oknie wiadomości usługi Azure AD JOIN](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="590a3-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="590a3-111">Podaj poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="590a3-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="590a3-112">To środowisko logowania będzie zawierać wszystkie kroki, które są wymagane do ukończenia uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="590a3-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="590a3-113">Jeśli należą federacyjnych dzierżawcy administratora pozwoli z obsługą federacji, hostowanej przez Twoją organizację.</span><span class="sxs-lookup"><span data-stu-id="590a3-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="590a3-114"><center>
   ![Podaj poświadczenia logowania](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="590a3-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="590a3-115">W przypadku organizacji skonfigurował Azure Multi-Factor Authentication w celu przyłączenia się do usługi Azure AD, należy podać drugi składnik przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="590a3-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="590a3-116">Kliknij przycisk **Akceptuj** na **Zezwalaj na to urządzenie, które mają być zarządzane** ekranu.</span><span class="sxs-lookup"><span data-stu-id="590a3-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="590a3-117">Powinien zostać wyświetlony komunikat "urządzenie zostało przyłączone do Twojej organizacji w usłudze Azure AD".</span><span class="sxs-lookup"><span data-stu-id="590a3-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="590a3-118">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="590a3-118">Additional information</span></span>
* [<span data-ttu-id="590a3-119">Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="590a3-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="590a3-120">Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10</span><span class="sxs-lookup"><span data-stu-id="590a3-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="590a3-121">Konfigurowanie funkcji Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="590a3-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="590a3-122">Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="590a3-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

