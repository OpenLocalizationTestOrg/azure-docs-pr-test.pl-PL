---
title: "aaaHow tooconfigure automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci tooregister urządzeń przyłączonych do domeny systemu Windows automatycznie i w trybie dyskretnym usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Wprowadzenie do rejestracja urządzeń w usłudze Azure Active Directory

Rejestracja urządzenia w usłudze Azure Active Directory jest hello foundation dla scenariuszy dostępu warunkowego opartego na urządzeniach. Po zarejestrowaniu urządzenia, rejestracja urządzeń w usłudze Azure Active Directory zapewnia hello urządzenia przy użyciu tożsamości, który jest używany tooauthenticate powitania po zalogowaniu użytkownika hello. urządzenie Hello uwierzytelniony i atrybuty hello hello urządzenia, można następnie tooenforce używane zasady dostępu warunkowego dla aplikacji, które znajdują się w chmurze hello i lokalnych.

W połączeniu z rozwiązaniem management(MDM) urządzeń przenośnych, takich jak Microsoft Intune, dodatkowe informacje o urządzeniu hello są aktualizowane hello atrybuty urządzenia w usłudze Azure Active Directory. Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności. Aby uzyskać więcej informacji dotyczących rejestrowania urządzeń w Microsoft Intune Zobacz rejestrowanie urządzeń do zarządzania w usłudze Intune.
Scenariusze obsługiwane przez rejestracji Azure Active Directory urządzenia rejestracji usługi Azure Active Directory urządzeń obejmuje obsługę systemu iOS, Android i Windows urządzeń. Witaj poszczególne scenariusze wykorzystujące usługę rejestracja urządzeń w usłudze Azure AD mogą mieć bardziej specyficzne wymagania i obsługę platform. 

Te scenariusze są następujące:

- **Dostęp warunkowy dla usługi Office 365 aplikacji w usłudze Microsoft Intune:** Administratorzy IT mogą aprowizować dostępu warunkowego urządzeń zasady toosecure zasobów firmowych, podczas gdy na powitania sam czas dzięki czemu pracownicy przetwarzający informacje na zgodnych urządzeniach tooaccess hello usługi. Aby uzyskać więcej informacji, zobacz zasady dostępu warunkowego urządzeń dla usług Office 365.

- **Tooapplications dostępu warunkowego, które są hostowane lokalnie:** zarejestrowane urządzenia można używać z zasadami dostępu dla aplikacji, które są skonfigurowane toouse usług AD FS w systemie Windows Server 2012 R2. Aby uzyskać więcej informacji na temat konfigurowania lokalnego dostępu warunkowego, zobacz [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md) (Konfigurowanie lokalnego dostępu warunkowego przy użyciu usługi rejestracji urządzeń w usłudze Azure Active Directory).

## <a name="setting-up-azure-active-directory-device-registration"></a>Konfigurowanie usługi Rejestracja urządzeń w usłudze Azure Active Directory

Rejestracja urządzenia toosetup, jest dostępnych kilka opcji:

- Kiedy rejestrować urządzenia przyłączone do tooAzure AD domeny. Aby uzyskać więcej informacji na ten temat możesz dodatkowe informacje na temat ustawień usługi Azure AD Join i hello wymaganych dla użytkowników domeny toojoin usługi Azure AD.

- Gdy użytkownicy dodawanie pracy lub szkoły kont tooWindows na osobistych urządzeniach lub tooa zasobów roboczych wymagają rejestracji łączenia urządzeń przenośnych można zarejestrować urządzenia. tooensure, musi włączyć rejestrowanie urządzeń w usłudze Azure AD w hello portalu Azure. 

- Można zarejestrować urządzenia za pomocą automatycznej rejestracji urządzeń dla tradycyjnych komputerów przyłączonych do domeny. tooensure, należy najpierw pierwszej instalacji programu Azure AD Connect, przed rozpoczęciem pracy z automatycznej rejestracji urządzeń.

Najnowsze instrukcje, zobacz [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).  
Można również przejrzeć i włączyć lub wyłączyć zarejestrowanych urządzeń w usłudze Azure Active Directory przy użyciu hello portalu administratora.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Włączanie usługi rejestracji urządzeń usługi Azure Active Directory hello

**Witaj tooenable usługi rejestracji urządzeń usługi Azure Active Directory:**

1.  Zaloguj się toohello portalu Microsoft Azure jako administrator.

2.  W okienku po lewej stronie powitania wybierz **usługi Active Directory**.

3.  Na karcie katalogu hello wybierz swój katalog.

4.  Kliknij pozycję **Konfiguruj**.

5.  Przewiń zbyt**urządzeń**.

6.  Wybierz wszystkie, aby użytkownicy mogą ZAREJESTROWAĆ swoje urządzenia w usłudze AZURE AD.

7.  Wybierz maksymalną liczbę hello urządzeń ma tooauthorize dla każdego użytkownika.

Rejestrowanie Hello usłudze Microsoft Intune lub zarządzania urządzeniami przenośnymi dla usługi Office 365 wymaga rejestracji urządzeń. Jeśli skonfigurowano którąś z tych usług **wszystkie** jest zaznaczone i **Brak** jest wyłączona. Upewnij się, że zostały prawidłowo skonfigurowane i ma hello odpowiednie licencjonowania.

Domyślnie uwierzytelnianie dwuskładnikowe nie jest włączone dla usługi hello. Jednak uwierzytelnianie dwuskładnikowe jest zalecane podczas rejestrowania urządzenia.

- Przed wymaganiem uwierzytelniania dwuskładnikowego dla tej usługi, należy skonfigurować dostawcę uwierzytelniania dwuskładnikowego w usłudze Azure Active Directory i skonfigurować konta użytkowników usługi Multi-Factor Authentication, zobacz Dodawanie usługi Multi-Factor Authentication tooAzure usługi Active Directory

- Jeśli korzystasz z usług AD FS w systemie Windows Server 2012 R2, należy skonfigurować moduł uwierzytelniania dwuskładnikowego w usługach AD FS, zobacz Używanie uwierzytelniania wieloskładnikowego z usługami federacyjnymi Active Directory.

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Wyświetlanie obiektów urządzeń i zarządzanie nimi w usłudze Azure Active Directory

Z portalu administratora platformy Azure hello można wyświetlać, blokować i odblokowywać urządzenia. Urządzenie jest zablokowane przestaną być tooapplications dostępu, które są skonfigurowane tooallow tylko zarejestrowane urządzenia.

**tooview obiektów urządzeń w usłudze Azure Active Directory i zarządzanie nimi:**
 
1.  Zaloguj się na toohello portalu Microsoft Azure jako administrator.

2.  W okienku po lewej stronie powitania wybierz **usługi Active Directory**.

3.  Wybierz swój katalog.

4.  Wybierz **użytkowników**. 

5.  Kliknij przycisk hello użytkownika, dla którego chcesz toosee hello urządzenia.

6.  Wybierz **urządzeń**.

7.  Wybierz **zarejestrowanych urządzeń**.

Teraz można przejrzeć, blokowania lub odblokować zarejestrowane urządzenia hello użytkownika.
Karcie hello użytkowników urządzeń z systemem Windows 10, które są lokalne przyłączonych do domeny i automatycznie zarejestrowane nie jest wyświetlana. Użyj toofind polecenia PowerShell Get-MsolDevice hello wszystkich urządzeń organizacji. 


## <a name="next-steps"></a>Następne kroki

toosetup automatycznego rejestracji urządzenia, zobacz [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).


