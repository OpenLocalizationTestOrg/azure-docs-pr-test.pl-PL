---
title: "Rozwiązywanie problemów z ustawieniami roamingu stanu przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Udostępnia toosome odpowiedzi na pytania Administratorzy IT mogą mieć o ustawieniach i synchronizacji danych aplikacji."
services: active-directory
keywords: "Enterprise mobilnego ustawienia stanu, chmury systemu windows, często zadawane pytania na roamingu stanu przedsiębiorstwa"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Rozwiązywanie problemów z ustawieniami roamingu stanu przedsiębiorstwa w usłudze Azure Active Directory

Ten temat zawiera informacje na temat tootroubleshoot i diagnozowanie problemów z roamingu stanu przedsiębiorstwa i udostępnia listę znanych problemów.

## <a name="preliminary-steps-for-troubleshooting"></a>Wstępne kroki rozwiązywania problemów 
Przed rozpoczęciem rozwiązywania problemów Sprawdź, czy hello użytkowników i urządzeń zostały skonfigurowane prawidłowo i czy wszystkie wymagania hello roamingu stanu przedsiębiorstwa są spełnione przez hello urządzeń i użytkowników hello. 

1. Windows 10 z hello najnowsze aktualizacje i minimalnej wersji 1511 (kompilacja systemu operacyjnego 10586 lub nowszym) jest zainstalowany na urządzeniu hello. 
2. urządzenie Hello jest usługi Azure AD dołączone do przyłączonych do domeny lub zarejestrowane w usłudze Azure AD.
3. W portalu usługi Azure Active Directory hello **roamingu stanu przedsiębiorstwa** jest włączone w katalogu hello **Konfiguruj** > **urządzeń**  >  **Użytkownicy mogą synchronizować ustawienia i dane aplikacji przedsiębiorstwa**. Wszyscy użytkownicy są wybrane, albo hello użytkownika jest włączone dla synchronizacji za pomocą opcji hello wybrane i się w grupie zabezpieczeń hello.
4. Użytkownik Hello ma subskrypcji platformy Azure Active Directory Premium przypisane toothem.  
5. ponowne uruchomienie urządzenia Hello i hello zalogowaniu się użytkownika po włączeniu opcji roamingu stanu przedsiębiorstwa.

## <a name="information-tooinclude-when-you-need-help"></a>Informacje o tooinclude, gdy będziesz potrzebować pomocy
Jeśli nie możesz rozwiązać problemu z poniższe wskazówki hello, możesz skontaktować się naszego pracowników działu pomocy technicznej. Możesz skontaktować się z nimi zaleca hello tooinclude następujących informacji:

- **Ogólny opis błędu hello** — są widoczne dla użytkowników hello komunikaty o błędach? Jeśli nie istnieje żaden komunikat o błędzie, opisano hello nieoczekiwanego zachowania, możesz zauważyć szczegółowo. Jakie funkcje są włączone do celów synchronizacji, a co jest oczekiwany toosync użytkownika hello? Wiele funkcji nie synchronizacji lub jest tooone izolowane it?
- **Użytkownicy, których to dotyczy** — jest synchronizacja pracy/niepowodzeniem dla jednego użytkownika lub wielu użytkowników? Ile urządzeń są zaangażowane na użytkownika? Są je nie synchronizuje wszystkie lub niektóre z nich synchronizowania i niektóre nie synchronizuje?
- **Informacje o użytkowniku hello** — jakie tożsamość jest hello użytkownika przy użyciu toolog toohello urządzenia? Jak jest hello użytkownik loguje się toohello urządzenia? Są one częścią wybranej grupy zabezpieczeń mogą toosync? 
- **Informacje o urządzeniu hello** — jest to urządzenie Joined usługi Azure AD lub przyłączonych do domeny? Na jakie kompilacji jest hello urządzenia? Jakie są najnowsze aktualizacje hello?
- **Daty i godziny / strefy czasowej** — jaka była hello dokładnej daty i czasu był wyświetlany błąd hello (Dołącz hello strefy czasowej)?
- Te informacje w tym pomoże nam w możliwie najkrótszym czasie rozwiązać tego problemu.

## <a name="troubleshooting-and-diagnosing-issues"></a>Rozwiązywanie problemów i diagnozowanie problemów
W tej sekcji przedstawiono sugestie dotyczące tootroubleshoot i diagnozowanie problemów tooEnterprise powiązane roamingu stanu.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Sprawdź synchronizacji, a Witaj "Synchronizuj swoje ustawienia" Ustawienia strony 

1. Po dołączeniu tooa Twojego komputera z systemem Windows 10 domeny, która jest skonfigurowana tooallow roamingu stanu przedsiębiorstwa, logowania za pomocą swojego konta służbowego. Przejdź za**ustawienia** > **kont** > **ustawień synchronizacji** i Potwierdź, że poszczególne ustawienia synchronizacji i hello są i że hello u góry Strona Ustawienia Hello wskazuje, że trwa synchronizacja z kontem służbowym. Potwierdź hello tego samego konta jest również używane jako konto logowania w **ustawienia** > **kont** > **Twoje informacje**. 
2. Sprawdź, czy synchronizacja działa na wielu komputerach, wprowadzając niektóre zmiany na maszynie oryginalnego hello, takie jak przeniesienie hello zadań toohello prawej lub górnej krawędzi hello ekranu. Obejrzyj zmiany hello propagację toohello drugiej maszyny w ciągu pięciu minut. 
 - Blokowanie i odblokowywanie ekranie powitania (Win + L) może ułatwić wyzwalanie synchronizacji.
 - Należy używać tego samego konta logowania na obu komputerach przeznaczonych do synchronizacji toowork — Witaj, roamingu stanu przedsiębiorstwa jest wiązana toohello konta użytkownika i konto komputera nie hello.

**Potencjalny problem**: hello ustawienia strony ma przełącza hello wyszarzone, a zamiast konta, zostanie wyświetlony tekst hello "niektórymi funkcjami systemu Windows są dostępne, jeśli używasz konta Microsoft lub konta służbowego". Ten problem może wystąpić dla urządzeń, które zostały skonfigurowane toobe przyłączonych do domeny i zarejestrowane tooAzure AD, ale urządzenie hello nie został pomyślnie uwierzytelniony tooAzure AD. Możliwą przyczyną jest hello urządzenia zasad należy zastosować, że ta aplikacja asynchroniczne i może zostać opóźnione przez kilka godzin. Sprawdź ten problem, wykonaj kroki hello tooverify hello toocheck stanu rejestracji urządzenia hello przypadku.

### <a name="verify-hello-device-registration-status"></a>Sprawdź stan rejestracji urządzenia hello
Roamingu stanu przedsiębiorstwa wymaga hello toobe urządzenia zarejestrowane w usłudze Azure AD. Chociaż nie dotyczą tooEnterprise roamingu stanu instrukcjami hello poniżej pomaga upewnij się, że powitania klienta systemu Windows 10 jest zarejestrowany i Potwierdź odcisku palca, adres URL ustawienia usługi Azure AD, stan NGC oraz inne informacje.

1.  Witaj Otwórz wiersz polecenia wyrównano. toodo to w systemie Windows, otwórz hello uruchamiania wykonywania (Win + R), a następnie wpisz tooopen "cmd".
2.  Po otwarciu hello wiersza polecenia, wpisz "*/status dsregcmd.exe*".
3.  Dla oczekiwane dane wyjściowe, hello **AzureAdJoined** wartość pola powinna być "Tak", **WamDefaultSet** wartości pola powinny być "Tak" i hello **WamDefaultGUID** wartość pola powinna być Identyfikator GUID z "(AzureAd)" na końcu hello.

**Potencjalny problem**: **WamDefaultSet** i **AzureAdJoined** zarówno "Nie" mają wartość pola hello, hello urządzenie zostało przyłączone do domeny i zarejestrowane w usłudze Azure AD i urządzenia hello synchronizacji. Jeśli jest on wyświetlany, hello urządzenie może potrzebę toowait toobe zasady stosowane lub hello uwierzytelniania hello urządzenia nie powiodła się podczas nawiązywania połączenia tooAzure AD. Witaj użytkownika może być toowait hello toobe zasady zastosowane po kilku godzinach. Z procedurą rozwiązywania problemów mogą obejmować ponawianie próby rejestracji automatycznej przez podpisywania, wyloguj się i ponownie lub uruchamiania zadań hello w harmonogramie zadań. W niektórych przypadkach uruchomiona "*dsregcmd.exe /leave*" w oknie wiersza polecenia z podwyższonym poziomem uprawnień, ponowny rozruch i podjęcie ponownej próby rejestracji mogą pomoc dotyczącą tego problemu.


**Potencjalny problem**: pole hello **AzureAdSettingsUrl** jest pusty i hello urządzenia nie synchronizacji. hello użytkownika może ostatnio zalogowali się toohello urządzenia przed włączeniem roamingu stanu przedsiębiorstwa w hello Azure Active Portal katalogu. Uruchom ponownie urządzenie hello i mieć hello dane logowania użytkownika. Opcjonalnie w portalu hello spróbuj o hello administrator IT wyłączenie i ponowne włączenie użytkownicy mogą synchronizacji ustawień i danych aplikacji przedsiębiorstwa. Po ponownie włączona, ponowne uruchomienie urządzenia hello i mieć hello dane logowania użytkownika. Jeśli to nie rozwiąże problemu hello **AzureAdSettingsUrl** może być pusty w przypadku hello certyfikatu zły urządzenia. W takim przypadku uruchomiona "*dsregcmd.exe /leave*" w oknie wiersza polecenia z podwyższonym poziomem uprawnień, ponowny rozruch i podjęcie ponownej próby rejestracji mogą pomoc dotyczącą tego problemu.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Roaming stanu przedsiębiorstwa i uwierzytelniania wieloskładnikowego 
W niektórych warunkach roamingu stanu przedsiębiorstwa toosync danych w przypadku w trybie Azure Multi-Factor Authentication jest skonfigurowany. Dodatkowe szczegóły dotyczące tych symptomów, zobacz dokument pomocy technicznej hello [KB3193683](https://support.microsoft.com/kb/3193683). 

**Potencjalny problem**: Jeśli urządzenie jest skonfigurowane toorequire uwierzytelnianie wieloskładnikowe w portalu usługi Azure Active Directory hello, może się nie ustawienia toosync podczas podpisywania w urządzeniu tooa systemu Windows 10 przy użyciu hasła. Ten typ konfiguracji usługi Multi-Factor Authentication jest zamierzone tooprotect konto administratora platformy Azure. Użytkownicy Administratorzy może nadal być toosync stanie po zarejestrowaniu się w urządzeniach tootheir systemu Windows 10 z ich Microsoft Passport dla numeru PIN pracy lub wykonując uwierzytelnianie wieloskładnikowe podczas uzyskiwania dostępu do innych usług Azure, takich jak usługi Office 365.

**Potencjalny problem**: synchronizacja może zakończyć się niepowodzeniem, jeśli Witaj, Administratorze konfiguruje zasady dostępu warunkowego hello uwierzytelniania wieloskładnikowego usług federacyjnych Active Directory i wygaśnięcia tokenu dostępu hello na urządzeniu hello. Upewnij się zalogujesz, wyloguj się przy użyciu hello Microsoft Passport dla pracy numeru PIN lub wykonać uwierzytelnianie wieloskładnikowe podczas uzyskiwania dostępu do innych usług Azure, takich jak usługi Office 365.

###<a name="event-viewer"></a>Podgląd zdarzeń
Do zaawansowanego rozwiązywania problemów, Podgląd zdarzeń mogą być używane toofind określonych błędów. Te są opisane w poniższej tabeli hello. zdarzenia Hello można znaleźć w Podglądzie zdarzeń > Dzienniki aplikacji i usług > **Microsoft** > **Windows** > **SettingSync** i w przypadku problemów z synchronizacją tożsamości **Microsoft** > **Windows** > **usługi Azure AD**.


## <a name="known-issues"></a>Znane problemy

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>Synchronizacja nie działa na urządzeniach, które znajdują się aplikacje ładowana za pomocą oprogramowania MDM

Wpływa na urządzeniach z systemem hello systemu Windows 10 Anniversary aktualizacji (wersji 1607). W Podglądzie zdarzeń w obszarze dzienniki SettingSync Azure hello hello 6013 identyfikator zdarzenia z powodu błędu 80070259 często jest widoczny.

**Zalecana akcja**  
Upewnij się, że hello systemu Windows 10 v1607 klient ma hello 23 sierpnia 2016 aktualizacji zbiorczej ([KB3176934](https://support.microsoft.com/kb/3176934) 14393.82 kompilacji systemu operacyjnego). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Ulubione programu Internet Explorer synchronizacji.

Wpływa na urządzeniach z systemem hello systemu Windows 10 listopada aktualizację (wersja 1511).

**Zalecana akcja**  
Upewnij się, że hello systemu Windows 10 v1511 klient ma hello lipca 2016 aktualizacji zbiorczej ([KB3172985](https://support.microsoft.com/kb/3172985) 10586.494 kompilacji systemu operacyjnego).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Nie jest synchronizowany motywu, a także dane chronione przy użyciu systemu Windows Information Protection 

tooprevent wycieku danych, danych, który jest chroniony za pomocą [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) zostanie zsynchronizowany przy użyciu roamingu stanu przedsiębiorstwa dla urządzeń przy użyciu hello systemu Windows 10 Anniversary aktualizacji.



**Zalecana akcja**  
Brak. Przyszłe aktualizacje tooWindows może rozwiązać ten problem.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>Ustawienia daty, godziny i Region nie synchronizowane na urządzeniu przyłączonym do domeny 
  
Urządzenia, które są przyłączone do domeny nie będzie działać z synchronizacji dla hello ustawienie daty, godziny i regionu: automatyczne czasu. Za pomocą czasu automatycznego może zastąpienie hello inne ustawienia daty, godziny i regionu i spowodować, że te ustawienia nie toosync. 

**Zalecana akcja**  
Brak. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>Podczas synchronizacji haseł monitów kontroli konta użytkownika

Wpływa na urządzeniach z systemem hello systemu Windows 10 listopada aktualizację (wersja 1511) z sieci bezprzewodowej karty Sieciowej, która jest skonfigurowana toosync hasła.

**Zalecana akcja**  
Upewnij się, że hello systemu Windows 10 v1511 klient ma hello aktualizacji zbiorczej ([KB3140743](https://support.microsoft.com/kb/3140743) 10586.494 kompilacji systemu operacyjnego).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>Synchronizacja nie działa na urządzeniach, które użycie karty inteligentnej do logowania
Jeśli próba toosign tooyour urządzenia z systemem Windows przy użyciu karty inteligentnej lub wirtualnej karty inteligentnej, ustawienia synchronizacji przestanie działać.     

**Zalecana akcja**  
Brak. Przyszłe aktualizacje tooWindows może rozwiązać ten problem.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>Urządzenia przyłączone do domeny nie jest synchronizowany po opuszczeniu sieci firmowej     
Przyłączonych do domeny urządzenia zarejestrowane tooAzure AD może wystąpić błąd synchronizacji, jeśli urządzenie hello jest poza nim przez dłuższy czas i nie może ukończyć uwierzytelniania domeny.

**Zalecana akcja**  
Tak, aby wznowić synchronizację, należy połączyć z sieci firmowej tooa hello urządzenia.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Azure AD Joined urządzenie nie jest synchronizowany, a użytkownik hello ma mieszane przypadku nazwa główna użytkownika.
 Jeśli użytkownik hello jest na urządzeniu Joined usługi Azure AD, który został uaktualniony z systemu Windows 10 kompilacji 10586 too14393 hello użytkownik ma mieszane przypadku głównej nazwy użytkownika (np. nazwę użytkownika zamiast nazwy użytkownika), hello na urządzeniu użytkownika może się nie powieść toosync. 

**Zalecana akcja**  
Witaj użytkownika należy toounjoin, a następnie ponowne przyłączenie hello urządzenia toohello chmury. toodo, zaloguj się jako hello użytkownika administratora lokalnego i odłączanie urządzenia hello przechodząc zbyt**ustawienia** > **systemu** > **o** i wybierz pozycję " Zarządzaj lub Odłącz od pracy lub nauki." Czyszczenie plików hello poniżej, a następnie Azure AD Join hello urządzenia ponownie w **ustawienia** > **systemu** > **o** i wybierając pozycję "Connect tooWork lub szkoły". Kontynuuj toojoin hello urządzenia tooAzure usługi Active Directory i hello ukończenia przepływu.

W kroku hello oczyszczania hello oczyszczania następujące pliki:
- Settings.dat w`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Witaj wszystkie pliki w folderze hello`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>Identyfikator zdarzenia 6065:80070533 przez tego użytkownika nie może zalogować, ponieważ to konto jest obecnie wyłączona.  
W Podglądzie zdarzeń w obszarze dzienniki SettingSync/Debug hello ten błąd może być widoczny podczas poświadczenia użytkownika hello wygasły. Ponadto może wystąpić, gdy hello dzierżawy nie miał automatycznie AzureRMS udostępnione. 

**Zalecana akcja**  
W pierwszym przypadku hello mają użytkownika hello, zaktualizuj swoje poświadczenia i urządzenia toohello logowania z nowymi poświadczeniami hello. Witaj toosolve problem AzureRMS kontynuować hello czynności opisane w [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>Identyfikator zdarzenia 1098: Błąd: 0xCAA5001C Token brokera operacja nie powiodła się  
W Podglądzie zdarzeń w obszarze dzienniki AAD/Operational hello tego błędu mogą być widoczne z 1104 zdarzeń: wywołanie wtyczki region chmury AAD token operacji Get zwróciło błąd: 0xC000005F. Ten problem występuje, gdy brakuje uprawnienia lub prawa własności atrybutów.    

**Zalecana akcja**  
Kontynuuj kroki hello [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Następne kroki

- Użyj hello [forum User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) tooprovide opinii i udostępnić sugestie dotyczące jak tooimprove Enterprise stanu mobilnego.

- Aby uzyskać więcej informacji, zobacz hello [opis roamingu stanu przedsiębiorstwa](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Powiązane tematy
* [Przegląd roamingu stanu przedsiębiorstwa](active-directory-windows-enterprise-state-roaming-overview.md)
* [Włącz roaming stanu przedsiębiorstwa w usłudze Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Ustawienia i dane mobilne — często zadawane pytania](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Zasady grupy i ustawienia zarządzania urządzeniami Przenośnymi dla ustawień synchronizacji](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Informacje dotyczące ustawień roamingu systemu Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
