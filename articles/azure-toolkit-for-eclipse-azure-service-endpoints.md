---
title: "aaaAzure punktów końcowych usług"
description: "Opisuje ustawienia punktu końcowego usługi Azure hello w hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="fa3b4-103">Punktami końcowymi usług Azure</span><span class="sxs-lookup"><span data-stu-id="fa3b4-103">Azure Service Endpoints</span></span>
<span data-ttu-id="fa3b4-104">Punktami końcowymi usług Azure określają, czy aplikacja jest wdrożony tooand zarządza hello globalne platformy Azure, Azure obsługiwany przez 21Vianet w Chinach lub prywatnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="fa3b4-105">Witaj **punktów końcowych usługi** okno dialogowe pozwala toospecify, który ma toouse punkty końcowe usługi.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="fa3b4-106">tooopen hello **punktów końcowych usługi** okna dialogowego, w programie Eclipse kliknij **okna**, kliknij przycisk **preferencje**, rozwiń węzeł **Azure**, a następnie kliknij przycisk **Punkty końcowe usługi**.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="fa3b4-107">Ustawienie hello **ustawić Active** Określa, w których usługa Azure punktów końcowych, które będą używane dla hello Azure projektów w bieżącym obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="fa3b4-108">Witaj poniżej pokazano hello **punktów końcowych usługi** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="fa3b4-109">punkty końcowe usługi hello tooset</span><span class="sxs-lookup"><span data-stu-id="fa3b4-109">tooset hello service endpoints</span></span>
<span data-ttu-id="fa3b4-110">W hello **punktów końcowych usługi** okno dialogowe, wykonaj jedną z hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="fa3b4-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="fa3b4-111">Jeśli chcesz, aby toouse hello globalne platformy Azure, z hello **ustawić Active** listy rozwijanej wybierz **windowsazure.com** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="fa3b4-112">Jeśli chcesz, aby toouse Azure obsługiwany przez 21Vianet w Chinach, z hello **ustawić Active** listy rozwijanej wybierz **windowsazure.cn (Chiny)** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="fa3b4-113">Jeśli chcesz, aby toouse prywatnej platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="fa3b4-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="fa3b4-114">Kliknij pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="fa3b4-115">Otwiera okno dialogowe informujące, że hello **punktów końcowych usługi** okno dialogowe zostanie zamknięte i hello preferencji ustawia plik zostanie otwarty.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="fa3b4-116">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-116">Click **OK**.</span></span>

  3. <span data-ttu-id="fa3b4-117">W pliku preferencesets.xml hello, Utwórz nową `preferenceset` elementu.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="fa3b4-118">Dla tego nowego elementu tworzenia `name`, `blob`, `management`, `portalURL` i `publishsettings` atrybutów, a następnie dodaj wartości dla nich odpowiadające tooyour prywatnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="fa3b4-119">Możesz użyć wartości hello podany dla istniejących hello `preferenceset` elementów jako szablon.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="fa3b4-120">**Uwaga**: hello wartość używana dla hello `blob` atrybutu musi zawierać tekst hello "blob" w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="fa3b4-121">Zapisz i zamknij preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="fa3b4-122">Otwórz ponownie hello **punktów końcowych usługi** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="fa3b4-123">Z hello **ustawić Active** listy rozwijanej wybierz hello aktywny ustawić utworzone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="fa3b4-124">Po utworzeniu prywatnej platformy Azure `preferenceset` elementu, można zmienić tooit przypisanych wartości hello klikając hello **Edytuj** przycisku na powitania **punktu końcowego usługi** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="fa3b4-125">Można również tworzyć wiele prywatnych platformy Azure `preferenceset` elementy, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="fa3b4-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="fa3b4-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fa3b4-126">See Also</span></span>
<span data-ttu-id="fa3b4-127">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fa3b4-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="fa3b4-128">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fa3b4-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="fa3b4-129">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="fa3b4-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="fa3b4-130">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="fa3b4-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
