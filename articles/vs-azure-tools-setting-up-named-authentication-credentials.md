---
title: "aaaSetting się poświadczenia uwierzytelniania o nazwie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa w chmurze programu Visual Studio za pomocą tooauthenticate żądań tooAzure toopublish tooAzure aplikacji z programu Visual Studio lub toomonitor istniejących poświadczeń tootooprovide... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="02e85-103">Konfigurowanie poświadczeń uwierzytelniania o nazwie</span><span class="sxs-lookup"><span data-stu-id="02e85-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="02e85-104">toopublish tooAzure aplikacji z programu Visual Studio lub toomonitor istniejącej usługi chmury, musisz podać poświadczenia programu Visual Studio za pomocą tooauthenticate żądań tooAzure.</span><span class="sxs-lookup"><span data-stu-id="02e85-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="02e85-105">Istnieje kilka obszarów w programie Visual Studio, w którym można zalogować się tooprovide te poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="02e85-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="02e85-106">Na przykład z hello Eksploratora serwera, możesz otworzyć menu skrótów hello hello **Azure** węzeł i wybierz polecenie **połączyć tooMicrosoft subskrypcji platformy Azure...** . Po zalogowaniu, hello informacji o subskrypcji skojarzonych z Twoim kontem platformy Azure jest dostępna w programie Visual Studio i nie ma nic więcej masz toodo.</span><span class="sxs-lookup"><span data-stu-id="02e85-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="02e85-107">Narzędzia platformy Azure obsługuje również starsze sposób podawania poświadczeń, przy użyciu hello subskrypcji (plik .publishsettings).</span><span class="sxs-lookup"><span data-stu-id="02e85-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="02e85-108">W tym temacie opisano metody nadal jest obsługiwany w 2.2 zestawu SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02e85-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="02e85-109">Witaj, następujące elementy są wymagane dla tooAzure uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="02e85-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="02e85-110">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="02e85-110">Your subscription ID</span></span>
* <span data-ttu-id="02e85-111">Prawidłowy certyfikat X.509 v3</span><span class="sxs-lookup"><span data-stu-id="02e85-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="02e85-112">Hello długość klucza certyfikatu X.509 v3 hello musi wynosić co najmniej 2048 bitów.</span><span class="sxs-lookup"><span data-stu-id="02e85-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="02e85-113">Azure spowoduje odrzucenie dowolny certyfikat, który nie spełnia tego wymagania lub nie jest prawidłowa.</span><span class="sxs-lookup"><span data-stu-id="02e85-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="02e85-114">Visual Studio będzie korzystać identyfikator subskrypcji oraz hello dane certyfikatu jako poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="02e85-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="02e85-115">odwołuje się hello subskrypcji (plik .publishsettings), który zawiera klucz publiczny certyfikatu hello Hello odpowiednie poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="02e85-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="02e85-116">Witaj subskrypcji plik może zawierać poświadczeń dla więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="02e85-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="02e85-117">Można edytować hello informacji o subskrypcji z hello **subskrypcji nowy i edytować** okno dialogowe, zgodnie z objaśnieniem w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="02e85-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="02e85-118">Chcesz toocreate certyfikatu samodzielnie, mogą odwoływać się instrukcjami toohello [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) , a następnie ręcznie przekazać toohello certyfikatu hello [klasycznego portalu Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="02e85-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="02e85-119">Te poświadczenia, które program Visual Studio wymaga toomanage, które nie są usługi w chmurze hello tych samych poświadczeń, które są wymagane tooauthenticate Żądanie hello usług magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02e85-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="02e85-120">Importuj, konfigurowanie lub edytowanie poświadczeń uwierzytelniania w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02e85-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="02e85-121">Można importować, skonfigurować lub zmodyfikować poświadczenia uwierzytelniania w hello **nową subskrypcję** okno dialogowe, które pojawia się po wykonaniu hello następujące działania:</span><span class="sxs-lookup"><span data-stu-id="02e85-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="02e85-122">W **Eksploratora serwera**, otwórz menu skrótów hello hello **Azure** węzła, wybierz **zarządzanie i subskrypcje filtru...** , wybierz hello **certyfikaty** , a następnie wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="02e85-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="02e85-123">Wybierz **zaimportować** dialogowe Importuj subskrypcji platformy Microsoft Azure hello tooopen której można pobrać pliku subskrypcje hello hello aktualnie załadowany subskrypcji, tooits przeglądania Lokalizacja pobierania, a następnie zaimportuj go do użycia w uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="02e85-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="02e85-124">Wybierz **nowy** tooopen hello nową subskrypcję okno, której można skonfigurować nowej subskrypcji do użytku podczas uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="02e85-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="02e85-125">Wybierz **Edytuj** (po wybraniu subskrypcji active) tooopen: hello okna dialogowego Edytowanie subskrypcji którym można edytować istniejącą subskrypcję do użycia w przypadku uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="02e85-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="02e85-126">Witaj poniższej procedurze przyjęto, że hello **nową subskrypcję** jest otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="02e85-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="02e85-127">tooset się poświadczenia uwierzytelniania w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02e85-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="02e85-128">W hello **wybierz istniejący certyfikat** dla listy uwierzytelniania należy wybrać certyfikat.</span><span class="sxs-lookup"><span data-stu-id="02e85-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="02e85-129">Wybierz hello **Kopiuj hello pełną ścieżkę** łącza.</span><span class="sxs-lookup"><span data-stu-id="02e85-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="02e85-130">Ścieżka Hello hello certyfikatu (pliku cer) jest skopiowany toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="02e85-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="02e85-131">toopublish aplikacji platformy Azure z programu Visual Studio, możesz przekazać ten toohello certyfikatu [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02e85-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="02e85-132">tooupload hello certyfikatu toohello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="02e85-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="02e85-133">Otwórz hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02e85-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="02e85-134">W przypadku wyświetlenia monitu zaloguj się w portalu toohello, a następnie przejdź zbyt**ustawienia**, **certyfikaty zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="02e85-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="02e85-135">W okienku certyfikatów zarządzania hello, wybierz **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="02e85-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="02e85-136">Wybierz subskrypcję platformy Azure, Wklej hello pełną ścieżkę pliku .cer hello, który został właśnie utworzony, a następnie wybierz **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="02e85-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
