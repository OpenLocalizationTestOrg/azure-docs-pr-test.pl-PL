---
title: "Wdrażanie lokalnej usługi Git w usłudze Azure App Service"
description: "Dowiedz się, jak włączyć lokalne wdrożenie systemu Git w usłudze Azure App Service."
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
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="fab84-103">Wdrażanie lokalnej usługi Git w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fab84-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="fab84-104">W tym samouczku przedstawiono sposób wdrażania aplikacji [usłudze Azure App Service] z repozytorium Git na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="fab84-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="fab84-105">Usługi aplikacji obsługuje tej metody z **Git lokalnego** opcji wdrażania w [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="fab84-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="fab84-106">Wiele poleceń Git opisane w tym artykule są wykonywane automatycznie podczas tworzenia aplikacji usługi App Service przy użyciu [interfejsu wiersza polecenia platformy Azure] zgodnie z opisem [tutaj](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fab84-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fab84-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fab84-107">Prerequisites</span></span>
<span data-ttu-id="fab84-108">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fab84-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="fab84-109">Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-109">Git.</span></span> <span data-ttu-id="fab84-110">Możesz pobrać binarne instalacji [tutaj](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="fab84-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="fab84-111">Podstawową wiedzę na temat narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="fab84-112">Konto platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fab84-112">A Microsoft Azure account.</span></span> <span data-ttu-id="fab84-113">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="fab84-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="fab84-114">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą wersję początkową aplikacji w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="fab84-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="fab84-115">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="fab84-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="fab84-116"><a name="Step1"></a>Krok 1: Tworzenie lokalnego repozytorium</span><span class="sxs-lookup"><span data-stu-id="fab84-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="fab84-117">Wykonaj następujące zadania w celu utworzenia nowego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="fab84-118">Uruchom narzędzie wiersza polecenia, takich jak **GitBash** (system Windows) lub **Bash** (powłoka systemu Unix).</span><span class="sxs-lookup"><span data-stu-id="fab84-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="fab84-119">OS X w systemach dostęp można uzyskać wiersza polecenia, za pomocą **Terminal** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fab84-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="fab84-120">Przejdź do katalogu, gdzie znajduje się będzie zawartość do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fab84-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="fab84-121">Aby zainicjować nowego repozytorium Git, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fab84-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="fab84-122"><a name="Step2"></a>Krok 2: Zatwierdź zawartości</span><span class="sxs-lookup"><span data-stu-id="fab84-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="fab84-123">Usługa aplikacji obsługuje aplikacje utworzone w różnych językach programowania.</span><span class="sxs-lookup"><span data-stu-id="fab84-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="fab84-124">Jeśli repozytorium zawiera już Pomiń zawartości tego punktu, a następnie przejdź do punktu 2 poniżej.</span><span class="sxs-lookup"><span data-stu-id="fab84-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="fab84-125">Jeśli repozytorium nie zawiera zawartości po prostu umieścić plik statyczny .html w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fab84-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="fab84-126">Za pomocą edytora tekstu, Utwórz nowy plik o nazwie **index.html** w katalogu głównym repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="fab84-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="fab84-127">Dodaj poniższy tekst jako zawartość dla index.html plik i zapisać go: *Git Witaj!*</span><span class="sxs-lookup"><span data-stu-id="fab84-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="fab84-128">W wierszu polecenia Sprawdź, czy w katalogu głównym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="fab84-129">Następnie użyj następującego polecenia, aby dodać pliki do repozytorium:</span><span class="sxs-lookup"><span data-stu-id="fab84-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="fab84-130">Następnie Zatwierdź zmiany do repozytorium przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fab84-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="fab84-131"><a name="Step3"></a>Krok 3: Włącz repozytorium aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="fab84-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="fab84-132">Wykonaj poniższe kroki, aby włączyć repozytorium Git aplikację usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fab84-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="fab84-133">Zaloguj się do [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="fab84-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="fab84-134">W bloku aplikację usługi aplikacji, kliknij przycisk **Ustawienia > źródło wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="fab84-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="fab84-135">Kliknij przycisk **wybierz źródło**, następnie kliknij przycisk **lokalnego repozytorium Git**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fab84-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Lokalne repozytorium Git](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="fab84-137">Jeśli jest to pierwszy ustawienia czasu zapasowej repozytorium na platformie Azure, musisz utworzyć poświadczenia logowania dla niego.</span><span class="sxs-lookup"><span data-stu-id="fab84-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="fab84-138">Użyje ich do zalogowania się do platformy Azure zmiany repozytorium i wypychania z lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="fab84-139">W bloku aplikacji kliknij **Ustawienia > poświadczenia wdrożenia**, skonfiguruj wdrożenia, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="fab84-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="fab84-140">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="fab84-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="fab84-141"><a name="Step4"></a>Krok 4: Wdrażanie projektu</span><span class="sxs-lookup"><span data-stu-id="fab84-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="fab84-142">Wykonaj następujące kroki, aby publikowanie aplikacji w usłudze App Service przy użyciu usługi Git lokalnego.</span><span class="sxs-lookup"><span data-stu-id="fab84-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="fab84-143">W bloku aplikacji w portalu Azure, kliknij **Ustawienia > właściwości** dla **adres URL Git**.</span><span class="sxs-lookup"><span data-stu-id="fab84-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="fab84-144">**Adres URL Git** jest zdalnego odwołania do wdrożenia z lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fab84-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="fab84-145">W poniższych krokach użyjesz tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fab84-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="fab84-146">Przy użyciu wiersza polecenia, sprawdź, czy w katalogu lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="fab84-147">Użyj `git remote` można dodać odwołania zdalnego na liście **adres URL Git** z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="fab84-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="fab84-148">Polecenie będzie wyglądać podobnie do poniższej:</span><span class="sxs-lookup"><span data-stu-id="fab84-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="fab84-149">**Zdalnego** polecenie dodaje nazwany odwołanie do repozytorium zdalnego.</span><span class="sxs-lookup"><span data-stu-id="fab84-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="fab84-150">W tym przykładzie powoduje utworzenie odwołania do repozytorium aplikacji sieci web o nazwie "azure".</span><span class="sxs-lookup"><span data-stu-id="fab84-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="fab84-151">Wypychania zawartości do usługi App Service przy użyciu nowego **azure** zdalnego utworzony.</span><span class="sxs-lookup"><span data-stu-id="fab84-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="fab84-152">Wróć do aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fab84-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="fab84-153">Wpis dziennika z najnowszych wypychania powinien być wyświetlany w **wdrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="fab84-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="fab84-154">Kliknij przycisk **Przeglądaj** na górze bloku aplikacji, aby sprawdzić zawartość została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="fab84-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="fab84-155"><a name="Step5"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="fab84-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="fab84-156">Poniżej znajdują się błędy lub problemy najczęściej występujące podczas przy użyciu narzędzia Git, aby opublikować aplikację usługi aplikacji na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="fab84-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="fab84-157">**Objaw**: nie można dostępu [siteURL]: nie można nawiązać połączenia z [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="fab84-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="fab84-158">**Przyczyna**: ten błąd może wystąpić, jeśli aplikacja nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fab84-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="fab84-159">**Rozdzielczość**: uruchomić aplikację w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fab84-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="fab84-160">Wdrożenie systemu Git nie będzie działać, chyba że aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fab84-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="fab84-161">**Objaw**: nie można rozpoznać nazwy hosta "hosta"</span><span class="sxs-lookup"><span data-stu-id="fab84-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="fab84-162">**Przyczyna**: ten błąd może wystąpić, jeśli adres wprowadzonej podczas tworzenia zdalnego "azure" jest niepoprawne.</span><span class="sxs-lookup"><span data-stu-id="fab84-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="fab84-163">**Rozdzielczość**: Użyj `git remote -v` polecenie, aby wyświetlić listę wszystkich element zdalny, wraz z powiązanego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fab84-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="fab84-164">Sprawdź, czy adres URL "platformy azure" zdalnego jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="fab84-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="fab84-165">W razie potrzeby usuń i ponownie utwórz ten zdalnego przy użyciu poprawny adres URL.</span><span class="sxs-lookup"><span data-stu-id="fab84-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="fab84-166">**Objaw**: nie odwołania do wspólnego i brak określone; żadne czynności.</span><span class="sxs-lookup"><span data-stu-id="fab84-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="fab84-167">Być może należy określić gałąź, takich jak 'master'.</span><span class="sxs-lookup"><span data-stu-id="fab84-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="fab84-168">**Przyczyna**: ten błąd może wystąpić, jeśli nie określisz gałąź podczas wykonywania git operacji wypychania, a nie ustawiono wartość push.default używana przez Git.</span><span class="sxs-lookup"><span data-stu-id="fab84-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="fab84-169">**Rozdzielczość**: wykonaj wypychania ponownie wykonać operację, określając gałęzi głównej.</span><span class="sxs-lookup"><span data-stu-id="fab84-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="fab84-170">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="fab84-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="fab84-171">**Objaw**: nie pasuje do żadnego src refspec [nazwa_gałęzi].</span><span class="sxs-lookup"><span data-stu-id="fab84-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="fab84-172">**Przyczyna**: ten błąd może wystąpić przy próbie wypychania do gałęzi innej niż główny "Azure" zdalnego.</span><span class="sxs-lookup"><span data-stu-id="fab84-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="fab84-173">**Rozdzielczość**: wykonaj wypychania ponownie wykonać operację, określając gałęzi głównej.</span><span class="sxs-lookup"><span data-stu-id="fab84-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="fab84-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="fab84-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="fab84-175">**Objaw**: RPC nie powiodło się; spowodować = 22, kod HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="fab84-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="fab84-176">**Przyczyna**: ten błąd może wystąpić przy próbie push repozytorium git dużych za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fab84-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="fab84-177">**Rozdzielczość**: Zmień konfigurację git na komputer lokalny, aby powiększyć postBuffer</span><span class="sxs-lookup"><span data-stu-id="fab84-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="fab84-178">**Objaw**: Błąd — zmiany do repozytorium zdalnego, ale aplikacja sieci web nie zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="fab84-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="fab84-179">**Przyczyna**: ten błąd może wystąpić w przypadku wdrażania aplikacji Node.js zawierający plik package.json, który określa dodatkowe wymagane moduły.</span><span class="sxs-lookup"><span data-stu-id="fab84-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="fab84-180">**Rozdzielczość**: dodatkowych komunikatów zawierających 'npm błąd!'</span><span class="sxs-lookup"><span data-stu-id="fab84-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="fab84-181">powinny być rejestrowane przed ten błąd i może zapewnić dodatkowy kontekst błędu.</span><span class="sxs-lookup"><span data-stu-id="fab84-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="fab84-182">Znane są następujące przyczyny tego błędu i odpowiednie "npm błąd!'</span><span class="sxs-lookup"><span data-stu-id="fab84-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="fab84-183">Komunikat:</span><span class="sxs-lookup"><span data-stu-id="fab84-183">message:</span></span>

* <span data-ttu-id="fab84-184">**Plik package.json źle sformułowane**: błąd npm!</span><span class="sxs-lookup"><span data-stu-id="fab84-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="fab84-185">Nie można odczytać zależności.</span><span class="sxs-lookup"><span data-stu-id="fab84-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="fab84-186">**Natywny moduł, który nie ma binarne dystrybucji dla systemu Windows**:</span><span class="sxs-lookup"><span data-stu-id="fab84-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="fab84-187">Błąd npm!</span><span class="sxs-lookup"><span data-stu-id="fab84-187">npm ERR!</span></span> <span data-ttu-id="fab84-188">\`cmd "/ c" "gyp węzła Odbuduj"\` nie powiodło się z 1</span><span class="sxs-lookup"><span data-stu-id="fab84-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="fab84-189">LUB</span><span class="sxs-lookup"><span data-stu-id="fab84-189">OR</span></span>
  * <span data-ttu-id="fab84-190">Błąd npm!</span><span class="sxs-lookup"><span data-stu-id="fab84-190">npm ERR!</span></span> <span data-ttu-id="fab84-191">[modulename@version] preinstalować: \`upewnij || gmake\`</span><span class="sxs-lookup"><span data-stu-id="fab84-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fab84-192">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fab84-192">Additional Resources</span></span>
* [<span data-ttu-id="fab84-193">Dokumentacja usługi Git</span><span class="sxs-lookup"><span data-stu-id="fab84-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="fab84-194">Dokumentacja Kudu projektu</span><span class="sxs-lookup"><span data-stu-id="fab84-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="fab84-195">Wdrożenie ciągłej w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fab84-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="fab84-196">Jak korzystać z programu PowerShell dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fab84-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="fab84-197">Sposób użycia interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fab84-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="fab84-198">[usłudze Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="fab84-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="fab84-199">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="fab84-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="fab84-200">[interfejsu wiersza polecenia platformy Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="fab84-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
