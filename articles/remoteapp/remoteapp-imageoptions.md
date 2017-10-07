---
title: "aaaCreate obrazu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat opcji hello dostępnych do tworzenia obrazów dla usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Tworzenie obrazu usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp używa aplikacji hello toohold obrazów, które możesz udostępniać użytkownikom. (Firma Microsoft podejmie obrazu i jego maszyn wirtualnych toocreate — które co hello użytkownicy uzyskują dostęp do podczas logowania się do usługi Azure RemoteApp.) toocreate kolekcji usługi Azure RemoteApp przy użyciu wybranych aplikacji, czy jest w chmurze czy hybrydowa, rozpoczyna się od utworzenia obrazu z tymi aplikacjami zainstalowane. Następnie utwórz kolekcję, która używa tego obrazu, Przypisz użytkowników toohello kolekcji i publikowanie aplikacji toothose użytkowników.

Istnieje kilka opcji tworzenia i używania obrazów. podstawowe Hello [wymaganie](remoteapp-imagereqs.md) obrazu jest uruchomiony system Windows Server 2012 R2 i zainstalowaną rolą zdalnego pulpitu sesji hosta hello. Jak wprowadzasz się, że jest, gdzie interesujący rzeczy.

Dostępne są następujące opcje, jeśli chodzi tooimages hello:

* Mogą być importowane i używane [na maszynie wirtualnej platformy Azure opartej na obrazie](remoteapp-image-on-azurevm.md). Jest to dobra dla aplikacji z biznesowych, które wymagają ustawienia niestandardowe. Można dostosować hello toowork obrazu dla aplikacji hello.
* Możesz [tworzenie i przekazywanie obrazu niestandardowego](remoteapp-create-custom-image.md). Jest to dobry, jeśli masz już obrazu używanego do lokalnego wdrożenia usług pulpitu zdalnego.
* Można użyć jednej z hello [obrazy szablonów](remoteapp-images.md) zawarte w ramach subskrypcji usługi RemoteApp. Te obrazy są tworzone i obsługiwane przez zespół usługi RemoteApp hello i zawiera kilka standardowych aplikacji (takich jak pakiet Office hello) ułatwia użytkownikom tooyour dostępne. Należy zauważyć, że tylko pakiet Office 365 Pro Plus obrazu hello mogą być używane w środowisku produkcyjnym.

Niezależnie od tego, gdzie znaleźć obrazu lub sposób tworzenia, należy się zapoznać hello toomake [wymagania dotyczące aplikacji](remoteapp-appreqs.md) tooensure, że aplikacja działa dobrze w programów RemoteApp. Następnie, następnym krokiem hello jest toocreate [chmury](remoteapp-create-cloud-deployment.md) lub [hybrydowego](remoteapp-create-hybrid-deployment.md) kolekcji.

