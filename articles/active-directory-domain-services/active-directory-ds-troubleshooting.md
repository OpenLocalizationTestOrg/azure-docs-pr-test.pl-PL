---
title: "Usługach domenowych Azure Active Directory: Przewodnik rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "Podręcznik rozwiązywania problemów dotyczących usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d6695b0c40f56093e8701dfe6394143268114453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Usługi domenowe usługi Azure AD — przewodnik rozwiązywania problemów
Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów, które można napotkać podczas konfigurowania lub administrowanie usług domenowych w usłudze Azure Active Directory (AD).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Nie można włączyć usługi domenowe Azure AD dla katalogu usługi Azure AD
Ta sekcja pomoże w rozwiązaniu błędy podczas próby włączenia usług domenowych Azure AD dla katalogu i jego nie powiedzie się lub pobiera ich "Wyłączone".

Wybierz odpowiadające kroki rozwiązywania problemów napotkanych komunikat o błędzie.

| **Komunikat o błędzie** | **Rozdzielczość** |
| --- |:--- |
| *Nazwa contoso100.com jest już używana w tej sieci. Określ nazwę, która nie jest używana.* |[Konflikt nazw domeny w sieci wirtualnej](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Nie można włączyć usług Domain Services w tej dzierżawie usługi Azure AD. Usługa nie ma odpowiednich uprawnień do aplikacji o nazwie „Azure AD Domain Services Sync”. Usuń aplikację o nazwie „Azure AD Domain Services Sync”, a następnie spróbuj włączyć usługi Domain Services dla dzierżawy usługi Azure AD.* |[Usług domenowych w usłudze nie ma wystarczających uprawnień do synchronizacji usługi domenowe Azure AD aplikacji](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Nie można włączyć usług Domain Services w tej dzierżawie usługi Azure AD. Aplikacja usług Domain Services w dzierżawie usługi Azure AD nie uprawnień wymaganych do włączenia usług Domain Services. Usuń aplikację z identyfikatorem d87dcbc6-a371-462e-88e3-28ad15ec4e64, a następnie spróbuj włączyć usługi Domain Services dla dzierżawy usługi Azure AD.* |[Aplikacja usług domenowych w usłudze nie jest prawidłowo skonfigurowana w Twojej dzierżawie](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Nie można włączyć usług Domain Services w tej dzierżawie usługi Azure AD. Aplikacja usługi Microsoft Azure AD jest wyłączona w dzierżawie usługi Azure AD. Włącz aplikację z identyfikatorem 00000002-0000-0000-c000-000000000000, a następnie spróbuj włączyć usługi Domain Services dla dzierżawy usługi Azure AD.* |[Aplikacja Microsoft Graph jest wyłączona w dzierżawie usługi Azure AD](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Konflikt nazw domeny
**Komunikat o błędzie:**

*Nazwa contoso100.com jest już używana w tej sieci. Określ nazwę, która nie jest używana.*

**Środki zaradcze:**

Upewnij się, że nie masz istniejącej domeny o takiej samej nazwie domeny, dostępne w tej sieci wirtualnej. Na przykład załóżmy, że masz domenę o nazwie „contoso.com” już dostępną w wybranej sieci wirtualnej. Później spróbuj włączyć domeny zarządzanej usług domenowych Azure AD z tą samą nazwą domeny (to znaczy "contoso.com") w tej sieci wirtualnej. Wystąpi awaria podczas próby włączenia usług domenowych Azure AD.

Ten błąd jest spowodowany konfliktów nazw dla nazwy domeny w sieci wirtualnej. W takiej sytuacji musisz użyć innej nazwy podczas konfigurowania domeny zarządzanej Usług domenowych Azure AD. Możesz również anulować aprowizację istniejącej domeny i kontynuować włączanie Usług domenowych Azure AD.

### <a name="inadequate-permissions"></a>Niewystarczające uprawnienia
**Komunikat o błędzie:**

*Nie można włączyć usług Domain Services w tej dzierżawie usługi Azure AD. Usługa nie ma odpowiednich uprawnień do aplikacji o nazwie „Azure AD Domain Services Sync”. Usuń aplikację o nazwie „Azure AD Domain Services Sync”, a następnie spróbuj włączyć usługi Domain Services dla dzierżawy usługi Azure AD.*

**Środki zaradcze:**

Sprawdź, czy istnieje aplikacja o nazwie "Sync usług domenowych Azure AD" w katalogu usługi Azure AD. Jeśli ta aplikacja istnieje, usuń go, a następnie ponownie włącz usługi domenowe Azure AD.

Wykonaj następujące kroki, aby sprawdzić obecność aplikacji i go usunąć, jeśli aplikacja istnieje:

1. Przejdź do **klasycznego portalu Azure** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. W lewym okienku wybierz węzeł **Active Directory**.
3. Wybierz dzierżawę (katalog) usługi Azure AD, dla której chcesz włączyć Usługi domenowe Azure AD.
4. Przejdź do **aplikacji** kartę.
5. Wybierz **aplikacji Moja firma jest właścicielem** opcji na liście rozwijanej.
6. Sprawdź, czy aplikacji o nazwie **synchronizacji usług domenowych Azure AD**. Jeśli aplikacja istnieje, przejdź do go usunąć.
7. Po usunięciu aplikacji, spróbuj ponownie włączyć usługi domenowe Azure AD.

### <a name="invalid-configuration"></a>Nieprawidłowa konfiguracja
**Komunikat o błędzie:**

*Nie można włączyć usług Domain Services w tej dzierżawie usługi Azure AD. Aplikacja usług Domain Services w dzierżawie usługi Azure AD nie uprawnień wymaganych do włączenia usług Domain Services. Usuń aplikację z identyfikatorem d87dcbc6-a371-462e-88e3-28ad15ec4e64, a następnie spróbuj włączyć usługi Domain Services dla dzierżawy usługi Azure AD.*

**Środki zaradcze:**

Sprawdź, czy masz aplikacja o nazwie "AzureActiveDirectoryDomainControllerServices" (z identyfikatorem aplikacji z d87dcbc6-a371-462e-88e3-28ad15ec4e64) w katalogu usługi Azure AD. Jeśli ta aplikacja istnieje, należy ją usunąć i ponownie włączyć usługi domenowe Azure AD.

Poniższy skrypt programu PowerShell umożliwia Znajdź aplikację i usuń go.

> [!NOTE]
> Ten skrypt używa **programu Azure AD PowerShell w wersji 2** polecenia cmdlet. Aby uzyskać pełną listę wszystkich dostępnych poleceń cmdlet i pobierania modułu, przeczytaj [dokumentacji programu AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Program Microsoft Graph wyłączone
**Komunikat o błędzie:**

Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Aplikacja usługi Microsoft Azure AD jest wyłączona w dzierżawie usługi Azure AD. Włącz aplikację z 00000002-0000-0000-c000-000000000000 identyfikator aplikacji, a następnie spróbuj włączyć usługi domenowe dla dzierżawy usługi Azure AD.

**Środki zaradcze:**

Sprawdź, jeśli wyłączono aplikacji o identyfikatorze 00000002-0000-0000-c000-000000000000. Ta aplikacja to aplikacja Microsoft Azure AD i zapewnia dostęp do interfejsu API programu Graph do dzierżawy usługi Azure AD. Usługi domenowe Azure AD musi umożliwiać zsynchronizować dzierżawy usługi Azure AD do domeny zarządzanej tej aplikacji.

Aby rozwiązać ten problem, Włącz tę aplikację, a następnie spróbuj włączyć usługi domenowe dla dzierżawy usługi Azure AD.

## <a name="users-are-unable-to-sign-in-to-the-azure-ad-domain-services-managed-domain"></a>Użytkownicy nie mogą zalogować się do domeny zarządzanej usług Azure AD Domain Services
Jeśli jeden lub więcej użytkowników w dzierżawie usługi Azure AD nie można zalogować się do domeny zarządzanej nowo utworzony, wykonaj następujące kroki:

* **Zaloguj się przy użyciu nazwy UPN format:** podejmą próbę zalogowania w formacie nazwy UPN (na przykład "joeuser@contoso.com") zamiast formatu SAMAccountName (CONTOSO\joeuser). SAMAccountName mogą być automatycznie generowane dla użytkowników, których prefiks nazwy UPN jest zbyt długa lub jest taki sam jak inny użytkownik domeny zarządzanej. Format nazwy UPN jest musi być unikatowy w ramach dzierżawy usługi Azure AD.

> [!NOTE]
> Firma Microsoft zaleca w formacie nazwy UPN logować się do domeny zarządzanej usług domenowych Azure AD.
>
>

* Upewnij się, że masz [włączoną synchronizację haseł](active-directory-ds-getting-started-password-sync.md) zgodnie z procedurą opisaną w przewodniku Wprowadzenie.
* **Kont zewnętrznych:** upewnij się, że konto użytkownika nie jest kontem zewnętrznych w dzierżawie usługi Azure AD. Kont zewnętrznych przykłady kont Microsoft (na przykład "joe@live.com") lub kont użytkowników z zewnętrznego katalogu usługi Azure AD. Ponieważ usługi domenowe Azure AD nie ma poświadczeń dla tych kont użytkowników, użytkownicy nie Zaloguj się do domeny zarządzanej.
* **Zsynchronizować konta:** Jeśli konta użytkownika, którego dotyczy są synchronizowane z katalogiem lokalnym, upewnij się, że:

  * Wdrożeniu lub zaktualizowany w celu [zalecane, najnowszej wersji programu Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Skonfigurowano Azure AD Connect do [wykonać pełną synchronizację](active-directory-ds-getting-started-password-sync.md).
  * W zależności od rozmiaru katalogu może potrwać do kont użytkowników i poświadczeń skrótów, które mają być dostępne w usługach domenowych Azure AD. Upewnij się, że należy odczekać wystarczająco długo Trwa ponawianie próby uwierzytelnienia (w zależności od rozmiaru katalogu - kilku godzin na dzień lub dwa dużych katalogów).
  * Jeśli problem nie zniknie po sprawdzeniu powyższych kroków, ponowne uruchomienie usługi Microsoft Azure AD Sync. Z komputera synchronizacji Uruchom wiersz polecenia i uruchom następujące polecenia:

    1. polecenie net stop "Microsoft Azure AD Sync"
    2. polecenie net start "Microsoft Azure AD Sync"
* **Tylko w chmurze kont**: Jeśli konto użytkownika, którego dotyczy to konto użytkownika tylko do chmury, upewnij się, że użytkownik zmienił swoje hasło po włączeniu usług domenowych Azure AD. Ten krok powoduje wygenerowanie skrótów poświadczeń wymaganych przez usługi Azure AD Domain Services.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Użytkowników usuniętych z dzierżawy usługi Azure AD nie są usuwane z domeny zarządzanej
Usługa Azure AD zapewnia ochronę przed przypadkowym usunięciem obiektów użytkowników. Po usunięciu konta użytkownika z dzierżawy usługi Azure AD odpowiedni obiekt użytkownika jest przenoszony do Kosza. Operacja usuwania jest synchronizowane do domeny zarządzanej, powoduje odpowiadającego mu konta użytkownika był oznaczony jako wyłączony. Ta funkcja pomaga odzyskać lub później cofanie usuwania konta użytkownika.

Konto użytkownika pozostaje w stanie wyłączenia, w domenie zarządzanej, nawet jeśli ponownie utworzyć konto użytkownika z tej samej nazwy UPN w katalogu usługi Azure AD. Aby usunąć konto użytkownika z domeny zarządzanej, należy wymusić usunięcie go z dzierżawy usługi Azure AD.

Aby usunąć konto użytkownika w pełni z domeny zarządzanej, należy trwale usunąć użytkownika z dzierżawy usługi Azure AD. Użyj polecenia cmdlet programu PowerShell Remove-MsolUser z opcją „-RemoveFromRecycleBin” w sposób opisany w tym [artykule MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Skontaktuj się z nami
Skontaktuj się z zespołem produktu usługi Azure Active Directory Domain Services, aby [udostępnić opinię lub pomocy technicznej](active-directory-ds-contact-us.md).
