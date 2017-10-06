---
title: "aaaDisplaying Javadoc zawartości w programie Eclipse dla hello pakietu biblioteki Azure dla języka Java"
description: "Jak toodisplay hello Javadoc zawartości dla biblioteki Azure hello w środowisku Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="b6ea9-103">Wyświetlanie zawartości Javadoc w środowisku Eclipse hello pakietu biblioteki Azure dla języka Java</span><span class="sxs-lookup"><span data-stu-id="b6ea9-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="b6ea9-104">Witaj Javadoc zawartość hello biblioteki Azure dla języka Java można wyświetlić w środowisku Eclipse kojarząc hello Javadoc zawartości toohello biblioteki Azure dla języka Java.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="b6ea9-105">Witaj poniższej procedurze pokazano, jak toouse tę funkcję w środowisku Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="b6ea9-106">W tej procedurze przyjęto założenie, że dodano już hello biblioteki Azure dla ścieżki kompilacji tooyour Java.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="b6ea9-107">toodisplay Javadoc zawartość w programie Eclipse hello biblioteki Azure dla języka Java</span><span class="sxs-lookup"><span data-stu-id="b6ea9-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="b6ea9-108">W środowisku Eclipse w Eksploratorze projektu w hello **odwołuje się do bibliotek** hello Otwórz menu kontekstowe dla hello biblioteki Azure dla programu Java JAR, sekcji projektu.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="b6ea9-109">Na przykład **microsoft-windowsazure-api-0.1.0.jar** (numer wersji hello mogą być różne, w zależności od wersji zainstalowane).</span><span class="sxs-lookup"><span data-stu-id="b6ea9-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="b6ea9-110">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-110">Click **Properties**.</span></span>

* <span data-ttu-id="b6ea9-111">W ramach hello **właściwości** okna dialogowego, w okienku po lewej stronie powitania kliknij **lokalizacji Javadoc**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="b6ea9-112">Witaj **lokalizacji Javadoc** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="b6ea9-113">Można określić **Javadoc URL**, lub **Javadoc w archiwum**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="b6ea9-114">Jeśli wybierzesz toospecify **Javadoc URL**, takich jak używać adresów URL hello **http://dl.windowsazure.com/javadoc** lub **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="b6ea9-115">Jeśli wybierzesz toouse **Javadoc w archiwum**, można określić plik lub pliku obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="b6ea9-116">Wybierz ustawienia i przeglądania/sprawdzanie poprawności stosownie do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="b6ea9-117">Witaj poniższy przykład kojarzy hello biblioteki Azure dla języka Java z hello odpowiedniego Javadoc JAR której pobierana lokalnie tooa folder o nazwie **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="b6ea9-118">*Krok opcjonalny*: kliknij **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="b6ea9-119">Potencjalne problemy z hello Javadoc JAR mogą być wyświetlone tutaj.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="b6ea9-120">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-120">Click **OK**.</span></span>

<span data-ttu-id="b6ea9-121">Po skojarzonych z biblioteką hello, hello zawartości Javadoc powinien być wyświetlany w środowiskiem Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="b6ea9-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="b6ea9-122">Na przykład jeśli `blob` zdefiniowano typu `CloudBlockBlob` w kodzie, hello poniżej przedstawiono przykład Javadoc zawartość, która pojawia się po wpisaniu `blob.acquireLease` w kodzie:</span><span class="sxs-lookup"><span data-stu-id="b6ea9-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="b6ea9-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b6ea9-123">See Also</span></span>
<span data-ttu-id="b6ea9-124">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6ea9-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="b6ea9-125">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6ea9-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="b6ea9-126">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6ea9-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="b6ea9-127">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="b6ea9-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
