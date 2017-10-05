---
title: "Wdrażanie pierwszej aplikacji do Foundry chmury w systemie Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Wdrażanie aplikacji Foundry chmurze na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="96adf-103">Wdrażanie pierwszej aplikacji do Foundry chmury w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="96adf-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="96adf-104">[Chmury Foundry](http://cloudfoundry.org) jest dostępna w systemie Microsoft Azure platformy popularnych aplikacji open source.</span><span class="sxs-lookup"><span data-stu-id="96adf-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="96adf-105">W tym artykule zostanie przedstawiony sposób wdrażania i zarządzania nimi aplikacji w chmurze Foundry w środowisku platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="96adf-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="96adf-106">Utwórz środowisko chmury Foundry</span><span class="sxs-lookup"><span data-stu-id="96adf-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="96adf-107">Dostępnych jest kilka opcji tworzenia środowiska Foundry chmurze na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="96adf-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="96adf-108">Użyj [oferta kluczową Foundry chmury] [ pcf-azuremarketplace] w portalu Azure Marketplace do utworzenia standardowe środowisko obejmujące PCF Operations Manager i usługi Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="96adf-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="96adf-109">Można znaleźć [wykonać instrukcje] [ pcf-azuremarketplace-pivotaldocs] wdrażania portalu marketplace oferują w kluczową dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="96adf-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="96adf-110">Utwórz dostosowane środowisko przez [wdrażania ręcznego kluczową Foundry chmury][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="96adf-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="96adf-111">[Wdrażanie pakietów Foundry chmury open source bezpośrednio] [ oss-cf-bosh] poprzez ustawienie [BOSH](http://bosh.io) dyrektora, maszynę Wirtualną, która koordynuje wdrożenia w środowisku chmury Foundry.</span><span class="sxs-lookup"><span data-stu-id="96adf-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="96adf-112">Jeśli wdrażasz PCF z portalu Azure Marketplace, zanotuj SYSTEMDOMAINURL i poświadczeń administratora wymagane do uzyskania dostępu kluczową Menedżera aplikacji, które zostały opisane w przewodniku wdrażania portalu marketplace.</span><span class="sxs-lookup"><span data-stu-id="96adf-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="96adf-113">Są one niezbędne do ukończenia tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="96adf-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="96adf-114">W przypadku wdrożeń marketplace SYSTEMDOMAINURL jest https://system formularza. *adres ip*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="96adf-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="96adf-115">Połączyć się z kontrolerem chmury</span><span class="sxs-lookup"><span data-stu-id="96adf-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="96adf-116">Kontroler chmury jest podstawowy punkt wejścia do środowiska chmury Foundry wdrażania i zarządzania aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="96adf-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="96adf-117">Core chmury kontrolera interfejsu API (CCAPI) to interfejs API REST, ale nie jest dostępny za pośrednictwem różnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="96adf-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="96adf-118">W takim przypadku możemy korzystać z niego za pośrednictwem [interfejsu wiersza polecenia chmury Foundry][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="96adf-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="96adf-119">Interfejsu wiersza polecenia można zainstalować w systemie Linux, MacOS lub systemu Windows, ale jeśli użytkownik nie chce go zainstalować na wszystkich, jest dostępny wstępnie zainstalowane w [powłoki chmury Azure][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="96adf-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="96adf-120">Aby zalogować się, dołączenie wartości `api` do SYSTEMDOMAINURL, uzyskany z wdrożenia w witrynie marketplace.</span><span class="sxs-lookup"><span data-stu-id="96adf-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="96adf-121">Ponieważ instalacja domyślna używa certyfikatu z podpisem własnym, należy także uwzględnić `skip-ssl-validation` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="96adf-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="96adf-122">Zostanie wyświetlony monit logowania do kontrolera chmury.</span><span class="sxs-lookup"><span data-stu-id="96adf-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="96adf-123">Użyj poświadczeń konta administratora, które uzyskane z portalu marketplace procedury wdrażania.</span><span class="sxs-lookup"><span data-stu-id="96adf-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="96adf-124">Udostępnia chmury Foundry *organizacjami* i *spacji* jako przestrzenie nazw, aby wykrywać zespołów i środowisk, w ramach wdrożenia udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="96adf-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="96adf-125">Wdrożenie marketplace PCF zawiera domyślne *systemu* organizacji i zestaw spacje zawiera podstawowe składniki, takie jak usługi Skalowanie automatyczne i brokera usług Azure.</span><span class="sxs-lookup"><span data-stu-id="96adf-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="96adf-126">Teraz, wybierz *systemu* miejsca.</span><span class="sxs-lookup"><span data-stu-id="96adf-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="96adf-127">Tworzenie schematu i miejsca</span><span class="sxs-lookup"><span data-stu-id="96adf-127">Create an org and space</span></span>

<span data-ttu-id="96adf-128">W przypadku wpisania `cf apps`, należy zapoznać się z zestawem aplikacji systemu, które zostały wdrożone w miejscu systemu w ramach org. systemu</span><span class="sxs-lookup"><span data-stu-id="96adf-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="96adf-129">Zachowaj *systemu* org zastrzeżone dla aplikacji systemu, dlatego Utwórz organizacji i miejsca do przechowywania naszych przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96adf-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="96adf-130">Przełącz się do nowego schematu i miejsca za pomocą polecenia docelowych:</span><span class="sxs-lookup"><span data-stu-id="96adf-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="96adf-131">Teraz gdy wdrażana jest aplikacja została ona utworzona automatycznie w nowej organizacji i miejsca.</span><span class="sxs-lookup"><span data-stu-id="96adf-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="96adf-132">Aby upewnić się, że żadne aplikacje nie są aktualnie w nowej organizacji/miejsca, wpisz `cf apps` ponownie.</span><span class="sxs-lookup"><span data-stu-id="96adf-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="96adf-133">Aby uzyskać więcej informacji na temat organizacjami i spacje i jak one używane do kontroli dostępu opartej na rolach (RBAC), zobacz [Foundry chmury dokumentacji][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="96adf-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="96adf-134">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="96adf-134">Deploy an application</span></span>

<span data-ttu-id="96adf-135">Użyjmy Foundry chmury przykładową aplikację o nazwie Hello Spring chmury, co jest napisany w języku Java i na podstawie [Spring Framework](http://spring.io) i [rozruchu Spring](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="96adf-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="96adf-136">Klonuj repozytorium Hello Spring chmury</span><span class="sxs-lookup"><span data-stu-id="96adf-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="96adf-137">Przykładowa aplikacja Hello Spring chmury jest dostępna w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="96adf-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="96adf-138">Sklonować go do środowiska i zmień do nowego katalogu:</span><span class="sxs-lookup"><span data-stu-id="96adf-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="96adf-139">Kompilowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="96adf-139">Build the application</span></span>

<span data-ttu-id="96adf-140">Tworzenie aplikacji w programie [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="96adf-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="96adf-141">Wdrażanie aplikacji z cf wypychania</span><span class="sxs-lookup"><span data-stu-id="96adf-141">Deploy the application with cf push</span></span>

<span data-ttu-id="96adf-142">Można wdrożyć większość aplikacji przy użyciu chmury Foundry `push` polecenia:</span><span class="sxs-lookup"><span data-stu-id="96adf-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="96adf-143">Gdy użytkownik *wypychania* aplikacji, chmury Foundry wykrywa typu aplikacji (w tym przypadku aplikacji Java) i jego zależności (w tym przypadku Spring framework) identyfikuje.</span><span class="sxs-lookup"><span data-stu-id="96adf-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="96adf-144">Pakiety następnie wszystko, co jest wymagane do uruchomienia kodu w obrazie kontenera autonomiczny, nazywany *dropletu*.</span><span class="sxs-lookup"><span data-stu-id="96adf-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="96adf-145">Na koniec Foundry chmury planuje aplikacji na jednym z dostępnych maszyn w środowisku i tworzy adres URL, w której możesz uzyskiwać dostęp, która jest dostępna w danych wyjściowych polecenia.</span><span class="sxs-lookup"><span data-stu-id="96adf-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![Dane wyjściowe polecenia wypychania cf][cf-push-output]

<span data-ttu-id="96adf-147">Aby wyświetlić aplikacji hello spring chmury, należy otworzyć podanego adresu URL w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="96adf-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Domyślny interfejs użytkownika dla chmury Hello Spring][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="96adf-149">Aby dowiedzieć się więcej na temat zachodzących podczas `cf push`, zobacz [jak aplikacje są umieszczane] [ cf-push-docs] w dokumentacji Foundry chmury.</span><span class="sxs-lookup"><span data-stu-id="96adf-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="96adf-150">Wyświetl dzienniki aplikacji</span><span class="sxs-lookup"><span data-stu-id="96adf-150">View application logs</span></span>

<span data-ttu-id="96adf-151">CLI Foundry chmury służy do wyświetlania dzienników dla aplikacji za pomocą nazwy:</span><span class="sxs-lookup"><span data-stu-id="96adf-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="96adf-152">Domyślnie dzienniki polecenia używa *tail*, który wskazuje nowe dzienniki, ponieważ są one zapisywane.</span><span class="sxs-lookup"><span data-stu-id="96adf-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="96adf-153">Aby zobaczyć nowe dzienniki są wyświetlane, Odśwież aplikacji hello spring chmury w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="96adf-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="96adf-154">Aby wyświetlić dzienniki, które już zostały zapisane, Dodaj `recent` przełącznika:</span><span class="sxs-lookup"><span data-stu-id="96adf-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="96adf-155">Skalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="96adf-155">Scale the application</span></span>

<span data-ttu-id="96adf-156">Domyślnie `cf push` tworzy tylko jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96adf-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="96adf-157">Aby zapewnić wysoką dostępność i włączyć skalowania w poziomie wyższej przepustowości, zazwyczaj chcesz uruchomić więcej niż jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96adf-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="96adf-158">Możesz łatwo skalować w poziomie już wdrożone aplikacje za pomocą `scale` polecenia:</span><span class="sxs-lookup"><span data-stu-id="96adf-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="96adf-159">Uruchomiona `cf app` polecenia w aplikacji pokazuje, że Foundry chmury wprowadza inne wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96adf-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="96adf-160">Po uruchomieniu aplikacji, w chmurze Foundry ruchu do niego równoważenia obciążenia jest uruchamiana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="96adf-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="96adf-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96adf-161">Next steps</span></span>

- <span data-ttu-id="96adf-162">[Zapoznaj się z dokumentacją chmury Foundry][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="96adf-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="96adf-163">[Konfigurowanie dodatku Visual Studio Team Services dla chmury Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="96adf-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="96adf-164">[Konfigurowanie końcówkę Analiza dzienników Microsoft dla chmury Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="96adf-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png