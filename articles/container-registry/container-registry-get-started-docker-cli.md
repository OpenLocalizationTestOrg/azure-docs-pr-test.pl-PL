---
title: aaaPush Docker obrazu tooprivate rejestru Azure | Dokumentacja firmy Microsoft
description: "I wypychania Docker rejestru kontener prywatnego tooa obrazów na platformie Azure przy użyciu interfejsu wiersza polecenia Docker hello"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a>Pierwszy obraz tooa prywatnej Docker kontenera rejestr przy użyciu interfejsu wiersza polecenia Docker hello push
Rejestru kontenera platformy Azure przechowywanych i zarządzanych prywatnej [Docker](http://hub.docker.com) kontener obrazów, podobne toohello sposób [Centrum Docker](https://hub.docker.com/) przechowuje publiczny obrazy usługi Docker. Użyj hello [interfejsu wiersza polecenia Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) dla [logowania](https://docs.docker.com/engine/reference/commandline/login/), [wypychania](https://docs.docker.com/engine/reference/commandline/push/), [ściągania](https://docs.docker.com/engine/reference/commandline/pull/)i inne operacje dotyczące Twojej kontenera rejestr.

Więcej tła i pojęć, zobacz [hello — omówienie](container-registry-intro.md)



## <a name="prerequisites"></a>Wymagania wstępne
* **Usługa Azure Container Registry** — Tworzy rejestr kontenera w subskrypcji platformy Azure. Na przykład użyć hello [portalu Azure](container-registry-get-started-portal.md) lub hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Interfejs wiersza polecenia docker** -tooset komputera lokalnego jako Docker dostępu i host hello Docker polecenia interfejsu wiersza polecenia, zainstaluj [aparatem platformy Docker](https://docs.docker.com/engine/installation/).

## <a name="log-in-tooa-registry"></a>Zaloguj się w rejestrze tooa
Uruchom `docker login` toolog w rejestrze kontenera tooyour z Twojej [poświadczenia rejestru](container-registry-authentication.md).

Witaj w poniższym przykładzie przekazuje hello Identyfikatora i hasła usługi Azure Active Directory [nazwy głównej usługi](../active-directory/active-directory-application-objects.md). Na przykład może przypisano rejestr tooyour główna usługi scenariusz automatyzacji.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> Upewnij się, że toospecify hello rejestru w pełni kwalifikowaną nazwę (tylko małe litery). W tym przykładzie jest to `myregistry.azurecr.io`.

## <a name="steps-toopull-and-push-an-image"></a>Kroki toopull i wypychania obrazu
Witaj wykonaj przykładowe, pliki do pobrania hello Nginx obrazu z publicznego rejestru Centrum Docker hello tagi go do rejestru prywatnej kontenera platformy Azure, wypchnięcia jej tooyour rejestru, a następnie pobiera go ponownie.

**1. Ściąganie hello Docker oficjalnego obrazu dla Nginx**

Pierwszy ściągania hello publicznego Nginx obrazu tooyour komputera lokalnego.

```
docker pull nginx
```
**2. Kontener Nginx hello Start**

Witaj następujące polecenie uruchamia kontener Nginx lokalne powitania interaktywnie portu 8080, dzięki czemu dane wyjściowe toosee Nginx. Usuwa hello systemem kontenera raz zatrzymana.

```
docker run -it --rm -p 8080:80 nginx
```

Przeglądaj zbyt[adresem http://localhost: 8080](http://localhost:8080) hello tooview systemem kontenera. Zostanie wyświetlony ekran toohello podobne, po jednym.

![Kontener Nginx na komputerze lokalnym](./media/container-registry-get-started-docker-cli/nginx.png)

toostop hello uruchomionych kontenera, naciśnij klawisz [CTRL] + [C].

**3. Utwórz alias obraz powitania w rejestrze**

Witaj następujące polecenie tworzy alias obrazu hello z rejestru tooyour pełną ścieżkę. W tym przykładzie określa hello `samples` bałaganu tooavoid przestrzeni nazw w głównym hello hello rejestru.

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

**4. Wypychanie hello obrazu tooyour rejestru**

```
docker push myregistry.azurecr.io/samples/nginx
```

**5. Obraz powitania ściągnięcia z rejestru**

```
docker pull myregistry.azurecr.io/samples/nginx
```

**6. Uruchom kontener Nginx hello z rejestru**

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

Przeglądaj zbyt[adresem http://localhost: 8080](http://localhost:8080) hello tooview systemem kontenera.

toostop hello uruchomionych kontenera, naciśnij klawisz [CTRL] + [C].

**7. (Opcjonalnie) Usuń obraz powitania**

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a>Limit procesów współbieżnych
W niektórych scenariuszach współbieżne wykonywanie wywołań może powodować błędy. w poniższej tabeli Hello zawiera hello limity jednoczesnych połączeń z operacji "Push" i "Pull" na rejestru kontenera platformy Azure:

| Operacja  | Limit                                  |
| ---------- | -------------------------------------- |
| ŚCIĄGANIE       | Zapasowej too10 równoczesnych ściąga na rejestru |
| WYPYCHANIE       | Zapasowej too5 równoczesnych wypchnięcia na rejestru |

## <a name="next-steps"></a>Następne kroki
Teraz znasz podstawy hello, wszystko jest gotowe toostart za pomocą rejestru! Na przykład rozpocząć wdrażanie kontenera obrazy tooan [usługi kontenera platformy Azure](https://azure.microsoft.com/documentation/services/container-service/) klastra.
