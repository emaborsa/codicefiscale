# Verifica Codice Fiscale in [GO](http://golang.org)
[![Build Status](https://travis-ci.org/squeeze69/codicefiscale.svg?branch=master)](https://travis-ci.org/squeeze69/codicefiscale)
## Licenza: LGPLv3

**Package**: github.com/squeeze69/codicefiscale

**Download del package**: go get github.com/squeeze69/codicefiscale

Simile ma per la [partita IVA](https://github.com/squeeze69/partitaiva)

Porting basato sulle informazioni pubblicate da Umberto Salsi su [Icosaedro](http://www.icosaedro.it/cf-pi/index.html)

## Verifica del codice di controllo del codice fiscale
```
package main

import (
	"github.com/squeeze69/codicefiscale"
	"fmt"
)

func main() {
	ok, err := codicefiscale.CodiceFiscale("ABCDEF12B23P432P")
	if err != nil {
		fmt.Println("Codice Fiscale non valido:",err)
	} else {
		fmt.Println("Codice Fiscale Valido")
	}
}
```

## Confronto dei codici fiscali

NOTA: il PRIMO può essere variato per omocodia
```
//Confronto codici fiscali - invertendo le modifiche in caso di omocodie
//prima fa una verifica di bontà in base al codice di controllo
//solo il PRIMO codice può essere modificato per omocodie
package main

import (
	"github.com/squeeze69/codicefiscale"
	"fmt"
)

func main() {
	ok, err := codicefiscale.ConfrontaCodicifiscaliOmocodici("ABCDEF12B23P43NE", "ABCDEF12B23P432P")
	if err != nil {
		fmt.Println("Codici Fiscali diversi:",err)
	} else {
		fmt.Println("Codice Fiscali uguali (tenendo conto di eventuali omocodie)")
	}
}
```

## Generazione del codice di controllo
```
//Generazione codice di controllo - in ingresso deve avere ALMENO 15 caratteri
//funziona - ovviamente - anche con codici modificati a causa di omocodie
package main

import (
	"github.com/squeeze69/codicefiscale"
	"fmt"
)

func main() {
	if s, err := Codicedicontrollo("ABCDEF12B23P432"); err != nil {
		fmt.Println("Errore", err)
	} else {
		fmt.Println("Il codice di controllo è:",s)
	}
}
```
