## <a name="incremental-and-complete-deployments"></a>Przyrostowe i pełne wdrożenia
W przypadku wdrażania zasobów, należy określić hello wdrożenia aktualizacji przyrostowej i pełnej aktualizacji. Witaj podstawowa różnica między tych dwóch trybów jest jak Resource Manager obsługuje istniejących zasobów w grupie zasobów hello, które nie są w szablonie hello:

* W trybie pełnej, Menedżer zasobów **usuwa** zasobów, które istnieją w grupie zasobów hello, ale nie są określone w szablonie hello. 
* W trybie przyrostowych, Menedżer zasobów **pozostawia niezmienione** zasobów, które istnieją w grupie zasobów hello, ale nie są określone w szablonie hello.

Dla obu trybów Resource Manager podejmie tooprovision wszystkich zasobów określonej w szablonie hello. Jeśli hello zasób już istnieje w grupie zasobów hello, jego ustawienia są takie same jak hello wynikiem operacji bez zmian. Jeśli zmienisz ustawienia hello zasobu zasobów hello jest udostępniane z te nowe ustawienia. Jeśli tooupdate hello lokalizację i typ istniejącego zasobu, hello wdrożenie zakończy się niepowodzeniem z powodu błędu. Zamiast tego należy wdrożyć nowy zasób z lokalizacją hello lub wpisz, że należy.

Domyślnie usługi Resource Manager tryb hello przyrostowe.

tooillustrate hello różnica między trybami przyrostowe i pełne, należy wziąć pod uwagę powitania od scenariusza.

**Istniejąca grupa zasobów** zawiera:

* Zasobów A
* Zasób B
* Zasób C

**Szablon** definiuje:

* Zasobów A
* Zasób B
* Zasób D

Po wdrożeniu w **przyrostowe** trybie hello grupa zasobów zawiera:

* Zasobów A
* Zasób B
* Zasób C
* Zasób D

Po wdrożeniu w **pełną** trybie C zasób zostanie usunięty. Grupa zasobów Hello zawiera:

* Zasobów A
* Zasób B
* Zasób D
