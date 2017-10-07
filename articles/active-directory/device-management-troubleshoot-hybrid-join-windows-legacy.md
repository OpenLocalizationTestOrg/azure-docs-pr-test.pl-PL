---
title: "niższego poziomu urządzeniach przyłączonych do aaaTroubleshooting hybrydowe usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory połączone urządzenia niższego poziomu."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory przyłączone do urządzeń niskiego poziomu 

Ten temat jest stosowane tylko toohello następujące urządzenia: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Dla systemu Windows 10 lub Windows Server 2016, zobacz [hybrydowego Rozwiązywanie problemów z usługą Azure Active Directory przyłączone do urządzeń z systemem Windows 10 i Windows Server 2016](device-management-troubleshoot-hybrid-join-windows-current.md).

W tym temacie założono, że [urządzeniach przyłączonych do skonfigurowanego hybrydowe usługi Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport następujące scenariusze:

- Dostępu warunkowego opartego na urządzeniu

- [Enterprise roaming ustawień](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello dla firm](active-directory-azureadjoin-passport-deployment.md) 





Ten temat zawiera rozwiązania wskazówki dotyczące sposobu tooresolve potencjalne problemy.  

**Co należy wiedzieć:** 

- Witaj maksymalną liczbę urządzeń dla każdego użytkownika jest perspektywy skoncentrowanej na urządzeniach. Na przykład jeśli *jdoe* i *jharnett* urządzenia tooa logowania, rejestracji odrębnych (DeviceID) jest tworzony dla każdego z nich w hello **użytkownika** kartę informacje.  

- Witaj początkowe rejestracyjny / join urządzeń jest skonfigurowany tooperform próba logowania lub lock / odblokowania. Mogą wystąpić opóźnienia 5-minutowy wyzwalane przez zadania harmonogramu zadań. 

- Ponowna instalacja systemu operacyjnego hello lub ręcznego unregister i wykonaj ponowną rejestrację może utworzyć nowej rejestracji w usłudze Azure AD i powoduje wiele wpisów hello użytkownika informacje o karcie w hello portalu Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Krok 1: Pobierz hello stan rejestracji 

**Stan rejestracji hello tooverify:**  

1. Witaj Otwórz wiersz polecenia jako administrator 

2. Typ`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

To polecenie wyświetla okno dialogowe, która udostępnia szczegółowe informacje o stanie sprzężenia hello.

![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Krok 2: Ocena hello hybrydowe usługi Azure AD join stanu 

Jeśli hello hybrydowe usługi Azure AD join zakończyła się niepowodzeniem, okno dialogowe hello zawiera szczegółowe informacje o problemie hello, który wystąpił.

**najbardziej typowe problemy Hello są:**

- Nieprawidłowej konfiguracji usług AD FS lub Azure AD

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Użytkownik nie jest zarejestrowany jako użytkownik domeny

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Osiągnięto limit przydziału

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Usługa Hello nie odpowiada 

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Informacje o stanie hello również można znaleźć w dzienniku zdarzeń hello w obszarze **aplikacji i usług Log\Microsoft-dołączania**.
  
**Najczęstszymi przyczynami sprzężenia usługi Azure AD nie powiodło się hybrydowego Hello są:** 

- Twój komputer nie jest w sieci wewnętrznej hello organizacji lub sieci VPN bez tooan połączenia lokalnego kontrolera domeny AD.

- Użytkownik jest zalogowany tooyour komputera przy użyciu konta komputera lokalnego. 

- Problemy z konfiguracją usługi: 

  - Witaj serwer federacyjny został skonfigurowany toosupport **WIAORMULTIAUTHN**. 

  - Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello.

  - Użytkownik osiągnął limit hello urządzeń. 

## <a name="next-steps"></a>Następne kroki

Odpowiedzi na pytania, zobacz hello [zarządzanie urządzeniami — często zadawane pytania](device-management-faq.md)  
