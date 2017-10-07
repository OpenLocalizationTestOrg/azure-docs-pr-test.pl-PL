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
# <a name="local-git-deployment-tooazure-app-service"></a>Lokalnego wdrożenia Git tooAzure usługi aplikacji
W tym samouczku przedstawiono sposób toodeploy aplikacji zbyt[usłudze Azure App Service] z repozytorium Git na komputerze lokalnym. App Service obsługuje takie podejście z hello **lokalnego Git** opcji wdrażania w hello [Azure Portal].  
Wiele poleceń Git hello opisane w tym artykule są wykonywane automatycznie podczas tworzenia aplikacji usługi app Service przy użyciu hello [interfejsu wiersza polecenia platformy Azure] zgodnie z opisem [tutaj](app-service-web-get-started.md).

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy:

* Git. Możesz pobrać binarne instalacji hello [tutaj](http://www.git-scm.com/downloads).  
* Podstawową wiedzę na temat narzędzia Git.
* Konto platformy Microsoft Azure. Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą wersję początkową aplikacji w usłudze App Service. Bez kart kredytowych i bez zobowiązań.  
> 
> 

## <a name="Step1"></a>Krok 1: Tworzenie lokalnego repozytorium
Wykonaj następujące zadania toocreate nowego repozytorium Git hello.

1. Uruchom narzędzie wiersza polecenia, takich jak **GitBash** (system Windows) lub **Bash** (powłoka systemu Unix). OS X w systemach hello wiersza polecenia można dostęp za pośrednictwem hello **Terminal** aplikacji.
2. Przejdź toohello katalogu, gdy toodeploy zawartości hello jest zlokalizowany.
3. Użyj następującego polecenia tooinitialize nowego repozytorium Git hello:

```bash  
git init
```

## <a name="Step2"></a>Krok 2: Zatwierdź zawartości
Usługa aplikacji obsługuje aplikacje utworzone w różnych językach programowania. 

1. Jeśli repozytorium już zawiera Pomiń zawartości tego punktu i Przenieś toopoint 2 poniżej. Jeśli repozytorium nie zawiera zawartości po prostu umieścić plik statyczny .html w następujący sposób: 
   
   * Za pomocą edytora tekstu, Utwórz nowy plik o nazwie **index.html** hello katalogu głównego repozytorium Git hello
   * Dodaj hello następującego tekstu jako hello index.html hello zawartości pliku i zapisz go: *Git Witaj!*
2. Z wiersza polecenia hello Sprawdź, czy w katalogu głównym hello repozytorium Git. Użyj następującego polecenia tooadd pliki tooyour repozytorium hello:

```bash  
git add -A
```
3. Następnie Zatwierdź hello zmiany toohello repozytorium przy użyciu następującego polecenia hello:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Krok 3: Włącz hello repozytorium aplikacji usługi aplikacji
Wykonaj następujące kroki tooenable repozytorium Git aplikację usługi aplikacji hello.

1. Zaloguj się za toohello [Azure Portal].
2. W bloku aplikację usługi aplikacji, kliknij przycisk **Ustawienia > źródło wdrożenia**. Kliknij przycisk **wybierz źródło**, następnie kliknij przycisk **lokalnego repozytorium Git**, a następnie kliknij przycisk **OK**.  
   
    ![Lokalne repozytorium Git](./media/app-service-deploy-local-git/local_git_selection.png)
3. Jeśli jest to pierwszy ustawienia czasu zapasowej repozytorium na platformie Azure, należy toocreate poświadczenia logowania dla niego. Użyjesz ich toolog do hello Azure repozytorium i Wypchnij zmiany z lokalnym repozytorium Git. W bloku aplikacji kliknij **Ustawienia > poświadczenia wdrożenia**, skonfiguruj wdrożenia, nazwę użytkownika i hasło. Gdy wszystko będzie gotowe, kliknij przycisk **zapisać**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Krok 4: Wdrażanie projektu
Użyj hello następujące kroki toopublish tooApp Twojej aplikacji usługi przy użyciu lokalnego Git.

1. W bloku aplikacji w portalu Azure hello, kliknij przycisk **Ustawienia > właściwości** dla hello **adres URL Git**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **Adres URL Git** jest toofrom toodeploy odwołania zdalnego hello lokalnym repozytorium. Ten adres URL będzie używany w hello następujące kroki.
2. Przy użyciu wiersza polecenia hello, sprawdź, czy w katalogu głównym hello lokalnego repozytorium Git.
3. Użyj `git remote` tooadd hello zdalnego odwołania na liście **adres URL Git** z kroku 1. Polecenie będzie wyglądać podobnie toohello następujące:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Witaj **zdalnego** polecenie dodaje tooa nazwanego odwołania zdalnego repozytorium. W tym przykładzie powoduje utworzenie odwołania do repozytorium aplikacji sieci web o nazwie "azure".
   > 
   > 
4. Push Twojej zawartości tooApp usługi przy użyciu nowego hello **azure** zdalnego utworzony.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Przejdź wstecz tooyour aplikacji w hello portalu Azure. Wpis dziennika z najnowszych wypychania powinien być wyświetlany w hello **wdrożeń** bloku. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Kliknij przycisk hello **Przeglądaj** u góry hello hello tooverify bloku aplikacji hello zawartości została wdrożona. 

## <a name="Step5"></a>Rozwiązywanie problemów
dostępne są następujące Hello: błędy lub problemy najczęściej występujące podczas korzystania tooan toopublish Git aplikacji usługi app Service na platformie Azure:

- - -
**Objaw**: nie można tooaccess [siteURL]: nie powiodło się tooconnect zbyt [scmAddress]

**Przyczyna**: ten błąd może wystąpić, jeśli aplikacja hello nie jest uruchomiona.

**Rozdzielczość**: Start aplikacji hello w hello portalu Azure. Wdrożenie systemu Git nie będzie działać, chyba że aplikacja hello jest uruchomiona. 

- - -
**Objaw**: nie można rozpoznać nazwy hosta "hosta"

**Przyczyna**: ten błąd może wystąpić, jeśli informacje o adresie hello wprowadzona podczas tworzenia powitania "azure" zdalnego jest niepoprawne.

**Rozdzielczość**: Użyj hello `git remote -v` polecenia toolist wszystkie element zdalny, wraz z hello skojarzony adres URL. Sprawdź, czy adres URL hello hello "azure" zdalnego jest poprawna. W razie potrzeby usuń i ponownie utwórz tym zdalnego przy użyciu hello Popraw adres URL.

- - -
**Objaw**: nie odwołania do wspólnego i brak określone; żadne czynności. Być może należy określić gałąź, takich jak 'master'.

**Przyczyna**: ten błąd może wystąpić, jeśli nie określić gałąź podczas wykonywania operacji wypychania narzędzia git i są wartości not set hello push.default używane przez Git.

**Rozdzielczość**: operacja hello wypychania ponownie, określając hello głównej gałęzi. Na przykład:

```bash  
git push azure master
```
- - -
**Objaw**: nie pasuje do żadnego src refspec [nazwa_gałęzi].

**Przyczyna**: ten błąd może wystąpić, jeśli próba toopush tooa gałęzi innej niż główny na powitania "azure" zdalnego.

**Rozdzielczość**: operacja hello wypychania ponownie, określając hello głównej gałęzi. Na przykład:

```bash  
git push azure master
```
- - -
**Objaw**: RPC nie powiodło się; spowodować = 22, kod HTTP = 502.

**Przyczyna**: ten błąd może wystąpić, jeśli próba toopush repozytorium git dużych za pośrednictwem protokołu HTTPS.

**Rozdzielczość**: Konfiguracja git hello zmiany na większy postBuffer hello toomake maszyny lokalne powitania

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Objaw**: błąd - repozytorium tooremote zatwierdzone zmiany ale aplikacji sieci web nie zostały zaktualizowane.

**Przyczyna**: ten błąd może wystąpić w przypadku wdrażania aplikacji Node.js zawierający plik package.json, który określa dodatkowe wymagane moduły.

**Rozdzielczość**: dodatkowych komunikatów zawierających 'npm błąd!' powinny być rejestrowane toothis wcześniejszych błędów i może zapewnić dodatkowy kontekst hello awarii. następujący Hello są znane przyczyny tego błędu i hello odpowiedniego "npm błąd!' Komunikat:

* **Plik package.json źle sformułowane**: błąd npm! Nie można odczytać zależności.
* **Natywny moduł, który nie ma binarne dystrybucji dla systemu Windows**:
  
  * Błąd npm! \`cmd "/ c" "gyp węzła Odbuduj"\` nie powiodło się z 1
    
      LUB
  * Błąd npm! [modulename@version] preinstalować: \`upewnij || gmake\`

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Dokumentacja usługi Git](http://git-scm.com/documentation)
* [Dokumentacja Kudu projektu](https://github.com/projectkudu/kudu/wiki)
* [TooAzure ciągłej wdrożenia usługi aplikacji](app-service-continuous-deployment.md)
* [Jak toouse programu PowerShell dla usługi Azure](/powershell/azure/overview)
* [Jak toouse hello interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md)

[usłudze Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[interfejsu wiersza polecenia platformy Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
