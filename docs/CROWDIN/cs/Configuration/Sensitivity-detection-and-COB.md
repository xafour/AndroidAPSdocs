# Detekce citlivosti

## Algoritmy detekce

V současné době máme 4 modely pro detekci citlivosti:

* Citlivost Oref0
* Citlivost AAPS
* Citlivost váženým průměrem
* Citlivost Oref1

### Citlivost Oref0

Citlivost je počítaná za posledních 24 hodin. Trávení sacharidů (pokud nejsou absorbované) se v simulaci zařezává na mezní dobu, která je uvedená v nastavení. Tento model pracuje obdobně jako OpenAPS Oref0, popsaný v [OpenAPS Oref0 dokumentaci](https://openaps.readthedocs.io/en/2017-05-21/docs/walkthrough/phase-4/advanced-features.html).

### Citlivost AAPS

Citlivost se počítá stejným způsobem jako v Oref0 variantě, ale můžete zadat čas do minulosti. Minimální absorpce sacharidů se počítá z maximální doby trávení sacharidů z nastavení

### Citlivost váženým průměrem

Citlivost je vypočítaná jako vážený průměr z odchylek. Novější odchylky mají větší váhu. Minimální absorpce sacharidů se počítá z maximální doby trávení sacharidů z nastavení. Tento algoritmus je nejrychlejší při následujících změnách citlivosti.

### Citlivost Oref1

Citlivost je vypočítaná z údajů 8 hodin do minulosti nebo od poslední výměny kanyly, pokud k ní došlo méně než 8 hodin zpět. Sacharidy (pokud nejsou absorbované) se odříznou po době určené v předvolbách. Pouze Oref1 algoritmus podporuje "neohlášené jídlo" (UAM, un-announced meal). To znamená, že časy s odhalenými UAM jsou vyjmuty z výpočtu citlivosti. Takže pokud používáte SMB s UAM, musíte si vybrat Oref1 algoritmus, aby výpočet citlivosti fungoval správně. Pro více informací si přečtěte [OpenAPS Oref1 dokumentaci](https://openaps.readthedocs.io/en/latest/docs/Customize-Iterate/autosens.html).

## COB příklady

Oref0 / Oref1 - nestrávené sacharidy jsou odříznuty po určené době

![COB z Oref0](../images/cob_oref0.png)

AAPS, vážený průměr - absorpce se počítá tak, aby bylo `COB == 0` po určité době

![COB z AAPS](../images/cob_aaps.png)

Jestliže je použitá minimální absorpce sacharidů namísto hodnoty vypočtené z odchylek, tak se v COB grafu objeví zelená tečka