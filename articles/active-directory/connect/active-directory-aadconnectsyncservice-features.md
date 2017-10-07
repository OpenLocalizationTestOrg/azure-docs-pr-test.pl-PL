---
title: Synchronizacja Connect aaaAzure AD service funkcji i konfiguracji | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji po stronie usługi dla usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Funkcje usługi synchronizacji programu Azure AD Connect
Witaj funkcji synchronizacji programu Azure AD Connect zawiera dwa składniki:

* Witaj lokalnymi składnika o nazwie **synchronizacja programu Azure AD Connect**, nazywany również **aparatu synchronizacji**.
* Usługa Hello znajdującej się w usłudze Azure AD, znanej także jako **usługi synchronizacji programu Azure AD Connect**

W tym temacie wyjaśniono, jak hello następujące funkcje programu hello **usługi synchronizacji programu Azure AD Connect** pracy i jak można je również skonfigurować za pomocą środowiska Windows PowerShell.

Te ustawienia są konfigurowane przez hello [Azure Active Directory modułu dla środowiska Windows PowerShell](http://aka.ms/aadposh). Pobierz i zainstaluj go niezależnie od Azure AD Connect. polecenia cmdlet Hello opisane w niniejszym dokumencie zostały wprowadzone w hello [wersji marca 2016 (kompilacja 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1). Jeśli nie masz hello poleceń cmdlet w tym temacie lub tworzy hello sam wyniku, a następnie upewnij się, że możesz uruchomić hello najnowszej wersji.

Konfiguracja hello toosee w katalogu usługi Azure AD, uruchom `Get-MsolDirSyncFeatures`.  
![Get-MsolDirSyncFeatures wyników](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

Wiele z tych ustawień można zmienić tylko przy użyciu usługi Azure AD Connect.

Witaj następujące ustawienia można skonfigurować przy `Set-MsolDirSyncFeature`:

| DirSyncFeature | Komentarz |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |Umożliwia toojoin obiektów userPrincipalName dodanie adresu tooprimary SMTP. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |Umożliwia atrybutu userPrincipalName hello tooupdate aparatu synchronizacji hello zarządzane licencjonowanych użytkowników (niefederacyjnych). |

Po włączeniu funkcji nie można wyłączyć ponownie.

> [!NOTE]
> Z 24 sierpnia 2016 hello funkcji *zduplikowany atrybut odporności* jest domyślnie włączona dla nowej usługi Azure AD katalogów. Ta funkcja będzie również wprowadzanie i włączone na katalogi utworzone przed tą datą. Otrzymasz wiadomość e-mail z powiadomieniem po katalogu o tooget ta funkcja jest włączona.
> 
> 

Witaj następujące ustawienia są skonfigurowane przy użyciu usługi Azure AD Connect i nie można zmodyfikować przez `Set-MsolDirSyncFeature`:

| DirSyncFeature | Komentarz |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: Włączanie zapisywania zwrotnego urządzeń](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Synchronizacja programu Azure AD Connect: rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |Umożliwia toobe atrybutu poddane kwarantannie, gdy jest duplikatem innego obiektu, a nie awarii całego obiektu hello podczas eksportowania. |
| PasswordSync |[Implementowanie synchronizacji haseł z synchronizacji Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[Podglądu: Zapisywanie zwrotne grup](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |Nie są obecnie obsługiwane. |

## <a name="duplicate-attribute-resiliency"></a>Zduplikowany atrybut odporności
Zamiast niepowodzeniem tooprovision obiekty z zduplikowane nazwy UPN / proxyAddresses, zduplikowany atrybut hello jest "poddane kwarantannie" i przypisano wartości tymczasowej. Po rozwiązaniu konfliktu hello hello tymczasowej nazwy UPN jest zmieniany automatycznie toohello poprawnej wartości. Aby uzyskać więcej informacji, zobacz [tożsamości synchronizacji i zduplikowany atrybut odporności](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="userprincipalname-soft-match"></a>UserPrincipalName nietrwałego dopasowania
Gdy ta funkcja jest włączona, soft-match jest włączone dla nazwy UPN w toohello dodanie [podstawowego adresu SMTP](https://support.microsoft.com/kb/2641663), który jest zawsze włączona. Soft-match jest używane toomatch istniejących użytkowników chmury w usłudze Azure AD z lokalnymi użytkownikami.

Jeśli potrzebujesz toomatch lokalnych kont usługi AD z istniejących kont utworzonych w chmurze hello nie używasz usługi Exchange Online, a następnie ta funkcja jest przydatna. W tym scenariuszu zwykle nie masz atrybutem Przyczyna tooset hello SMTP w chmurze hello.

Ta funkcja jest na domyślnie dla nowo utworzone katalogów usługi Azure AD. Możesz sprawdzić, czy ta funkcja jest włączona dla Ciebie, uruchamiając:  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Jeśli ta funkcja nie jest włączona dla katalogu usługi Azure AD, następnie możesz je włączyć, uruchamiając:  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>Synchronizowanie aktualizacji userPrincipalName
W przeszłości atrybutu UserPrincipalName toohello aktualizacje przy użyciu usługi synchronizacji hello z lokalnymi został zablokowany, chyba że oba te warunki są spełnione:

* Użytkownik Hello jest zarządzany (niefederacyjnych).
* Witaj użytkownika nie ma przypisanej licencji.

Aby uzyskać więcej informacji, zobacz [użytkownika nazwy w usłudze Office 365, Azure lub Intune nie są zgodne hello lokalną nazwą UPN lub alternatywnym Identyfikatorem logowania](https://support.microsoft.com/kb/2523192).

Włączenie tej funkcji umożliwia hello synchronizacji aparat tooupdate hello userPrincipalName, gdy jest zmienione lokalnymi i użyciu synchronizacji haseł. Jeśli używasz federacyjnych, ta funkcja nie jest obsługiwana.

Ta funkcja jest na domyślnie dla nowo utworzone katalogów usługi Azure AD. Możesz sprawdzić, czy ta funkcja jest włączona dla Ciebie, uruchamiając:  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Jeśli ta funkcja nie jest włączona dla katalogu usługi Azure AD, następnie możesz je włączyć, uruchamiając:  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

Po włączeniu tej funkcji, zostaną one istniejące wartości userPrincipalName — jest. Dla następnej zmiany hello userPrincipalName atrybutu lokalnymi synchronizacja różnicowa normalne hello na użytkowników spowoduje zaktualizowanie hello głównej nazwy użytkownika.  

## <a name="see-also"></a>Zobacz też
* [Synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

