---
title: "aaaMove zasobów aplikacji sieci Web tooanother grupy zasobów"
description: "Opisano scenariusze hello, których można przenosić aplikacje sieci Web i aplikacji usługi z jednym tooanother grupy zasobów."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>Przenieś obsługiwane konfiguracje
Można przenieść zasobów aplikacji sieci Web platformy Azure przy użyciu hello [API zasobów Przenieś Menedżera zasobów](../azure-resource-manager/resource-group-move-resources.md).

Aplikacje sieci Web platformy Azure obsługuje obecnie następujące scenariusze przenoszenia hello:

* Przenieś hello całą zawartość grupy zasobów (aplikacje sieci web, planów usługi aplikacji i certyfikaty) tooanother grupy zasobów. 
   > [!Note]
   > Grupa zasobów Hello docelowego nie może zawierać żadnych zasobów Microsoft.Web w tym scenariuszu.

* Przenieś poszczególnych sieci web apps tooa innej grupie zasobów, podczas nadal hosting je w ich bieżący plan usługi app service (hello aplikacji usługi plan pozostaje w grupie zasobów starego hello).


