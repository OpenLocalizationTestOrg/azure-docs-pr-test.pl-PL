---
title: "Omówienie rejestracji urządzeń usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Rejestracja urządzenia w usłudze Azure Active Directory jest hello foundation dla scenariuszy dostępu warunkowego opartego na urządzeniach. Po zarejestrowaniu urządzenia przepisy rejestracji urządzeń usługi Azure Active Directory hello urządzenia przy użyciu tożsamości, który jest używany tooauthenticate powitania po zalogowaniu użytkownika hello."
services: active-directory
keywords: "rejestracja urządzenia, włączanie rejestracji urządzenia, rejestracja urządzenia i MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Wprowadzenie do rejestracja urządzeń w usłudze Azure Active Directory
Rejestracja urządzenia w usłudze Azure Active Directory jest hello foundation dla scenariuszy dostępu warunkowego opartego na urządzeniach. Po zarejestrowaniu urządzenia, rejestracja urządzeń w usłudze Azure Active Directory zapewnia hello urządzenia przy użyciu tożsamości, który jest używany tooauthenticate powitania po zalogowaniu użytkownika hello. urządzenie Hello uwierzytelniony i atrybuty hello hello urządzenia, można następnie tooenforce używane zasady dostępu warunkowego dla aplikacji, które znajdują się w chmurze hello i lokalnych.

W połączeniu z rozwiązaniem management(MDM) urządzeń przenośnych, takich jak Microsoft Intune, dodatkowe informacje o urządzeniu hello są aktualizowane hello atrybuty urządzenia w usłudze Azure Active Directory. Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności. Aby uzyskać więcej informacji na temat rejestrowania urządzeń w usłudze Microsoft Intune, zobacz artykuł [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune) (Rejestrowanie urządzeń w usłudze Intune w celu zarządzania nimi).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Scenariusze obsługiwane przez usługę rejestracji urządzeń w usłudze Azure Active Directory
Rejestracja urządzeń w usłudze Azure Active Directory obejmuje obsługę urządzeń z systemami iOS, Android i Windows. Witaj poszczególne scenariusze wykorzystujące usługę rejestracja urządzeń usługi Azure AD mogą mieć bardziej specyficzne wymagania i obsługę platform. Te scenariusze są następujące:

* **Tooapplications dostępu warunkowego, które są hostowane lokalnie**: zarejestrowane urządzenia można używać z zasadami dostępu dla aplikacji, które są skonfigurowane toouse usług AD FS w systemie Windows Server 2012 R2. Aby uzyskać więcej informacji na temat konfigurowania lokalnego dostępu warunkowego, zobacz [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md) (Konfigurowanie lokalnego dostępu warunkowego przy użyciu usługi rejestracji urządzeń w usłudze Azure Active Directory).
* **Dostęp warunkowy dla usługi Office 365 aplikacji w usłudze Microsoft Intune** : Administratorzy IT mogą aprowizować dostępu warunkowego urządzeń zasady toosecure zasobów firmowych, podczas gdy na powitania sam czas dzięki czemu pracownicy przetwarzający informacje na zgodnych urządzeniach tooaccess hello usługi. Aby uzyskać więcej informacji, zobacz artykuł [Conditional Access Device Policies for Office 365 services](active-directory-conditional-access-device-policies.md) (Zasady dostępu warunkowego urządzeń dla usług Office 365).

## <a name="setting-up-azure-active-directory-device-registration"></a>Konfigurowanie rejestracji urządzeń w usłudze Azure Active Directory
Należy tooenable rejestracji urządzeń usługi Azure AD w hello portalu Azure, aby urządzenia przenośne mogły odnajdywać usługę hello przez wyszukiwanie dobrze znanych rekordów systemu DNS. System DNS firmy należy skonfigurować tak, aby urządzenia z systemem Windows 10, Windows 8.1, Windows 7, Android i iOS można odnajdywania i używania usługi hello.
Możesz wyświetlić i włączanie/wyłączanie urządzeń zarejestrowanych za pomocą hello portalu administratora w usłudze Azure Active Directory.

> [!NOTE]
> Najnowsze informacje dotyczące zobacz temat tooset się automatycznej rejestracji urządzeń [jak toosetup automatyczna rejestracja domeny systemu Windows przyłączone do urządzeń w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Włączanie usługi rejestracji urządzeń w usłudze Azure Active Directory
1. Zaloguj się toohello portalu Microsoft Azure jako Administrator.
2. W okienku po lewej stronie powitania wybierz **usługi Active Directory**.
3. Na powitania **katalogu** , a następnie wybierz katalog.
4. Wybierz hello **Konfiguruj** kartę.
5. Przewiń do sekcji toohello **urządzeń**.
6. Wybierz opcję **WSZYSTKIE** dla pozycji **UŻYTKOWNICY MOGĄ DOŁĄCZAĆ URZĄDZENIA W MIEJSCU PRACY**.
7. Wybierz maksymalną liczbę hello urządzeń ma tooauthorize dla każdego użytkownika.

> [!NOTE]
> Rejestracja za pomocą usługi Microsoft Intune lub funkcji zarządzania urządzeniami przenośnymi dla usługi Office 365 wymaga dołączenia w miejscu pracy. Jeśli skonfigurowano którąś z tych usług, zaznaczona jest opcja wszystkie, i hello brak jest wyłączona.
> 
> 

Domyślnie uwierzytelnianie dwuskładnikowe nie jest włączone dla usługi hello. Jednak uwierzytelnianie dwuskładnikowe jest zalecane podczas rejestrowania urządzenia.

* Przed wymaganiem uwierzytelniania dwuskładnikowego dla tej usługi, należy skonfigurować dostawcę uwierzytelniania dwuskładnikowego w usłudze Azure Active Directory i skonfigurować konta użytkowników usługi Multi-Factor Authentication, zobacz [Dodawanie wieloskładnikowego TooAzure uwierzytelniania usługi Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Jeśli korzystasz z usług AD FS w systemie Windows Server 2012 R2, należy skonfigurować moduł uwierzytelniania dwuskładnikowego w usługach AD FS — zobacz [Using Multi-Factor Authentication with Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md) (Używanie usługi Multi-Factor Authentication w usługach Active Directory Federation Services).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Konfigurowanie odnajdywania usługi rejestracji urządzeń w usłudze Azure Active Directory
Urządzenia z systemem Windows 7 i Windows 8.1 odnajdzie usługi rejestracji urządzeń hello łącząc hello nazwę konta użytkownika z nazwą serwera rejestracji dobrze znanych urządzeń.

Należy utworzyć rekord CNAME w systemie DNS wskazujący rekord toohello A skojarzony z usługą rejestracji urządzeń usługi Azure Active Directory. Hello rekord CNAME musi używać hello dobrze znanego prefiksu enterpriseregistration następuje hello sufiks nazwy UPN używanego przez hello kont użytkowników w organizacji. Jeśli organizacja używa wielu sufiksów nazw UPN, należy utworzyć wiele rekordów CNAME w systemie DNS.

Na przykład, jeśli używasz dwa sufiksy nazw UPN w danej organizacji o nazwie @contoso.com i @region.contoso.com, utworzysz następujące rekordy DNS hello.

| Wpis | Typ | Adres |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Wyświetlanie obiektów urządzeń i zarządzanie nimi w usłudze Azure Active Directory
1. Z portalu administratora platformy Azure hello można wyświetlać, blokować i odblokowywać urządzenia. Urządzenie jest zablokowane przestaną być tooapplications dostępu, które są skonfigurowane tooallow tylko zarejestrowane urządzenia.
2. Zaloguj się na toohello portalu Microsoft Azure jako Administrator.
3. W okienku po lewej stronie powitania wybierz **usługi Active Directory**.
4. Wybierz swój katalog.
5. Wybierz hello **użytkowników** kartę. Następnie wybierz tooview użytkownika urządzeń
6. Wybierz hello **urządzeń** kartę.
7. Wybierz **zarejestrowane urządzenia** z hello menu rozwijanym.
8. W tym miejscu można wyświetlić, zablokować lub odblokować zarejestrowane urządzenia użytkowników hello.

## <a name="additional-topics"></a>Tematy dodatkowe
Za pomocą rejestracji urządzeń w usłudze Azure Active Directory można rejestrować urządzenia z systemem Windows 7 i Windows 8.1 przyłączone do domeny. następujące tematy Hello zawiera więcej informacji na temat wymagań wstępnych hello i usługi rejestracji urządzeń tooconfigure wymagane kroki hello na urządzeniach z systemem Windows 7 i Windows 8.1.

* [Automatic device registration with Azure Active Directory for Windows Domain-Joined Devices (Automatyczna rejestracja w usłudze Azure Active Directory urządzeń przyłączonych do domeny systemu Windows)](active-directory-conditional-access-automatic-device-registration.md)
* [Automatic device registration with Azure Active Directory for Windows 10 domain-joined devices (Automatyczna rejestracja w usłudze Azure Active Directory urządzeń z systemem Windows 10 przyłączonych do domeny)](active-directory-azureadjoin-devices-group-policy.md)

