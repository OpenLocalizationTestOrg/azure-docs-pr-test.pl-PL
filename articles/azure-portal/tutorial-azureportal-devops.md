---
title: 'Samouczek: DevOps z hello portalu Azure | Dokumentacja firmy Microsoft'
description: "Dowiedz się hello różnych przepływy DevOps hello portalu Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="0ef1a-103">Samouczek: DevOps z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ef1a-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="0ef1a-104">Witaj platformy Azure jest pełny elastyczne DevOps przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="0ef1a-105">Z tego samouczka dowiesz się, jak tooleverage możliwości hello hello toodevelop portalu Azure, testów, wdrażania, rozwiązywanie problemów z, monitorowania i zarządzania uruchomionych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="0ef1a-106">Ten samouczek koncentruje się na następujących hello:</span><span class="sxs-lookup"><span data-stu-id="0ef1a-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="0ef1a-107">Tworzenie aplikacji sieci Web i włączanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="0ef1a-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="0ef1a-108">Tworzenie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0ef1a-108">Develop and test an app</span></span>
3. <span data-ttu-id="0ef1a-109">Monitorowanie aplikacji i rozwiązywanie problemów z nią związanych</span><span class="sxs-lookup"><span data-stu-id="0ef1a-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="0ef1a-110">Ogólne zadania zarządzania aplikacją</span><span class="sxs-lookup"><span data-stu-id="0ef1a-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="0ef1a-111">Tworzenie aplikacji sieci Web i włączanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="0ef1a-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="0ef1a-112">Tworzenie aplikacji sieci Web z [usłudze Azure App Service](https://azure.microsoft.com/services/app-service/), który zostanie użyty w hello pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="0ef1a-113">Na początku zostanie włączone ciągłe wdrażanie z repozytorium kodu źródłowego do uruchomionego środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="0ef1a-114">Zaloguj się do hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ef1a-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="0ef1a-115">Wybierz **usługi aplikacji** &gt; **ikonę Dodaj** i wprowadź nazwę, wybierz subskrypcję i Utwórz nowe tooserve grupy zasobów jako kontener hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="0ef1a-116">Grupy zasobów umożliwiają toomanage różnych aspektów hello rozwiązania, takich jak rozliczenia, wdrożenia i monitorowania wszystkich jako pojedynczej grupy za pomocą [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ef1a-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="0ef1a-118">Po chwil zostanie utworzona usługa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="0ef1a-119">W portalu hello, należy wykonać kilka minut tooexplore hello różnych opcji menu hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="0ef1a-121">Kliknij przycisk hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-121">Click hello URL.</span></span> <span data-ttu-id="0ef1a-122">Zwróć uwagę, hello różnych dostępnych narzędzi i repozytoriów sposobów.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="0ef1a-123">Można również użyć hello języków i struktur wybranego w tym .NET, Java i Ruby.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="0ef1a-125">Witaj portalu Azure sprawia, że ciągłe wdrażanie prosty proces obejmuje kilka prostych kroków.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="0ef1a-126">W portalu Azure hello wybierz ustawienia z hello ikonę usługi aplikacji hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="0ef1a-128">W bloku hello otwartym na powitania prawo przewiń toohello publikowania sekcji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="0ef1a-130">Następnie należy skonfigurować niektóre ustawienia tooenable ciągłe wdrażanie dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="0ef1a-131">Kliknij kolejno pozycje Źródło wdrożenia i Wybierz źródło.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="0ef1a-132">Zwróć uwagę, hello różnych opcji dla źródeł repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="0ef1a-134">W tym przykładzie należy wybrać serwis GitHub.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-134">For this example choose GitHub.</span></span> <span data-ttu-id="0ef1a-135">Opcjonalnie wybierz repozytorium hello wybranych przez użytkownika i skonfigurować poświadczenia autoryzacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="0ef1a-137">Po autoryzacji tooyour repozytorium można wybrać projekt i chcesz toodeploy gałęzi.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="0ef1a-138">Poniżej znajduje się kilka fikcyjnych przykładów.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="0ef1a-140">Po wybraniu projektu i gałęzi kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="0ef1a-141">Należy rozpocząć toosee powiadomienia o wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="0ef1a-143">Przejdź wstecz tooGitHub toosee hello webhook utworzonego repozytorium kontroli źródła hello toointegrate przy użyciu usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="0ef1a-144">Witaj portalu Azure umożliwia integrację z usługi GitHub z kilku prostych krokach.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="0ef1a-146">ciągłe wdrażanie toodemonstrate szybko dodać niektóre toohello zawartości repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="0ef1a-147">Na przykład prosty Dodaj repozytorium GitHub tooa plik przykładowy tekst.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="0ef1a-148">Jesteś toouse wolnego .NET, Ruby, Python lub inny rodzaj aplikacji z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="0ef1a-149">Możesz wolnego tooadd pliku tekstowego, ASP.NET MVC, Java lub Ruby repozytorium toohello aplikacji wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="0ef1a-151">Po zatwierdzania zmian tooyour repozytorium, zostanie wyświetlony nowy zainicjowanie wdrożenia w obszarze powiadomień portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="0ef1a-152">Kliknij przycisk synchronizacji, jeśli nie szybko ma zmiany po zatwierdzania tooyour repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="0ef1a-154">W tym momencie Jeśli spróbuj i załadowania strony hello usługi aplikacji hello, może zostać wyświetlony błąd 403.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="0ef1a-155">W tym przykładzie jest ponieważ nie istnieje żadne ustawienia dokumentu typowy domyślny dla strony hello, takie jak plików, takich jak index.htm lub default.html.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="0ef1a-156">Można szybko rozwiązać ten z hello narzędzi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="0ef1a-157">W portalu Azure hello wybierz ustawienia &gt; ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="0ef1a-159">Zostanie otwarty blok ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-159">A blade opens for application settings.</span></span> <span data-ttu-id="0ef1a-160">Wprowadź nazwę hello strony powitania "SamplePage.html", a następnie kliknij przycisk Zapisz.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="0ef1a-161">Potrwać kilka minut tooexplore hello innych ustawień.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="0ef1a-163">Opcjonalnie można odświeżyć tooensure adres URL z przeglądarki, zobacz hello oczekiwano zmiany.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="0ef1a-164">W takim przypadku jest prosty tekst teraz wypełnianie hello strony.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="0ef1a-165">Każdego repozytorium toohello dodatkowe zmiany spowoduje automatyczne nowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="0ef1a-167">Włączanie ciągłego wdrażania z hello Azure Portal to środowisko łatwe.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="0ef1a-168">Można również utworzyć bardziej złożoną potoki wersji i użyć innych technik istniejących kontroli źródła i ciągłej integracji tooAzure toodeploy systemów, takich jak wykorzystaniu automatycznych kompilacji oraz wersji systemów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="0ef1a-169">Tworzenie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0ef1a-169">Develop and test an app</span></span>
<span data-ttu-id="0ef1a-170">Następnie wprowadzić kilka zmian kodu toohello podstawowej i szybko wdrożyć tych zmian.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="0ef1a-171">Zostanie również skonfigurować niektóre testowanie wydajnościowe na potrzeby aplikacji sieci Web hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="0ef1a-172">W portalu Azure hello wybrać aplikacji usługi z okienka nawigacji hello, a następnie zlokalizuj usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="0ef1a-174">Kliknij pozycję Narzędzia.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="0ef1a-176">Zwróć uwagę, hello opracowanie kategorię w menu Narzędzia.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="0ef1a-177">Istnieje kilka przydatne narzędzi, w tym miejscu pozwalających nam toowork z aplikacji bez opuszczania hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="0ef1a-178">Kliknij pozycję Konsola.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="0ef1a-180">W oknie konsoli hello możesz wykonywać poleceń na żywo dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="0ef1a-181">Typ hello dir polecenie i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="0ef1a-182">Pamiętaj o tym, że polecenia wymagające podwyższonego poziomu uprawnień nie będą działać.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="0ef1a-184">Powrót toohello opracowanie kategorii, a następnie wybierz pozycję Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="0ef1a-185">Uwaga: usługa Visual Studio Online nosi teraz nazwę Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="0ef1a-187">Przełącz na powitania proces edycji w przeglądarce dla twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="0ef1a-189">Dla aplikacji zostanie zainstalowane rozszerzenie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-189">A web extension installs for your app.</span></span> <span data-ttu-id="0ef1a-190">Rozszerzenia szybkie i łatwe do dodawania tooapps funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="0ef1a-191">Zwróć uwagę, niektóre hello inne typy rozszerzeń dostępnych hello poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="0ef1a-193">Po zainstalowaniu hello rozszerzenia usługi Visual Studio Online, kliknij Go.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="0ef1a-195">Przeglądarki karcie której występuje programowanie IDE bezpośrednio w przeglądarce hello zostanie otwarta.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="0ef1a-196">Środowisko hello Uwaga poniżej znajduje się w Chrome.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-196">Notice hello experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="0ef1a-198">Można wykonać kilka czynności, takie jak edytować pliki, dodać pliki i foldery i pobieranie zawartości z lokacji na żywo hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="0ef1a-199">Udostępnij plik SamplePage.html toohello szybkie edycji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="0ef1a-201">Za chwilę zmiany hello są automatycznie zapisywane.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="0ef1a-202">Jeśli przejdziesz toohello tylnej strony widać hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="0ef1a-203">Warto pamiętać, że takie wprowadzanie zmian „na żywo” nie jest zalecane w środowiskach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="0ef1a-204">Jednak narzędzi hello go łatwo toomake szybko wprowadź zmiany dla deweloperów i przetestować środowisk.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="0ef1a-207">Powrót toohello narzędzia bloku i kategorii opracowanie powitania kliknij testu wydajności.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="0ef1a-209">Należy tooset konta usług team.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-209">You need tooset a team services account.</span></span> <span data-ttu-id="0ef1a-210">Więcej informacji można znaleźć w artykule [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) (Tworzenie konta usług Team Services).</span><span class="sxs-lookup"><span data-stu-id="0ef1a-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="0ef1a-211">Kliknij nowy toocreate testów wydajności sieci.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-211">Click on New toocreate a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="0ef1a-213">Skonfiguruj hello różne wartości, a następnie kliknij przycisk Uruchom Test u dołu hello tooinitiate dialogu hello testów wydajności sieci.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="0ef1a-216">Gdy hello test zacznie działać, można monitorować stan hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="0ef1a-218">Po zakończeniu testu hello, klikając hello wynik zawiera więcej szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="0ef1a-220">W tym przykładzie utworzono małych testy, więc istnieje tooanalyze ograniczoną ilość danych, ale można zobaczyć różnych metryk oraz jak ponowne uruchomienie testu z tego widoku.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="0ef1a-221">Hello Azure Portal sprawia, że tworzenie, wykonywanie i analizowanie łatwy testów wydajności sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="0ef1a-222">Poniższe zrzuty ekranu Hello przedstawia hello dane wydajności.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-222">hello screenshots below display hello performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="0ef1a-226">Monitorowanie aplikacji i rozwiązywanie problemów z nią związanych</span><span class="sxs-lookup"><span data-stu-id="0ef1a-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="0ef1a-227">Platforma Azure udostępnia wiele możliwości monitorowania uruchomionych aplikacji i rozwiązywania problemów z nimi związanych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="0ef1a-228">W hello Azure Portal dla aplikacji sieci Web wybierz narzędzia.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="0ef1a-230">Rozwiązywanie problemów z kategorii hello Zwróć uwagę hello różnych opcji przy użyciu narzędzia tootroubleshoot potencjalnych problemów z uruchomionej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="0ef1a-231">Można wykonywać takie czynności, jak na przykład monitorowanie bieżącego ruchu HTTP, włączanie samonaprawiania czy wyświetlanie dzienników.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="0ef1a-233">Wybierz widok niektórych kodów HTTP get tooquickly metryki lokacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="0ef1a-235">Wybierz pozycję Diagnostyka jako usługa.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="0ef1a-236">Wybierz typ aplikacji, a następnie wybierz przycisk Uruchom.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="0ef1a-238">Rozpocznie się zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="0ef1a-240">Możesz wybrać odpowiedni dziennik hello toodiagnose potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="0ef1a-241">Należy toosee rejestrowania tooenable wszystkie dostępne dane hello opcje, takie jak dzienniki HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="0ef1a-243">Klikając plik zrzutu pamięci hello można pobrać i przeanalizować DebugDiag toohelp raportu analizy odnaleźć potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="0ef1a-245">tooview większej ilości danych, należy tooenable dodatkowe rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="0ef1a-246">Hello portalu Azure przejdź do aplikacji sieci Web toohello i wybierz polecenie Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="0ef1a-248">Przewiń w dół toohello funkcje kategorii, a następnie wybierz pozycję dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="0ef1a-250">Zwróć uwagę, hello różne opcje rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-250">Notice hello various options for logging.</span></span> <span data-ttu-id="0ef1a-251">Włącz opcję Rejestrowanie serwera sieci Web i kliknij przycisk Zapisz.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="0ef1a-253">Powrót toohello obszaru narzędzia dla aplikacji hello i wybierz diagnostyki jako usługi, a następnie kliknij przycisk Uruchom toorerun hello danych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="0ef1a-255">Ustawienie rejestrowania hello HTTP jest włączone, pojawi się dane zbierane w dziennikach HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="0ef1a-257">Klikając hello HTML pliku dziennika, należy utworzyć rozbudowany raport przeglądarki w celu dokładniejszego zbadania.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="0ef1a-259">Powrót toohello narzędzia części hello Azure Portal dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="0ef1a-260">Przewiń do sekcji narzędzia toohello, a następnie wybierz Eksploratora procesów.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="0ef1a-262">Eksplorator procesów pozwala wyświetlić szczegółowe informacje o uruchomionych procesach.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="0ef1a-263">Uwagi poniżej można przejść do procesów i nawet kill wszystkie procesy hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="0ef1a-266">Powrót bloku ustawienia toohello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="0ef1a-267">Kliknij pozycję Nowe żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="0ef1a-269">W bloku hello na powitania prawo wypełniania szczegółowe informacje o problemach hello, wprowadź informacje kontaktowe, a nawet przekazywanie danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="0ef1a-270">Hello Azure Portal umożliwia współpracę z pomocy technicznej firmy Microsoft nie zakłóca pracy.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="0ef1a-273">Hello Azure Portal zapewnia wydajne i znanych narzędzi monitor toohelp środowiska i rozwiązywanie problemów z naszych uruchamianie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="0ef1a-274">Ma również akcji tootake mogli szybko przez wykonywanie zadań takich jak odtwarzanie procesów, włączanie i wyłączanie różnych zbierania danych i nawet integracji z professional pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="0ef1a-275">Ogólne zarządzanie aplikacjami</span><span class="sxs-lookup"><span data-stu-id="0ef1a-275">General Application Management</span></span>
<span data-ttu-id="0ef1a-276">Jeśli zarządzanie aplikacjami, często konieczne tooperform szerokiej gamy działania, takie jak konfigurowanie strategii tworzenia kopii zapasowych, wdrażanie i zarządzanie dostawców tożsamości i konfigurowania kontroli dostępu opartej na rolach.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="0ef1a-277">Zgodnie z hello inne środowiska DevOps, hello platformy Azure integruje te zadania bezpośrednio w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="0ef1a-278">tooensure są utrzymywanie hello aplikacji sieci Web przed utratą danych należy tooconfigure kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="0ef1a-279">Przejdź toohello obszaru Ustawienia dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="0ef1a-281">W bloku hello na powitania prawo przewiń w dół toohello funkcje kategorii.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="0ef1a-283">Wybierz kopie zapasowe; zostanie otwarty blok na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="0ef1a-285">Kliknij przycisk Konfiguruj, wybierz konto magazynu z bloku hello na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="0ef1a-287">Teraz można tworzyć i wybierz toohold kontenera magazynu kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="0ef1a-288">Kliknij przycisk Utwórz u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="0ef1a-289">Następnie wybierz kontener hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-289">Then select hello container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="0ef1a-291">Po wybraniu opcji kontenera hello, można skonfigurować harmonogramy, a także ustawienia kopii zapasowych baz danych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="0ef1a-292">W tym scenariuszu kliknij hello Zapisz ikony.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-292">For this scenario, click hello save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="0ef1a-294">Po zapisaniu, przewiń blok toohello wstecz po lewej stronie powitania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="0ef1a-295">Kliknij przycisk Utwórz kopię zapasową teraz tooback hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-295">Click Backup Now tooback hello application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="0ef1a-297">Po chwili zostanie utworzona kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="0ef1a-298">Powiadomienie hello Przywróć teraz opcję hello zrzut ekranu poniżej.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="0ef1a-300">Wybierz polecenie Przywróć teraz i sprawdź, czy blok toohello opcje hello na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="0ef1a-301">Możesz wybrać odpowiednie kopii zapasowej i łatwo tooan przywracania wcześniej stanu niezbędne.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="0ef1a-302">Witaj portalu Azure pomógł nam go łatwo uaktywnić strategię odzyskiwania po awarii proste aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="0ef1a-304">Powrót bloku ustawienia toohello powitania po lewej stronie, a w obszarze funkcje, a następnie wybierz uwierzytelniania/autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="0ef1a-306">W bloku hello na powitania prawo wybierz Uwierzytelnianie usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="0ef1a-307">Zwróć uwagę, hello różne opcje, które można skonfigurować z popularnych dostawców.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="0ef1a-309">Wybierz dostawcę hello wybranych przez użytkownika i zwróć uwagę, opcje hello hello zakresu.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="0ef1a-310">Można podać identyfikator aplikacji i klucz tajny aplikacji i szybko włączyć uwierzytelniania serwisu Facebook dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="0ef1a-311">Witaj Azure Portal umożliwia użycie uwierzytelniania, gotowe rozwiązanie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="0ef1a-313">Powrót toohello bloku ustawienia, a następnie wybierz użytkowników w kategorii zarządzanie zasobami hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="0ef1a-315">W bloku hello na powitania prawo Sprawdź hello różnych opcji dodawania ról i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="0ef1a-316">Witaj Azure Portal pozwala łatwo zarządzać RBAC (kontrola dostępu oparta na rolach) dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="0ef1a-318">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0ef1a-318">Summary</span></span>
<span data-ttu-id="0ef1a-319">W tym samouczku przedstawiono niektóre hello zasilania z hello platformy Azure szybko włączając ciągłe wdrażanie dla aplikacji sieci web, wykonywanie różnych programowanie i testowania czynności, monitorowania i rozwiązywania problemów w aktywnej aplikacji i na koniec zarządzania kluczem Strategie odzyskiwania po awarii, tożsamości i kontroli dostępu opartej na rolach.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="0ef1a-320">Witaj platformy Azure umożliwia zintegrowane środowisko dla tych przepływów pracy DevOps oraz można pracować wydajnie pozostając w kontekście dla wykonywanego zadania hello.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ef1a-321">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ef1a-321">Next steps</span></span>
* <span data-ttu-id="0ef1a-322">Usługa Azure Resource Manager jest ważne w przypadku włączania DevOps na powitania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef1a-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="0ef1a-323">więcej odwiedź toolearn [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ef1a-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="0ef1a-324">więcej informacji na temat wdrażania usługi Azure App Service można znaleźć toolearn [wdrażanie tooAzure Twojego aplikację usługi aplikacji](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="0ef1a-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
