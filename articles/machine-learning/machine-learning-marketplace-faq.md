---
title: "często zadawane pytania — aaa(deprecated) publikowania i korzystać z usługi Machine Learning aplikacji w portalu Azure Marketplace | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Często zadawane pytania dotyczące publikowania aplikacji uczenia maszynowego w hello Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a><span data-ttu-id="b4f50-103">(przestarzałe) Publikowanie i za pomocą uczenia maszynowego aplikacji w portalu Azure Marketplace hello: często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b4f50-103">(deprecated) Publishing and using Machine Learning apps in hello Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="b4f50-104">DataMarket i usług danych jest wycofana i istniejące subskrypcje zostaną wycofane i anulowane uruchamianie 3/31/2017 r.</span><span class="sxs-lookup"><span data-stu-id="b4f50-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="b4f50-105">W związku z tym w tym artykule jest przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="b4f50-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="b4f50-106">Alternatywnie, można opublikować toohello eksperymentów z uczenia maszynowego [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) asysty hello hello danych nauki społeczności.</span><span class="sxs-lookup"><span data-stu-id="b4f50-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="b4f50-107">Aby uzyskać więcej informacji, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="b4f50-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="b4f50-108">Pytania dotyczące Korzystanie z portalu Marketplace</span><span class="sxs-lookup"><span data-stu-id="b4f50-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="b4f50-109">**1. Dlaczego pojawia się następujący komunikat o błędzie po wprowadzić dane wejściowe dla usługi sieci web hello hello:**</span><span class="sxs-lookup"><span data-stu-id="b4f50-109">**1. Why do I get hello following error message after I enter input for hello web service:**</span></span>

<span data-ttu-id="b4f50-110">**Żądanie hello spowodowała zaplecza upłynął limit czasu lub błędu wewnętrznego. zespół Hello bada problem hello. Możemy Przepraszamy za niedogodności hello. (500)**</span><span class="sxs-lookup"><span data-stu-id="b4f50-110">**hello request resulted in a back-end time out or back-end error. hello team is investigating hello issue. We are sorry for hello inconvenience. (500)**</span></span>

<span data-ttu-id="b4f50-111">Twoje parametrów wejściowych może nie być zgodne toohello wymagany format hello internetowych specyficzne dla usługi.</span><span class="sxs-lookup"><span data-stu-id="b4f50-111">Your input parameter(s) may not conform toohello required format for hello specific web service.</span></span> <span data-ttu-id="b4f50-112">Można znaleźć toohello odpowiedniej dokumentacji łącze toofind hello poprawny format dla parametrów wejściowych i ograniczenia hello tej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="b4f50-112">Please refer toohello corresponding documentation link toofind hello correct format for input parameters and hello limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="b4f50-113">**2. Jeśli skopiować łącza hello interfejsu API usługi sieci web hello, które są widoczne na hello strony "Eksploruj ten zestaw danych" i wklej go do innego okna przeglądarki, poświadczeniami, które powinny używać tooaccess hello wyników i jak widać je?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-113">**2. If I copy hello API link for hello web service that I see on hello "Explore this dataset" page and paste it into another browser window, what credentials should I use tooaccess hello results, and how do I see them?**</span></span>

<span data-ttu-id="b4f50-114">Należy używać konta witryny Marketplace jako hello nazwy użytkownika i klucza podstawowego konta hello jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="b4f50-114">You should use your Marketplace account as hello username and hello primary account key as hello password.</span></span> <span data-ttu-id="b4f50-115">klucz podstawowy konta Hello znajduje się na powitania **Eksploruj ten zestaw danych** w obszarze hello opis usługi sieci web hello (kliknij hello **Pokaż** przycisk).</span><span class="sxs-lookup"><span data-stu-id="b4f50-115">hello primary account key can be found on hello **Explore this dataset** page under hello description of hello web service (click hello **show** button).</span></span> <span data-ttu-id="b4f50-116">wynik Hello może być wyświetlany w przeglądarce hello lub może on być dostępny za pobierania, w zależności od przeglądarki, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="b4f50-116">hello result may display in hello browser or it may be available too download, depending on which browser you are using.</span></span>

<span data-ttu-id="b4f50-117">**3. Dlaczego uzyskać powitania po wprowadzić dane wejściowe hello usługi sieci web hello na stronie "Eksploruj ten zestaw danych" hello, następujący komunikat o błędzie:**</span><span class="sxs-lookup"><span data-stu-id="b4f50-117">**3. Why do I get hello following error message after I enter hello input for hello web service on hello "Explore this dataset" page:**</span></span> 

<span data-ttu-id="b4f50-118">**Wystąpił nieoczekiwany błąd podczas przetwarzania żądania. Spróbuj ponownie.**</span><span class="sxs-lookup"><span data-stu-id="b4f50-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="b4f50-119">Jeden lub więcej parametrów wejściowych usługi sieci web została przekroczona limit długości hello przypadku konsumowania usługi sieci web hello w witrynie marketplace hello **Eksploruj ten zestaw danych** strony.</span><span class="sxs-lookup"><span data-stu-id="b4f50-119">One or more input parameters of your web service may have exceeded hello length limit when consuming hello web service on hello marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="b4f50-120">Witaj usługi może być wywołany z już długości danych wejściowych przy użyciu metody POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4f50-120">hello services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="b4f50-121">Aby uzyskać przykłady, zobacz [przykładowe rozwiązania z wykorzystaniem R uczenia maszynowego i opublikowanych tooMarketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="b4f50-121">For examples, see [Sample solutions using R on Machine Learning and published tooMarketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="b4f50-122">**4. Dlaczego nie widzę żadnych czynności w hello "Interfejsu API EKSPLORATORA" kartę int hello magazynu w hello klasycznego portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-122">**4. Why do I not see anything in hello "API EXPLORER" tab int hello Store in hello Azure Classic Portal?**</span></span> 

<span data-ttu-id="b4f50-123">Jest to znany problem dotyczący hello Azure Classic Portal Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b4f50-123">This is a known issue with hello Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="b4f50-124">Witaj zespołu działa tooresolve ten problem.</span><span class="sxs-lookup"><span data-stu-id="b4f50-124">hello team is working tooresolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="b4f50-125">Pytania dotyczące publikowania z usługi Azure Machine Learning w witrynie Marketplace</span><span class="sxs-lookup"><span data-stu-id="b4f50-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="b4f50-126">**1. Dlaczego moja transakcji logo lub obrazów nie są odświeżanie Moje usługi sieci web?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="b4f50-127">Logo i obrazy są buforowane w portalu publikowania hello i może potrwać dni too10 hello nowe logo lub tooupdate obrazu na powitania portalu.</span><span class="sxs-lookup"><span data-stu-id="b4f50-127">Logos and images are cached in hello publishing portal, and it may take up too10 days for hello new logo or image tooupdate on hello portal.</span></span>

<span data-ttu-id="b4f50-128">**2. Dlaczego jest karty "Szczegóły" hello z moją usługę sieci web w witrynie Marketplace przedstawiający komunikat o błędzie?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-128">**2. Why is hello “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="b4f50-129">Istnieje znany problem Marketplace, łącząc tooAzure uczenie maszynowe, aby uzyskać szczegółowe informacje o usłudze.</span><span class="sxs-lookup"><span data-stu-id="b4f50-129">There is a known Marketplace issue when connecting tooAzure Machine Learning for service details.</span></span> <span data-ttu-id="b4f50-130">Witaj zespołu działa tooresolve ten problem.</span><span class="sxs-lookup"><span data-stu-id="b4f50-130">hello team is working tooresolve this issue.</span></span>

<span data-ttu-id="b4f50-131">**3. Dlaczego hello R przykładowy kod w usługach sieci web Azure Machine Learning hello nie działa dla odbierającą hello usług sieci web w witrynie Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-131">**3. Why does hello R sample code in hello Azure Machine Learning web services not work for consuming hello web services in Marketplace?**</span></span>

<span data-ttu-id="b4f50-132">systemami uwierzytelniania Hello są różne, bezpośrednie połączenie usługi sieci web uczenie maszynowe tooAzure względem usługi sieci web toothese tooconnecting za pośrednictwem hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b4f50-132">hello authentication systems are different when connecting tooAzure Machine Learning web services directly compared tooconnecting toothese web services through hello Marketplace.</span></span> <span data-ttu-id="b4f50-133">usługi Hello w witrynie Marketplace są usługi OData i może być wywołana za pomocą metod GET lub POST.</span><span class="sxs-lookup"><span data-stu-id="b4f50-133">hello services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="b4f50-134">**4. Dlaczego są łącza pomocy technicznej hello moją usługę sieci web oferuje nie zostaną zaktualizowane prawidłowo dla niektórych Moje oferty?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-134">**4. Why are hello support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="b4f50-135">łącza pomocy technicznej Hello są globalne na wydawcy, a nie na ofertę.</span><span class="sxs-lookup"><span data-stu-id="b4f50-135">hello support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="b4f50-136">**5. Jak opublikować usługi sieci web za pomocą tryb wprowadzania partii w witrynie Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="b4f50-137">tryb wprowadzania Hello partii nie jest obecnie obsługiwane w portalu Marketplace usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="b4f50-137">hello batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="b4f50-138">**6. Kto I skontaktuj się z tooget pomocy w przypadku pytań dotyczących wydawca danych lub, jeśli mam problemy podczas publikowania?**</span><span class="sxs-lookup"><span data-stu-id="b4f50-138">**6. Who should I contact tooget help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="b4f50-139">Skontaktuj się z zespołem portalu Azure Marketplace hello na < mailto:datamarketbd@microsoft.com > Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b4f50-139">Please contact hello Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

