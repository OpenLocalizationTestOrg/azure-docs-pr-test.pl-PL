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
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Konfigurowanie urządzenia Windows 10 z usługą Azure AD z ustawień
Jeśli korzystasz już z systemem Windows 7 lub Windows 8 i komputera lub urządzenia został uaktualniony do systemu Windows 10, można dołączyć do usługi Azure Active Directory (Azure AD), za pomocą menu Ustawienia.

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a>Aby przyłączyć się do usługi Azure AD z menu ustawień
1. Z **Start** menu, kliknij przycisk **ustawienia** panelu.
2. Z **ustawienia**, wybierz pozycję **systemu**->**o**->**usługi Azure AD Join**.
   
   <center>
   ![Dołącz do usługi Azure AD z menu ustawień](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Kliknij przycisk **Kontynuuj** w oknie wiadomości Azure AD Join.
   
   <center>
   ![W oknie wiadomości usługi Azure AD JOIN](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Podaj poświadczenia logowania. To środowisko logowania będzie zawierać wszystkie kroki, które są wymagane do ukończenia uwierzytelniania. Jeśli należą federacyjnych dzierżawcy administratora pozwoli z obsługą federacji, hostowanej przez Twoją organizację.
   <center>
   ![Podaj poświadczenia logowania](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. W przypadku organizacji skonfigurował Azure Multi-Factor Authentication w celu przyłączenia się do usługi Azure AD, należy podać drugi składnik przed kontynuowaniem.
6. Kliknij przycisk **Akceptuj** na **Zezwalaj na to urządzenie, które mają być zarządzane** ekranu.
7. Powinien zostać wyświetlony komunikat "urządzenie zostało przyłączone do Twojej organizacji w usłudze Azure AD".

## <a name="additional-information"></a>Dodatkowe informacje
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)

