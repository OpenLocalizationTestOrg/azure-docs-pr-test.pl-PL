


## <a name="tagging-a-virtual-machine-through-templates"></a>Znakowanie maszynę wirtualną za pomocą szablonów
Po pierwsze Przyjrzyjmy się znakowanie za pomocą szablonów. [Ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) umieszcza tagi na powitania następujące zasoby: obliczeniowych (maszyna wirtualna), magazynu (konta magazynu) i sieci (publicznego adresu IP sieci wirtualnej i interfejsu sieciowego). Ten szablon jest przeznaczony dla maszyny Wirtualnej systemu Windows, ale mogą być dostosowywane dla maszyn wirtualnych systemu Linux.

Kliknij przycisk hello **wdrażanie tooAzure** przycisk od hello [łącze szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Spowoduje to przejście toohello [portalu Azure](https://portal.azure.com/) którym można wdrożyć tego szablonu.

![Proste wdrożenie przy użyciu tagów](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Ten szablon obejmuje następujące znaczniki hello: *działu*, *aplikacji*, i *utworzony przez*. Użytkownik może Dodawanie/edytowanie znaczniki bezpośrednio w szablonie hello Jeśli chcesz różnych nazwach.

![Azure tagów w szablonie](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Jak widać, tagi hello są definiowane jako pary klucz wartość oddzielone dwukropkiem (:). tagi Hello musi być zdefiniowana w następującym formacie:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Zapisz plik szablonu hello po zakończeniu edycji za pomocą tagów hello wybranych przez użytkownika.

Następnie w hello **Edytuj parametry** sekcji, możesz też wypełnić hello wartości dla tagów.

![Edytowanie tagów w portalu Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Kliknij przycisk **Utwórz** toodeploy tego szablonu o wartości tagu.

## <a name="tagging-through-hello-portal"></a>Znakowanie za pośrednictwem hello portalu
Po utworzeniu zasobów za pomocą tagów, można wyświetlać, dodawania i usuwania tagów w portalu hello.

Wybierz hello tagów tooview ikona tagów:

![Ikona tagów w portalu Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Dodaj nowy znacznik za pośrednictwem portalu hello, definiując własne parę klucza i wartości i zapisz go.

![Dodaj nowy znacznik w portalu Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Twoje nowy znacznik powinien zostać wyświetlony na liście hello znaczników dla zasobu.

![Nowy znacznik zapisane w portalu Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

