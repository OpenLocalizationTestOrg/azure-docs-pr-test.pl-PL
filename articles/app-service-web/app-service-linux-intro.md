---
title: Wprowadzenie do aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="e4485-104">Wprowadzenie do aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e4485-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="e4485-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e4485-105">Overview</span></span>
<span data-ttu-id="e4485-106">Klienci mogą użyć aplikacji sieci Web w systemie Linux do aplikacji sieci web hosta natywnie w systemie Linux dla stosy obsługiwanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4485-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="e4485-107">W poniższej sekcji przedstawiono stosy aplikacji, które są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e4485-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="e4485-108">Funkcje</span><span class="sxs-lookup"><span data-stu-id="e4485-108">Features</span></span>
<span data-ttu-id="e4485-109">Aplikacji w systemie Linux sieci Web obsługuje obecnie następujących stosy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e4485-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="e4485-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="e4485-110">Node.js</span></span>
    * <span data-ttu-id="e4485-111">4.4</span><span class="sxs-lookup"><span data-stu-id="e4485-111">4.4</span></span>
    * <span data-ttu-id="e4485-112">4.5</span><span class="sxs-lookup"><span data-stu-id="e4485-112">4.5</span></span>
    * <span data-ttu-id="e4485-113">6.2</span><span class="sxs-lookup"><span data-stu-id="e4485-113">6.2</span></span>
    * <span data-ttu-id="e4485-114">6.6</span><span class="sxs-lookup"><span data-stu-id="e4485-114">6.6</span></span>
    * <span data-ttu-id="e4485-115">6.9</span><span class="sxs-lookup"><span data-stu-id="e4485-115">6.9</span></span>
    * <span data-ttu-id="e4485-116">6.10</span><span class="sxs-lookup"><span data-stu-id="e4485-116">6.10</span></span>
    * <span data-ttu-id="e4485-117">6.11</span><span class="sxs-lookup"><span data-stu-id="e4485-117">6.11</span></span>
    * <span data-ttu-id="e4485-118">8.0</span><span class="sxs-lookup"><span data-stu-id="e4485-118">8.0</span></span>
    * <span data-ttu-id="e4485-119">8.1</span><span class="sxs-lookup"><span data-stu-id="e4485-119">8.1</span></span>
* <span data-ttu-id="e4485-120">PHP</span><span class="sxs-lookup"><span data-stu-id="e4485-120">PHP</span></span>
    * <span data-ttu-id="e4485-121">5.6</span><span class="sxs-lookup"><span data-stu-id="e4485-121">5.6</span></span>
    * <span data-ttu-id="e4485-122">7.0</span><span class="sxs-lookup"><span data-stu-id="e4485-122">7.0</span></span>
* <span data-ttu-id="e4485-123">Oprogramowanie .NET core</span><span class="sxs-lookup"><span data-stu-id="e4485-123">.Net Core</span></span>
    * <span data-ttu-id="e4485-124">1.0</span><span class="sxs-lookup"><span data-stu-id="e4485-124">1.0</span></span>
    * <span data-ttu-id="e4485-125">1.1</span><span class="sxs-lookup"><span data-stu-id="e4485-125">1.1</span></span>
* <span data-ttu-id="e4485-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="e4485-126">Ruby</span></span>
    * <span data-ttu-id="e4485-127">2.3</span><span class="sxs-lookup"><span data-stu-id="e4485-127">2.3</span></span>

<span data-ttu-id="e4485-128">Klienci mogą wdrożyć swoich aplikacji przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="e4485-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="e4485-129">FTP</span><span class="sxs-lookup"><span data-stu-id="e4485-129">FTP</span></span>
* <span data-ttu-id="e4485-130">Lokalne Git</span><span class="sxs-lookup"><span data-stu-id="e4485-130">Local Git</span></span>
* <span data-ttu-id="e4485-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="e4485-131">GitHub</span></span>
* <span data-ttu-id="e4485-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="e4485-132">Bitbucket</span></span>

<span data-ttu-id="e4485-133">Do skalowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e4485-133">For application scaling:</span></span>

* <span data-ttu-id="e4485-134">Klientów można skalować aplikacji sieci web górę i w dół, zmieniając warstwę ich planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4485-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="e4485-135">Klienci mogą skalowanie aplikacji i uruchamiać wiele wystąpień aplikacji w obrębie ich jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="e4485-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="e4485-136">Dla Kudu, niektóre podstawowe funkcje:</span><span class="sxs-lookup"><span data-stu-id="e4485-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="e4485-137">Środowisk</span><span class="sxs-lookup"><span data-stu-id="e4485-137">Environments</span></span>
* <span data-ttu-id="e4485-138">Wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e4485-138">Deployments</span></span>
* <span data-ttu-id="e4485-139">Podstawowe konsoli</span><span class="sxs-lookup"><span data-stu-id="e4485-139">Basic console</span></span>
* <span data-ttu-id="e4485-140">SSH</span><span class="sxs-lookup"><span data-stu-id="e4485-140">SSH</span></span>

<span data-ttu-id="e4485-141">Dla opracowywania oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="e4485-141">For devops:</span></span>

* <span data-ttu-id="e4485-142">Środowiska przejściowe</span><span class="sxs-lookup"><span data-stu-id="e4485-142">Staging environments</span></span>
* <span data-ttu-id="e4485-143">ACR i DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="e4485-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="e4485-144">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="e4485-144">Limitations</span></span>
<span data-ttu-id="e4485-145">Azure portal zawiera tylko funkcje, które obecnie działają dla aplikacji sieci Web w systemie Linux i ukrywa pozostałe.</span><span class="sxs-lookup"><span data-stu-id="e4485-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="e4485-146">Jak możemy włączyć funkcje dodatkowe, będą one widoczne w portalu.</span><span class="sxs-lookup"><span data-stu-id="e4485-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="e4485-147">Niektóre funkcje, takie jak integracji sieci wirtualnej, Azure Active Directory/uwierzytelniania innej firmy lub Kudu rozszerzenia lokacji, nie są jeszcze dostępne.</span><span class="sxs-lookup"><span data-stu-id="e4485-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="e4485-148">Gdy te funkcje są dostępne, aktualizujemy nasze dokumentację i blog o zmianach.</span><span class="sxs-lookup"><span data-stu-id="e4485-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="e4485-149">Ta publicznej wersji zapoznawczej jest obecnie dostępna tylko w następujących regionach:</span><span class="sxs-lookup"><span data-stu-id="e4485-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="e4485-150">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="e4485-150">West US</span></span>
* <span data-ttu-id="e4485-151">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="e4485-151">East US</span></span>
* <span data-ttu-id="e4485-152">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="e4485-152">West Europe</span></span>
* <span data-ttu-id="e4485-153">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="e4485-153">North Europe</span></span>
* <span data-ttu-id="e4485-154">Środkowo-południowe stany USA</span><span class="sxs-lookup"><span data-stu-id="e4485-154">South Central US</span></span>
* <span data-ttu-id="e4485-155">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="e4485-155">North Central US</span></span>
* <span data-ttu-id="e4485-156">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e4485-156">Southeast Asia</span></span>
* <span data-ttu-id="e4485-157">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e4485-157">East Asia</span></span>
* <span data-ttu-id="e4485-158">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e4485-158">Australia East</span></span>
* <span data-ttu-id="e4485-159">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e4485-159">Japan East</span></span>
* <span data-ttu-id="e4485-160">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="e4485-160">Brazil South</span></span>
* <span data-ttu-id="e4485-161">Indie Południowe</span><span class="sxs-lookup"><span data-stu-id="e4485-161">South India</span></span>

<span data-ttu-id="e4485-162">Web Apps w systemie Linux jest obsługiwana tylko w planie usługi aplikacji dedykowanej i nie ma warstwy bezpłatna lub udostępnione.</span><span class="sxs-lookup"><span data-stu-id="e4485-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="e4485-163">Ponadto planów usługi App Service dla zwykłych oraz aplikacje sieci web systemu Linux wzajemnie się wykluczają, więc nie można utworzyć aplikacji sieci web systemu Linux w planie usługi aplikacji z systemem innym niż Linux.</span><span class="sxs-lookup"><span data-stu-id="e4485-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="e4485-164">Web Apps w systemie Linux należy utworzyć w grupie zasobów, która nie zawiera aplikacji sieci web z systemem innym niż Linux, w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="e4485-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e4485-165">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e4485-165">Troubleshooting</span></span> ##

<span data-ttu-id="e4485-166">Aplikacji nie powiedzie się lub chcesz sprawdzić rejestrowania z aplikacji, sprawdź dzienniki w katalogu LogFiles Docker.</span><span class="sxs-lookup"><span data-stu-id="e4485-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="e4485-167">Za pomocą witryny SCM, lub za pośrednictwem protokołu FTP można uzyskać dostępu do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="e4485-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="e4485-168">W dzienniku `stdout` i `stderr` z Twojej kontenera, musisz włączyć **rejestrowania kontenera Docker** w obszarze **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="e4485-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Włączanie rejestrowania][2]

![Aby wyświetlić dzienniki Docker przy użyciu Kudu][1]

<span data-ttu-id="e4485-171">Można uzyskać dostępu do lokacji SCM z **zaawansowane narzędzia** w **narzędzi programistycznych** menu.</span><span class="sxs-lookup"><span data-stu-id="e4485-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4485-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4485-172">Next steps</span></span>
<span data-ttu-id="e4485-173">Zobacz poniższe łącza, aby rozpocząć korzystanie z usługi aplikacji w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="e4485-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="e4485-174">Pytania i uwagi można umieścić na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="e4485-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="e4485-175">Sposób użycia niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e4485-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="e4485-176">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e4485-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="e4485-177">W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="e4485-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="e4485-178">W aplikacji sieci Web usługi aplikacji Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="e4485-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="e4485-179">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="e4485-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="e4485-180">Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e4485-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="e4485-181">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="e4485-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="e4485-182">Centrum docker ciągłego wdrażania aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e4485-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png