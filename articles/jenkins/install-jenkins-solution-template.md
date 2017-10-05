---
title: Tworzenie serwera Jenkins na platformie Azure
description: "Zainstaluj usługę Jenkins na maszynie wirtualnej z systemem Linux platformy Azure za pomocą szablonu rozwiązania Jenkins i utwórz przykładową aplikację Java."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="80435-103">Tworzenie serwera Jenkins na maszynie wirtualnej z systemem Linux platformy Azure przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="80435-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="80435-104">W tym przewodniku Szybki start pokazano, jak zainstalować usługę [Jenkins](https://jenkins.io) z narzędziami i wtyczkami skonfigurowanymi do współdziałania z platformą Azure na maszynie wirtualnej z systemem Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="80435-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="80435-105">Po zakończeniu uzyskasz działający na platformie Azure serwer Jenkins umożliwiający skompilowanie przykładowej aplikacji Java z usługi [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="80435-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80435-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="80435-106">Prerequisites</span></span>

* <span data-ttu-id="80435-107">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="80435-107">An Azure subscription</span></span>
* <span data-ttu-id="80435-108">Dostęp do powłoki SSH w wierszu polecenia na komputerze (takiej jak powłoka Bash lub [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="80435-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="80435-109">Tworzenie maszyny wirtualnej z usługą Jenkins za pomocą szablonu rozwiązania</span><span class="sxs-lookup"><span data-stu-id="80435-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="80435-110">Otwórz [obraz usługi Jenkins z witryny Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) w przeglądarce internetowej i wybierz pozycję **POBIERZ TERAZ** po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="80435-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="80435-111">Przejrzyj informacje o cenach i wybierz przycisk **Kontynuuj**, a następnie wybierz pozycję **Utwórz**, aby skonfigurować serwer Jenkins w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="80435-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Okno dialogowe witryny Azure Portal](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="80435-113">Na karcie **Konfigurowanie ustawień podstawowych** wypełnij następujące pola:</span><span class="sxs-lookup"><span data-stu-id="80435-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![Konfigurowanie ustawień podstawowych](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="80435-115">W polu **Nazwa** użyj wartości **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="80435-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="80435-116">Wprowadź **nazwę użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="80435-116">Enter a **User name**.</span></span> <span data-ttu-id="80435-117">Nazwa użytkownika musi spełniać [konkretne wymagania](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="80435-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="80435-118">Jako ustawienie **Typ uwierzytelniania** wybierz pozycję **Hasło** i wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="80435-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="80435-119">Hasło musi zawierać co najmniej jedną wielką literę, jedną cyfrę i jeden znak specjalny.</span><span class="sxs-lookup"><span data-stu-id="80435-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="80435-120">W polu **Grupa zasobów** użyj wartości **myJenkinsResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="80435-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="80435-121">Z listy rozwijanej **Lokalizacja** wybierz [region świadczenia usługi Azure](https://azure.microsoft.com/regions/) **Wschodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="80435-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="80435-122">Wybierz przycisk **OK**, aby przejść do karty **Konfigurowanie opcji dodatkowych**. Wprowadź unikatową nazwę domeny do identyfikacji serwera Jenkins i wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="80435-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![Konfigurowanie opcji dodatkowych](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="80435-124">Po pomyślnej weryfikacji ponownie wybierz przycisk **OK** na karcie **Podsumowanie**. Na koniec wybierz pozycję **Zakup**, aby utworzyć maszynę wirtualną z usługą Jenkins.</span><span class="sxs-lookup"><span data-stu-id="80435-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="80435-125">Gdy serwer będzie gotowy, otrzymasz powiadomienie w witrynie Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="80435-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Powiadomienie o tym, że usługa Jenkins jest gotowa](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="80435-127">Nawiązywanie połączenia z usługą Jenkins</span><span class="sxs-lookup"><span data-stu-id="80435-127">Connect to Jenkins</span></span>

<span data-ttu-id="80435-128">Przejdź do maszyny wirtualnej (na przykład http://jenkins2517454.eastus.cloudapp.azure.com/) w przeglądarce internetowej.</span><span class="sxs-lookup"><span data-stu-id="80435-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="80435-129">Konsola usługi Jenkins nie jest dostępna za pośrednictwem niezabezpieczonych połączeń HTTP, więc na stronie będą podane instrukcje, aby uzyskać dostęp do tej konsoli w sposób bezpieczny z komputera przy użyciu tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="80435-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Odblokowywanie usługi Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="80435-131">Skonfiguruj tunel przy użyciu polecenia `ssh` na stronie z wiersza polecenia, zamieniając pozycję `username` na nazwę użytkownika administratora maszyny wirtualnej wybraną wcześniej podczas konfigurowania maszyny wirtualnej za pomocą szablonu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="80435-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="80435-132">Po uruchomieniu tunelu przejdź do adresu http://localhost:8080/ na maszynie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="80435-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="80435-133">Uzyskaj hasło początkowe, uruchamiając następujące polecenie w wierszu polecenia przy aktywnym połączeniu z maszyną wirtualną z usługą Jenkins za pośrednictwem powłoki SSH.</span><span class="sxs-lookup"><span data-stu-id="80435-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="80435-134">Odblokuj pulpit nawigacyjny usługi Jenkins za pomocą hasła początkowego.</span><span class="sxs-lookup"><span data-stu-id="80435-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Odblokowywanie usługi Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="80435-136">Na następnej stronie wybierz pozycję **Zainstaluj sugerowane wtyczki**, a następnie utwórz administratora usługi Jenkins, który będzie służyć do uzyskiwania dostępu do pulpitu nawigacyjnego usługi Jenkins.</span><span class="sxs-lookup"><span data-stu-id="80435-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Usługa Jenkins jest gotowa do użycia.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="80435-138">Serwer Jenkins jest już gotowy do kompilowania kodu.</span><span class="sxs-lookup"><span data-stu-id="80435-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="80435-139">Tworzenie pierwszego zadania</span><span class="sxs-lookup"><span data-stu-id="80435-139">Create your first job</span></span>

<span data-ttu-id="80435-140">W konsoli usługi Jenkins wybierz pozycję **Utwórz nowe zadania**, nadaj temu elementowi nazwę **mySampleApp** i wybierz pozycję **Projekt dowolny**, a następnie wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="80435-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Tworzenie nowego zadania](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="80435-142">Wybierz kartę **Zarządzanie kodem źródłowym**, włącz pozycję **Git** i wprowadź następujący adres URL w polu **Adres URL repozytorium**:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="80435-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Definiowanie repozytorium Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="80435-144">Wybierz kartę **Kompilacja**, a następnie wybierz pozycję **Dodaj krok kompilacji**, **Wywołaj skrypt Gradle**.</span><span class="sxs-lookup"><span data-stu-id="80435-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="80435-145">Wybierz pozycję **Użyj otoki Gradle**, a następnie wprowadź wartość `complete` w polu **Lokalizacja otoki** i wartość `build` w polu **Zadania**.</span><span class="sxs-lookup"><span data-stu-id="80435-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Kompilowanie przy użyciu otoki Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="80435-147">Wybierz pozycję **Zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="80435-147">Select **Advanced..**</span></span> <span data-ttu-id="80435-148">Następnie wprowadź wartość `complete` w polu **Główny skrypt kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="80435-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="80435-149">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="80435-149">Select **Save**.</span></span>

![Konfigurowanie ustawień zaawansowanych w kroku dotyczącym kompilacji i otoki Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="80435-151">Kompilowanie kod</span><span class="sxs-lookup"><span data-stu-id="80435-151">Build the code</span></span>

<span data-ttu-id="80435-152">Wybierz pozycję **Kompiluj teraz**, aby skompilować kod i utworzyć pakiet z aplikacją przykładową.</span><span class="sxs-lookup"><span data-stu-id="80435-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="80435-153">Po zakończeniu kompilacji wybierz link **Obszar roboczy** dla projektu.</span><span class="sxs-lookup"><span data-stu-id="80435-153">When your build completes, select the **Workspace** link for the project.</span></span>

![Przechodzenie do obszaru roboczego w celu pobrania pliku JAR z kompilacji](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="80435-155">Przejdź do folderu `complete/build/libs` i upewnij się, że znajduje się tam plik `gs-spring-boot-0.1.0.jar`, w celu potwierdzenia, że kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="80435-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="80435-156">Serwer Jenkins jest już gotowy i możesz za jego pomocą kompilować własne projekty na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="80435-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80435-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80435-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80435-158">Dodawanie maszyn wirtualnych platformy Azure jako agentów usługi Jenkins</span><span class="sxs-lookup"><span data-stu-id="80435-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
