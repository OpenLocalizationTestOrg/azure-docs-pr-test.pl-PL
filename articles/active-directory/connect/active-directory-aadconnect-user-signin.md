---
title: "Usługi Azure AD Connect: Logowanie użytkownika | Dokumentacja firmy Microsoft"
description: "Azure AD Connect logowania użytkownika dla ustawień niestandardowych."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Azure AD Connect użytkownika opcje logowania
Połącz usługi Azure Active Directory (Azure AD) pozwala toosign Twojego użytkowników w chmurze tooboth i zasobów lokalnych za pomocą hello takich samych haseł. W tym artykule opisano podstawowe pojęcia dla każdego toohelp modelu tożsamości wybierz hello tożsamości, która ma być toouse logowanie tooAzure AD.

Jeśli znasz już modelu tożsamości usługi Azure AD hello i chcesz toolearn więcej informacji na temat określonej metody, zobacz hello odpowiednie łącze:

* [Synchronizacja haseł](#password-synchronization) z [logowanie jednokrotne (SSO)](active-directory-aadconnect-sso.md)
* [Przekazywanego uwierzytelniania](active-directory-aadconnect-pass-through-authentication.md)
* [Federacyjną rejestracją Jednokrotną (z usługi Active Directory Federation Services (AD FS))](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>Wybieranie metody logowania użytkownika hello w Twojej organizacji.
W przypadku większości organizacji, które właśnie tooenable użytkownika logowania tooOffice 365 aplikacji SaaS i innych zasobów platformy Azure na podstawie usługi AD zalecamy opcji synchronizacji haseł domyślnej hello. Niektóre organizacje, jednak nie są toouse możliwe przyczyny tej opcji. Wybiera on albo federacyjnych opcji logowania, takie jak usługi AD FS lub uwierzytelnianie przekazywane. Możesz użyć powitania po wybrać opcje hello toohelp tabeli.

Potrzebuję zbyt| PS z logowania jednokrotnego| PA z logowania jednokrotnego| USŁUGI AD FS |
 --- | --- | --- | --- |
Synchronizuj automatycznie nowe, skontaktuj się z pomocą, kont użytkowników i grup w lokalnej usłudze Active Directory toohello chmury.|x|x|x|
Skonfiguruj moje dzierżawy w scenariuszach hybrydowych usługi Office 365.|x|x|x|
Włącz Mój toosign użytkowników w i dostępu do usługi w chmurze przy użyciu swoich haseł lokalnych.|x|x|x|
Implementowanie logowania jednokrotnego przy użyciu poświadczeń firmowych.|x|x|x|
Upewnij się, że hasła nie są przechowywane w chmurze hello.||x *|x|
Włącz lokalnymi rozwiązaniami usługi Multi-Factor authentication.|||x|

* Za pośrednictwem lekkie łącznika.

>[!NOTE]
> Uwierzytelnianie przekazywane aktualnie ma pewne ograniczenia z klientów zaawansowanych. Zobacz [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) więcej szczegółów.

### <a name="password-synchronization"></a>Synchronizacja haseł
Synchronizacja haseł skrótów haseł użytkowników są synchronizowane z lokalnej usługi Active Directory tooAzure AD. Hasła są zmieniane lub zresetować lokalnymi, hello nowe hasła są synchronizowane tooAzure AD natychmiast, dzięki czemu użytkownicy mogą zawsze Użyj hello sam hasło dla zasobów w chmurze i zasobów lokalnych. Hello hasła nigdy nie są wysyłane tooAzure AD lub przechowywane w usłudze Azure AD w postaci zwykłego tekstu. Umożliwia synchronizację haseł wraz z hasłem tooenable zapisu samodzielnego resetowania haseł w usłudze Azure AD.

Ponadto można włączyć [logowania jednokrotnego](active-directory-aadconnect-sso.md) dla użytkowników na komputerach przyłączonych do domeny, znajdujących się w sieci firmowej hello. Pojedynczy logowania, włączone tylko dla użytkowników wymaga tooenter toohelp username, ich bezpiecznego dostępu do zasobów w chmurze.

![Synchronizacja haseł](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Aby uzyskać więcej informacji, zobacz hello [synchronizacji haseł](active-directory-aadconnectsync-implement-password-synchronization.md) artykułu.

### <a name="pass-through-authentication"></a>Przekazywanego uwierzytelniania
Przy użyciu przekazywanego uwierzytelniania hasła użytkownika hello jest weryfikowany pod kątem hello lokalnej usługi Active Directory kontrolera. hasło Hello nie wymaga toobe obecne w usłudze Azure AD w jakimkolwiek formularzu. Dzięki temu zasady lokalne, takie jak ograniczeń logowania godzinę toobe oszacowane w trakcie uwierzytelniania toocloud usług.

Przekazywanego uwierzytelniania przy użyciu prostego agenta na komputerze przyłączonym do domeny systemu Windows Server 2012 R2 w środowisku lokalne powitania. Ten agent nasłuchuje żądań sprawdzania poprawności hasła. Nie wymaga żadnych portów przychodzących toobe Otwórz toohello Internet.

Ponadto można również włączyć logowanie jednokrotne dla użytkowników na komputerach przyłączonych do domeny, znajdujących się w sieci firmowej hello. Pojedynczy logowania, włączone tylko dla użytkowników wymaga tooenter toohelp username, ich bezpiecznego dostępu do zasobów w chmurze.
![Przekazywanego uwierzytelniania](./media/active-directory-aadconnect-user-signin/pta.png)

Aby uzyskać więcej informacji, zobacz:
- [Przekazywanego uwierzytelniania](active-directory-aadconnect-pass-through-authentication.md)
- [Logowanie jednokrotne](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Federacyjnego, który używa nowej lub istniejącej farmy usług AD FS w systemie Windows Server 2012 R2
Z federacyjnego logowania użytkownicy będą mogli logować w tooAzure usług AD wraz z programem swoich haseł lokalnych. Gdy są one w sieci firmowej hello ich nie muszą nawet być tooenter haseł. Przy użyciu opcji federacyjnego hello z usługami AD FS, można wdrożyć nowej lub istniejącej farmy z usługami AD FS w systemie Windows Server 2012 R2. Jeśli wybierzesz toospecify istniejącej farmy, Azure AD Connect konfiguruje hello zaufania między farmy i usługi Azure AD, dzięki czemu użytkownicy mogą zalogować.

<center>![Federacja z usług AD FS w systemie Windows Server 2012 R2](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Wdrażanie federacyjnych z usługami AD FS w systemie Windows Server 2012 R2

W przypadku instalowania nowej farmy, potrzebne są:

* Serwer Windows Server 2012 R2 dla serwera federacyjnego hello.
* Serwer Windows Server 2012 R2 powitania serwera Proxy aplikacji sieci Web.
* Plik PFX o jeden certyfikat protokołu SSL dla nazwy usługi federacyjnej zamierzone. Na przykład: fs.contoso.com.

Jeśli wdrażasz nową farmę lub przy użyciu istniejącej farmy, należy:

* Poświadczenia administratora lokalnego na serwerach federacyjnych.
* Poświadczenia administratora lokalnego na żadnym serwerze grupy roboczej (nie przyłączonych do domeny), który ma toodeploy hello roli serwera Proxy aplikacji sieci Web na.
* Maszyna Hello uruchomienie Kreatora hello na tooany stanie tooconnect toobe innych komputerów, które mają tooinstall usług AD FS lub serwer Proxy aplikacji sieci Web na przy użyciu zdalnego zarządzania systemem Windows.

Aby uzyskać więcej informacji, zobacz [Konfigurowanie logowania jednokrotnego za pomocą usług AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Zaloguj się przy użyciu wcześniejszej wersji usług AD FS lub rozwiązanie innej firmy
Jeśli już skonfigurowano logowania w chmurze przy użyciu wcześniejszej wersji usług AD FS (np. usługi AD FS 2.0) lub dostawcy federacyjnego innych firm, można wybierać Konfiguracja logowania użytkownika tooskip za pośrednictwem usługi Azure AD Connect. Pozwoli to tooget hello ostatniej synchronizacji i innych funkcji programu Azure AD Connect podczas nadal przy użyciu istniejącego rozwiązania do logowania.

Aby uzyskać więcej informacji, zobacz hello [listę zgodności federacyjnych innych firm w usłudze Azure AD](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Logowanie użytkownika i głównej nazwy użytkownika
### <a name="understanding-user-principal-name"></a>Opis główna nazwa użytkownika
W usłudze Active Directory hello domyślne użytkownika sufiks głównej nazwy (UPN) jest hello nazwę DNS domeny hello, w którym utworzono konto użytkownika hello. W większości przypadków jest to hello nazwę domeny, która jest zarejestrowana jako domena przedsiębiorstwa hello na powitania Internet. Jednak można dodać więcej sufiksów UPN przy użyciu domeny usługi Active Directory i relacje zaufania.

Witaj nazwę UPN użytkownika hello ma hello format username@domain. Na przykład dla domeny usługi Active Directory o nazwie "contoso.com" użytkownika o nazwie Jan może być hello UPN "john@contoso.com". Witaj nazwę UPN użytkownika hello jest oparta na RFC 822. Chociaż hello UPN i udziału e-mail hello w tym samym formacie, wartość hello hello nazwy UPN użytkownika może lub nie może być hello takie same jak hello adres e-mail użytkownika hello.

### <a name="user-principal-name-in-azure-ad"></a>Główna nazwa użytkownika w usłudze Azure AD
Kreator Azure AD Connect Hello używa atrybutu userPrincipalName hello lub umożliwia określenie hello toobe atrybutu (w instalacji niestandardowej) używany z lokalnymi jako hello główną nazwę użytkownika w usłudze Azure AD. Jest to wartość hello, która jest używana dla logowania tooAzure AD. Jeśli hello wartość atrybutu userPrincipalName hello nie odpowiada tooa zweryfikowaną domeną w usłudze Azure AD, a następnie usługi Azure AD zastępuje ona wartości domyślnej. wartość onmicrosoft.com.

Każdym katalogu w usłudze Azure Active Directory jest dostarczany z nazwą domeny wbudowanej z hello format contoso.onmicrosoft.com, umożliwiające możesz rozpocząć korzystanie z platformy Azure lub innych usług firmy Microsoft. Można Usprawnij i Uprość hello logowania za pomocą domen niestandardowych. Aby uzyskać informacje o niestandardowych nazw domen w usłudze Azure AD i tooverify domeny, zobacz temat [dodać tooAzure nazwa Twojej niestandardową domenę usługi Active Directory](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Konfiguracja logowania się w usłudze Azure AD
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Konfiguracji platformy Azure AD logowania z programem Azure AD Connect
środowiska logowania Hello Azure AD zależy od tego, czy usługi Azure AD może być zgodne z sufiksem nazwy głównej użytkownika hello użytkownika, który ma zostać zsynchronizowane tooone hello domen niestandardowych, które są sprawdzane w katalogu usługi Azure AD hello. Azure AD Connect zawiera informacje pomocne podczas konfigurowania ustawień usługi Azure AD logowania, tak, aby hello użytkownika logowania w chmurze hello jest podobne możliwości lokalnymi toohello.

Sufiksy nazw UPN, zdefiniowanych dla toomatch domeny i prób hello hello Azure AD Connect list z domeny niestandardowej w usłudze Azure AD. Następnie pomaga z hello odpowiednie działaniami, które należy podjąć toobe.
Strona logowania Hello Azure AD znajduje się lista hello sufiksy nazw UPN, które są zdefiniowane dla lokalnej usługi Active Directory a hello odpowiedni stan każdego sufiksu. wartości stanu Hello może być jedną z następujących hello:

| Stan | Opis | Wymagana akcja |
|:--- |:--- |:--- |
| Weryfikacji |Azure AD Connect odnaleziono odpowiadającego mu zweryfikowaną domeną w usłudze Azure AD. Wszyscy użytkownicy w tej domenie zalogować się przy użyciu poświadczeń lokalnych. |Nie jest potrzebne nie działanie. |
| Nie zweryfikowano |Azure AD Connect można odnaleźć pasującego domeny niestandardowej w usłudze Azure AD, ale nie jest on weryfikowany. Hello sufiks nazwy UPN użytkowników hello ta domena będzie można zmienić domyślny toohello. po synchronizacji, jeśli nie jest zweryfikowana hello domeny zostanie dodany sufiks onmicrosoft.com. | [Sprawdź domenę niestandardową hello w usłudze Azure AD.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Nie dodano |Azure AD Connect nie znaleziono tego zgodnych toohello sufiks nazwy UPN domeny niestandardowej. Hello sufiks nazwy UPN użytkowników hello ta domena będzie można zmienić domyślne toohello. Jeśli hello domeny nie jest dodany i zweryfikowane na platformie Azure zostanie dodany sufiks onmicrosoft.com. | [Dodawania i weryfikowania domeny niestandardowej, która odpowiada toohello sufiks głównej nazwy użytkownika.](../add-custom-domain.md) |

Strona logowania Hello Azure AD wymieniono hello sufiksy nazw UPN, które są definiowane dla lokalnej usługi Active Directory i hello odpowiedniej domeny niestandardowej w usłudze Azure AD z hello bieżący stan weryfikacji. Do niestandardowej instalacji można teraz wybrać hello atrybut nazwy głównej użytkownika hello na powitania **logowania w usłudze Azure AD** strony.

![Strona logowania usługi AD platformy Azure](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Możesz kliknąć hello odświeżania przycisk pobierania toore hello najnowszy stan hello niestandardowych domen z usługi Azure AD.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Wybranie atrybutu hello hello główną nazwę użytkownika w usłudze Azure AD
Witaj atrybut userPrincipalName jest hello atrybut, którego użytkownicy po zalogowaniu tooAzure AD i Office 365. Należy sprawdzić domen hello (znanej także jako sufiksy nazw UPN), które są używane w usłudze Azure AD przed hello użytkowników są synchronizowane.

Zdecydowanie zaleca się pozostawienie hello domyślnego atrybutu userPrincipalName. Jeśli ten atrybut jest nonroutable i nie można zweryfikować, wówczas jest to możliwe tooselect innego atrybutu (na przykład e-mail) jako atrybut hello, która przechowuje hello identyfikator logowania. Jest to nazywane hello alternatywny identyfikator. Witaj wartość atrybutu alternatywnego Identyfikatora musi występować po hello RFC 822 standard. Alternatywnego Identyfikatora można użyć zarówno hasło logowania jednokrotnego i federacyjnego logowania jednokrotnego hello logowania rozwiązanie problemu.

> [!NOTE]
> Korzystanie z alternatywnego Identyfikatora nie jest zgodna z wszystkich obciążeń usługi Office 365. Aby uzyskać więcej informacji, zobacz [Konfigurowanie alternatywnego Identyfikatora logowania](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>Stany różnych domen niestandardowych i ich wpływ na środowisko hello Azure logowania
Jest bardzo ważne toounderstand hello relacja między Stanami domeny niestandardowej hello w katalogu usługi Azure AD i hello sufiksy nazw UPN, które są zdefiniowane lokalnie. Przejdźmy za pomocą hello różne możliwe Azure logowania środowiska podczas podczas konfigurowania synchronizacji za pomocą usługi Azure AD Connect.

W następujących informacji hello, załóżmy, że firma Microsoft jest związane z hello UPN sufiks contoso.com, który jest używany w katalogu lokalnym hello jako część nazwy UPN — na przykład user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Express synchronizacji ustawień i hasła
| Stan | Wpływ na środowisko użytkownika Azure logowania |
|:---:|:--- |
| Nie dodano |W takim przypadku nie domeny niestandardowej dla domeny contoso.com został dodany w katalogu usługi Azure AD hello. Użytkownicy, którzy mają nazwy UPN lokalne powitania sufiksu @contoso.com nie będzie możliwe toouse ich lokalnych toosign nazwy UPN w tooAzure. Będzie zamiast tego mają toouse nowej nazwy UPN, który udostępnił toothem przez usługę Azure AD przez dodanie sufiksu hello hello domyślny katalog usługi Azure AD. Na przykład, jeśli jest synchronizowanie użytkowników toohello usługi Azure AD directory azurecontoso.onmicrosoft.com, następnie hello lokalnego użytkownika user@contoso.com podaje nazwę UPN user@azurecontoso.onmicrosoft.com. |
| Nie zweryfikowano |W takim przypadku mamy niestandardowej domeny contoso.com, który został dodany w katalogu hello Azure AD. Jednak jeszcze nie sprawdza. Jeśli hypervreplicavolumesize z synchronizowania użytkowników bez weryfikowania domeny hello, następnie hello użytkownicy zostaną przypisane nowe nazwy UPN przez usługę Azure AD, podobnie jak w scenariuszu "Nie dodano" hello. |
| Weryfikacji |W takim przypadku mamy niestandardowej domeny contoso.com, który został już dodany i zweryfikowane w usłudze Azure AD dla hello sufiks głównej nazwy użytkownika. Użytkownicy będą mogli toouse ich lokalnych główna nazwa użytkownika, na przykład user@contoso.com, toosign w tooAzure po są one zsynchronizowane tooAzure AD. |

###### <a name="ad-fs-federation"></a>Usługi AD FS federation
Nie można utworzyć federacji z domyślnymi hello. domeny onmicrosoft.com w usłudze Azure AD lub niezweryfikowanej domeny niestandardowej w usłudze Azure AD. Czas pracy Kreatora hello Azure AD Connect w przypadku wybrania toocreate niezweryfikowanej domeny federacji z, a następnie rejestruje program hello niezbędne toobe utworzone, gdzie jest hostowana serwery DNS dla domeny hello monity Azure AD Connect. Aby uzyskać więcej informacji, zobacz [weryfikowanie domeny hello Azure AD wybranej do Federacji](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

W przypadku wybrania opcji logowania użytkownika hello **Federacja z usługami AD FS**, a następnie musi mieć toocontinue domeny niestandardowej, tworzenie federacji w usłudze Azure AD. Nasze omówienie oznacza to, firma Microsoft ma niestandardową domenę contoso.com dodane w katalogu hello Azure AD.

| Stan | Wpływ na hello Azure logowania użytkowników |
|:---:|:--- |
| Nie dodano |W takim przypadku Azure AD Connect nie znaleziono pasującego domeny niestandardowej dla domeny contoso.com sufiks nazwy UPN hello w katalogu usługi Azure AD hello. Należy tooadd contoso.com domeny niestandardowej, jeśli potrzebujesz toosign użytkowników w za pomocą usług AD FS z lokalnych nazw UPN (jak user@contoso.com). |
| Nie zweryfikowano |W takim przypadku Azure AD Connect monit odpowiednie szczegóły dotyczące sposobu weryfikacji domeny na późniejszym etapie. |
| Weryfikacji |W takim przypadku można przejść dalej z konfiguracją hello bez dalszych działań. |

## <a name="changing-hello-user-sign-in-method"></a>Zmiana hello użytkownik logowania — metoda
Możesz zmienić metody logowania użytkownika hello w Federacji, synchronizacja haseł lub uwierzytelnianie przekazywane przy użyciu hello zadań, które są dostępne w programie Azure AD Connect po wykonaniu konfiguracji początkowej hello programu Azure AD Connect przy użyciu Kreatora hello. Ponownie uruchom Kreator Azure AD Connect hello, i zobaczysz listę zadań, które można wykonywać. Wybierz **zmienić logowania użytkownika** z hello listy zadań.

![Zmień logowanie użytkowników](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Na następnej stronie powitania zostanie wyświetlone pytanie tooprovide hello poświadczenia dla usługi Azure AD.

![Połącz tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Na powitania **logowania użytkownika** wybierz hello potrzeby logowania użytkownika.

![Połącz tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Jeśli wprowadzasz synchronizacji toopassword tymczasowego przełącznika, a następnie wybierz hello **kont użytkowników nie można konwertować** pole wyboru. Nie sprawdza opcja hello przekonwertuje toofederated każdego użytkownika, a może zająć kilka godzin.
>
>

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
- Dowiedz się więcej o [zagadnienia dotyczące projektowania usługi Azure AD Connect](active-directory-aadconnect-design-concepts.md).
