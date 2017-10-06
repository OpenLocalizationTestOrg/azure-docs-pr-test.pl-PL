---
title: "usługi w chmurze Azure z usługą Azure CDN aaaIntegrate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy usługi w chmurze służy do zawartości z punktu końcowego zintegrowane usługi Azure CDN"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a>Integracja z usługą w chmurze z usługą Azure CDN
Usługi w chmurze można zintegrować z usługą Azure CDN, obsługująca zawartość z lokalizacji usługi chmury hello. To podejście umożliwia hello następujące korzyści:

* Łatwe wdrażanie i aktualizowanie obrazów, skrypty i arkusze stylów w katalogu projektu usługi chmury
* Łatwo przeprowadzić uaktualnienie hello pakietów NuGet w usługi w chmurze, np. jQuery lub ładowania początkowego wersji
* Zarządzanie aplikacji sieci Web i obsługiwane sieci CDN zawartości wszystkich z hello sam interfejs programu Visual Studio
* Przepływ pracy ujednoliconego wdrożenia dla aplikacji sieci Web i zawartości obsługiwanych w sieci CDN
* Integracja z usługą Azure CDN ASP.NET tworzenie pakietów i minimalizowanie

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym samouczku przedstawiono sposób:

* [Integracja punktu końcowego usługi Azure CDN z usługi w chmurze i udostępniać zawartość statyczną na stronach sieci Web z usługi Azure CDN](#deploy)
* [Skonfiguruj ustawienia pamięci podręcznej zawartość statyczną w usługi w chmurze](#caching)
* [Udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN](#controller)
* [Służą powiązane i zminimalizowane zawartości za pomocą usługi Azure CDN przy zachowaniu skryptu hello debugowanie w programie Visual Studio](#bundling)
* [Skonfigurować powrotu skryptów i CSS z usługi Azure CDN jest w trybie offline](#fallback)

## <a name="what-you-will-build"></a>Zostanie utworzona
Wdrażania roli sieci Web usługi chmury, za pomocą hello domyślnego szablonu platformy ASP.NET MVC, Dodaj kod tooserve zawartości z zintegrowane usługi Azure CDN, takich jak obraz, wyniki akcji kontrolera i pliki obsługi języka JavaScript i CSS hello domyślnej i również napisać kod tooconfigure hello mechanizm rezerwowy umożliwiający pakiety obsługiwanych w przypadku hello tego hello CDN jest w trybie offline.

## <a name="what-you-will-need"></a>Dane będą potrzebne
Ten samouczek ma hello następujące wymagania wstępne:

* Aktywny [konta Microsoft Azure](/account/)
* Visual Studio 2015 z [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Należy toocomplete konto platformy Azure w tym samouczku:
> 
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — otrzymasz kredyt płatnej usług platformy Azure można użyć tootry wychodzących, a nawet po wyczerpaniu kredytu możesz zachować konto hello i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web.
> * Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -subskrypcji Your MSDN otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Wdrażanie usługi w chmurze
W tej sekcji zostanie wdrażanie hello domyślnego szablonu aplikacji platformy ASP.NET MVC w roli programu Visual Studio 2015 tooa chmury usługi sieci Web i zintegrować ją z nowy punkt końcowy CDN. Wykonaj poniższe instrukcje hello:

1. W programie Visual Studio 2015, Utwórz nową usługę w chmurze Azure z paska menu hello przechodząc zbyt**pliku > Nowy > Projekt > chmura > usługi w chmurze Azure**. Nadaj mu nazwę, a następnie kliknij przycisk **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Wybierz **roli sieci Web ASP.NET** i kliknij przycisk hello  **>**  przycisku. Kliknij przycisk OK.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Wybierz **MVC** i kliknij przycisk **OK**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Teraz Opublikuj ten tooan roli sieci Web usługi w chmurze Azure. Kliknij prawym przyciskiem myszy projekt usługi w chmurze hello i wybierz **publikowania**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Jeśli dany komputer nie ma jeszcze podpisany w Microsoft Azure, kliknij przycisk hello **Dodaj konto...**  hello listy rozwijanej, a następnie kliknij przycisk **Dodaj konto** elementu menu.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. W hello strony logowania Zaloguj się przy użyciu hello konta Microsoft użyty tooactivate konta platformy Azure.
7. Gdy użytkownik jest zarejestrowany, kliknij przycisk **dalej**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Przy założeniu, że nie utworzono konta usługi lub magazynu chmury, Visual Studio pomoże utworzyć jednocześnie. W hello **Tworzenie usługi w chmurze i konto** okna dialogowego, nazwa żądanej usługi hello typu i hello wybierz odpowiedni region. Następnie kliknij pozycję **Utwórz**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. W hello strona ustawień publikowania, sprawdź konfigurację hello i kliknij przycisk **publikowania**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > Witaj proces publikowania dla usługi w chmurze zajmuje dużo czasu. wprowadzić Hello Włącz narzędzia Web Deploy w dla wszystkich ról opcji debugowania usługi w chmurze znacznie szybsza, bo zapewniając tooyour aktualizacje szybkiego (ale tymczasowe) role sieci Web. Aby uzyskać więcej informacji na temat tej opcji, zobacz [publikowania usługi w chmurze przy użyciu narzędzia Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Gdy hello **dziennik aktywności programu Microsoft Azure** pokazuje, że stan publikowania **Ukończono**, spowoduje utworzenie punktu końcowego usługi CDN, który jest zintegrowany z usługą w chmurze.
   
   > [!WARNING]
   > Jeśli po opublikowaniu hello wdrożona usługa w chmurze wyświetla komunikat o błędzie, prawdopodobnie ponieważ korzysta z usługi w chmurze hello wdrożeniu [gościa systemu operacyjnego, który nie obejmuje .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Można obejść ten problem przez [wdrażanie .NET 4.5.2 jako zadanie uruchamiania](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Tworzenie nowego profilu CDN
Profil CDN jest kolekcją punktów końcowych usługi CDN.  Każdy profil zawiera jeden lub więcej punktów końcowych usługi CDN.  Możesz toouse wiele profilów tooorganize punktami końcowymi CDN według domeny internetowej, aplikacji sieci web lub innych kryteriów.

> [!TIP]
> Jeśli masz już profil CDN ma toouse w tym samouczku, kontynuować zbyt[utworzyć nowy punkt końcowy CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Tworzenie nowego punktu końcowego usługi CDN
**toocreate nowy punkt końcowy CDN dla konta magazynu**

1. W hello [portalu zarządzania Azure](https://portal.azure.com), przejdź tooyour profilu CDN.  Użytkownik może został on przypięty toohello pulpitu nawigacyjnego w poprzednim kroku hello.  Jeśli użytkownik nie, możesz go znaleźć, klikając **Przeglądaj**, następnie **profilów usługi CDN**, i klikając profil hello planujesz tooadd punkt końcowy.
   
    zostanie wyświetlony blok profilu CDN Hello.
   
    ![Profil CDN][cdn-profile-settings]
2. Kliknij przycisk hello **Dodawanie punktu końcowego** przycisku.
   
    ![Przycisk dodawania punktu końcowego][cdn-new-endpoint-button]
   
    Witaj **Dodawanie punktu końcowego** zostanie wyświetlony blok.
   
    ![Blok dodawania punktu końcowego][cdn-add-endpoint]
3. Wprowadź **nazwę** dla tego punktu końcowego usługi CDN.  Ta nazwa będzie używana tooaccess buforowanych zasobów w domenie hello `<EndpointName>.azureedge.net`.
4. W hello **typ źródła** listy rozwijanej wybierz *usługi w chmurze*.  
5. W hello **nazwę hosta źródła** listy rozwijanej wybierz usługi w chmurze.
6. Pozostaw ustawienia domyślne hello **ścieżki źródła**, **nagłówka hosta źródła**, i **port protokołu/źródła**.  Należy określić co najmniej jeden protokół (HTTP lub HTTPS).
7. Kliknij przycisk hello **Dodaj** toocreate przycisk hello nowy punkt końcowy.
8. Po utworzeniu punktu końcowego hello pojawia się na liście punktów końcowych dla profilu hello. Widok listy Hello pokazuje tooaccess toouse adres URL hello w pamięci podręcznej zawartości, a także domeny źródła hello.
   
    ![Punkt końcowy usługi CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > punkt końcowy Hello nie natychmiast będą dostępne do użycia.  Too90 minut toopropagate rejestracji hello hello sieci CDN może potrwać. Użytkownicy, którzy natychmiast podjąć próbę nazwy domeny usługi CDN hello toouse może zostać wyświetlony kod stanu 404, dopóki hello zawartość jest dostępna za pośrednictwem hello CDN.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Test hello punktu końcowego CDN
Gdy stan publikowania hello jest **Ukończono**, Otwórz okno przeglądarki i przejść za**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. Moje ustawienia ten adres URL jest:

    http://camservice.azureedge.net/Content/bootstrap.css

Które odpowiada toohello po źródłowy adres URL w punkcie końcowym CDN hello:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Po przejściu się zbyt**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, w zależności od przeglądarki, będzie zostanie wyświetlony monit o toodownload lub Otwórz hello bootstrap.css który pochodzi z opublikowanych aplikacji sieci Web.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

Podobnie można uzyskać dostępu do dowolny publicznie dostępny adres URL w  **http://*&lt;serviceName >*.cloudapp.net/** bezpośrednio z punktu końcowego CDN. Na przykład:

* Pliku ze ścieżki/Script hello js
* Dowolny plik zawartości z hello argumencie / ścieżki
* Wszelkie kontrolera/działania
* Jeśli ciąg zapytania hello jest włączona na punkt końcowy CDN dowolny adres URL z ciągami zapytań

W rzeczywistości z hello powyżej konfiguracji, może obsługiwać usługę chmury całego hello w  **http://*&lt;cdnName >*.azureedge.net/**. Jeśli można przejść za**http://camservice.azureedge.net/ ** pobrać hello wyniku akcji z głównej/indeksu.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Oznacza to, mimo że zawsze jest dobrym rozwiązaniem tooserve usługi w chmurze całego za pośrednictwem usługi Azure CDN. 

CDN z optymalizacją dostarczania statycznych nie zawsze przyspiesza dostarczania dynamiczne zasoby, które nie mają w pamięci podręcznej toobe lub bardzo często są aktualizowane, ponieważ hello CDN musi ściągnięcia nowej wersji hello zasobów z serwera źródłowego hello bardzo często. W tym scenariuszu można włączyć [dynamiczne przyspieszenie lokacji](cdn-dynamic-site-acceleration.md) optymalizacji (DSA) na punkt końcowy CDN używający różnych technik toospeed dostarczenia-buforowalnej zasobów dynamicznych. 

Jeśli masz lokacji z różnymi statycznych i dynamicznych zawartości można tooserve zawartość statyczną z sieci CDN z typem optymalizacji statyczne (np. dostarczenie ogólne sieci web), a zawartość dynamiczną tooserve bezpośrednio z serwera źródłowego hello lub za pośrednictwem sieci CDN punkt końcowy z optymalizacją DSA włączone w przypadku. końcowy toothat ma już widoczny, jak tooaccess zawartość poszczególnych plików z punktu końcowego CDN hello. I opisano sposób tooserve akcji kontrolera określonej za pomocą określonego punktu końcowego sieci CDN w obsługiwać zawartość z akcji kontrolera, za pomocą usługi Azure CDN.

Alternatywą Hello jest toodetermine, którego zawartość tooserve z usługi Azure CDN na podstawie przypadku — w usłudze w chmurze. końcowy toothat ma już widoczny, jak tooaccess zawartość poszczególnych plików z punktu końcowego CDN hello. I opisano, jak tooserve akcji kontrolera określonej za pomocą hello punkt końcowy sieci CDN w [udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Skonfiguruj opcje buforowania plików statycznych w usłudze w chmurze
Azure CDN integracji usługi w chmurze można określić sposób statycznych toobe zawartości w pamięci podręcznej w hello punktu końcowego CDN. toodo, otwórz *Web.config* z roli sieci Web projektu (np. WebRole1) i Dodaj `<staticContent>` element zbyt`<system.webServer>`. Witaj XML poniżej konfiguruje hello tooexpire pamięci podręcznej w 3 dni.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Po wykonaniu tej czynności wszystkie pliki statyczne z usługi w chmurze będzie obserwować hello same reguły w pamięci podręcznej usługi CDN. Bardziej szczegółowego kontrolowania ustawień pamięci podręcznej, należy dodać *Web.config* plików do folderu, a następnie dodaj ustawienia istnieje. Na przykład dodać *Web.config* pliku toohello *\Content* folderu i Zamień hello zawartości z powitania po XML:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

To ustawienie powoduje, że wszystkie pliki statyczne z hello *\Content* toobe folderu pamięci podręcznej przez 15 dni.

Aby uzyskać więcej informacji na temat tooconfigure hello `<clientCache>` elementu, zobacz [pamięci podręcznej klienta &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

W [udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN](#controller), można również opisano, jak można skonfigurować ustawienia pamięci podręcznej dla wyników akcji kontrolera w hello CDN pamięci podręcznej.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Udostępniać zawartość z akcji kontrolera, za pomocą usługi Azure CDN
Po zintegrowaniu rolę sieci Web usługi w chmurze z usługą Azure CDN jest stosunkowo łatwa tooserve zawartości z akcji kontrolera za pośrednictwem hello Azure CDN. Inne niż obsługująca chmury usługi bezpośrednio za pomocą usługi Azure CDN (zostało to pokazane powyżej), [Maarten Balliauw](https://twitter.com/maartenballiauw) przedstawiono toodo go to MemeGenerator kontrolera w [zmniejsza opóźnienie w sieci web hello z hello Azure CDN ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). I będzie po prostu go odtworzyć w tym miejscu.

Załóżmy, że w usłudze w chmurze ma memes toogenerate na podstawie małych obrazu Norris Jan (photo przez [światła Alan](http://www.flickr.com/photos/alan-light/218493788/)), takich jak to:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Masz prostą `Index` akcję, która umożliwia klientom Witaj superlatywy hello toospecify w obrazie hello następnie generuje meme powitania po przesyłać toohello akcji. Ponieważ jest Norris Jan, można oczekiwać toobecome tej strony bardzo popularny globalnie. Jest to przykład obsługę częściowo dynamicznej zawartości z usługi Azure CDN.

Wykonaj kroki hello powyżej toosetup tej akcji kontrolera:

1. W hello *\Controllers* folderu, Utwórz nowy plik .cs o nazwie *MemeGeneratorController.cs* i Zastąp hello zawartości z hello następującego kodu. Należy się tooreplace hello wyróżnione części z nazwy CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Kliknij prawym przyciskiem myszy domyślne hello `Index()` akcji i wybierz **Dodaj widok**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Zaakceptuj ustawienia hello poniżej i kliknij przycisk **Dodaj**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Otwórz nowy hello *Views\MemeGenerator\Index.cshtml* i Zastąp zawartość hello powitania od prostego HTML składania superlatywy hello:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Ponownie opublikować hello usługi w chmurze i przejdź zbyt**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** w przeglądarce.

Podczas przesyłania wartości formularza hello zbyt`/MemeGenerator/Index`, hello `Index_Post` metoda akcji zwraca toohello łącze `Show` metodę akcji za pomocą hello odpowiednich identyfikator wejściowy. Po kliknięciu łącza hello przejściu hello następującego kodu:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Jeśli lokalne debuger jest dołączony, zostanie wyświetlona hello regularne debugowania środowisko przy użyciu przekierowania lokalnego. Jeśli jest on uruchomiony hello w usłudze w chmurze, następnie go spowoduje przekierowanie do:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Które odpowiada toohello po źródłowy adres URL na punkt końcowy CDN:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Następnie można użyć hello `OutputCacheAttribute` atrybutu na powitania `Generate` toospecify metody jak mają być buforowane hello wynik akcji, które podlegają Azure CDN. Poniższy kod Hello Określ pamięci podręcznej ważności 1 godzina (3600 sekund).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Podobnie użytkownik może służyć się zawartość z dowolnego akcji kontrolera w usłudze w chmurze za pośrednictwem sieci Azure CDN z opcją buforowania hello potrzeby.

W następnej sekcji hello I opisano sposób tooserve hello powiązane i zminimalizowane skryptów i CSS za pomocą usługi Azure CDN.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Integracja z usługą Azure CDN ASP.NET tworzenie pakietów i minimalizowanie
Arkusze stylów CSS i skrypty Zmień rzadko i głównym nadają się do hello Azure CDN pamięci podręcznej. Obsługa hello całej roli sieci Web za pomocą programu Azure CDN jest hello Najprostszym sposobem toointegrate tworzenie pakietów i minimalizowanie z usługą Azure CDN. Jednak można dowolnie może nie toodo to, I opisano, jak toodo go przy zachowaniu hello potrzeby środowisko programistyczne ASP.NET tworzenie pakietów i minimalizowanie, takich jak:

* Środowisko trybu dużą debugowania
* Prostsze wdrożenia
* Tooclients natychmiastowej aktualizacji dla uaktualnienia wersji skryptu/CSS
* Mechanizm rezerwowy, gdy punkt końcowy CDN nie powiodło się.
* Minimalizowanie modyfikacji kodu

W hello **WebRole1** projektu, który został utworzony w [integracji punktu końcowego usługi Azure CDN z witryny sieci Web platformy Azure i udostępniać zawartość statyczną na stronach sieci Web z usługi Azure CDN](#deploy), otwórz *App_Start\ BundleConfig.cs* i spójrz na powitania `bundles.Add()` wywołania metody.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Witaj najpierw `bundles.Add()` instrukcja dodaje pakiet skryptu w katalogu wirtualnego hello `~/bundles/jquery`. Następnie otwórz *Views\Shared\_Layout.cshtml* toosee sposób renderowania tagu pakietu skryptu hello. Powinny być hello stanie toofind po wierszu kodu Razor:

    @Scripts.Render("~/bundles/jquery")

Po uruchomieniu tego kodu Razor w roli sieci Web Azure hello będą zawierały `<script>` tagu hello skryptu pakietu podobne toohello poniżej:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Jednak gdy jest uruchamiana w programie Visual Studio, wpisując `F5`, go spowoduje, że każdy plik skryptu w pakiecie hello pojedynczo (w przypadku hello powyżej, skryptu tylko jeden plik jest w pakiecie hello):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Dzięki temu możesz kod JavaScript hello toodebug w środowisku projektowania podczas zmniejszenie połączeń współbieżnych klienta (grupowania) i poprawy pliku Pobierz wydajności (minimalizowanie) w środowisku produkcyjnym. Jest toopreserve wspaniałych funkcji, dzięki integracji usługi Azure CDN. Ponadto, ponieważ hello renderowane pakietu już zawiera ciąg wersji automatycznie wygenerowaną, ma tooreplicate, które funkcje tak hello po zaktualizowaniu wersji jQuery za pośrednictwem pakietu NuGet, mogą być aktualizowane po stronie klienta hello jak najszybciej możliwe.

Wykonaj kroki hello poniżej toointegration ASP.NET tworzenie pakietów i minimalizowanie z punktu końcowego CDN.

1. W *App_Start\BundleConfig.cs*, zmodyfikuj hello `bundles.Add()` toouse metody innej [Konstruktor pakietu](http://msdn.microsoft.com/library/jj646464.aspx), który określa adres usługi CDN. toodo hello, Zastąp `RegisterBundles` definicję metody z hello następującego kodu:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Należy się tooreplace `<yourCDNName>` hello nazwą Twojej usługi Azure CDN.
   
    Prosty opis ustawienie `bundles.UseCdn = true` i dodać dokładnie przygotowanego pakietu tooeach adresu CDN. Na przykład hello pierwszy konstruktora w kodzie hello:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    jest hello taki sam jak:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Ten konstruktor informuje ASP.NET tworzenie pakietów i minimalizowanie toorender skryptu poszczególnych plików podczas debugowania lokalnie, ale użyj hello określona zagrożona skryptu hello tooaccess adresu CDN. Zwróć jednak uwagę dwie najważniejsze czynniki z dokładnie przygotowanego CDN adres URL:
   
   * Hello źródła dla tego adresu URL usługi CDN jest `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, który jest rzeczywiście hello katalog wirtualny hello skryptu pakietu w usłudze w chmurze.
   * Ponieważ używasz konstruktora CDN hello tag skryptu CDN dla pakietu hello nie zawiera już hello są generowane automatycznie ciąg wersji w hello renderowane adresu URL. Musisz ręcznie wygenerować ciąg wersji unikatowy każdorazowego pakiet skryptu hello jest zmodyfikowany tooforce pamięci podręcznej pominięte w sieci Azure CDN. At hello sam czas ten ciąg wersji unikatowy musi pozostać niezmienione za pośrednictwem życia hello hello wdrożenia toomaximize trafień w pamięci podręcznej w sieci Azure CDN, po wdrożeniu pakietu hello.
   * Witaj ciągu zapytania v = < W.X.Y.Z > ściąga z *Properties\AssemblyInfo.cs* w projekcie roli sieci Web. Przepływ pracy wdrożenia, który zawiera przyrostową wersję zestawu hello każdym publikowaniu tooAzure może mieć. Lub, można zmodyfikować *Properties\AssemblyInfo.cs* w ciągu wersji projektu tooautomatically przyrostu hello za każdym razem, gdy kompilacji, przy użyciu hello wieloznaczny "*". Na przykład:
     
        [zestawu: AssemblyVersion("1.0.0.*")]
     
     Wszystkie inne toostreamline strategii generowania unikatowy ciąg dla hello życia wdrożenia będzie działać w tym miejscu.
2. Ponownie opublikować hello chmury dostępu i usługa hello strony głównej.
3. Widok hello kodu HTML dla strony hello. Powinno być możliwe toosee hello renderowane zawierające ciąg wersji unikatowy za każdym razem, gdy opublikować zmian usługi w chmurze tooyour adresu CDN. Na przykład:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. W programie Visual Studio debugowanie hello usługi w chmurze w programie Visual Studio, wpisując `F5`.,
5. Widok hello kodu HTML dla strony hello. Będą również widzieć każdego pliku skryptu indywidualnie renderowane, dzięki czemu mają debugowania spójne środowisko w programie Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Mechanizm rezerwowy umożliwiający CDN adresy URL
Gdy punktu końcowego usługi Azure CDN nie powiedzie się z jakiegokolwiek powodu, ma toobe Twojego strony sieci Web inteligentne za mało tooaccess serwera sieci Web źródła jako opcji rezerwowej hello ładowania JavaScript lub ładowania początkowego. Jest wystarczające toolose obrazów w witrynie sieci Web powodu niedostępności tooCDN, ale wiele poważniejsze toolose strony ważnych funkcji udostępnianych przez usługę własne skrypty i arkusze stylów.

Witaj [pakietu](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) klasa zawiera właściwość o nazwie [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) umożliwiająca tooconfigure hello rezerwowy mechanizm awarii sieci CDN. toouse tę właściwość, wykonaj poniższe kroki hello:

1. W projekcie roli sieci Web otwórz *App_Start\BundleConfig.cs*, gdzie adresu CDN jest dodana w każdym [Konstruktor pakietu](http://msdn.microsoft.com/library/jj646464.aspx)i wprowadź następujące hello wyróżnione zmiany toohello mechanizm rezerwowy tooadd Domyślne pakiety:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Gdy `CdnFallbackExpression` jest niezerowa, skrypt jest wstrzykuje tootest hello HTML czy hello pakietu została pomyślnie załadowana i, jeśli nie, uzyskać dostęp do pakietu hello bezpośrednio z serwera sieci Web źródła hello. Ta właściwość musi toobe zestaw tooa JavaScript wyrażenie, które sprawdza, czy hello odpowiednich CDN pakietu jest poprawnie załadowany. wyrażenie Hello potrzebne tootest zgodnie z zawartością toohello różni się każdego pakietu. Dla pakietów domyślne hello powyżej:
   
   * `window.jquery`jest zdefiniowany w jquery {wersja}-js
   * `$.validator`jest zdefiniowany w jquery.validate.js
   * `window.Modernizr`jest zdefiniowany w modernizer {wersja}-js
   * `$.fn.modal`jest zdefiniowany w bootstrap.js
     
     Zwróć uwagę, że nie ustawić CdnFallbackExpression dla hello `~/Cointent/css` pakietu. Ponieważ jest obecnie [usterkę w System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) który injects `<script>` tagu hello oczekiwano rezerwowy CSS zamiast hello `<link>` tagu.
     
     Istnieje, jednak duże [powrotu pakietu styl](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferowane przez [Członkowskimi konsultacji grupy](https://github.com/EmberConsultingGroup).
2. Obejście hello toouse CSS, Utwórz nowy plik .cs w projekcie roli sieci Web *App_Start* folder o nazwie *StyleBundleExtensions.cs*i zastąpić jej zawartość hello [kodu z GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. W *App_Start\StyleFundleExtensions.cs*, Zmień nazwę hello przestrzeni nazw tooyour Web roli (np. **WebRole1**).
4. Wróć za`App_Start\BundleConfig.cs` i zmodyfikuj hello ostatnio `bundles.Add` instrukcji z powitania po wyróżniony kod:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Ta nowa metoda rozszerzenia używa hello tego samego pomysł tooinject skryptu w modelu DOM hello toocheck hello HTML dla hello zgodną nazwę klasy, nazwy reguły i wartość reguły zdefiniowany w pakiecie CSS hello i wypada wstecz toohello źródła serwera sieci Web w przypadku niepowodzenia toofind hello dopasowania.
5. Opublikuj ponownie usługa w chmurze hello i strony głównej hello dostępu.
6. Widok hello kodu HTML dla strony hello. Należy znaleźć wprowadzony skrypty podobne toohello następujące:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Należy zauważyć, że wprowadzony skryptu dla pakietu CSS hello nadal zawiera hello niewykorzystany wadliwe z hello `CdnFallbackExpression` właściwości w wierszu hello:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Ale od czasu pierwszej części hello hello || wyrażenie zawsze zwróci wartość true (w wierszu hello bezpośrednio powyżej), funkcja wywołania document.write() hello nigdy nie zostanie uruchomiony.

## <a name="more-information"></a>Więcej informacji
* [Omówienie hello Azure sieci dostarczania zawartości (CDN)](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Za pomocą usługi Azure CDN](cdn-create-new-endpoint.md)
* [ASP.NET tworzenie pakietów i minimalizowanie](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
