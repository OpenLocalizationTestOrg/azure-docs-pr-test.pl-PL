---
title: "kolekcje w chmurze usługi RemoteApp aaaTroubleshoot — tworzenie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy tworzenia kolekcji w chmurze tootroubleshoot programów RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="27ed5-103">Rozwiązywanie problemów z kolekcji usługi RemoteApp tworzenia w chmurze</span><span class="sxs-lookup"><span data-stu-id="27ed5-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="27ed5-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="27ed5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="27ed5-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="27ed5-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="27ed5-106">Jeśli występują problemy z tworzeniem kolekcji w chmurze, zapoznaj się z następujących informacji hello.</span><span class="sxs-lookup"><span data-stu-id="27ed5-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="27ed5-107">Obraz jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="27ed5-107">Your image is invalid</span></span>
<span data-ttu-id="27ed5-108">Jeśli zostanie wyświetlony komunikat, takie jak "GoldImageInvalid" podczas oczekiwania dla usługi Azure tooprovision kolekcji, oznacza to, że obraz szablonu nie spełnia wymagań hello [określone wymagania dotyczące obrazu](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="27ed5-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="27ed5-109">Tak, przejdź do odczytu tych [wymagania](remoteapp-imagereqs.md), Usuń obraz i spróbuj toocreate kolekcji ponownie.</span><span class="sxs-lookup"><span data-stu-id="27ed5-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="27ed5-110">Typowe błędy widoczne w portalu zarządzania Azure hello</span><span class="sxs-lookup"><span data-stu-id="27ed5-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="27ed5-111">Kolekcje w chmurze często błędów podczas tworzenia z powodu możesz korzystają z niestandardowych obrazów.</span><span class="sxs-lookup"><span data-stu-id="27ed5-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="27ed5-112">Jeśli używasz kolekcji hello toocreate niestandardowego obrazu wystąpiła jedna z hello powyżej błędy, sprawdź, czy hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="27ed5-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="27ed5-113">Upewnij się, że obrazu niestandardowego hello przesłanych spełnia wymagania dotyczące obrazu.</span><span class="sxs-lookup"><span data-stu-id="27ed5-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="27ed5-114">W większości przypadków hello powszechny problem jest ten obraz powitania nie została prawidłowo przetworzonej przez program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="27ed5-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="27ed5-115">Sprawdź obraz powitania można uruchomić w ramach funkcji Hyper-V lub spróbuj utworzyć maszyn wirtualnych IAAS bezpośrednio w Twojej subskrypcji platformy Azure przy użyciu obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="27ed5-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="27ed5-116">Jeśli hello maszyny Wirtualnej nie powiedzie się tooboot i nie start, a następnie zwykle oznacza to, że danego hello niestandardowego obrazu nie został poprawnie przygotowany.</span><span class="sxs-lookup"><span data-stu-id="27ed5-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="27ed5-117">Sprawdź, czy hello niestandardowy obraz został utworzony po hello jak toocreate szablonu niestandardowego obrazu usługi RemoteApp</span><span class="sxs-lookup"><span data-stu-id="27ed5-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="27ed5-118">Jeśli korzystasz z jednego z obrazów Microsoft hello uwzględnionych w subskrypcji, spróbuj ponownie toocreate hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="27ed5-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="27ed5-119">Jeśli hello problem będzie się powtarzać, skontaktuj się pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27ed5-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="27ed5-120">Jeśli zostanie wyświetlony błąd ten zwykle oznacza to, który został uaktualniony tooa płatne konto, lecz próbujesz toouse obrazu firmę Microsoft, który jest prawidłowy tylko w trakcie hello trybu wersji próbnej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="27ed5-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="27ed5-121">W takim przypadku spróbuj toocreate ponownie kolekcji chmury, ale można się toospecify hello prawidłowy obraz.</span><span class="sxs-lookup"><span data-stu-id="27ed5-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

