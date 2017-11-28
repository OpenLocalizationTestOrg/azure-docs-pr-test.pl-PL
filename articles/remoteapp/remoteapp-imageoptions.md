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
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="bd2bf-103">Tworzenie obrazu usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bd2bf-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bd2bf-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bd2bf-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bd2bf-106">Usługa Azure RemoteApp używa aplikacji hello toohold obrazów, które możesz udostępniać użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="bd2bf-107">(Firma Microsoft podejmie obrazu i jego maszyn wirtualnych toocreate — które co hello użytkownicy uzyskują dostęp do podczas logowania się do usługi Azure RemoteApp.) toocreate kolekcji usługi Azure RemoteApp przy użyciu wybranych aplikacji, czy jest w chmurze czy hybrydowa, rozpoczyna się od utworzenia obrazu z tymi aplikacjami zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="bd2bf-108">Następnie utwórz kolekcję, która używa tego obrazu, Przypisz użytkowników toohello kolekcji i publikowanie aplikacji toothose użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="bd2bf-109">Istnieje kilka opcji tworzenia i używania obrazów.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-109">You have several options for creating or using images.</span></span> <span data-ttu-id="bd2bf-110">podstawowe Hello [wymaganie](remoteapp-imagereqs.md) obrazu jest uruchomiony system Windows Server 2012 R2 i zainstalowaną rolą zdalnego pulpitu sesji hosta hello.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="bd2bf-111">Jak wprowadzasz się, że jest, gdzie interesujący rzeczy.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="bd2bf-112">Dostępne są następujące opcje, jeśli chodzi tooimages hello:</span><span class="sxs-lookup"><span data-stu-id="bd2bf-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="bd2bf-113">Mogą być importowane i używane [na maszynie wirtualnej platformy Azure opartej na obrazie](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="bd2bf-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="bd2bf-114">Jest to dobra dla aplikacji z biznesowych, które wymagają ustawienia niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="bd2bf-115">Można dostosować hello toowork obrazu dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="bd2bf-116">Możesz [tworzenie i przekazywanie obrazu niestandardowego](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="bd2bf-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="bd2bf-117">Jest to dobry, jeśli masz już obrazu używanego do lokalnego wdrożenia usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="bd2bf-118">Można użyć jednej z hello [obrazy szablonów](remoteapp-images.md) zawarte w ramach subskrypcji usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="bd2bf-119">Te obrazy są tworzone i obsługiwane przez zespół usługi RemoteApp hello i zawiera kilka standardowych aplikacji (takich jak pakiet Office hello) ułatwia użytkownikom tooyour dostępne.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="bd2bf-120">Należy zauważyć, że tylko pakiet Office 365 Pro Plus obrazu hello mogą być używane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="bd2bf-121">Niezależnie od tego, gdzie znaleźć obrazu lub sposób tworzenia, należy się zapoznać hello toomake [wymagania dotyczące aplikacji](remoteapp-appreqs.md) tooensure, że aplikacja działa dobrze w programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="bd2bf-122">Następnie, następnym krokiem hello jest toocreate [chmury](remoteapp-create-cloud-deployment.md) lub [hybrydowego](remoteapp-create-hybrid-deployment.md) kolekcji.</span><span class="sxs-lookup"><span data-stu-id="bd2bf-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

