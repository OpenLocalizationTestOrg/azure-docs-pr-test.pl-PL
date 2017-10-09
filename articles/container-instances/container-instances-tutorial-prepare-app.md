---
title: "aaaAzure samouczek wystąpień kontenera — przygotowanie aplikacji | Dokumentacja platformy Azure"
description: "Przygotowywanie aplikacji do wdrożenia tooAzure wystąpień kontenera"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Utwórz kontener dla wdrożenia tooAzure wystąpień kontenera

Usługa Azure Container Instances umożliwia wdrażanie kontenerów Docker w infrastrukturze platformy Azure bez aprowizowania maszyn wirtualnych ani adaptowania usług wyższego poziomu. Podczas pracy z tym samouczkiem utworzysz prostą aplikację internetową w środowisku Node.js i spakujesz ją w kontenerze, który można uruchomić za pomocą usługi Azure Container Instances. Przedstawimy następujące zagadnienia:

> [!div class="checklist"]
> * Klonowanie źródła aplikacji z usługi GitHub  
> * Tworzenie obrazów kontenera z poziomu źródła aplikacji
> * Testowanie obrazów hello w lokalnym środowisku Docker

W kolejnych samouczkach będzie przekazać tooan Twojego obrazu rejestru kontenera platformy Azure, a następnie wdrożyć je tooAzure wystąpień kontenera.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Ten samouczek zakłada, że masz podstawową wiedzę na temat bazowych koncepcji usługi Docker, takich jak kontenery, obrazy kontenerów i podstawowe polecenia usługi Docker. W razie potrzeby zapoznaj się z tematem [Get starter with Docker (Rozpoczynanie pracy z platformą Docker)]( https://docs.docker.com/get-started/), aby uzyskać podstawowe informacje na temat kontenerów. 

toocomplete tego samouczka potrzebne jest środowisko rozwoju Docker. Środowisko Docker zawiera pakiety, które umożliwiają łatwe konfigurowanie platformy Docker w systemie [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) lub [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Pobieranie kodu aplikacji

Przykładowe Hello w tym samouczku obejmuje prostą aplikację sieci web wbudowane [Node.js](http://nodejs.org). Aplikacja Hello służy statyczne strony HTML i wygląda następująco:

![Samouczek aplikacji wyświetlony w przeglądarce][aci-tutorial-app]

Użyj przykładowych hello toodownload git:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Utwórz obraz kontenera hello

Hello plik Dockerfile w repozytorium przykładowej hello pokazuje, jak kontenera hello jest wbudowana. Rozpoczyna od [oficjalnego obrazu Node.js] [ dockerhub-nodeimage] na podstawie [Alpine Linux](https://alpinelinux.org/), małych dystrybucji, który jest dobrze nadają się toouse z kontenerami. Następnie kopiuje pliki aplikacji hello do kontenera hello, instalacji zależności za pomocą hello Node Package Manager, a na koniec uruchamia aplikację hello.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Użyj hello `docker build` polecenia toocreate hello kontener obrazu, oznaczanie go jako *aci samouczek aplikacji*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Użyj hello `docker images` toosee hello wbudowane obrazu:

```bash
docker images
```

Dane wyjściowe:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Uruchom lokalnie hello kontenera

Przed przystąpieniem do wdrażania tooAzure kontenera hello wystąpień kontenera, uruchomić je lokalnie tooconfirm jego działanie. Witaj `-d` przełącznik umożliwia kontenera hello wykonywane w tle hello podczas `-p` pozwala toomap dowolnego portu tooport Twojego obliczeń 80 w kontenerze hello.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Otwórz hello tooconfirm toohttp://localhost:8080 przeglądarki, która hello kontenera jest uruchomiona.

![Uruchomionej aplikacji hello lokalnie w przeglądarce hello][aci-tutorial-app-local]

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzony obraz kontenera, który może być wdrożony tooAzure wystąpień kontenera. Zakończono Hello następujące kroki:

> [!div class="checklist"]
> * Klonowanie źródła aplikacji hello z usługi GitHub  
> * Tworzenie obrazów kontenera z poziomu źródła aplikacji
> * Testowanie kontenera hello lokalnie

Przejdź dalej toolearn samouczka toohello o przechowywania obrazów kontenera w rejestrze kontenera platformy Azure.

> [!div class="nextstepaction"]
> [Wypychanie tooAzure obrazów rejestru kontenera](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png