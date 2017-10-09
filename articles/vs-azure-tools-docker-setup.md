---
title: Host Docker z VirtualBox aaaConfigure | Dokumentacja firmy Microsoft
description: "Wystąpienie domyślne Docker przy użyciu rozwiązania Docker maszyny i VirtualBox tooconfigure instrukcje krok po kroku"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>Konfigurowanie hosta Docker z VirtualBox
## <a name="overview"></a>Omówienie
W tym artykule przedstawiono Konfigurowanie domyślnego wystąpienia Docker przy użyciu rozwiązania Docker maszyny i VirtualBox. Jeśli używasz hello [Docker dla systemu Windows w wersji beta](http://beta.docker.com/), ta konfiguracja nie jest konieczne.

## <a name="prerequisites"></a>Wymagania wstępne
Witaj następujących narzędzi muszą toobe zainstalowane.

* [Przybornik docker](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Konfigurowanie klienta platformy Docker hello przy użyciu programu Windows PowerShell
po prostu tooconfigure Docker klienta, Otwórz program Windows PowerShell i wykonaj hello następujące kroki:

1. Utwórz wystąpienie domyślne hostów docker.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Sprawdź, czy wystąpienie domyślne hello jest skonfigurowana i uruchomiona. (Powinna zostać wyświetlona wystąpienia o nazwie "default" systemem.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![dane wyjściowe ls maszyny docker][0]
3. Domyślne jako hello bieżącego hosta i konfigurowanie powłoki.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Wyświetlanie hello kontenery usługi active Docker. Lista Hello powinna być pusta.
   
    ```PowerShell
    docker ps
    ```
   
    ![dane wyjściowe ps docker][1]

> [!NOTE]
> Każdym uruchomieniu komputerze deweloperskim, należy toorestart hosta lokalnego docker.
> toodo hello tego problemu, następujące polecenie w wierszu polecenia: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
