---
title: "Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Wraz z wydaniem aplikacji sieci Web w systemie Linux pracujemy nad Dodawanie funkcji i wprowadzać ulepszenia platformy. Poniżej przedstawiono niektóre często zadawane pytania (FAQ), które naszym klientom ma zostały prośbą z ostatnich miesięcy.
Jeśli masz pytania, komentarza, w artykule i firma Microsoft będzie odpowiedź tak szybko, jak to możliwe.

## <a name="built-in-images"></a>Wbudowane obrazów

**Pytanie:** chcę rozwidlania wbudowanych kontenerów Docker, które zapewnia platformę. Gdzie można znaleźć te pliki?

**Odpowiedź:** wszystkie pliki Docker można znaleźć w [GitHub](https://github.com/azure-app-service). Możesz znaleźć wszystkie kontenery Docker na [Centrum Docker](https://hub.docker.com/u/appsvc/).

**Pytanie:** co to są oczekiwanych wartości dla pliku uruchomienia sekcji podczas konfigurowania środowiska uruchomieniowego stosu?

**Odpowiedź:** dla środowiska Node.Js, określ plik konfiguracyjny PM2 lub plik skryptu. Określ nazwę skompilowanej biblioteki DLL dla platformy .NET Core. Dla środowiska Ruby można określić skrypt dopisków fonetycznych, który chcesz zainicjować aplikacji za pomocą.

## <a name="management"></a>Zarządzanie

**Pytanie:** co się stanie po naciśnięciu przycisku ponownego uruchomienia w portalu Azure?

**Odpowiedź:** to odpowiednik Docker ponownego uruchomienia komputera.

**Pytanie:** czy za pomocą protokołu Secure Shell (SSH) można nawiązać połączenia z aplikacji kontenera maszyny wirtualnej (VM)?

**Odpowiedź:** tak, możesz to zrobić za pośrednictwem witryny SCM, sprawdź następujący artykuł, aby uzyskać więcej informacji [Obsługa protokołu SSH dla aplikacji sieci Web w systemie Linux](./app-service-linux-ssh-support.md)

**Pytanie:** Utwórz płaszczyźnie Linux App Service przy użyciu zestawu SDK lub szablon ARM, jak można to osiągnąć?

**Odpowiedź:** należy ustawić `reserved` pole app service w celu `true`.

## <a name="continuous-integrationdeployment"></a>Ciągła integracja/wdrożenia

**Pytanie:** Moja aplikacja sieci web nadal używa stary obraz kontenera Docker po po aktualizacji obraz Centrum Docker. Czy ciągłej integracji/wdrożenia kontenerów niestandardowe są obsługiwane?

**A:** do skonfigurowania integracji ciągłej/wdrożenia do rejestru kontenera platformy Azure lub DockerHub obrazy sprawdzając artykule [ciągłego wdrażania z aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md). Dla prywatnych rejestrów można odświeżyć kontenera przez zatrzymanie i uruchomienie następnie aplikacji sieci web. Lub możesz zmienić lub Dodaj ustawienie aplikacji fikcyjny, aby wymusić odświeżenie z kontenera.

**Pytanie:** czy środowisk przemieszczania są obsługiwane?

**Odpowiedź:** tak.

**Pytanie:** można użyć **narzędzia web deploy** wdrażania Moja aplikacja sieci web?

**Odpowiedź:** tak, należy określić aplikację nosi nazwę `WEBSITE_WEBDEPLOY_USE_SCM` do `false`.

## <a name="language-support"></a>Obsługa języków

**Pytanie:** czy nie skompilowanego aplikacji .NET Core są obsługiwane?

**Odpowiedź:** tak.

**Pytanie:** są obsługiwane Composer Menedżer zależności dla aplikacji PHP?

**Odpowiedź:** tak. Podczas wdrażania narzędzia Git Kudu powinna wykryć wdrażania aplikacji PHP (dzięki użyciu obecność pliku composer.json), a następnie wyzwala instalacji composer dla Ciebie.

## <a name="custom-containers"></a>Kontenery niestandardowych

**Pytanie:** używam własne niestandardowe kontenera. Moja aplikacja znajduje się w `\home\` katalogu, ale nie można odnaleźć plików, podczas I przeglądać zawartość przy użyciu [lokacji SCM](https://github.com/projectkudu/kudu) lub klient FTP. Gdzie są pliki?

**Odpowiedź:** możemy instalowanie udziału SMB do `\home\` katalogu. Spowoduje to zastąpienie zawartość, która jest.

**Pytanie:** używam własne niestandardowe kontenera. Nie chcę platformy w celu zainstalowania udziału SMB do `\home\`.

**Odpowiedź:** możesz to zrobić przez ustawienie `WEBSITES_ENABLE_APP_SERVICE_STORAGE` ustawienia aplikacji na `false`.

**Pytanie:** Moje niestandardowe kontenera zajmuje dużo czasu do uruchomienia i platforma Uruchom kontenera przed zakończeniem uruchamiania.

**Odpowiedź:** możesz skonfigurować czas platformy będzie czekać przed ponownym uruchomieniem z kontenera. Można to zrobić przez ustawienie `WEBSITES_CONTAINER_START_TIME_LIMIT` ustawienia aplikacji na żądaną wartość w sekundach. Wartość domyślna to 230 sekund, a maksymalna to 600 sekund.

**Pytanie:** co to jest format adresu url serwera prywatnej rejestru?

**Odpowiedź:** musisz podać z rejestru pełnego adresu url, w tym `http://` lub `https://`.

**Pytanie:** co to jest format nazwy obrazu w opcji prywatnych rejestru?

**Odpowiedź:** należy dodać nazwę pełnego obrazu tym rejestru prywatnego adresu url (np. myacr.azurecr.IO/DotNet:Latest)

**Pytanie:** warto udostępnić więcej niż jeden port na obraz niestandardowy kontenera. Jest to możliwe?

**Odpowiedź:** obecnie, która nie jest obsługiwana.

**Pytanie:** własnych magazynu można przełączyć?

**Odpowiedź:** która obecnie nie jest obsługiwana.

**Pytanie:** I nie może przejrzeć Moje niestandardowe kontenera procesy systemu lub z systemem plików z lokacji, Menedżer sterowania usługami. Dlaczego jest to, że?

**Odpowiedź:** SCM witryna jest uruchamiana w oddzielnym kontenera. Nie można sprawdzić procesy systemu lub z systemem plików kontenera aplikacji.

**Pytanie:** Moje niestandardowe kontenera nasłuchuje portu innego niż port 80. Jak można skonfigurować mojej aplikacji można przekierować żądania do tego portu

**A:** mamy automatyczne wykrywanie portu, można również określić aplikacja nosi nazwę **WEBSITES_PORT**i nadaj mu wartość numeru portu oczekiwanego. Poprzednio używał platformy `PORT` aplikacji ustawienie, firma Microsoft planuje zastąpić użycie tej aplikacji, ustawienia i przenieść przy użyciu `WEBSITES_PORT` wyłącznie.

**Pytanie:** należy zaimplementować HTTPS w mojej niestandardowych kontenera.

**Odpowiedź:** nie, platforma obsługuje zakończenia połączenia HTTPS w frontends udostępnionego.

## <a name="pricing-and-sla"></a>Cennik i umowy SLA

**Pytanie:** co to jest cennik podczas korzystania z publicznej wersji zapoznawczej?

**Odpowiedź:** połowie liczby godzin, w których aplikacja będzie działać, z normalnym cennik usługi aplikacji Azure są naliczane. Oznacza to, że możesz uzyskać rabat 50 procent normalne cennik usługi aplikacji Azure.

## <a name="other"></a>Inne

**Pytanie:** co to są obsługiwane znaki w nazwach ustawienia aplikacji?

**Odpowiedź:** A-Z, a-z, 0-9 i znak podkreślenia można używać tylko dla ustawień aplikacji.

**Pytanie:** których mogą żądać nowych funkcji?

**Odpowiedź:** mogą przesyłać Twój pomysł na [forum opinii aplikacje sieci Web](https://aka.ms/webapps-uservoice). Do tytułu Twój pomysł, należy dodać "[Linux]".

## <a name="next-steps"></a>Następne kroki
* [Co to jest aplikacja sieci Web Azure w systemie Linux?](app-service-linux-intro.md)
* [Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ssh-support.md)
* [Konfigurowanie środowisk w usłudze Azure App Service przejściowych](./web-sites-staged-publishing.md)
* [Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md)
