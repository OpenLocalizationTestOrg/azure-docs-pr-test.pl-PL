---
title: "Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service"
description: "Dowiedz się, jak lotu nowych funkcji w aplikacji lub wersji beta testowania aktualizacji w tym samouczku end-to-end. Powoduje przeniesienie razem usługi aplikacji funkcje, takie jak ciągła publikowania, miejsc routingu ruchu i integracji usługi Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="c9d1f-104">Flighting wdrożenia (testowania wersji beta) w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c9d1f-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="c9d1f-105">W tym samouczku przedstawiono sposób wykonywania *flighting wdrożeń* dzięki integracji z różnych funkcji programu [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="c9d1f-106">*Flighting* jest procesem wdrażania, która weryfikuje nowej funkcji lub zmiany z ograniczoną liczbą rzeczywistą klientów, a główne testowanie w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="c9d1f-107">Podobnie testowania w wersji beta i jest czasem nazywana "transmitowane kontrolowane testu".</span><span class="sxs-lookup"><span data-stu-id="c9d1f-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="c9d1f-108">Wiele dużych przedsiębiorstw witrynę internetową Użyj tej metody, aby uzyskać wczesne sprawdzania poprawności na ich aktualizacji aplikacji, w praktyce ich [elastyczne programowanie](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="c9d1f-109">Usługa aplikacji Azure umożliwia testowanie w produkcji jest integrowana z ciągłej publikowanie i Application Insights, aby wdrożyć scenariusz dla tego samego DevOps.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span></span> <span data-ttu-id="c9d1f-110">Zalety tego podejścia:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="c9d1f-111">**Uzyskaj opinie rzeczywistych *przed* aktualizacje są wydawane w środowisku produkcyjnym** -jedynym elementem lepszym rozwiązaniem niż uzyskanie opinii zaraz po zwolnieniu jest uzyskanie opinii przed zwolnieniem.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="c9d1f-112">Wczesne wymagasz w cyklu życia produktu można przetestować aktualizacje o ruchu rzeczywistych użytkowników i zachowania.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span></span>
* <span data-ttu-id="c9d1f-113">**Ulepszanie [ciągłego test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  — dzięki zintegrowaniu testowanie w produkcji z ciągłej integracji i instrumentacji z usługi Application Insights, sprawdzanie poprawności użytkownika odbywa się wczesne i automatycznie w cykl życia.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="c9d1f-114">Pozwala to zmniejszyć inwestycji czas wykonywania testu ręcznego.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="c9d1f-115">**Optymalizacja przepływ testowej pracy w** -automatyzując testowanie w produkcji z ciągłego monitorowania Instrumentacji potencjalnie wykonasz celów różnego rodzaju testów w ramach jednego procesu, taką jak [integracji](https://en.wikipedia.org/wiki/Integration_testing), [regresji](https://en.wikipedia.org/wiki/Regression_testing), [użyteczność](https://en.wikipedia.org/wiki/Usability_testing), ułatwień dostępu, lokalizacji, [wydajności](https://en.wikipedia.org/wiki/Software_performance_testing), [zabezpieczeń](https://en.wikipedia.org/wiki/Security_testing), i [akceptacji](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="c9d1f-116">Flighting wdrożenia nie jest niemal routingu ruchu sieciowego na żywo.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="c9d1f-117">W takim wdrożeniu chcesz uzyskiwać wgląd w możliwie jak najszybciej czy też być nieoczekiwany błąd, spadek wydajności, problemy środowisko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="c9d1f-118">Należy pamiętać, że mamy do czynienia z klientami prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="c9d1f-119">Tak aby zrobić to prawo, należy się upewnić czy zdefiniowano flighting wdrożenia można zebrać wszystkie dane potrzebne do podjąć świadomej decyzji dla kolejny krok.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span></span> <span data-ttu-id="c9d1f-120">Ten samouczek pokazuje, jak zbierać dane z usługi Application Insights, ale możesz użyć usługi New Relic lub inne technologie, które pasujące do danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c9d1f-121">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="c9d1f-121">What you will do</span></span>
<span data-ttu-id="c9d1f-122">Z tego samouczka dowiesz się, jak można wyświetlić następujące scenariusze ze sobą, aby przetestować aplikację usługi aplikacji w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span></span>

* <span data-ttu-id="c9d1f-123">[Kierować ruchem produkcji](app-service-web-test-in-production-get-start.md) do aplikacji w wersji beta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span></span>
* <span data-ttu-id="c9d1f-124">[Instrumentacja aplikacji](../application-insights/app-insights-web-track-usage.md) uzyskać przydatne metryki</span><span class="sxs-lookup"><span data-stu-id="c9d1f-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span></span>
* <span data-ttu-id="c9d1f-125">Stale wdrażanie aplikacji w wersji beta i śledzić metryki aktywnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="c9d1f-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="c9d1f-126">Porównywanie metryk między aplikacją produkcyjnych i aplikacji w wersji beta, aby zobaczyć, jak zmiany kodu przełożyć na wyniki</span><span class="sxs-lookup"><span data-stu-id="c9d1f-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="c9d1f-127">Dane będą potrzebne</span><span class="sxs-lookup"><span data-stu-id="c9d1f-127">What you will need</span></span>
* <span data-ttu-id="c9d1f-128">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c9d1f-128">An Azure account</span></span>
* <span data-ttu-id="c9d1f-129">A [GitHub](https://github.com/) konta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="c9d1f-130">Visual Studio 2015 — można pobrać [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="c9d1f-131">Powłoka Git (zainstalowaną z [GitHub dla systemu Windows](https://windows.github.com/)) — umożliwia to uruchamianie poleceń programu PowerShell i Git w tej samej sesji</span><span class="sxs-lookup"><span data-stu-id="c9d1f-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span></span>
* <span data-ttu-id="c9d1f-132">Najnowsze [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) usługi bits</span><span class="sxs-lookup"><span data-stu-id="c9d1f-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="c9d1f-133">Podstawową wiedzę na temat następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-133">Basic understanding of the following:</span></span>
  * <span data-ttu-id="c9d1f-134">[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania szablonu (zobacz [wdrażanie złożonych aplikacji przewidywalnego na platformie Azure](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="c9d1f-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="c9d1f-135">Git</span><span class="sxs-lookup"><span data-stu-id="c9d1f-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="c9d1f-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9d1f-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="c9d1f-137">Do ukończenia tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-137">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="c9d1f-138">Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt służy do wypróbowania płatnych usług Azure, a nawet po wyczerpaniu możesz zachować konto i korzystać z bezpłatnych usług platformy Azure, takich jak aplikacje sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="c9d1f-139">Możesz [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -Your Visual Studio subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="c9d1f-140">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c9d1f-141">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="c9d1f-142">Konfigurowanie aplikacji sieci web w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="c9d1f-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="c9d1f-143">Skrypt używany w tym samouczku zostaną skonfigurowane automatycznie ciągłego publikowania z repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="c9d1f-144">Wymaga to, że Twoje poświadczenia GitHub są już przechowywane na platformie Azure, w przeciwnym razie wdrażanie przy użyciu skryptu zakończy się niepowodzeniem podczas próby skonfigurowania ustawień kontroli źródła dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span></span>
>
> <span data-ttu-id="c9d1f-145">Aby przechowywać swoje poświadczenia usługi GitHub na platformie Azure, tworzenie aplikacji sieci web w [Azure Portal](https://portal.azure.com/) i [skonfigurować wdrożenie GitHub](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="c9d1f-146">Wystarczy wykonać jeden raz.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-146">You only need to do this once.</span></span>
>
>

<span data-ttu-id="c9d1f-147">W typowy scenariusz DevOps masz aplikację, która działa na platformie Azure, i chcesz wprowadzić zmiany poprzez publikowanie ciągłe.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="c9d1f-148">W tym scenariuszu zostanie wdrożona do środowiska produkcyjnego szablonu, który został opracowany i przetestowany.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-148">In this scenario, you will deploy to production a template that you have developed and tested.</span></span>

1. <span data-ttu-id="c9d1f-149">Tworzenie własnych rozwidlenia [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="c9d1f-150">Aby uzyskać informacje dotyczące tworzenia rozwidlenia, zobacz [rozwidlania repozytorium](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="c9d1f-151">Po utworzeniu rozwidlenia, można to sprawdzić w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="c9d1f-152">Otwórz sesję powłoki Git.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-152">Open a Git Shell session.</span></span> <span data-ttu-id="c9d1f-153">Jeśli nie masz jeszcze powłoki Git, zainstaluj [GitHub dla systemu Windows](https://windows.github.com/) teraz.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="c9d1f-154">Utwórz lokalne Sklonowanie rozwidlenia, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-154">Create a local clone of your fork by executing the following command:</span></span>

     <span data-ttu-id="c9d1f-155">https://github.com/<your_fork>/ToDoApp.git klonowania git</span><span class="sxs-lookup"><span data-stu-id="c9d1f-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="c9d1f-156">Po utworzeniu sieci lokalnej klonowania, przejdź do  *&lt;repository_root >*\ARMTemplates i uruchomić deploy.ps1 skrypt z unikatowy sufiks, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-156">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="c9d1f-157">https://github.com/<your_fork>/todoapp.git — RepoUrl.\deploy.ps1 - ResourceGroupSuffix < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c9d1f-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="c9d1f-158">Po wyświetleniu monitu wpisz odpowiednią nazwę użytkownika i hasło dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-158">When prompted, type in the desired username and password for database access.</span></span> <span data-ttu-id="c9d1f-159">Pamiętaj poświadczenia bazy danych, ponieważ trzeba je ponownie określić podczas aktualizowania grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span></span>

   <span data-ttu-id="c9d1f-160">Postęp inicjowania obsługi administracyjnej z różnymi zasobami Azure powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-160">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="c9d1f-161">Po zakończeniu wdrażania, skrypt zostanie uruchomić aplikację w przeglądarce i podamy przyjazne sygnału dźwiękowego.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="c9d1f-162">Ponownie w sesji programu Git powłoki, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="c9d1f-163">. \swap — nazwa ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c9d1f-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="c9d1f-164">Po zakończeniu działania skryptu, przejdź wstecz, aby przejść do adresu serwera sieci Web (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) aby zobaczyć aplikacja była uruchomiona w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="c9d1f-165">Zaloguj się do [Azure Portal](https://portal.azure.com/) i spójrz na to, co jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="c9d1f-166">Powinny być widoczne dwie aplikacje sieci web w tej samej grupie zasobów, z `Api` sufiksu w nazwie.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="c9d1f-167">Jeśli wyświetlany jest widok grupy zasobów, pojawi się także z bazą danych SQL i serwera, plan usługi aplikacji i tymczasowej miejsc aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="c9d1f-168">Przechodzenie przez różne zasoby i porównaj je z  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json aby zobaczyć, jak są konfigurowane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-168">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="c9d1f-169">Zdefiniowano aplikacji produkcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-169">You have set up the production app.</span></span>  <span data-ttu-id="c9d1f-170">Teraz załóżmy Załóżmy, że nie możesz odbierać opinię, że użyteczność jest niska dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span></span> <span data-ttu-id="c9d1f-171">Zdecydować zbadać.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-171">So you decide to investigate.</span></span> <span data-ttu-id="c9d1f-172">Zamierzasz Instrumentacja aplikacji pozwalają opinii.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-172">You're going to instrument your app to give you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="c9d1f-173">Zbadaj: Instrumentacja aplikację klienta dla monitorowania metryki</span><span class="sxs-lookup"><span data-stu-id="c9d1f-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="c9d1f-174">Otwórz  *&lt;repository_root >*\src\MultiChannelToDo.sln w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="c9d1f-175">Przywróć wszystkie pakiety Nuget, klikając prawym przyciskiem myszy rozwiązanie > **Zarządzaj pakietami NuGet dla rozwiązania** > **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="c9d1f-176">Kliknij prawym przyciskiem myszy **MultiChannelToDo.Web** > **Dodaj Telemetrię usługi Application Insights** > **Konfigurowanie ustawień** > Zmień grupę zasobów do ToDoApp*&lt;your_suffix >* > **Dodaj usługę Application Insights do projektu**.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
4. <span data-ttu-id="c9d1f-177">W portalu Azure, otwórz blok dla **MultiChannelToDo.Web** zasobów szczegółowe informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="c9d1f-178">Następnie w **kondycji aplikacji** część, kliknij przycisk **Dowiedz się, jak zbierać dane ładowania stron przeglądarki** > skopiować kod.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="c9d1f-179">Dodaj skopiowany kod Instrumentacji JS do  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml tuż przed zamknięciem `<heading>` tagu.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-179">Add the copied JS instrumentation code to *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span></span> <span data-ttu-id="c9d1f-180">Musi on zawierać klucz Instrumentacji unikatowy zasób szczegółowe informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-180">It should contain the unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="c9d1f-181">Wysyłanie zdarzeń niestandardowych do usługi Application Insights dla myszy kliknięć przez dodanie poniższego kodu do dolnej części treści:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="c9d1f-182">Ta Wstawka kodu JavaScript wysyła do usługi Application Insights zdarzenie niestandardowe, za każdym razem, gdy użytkownik kliknie w dowolnym miejscu w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span></span>
7. <span data-ttu-id="c9d1f-183">W powłoce Git Zatwierdź i Wypchnij zmiany do rozwidlenia w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-183">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="c9d1f-184">Następnie odczekaj klientów odświeżyć przeglądarkę.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-184">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="c9d1f-185">Zamień zmiany wdrożonej aplikacji w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-185">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="c9d1f-186">. \swap — nazwa ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c9d1f-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="c9d1f-187">Przejdź do zasobu usługi Application Insights, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-187">Browse to the Application Insights resource that you configured.</span></span> <span data-ttu-id="c9d1f-188">Niestandardowe zdarzenia kliknięcia.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="c9d1f-189">Jeśli nie widzisz metryki dla niestandardowych zdarzeń, poczekaj kilka minut i kliknij przycisk **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="c9d1f-190">Załóżmy, że zostanie wyświetlony wykres, takich jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="c9d1f-191">I poniżej siatki zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-191">And the event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="c9d1f-192">Zgodnie z ToDoApp kod aplikacji **przycisk** zdarzenia odpowiada przycisk przesyłania i **dane wejściowe** zdarzenie odnosi się do pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span></span> <span data-ttu-id="c9d1f-193">Do tej pory rzeczy sensu.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-193">So far, things make sense.</span></span> <span data-ttu-id="c9d1f-194">Jednak prawdopodobnie jest dobrym ilość kliknięcia i bardzo kilku kliknięć na zadaniach do wykonania ( **LI** zdarzeń).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span></span>

<span data-ttu-id="c9d1f-195">Na podstawie tych formularza należy Twojej hipotezę, że niektórych użytkowników występują pomylić, która część interfejsu użytkownika nie jest aktywne i to, że kursor jest wstawiony do zaznaczonego tekstu, gdy znajduje się na elementy listy i ich ikony.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="c9d1f-196">Może to być contrived przykład.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-196">This might be a contrived example.</span></span> <span data-ttu-id="c9d1f-197">Niemniej jednak użytkownik chce wprowadzić ulepszenia do aplikacji, a następnie wykonaj flighting wdrożenia do dostawać opinie użyteczności klientów na żywo.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="c9d1f-198">Instrumentacja dla monitorowania metryki aplikacji serwera</span><span class="sxs-lookup"><span data-stu-id="c9d1f-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="c9d1f-199">Jest to tangens, ponieważ scenariusz przedstawiona w tym samouczku dotyczy tylko aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span></span> <span data-ttu-id="c9d1f-200">Jednak aby informacje były kompletne skonfigurujesz aplikacji po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-200">However, for completeness you will set up the server-side app.</span></span>

1. <span data-ttu-id="c9d1f-201">Kliknij prawym przyciskiem myszy **MultiChannelToDo** > **Dodaj Telemetrię usługi Application Insights** > **Konfigurowanie ustawień** > Zmień grupę zasobów do ToDoApp*&lt;your_suffix >* > **Dodaj usługę Application Insights do projektu**.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
2. <span data-ttu-id="c9d1f-202">W powłoce Git Zatwierdź i Wypchnij zmiany do rozwidlenia w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-202">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="c9d1f-203">Następnie odczekaj klientów odświeżyć przeglądarkę.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-203">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="c9d1f-204">Zamień zmiany wdrożonej aplikacji w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-204">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="c9d1f-205">. \swap — nazwa ToDoApp < your_suffix ></span><span class="sxs-lookup"><span data-stu-id="c9d1f-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="c9d1f-206">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a><span data-ttu-id="c9d1f-207">Zbadaj: Dodawanie tagów specyficzne dla miejsca do Twojej metryk aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-207">Investigate: Add slot-specific tags to your client app metrics</span></span>
<span data-ttu-id="c9d1f-208">W tej sekcji skonfigurujesz miejsc wdrożenia różnych, aby wysłać dane telemetryczne specyficzne dla miejsca do tego samego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span></span> <span data-ttu-id="c9d1f-209">W ten sposób można łatwo zobaczyć efekt zmian aplikacji można porównać dane telemetryczne między ruchu z różnych miejsc (środowisk wdrażania).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span></span> <span data-ttu-id="c9d1f-210">W tym samym czasie ruchu produkcyjnym można oddzielić od pozostałych dzięki czemu można kontynuować do monitorowania aplikacji produkcyjnych zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span></span>

<span data-ttu-id="c9d1f-211">Ponieważ w przypadku zbierania danych na zachowanie klienta będzie [dodać inicjatora telemetrii w kodzie JavaScript](../application-insights/app-insights-api-filtering-sampling.md) w index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="c9d1f-212">Jeśli chcesz przetestować wydajności po stronie serwera, na przykład, również należy podobnie w kodzie serwera (zobacz [aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="c9d1f-213">Najpierw należy dodać kodu bewteen dwa `//` komentarze poniżej w języku JavaScript zablokować ten zostanie dodany do `<heading>` tagu wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="c9d1f-214">Powoduje, że ten kod inicjatora `appInsights` obiekt, aby dodać właściwość niestandardowa o nazwie `Environment` na każdą wysyłania danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span></span>
2. <span data-ttu-id="c9d1f-215">Następnie dodaj tej właściwości niestandardowej jako [gniazdo ustawienie](web-sites-staged-publishing.md#AboutConfiguration) dla aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="c9d1f-216">Aby to zrobić, uruchom następujące polecenia w sesji programu Git powłoki.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-216">To do this, run the following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="c9d1f-217">Plik Web.config w projekcie już definiuje `environment` ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-217">The Web.config in your project already defines the `environment` app setting.</span></span> <span data-ttu-id="c9d1f-218">To ustawienie, gdy należy przetestować aplikację lokalnie, Twoje metryki zostanie oznaczone z `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="c9d1f-219">Jednak gdy Wypchnij zmiany do platformy Azure, Azure znajduje i używa `environment` aplikacji zamiast tego ustawienia w konfiguracji aplikacji sieci web, a Twoje metryki zostaną oznaczone tagiem `Production`.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="c9d1f-220">Zatwierdź i Wypchnij zmiany kodu do rozwidlenia w witrynie GitHub, a następnie odczekaj dla użytkowników, aby używali nowych aplikacji (trzeba odświeżyć przeglądarkę).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="c9d1f-221">Trwa około 15 minut nową właściwość wyświetlani w szczegółowe dane aplikacji `MultiChannelToDo.Web` zasobów.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. <span data-ttu-id="c9d1f-222">Teraz, przejdź do **niestandardowe zdarzenia** ponownie bloku i odfiltrować metryki `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span></span> <span data-ttu-id="c9d1f-223">Teraz można wyświetlić wszystkich nowych zdarzeń niestandardowych w gnieździe produkcyjnym z tego filtru.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-223">You should now be able to see all the new custom events in the production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="c9d1f-224">Kliknij przycisk **ulubione** przycisk, aby zapisać bieżące ustawienia Eksploratora metryk podobną **zdarzenia niestandardowe: produkcji**.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span></span> <span data-ttu-id="c9d1f-225">Możesz łatwo przełączać się między tego widoku oraz widoku miejsca wdrożenia później.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="c9d1f-226">W celu wykonania analizy jeszcze bardziej skuteczne, należy wziąć pod uwagę [integrowanie zasobu usługi Application Insights z usługi Power BI](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a><span data-ttu-id="c9d1f-227">Dodaj znaczniki specyficzne dla miejsca do Twojej metryki aplikacji serwera</span><span class="sxs-lookup"><span data-stu-id="c9d1f-227">Add slot-specific tags to your server app metrics</span></span>
<span data-ttu-id="c9d1f-228">Ponownie aby informacje były kompletne skonfigurujesz aplikacji po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-228">Again, for completeness you will set up the server-side app.</span></span> <span data-ttu-id="c9d1f-229">W przeciwieństwie do aplikacji klienckiej, która jest instrumentowany w języku JavaScript tagi miejsca specyficzne dla aplikacji serwera są instrumentowane przy użyciu kodu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="c9d1f-230">Otwórz  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="c9d1f-231">Dodaj blok kodu poniżej, bezpośrednio przed zamykający nawias klamrowy w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-231">Add the code block below, just before the closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="c9d1f-232">Popraw błędy rozpoznawania nazw, dodając `using` instrukcje poniżej na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="c9d1f-233">Dodaj poniższy kod do początku `Application_Start()` metody:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-233">Add the code below to the beginning of the `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="c9d1f-234">Zatwierdź i Wypchnij zmiany kodu do rozwidlenia w witrynie GitHub, a następnie odczekaj dla użytkowników, aby używali nowych aplikacji (trzeba odświeżyć przeglądarkę).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="c9d1f-235">Trwa około 15 minut nową właściwość wyświetlani w szczegółowe dane aplikacji `MultiChannelToDo` zasobów.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="c9d1f-236">Aktualizacja: Konfigurowanie gałąź w wersji beta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="c9d1f-237">Otwórz  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json i Znajdź `appsettings` zasobów (Wyszukaj `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="c9d1f-238">Istnieją 4 z nich, po jednej dla każdego miejsca.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="c9d1f-239">Dla każdego `appsettings` zasobów, Dodaj `"environment": "[parameters('slotName')]"` ustawienia aplikacji na końcu `properties` tablicy.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span></span> <span data-ttu-id="c9d1f-240">Nie zapomnij o zakończenie poprzedniego wiersza przecinkami.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-240">Don't forget to end the previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="c9d1f-241">Dodany `environment` ustawienia aplikacji na wszystkich miejsc w szablonie.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-241">You have just added the `environment` app setting to all the slots in the template.</span></span>
3. <span data-ttu-id="c9d1f-242">W tym samym pliku, Znajdź `slotconfignames` zasobów (Wyszukaj `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="c9d1f-243">Istnieją 2 z nich, po jednej dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="c9d1f-244">Dla każdego `slotconfignames` zasobów, Dodaj `"environment"` na końcu `appSettingNames` tablicy.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span></span> <span data-ttu-id="c9d1f-245">Nie zapomnij o zakończenie poprzedniego wiersza przecinkami.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-245">Don't forget to end the previous line with a comma.</span></span>

    <span data-ttu-id="c9d1f-246">Zostały wprowadzone `environment` aplikacji ustawienie USB na jej miejsce wdrożenia odpowiednich dla obydwu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="c9d1f-247">W sesji programu Git powłoki uruchom następujące polecenia z tej samej grupy zasobów sufiks używany przed.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="c9d1f-248">Po wyświetleniu monitu podaj tego samego SQL poświadczenia bazy danych jako przed.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-248">When prompted, specify the same SQL database credentials as before.</span></span> <span data-ttu-id="c9d1f-249">Następnie po otrzymaniu monitu, aby zaktualizować grupy zasobów, wpisz `Y`, następnie `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="c9d1f-250">Po zakończeniu skryptu, wszystkich zasobów w grupie zasobów oryginalnego zostaną zachowane, ale nowe miejsce o nazwie "beta" jest tworzony w nim z taką samą konfigurację jak miejsca "Tymczasowe", który został utworzony na początku.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c9d1f-251">Ta metoda tworzenia wdrożenia w różnych środowiskach różni się od metody w [Agile software development z usługi aplikacji Azure](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="c9d1f-252">W tym miejscu Utwórz środowisk wdrażania z miejsc wdrożenia, w której jako utworzono środowisk wdrażania z grupami zasobów.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="c9d1f-253">Zarządzanie środowisk wdrażania z grupami zasobów pozwala na przechowywanie w środowisku produkcyjnym off-limits dla deweloperów, ale nie jest łatwe testowanie w środowisku produkcyjnym, co można zrobić w prosty sposób z miejsc.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="c9d1f-254">W razie potrzeby, można również utworzyć aplikację alfa, uruchamiając</span><span class="sxs-lookup"><span data-stu-id="c9d1f-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="c9d1f-255">W tym samouczku użytkownik będzie tylko nadal używać aplikacji w wersji beta.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-to-the-beta-app"></a><span data-ttu-id="c9d1f-256">Aktualizacja: Wypychanie aktualizacji aplikacji w wersji beta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-256">Update: Push your updates to the beta app</span></span>
<span data-ttu-id="c9d1f-257">Powrót do aplikacji, który chcesz zwiększyć.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-257">Back to your app that you want to improve.</span></span>

1. <span data-ttu-id="c9d1f-258">Upewnij się, że możesz teraz w gałęzi w wersji beta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="c9d1f-259">W  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, Znajdź `<li>` tagu i Dodaj `style="cursor:pointer"` atrybutu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="c9d1f-260">Zatwierdzanie i wypychania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-260">commit and push to Azure.</span></span>
4. <span data-ttu-id="c9d1f-261">Sprawdź, czy zmiany jest teraz widoczne w gnieździe w wersji beta przechodząc do http://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="c9d1f-262">Jeśli nie widzisz jeszcze zmiany, Odśwież przeglądarkę, aby uzyskać nowy kod javascript.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="c9d1f-263">Teraz, gdy masz zmiany w gnieździe w wersji beta można przystąpić do wykonania flighting wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span></span>

## <a name="validate-route-traffic-to-the-beta-app"></a><span data-ttu-id="c9d1f-264">Sprawdź poprawność: Kierować ruchem do aplikacji w wersji beta</span><span class="sxs-lookup"><span data-stu-id="c9d1f-264">Validate: Route traffic to the beta app</span></span>
<span data-ttu-id="c9d1f-265">W tej sekcji będzie kierować ruchem do aplikacji w wersji beta.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-265">In this section, you will route traffic to the beta app.</span></span> <span data-ttu-id="c9d1f-266">For sake of przejrzystości demonstracyjnych możesz zacząć trasy znaczna część ruchu użytkowników do niego.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span></span> <span data-ttu-id="c9d1f-267">W rzeczywistości ilość ruchu sieciowego, które chcesz rozesłać zależy od konkretnej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span></span> <span data-ttu-id="c9d1f-268">Na przykład jeśli witryna jest na dużą skalę Microsoft.com, następnie konieczne może mniej niż jeden procent całkowitej ruchu w celu uzyskania przydatnych danych.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span></span>

1. <span data-ttu-id="c9d1f-269">W sesji Git powłoki, uruchom następujące polecenia, aby kierować połowy ruchu produkcji do gniazda, w wersji beta:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="c9d1f-270">`ReroutePercentage=50` Właściwość określa, że 50% ruchu produkcyjnego będą kierowane do adresu URL aplikacji w wersji beta (określonego przez `ActionHostName` właściwości).</span><span class="sxs-lookup"><span data-stu-id="c9d1f-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span></span>
2. <span data-ttu-id="c9d1f-271">Teraz przejdź do http://ToDoApp*&lt;your_suffix >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="c9d1f-272">50% ruchu teraz powinno nastąpić przekierowanie do gniazda, w wersji beta.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-272">50% of the traffic should now be redirected to the beta slot.</span></span>
3. <span data-ttu-id="c9d1f-273">W zasobu usługi Application Insights, filtrować metryki przez środowisko = "beta".</span><span class="sxs-lookup"><span data-stu-id="c9d1f-273">In your Application Insights resource, filter the metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="c9d1f-274">Jeśli zapiszesz ten widok filtrowany jako ulubiony innego, można łatwo Przerzuć widoków Eksploratora metryk między produkcyjnego i widoków w wersji beta.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="c9d1f-275">Załóżmy, że w usłudze Application Insights Zobacz podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-275">Suppose in Application Insights you see something similar to the following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="c9d1f-276">Nie tylko jest to wskazującą, że istnieje wiele więcej kliknięć na `<li>` tagi, ale wydaje się skoków kliknięć na `<li>` tagów.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="c9d1f-277">Następnie stwierdzić, że osoby odkryć nowe `<li>` znaczniki są aktywne i są teraz wyczyszczenie wszystkich ich wcześniej wykonać zadania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span></span>

<span data-ttu-id="c9d1f-278">Na podstawie danych flighting wdrożenia, możesz zdecydować, że Twój nowy interfejs użytkownika jest gotowa do produkcji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="c9d1f-279">Przejdź na żywo: Przenieś nowy kod do środowiska produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="c9d1f-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="c9d1f-280">Teraz możesz przenieść aktualizacji do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-280">You're now ready to move your update to production.</span></span> <span data-ttu-id="c9d1f-281">Co to jest doskonałym rozwiązaniem jest teraz wiesz, że aktualizacja została już sprawdzona *przed* zostanie przypisany do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span></span> <span data-ttu-id="c9d1f-282">Dlatego teraz możesz mogą bezpiecznie wdrażać go.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="c9d1f-283">Ponieważ wprowadzono aktualizacji do aplikacji klienckiej AngularJS, sprawdzić poprawności tylko kod po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span></span> <span data-ttu-id="c9d1f-284">Jeśli masz zamiar dokonać zmian w aplikacji interfejsu API sieci Web zaplecza, można zweryfikować zmiany podobnie i łatwe.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="c9d1f-285">W powłoce Git należy usunąć regułę routingu ruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-285">In Git Shell, remove the traffic routing rule by running the following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="c9d1f-286">Uruchom polecenia Git:</span><span class="sxs-lookup"><span data-stu-id="c9d1f-286">Run the Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="c9d1f-287">Poczekaj kilka minut, aż nowy kod do wdrożenia dla miejsca przemieszczania, a następnie uruchom http://ToDoApp*&lt;your_suffix >*-staging.azurewebsites.net, aby sprawdzić, czy nowa aktualizacja jest przygotowaniu miejsca, w miejsce wystawiania.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span></span> <span data-ttu-id="c9d1f-288">Należy pamiętać, że Twoje rozwidlenia głównej gałęzi jest połączony z miejsca przemieszczania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span></span>
4. <span data-ttu-id="c9d1f-289">Teraz Zamień miejsce wystawiania w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="c9d1f-289">Now, swap the staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="c9d1f-290">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c9d1f-290">Summary</span></span>
<span data-ttu-id="c9d1f-291">Usługa aplikacji Azure ułatwia dla małych — do średnich firm do testowania ich aplikacji dostępnych dla klienta w środowisku produkcyjnym, coś tradycyjnie wykonanej w dużych przedsiębiorstw.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="c9d1f-292">Mamy nadzieję, że w tym samouczku przyznał Ci wiedzy potrzebne ze sobą usługi aplikacji i usługi Application Insights flighting wdrażania, a także innych scenariuszy testów w środowisku produkcyjnym w sieci world DevOps.</span><span class="sxs-lookup"><span data-stu-id="c9d1f-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="c9d1f-293">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="c9d1f-293">More resources</span></span>
* [<span data-ttu-id="c9d1f-294">Programowanie zwinne oprogramowania z usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="c9d1f-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="c9d1f-295">Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="c9d1f-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="c9d1f-296">Wdrażanie złożonych aplikacji przewidywalnego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c9d1f-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="c9d1f-297">Tworzenie szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c9d1f-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="c9d1f-298">JSONLint — moduł sprawdzania poprawności JSON</span><span class="sxs-lookup"><span data-stu-id="c9d1f-298">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="c9d1f-299">Rozgałęzianie Git — podstawowe rozgałęzianie i scalanie</span><span class="sxs-lookup"><span data-stu-id="c9d1f-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="c9d1f-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9d1f-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="c9d1f-301">Witryna typu Wiki Kudu projektu</span><span class="sxs-lookup"><span data-stu-id="c9d1f-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
