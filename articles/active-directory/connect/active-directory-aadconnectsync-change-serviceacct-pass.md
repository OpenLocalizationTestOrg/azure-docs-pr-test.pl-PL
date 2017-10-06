---
title: "Synchronizacja programu Azure AD Connect: Zmiana konta usługi synchronizacji połączyć hello Azure AD | Dokumentacja firmy Microsoft"
description: "W tym dokumencie tematu opisano hello klucza szyfrowania i jak tooabandon po hello hasło jest zmienione."
services: active-directory
keywords: "Konto usługi synchronizacji programu Azure AD, hasło"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Zmiana hasła konta usługi synchronizacji Azure AD Connect hello
Jeśli zmienisz hasło konta usługi synchronizacji Azure AD Connect hello hello usługi synchronizacji nie będą mogli start poprawnie dopiero po porzucone hello klucza szyfrowania i ponownie zainicjować hasło konta usługi synchronizacji Azure AD Connect hello. 

Azure AD Connect, jako część usługi synchronizacji hello używa szyfrowania klucza toostore hello hasła hello usług AD DS i konta usługi Azure AD.  Konta te są szyfrowane przed są przechowywane w bazie danych hello. 

Witaj klucz szyfrowania używany jest zabezpieczone przy użyciu [ochrony danych systemu Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI chroni hello klucza szyfrowania za pomocą hello **hasło konta usługi synchronizacji programu hello Azure AD Connect**. 

Jeśli potrzebujesz hasło konta usługi hello toochange można użyć procedury hello [klucza szyfrowania programu Abandoning hello Azure AD Connect synchronizacji](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish to.  Te procedury należy również Jeśli potrzebujesz klucza szyfrowania hello tooabandon różnych przyczyn.

##<a name="issues-that-arise-from-changing-hello-password"></a>Problemy, które wynikają z zmiany hasła hello
Istnieją dwie czynności wymagające toobe wykonane po zmianie hello hasło do konta usługi.

Najpierw należy toochange hello hasło w obszarze hello Menedżera sterowania usługami systemu Windows.  Dopóki ten problem zostanie rozwiązany, zostaną wyświetlone następujące błędy:


- Jeśli spróbujesz hello toostart usługi synchronizacji w Menedżera sterowania usługami systemu Windows o błędzie hello "**systemu Windows nie można uruchomić usługi Microsoft Azure AD Sync hello na komputerze lokalnym**". **Błąd 1069: hello usługa nie została uruchomiona ze względu na błąd logowania tooa.** "
- W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń systemowych hello zawiera błąd **7038 identyfikator zdarzenia** i wiadomości "**hello usługi ADSync nie są toolog tak jak w przypadku hello obecnie skonfigurowane hasło powodu toohello następujących błędów: Witaj, nazwa użytkownika lub hasło jest niepoprawne.** "

Po drugie określonych warunkach, jeśli hasło hello jest aktualizowany, hello usługi synchronizacji można już pobierać hello klucz szyfrowania za pośrednictwem DPAPI. Bez klucza szyfrowania hello powitalne Usługa synchronizacji nie można odszyfrować toosynchronize hello hasła wymagane do i z lokalnej usługi AD i Azure AD.
Zostaną wyświetlone błędy takie jak:

- W obszarze Menedżer sterowania usługami systemu Windows Jeśli spróbuj hello toostart usługi synchronizacji i nie może pobrać klucza szyfrowania hello go zakończy się niepowodzeniem z powodu błędu "** Windows hello Microsoft Azure AD Sync nie można uruchomić na komputerze lokalnym. Aby uzyskać więcej informacji przejrzyj dziennik zdarzeń systemowych hello. Jeśli jest to usługa firmy Microsoft, skontaktuj się z dostawcą usługi hello i odwołuje się kod błędu tooservice **-21451857952 ***. "
- W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń aplikacji hello zawiera błąd **6028 identyfikator zdarzenia** i komunikat o błędzie *"**nie można uzyskać dostępu do klucza szyfrowania serwera hello.* *"*

tooensure nie otrzymasz tych błędów, postępuj zgodnie z procedurami hello w [klucza szyfrowania programu Abandoning hello Azure AD Connect synchronizacji](#abandoning-the-azure-ad-connect-sync-encryption-key) podczas zmiany hasła hello.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Porzucanie klucza szyfrowania hello synchronizacji Azure AD Connect
>[!IMPORTANT]
>Witaj następujące procedury mają zastosowanie tylko tooAzure AD Connect kompilacji 1.1.443.0 lub starszy.

Użyj powitania po klucz szyfrowania hello tooabandon procedury.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Jakie toodo, aby uzyskać klucz szyfrowania hello tooabandon

Klucz szyfrowania hello tooabandon, należy użyć powitania po tooaccomplish procedury.

1. [Porzuć hello istniejącego klucza szyfrowania](#abandon-the-existing-encryption-key)

2. [Podaj hasło hello hello konta usług AD DS](#provide-the-password-of-the-ad-ds-account)

3. [Zainicjuj ponownie hasło hello hello konta synchronizacji usługi Azure AD](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Uruchom hello usługi synchronizacji](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Porzuć hello istniejącego klucza szyfrowania
Porzuć hello istniejącego klucza szyfrowania, więc można utworzyć tego nowego klucza szyfrowania:

1. Zaloguj się za tooyour Azure AD Connect serwera jako administrator.

2. Rozpocznij nową sesję programu PowerShell.

3. Przejdź toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Uruchom polecenie hello:`./miiskmu.exe /a`

![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Podaj hasło hello hello konta usług AD DS
Jak już istniejące hasła hello przechowywany w bazie danych hello mogły być odszyfrowane, należy tooprovide hello usługi synchronizacji z hello hasło konta hello usług AD DS. Witaj usługi synchronizacji szyfruje hello hasła przy użyciu nowego klucza szyfrowania hello:

1. Uruchom hello Synchronization Service Manager (START → usługa synchronizacji).
</br>![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Przejdź toohello **łączniki** kartę.
3. Wybierz hello **łącznika AD** , który odpowiada tooyour lokalnej usłudze AD. Jeśli masz więcej niż jeden łącznik AD, powtórz hello następujące kroki dla każdego z nich.
4. W obszarze **akcje**, wybierz pozycję **właściwości**.
5. W wyskakującym oknie dialogowym hello, wybierz **Connect lesie katalogu tooActive**:
6. Wprowadź hasło hello konta hello usług AD DS w hello **hasło** pola tekstowego. Jeśli nie znasz swojego hasła, należy ustawić tooa znane wartości przed wykonaniem tej czynności.
7. Kliknij przycisk **OK** toosave hello nowe hasło i zamknij hello podręczne okno dialogowe.
![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Zainicjuj ponownie hasło hello hello konta synchronizacji usługi Azure AD
Nie można bezpośrednio podać hasło hello hello Azure AD service konta toohello usługi synchronizacji. Zamiast tego należy polecenia cmdlet hello toouse **ADSyncAADServiceAccount Dodaj** hello tooreinitialize konta usługi Azure AD. polecenia cmdlet Hello resetuje hasło konta hello i ułatwia toohello dostępne usługi synchronizacji:

1. Rozpocznij nową sesję programu PowerShell na powitania serwera Azure AD Connect.
2. Uruchom polecenie cmdlet `Add-ADSyncAADServiceAccount`.
3. W wyskakującym oknie dialogowym hello Podaj poświadczenia administratora globalnego hello Azure AD dla dzierżawy usługi Azure AD.
![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Jeśli ten zakończy się powodzeniem, zostanie wyświetlony wiersz polecenia programu PowerShell hello.

#### <a name="start-hello-synchronization-service"></a>Uruchom hello usługi synchronizacji
Klucz szyfrowania toohello dostępu ma hello usługi synchronizacji i wszystkie hello haseł musi, można ponownie uruchomić usługę hello w hello Menedżera sterowania usługami systemu Windows:


1. Przejdź tooWindows Menedżera sterowania usługami (usługi → START).
2. Wybierz **Microsoft Azure AD Sync** i kliknij przycisk Uruchom ponownie.

## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)

* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
