---
title: "aaaAzure próbki interfejsu wiersza polecenia — usługi App Service | Dokumentacja firmy Microsoft"
description: "Przykłady Azure CLI - usługi aplikacji"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Przykłady Azure CLI

Witaj Poniższa tabela zawiera linki toobash skrypty utworzone przy użyciu interfejsu wiersza polecenia Azure hello.

| | |
|-|-|
|**Tworzenie aplikacji**||
| [Tworzenie aplikacji sieci Web i wdrażanie kodu z usługi GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzenie aplikacji sieci web platformy Azure i wdraża kod z publicznego repozytorium GitHub. |
| [Tworzenie aplikacji sieci Web z ciągłym wdrażania z usługi GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzy aplikację sieci web platformy Azure z publikowaniem ciągłego z repozytorium GitHub użytkownika. |
| [Tworzenie aplikacji sieci Web i wdrażanie kodu z lokalnego repozytorium Git](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzenie aplikacji sieci web platformy Azure i konfiguruje wypychania kodu z lokalnego repozytorium Git. |
| [Tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy aplikację sieci web platformy Azure z miejscem wdrożenia, do przemieszczania zmian w kodzie. |
| [Tworzenie aplikacji sieci Web ASP.NET Core w kontenerze platformy Docker](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzenie aplikacji sieci web platformy Azure w systemie Linux i ładuje obraz Docker z Centrum Docker. |
|**Konfigurowanie aplikacji**||
| [Mapa aplikacji sieci web tooa domeny niestandardowej](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzenie aplikacji sieci web platformy Azure, a następnie mapuje tooit nazwy domeny niestandardowej. |
| [Powiąż niestandardowej aplikacji sieci web tooa certyfikat protokołu SSL](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzenie aplikacji sieci web platformy Azure i powiązanie certyfikatu SSL hello tooit nazwy domeny niestandardowej. |
|**Skalowanie aplikacji**||
| [Ręczne skalowanie aplikacji sieci Web](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzenie aplikacji sieci web platformy Azure i skaluje go w wystąpieniach 2. |
| [Skalowanie aplikacji sieci Web na całym świecie przy użyciu architektury wysokiej dostępności](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy dwie aplikacje sieci web platformy Azure w dwóch różnych regionach geograficznych i udostępnia je poprzez jeden punkt końcowy za pomocą usługi Azure Traffic Manager. |
|**Połącz tooresources aplikacji**||
| [Połącz tooa aplikacji sieci web bazy danych SQL](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzy aplikację sieci web platformy Azure i bazy danych SQL, a następnie dodaje ustawień aplikacji toohello parametrów połączenia hello bazy danych. |
| [Połącz z kontem magazynu tooa aplikacji sieci web](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Tworzy aplikację sieci web platformy Azure i konto magazynu, a następnie dodaje ustawień aplikacji toohello parametrów połączenia magazynu hello. |
| [Połączenie pamięci podręcznej redis tooa aplikacji sieci web](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy aplikację sieci web platformy Azure i pamięci podręcznej redis, a następnie dodaje ustawień aplikacji hello redis połączenia szczegóły toohello.) |
| [Połącz tooCosmos aplikacji sieci web bazy danych](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy aplikację sieci web platformy Azure i DB rozwiązania Cosmos, a następnie dodaje ustawień aplikacji toohello szczegóły połączenia hello DB rozwiązania Cosmos. |
|**Monitoruj aplikację**||
| [Monitorowanie aplikacji sieci Web za pomocą dzienników serwera sieci Web](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzenie aplikacji sieci web platformy Azure, włączenie rejestrowania dla niego i pobiera maszyny lokalne powitania dzienniki tooyour. |
| | |