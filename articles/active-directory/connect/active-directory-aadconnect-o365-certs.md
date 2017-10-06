---
title: "Odnawianie aaaCertificate dla użytkowników usługi Office 365 i Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano tooOffice użytkowników 365 jak tooresolve problemy związane z wiadomościami e-mail powiadamiać użytkowników o odnawiania certyfikatu."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Odnawianie certyfikatów Federacji dla usługi Office 365 i Azure Active Directory
## <a name="overview"></a>Omówienie
Dla pomyślnego federacji między Azure Active Directory (Azure AD) i Active Directory Federation Services (AD FS) hello certyfikatów używanych przez usługi AD FS toosign zabezpieczeń tokeny tooAzure AD powinna odpowiadać co to jest skonfigurowany w usłudze Azure AD. Wszelkie niezgodność może prowadzić toobroken zaufania. Usługi Azure AD zapewnia, że te informacje są utrzymywane w synchronizacji podczas wdrażania usług AD FS i serwera Proxy aplikacji sieci Web (Aby uzyskać dostęp przez ekstranet).

Ten artykuł zawiera dodatkowe informacje toomanage token certyfikaty podpisywania i przechowywać w synchronizacji z usługą Azure AD w hello w następujących przypadkach:

* Nie wymaga wdrażania powitania serwera Proxy aplikacji sieci Web, a w związku z tym nie jest dostępna w ekstranecie hello hello metadanych federacji.
* Nie używasz hello domyślnej konfiguracji usług AD FS certyfikaty podpisywania tokenu.
* Czy przy użyciu dostawcy tożsamości innych firm.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Domyślna konfiguracja usług AD FS dla certyfikatów podpisywania tokenu
Hello podpisywania tokenu i odszyfrowywania certyfikaty token są zazwyczaj samodzielnie podpisanych certyfikatów i są dobrym przez jeden rok. Domyślnie usługi AD FS obejmują proces automatycznego odnawiania o nazwie **AutoCertificateRollover**. Jeśli korzystasz z usług AD FS 2.0 lub nowszej, usługi Office 365 i Azure AD automatycznie aktualizuje certyfikatu przed jego wygaśnięciem.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Powiadomienie odnawiania z portalu usługi Office 365 hello lub wiadomości e-mail
> [!NOTE]
> Jeśli otrzymanej wiadomości e-mail lub portalu powiadomienie monitem toorenew certyfikat dla pakietu Office, zobacz [Zarządzanie zmienia tootoken certyfikaty podpisywania](#managecerts) toocheck, jeśli potrzebujesz tootake żadnych działań. Firma Microsoft dokłada świadomość możliwy problem, który może prowadzić toonotifications odnowienia certyfikatu są wysyłane, nawet wtedy, gdy nie jest wymagana żadna akcja.
>
>

Usługi Azure AD podejmuje metadanych Federacji hello toomonitor i certyfikatów podpisywania wskazywany przez te metadane token hello aktualizacji. 30 dni przed wygaśnięciem hello certyfikaty podpisywania tokenu hello Azure AD sprawdza nowe certyfikaty są dostępne przez sondowanie hello metadanych federacji.

* Czy można pomyślnie sondowania metadanych Federacji hello i pobrać nowe certyfikaty hello, bez powiadomienia e-mail i ostrzeżenia w portalu usługi Office 365 hello jest wystawiony toohello użytkownika.
* Jeśli nie może pobrać hello nowych certyfikatów podpisywania tokenu, albo ponieważ hello metadanych federacji nie jest dostępny lub nie włączono automatycznego przerzucania, usługa Azure AD wystawia wiadomość e-mail z powiadomieniem i ostrzeżenie w portalu usługi Office 365 hello.

![Powiadomieniu portalu usługi Office 365](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Jeśli używasz usług AD FS, tooensure ciągłość prowadzenia działalności biznesowej, sprawdź, czy serwery mają powitania po aktualizacji, dzięki czemu nie występują błędy uwierzytelniania pod kątem znanych problemów. Zmniejsza to zagrożenie wynikające znanych problemów dotyczących serwera proxy usług AD FS dla tego odnawiania i okresy przyszłych odnawiania:
>
> Server 2012 R2 — [systemu Windows Server zbiorczy maja 2014](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 i 2012 — [niepowodzenia uwierzytelniania za pośrednictwem serwera proxy w systemie Windows Server 2012 lub Windows 2008 R2 z dodatkiem SP1](http://support.microsoft.com/kb/3094446)
>
>

## Sprawdzaj, czy certyfikaty hello wymagają toobe zaktualizowane<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Krok 1: Sprawdź stan AutoCertificateRollover hello
Na serwerze usług AD FS Otwórz program PowerShell. Sprawdź, czy hello AutoCertificateRollover wartość tooTrue.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>Jeśli korzystasz z usług AD FS 2.0, najpierw uruchom Microsoft.Adfs.Powershell Dodaj-Pssnapin.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Krok 2: Sprawdź, czy usługi AD FS a usługą Azure AD są zsynchronizowane
Na serwerze usług AD FS Otwórz hello Azure AD PowerShell wiersza, a następnie połącz tooAzure AD.

> [!NOTE]
> Możesz pobrać program Azure AD PowerShell [tutaj](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Sprawdź certyfikaty hello skonfigurowane w usłudze AD FS i właściwości zaufania usługi Azure AD dla hello określonej domeny.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Jeśli odciski palców hello zarówno hello wyniki zgodne, certyfikaty są zsynchronizowane z usługą Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Krok 3: Sprawdź, czy certyfikat o tooexpire
W danych wyjściowych hello Get MsolFederationProperty lub Get-AdfsCertificate Sprawdź datę hello w obszarze "Nie po." Jeśli data hello jest mniej niż 30 dni nieobecności, należy podjąć akcję.

| AutoCertificateRollover | Certyfikaty w synchronizacji z usługą Azure AD | Jest dostępny publicznie element metadanych Federacji | Ważność | Akcja |
|:---:|:---:|:---:|:---:|:---:|
| Tak |Tak |Tak |- |Nie jest wymagana żadna akcja. Zobacz [podpisywania tokenu odnawiania certyfikatów automatycznie](#autorenew). |
| Tak |Nie |- |Mniej niż 15 dni |Odnów natychmiast. Zobacz [podpisywania tokenu odnawiania certyfikatu ręcznie](#manualrenew). |
| Nie |- |- |Mniej niż 30 dni |Odnów natychmiast. Zobacz [podpisywania tokenu odnawiania certyfikatu ręcznie](#manualrenew). |

\[-] Nie ma znaczenia.

## Odnów certyfikat podpisywania automatycznie token hello (zalecane)<a name="autorenew"></a>
Nie trzeba tooperform wszelkie wymagane ręczne wykonanie czynności, jeśli spełnione są następujące hello:

* Serwer Proxy aplikacji sieci Web, która może umożliwić metadanych Federacji toohello dostępu z ekstranetu hello została wdrożona.
* Używasz usług AD FS hello domyślnej konfiguracji (AutoCertificateRollover jest włączona).

Sprawdź, czy powitania po tooconfirm, który hello certyfikatu może być aktualizowana automatycznie.

**1. hello właściwości usługi AD FS AutoCertificateRollover musi być ustawiona tooTrue.** Oznacza to, że usługi AD FS automatycznie generuje nowy podpisywania tokenu i certyfikaty odszyfrowywania tokenów, przed hello tych wygaśnie stary.

**2. metadane Federacji hello usługi AD FS jest dostępny publicznie.** Sprawdź, czy z metadanych federacji jest dostępny publicznie, przechodząc toohello następującego adresu URL z komputera hello publicznego Internetu (poza siecią firmową hello):

/federationmetadata/2007-06/federationmetadata.xml https:// (your_FS_name)

gdzie `(your_FS_name) `jest zastępowany hello nazwa usługi federacyjnej hosta używa Twojej organizacji, na przykład fs.contoso.com.  Jeśli to możliwe tooverify z tych ustawień pomyślnie, nie dysponujesz toodo inaczej.  

Przykład: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Odnów token hello ręcznie podpisywania certyfikatu<a name="manualrenew"></a>
Możesz wybrać toorenew certyfikaty podpisywania tokenu hello ręcznie. Na przykład hello następujące scenariusze mogą działać lepiej odnowienia ręczne:

* Certyfikaty podpisywania tokenu to certyfikaty nie podpisem. Hello Najczęstszą przyczyną tego błędu jest to, czy Twoja organizacja zarządza certyfikatów usługi AD FS zarejestrowane od urzędu certyfikacji w organizacji.
* Zabezpieczenia sieci nie zezwala na toobe metadanych Federacji hello publicznie dostępne.

W tych scenariuszach za każdym razem, gdy token hello podpisywania certyfikatów, należy również zaktualizować domeną usługi Office 365 za pomocą polecenia programu PowerShell hello, MsolFederatedDomain aktualizacji.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Krok 1: Upewnij się, że usługi AD FS ma nowych certyfikatów podpisywania tokenu
**Inne niż domyślne konfiguracji**

Jeśli używasz niedomyślna Konfiguracja usług AD FS (gdzie **AutoCertificateRollover** ustawiono zbyt**False**), są prawdopodobnie używa niestandardowych certyfikatów (nie z podpisem własnym). Aby uzyskać więcej informacji dotyczących sposobu toorenew hello AD FS tokenu podpisywania certyfikatów, zobacz [wskazówki dotyczące klientów nie korzystających z usług AD FS certyfikaty z podpisem własnym](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Metadane federacji nie jest publicznie dostępna**

Na hello drugiej strony, jeśli **AutoCertificateRollover** ustawiono zbyt**True**, ale z metadanych federacji nie jest dostępny publicznie, najpierw upewnij się, że nowe certyfikaty podpisywania tokenu zostały wygenerowane przez usługi AD FS. Upewnij się, że masz nowy token certyfikaty podpisywania przez pobieranie hello następujące kroki:

1. Sprawdź, czy użytkownik jest zalogowany toohello głównej usługi AD FS serwera.
2. Sprawdź hello bieżącego podpisywania certyfikatów w usługach AD FS, otwierając okno polecenia programu PowerShell i uruchamiając hello następujące polecenie:

    PS C:\>podpisywania tokenu Get-ADFSCertificate — CertificateType

   > [!NOTE]
   > Jeśli korzystasz z usług AD FS 2.0, należy najpierw uruchomić Microsoft.Adfs.Powershell Dodaj-Pssnapin.
   >
   >
3. Sprawdź dane wyjściowe polecenia hello na wszystkie certyfikaty na liście. Jeśli usługi AD FS wygenerował nowy certyfikat, powinny pojawić się dwa certyfikaty w danych wyjściowych hello: jeden dla których hello **IsPrimary** wartość jest **True** i hello **nie później niż** Data jest w ciągu 5 dni, a drugi, dla którego **IsPrimary** jest **False** i **nie później niż** dotyczy roku w przyszłości hello.
4. Jeśli tylko jeden certyfikat w temacie i hello **nie później niż** przypada w ciągu 5 dni, należy toogenerate nowego certyfikatu.
5. toogenerate nowego świadectwa, wykonaj następujące polecenie w wierszu polecenia programu PowerShell hello: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Sprawdź hello aktualizacji, uruchamiając hello ponownie następujące polecenie: PS C:\>podpisywania tokenu Get-ADFSCertificate — CertificateType

Powinien być teraz wyświetlany dwa certyfikaty, z których jedna ma **nie później niż** około co roku w przyszłości hello i dla których hello **IsPrimary** wartość jest **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Krok 2: Zaktualizuj hello podpisywania certyfikatów dla zaufania usługi Office 365 hello nowy token.
Aktualizacja usługi Office 365 z hello nowy token podpisywania certyfikatów toobe używane dla zaufania hello w następujący sposób.

1. Otwórz hello Microsoft Azure Active Directory modułu dla środowiska Windows PowerShell.
2. Uruchom $cred = Get-Credential. Gdy to polecenie cmdlet wyświetla monit o podanie poświadczeń, wpisz poświadczenia konta administratora usługi chmury.
3. Uruchom Connect MsolService — $cred poświadczeń. To polecenie cmdlet łączy toohello usługi w chmurze. Tworzenie kontekstu, który łączy użytkownika usługi w chmurze toohello jest wymagana przed uruchomieniem wszelkie dodatkowe polecenia cmdlet hello instalowane przez narzędzie hello.
4. Jeśli używasz tych poleceń na komputerze, który nie jest hello usług AD FS podstawowy serwer federacyjny, uruchom zestaw MSOLAdfscontext-komputer <AD FS primary server>, gdzie <AD FS primary server> jest hello wewnętrznej nazwy FQDN hello głównej usługi AD FS serwera. To polecenie cmdlet tworzy kontekstu, który łączy tooAD FS.
5. Uruchom aktualizacji MSOLFederatedDomain — DomainName <domain>. To polecenie cmdlet ustawienia hello z usług AD FS do usługi w chmurze hello aktualizacji i konfiguruje hello relacji zaufania między dwoma hello.

> [!NOTE]
> Jeśli potrzebujesz toosupport wiele domen najwyższego poziomu, takich jak contoso.com i fabrikam.com, należy użyć hello **SupportMultipleDomain** przełącznik z dowolnego polecenia cmdlet. Aby uzyskać więcej informacji, zobacz [Obsługa wielu domen poziom górnej](active-directory-aadconnect-multiple-domains.md).
>
>

## Napraw zaufania usługi Azure AD za pomocą usługi Azure AD Connect<a name="connectrenew"></a>
Jeśli farma usług AD FS, a relacja zaufania usługi Azure AD są skonfigurowane za pomocą usługi Azure AD Connect, można użyć toodetect Azure AD Connect, jeśli potrzebujesz tootake dowolną akcję dla Twojego certyfikaty podpisywania tokenu. Toorenew hello certyfikatów, należy więc można użyć toodo Azure AD Connect.

Aby uzyskać więcej informacji, zobacz [naprawiania zaufania hello](active-directory-aadconnect-federation-management.md).
