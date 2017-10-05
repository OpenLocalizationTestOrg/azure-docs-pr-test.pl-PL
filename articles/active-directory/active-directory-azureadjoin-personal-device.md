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
# <a name="join-a-personal-device-to-your-organization"></a>Przyłączanie urządzenia osobistego do organizacji
## <a name="to-join-a-windows-10-device-to-your-organization"></a>Aby przyłączyć urządzenie z systemem Windows 10 do organizacji
1. Z **Start** menu, wybierz opcję **ustawienia**.
2. Wybierz **kont**, a następnie kliknij przycisk **konta**.
3. Kliknij przycisk **dodać konta służbowego**, a następnie wpisz w Twoim kontem organizacyjnym.
4. Na stronie logowania dla Twojej organizacji, wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**.
5. Zostanie wyświetlony monit dla żądania uwierzytelniania wieloskładnikowego. (To żądanie jest konfigurowane przez administratora IT).
6. Azure Active Directory (Azure AD), sprawdza, czy urządzenie wymaga rejestracji funkcji zarządzania urządzeniami przenośnymi.
7. System Windows zarejestrowanie urządzenia w katalogu organizacji w usłudze Azure AD i rejestruje w przystawce Zarządzanie urządzeniami przenośnymi w razie potrzeby.
8. Jeśli jesteś użytkownikiem zarządzanych systemu Windows umożliwia przejście do pulpitu za pośrednictwem automatycznego logowania.
9. W przypadku użytkowników federacyjnych, nastąpi przekierowanie do ekranu logowania systemu Windows o podanie poświadczeń.

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

