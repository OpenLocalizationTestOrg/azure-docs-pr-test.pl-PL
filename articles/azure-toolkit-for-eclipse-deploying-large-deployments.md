---
title: "aaaDeploying dużych wdrożeń"
description: "Dowiedz się, jak toodeploy dużych wdrożeń za pomocą hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="23166-103">Wdrażanie dużych wdrożeń</span><span class="sxs-lookup"><span data-stu-id="23166-103">Deploying Large Deployments</span></span>
<span data-ttu-id="23166-104">Wdrożenie jest zbyt duży toobe znajdujące się w folderze approot domyślne hello, można użyć zasobów magazynu lokalnego jako folder główny wdrożenia hello, dla Twojej JDK i serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23166-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="23166-105">toouse zasobu magazynu lokalnego jako folder główny wdrożenia hello w przypadku dużych wdrożeń</span><span class="sxs-lookup"><span data-stu-id="23166-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="23166-106">Tworzenie nowego zasobu magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="23166-106">Create a new local storage resource.</span></span> <span data-ttu-id="23166-107">Nazwa Hello hello zasobu nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="23166-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="23166-108">Zasoby magazynu są definiowane na poziomie roli hello.</span><span class="sxs-lookup"><span data-stu-id="23166-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="23166-109">Witaj najszybszy sposób tooaccess hello Magazyn lokalny okna dialogowego konfiguracji, w którym można utworzyć nowego zasobu lokalnego magazynu polega na użyciu hello następujące kroki: kliknij prawym przyciskiem myszy rolę hello w hello **Eksplorator projektów** widoku (rozwiń węzeł sieci Azure węzła projektu, jeśli nie widzisz roli hello), kliknij przycisk **Azure**, a następnie kliknij przycisk **Magazyn lokalny**.</span><span class="sxs-lookup"><span data-stu-id="23166-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="23166-110">W ramach hello **Magazyn lokalny** okna dialogowego, kliknij przycisk **Dodaj** toocreate nowego zasobu magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="23166-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="23166-111">Witaj zestaw żądaną tooat rozmiar co najmniej 2048 MB (niczego mniej może powodować hello takie same problemy rozmiar pliku, ponieważ może wystąpić w hello approot).</span><span class="sxs-lookup"><span data-stu-id="23166-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="23166-112">Upewnij się, że **wyczyścić zawartość hello podczas odtwarzania wystąpienia roli hello** zaznaczono; może to pomóc w zabezpieczeniu Logika uruchamiania wdrożenia hello z systemem Windows powoduje konflikt z istniejące pliki w zasobie hello po hello roli wystąpienie zostanie odtworzony.</span><span class="sxs-lookup"><span data-stu-id="23166-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="23166-113">Upewnij się, że hello **przechowywania zmiennych środowiska hello ścieżki katalogu zasobu po wdrożeniu** wartość ciągu toohello **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="23166-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="23166-114">Twoje okno dialogowe zasobu lokalnego magazynu będzie wyglądać podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="23166-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="23166-115">Alternatywnie Jeśli używasz **DEPLOYROOT** jako hello *nazwa* zasobu lokalnego, a nie należy zmieniać nazwę zmiennej środowiskowej generowane automatycznie hello (której będzie można ustawić za **DEPLOYROOT_PATH** w takim przypadku), który będzie działać również aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23166-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="23166-116">Dodatkowe informacje na temat tworzenia zasobu lokalnego magazynu można znaleźć w folderze [właściwości magazynu lokalnego][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="23166-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="23166-117">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="23166-117">See Also</span></span>
<span data-ttu-id="23166-118">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="23166-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="23166-119">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="23166-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="23166-120">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="23166-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="23166-121">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="23166-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
