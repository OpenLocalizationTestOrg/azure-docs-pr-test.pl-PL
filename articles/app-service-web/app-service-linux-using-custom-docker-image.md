---
title: "Sposób użycia niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Jak używać niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux."
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
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Przy użyciu niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Usługi aplikacji umożliwia stosy wstępnie zdefiniowanych aplikacji w systemie Linux obsługę dla określonej wersji, takich jak PHP w wersji 7.0 i Node.js 4.5. Usługa aplikacji w systemie Linux używa kontenerów Docker do obsługi tych stosów wstępnie zbudowanych aplikacji. Aby wdrożyć aplikację sieci web stosu aplikacji, która nie jest już zdefiniowana w Azure umożliwia także niestandardowego obrazu Docker. Niestandardowe obrazy usługi Docker może być hostowana na obu publicznych lub prywatnych Docker repozytorium.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Porady: Ustawianie obrazu niestandardowego Docker dla aplikacji sieci web
Można ustawić niestandardowego obrazu Docker obie aplikacje nowych i istniejących sieci Web. Po utworzeniu aplikacji sieci web w systemie Linux w [portalu Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), kliknij przycisk **kontenera konfiguracji** można ustawić niestandardowego obrazu Docker:

![Niestandardowy obraz Docker dla nowej aplikacji sieci web w systemie Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Porady: użycie niestandardowego obrazu Docker z Centrum Docker ##
Aby użyć niestandardowego obrazu Docker z Centrum Docker:

1. W [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.

2.  Wybierz **Centrum Docker** jako **źródło obrazu**, następnie kliknij opcję **publicznego** lub **prywatnej** i wpisz **obrazu i Nazwa tagu opcjonalne**, takich jak `node:4.5`. **Uruchomienia polecenia** jest zestaw automatycznie na podstawie co to jest zdefiniowana w pliku obrazu Docker, ale możesz ustawić własne polecenia.  

    ![Konfigurowanie Centrum Docker publicznego repozytorium obrazów][2]

    W przypadku obrazu z prywatnym repozytorium, należy wprowadzić poświadczenia Centrum Docker jako (**nazwa logowania użytkownika** i **hasło**) do prywatnego repozytorium Centrum Docker.

    ![Konfigurowanie Centrum Docker prywatnym repozytorium obrazów][3]

3. Po skonfigurowaniu kontenera, kliknij przycisk **zapisać**.

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a>Jak używać obrazu platformy Docker z rejestru prywatnej obrazu ##
Aby użyć niestandardowego obrazu Docker z rejestru prywatnej obrazu:

1. W [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.

2.  Kliknij przycisk **prywatnej rejestru** jako **źródło obrazu**. Wprowadź **obrazu i nazwę tagu opcjonalne**, **adres URL serwera** dla prywatnych rejestru, oraz poświadczenia (**nazwa logowania użytkownika** i **hasło**). Kliknij pozycję **Zapisz**.

    ![Konfigurowanie obrazu Docker z rejestru prywatnych][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a>Porady: Ustawianie portu używanego przez obraz Docker ##

Jeśli używasz niestandardowego obrazu Docker dla aplikacji sieci web, możesz użyć `WEBSITES_PORT` zmiennej środowiskowej w Twojej plik Dockerfile pobiera dodać do kontenera wygenerowany. Rozważmy poniższy przykład przedstawia plik docker dla dopisków fonetycznych aplikacji:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Na ostatnim wierszu polecenia można zobaczyć, że zmienna środowiskowa WEBSITES_PORT jest przekazywany w czasie wykonywania. Należy pamiętać, że wielkość liter ma znaczenie w poleceniach.

Poprzednio używał platformy `PORT` aplikacji ustawienie, firma Microsoft planuje zastąpić użycie tej aplikacji, ustawienia i przenieść przy użyciu `WEBSITES_PORT` wyłącznie.

Korzystając z istniejącego obrazu platformy Docker utworzony przez inną osobę, konieczne może być Określ port inny niż port 80 dla aplikacji. Aby skonfigurować port, dodaj aplikację, ustawienie o nazwie `WEBSITES_PORT` z wartością, jak pokazano poniżej:

![Skonfiguruj ustawienia aplikacji portu dla niestandardowego obrazu Docker][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a>Porady: Ustawianie czasu uruchamiania obrazu Docker ##

Domyślnie jeśli nie można uruchomić z kontenera przed 230 sekund platformy zostanie uruchomiony ponownie z kontenera. Jeśli obraz niestandardowy Docker rozpoczyna się w więcej niż 230 sekund, możesz użyć `WEBSITES_CONTAINER_START_TIME_LIMIT` aplikacji ustawienie, wartość tego ustawienia w sekundach, pozwoli to zachować platformy z kontenera uruchomiona przed ponownym jego uruchomieniem. Wartość domyślna to 230 sekund, a maksymalna dopuszczalna wartość wynosi 600 sekund.

## <a name="how-to-unmount-the-platform-provided-storage"></a>Porady: Odinstaluj magazynu platforma pochodząca ##

Domyślnie platforma będzie zainstalować udział magazynu trwałego na `\home\` katalogu. Obraz kontenera trwałego udziału nie jest konieczne, można wyłączyć instalowanie magazynu przez ustawienie `WEBSITES_ENABLE_APP_SERVICE_STORAGE` ustawienia aplikacji na `false`. Masz nadal dostęp do tego magazynu z lokacji scm, a wszystkie dzienniki Docker (jeśli jest włączona) będą zapisywane pliki dziennika wygenerowane przez platformę.

## <a name="how-to-switch-back-to-using-a-built-in-image"></a>Porady: wrócić do przy użyciu wbudowanych obrazu ##

Aby przełączyć się z przy użyciu niestandardowego obrazu przy użyciu wbudowanych obrazu:

1. W [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **usługi aplikacji**.

2. Wybierz użytkownika **stosu środowiska uruchomieniowego** do użycia wbudowanych obrazu, następnie kliknij przycisk **zapisać**. 

![Konfigurowanie obrazu wbudowanych Docker][5]


## <a name="troubleshooting"></a>Rozwiązywanie problemów ##

Gdy aplikacja nie można uruchomić z niestandardowego obrazu Docker, sprawdź dzienniki Docker w katalogu LogFiles. Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.
W dzienniku `stdout` i `stderr` z Twojej kontenera, musisz włączyć **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.

![Włączanie rejestrowania][8]

![Aby wyświetlić dzienniki Docker przy użyciu Kudu][7]

Można uzyskać dostępu do lokacji SCM z **zaawansowane narzędzia** w **narzędzi programistycznych** menu.

## <a name="next-steps"></a>Następne kroki ##

Wykonaj poniższe łącza, aby rozpocząć korzystanie z aplikacji sieci Web w systemie Linux.   

* [Wprowadzenie do aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-intro.md)
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
