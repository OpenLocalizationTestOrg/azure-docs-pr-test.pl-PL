---
title: "toodeploy aaaHow usługi sieci Web regionów toomultiple | Dokumentacja firmy Microsoft"
description: "Kroki toodeploy (Kopiuj) regionów tooother nową usługę sieci Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Jak toodeploy usługi sieci Web toomultiple regionów
Hello nowych usług sieci Web Azure pozwala tooeasily wdrażanie regiony toomultiple usługi sieci web bez konieczności wielu subskrypcji lub obszarów roboczych. 

Cennik jest określone, dlatego należy zdefiniować plan rozliczeniowy dla każdego regionu, w którym zostanie wdrożona usługa sieci web hello regionu.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate planu w innym regionie
1. Zaloguj się do [platformy Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).
2. Kliknij przycisk hello **plany** opcji menu.
3. W planie hello za pośrednictwem widoku strony, kliknij przycisk **nowy**.
4. Z hello **subskrypcji** listy rozwijanej wybierz hello subskrypcji w hello, które będą znajdować się nowy plan.
5. Z hello **Region** listy rozwijanej wybierz region hello nowego planu. Witaj opcje planowania dla wybranego regionu hello będą wyświetlane na powitania **opcje planowania** sekcji hello strony.
6. Z hello **grupy zasobów** listy rozwijanej wybierz zasób grupy hello planu. Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. W **Nazwa planu** Nazwa typu hello hello planu.
8. W obszarze **opcje planu**, kliknij przycisk Poziom rozliczeń hello hello nowego planu.
9. Kliknij przycisk **Utwórz**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Wdrażanie region tooanother usługi sieci web hello
1. Kliknij przycisk hello **usług sieci Web** opcji menu.
2. Wybierz hello wdrażasz nowego regionu tooa usługi sieci Web.
3. Kliknij przycisk **kopiowania**.
4. W **nazwę usługi sieci Web**, wpisz nową nazwę dla usługi sieci web hello.
5. W **sieci Web opisu usługi**, wpisz opis hello usługi sieci web.
6. Z hello **subskrypcji** listy rozwijanej wybierz hello subskrypcji, w których hello nową usługę sieci web będzie znajdować się.
7. Z hello **grupy zasobów** listy rozwijanej wybierz zasób grupy dla usługi sieci web hello. Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Z hello **Region** listy rozwijanej wybierz hello region usługi sieci web, która hello toodeploy.
9. Z hello **konta magazynu** listy rozwijanej, wybierz konto magazynu, w którym hello toostore usługi sieci web.
10. Z hello **planu cen** listy rozwijanej wybierz plan w regionie hello wybranej w kroku 8.
11. Kliknij przycisk **kopiowania**.

