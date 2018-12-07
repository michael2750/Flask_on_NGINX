## Flask applikation kørende på Nginx
Hvis du gør brug af Flask i en større applikation er der stor sandsynlighed for dette ikke er den bedste løsning, da Flask har sine begrænsninger i forhold til, at håndtere requests.
Flask kan blive et problem for virksomheder, hvis mængden af requests overstiger den mængde Flask er i stand til at håndtere, og dermed skaber en bottleneck i applikationen. En nem løsning ville være at implementere Nginx, så man derved kan undgå den bottleneck der er opstået.
Ved at implementere Nginx vil firmaet både spare problemer angående klager, pga. et langsomt response, men den vil samtidig også øge applikationens stabilitet.
