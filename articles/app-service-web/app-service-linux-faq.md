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
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="320c1-104">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="320c1-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="320c1-105">Witaj wersji z aplikacji sieci Web w systemie Linux pracujemy nad Dodawanie funkcji oraz wprowadzania ulepszenia tooour platformy.</span><span class="sxs-lookup"><span data-stu-id="320c1-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="320c1-106">W tym miejscu przedstawiono często zadawane pytania (FAQ), które naszym klientom ma zostały prośbą za pośrednictwem hello ostatnio miesięcy.</span><span class="sxs-lookup"><span data-stu-id="320c1-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="320c1-107">Jeśli masz pytania, komentarza, w artykule hello i firma Microsoft będzie odpowiedź tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="320c1-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="320c1-108">Wbudowane obrazów</span><span class="sxs-lookup"><span data-stu-id="320c1-108">Built-in images</span></span>

<span data-ttu-id="320c1-109">**Pytanie:** ma zapewnia toofork hello wbudowanych Docker kontenerów, które hello platformy.</span><span class="sxs-lookup"><span data-stu-id="320c1-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="320c1-110">Gdzie można znaleźć te pliki?</span><span class="sxs-lookup"><span data-stu-id="320c1-110">Where can I find those files?</span></span>

<span data-ttu-id="320c1-111">**Odpowiedź:** wszystkie pliki Docker można znaleźć w [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="320c1-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="320c1-112">Możesz znaleźć wszystkie kontenery Docker na [Centrum Docker](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="320c1-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="320c1-113">**Pytanie:** co to są hello oczekiwanych wartości dla hello sekcji uruchamiania pliku podczas konfigurowania stosu środowiska uruchomieniowego hello?</span><span class="sxs-lookup"><span data-stu-id="320c1-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="320c1-114">**Odpowiedź:** dla środowiska Node.Js, określ plik konfiguracyjny hello PM2 lub plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="320c1-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="320c1-115">Określ nazwę skompilowanej biblioteki DLL dla platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="320c1-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="320c1-116">Dla środowiska Ruby, można określić hello skryptu dopisków fonetycznych, które mają tooinitialize aplikacji za pomocą.</span><span class="sxs-lookup"><span data-stu-id="320c1-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="320c1-117">Zarządzanie</span><span class="sxs-lookup"><span data-stu-id="320c1-117">Management</span></span>

<span data-ttu-id="320c1-118">**Pytanie:** co się stanie po naciśnięciu przycisku ponownego uruchomienia hello w portalu Azure hello?</span><span class="sxs-lookup"><span data-stu-id="320c1-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="320c1-119">**Odpowiedź:** hello jest to równoważne Docker ponownego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="320c1-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="320c1-120">**Pytanie:** można użyć aplikacji toohello tooconnect Secure Shell (SSH) kontenera maszyny wirtualnej (VM)?</span><span class="sxs-lookup"><span data-stu-id="320c1-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="320c1-121">**Odpowiedź:** tak, czy za pośrednictwem witryny SCM hello, sprawdź następujące hello artykuł Aby uzyskać więcej informacji [Obsługa protokołu SSH dla aplikacji sieci Web w systemie Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="320c1-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="320c1-122">**Pytanie:** ma toocreate płaszczyźnie Linux App Service przy użyciu zestawu SDK lub szablon ARM, jak można to osiągnąć?</span><span class="sxs-lookup"><span data-stu-id="320c1-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="320c1-123">**A:** należy tooset hello `reserved` pola aplikacji hello usługi zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="320c1-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="320c1-124">Ciągła integracja/wdrożenia</span><span class="sxs-lookup"><span data-stu-id="320c1-124">Continuous integration/deployment</span></span>

<span data-ttu-id="320c1-125">**Pytanie:** Moja aplikacja sieci web nadal używa stary obraz kontenera Docker po po aktualizacji obraz powitania w Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="320c1-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="320c1-126">Czy ciągłej integracji/wdrożenia kontenerów niestandardowe są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="320c1-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="320c1-127">**Odpowiedź:** tooset ciągłej integracji/wdrożenia obrazów rejestru kontenera platformy Azure lub DockerHub przez hello wyboru poniższego artykułu [ciągłego wdrażania z aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="320c1-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="320c1-128">Dla prywatnych rejestrów można odświeżyć hello kontenera przez zatrzymanie i uruchomienie następnie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="320c1-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="320c1-129">Lub możesz zmienić lub dodać aplikację fikcyjny ustawienie tooforce odświeżania z kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="320c1-130">**Pytanie:** czy środowisk przemieszczania są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="320c1-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="320c1-131">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="320c1-131">**A:** Yes.</span></span>

<span data-ttu-id="320c1-132">**Pytanie:** można użyć **narzędzia web deploy** toodeploy Moja aplikacja sieci web?</span><span class="sxs-lookup"><span data-stu-id="320c1-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="320c1-133">**Odpowiedź:** tak, potrzebujesz tooset aplikacji nosi nazwę `WEBSITE_WEBDEPLOY_USE_SCM` zbyt`false`.</span><span class="sxs-lookup"><span data-stu-id="320c1-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="320c1-134">Obsługa języków</span><span class="sxs-lookup"><span data-stu-id="320c1-134">Language support</span></span>

<span data-ttu-id="320c1-135">**Pytanie:** czy nie skompilowanego aplikacji .NET Core są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="320c1-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="320c1-136">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="320c1-136">**A:** Yes.</span></span>

<span data-ttu-id="320c1-137">**Pytanie:** są obsługiwane Composer Menedżer zależności dla aplikacji PHP?</span><span class="sxs-lookup"><span data-stu-id="320c1-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="320c1-138">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="320c1-138">**A:** Yes.</span></span> <span data-ttu-id="320c1-139">Podczas wdrażania narzędzia Git Kudu powinna wykryć wdrażania aplikacji PHP (Dziękujemy toohello obecność pliku composer.json), a następnie wyzwala instalacji composer dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="320c1-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="320c1-140">Kontenery niestandardowych</span><span class="sxs-lookup"><span data-stu-id="320c1-140">Custom containers</span></span>

<span data-ttu-id="320c1-141">**Pytanie:** używam własne niestandardowe kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="320c1-142">Moja aplikacja znajduje się w hello `\home\` katalogu, ale nie można odnaleźć plików I przeglądających hello zawartości przy użyciu hello [lokacji SCM](https://github.com/projectkudu/kudu) lub klient FTP.</span><span class="sxs-lookup"><span data-stu-id="320c1-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="320c1-143">Gdzie są pliki?</span><span class="sxs-lookup"><span data-stu-id="320c1-143">Where are my files?</span></span>

<span data-ttu-id="320c1-144">**Odpowiedź:** możemy zainstalować toohello udziału SMB `\home\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="320c1-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="320c1-145">Spowoduje to zastąpienie zawartość, która jest.</span><span class="sxs-lookup"><span data-stu-id="320c1-145">This will override any content that's there.</span></span>

<span data-ttu-id="320c1-146">**Pytanie:** używam własne niestandardowe kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="320c1-147">Nie chcę hello platformy toomount toohello udziału SMB `\home\`.</span><span class="sxs-lookup"><span data-stu-id="320c1-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="320c1-148">**Odpowiedź:** możesz to zrobić przez ustawienie hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplikacji ustawienie zbyt`false`.</span><span class="sxs-lookup"><span data-stu-id="320c1-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="320c1-149">**Pytanie:** Moje niestandardowe kontenera przyjmuje toostart dużo czasu i hello platformy ponownego uruchomienia hello kontenera przed zakończeniem uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="320c1-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="320c1-150">**Odpowiedź:** możesz skonfigurować czas hello platformy hello czeka przed ponownym uruchomieniem z kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="320c1-151">Można to zrobić przez ustawienie hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello ustawienie aplikacji Żądana wartość w sekundach.</span><span class="sxs-lookup"><span data-stu-id="320c1-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="320c1-152">domyślną Hello jest 230 sekund, a maksymalna hello jest 600 sekund.</span><span class="sxs-lookup"><span data-stu-id="320c1-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="320c1-153">**Pytanie:** co to jest hello format adresu url serwera prywatnej rejestru?</span><span class="sxs-lookup"><span data-stu-id="320c1-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="320c1-154">**Odpowiedź:** należy tooprovide hello rejestru pełnego adresu url w tym `http://` lub `https://`.</span><span class="sxs-lookup"><span data-stu-id="320c1-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="320c1-155">**Pytanie:** co to jest hello format nazw obraz powitania w opcji prywatnych rejestru?</span><span class="sxs-lookup"><span data-stu-id="320c1-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="320c1-156">**Odpowiedź:** potrzebna nazwa pełny obraz powitania tooadd tym hello prywatnej rejestru url (np.</span><span class="sxs-lookup"><span data-stu-id="320c1-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="320c1-157">myacr.azurecr.IO/DotNet:Latest)</span><span class="sxs-lookup"><span data-stu-id="320c1-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="320c1-158">**Pytanie:** ma więcej niż jeden port tooexpose na obraz niestandardowy kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="320c1-159">Jest to możliwe?</span><span class="sxs-lookup"><span data-stu-id="320c1-159">Is that possible?</span></span>

<span data-ttu-id="320c1-160">**Odpowiedź:** obecnie, która nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="320c1-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="320c1-161">**Pytanie:** własnych magazynu można przełączyć?</span><span class="sxs-lookup"><span data-stu-id="320c1-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="320c1-162">**Odpowiedź:** która obecnie nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="320c1-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="320c1-163">**Pytanie:** I nie może przejrzeć Moje niestandardowe kontenera procesy systemu lub z systemem plików z witryny SCM hello.</span><span class="sxs-lookup"><span data-stu-id="320c1-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="320c1-164">Dlaczego jest to, że?</span><span class="sxs-lookup"><span data-stu-id="320c1-164">Why is that?</span></span>

<span data-ttu-id="320c1-165">**Odpowiedź:** hello SCM witryna jest uruchamiana w oddzielnym kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="320c1-166">Nie można sprawdzić system plików hello lub uruchomionych procesów hello kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="320c1-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="320c1-167">**Pytanie:** Moje niestandardowe kontenera nasłuchuje tooa portu innego niż port 80.</span><span class="sxs-lookup"><span data-stu-id="320c1-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="320c1-168">Jak można skonfigurować port tooroute toothat żądań hello mojej aplikacji?</span><span class="sxs-lookup"><span data-stu-id="320c1-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="320c1-169">**Odpowiedź:** mamy automatyczne wykrywanie portu, można również określić aplikacja nosi nazwę **WEBSITES_PORT**i nadaj mu wartość hello hello oczekiwany numer portu.</span><span class="sxs-lookup"><span data-stu-id="320c1-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="320c1-170">Poprzednio używał platformy hello `PORT` aplikacji, możemy planowania użycia hello toodeprecate tej aplikacji, ustawienia i Przenieś toousing `WEBSITES_PORT` wyłącznie.</span><span class="sxs-lookup"><span data-stu-id="320c1-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="320c1-171">**Pytanie:** należy tooimplement HTTPS w mojej niestandardowych kontenera.</span><span class="sxs-lookup"><span data-stu-id="320c1-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="320c1-172">**Odpowiedź:** nie, hello platformy obsługuje zakończenia połączenia HTTPS w frontends hello udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="320c1-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="320c1-173">Cennik i umowy SLA</span><span class="sxs-lookup"><span data-stu-id="320c1-173">Pricing and SLA</span></span>

<span data-ttu-id="320c1-174">**Pytanie:** co to jest hello cennik podczas korzystania z publicznej wersji zapoznawczej hello?</span><span class="sxs-lookup"><span data-stu-id="320c1-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="320c1-175">**Odpowiedź:** połowa hello liczbę godzin, w których aplikacja będzie działać, z normalnym cennik usługi aplikacji Azure hello są naliczane.</span><span class="sxs-lookup"><span data-stu-id="320c1-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="320c1-176">Oznacza to, że możesz uzyskać rabat 50 procent normalne cennik usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="320c1-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="320c1-177">Inne</span><span class="sxs-lookup"><span data-stu-id="320c1-177">Other</span></span>

<span data-ttu-id="320c1-178">**Pytanie:** co to są hello obsługiwane znaki w nazwach ustawienia aplikacji?</span><span class="sxs-lookup"><span data-stu-id="320c1-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="320c1-179">**Odpowiedź:** można tylko użyć A-Z, a-z, 0-9 i hello podkreślenia dla ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="320c1-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="320c1-180">**Pytanie:** których mogą żądać nowych funkcji?</span><span class="sxs-lookup"><span data-stu-id="320c1-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="320c1-181">**A:** można przesłać Twój pomysł na powitania [forum opinii aplikacje sieci Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="320c1-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="320c1-182">Dodaj tytuł toohello "[Linux]" Twój pomysł.</span><span class="sxs-lookup"><span data-stu-id="320c1-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="320c1-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="320c1-183">Next steps</span></span>
* [<span data-ttu-id="320c1-184">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="320c1-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="320c1-185">Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="320c1-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="320c1-186">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="320c1-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="320c1-187">Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="320c1-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
