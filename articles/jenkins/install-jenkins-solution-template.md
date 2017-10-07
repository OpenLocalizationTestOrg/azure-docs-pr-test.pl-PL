---
title: "aaaCreate serwer Wpięć na platformie Azure"
description: "Zainstaluj Wpięć na maszynie wirtualnej platformy Azure Linux z szablon rozwiązania Wpięć hello i tworzenia przykładowej aplikacji Java."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="44e30-103">Utwórz serwer Wpięć na maszynie Wirtualnej platformy Azure Linux z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44e30-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="44e30-104">Ta opcja szybkiego startu przedstawia sposób tooinstall [Wpięć](https://jenkins.io) Ubuntu Linux maszyny wirtualnej z narzędziami hello i toowork dodatków plug-in skonfigurowane przy użyciu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="44e30-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="44e30-105">Po zakończeniu uzyskasz działający na platformie Azure serwer Jenkins umożliwiający skompilowanie przykładowej aplikacji Java z usługi [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="44e30-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44e30-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44e30-106">Prerequisites</span></span>

* <span data-ttu-id="44e30-107">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="44e30-107">An Azure subscription</span></span>
* <span data-ttu-id="44e30-108">TooSSH dostępu w wierszu polecenia na komputerze (takie jak hello Bash powłoki lub [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="44e30-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="44e30-109">Utwórz hello Wpięć maszyny Wirtualnej na podstawie hello szablon rozwiązania</span><span class="sxs-lookup"><span data-stu-id="44e30-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="44e30-110">Otwórz hello [obrazu z witryny marketplace Wpięć](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) w przeglądarce sieci web i wybierz **UZYSKAĆ IT** z powitania po lewej stronie powitania strony.</span><span class="sxs-lookup"><span data-stu-id="44e30-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="44e30-111">Przejrzyj hello cennik szczegółowe informacje, a następnie wybierz **Kontynuuj**, a następnie wybierz pozycję **Utwórz** tooconfigure hello Wpięć serwera w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44e30-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Okno dialogowe witryny Azure Portal](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="44e30-113">W hello **skonfigurowania podstawowych ustawień** karcie, wypełnij hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="44e30-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Konfigurowanie ustawień podstawowych](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="44e30-115">W polu **Nazwa** użyj wartości **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="44e30-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="44e30-116">Wprowadź **nazwę użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="44e30-116">Enter a **User name**.</span></span> <span data-ttu-id="44e30-117">Nazwa użytkownika Hello musi spełniać [szczególne wymagania](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="44e30-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="44e30-118">Wybierz **hasło** jako hello **typ uwierzytelniania** i wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="44e30-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="44e30-119">hasło Hello musi zawierać się wielką literą, cyfry i znak specjalny.</span><span class="sxs-lookup"><span data-stu-id="44e30-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="44e30-120">Użyj **myJenkinsResourceGroup** dla hello **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="44e30-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="44e30-121">Wybierz hello **wschodnie stany USA** [regionu Azure](https://azure.microsoft.com/regions/) z hello **lokalizacji** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="44e30-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="44e30-122">Wybierz **OK** tooproceed toohello **Konfigurowanie dodatkowych opcji** kartę. Wprowadź unikatowy serwera nazw domen i tooidentify hello Wpięć i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="44e30-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Konfigurowanie opcji dodatkowych](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="44e30-124">Po pomyślnej weryfikacji, wybierz **OK** ponownie z hello **Podsumowanie** kartę. Na koniec wybierz **zakupu** toocreate hello Wpięć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="44e30-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="44e30-125">Gdy serwer jest gotowy, otrzymasz powiadomienie w hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="44e30-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Powiadomienie o tym, że usługa Jenkins jest gotowa](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="44e30-127">Połącz tooJenkins</span><span class="sxs-lookup"><span data-stu-id="44e30-127">Connect tooJenkins</span></span>

<span data-ttu-id="44e30-128">Przejdź tooyour maszyny wirtualnej (na przykład http://jenkins2517454.eastus.cloudapp.azure.com/) w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="44e30-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="44e30-129">konsoli Wpięć Hello jest niedostępna za pośrednictwem niezabezpieczonej HTTP, więc instrukcje znajdują się na powitania strony tooaccess hello Wpięć konsoli bezpiecznie z komputera przy użyciu tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="44e30-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Odblokowywanie usługi Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="44e30-131">Konfigurowanie tunelu hello przy użyciu hello `ssh` polecenia na stronie powitania z wiersza polecenia hello, zastępując `username` o nazwie hello administrator maszyny wirtualnej hello wcześniej wybrany podczas konfigurowania maszyny wirtualnej hello z hello szablon rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="44e30-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="44e30-132">Po uruchomieniu tunelu hello Przejdź toohttp://localhost:8080 / na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="44e30-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="44e30-133">Pobierz hasła początkowego hello, uruchamiając następujące polecenie w wierszu polecenia hello nawiązaniu połączenia za pośrednictwem toohello SSH maszyny Wirtualnej Wpięć hello.</span><span class="sxs-lookup"><span data-stu-id="44e30-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="44e30-134">Odblokuj hello Wpięć, odwiedź pulpit nawigacyjny hello pierwsze logowanie przy użyciu tego hasła początkowego.</span><span class="sxs-lookup"><span data-stu-id="44e30-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Odblokowywanie usługi Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="44e30-136">Wybierz **Instalowanie wtyczki sugerowane** na powitania następnej strony, a następnie utwórz Wpięć administratora używane tooaccess hello Wpięć pulpit nawigacyjny użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44e30-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Usługa Jenkins jest gotowa do użycia.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="44e30-138">Serwer Wpięć Hello jest teraz gotowy toobuild kodu.</span><span class="sxs-lookup"><span data-stu-id="44e30-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="44e30-139">Tworzenie pierwszego zadania</span><span class="sxs-lookup"><span data-stu-id="44e30-139">Create your first job</span></span>

<span data-ttu-id="44e30-140">Wybierz **tworzenie nowych zadań** za pomocą konsoli Wpięć hello, nadaj mu nazwę **mySampleApp** i wybierz **stylu projektu**, a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="44e30-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Tworzenie nowego zadania](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="44e30-142">Wybierz hello **zarządzania kodem źródłowym** pozycję Włącz **Git**i wprowadź hello następującego adresu URL w **adres URL repozytorium** pola:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="44e30-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Zdefiniuj hello repozytorium Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="44e30-144">Wybierz hello **kompilacji** , a następnie wybierz **kroku kompilacji Dodaj**, **Gradle wywołanie skryptu**.</span><span class="sxs-lookup"><span data-stu-id="44e30-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="44e30-145">Wybierz pozycję **Użyj otoki Gradle**, a następnie wprowadź wartość `complete` w polu **Lokalizacja otoki** i wartość `build` w polu **Zadania**.</span><span class="sxs-lookup"><span data-stu-id="44e30-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Użyj hello Gradle otoki toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="44e30-147">Wybierz pozycję **Zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="44e30-147">Select **Advanced..**</span></span> <span data-ttu-id="44e30-148">a następnie wprowadź `complete` w hello **głównego kompilacji skryptu** pola.</span><span class="sxs-lookup"><span data-stu-id="44e30-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="44e30-149">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="44e30-149">Select **Save**.</span></span>

![Zaawansowane ustawienia kroku kompilacji otoki Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="44e30-151">Tworzenie hello kodu</span><span class="sxs-lookup"><span data-stu-id="44e30-151">Build hello code</span></span>

<span data-ttu-id="44e30-152">Wybierz **kompilacji teraz** toocompile hello kod i pakietów hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44e30-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="44e30-153">Po zakończeniu kompilacji, wybierz hello **obszaru roboczego** łącze hello projektu.</span><span class="sxs-lookup"><span data-stu-id="44e30-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Przeglądaj toohello plik JAR hello tooget obszaru roboczego z hello kompilacji](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="44e30-155">Przejdź za`complete/build/libs` i upewnij się, hello `gs-spring-boot-0.1.0.jar` jest tooverify pomyślnym kompilacji.</span><span class="sxs-lookup"><span data-stu-id="44e30-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="44e30-156">Z Wpięć, który serwer jest teraz gotowy toobuild projekty na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="44e30-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e30-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44e30-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44e30-158">Dodawanie maszyn wirtualnych platformy Azure jako agentów usługi Jenkins</span><span class="sxs-lookup"><span data-stu-id="44e30-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
