---
title: "Azure AD SSPR z zapisywaniem zwrotnym haseł | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure AD i Azure AD Connect do zapisywania zwrotnego haseł do katalogu lokalnego"
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
ms.openlocfilehash: 6b195fdcce17184628acd98a686520528a6dadd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="password-writeback-overview"></a>Omówienie funkcji zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł umożliwia konfigurowanie usługi Azure AD można zapisać hasła powrót do lokalnej usługi Active Directory. Eliminuje potrzebę konfigurowania i zarządzania nią rozwiązanie resetowania hasła samoobsługi skomplikowane lokalnymi i zapewnia wygodny sposób oparte na chmurze użytkownikom resetowania swoich haseł lokalnych, wszędzie tam, gdzie są one. Zapisywanie zwrotne haseł jest składnikiem [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) czy włączone i używane przez bieżące subskrybentów Premium [wersje usługi Azure Active Directory](active-directory-editions.md).

Zapisywanie zwrotne haseł zapewnia następujące funkcje

* **Zero opinii opóźnienie** — zapisywanie zwrotne haseł jest operacja synchroniczna. Użytkownicy są niezwłocznie powiadomiona, jeśli hasło nie spełnia warunków zasady lub nie może zresetować lub zmianie dowolnego powodu.
* **Obsługuje resetowanie haseł dla użytkowników za pomocą usług AD FS lub inne technologie federacyjnego** — z funkcji zapisywania zwrotnego haseł, tak długo, jak konta użytkowników federacyjnych są zsynchronizowane w dzierżawie usługi Azure AD, są w stanie zarządzać lokalnych haseł usługi AD z chmury.
* **Obsługuje resetowanie haseł dla użytkowników przy użyciu [synchronizacji skrótów haseł](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  — w przypadku usługi resetowania hasła wykryje, że konto synchronizowanego użytkownika jest włączona dla synchronizacji skrótów haseł, aż przywrócone zostaną zarówno w przypadku tego konta lokalnego, jak i hasło chmury jednocześnie.
* **Obsługuje zmienianie haseł z usługi Office 365 i panelu dostępu** — federacyjnych lub synchronizacji haseł użytkowników się zmieniać swoje hasła wygasły lub nie wygasły, możemy zapisywać te hasła zwrotnie do środowiska lokalnego AD.
* **Obsługuje zapisywania ponownie hasła, gdy administrator zresetować je z portalu Azure** — zawsze, gdy administrator resetuje hasło użytkownika w [portalu Azure](https://portal.azure.com), jeśli tego użytkownika jest Sfederowane lub synchronizacji haseł, zaplanujemy hasło administratora wybiera na lokalnej usługi AD, a także. Jest to obecnie nieobsługiwane w portalu administracyjnym pakietu Office.
* **Wymusza lokalnej zasady haseł AD** — użytkownik resetuje hasła, możemy upewnij się, że spełnia on lokalnej zasada domeny przed zatwierdzeniem go do tego katalogu. W tym historii, złożoności, wieku, filtry hasła i inne ograniczenia hasła, zdefiniowanych w lokalnej usługi AD.
* **Nie wymaga żadnych reguł zapory dla ruchu przychodzącego** — zapisywanie zwrotne haseł używa przekaźnika usługi Azure Service Bus jako podstawowy kanał komunikacyjny, co oznacza, że nie trzeba otworzyć żadnych portów przychodzących na zaporze, aby ta funkcja działała.
* **Nie jest obsługiwana dla kont użytkowników, które istnieją w ramach grup ochrony w lokalnej usługi Active Directory** — Aby uzyskać więcej informacji na temat grup ochrony, zobacz [kont chronionych i grup w usłudze Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Sposób działania funkcji zapisywania zwrotnego haseł

Gdy skrót federacyjnych lub hasło synchronizowanego użytkownika jest dostarczany do resetowania lub zmieniania swoich haseł w chmurze, są następujące operacje:

1. Sprawdzamy, do jakiego rodzaju hasła użytkownik nie ma.
    * Jeśli widzimy hasło odbywa się lokalnie
        * Sprawdzamy, czy usługa zapisywania zwrotnego działa i jest uruchomiony, jeśli jest, nie możemy udostępnić użytkownika kontynuować
        * Jeśli usługa zapisywania zwrotnego nie znajduje się w górę, możemy Monituj użytkownika, że nie można zresetować swoje hasło teraz
2. Następnie użytkownik przekazuje bramy uwierzytelniania i osiągnie ekranu resetowania hasła.
3. Użytkownik wybiera nowe hasło i potwierdza go.
4. Po kliknięciu przesyłania, firma Microsoft szyfrowania z klucza symetrycznego, który został utworzony podczas instalacji funkcji zapisywania zwrotnego haseł w postaci zwykłego tekstu.
5. Po szyfrowania hasła, przeprowadzamy go w ładunku, które są wysyłane za pośrednictwem kanału HTTPS do sieci specyficznego dla dzierżawy usługi bus relay (również skonfigurowanie automatycznie podczas instalacji funkcji zapisywania zwrotnego). Ta przekazywania jest chroniony przez losowo generowane hasło, który zna instalacji lokalnej.
6. Gdy komunikat dociera do usługi service bus, punkt końcowy resetowania hasła budzi i automatycznie widzi, że ma oczekujące żądanie resetowania.
7. Usługa następnie szuka użytkownika danego przy użyciu atrybutu zakotwiczenia chmury. Dla tego odnośnika powiodła się:

    * Obiekt użytkownika musi istnieć w przestrzeni łącznika AD
    * Obiekt użytkownika muszą być połączone z odpowiedniego obiektu MV
    * Obiekt użytkownika muszą być połączone z odpowiedni obiekt łącznika usługi AAD.
    * Link z obiektu łącznika usługi Active Directory do MV musi mieć reguły synchronizacji `Microsoft.InfromADUserAccountEnabled.xxx` łącze. <br> <br>
    Gdy wywołanie z chmury, aparat synchronizacji używa atrybutu cloudAnchor do odszukania obiektu przestrzeni łącznika usługi AAD, następujące łącze z powrotem do obiektu MV i następnie lokalizuje łącze obiektu usługi Active Directory. Ponieważ może istnieć wiele obiektów AD (obejmującego wiele lasów) dla tego samego użytkownika, na podstawie aparatu synchronizacji `Microsoft.InfromADUserAccountEnabled.xxx` łącze do pobrania poprawne.

    > [!Note]
    > W wyniku tej logiki Azure AD Connect musi mieć możliwość komunikacji z Emulator podstawowego kontrolera domeny dla funkcji zapisywania zwrotnego haseł do pracy. Jeśli musisz ręcznie włączyć, możesz połączyć Azure AD Connect do emulatora podstawowego kontrolera domeny przez kliknięcie prawym przyciskiem myszy **właściwości** łącznika synchronizacji usługi Active Directory, wybierając **Konfigurowanie partycji katalogu**. Z tego miejsca poszukaj sekcji **Ustawienia połączenia kontrolera domeny** i zaznacz pole wyboru o nazwie **Korzystaj tylko z preferowanych kontrolerów domeny**. Nawet jeśli preferowany kontroler domeny nie jest emulator podstawowego kontrolera domeny, Azure AD Connect będzie podejmować próby połączenia z podstawowym kontrolerem domeny dla funkcji zapisywania zwrotnego haseł.

8. Po znalezieniu konta użytkownika, możemy próba zresetowania hasła bezpośrednio w odpowiednich lasu usługi AD.
9. Jeśli hasło operacji set zakończy się pomyślnie, firma Microsoft Poinformuj użytkownika swoje hasło zostało zmienione.
    > [!NOTE]
    > W przypadku gdy hasło użytkownika są synchronizowane z usługą Azure AD przy użyciu synchronizacji haseł, istnieje ryzyko, że lokalne zasady haseł jest mniejsze niż zasady haseł w chmurze. W takim przypadku Będziemy nadal wymusza niezależnie od zasady lokalnej jest i zezwolić synchronizacji skrótu hasła do synchronizowania skrótów tego hasła. Gwarantuje to, czy zasady lokalne są wymuszane w chmurze, niezależnie w celu zapewnienia logowania jednokrotnego za pomocą synchronizacji haseł lub federacyjnych.

10. Jeśli hasło ustawione operacja kończy się niepowodzeniem, możemy zwrócić błąd do użytkownika i daj spróbuj ponownie.
    * Operacja może zakończyć się niepowodzeniem z powodu poniżej
        * Usługa nie działa
        * Hasło, które są wybrane nie spełnia warunków zasady organizacji
        * Nie można znaleźć użytkownika w lokalnej usłudze AD

    Firma Microsoft może mieć określonego komunikatu dla wielu z tych przypadków, a następnie poinformuj użytkownika, sposób ich działania, aby rozwiązać ten problem.

## <a name="configuring-password-writeback"></a>Konfigurowanie funkcji zapisywania zwrotnego haseł

Zalecane jest użycie funkcji automatycznej aktualizacji [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) Jeśli chcesz użyć funkcji zapisywania zwrotnego haseł.

Narzędzia DirSync i Azure AD Sync nie są już obsługiwane sposób włączania funkcji zapisywania zwrotnego haseł artykuł [uaktualnienie z narzędzia DirSync i Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) zawiera więcej informacji, aby pomóc w przejście.

Poniższe kroki założono skonfigurowano już program Azure AD Connect w środowisku za pomocą [Express](./connect/active-directory-aadconnect-get-started-express.md) lub [niestandardowy](./connect/active-directory-aadconnect-get-started-custom.md) ustawienia.

1. Aby skonfigurować i włączyć dziennik zapisywania zwrotnego haseł w z serwerem usługi Azure AD Connect i uruchomić **Azure AD Connect** Kreatora konfiguracji.
2. Na ekranie powitalnym kliknij przycisk **Konfiguruj**.
3. Na dodatkowe zadania ekranu kliknij **Dostosuj opcje synchronizacji** , a następnie wybierz **dalej**.
4. Na ekranie łączenie z usługą Azure AD wprowadź poświadczenia administratora globalnego i wybierz polecenie **dalej**.
5. Na Połącz z katalogów i domenę i jednostkę Organizacyjną ekrany filtrowania można wybrać **dalej**.
6. Na ekranie funkcji opcjonalnych zaznacz pole wyboru obok pozycji **funkcji zapisywania zwrotnego haseł** i kliknij przycisk **dalej**.
   ![Włączanie zapisywania zwrotnego haseł w programie Azure AD Connect][Writeback]
7. Polecenie wszystko gotowe do skonfigurowania ekranu **Konfiguruj** i poczekaj na zakończenie procesu.
8. Po wyświetleniu konfiguracji pełną możesz kliknąć **zakończenia**

## <a name="licensing-requirements-for-password-writeback"></a>Wymagania dotyczące funkcji zapisywania zwrotnego haseł licencjonowania

Aby uzyskać informacje dotyczące licencjonowania, zobacz temat [licencji wymagane dla funkcji zapisywania zwrotnego haseł](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) lub następujące witryny

* [Usługi Azure site cennik usługi Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Bezpieczne produktywności Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Tryby uwierzytelniania obsługiwane w przypadku funkcji zapisywania zwrotnego haseł lokalnymi

Zapisywanie zwrotne haseł działa dla następujących typów hasło użytkownika:

* **Tylko w chmurze użytkowników**: funkcji zapisywania zwrotnego haseł nie ma zastosowania w takiej sytuacji, ponieważ nie istnieje żadne lokalnego hasła
* **Synchronizowane hasła użytkowników**: obsługiwane zapisywania zwrotnego haseł
* **Użytkownicy federacyjni**: obsługiwane zapisywania zwrotnego haseł
* **Użytkownicy uwierzytelniania przekazywanego**: obsługiwane zapisywania zwrotnego haseł

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Operacje użytkownika i administratora, obsługiwane w przypadku funkcji zapisywania zwrotnego haseł

Hasła są zapisywane w następujących sytuacjach:

* **Obsługiwane operacje użytkownika końcowego**
  * Wszelkie dobrowolnej samoobsługi użytkownika końcowego zmienić operacji hasła
  * Dowolnego użytkownika końcowego samoobsługi życie operacji zmiany hasła (na przykład, datę wygaśnięcia hasła)
  * Dowolnego użytkownika samoobsługowego resetowania hasła pochodzące z [portalu resetowania haseł](https://passwordreset.microsoftonline.com)
* **Obsługiwane operacje administratora**
  * Wszelkie dobrowolnej samoobsługi administratora Zmień operacji hasła
  * Wszelkie administratora samoobsługi życie operacji zmiany hasła (na przykład, datę wygaśnięcia hasła)
  * Wszelkie administratora samoobsługowego resetowania hasła pochodzące z [portalu resetowania haseł](https://passwordreset.microsoftonline.com)
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z [klasycznego portalu Azure](https://manage.windowsazure.com)
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z [portalu Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Operacje administrator i użytkownik nie jest obsługiwane dla funkcji zapisywania zwrotnego haseł

Hasła są **nie** zapisywane w następujących sytuacjach:

* **Nieobsługiwany operacji użytkowników końcowych**
  * Każdy użytkownik końcowy Resetowanie własnych haseł przy użyciu programu PowerShell v1, v2 lub interfejsu API programu Azure AD Graph
* **Nieobsługiwane operacje administratora**
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z [portalu zarządzania usługi Office](https://portal.office.com)
  * Wszystkie hasła przez użytkownika końcowego inicjowanych przez administratora zresetować z programu PowerShell v1, v2 lub interfejsu API programu Azure AD Graph

Gdy pracujemy, aby usunąć te ograniczenia, nie ma określonej osi czasu, który firma Microsoft może udostępniać jeszcze.

## <a name="password-writeback-security-model"></a>Model zabezpieczeń zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł jest usługą wysokim poziomie zabezpieczeń.  Aby upewnić się, że Twoje informacje są chronione, możemy Włącz model zabezpieczeń 4-warstwowy, które jest opisane poniżej.

* **Przekaźnik usługi service bus specyficznego dla dzierżawy**
  * Po skonfigurowaniu usługi skonfigurowanie specyficznego dla dzierżawy usługi przekazywania magistrali, która jest chroniona przez losowo generowany silne hasło, które firma Microsoft nigdy nie ma dostępu do.
* **Klucz szyfrowania zablokowaną, kryptograficznie silne hasło**
  * Po utworzeniu przekaźnik magistrali usług, utworzymy silnego klucza symetrycznego używanego do szyfrowania hasła, ponieważ pochodzi przez sieć. Ten klucz znajduje się tylko w sklepie tajny firmy w chmurze, które silnie jest zablokowany i inspekcji, podobnie jak wszystkie hasła w katalogu.
* **Branżowy standard TLS**
  1. Gdy hasło Resetowanie lub zmienianie operacja odbywa się w chmurze, możemy pobrać hasła w postaci zwykłego tekstu i szyfrowania kluczem publicznym.
  2. Możemy umieścić który w komunikatu protokołu HTTPS, który był wysyłany za pośrednictwem kanału szyfrowanego przy użyciu certyfikatów SSL firmy Microsoft do Twojej przekaźnik magistrali usługi.
  3. Po odebraniu komunikatu do usługi Service Bus agenta lokalnie budzi i uwierzytelnia się na magistrali usług przy użyciu silnego hasła, który wcześniej został wygenerowany.
  4. Agent lokalnymi przejmuje zaszyfrowanego komunikatu, odszyfrowuje je przy użyciu klucza prywatnego, możemy wygenerowany.
  5. Następnie lokalnego agenta próbuje ustawić hasła za pośrednictwem interfejsu API UstawianieHasła AD DS.
     * Ten krok jest, co umożliwia firmie Microsoft w celu wymuszenia użytkownika AD lokalne zasady haseł (złożoności, wieku, Historia, filtrami itp.) w chmurze.
* **Zasady wygasania wiadomości** 
  * Jeśli wiadomość znajduje się w usłudze Service Bus, ponieważ usługi lokalnej nie działa, przekroczy limit czasu i usunięte po kilku minutach, aby zwiększyć bezpieczeństwo jeszcze bardziej.

### <a name="password-writeback-encryption-details"></a>Szczegóły szyfrowania zapisywania zwrotnego haseł

Kroki szyfrowania żądanie zresetowania hasła przechodzi przez po przesłaniu przez użytkownika, zanim zostanie odebrane w środowisku lokalnymi w celu zapewnienia maksymalnej niezawodności i zabezpieczeń są opisane poniżej.

* **Krok 1 — hasło szyfrowania kluczem RSA 2048-bitowego** — po przesłaniu przez użytkownika hasła można zapisać zwrotnie do lokalnej, najpierw przesłane samego hasła są szyfrowane za pomocą klucza RSA 2048-bitowego.
* **Krok 2 — pakiet poziom szyfrowania z usługą GCM AES** — a następnie cały pakiet (hasło + wymaganych metadanych) są zaszyfrowane za pomocą usługi GCM AES. Zapobiega to każda osoba mająca bezpośredni dostęp do podstawowego kanału magistrali usług wyświetlanie/manipulowanie zawartością.
* **Krok 3 - cała komunikacja odbywa się za pośrednictwem protokołu TLS / SSL** -cała komunikacja z magistrali usług odbywa się w kanału SSL/TLS. To chroni zawartość z nieupoważnione 3.
* **Automatyczne Przerzucanie klucza co sześć miesięcy** — automatycznie co 6 miesięcy, lub za każdym razem, gdy funkcji zapisywania zwrotnego haseł jest wyłączony lub ponownie aktywne na Azure AD Connect, możemy przerzucania te klucze do zapewnienia bezpieczeństwa i zabezpieczeń maksymalnej.

### <a name="password-writeback-bandwidth-usage"></a>Wykorzystanie przepustowości zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł jest usługą niskiej przepustowości, która wysyła żądania do agenta lokalnie, tylko w następujących okolicznościach:

1. Dwa komunikaty wysyłane podczas włączania lub wyłączania funkcji za pośrednictwem usługi Azure AD Connect.
2. Jeden komunikat jest wysyłane co pięć minut jako pulsu usługi dla tak długo, jak usługa jest uruchomiona.
3. Dwa komunikaty są wysyłane poszczególnych czas przesłaniu nowego hasła
    * Pierwszy komunikat jako żądania do wykonania tej operacji
    * Drugi komunikat, który zawiera wynik operacji i są wysyłane w następujących okolicznościach:
        * Zawsze przesłaniu nowego hasła podczas użytkownika samoobsługowego resetowania hasła.
        * Zawsze przesłaniu nowego hasła podczas operacji zmiany hasła użytkownika.
        * Zawsze przesłaniu nowego hasła podczas resetowania (od administratora platformy Azure portali tylko) hasła użytkownika inicjowanych przez administratora.

#### <a name="message-size-and-bandwidth-considerations"></a>Zagadnienia dotyczące rozmiaru i przepustowości wiadomości

Rozmiar każdego komunikatu opisany powyżej jest zwykle w obszarze 1 kb, nawet w przypadku obciążeń skrajne, sama usługa zapisywania zwrotnego haseł zajmuje kilka kilobitów na sekundę przepustowości. Ponieważ każdy komunikat jest wysyłany w czasie rzeczywistym, tylko wtedy, gdy jest to wymagane przez operację aktualizacji hasła i jest tyle mały rozmiar komunikatu przepustowości możliwości zapisywania zwrotnego jest skutecznie za mały, aby miały rzeczywistym zauważalnego wpływu.

## <a name="next-steps"></a>Następne kroki

Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami
* [**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych
* [**Dostosowywanie**](active-directory-passwords-customize.md) — Dostosowywanie wyglądu i działania środowiska samoobsługowego resetowania haseł dla firmy
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? — Odpowiedzi na wszystkie nurtujące Cię pytania
* [**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Włączanie zapisywania zwrotnego haseł w programie Azure AD Connect"
