---
title: "krok aaaTwo weryfikacji i usług AD FS — usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA i usług AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Wprowadzenie do usługi Azure Multi-Factor Authentication i usług Active Directory Federation Services
<center>![Chmura](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

W przypadku organizacji, które sfederowały lokalną usługę Active Directory z usługą Azure Active Directory za pomocą usług AD FS, dostępne są dwie opcje używania usługi Azure Multi-Factor Authentication.

* Zabezpieczenie zasobów w chmurze za pomocą usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services
* Zabezpieczenie zasobów w chmurze i zasobów lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication

Witaj w poniższej tabeli znajduje się podsumowanie hello weryfikacji środowisko obejmujące zabezpieczanie zasobów przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS

| Proces weryfikacji — aplikacje korzystające z przeglądarki | Proces weryfikacji — aplikacje niekorzystające z przeglądarki |
|:--- |:--- |:--- |
| Zabezpieczanie zasobów usługi Azure AD za pomocą usługi Azure Multi-Factor Authentication |<li>pierwszym krokiem weryfikacji Hello jest wykonywane lokalnie za pomocą usług AD FS.</li> <li>drugim krokiem Hello to metoda telefoniczną przeprowadzane przy użyciu uwierzytelniania w chmurze.</li> |
| Zabezpieczanie zasobów usługi Azure AD za pomocą usług Active Directory Federation Services |<li>pierwszym krokiem weryfikacji Hello jest wykonywane lokalnie za pomocą usług AD FS.</li><li>drugi etap Hello jest realizowany lokalnie przy zachowaniu hello oświadczeń.</li> |

Zastrzeżenia dotyczące haseł aplikacji używanych przez użytkowników federacyjnych:

* Hasła aplikacji są weryfikowane przy użyciu uwierzytelniania w chmurze, co pozwala pominąć federację. Federacja jest aktywnie używana tylko podczas konfigurowania hasła aplikacji.
* Ustawienia lokalnej kontroli dostępu klienta nie są uznawane przez hasła aplikacji.
* Nie będzie można lokalnie rejestrować uwierzytelniania haseł aplikacji.
* Wyłączenie/usunięcie konta może trwać toothree godzin synchronizacji katalogów, opóźnienie wyłączenia/usunięcia hasła aplikacji w hello tożsamość w chmurze.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje na temat konfigurowania usługi Azure Multi-Factor Authentication lub powitania serwera usługi Azure Multi-Factor Authentication z usługami AD FS zobacz następujące artykuły hello:

* [Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Zabezpieczanie zasobów w chmurze i lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS systemu Windows Server 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Zabezpieczanie zasobów w chmurze i zasobów lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
