---
title: "aaaUpgrade PhoneFactor tooAzure serwera usługi MFA | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z serwera usługi Azure MFA po uaktualnieniu z hello starsze phonefactor agent."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Uaktualnij hello tooAzure PhoneFactor Agent serwera Multi-Factor Authentication
tooupgrade hello PhoneFactor Agent 5.x lub starsze tooAzure aplikacji serwer Multi-Factor Authentication, odinstaluj hello PhoneFactor Agent i powiązane składniki, najpierw. Następnie hello aplikacji serwer Multi-Factor Authentication i jej powiązane składniki mogą być instalowane.

## <a name="uninstall-hello-phonefactor-agent"></a>Odinstaluj hello PhoneFactor Agent

1. Najpierw utwórz kopię zapasową pliku danych PhoneFactor hello. Witaj, domyślna lokalizacja instalacji to C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Jeśli zainstalowano hello portalu użytkownika:
  1. Przejdź do folderu instalacyjnego toohello i utworzyć kopię zapasową pliku web.config hello. Witaj, domyślna lokalizacja instalacji to C:\inetpub\wwwroot\PhoneFactor.

  2. Po dodaniu niestandardowych kompozycji toohello portalu, wykonaj kopię zapasową niestandardowego folderu poniżej hello C:\inetpub\wwwroot\PhoneFactor\App_Themes katalogu.

  3. Odinstaluj hello portalu użytkownika, za pośrednictwem hello PhoneFactor Agent (dostępne tylko, jeśli zainstalowana na powitania tym samym serwerze co hello PhoneFactor Agent) lub za pośrednictwem systemu Windows w aplecie Programy i funkcje.

3. Jeśli zainstalowano hello Mobile App Web Service:

  1. Przejdź do folderu instalacyjnego toohello i utworzyć kopię zapasową pliku web.config hello. Witaj, domyślna lokalizacja instalacji to C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService.

  2. Odinstaluj hello Mobile App Web Service za pośrednictwem systemu Windows w aplecie Programy i funkcje.

4. Jeśli zainstalowano hello zestawu SDK usług sieci Web, należy ją odinstalować, za pośrednictwem hello PhoneFactor Agent lub systemu Windows w aplecie Programy i funkcje.

5. Odinstaluj hello PhoneFactor Agent za pomocą programów systemu Windows i funkcje.

## <a name="install-hello-multi-factor-authentication-server"></a>Zainstaluj hello aplikacji serwer Multi-Factor Authentication

Hello ścieżka instalacji jest pobierana z rejestru hello z poprzedniej instalacji hello PhoneFactor Agent, aby go zainstalować w hello takie same lokalizacji (na przykład C:\Program Files\PhoneFactor). Nowe instalacje mają inne domyślne ścieżki instalacji (np. C:\Program Files\Multi-Factor Authentication Server). Witaj pliku danych pozostawionego przez poprzednie hello PhoneFactor Agent powinny zostać uaktualnione podczas instalacji, więc ustawienia i użytkownicy nadal powinno być się, że istnieje po zainstalowaniu hello nowej aplikacji serwer Multi-Factor Authentication.

1. Jeśli zostanie wyświetlony monit, Aktywuj hello aplikacji serwer Multi-Factor Authentication i upewnij się, że jest ona przypisana toohello odpowiedniej grupie replikacji.

2. Jeśli wcześniej zainstalowano hello zestawu SDK usług sieci Web, zainstaluj hello nowego zestawu SDK usług sieci Web za pośrednictwem hello interfejs użytkownika serwera uwierzytelniania wieloskładnikowego.

  Domyślna nazwa katalogu wirtualnego jest teraz Hello **MultiFactorAuthWebServiceSdk** zamiast **PhoneFactorWebServiceSdk**. Jeśli nazwa poprzedniego hello toouse, należy zmienić nazwę hello hello katalogu wirtualnego podczas instalacji. W przeciwnym razie wartość zezwolenie hello toouse hello nowe domyślna nazwa instalacji masz toochange hello URL w aplikacji hello tego odwołania zestawu SDK usług sieci Web (na przykład hello portalu użytkowników i Mobile App Web Service) toopoint w poprawnej lokalizacji hello.

3. Jeśli hello Portal użytkowników została poprzednio zainstalowana na powitania serwera agenta PhoneFactor, zainstaluj hello nowy Portal użytkowników usługi Multi-Factor Authentication za pośrednictwem hello interfejs użytkownika serwera uwierzytelniania wieloskładnikowego.

  Domyślna nazwa katalogu wirtualnego jest teraz Hello **MultiFactorAuth** zamiast **PhoneFactor**. Jeśli nazwa poprzedniego hello toouse, należy zmienić nazwę hello hello katalogu wirtualnego podczas instalacji. W przeciwnym razie jeśli zezwolisz hello toouse hello nowe domyślna nazwa instalacji należy kliknij ikonę Portal użytkowników hello na powitania serwera Multi-Factor Authentication i aktualizować hello adres URL portalu użytkowników na karcie Ustawienia hello.

4. Jeśli hello na innym serwerze z hello PhoneFactor Agent został wcześniej zainstalowany Portal użytkowników i/lub usługa sieci Web aplikacji mobilnej:

  1. Przejdź do lokalizacji instalacji toohello (na przykład C:\Program Files\PhoneFactor), a następnie skopiuj toohello instalatory co najmniej jeden inny serwer. Istnieje 32-bitowe i 64-bitowe instalatorów hello portalu użytkowników i Mobile App Web Service. Mają one nazwy MultiFactorAuthenticationUserPortalSetupXX.msi i MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. tooinstall hello Portal użytkowników na serwerze sieci web hello, otwórz wiersz polecenia jako administrator i uruchom MultiFactorAuthenticationUserPortalSetupXX.msi.

    Domyślna nazwa katalogu wirtualnego jest teraz Hello **MultiFactorAuth** zamiast **PhoneFactor**. Jeśli nazwa poprzedniego hello toouse, należy zmienić nazwę hello hello katalogu wirtualnego podczas instalacji. W przeciwnym razie jeśli zezwolisz hello toouse hello nowe domyślna nazwa instalacji należy kliknij ikonę Portal użytkowników hello na powitania serwera Multi-Factor Authentication i aktualizować hello adres URL portalu użytkowników na karcie Ustawienia hello. Istniejący użytkownicy muszą toobe o hello nowego adresu URL.

  3. Przejdź do lokalizacji instalacji toohello portalu użytkowników (na przykład C:\inetpub\wwwroot\MultiFactorAuth) i edytowania pliku web.config hello. Skopiuj wartości hello w sekcji appSettings i applicationSettings hello oryginalnego pliku web.config, które utworzono kopię zapasową przed uaktualnieniem hello na powitania nowy plik web.config. Nową nazwę katalogu wirtualnego domyślne hello znajdowały się podczas instalowania hello zestawu SDK usług sieci Web, zmiana adresu URL hello w hello applicationSettings sekcji toopoint toohello bieżącej lokalizacji. W przypadku innych wartości domyślnych zostały zmienione w pliku web.config poprzedniej hello, zastosuj tych samym zmiany toohello nowy plik web.config.

  4. tooinstall hello Mobile App Web Service na serwerze sieci web hello, otwórz wiersz polecenia jako administrator i uruchom hello MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

    Domyślna nazwa katalogu wirtualnego jest teraz Hello **wartość MultiFactorAuthMobileAppWebService** zamiast **PhoneFactorPhoneAppWebService**. Jeśli nazwa poprzedniego hello toouse, należy zmienić nazwę hello hello katalogu wirtualnego podczas instalacji. Może być toochoose krótszą toomake nazwa go łatwo tootype użytkowników końcowych w urządzeniach przenośnych. W przeciwnym razie jeśli zezwolisz hello toouse hello nowe domyślna nazwa instalacji należy kliknij ikonę aplikacji mobilnej hello na powitania serwera Multi-Factor Authentication i aktualizować hello URL usługi sieci Web aplikacji mobilnej.

  5. Przejdź do lokalizacji instalacji usługi sieci Web aplikacji mobilnej toohello (na przykład C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) i edytowania pliku web.config hello. Skopiuj wartości hello w sekcji appSettings i applicationSettings hello oryginalnego pliku web.config, które utworzono kopię zapasową przed uaktualnieniem hello na powitania nowy plik web.config. Nową nazwę katalogu wirtualnego domyślne hello znajdowały się podczas instalowania hello zestawu SDK usług sieci Web, zmiana adresu URL hello w hello applicationSettings sekcji toopoint toohello bieżącej lokalizacji. W przypadku innych wartości domyślnych zostały zmienione w pliku web.config poprzedniej hello, zastosuj tych samym zmiany toohello nowy plik web.config.

## <a name="next-steps"></a>Następne kroki

- [Zainstaluj portal użytkowników hello](multi-factor-authentication-get-started-portal.md) na powitania serwera usługi Azure Multi-Factor Authentication.

- [Skonfiguruj uwierzytelnianie systemu Windows](multi-factor-authentication-get-started-server-windows.md) dla aplikacji. 
