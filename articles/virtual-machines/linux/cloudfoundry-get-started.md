---
title: aaaGetting Started with Foundry chmury w systemie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Uruchom OSS lub Foundry kluczową chmurze na platformie Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Usługa Cloud Foundry na platformie Azure

Foundry chmury jest open source platformy jako — usługa (PaaS) dotyczące tworzenia, wdrażania i obsługi 12-factor aplikacji utworzonych w różnych języków i struktur. W tym dokumencie opisano opcje hello masz zasilany Foundry chmury Azure i jak możesz rozpocząć pracę.

## <a name="cloud-foundry-offerings"></a>Foundry oferty usług w chmurze

Istnieją dwie formy toorun dostępne Foundry chmurze na platformie Azure: chmury Foundry (OSS CF) i kluczową chmury Foundry (PCF) open source. OSS CF jest całkowicie [open source](https://github.com/cloudfoundry) wersji Foundry chmury zarządza hello Foundation Foundry chmury. Kluczową Foundry chmury jest dystrybucja enterprise Foundry chmury z kluczową Inc. oprogramowania Przyjrzymy się niektóre hello różnice między Witaj dwie oferty.

### <a name="open-source-cloud-foundry"></a>Chmura open source Foundry

Można wdrożyć OSS Foundry chmury Azure najpierw wdrażanie Dyrektor BOSH, a następnie wdrażanie Foundry chmury, za pomocą hello [instrukcje podane w serwisie GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn więcej informacji o użyciu CF systemów operacyjnych, zobacz hello [dokumentacji](https://docs.cloudfoundry.org/) podał hello Foundation Foundry chmury.

Firma Microsoft udostępnia optymalnych obsługę OSS CF za pośrednictwem następujących kanałów społeczności hello:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>kanał bosh-azure-cpi na [Slack Foundry chmury](https://slack.cloudfoundry.org/)
- [listy adresowej CF bosh](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Problemy z usługi GitHub hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) i [programu service broker](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> Witaj poziom obsługi zasobów platformy Azure, takich jak maszyny wirtualne hello realizującym Foundry chmury opiera się na umowie pomocy technicznej platformy Azure. Obsługa społeczności optymalnych dotyczy tylko składniki toohello Foundry specyficzne dla chmury.

### <a name="pivotal-cloud-foundry"></a>Kluczową chmury Foundry

Kluczową Foundry chmury obejmuje hello tej samej podstawowej platformy jako dystrybucji hello OSS, wraz z zestawem narzędzi do zarządzania zastrzeżonych i pomocy technicznej enterprise. toorun PCF na platformie Azure, w przypadku uzyskania licencji z Pivotal. Oferta PCF Hello z hello Azure marketplace zawiera 90-dniowy licencja próbna.

narzędzia Hello obejmują [kluczową programu Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), aplikacji sieci web, które upraszcza wdrażanie i zarządzanie foundation Foundry chmury, a [kluczową Menedżera aplikacji](https://docs.pivotal.io/pivotalcf/console/), aplikacji sieci web do zarządzania Użytkownicy i aplikacje.

Ponadto wymienione powyżej CF OSS kanałów pomocy technicznej toohello, licencji PCF uprawnia możesz toocontact Pivotal pomocy technicznej. Microsoft Pivotal również włączono obsługę przepływy pracy, które pozwalają toocontact każdą stronę pomocy i mieć Twojego zapytania kierowane odpowiednio w zależności od tego, gdzie znajduje się problem hello.

## <a name="azure-service-broker"></a>Broker usług Azure

Chmura Foundry zachęca hello ["12 factor aplikacja"](https://12factor.net/) metodologii, która wspiera czyste rozdzielenie procesów aplikacji bezstanowych i stateful kopii usług. [Usługa brokerzy](https://docs.cloudfoundry.org/services/api.html) oferować tooprovision spójny sposób i powiązać tooapplications usługi tworzenia kopii. Witaj [brokera usług Azure](https://github.com/Azure/meta-azure-service-broker) zawiera niektóre z hello klucza usługi Azure za pośrednictwem tego kanału, w tym magazynu Azure i Azure SQL.

Jeśli używasz kluczową Foundry chmury programu service broker hello jest również [dostępne jako Kafelek](https://docs.pivotal.io/azure-sb/installing.html) z hello kluczową sieci.

## <a name="related-resources"></a>Powiązane zasoby

### <a name="visual-studio-team-services-plugin"></a>Visual Studio Team Services wtyczki

Foundry chmury jest rozwoju oprogramowania dobrze nadają się tooagile, włączając stosowania hello ciągłej integracji (CI) i ciągłego dostarczania (CD). Jeśli używasz programu Visual Studio Team Services (VSTS) toomanage swoje projekty i chcesz tooset się potoku CI/CD przeznaczonych dla Foundry chmury, można użyć hello [rozszerzenie kompilacji programu VSTS chmury Foundry](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). Hello wtyczki powoduje tooconfigure proste i zautomatyzować wdrożeń tooCloud Foundry, czy uruchomione w Azure lub w innym środowisku.

## <a name="next-steps"></a>Następne kroki

- [Wdrażanie kluczową Foundry chmury z hello Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Wdrażanie aplikacji tooCloud Foundry na platformie Azure](./cloudfoundry-deploy-your-first-app.md)
