---
title: "Konfigurowanie i używanie Machine Learning zalecenia API | Dokumentacja firmy Microsoft"
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
redirect_document_id: TRUE
ms.openlocfilehash: 3851589818bb8f4309bf3c65f17b115e0dcd27fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="34922-103">Konfigurowanie i używanie interfejsu API zaleceń usługi Machine Learning — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="34922-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="34922-104">**Co to jest zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="34922-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="34922-105">Należy rozpocząć korzystanie z usługi kognitywnych interfejsu API zalecenia zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="34922-105">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="34922-106">Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="34922-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="34922-107">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="34922-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="34922-108">Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="34922-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="34922-109">W przypadku organizacji i firm, które zależą od zaleceń dotyczących sprzedaży i sprzedaje up produktów i usług klientom zalecenia w usłudze Azure Machine Learning zapewnia aparat samoobsługi zalecenia.</span><span class="sxs-lookup"><span data-stu-id="34922-109">For organizations and businesses that rely on recommendations to cross-sell and up-sell products and services to their customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="34922-110">Jest implementację współpracy filtrowania, która używa factorization macierzy jako jego algorytmu core.</span><span class="sxs-lookup"><span data-stu-id="34922-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="34922-111">Deweloperzy aplikacji można uzyskać dostępu do zalecenia za pomocą interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="34922-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="34922-112">**Co można zrobić z ZALECENIAMI?**</span><span class="sxs-lookup"><span data-stu-id="34922-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="34922-113">Zalecenia dotyczące przyjmuje jako wejście element lub zbiór elementów i zwraca listę odpowiednich zaleceń.</span><span class="sxs-lookup"><span data-stu-id="34922-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="34922-114">Na przykład: klient sklepie internetowym kliknie produktu.</span><span class="sxs-lookup"><span data-stu-id="34922-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="34922-115">Online detalicznej wysyła tego produktu jako dane wejściowe zalecenia, pobiera listę produktów w zamian i decyduje o tym, które z tych produktów będzie wyświetlana dla klienta.</span><span class="sxs-lookup"><span data-stu-id="34922-115">The online retailer sends that product as input to RECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown to the customer.</span></span> <span data-ttu-id="34922-116">Może zajść potrzeba użycia zaleceń w celu zoptymalizowania sklepu online lub nawet powiadomienia użytkownika wewnątrz sprzedaży, działu lub wywołanie Centrum.</span><span class="sxs-lookup"><span data-stu-id="34922-116">You may want to use RECOMMENDATIONS to optimize your online store or even to inform your inside sales department or call center.</span></span>

<span data-ttu-id="34922-117">**Czy istnieją jakiekolwiek ograniczenia użycia?**</span><span class="sxs-lookup"><span data-stu-id="34922-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="34922-118">Zalecenia dotyczące ma następujące ograniczenia użycia:</span><span class="sxs-lookup"><span data-stu-id="34922-118">Recommendations has the following usage limitations:</span></span>

* <span data-ttu-id="34922-119">Maksymalna liczba modeli dla subskrypcji: 10</span><span class="sxs-lookup"><span data-stu-id="34922-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="34922-120">Maksymalna liczba elementów, które mogą zawierać wykaz: 100 000</span><span class="sxs-lookup"><span data-stu-id="34922-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="34922-121">Maksymalna liczba punktów użycia, które są zachowane jest ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="34922-121">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="34922-122">Najstarszych zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="34922-122">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="34922-123">Maksymalny rozmiar danych, który można wysłać w wiadomości e-mail (na przykład importu wykazu danych, importowanie danych użycia) to 200 MB</span><span class="sxs-lookup"><span data-stu-id="34922-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="34922-124">Liczba transakcji na sekundę (TPS) dla kompilacji modelu zalecenia, która nie jest aktywny jest TPS ~ 2.</span><span class="sxs-lookup"><span data-stu-id="34922-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="34922-125">Zalecenia kompilacji modelu, który jest aktywny może przechowywać maksymalnie 20 TPS.</span><span class="sxs-lookup"><span data-stu-id="34922-125">A Recommendations model build that is active can hold up to 20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="34922-126">Zakup i rozliczenia</span><span class="sxs-lookup"><span data-stu-id="34922-126">Purchase and Billing</span></span>
<span data-ttu-id="34922-127">**Jaki jest koszt zalecenia w okresie uruchamiania?**</span><span class="sxs-lookup"><span data-stu-id="34922-127">**How much does Recommendations cost during the launch period?**</span></span>

<span data-ttu-id="34922-128">Zalecenia dotyczące jest usługą opartą na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="34922-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="34922-129">Ładowanie opiera się na woluminie transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="34922-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="34922-130">Możesz sprawdzić [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) w Microsoft Azure Marketplace w celu uzyskania informacji o cenach.</span><span class="sxs-lookup"><span data-stu-id="34922-130">You can check the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="34922-131">**Czy istnieją kosztów związanych z o zalecenia dotyczące śledzenia i przechowywania aktywności użytkownika?**</span><span class="sxs-lookup"><span data-stu-id="34922-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="34922-132">Nie w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="34922-132">Not at the moment.</span></span>

<span data-ttu-id="34922-133">**Zalecenia dotyczące ma bezpłatną wersję próbną?**</span><span class="sxs-lookup"><span data-stu-id="34922-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="34922-134">Brak wolnego dziennik, który jest ograniczony do 10 000 transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="34922-134">There is a free trail which is restricted to 10,000 transactions per month.</span></span>

<span data-ttu-id="34922-135">**Gdy zostanie I opłaty będą naliczane za zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="34922-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="34922-136">Subskrypcja płatna jest żadnej subskrypcji, dla którego jest miesięcznej opłaty za.</span><span class="sxs-lookup"><span data-stu-id="34922-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="34922-137">Po zakupie subskrypcji płatnej, natychmiast są naliczane do użytku w pierwszym miesiącu.</span><span class="sxs-lookup"><span data-stu-id="34922-137">When you purchase a paid subscription, you are immediately charged for the first month's use.</span></span> <span data-ttu-id="34922-138">Naliczane są opłaty kwotę, która jest skojarzona z ofertą na stronę subskrypcji (oraz podatków).</span><span class="sxs-lookup"><span data-stu-id="34922-138">You are charged the amount that is associated with the offer on the subscription page (plus applicable taxes).</span></span> <span data-ttu-id="34922-139">Opłata miesięczna następuje co miesiąc, w tym samym dniu kalendarza jako pierwotnego zakupu do momentu anulowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34922-139">This monthly charge is made each month on the same calendar date as your original purchase until you cancel the subscription.</span></span> 

<span data-ttu-id="34922-140">**Jak uaktualnić usługą wyższej warstwy**</span><span class="sxs-lookup"><span data-stu-id="34922-140">**How do I upgrade to a higher tier service?**</span></span>

<span data-ttu-id="34922-141">Możesz kupić lub zaktualizować subskrypcji [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations) strony w witrynie Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="34922-141">You can buy or update your subscription from the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="34922-142">Po uaktualnieniu subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="34922-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="34922-143">Transakcje, które pozostały w ramach starego subskrypcji nie są dodawane do nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34922-143">Transactions that are remaining on your old subscription are not added to your new subscription.</span></span> 
* <span data-ttu-id="34922-144">Płać pełną cenę nowej subskrypcji, nawet jeśli masz nieużywane transakcji na starym subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34922-144">You pay full price for the new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="34922-145">Proces uaktualniania subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="34922-145">Process to upgrade a subscription:</span></span>

* <span data-ttu-id="34922-146">Nevigate do [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="34922-146">Nevigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="34922-147">Zaloguj się do witryny Marketplace, jeśli nie jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="34922-147">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="34922-148">W okienku po prawej stronie są wyświetlane wszystkie dostępne plany.</span><span class="sxs-lookup"><span data-stu-id="34922-148">In the right pane, all the available plans are listed.</span></span> <span data-ttu-id="34922-149">Kliknij przycisk radiowy planu, który chcesz uaktualnić do wersji.</span><span class="sxs-lookup"><span data-stu-id="34922-149">Click the radio button for the plan you want to upgrade to.</span></span>
* <span data-ttu-id="34922-150">Jeśli chcesz uaktualnić, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="34922-150">If you want to upgrade, click **OK**.</span></span> <span data-ttu-id="34922-151">Jeśli nie chcesz uaktualnić, kliknij przycisk **anulować**.</span><span class="sxs-lookup"><span data-stu-id="34922-151">If you do not want to upgrade, click **Cancel**.</span></span>

<span data-ttu-id="34922-152">**Ważne** należy dokładnie zapoznać się okno dialogowe przed rozpoczęciem uaktualniania, ponieważ istnieją rozliczeń i użycia.</span><span class="sxs-lookup"><span data-stu-id="34922-152">**Important** Carefully read the dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="34922-153">**Kiedy skończy się subskrypcję zalecenia**</span><span class="sxs-lookup"><span data-stu-id="34922-153">**When will my subscription to Recommendations end?**</span></span>

<span data-ttu-id="34922-154">Subskrypcja zakończy się po anulowaniu jej.</span><span class="sxs-lookup"><span data-stu-id="34922-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="34922-155">Jeśli chcesz anulować subskrypcji, zobacz poniższe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="34922-155">If you would like to cancel your subscriptions, see the following instructions.</span></span>

<span data-ttu-id="34922-156">**Jak anulować subskrypcję zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="34922-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="34922-157">Aby anulować subskrypcję, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="34922-157">To cancel your subscription, use the following steps.</span></span> <span data-ttu-id="34922-158">Jeśli Twojej bieżącej subskrypcji płatnej subskrypcji, subskrypcji nadal obowiązują do końca bieżącego okresu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="34922-158">If your current subscription is a paid subscription, your subscription continues in effect until the end of the current billing period.</span></span> <span data-ttu-id="34922-159">Anulowania do obowiązywać natychmiast, należy skontaktować się z nami pod adresem [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="34922-159">If you need the cancellation to be effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="34922-160">**Uwaga** zwrot nie podano anulowanie przed zakończeniem okresu rozliczeniowego lub nieużywane transakcji w okresie rozliczeniowym.</span><span class="sxs-lookup"><span data-stu-id="34922-160">**Note** No refund is given if you cancel before the end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="34922-161">Przejdź do [oferują strony](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="34922-161">Navigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="34922-162">Zaloguj się do witryny Marketplace, jeśli nie jest już zalogowany.</span><span class="sxs-lookup"><span data-stu-id="34922-162">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="34922-163">Kliknij przycisk **anulować** z prawej strony nazwy zestawu danych i stanu.</span><span class="sxs-lookup"><span data-stu-id="34922-163">Click **Cancel** to the right of the dataset name and status.</span></span> <span data-ttu-id="34922-164">Możesz użyć tej subskrypcji do końca bieżącego okresu rozliczeniowego lub osiągnięto limit transakcji (cokolwiek nastąpi najpierw).</span><span class="sxs-lookup"><span data-stu-id="34922-164">You can use this subscription until the end of the current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="34922-165">Jeśli chcesz anulować subskrypcję, natychmiast, więc możesz kupić nową subskrypcję, założyć zgłoszenie w [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="34922-165">If you would like to cancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="34922-166">Wprowadzenie do zalecenia</span><span class="sxs-lookup"><span data-stu-id="34922-166">Getting started with Recommendations</span></span>
<span data-ttu-id="34922-167">**Zalecenia dotyczące jest dla mnie?**</span><span class="sxs-lookup"><span data-stu-id="34922-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="34922-168">Zalecenia w uczeniu maszynowym jest przeznaczony dla organizacji i firm, które zależą od zaleceń dotyczących sprzedaży i sprzedaje up produktów lub usług klientom.</span><span class="sxs-lookup"><span data-stu-id="34922-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations to cross-sell and up-sell products or services to their customers.</span></span> <span data-ttu-id="34922-169">Jeśli masz witryny sieci Web skierowane do klientów, pracownicy działu sprzedaży, wewnętrznej pracownicy działu sprzedaży lub biurem, oraz Jeśli oferujesz katalogu więcej niż kilka dozen produktów lub usług wyników firmy mogą korzystać z zalecenia.</span><span class="sxs-lookup"><span data-stu-id="34922-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="34922-170">Eksperymentowanie z zaleceniami ma być stosunkowo proste.</span><span class="sxs-lookup"><span data-stu-id="34922-170">Experimenting with Recommendations is designed to be fairly simple.</span></span> <span data-ttu-id="34922-171">Bieżąca wersja interfejsu API na podstawie wymaga podstawowe umiejętności programowania.</span><span class="sxs-lookup"><span data-stu-id="34922-171">The current API-based version requires basic programming skills.</span></span> <span data-ttu-id="34922-172">Jeśli potrzebujesz pomocy, skontaktuj się z dostawcą, która opracowała witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="34922-172">If you need assistance, contact the vendor who developed your website.</span></span> <span data-ttu-id="34922-173">Jeśli masz wewnętrzny dział IT lub lokalnego projektanta, należy uzyskać zalecenia do działania.</span><span class="sxs-lookup"><span data-stu-id="34922-173">If you have an internal IT department or an in-house developer, they should be able to get Recommendations to work for you.</span></span> 

<span data-ttu-id="34922-174">**Jakie są wymagania wstępne dotyczące konfigurowania zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="34922-174">**What are the prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="34922-175">Zalecenia dotyczące wymaga dziennika opcji użytkownika w odniesieniu do katalogu.</span><span class="sxs-lookup"><span data-stu-id="34922-175">Recommendations requires that you have a log of user choices as it relates to your catalog.</span></span> <span data-ttu-id="34922-176">Jeśli nie masz takiego dziennika i masz klienta witryna sieci Web, zalecenia mogą zbierać aktywność użytkowników dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="34922-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="34922-177">Zalecenia dotyczące wymaga także katalog produktów i usług.</span><span class="sxs-lookup"><span data-stu-id="34922-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="34922-178">Jeśli nie masz katalogu zalecenia można użyć klienta rzeczywiste dane użycia i przetwarzania wykazu.</span><span class="sxs-lookup"><span data-stu-id="34922-178">If you don't have the catalog, Recommendations can use the actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="34922-179">Dorozumiany katalogu nie będzie zawierać elementy, które nie zostały zgłoszone w ramach transakcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="34922-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="34922-180">**Sposób konfigurowania zalecenia po raz pierwszy**</span><span class="sxs-lookup"><span data-stu-id="34922-180">**How do I set up Recommendations for the first time?**</span></span>

<span data-ttu-id="34922-181">Po [subskrybującą](https://datamarket.azure.com/dataset/amla/recommendations) zaleceń, należy używać w dokumentacji interfejsu API w [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md) do skonfigurowania usługi.</span><span class="sxs-lookup"><span data-stu-id="34922-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) to Recommendations, you should use the API documentation in the [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) to set up the service.</span></span>

<span data-ttu-id="34922-182">**Gdzie można znaleźć dokumentację interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="34922-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="34922-183">Dokumentacja interfejsu API jest [Azure Machine Learning zalecenia — Przewodnik Szybki Start](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="34922-183">The API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="34922-184">**Jakie opcje czy mają przekazywać dane katalogu i użycia do zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="34922-184">**What options do I have to upload catalog and usage data to Recommendations?**</span></span>

<span data-ttu-id="34922-185">Dostępne są dwie opcje do przekazywania danych katalogu i użycia: można eksportować dane z tego systemu CRM lub inne dzienniki i przekaż go do zalecenia lub można dodać tagów do witryny sieci Web, który będzie śledzić działania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="34922-185">You have two options for uploading your catalog and usage data: You can export the data from your CRM system or other logs and upload it to Recommendations, or you can add tags to your website that will track user activities.</span></span> <span data-ttu-id="34922-186">Jeśli używasz druga metoda, dane będą przechowywane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34922-186">If you use the latter method, the data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="34922-187">Obsługi i pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="34922-187">Maintenance and support</span></span>
<span data-ttu-id="34922-188">**Jak duży może być zestawu danych?**</span><span class="sxs-lookup"><span data-stu-id="34922-188">**How large can my data set be?**</span></span>

<span data-ttu-id="34922-189">Każdy zestaw danych może zawierać maksymalnie 100 000 elementów katalogu i 2048 MB danych użycia.</span><span class="sxs-lookup"><span data-stu-id="34922-189">Each data set can contain up to 100,000 catalog items and up to 2048 MB of usage data.</span></span>
<span data-ttu-id="34922-190">Ponadto subskrypcja może zawierać maksymalnie 10 zestawów danych (modeli).</span><span class="sxs-lookup"><span data-stu-id="34922-190">In addition, a subscription can contain up to 10 data sets (models).</span></span>

<span data-ttu-id="34922-191">**Gdzie można uzyskać pomoc techniczną dotyczącą zalecenia?**</span><span class="sxs-lookup"><span data-stu-id="34922-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="34922-192">Pomoc techniczna jest dostępna na [Microsoft Azure obsługuje](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) lokacji.</span><span class="sxs-lookup"><span data-stu-id="34922-192">Technical support is available on the [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="34922-193">**Gdzie można znaleźć warunki użytkowania?**</span><span class="sxs-lookup"><span data-stu-id="34922-193">**Where can I find the terms of use?**</span></span>

<span data-ttu-id="34922-194">[Microsoft Azure Machine Learning zalecenia dotyczące interfejsu API warunków użytkowania usługi](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="34922-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

