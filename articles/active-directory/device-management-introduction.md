---
title: "aaaIntroduction toodevice zarządzania w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzanie urządzeniami może pomóc tooget kontrola nad urządzeniami hello, które uzyskują dostęp do zasobów w danym środowisku."
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Wprowadzenie toodevice zarządzania w usłudze Azure Active Directory

W świecie pierwszy mobile, najpierw chmury Azure Active Directory (Azure AD) umożliwia toodevices rejestracji jednokrotnej, aplikacji i usług z dowolnego miejsca. Z hello mnożenie urządzeń — łącznie z urządzenia (PRZYNIEŚ własne) specjalistów IT muszą stawiać czoła dwóch celów przeciwna:

- Zwiększenie możliwości dostępnych dla toobe użytkownicy końcowi hello produktywności wszędzie tam, gdzie i po każdej zmianie
- Ochrona zasobów firmowych hello w dowolnym momencie

Za pomocą urządzeń użytkownicy są uzyskiwania dostępu tooyour zasobów firmowych. tooprotect z zasobami firmy jako IT administrator chcesz toohave kontrolę nad tymi urządzeniami. Dzięki temu toomake się upewnić, że użytkownicy uzyskują dostęp do zasobów z urządzeń, które spełniają standardy zabezpieczeń i zgodności. 

Zarządzanie urządzeniami jest również podstawą hello [dostępu warunkowego opartego na urządzeniu](active-directory-conditional-access-policy-connected-applications.md). Przy użyciu dostępu warunkowego opartego na urządzeniach można zapewnić, że dostępu tooresources w danym środowisku jest możliwe za pomocą tylko zaufane urządzenia.   

W tym temacie wyjaśniono, jak działa zarządzanie urządzeniami w usłudze Azure Active Directory.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Pobieranie urządzeń pod kontrolą hello usługi Azure AD

tooget urządzenie pod kontrolą hello usługi Azure AD, dostępne są dwie opcje:

- Rejestrowanie 
- Łączenie

**Rejestrowanie** tooAzure urządzenia AD umożliwia możesz toomanage tożsamości urządzenia. Po zarejestrowaniu urządzenia rejestracji urządzeń usługi Azure AD zapewnia hello urządzenia przy użyciu tożsamości, która jest używana tooauthenticate hello urządzenia, gdy tooAzure loguje użytkownika AD. Można użyć tooenable tożsamości hello lub wyłącz urządzenie.

W połączeniu z rozwiązaniem management(MDM) urządzeń przenośnych, takich jak Microsoft Intune, dodatkowe informacje o urządzeniu hello są aktualizowane hello atrybutów urządzenia w usłudze Azure AD. Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności. Aby uzyskać więcej informacji dotyczących rejestrowania urządzeń w Microsoft Intune Zobacz rejestrowanie urządzeń do zarządzania w usłudze Intune.

**Sprzęganie** urządzenie jest tooregistering rozszerzenia urządzenia. Oznacza to, zapewnia ona wszystkich funkcji hello rejestrowania urządzenia i w dodatku toothis, również zmiany stanu lokalne powitania urządzenia. Zmiana stanu lokalne powitania umożliwia urządzenie toosign w tooa użytkowników przy użyciu organizacji konta firmowego lub szkolnego, zamiast konta osobistego.

## <a name="azure-ad-registered-devices"></a>Urządzenia zarejestrowane usługi Azure AD   

Witaj celem urządzeń usługi Azure AD w zarejestrowany jest tooprovide o obsługę hello **urządzenia (PRZYNIEŚ własne)** scenariusza. W tym scenariuszu użytkownik mógł korzystać z zasobów usługi Azure Active Directory pod kontrolą firmy za pomocą urządzeń osobistych.  

![Urządzenia zarejestrowane usługi Azure AD](./media/device-management-introduction/03.png)

Witaj dostępu jest oparty na konta firmowego lub szkolnego, który został wprowadzony na urządzeniu hello.  
Na przykład systemu Windows 10 umożliwia tooadd użytkownikom pracy lub komputerów osobistych tooa konto służbowe, tabletu lub telefonu.  
Gdy użytkownik został dodany pracy lub konta służbowego, urządzenia hello jest zarejestrowana w usłudze Azure AD i opcjonalnie zarejestrowane w systemie zarządzania urządzeniami Przenośnymi na urządzenie przenośne hello, skonfigurowanego w Twojej organizacji. Użytkowników w organizacji można dodać służbowego lub szkolnego konta tooa osobiste urządzenie wygodny sposób:

- Podczas uzyskiwania dostępu do aplikacji pracy dla powitania po raz pierwszy
- Ręcznie za pośrednictwem hello **ustawienia** menu w przypadku hello systemu Windows 10 

Możesz skonfigurować urządzenia usługi Azure AD w zarejestrowany dla systemu Windows 10, iOS, Android i macOS.

## <a name="azure-ad-joined-devices"></a>Urządzeniach przyłączonych do usługi Azure AD

Celem Hello urządzeń usługi Azure AD przyłączony jest toosimplify:

- Wdrażanie systemu Windows urządzenia należące do pracy 
- Dostęp tooorganizational aplikacje i zasoby na dowolnym urządzeniu z systemem Windows

![Urządzenia zarejestrowane usługi Azure AD](./media/device-management-introduction/02.png)


Te cele są osiągane przez zapewnienie użytkownikom przy użyciu środowiska samoobsługi dla pobierania urządzenia należące do pracy pod kontrolą hello usługi Azure AD.  
**Azure AD Join** jest przeznaczona dla organizacji, które są najpierw chmury / tylko w chmurze. Są to zazwyczaj małych i średnich firm, które nie mają infrastruktury lokalnej usługi Active Directory systemu Windows Server. 

Wdrażanie usługi Azure AD przyłączone do urządzeń zawiera hello następujące korzyści:

- **Single-Sign-On rejestracji jednokrotnej (SSO)** tooyour Azure zarządzanych usług i aplikacji SaaS. Użytkownicy nie zobaczą monity o dodatkowe uwierzytelnianie podczas uzyskiwania dostępu do zasobów roboczych. Hello funkcji rejestracji Jednokrotnej jest parzysta, gdy nie są one dostępnych sieci połączonych toohello domeny.

- **Roaming zgodne Enterprise** ustawień użytkownika na urządzeniach połączonych. Użytkownicy nie muszą tooconnect toosee ustawienia konta (na przykład usługi Hotmail) firmy Microsoft na urządzeniach.

- **Dostęp tooWindows sklepu dla firm** przy użyciu konta usługi AD. Użytkownicy, można wybrać ze spisu aplikacji wstępnie wybrany przez organizację hello.

- **Usługi Windows Hello** obsługę dostęp do bezpiecznego i wygodne toowork zasobów.

- **Ograniczenie dostępu** tooapps z tylko w przypadku urządzeń, które spełniają zasady zgodności.

Podczas usługi Azure AD join jest przeznaczone głównie dla organizacji, które nie mają infrastruktury lokalnej usługi Active Directory systemu Windows Server, można wykonywać następujące czynności na pewno również korzystać w scenariuszach, w których:

- Przyłączanie do domeny lokalnej nie można użyć na przykład, jeśli potrzebujesz tooget urządzeń przenośnych, takich jak tablety i telefony pod kontrolą.

- Użytkownicy potrzebują głównie tooaccess usługi Office 365 lub innych aplikacji SaaS zintegrowanych z usługą Azure AD.

- Ma toomanage grupy użytkowników w usłudze Azure AD, a nie w usłudze Active Directory. Może to dotyczyć, na przykład tooseasonal pracownicy, wykonawcy lub studentów.

- Ma tooprovide łącząca tooworkers możliwości w biurach oddziałów zdalnego z infrastruktury lokalnej ograniczone.

Możesz skonfigurować urządzenia usługi Azure AD połączone dla urządzeń z systemem Windows 10.


## <a name="hybrid-azure-ad-joined-devices"></a>Urządzeniach przyłączonych do hybrydowej usługi Azure AD

Przez ponad dekadę w wielu organizacjach używanych hello domeny sprzężenia tootheir lokalnej usługi Active Directory tooenable:

- IT działów toomanage pracy urządzeń należących do firmy z centralnej lokalizacji.

- Toosign użytkowników na urządzeniach tootheir z ich Active Directory służbowe kont. 

Zazwyczaj organizacji mających wpływ na lokalnym zależne od metod tooprovision urządzenia do obrazowania, a często używane **programu System Center Configuration Manager (SCCM)** lub **(GP) zasad grupy** toomanage je.

Jeśli środowisko ma lokalnego wpływ AD, a także korzyści z hello możliwości oferowane przez usługi Azure Active Directory, można zaimplementować hybrydowe usługi Azure AD przyłączone do urządzeń. Są to urządzenia, które są, tooyour dołączonego do lokalnej usługi Active Directory i Azure Active Directory.

![Urządzenia zarejestrowane usługi Azure AD](./media/device-management-introduction/01.png)


Należy używać urządzeń hybrydowego przyłączonych do usługi Azure AD, jeśli:

- Urządzeń toothese wdrożonej aplikacji Win32, korzystających z protokołu NTLM / Kerberos.

- Wymagaj zasad grupy lub SCCM / DCM toomanage urządzeń.

- Chcesz toocontinue toouse obrazowania rozwiązań tooconfigure urządzenia dla pracowników.

Można skonfigurować hybrydowe usługi Azure AD urządzeniach przyłączonych do systemu Windows 10 i urządzeniach niskiego poziomu, takich jak Windows 8 i Windows 7.

## <a name="summary"></a>Podsumowanie

Zarządzanie urządzeniami w usłudze Azure AD możesz: 

- Uprościć proces hello zapewniania urządzeń pod kontrolą hello usługi Azure AD

- Zapewnić użytkownikom łatwe toouse dostępu tooyour organizacji zasobów w chmurze

Zgodnie z zasadą thumb należy użyć:

- Usługi Azure AD zarejestrowane urządzenia dla urządzeń osobistych

- Przyłączone urządzeń do usługi Azure AD dla urządzeń, które nie są przyłączone do tooan lokalnej usłudze AD 

- Hybrydowe usługi Azure AD przyłączone urządzeń dla urządzeń, które są przyłączone do tooan lokalnej usłudze AD     




## <a name="next-steps"></a>Następne kroki

- tooget jak urządzenie toomanage hello Azure portalu, zobacz Omówienie [zarządzanie urządzeniami za pomocą hello portalu Azure](device-management-azure-portal.md)

- toolearn więcej informacji na temat dostępu warunkowego opartego na urządzeniu, zobacz [Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

- toosetup hybrydowe usługi Azure AD przyłączone do urządzenia, zobacz [jak tooconfigure hybrydowe usługi Azure Active Directory łączone urządzeń](device-management-hybrid-azuread-joined-devices-setup.md).


