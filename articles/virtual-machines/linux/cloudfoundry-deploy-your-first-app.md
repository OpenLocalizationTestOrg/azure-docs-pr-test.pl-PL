---
title: aaaDeploy pierwszy tooCloud aplikacji Foundry w systemie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie aplikacji tooCloud Foundry na platformie Azure"
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
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="7abc0-103">Wdrażanie pierwszego tooCloud aplikacji Foundry w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7abc0-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="7abc0-104">[Chmury Foundry](http://cloudfoundry.org) jest dostępna w systemie Microsoft Azure platformy popularnych aplikacji open source.</span><span class="sxs-lookup"><span data-stu-id="7abc0-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="7abc0-105">W tym artykule zostanie przedstawiony sposób toodeploy i zarządzanie nimi aplikacji w chmurze Foundry w środowisku platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7abc0-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="7abc0-106">Utwórz środowisko chmury Foundry</span><span class="sxs-lookup"><span data-stu-id="7abc0-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="7abc0-107">Dostępnych jest kilka opcji tworzenia środowiska Foundry chmurze na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="7abc0-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="7abc0-108">Użyj hello [oferta kluczową Foundry chmury] [ pcf-azuremarketplace] w hello Azure Marketplace toocreate standardowe środowisko obejmujące PCF Operations Manager i hello Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="7abc0-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="7abc0-109">Można znaleźć [wykonać instrukcje] [ pcf-azuremarketplace-pivotaldocs] wdrażania hello marketplace oferty w hello kluczową dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="7abc0-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="7abc0-110">Utwórz dostosowane środowisko przez [wdrażania ręcznego kluczową Foundry chmury][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="7abc0-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="7abc0-111">[Wdrażanie pakietów Foundry chmury open source hello bezpośrednio] [ oss-cf-bosh] poprzez ustawienie [BOSH](http://bosh.io) dyrektora, maszynę Wirtualną, która koordynuje hello wdrożenia środowiska chmury Foundry hello.</span><span class="sxs-lookup"><span data-stu-id="7abc0-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7abc0-112">Jeśli wdrażasz PCF z hello Azure Marketplace, zanotuj hello SYSTEMDOMAINURL i poświadczeń administratora hello wymagane tooaccess hello kluczową Menedżera aplikacje, które są opisanej w przewodniku wdrażania marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="7abc0-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="7abc0-113">One są toocomplete potrzebne w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7abc0-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="7abc0-114">W przypadku wdrożeń marketplace hello SYSTEMDOMAINURL jest https://system formularza hello. *adres ip*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="7abc0-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="7abc0-115">Połącz toohello kontrolerem chmury</span><span class="sxs-lookup"><span data-stu-id="7abc0-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="7abc0-116">Hello kontrolerem chmury to hello podstawowy wpis punktu tooa Foundry chmury środowisko wdrażania aplikacji i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="7abc0-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="7abc0-117">core Hello chmury kontrolera interfejsu API (CCAPI) to interfejs API REST, ale nie jest dostępny za pośrednictwem różnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="7abc0-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="7abc0-118">W takim przypadku możemy korzystać z niego za pośrednictwem hello [interfejsu wiersza polecenia chmury Foundry][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="7abc0-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="7abc0-119">Hello interfejsu wiersza polecenia można zainstalować w systemie Linux, MacOS lub systemu Windows, ale jeśli wolisz nie tooinstall go wcale, jest dostępny wstępnie zainstalowane w hello [powłoki chmury Azure][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="7abc0-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="7abc0-120">dołączenie wartości toolog, `api` toohello SYSTEMDOMAINURL uzyskany z hello marketplace wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7abc0-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="7abc0-121">Ponieważ hello domyślne wdrożenie używa certyfikatu z podpisem własnym, należy także uwzględnić hello `skip-ssl-validation` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="7abc0-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="7abc0-122">Jesteś zostanie wyświetlony monit o toolog w toohello kontrolerem chmury.</span><span class="sxs-lookup"><span data-stu-id="7abc0-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="7abc0-123">Użyj hello poświadczeń konta administratora, które uzyskane z kroki wdrażania hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="7abc0-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="7abc0-124">Udostępnia chmury Foundry *organizacjami* i *spacji* jako przestrzenie nazw tooisolate hello zespołów i środowisk, w ramach wdrożenia udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="7abc0-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="7abc0-125">Hello PCF wdrożenia marketplace zawiera domyślne hello *systemu* organizacji i zestaw funkcji miejsca do utworzenia toocontain hello podstawowe składniki, takie jak usługi Skalowanie automatyczne hello i hello brokera usług Azure.</span><span class="sxs-lookup"><span data-stu-id="7abc0-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="7abc0-126">Teraz, wybierz hello *systemu* miejsca.</span><span class="sxs-lookup"><span data-stu-id="7abc0-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="7abc0-127">Tworzenie schematu i miejsca</span><span class="sxs-lookup"><span data-stu-id="7abc0-127">Create an org and space</span></span>

<span data-ttu-id="7abc0-128">W przypadku wpisania `cf apps`, należy zapoznać się z zestawem aplikacji systemu, które zostały wdrożone w miejscu systemu hello w hello org. systemu</span><span class="sxs-lookup"><span data-stu-id="7abc0-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="7abc0-129">Zachowaj hello *systemu* org zastrzeżone dla aplikacji systemu dlatego Utwórz toohouse organizacji i miejsca naszych przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abc0-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="7abc0-130">Użyj hello docelowego polecenia tooswitch toohello nowej organizacji i miejsca:</span><span class="sxs-lookup"><span data-stu-id="7abc0-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="7abc0-131">Teraz gdy wdrażana jest aplikacja została ona utworzona automatycznie w nowej organizacji hello i miejsca.</span><span class="sxs-lookup"><span data-stu-id="7abc0-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="7abc0-132">tooconfirm, który obecnie nie istnieją żadne aplikacji w nowej organizacji hello na miejsce, typu `cf apps` ponownie.</span><span class="sxs-lookup"><span data-stu-id="7abc0-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="7abc0-133">Aby uzyskać więcej informacji na temat organizacjami i spacje i jak one używane do kontroli dostępu opartej na rolach (RBAC), zobacz hello [Foundry chmury dokumentacji][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="7abc0-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="7abc0-134">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7abc0-134">Deploy an application</span></span>

<span data-ttu-id="7abc0-135">Użyjmy Foundry chmury przykładową aplikację o nazwie Hello Spring chmury, co jest napisany w języku Java i oparte na powitania [Spring Framework](http://spring.io) i [rozruchu Spring](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="7abc0-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="7abc0-136">Klonuj repozytorium chmury Spring Hello hello</span><span class="sxs-lookup"><span data-stu-id="7abc0-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="7abc0-137">Chmury Spring Hello Przykładowa aplikacja Hello jest dostępna w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7abc0-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="7abc0-138">Ją sklonować tooyour środowiska i zmień do nowego katalogu hello:</span><span class="sxs-lookup"><span data-stu-id="7abc0-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="7abc0-139">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7abc0-139">Build hello application</span></span>

<span data-ttu-id="7abc0-140">Przy użyciu aplikacji hello kompilacji [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="7abc0-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="7abc0-141">Wdrażanie aplikacji hello z cf wypychania</span><span class="sxs-lookup"><span data-stu-id="7abc0-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="7abc0-142">Większość aplikacji tooCloud Foundry można wdrożyć przy użyciu hello `push` polecenia:</span><span class="sxs-lookup"><span data-stu-id="7abc0-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="7abc0-143">Gdy użytkownik *wypychania* aplikacji, chmury Foundry wykrywa hello typu aplikacji (w tym przypadku aplikacji Java) i jego zależności (w przypadku platforma Spring hello) identyfikuje.</span><span class="sxs-lookup"><span data-stu-id="7abc0-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="7abc0-144">Pakiety następnie wszystkie elementy wymagane toorun kodu w obrazie kontenera autonomiczny, nazywany *dropletu*.</span><span class="sxs-lookup"><span data-stu-id="7abc0-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="7abc0-145">Na koniec harmonogramy Foundry chmury hello aplikacji na jednym hello dostępne maszyn w środowisku i tworzy adresu URL, na której możesz uzyskiwać dostęp, która jest dostępna w hello dane wyjściowe polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="7abc0-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Dane wyjściowe polecenia wypychania cf][cf-push-output]

<span data-ttu-id="7abc0-147">toosee hello hello spring chmury aplikacji, otwórz hello podany adres URL, w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="7abc0-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Domyślny interfejs użytkownika dla chmury Hello Spring][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="7abc0-149">więcej informacji na temat efektów podczas toolearn `cf push`, zobacz [jak aplikacje są umieszczane] [ cf-push-docs] w hello dokumentacji Foundry chmury.</span><span class="sxs-lookup"><span data-stu-id="7abc0-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="7abc0-150">Wyświetl dzienniki aplikacji</span><span class="sxs-lookup"><span data-stu-id="7abc0-150">View application logs</span></span>

<span data-ttu-id="7abc0-151">Witaj CLI Foundry chmury tooview dzienników można używać do aplikacji, za pomocą nazwy:</span><span class="sxs-lookup"><span data-stu-id="7abc0-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="7abc0-152">Domyślnie program hello rejestruje używa polecenia *tail*, który wskazuje nowe dzienniki, ponieważ są one zapisywane.</span><span class="sxs-lookup"><span data-stu-id="7abc0-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="7abc0-153">pojawią się nowe dzienniki toosee, Odśwież hello aplikacji hello spring chmury w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="7abc0-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="7abc0-154">Dzienniki tooview, które już zostały zapisane, Dodaj hello `recent` przełącznika:</span><span class="sxs-lookup"><span data-stu-id="7abc0-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="7abc0-155">Aplikacja hello skali</span><span class="sxs-lookup"><span data-stu-id="7abc0-155">Scale hello application</span></span>

<span data-ttu-id="7abc0-156">Domyślnie `cf push` tworzy tylko jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abc0-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="7abc0-157">tooensure wysokiej dostępności i Włączanie skalowania dla wyższej przepustowości, zazwyczaj mają toorun więcej niż jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abc0-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="7abc0-158">Możesz łatwo skalować w poziomie już wdrożone aplikacje za pomocą hello `scale` polecenia:</span><span class="sxs-lookup"><span data-stu-id="7abc0-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="7abc0-159">Uruchomione hello `cf app` polecenia w aplikacji hello pokazuje, czy inne wystąpienie aplikacji hello tworzy Foundry chmury.</span><span class="sxs-lookup"><span data-stu-id="7abc0-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="7abc0-160">Po uruchomieniu aplikacji hello, w chmurze Foundry tooit ruchu równoważenia obciążenia jest uruchamiana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7abc0-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7abc0-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7abc0-161">Next steps</span></span>

- <span data-ttu-id="7abc0-162">[Witaj odczytu dokumentacji chmury Foundry][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="7abc0-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="7abc0-163">[Konfigurowanie hello dodatku Visual Studio Team Services dla chmury Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="7abc0-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="7abc0-164">[Konfigurowanie hello końcówki Analiza dzienników Microsoft dla chmury Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="7abc0-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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