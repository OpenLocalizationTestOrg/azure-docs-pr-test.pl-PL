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
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="80dbe-104">Przy użyciu niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="80dbe-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="80dbe-105">Usługi aplikacji umożliwia stosy wstępnie zdefiniowanych aplikacji w systemie Linux obsługę dla określonej wersji, takich jak PHP w wersji 7.0 i Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="80dbe-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="80dbe-106">Usługa aplikacji w systemie Linux używa kontenerów Docker do obsługi tych stosów wstępnie zbudowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80dbe-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="80dbe-107">Aby wdrożyć aplikację sieci web stosu aplikacji, która nie jest już zdefiniowana w Azure umożliwia także niestandardowego obrazu Docker.</span><span class="sxs-lookup"><span data-stu-id="80dbe-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="80dbe-108">Niestandardowe obrazy usługi Docker może być hostowana na obu publicznych lub prywatnych Docker repozytorium.</span><span class="sxs-lookup"><span data-stu-id="80dbe-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="80dbe-109">Porady: Ustawianie obrazu niestandardowego Docker dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="80dbe-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="80dbe-110">Można ustawić niestandardowego obrazu Docker obie aplikacje nowych i istniejących sieci Web.</span><span class="sxs-lookup"><span data-stu-id="80dbe-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="80dbe-111">Po utworzeniu aplikacji sieci web w systemie Linux w [portalu Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), kliknij przycisk **kontenera konfiguracji** można ustawić niestandardowego obrazu Docker:</span><span class="sxs-lookup"><span data-stu-id="80dbe-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Niestandardowy obraz Docker dla nowej aplikacji sieci web w systemie Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="80dbe-113">Porady: użycie niestandardowego obrazu Docker z Centrum Docker</span><span class="sxs-lookup"><span data-stu-id="80dbe-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="80dbe-114">Aby użyć niestandardowego obrazu Docker z Centrum Docker:</span><span class="sxs-lookup"><span data-stu-id="80dbe-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="80dbe-115">W [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="80dbe-116">Wybierz **Centrum Docker** jako **źródło obrazu**, następnie kliknij opcję **publicznego** lub **prywatnej** i wpisz **obrazu i Nazwa tagu opcjonalne**, takich jak `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="80dbe-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="80dbe-117">**Uruchomienia polecenia** jest zestaw automatycznie na podstawie co to jest zdefiniowana w pliku obrazu Docker, ale możesz ustawić własne polecenia.</span><span class="sxs-lookup"><span data-stu-id="80dbe-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Konfigurowanie Centrum Docker publicznego repozytorium obrazów][2]

    <span data-ttu-id="80dbe-119">W przypadku obrazu z prywatnym repozytorium, należy wprowadzić poświadczenia Centrum Docker jako (**nazwa logowania użytkownika** i **hasło**) do prywatnego repozytorium Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="80dbe-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Konfigurowanie Centrum Docker prywatnym repozytorium obrazów][3]

3. <span data-ttu-id="80dbe-121">Po skonfigurowaniu kontenera, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="80dbe-122">Jak używać obrazu platformy Docker z rejestru prywatnej obrazu</span><span class="sxs-lookup"><span data-stu-id="80dbe-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="80dbe-123">Aby użyć niestandardowego obrazu Docker z rejestru prywatnej obrazu:</span><span class="sxs-lookup"><span data-stu-id="80dbe-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="80dbe-124">W [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **kontenera Docker**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="80dbe-125">Kliknij przycisk **prywatnej rejestru** jako **źródło obrazu**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="80dbe-126">Wprowadź **obrazu i nazwę tagu opcjonalne**, **adres URL serwera** dla prywatnych rejestru, oraz poświadczenia (**nazwa logowania użytkownika** i **hasło**).</span><span class="sxs-lookup"><span data-stu-id="80dbe-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="80dbe-127">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-127">Click **Save**.</span></span>

    ![Konfigurowanie obrazu Docker z rejestru prywatnych][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="80dbe-129">Porady: Ustawianie portu używanego przez obraz Docker</span><span class="sxs-lookup"><span data-stu-id="80dbe-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="80dbe-130">Jeśli używasz niestandardowego obrazu Docker dla aplikacji sieci web, możesz użyć `WEBSITES_PORT` zmiennej środowiskowej w Twojej plik Dockerfile pobiera dodać do kontenera wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="80dbe-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="80dbe-131">Rozważmy poniższy przykład przedstawia plik docker dla dopisków fonetycznych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="80dbe-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="80dbe-132">Na ostatnim wierszu polecenia można zobaczyć, że zmienna środowiskowa WEBSITES_PORT jest przekazywany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="80dbe-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="80dbe-133">Należy pamiętać, że wielkość liter ma znaczenie w poleceniach.</span><span class="sxs-lookup"><span data-stu-id="80dbe-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="80dbe-134">Poprzednio używał platformy `PORT` aplikacji ustawienie, firma Microsoft planuje zastąpić użycie tej aplikacji, ustawienia i przenieść przy użyciu `WEBSITES_PORT` wyłącznie.</span><span class="sxs-lookup"><span data-stu-id="80dbe-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="80dbe-135">Korzystając z istniejącego obrazu platformy Docker utworzony przez inną osobę, konieczne może być Określ port inny niż port 80 dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80dbe-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="80dbe-136">Aby skonfigurować port, dodaj aplikację, ustawienie o nazwie `WEBSITES_PORT` z wartością, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="80dbe-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![Skonfiguruj ustawienia aplikacji portu dla niestandardowego obrazu Docker][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="80dbe-138">Porady: Ustawianie czasu uruchamiania obrazu Docker</span><span class="sxs-lookup"><span data-stu-id="80dbe-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="80dbe-139">Domyślnie jeśli nie można uruchomić z kontenera przed 230 sekund platformy zostanie uruchomiony ponownie z kontenera.</span><span class="sxs-lookup"><span data-stu-id="80dbe-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="80dbe-140">Jeśli obraz niestandardowy Docker rozpoczyna się w więcej niż 230 sekund, możesz użyć `WEBSITES_CONTAINER_START_TIME_LIMIT` aplikacji ustawienie, wartość tego ustawienia w sekundach, pozwoli to zachować platformy z kontenera uruchomiona przed ponownym jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="80dbe-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="80dbe-141">Wartość domyślna to 230 sekund, a maksymalna dopuszczalna wartość wynosi 600 sekund.</span><span class="sxs-lookup"><span data-stu-id="80dbe-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="80dbe-142">Porady: Odinstaluj magazynu platforma pochodząca</span><span class="sxs-lookup"><span data-stu-id="80dbe-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="80dbe-143">Domyślnie platforma będzie zainstalować udział magazynu trwałego na `\home\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="80dbe-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="80dbe-144">Obraz kontenera trwałego udziału nie jest konieczne, można wyłączyć instalowanie magazynu przez ustawienie `WEBSITES_ENABLE_APP_SERVICE_STORAGE` ustawienia aplikacji na `false`.</span><span class="sxs-lookup"><span data-stu-id="80dbe-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="80dbe-145">Masz nadal dostęp do tego magazynu z lokacji scm, a wszystkie dzienniki Docker (jeśli jest włączona) będą zapisywane pliki dziennika wygenerowane przez platformę.</span><span class="sxs-lookup"><span data-stu-id="80dbe-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="80dbe-146">Porady: wrócić do przy użyciu wbudowanych obrazu</span><span class="sxs-lookup"><span data-stu-id="80dbe-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="80dbe-147">Aby przełączyć się z przy użyciu niestandardowego obrazu przy użyciu wbudowanych obrazu:</span><span class="sxs-lookup"><span data-stu-id="80dbe-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="80dbe-148">W [portalu Azure](https://portal.azure.com), następnie zlokalizować aplikacji sieci web w systemie Linux w **ustawienia** kliknij **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="80dbe-149">Wybierz użytkownika **stosu środowiska uruchomieniowego** do użycia wbudowanych obrazu, następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Konfigurowanie obrazu wbudowanych Docker][5]


## <a name="troubleshooting"></a><span data-ttu-id="80dbe-151">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="80dbe-151">Troubleshooting</span></span> ##

<span data-ttu-id="80dbe-152">Gdy aplikacja nie można uruchomić z niestandardowego obrazu Docker, sprawdź dzienniki Docker w katalogu LogFiles.</span><span class="sxs-lookup"><span data-stu-id="80dbe-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="80dbe-153">Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="80dbe-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="80dbe-154">W dzienniku `stdout` i `stderr` z Twojej kontenera, musisz włączyć **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="80dbe-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Włączanie rejestrowania][8]

![Aby wyświetlić dzienniki Docker przy użyciu Kudu][7]

<span data-ttu-id="80dbe-157">Można uzyskać dostępu do lokacji SCM z **zaawansowane narzędzia** w **narzędzi programistycznych** menu.</span><span class="sxs-lookup"><span data-stu-id="80dbe-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80dbe-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80dbe-158">Next Steps</span></span> ##

<span data-ttu-id="80dbe-159">Wykonaj poniższe łącza, aby rozpocząć korzystanie z aplikacji sieci Web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="80dbe-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="80dbe-160">Wprowadzenie do aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="80dbe-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="80dbe-161">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="80dbe-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="80dbe-162">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="80dbe-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="80dbe-163">Opublikuj pytania i uwagi na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="80dbe-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
