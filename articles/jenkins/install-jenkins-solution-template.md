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
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Utwórz serwer Wpięć na maszynie Wirtualnej platformy Azure Linux z hello portalu Azure

Ta opcja szybkiego startu przedstawia sposób tooinstall [Wpięć](https://jenkins.io) Ubuntu Linux maszyny wirtualnej z narzędziami hello i toowork dodatków plug-in skonfigurowane przy użyciu platformy Azure. Po zakończeniu uzyskasz działający na platformie Azure serwer Jenkins umożliwiający skompilowanie przykładowej aplikacji Java z usługi [GitHub](https://github.com).

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure
* TooSSH dostępu w wierszu polecenia na komputerze (takie jak hello Bash powłoki lub [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Utwórz hello Wpięć maszyny Wirtualnej na podstawie hello szablon rozwiązania

Otwórz hello [obrazu z witryny marketplace Wpięć](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) w przeglądarce sieci web i wybierz **UZYSKAĆ IT** z powitania po lewej stronie powitania strony. Przejrzyj hello cennik szczegółowe informacje, a następnie wybierz **Kontynuuj**, a następnie wybierz pozycję **Utwórz** tooconfigure hello Wpięć serwera w hello portalu Azure. 
   
![Okno dialogowe witryny Azure Portal](./media/install-jenkins-solution-template/ap-create.png)

W hello **skonfigurowania podstawowych ustawień** karcie, wypełnij hello następujące pola:

![Konfigurowanie ustawień podstawowych](./media/install-jenkins-solution-template/ap-basic.png)

* W polu **Nazwa** użyj wartości **Jenkins**.
* Wprowadź **nazwę użytkownika**. Nazwa użytkownika Hello musi spełniać [szczególne wymagania](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Wybierz **hasło** jako hello **typ uwierzytelniania** i wprowadź hasło. hasło Hello musi zawierać się wielką literą, cyfry i znak specjalny.
* Użyj **myJenkinsResourceGroup** dla hello **grupy zasobów**.
* Wybierz hello **wschodnie stany USA** [regionu Azure](https://azure.microsoft.com/regions/) z hello **lokalizacji** listy rozwijanej.

Wybierz **OK** tooproceed toohello **Konfigurowanie dodatkowych opcji** kartę. Wprowadź unikatowy serwera nazw domen i tooidentify hello Wpięć i wybierz **OK**.

![Konfigurowanie opcji dodatkowych](./media/install-jenkins-solution-template/ap-addtional.png)  

 Po pomyślnej weryfikacji, wybierz **OK** ponownie z hello **Podsumowanie** kartę. Na koniec wybierz **zakupu** toocreate hello Wpięć maszyny Wirtualnej. Gdy serwer jest gotowy, otrzymasz powiadomienie w hello portalu Azure:   

![Powiadomienie o tym, że usługa Jenkins jest gotowa](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Połącz tooJenkins

Przejdź tooyour maszyny wirtualnej (na przykład http://jenkins2517454.eastus.cloudapp.azure.com/) w przeglądarce sieci web. konsoli Wpięć Hello jest niedostępna za pośrednictwem niezabezpieczonej HTTP, więc instrukcje znajdują się na powitania strony tooaccess hello Wpięć konsoli bezpiecznie z komputera przy użyciu tunelu SSH.

![Odblokowywanie usługi Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Konfigurowanie tunelu hello przy użyciu hello `ssh` polecenia na stronie powitania z wiersza polecenia hello, zastępując `username` o nazwie hello administrator maszyny wirtualnej hello wcześniej wybrany podczas konfigurowania maszyny wirtualnej hello z hello szablon rozwiązania.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Po uruchomieniu tunelu hello Przejdź toohttp://localhost:8080 / na komputerze lokalnym. 

Pobierz hasła początkowego hello, uruchamiając następujące polecenie w wierszu polecenia hello nawiązaniu połączenia za pośrednictwem toohello SSH maszyny Wirtualnej Wpięć hello.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Odblokuj hello Wpięć, odwiedź pulpit nawigacyjny hello pierwsze logowanie przy użyciu tego hasła początkowego.

![Odblokowywanie usługi Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

Wybierz **Instalowanie wtyczki sugerowane** na powitania następnej strony, a następnie utwórz Wpięć administratora używane tooaccess hello Wpięć pulpit nawigacyjny użytkowników.

![Usługa Jenkins jest gotowa do użycia.](./media/install-jenkins-solution-template/jenkins-welcome.png)

Serwer Wpięć Hello jest teraz gotowy toobuild kodu.

## <a name="create-your-first-job"></a>Tworzenie pierwszego zadania

Wybierz **tworzenie nowych zadań** za pomocą konsoli Wpięć hello, nadaj mu nazwę **mySampleApp** i wybierz **stylu projektu**, a następnie wybierz pozycję **OK**.

![Tworzenie nowego zadania](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Wybierz hello **zarządzania kodem źródłowym** pozycję Włącz **Git**i wprowadź hello następującego adresu URL w **adres URL repozytorium** pola:`https://github.com/spring-guides/gs-spring-boot.git`

![Zdefiniuj hello repozytorium Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Wybierz hello **kompilacji** , a następnie wybierz **kroku kompilacji Dodaj**, **Gradle wywołanie skryptu**. Wybierz pozycję **Użyj otoki Gradle**, a następnie wprowadź wartość `complete` w polu **Lokalizacja otoki** i wartość `build` w polu **Zadania**.

![Użyj hello Gradle otoki toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Wybierz pozycję **Zaawansowane**. a następnie wprowadź `complete` w hello **głównego kompilacji skryptu** pola. Wybierz pozycję **Zapisz**.

![Zaawansowane ustawienia kroku kompilacji otoki Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Tworzenie hello kodu

Wybierz **kompilacji teraz** toocompile hello kod i pakietów hello przykładowej aplikacji. Po zakończeniu kompilacji, wybierz hello **obszaru roboczego** łącze hello projektu.

![Przeglądaj toohello plik JAR hello tooget obszaru roboczego z hello kompilacji](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Przejdź za`complete/build/libs` i upewnij się, hello `gs-spring-boot-0.1.0.jar` jest tooverify pomyślnym kompilacji. Z Wpięć, który serwer jest teraz gotowy toobuild projekty na platformie Azure.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dodawanie maszyn wirtualnych platformy Azure jako agentów usługi Jenkins](jenkins-azure-vm-agents.md)
