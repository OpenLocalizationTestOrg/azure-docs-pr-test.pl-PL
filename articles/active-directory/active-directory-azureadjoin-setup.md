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
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Konfigurowanie funkcji Azure AD Join w organizacji
Przed rozpoczęciem konfigurowania usługi Azure Active Directory Join (Azure AD Join), należy tooeither Synchronizacja katalogu lokalnych użytkowników toohello chmury w górę lub ręcznie utworzyć konta zarządzane w usłudze Azure AD.

Szczegółowe instrukcje synchronizowanie tooAzure użytkowników z lokalnej usługi AD znajdują się w [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

toomanually tworzenie i zarządzanie użytkownikami w usłudze Azure AD, można znaleźć za[Zarządzanie użytkownikami w usłudze Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Konfigurowanie rejestracji urządzeń
1. Zaloguj się na toohello portalu Azure jako administrator.
2. W okienku po lewej stronie powitania wybierz **usługi Active Directory**.
3. Na powitania **katalogu** , a następnie wybierz katalog.
4. Wybierz hello **Konfiguruj** kartę.
5. Przejdź toohello **urządzeń** sekcji.
6. Na powitania **urządzeń** ustaw następujące hello:  
   * **Maksymalna liczba urządzeń na użytkownika**: Wybierz hello maksymalną liczbę urządzeń, które użytkownik może mieć w usłudze Azure AD.  Jeśli użytkownik osiągnie ten limit przydziału, nie będą mogli tooadd dodatkowych urządzeń dopóki co najmniej jeden z istniejących urządzeń są usuwane.
   * **WYMAGAJ uwierzytelniania WIELOSKŁADNIKOWEGO tooJOIN urządzeń**: Określanie, czy użytkownicy są wymagane tooprovide drugiego uwierzytelniania dwuskładnikowego toojoin ich tooAzure urządzenia AD. Aby uzyskać więcej informacji dotyczących usługi Azure Multi-Factor Authentication, zobacz [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **Użytkownicy mogą AZURE AD JOIN urządzenia**: Wybierz hello użytkowników i grup, które mogą toojoin urządzeń tooAzure AD.
   * **URZĄDZEŃ dołączonych do programu dodatkowych ADMINISTRATORÓW usługi AZURE AD**: Z usługi Azure AD Premium lub hello Enterprise Mobility Suite (EMS), można wybrać użytkowników, którzy mają prawa administratora lokalnego toohello urządzenia. Administratorom globalnym i właścicielom urządzeń uprawnienia administratora lokalnego są przyznawane domyślnie.

<center>![Konfigurowanie rejestracji urządzeń](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

Po skonfigurowaniu usługi Azure AD Join dla użytkowników, można połączyć z tooAzure AD za pomocą ich firmowych lub osobistych urządzeń.

Poniżej przedstawiono trzy scenariusze hello można korzystać z tooenable Twojego tooset użytkowników usługi Azure AD Join:

* Użytkownikom dołączenie urządzenia należące do firmy bezpośrednio tooAzure AD.
* Użytkownicy — przyłączenie do domeny należące do firmy urządzenia toohello lokalnej usługi Active Directory, a następnie rozszerzyć hello urządzenia tooAzure AD.
* Użytkownikom dodawanie pracy lub szkoły kont tooWindows na urządzeniu osobistym.

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

