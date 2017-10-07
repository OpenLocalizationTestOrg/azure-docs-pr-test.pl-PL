---
title: "Samouczek wystąpień kontenera aaaAzure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek wystąpień kontenera platformy Azure — wdrażanie aplikacji"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a>Wdrażanie kontenera tooAzure wystąpień kontenera

Jest to hello ostatnich trzech części samouczka. W poprzednich sekcjach [utworzono obrazów kontenera](container-instances-tutorial-prepare-app.md) i [wypychana tooan rejestru kontenera Azure](container-instances-tutorial-prepare-acr.md). W tej sekcji zakończeniu samouczka hello wdrażając tooAzure kontenera hello wystąpień kontenera. Ukończono kroki obejmują:

> [!div class="checklist"]
> * Definiowanie grupy kontenera przy użyciu szablonu usługi Azure Resource Manager
> * Wdrażanie hello kontenera grupy przy użyciu hello wiersza polecenia platformy Azure
> * Wyświetlanie dzienników kontenera

## <a name="deploy-hello-container-using-hello-azure-cli"></a>Wdrażanie kontenera hello przy użyciu hello wiersza polecenia platformy Azure

Hello interfejsu wiersza polecenia Azure umożliwia wdrożenie tooAzure kontener wystąpień kontenera za pomocą jednego polecenia. Ponieważ obraz kontenera hello jest obsługiwana w hello prywatnej rejestru kontenera platformy Azure, musi zawierać tooaccess wymagane poświadczenia hello go. W razie potrzeby można je zapytanie, jak pokazano poniżej.

Kontener rejestru logowania serwera (aktualizacja nazwą rejestru):

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

Kontener rejestru hasło:

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

toodeploy kontener obrazu z rejestru kontenera hello z zasobem żądania 1 rdzeń procesora CPU i 1GB pamięci, uruchom następujące polecenie hello:

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

W ciągu kilku sekund zostanie wyświetlony początkową odpowiedź z usługi Azure Resource Manager. Stan hello tooview hello wdrożenia, użyj:

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

Można kontynuować, wykonanie tego polecenia, dopóki hello stan zmieni się z *oczekujące* za*systemem*. Następnie można przejść.

## <a name="view-hello-application-and-container-logs"></a>Wyświetl dzienniki aplikacji i kontener hello

Po pomyślnym wdrożenia hello, Otwórz swój adres IP przeglądarki toohello wyświetlany w danych wyjściowych hello hello następujące polecenie:

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Witaj świecie aplikację w przeglądarce hello][aci-app-browser]

Można również wyświetlić wpisu w dzienniku hello hello kontenera:

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

Dane wyjściowe:

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku została ukończona hello proces wdrażania tooAzure Twojego kontenery wystąpień kontenera. Zakończono Hello następujące kroki:

> [!div class="checklist"]
> * Wdrażanie kontenera hello z hello rejestru kontenera Azure za pomocą hello wiersza polecenia platformy Azure
> * Wyświetlanie aplikacji hello w przeglądarce hello
> * Wyświetlanie hello kontenera dzienników

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
