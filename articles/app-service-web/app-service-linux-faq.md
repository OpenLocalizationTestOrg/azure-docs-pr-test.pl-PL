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
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="454c4-104">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="454c4-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="454c4-105">Wraz z wydaniem aplikacji sieci Web w systemie Linux pracujemy nad Dodawanie funkcji i wprowadzać ulepszenia platformy.</span><span class="sxs-lookup"><span data-stu-id="454c4-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="454c4-106">Poniżej przedstawiono niektóre często zadawane pytania (FAQ), które naszym klientom ma zostały prośbą z ostatnich miesięcy.</span><span class="sxs-lookup"><span data-stu-id="454c4-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="454c4-107">Jeśli masz pytania, komentarza, w artykule i firma Microsoft będzie odpowiedź tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="454c4-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="454c4-108">Wbudowane obrazów</span><span class="sxs-lookup"><span data-stu-id="454c4-108">Built-in images</span></span>

<span data-ttu-id="454c4-109">**Pytanie:** chcę rozwidlania wbudowanych kontenerów Docker, które zapewnia platformę.</span><span class="sxs-lookup"><span data-stu-id="454c4-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="454c4-110">Gdzie można znaleźć te pliki?</span><span class="sxs-lookup"><span data-stu-id="454c4-110">Where can I find those files?</span></span>

<span data-ttu-id="454c4-111">**Odpowiedź:** wszystkie pliki Docker można znaleźć w [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="454c4-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="454c4-112">Możesz znaleźć wszystkie kontenery Docker na [Centrum Docker](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="454c4-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="454c4-113">**Pytanie:** co to są oczekiwanych wartości dla pliku uruchomienia sekcji podczas konfigurowania środowiska uruchomieniowego stosu?</span><span class="sxs-lookup"><span data-stu-id="454c4-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="454c4-114">**Odpowiedź:** dla środowiska Node.Js, określ plik konfiguracyjny PM2 lub plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="454c4-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="454c4-115">Określ nazwę skompilowanej biblioteki DLL dla platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="454c4-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="454c4-116">Dla środowiska Ruby można określić skrypt dopisków fonetycznych, który chcesz zainicjować aplikacji za pomocą.</span><span class="sxs-lookup"><span data-stu-id="454c4-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="454c4-117">Zarządzanie</span><span class="sxs-lookup"><span data-stu-id="454c4-117">Management</span></span>

<span data-ttu-id="454c4-118">**Pytanie:** co się stanie po naciśnięciu przycisku ponownego uruchomienia w portalu Azure?</span><span class="sxs-lookup"><span data-stu-id="454c4-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="454c4-119">**Odpowiedź:** to odpowiednik Docker ponownego uruchomienia komputera.</span><span class="sxs-lookup"><span data-stu-id="454c4-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="454c4-120">**Pytanie:** czy za pomocą protokołu Secure Shell (SSH) można nawiązać połączenia z aplikacji kontenera maszyny wirtualnej (VM)?</span><span class="sxs-lookup"><span data-stu-id="454c4-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="454c4-121">**Odpowiedź:** tak, możesz to zrobić za pośrednictwem witryny SCM, sprawdź następujący artykuł, aby uzyskać więcej informacji [Obsługa protokołu SSH dla aplikacji sieci Web w systemie Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="454c4-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="454c4-122">**Pytanie:** Utwórz płaszczyźnie Linux App Service przy użyciu zestawu SDK lub szablon ARM, jak można to osiągnąć?</span><span class="sxs-lookup"><span data-stu-id="454c4-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="454c4-123">**Odpowiedź:** należy ustawić `reserved` pole app service w celu `true`.</span><span class="sxs-lookup"><span data-stu-id="454c4-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="454c4-124">Ciągła integracja/wdrożenia</span><span class="sxs-lookup"><span data-stu-id="454c4-124">Continuous integration/deployment</span></span>

<span data-ttu-id="454c4-125">**Pytanie:** Moja aplikacja sieci web nadal używa stary obraz kontenera Docker po po aktualizacji obraz Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="454c4-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="454c4-126">Czy ciągłej integracji/wdrożenia kontenerów niestandardowe są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="454c4-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="454c4-127">**A:** do skonfigurowania integracji ciągłej/wdrożenia do rejestru kontenera platformy Azure lub DockerHub obrazy sprawdzając artykule [ciągłego wdrażania z aplikacji sieci Web platformy Azure w systemie Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="454c4-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="454c4-128">Dla prywatnych rejestrów można odświeżyć kontenera przez zatrzymanie i uruchomienie następnie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="454c4-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="454c4-129">Lub możesz zmienić lub Dodaj ustawienie aplikacji fikcyjny, aby wymusić odświeżenie z kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="454c4-130">**Pytanie:** czy środowisk przemieszczania są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="454c4-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="454c4-131">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="454c4-131">**A:** Yes.</span></span>

<span data-ttu-id="454c4-132">**Pytanie:** można użyć **narzędzia web deploy** wdrażania Moja aplikacja sieci web?</span><span class="sxs-lookup"><span data-stu-id="454c4-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="454c4-133">**Odpowiedź:** tak, należy określić aplikację nosi nazwę `WEBSITE_WEBDEPLOY_USE_SCM` do `false`.</span><span class="sxs-lookup"><span data-stu-id="454c4-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="454c4-134">Obsługa języków</span><span class="sxs-lookup"><span data-stu-id="454c4-134">Language support</span></span>

<span data-ttu-id="454c4-135">**Pytanie:** czy nie skompilowanego aplikacji .NET Core są obsługiwane?</span><span class="sxs-lookup"><span data-stu-id="454c4-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="454c4-136">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="454c4-136">**A:** Yes.</span></span>

<span data-ttu-id="454c4-137">**Pytanie:** są obsługiwane Composer Menedżer zależności dla aplikacji PHP?</span><span class="sxs-lookup"><span data-stu-id="454c4-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="454c4-138">**Odpowiedź:** tak.</span><span class="sxs-lookup"><span data-stu-id="454c4-138">**A:** Yes.</span></span> <span data-ttu-id="454c4-139">Podczas wdrażania narzędzia Git Kudu powinna wykryć wdrażania aplikacji PHP (dzięki użyciu obecność pliku composer.json), a następnie wyzwala instalacji composer dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="454c4-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="454c4-140">Kontenery niestandardowych</span><span class="sxs-lookup"><span data-stu-id="454c4-140">Custom containers</span></span>

<span data-ttu-id="454c4-141">**Pytanie:** używam własne niestandardowe kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="454c4-142">Moja aplikacja znajduje się w `\home\` katalogu, ale nie można odnaleźć plików, podczas I przeglądać zawartość przy użyciu [lokacji SCM](https://github.com/projectkudu/kudu) lub klient FTP.</span><span class="sxs-lookup"><span data-stu-id="454c4-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="454c4-143">Gdzie są pliki?</span><span class="sxs-lookup"><span data-stu-id="454c4-143">Where are my files?</span></span>

<span data-ttu-id="454c4-144">**Odpowiedź:** możemy instalowanie udziału SMB do `\home\` katalogu.</span><span class="sxs-lookup"><span data-stu-id="454c4-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="454c4-145">Spowoduje to zastąpienie zawartość, która jest.</span><span class="sxs-lookup"><span data-stu-id="454c4-145">This will override any content that's there.</span></span>

<span data-ttu-id="454c4-146">**Pytanie:** używam własne niestandardowe kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="454c4-147">Nie chcę platformy w celu zainstalowania udziału SMB do `\home\`.</span><span class="sxs-lookup"><span data-stu-id="454c4-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="454c4-148">**Odpowiedź:** możesz to zrobić przez ustawienie `WEBSITES_ENABLE_APP_SERVICE_STORAGE` ustawienia aplikacji na `false`.</span><span class="sxs-lookup"><span data-stu-id="454c4-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="454c4-149">**Pytanie:** Moje niestandardowe kontenera zajmuje dużo czasu do uruchomienia i platforma Uruchom kontenera przed zakończeniem uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="454c4-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="454c4-150">**Odpowiedź:** możesz skonfigurować czas platformy będzie czekać przed ponownym uruchomieniem z kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="454c4-151">Można to zrobić przez ustawienie `WEBSITES_CONTAINER_START_TIME_LIMIT` ustawienia aplikacji na żądaną wartość w sekundach.</span><span class="sxs-lookup"><span data-stu-id="454c4-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="454c4-152">Wartość domyślna to 230 sekund, a maksymalna to 600 sekund.</span><span class="sxs-lookup"><span data-stu-id="454c4-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="454c4-153">**Pytanie:** co to jest format adresu url serwera prywatnej rejestru?</span><span class="sxs-lookup"><span data-stu-id="454c4-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="454c4-154">**Odpowiedź:** musisz podać z rejestru pełnego adresu url, w tym `http://` lub `https://`.</span><span class="sxs-lookup"><span data-stu-id="454c4-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="454c4-155">**Pytanie:** co to jest format nazwy obrazu w opcji prywatnych rejestru?</span><span class="sxs-lookup"><span data-stu-id="454c4-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="454c4-156">**Odpowiedź:** należy dodać nazwę pełnego obrazu tym rejestru prywatnego adresu url (np.</span><span class="sxs-lookup"><span data-stu-id="454c4-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="454c4-157">myacr.azurecr.IO/DotNet:Latest)</span><span class="sxs-lookup"><span data-stu-id="454c4-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="454c4-158">**Pytanie:** warto udostępnić więcej niż jeden port na obraz niestandardowy kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="454c4-159">Jest to możliwe?</span><span class="sxs-lookup"><span data-stu-id="454c4-159">Is that possible?</span></span>

<span data-ttu-id="454c4-160">**Odpowiedź:** obecnie, która nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="454c4-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="454c4-161">**Pytanie:** własnych magazynu można przełączyć?</span><span class="sxs-lookup"><span data-stu-id="454c4-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="454c4-162">**Odpowiedź:** która obecnie nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="454c4-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="454c4-163">**Pytanie:** I nie może przejrzeć Moje niestandardowe kontenera procesy systemu lub z systemem plików z lokacji, Menedżer sterowania usługami.</span><span class="sxs-lookup"><span data-stu-id="454c4-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="454c4-164">Dlaczego jest to, że?</span><span class="sxs-lookup"><span data-stu-id="454c4-164">Why is that?</span></span>

<span data-ttu-id="454c4-165">**Odpowiedź:** SCM witryna jest uruchamiana w oddzielnym kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="454c4-166">Nie można sprawdzić procesy systemu lub z systemem plików kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454c4-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="454c4-167">**Pytanie:** Moje niestandardowe kontenera nasłuchuje portu innego niż port 80.</span><span class="sxs-lookup"><span data-stu-id="454c4-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="454c4-168">Jak można skonfigurować mojej aplikacji można przekierować żądania do tego portu</span><span class="sxs-lookup"><span data-stu-id="454c4-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="454c4-169">**A:** mamy automatyczne wykrywanie portu, można również określić aplikacja nosi nazwę **WEBSITES_PORT**i nadaj mu wartość numeru portu oczekiwanego.</span><span class="sxs-lookup"><span data-stu-id="454c4-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="454c4-170">Poprzednio używał platformy `PORT` aplikacji ustawienie, firma Microsoft planuje zastąpić użycie tej aplikacji, ustawienia i przenieść przy użyciu `WEBSITES_PORT` wyłącznie.</span><span class="sxs-lookup"><span data-stu-id="454c4-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="454c4-171">**Pytanie:** należy zaimplementować HTTPS w mojej niestandardowych kontenera.</span><span class="sxs-lookup"><span data-stu-id="454c4-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="454c4-172">**Odpowiedź:** nie, platforma obsługuje zakończenia połączenia HTTPS w frontends udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="454c4-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="454c4-173">Cennik i umowy SLA</span><span class="sxs-lookup"><span data-stu-id="454c4-173">Pricing and SLA</span></span>

<span data-ttu-id="454c4-174">**Pytanie:** co to jest cennik podczas korzystania z publicznej wersji zapoznawczej?</span><span class="sxs-lookup"><span data-stu-id="454c4-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="454c4-175">**Odpowiedź:** połowie liczby godzin, w których aplikacja będzie działać, z normalnym cennik usługi aplikacji Azure są naliczane.</span><span class="sxs-lookup"><span data-stu-id="454c4-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="454c4-176">Oznacza to, że możesz uzyskać rabat 50 procent normalne cennik usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="454c4-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="454c4-177">Inne</span><span class="sxs-lookup"><span data-stu-id="454c4-177">Other</span></span>

<span data-ttu-id="454c4-178">**Pytanie:** co to są obsługiwane znaki w nazwach ustawienia aplikacji?</span><span class="sxs-lookup"><span data-stu-id="454c4-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="454c4-179">**Odpowiedź:** A-Z, a-z, 0-9 i znak podkreślenia można używać tylko dla ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454c4-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="454c4-180">**Pytanie:** których mogą żądać nowych funkcji?</span><span class="sxs-lookup"><span data-stu-id="454c4-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="454c4-181">**Odpowiedź:** mogą przesyłać Twój pomysł na [forum opinii aplikacje sieci Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="454c4-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="454c4-182">Do tytułu Twój pomysł, należy dodać "[Linux]".</span><span class="sxs-lookup"><span data-stu-id="454c4-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="454c4-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="454c4-183">Next steps</span></span>
* [<span data-ttu-id="454c4-184">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="454c4-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="454c4-185">Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="454c4-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="454c4-186">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="454c4-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="454c4-187">Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="454c4-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
