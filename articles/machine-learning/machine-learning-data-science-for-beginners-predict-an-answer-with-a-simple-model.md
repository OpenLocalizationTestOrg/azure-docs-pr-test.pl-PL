---
title: "Przewidywanie odpowiedzi z modelu regresji proste — usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak utworzyć model regresji proste do prognozowania cen w nauce danych dla początkujących 4 wideo. Obejmuje regresji liniowej z danych docelowych."
keywords: Tworzenie modelu, modelu prostego, prognozowanie cen, model regresji proste
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 24df1823af2610a5111118f47e4cadbcfcc0eff1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="49300-105">Prognozowanie odpowiedzi za pomocą prostego modelu</span><span class="sxs-lookup"><span data-stu-id="49300-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="49300-106">Wideo 4: Nauki danych serii dla początkujących</span><span class="sxs-lookup"><span data-stu-id="49300-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="49300-107">Dowiedz się, jak utworzyć model regresji proste do prognozowania cen romb w nauce danych dla początkujących 4 wideo.</span><span class="sxs-lookup"><span data-stu-id="49300-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="49300-108">Firma Microsoft będzie Rysuj modelu regresji z danych docelowych.</span><span class="sxs-lookup"><span data-stu-id="49300-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="49300-109">Aby uzyskać wykorzystanie serii, obejrzyj je wszystkie.</span><span class="sxs-lookup"><span data-stu-id="49300-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="49300-110">[Przejdź do listy filmów wideo](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="49300-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="49300-111">Inne pliki wideo w tej serii</span><span class="sxs-lookup"><span data-stu-id="49300-111">Other videos in this series</span></span>
<span data-ttu-id="49300-112">*Nauki danych dla początkujących* jest szybkie wprowadzenie do analizy danych w pięciu krótkie wideo.</span><span class="sxs-lookup"><span data-stu-id="49300-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="49300-113">Wideo 1: [danych nauki odpowiedzi na pytania 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sek.)*</span><span class="sxs-lookup"><span data-stu-id="49300-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="49300-114">Wideo 2: [jest gotowy do analizy danych danych?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="49300-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="49300-115">*(4 s 56 min)*</span><span class="sxs-lookup"><span data-stu-id="49300-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="49300-116">Wideo 3: [Zadaj pytanie może odpowiedzieć z danymi](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 s 17 min)*</span><span class="sxs-lookup"><span data-stu-id="49300-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="49300-117">Wideo 4: Odpowiedź z prostego modelu prognozowania</span><span class="sxs-lookup"><span data-stu-id="49300-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="49300-118">Wideo 5: [skopiuj pracy innych osób nauki danych](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sek.)*</span><span class="sxs-lookup"><span data-stu-id="49300-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="49300-119">Zapis: Przewidywanie odpowiedzi z modelu prostego</span><span class="sxs-lookup"><span data-stu-id="49300-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="49300-120">Witamy w czwartym wideo w "danych nauki dla początkujących" serii.</span><span class="sxs-lookup"><span data-stu-id="49300-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span></span> <span data-ttu-id="49300-121">W tym przypadku firma Microsoft budowanie prostego modelu i prognozowanie.</span><span class="sxs-lookup"><span data-stu-id="49300-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="49300-122">A *modelu* jest uproszczone artykuł o naszych danych.</span><span class="sxs-lookup"><span data-stu-id="49300-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="49300-123">Będzie można wyświetlić I znaczenie.</span><span class="sxs-lookup"><span data-stu-id="49300-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="49300-124">Zbieranie odpowiednich, dokładne, połączenie, jest za mało danych</span><span class="sxs-lookup"><span data-stu-id="49300-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="49300-125">Załóżmy, że chcę sklep romb.</span><span class="sxs-lookup"><span data-stu-id="49300-125">Say I want to shop for a diamond.</span></span> <span data-ttu-id="49300-126">Mam pierścień, który należał do mojego babcia z ustawieniem dla romb 1.35 karatach i chcę uzyskać informacje o tym, jaki będzie koszt.</span><span class="sxs-lookup"><span data-stu-id="49300-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span></span> <span data-ttu-id="49300-127">Muszę zrobić Notatnik i pióra do magazynu Biżuteria i I Zanotuj cen wszystkich diamentów w przypadku i ile porównać w carats.</span><span class="sxs-lookup"><span data-stu-id="49300-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span></span> <span data-ttu-id="49300-128">Począwszy od pierwszego romb - carats 1.01 jego i 7,366 $.</span><span class="sxs-lookup"><span data-stu-id="49300-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="49300-129">Teraz przejdź i zrób to inne diamentowego w magazynie.</span><span class="sxs-lookup"><span data-stu-id="49300-129">Now I go through and do this for all the other diamonds in the store.</span></span>

![Kolumny danych romb](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="49300-131">Zwróć uwagę, że naszej listy ma dwie kolumny.</span><span class="sxs-lookup"><span data-stu-id="49300-131">Notice that our list has two columns.</span></span> <span data-ttu-id="49300-132">Każda kolumna ma inny atrybut — wagę carats i cen — oraz każdy wiersz jest pojedynczego punktu danych reprezentujący pojedynczego romb.</span><span class="sxs-lookup"><span data-stu-id="49300-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="49300-133">Faktycznie utworzyliśmy małą tutaj — zestawu danych tabeli.</span><span class="sxs-lookup"><span data-stu-id="49300-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="49300-134">Zwróć uwagę, że spełnia kryteriów jakości:</span><span class="sxs-lookup"><span data-stu-id="49300-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="49300-135">Dane są **odpowiednich** -wagi ostatecznie jest powiązana do ceny</span><span class="sxs-lookup"><span data-stu-id="49300-135">The data is **relevant** - weight is definitely related to price</span></span>
* <span data-ttu-id="49300-136">Ma ona **dokładne** -możemy double-checked ceny, które firma Microsoft Zapisz</span><span class="sxs-lookup"><span data-stu-id="49300-136">It's **accurate** - we double-checked the prices that we write down</span></span>
* <span data-ttu-id="49300-137">Ma ona **połączone** — istnieją nie spacji w dowolnej z tych kolumn</span><span class="sxs-lookup"><span data-stu-id="49300-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="49300-138">I jak zajmiemy się tym, ma **za mało** odpowiedź na pytanie naszych</span><span class="sxs-lookup"><span data-stu-id="49300-138">And, as we'll see, it's **enough** data to answer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="49300-139">Zadaj pytanie sharp</span><span class="sxs-lookup"><span data-stu-id="49300-139">Ask a sharp question</span></span>
<span data-ttu-id="49300-140">Obecnie firma Microsoft będzie stanowić naszych zapytania w sposób sharp: "będzie kosztem, jaki kupić romb karatach 1.35?"</span><span class="sxs-lookup"><span data-stu-id="49300-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="49300-141">Naszej listy nie ma romb 1.35 karatach, dlatego firma Microsoft będzie konieczne Użyj pozostałej części danych, aby uzyskać odpowiedzi na pytanie.</span><span class="sxs-lookup"><span data-stu-id="49300-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span></span>

## <a name="plot-the-existing-data"></a><span data-ttu-id="49300-142">Istniejących danych</span><span class="sxs-lookup"><span data-stu-id="49300-142">Plot the existing data</span></span>
<span data-ttu-id="49300-143">W pierwszej kolejności robimy jest poziomej linii numer o nazwie osi, do wykresu wag.</span><span class="sxs-lookup"><span data-stu-id="49300-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span></span> <span data-ttu-id="49300-144">Zakres wag jest 0-2, dlatego firma Microsoft będzie rysowanie linii obejmujący zakresu i umieścić znaczniki dla każdego połowa karatach.</span><span class="sxs-lookup"><span data-stu-id="49300-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="49300-145">Firma Microsoft będzie dalej Rysuj osi pionowej do rejestrowania ceny i podłącz go do osi poziomej wagi.</span><span class="sxs-lookup"><span data-stu-id="49300-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span></span> <span data-ttu-id="49300-146">Są to w jednostkach kwoty.</span><span class="sxs-lookup"><span data-stu-id="49300-146">This will be in units of dollars.</span></span> <span data-ttu-id="49300-147">Teraz mamy zestaw współrzędnych osi.</span><span class="sxs-lookup"><span data-stu-id="49300-147">Now we have a set of coordinate axes.</span></span>

![Osie wagi i cen](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="49300-149">Chcemy się teraz pobrać te dane i włącz go do *wykres punktowy*.</span><span class="sxs-lookup"><span data-stu-id="49300-149">We're going to take this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="49300-150">Jest to dobry sposób na wizualizowania wartości liczbowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="49300-150">This is a great way to visualize numerical data sets.</span></span>

<span data-ttu-id="49300-151">Dla pierwszego punktu danych Firma Microsoft eyeball pionowych linii w 1.01 carats.</span><span class="sxs-lookup"><span data-stu-id="49300-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="49300-152">Następnie możemy eyeball poziomych linii w 7,366 $.</span><span class="sxs-lookup"><span data-stu-id="49300-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="49300-153">Jeżeli spełniają one możemy zwrócić kropką.</span><span class="sxs-lookup"><span data-stu-id="49300-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="49300-154">Reprezentuje naszym pierwszym romb.</span><span class="sxs-lookup"><span data-stu-id="49300-154">This represents our first diamond.</span></span>

<span data-ttu-id="49300-155">Teraz możemy przejść przez każdego romb na tej liście i tak samo postąpić.</span><span class="sxs-lookup"><span data-stu-id="49300-155">Now we go through each diamond on this list and do the same thing.</span></span> <span data-ttu-id="49300-156">Kiedy jesteśmy za pośrednictwem jest będziemy mieć: licznych kropkami, jeden dla każdej romb.</span><span class="sxs-lookup"><span data-stu-id="49300-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![Wykres punktowy](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-the-model-through-the-data-points"></a><span data-ttu-id="49300-158">Rysuj modelu punktów danych</span><span class="sxs-lookup"><span data-stu-id="49300-158">Draw the model through the data points</span></span>
<span data-ttu-id="49300-159">Teraz można spojrzeć na squint i kropek kolekcji wygląda jak linia fat, rozmytego.</span><span class="sxs-lookup"><span data-stu-id="49300-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="49300-160">Możemy zająć naszych znacznika i rysowanie linii prostej za jego pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="49300-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="49300-161">Za pomocą rysowania linii, utworzyliśmy *modelu*.</span><span class="sxs-lookup"><span data-stu-id="49300-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="49300-162">Należy traktować jako biorąc rzeczywistych i wersji simplistic kreskówki go.</span><span class="sxs-lookup"><span data-stu-id="49300-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="49300-163">Teraz kreskówki jest nieprawidłowy — wiersza nie jest akceptowana wszystkich punktów danych.</span><span class="sxs-lookup"><span data-stu-id="49300-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span></span> <span data-ttu-id="49300-164">Jednak jest przydatne uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="49300-164">But, it's a useful simplification.</span></span>

![Regresji liniowej](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="49300-166">Fakt, że wszystkie punkty nie przechodzą dokładnie wiersz jest OK.</span><span class="sxs-lookup"><span data-stu-id="49300-166">The fact that all the dots don't go exactly through the line is OK.</span></span> <span data-ttu-id="49300-167">Analityków danych opisano to przez informujący, że jest model — jest to wiersz - i następnie każdego punktu ma kilka *szumu* lub *wariancji* skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="49300-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="49300-168">Podstawowej relacji doskonałe, a następnie istnieje świata niepowtarzalne, rzeczywistych, w której dodaje szumu i niedokładność.</span><span class="sxs-lookup"><span data-stu-id="49300-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="49300-169">Ponieważ próbujemy odpowiedzi na pytanie *ile?* jest to *regresji*.</span><span class="sxs-lookup"><span data-stu-id="49300-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="49300-170">I dlatego firma Microsoft korzysta z prostej, jest *regresji liniowej*.</span><span class="sxs-lookup"><span data-stu-id="49300-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-the-model-to-find-the-answer"></a><span data-ttu-id="49300-171">Użyj modelu, aby znaleźć odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="49300-171">Use the model to find the answer</span></span>
<span data-ttu-id="49300-172">Teraz mamy modelu i poprosimy go naszych pytanie: jaka będzie romb 1.35 karatach koszt?</span><span class="sxs-lookup"><span data-stu-id="49300-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="49300-173">Odpowiedzi na pytanie naszych, firma Microsoft oka 1.35 carats i rysowanie linii pionowej.</span><span class="sxs-lookup"><span data-stu-id="49300-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="49300-174">Gdzie go przecina wiersza modelu możemy eyeball linii poziomej osi dolara ($).</span><span class="sxs-lookup"><span data-stu-id="49300-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span></span> <span data-ttu-id="49300-175">Trafienia jego prawej strony na 10 000.</span><span class="sxs-lookup"><span data-stu-id="49300-175">It hits right at 10,000.</span></span> <span data-ttu-id="49300-176">Wysięgnik!</span><span class="sxs-lookup"><span data-stu-id="49300-176">Boom!</span></span> <span data-ttu-id="49300-177">To odpowiedź: romb 1.35 karatach koszty około 10 000.</span><span class="sxs-lookup"><span data-stu-id="49300-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Znajdź odpowiedzi na modelu](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="49300-179">Utwórz przedział ufności</span><span class="sxs-lookup"><span data-stu-id="49300-179">Create a confidence interval</span></span>
<span data-ttu-id="49300-180">Jest fizyczne do zastanawiasz się, jak dokładne jest to prognozowania.</span><span class="sxs-lookup"><span data-stu-id="49300-180">It's natural to wonder how precise this prediction is.</span></span> <span data-ttu-id="49300-181">Jest grupowaniu można sprawdzić, czy romb 1.35 karatach będzie bardzo bliski 10 000, lub znacznie większej lub mniejszej.</span><span class="sxs-lookup"><span data-stu-id="49300-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span></span> <span data-ttu-id="49300-182">Aby ustalić tę możliwość, umożliwia Rysuj koperty wokół regresji, który zawiera większość punktów.</span><span class="sxs-lookup"><span data-stu-id="49300-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span></span> <span data-ttu-id="49300-183">Ten koperty jest wywoływana naszych *przedział ufności*: jesteśmy pretty pewność, że ceny mieszczą się w tym koperty, ponieważ w ciągu ostatnich większość z nich.</span><span class="sxs-lookup"><span data-stu-id="49300-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span></span> <span data-ttu-id="49300-184">Firma Microsoft Rysuj dwóch więcej poziome linie, z których wiersza 1.35 karatach przecina góry i u dołu tej koperty.</span><span class="sxs-lookup"><span data-stu-id="49300-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span></span>

![Przedział ufności](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="49300-186">Teraz możemy powiedzieć coś o naszych przedział ufności: możemy powiedzieć bez obaw czy cena romb 1.35 karatach jest około $ 10 000 -, ale może być możliwie jak $8000 i może być możliwie jak 12 000.</span><span class="sxs-lookup"><span data-stu-id="49300-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="49300-187">Skończymy, bez matematyczne lub komputerów</span><span class="sxs-lookup"><span data-stu-id="49300-187">We're done, with no math or computers</span></span>
<span data-ttu-id="49300-188">Robiliśmy, jakie analityków danych uzyskać płatną zrobić i robiliśmy tylko za pomocą rysowania:</span><span class="sxs-lookup"><span data-stu-id="49300-188">We did what data scientists get paid to do, and we did it just by drawing:</span></span>

* <span data-ttu-id="49300-189">Firma Microsoft zadawane pytania firma Microsoft może odpowiedzi z danymi</span><span class="sxs-lookup"><span data-stu-id="49300-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="49300-190">Budujemy *modelu* przy użyciu *regresji liniowej*</span><span class="sxs-lookup"><span data-stu-id="49300-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="49300-191">Wprowadziliśmy *prognozowania*, wraz z *przedział ufności*</span><span class="sxs-lookup"><span data-stu-id="49300-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="49300-192">I nie używamy matematyczne lub komputerów Aby wykonać to zadanie.</span><span class="sxs-lookup"><span data-stu-id="49300-192">And we didn't use math or computers to do it.</span></span>

<span data-ttu-id="49300-193">Teraz, jeśli tak samo, jak gdyby było więcej informacji...</span><span class="sxs-lookup"><span data-stu-id="49300-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="49300-194">Przecięcie romb</span><span class="sxs-lookup"><span data-stu-id="49300-194">the cut of the diamond</span></span>
* <span data-ttu-id="49300-195">kolory (jak blisko romb jest jest białe)</span><span class="sxs-lookup"><span data-stu-id="49300-195">color variations (how close the diamond is to being white)</span></span>
* <span data-ttu-id="49300-196">Liczba dołączenia w romb</span><span class="sxs-lookup"><span data-stu-id="49300-196">the number of inclusions in the diamond</span></span>

<span data-ttu-id="49300-197">.. .i firma musiałaby większą liczbę kolumn.</span><span class="sxs-lookup"><span data-stu-id="49300-197">...then we would have had more columns.</span></span> <span data-ttu-id="49300-198">W takim przypadku matematyczne staje się przydatne.</span><span class="sxs-lookup"><span data-stu-id="49300-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="49300-199">Jeśli masz więcej niż dwie kolumny jest trudna do rysowania kropki w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="49300-199">If you have more than two columns, it's hard to draw dots on paper.</span></span> <span data-ttu-id="49300-200">Obliczenia umożliwia bardzo dobrze nadające się tego wiersza lub tej płaszczyzny do danych.</span><span class="sxs-lookup"><span data-stu-id="49300-200">The math lets you fit that line or that plane to your data very nicely.</span></span>

<span data-ttu-id="49300-201">Ponadto jeśli zamiast tylko kilku karo, było dwa tysiące lub dwóch milionów, a następnie wykonaj pracy znacznie szybciej z komputerem.</span><span class="sxs-lookup"><span data-stu-id="49300-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="49300-202">Obecnie zajmowaliśmy sposób wykonywania regresji liniowej i wprowadziliśmy prognozowania, przy użyciu danych.</span><span class="sxs-lookup"><span data-stu-id="49300-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="49300-203">Należy koniecznie zapoznaj się z innych plików wideo "Danych nauki dla początkujących" z Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49300-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49300-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49300-204">Next steps</span></span>
* [<span data-ttu-id="49300-205">Spróbuj pierwszego eksperymentu analizy danych z usługi Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="49300-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="49300-206">Wprowadzenie do uczenia maszynowego w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="49300-206">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
