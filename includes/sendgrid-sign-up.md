W każdym miesiącu klienci platformy Azure mogą odblokować 25 000 bezpłatnych wiadomości e-mail. 25 000 bezpłatne miesięczne wiadomościach zapewni dostęp tooadvanced raportowania i analiz i [wszystkich interfejsów API] [ all APIs] (sieci Web, SMTP, zdarzenia, analizy i inne). Informacje o dodatkowe usługi zapewnianie przez włączenie, można znaleźć hello [rozwiązań SendGrid] [ SendGrid Solutions] strony.

### <a name="toosign-up-for-a-sendgrid-account"></a>toosign dla konta SendGrid
1. Zaloguj się za toohello [portalu zarządzania Azure][Azure Management Portal].
2. W menu powitania po lewej stronie powitania kliknij **nowy**.

    ![command-bar-new][command-bar-new]
3. Kliknij kolejno pozycje **Dodatki** i **Dostarczanie poczty e-mail przy użyciu usługi SendGrid**.

    ![sendgrid-store][sendgrid-store]
4. Wypełnij formularz rejestracji hello i wybierz **Utwórz**.

    ![sendgrid-create][sendgrid-create]
5. Wprowadź **nazwa** tooidentify Twojego SendGrid usługa w ustawieniach platformy Azure. Nazwa musi mieć długość od 1 do 100 znaków i może zawierać tylko znaki alfanumeryczne, łączniki, kropki i znaki podkreślenia. Nazwa Hello musi być unikatowa na liście elementów subskrybowanego magazynu Azure.
6. Wprowadź i potwierdź **hasło**.
7. Wybierz **subskrypcję**.
8. Utwórz nową **grupę zasobów** lub wybierz istniejącą.
9. W hello **warstwa cenowa** sekcji wybierz plan SendGrid hello ma toosign usłudze.

    ![sendgrid-pricing][sendgrid-pricing]
10. Wprowadź **kod promocyjny**, jeśli go masz.
11. Wprowadź **informacje kontaktowe**.
12. Przejrzyj i zaakceptuj hello **postanowienia prawne**.
13. Po potwierdzeniu zakupu zobaczysz **Zakończono pomyślnie wdrażanie** okienko wyskakujące, a zostanie wyświetlony na liście hello konta **wszystkie zasoby** sekcji.

    ![all-resources][all-resources]

    Po ukończone zakupu i kliknięciu hello **Zarządzaj** proces weryfikacji przycisk tooinitiate hello poczty e-mail, otrzymasz wiadomość e-mail z prośbą tooverify SendGrid Twoje konto. Jeśli wiadomość e-mail nie dotarła do Ciebie lub masz problemy z weryfikacją konta, zobacz zbiór często zadawanych pytań.

    ![manage][manage]

    **Możesz wysyłać tylko górę too100 wiadomości e-mail/dzień dopóki nie upewnisz się konta.**

    toomodify Twojego planu subskrypcji lub zobacz hello ustawienia osoby kontaktowej SendGrid, kliknij nazwę hello hello tooopen Twojego SendGrid usługi Pulpit nawigacyjny z witryny SendGrid Marketplace.

    ![settings][settings]

    toosend usługi poczty e-mail przy użyciu SendGrid, należy podać klucz interfejsu API.

### <a name="toofind-your-sendgrid-api-key"></a>toofind SendGrid klucza interfejsu API
1. Kliknij pozycję **Zarządzaj**.

    ![manage][manage]
2. Na pulpicie nawigacyjnym SendGrid wybierz **ustawienia** , a następnie **klucze interfejsu API** hello menu po lewej stronie powitania.

    ![api-keys][api-keys]

3. Kliknij przycisk hello **Utwórz klucz interfejsu API** listy rozwijanej i wybierz **klucz interfejsu API ogólne**.

    ![general-api-key][general-api-key]
4. Co najmniej, podaj hello **nazwa tego klucza** i umożliwianie pełnego dostępu zbyt**wysyłania poczty** i wybierz **zapisać**.

    ![access][access]
5. Po wykonaniu tych czynności zostanie wyświetlony klucz interfejsu API. Należy się upewnić toostore go bezpiecznie.

### <a name="toofind-your-sendgrid-credentials"></a>toofind poświadczeń SendGrid
1. Kliknij hello ikonę klucza toofind Twojego **Username**.

    ![key][key]
2. hasło Hello jest hello co wybrane podczas instalacji. Możesz wybrać **Zmień hasło** lub **resetowania hasła** toomake wszelkie zmiany.

toomanage powitania kliknij przycisk Ustawienia poczty e-mail deliverability **przycisku Zarządzaj**. Nastąpi przekierowanie tooyour SendGrid z pulpitu nawigacyjnego.

    ![manage][manage]

    For more information on sending email through SendGrid, visit hello [Email API Overview][Email API Overview].

<!--images-->

[command-bar-new]: ./media/sendgrid-sign-up/new-addon.png
[sendgrid-store]: ./media/sendgrid-sign-up/sendgrid-store.png
[sendgrid-create]: ./media/sendgrid-sign-up/sendgrid-create.png
[sendgrid-pricing]: ./media/sendgrid-sign-up/sendgrid-pricing.png
[all-resources]: ./media/sendgrid-sign-up/all-resources.png
[manage]: ./media/sendgrid-sign-up/manage.png
[settings]: ./media/sendgrid-sign-up/settings.png
[api-keys]: ./media/sendgrid-sign-up/api-keys.png
[general-api-key]: ./media/sendgrid-sign-up/general-api-key.png
[access]: ./media/sendgrid-sign-up/access.png
[key]: ./media/sendgrid-sign-up/key.png

<!--Links-->

[SendGrid Solutions]: https://sendgrid.com/solutions
[Azure Management Portal]: https://manage.windowsazure.com
[SendGrid Getting Started]: http://sendgrid.com/docs
[SendGrid Provisioning Process]: https://support.sendgrid.com/hc/articles/200181628-Why-is-my-account-being-provisioned-
[all APIs]: https://sendgrid.com/docs/API_Reference/index.html
[Email API Overview]: https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html
