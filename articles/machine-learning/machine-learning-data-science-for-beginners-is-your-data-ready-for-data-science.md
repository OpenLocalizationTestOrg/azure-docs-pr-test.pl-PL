---
title: "Czy Twoje dane są gotowe na analizę danych? Ocena danych - Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się 4 kryteria dla danych będzie gotowa do analizy danych. Nauki danych dla początkujących wideo 2 ma konkretnego przykłady ułatwiające oceny podstawowe dane."
keywords: "odpowiednie dane oceny danych, należy przygotować danych kryteria danych, danych gotowe"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: c4a8bc11aec2f71796f589c0af54cc92253e5180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="c4cfa-106">Czy Twoje dane są gotowe na analizę danych?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="c4cfa-107">Wideo 2: Nauki danych serii dla początkujących</span><span class="sxs-lookup"><span data-stu-id="c4cfa-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="c4cfa-108">Dowiedz się, jak można obliczyć wartości danych, aby upewnić się, że spełnia on podstawowe kryteria gotowość do analizy danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span></span>

<span data-ttu-id="c4cfa-109">Aby uzyskać wykorzystanie serii, obejrzyj je wszystkie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="c4cfa-110">[Przejdź do listy filmów wideo](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="c4cfa-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="c4cfa-111">Inne pliki wideo w tej serii</span><span class="sxs-lookup"><span data-stu-id="c4cfa-111">Other videos in this series</span></span>
<span data-ttu-id="c4cfa-112">*Nauki danych dla początkujących* jest szybkie wprowadzenie do analizy danych w pięciu krótkie wideo.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="c4cfa-113">Wideo 1: [danych nauki odpowiedzi na pytania 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sek.)*</span><span class="sxs-lookup"><span data-stu-id="c4cfa-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="c4cfa-114">Wideo 2: Jest gotowy do analizy danych danych?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="c4cfa-115">Wideo 3: [Zadaj pytanie może odpowiedzieć z danymi](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 s 17 min)*</span><span class="sxs-lookup"><span data-stu-id="c4cfa-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="c4cfa-116">Wideo 4: [prognozowania odpowiedzi z modelu prostego](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 s 42 min)*</span><span class="sxs-lookup"><span data-stu-id="c4cfa-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="c4cfa-117">Wideo 5: [skopiuj pracy innych osób nauki danych](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sek.)*</span><span class="sxs-lookup"><span data-stu-id="c4cfa-117">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="c4cfa-118">Zapis: Jest gotowy do analizy danych danych?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="c4cfa-119">— Zapraszamy! "Jest danych gotowe do analizy danych?"</span><span class="sxs-lookup"><span data-stu-id="c4cfa-119">Welcome to "Is your data ready for data science?"</span></span> <span data-ttu-id="c4cfa-120">drugi wideo w serii *nauki danych dla początkujących*.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-120">the second video in the series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="c4cfa-121">Przed nauki danych można nadać odpowiedzi, który ma, należy nadać mu niektórych materiałów raw wysokiej jakości do pracy z.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span></span> <span data-ttu-id="c4cfa-122">Podobnie jak wprowadzenie składników rozpoczęcia z lepsze produktu końcowego pizza, tym lepiej.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="c4cfa-123">Kryteria dla danych</span><span class="sxs-lookup"><span data-stu-id="c4cfa-123">Criteria for data</span></span>
<span data-ttu-id="c4cfa-124">Tak w przypadku analizy danych, ma niektórych składników, które należy do scalenia.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-124">So, in the case of data science, there are some ingredients that we need to pull together.</span></span>

<span data-ttu-id="c4cfa-125">Potrzebujemy dane, które są:</span><span class="sxs-lookup"><span data-stu-id="c4cfa-125">We need data that is:</span></span>

* <span data-ttu-id="c4cfa-126">Odpowiednie</span><span class="sxs-lookup"><span data-stu-id="c4cfa-126">Relevant</span></span>
* <span data-ttu-id="c4cfa-127">połączone</span><span class="sxs-lookup"><span data-stu-id="c4cfa-127">Connected</span></span>
* <span data-ttu-id="c4cfa-128">Dokładne</span><span class="sxs-lookup"><span data-stu-id="c4cfa-128">Accurate</span></span>
* <span data-ttu-id="c4cfa-129">Aby pracować z</span><span class="sxs-lookup"><span data-stu-id="c4cfa-129">Enough to work with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="c4cfa-130">Dotyczy danych?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-130">Is your data relevant?</span></span>
<span data-ttu-id="c4cfa-131">Potrzebujemy pierwszy składnik — dane, które są odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-131">So the first ingredient - we need data that's relevant.</span></span>

![Istotne dane, a dane nie ma znaczenia — oceny danych](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="c4cfa-133">Szukaj w tabeli po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-133">Look at the table on the left.</span></span> <span data-ttu-id="c4cfa-134">Firma Microsoft spełnione siedmiu osób poza paski Boston, mierzony poziom alkohol krwi, Sox czerwony średnią batting ich ostatniego gry, w i cen mleka w najbliższej sklepie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-134">We met seven people outside of Boston bars, measured their blood alcohol level, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span></span>

<span data-ttu-id="c4cfa-135">To są wszystkie dane doskonale uzasadnionych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="c4cfa-136">Błąd tylko jego jest, że nie jest odpowiedni.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="c4cfa-137">Nie ma żadnej oczywiste zależności między te liczby.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="c4cfa-138">Jeśli po otwarciu bieżącej ceny i średnia batting Sox czerwony, nie istnieje sposób można odgadnąć Moja zawartość alkoholu krwi.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-138">If I gave you the current price of milk and the Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="c4cfa-139">Teraz wyglądać w tabeli po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-139">Now look at the table on the right.</span></span> <span data-ttu-id="c4cfa-140">Teraz możemy mierzony każda osoba body masowej i zliczane liczba napojów one właśnie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-140">This time we measured each person’s body mass and counted the number of drinks they’ve had.</span></span>  <span data-ttu-id="c4cfa-141">Numery w każdym wierszu teraz mają zastosowanie do siebie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-141">The numbers in each row are now relevant to each other.</span></span> <span data-ttu-id="c4cfa-142">Jeśli I udostępniła Ci Moje treści masowej oraz liczby Margaritas I właśnie, można utworzyć wynik w mojej krwi alkohol zawartości.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-142">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="c4cfa-143">Czy nawiązano połączenie danych?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-143">Do you have connected data?</span></span>
<span data-ttu-id="c4cfa-144">Następny składnik jest połączonych danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-144">The next ingredient is connected data.</span></span>

![Połączenia danych, a dane bez połączenia — kryteria danych danych gotowe](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="c4cfa-146">Oto niektóre dane dotyczące jakości hamburgers: kraty temperatury, waga patty i ocenę w lokalnym żywności magazyn.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-146">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span></span> <span data-ttu-id="c4cfa-147">Jednak zauważyć luk w tabeli po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-147">But notice the gaps in the table on the left.</span></span>

<span data-ttu-id="c4cfa-148">Brak niektórych wartości większość zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-148">Most data sets are missing some values.</span></span> <span data-ttu-id="c4cfa-149">Jest często mają luk w następujący sposób i sposoby ich obejścia.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-149">It's common to have holes like this and there are ways to work around them.</span></span> <span data-ttu-id="c4cfa-150">Jednak jeśli istnieje za dużo Brak, dane rozpocznie się wyglądały jak ser Szwajcaria.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-150">But if there's too much missing, your data begins to look like Swiss cheese.</span></span>

<span data-ttu-id="c4cfa-151">Jeśli Szukaj w tabeli po lewej stronie ma tak dużo brakujące dane, trudno jest opracowywane dowolnego rodzaju relacji między rusztem temperatury i patty wagi.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-151">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="c4cfa-152">To jest przykład bez połączenia danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="c4cfa-153">Tabeli po prawej stronie, jednak jest zapełniony i ukończenia — przykład połączonych danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-153">The table on the right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="c4cfa-154">Dane są dokładne?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-154">Is your data accurate?</span></span>
<span data-ttu-id="c4cfa-155">Następny składnik, potrzebne jest dokładności.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-155">The next ingredient we need is accuracy.</span></span> <span data-ttu-id="c4cfa-156">Poniżej przedstawiono cztery obiektów docelowych, które chcielibyśmy trafień za pomocą strzałek.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-156">Here are four targets that we’d like to hit with arrows.</span></span>

![Dokładne dane a niedokładne dane — kryteria danych](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="c4cfa-158">Szukaj w celu, w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-158">Look at the target in the upper right.</span></span> <span data-ttu-id="c4cfa-159">Mamy ścisłej grupowania prawo wokół bullseye.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-159">We’ve got a tight grouping right around the bullseye.</span></span> <span data-ttu-id="c4cfa-160">Oczywiście jest dokładna.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-160">That, of course, is accurate.</span></span> <span data-ttu-id="c4cfa-161">Dziwnie danego języka nauki danych naszych wydajności z prawej strony docelowej poniżej jest traktowana jako dokładne.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-161">Oddly, in the language of data science, our performance on the target right below it is also considered accurate.</span></span>

<span data-ttu-id="c4cfa-162">Jeśli do mapowania Centrum te strzałki, zobaczysz, że bardzo jest bliski bullseye.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-162">If you were to map out the center of these arrows, you'd see that it's very close to the bullseye.</span></span> <span data-ttu-id="c4cfa-163">Strzałki są rozproszone wszystkie wokół docelowej, więc są traktowane jako nieprecyzyjna, ale jest wyśrodkowane wokół bullseye, więc są traktowane jako dokładne.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-163">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="c4cfa-164">Teraz wyglądać w lewym górnym docelowej.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-164">Now look at the upper-left target.</span></span> <span data-ttu-id="c4cfa-165">W tym miejscu naszych strzałki bardzo blisko siebie osiągnęła ścisłej grupowania.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="c4cfa-166">Są one dokładne, ale są one nieprawidłowe, ponieważ Centrum jest sposób poza bullseye.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-166">They're precise, but they're inaccurate because the center is way off the bullseye.</span></span> <span data-ttu-id="c4cfa-167">I oczywiście strzałki w lewym dolnym rogu docelowej są niedokładne i niedokładna.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-167">And, of course, the arrows in the bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="c4cfa-168">Ten archer wymaga więcej rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-to-work-with"></a><span data-ttu-id="c4cfa-169">Masz za mało danych do pracy z?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-169">Do you have enough data to work with?</span></span>
<span data-ttu-id="c4cfa-170">Na koniec składnik #4 - musimy mieć wystarczającej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-170">Finally, ingredient #4 - we need to have enough data.</span></span>

![Masz za mało danych do analizy?](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="c4cfa-173">Pomyśl o każdego punktu danych w tabeli jako pędzla w malowania.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="c4cfa-174">Jeśli masz tylko niektóre z nich może być dość rozmytego rysowania — jest stwierdzić, co to jest.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-174">If you have only a few of them, the painting can be pretty fuzzy - it's hard to tell what it is.</span></span>

<span data-ttu-id="c4cfa-175">Jeśli dodasz kilka więcej pociągnięć Twojej rysowania uruchamia uzyskać nieco ostrzejszy.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-175">If you add some more brush strokes, then your painting starts to get a little sharper.</span></span>

<span data-ttu-id="c4cfa-176">Jeśli masz prawie za mało pociągnięć widać niektóre szerokie decyzje, aby.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-176">When you have barely enough strokes, you can see just enough to make some broad decisions.</span></span> <span data-ttu-id="c4cfa-177">Jest to miejsce, które można znaleźć?</span><span class="sxs-lookup"><span data-stu-id="c4cfa-177">Is it somewhere I might want to visit?</span></span> <span data-ttu-id="c4cfa-178">Wygląda na to jasny, to wygląda czystej wody — tak, będącą, gdzie użyjemy na urlop.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="c4cfa-179">Jak dodać więcej danych obraz staje się jaśniejszy i bardziej szczegółowe decyzje.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-179">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="c4cfa-180">Teraz można przyjrzeć trzy hotels na lewym bank.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-180">Now I can look at the three hotels on the left bank.</span></span> <span data-ttu-id="c4cfa-181">Znasz, naprawdę jak z architektury funkcje co na pierwszym planie.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-181">You know, I really like the architectural features of the one in the foreground.</span></span> <span data-ttu-id="c4cfa-182">I będzie pozostać, trzeci piętra.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-182">I’ll stay there, on the third floor.</span></span>

<span data-ttu-id="c4cfa-183">Z danych, które jest odpowiednie, połączony, dokładne i wystarczająco, firma Microsoft ma wszystkich składników należy wykonać niektóre nauki wysokiej jakości danych.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-183">With data that's relevant, connected, accurate, and enough, we have all the ingredients we need to do some high-quality data science.</span></span>

<span data-ttu-id="c4cfa-184">Należy koniecznie zapoznaj się z czterech wideo w *nauki danych dla początkujących* z Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c4cfa-184">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4cfa-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4cfa-185">Next steps</span></span>
* [<span data-ttu-id="c4cfa-186">Spróbuj pierwszego eksperymentu analizy danych z usługi Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="c4cfa-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="c4cfa-187">Wprowadzenie do uczenia maszynowego w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c4cfa-187">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
