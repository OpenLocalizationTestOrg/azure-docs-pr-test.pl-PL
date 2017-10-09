---
title: "aaaAzure przykład usługi sieci szkieletowej interfejsu wiersza polecenia skryptu wdrażania"
description: "Wdrażanie klastra usługi sieć szkieletowa usług Azure tooan dla aplikacji przy użyciu hello Azure Service Fabric interfejsu wiersza polecenia"
services: service-fabric
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Wdrażanie klastra usługi sieć szkieletowa tooa aplikacji

Ten przykładowy skrypt kopiuje pakiet tooa klastra obrazu sklepu z aplikacjami, rejestruje typ aplikacji hello w klastrze hello i tworzy wystąpienie aplikacji na podstawie typu aplikacji hello. Wszystkie usługi domyślne są również tworzone w tym momencie.

Jeśli to konieczne, zainstaluj hello [interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).

## <a name="sample-script"></a>Przykładowy skrypt

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po zakończeniu hello [Usuń](cli-remove-application.md) skryptu może być używane tooremove hello aplikacji. skryptu remove Hello usuwa wystąpienie aplikacji hello wyrejestrowuje typ aplikacji hello i usuwa pakiet aplikacji hello z magazynu obrazów.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz hello [dokumentacji interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).

Dodatkowe przykłady interfejsu wiersza polecenia usługi sieci szkieletowej dla sieci szkieletowej usług Azure można znaleźć w hello [przykłady interfejsu wiersza polecenia usługi sieć szkieletowa](../samples-cli.md).
