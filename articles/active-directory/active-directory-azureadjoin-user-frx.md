---
title: "Konfigurowanie nowego urządzenia z usługą Azure AD podczas instalacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Konfigurowanie nowego urządzenia z usługą Azure AD podczas instalacji
W systemie Windows 10 użytkownicy mogą dołączenie swojego urządzenia do usługi Azure Active Directory (Azure AD) w pierwszego uruchomienia komputera (FRX). Dzięki temu organizacje mogą Dystrybuuj urządzenia porządnie zapakowane pracownikom lub studentów lub daj wybrać własne urządzenia (CYOD).
Jeśli system Windows 10 Professional lub Windows 10 Enterprise Edition jest zainstalowany na urządzeniu, środowisko domyślnie procesu instalacji urządzenia należące do firmy.

## <a name="to-join-a-device-to-azure-ad"></a>Aby dołączyć urządzenie do usługi Azure AD
1. Po włączeniu nowe urządzenie i rozpocząć proces instalacji, powinna zostać wyświetlona **pierwsze gotowe** wiadomości. Postępuj zgodnie z monitami, aby skonfigurować urządzenie.
2. Rozpocznij od Dostosowywanie region i język. Następnie zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft.
   ![Dostosowywanie w Twoim regionie](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Wybierz sieć, który ma być używany do łączenia się z Internetem.
4. Określ, czy używasz osobiste urządzenie lub urządzenia należące do firmy. Jeśli należące do firmy, kliknij przycisk **to urządzenie należy do mojej organizacji**. Spowoduje to uruchomienie środowiska Azure AD Join. Poniżej znajduje się ekranu, że zobaczysz, jeśli używasz systemu Windows 10 Professional.
   <center>
   ![Kto jest właścicielem tego ekranu komputera](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Wprowadź poświadczenia, które zostały przekazane użytkownikowi przez organizację.
   <center>
   ![Ekran logowania](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Po wprowadzeniu nazwy użytkownika pasującego dzierżawy znajduje się w usłudze Azure AD. Jeśli w domenie federacyjnych, nastąpi przekierowanie do lokalnego serwera Secure Token Service (STS) — na przykład Active Directory Federation Services (AD FS).
7. Jeśli użytkownik jest użytkownikiem domeny z systemem innym niż federacyjnych, wprowadź swoje poświadczenia bezpośrednio na stronie hostowanych przez usługi AD platformy Azure. Jeśli skonfigurowano logo firmy, będą również Zobacz logo organizacji i obsługuje tekstu.
8. Zostanie wyświetlony monit o żądanie uwierzytelniania wieloskładnikowego. To żądanie jest konfigurowane przez administratora IT.
9. Usługi Azure AD sprawdza, czy użytkownika/urządzenie wymaga rejestracji w zarządzaniu urządzeniami przenośnymi.
10. System Windows zarejestrowanie urządzenia w katalogu organizacji w usłudze Azure AD i rejestruje w przystawce Zarządzanie urządzeniami przenośnymi w razie potrzeby.
11. Jeśli jesteś użytkownikiem zarządzanych systemu Windows umożliwia przejście do pulpitu za pośrednictwem proces automatycznego logowania.
12. W przypadku użytkowników federacyjnych są przekierowywane do ekranu logowania systemu Windows, aby wprowadzić swoje poświadczenia.

> [!NOTE]
> Przyłączania do domeny usługi Active Directory systemu Windows Server lokalne środowisko out-of-box systemu Windows nie jest obsługiwana. W związku z tym, jeśli planujesz przyłączyć komputer do domeny, należy wybrać link **instalacji systemu Windows przy użyciu konta lokalnego** zamiast tego. Następnie można przyłączyć do domeny z ustawień na komputerze, jak zostało wykonane przed.
> 
> 

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

