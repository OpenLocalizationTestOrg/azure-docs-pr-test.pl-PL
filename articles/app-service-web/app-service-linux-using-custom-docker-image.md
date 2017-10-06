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
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="f427f-104">Przy użyciu niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f427f-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="f427f-105">Usługi aplikacji umożliwia stosy wstępnie zdefiniowanych aplikacji w systemie Linux obsługę dla określonej wersji, takich jak PHP w wersji 7.0 i Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="f427f-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="f427f-106">Usługa aplikacji w systemie Linux używa kontenerów Docker toohost te wstępnie skompilowany stosy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f427f-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="f427f-107">Umożliwia także niestandardowych toodeploy obrazu Docker stosu sieci web aplikacji tooan aplikacji, która nie jest już zdefiniowany w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="f427f-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="f427f-108">Niestandardowe obrazy usługi Docker może być hostowana na obu publicznych lub prywatnych Docker repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f427f-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="f427f-109">Porady: Ustawianie obrazu niestandardowego Docker dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="f427f-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="f427f-110">Można ustawić hello niestandardowego obrazu Docker dla obu tych nowych i istniejących aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f427f-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="f427f-111">Po utworzeniu aplikacji sieci web w systemie Linux w hello [portalu Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), kliknij przycisk **kontenera konfiguracji** tooset niestandardowego obrazu Docker:</span><span class="sxs-lookup"><span data-stu-id="f427f-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Niestandardowy obraz Docker dla nowej aplikacji sieci web w systemie Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="f427f-113">Porady: użycie niestandardowego obrazu Docker z Centrum Docker</span><span class="sxs-lookup"><span data-stu-id="f427f-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="f427f-114">toouse niestandardowego obrazu Docker z Centrum Docker:</span><span class="sxs-lookup"><span data-stu-id="f427f-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="f427f-115">W hello [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.</span><span class="sxs-lookup"><span data-stu-id="f427f-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="f427f-116">Wybierz **Centrum Docker** jako hello **źródło obrazu**, następnie kliknij opcję **publicznego** lub **prywatnej** i typ hello **obrazu i Nazwa tagu opcjonalne**, takich jak `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="f427f-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="f427f-117">Witaj **uruchomienia polecenia** jest zestaw automatycznie na podstawie co to jest zdefiniowany w pliku obrazu Docker hello, ale możesz ustawić własne polecenia.</span><span class="sxs-lookup"><span data-stu-id="f427f-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Konfigurowanie Centrum Docker publicznego repozytorium obrazów][2]

    <span data-ttu-id="f427f-119">W przypadku obrazu z prywatnym repozytorium, należy również tooenter hello Centrum Docker poświadczenia w postaci (**nazwa logowania użytkownika** i **hasło**) hello prywatne repozytorium Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="f427f-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Konfigurowanie Centrum Docker prywatnym repozytorium obrazów][3]

3. <span data-ttu-id="f427f-121">Po skonfigurowaniu kontenera powitania kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="f427f-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="f427f-122">Jak toouse Docker obraz z rejestru prywatnej obrazu</span><span class="sxs-lookup"><span data-stu-id="f427f-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="f427f-123">toouse niestandardowego obrazu Docker z rejestru prywatnej obrazu:</span><span class="sxs-lookup"><span data-stu-id="f427f-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="f427f-124">W hello [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.</span><span class="sxs-lookup"><span data-stu-id="f427f-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="f427f-125">Kliknij przycisk **prywatnej rejestru** jako hello **źródło obrazu**.</span><span class="sxs-lookup"><span data-stu-id="f427f-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="f427f-126">Wprowadź hello **obrazu i nazwę tagu opcjonalne**, **adres URL serwera** dla prywatnych rejestru hello wraz z poświadczeniami hello (**nazwa logowania użytkownika** i **hasła** ).</span><span class="sxs-lookup"><span data-stu-id="f427f-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="f427f-127">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f427f-127">Click **Save**.</span></span>

    ![Konfigurowanie obrazu Docker z rejestru prywatnych][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="f427f-129">Porady: Ustawianie hello port używany przez obraz Docker</span><span class="sxs-lookup"><span data-stu-id="f427f-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="f427f-130">Korzystając z niestandardowego obrazu Docker dla aplikacji sieci web, można użyć hello `WEBSITES_PORT` zmiennej środowiskowej w Twojej plik Dockerfile pobiera dodać kontener toohello wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="f427f-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="f427f-131">Należy wziąć pod uwagę następujące przykładowy plik docker dopisków fonetycznych aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="f427f-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="f427f-132">Ostatniego wiersza polecenia hello można zauważyć, że tej zmiennej środowiskowej WEBSITES_PORT hello jest przekazywany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f427f-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="f427f-133">Należy pamiętać, że wielkość liter ma znaczenie w poleceniach.</span><span class="sxs-lookup"><span data-stu-id="f427f-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="f427f-134">Poprzednio używał platformy hello `PORT` aplikacji, możemy planowania użycia hello toodeprecate tej aplikacji, ustawienia i Przenieś toousing `WEBSITES_PORT` wyłącznie.</span><span class="sxs-lookup"><span data-stu-id="f427f-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="f427f-135">Korzystając z istniejącego obrazu platformy Docker utworzony przez inną osobę, może być konieczne toospecify portu innego niż port 80 dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f427f-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="f427f-136">tooconfigure hello portu, dodaj aplikację, ustawienie o nazwie `WEBSITES_PORT` z wartością hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="f427f-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Skonfiguruj ustawienia aplikacji portu dla niestandardowego obrazu Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="f427f-138">Porady: ustawić czas uruchamiania hello obrazu Docker</span><span class="sxs-lookup"><span data-stu-id="f427f-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="f427f-139">Domyślnie jeśli nie można uruchomić z kontenera przed 230 sekund platformy hello zostanie uruchomiony ponownie z kontenera.</span><span class="sxs-lookup"><span data-stu-id="f427f-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="f427f-140">Jeśli obraz niestandardowy Docker rozpoczyna się w więcej niż 230 sekund, można użyć hello `WEBSITES_CONTAINER_START_TIME_LIMIT` ustawienie aplikacji hello wartość tego ustawienia w sekundach, pozwoli to zachować platformy hello z kontenera uruchomiona przed ponownym jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="f427f-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="f427f-141">Witaj, wartością domyślną jest 230 sekund i hello maksymalny dozwolony, czy wartość jest 600 sekund.</span><span class="sxs-lookup"><span data-stu-id="f427f-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="f427f-142">Porady: Odinstaluj hello platforma pochodząca magazynu</span><span class="sxs-lookup"><span data-stu-id="f427f-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="f427f-143">Domyślnie platforma hello zainstaluje toohello udziału magazynu trwałego `\home\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="f427f-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="f427f-144">Obraz kontenera trwałego udziału nie jest konieczne, można wyłączyć instalowanie magazynu przez ustawienie hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplikacji ustawienie zbyt`false`.</span><span class="sxs-lookup"><span data-stu-id="f427f-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="f427f-145">Nadal będziesz mieć dostęp do magazynu toothat z hello scm lokacji, a wszystkie dzienniki Docker (jeśli jest włączona) zostanie zapisany toohello plików dziennika generowanych przez hello platformy.</span><span class="sxs-lookup"><span data-stu-id="f427f-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="f427f-146">Porady: Przejdź z powrotem toousing wbudowanych obrazu</span><span class="sxs-lookup"><span data-stu-id="f427f-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="f427f-147">tooswitch z przy użyciu niestandardowego obrazu toousing wbudowanych obrazu:</span><span class="sxs-lookup"><span data-stu-id="f427f-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="f427f-148">W hello [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f427f-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="f427f-149">Wybierz użytkownika **stosu środowiska uruchomieniowego** toouse hello wbudowanych obrazu, następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="f427f-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Konfigurowanie obrazu wbudowanych Docker][5]


## <a name="troubleshooting"></a><span data-ttu-id="f427f-151">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f427f-151">Troubleshooting</span></span> ##

<span data-ttu-id="f427f-152">W przypadku awarii aplikacji toostart z niestandardowego obrazu Docker Sprawdź hello dzienniki w katalogu LogFiles hello Docker.</span><span class="sxs-lookup"><span data-stu-id="f427f-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="f427f-153">Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="f427f-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="f427f-154">toolog hello `stdout` i `stderr` z Twojej kontenera należy tooenable **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="f427f-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Włączanie rejestrowania][8]

![Przy użyciu dzienników Docker tooview Kudu][7]

<span data-ttu-id="f427f-157">Można uzyskać dostępu do hello SCM lokacji z **zaawansowane narzędzia** w hello **narzędzi programistycznych** menu.</span><span class="sxs-lookup"><span data-stu-id="f427f-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f427f-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f427f-158">Next Steps</span></span> ##

<span data-ttu-id="f427f-159">Wykonaj hello następującego łącza tooget wprowadzenie do aplikacji sieci Web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f427f-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="f427f-160">Wprowadzenie tooAzure aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f427f-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="f427f-161">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="f427f-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="f427f-162">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f427f-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="f427f-163">Opublikuj pytania i uwagi na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="f427f-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
