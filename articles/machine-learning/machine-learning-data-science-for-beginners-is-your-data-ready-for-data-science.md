---
title: aaaIs danych gotowe do analizy danych? Ocena danych - Azure Machine Learning | Dokumentacja firmy Microsoft
description: "Dowiedz się kryteria hello 4 toobe danych gotowe do analizy danych. Nauki danych dla początkujących wideo 2 ma toohelp konkretnych przykłady oceny podstawowe dane."
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
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="0f17c-106">Czy Twoje dane są gotowe na analizę danych?</span><span class="sxs-lookup"><span data-stu-id="0f17c-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="0f17c-107">Wideo 2: Nauki danych serii dla początkujących</span><span class="sxs-lookup"><span data-stu-id="0f17c-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="0f17c-108">Dowiedz się, jak tooevaluate Twojego toomake danych się, że spełnia on wymagania podstawowe kryteria toobe gotowe do analizy danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-108">Learn how tooevaluate your data toomake sure it meets basic criteria toobe ready for data science.</span></span>

<span data-ttu-id="0f17c-109">Witaj tooget wykorzystanie serii hello, obejrzyj je wszystkie.</span><span class="sxs-lookup"><span data-stu-id="0f17c-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="0f17c-110">[Przejdź do listy toohello filmów wideo](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="0f17c-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="0f17c-111">Inne pliki wideo w tej serii</span><span class="sxs-lookup"><span data-stu-id="0f17c-111">Other videos in this series</span></span>
<span data-ttu-id="0f17c-112">*Nauki danych dla początkujących* to nauka toodata szybkie wprowadzenie w pięciu krótkie wideo.</span><span class="sxs-lookup"><span data-stu-id="0f17c-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="0f17c-113">Wideo 1: [danych nauki odpowiedzi na pytania hello 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sek.)*</span><span class="sxs-lookup"><span data-stu-id="0f17c-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="0f17c-114">Wideo 2: Jest gotowy do analizy danych danych?</span><span class="sxs-lookup"><span data-stu-id="0f17c-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="0f17c-115">Wideo 3: [Zadaj pytanie może odpowiedzieć z danymi](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 s 17 min)*</span><span class="sxs-lookup"><span data-stu-id="0f17c-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="0f17c-116">Wideo 4: [prognozowania odpowiedzi z modelu prostego](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 s 42 min)*</span><span class="sxs-lookup"><span data-stu-id="0f17c-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="0f17c-117">Wideo 5: [skopiować inne osoby pracy toodo danych nauki](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sek.)*</span><span class="sxs-lookup"><span data-stu-id="0f17c-117">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="0f17c-118">Zapis: Jest gotowy do analizy danych danych?</span><span class="sxs-lookup"><span data-stu-id="0f17c-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="0f17c-119">Zapraszamy zbyt "jest danych gotowe do analizy danych?"</span><span class="sxs-lookup"><span data-stu-id="0f17c-119">Welcome too"Is your data ready for data science?"</span></span> <span data-ttu-id="0f17c-120">Witaj drugi wideo w serii hello *nauki danych dla początkujących*.</span><span class="sxs-lookup"><span data-stu-id="0f17c-120">hello second video in hello series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="0f17c-121">Przed danych naukowe zapewnić hello odpowiedzi mają, masz toogive on toowork niektórych materiałów wysokiej jakości z.</span><span class="sxs-lookup"><span data-stu-id="0f17c-121">Before data science can give you hello answers you want, you have toogive it some high-quality raw materials toowork with.</span></span> <span data-ttu-id="0f17c-122">Podobnie jak wprowadzania pizza, hello lepsze hello składników rozpoczęcia, lepiej hello hello produktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="0f17c-122">Just like making a pizza, hello better hello ingredients you start with, hello better hello final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="0f17c-123">Kryteria dla danych</span><span class="sxs-lookup"><span data-stu-id="0f17c-123">Criteria for data</span></span>
<span data-ttu-id="0f17c-124">Tak w przypadku hello analizy danych, brak niektórych składników, że razem potrzebujemy toopull.</span><span class="sxs-lookup"><span data-stu-id="0f17c-124">So, in hello case of data science, there are some ingredients that we need toopull together.</span></span>

<span data-ttu-id="0f17c-125">Potrzebujemy dane, które są:</span><span class="sxs-lookup"><span data-stu-id="0f17c-125">We need data that is:</span></span>

* <span data-ttu-id="0f17c-126">Odpowiednie</span><span class="sxs-lookup"><span data-stu-id="0f17c-126">Relevant</span></span>
* <span data-ttu-id="0f17c-127">połączone</span><span class="sxs-lookup"><span data-stu-id="0f17c-127">Connected</span></span>
* <span data-ttu-id="0f17c-128">Dokładne</span><span class="sxs-lookup"><span data-stu-id="0f17c-128">Accurate</span></span>
* <span data-ttu-id="0f17c-129">Za mało toowork z</span><span class="sxs-lookup"><span data-stu-id="0f17c-129">Enough toowork with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="0f17c-130">Dotyczy danych?</span><span class="sxs-lookup"><span data-stu-id="0f17c-130">Is your data relevant?</span></span>
<span data-ttu-id="0f17c-131">Potrzebujemy hello pierwszy składnik — dane, które są odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="0f17c-131">So hello first ingredient - we need data that's relevant.</span></span>

![Istotne dane, a dane nie ma znaczenia — oceny danych](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="0f17c-133">Spójrz na powitania tabeli po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0f17c-133">Look at hello table on hello left.</span></span> <span data-ttu-id="0f17c-134">Firma Microsoft spełnione siedmiu osób poza paski Boston, mierzona ich poziom alkohol krwi, średnia batting Sox czerwony hello ich ostatniego gry, w i cen hello mleka na powitania najbliższej sklepie.</span><span class="sxs-lookup"><span data-stu-id="0f17c-134">We met seven people outside of Boston bars, measured their blood alcohol level, hello Red Sox batting average in their last game, and hello price of milk in hello nearest convenience store.</span></span>

<span data-ttu-id="0f17c-135">To są wszystkie dane doskonale uzasadnionych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="0f17c-136">Błąd tylko jego jest, że nie jest odpowiedni.</span><span class="sxs-lookup"><span data-stu-id="0f17c-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="0f17c-137">Nie ma żadnej oczywiste zależności między te liczby.</span><span class="sxs-lookup"><span data-stu-id="0f17c-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="0f17c-138">Jeśli po otwarciu hello bieżącej ceny mleka i hello średniej batting Sox czerwony, nie istnieje sposób można odgadnąć Moja zawartość alkoholu krwi.</span><span class="sxs-lookup"><span data-stu-id="0f17c-138">If I gave you hello current price of milk and hello Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="0f17c-139">Teraz wyglądać w tabeli hello na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="0f17c-139">Now look at hello table on hello right.</span></span> <span data-ttu-id="0f17c-140">Teraz możemy mierzone każda osoba treści hello masowych i są one uwzględniane liczba napojów one właśnie.</span><span class="sxs-lookup"><span data-stu-id="0f17c-140">This time we measured each person’s body mass and counted hello number of drinks they’ve had.</span></span>  <span data-ttu-id="0f17c-141">numery Hello w każdym wierszu są teraz tooeach odpowiednich innymi.</span><span class="sxs-lookup"><span data-stu-id="0f17c-141">hello numbers in each row are now relevant tooeach other.</span></span> <span data-ttu-id="0f17c-142">Jeśli po otwarciu Moje treści masowej i hello liczbę Margaritas I właśnie, można wprowadzeniu wynik w mojej krwi alkohol zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f17c-142">If I gave you my body mass and hello number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="0f17c-143">Czy nawiązano połączenie danych?</span><span class="sxs-lookup"><span data-stu-id="0f17c-143">Do you have connected data?</span></span>
<span data-ttu-id="0f17c-144">następny składnik Hello jest połączonych danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-144">hello next ingredient is connected data.</span></span>

![Połączenia danych, a dane bez połączenia — kryteria danych danych gotowe](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="0f17c-146">Oto niektóre dane dotyczące jakości hello hamburgers: kraty temperatury, waga patty i ocenę w żywności lokalne powitania magazyn.</span><span class="sxs-lookup"><span data-stu-id="0f17c-146">Here is some relevant data on hello quality of hamburgers: grill temperature, patty weight, and rating in hello local food magazine.</span></span> <span data-ttu-id="0f17c-147">Jednak zauważyć hello luk w hello tabeli po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0f17c-147">But notice hello gaps in hello table on hello left.</span></span>

<span data-ttu-id="0f17c-148">Brak niektórych wartości większość zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-148">Most data sets are missing some values.</span></span> <span data-ttu-id="0f17c-149">Jest on typowe luk toohave następująco i istnieją sposoby toowork wokół nich.</span><span class="sxs-lookup"><span data-stu-id="0f17c-149">It's common toohave holes like this and there are ways toowork around them.</span></span> <span data-ttu-id="0f17c-150">Jednak jeśli istnieje za dużo Brak, dane rozpocznie się toolook, takich jak ser Szwajcaria.</span><span class="sxs-lookup"><span data-stu-id="0f17c-150">But if there's too much missing, your data begins toolook like Swiss cheese.</span></span>

<span data-ttu-id="0f17c-151">Czy tabeli hello przyjrzeć się po lewej stronie powitania, jest więc dużo brakujące dane, twardych toocome się z dowolnego rodzaju relacji między kraty temperatury i patty wagi.</span><span class="sxs-lookup"><span data-stu-id="0f17c-151">If you look at hello table on hello left, there's so much missing data, it's hard toocome up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="0f17c-152">To jest przykład bez połączenia danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="0f17c-153">jednak Hello tabeli po prawej stronie powitania jest zapełniony i ukończenia — przykład połączonych danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-153">hello table on hello right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="0f17c-154">Dane są dokładne?</span><span class="sxs-lookup"><span data-stu-id="0f17c-154">Is your data accurate?</span></span>
<span data-ttu-id="0f17c-155">Witaj następny składnik potrzebne jest dokładności.</span><span class="sxs-lookup"><span data-stu-id="0f17c-155">hello next ingredient we need is accuracy.</span></span> <span data-ttu-id="0f17c-156">Poniżej przedstawiono cztery elementy docelowe, chcielibyśmy toohit z strzałki.</span><span class="sxs-lookup"><span data-stu-id="0f17c-156">Here are four targets that we’d like toohit with arrows.</span></span>

![Dokładne dane a niedokładne dane — kryteria danych](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="0f17c-158">Szukaj w celu hello w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="0f17c-158">Look at hello target in hello upper right.</span></span> <span data-ttu-id="0f17c-159">Mamy ścisłej grupowania prawo wokół hello bullseye.</span><span class="sxs-lookup"><span data-stu-id="0f17c-159">We’ve got a tight grouping right around hello bullseye.</span></span> <span data-ttu-id="0f17c-160">Oczywiście jest dokładna.</span><span class="sxs-lookup"><span data-stu-id="0f17c-160">That, of course, is accurate.</span></span> <span data-ttu-id="0f17c-161">Dziwnie języka hello nauki danych naszych wydajności prawej strony docelowej hello poniżej jest traktowana jako dokładne.</span><span class="sxs-lookup"><span data-stu-id="0f17c-161">Oddly, in hello language of data science, our performance on hello target right below it is also considered accurate.</span></span>

<span data-ttu-id="0f17c-162">Gdyby toomap limit hello środek te strzałki, zobaczysz, jest bardzo Zamknij toohello bullseye.</span><span class="sxs-lookup"><span data-stu-id="0f17c-162">If you were toomap out hello center of these arrows, you'd see that it's very close toohello bullseye.</span></span> <span data-ttu-id="0f17c-163">strzałki Hello są rozproszone wszystkie wokół docelowej hello są traktowane jako nieprecyzyjne, ale jest wyśrodkowywana wokół hello bullseye, są traktowane jako dokładne.</span><span class="sxs-lookup"><span data-stu-id="0f17c-163">hello arrows are spread out all around hello target, so they're considered imprecise, but they're centered around hello bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="0f17c-164">Teraz wyglądać w celu lewej górnej hello.</span><span class="sxs-lookup"><span data-stu-id="0f17c-164">Now look at hello upper-left target.</span></span> <span data-ttu-id="0f17c-165">W tym miejscu naszych strzałki bardzo blisko siebie osiągnęła ścisłej grupowania.</span><span class="sxs-lookup"><span data-stu-id="0f17c-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="0f17c-166">Są one dokładne, ale są one nieprawidłowe, ponieważ Centrum hello jest sposób poza hello bullseye.</span><span class="sxs-lookup"><span data-stu-id="0f17c-166">They're precise, but they're inaccurate because hello center is way off hello bullseye.</span></span> <span data-ttu-id="0f17c-167">I oczywiście strzałki hello w celu lewym dolnym rogu hello są niedokładne i niedokładna.</span><span class="sxs-lookup"><span data-stu-id="0f17c-167">And, of course, hello arrows in hello bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="0f17c-168">Ten archer wymaga więcej rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0f17c-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-toowork-with"></a><span data-ttu-id="0f17c-169">Masz za mało danych toowork z?</span><span class="sxs-lookup"><span data-stu-id="0f17c-169">Do you have enough data toowork with?</span></span>
<span data-ttu-id="0f17c-170">Na koniec składnik #4 - potrzebujemy toohave wystarczającej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-170">Finally, ingredient #4 - we need toohave enough data.</span></span>

![Masz za mało danych do analizy?](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="0f17c-173">Pomyśl o każdego punktu danych w tabeli jako pędzla w malowania.</span><span class="sxs-lookup"><span data-stu-id="0f17c-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="0f17c-174">Jeśli masz tylko niektóre z nich, rysowania hello może być dość rozmytego — jest tootell twardym co to jest.</span><span class="sxs-lookup"><span data-stu-id="0f17c-174">If you have only a few of them, hello painting can be pretty fuzzy - it's hard tootell what it is.</span></span>

<span data-ttu-id="0f17c-175">Jeśli dodasz kilka więcej pociągnięć Twojej rysowania uruchamia tooget małego Wyostrzanie.</span><span class="sxs-lookup"><span data-stu-id="0f17c-175">If you add some more brush strokes, then your painting starts tooget a little sharper.</span></span>

<span data-ttu-id="0f17c-176">Jeśli masz pociągnięć prawie wystarczającej ilości widać tylko za mało toomake kilku szerokie decyzji.</span><span class="sxs-lookup"><span data-stu-id="0f17c-176">When you have barely enough strokes, you can see just enough toomake some broad decisions.</span></span> <span data-ttu-id="0f17c-177">Jest to innym można toovisit?</span><span class="sxs-lookup"><span data-stu-id="0f17c-177">Is it somewhere I might want toovisit?</span></span> <span data-ttu-id="0f17c-178">Wygląda na to jasny, to wygląda czystej wody — tak, będącą, gdzie użyjemy na urlop.</span><span class="sxs-lookup"><span data-stu-id="0f17c-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="0f17c-179">Jak dodać więcej danych obraz powitania staje się jaśniejszy i bardziej szczegółowe decyzje.</span><span class="sxs-lookup"><span data-stu-id="0f17c-179">As you add more data, hello picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="0f17c-180">Teraz można obejrzeć hello trzy hotels na powitania bank po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="0f17c-180">Now I can look at hello three hotels on hello left bank.</span></span> <span data-ttu-id="0f17c-181">Znasz, naprawdę jak z architektury funkcji hello jedną na pierwszym planie hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f17c-181">You know, I really like hello architectural features of hello one in hello foreground.</span></span> <span data-ttu-id="0f17c-182">I będzie pozostać, hello trzeci piętra.</span><span class="sxs-lookup"><span data-stu-id="0f17c-182">I’ll stay there, on hello third floor.</span></span>

<span data-ttu-id="0f17c-183">Z danymi, które jest odpowiednie, połączony, dokładne oraz za mało, mamy wszystkich składników hello potrzebujemy toodo niektórych nauki wysokiej jakości danych.</span><span class="sxs-lookup"><span data-stu-id="0f17c-183">With data that's relevant, connected, accurate, and enough, we have all hello ingredients we need toodo some high-quality data science.</span></span>

<span data-ttu-id="0f17c-184">Należy się toocheck limit hello innych cztery pliki wideo w *nauki danych dla początkujących* z Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0f17c-184">Be sure toocheck out hello other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f17c-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f17c-185">Next steps</span></span>
* [<span data-ttu-id="0f17c-186">Spróbuj pierwszego eksperymentu analizy danych z usługi Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="0f17c-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="0f17c-187">Pobierz wprowadzenie tooMachine uczenia w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0f17c-187">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
