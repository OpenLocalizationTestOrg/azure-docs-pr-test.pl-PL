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
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Usługi domenowe usługi Azure AD — przewodnik rozwiązywania problemów
Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów, które można napotkać podczas konfigurowania lub administrowanie usług domenowych w usłudze Azure Active Directory (AD).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Nie można włączyć usługi domenowe Azure AD dla katalogu usługi Azure AD
Tej sekcji podano informacje ułatwiające rozwiązywanie problemów podczas próby tooenable usług domenowych Azure AD dla katalogu i kończy się niepowodzeniem, lub pobiera przełączane wstecz too'Disabled ".

Wybierz hello kroki odpowiadające toohello następujący komunikat o błędzie wystąpią rozwiązywania problemów.

| **Komunikat o błędzie** | **Rozdzielczość** |
| --- |:--- |
| *Witaj contoso100.com nazwa jest już używana w tej sieci. Określ nazwę, która nie jest używana.* |[Konflikt nazw domeny w sieci wirtualnej hello](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Usługa Hello nie ma wystarczających uprawnień toohello aplikacji o nazwie "Sync usług domenowych Azure AD". Usuwanie aplikacji hello o nazwie "Sync usług domenowych Azure AD", a następnie spróbuj usług domenowych tooenable dla dzierżawy usługi Azure AD.* |[Usług domenowych w usłudze nie ma wystarczających uprawnień toohello synchronizacji usług domenowych Azure AD aplikacji](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Hello usług domenowych w usłudze hello aplikację w dzierżawie usługi Azure AD nie ma wymagane uprawnienia tooenable usług domenowych w usłudze. Usunięcie aplikacji hello z d87dcbc6-a371-462e-88e3-28ad15ec4e64 identyfikator aplikacji hello, a następnie spróbuj tooenable usługi domenowe dla dzierżawy usługi Azure AD.* |[Witaj usług domenowych w usłudze aplikacji nie został prawidłowo skonfigurowany w Twojej dzierżawie](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Witaj aplikacji usługi Microsoft Azure AD jest wyłączona w dzierżawie usługi Azure AD. Włączanie aplikacji hello z 00000002-0000-0000-c000-000000000000 identyfikator aplikacji hello, a następnie spróbuj tooenable usługi domenowe dla dzierżawy usługi Azure AD.* |[Aplikacja Microsoft Graph Hello jest wyłączona w dzierżawie usługi Azure AD](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Konflikt nazw domeny
**Komunikat o błędzie:**

*Witaj contoso100.com nazwa jest już używana w tej sieci. Określ nazwę, która nie jest używana.*

**Środki zaradcze:**

Upewnij się, że nie masz istniejącej domeny hello tej samej nazwy domeny jest dostępny w tej sieci wirtualnej. Na przykład załóżmy, że masz domenę o nazwie "contoso.com" już dostępną na powitania wybranej sieci wirtualnej. Później, spróbuj tooenable domeny zarządzanej usług domenowych Azure AD z hello tą samą nazwą domeny (to znaczy "contoso.com") w tej sieci wirtualnej. Podczas próby usług domenowych w usłudze Azure AD tooenable wystąpi awaria.

Ten błąd jest powodu konfliktów tooname hello nazwy domeny w sieci wirtualnej. W takiej sytuacji należy użyć tooset inną nazwę zapasowej domeny zarządzanej usług domenowych Azure AD. Alternatywnie można anulować aprowizację istniejącej domeny hello, a następnie przejdź usług domenowych w usłudze tooenable usługi Azure AD.

### <a name="inadequate-permissions"></a>Niewystarczające uprawnienia
**Komunikat o błędzie:**

*Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Usługa Hello nie ma wystarczających uprawnień toohello aplikacji o nazwie "Sync usług domenowych Azure AD". Usuwanie aplikacji hello o nazwie "Sync usług domenowych Azure AD", a następnie spróbuj usług domenowych tooenable dla dzierżawy usługi Azure AD.*

**Środki zaradcze:**

Toosee należy sprawdzić, czy aplikacja o nazwie hello "Sync usług domenowych Azure AD" w katalogu usługi Azure AD. Jeśli ta aplikacja istnieje, usuń go, a następnie ponownie włącz usługi domenowe Azure AD.

Wykonaj hello następujące kroki toocheck hello obecności aplikacji hello i toodelete, jeśli aplikacja hello istnieje:

1. Przejdź toohello **klasycznego portalu Azure** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Wybierz hello **usługi Active Directory** węzła w okienku po lewej stronie powitania.
3. Wybierz hello Azure AD dzierżawę (katalog), dla którego chcesz tooenable usług domenowych Azure AD.
4. Przejdź toohello **aplikacji** kartę.
5. Wybierz hello **aplikacji Moja firma jest właścicielem** opcję hello listy rozwijanej.
6. Sprawdź, czy aplikacji o nazwie **synchronizacji usług domenowych Azure AD**. Jeśli aplikacja hello istnieje, przejdź toodelete go.
7. Po usunięciu aplikacji hello usług domenowych w usłudze Azure AD tooenable spróbuj ponownie.

### <a name="invalid-configuration"></a>Nieprawidłowa konfiguracja
**Komunikat o błędzie:**

*Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Hello usług domenowych w usłudze hello aplikację w dzierżawie usługi Azure AD nie ma wymagane uprawnienia tooenable usług domenowych w usłudze. Usunięcie aplikacji hello z d87dcbc6-a371-462e-88e3-28ad15ec4e64 identyfikator aplikacji hello, a następnie spróbuj tooenable usługi domenowe dla dzierżawy usługi Azure AD.*

**Środki zaradcze:**

Sprawdź toosee, jeśli aplikacja o nazwie hello "AzureActiveDirectoryDomainControllerServices" (z identyfikatorem aplikacji z d87dcbc6-a371-462e-88e3-28ad15ec4e64) w katalogu usługi Azure AD. Ta aplikacja istnieje, należy najpierw toodelete go i następnie usługi domenowe Azure AD ponownie włączyć.

Użyj powitania po aplikacji hello toofind skryptu środowiska PowerShell i usuń go.

> [!NOTE]
> Ten skrypt używa **programu Azure AD PowerShell w wersji 2** polecenia cmdlet. Aby uzyskać pełną listę wszystkich dostępnych poleceń cmdlet i toodownload hello modułu przeczytaj hello [dokumentacji programu AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
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
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Program Microsoft Graph wyłączone
**Komunikat o błędzie:**

Nie można włączyć usługi domenowe w tej dzierżawy usługi Azure AD. Witaj aplikacji usługi Microsoft Azure AD jest wyłączona w dzierżawie usługi Azure AD. Włączanie aplikacji hello z 00000002-0000-0000-c000-000000000000 identyfikator aplikacji hello, a następnie spróbuj tooenable usługi domenowe dla dzierżawy usługi Azure AD.

**Środki zaradcze:**

Sprawdź toosee wyłączenie aplikacji o identyfikatorze hello 00000002-0000-0000-c000-000000000000. Ta aplikacja jest hello aplikacji usługi Microsoft Azure AD i zapewnia dzierżawy usługi Azure AD tooyour dostępu interfejsu API programu Graph. Usługi domenowe Azure AD wymaga tego toosynchronize toobe włączone aplikacji zarządzanych w Twojej tooyour dzierżawy usługi Azure AD domeny.

tooresolve tego błędu, Włącz tę aplikację, a następnie spróbuj usług domenowych tooenable dla dzierżawy usługi Azure AD.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Użytkownicy są toosign w toohello domeny zarządzanej usług domenowych Azure AD
Jeśli jeden lub więcej użytkowników w dzierżawie usługi Azure AD toosign w nowo utworzony toohello domeny zarządzanej, wykonaj hello następujące kroki rozwiązywania problemów:

* **Zaloguj się przy użyciu nazwy UPN format:** spróbuj toosign w formacie nazwy UPN hello (na przykład "joeuser@contoso.com") zamiast formatu SAMAccountName hello (CONTOSO\joeuser). Hello SAMAccountName mogą być generowane automatycznie dla użytkowników, których prefiks nazwy UPN jest zbyt długa lub jest sama hello jako inny użytkownik na powitania domeny zarządzanej. format nazwy UPN Hello jest gwarantowana toobe unikatowa w ramach dzierżawy usługi Azure AD.

> [!NOTE]
> Zalecamy używanie toosign format nazwy UPN hello w domenie zarządzanej usług domenowych Azure AD toohello.
>
>

* Upewnij się, że masz [włączony synchronizacja haseł](active-directory-ds-getting-started-password-sync.md) zgodnie z hello kroki opisane w przewodniku wprowadzenie hello.
* **Kont zewnętrznych:** upewnij się, że hello wpływ na konto użytkownika nie jest kontem zewnętrznych w dzierżawie powitalnych usługi Azure AD. Kont zewnętrznych przykłady kont Microsoft (na przykład "joe@live.com") lub kont użytkowników z zewnętrznego katalogu usługi Azure AD. Ponieważ usługi domenowe Azure AD nie ma poświadczeń dla tych kont użytkowników, użytkownicy nie można zalogować toohello domeny zarządzanej.
* **Zsynchronizować konta:** Jeśli hello wpływ na konta użytkowników są synchronizowane z katalogiem lokalnym, upewnij się, że:

  * Wdrożeniu lub zaktualizować toohello [zalecane, najnowszej wersji programu Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Azure AD Connect zostały skonfigurowane za[wykonać pełną synchronizację](active-directory-ds-getting-started-password-sync.md).
  * W zależności od rozmiaru hello katalogu może chwilę potrwać dla kont użytkowników i poświadczeń toobe skrótów dostępnych w usługach domenowych Azure AD. Upewnij się, że Poczekaj wystarczająco długi, przed podjęciem próby wykonania uwierzytelniania (w zależności od rozmiaru hello katalogu - kilka godzin tooa dzień lub dwa dużych katalogów).
  * Jeśli hello problem będzie nadal występować po zweryfikowaniu hello w poprzednich krokach, ponowne uruchomienie hello usługi Microsoft Azure AD Sync. W tym komputerze synchronizacji Uruchom wiersz polecenia i wykonaj hello następującego polecenia:

    1. polecenie net stop "Microsoft Azure AD Sync"
    2. polecenie net start "Microsoft Azure AD Sync"
* **Tylko w chmurze kont**: hello dotyczy konta użytkownika w przypadku konta użytkownika tylko do chmury, upewnij się, ten użytkownik hello zmienił swoje hasło po włączeniu usług domenowych Azure AD. Ten krok powoduje, że poświadczenie hello skrótów wymaganych do wygenerowanych toobe usługi domenowe Azure AD.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Użytkowników usuniętych z dzierżawy usługi Azure AD nie są usuwane z domeny zarządzanej
Usługa Azure AD zapewnia ochronę przed przypadkowym usunięciem obiektów użytkowników. Po usunięciu konta użytkownika z dzierżawy usługi Azure AD hello odpowiedni obiekt użytkownika jest przenoszone toohello Kosza. Gdy ta operacja delete jest synchronizowane tooyour domeny zarządzanej, powoduje hello odpowiadającego toobe konta użytkownika oznaczone jako wyłączone. Ta funkcja pomaga odzyskać lub cofanie usuwania konta użytkownika hello później.

Witaj pozostaje w hello stanu w domenie zarządzanej wyłączonego konta użytkownika, nawet jeśli ponownie utworzyć konto użytkownika z hello tej samej nazwy UPN w katalogu usługi Azure AD. tooremove hello konta użytkownika z domeny zarządzanej, należy tooforce usunąć ją z dzierżawy usługi Azure AD.

konto użytkownika hello tooremove pełni z domeny zarządzanej, trwale usunąć użytkownika hello z dzierżawy usługi Azure AD. Użyj polecenia cmdlet Remove-MsolUser PowerShell hello z hello "-RemoveFromRecycleBin" opcja, zgodnie z opisem w tym [artykuł w witrynie MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Skontaktuj się z nami
Skontaktuj się z zespołu produktu usługi Azure Active Directory Domain Services hello zbyt[udostępnić opinię lub pomocy technicznej](active-directory-ds-contact-us.md).
