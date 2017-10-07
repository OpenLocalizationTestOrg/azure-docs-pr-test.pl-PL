---
title: "aaaAzure Active Directory Connect kondycji — często zadawane pytania - Azure | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania odpowiedzi na pytania dotyczące usługi Azure AD Connect Health. Często zadawane pytania obejmuje pytania dotyczące korzystania z usługi hello, w tym hello rozliczeń modelu, możliwości, ograniczeń i pomocy technicznej."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Azure AD Connect Health — często zadawane pytania
Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania (FAQ) dotyczące usługi Azure Active Directory (Azure AD) Connect Health. Te często zadawane pytania dotyczące pokrycia pytania dotyczące sposobu toouse hello usługi, która obejmuje hello rozliczeń modelu, możliwości, ograniczeń i pomocy technicznej.

## <a name="general-questions"></a>Pytania ogólne
**Pytanie: czy mogę zarządzać wielu katalogów usługi Azure AD. Jak zmienić toohello, który ma Azure Active Directory Premium?**

tooswitch między różnymi dzierżawy usługi Azure AD, wybierz hello obecnie zalogowany **nazwy użytkownika** na hello prawym górnym rogu, a następnie wybierz odpowiednie konto hello. Jeśli hello konto nie ma na liście, wybierz **Wyloguj**, a następnie użyj poświadczeń administratora globalnego hello hello katalogu, który ma Azure Active Directory Premium włączony toosign w.

**Pytanie: jakie wersji role są obsługiwane przez program Azure AD Connect Health tożsamości?**

Witaj poniższej tabeli wymieniono role hello i obsługiwanych wersjach systemu operacyjnego.

|Rola| System operacyjny / wersji|
|--|--|
|Usługi federacyjne Active Directory (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Program Azure AD Connect | Wersja 1.0.9125 lub nowszej|
|Usługi domenowe Active Directory (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Należy pamiętać, że hello funkcji udostępnianych przez usługę hello może różnić się na podstawie roli hello i hello systemu operacyjnego. Innymi słowy wszystkie funkcje hello mogą być dostępne dla wszystkich wersji systemu operacyjnego. Zobacz opis funkcji hello szczegółowe informacje.

**Pytanie: jak liczby licencji czy potrzebuję toomonitor Moje infrastruktury?**

* Witaj pierwszego połączenia agenta kondycji wymaga co najmniej jedną licencję usługi Azure AD Premium.
* Każdy agent, dodatkowe zarejestrowane wymaga 25 dodatkowe licencje usługi Azure AD Premium.
* Liczba agentów jest równoważne toohello łączna liczba agentów, które są zarejestrowane przez wszystkie role monitorowanych (usług AD FS, Azure AD Connect lub usług AD DS).

Informacje o licencji znajduje się także na powitania [strony cennik usługi Azure AD](https://aka.ms/aadpricing).

Przykład:

| Zarejestrowany agentów | Potrzebnych licencji | Przykładowa konfiguracja monitorowania |
| ------ | --------------- | --- |
| 1 | 1 | 1 serwer azure AD Connect |
| 2 | 26| 1 serwera azure AD Connect i kontrolera domeny 1 |
| 3 | 51 | 1 serwer usługi active Directory Federation Services (AD FS), 1, AD FS z serwera proxy i kontrolera domeny 1 |
| 4 | 76 | Serwera 1 AD FS, 1, AD FS z serwera proxy i 2 kontrolerów domeny |
| 5 | 101 | 1 serwer azure AD Connect, serwera 1 AD FS 1 AD FS z serwera proxy i 2 kontrolerów domeny |


## <a name="installation-questions"></a>Pytania dotyczące instalacji

**Pytanie: co to jest wpływ hello instalowanie hello Azure AD Connect Health Agent na poszczególnych serwerach?**

Instalowanie serwerów proxy aplikacji sieci web Microsoft Azure AD Connect Agent kondycji, usługi AD FS hello, Azure AD Connect (synchronizacja) serwery, kontrolery domeny wpływ Hello jest minimalnym z względem toohello Procesora, wykorzystanie pamięci przepustowości sieci i magazynu.

Witaj następującej liczby są zbliżenia:

* Użycie procesora CPU: Zwiększ ~ 1-5%.
* Zużycie pamięci: % too10 hello całkowitej pamięci systemu.

> [!NOTE]
> Jeśli hello agent nie może komunikować się z platformy Azure, hello agent przechowuje dane hello lokalnie zdefiniowany maksymalny limit. Hello agent zastępuje hello "" buforowane na zasadzie "najdawniej obsługiwane".
>
>

* Bufor lokalnego magazynu dla usługi Azure AD Connect agentów kondycji: ~ 20 MB.
* Serwery usług AD FS zaleca się, że udostępnieniem miejsca 1024 MB (1 GB) dla kanału inspekcji hello usług AD FS dla usługi Azure AD Connect agentów kondycji tooprocess wszystkich danych inspekcji hello zanim zostanie on zastąpiony.

**P: będzie konieczne tooreboot Moje serwery podczas instalacji agentów hello Azure AD Connect Health hello?**

Nie. Instalacja Hello hello agentów nie wymagają tooreboot powitania serwera. Niektóre wstępnie wymagane kroki instalacji mogą jednak wymagać ponownego uruchomienia serwera hello.

Na przykład systemu Windows Server 2008 R2, instalacja programu .NET 4.5 Framework wymaga ponownego uruchomienia serwera.

**Pytanie: czy Azure AD Connect Health pracy za pośrednictwem przekazujący serwer proxy HTTP?**

Tak. Dla bieżących operacji można skonfigurować toouse agenta kondycji hello wychodzących żądań HTTP HTTP serwera proxy tooforward.
Przeczytaj więcej na temat [Konfigurowanie serwera HTTP Proxy dla agentów kondycji](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Jeśli potrzebujesz tooconfigure serwera proxy podczas rejestracji agenta, może zaistnieć toomodify ustawienia serwera Proxy programu Internet Explorer wcześniej.

1. Otwórz program Internet Explorer > **ustawienia** > **Opcje internetowe** > **połączeń** > **ustawienia sieci LAN**.
2. Wybierz **Użyj serwera Proxy dla sieci LAN**.
3. Wybierz **zaawansowane** Jeśli porty na inny serwer proxy dla protokołu HTTP i HTTPS/Secure.

**Pytanie: czy uwierzytelnianie podstawowe pomocy technicznej usługi Azure AD Connect Health, łącząc tooHTTP proxy?**

Nie. Mechanizm toospecify nazwa dowolnego użytkownika i hasło dla uwierzytelniania podstawowego nie jest obecnie obsługiwane.

**Pytanie: co zrobić porty zapory potrzebuje tooopen hello Azure AD Connect Agent kondycji toowork?**

Zobacz hello [sekcji wymagania](active-directory-aadconnect-health-agent-install.md#requirements) hello lista portów zapory i inne wymagania dotyczące łączności.

**Pytanie: Dlaczego Zobacz dwa serwery z hello takie same nazwy hello Azure AD Connect Health portalu?**

Po usunięciu agenta z serwera powitania serwera nie jest automatycznie usunięte z portalu Azure AD Connect Health hello. Ręcznie usuń agenta z serwera lub usunąć hello sam serwer, należy najpierw toomanually delete powitania serwera wpis hello Azure AD Connect Health portalu.

Można odtworzyć serwer lub Utwórz nowy serwer z hello tego samego szczegółów (takich jak nazwa komputera). Jeśli nie usunięto hello już zarejestrowanego serwera z hello Azure AD Connect Health portalu, a hello agenta jest zainstalowane na nowym serwerze hello, mogą pojawić dwóch wpisów z hello tej samej nazwy.

W takim przypadku ręcznie usunąć wpis hello, który należy toohello starszym serwerze. Witaj dane dla tego serwera powinny być nieaktualne.

## <a name="health-agent-registration-and-data-freshness"></a>Agent kondycji świeżości rejestracji i danych

**Pytanie: jakie są typowe przyczyny niepowodzenia rejestracji agenta kondycji hello i sposób rozwiązywania problemów?**

Witaj agenta kondycji może zakończyć się niepowodzeniem tooregister powodu toohello następujące możliwe przyczyny:

* Hello agenta nie może komunikować się z punktami końcowymi hello wymagane, ponieważ Zapora blokuje ruch. Jest to szczególnie wspólnej na serwerach proxy aplikacji sieci web. Upewnij się, że zezwolono punkty końcowe wymagane toohello komunikacji wychodzącej i porty. Zobacz hello [sekcji wymagania](active-directory-aadconnect-health-agent-install.md#requirements) szczegółowe informacje.
* Komunikacji wychodzącej jest poddane tooan SSL wglądu hello warstwy sieci. Powoduje to, że certyfikat hello hello agent używa toobe zastępuje hello inspekcji serwera na jednostkę, czy niepowodzeniem hello kroki toocomplete hello agenta rejestracji.
* Witaj użytkownik nie ma dostępu tooperform hello rejestracji hello agenta. Administratorzy globalni mają dostęp domyślnie. Można użyć [kontroli dostępu opartej na rolach](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate tooother użytkowników.

**Pytanie: czy mogę am uzyskiwanie alertów czy "dane usługi kondycji nie jest zapasowej toodate." Jak rozwiązać problem hello?**

Azure AD Connect Health generuje hello alert w przypadku nie otrzyma wszystkie punkty danych hello z serwera hello w hello ostatnich dwóch godzin. Może istnieć wiele przyczyn, dla tego alertu.

* Hello agenta nie może komunikować się z punktami końcowymi hello wymagane, ponieważ Zapora blokuje ruch. Jest to szczególnie wspólnej na serwerach proxy aplikacji sieci web. Upewnij się, mogą się z punktów końcowych toohello wymagane komunikacji wychodzącej i portów. Zobacz hello [sekcji wymagania](active-directory-aadconnect-health-agent-install.md#requirements) szczegółowe informacje.
* Komunikacji wychodzącej jest poddane tooan SSL wglądu hello warstwy sieci. Powoduje to, że certyfikat hello hello agent używa toobe zastępuje hello inspekcji serwera na jednostkę, czy hello niepowodzenia usługi Azure AD Connect Health toohello danych tooupload.
* Możesz użyć polecenia łączności hello wbudowane hello agenta. [Dowiedz się więcej](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* agenci Hello obsługują także łączność wychodząca za pośrednictwem nieuwierzytelnione serwer HTTP Proxy. [Dowiedz się więcej](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Pytania dotyczące działań
**Pytanie: należy tooenable inspekcji na serwerach proxy aplikacji sieci web hello?**

Nie, inspekcja nie jest konieczne toobe włączone na serwerach proxy aplikacji sieci web hello.

**Pytanie: jak uzyskać rozwiązane alerty dotyczące kondycji połączenia usługi Azure AD?**

Alerty usługi Azure AD Connect Health uzyskać rozwiązane na stan powodzenia. Azure AD Connect agentów kondycji wykrywa i okresowo raportują hello Powodzenie warunki toohello usługi. Kilka alertów pomijanie hello jest oparte na czasie. Innymi słowy Jeśli hello tego samego błędu nie jest przestrzegana w 72 godziny od Generowanie alertów, hello alert jest automatycznie rozwiązany.

**Pytanie: czy mogę am pobierania alerty czy "Test żądania uwierzytelniania (transakcja syntetyczna) nie powiodło się tooobtain token." Jak rozwiązać problem hello?**

Azure AD Connect Health dla usług AD FS generuje ten alert w przypadku hello zainstalowanego na serwerze usług AD FS agenta kondycji zakończy się niepowodzeniem tooobtain token jako część transakcji syntetycznych inicjowane przez hello Agent kondycji. agent kondycji Hello używa kontekstu systemu lokalnego hello i próbuje tooget token dla samej siebie jednostki uzależnionej. Jest to tooensure wychwytywania testu, będącą w stanie wystawiania tokenów usług AD FS.

W większości przypadków tego testu nie działa, ponieważ nazwy farmy usług AD FS hello tooresolve jest hello Agent kondycji. Może to nastąpić, jeśli hello AD FS serwery są za moduły równoważenia obciążenia sieciowego i żądania hello pobiera inicjowany z węzła, który jest za hello równoważenia obciążenia (co min. tooa regularne klienta, który jest przed hello modułu równoważenia obciążenia). Można to naprawiony przez zaktualizowanie pliku hello "hosts" znajduje się w obszarze "C:\Windows\System32\drivers\etc" tooinclude hello adres IP serwera usług AD FS hello lub adresem IP sprzężenia zwrotnego (127.0.0.1) dla nazwy farmy usług AD FS hello (np. sts.contoso.com). Dodawanie pliku hosta hello będzie zwarcia wywołania sieci hello, dzięki czemu hello agenta kondycji tooget hello tokenu.

**Pytanie: otrzymano wiadomość e-mail wskazujący, że moje maszyny nie są poprawiono hello ostatnie ransomeware atakami. Dlaczego otrzymuję ten adres e-mail?**

Usługa Azure AD Connect Health skanowane wszystkie powitalne maszyny monitoruje tooensure hello wymagane poprawki zostały zainstalowane. Witaj wiadomość e-mail została wysłana toohello Administratorzy dzierżawy, jeśli co najmniej jeden komputer nie miał hello krytycznych poprawek. Witaj następujących logiki został użyty toomake to.
1. Znajdź wszystkie poprawki hello zainstalowany na komputerze hello.
2. Sprawdź, czy co najmniej jeden z hello poprawki z hello zdefiniowana lista jest obecny.
3. Jeśli tak, maszyna hello jest chroniona. W przeciwnym razie maszyna hello jest narażone na atak powitania.

Możesz użyć powitania po tooperform skrypt programu PowerShell to sprawdzenie ręcznie. Implementuje hello powyżej logiki.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Powiązane linki
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
