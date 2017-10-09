---
title: "toocreate aaaUse 2.0 interfejsu wiersza polecenia aplikacji usługi Azure AD i skonfiguruj ją tooaccess interfejsu API usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toocreate toouse 2.0 interfejsu wiersza polecenia aplikacji usługi Azure AD i skonfiguruj ją tooaccess interfejsu API usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Użyj toocreate 2.0 interfejsu wiersza polecenia aplikacji AAD i skonfiguruj go tooaccess interfejsu API usługi Azure Media Services

W tym temacie pokazano, jak toocreate toouse 2.0 interfejsu wiersza polecenia aplikacji usługi Azure Active Directory (Azure AD) i tooaccess główną usługi Azure Media Services zasobów. 

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Konto usługi Media Services. Aby uzyskać więcej informacji, zobacz [Tworzenie konta usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Użyj hello powłoki chmury Azure

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Uruchom program hello powłoki chmury z hello górnym okienku nawigacji portalu hello.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Cloud powłoki](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Utwórz aplikację usługi Azure AD i skonfiguruj dostęp do konta usługi media toohello 2.0 interfejsu wiersza polecenia
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Na przykład:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

W tym przykładzie hello **zakres** jest ścieżką wszystkich zasobów hello nośnika hello konta usługi. Jednak hello **zakres** może być dowolnym poziomie.

Może to być na przykład jeden z następujących poziomów hello:
 
* Witaj **subskrypcji** poziom.
* Witaj **grupy zasobów** poziom.
* Witaj **zasobów** poziom (na przykład konto nośnika).

Aby uzyskać więcej informacji, zobacz [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Zobacz też [Manage Role-Based kontrola dostępu przy użyciu interfejsu wiersza polecenia platformy Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Następne kroki

Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-portal-upload-files.md).
