---
title: "Synchronizacja haseł aaaImplement z synchronizacji Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Zawiera informacje na temat sposobu działania synchronizacji haseł i w jaki sposób tooset w górę."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Implementowanie synchronizacji haseł z synchronizacji Azure AD Connect
Ten artykuł zawiera informacje dotyczące toosynchronize Twojego hasła użytkowników z lokalnej usługi Active Directory wystąpienia tooa oparte na chmurze usługi Azure Active Directory (Azure AD) wystąpienia.

## <a name="what-is-password-synchronization"></a>Co to jest synchronizacja haseł
Witaj prawdopodobieństwo czy jest blokowane pracę powodu tooa zapomniane hasło jest powiązany numer toohello różnych haseł należy tooremember. Witaj więcej haseł należy tooremember, hello wyższej hello prawdopodobieństwo tooforget jeden. Pytania i wywołania dotyczące resetowania hasła i inne żądanie problemy związane z hasłem hello najwięcej zasobów pomocy technicznej.

Synchronizacja haseł to funkcja używanych toosynchronize haseł użytkowników z lokalnej usługi Active Directory wystąpienia tooa oparte na chmurze usługi Azure AD wystąpienia.
Użyj tej funkcji toosign w tooAzure AD usług, takich jak usługi Office 365, Microsoft Intune CRM Online i Azure Active Directory Domain Services (Azure AD DS). Zaloguj się toohello usługi za pomocą hello tego samego hasła, użyj toosign w tooyour lokalne wystąpienie usługi Active Directory.

![Co to jest program Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

Dzięki zmniejszeniu liczby hello haseł, użytkownicy będą potrzebowali toojust toomaintain, jeden. Synchronizacja haseł ułatwia:

* Zwiększenie produktywności hello użytkowników.
* Obniżyć koszty pomocy technicznej.  

Ponadto jeśli zdecydujesz toouse [federacji z usługi Active Directory Federation Services (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), można opcjonalnie skonfigurować synchronizacji haseł jako zapasowy na wypadek awarii infrastruktury usług AD FS.

Synchronizacja haseł to funkcja synchronizacji katalogu toohello rozszerzenia implementowane przez synchronizacja programu Azure AD Connect. Synchronizacja haseł toouse w danym środowisku, należy:

* Instalowanie usługi Azure AD Connect.  
* Skonfigurować synchronizację katalogów między lokalnym wystąpieniem usługi Active Directory i wystąpienie usługi Azure Active Directory.
* Włączanie synchronizacji haseł.

Aby uzyskać więcej informacji, zobacz [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

> [!NOTE]
> Aby uzyskać więcej informacji na temat usługi Azure Active Directory Domain Services skonfigurowany dla FIPS i synchronizacja haseł, zobacz "synchronizacji haseł i FIPS" w dalszej części tego artykułu.
>
>

## <a name="how-password-synchronization-works"></a>Opis działania synchronizacji haseł
Witaj usług domenowych Active Directory przechowuje hasła w postaci hello reprezentacji wartość skrótu hasła użytkownika rzeczywiste hello. Wartość skrótu jest wynikiem jednokierunkowej funkcji matematycznych (hello *algorytmem wyznaczania wartości skrótu*). Nie ma żadnych wyników hello toorevert metody w wersji jednokierunkowa funkcja toohello zwykłego tekstu hasła. Nie można użyć toosign skrótu hasła tooyour sieci lokalnej.

toosynchronize, który hasła, synchronizacja programu Azure AD Connect wyodrębnia z skrót hasła z hello lokalnego wystąpienia usługi Active Directory. Zastosowano dodatkowe zabezpieczenia przetwarzania toohello skrót hasła, zanim zostanie zsynchronizowany Usługa uwierzytelniania usługi Azure Active Directory toohello. Hasła są synchronizowane na poszczególnych użytkowników i w kolejności chronologicznej.

Przepływ danych rzeczywistych Hello proces synchronizacji haseł hello jest podobne toohello synchronizacji danych użytkownika, takich jak DisplayName lub adresy E-mail. Jednak hasła są synchronizowane częściej niż okno synchronizacji katalogu standard hello innych atrybutów. proces synchronizacji haseł Hello jest uruchamiane co 2 minut. Nie można zmodyfikować częstotliwości hello tego procesu. Podczas synchronizowania hasła, zastępuje on istniejące hasło chmury hello.

Witaj pierwszym włączeniu funkcji synchronizacji haseł hello, wykonuje wstępnej synchronizacji haseł hello wszystkich użytkowników w zakresie. Nie można jawnie definiować podzbiór, które mają toosynchronize haseł użytkowników.

Jeśli zmienisz hasło lokalne powitania zaktualizować hasło jest zsynchronizowany, najczęściej w ciągu kilku minut.
Funkcja synchronizacji hasła Hello ma automatycznie ponawiać próby synchronizacji nie powiodło się. Jeśli wystąpi błąd podczas próby toosynchronize hasła, błąd jest rejestrowany w podglądu zdarzeń.

Witaj Synchronizacja hasła nie ma wpływu na powitania użytkownika, który jest aktualnie zalogowany.
Zmiany hasła zsynchronizowane, która występuje, gdy użytkownik jest zarejestrowany w usłudze w chmurze tooa nie występuje od razu w bieżącej sesji usługi chmury. Gdy usługa w chmurze hello wymaga tooauthenticate ponownie, jednak tooprovide nowego hasła.

Użytkownik musi wprowadzić poświadczenia firmowe drugi czasu tooauthenticate tooAzure AD, niezależnie od tego, czy jest zalogowany w sieci firmowej tootheir. Wzorzec te można zminimalizować, jednak jeśli hello użytkownik wybiera hello Keep mnie podpisany w pole wyboru (KMSI) podczas logowania. Wybranie tej opcji ustawia plik cookie sesji omija uwierzytelniania krótki okres. Zachowanie KMSI można włączona lub wyłączona przez administratora usługi Azure AD hello.

> [!NOTE]
> Synchronizacja haseł jest obsługiwana tylko dla hello obiektu Typ użytkownika w usłudze Active Directory. Nie jest obsługiwana dla typu obiektu iNetOrgPerson hello.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Szczegółowy opis działania synchronizacji haseł
niżej Hello przedstawiono szczegółowy opis działania synchronizacji haseł od usługi Active Directory i Azure AD.

![Przepływ szczegółowe hasła](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. Co dwie minuty hello agent synchronizacji haseł na serwerze Connect hello AD żądań skrótów haseł przechowywanych (atrybut unicodePwd hello) z kontrolera domeny za pomocą standardowych hello [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) toosynchronize danych używany przez protokół replikacji między kontrolerów domeny. Konto usługi Hello musi mieć replikować zmiany katalogu i replikować katalogu zmiany wszystkich AD skrótów haseł hello tooobtain uprawnienia (domyślnie na instalację).
2. Przed wysłaniem, hello DC szyfruje hello MD4 skrót hasła przy użyciu klucza, który jest [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) skrótu klucza sesji hello RPC i soli. Wysyła następnie agent synchronizacji haseł hello wynik toohello za pośrednictwem wywołania RPC. Witaj DC przekazuje także hello soli toohello synchronizacji agenta przy użyciu protokołu replikacji hello kontrolera domeny, więc agenta hello będą mogli toodecrypt hello koperty.
3.  Agent synchronizacji haseł powitania po koperty zaszyfrowanych hello używa [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) i hello soli toogenerate klucza toodecrypt hello Odebrano wstecz tooits oryginalnego MD4 format danych. W żadnym punkcie agent synchronizacji haseł hello mają dostęp toohello nieszyfrowanego hasła. Witaj agent synchronizacji haseł zastosowaniem MD5 jest ściśle zgodność z protokołem replikacji z hello kontrolera domeny i jest używana tylko na lokalne między hello kontrolera domeny i agent synchronizacji haseł hello.
4.  agent synchronizacji haseł Hello rozszerza bajtów too64 skrótu hasła binarne 16-bajtowych hello przez pierwszy konwertowania hello skrótu tooa 32-bajtowych ciąg szesnastkowy, a następnie konwertowania tego ciągu z powrotem do binarną, używając kodowania UTF-16.
5.  agent synchronizacji haseł Hello dodaje soli, składające się soli długość 10-bajtowych, toofurther binarne 64-bajtowych toohello chronić hello oryginalnego wyznaczania wartości skrótu.
6.  agent synchronizacji haseł Hello następnie łączy skrót hello MD4 plus soli i danych wejściowych go do hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) funkcji. 1000 iteracji hello [HMAC SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) kluczem algorytmu wyznaczania wartości skrótu jest używany. 
7.  agent synchronizacji haseł Hello przyjmuje hello wynikowy 32 bajtów skrótu, łączy zarówno soli hello hello liczba SHA256 tooit iteracji (na potrzeby używania przez usługę Azure AD), a następnie przesyła ciąg hello z usługi Azure AD Connect tooAzure AD przy użyciu protokołu SSL.</br> 
8.  Podczas prób toosign w tooAzure AD i wprowadza swoje hasło, hello hasło użytkownika, które jest uruchamiane za pomocą hello tego samego MD4 + ziarna + PBKDF2 + HMAC SHA256 procesu. Jeśli hello wynikowy skrót zgodny hello wyznaczania wartości skrótu, przechowywane w usłudze Azure AD, hello użytkownik wprowadził hello prawidłowe hasło i zostanie uwierzytelniony. 

>[!Note] 
>wyznaczania wartości skrótu MD4 oryginalnego Hello nie jest przesyłane tooAzure AD. Zamiast tego są przesyłane hello wyznaczania wartości skrótu MD4 oryginalnego hello skrót SHA256. W związku z tym Jeśli skrót hello przechowywane w usłudze Azure AD są uzyskiwane, nie można użyć w ataku pass--hash lokalnymi.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Opis działania synchronizacji haseł z usług domenowych Azure Active Directory
Umożliwia także toosynchronize funkcji synchronizacji haseł hello lokalnego hasła zbyt[Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md). W tym scenariuszu wystąpienia usługi Azure Active Directory Domain Services hello uwierzytelnia użytkowników w chmurze hello ze wszystkich metod hello dostępnych w lokalnym wystąpieniu usługi Active Directory. środowisko Hello tego scenariusza jest podobne hello toousing narzędzie migracji usługi Active Directory (ADMT) w środowisku lokalnym.

### <a name="security-considerations"></a>Zagadnienia związane z zabezpieczeniami
Podczas synchronizacji haseł hello zwykłego tekstu wersja hasła nie jest funkcja synchronizacji hasła narażonych toohello, tooAzure AD lub hello skojarzone usługi.

Uwierzytelnianie użytkownika ma miejsce przed usługi Azure AD, a nie na wystąpieniu usługi Active Directory w organizacji hello. Jeśli Twoja organizacja ma problemów dotyczących danych hasła w jakimkolwiek formularzu, pozostawiając hello lokalne, należy wziąć pod uwagę fakt hello tego hello SHA256 hasło danych przechowywanych w usłudze Azure AD — skrót hello oryginalnego skrótu MD4 — jest znacznie bezpieczniejsze niż co to jest przechowywane w usłudze Active Directory. Co więcej ponieważ nie można odszyfrować ten skrót SHA256, uniemożliwiający przywrócone środowiska usługi Active Directory w firmie toohello i widoczne jako prawidłowego użytkownika hasła w ataku typu pass--hash.





### <a name="password-policy-considerations"></a>Zagadnienia dotyczące zasad haseł
Istnieją dwa typy zasad haseł, których dotyczy Włączanie synchronizacji haseł:

* Zasady złożoności haseł
* Zasady wygasania haseł

#### <a name="password-complexity-policy"></a>Zasady złożoności haseł  
Po włączeniu synchronizacji haseł hello zasady złożoności haseł w lokalnym wystąpieniu usługi Active Directory zastępują zasady złożoności w chmurze hello zsynchronizowanych użytkowników. Możliwość używania wszystkich hello prawidłowy haseł z tooaccess wystąpienia usługi Azure AD z lokalnej usługi Active Directory.

> [!NOTE]
> Hasła użytkowników, które są tworzone bezpośrednio w chmurze hello są nadal podmiotu toopassword zasady zgodnie z definicją w chmurze hello.

#### <a name="password-expiration-policy"></a>Zasady wygasania haseł  
Jeśli użytkownik jest w zakresie hello synchronizacji haseł, hello chmury ustawione hasło konta jest zbyt*nigdy nie wygasa*.

Możesz kontynuować toosign tooyour usług w chmurze przy użyciu hasła zsynchronizowane, który wygasł w środowisku lokalnym. Hasło chmury jest aktualizowany hello następnym zmienić hasło hello w hello w środowisku lokalnym.

#### <a name="account-expiration"></a>Okres ważności konta
Jeśli organizacja używa atrybutu accountExpires hello jako część Zarządzanie kontami użytkowników, należy pamiętać, że ten atrybut nie jest zsynchronizowane tooAzure AD. W związku z tym wygasłe konto usługi Active Directory w środowisku skonfigurowana z synchronizacją hasła pozostaje aktywna w usłudze Azure AD. Zaleca się, że wygasł hello konta akcji przepływu pracy powinno spowodować skrypt PowerShell, który powoduje wyłączenie konta usługi Azure AD hello użytkownika. Z drugiej strony gdy konto hello jest włączona, wystąpienia usługi Azure AD hello powinna być włączona.

### <a name="overwrite-synchronized-passwords"></a>Zastąp synchronizowane hasła
Administrator może ręcznie zresetować hasło przy użyciu programu Windows PowerShell.

W takim przypadku nowe hasło hello zastępuje synchronizowane hasła, a wszystkie zasady haseł zdefiniowane w chmurze hello są stosowane toohello nowe hasło.

W przypadku zmiany hasła lokalne powitania nowe hasło jest zsynchronizowany chmury toohello i zastępuje on hello ręcznie zaktualizować hasło.

Witaj Synchronizacja hasła nie ma wpływu na hello Azure, użytkownik jest zalogowany. Zmiany hasła zsynchronizowane występujący po zarejestrowaniu w usłudze w chmurze tooa nie występuje od razu w bieżącej sesji usługi chmury. KMSI rozszerza hello czas trwania tej różnicy. Gdy usługa w chmurze hello wymaga tooauthenticate ponownie, należy tooprovide nowego hasła.

### <a name="additional-advantages"></a>Dodatkowe korzyści

- Ogólnie rzecz biorąc synchronizacja haseł jest łatwiejsze tooimplement niż usługi federacyjnej. Nie wymaga żadnych dodatkowych serwerów i eliminuje zależność od użytkowników tooauthenticate usługi federacyjnej wysokiej dostępności. 
- Synchronizację haseł można włączyć w taki sposób, w toofederation dodanie. Mogą być używane jako rezerwowe, jeśli usługi federacyjnej ulegnie awarii.












## <a name="enable-password-synchronization"></a>Włączanie synchronizacji haseł
Po zainstalowaniu usługi Azure AD Connect przy użyciu hello **ustawień ekspresowych** opcji synchronizacji haseł jest automatycznie włączone. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z usługi Azure AD Connect przy użyciu ustawień ekspresowych](active-directory-aadconnect-get-started-express.md).

Jeśli używasz ustawienia niestandardowe, po zainstalowaniu usługi Azure AD Connect, synchronizacja haseł jest dostępne na stronie logowania użytkownika hello. Aby uzyskać więcej informacji, zobacz [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

![Włączanie synchronizacji haseł](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Synchronizacja haseł i FIPS
Jeśli serwer został zablokowany zgodnie z tooFederal Information Processing (Standard FIPS), MD5 jest wyłączone.

**tooenable MD5, aby synchronizować hasła, wykonaj hello następujące kroki:**

1. Przejdź Sync\Bin too%programfiles%\Azure AD.
2. Otwórz miiserver.exe.config.
3. Przejdź węzła konfiguracji/runtime toohello na końcu hello hello pliku.
4. Dodaj hello następującego węzła:`<enforceFIPSPolicy enabled="false"/>`
5. Zapisz zmiany.

Odwołanie ta Wstawka kodu jest jak go powinna wyglądać:

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Aby uzyskać informacje o zabezpieczeniach i FIPS, zobacz [zgodności AAD Sync hasła, szyfrowania i FIPS](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).

## <a name="troubleshoot-password-synchronization"></a>Rozwiązywanie problemów z synchronizacją haseł
Jeśli masz problemy z synchronizacją haseł, zobacz [Rozwiązywanie problemów z synchronizacją hasła](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Następne kroki
* [Synchronizacja programu Azure AD Connect: Dostosowywanie opcji synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
