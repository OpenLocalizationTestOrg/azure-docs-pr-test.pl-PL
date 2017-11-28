---
title: "aaaSet się i użyj hello Machine Learning API zalecenia | Dokumentacja firmy Microsoft"
description: "Interfejs API zalecenia Microsoft skompilowanej za pomocą usługi Azure Machine Learning — często zadawane pytania"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="389d1-103">Konfigurowanie i używanie interfejsu API zaleceń usługi Machine Learning — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="389d1-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="389d1-104">**Co to jest zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="389d1-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="389d1-105">Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="389d1-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="389d1-106">Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="389d1-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="389d1-107">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="389d1-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="389d1-108">Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="389d1-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="389d1-109">W przypadku organizacji i firm, które opierają się na sprzedaży toocross zalecenia i sprzedaje up produktów i usług tootheir klientów zalecenia w usłudze Azure Machine Learning zapewnia aparat samoobsługi zalecenia.</span><span class="sxs-lookup"><span data-stu-id="389d1-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="389d1-110">Jest implementację współpracy filtrowania, która używa factorization macierzy jako jego algorytmu core.</span><span class="sxs-lookup"><span data-stu-id="389d1-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="389d1-111">Deweloperzy aplikacji można uzyskać dostępu do zalecenia za pomocą interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="389d1-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="389d1-112">**Co można zrobić z ZALECENIAMI?**</span><span class="sxs-lookup"><span data-stu-id="389d1-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="389d1-113">Zalecenia dotyczące przyjmuje jako wejście element lub zbiór elementów i zwraca listę odpowiednich zaleceń.</span><span class="sxs-lookup"><span data-stu-id="389d1-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="389d1-114">Na przykład: klient sklepie internetowym kliknie produktu.</span><span class="sxs-lookup"><span data-stu-id="389d1-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="389d1-115">Hello online detalicznej tego produktu są wysyłane jako tooRECOMMENDATIONS wejściowych, pobiera listę produktów w zamian i decyduje o tym, które te produkty zostaną wyświetlone toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="389d1-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="389d1-116">Może mają toooptimize zalecenia toouse sklepu online lub nawet tooinform Twojego wewnątrz sprzedaży, działu lub wywołanie Centrum.</span><span class="sxs-lookup"><span data-stu-id="389d1-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="389d1-117">**Czy istnieją jakiekolwiek ograniczenia użycia?**</span><span class="sxs-lookup"><span data-stu-id="389d1-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="389d1-118">Zalecenia dotyczące ma hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="389d1-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="389d1-119">Maksymalna liczba modeli dla subskrypcji: 10</span><span class="sxs-lookup"><span data-stu-id="389d1-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="389d1-120">Maksymalna liczba elementów, które mogą zawierać wykaz: 100 000</span><span class="sxs-lookup"><span data-stu-id="389d1-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="389d1-121">Maksymalna liczba punktów użycia, które są zachowane w Hello jest ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="389d1-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="389d1-122">Hello najstarsze zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="389d1-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="389d1-123">Maksymalny rozmiar danych, który można wysłać w wiadomości e-mail (na przykład importu wykazu danych, importowanie danych użycia) to 200 MB</span><span class="sxs-lookup"><span data-stu-id="389d1-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="389d1-124">Liczba transakcji na sekundę (TPS) dla kompilacji modelu zalecenia, która nie jest aktywny jest TPS ~ 2.</span><span class="sxs-lookup"><span data-stu-id="389d1-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="389d1-125">Zalecenia dotyczące kompilacji modelu, która jest aktywna mogą przechowywać się too20 TPS.</span><span class="sxs-lookup"><span data-stu-id="389d1-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="389d1-126">Zakup i rozliczenia</span><span class="sxs-lookup"><span data-stu-id="389d1-126">Purchase and Billing</span></span>
<span data-ttu-id="389d1-127">**Ile kosztuje zalecenia w okresie uruchamiania hello?**</span><span class="sxs-lookup"><span data-stu-id="389d1-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="389d1-128">Zalecenia dotyczące jest usługą opartą na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="389d1-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="389d1-129">Ładowanie opiera się na woluminie transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="389d1-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="389d1-130">Możesz sprawdzić hello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) w Microsoft Azure Marketplace w celu uzyskania informacji o cenach.</span><span class="sxs-lookup"><span data-stu-id="389d1-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="389d1-131">**Czy istnieją kosztów związanych z o zalecenia dotyczące śledzenia i przechowywania aktywności użytkownika?**</span><span class="sxs-lookup"><span data-stu-id="389d1-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="389d1-132">Nie w momencie hello.</span><span class="sxs-lookup"><span data-stu-id="389d1-132">Not at hello moment.</span></span>

<span data-ttu-id="389d1-133">**Zalecenia dotyczące ma bezpłatną wersję próbną?**</span><span class="sxs-lookup"><span data-stu-id="389d1-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="389d1-134">Brak wolnego dziennik, który jest ograniczony too10, 000 transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="389d1-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="389d1-135">**Gdy zostanie I opłaty będą naliczane za zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="389d1-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="389d1-136">Subskrypcja płatna jest żadnej subskrypcji, dla którego jest miesięcznej opłaty za.</span><span class="sxs-lookup"><span data-stu-id="389d1-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="389d1-137">Jeśli kupisz subskrypcję płatną, możesz są natychmiast naliczane opłaty za hello najpierw użyj miesiącu.</span><span class="sxs-lookup"><span data-stu-id="389d1-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="389d1-138">Naliczane są opłaty hello ilość, którą jest skojarzone z ofertą hello na stronę subskrypcji hello (oraz podatków).</span><span class="sxs-lookup"><span data-stu-id="389d1-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="389d1-139">Opłata miesięczna utworzona na powitania sam kalendarza daty w postaci pierwotnego zakupu do momentu anulowania subskrypcji hello każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="389d1-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="389d1-140">**Jak uaktualnić tooa wyższej warstwy usługi?**</span><span class="sxs-lookup"><span data-stu-id="389d1-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="389d1-141">Możesz kupić lub zaktualizować subskrypcji hello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) strony w witrynie Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="389d1-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="389d1-142">Po uaktualnieniu subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="389d1-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="389d1-143">Transakcje, które pozostały w ramach starego subskrypcji nie są dodawane tooyour nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="389d1-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="389d1-144">Płacisz pełną cenę hello nowej subskrypcji, nawet jeśli masz nieużywane transakcji na starym subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="389d1-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="389d1-145">Proces tooupgrade subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="389d1-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="389d1-146">Nevigate toohello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="389d1-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="389d1-147">Zaloguj się w toohello Marketplace, jeśli nie jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="389d1-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="389d1-148">W okienku po prawej stronie powitania są wyświetlane wszystkie dostępne plany hello.</span><span class="sxs-lookup"><span data-stu-id="389d1-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="389d1-149">Kliknij przycisk radiowy hello hello planu, który ma tooupgrade do.</span><span class="sxs-lookup"><span data-stu-id="389d1-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="389d1-150">Jeśli chcesz tooupgrade, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="389d1-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="389d1-151">Jeśli nie chcesz, aby tooupgrade, kliknij przycisk **anulować**.</span><span class="sxs-lookup"><span data-stu-id="389d1-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="389d1-152">**Ważne** okno dialogowe hello dokładnie Przeczytaj przed rozpoczęciem uaktualniania, ponieważ istnieją rozliczeń i użycia.</span><span class="sxs-lookup"><span data-stu-id="389d1-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="389d1-153">**Gdy zakończy się tooRecommendations mojej subskrypcji?**</span><span class="sxs-lookup"><span data-stu-id="389d1-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="389d1-154">Subskrypcja zakończy się po anulowaniu jej.</span><span class="sxs-lookup"><span data-stu-id="389d1-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="389d1-155">Jeśli chcesz toocancel subskrypcji, zobacz hello, postępując zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="389d1-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="389d1-156">**Jak anulować subskrypcję zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="389d1-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="389d1-157">toocancel, które subskrypcji, użyj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="389d1-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="389d1-158">Jeśli Twojej bieżącej subskrypcji płatnej subskrypcji, subskrypcji nadal obowiązują do końca hello hello bieżącego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="389d1-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="389d1-159">Jeśli należy natychmiast hello toobe anulowania skuteczne, skontaktuj się z nami pod adresem [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="389d1-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="389d1-160">**Uwaga** zwrot nie podano anulowanie przed zakończeniem hello okresie rozliczeniowym lub nieużywane transakcji w okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="389d1-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="389d1-161">Przejdź toohello [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="389d1-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="389d1-162">Zaloguj się w toohello Marketplace, jeśli nie jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="389d1-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="389d1-163">Kliknij przycisk **anulować** toohello rogu hello nazwę zestawu danych i stanu.</span><span class="sxs-lookup"><span data-stu-id="389d1-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="389d1-164">Ta subskrypcja jest używana, aż do osiągnięcia końca hello hello bieżącego rozliczeń okres lub Twój limit transakcji (cokolwiek nastąpi najpierw).</span><span class="sxs-lookup"><span data-stu-id="389d1-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="389d1-165">Jeśli chcesz toocancel subskrypcji natychmiast, więc możesz kupić nową subskrypcję, założyć zgłoszenie w [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="389d1-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="389d1-166">Wprowadzenie do zalecenia</span><span class="sxs-lookup"><span data-stu-id="389d1-166">Getting started with Recommendations</span></span>
<span data-ttu-id="389d1-167">**Zalecenia dotyczące jest dla mnie?**</span><span class="sxs-lookup"><span data-stu-id="389d1-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="389d1-168">Zalecenia w uczeniu maszynowym jest przeznaczony dla organizacji i firm, które zależą od zaleceń toocross sprzedaży i sprzedaje up produktów lub usług tootheir klientów.</span><span class="sxs-lookup"><span data-stu-id="389d1-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="389d1-169">Jeśli masz witryny sieci Web skierowane do klientów, pracownicy działu sprzedaży, wewnętrznej pracownicy działu sprzedaży lub biurem, oraz Jeśli oferujesz katalogu więcej niż kilka dozen produktów lub usług wyników firmy mogą korzystać z zalecenia.</span><span class="sxs-lookup"><span data-stu-id="389d1-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="389d1-170">Eksperymentowanie z zaleceniami jest zaprojektowana toobe dość proste.</span><span class="sxs-lookup"><span data-stu-id="389d1-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="389d1-171">Bieżąca wersja interfejsu API na podstawie Hello wymaga podstawowe umiejętności programowania.</span><span class="sxs-lookup"><span data-stu-id="389d1-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="389d1-172">Jeśli potrzebujesz pomocy, skontaktuj się z dostawcą hello, która opracowała witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="389d1-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="389d1-173">Jeśli masz wewnętrzny dział IT lub lokalnego projektanta, powinny być możliwe tooget toowork zalecenia dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="389d1-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="389d1-174">**Jakie są wymagania wstępne hello konfigurowania zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="389d1-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="389d1-175">Zalecenia dotyczące wymaga dziennika opcji użytkownika pod kątem tooyour katalogu.</span><span class="sxs-lookup"><span data-stu-id="389d1-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="389d1-176">Jeśli nie masz takiego dziennika i masz klienta witryna sieci Web, zalecenia mogą zbierać aktywność użytkowników dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="389d1-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="389d1-177">Zalecenia dotyczące wymaga także katalog produktów i usług.</span><span class="sxs-lookup"><span data-stu-id="389d1-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="389d1-178">Jeśli nie masz katalogu hello zalecenia można użyć danych użycia klienta rzeczywiste hello i przetwarzania wykazu.</span><span class="sxs-lookup"><span data-stu-id="389d1-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="389d1-179">Dorozumiany katalogu nie będzie zawierać elementy, które nie zostały zgłoszone w ramach transakcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="389d1-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="389d1-180">**Jak skonfigurować zalecenia dla powitania po raz pierwszy?**</span><span class="sxs-lookup"><span data-stu-id="389d1-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="389d1-181">Po [subskrybującą](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, powinien użyć dokumentacji interfejsu API hello hello [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md) tooset hello usługi.</span><span class="sxs-lookup"><span data-stu-id="389d1-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="389d1-182">**Gdzie można znaleźć dokumentację interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="389d1-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="389d1-183">Dokumentacja interfejsu API Hello jest [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="389d1-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="389d1-184">**Opcje czy mam tooRecommendations tooupload katalogu i użycia danych?**</span><span class="sxs-lookup"><span data-stu-id="389d1-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="389d1-185">Dostępne są dwie opcje do przekazywania danych katalogu i użycia: można wyeksportować hello dane systemu CRM lub inne dzienniki i przekaż go tooRecommendations lub można dodać tagów tooyour witryny sieci Web, który będzie śledzić działania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="389d1-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="389d1-186">Jeśli używasz hello druga metoda hello dane będą przechowywane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="389d1-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="389d1-187">Obsługi i pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="389d1-187">Maintenance and support</span></span>
<span data-ttu-id="389d1-188">**Jak duży może być zestawu danych?**</span><span class="sxs-lookup"><span data-stu-id="389d1-188">**How large can my data set be?**</span></span>

<span data-ttu-id="389d1-189">Każdy zestaw danych może zawierać too100, 000 elementów katalogu i too2048 MB danych użycia.</span><span class="sxs-lookup"><span data-stu-id="389d1-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="389d1-190">Ponadto subskrypcja może zawierać zapasowej too10 zestawów danych (modeli).</span><span class="sxs-lookup"><span data-stu-id="389d1-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="389d1-191">**Gdzie można uzyskać pomoc techniczną dotyczącą zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="389d1-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="389d1-192">Pomoc techniczna jest dostępna na powitania [Microsoft Azure obsługuje](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) lokacji.</span><span class="sxs-lookup"><span data-stu-id="389d1-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="389d1-193">**Gdzie można znaleźć hello warunki użytkowania?**</span><span class="sxs-lookup"><span data-stu-id="389d1-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="389d1-194">[Microsoft Azure Machine Learning zalecenia dotyczące interfejsu API warunków użytkowania usługi](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="389d1-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

