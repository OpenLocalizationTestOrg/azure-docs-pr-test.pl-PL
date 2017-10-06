---
title: toouse aaaHow niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft
description: Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux.
keywords: "Usługa aplikacji Azure, aplikacji sieci web, linux, docker, kontenera"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Przy użyciu niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Usługi aplikacji umożliwia stosy wstępnie zdefiniowanych aplikacji w systemie Linux obsługę dla określonej wersji, takich jak PHP w wersji 7.0 i Node.js 4.5. Usługa aplikacji w systemie Linux używa kontenerów Docker toohost te wstępnie skompilowany stosy aplikacji. Umożliwia także niestandardowych toodeploy obrazu Docker stosu sieci web aplikacji tooan aplikacji, która nie jest już zdefiniowany w systemie Azure. Niestandardowe obrazy usługi Docker może być hostowana na obu publicznych lub prywatnych Docker repozytorium.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Porady: Ustawianie obrazu niestandardowego Docker dla aplikacji sieci web
Można ustawić hello niestandardowego obrazu Docker dla obu tych nowych i istniejących aplikacji sieci Web. Po utworzeniu aplikacji sieci web w systemie Linux w hello [portalu Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), kliknij przycisk **kontenera konfiguracji** tooset niestandardowego obrazu Docker:

![Niestandardowy obraz Docker dla nowej aplikacji sieci web w systemie Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Porady: użycie niestandardowego obrazu Docker z Centrum Docker ##
toouse niestandardowego obrazu Docker z Centrum Docker:

1. W hello [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.

2.  Wybierz **Centrum Docker** jako hello **źródło obrazu**, następnie kliknij opcję **publicznego** lub **prywatnej** i typ hello **obrazu i Nazwa tagu opcjonalne**, takich jak `node:4.5`. Witaj **uruchomienia polecenia** jest zestaw automatycznie na podstawie co to jest zdefiniowany w pliku obrazu Docker hello, ale możesz ustawić własne polecenia.  

    ![Konfigurowanie Centrum Docker publicznego repozytorium obrazów][2]

    W przypadku obrazu z prywatnym repozytorium, należy również tooenter hello Centrum Docker poświadczenia w postaci (**nazwa logowania użytkownika** i **hasło**) hello prywatne repozytorium Centrum Docker.

    ![Konfigurowanie Centrum Docker prywatnym repozytorium obrazów][3]

3. Po skonfigurowaniu kontenera powitania kliknij **zapisać**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Jak toouse Docker obraz z rejestru prywatnej obrazu ##
toouse niestandardowego obrazu Docker z rejestru prywatnej obrazu:

1. W hello [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.

2.  Kliknij przycisk **prywatnej rejestru** jako hello **źródło obrazu**. Wprowadź hello **obrazu i nazwę tagu opcjonalne**, **adres URL serwera** dla prywatnych rejestru hello wraz z poświadczeniami hello (**nazwa logowania użytkownika** i **hasła** ). Kliknij pozycję **Zapisz**.

    ![Konfigurowanie obrazu Docker z rejestru prywatnych][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Porady: Ustawianie hello port używany przez obraz Docker ##

Korzystając z niestandardowego obrazu Docker dla aplikacji sieci web, można użyć hello `WEBSITES_PORT` zmiennej środowiskowej w Twojej plik Dockerfile pobiera dodać kontener toohello wygenerowany. Należy wziąć pod uwagę następujące przykładowy plik docker dopisków fonetycznych aplikacji hello:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Ostatniego wiersza polecenia hello można zauważyć, że tej zmiennej środowiskowej WEBSITES_PORT hello jest przekazywany w czasie wykonywania. Należy pamiętać, że wielkość liter ma znaczenie w poleceniach.

Poprzednio używał platformy hello `PORT` aplikacji, możemy planowania użycia hello toodeprecate tej aplikacji, ustawienia i Przenieś toousing `WEBSITES_PORT` wyłącznie.

Korzystając z istniejącego obrazu platformy Docker utworzony przez inną osobę, może być konieczne toospecify portu innego niż port 80 dla aplikacji hello. tooconfigure hello portu, dodaj aplikację, ustawienie o nazwie `WEBSITES_PORT` z wartością hello, jak pokazano poniżej:

![Skonfiguruj ustawienia aplikacji portu dla niestandardowego obrazu Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Porady: ustawić czas uruchamiania hello obrazu Docker ##

Domyślnie jeśli nie można uruchomić z kontenera przed 230 sekund platformy hello zostanie uruchomiony ponownie z kontenera. Jeśli obraz niestandardowy Docker rozpoczyna się w więcej niż 230 sekund, można użyć hello `WEBSITES_CONTAINER_START_TIME_LIMIT` ustawienie aplikacji hello wartość tego ustawienia w sekundach, pozwoli to zachować platformy hello z kontenera uruchomiona przed ponownym jego uruchomieniem. Witaj, wartością domyślną jest 230 sekund i hello maksymalny dozwolony, czy wartość jest 600 sekund.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Porady: Odinstaluj hello platforma pochodząca magazynu ##

Domyślnie platforma hello zainstaluje toohello udziału magazynu trwałego `\home\` katalogu. Obraz kontenera trwałego udziału nie jest konieczne, można wyłączyć instalowanie magazynu przez ustawienie hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplikacji ustawienie zbyt`false`. Nadal będziesz mieć dostęp do magazynu toothat z hello scm lokacji, a wszystkie dzienniki Docker (jeśli jest włączona) zostanie zapisany toohello plików dziennika generowanych przez hello platformy.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Porady: Przejdź z powrotem toousing wbudowanych obrazu ##

tooswitch z przy użyciu niestandardowego obrazu toousing wbudowanych obrazu:

1. W hello [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **usługi aplikacji**.

2. Wybierz użytkownika **stosu środowiska uruchomieniowego** toouse hello wbudowanych obrazu, następnie kliknij przycisk **zapisać**. 

![Konfigurowanie obrazu wbudowanych Docker][5]


## <a name="troubleshooting"></a>Rozwiązywanie problemów ##

W przypadku awarii aplikacji toostart z niestandardowego obrazu Docker Sprawdź hello dzienniki w katalogu LogFiles hello Docker. Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.
toolog hello `stdout` i `stderr` z Twojej kontenera należy tooenable **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.

![Włączanie rejestrowania][8]

![Przy użyciu dzienników Docker tooview Kudu][7]

Można uzyskać dostępu do hello SCM lokacji z **zaawansowane narzędzia** w hello **narzędzi programistycznych** menu.

## <a name="next-steps"></a>Następne kroki ##

Wykonaj hello następującego łącza tooget wprowadzenie do aplikacji sieci Web w systemie Linux.   

* [Wprowadzenie tooAzure aplikacji sieci Web w systemie Linux](./app-service-linux-intro.md)
* [Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-using-nodejs-pm2.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](app-service-linux-faq.md)

Opublikuj pytania i uwagi na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
