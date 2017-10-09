---
title: "Uaktualnianie serwera usługi MFA aaaAzure | Dokumentacja firmy Microsoft"
description: "Kroki i wskazówki dotyczące tooupgrade powitania serwera usługi Azure Multi-Factor Authentication tooa nowszej wersji."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Uaktualnij toohello najnowsze serwera usługi Azure Multi-Factor Authentication

W tym artykule przedstawiono hello proces uaktualniania serwera usługi Azure Multi-Factor Authentication (MFA) w wersji 6.0 lub nowszej. Tooupgrade stara wersja hello PhoneFactor Agent, należy odwoływać się za[hello uaktualnienia tooAzure PhoneFactor Agent serwera Multi-Factor Authentication](multi-factor-authentication-get-started-server-upgrade.md).

W przypadku uaktualniania z 6.x lub starsze toov7.x lub nowszej, wszystkie składniki zmienić too.NET .NET 2.0 4.5. Wszystkie składniki wymagają programu Microsoft Visual C++ 2015 Redistributable Update 1 lub nowszej. powitania serwera usługi MFA Instalator instaluje obie hello x86 i x64 wersje tych składników, jeśli jeszcze nie są zainstalowane. Hello portalu użytkowników i Mobile App Web Service, uruchom na osobnych serwerach, należy najpierw tooinstall pakiety przed rozpoczęciem uaktualniania tych składników. Możesz wyszukać najnowszą aktualizację programu Microsoft Visual C++ 2015 Redistributable hello na powitania [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Zainstaluj najnowszą wersję powitania serwera usługi Azure MFA

1. Użyj instrukcji hello w [hello pobierania serwera usługi Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello najnowszą wersję powitania serwera usługi Azure MFA.
2. Wykonaj kopię zapasową pliku danych serwera usługi MFA hello znajdujący się w C:\Program Files\Multi-Factor Authentication Server\Data\PhoneFactor.pfdata (lokalizacja hello instalacja domyślna przyjmuje) na serwerze głównym usługi MFA.
3. Po uruchomieniu wielu serwerów w celu zapewnienia wysokiej dostępności, zmień systemy klienckie hello uwierzytelniających toohello serwera usługi MFA, tak aby ich Zatrzymaj przesyłanie ruchu toohello serwerów, które uaktualniania. Jeśli używasz usługi równoważenia obciążenia, usuwany jest serwer usługi MFA z usługi równoważenia obciążenia hello, hello uaktualniania, a następnie dodaj powitania serwera do farmy hello.
4. Uruchom Instalatora nowe hello na każdym serwerze usługi MFA. Serwery podrzędne należy najpierw uaktualnić, ponieważ może odczytywać hello replikowana przez główny hello starego pliku danych. 

  Nie trzeba toouninstall bieżącego serwera usługi MFA przed uruchomiony Instalator hello. Instalator Hello przeprowadza uaktualnienie w miejscu. Hello ścieżka instalacji jest pobierana z rejestru hello z poprzedniej instalacji hello, więc instaluje w hello sam lokalizacji (na przykład C:\Program Files\Multi-Factor Authentication Server). 
  
5. Jeśli zostanie wyświetlony monit o tooinstall Microsoft Visual C++ 2015 Redistributable aktualizacji pakietu, należy zaakceptować monit o hello. Obie hello x86 i x64 wersje pakietów hello są zainstalowane.
5. Jeśli używasz hello zestawu SDK usług sieci Web, zostanie wyświetlony monit tooinstall hello nowego zestawu SDK usług sieci Web. Po zainstalowaniu hello nowego zestawu SDK usług sieci Web, upewnij się, że nazwa katalogu wirtualnego tego hello odpowiada hello wcześniej zainstalowane katalogu wirtualnego (na przykład MultiFactorAuthWebServiceSdk).
6. Powtórz kroki hello na wszystkich serwerach podrzędnych. Podwyższ poziom jednego z hello podwładnych toobe hello nowy wzorzec, a następnie uaktualnienia hello starego serwera głównego. 

## <a name="upgrade-hello-user-portal"></a>Uaktualnij hello portalu użytkowników

1. Wykonaj kopię zapasową pliku web.config hello, który znajduje się w katalogu wirtualnego hello hello lokalizacji instalacji portalu użytkowników (na przykład C:\inetpub\wwwroot\MultiFactorAuth). Wszelkie zmiany dokonane toohello motyw domyślny, należy wykonać kopię zapasową hello App_Themes\Default również folder. Jest lepsze toocreate kopię hello domyślny folder i utworzyć nową kompozycję niż toochange hello domyślny motyw.
2. Jeśli hello Portal użytkowników jest uruchamiany na powitania tym samym serwerze, ponieważ hello inne składniki serwera usługi MFA hello instalacji serwera usługi MFA żąda hello tooupdate Portal użytkowników. Akceptowanie monitu hello i zainstaluj aktualizację portalu użytkowników hello. Sprawdź, czy nazwa katalogu wirtualnego tego hello odpowiada hello wcześniej zainstalowane katalogu wirtualnego (na przykład MultiFactorAuth).
3. W przypadku hello Portal użytkowników na osobnym serwerze, plik MultiFactorAuthenticationUserPortalSetup64.msi hello kopiowania z hello zainstalować lokalizację hello serwerów MFA i umieść je na serwer sieci web portalu użytkowników hello. Uruchom Instalatora hello. 

  Jeśli wystąpi błąd określania, "Microsoft Visual C++ 2015 Redistributable Update 1 lub nowszy jest wymagany," Pobierz i zainstaluj najnowszy pakiet aktualizacji hello z hello [Microsoft Download Center](https://www.microsoft.com/download/). Należy zainstalować obie wersje x86 i x64 hello.

4. Po zaktualizowaniu portalu użytkownika jest zainstalowane oprogramowanie hello porównać hello kopii zapasowej pliku web.config, wprowadzone w kroku 1 z hello nowy plik web.config. Jeśli nie istnieją żadne nowe atrybuty w pliku web.config nowe hello, skopiowany hello katalog wirtualny toooverwrite hello nowej kopii zapasowej pliku web.config. Innym rozwiązaniem jest toocopy/Wklej hello appSettings wartości i hello adres URL zestawu SDK usługi sieci Web z pliku kopii zapasowej hello do nowego pliku web.config hello.

Jeśli masz hello Portal użytkowników na wielu serwerach, powtórz hello instalacji na wszystkich z nich. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Uaktualnij hello Mobile App Web Service

1. Wykonaj kopię zapasową pliku web.config hello, który znajduje się w katalogu wirtualnego hello hello lokalizacji instalacji usługi Mobile App Web Service (na przykład C:\inetpub\wwwroot\app lub C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Kopiuj hello MultiFactorAuthenticationMobileAppWebServiceSetup64.msi plik z hello lokalizacji hello serwerów MFA instalacji i umieść je na serwer sieci web rejestracji aplikacji mobilnej hello.
3. Uruchom Instalatora hello. 

  Jeśli wystąpi błąd informujący, że program Microsoft Visual C++ 2015 Redistributable Update 1 lub nowszy jest wymagany, Pobierz i zainstaluj najnowszy pakiet aktualizacji hello z hello [Microsoft Download Center](https://www.microsoft.com/download/). Należy zainstalować obie wersje x86 i x64 hello.

4. Po zainstalowaniu oprogramowania Mobile App Web Service hello zaktualizowane Porównaj plik web.config hello utworzono kopię zapasową w kroku 1 z hello nowy plik web.config. Jeśli nie istnieją żadne nowe atrybuty w pliku web.config nowe hello, możesz skopiować zapisanego pliku web.config wrócić do katalogu wirtualnego hello i zastąpić hello nową. Innym rozwiązaniem jest toocopy/Wklej hello appSettings wartości i hello adres URL zestawu SDK usługi sieci Web z pliku kopii zapasowej hello do nowego pliku web.config hello.

Jeśli masz hello Mobile App Web Service na wielu serwerach, powtórz hello instalacji na wszystkich z nich. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Uaktualnij hello AD FS kart


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Jeśli uwierzytelnianie wieloskładnikowe jest uruchomiony na różnych serwerach niż usługi AD FS

Te instrukcje stosowane tylko wtedy, jeśli serwer Multi-Factor Authentication należy uruchomić niezależnie od serwerów usług AD FS. Jeśli obie usługi są uruchamiane hello samych serwerów, Pomiń tę sekcję i przejdź toohello kroki instalacji. 

1. Zapisz kopię pliku MultiFactorAuthenticationAdfsAdapter.config hello, który został zarejestrowany w usługach AD FS lub eksportu przy użyciu następującego polecenia programu PowerShell hello konfiguracji hello: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. Nazwa karty Hello jest "Element WindowsAzureMultiFactorAuthentication" lub "AzureMfaServerAuthentication" w zależności od wersji hello wcześniej zainstalowane.
2. Skopiuj następujące pliki z powitania serwera usługi MFA instalacji lokalizacji toohello AD FS serwerów hello:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Edytowanie skryptu hello Register-MultiFactorAuthenticationAdfsAdapter.ps1 przez dodanie `-ConfigurationFilePath [path]` toohello koniec hello `Register-AdfsAuthenticationProvider` polecenia. Zastąp *[ścieżka]* z toohello pełną ścieżkę hello MultiFactorAuthenticationAdfsAdapter.config lub pliku konfiguracji hello wyeksportowane hello poprzedniego kroku. 

  Sprawdź atrybuty hello w nowych toosee MultiFactorAuthenticationAdfsAdapter.config hello spełniające hello starego pliku konfiguracji. Jeśli wszystkie atrybuty zostały dodane lub usunięte w nowej wersji hello, skopiować hello wartości atrybutów z hello starego konfiguracji pliku toohello nową lub zmodyfikować hello starego toomatch pliku konfiguracji.

### <a name="install-new-ad-fs-adapters"></a>Zainstaluj nowe karty usług AD FS

> [!IMPORTANT] 
> Użytkownicy nie będą wymagane tooperform weryfikacji dwuetapowej etapach 3 – 8 przedstawione w tej sekcji. Jeśli masz usługi AD FS w wielu klastrów, można usunąć, uaktualniania i przywracanie poszczególnych klastrów w hello farmy niezależnie od hello inne klastry tooavoid przestoju.

1. Usuń niektóre serwery usług AD FS z hello farmy. Zaktualizuj te serwery podczas hello, które nadal działają inne osoby.
2. Zainstaluj nowy adapter AD FS hello na każdym serwerze usunięte z hello AD FS farmy. Jeśli powitania serwera usługi MFA jest zainstalowany na każdym serwerze usług AD FS, możesz je zaktualizować za pomocą serwera usługi MFA Witaj, Administratorze UX. W przeciwnym razie należy zaktualizować, uruchamiając MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  Jeśli wystąpi błąd określania, "Microsoft Visual C++ 2015 Redistributable Update 1 lub nowszy jest wymagany," Pobierz i zainstaluj najnowszy pakiet aktualizacji hello z hello [Microsoft Download Center](https://www.microsoft.com/download/). Należy zainstalować obie wersje x86 i x64 hello.

3. Przejdź za**usług AD FS** > **zasady uwierzytelniania** > **Edytuj globalne zasady uwierzytelniania Wieloskładnikowa**. Usuń zaznaczenie pola wyboru **element WindowsAzureMultiFactorAuthentication** lub **AzureMFAServerAuthentication** (w zależności od hello zainstalowaną bieżącą wersję). 

  Po wykonaniu tego kroku weryfikację dwuetapową, za pomocą serwera usługi MFA jest niedostępna w tym klastrze usług AD FS dopiero po wykonaniu kroku 8.

4. Wyrejestrowywanie hello starszej wersji hello AD FS karty, uruchamiając skrypt programu PowerShell Unregister-MultiFactorAuthenticationAdfsAdapter.ps1 hello. Upewnij się, że hello *— nazwa* parametr ("Element WindowsAzureMultiFactorAuthentication" lub "AzureMFAServerAuthentication") odpowiada nazwie hello, który był wyświetlany w kroku 3. Dotyczy to serwery tooall hello tego samego AD FS klastra, ponieważ konfiguracja centralnych.
5. Zarejestruj nowy adapter AD FS hello za pomocą skryptu PowerShell Register-MultiFactorAuthenticationAdfsAdapter.ps1 hello. Dotyczy to serwery tooall hello tego samego AD FS klastra, ponieważ konfiguracja centralnych.
6. Witaj ponownego uruchomienia usług AD FS na każdym serwerze usunięte z hello farma usług AD FS.
7. Dodaj, Usuń hello hello farmy serwerów i serwerów hello zaktualizowane kopii toohello AD FS farmy.
8. Przejdź za**usług AD FS** > **zasady uwierzytelniania** > **Edytuj globalne zasady uwierzytelniania Wieloskładnikowa**. Sprawdź **AzureMfaServerAuthentication**.
9. Powtórz krok 2 tooupdate hello serwerów, teraz są usuwane z hello AD FS farmy i ponownie uruchom program hello AD FS usługi na tych serwerach.
10. Dodaj tych serwerów do farmy hello usług AD FS.

## <a name="next-steps"></a>Następne kroki

- Pobierz przykłady [zaawansowanych scenariuszy z usługi Azure Multi-Factor Authentication i sieci VPN innych firm](multi-factor-authentication-advanced-vpn-configurations.md)

- [Synchronizowanie serwera usługi MFA z usługi Active Directory systemu Windows Server](multi-factor-authentication-get-started-server-dirint.md)

- [Skonfiguruj uwierzytelnianie systemu Windows](multi-factor-authentication-get-started-server-windows.md) dla aplikacji
