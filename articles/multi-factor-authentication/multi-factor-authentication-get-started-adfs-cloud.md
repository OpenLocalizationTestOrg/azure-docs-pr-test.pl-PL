---
title: "aaaSecure zasobów w chmurze z usługą Azure MFA i usług AD FS | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA i usług AD FS w chmurze hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS
Jeśli Twoja organizacja jest Sfederowane przy użyciu usługi Azure Active Directory, należy użyć usługi Azure Multi-Factor Authentication lub zasobów toosecure Active Directory Federation Services (AD FS), które są udostępniane przez usługę Azure AD. Hello Użyj następujących procedur toosecure usługi Azure Active Directory zasobów przy użyciu usługi Azure Multi-Factor Authentication lub usług federacyjnych Active Directory.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Zabezpieczanie zasobów usługi Azure AD za pomocą usług AD FS
toosecure zasób chmury, ustaw reguły oświadczeń Active Directory Federation Services emituje hello multipleauthn oświadczenia, gdy użytkownik wykona pomyślnie weryfikacji dwuetapowej. Tego oświadczenia są przekazywane tooAzure AD. Wykonaj tej procedury toowalk hello kroki:


1. Otwórz przystawkę zarządzania usługami AD FS.
2. Po lewej stronie powitania, wybierz **zaufania jednostek uzależnionych**.
3. Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **przekazuj lub Filtruj oświadczenie przychodzące** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Nadaj regule nazwę. 
7. Wybierz **odwołania do metod uwierzytelniania** hello przychodzące typ oświadczenia.
8. Wybierz pozycję **Przekazuj wszystkie wartości oświadczeń**.
    ![Kreator dodawania reguły przekształcania dotyczącej oświadczeń](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Kliknij przycisk **Zakończ**. Zamknij konsolę zarządzania FS hello AD.

## <a name="trusted-ips-for-federated-users"></a>Zaufane adresy IP dla użytkowników federacyjnych
Listę zaufanych adresów IP pozwala administratorom tooby przebiegu weryfikacji dwuetapowej dla określonych adresów IP lub dla użytkowników federacyjnych, mających żądań wysyłanych z we własnej sieci intranet. Witaj poniższych sekcjach opisano sposób tooconfigure Azure Multi-Factor Authentication zaufanych adresów IP z użytkowników federacyjnych i obejście weryfikację dwuetapową, jeśli żądanie pochodzi z w intranecie użytkowników federacyjnych. Jest to osiągane przez skonfigurowanie usług AD FS toouse przekazującego lub filtr szablonem oświadczenia przychodzące z hello typ oświadczenia wewnątrz sieci firmowej.

W tym przykładzie użyto usługi Office 365 w celu pokazania obsługi relacji zaufania jednostek zależnych.

### <a name="configure-hello-ad-fs-claims-rules"></a>Konfigurowanie reguł oświadczeń hello usług AD FS
najpierw Hello potrzebujemy toodo jest tooconfigure oświadczeń hello usług AD FS. Utworzenie dwóch reguł oświadczeń, jeden dla hello wewnątrz sieci firmowej oświadczeń, typ i dodatkowe jeden aktualizowania użytkowników zalogowany.

1. Otwórz przystawkę zarządzania usługami AD FS.
2. Po lewej stronie powitania, wybierz **zaufania jednostek uzależnionych**.
3. Kliknij prawym przyciskiem myszy pozycję **Platforma tożsamości usługi Microsoft Office 365** i wybierz pozycję **Edytuj reguły oświadczeń...**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę.**
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **przekazuj lub Filtruj oświadczenie przychodzące** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. W hello pole dalej tooClaim Nazwa reguły Nadaj regule nazwę. np. WewnSiećFirm.
7. Z listy rozwijanej hello, tooIncoming dalej typ oświadczenia, wybierz **wewnątrz sieci firmowej**.
   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Kliknij przycisk **Finish** (Zakończ).
9. Na karcie Reguły przekształcania wystawiania kliknij pozycję **Dodaj regułę**.
10. Na hello przekształcenie Kreatorze dodawania reguły oświadczenia, wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej** z hello listy rozwijanej, a następnie kliknij przycisk **dalej**.
11. W obszarze Nazwa reguły oświadczeń hello: wprowadź *zachowania użytkowników podpisany w*.
12. W hello niestandardowe reguły wpisz:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Kliknij przycisk **Zakończ**.
14. Kliknij przycisk **Zastosuj**.
15. Kliknij przycisk **OK**.
16. Zamknij przystawkę zarządzania usługami AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Konfigurowanie zaufanych adresów IP usługi Azure Multi-Factor Authentication dla użytkowników federacyjnych
Teraz, oświadczenia hello znajdują się w miejscu, można skonfigurować listę zaufanych adresów IP.

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Powitania po lewej stronie, kliknij przycisk **usługi Active Directory**.
3. W katalogu wybierz katalog hello miejscu tooset zapasowej listę zaufanych adresów IP.
4. W katalogu wybrano hello, kliknij polecenie **Konfiguruj**.
5. W sekcji uwierzytelnianie wieloskładnikowe powitania kliknij **Zarządzaj ustawieniami usługi**.
6. Na stronie ustawień usługi hello w obszarze listę zaufanych adresów IP, wybierz **pominąć kilku-factor uwierzytelniania dla żądań od użytkowników federacyjnych w moim intranecie**.  

   ![Chmura](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Kliknij pozycję **Zapisz**.
8. Po zastosowaniu aktualizacji powitania kliknij **zamknąć**.

Gotowe. W tym momencie użytkowników federacyjnych usługi Office 365 powinien mieć tylko toouse MFA gdy oświadczenie pochodzi z poza hello firmowego intranetu.
