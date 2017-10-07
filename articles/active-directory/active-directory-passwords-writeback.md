---
title: "Azure AD SSPR z zapisywaniem zwrotnym haseł | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure AD i Azure AD Connect toowriteback hasła tooon lokalnego katalogu"
services: active-directory
keywords: "Zarządzanie hasłami w usłudze Active directory, zarządzanie hasłami, usługi Azure AD samodzielnego resetowania hasła usługi"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Omówienie funkcji zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł umożliwia tooconfigure usługi Azure AD toowrite hasła kopię tooyou lokalnej usługi Active Directory. Usuwa hello tooset muszą się i zarządzanie rozwiązanie resetowania hasła samoobsługi skomplikowane lokalnymi i zapewnia wygodny sposób oparte na chmurze dla Twojego tooreset użytkowników swoich haseł lokalnych wszędzie tam, gdzie są one. Zapisywanie zwrotne haseł jest składnikiem [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) czy włączone i używane przez bieżące subskrybentów Premium [wersje usługi Azure Active Directory](active-directory-editions.md).

Zapisywanie zwrotne haseł udostępnia następujące funkcje hello

* **Zero opinii opóźnienie** — zapisywanie zwrotne haseł jest operacja synchroniczna. Użytkownicy są niezwłocznie powiadomiona, jeśli hasło nie spełnia warunków zasady lub został toobe nie można zresetować lub zmienione w różnych przyczyn.
* **Obsługuje resetowanie haseł dla użytkowników za pomocą usług AD FS lub inne technologie federacyjnego** — z funkcji zapisywania zwrotnego haseł, dopóki hello kont użytkowników federacyjnych są zsynchronizowane w dzierżawie usługi Azure AD są toomanage stanie ich lokalnej usługi AD hasła z hello chmury.
* **Obsługuje resetowanie haseł dla użytkowników przy użyciu [synchronizacji skrótów haseł](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  — w przypadku usługi resetowania hasła hello wykryje, że synchronizowane konta jest włączona dla synchronizacji skrótów haseł, aż przywrócone zostaną zarówno tego konta lokalnie i w chmurze hasło jednocześnie.
* **Zmienianie haseł z hello obsługuje dostęp do panelu i Office 365** — federacyjnych lub hasło synchronizowane toochange dostarczanych użytkowników haseł wygasły lub nie wygasły, możemy zapisu tych środowiska wstecz tooyour AD lokalnego hasła.
* **Obsługuje zapis ponownie hasła, gdy administrator zresetować je z hello portalu Azure** — zawsze, gdy administrator resetuje hasło użytkownika w hello [portalu Azure](https://portal.azure.com), jeśli tego użytkownika jest Sfederowane lub synchronizacji haseł, zaplanujemy hello Witaj, Administratorze hasła wybiera na lokalnej usługi AD, a także. Jest to obecnie nieobsługiwane w hello portalu administratora usługi Office.
* **Wymusza lokalnej zasady haseł AD** — użytkownik resetuje hasła, Upewniamy się, że spełnia on lokalnej zasada domeny przed zatwierdzeniem go toothat katalogu. W tym historii, złożoności, wieku, filtry hasła i inne ograniczenia hasła, zdefiniowanych w lokalnej usługi AD.
* **Nie wymaga żadnych reguł zapory dla ruchu przychodzącego** — zapisywanie zwrotne haseł używa przekaźnika usługi Azure Service Bus jako podstawowy kanał komunikacyjny, co oznacza, że nie masz tooopen żadnych portów przychodzących na zaporze dla toowork tej funkcji.
* **Nie jest obsługiwana dla kont użytkowników, które istnieją w ramach grup ochrony w lokalnej usługi Active Directory** — Aby uzyskać więcej informacji na temat grup ochrony, zobacz [kont chronionych i grup w usłudze Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Sposób działania funkcji zapisywania zwrotnego haseł

Po zsynchronizowaniu skrótów federacyjnych lub hasło użytkownika jest dostarczany tooreset lub zmienić swoje hasło w chmurze hello hello rejestrowany:

1. Sprawdzamy toosee typ użytkownika hello hasła.
    * Jeśli widzimy hasła hello odbywa się lokalnie
        * Firma Microsoft Sprawdź, czy hello usługi zapisywania zwrotnego działa i jest uruchomiony, jeśli jest, nie możemy udostępnić użytkownika hello kontynuować
        * Jeśli usługa zapisywania zwrotnego hello nie jest aktywny, możemy Monituj hello użytkownika, że nie można zresetować swoje hasło teraz
2. Następnie użytkownik hello przekazuje hello uwierzytelniania odpowiednich bram i osiągnie hello resetowania hasła ekranu.
3. Hello użytkownik wybiera nowe hasło i potwierdzenie go.
4. Po kliknięciu przesyłania, możemy szyfrowania z klucza symetrycznego, który został utworzony podczas procesu konfiguracji funkcji zapisywania zwrotnego hello hello hasła w postaci zwykłego tekstu.
5. Po szyfrowaniu hello hasła, przeprowadzamy go w ładunku, które są wysyłane za pośrednictwem protokołu HTTPS kanału tooyour specyficznego dla dzierżawy usługi bus relay (również skonfigurowanie automatycznie podczas procesu konfiguracji funkcji zapisywania zwrotnego hello). Ta przekazywania jest chroniony przez losowo generowane hasło, który zna instalacji lokalnej.
6. Po wiadomość hello dociera do usługi service bus, hello punkt końcowy resetowania hasła budzi i automatycznie widzi, że ma oczekujące żądanie resetowania.
7. usługi Hello następnie szuka użytkownika hello zagrożona przy użyciu atrybutu zakotwiczenia hello chmury. Dla tego toosucceed wyszukiwania:

    * obiekt użytkownika Hello musi istnieć w hello przestrzeni łącznika AD
    * obiekt użytkownika Hello musi być połączone toohello odpowiedniego obiektu MV
    * obiekt użytkownika Hello musi być połączone toohello odpowiedni obiekt łącznika usługi AAD.
    * Hello łącza z tooMV obiekt łącznika AD musi mieć reguły synchronizacji hello `Microsoft.InfromADUserAccountEnabled.xxx` hello łącze. <br> <br>
    Wywołanie hello jest dostarczany z chmury hello, używa aparatu synchronizacji hello hello toolook atrybutu cloudAnchor zapasową obiektu przestrzeni łącznika AAD hello, następuje obiektu MV toohello wstecz łącza hello i następnie następuje hello link wsteczny toohello AD obiektu. Ponieważ może istnieć wiele obiektów AD (obejmującego wiele lasów) dla tego samego użytkownika, powitalne aparatu synchronizacji polega na powitania hello `Microsoft.InfromADUserAccountEnabled.xxx` hello toopick łącza, popraw jedną.

    > [!Note]
    > W wyniku tej logiki Azure AD Connect musi być możliwe toocommunicate z hello Emulator podstawowego kontrolera domeny dla toowork zapisywania zwrotnego haseł. Tooenable tym ręcznie, należy możesz połączyć toohello Azure AD Connect Emulator podstawowego kontrolera domeny, klikając prawym przyciskiem myszy na powitania **właściwości** hello łącznika synchronizacji usługi Active Directory, wybierając **skonfigurować partycje katalogu**. Z tego miejsca, wyszukaj hello **ustawienia połączenia kontrolera domeny** sekcji i sprawdź pole hello zatytułowany **korzystają z kontrolerów domeny preferowanych**. Nawet jeśli hello preferowane, że kontroler domeny nie jest emulator podstawowego kontrolera domeny, Azure AD Connect będzie podejmować tooconnect toohello podstawowego kontrolera domeny dla funkcji zapisywania zwrotnego haseł.

8. Po znalezieniu hello konta użytkownika, możemy próba tooreset hello hasło bezpośrednio w hello odpowiednie lasu usługi AD.
9. Jeśli hello hasła zestawu operacja się powiodła, możemy Monituj użytkownika hello, się, że ich hasło zostało zmienione.
    > [!NOTE]
    > W przypadku hello, jeśli hasło użytkownika hello jest synchronizowane tooAzure AD przy użyciu synchronizacji haseł, istnieje ryzyko, że zasady haseł lokalne powitania jest mniejsze niż zasady haseł hello chmury. W takim przypadku Będziemy nadal wymuszania niezależnie od zasady lokalne powitania jest, a zamiast tego Zezwalaj na hasło skrótu synchronizacji toosynchronize hello skrótu tego hasła. Dzięki temu, czy zasady lokalne są wymuszane w chmurze hello niezależnie użycie hasła synchronizacji lub Federacji tooprovide logowanie jednokrotne.

10. Jeśli hasło hello operacja kończy się niepowodzeniem, możemy zwrócić hello błąd toohello użytkownika i daj spróbuj ponownie.
    * Operacja Hello może zakończyć się niepowodzeniem z powodu następujących hello
        * Witaj usługa nie działa
        * Hello hasło, które są wybrane nie spełnia warunków zasady organizacji
        * Nie można odnaleźć użytkownika hello w hello lokalnej usługi AD

    Mamy określonego komunikatu dla wielu przypadkach i poinformuj hello użytkownika, co można zrobić tooresolve hello problem.

## <a name="configuring-password-writeback"></a>Konfigurowanie funkcji zapisywania zwrotnego haseł

Zalecane jest użycie funkcji automatycznej aktualizacji hello [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) Jeśli chcesz toouse zapisywania zwrotnego haseł.

Narzędzia DirSync i Azure AD Sync nie są już obsługiwane metody zapewniania artykułu hello zapisywania zwrotnego haseł [uaktualnienie z narzędzia DirSync i Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) ma więcej toohelp informacji o przejście.

Witaj czynności założono skonfigurowano już program Azure AD Connect w środowisku przy użyciu hello [Express](./connect/active-directory-aadconnect-get-started-express.md) lub [niestandardowy](./connect/active-directory-aadconnect-get-started-custom.md) ustawienia.

1. tooconfigure i włączyć funkcję zapisywania zwrotnego haseł logowania tooyour usługi Azure AD Connect serwera i uruchomić hello **Azure AD Connect** Kreatora konfiguracji.
2. Na ekranie powitalnym powitania kliknij **Konfiguruj**.
3. Na powitania dodatkowych zadań ekranu kliknij **Dostosuj opcje synchronizacji** , a następnie wybierz **dalej**.
4. Na ekranie tooAzure AD Connect hello wprowadź poświadczenia administratora globalnego i wybierz **dalej**.
5. Na powitania Podłącz katalogów i domeny i jednostki Organizacyjnej filtrowania ekrany można wybrać **dalej**.
6. Na ekranie funkcji opcjonalnych hello hello pole wyboru obok zbyt**funkcji zapisywania zwrotnego haseł** i kliknij przycisk **dalej**.
   ![Włączanie zapisywania zwrotnego haseł w programie Azure AD Connect][Writeback]
7. Na ekranie gotowe tooconfigure powitania kliknij **Konfiguruj** i poczekaj, aż hello toocomplete procesu.
8. Po wyświetleniu konfiguracji pełną możesz kliknąć **zakończenia**

## <a name="licensing-requirements-for-password-writeback"></a>Wymagania dotyczące funkcji zapisywania zwrotnego haseł licencjonowania

Informacji na temat licencjonowania, zobacz temat hello [licencji wymagane dla funkcji zapisywania zwrotnego haseł](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) lub hello witryn

* [Usługi Azure site cennik usługi Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Bezpieczne produktywności Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Tryby uwierzytelniania obsługiwane w przypadku funkcji zapisywania zwrotnego haseł lokalnymi

Zapisywanie zwrotne haseł działa hello następujące typy hasło użytkownika:

* **Tylko w chmurze użytkowników**: funkcji zapisywania zwrotnego haseł nie ma zastosowania w takiej sytuacji, ponieważ nie istnieje żadne lokalnego hasła
* **Synchronizowane hasła użytkowników**: obsługiwane zapisywania zwrotnego haseł
* **Użytkownicy federacyjni**: obsługiwane zapisywania zwrotnego haseł
* **Użytkownicy uwierzytelniania przekazywanego**: obsługiwane zapisywania zwrotnego haseł

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Operacje użytkownika i administratora, obsługiwane w przypadku funkcji zapisywania zwrotnego haseł

Hasła są zapisywane w hello wszystkie następujące sytuacje:

* **Obsługiwane operacje użytkownika końcowego**
  * Wszelkie dobrowolnej samoobsługi użytkownika końcowego zmienić operacji hasła
  * Dowolnego użytkownika końcowego samoobsługi życie operacji zmiany hasła (na przykład, datę wygaśnięcia hasła)
  * Dowolnego użytkownika samoobsługowego resetowania hasła pochodzące z hello [portalu resetowania haseł](https://passwordreset.microsoftonline.com)
* **Obsługiwane operacje administratora**
  * Wszelkie dobrowolnej samoobsługi administratora Zmień operacji hasła
  * Wszelkie administratora samoobsługi życie operacji zmiany hasła (na przykład, datę wygaśnięcia hasła)
  * Wszelkie administratora samoobsługowego resetowania hasła pochodzące z hello [portalu resetowania haseł](https://passwordreset.microsoftonline.com)
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z hello [klasycznego portalu Azure](https://manage.windowsazure.com)
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z hello [portalu Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Operacje administrator i użytkownik nie jest obsługiwane dla funkcji zapisywania zwrotnego haseł

Hasła są **nie** napisane Wstecz w hello następujące sytuacje:

* **Nieobsługiwany operacji użytkowników końcowych**
  * Każdy użytkownik końcowy Resetowanie własnych haseł przy użyciu programu PowerShell v1, v2 lub hello Azure AD Graph API
* **Nieobsługiwane operacje administratora**
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z hello [portalu zarządzania usługi Office](https://portal.office.com)
  * Wszelkie resetowania z programu PowerShell v1, v2 lub hello Azure AD Graph API hasła przez użytkownika końcowego inicjowanych przez administratora

Pracujemy nad tooremove ograniczenia te powodują, firma Microsoft nie ma określonych osi czasu, który firma Microsoft może udostępniać jeszcze.

## <a name="password-writeback-security-model"></a>Model zabezpieczeń zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł jest usługą wysokim poziomie zabezpieczeń.  tooensure informacji jest chroniony, możemy Włącz model zabezpieczeń 4-warstwowy, które jest opisane poniżej.

* **Przekaźnik usługi service bus specyficznego dla dzierżawy**
  * Po skonfigurowaniu usługi hello skonfigurowanie specyficznego dla dzierżawy usługi przekazywania magistrali, która jest chroniona przez losowo generowany silne hasło, które firma Microsoft nigdy nie ma dostępu do.
* **Klucz szyfrowania zablokowaną, kryptograficznie silne hasło**
  * Po utworzeniu przekaźnik magistrali usług hello utworzymy silnego klucza symetrycznego używamy tooencrypt hello hasła, ponieważ pochodzi za pośrednictwem przewodowy hello. Ten klucz znajduje się tylko w sklepie tajny firmy w hello chmury, co znacznie jest zablokowany i inspekcji, podobnie jak wszystkie hasła w katalogu hello.
* **Branżowy standard TLS**
  1. Gdy hasło Resetowanie lub zmienianie operacja odbywa się w chmurze hello, możemy pobrać hello przechowywała hasła i szyfrowania kluczem publicznym.
  2. Możemy umieścić który w komunikatu protokołu HTTPS, który był wysyłany za pośrednictwem kanału szyfrowanego przy użyciu przekaźnika bus usługi tooyour certyfikaty SSL firmy Microsoft.
  3. Po wiadomość hello dociera do usługi Service Bus, agenta lokalnie wznawia pracę w górę i uwierzytelnia tooService Bus przy użyciu hello silne hasło, które wcześniej został wygenerowany.
  4. Agent lokalnymi przejmuje zaszyfrowaną wiadomość hello, odszyfrowuje ją przy użyciu klucza prywatnego hello wygenerowania firma Microsoft.
  5. Agent lokalnymi podejmuje tooset hello hasła za pośrednictwem hello AD DS UstawianieHasła API.
     * Ten krok jest, co pozwala nam tooenforce AD lokalne zasady haseł (złożoności, wieku, Historia, filtrami itp.) w chmurze hello.
* **Zasady wygasania wiadomości** 
  * Jeśli wiadomość hello znajduje się w usłudze Service Bus, ponieważ usługi lokalnej nie działa, przekroczy limit czasu i po kilku minutach tooincrease zabezpieczeń jeszcze bardziej zostać usunięta.

### <a name="password-writeback-encryption-details"></a>Szczegóły szyfrowania zapisywania zwrotnego haseł

Poniżej opisano kroki szyfrowania Hello żądanie zresetowania hasła przechodzi przez po przesłaniu przez użytkownika, zanim zostanie odebrane w w środowisku lokalnym, tooensure maksymalnej niezawodności i zabezpieczeń.

* **Krok 1 — hasło szyfrowania kluczem RSA 2048-bitowego** — gdy użytkownik prześle toobe hasła, zapisywane tooon lokalnego najpierw hello przesłanych samego hasła są szyfrowane za pomocą klucza RSA 2048-bitowego.
* **Krok 2 — pakiet poziom szyfrowania z usługą GCM AES** — a następnie hello cały pakiet (hasło + wymaganych metadanych) są zaszyfrowane za pomocą usługi GCM AES. Zapobiega każda osoba mająca kanału magistrali usług podstawowych toohello bezpośredni dostęp do wyświetlania/manipulowanie hello zawartość.
* **Krok 3 - cała komunikacja odbywa się za pośrednictwem protokołu TLS / SSL** -cała komunikacja hello z magistrali usług odbywa się w kanału SSL/TLS. To chroni zawartość hello z nieupoważnione 3.
* **Automatyczne Przerzucanie klucza co sześć miesięcy** — automatycznie co 6 miesięcy, lub za każdym razem, gdy funkcji zapisywania zwrotnego haseł jest wyłączony lub ponownie aktywne na Azure AD Connect, możemy przerzucania te klucze tooensure maksymalną usługi zabezpieczeń i bezpieczeństwa.

### <a name="password-writeback-bandwidth-usage"></a>Wykorzystanie przepustowości zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł jest usługą niskiej przepustowości, która wysyła żądania kopii toohello lokalnego agenta tylko w obszarze hello następujące okoliczności:

1. Dwa komunikaty wysyłane podczas włączania lub wyłączania funkcji hello za pośrednictwem usługi Azure AD Connect.
2. Jeden komunikat jest wysyłane co pięć minut jako pulsu usługi dla tak długo, jak działa usługa hello.
3. Dwa komunikaty są wysyłane poszczególnych czas przesłaniu nowego hasła
    * Pierwszy komunikat jako operacja żądanie tooperform hello
    * Drugi komunikat, który zawiera hello wynik operacji hello i są wysyłane w hello następujące okoliczności:
        * Zawsze przesłaniu nowego hasła podczas użytkownika samoobsługowego resetowania hasła.
        * Zawsze przesłaniu nowego hasła podczas operacji zmiany hasła użytkownika.
        * Zawsze przesłaniu nowego hasła podczas resetowania (w wyniku hello tylko portali administratora platformy Azure) hasła użytkownika inicjowanych przez administratora.

#### <a name="message-size-and-bandwidth-considerations"></a>Zagadnienia dotyczące rozmiaru i przepustowości wiadomości

Hello rozmiar każdego z opisanych powyżej wiadomość hello jest zwykle w obszarze 1 kb, nawet w przypadku obciążeń skrajne, hello hasła zapisywania zwrotnego sama usługa zajmuje kilka kilobitów na sekundę przepustowości. Ponieważ każdy komunikat jest wysyłany w czasie rzeczywistym, tylko wtedy, gdy jest to wymagane przez operację aktualizacji hasła i ponieważ tyle mały rozmiar wiadomości powitania, przepustowości hello możliwości zapisywania zwrotnego hello skutecznie toohave za mały rzeczywistym zauważalnego wpływu.

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Włączanie zapisywania zwrotnego haseł w programie Azure AD Connect"
