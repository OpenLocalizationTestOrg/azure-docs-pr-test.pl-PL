---
title: "aaaLocal wdrożenia Git tooAzure usługi aplikacji"
description: "Dowiedz się, jak tooAzure tooenable do wdrożenia lokalnego Git usługi aplikacji."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="59694-103">Lokalnego wdrożenia Git tooAzure usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="59694-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="59694-104">W tym samouczku przedstawiono sposób toodeploy aplikacji zbyt[usłudze Azure App Service] z repozytorium Git na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="59694-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="59694-105">App Service obsługuje takie podejście z hello **lokalnego Git** opcji wdrażania w hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="59694-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="59694-106">Wiele poleceń Git hello opisane w tym artykule są wykonywane automatycznie podczas tworzenia aplikacji usługi app Service przy użyciu hello [interfejsu wiersza polecenia platformy Azure] zgodnie z opisem [tutaj](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="59694-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59694-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59694-107">Prerequisites</span></span>
<span data-ttu-id="59694-108">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="59694-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="59694-109">Git.</span><span class="sxs-lookup"><span data-stu-id="59694-109">Git.</span></span> <span data-ttu-id="59694-110">Możesz pobrać binarne instalacji hello [tutaj](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="59694-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="59694-111">Podstawową wiedzę na temat narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="59694-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="59694-112">Konto platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="59694-112">A Microsoft Azure account.</span></span> <span data-ttu-id="59694-113">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="59694-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="59694-114">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą wersję początkową aplikacji w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="59694-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="59694-115">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="59694-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="59694-116"><a name="Step1"></a>Krok 1: Tworzenie lokalnego repozytorium</span><span class="sxs-lookup"><span data-stu-id="59694-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="59694-117">Wykonaj następujące zadania toocreate nowego repozytorium Git hello.</span><span class="sxs-lookup"><span data-stu-id="59694-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="59694-118">Uruchom narzędzie wiersza polecenia, takich jak **GitBash** (system Windows) lub **Bash** (powłoka systemu Unix).</span><span class="sxs-lookup"><span data-stu-id="59694-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="59694-119">OS X w systemach hello wiersza polecenia można dostęp za pośrednictwem hello **Terminal** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59694-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="59694-120">Przejdź toohello katalogu, gdy toodeploy zawartości hello jest zlokalizowany.</span><span class="sxs-lookup"><span data-stu-id="59694-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="59694-121">Użyj następującego polecenia tooinitialize nowego repozytorium Git hello:</span><span class="sxs-lookup"><span data-stu-id="59694-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="59694-122"><a name="Step2"></a>Krok 2: Zatwierdź zawartości</span><span class="sxs-lookup"><span data-stu-id="59694-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="59694-123">Usługa aplikacji obsługuje aplikacje utworzone w różnych językach programowania.</span><span class="sxs-lookup"><span data-stu-id="59694-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="59694-124">Jeśli repozytorium już zawiera Pomiń zawartości tego punktu i Przenieś toopoint 2 poniżej.</span><span class="sxs-lookup"><span data-stu-id="59694-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="59694-125">Jeśli repozytorium nie zawiera zawartości po prostu umieścić plik statyczny .html w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="59694-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="59694-126">Za pomocą edytora tekstu, Utwórz nowy plik o nazwie **index.html** hello katalogu głównego repozytorium Git hello</span><span class="sxs-lookup"><span data-stu-id="59694-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="59694-127">Dodaj hello następującego tekstu jako hello index.html hello zawartości pliku i zapisz go: *Git Witaj!*</span><span class="sxs-lookup"><span data-stu-id="59694-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="59694-128">Z wiersza polecenia hello Sprawdź, czy w katalogu głównym hello repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="59694-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="59694-129">Użyj następującego polecenia tooadd pliki tooyour repozytorium hello:</span><span class="sxs-lookup"><span data-stu-id="59694-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="59694-130">Następnie Zatwierdź hello zmiany toohello repozytorium przy użyciu następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="59694-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="59694-131"><a name="Step3"></a>Krok 3: Włącz hello repozytorium aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="59694-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="59694-132">Wykonaj następujące kroki tooenable repozytorium Git aplikację usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="59694-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="59694-133">Zaloguj się za toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="59694-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="59694-134">W bloku aplikację usługi aplikacji, kliknij przycisk **Ustawienia > źródło wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="59694-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="59694-135">Kliknij przycisk **wybierz źródło**, następnie kliknij przycisk **lokalnego repozytorium Git**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="59694-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Lokalne repozytorium Git](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="59694-137">Jeśli jest to pierwszy ustawienia czasu zapasowej repozytorium na platformie Azure, należy toocreate poświadczenia logowania dla niego.</span><span class="sxs-lookup"><span data-stu-id="59694-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="59694-138">Użyjesz ich toolog do hello Azure repozytorium i Wypchnij zmiany z lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="59694-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="59694-139">W bloku aplikacji kliknij **Ustawienia > poświadczenia wdrożenia**, skonfiguruj wdrożenia, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="59694-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="59694-140">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="59694-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="59694-141"><a name="Step4"></a>Krok 4: Wdrażanie projektu</span><span class="sxs-lookup"><span data-stu-id="59694-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="59694-142">Użyj hello następujące kroki toopublish tooApp Twojej aplikacji usługi przy użyciu lokalnego Git.</span><span class="sxs-lookup"><span data-stu-id="59694-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="59694-143">W bloku aplikacji w portalu Azure hello, kliknij przycisk **Ustawienia > właściwości** dla hello **adres URL Git**.</span><span class="sxs-lookup"><span data-stu-id="59694-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="59694-144">**Adres URL Git** jest toofrom toodeploy odwołania zdalnego hello lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="59694-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="59694-145">Ten adres URL będzie używany w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="59694-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="59694-146">Przy użyciu wiersza polecenia hello, sprawdź, czy w katalogu głównym hello lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="59694-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="59694-147">Użyj `git remote` tooadd hello zdalnego odwołania na liście **adres URL Git** z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="59694-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="59694-148">Polecenie będzie wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="59694-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="59694-149">Witaj **zdalnego** polecenie dodaje tooa nazwanego odwołania zdalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="59694-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="59694-150">W tym przykładzie powoduje utworzenie odwołania do repozytorium aplikacji sieci web o nazwie "azure".</span><span class="sxs-lookup"><span data-stu-id="59694-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="59694-151">Push Twojej zawartości tooApp usługi przy użyciu nowego hello **azure** zdalnego utworzony.</span><span class="sxs-lookup"><span data-stu-id="59694-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="59694-152">Przejdź wstecz tooyour aplikacji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59694-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="59694-153">Wpis dziennika z najnowszych wypychania powinien być wyświetlany w hello **wdrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="59694-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="59694-154">Kliknij przycisk hello **Przeglądaj** u góry hello hello tooverify bloku aplikacji hello zawartości została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="59694-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="59694-155"><a name="Step5"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="59694-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="59694-156">dostępne są następujące Hello: błędy lub problemy najczęściej występujące podczas korzystania tooan toopublish Git aplikacji usługi app Service na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="59694-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="59694-157">**Objaw**: nie można tooaccess [siteURL]: nie powiodło się tooconnect zbyt [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="59694-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="59694-158">**Przyczyna**: ten błąd może wystąpić, jeśli aplikacja hello nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="59694-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="59694-159">**Rozdzielczość**: Start aplikacji hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59694-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="59694-160">Wdrożenie systemu Git nie będzie działać, chyba że aplikacja hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="59694-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="59694-161">**Objaw**: nie można rozpoznać nazwy hosta "hosta"</span><span class="sxs-lookup"><span data-stu-id="59694-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="59694-162">**Przyczyna**: ten błąd może wystąpić, jeśli informacje o adresie hello wprowadzona podczas tworzenia powitania "azure" zdalnego jest niepoprawne.</span><span class="sxs-lookup"><span data-stu-id="59694-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="59694-163">**Rozdzielczość**: Użyj hello `git remote -v` polecenia toolist wszystkie element zdalny, wraz z hello skojarzony adres URL.</span><span class="sxs-lookup"><span data-stu-id="59694-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="59694-164">Sprawdź, czy adres URL hello hello "azure" zdalnego jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="59694-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="59694-165">W razie potrzeby usuń i ponownie utwórz tym zdalnego przy użyciu hello Popraw adres URL.</span><span class="sxs-lookup"><span data-stu-id="59694-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="59694-166">**Objaw**: nie odwołania do wspólnego i brak określone; żadne czynności.</span><span class="sxs-lookup"><span data-stu-id="59694-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="59694-167">Być może należy określić gałąź, takich jak 'master'.</span><span class="sxs-lookup"><span data-stu-id="59694-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="59694-168">**Przyczyna**: ten błąd może wystąpić, jeśli nie określić gałąź podczas wykonywania operacji wypychania narzędzia git i są wartości not set hello push.default używane przez Git.</span><span class="sxs-lookup"><span data-stu-id="59694-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="59694-169">**Rozdzielczość**: operacja hello wypychania ponownie, określając hello głównej gałęzi.</span><span class="sxs-lookup"><span data-stu-id="59694-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="59694-170">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="59694-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="59694-171">**Objaw**: nie pasuje do żadnego src refspec [nazwa_gałęzi].</span><span class="sxs-lookup"><span data-stu-id="59694-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="59694-172">**Przyczyna**: ten błąd może wystąpić, jeśli próba toopush tooa gałęzi innej niż główny na powitania "azure" zdalnego.</span><span class="sxs-lookup"><span data-stu-id="59694-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="59694-173">**Rozdzielczość**: operacja hello wypychania ponownie, określając hello głównej gałęzi.</span><span class="sxs-lookup"><span data-stu-id="59694-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="59694-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="59694-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="59694-175">**Objaw**: RPC nie powiodło się; spowodować = 22, kod HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="59694-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="59694-176">**Przyczyna**: ten błąd może wystąpić, jeśli próba toopush repozytorium git dużych za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59694-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="59694-177">**Rozdzielczość**: Konfiguracja git hello zmiany na większy postBuffer hello toomake maszyny lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="59694-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="59694-178">**Objaw**: błąd - repozytorium tooremote zatwierdzone zmiany ale aplikacji sieci web nie zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="59694-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="59694-179">**Przyczyna**: ten błąd może wystąpić w przypadku wdrażania aplikacji Node.js zawierający plik package.json, który określa dodatkowe wymagane moduły.</span><span class="sxs-lookup"><span data-stu-id="59694-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="59694-180">**Rozdzielczość**: dodatkowych komunikatów zawierających 'npm błąd!'</span><span class="sxs-lookup"><span data-stu-id="59694-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="59694-181">powinny być rejestrowane toothis wcześniejszych błędów i może zapewnić dodatkowy kontekst hello awarii.</span><span class="sxs-lookup"><span data-stu-id="59694-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="59694-182">następujący Hello są znane przyczyny tego błędu i hello odpowiedniego "npm błąd!'</span><span class="sxs-lookup"><span data-stu-id="59694-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="59694-183">Komunikat:</span><span class="sxs-lookup"><span data-stu-id="59694-183">message:</span></span>

* <span data-ttu-id="59694-184">**Plik package.json źle sformułowane**: błąd npm!</span><span class="sxs-lookup"><span data-stu-id="59694-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="59694-185">Nie można odczytać zależności.</span><span class="sxs-lookup"><span data-stu-id="59694-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="59694-186">**Natywny moduł, który nie ma binarne dystrybucji dla systemu Windows**:</span><span class="sxs-lookup"><span data-stu-id="59694-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="59694-187">Błąd npm!</span><span class="sxs-lookup"><span data-stu-id="59694-187">npm ERR!</span></span> <span data-ttu-id="59694-188">\`cmd "/ c" "gyp węzła Odbuduj"\` nie powiodło się z 1</span><span class="sxs-lookup"><span data-stu-id="59694-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="59694-189">LUB</span><span class="sxs-lookup"><span data-stu-id="59694-189">OR</span></span>
  * <span data-ttu-id="59694-190">Błąd npm!</span><span class="sxs-lookup"><span data-stu-id="59694-190">npm ERR!</span></span> <span data-ttu-id="59694-191">[modulename@version] preinstalować: \`upewnij || gmake\`</span><span class="sxs-lookup"><span data-stu-id="59694-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59694-192">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="59694-192">Additional Resources</span></span>
* [<span data-ttu-id="59694-193">Dokumentacja usługi Git</span><span class="sxs-lookup"><span data-stu-id="59694-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="59694-194">Dokumentacja Kudu projektu</span><span class="sxs-lookup"><span data-stu-id="59694-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="59694-195">TooAzure ciągłej wdrożenia usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="59694-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="59694-196">Jak toouse programu PowerShell dla usługi Azure</span><span class="sxs-lookup"><span data-stu-id="59694-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="59694-197">Jak toouse hello interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="59694-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[usłudze Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[interfejsu wiersza polecenia platformy Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
