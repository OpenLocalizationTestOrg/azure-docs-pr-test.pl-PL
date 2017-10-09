---
title: "aaaSet nowego urządzenia z usługą Azure AD podczas instalacji | Dokumentacja firmy Microsoft"
description: "Temat, który objaśnia, jak użytkownicy mogli skonfigurować Azure AD Join podczas ich środowisko pierwszego uruchomienia."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Konfigurowanie nowego urządzenia z usługą Azure AD podczas instalacji
W systemie Windows 10 użytkownicy mogą dołączać tooAzure ich urządzeń do usługi Active Directory (Azure AD) w hello pierwszego uruchomienia (FRX). Umożliwia organizacjom toodistribute porządnie zapakowane urządzeń tootheir pracowników lub studentów lub daj wybrać własne urządzenia (CYOD).
Jeśli system Windows 10 Professional lub Windows 10 Enterprise Edition jest zainstalowany na urządzeniu, hello zgłaszać proces instalacji toohello domyślne ustawienia dla urządzeń należących do firmy.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin tooAzure urządzenia AD
1. Po włączeniu nowe urządzenie i rozpocząć proces instalacji hello, powinny pojawić się hello **pierwsze gotowe** wiadomości. Wykonaj hello monity tooset Twojego urządzenia.
2. Rozpocznij od Dostosowywanie region i język. Następnie zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.
   ![Dostosowywanie w Twoim regionie](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Wybierz sieć hello ma toouse podłączania toohello Internet.
4. Określ, czy używasz osobiste urządzenie lub urządzenia należące do firmy. Jeśli należące do firmy, kliknij przycisk **to urządzenie należy organizacji toomy**. Spowoduje to uruchomienie środowiska Azure AD Join hello. Poniżej znajduje się ekranu, że zobaczysz, jeśli używasz systemu Windows 10 Professional.
   <center>
   ![Kto jest właścicielem tego ekranu komputera](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Wprowadź poświadczenia hello, które zostały podane tooyou przez organizację.
   <center>
   ![Ekran logowania](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Po wprowadzeniu nazwy użytkownika pasującego dzierżawy znajduje się w usłudze Azure AD. Jeśli w domenie federacyjnych, będzie tooyour przekierowanego lokalnego serwera Secure Token Service (STS) — na przykład Active Directory Federation Services (AD FS).
7. Jeśli użytkownik jest użytkownikiem domeny z systemem innym niż federacyjnych, wprowadź swoje poświadczenia bezpośrednio na hello Azure strony hostowanych przez usługi AD. Jeśli skonfigurowano logo firmy, będą również Zobacz logo organizacji i obsługuje tekstu.
8. Zostanie wyświetlony monit o żądanie uwierzytelniania wieloskładnikowego. To żądanie jest konfigurowane przez administratora IT.
9. Usługi Azure AD sprawdza, czy użytkownika/urządzenie wymaga rejestracji w zarządzaniu urządzeniami przenośnymi.
10. System Windows rejestruje urządzenie hello w katalogu organizacji hello w usłudze Azure AD i rejestruje w przystawce Zarządzanie urządzeniami przenośnymi w razie potrzeby.
11. Jeśli jesteś użytkownikiem zarządzanych, system Windows wykonuje toohello pulpitu za pośrednictwem hello automatycznego procesu logowania.
12. W przypadku użytkowników federacyjnych są przekierowywane toohello logowania systemu Windows ekranu tooenter swoje poświadczenia.

> [!NOTE]
> Dołączania lokalnej domeny usługi Active Directory systemu Windows Server w systemie Windows hello out-of-box experience nie jest obsługiwane. W związku z tym, jeśli planujesz toojoin domeny tooa komputera, należy wybrać hello link **instalacji systemu Windows przy użyciu konta lokalnego** zamiast tego. Następnie można dołączyć domeny hello z hello ustawienia na komputerze, jak zostało wykonane przed.
> 
> 

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

