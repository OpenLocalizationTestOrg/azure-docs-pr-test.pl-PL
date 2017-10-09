---
title: "aaaAzure Functions — Omówienie środowiska uruchomieniowego | Dokumentacja firmy Microsoft"
description: "Omówienie hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Azure Functions — Omówienie środowiska uruchomieniowego

Hello środowisko uruchomieniowe Functions Azure udostępnia nową metodę możesz tootake zaletą hello prostotę i elastyczność hello Azure Functions programowania modelu lokalnego. Oparty na powitania sam Otwórz katalogi główne źródła, zgodnie z usługi Azure Functions, środowisko uruchomieniowe Functions Azure jest niemal identyczne programowanie występują jako usługa w chmurze hello tooprovide wdrożonego na lokalnej.

![Portal w wersji zapoznawczej usługi Azure Functions środowiska wykonawczego][1]

Hello Azure środowisko uruchomieniowe Functions umożliwia dla Ciebie tooexperience usługi Azure Functions przed zatwierdzeniem toohello chmury. W ten sposób zasobów kodu hello tworzonego można podejmowana z chmurą toohello podczas migracji.  środowisko uruchomieniowe Hello otwiera również nowe opcje, takie jak przy użyciu mocy obliczeniowej zapasowe hello procesów partii toorun komputerami lokalnymi noc. Można też używać urządzeń w Twojej organizacji tooconditionally wysyłania tooother systemów danych, zarówno lokalnie, jak i w chmurze hello.

Witaj środowisko uruchomieniowe Functions Azure składa się z dwóch części:
* Rola zarządzania Azure Functions środowiska wykonawczego
* Azure Functions roli procesu roboczego środowiska wykonawczego

## <a name="azure-functions-management-role"></a>Rola zarządzania Azure Functions

Hello Azure funkcje zarządzania roli zawiera hosta do zarządzania hello funkcji lokalnej. Ta rola wykonuje hello następujące zadania:

* Hosting hello funkcje portalu zarządzania Azure, czyli hello hello jednego widoczne w hello [portalu Azure](https://portal.azure.com). Pozwala to utworzyć funkcji w hello sam sposób jak w hello portalu Azure.
* Dystrybucja funkcje na wiele funkcji pracowników.
* Udostępnianie publikowania punktu końcowego, dzięki czemu można opublikować bezpośrednio z funkcji z programu Microsoft Visual Studio.

## <a name="azure-functions-worker-role"></a>Środowisko Azure Functions roli procesu roboczego

Role procesów roboczych funkcji Azure Hello są wdrażane w kontenerach systemu Windows i jest to, gdzie wykonuje kodu funkcji.  Można wdrożyć wiele ról procesów roboczych w całej organizacji i mocy obliczeniowej zapasowych za pomocą klucza sposób, w którym można wprowadzić klientów.

## <a name="minimum-requirements"></a>Minimalne wymagania

tooget wprowadzenie hello Azure środowisko uruchomieniowe Functions musi mieć maszyny z **systemu Windows Server 2016 lub Windows 10 twórców Update** z tooa dostępu **programu SQL Server** wystąpienia.

## <a name="next-steps"></a>Następne kroki

Zainstaluj hello [środowisko uruchomieniowe Functions Azure w wersji zapoznawczej](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
