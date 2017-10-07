---
title: tooAzure aaaIntroduction aplikacji sieci Web w systemie Linux | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="4f0ed-104">Wprowadzenie tooAzure aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f0ed-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="4f0ed-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4f0ed-105">Overview</span></span>
<span data-ttu-id="4f0ed-106">Klienci mogą użyć aplikacji sieci Web aplikacji sieci web toohost Linux natywnie w systemie Linux dla stosy obsługiwanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="4f0ed-107">Witaj poniższej sekcji przedstawiono stosy aplikacji hello, które są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="4f0ed-108">Funkcje</span><span class="sxs-lookup"><span data-stu-id="4f0ed-108">Features</span></span>
<span data-ttu-id="4f0ed-109">Aplikacji w systemie Linux sieci Web obsługuje obecnie następujące stosy aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="4f0ed-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="4f0ed-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="4f0ed-110">Node.js</span></span>
    * <span data-ttu-id="4f0ed-111">4.4</span><span class="sxs-lookup"><span data-stu-id="4f0ed-111">4.4</span></span>
    * <span data-ttu-id="4f0ed-112">4.5</span><span class="sxs-lookup"><span data-stu-id="4f0ed-112">4.5</span></span>
    * <span data-ttu-id="4f0ed-113">6.2</span><span class="sxs-lookup"><span data-stu-id="4f0ed-113">6.2</span></span>
    * <span data-ttu-id="4f0ed-114">6.6</span><span class="sxs-lookup"><span data-stu-id="4f0ed-114">6.6</span></span>
    * <span data-ttu-id="4f0ed-115">6.9</span><span class="sxs-lookup"><span data-stu-id="4f0ed-115">6.9</span></span>
    * <span data-ttu-id="4f0ed-116">6.10</span><span class="sxs-lookup"><span data-stu-id="4f0ed-116">6.10</span></span>
    * <span data-ttu-id="4f0ed-117">6.11</span><span class="sxs-lookup"><span data-stu-id="4f0ed-117">6.11</span></span>
    * <span data-ttu-id="4f0ed-118">8.0</span><span class="sxs-lookup"><span data-stu-id="4f0ed-118">8.0</span></span>
    * <span data-ttu-id="4f0ed-119">8.1</span><span class="sxs-lookup"><span data-stu-id="4f0ed-119">8.1</span></span>
* <span data-ttu-id="4f0ed-120">PHP</span><span class="sxs-lookup"><span data-stu-id="4f0ed-120">PHP</span></span>
    * <span data-ttu-id="4f0ed-121">5.6</span><span class="sxs-lookup"><span data-stu-id="4f0ed-121">5.6</span></span>
    * <span data-ttu-id="4f0ed-122">7.0</span><span class="sxs-lookup"><span data-stu-id="4f0ed-122">7.0</span></span>
* <span data-ttu-id="4f0ed-123">Oprogramowanie .NET core</span><span class="sxs-lookup"><span data-stu-id="4f0ed-123">.Net Core</span></span>
    * <span data-ttu-id="4f0ed-124">1.0</span><span class="sxs-lookup"><span data-stu-id="4f0ed-124">1.0</span></span>
    * <span data-ttu-id="4f0ed-125">1.1</span><span class="sxs-lookup"><span data-stu-id="4f0ed-125">1.1</span></span>
* <span data-ttu-id="4f0ed-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="4f0ed-126">Ruby</span></span>
    * <span data-ttu-id="4f0ed-127">2.3</span><span class="sxs-lookup"><span data-stu-id="4f0ed-127">2.3</span></span>

<span data-ttu-id="4f0ed-128">Klienci mogą wdrożyć swoich aplikacji przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="4f0ed-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="4f0ed-129">FTP</span><span class="sxs-lookup"><span data-stu-id="4f0ed-129">FTP</span></span>
* <span data-ttu-id="4f0ed-130">Lokalne Git</span><span class="sxs-lookup"><span data-stu-id="4f0ed-130">Local Git</span></span>
* <span data-ttu-id="4f0ed-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="4f0ed-131">GitHub</span></span>
* <span data-ttu-id="4f0ed-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="4f0ed-132">Bitbucket</span></span>

<span data-ttu-id="4f0ed-133">Do skalowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4f0ed-133">For application scaling:</span></span>

* <span data-ttu-id="4f0ed-134">Klientów można skalować aplikacji sieci web górę i w dół, zmieniając warstwę hello ich planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="4f0ed-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="4f0ed-135">Klienci mogą skalowanie aplikacji i uruchamiać wiele wystąpień aplikacji w obrębie hello ich jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="4f0ed-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="4f0ed-136">Dla Kudu, niektóre podstawowe funkcje hello:</span><span class="sxs-lookup"><span data-stu-id="4f0ed-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="4f0ed-137">Środowisk</span><span class="sxs-lookup"><span data-stu-id="4f0ed-137">Environments</span></span>
* <span data-ttu-id="4f0ed-138">Wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-138">Deployments</span></span>
* <span data-ttu-id="4f0ed-139">Podstawowe konsoli</span><span class="sxs-lookup"><span data-stu-id="4f0ed-139">Basic console</span></span>
* <span data-ttu-id="4f0ed-140">SSH</span><span class="sxs-lookup"><span data-stu-id="4f0ed-140">SSH</span></span>

<span data-ttu-id="4f0ed-141">Dla opracowywania oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="4f0ed-141">For devops:</span></span>

* <span data-ttu-id="4f0ed-142">Środowiska przejściowe</span><span class="sxs-lookup"><span data-stu-id="4f0ed-142">Staging environments</span></span>
* <span data-ttu-id="4f0ed-143">ACR i DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="4f0ed-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="4f0ed-144">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-144">Limitations</span></span>
<span data-ttu-id="4f0ed-145">Witaj portalu Azure zawiera tylko funkcje, które obecnie działają dla aplikacji sieci Web w systemie Linux i ukrywa hello rest.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="4f0ed-146">Jak możemy włączyć funkcje dodatkowe, będą one widoczne w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="4f0ed-147">Niektóre funkcje, takie jak integracji sieci wirtualnej, Azure Active Directory/uwierzytelniania innej firmy lub Kudu rozszerzenia lokacji, nie są jeszcze dostępne.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="4f0ed-148">Gdy te funkcje są dostępne, aktualizujemy nasze dokumentację i blog o zmianach hello.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="4f0ed-149">Ta publicznej wersji zapoznawczej jest obecnie dostępna tylko w następujących regionach hello:</span><span class="sxs-lookup"><span data-stu-id="4f0ed-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="4f0ed-150">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="4f0ed-150">West US</span></span>
* <span data-ttu-id="4f0ed-151">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="4f0ed-151">East US</span></span>
* <span data-ttu-id="4f0ed-152">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-152">West Europe</span></span>
* <span data-ttu-id="4f0ed-153">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="4f0ed-153">North Europe</span></span>
* <span data-ttu-id="4f0ed-154">Środkowo-południowe stany USA</span><span class="sxs-lookup"><span data-stu-id="4f0ed-154">South Central US</span></span>
* <span data-ttu-id="4f0ed-155">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="4f0ed-155">North Central US</span></span>
* <span data-ttu-id="4f0ed-156">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-156">Southeast Asia</span></span>
* <span data-ttu-id="4f0ed-157">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-157">East Asia</span></span>
* <span data-ttu-id="4f0ed-158">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-158">Australia East</span></span>
* <span data-ttu-id="4f0ed-159">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="4f0ed-159">Japan East</span></span>
* <span data-ttu-id="4f0ed-160">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="4f0ed-160">Brazil South</span></span>
* <span data-ttu-id="4f0ed-161">Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="4f0ed-161">South India</span></span>

<span data-ttu-id="4f0ed-162">Web Apps w systemie Linux jest obsługiwana tylko w planie usługi aplikacji dedykowanych hello i nie ma warstwy bezpłatna lub udostępnione.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="4f0ed-163">Ponadto planów usługi App Service dla zwykłych oraz aplikacje sieci web systemu Linux wzajemnie się wykluczają, więc nie można utworzyć aplikacji sieci web systemu Linux w planie usługi aplikacji z systemem innym niż Linux.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="4f0ed-164">Web Apps w systemie Linux należy utworzyć w grupie zasobów, która nie zawiera aplikacji sieci web z systemem innym niż Linux w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4f0ed-165">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="4f0ed-165">Troubleshooting</span></span> ##

<span data-ttu-id="4f0ed-166">Aplikacji nie powiedzie się toostart lub toocheck hello rejestrowania z aplikacji, sprawdź hello dzienniki w katalogu LogFiles hello Docker.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="4f0ed-167">Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="4f0ed-168">toolog hello `stdout` i `stderr` z Twojej kontenera należy tooenable **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Włączanie rejestrowania][2]

![Przy użyciu dzienników Docker tooview Kudu][1]

<span data-ttu-id="4f0ed-171">Można uzyskać dostępu do hello SCM lokacji z **zaawansowane narzędzia** w hello **narzędzi programistycznych** menu.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f0ed-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f0ed-172">Next steps</span></span>
<span data-ttu-id="4f0ed-173">Zobacz hello następującego łącza tooget korzystania z usługi aplikacji w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="4f0ed-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="4f0ed-174">Pytania i uwagi można umieścić na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="4f0ed-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="4f0ed-175">Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f0ed-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="4f0ed-176">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f0ed-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="4f0ed-177">W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="4f0ed-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="4f0ed-178">W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="4f0ed-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="4f0ed-179">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="4f0ed-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="4f0ed-180">Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f0ed-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="4f0ed-181">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="4f0ed-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="4f0ed-182">Centrum docker ciągłego wdrażania aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4f0ed-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png