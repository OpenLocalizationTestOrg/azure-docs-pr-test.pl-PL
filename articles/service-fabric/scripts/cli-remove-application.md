---
title: "Usługa Azure sieci szkieletowej interfejsu wiersza polecenia skryptu Remove próbki"
description: "Usuń aplikację z klastra usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
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
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Usuń aplikację z klastra sieci szkieletowej usług

Ten przykładowy skrypt usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług, wyrejestrowuje typ i wersja aplikacji z klastra.  Usuwanie wystąpienia aplikacji spowoduje również usunięcie wszystkich uruchomionych wystąpień skojarzoną z daną aplikacją usługi. Następnie pliki aplikacji są usuwane z magazynu obrazów. 

Jeśli to konieczne, zainstaluj [interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).

## <a name="sample-script"></a>Przykładowy skrypt

[!code-sh[główne](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "usuwania aplikacji z klastra")]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz [dokumentacji interfejsu wiersza polecenia usługi sieć szkieletowa](../service-fabric-cli.md).

Dodatkowe przykłady interfejsu wiersza polecenia usługi sieci szkieletowej dla sieci szkieletowej usług Azure można znaleźć w [przykłady interfejsu wiersza polecenia usługi sieć szkieletowa](../samples-cli.md).
