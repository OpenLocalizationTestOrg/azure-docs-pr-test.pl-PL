Hello systemu nazw domen (DNS) jest używane toolocate elementy na powitania internet. Na przykład podczas wprowadzania adresu w przeglądarce, lub kliknij łącze na stronie sieci web, używa domeny hello tootranslate DNS, do adresu IP. adres IP Hello przypomina sortowania w ulicę, ale nie jest bardzo człowieka przyjazne. Na przykład jest znacznie łatwiejsze tooremember nazwy DNS, takich jak **contoso.com** niż jest tooremember adresu IP, takie jak 192.168.1.88 lub 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Witaj DNS system jest oparta na *rekordów*. Rejestruje skojarzenia określony *nazwa*, takich jak **contoso.com**, adres IP lub nazwa DNS innej. Aplikacji, takich jak przeglądarki sieci web, wyszukuje nazwy w systemie DNS, znajduje rekord hello, a używa on punktów tooas hello adres. Jeśli hello wartość toois punktów adresu IP, przeglądarki hello użyje tej wartości. Wskazuje nazwę DNS tooanother, następnie aplikacji hello ma rozdzielczość toodo ponownie. Ostatecznie rozpoznawanie nazw zakończy adresu IP.

Podczas tworzenia witryny sieci Web platformy Azure, nazwa DNS jest automatycznie przypisywany toohello lokacji. Ta nazwa ma formę hello  **&lt;yoursitename&gt;. azurewebsites.net**. Po dodaniu witryny sieci Web jako punktu końcowego usługi Azure Traffic Manager witryny sieci Web jest dostępna za pośrednictwem hello  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** domeny.

> [!NOTE]
> Gdy witryny sieci Web jest skonfigurowany jako punkt końcowy Menedżera ruchu, użyje hello **. trafficmanager.net** adresów podczas tworzenia rekordów DNS.
> 
> Można używać tylko rekordy CNAME z Menedżera ruchu
> 
> 

Są również wiele typów rekordów, każda z własnych funkcji i ograniczeń, ale dla witryn sieci Web skonfigurowana tooas punktów końcowych usługi Traffic Manager, tylko Dbamy o jeden; *CNAME* rekordów.

### <a name="cname-or-alias-record"></a>Rekord CNAME lub Alias
Rekord CNAME mapuje *określonych* nazwy DNS, takich jak **mail.contoso.com** lub **www.contoso.com**, tooanother nazwy domeny (canonical). W przypadku hello Azure witryn sieci Web przy użyciu Menedżera ruchu, nazwa domeny canonical hello jest hello  **&lt;moja_aplikacja >. trafficmanager.net** nazwę domeny profilu usługi Traffic Manager. Po utworzeniu hello CNAME tworzy alias dla hello  **&lt;moja_aplikacja >. trafficmanager.net** nazwy domeny. Hello wpis CNAME rozwiąże adres IP toohello Twojego  **&lt;moja_aplikacja >. trafficmanager.net** automatycznie, nazwa domeny, jeśli zmieni adres IP hello hello witryny sieci Web, nie masz tootake żadnych działań.

Po odebraniu ruchu na Menedżera ruchu następnie przekierowuje hello ruchu tooyour witryny sieci Web, przy użyciu metody, które nie jest skonfigurowana do równoważenia obciążenia hello. To jest całkowicie niewidoczne toovisitors tooyour witryny sieci Web. Użytkownik widzi tylko hello niestandardową nazwę domeny w przeglądarce.

> [!NOTE]
> Niektóre domeny rejestratorów tylko pozwalają poddomen toomap podczas przy użyciu rekordu CNAME, takich jak **www.contoso.com**, a nie głównego nazwy, takie jak **contoso.com**. Więcej informacji o rekordy CNAME, można znaleźć w dokumentacji hello przez rejestratora, <a href="http://en.wikipedia.org/wiki/CNAME_record">hello wpis Wikipedia rekordu CNAME</a>, lub hello <a href="http://tools.ietf.org/html/rfc1035">nazwy domen IETF - wdrażania i specyfikację</a> dokument.
> 
> 

