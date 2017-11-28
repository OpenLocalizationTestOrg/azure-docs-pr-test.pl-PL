---
title: 'Samouczek: metodyka DevOps w witrynie Azure Portal | Microsoft Docs'
description: "Informacje o różnych przepływach pracy metodyki DevOps w witrynie Azure Portal."
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
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="45965-103">Samouczek: metodyka DevOps w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="45965-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="45965-104">Platforma Azure zawiera wiele elastycznych przepływów pracy metodyki DevOps.</span><span class="sxs-lookup"><span data-stu-id="45965-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="45965-105">Niniejszy samouczek zawiera informacje na temat możliwości witryny Azure Portal, które pozwalają opracowywać, testować, wdrażać i monitorować uruchomione aplikacje oraz zarządzać nimi, a także rozwiązywać problemy z nimi związane.</span><span class="sxs-lookup"><span data-stu-id="45965-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="45965-106">W tym samouczku omówiono następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="45965-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="45965-107">Tworzenie aplikacji sieci Web i włączanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="45965-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="45965-108">Tworzenie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="45965-108">Develop and test an app</span></span>
3. <span data-ttu-id="45965-109">Monitorowanie aplikacji i rozwiązywanie problemów z nią związanych</span><span class="sxs-lookup"><span data-stu-id="45965-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="45965-110">Ogólne zadania zarządzania aplikacją</span><span class="sxs-lookup"><span data-stu-id="45965-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="45965-111">Tworzenie aplikacji sieci Web i włączanie ciągłego wdrażania</span><span class="sxs-lookup"><span data-stu-id="45965-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="45965-112">Aplikacja sieci Web zostanie utworzona za pomocą usługi [Azure App Service](https://azure.microsoft.com/services/app-service/), która będzie używana w pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="45965-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="45965-113">Na początku zostanie włączone ciągłe wdrażanie z repozytorium kodu źródłowego do uruchomionego środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="45965-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="45965-114">Zaloguj się do witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45965-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="45965-115">Wybierz kolejno pozycje **App Services** &gt; **ikona Dodaj**, a następnie wprowadź nazwę, wybierz subskrypcję i utwórz nową grupę zasobów, która posłuży jako kontener dla usługi.</span><span class="sxs-lookup"><span data-stu-id="45965-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="45965-116">Grupy zasobów umożliwiają zarządzanie różnymi aspektami rozwiązania, takimi jak rozliczenia, wdrożenia i monitorowanie, w ramach pojedynczej grupy za pośrednictwem usługi [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45965-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="45965-118">Po chwil zostanie utworzona usługa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="45965-119">Poświęć kilka minut na zapoznanie się z opcjami menu dla tej usługi, które są dostępne w portalu.</span><span class="sxs-lookup"><span data-stu-id="45965-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="45965-121">Kliknij adres URL.</span><span class="sxs-lookup"><span data-stu-id="45965-121">Click the URL.</span></span> <span data-ttu-id="45965-122">Zwróć uwagę na to, że możesz wybierać spośród wielu dostępnych narzędzi i repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="45965-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="45965-123">Możesz również używać swoich ulubionych języków i platform, na przykład .NET, Java i Ruby.</span><span class="sxs-lookup"><span data-stu-id="45965-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="45965-125">Dzięki witrynie Azure Portal włączenie procesu ciągłego wdrażania jest łatwe i wymaga wykonania tylko kilku prostych czynności.</span><span class="sxs-lookup"><span data-stu-id="45965-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="45965-126">W witrynie Azure Portal wybierz ikonę nowo utworzonej usługi aplikacji, a następnie wybierz pozycję Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="45965-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="45965-128">W bloku, który zostanie otwarty po prawej stronie, przewiń do sekcji publikowania.</span><span class="sxs-lookup"><span data-stu-id="45965-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="45965-130">Teraz musisz skonfigurować ustawienia umożliwiające włączenie ciągłego wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="45965-131">Kliknij kolejno pozycje Źródło wdrożenia i Wybierz źródło.</span><span class="sxs-lookup"><span data-stu-id="45965-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="45965-132">Zwróć uwagę na różne opcje dotyczące źródeł repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45965-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="45965-134">W tym przykładzie należy wybrać serwis GitHub.</span><span class="sxs-lookup"><span data-stu-id="45965-134">For this example choose GitHub.</span></span> <span data-ttu-id="45965-135">Możesz też wybrać inne repozytorium i skonfigurować poświadczenia autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="45965-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="45965-137">Po skonfigurowaniu autoryzacji w repozytorium możesz wybrać projekt i gałąź, które chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="45965-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="45965-138">Poniżej znajduje się kilka fikcyjnych przykładów.</span><span class="sxs-lookup"><span data-stu-id="45965-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="45965-140">Po wybraniu projektu i gałęzi kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="45965-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="45965-141">Zaczną pojawiać się powiadomienia dotyczące wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="45965-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="45965-143">Wróć do witryny GitHub i wyświetl element webhook, który został utworzony w celu integracji repozytorium kontroli źródła z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="45965-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="45965-144">Witryna Azure Portal umożliwia integrację z usługą GitHub przez wykonanie zaledwie kilku prostych czynności.</span><span class="sxs-lookup"><span data-stu-id="45965-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="45965-146">Aby pokazać ciągłe wdrażanie, szybko dodamy zawartość do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45965-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="45965-147">Prostym przykładem może być dodanie przykładowego pliku tekstowego do repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="45965-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="45965-148">Z usługą App Service możesz używać platform .NET, Ruby, Python lub innych typów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="45965-149">Do wybranego repozytorium możesz dodać plik tekstowy albo aplikację platformy ASP.NET MVC, Java lub Ruby.</span><span class="sxs-lookup"><span data-stu-id="45965-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="45965-151">Po zatwierdzeniu zmian w repozytorium w obszarze powiadomień portalu zobaczysz informacje dotyczące inicjowania nowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="45965-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="45965-152">Jeśli zmiany nie pojawią się szybko, kliknij opcję synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="45965-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="45965-154">Jeśli spróbujesz teraz załadować stronę usługi aplikacji, może zostać wyświetlony komunikat o błędzie 403.</span><span class="sxs-lookup"><span data-stu-id="45965-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="45965-155">Dzieje się tak, ponieważ nie określono typowej konfiguracji domyślnego dokumentu dla strony, takiego jak plik index.htm lub default.html.</span><span class="sxs-lookup"><span data-stu-id="45965-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="45965-156">Ten problem można szybko rozwiązać za pomocą narzędzi dostępnych w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45965-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="45965-157">W witrynie Azure Portal wybierz kolejno pozycje Ustawienia &gt; Ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="45965-159">Zostanie otwarty blok ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-159">A blade opens for application settings.</span></span> <span data-ttu-id="45965-160">Wprowadź nazwę strony — „Strona_przykładowa.html” — i kliknij pozycję Zapisz.</span><span class="sxs-lookup"><span data-stu-id="45965-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="45965-161">Poświęć kilka minut na zapoznanie się z innymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="45965-161">Take a few minutes to explore the other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="45965-163">Możesz odświeżyć adres URL w przeglądarce, aby mieć pewność, że oczekiwane zmiany są widoczne.</span><span class="sxs-lookup"><span data-stu-id="45965-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="45965-164">W tym przykładzie na stronie jest wyświetlany krótki tekst.</span><span class="sxs-lookup"><span data-stu-id="45965-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="45965-165">Każda kolejna zmiana w repozytorium spowoduje automatyczne włączenie nowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="45965-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="45965-167">Włączanie ciągłego wdrażania w witrynie Azure Portal jest proste.</span><span class="sxs-lookup"><span data-stu-id="45965-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="45965-168">Możesz również tworzyć bardziej złożone potoki tworzenia wersji i korzystać z wielu innych rozwiązań, takich jak systemy automatycznej kompilacji i zarządzania wersjami, umożliwiających wdrażanie na platformie Azure istniejących systemów kontroli źródła i ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="45965-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="45965-169">Tworzenie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="45965-169">Develop and test an app</span></span>
<span data-ttu-id="45965-170">Teraz w bazie kodu zostaną wprowadzone pewne zmiany, które zostaną szybko wdrożone.</span><span class="sxs-lookup"><span data-stu-id="45965-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="45965-171">Zostanie również skonfigurowane testowanie wydajności aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="45965-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="45965-172">W witrynie Azure Portal w okienku nawigacji wybierz pozycję App Services i znajdź swoją usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="45965-174">Kliknij pozycję Narzędzia.</span><span class="sxs-lookup"><span data-stu-id="45965-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="45965-176">W obszarze Narzędzia przejdź do kategorii Tworzenie.</span><span class="sxs-lookup"><span data-stu-id="45965-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="45965-177">Znajduje się w niej kilka przydatnych narzędzi, które pozwalają pracować z aplikacjami bez opuszczania witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45965-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="45965-178">Kliknij pozycję Konsola.</span><span class="sxs-lookup"><span data-stu-id="45965-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="45965-180">Za pomocą okna konsoli możesz przesyłać aktywne polecenia do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="45965-181">Wpisz polecenie dir i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="45965-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="45965-182">Pamiętaj o tym, że polecenia wymagające podwyższonego poziomu uprawnień nie będą działać.</span><span class="sxs-lookup"><span data-stu-id="45965-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="45965-184">Wróć do kategorii Tworzenie i wybierz pozycję Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="45965-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="45965-185">Uwaga: usługa Visual Studio Online nosi teraz nazwę Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="45965-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="45965-187">Włącz opcję edytowania aplikacji w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="45965-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="45965-189">Dla aplikacji zostanie zainstalowane rozszerzenie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="45965-189">A web extension installs for your app.</span></span> <span data-ttu-id="45965-190">Za pomocą rozszerzeń można szybko i łatwo dodawać funkcje do aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="45965-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="45965-191">Poniższy zrzut ekranu przedstawia niektóre inne typy dostępnych rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="45965-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="45965-193">Po zainstalowaniu rozszerzenia Visual Studio Online kliknij pozycję Przejdź.</span><span class="sxs-lookup"><span data-stu-id="45965-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="45965-195">Zostanie otwarta karta przeglądarki zawierająca środowisko IDE tworzenia.</span><span class="sxs-lookup"><span data-stu-id="45965-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="45965-196">Zwróć uwagę na to, że poniższy interfejs jest dostępny za pomocą przeglądarki Chrome.</span><span class="sxs-lookup"><span data-stu-id="45965-196">Notice the experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="45965-198">Dostępnych jest kilka działań, takich jak edytowanie plików, dodawanie plików i folderów oraz pobieranie zawartości z działającej witryny.</span><span class="sxs-lookup"><span data-stu-id="45965-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="45965-199">Wprowadź drobną zmianę w pliku Strona_przykładowa.html.</span><span class="sxs-lookup"><span data-stu-id="45965-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="45965-201">Po chwili zmiany zostaną automatycznie zapisane</span><span class="sxs-lookup"><span data-stu-id="45965-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="45965-202">i będą widoczne na stronie.</span><span class="sxs-lookup"><span data-stu-id="45965-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="45965-203">Warto pamiętać, że takie wprowadzanie zmian „na żywo” nie jest zalecane w środowiskach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="45965-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="45965-204">Jednak za pomocą narzędzi można bardzo łatwo wprowadzić szybkie zmiany w środowiskach tworzenia i testowania.</span><span class="sxs-lookup"><span data-stu-id="45965-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="45965-207">Wróć do bloku narzędzi i kliknij pozycję Test wydajności w obszarze Tworzenie.</span><span class="sxs-lookup"><span data-stu-id="45965-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="45965-209">Musisz skonfigurować konto usług Team Services.</span><span class="sxs-lookup"><span data-stu-id="45965-209">You need to set a team services account.</span></span> <span data-ttu-id="45965-210">Więcej informacji można znaleźć w artykule [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) (Tworzenie konta usług Team Services).</span><span class="sxs-lookup"><span data-stu-id="45965-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="45965-211">Kliknij pozycję Nowy, aby utworzyć test wydajności.</span><span class="sxs-lookup"><span data-stu-id="45965-211">Click on New to create a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="45965-213">Skonfiguruj odpowiednie wartości i kliknij przycisk Uruchom test u dołu okna dialogowego, aby zainicjować test wydajności.</span><span class="sxs-lookup"><span data-stu-id="45965-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="45965-216">Po uruchomieniu testu możesz zacząć monitorować stan.</span><span class="sxs-lookup"><span data-stu-id="45965-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="45965-218">Gdy test zostanie zakończony, kliknij wynik, aby wyświetlić więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="45965-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="45965-220">Przebieg testowy utworzony w tym przykładzie nie jest obszerny, dlatego zestaw danych przeznaczonych do analizy jest ograniczony. Możesz jednak wyświetlić różne metryki oraz ponownie uruchomić test z poziomu tego widoku.</span><span class="sxs-lookup"><span data-stu-id="45965-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="45965-221">Witryna Azure Portal umożliwia łatwe tworzenie, przeprowadzanie i analizowanie testów wydajności aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="45965-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="45965-222">Na poniższych zrzutach ekranu przedstawiono dane dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="45965-222">The screenshots below display the performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="45965-226">Monitorowanie aplikacji i rozwiązywanie problemów z nią związanych</span><span class="sxs-lookup"><span data-stu-id="45965-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="45965-227">Platforma Azure udostępnia wiele możliwości monitorowania uruchomionych aplikacji i rozwiązywania problemów z nimi związanych.</span><span class="sxs-lookup"><span data-stu-id="45965-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="45965-228">W witrynie Azure Portal przejdź do utworzonej aplikacji sieci Web i wybierz pozycję Narzędzia.</span><span class="sxs-lookup"><span data-stu-id="45965-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="45965-230">W obszarze Rozwiązywanie problemów są dostępne różne narzędzia służące do rozwiązywania potencjalnych problemów z uruchomioną aplikacją.</span><span class="sxs-lookup"><span data-stu-id="45965-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="45965-231">Można wykonywać takie czynności, jak na przykład monitorowanie bieżącego ruchu HTTP, włączanie samonaprawiania czy wyświetlanie dzienników.</span><span class="sxs-lookup"><span data-stu-id="45965-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="45965-233">Wybierz pozycję Metryki witryn, aby szybko uzyskać wgląd w wybrane kody HTTP.</span><span class="sxs-lookup"><span data-stu-id="45965-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="45965-235">Wybierz pozycję Diagnostyka jako usługa.</span><span class="sxs-lookup"><span data-stu-id="45965-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="45965-236">Wybierz typ aplikacji, a następnie wybierz przycisk Uruchom.</span><span class="sxs-lookup"><span data-stu-id="45965-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="45965-238">Rozpocznie się zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="45965-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="45965-240">Wybranie odpowiedniego dziennika umożliwia diagnozowanie potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="45965-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="45965-241">Jeśli włączysz rejestrowanie, zobaczysz wszystkie dostępne opcje danych, na przykład dzienniki protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="45965-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="45965-243">Po kliknięciu pliku zrzutu pamięci możesz pobrać raport analizy DebugDiag, który ułatwia znalezienie potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="45965-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="45965-245">Aby wyświetlić więcej danych, musisz włączyć dodatkowe opcje rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="45965-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="45965-246">W witrynie Azure Portal przejdź do aplikacji sieci Web i wybierz pozycję Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="45965-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="45965-248">Przewiń w dół do kategorii funkcji i wybierz pozycję Dzienniki diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="45965-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="45965-250">Zostaną wyświetlone różne opcje rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="45965-250">Notice the various options for logging.</span></span> <span data-ttu-id="45965-251">Włącz opcję Rejestrowanie serwera sieci Web i kliknij przycisk Zapisz.</span><span class="sxs-lookup"><span data-stu-id="45965-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="45965-253">Wróć do obszaru narzędzi aplikacji i wybierz pozycję Diagnostyka jako usługa, a następnie kliknij przycisk Uruchom, aby ponownie uruchomić zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="45965-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="45965-255">Po włączeniu opcji rejestrowania HTTP są widoczne dane rejestrowane w dziennikach HTTP.</span><span class="sxs-lookup"><span data-stu-id="45965-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="45965-257">Po kliknięciu pliku dziennika HTML zostanie wyświetlony rozbudowany raport obsługiwany w przeglądarce, który zapewnia bardziej szczegółowy wgląd w dane.</span><span class="sxs-lookup"><span data-stu-id="45965-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="45965-259">Wróć do obszaru narzędzi aplikacji w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45965-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="45965-260">Przewiń do sekcji Narzędzia i wybierz pozycję Eksplorator procesów.</span><span class="sxs-lookup"><span data-stu-id="45965-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="45965-262">Eksplorator procesów pozwala wyświetlić szczegółowe informacje o uruchomionych procesach.</span><span class="sxs-lookup"><span data-stu-id="45965-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="45965-263">Jak pokazano na poniższych zrzutach ekranu, można przechodzić do szczegółów procesów, a nawet kończyć je — wszystko z poziomu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45965-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="45965-266">Wróć do bloku Ustawienia po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="45965-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="45965-267">Kliknij pozycję Nowe żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="45965-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="45965-269">W bloku po prawej stronie możesz wprowadzić dane kontaktowe i szczegółowe informacje o problemach, a nawet przekazać dane diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="45965-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="45965-270">Witryna Azure Portal umożliwia płynną i bezproblemową współpracę z pomocą techniczną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="45965-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="45965-273">Witryna Azure Portal zapewnia komfort korzystania z zaawansowanych i dobrze znanych narzędzi, które ułatwiają monitorowanie uruchomionych aplikacji i rozwiązywanie problemów z nimi.</span><span class="sxs-lookup"><span data-stu-id="45965-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="45965-274">Ponadto możesz szybko podejmować odpowiednie działania i wykonywać takie zadania, jak odtwarzanie procesów, włączanie i wyłączanie zbierania różnych danych, a także integracja z profesjonalną pomocą techniczną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="45965-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="45965-275">Ogólne zarządzanie aplikacjami</span><span class="sxs-lookup"><span data-stu-id="45965-275">General Application Management</span></span>
<span data-ttu-id="45965-276">Zarządzanie aplikacjami często obejmuje szeroką gamę działań, takich jak konfigurowanie strategii tworzenia kopii zapasowych, wdrażanie dostawców tożsamości i zarządzanie nimi oraz konfigurowanie kontroli dostępu opartej na rolach.</span><span class="sxs-lookup"><span data-stu-id="45965-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="45965-277">Podobnie jak w przypadku innych funkcji metodyki DevOps, platforma Azure pozwala zintegrować te zadania bezpośrednio z portalem.</span><span class="sxs-lookup"><span data-stu-id="45965-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="45965-278">Aby zapobiec utracie danych aplikacji sieci Web, musisz skonfigurować kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="45965-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="45965-279">Przejdź do obszaru Ustawienia swojej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="45965-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="45965-281">W bloku po prawej stronie przewiń w dół do kategorii Funkcje.</span><span class="sxs-lookup"><span data-stu-id="45965-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="45965-283">Wybierz pozycję Kopie zapasowe. Z prawej strony pojawi się odpowiedni blok.</span><span class="sxs-lookup"><span data-stu-id="45965-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="45965-285">Kliknij pozycję Konfiguruj i wybierz konto magazynu w bloku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="45965-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="45965-287">Następnie utwórz i wybierz kontener magazynu, w którym będą przechowywane kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="45965-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="45965-288">Kliknij pozycję Utwórz w dolnej części bloku</span><span class="sxs-lookup"><span data-stu-id="45965-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="45965-289">i wybierz kontener.</span><span class="sxs-lookup"><span data-stu-id="45965-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="45965-291">Po wybraniu kontenera możesz skonfigurować harmonogramy tworzenia kopii zapasowych baz danych.</span><span class="sxs-lookup"><span data-stu-id="45965-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="45965-292">W tym scenariuszu kliknij ikonę Zapisz.</span><span class="sxs-lookup"><span data-stu-id="45965-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="45965-294">Po zapisaniu wróć do bloku Kopie zapasowe po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="45965-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="45965-295">Kliknij pozycję Utwórz kopię zapasową teraz, aby utworzyć kopię zapasową aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="45965-297">Po chwili zostanie utworzona kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="45965-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="45965-298">Zwróć uwagę na opcję Przywróć teraz, widoczną na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="45965-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="45965-300">Kliknij pozycję Przywróć teraz i zapoznaj się z opcjami wyświetlonymi w bloku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="45965-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="45965-301">W razie potrzeby możesz wybrać odpowiednią kopię zapasową i łatwo przywrócić dane do wcześniejszego stanu.</span><span class="sxs-lookup"><span data-stu-id="45965-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="45965-302">Za pomocą witryny Azure Portal udało się łatwo wdrożyć prostą strategię odzyskiwania awaryjnego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="45965-304">Wróć do bloku Ustawienia po lewej stronie i wybierz pozycję Uwierzytelnianie/autoryzacja w obszarze Funkcje.</span><span class="sxs-lookup"><span data-stu-id="45965-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="45965-306">W bloku po prawej stronie wybierz pozycję Uwierzytelnianie usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="45965-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="45965-307">Zwróć uwagę na możliwość skonfigurowania wielu popularnych dostawców.</span><span class="sxs-lookup"><span data-stu-id="45965-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="45965-309">Wybierz dostawcę i zapoznaj się z opcjami dotyczącymi zakresu.</span><span class="sxs-lookup"><span data-stu-id="45965-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="45965-310">Po wprowadzeniu identyfikatora i klucza tajnego aplikacji możesz szybko włączyć uwierzytelnianie w aplikacji za pomocą serwisu Facebook.</span><span class="sxs-lookup"><span data-stu-id="45965-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="45965-311">Witryna Azure Portal udostępnia uwierzytelnianie w aplikacjach jako gotowe rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="45965-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="45965-313">Wróć do bloku Ustawienia i wybierz pozycję Użytkownicy w kategorii Zarządzanie zasobami.</span><span class="sxs-lookup"><span data-stu-id="45965-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="45965-315">W bloku po prawej stronie zapoznaj się z różnymi opcjami dodawania ról i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="45965-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="45965-316">Witryna Azure Portal pozwala łatwo korzystać z kontroli dostępu opartej na rolach w celu sterowania dostępem do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45965-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="45965-318">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="45965-318">Summary</span></span>
<span data-ttu-id="45965-319">W tym samouczku przedstawiono niektóre możliwości udostępniane przez platformę Azure: szybkie włączanie ciągłego wdrażania aplikacji sieci Web, wykonywanie różnych działań w zakresie tworzenia i testowania aplikacji, monitorowanie uruchomionej aplikacji i rozwiązywanie problemów z nią związanych oraz zarządzanie kluczowymi strategiami, takimi jak odzyskiwanie awaryjne, zarządzanie tożsamościami i kontrola dostępu oparta na rolach.</span><span class="sxs-lookup"><span data-stu-id="45965-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="45965-320">Platforma Azure umożliwia integrację tych przepływów pracy metodyki DevOps, pozwalając użytkownikom pracować wydajnie dzięki możliwości korzystania z informacji kontekstowych dotyczących wykonywanego zadania.</span><span class="sxs-lookup"><span data-stu-id="45965-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45965-321">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="45965-321">Next steps</span></span>
* <span data-ttu-id="45965-322">Usługa Azure Resource Manager pełni ważną rolę w procesie włączania metodyki DevOps na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="45965-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="45965-323">Aby dowiedzieć się więcej, zobacz artykuł [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45965-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="45965-324">Aby dowiedzieć się więcej o wdrażaniu w usłudze Azure App Service, zobacz artykuł [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md) (Wdrażanie aplikacji w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="45965-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
