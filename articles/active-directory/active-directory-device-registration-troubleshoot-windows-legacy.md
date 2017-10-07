---
title: "komputery przyłączone aaaTroubleshooting hello automatyczną rejestrację domeny usługi Azure AD dla klientów niższego poziomu z systemem Windows | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z hello automatyczną rejestrację domeny usługi Azure AD komputerów przyłączonych do klientów niższego poziomu z systemem Windows."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD dla klientów niższego poziomu z systemem Windows 

Ten temat jest stosowane tylko toohello od klientów: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Dla systemu Windows 10 lub Windows Server 2016, zobacz [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

W tym temacie założono, że skonfigurowano automatyczną rejestrację urządzeń przyłączonych do domeny jako obramowane w opisanych w [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-device-registration-get-started.md).
 
Ten temat zawiera rozwiązania wskazówki dotyczące sposobu tooresolve potencjalne problemy.  
Niektóre elementy toonote dla pomyślnych wyników: 

- Rejestracja tych klientów w usłudze Azure AD jest na użytkownika/urządzenie. Na przykład: Jeśli jdoe i jharnett zalogować się w urządzeniu toothis, oddzielne rejestracji (DeviceID) jest tworzony dla każdego z tych użytkowników hello użytkownika informacje o karcie.  

- Rejestracja tych klientów fabrycznej hello jest skonfigurowany tootry podczas logowania lub Zablokuj/Odblokuj i mogą występować opóźnienia 5 minut, że jest to wyzwalane za pomocą zadania harmonogramu zadań. 

- Ponownie zainstaluj system operacyjny hello lub ręczne wyrejestrowanie i ponowne zarejestrowanie może utworzyć nowej rejestracji w usłudze Azure AD i spowoduje wiele wpisów hello użytkownika informacje o karcie w hello portalu Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Krok 1: Pobierz hello stan rejestracji 

**Stan rejestracji hello tooverify:**  

1. Witaj Otwórz wiersz polecenia jako administrator 

2. Typ`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

To polecenie wyświetla okno dialogowe, która udostępnia szczegółowe informacje o stanie sprzężenia hello.

![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Krok 2: Ocena hello stan rejestracji 

Jeśli sprzężenia hello zakończyła się niepowodzeniem, okno dialogowe hello zawiera szczegółowe informacje o problemie hello, który wystąpił.

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
  
**Najczęstszymi przyczynami niepowodzenia rejestracji Hello są:** 

- Twój komputer nie jest w sieci wewnętrznej hello organizacji lub sieci VPN bez tooan połączenia lokalnego kontrolera domeny AD.

- Użytkownik jest zalogowany tooyour komputera przy użyciu konta komputera lokalnego. 

- Problemy z konfiguracją usługi: 

  - Witaj serwer federacyjny został skonfigurowany toosupport **WIAORMULTIAUTHN**. 

  - Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello.

  - Użytkownik osiągnął limit hello urządzeń. Zobacz wprowadzenie do rejestracji urządzeń usługi Azure Active Directory.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz hello [automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md) 
