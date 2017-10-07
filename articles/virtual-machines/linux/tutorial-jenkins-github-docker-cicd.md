---
title: "rozwój potoku na platformie Azure z Wpięć aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak maszyny toocreate Wpięć wirtualnego w platformie Azure, że ściąga z serwisu GitHub dla każdego kodu zatwierdzić i tworzy nowy Docker toorun kontenera aplikacji"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Jak toocreate infrastrukturze programowanie na maszynie Wirtualnej systemu Linux na platformie Azure z Wpięć, GitHub i Docker
tooautomate hello kompilacji i przetestowania etap tworzenia aplikacji, można użyć ciągłej integracji i wdrażania (CI/CD) potoku. W tym samouczku, możesz utworzyć potok CI/CD na maszynie Wirtualnej platformy Azure w tym jak:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej z Wpięć
> * Instalowanie i konfigurowanie Wpięć
> * Utwórz integrację elementu webhook GitHub i Wpięć
> * Tworzenie i zatwierdza wyzwalacza Wpięć Tworzenie zadania z usługi GitHub
> * Tworzenie obrazu Docker dla aplikacji
> * Sprawdź, czy zatwierdzenia GitHub Tworzenie nowego obrazu Docker i aktualizacje uruchamiania aplikacji


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Utwórz wystąpienie Wpięć
W poprzednim samouczek dotyczący [jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md), możesz przedstawiono sposób dostosowywania maszyny Wirtualnej tooautomate z inicjowaniem chmury. Ten samouczek używa init chmury pliku tooinstall Wpięć i Docker na maszynie Wirtualnej. 

W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji. Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym. Wprowadź `sensible-editor cloud-init-jenkins.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory. Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupJenkins* w hello *eastus* lokalizacji:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Użyj hello `--custom-data` toopass parametru w pliku config init chmury. Podaj pełną ścieżkę hello zbyt*chmurze init-jenkins.txt* po zapisaniu pliku hello poza istnieje katalog roboczy.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Trwa kilka minut, aż hello wirtualna toobe utworzone i skonfigurowane.

tooallow web tooreach ruch maszyny Wirtualnej, użyj [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) portu tooopen *8080* Wpięć ruchu i portu *1337* hello aplikacji Node.js, który jest używany toorun przykładową aplikację:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Skonfiguruj Wpięć
tooaccess Twojego Wpięć wystąpienia, Uzyskaj hello publicznego adresu IP maszyny Wirtualnej:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Ze względów bezpieczeństwa należy tooenter hello początkowej administratora hasła, które są przechowywane w pliku tekstowym na Wpięć zainstalować powitalne toostart Twojej maszyny Wirtualnej. Użyj hello uzyskane w hello poprzedniego kroku tooSSH tooyour maszyny Wirtualnej publiczny adres IP:

```bash
ssh azureuser@<publicIps>
```

Widok hello `initialAdminPassword` Twojego Wpięć zainstalować i skopiuj go:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Jeśli plik hello nie jest jeszcze dostępny, zaczekaj kilka minut dla chmury init toocomplete hello Wpięć i zainstaluj Docker.

Teraz Otwórz przeglądarkę sieci web i przejdź zbyt`http://<publicIps>:8080`. Ukończenie początkowej konfiguracji Wpięć hello w następujący sposób:

- Wprowadź hello *initialAdminPassword* uzyskane z hello maszyny Wirtualnej w poprzednim kroku hello.
- Kliknij przycisk **wybierz tooinstall wtyczek**
- Wyszukaj *GitHub* w polu tekstowym hello hello górze wybierz hello *wtyczki GitHub*, następnie kliknij przycisk **instalacji**
- toocreate Wpięć konta użytkownika, wypełnij formularz hello zgodnie z potrzebami. Z punktu widzenia zabezpieczeń należy utworzyć ten pierwszy użytkownik Wpięć zamiast kontynuowanie jako hello domyślnego konta administratora.
- Gdy skończysz, kliknij przycisk **Rozpoczynanie korzystania z Wpięć**


## <a name="create-github-webhook"></a>Utwórz element webhook GitHub
tooconfigure hello Integracja z usługą GitHub, otwórz hello [Node.js Hello World Przykładowa aplikacja](https://github.com/Azure-Samples/nodejs-docs-hello-world) z hello repozytorium przykładów dla platformy Azure. toofork hello repozytorium tooyour własne konto GitHub, kliknij przycisk hello **rozwidlenia** przycisk w prawym górnym rogu hello.

Tworzenie elementu webhook wewnątrz rozwidlenia hello, utworzone:

- Kliknij przycisk **ustawienia**, a następnie wybierz pozycję **integracji i usługi** na powitania po lewej stronie.
- Kliknij przycisk **dodawania usługi**, wprowadź *Wpięć* w polu filtru.
- Wybierz *Wpięć (GitHub wtyczki)*
- Dla hello **Wpięć utworzenie punktu zaczepienia adresu URL**, wprowadź `http://<publicIps>:8080/github-webhook/`. Upewnij się, że możesz uwzględnić końcowe hello /
- Kliknij przycisk **dodawania usługi**

![Dodaj repozytorium tooyour rozwidlone elementu webhook GitHub](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Utwórz zadanie Wpięć
toohave Wpięć odpowiedź tooan zdarzeń w usłudze GitHub takich jak zatwierdzania kodu, Utwórz zadanie Wpięć. 

W witrynie sieci Web Wpięć kliknij **tworzenie nowych zadań** ze strony głównej hello:

- Wprowadź *HelloWorld* jako nazwa zadania. Wybierz **stylu projektu**, a następnie wybierz pozycję **OK**.
- W obszarze hello **ogólne** zaznacz **GitHub** projektu i wprowadź adres URL repozytorium rozwidlonych, takich jak *https://github.com/iainfoulds/nodejs-docs-hello-world*
- W obszarze hello **źródła zarządzania kodem** zaznacz **Git**, wprowadź Twojego repozytorium rozwidlonych *.git* adres URL, takie jak *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- W obszarze hello **kompilacji wyzwalaczy** zaznacz **wyzwalacza haku GitHub dla sondowania GITscm**.
- W obszarze hello **kompilacji** wybierz **kroku kompilacji Dodaj**. Wybierz **wykonywania powłoki**, wprowadź `echo "Testing"` w oknie toocommand.
- Kliknij przycisk **zapisać** u dołu okna zadań hello hello.


## <a name="test-github-integration"></a>Testowanie integracji usługi GitHub
Witaj tootest GitHub integracji z Wpięć, zatwierdzić zmiany w rozwidlenia. 

W witrynie GitHub interfejs użytkownika sieci web, wybierz użytkownika rozwidlonych repozytorium, a następnie kliknij hello **index.js** pliku. Kliknij ten plik tooedit ikonę ołówka hello tak odczytuje wiersz 6:

```nodejs
response.end("Hello World!");
```

toocommit zmiany, kliknij przycisk hello **Zatwierdź zmiany** u dołu hello.

W Wpięć, nowej kompilacji zaczyna się w obszarze hello **kompilacji historii** sekcji hello lewym dolnym rogu strony zadania. Kliknij łącze numer kompilacji hello i wybierz **dane wyjściowe konsoli** hello rozmiaru po lewej stronie. Można wyświetlić kroki hello Wpięć przyjmuje jako kodu są pobierane z usługi GitHub i hello kompilacji akcji dane wyjściowe wiadomości powitania `Testing` toohello konsoli. Zawsze, gdy zatwierdzenie jest przeprowadzane w witrynie GitHub, hello webhook przez nią miejsce osiągnie limit tooJenkins i wyzwalają nowej kompilacji w ten sposób.


## <a name="define-docker-build-image"></a>Zdefiniuj obraz kompilacji Docker
Aplikacja Node.js hello toosee oparte na systemie zatwierdzenia GitHub, umożliwia tworzenie aplikacji hello toorun obrazu Docker. Obraz powitania składa się z plik Dockerfile, który definiuje sposób tooconfigure hello kontenera, w którym działa aplikacja hello. 

Z tooyour połączenia SSH hello maszyny Wirtualnej należy zmienić katalogu roboczego Wpięć toohello o nazwie po zadaniu hello, utworzony w poprzednim kroku. W naszym przykładzie, który miał nazwę *HelloWorld*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Utwórz plik o w bieżącym katalogu roboczym z `sudo sensible-editor Dockerfile` i Wklej powitania po zawartości. Upewnij się, że w tym hello jest cały plik Dockerfile skopiowane poprawnie, szczególnie hello pierwszy wiersz:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Ten plik Dockerfile używa hello podstawowy obraz Node.js przy użyciu Alpine Linux, port ujawnia 1337 aplikacji Hello World hello jest uruchamiany na, a następnie kopiuje pliki aplikacji hello i inicjuje go.


## <a name="create-jenkins-build-rules"></a>Tworzenie reguł kompilacji Wpięć
W poprzednim kroku możesz utworzyć podstawowe reguły kompilacji Wpięć, że dane wyjściowe konsoli toohello wiadomości. Umożliwia tworzenie toouse kroku kompilacji hello naszych plik Dockerfile i uruchamianie aplikacji hello.

Ponownie w wystąpieniu Wpięć wybierz zadanie hello, utworzony w poprzednim kroku. Kliknij przycisk **Konfiguruj** na powitania po lewej stronie i przewiń w dół toohello **kompilacji** sekcji:

- Usuń istniejącą `echo "Test"` kroku kompilacji. Kliknij przycisk hello red cross na powitania prawym górnym rogu hello istniejącego pola kroku kompilacji.
- Kliknij przycisk **kroku kompilacji Dodaj**, a następnie wybierz pozycję **wykonania powłoki**
- W hello **polecenia** polu, wprowadź następujące polecenia Docker hello, a następnie wybierz **zapisać**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

kroki procesu kompilacji Docker Hello Tworzenie obrazu i tagu za pomocą hello Wpięć numer kompilacji, więc można zachowują historię obrazów. Kontenerach istniejących uruchamiania aplikacji hello są zatrzymane i następnie usuwane. Nowy kontener jest uruchomiony przy użyciu obrazu hello i uruchamia aplikację Node.js oparte na najnowszej zatwierdzeń hello w serwisie GitHub.


## <a name="test-your-pipeline"></a>Testowanie potoku sieci
toosee hello całego procesu akcji, Edytuj hello *index.js* ponownie plik w Twojej rozwidlonych repozytorium GitHub i kliknij przycisk **zatwierdzić zmiany**. Nowe zadanie uruchamia w Wpięć oparta na powitania webhook GitHub. On zajmuje kilka sekund toocreate hello Docker obrazu i uruchomić aplikację w nowym kontenerze.

W razie potrzeby ponownie uzyskać hello publicznego adresu IP maszyny Wirtualnej:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Otwórz przeglądarkę sieci web, a następnie wprowadź `http://<publicIps>:1337`. Aplikacji Node.js jest wyświetlany i odzwierciedla hello najnowsze zatwierdzenia w rozwidlenia GitHub w następujący sposób:

![Uruchomionej aplikacji Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Teraz należy innego toohello edycji *index.js* plików w przypadku zmiany hello GitHub i zatwierdzania. Zaczekaj kilka sekund na powitania toocomplete zadania w Wpięć, a następnie Odśwież wersji hello zaktualizowane toosee przeglądarki sieci web programu aplikacji uruchomionej w nowym kontenerze w następujący sposób:

![Uruchomienie aplikacji Node.js po innym zatwierdzenia GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Następne kroki
W tym samouczku skonfigurowane toorun GitHub zadania kompilacji Wpięć na każdym zatwierdzeniu kodu, a następnie wdrożyć tootest kontenera Docker aplikacji. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej z Wpięć
> * Instalowanie i konfigurowanie Wpięć
> * Utwórz integrację elementu webhook GitHub i Wpięć
> * Tworzenie i zatwierdza wyzwalacza Wpięć Tworzenie zadania z usługi GitHub
> * Tworzenie obrazu Docker dla aplikacji
> * Sprawdź, czy zatwierdzenia GitHub Tworzenie nowego obrazu Docker i aktualizacje uruchamiania aplikacji

Więcej informacji na temat przejść dalej toolearn samouczka toohello toointegrate Wpięć z Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Wdrażanie aplikacji przy użyciu Wpięć i usługi Team Services](tutorial-build-deploy-jenkins.md)