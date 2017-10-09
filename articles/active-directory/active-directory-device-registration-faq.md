---
title: "aaaAzure usługi Active Directory automatycznej rejestracji urządzeń — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Automatycznej rejestracji urządzeń z usługi Azure Active Directory — często zadawane pytania."
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
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a>Często zadawane pytania dotyczące automatycznej rejestracji urządzeń w usłudze Azure Active Directory

**Pytanie: czy mogę ostatnio zarejestrowany hello urządzenia. Dlaczego nie widzę hello urządzenia w obszarze Moje informacje użytkownika w portalu Azure hello?**

**Odpowiedź:** urządzeń z systemem Windows 10, które są przyłączone do domeny z automatycznej rejestracji urządzeń nie są wyświetlane w obszarze hello informacje o użytkowniku.
Należy toouse PowerShell toosee wszystkie urządzenia. 

Tylko hello następujące urządzenia są wyświetlane w obszarze informacje o użytkowniku hello:

- Wszystkich urządzeń osobistych, które nie są przyłączone do przedsiębiorstwa 
- Wszystkie z systemem innym niż Windows 10 / Windows Server 2016 
- Wszystkie urządzenia z systemem innym niż Windows 

---

**Pytanie: Dlaczego nie można wyświetlić wszystkie urządzenia hello zarejestrowane w usłudze Azure Active Directory w portalu Azure hello?** 

**Odpowiedź:** nie istnieje aktualnie nie toosee sposób wszystkich zarejestrowanych urządzeń w hello portalu Azure. Można użyć programu Azure PowerShell toofind wszystkie urządzenia. Aby uzyskać więcej informacji, zobacz hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) polecenia cmdlet.

--- 

**Pytanie: jak sprawdzić, jakie stan rejestracji urządzenia hello powitania klienta jest?**

**Odpowiedź:** zależy od stanu rejestracji urządzenia hello:

- Jakie urządzenia hello jest
- Jak został zarejestrowany 
- Szczegółowe informacje dotyczące tooit. 
 

---

**Pytanie: Dlaczego jest to urządzenie I usunięto w hello Azure portalu lub przy użyciu programu Windows PowerShell nadal wymieniony jako zarejestrowane?**

**Odpowiedź:** to jest celowe. Witaj urządzenie nie będzie miał tooresources dostęp w chmurze hello. Jeśli mają tooremove hello urządzenia i zarejestrować go ponownie, akcji ręcznej musi być toobe wykonywaną na urządzeniu hello. 

Dla systemu Windows 10 i Windows Server 2016, które są lokalne AD przyłączonych do domeny:

1.  Witaj Otwórz wiersz polecenia jako administrator.

2.  Typ`dsregcmd.exe /debug /leave`

3.  Wyloguj się i zaloguj się tootrigger hello zaplanowane zadanie, które rejestruje urządzenie hello ponownie. 

Dla innych platform systemu Windows, które znajdują się na obszarze AD przyłączonych do domeny:

1.  Witaj Otwórz wiersz polecenia jako administrator.
2.  Wpisz polecenie `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.  Wpisz polecenie `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**Pytanie: Dlaczego Zobacz urządzenia zduplikowanych wpisów w portalu Azure?**

**ODP.:**

-   Dla systemu Windows 10 i Windows Server 2016, jeśli są toounjoin kolejnych nieudanych prób i ponownie Dołącz hello tego samego urządzenia, może być w niej zduplikowanych pozycji. 

-   Jeśli używasz konta Dodaj firmowego lub szkolnego każdego użytkownika systemu windows, który używa konta Dodaj firmowego lub szkolnego utworzy nowy rekord urządzenia hello tę samą nazwę urządzenia.

-   Inne platformy systemu Windows, które znajdują się na obszarze AD przyłączonych do domeny za pomocą automatycznej rejestracji utworzy nowy rekord urządzenia z hello tę samą nazwę urządzenia dla każdego użytkownika domeny, który loguje się do hello urządzenia. 

-   AADJ maszynę, która została wyczyszczona, ponowna instalacja i ponownie połączony z hello takie same nazwy, będzie wyświetlany jako inny rekord z hello tę samą nazwę urządzenia.

---

**Pytanie: Dlaczego użytkownik nadal dostęp do zasobów z urządzenia I zostały wyłączone w portalu Azure hello?**

**Odpowiedź:** może potrwać godzinę tooan toobe odwołania, stosowane.

>[!Note] 
>Utracone urządzeń zaleca się czyszczenie hello urządzenia tooensure, że użytkownicy nie mają dostępu hello urządzenia. Aby uzyskać więcej informacji, zobacz [rejestrowanie urządzeń do zarządzania w usłudze Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**Pytanie: Dlaczego Moi użytkownicy widzą "Nie można pobrać istnieje w tym miejscu"?**

**Odpowiedź:** hello urządzenie nie spełnia kryteriów hello skonfigurowano niektórych toorequire zasady dostępu warunkowego stanu określonego urządzenia, użytkownicy są blokowane, a ten komunikat zostanie wyświetlony. Sprawdź oszacowanie reguł hello i upewnij się, czy urządzenie hello jest możliwe toomeet hello kryteria tooavoid tego komunikatu.

---


**Pytanie: Zobacz hello rekordem urządzenia w obszarze hello informacje o użytkowniku w portalu Azure hello i widoczny stan hello zarejestrowany na powitania klienta. Czy prawidłowo skonfigurować do korzystania z dostępu warunkowego?**

**Odpowiedź:** hello rekord urządzenia (deviceID) i stan na powitania portalu Azure musi odpowiada powitania klienta i spełniać wszystkie kryteria oceny dostępu warunkowego. Aby uzyskać więcej informacji, zobacz [wprowadzenie do rejestracji urządzeń usługi Azure Active Directory](active-directory-device-registration.md).

---

**Pytanie: Dlaczego jest wyświetlany jest komunikat "Nazwa użytkownika lub hasło jest niepoprawne" urządzenia I po prostu dołączeniu tooAzure AD?**

**Odpowiedź:** są typowe przyczyny tego scenariusza:

- Poświadczenia użytkownika nie są już prawidłowe.

- Ten komputer jest toocommunicate w usłudze Azure Active Directory. Sprawdź, czy wszystkie problemy z połączeniem sieciowym.

- Hello Azure AD Join wymagania wstępne nie zostały spełnione. Upewnij się, że zostały wykonane kroki hello [rozszerzanie możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join chmury](active-directory-azureadjoin-overview.md).  

- Logowania federacyjnego wymaga programu toosupport serwera federacyjnego aktywny punkt końcowy protokołu WS-Trust. 

---

**Pytanie: Dlaczego Zobacz hello "Oops... Wystąpił błąd!" okna dialogowego podczas próby dołączenia komputera?**

**Odpowiedź:** jest to wynik konfigurowania rejestracji usługi Azure Active Directory z usługą Intune. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zarządzania urządzeniami z systemem Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**Pytanie: Dlaczego moja toojoin próba komputer się nie powieść, mimo że uzyskane informacje o błędzie?**

**Odpowiedź:** prawdopodobną przyczyną jest hello jest on zalogowany w toohello urządzenia przy użyciu hello wbudowanego konta administratora. Przed rozpoczęciem korzystania z usługi Azure Active Directory Join toocomplete hello Instalator, Utwórz innego konta lokalnego. 

---

**Pytanie: gdzie można znaleźć instrukcje instalacji hello automatycznej rejestracji urządzeń?**

**A:** szczegółowe instrukcje, zobacz [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**Pytanie: gdzie mogę znaleźć, rozwiązywanie problemów z informacji o hello automatycznej rejestracji urządzeń?**

**Odpowiedź:** informacje dotyczące rozwiązywania problemów, zobacz:

- [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD dla klientów niższego poziomu z systemem Windows](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

