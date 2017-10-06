---
title: "Azure Active Directory Connect: Często zadawane pytania dotyczące - | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera często zadawane pytania dotyczące usługi Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Często zadawane pytania dotyczące usługi Azure Active Directory Connect

## <a name="general-installation"></a>Ogólne instalacji
**Pytanie: czy będzie instalacji działać, jeśli hello Azure AD administratora globalnego ma 2FA włączone?**  
Z kompilacjami powitania od lutego 2016 jest to obsługiwane.

**Pytanie: czy istnieje tooinstall sposób Azure AD Connect nienadzorowanej?**  
Jest tylko obsługiwana tooinstall Azure AD Connect przy użyciu Kreatora instalacji hello. Instalacja nienadzorowana i dyskretnej nie jest obsługiwana.

**Pytanie: czy masz lasu, gdy nie można skontaktować się z jednej domeny. Jak zainstalować usługi Azure AD Connect?**  
Z kompilacjami powitania od lutego 2016 jest to obsługiwane.

**Pytanie: czy hello pracy agenta kondycji usług AD DS w instalacji server core?**  
Tak. Po zainstalowaniu agenta hello, można ukończyć procesu rejestracji hello za pomocą następującego polecenia cmdlet programu PowerShell hello: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Sieć
**Pytanie: czy mam zapory, urządzenia sieciowego lub czegoś innego, która ogranicza hello maksymalny czas połączenia pozostają otwarte w sieci. Jak długo Moje próg limitu czasu po stronie klienta należy przy użyciu usługi Azure AD Connect?**  
Całe oprogramowanie sieciowe, urządzenia fizyczne lub jakikolwiek inny limity hello maksymalnego czasu połączenia może pozostawać otwarte powinien używać progu co najmniej 5 minut (300 sekund) do obsługi łączności między hello serwer, gdzie hello klienta usługi Azure AD Connect jest zainstalowany i Azure Active Directory. Dotyczy to również narzędzia synchronizacji pakietu Microsoft Identity tooall wydane wcześniej.

**Pytanie: czy domeny drugiego poziomu (jednej etykiety domen) obsługiwane?**  
Nie, usługi Azure AD Connect nie obsługuje lokalnymi lasami/domenami przy użyciu drugiego poziomu.

**Pytanie: czy "kropkami" o nazwie NetBios obsługiwane?**  
Nie, usługi Azure AD Connect nie obsługuje lokalnymi lasami/domenami, których nazwa NetBios hello zawiera kropkę "." w nazwie hello.

## <a name="federation"></a>Federacyjna
**Pytanie: co zrobić, jeśli otrzymuję wiadomość e-mail, który monit toorenew certyfikatu usługi Office 365**  
Użyj wskazówek hello, opisaną w hello [odnawiania certyfikatów](active-directory-aadconnect-o365-certs.md) tematu w sposób toorenew hello certyfikatu.

**Pytanie: czy masz "Automatycznie Aktualizuj jednostki uzależnionej" dla jednostki uzależnionej usługi Office 365. Należy tootake żadnych działań po Moje token certyfikatu podpisywania automatycznie najedzie na?**  
Użyj wskazówek hello, opisaną w artykule hello [odnawiania certyfikatów](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Środowisko
**Pytanie: jest obsługiwane it toorename powitania serwera po zainstalowaniu usługi Azure AD Connect?**  
Nie. Zmiana nazwy serwera hello toonot aparatu synchronizacji hello Przyczyna będą mogli tooconnect toohello SQL database i hello usługi nie będą mogli toostart.

## <a name="identity-data"></a>Danych tożsamości
**Pytanie: hello atrybut nazwy UPN (userPrincipalName) w usłudze Azure AD nie odpowiada hello UPN lokalnego — Dlaczego?**  
Zobacz następujące artykuły:

* [Nazwy użytkowników nie są zgodne w usłudze Office 365, Azure lub Intune hello lokalną nazwą UPN lub alternatywnym Identyfikatorem logowania](https://support.microsoft.com/en-us/kb/2523192)
* [Zmiany nie są synchronizowane przez narzędzie do synchronizacji usługi Azure Active Directory powitania po zmianie hello UPN toouse konto użytkownika innej domeny federacyjnej](https://support.microsoft.com/en-us/kb/2669550)

Można również skonfigurować userPrincipalName hello tooupdate aparatu synchronizacji usługi Azure AD tooallow hello zgodnie z opisem w [funkcji Usługa synchronizacji Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**Pytanie: jest it obsługiwane toosoft dopasowania lokalnych obiektów grupy AD skontaktuj się z obiektami usługi Azure AD grupy/skontaktuj się z istniejącą?**  
Nie jest to obecnie nieobsługiwane.

**P: jest toomanually it obsługiwane atrybut nazwę ImmutableId na istniejące usługi Azure AD grupy/skontaktuj się z obiektów toohard dopasowanie tooon lokalnych obiektów grupy AD skontaktuj się z?**  
Nie jest to obecnie nieobsługiwane.



## <a name="custom-configuration"></a>Konfiguracja niestandardowa
**Pytanie: gdzie są polecenia cmdlet programu PowerShell hello Azure AD Connect udokumentowane?**  
Z wyjątkiem hello poleceń cmdlet hello opisane w tej lokacji innych poleceń cmdlet programu PowerShell znaleziono w programie Azure AD Connect nie są obsługiwane przez klienta.

**Pytanie: czy można użyć "Serwera serwer eksportu/importu" znaleziony w *Menedżera usługi synchronizacji* konfiguracji toomove między serwerami?**  
Nie. Ta opcja nie pobierze wszystkie ustawienia konfiguracji i nie powinna być używana. Zamiast tego należy użyć konfiguracji podstawowej hello toocreate kreatora hello na drugim serwerze hello i użyć reguły synchronizacji hello Edytor toomove skryptów PowerShell toogenerate wszystkie reguły niestandardowej między serwerami. Zobacz [migracji w kierunku](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**Pytanie: hasła można buforować strony hello Azure logowania i może to być zablokowana, ponieważ zawiera element input hasła Autouzupełnianie hello = "false" atrybutu?**</br>
Obecnie nie obsługujemy modyfikowania atrybutów HTML hello pola wejściowego hasła hello, tym hello autouzupełniania tagu. Obecnie pracujemy funkcja, która pozwoli niestandardowych skryptów Javascript, co pozwoli tooadd wszystkie pola atrybutu toohello hasła. Powinna to być nowsze część 2017 r.

**P: na hello Azure strony logowania są wyświetlane nazwy użytkowników dla użytkowników, którzy wcześniej zalogowali się pomyślnie.  Można to zachowanie wyłączyć?**</br>
Obecnie nie obsługujemy modyfikowanie hello atrybuty HTML strony logowania hello. Obecnie pracujemy funkcja, która pozwoli niestandardowych skryptów Javascript, co pozwoli tooadd wszystkie pola atrybutu toohello hasła. Powinna to być nowsze część 2017 r.

**Pytanie: czy istnieje tooprevent sposób równoczesnych sesji?**</br>
Nie.



## <a name="troubleshooting"></a>Rozwiązywanie problemów
**Pytanie: jak uzyskać pomoc dotyczącą usługi Azure AD Connect?**

[Witaj wyszukiwania bazy wiedzy Microsoft Knowledge Base (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Witaj wyszukiwania bazy wiedzy Microsoft Knowledge Base (KB) dla rozwiązań technicznych toocommon naprawa w razie awarii problemy dotyczące pomocy technicznej programu Azure AD Connect.

[Fora dotyczące usługi Active Directory platformy Microsoft Azure](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Można wyszukiwać i wyszukać technicznych pytania i odpowiedzi od społeczności hello lub zadać pytanie własne klikając [tutaj](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Dział obsługi klienta usługi Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Użyj tej obsługi tooget łącza za pomocą hello portalu Azure.

