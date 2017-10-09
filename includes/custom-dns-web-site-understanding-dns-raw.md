Witaj systemu nazw domen (DNS, Domain Name System) jest używane toolocate zasobów na powitania internet. Na przykład wprowadź adres aplikacji sieci web w przeglądarce, lub kliknij łącze na stronie sieci web, używa domeny hello tootranslate DNS, do adresu IP. adres IP Hello przypomina sortowania w ulicę, ale nie jest bardzo człowieka przyjazne. Na przykład jest znacznie łatwiejsze tooremember nazwy DNS, takich jak **contoso.com** niż jest tooremember adresu IP, takie jak 192.168.1.88 lub 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Witaj DNS system jest oparta na *rekordów*. Rejestruje skojarzenia określony *nazwa*, takich jak **contoso.com**, adres IP lub nazwa DNS innej. Aplikacji, takich jak przeglądarki sieci web, wyszukuje nazwy w systemie DNS, znajduje rekord hello, a używa on punktów tooas hello adres. Jeśli hello wartość toois punktów adresu IP, przeglądarki hello użyje tej wartości. Wskazuje nazwę DNS tooanother, następnie aplikacji hello ma rozdzielczość toodo ponownie. Ostatecznie rozpoznawanie nazw zakończy adresu IP.

Podczas tworzenia aplikacji sieci web w usłudze App Service, nazwa DNS jest automatycznie przypisywany toohello aplikacji sieci web. Ta nazwa ma formę hello  **&lt;yourwebappname&gt;. azurewebsites.net**. Istnieje również wirtualnego adresu IP dostępne do użycia podczas tworzenia DNS rekordów, więc możesz utworzyć rekordy toohello tego punktu **. azurewebsites.net**, lub możesz wskazać toohello adresu IP.

> [!NOTE]
> adres IP Hello aplikacji sieci web ulegnie zmianie, usunięcie i ponowne utworzenie aplikacji sieci web lub zmienić hello tryb planu usługi aplikacji za**wolne** po jego ustawieniu zbyt**podstawowe**, **Shared**, lub **standardowe**.
> 
> 

Są także wiele typów rekordów, każda z własnych funkcji i ograniczeń, ale dla aplikacji sieci web tylko Dbamy o dwóch *A* i *CNAME* rekordów.

### <a name="address-record-a-record"></a>Rekordu adresu (rekord)
Rekord A mapuje domeny, takie jak **contoso.com** lub **www.contoso.com**, *lub domena symboli wieloznacznych* takich jak  **\*. contoso.com**, tooan adresu IP. W przypadku hello aplikacji sieci web w usłudze App Service albo hello wirtualnego adresu IP usługi hello lub określonego adresu IP, które zakupione dla aplikacji sieci web.

główne zalety rekord A za pośrednictwem rekordu CNAME Hello to:

* Można mapować domeny głównej, takich jak **contoso.com** adres IP tooan; wiele rejestratorów Zezwalaj tylko na użyciu rekordów
* Może mieć jeden wpis, który używa symboli wieloznacznych, takich jak  **\*. contoso.com**, który będzie obsługiwać żądania wielu domen podrzędnych takich jak **mail.contoso.com**,  **blogs.contoso.com**, lub **www.contso.com**.

> [!NOTE]
> Ponieważ rekord jest mapowany tooa statyczny adres IP, nie może automatycznie rozwiązać zmian adresu IP toohello aplikacji sieci web. Adres IP do użycia z rekordu jest dostępne po skonfigurowaniu ustawienia nazwy domeny niestandardowej dla aplikacji sieci web; Jednak ta wartość może zmienić usunięcie i ponowne utworzenie aplikacji sieci web lub zmienić hello tooback trybie planu usługi aplikacji za**wolne**.
> 
> 

### <a name="alias-record-cname-record"></a>Rekord aliasu (rekordu CNAME)
Rekord CNAME mapuje *określonych* nazwy DNS, takich jak **mail.contoso.com** lub **www.contoso.com**, tooanother nazwy domeny (canonical). W przypadku aplikacji usługi sieci Web aplikacji hello, nazwa domeny canonical hello jest hello  **&lt;yourwebappname >. azurewebsites.net** nazwy domeny aplikacji sieci web. Po utworzeniu hello CNAME tworzy alias dla hello  **&lt;yourwebappname >. azurewebsites.net** nazwy domeny. Hello wpis CNAME rozwiąże adres IP toohello Twojego  **&lt;yourwebappname >. azurewebsites.net** automatycznie, nazwa domeny, jeśli zmieni adres IP hello hello aplikacji sieci web, nie masz tootake żadnych działań.

> [!NOTE]
> Niektóre domeny rejestratorów tylko pozwalają poddomen toomap podczas przy użyciu rekordu CNAME, takich jak **www.contoso.com**, a nie głównego nazwy, takie jak **contoso.com**. Więcej informacji o rekordy CNAME, można znaleźć w dokumentacji hello przez rejestratora, <a href="http://en.wikipedia.org/wiki/CNAME_record">hello wpis Wikipedia rekordu CNAME</a>, lub hello <a href="http://tools.ietf.org/html/rfc1035">nazwy domen IETF - wdrażania i specyfikację</a> dokument.
> 
> 

### <a name="web-app-dns-specifics"></a>Szczegóły DNS aplikacji sieci Web
Przy użyciu rekordu A dla aplikacji sieci Web wymaga toofirst utworzyć następujące rekordy TXT hello:

* **Dla domeny głównej hello** — rekord TXT usługi DNS A  **@**  za  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Dla określonej domeny podrzędnej** — nazwa A DNS  **&lt;domeny podrzędnej >** za**&lt;yourwebappname&gt;. azurewebsites.net**. Na przykład **blogi** Jeśli hello rekord jest przeznaczony dla **blogs.contoso.com**.
* **Dla symbolu wieloznacznego hello sub-dodmains** — rekord TXT usługi DNS A *** zbyt  **&lt;yourwebappname&gt;. azurewebsites.net**.

Ten rekord TXT jest używane tooverify, że jesteś właścicielem domeny hello próbujesz toouse. Ponadto to rekord A toocreating wskazanie toohello wirtualnego adresu IP aplikacji sieci web.

Można znaleźć adres IP hello i **. azurewebsites.net** hello nazw dla aplikacji sieci web, wykonując następujące kroki:

1. W przeglądarce otwórz hello [Azure Portal](https://portal.azure.com).
2. W hello **aplikacje sieci Web** bloku, kliknij nazwę hello aplikacji sieci web, a następnie wybierz **domen niestandardowych** od dołu hello hello strony.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. W hello **domen niestandardowych** bloku, zobaczysz hello wirtualnego adresu IP. Zapisz te informacje jako będzie używane podczas tworzenia rekordów DNS
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > Nie można użyć nazwy domeny niestandardowej z **wolne** sieci web app i należy uaktualnić hello planu usługi App Service za**Shared**, **podstawowe**, **standardowe**, lub **Premium** warstwy. Aby uzyskać więcej informacji na powitania usługi aplikacji — plan obiektu warstw cenowych, tym, jak toochange hello warstwy cenowej aplikacja sieci web, zobacz [jak aplikacje sieci web na tooscale](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

