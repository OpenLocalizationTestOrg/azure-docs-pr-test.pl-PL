---
title: "aaaAzure aplikację usługi sieci Web aplikacji na systemie Linux — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, często zadawane pytania, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Witaj wersji z aplikacji sieci Web w systemie Linux pracujemy nad Dodawanie funkcji oraz wprowadzania ulepszenia tooour platformy. W tym miejscu przedstawiono często zadawane pytania (FAQ), które naszym klientom ma zostały prośbą za pośrednictwem hello ostatnio miesięcy.
Jeśli masz pytania, komentarza, w artykule hello i firma Microsoft będzie odpowiedź tak szybko, jak to możliwe.

## <a name="built-in-images"></a>Wbudowane obrazów

**Pytanie:** ma zapewnia toofork hello wbudowanych Docker kontenerów, które hello platformy. Gdzie można znaleźć te pliki?

**Odpowiedź:** wszystkie pliki Docker można znaleźć w [GitHub](https://github.com/azure-app-service). Możesz znaleźć wszystkie kontenery Docker na [Centrum Docker](https://hub.docker.com/u/appsvc/).

**Pytanie:** co to są hello oczekiwanych wartości dla hello sekcji uruchamiania pliku podczas konfigurowania stosu środowiska uruchomieniowego hello?

**Odpowiedź:** dla środowiska Node.Js, określ plik konfiguracyjny hello PM2 lub plik skryptu. Określ nazwę skompilowanej biblioteki DLL dla platformy .NET Core. Dla środowiska Ruby, można określić hello skryptu dopisków fonetycznych, które mają tooinitialize aplikacji za pomocą.

## <a name="management"></a>Zarządzanie

**Pytanie:** co się stanie po naciśnięciu przycisku ponownego uruchomienia hello w portalu Azure hello?

**Odpowiedź:** hello jest to równoważne Docker ponownego uruchamiania.

**Pytanie:** można użyć aplikacji toohello tooconnect Secure Shell (SSH) kontenera maszyny wirtualnej (VM)?

**Odpowiedź:** tak, czy za pośrednictwem witryny SCM hello, sprawdź następujące hello artykuł Aby uzyskać więcej informacji [Obsługa protokołu SSH dla aplikacji sieci Web w systemie Linux](./app-service-linux-ssh-support.md)

**Pytanie:** ma toocreate płaszczyźnie Linux App Service przy użyciu zestawu SDK lub szablon ARM, jak można to osiągnąć?

**A:** należy tooset hello `reserved` pola aplikacji hello usługi zbyt`true`.

## <a name="continuous-integrationdeployment"></a>Ciągła integracja/wdrożenia

**Pytanie:** Moja aplikacja sieci web nadal używa stary obraz kontenera Docker po po aktualizacji obraz powitania w Centrum Docker. Czy ciągłej integracji/wdrożenia kontenerów niestandardowe są obsługiwane?

**Odpowiedź:** tooset ciągłej integracji/wdrożenia obrazów rejestru kontenera platformy Azure lub DockerHub przez hello wyboru poniższego artykułu [ciągłego wdrażania z aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md). Dla prywatnych rejestrów można odświeżyć hello kontenera przez zatrzymanie i uruchomienie następnie aplikacji sieci web. Lub możesz zmienić lub dodać aplikację fikcyjny ustawienie tooforce odświeżania z kontenera.

**Pytanie:** czy środowisk przemieszczania są obsługiwane?

**Odpowiedź:** tak.

**Pytanie:** można użyć **narzędzia web deploy** toodeploy Moja aplikacja sieci web?

**Odpowiedź:** tak, potrzebujesz tooset aplikacji nosi nazwę `WEBSITE_WEBDEPLOY_USE_SCM` zbyt`false`.

## <a name="language-support"></a>Obsługa języków

**Pytanie:** czy nie skompilowanego aplikacji .NET Core są obsługiwane?

**Odpowiedź:** tak.

**Pytanie:** są obsługiwane Composer Menedżer zależności dla aplikacji PHP?

**Odpowiedź:** tak. Podczas wdrażania narzędzia Git Kudu powinna wykryć wdrażania aplikacji PHP (Dziękujemy toohello obecność pliku composer.json), a następnie wyzwala instalacji composer dla Ciebie.

## <a name="custom-containers"></a>Kontenery niestandardowych

**Pytanie:** używam własne niestandardowe kontenera. Moja aplikacja znajduje się w hello `\home\` katalogu, ale nie można odnaleźć plików I przeglądających hello zawartości przy użyciu hello [lokacji SCM](https://github.com/projectkudu/kudu) lub klient FTP. Gdzie są pliki?

**Odpowiedź:** możemy zainstalować toohello udziału SMB `\home\` katalogu. Spowoduje to zastąpienie zawartość, która jest.

**Pytanie:** używam własne niestandardowe kontenera. Nie chcę hello platformy toomount toohello udziału SMB `\home\`.

**Odpowiedź:** możesz to zrobić przez ustawienie hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplikacji ustawienie zbyt`false`.

**Pytanie:** Moje niestandardowe kontenera przyjmuje toostart dużo czasu i hello platformy ponownego uruchomienia hello kontenera przed zakończeniem uruchamiania.

**Odpowiedź:** możesz skonfigurować czas hello platformy hello czeka przed ponownym uruchomieniem z kontenera. Można to zrobić przez ustawienie hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello ustawienie aplikacji Żądana wartość w sekundach. domyślną Hello jest 230 sekund, a maksymalna hello jest 600 sekund.

**Pytanie:** co to jest hello format adresu url serwera prywatnej rejestru?

**Odpowiedź:** należy tooprovide hello rejestru pełnego adresu url w tym `http://` lub `https://`.

**Pytanie:** co to jest hello format nazw obraz powitania w opcji prywatnych rejestru?

**Odpowiedź:** potrzebna nazwa pełny obraz powitania tooadd tym hello prywatnej rejestru url (np. myacr.azurecr.IO/DotNet:Latest)

**Pytanie:** ma więcej niż jeden port tooexpose na obraz niestandardowy kontenera. Jest to możliwe?

**Odpowiedź:** obecnie, która nie jest obsługiwana.

**Pytanie:** własnych magazynu można przełączyć?

**Odpowiedź:** która obecnie nie jest obsługiwana.

**Pytanie:** I nie może przejrzeć Moje niestandardowe kontenera procesy systemu lub z systemem plików z witryny SCM hello. Dlaczego jest to, że?

**Odpowiedź:** hello SCM witryna jest uruchamiana w oddzielnym kontenera. Nie można sprawdzić system plików hello lub uruchomionych procesów hello kontenera aplikacji.

**Pytanie:** Moje niestandardowe kontenera nasłuchuje tooa portu innego niż port 80. Jak można skonfigurować port tooroute toothat żądań hello mojej aplikacji?

**Odpowiedź:** mamy automatyczne wykrywanie portu, można również określić aplikacja nosi nazwę **WEBSITES_PORT**i nadaj mu wartość hello hello oczekiwany numer portu. Poprzednio używał platformy hello `PORT` aplikacji, możemy planowania użycia hello toodeprecate tej aplikacji, ustawienia i Przenieś toousing `WEBSITES_PORT` wyłącznie.

**Pytanie:** należy tooimplement HTTPS w mojej niestandardowych kontenera.

**Odpowiedź:** nie, hello platformy obsługuje zakończenia połączenia HTTPS w frontends hello udostępnionych.

## <a name="pricing-and-sla"></a>Cennik i umowy SLA

**Pytanie:** co to jest hello cennik podczas korzystania z publicznej wersji zapoznawczej hello?

**Odpowiedź:** połowa hello liczbę godzin, w których aplikacja będzie działać, z normalnym cennik usługi aplikacji Azure hello są naliczane. Oznacza to, że możesz uzyskać rabat 50 procent normalne cennik usługi aplikacji Azure.

## <a name="other"></a>Inne

**Pytanie:** co to są hello obsługiwane znaki w nazwach ustawienia aplikacji?

**Odpowiedź:** można tylko użyć A-Z, a-z, 0-9 i hello podkreślenia dla ustawienia aplikacji.

**Pytanie:** których mogą żądać nowych funkcji?

**A:** można przesłać Twój pomysł na powitania [forum opinii aplikacje sieci Web](https://aka.ms/webapps-uservoice). Dodaj tytuł toohello "[Linux]" Twój pomysł.

## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](app-service-linux-intro.md)
* [Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ssh-support.md)
* [Konfigurowanie środowisk w usłudze Azure App Service przejściowych](./web-sites-staged-publishing.md)
* [Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md)
