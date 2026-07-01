### Inleiding

Deze implementatiegids bevat de afspraken en specificaties die nodig zijn voor het realiseren van routering binnen eOverdracht. 

### Procesbeschrijving

Deze implementatiegids voegt routering toe aan eOverdracht. Een functionele beschrijving van eOverdracht is te vinden in het [Functioneel Ontwerp eOverdracht](https://informatiestandaarden.nictiz.nl/wiki/vpk:V4.0_Ontwerp_eOverdracht).
Routering betekent in de context van eOverdracht dat wanneer gewenst de versturende zorgorganisatie een cliënt/patiënt overdraaft naar een specifiek onderdeel van de ontvangende zorgorganisatie. Dit kan een specifieke locatie, afdeling, team of zorgdienst van de ontvangende zorgorganisatie zijn.

Voorbeelden:
- Een patient wordt overgedragen van het ziekenhuis naar de afdeinng geriatrische revalidatiezorg van een vvt-organisatie.
- Een patient wordt overgedragen van een intramurale vvt-organisatie naar een specifiek wijkzorgteam van een landelijke wijkzorgorganisatie.

### Principes

1. Deze specificatie maakt gebruik van de bestaande afspraken over eOverdracht zoals vastgelegd in de [TA eOverdracht](https://www.actiz.nl/sites/default/files/inline-files/TA%20eOverdracht%20%28Verpleegkundige%20Overdracht%29.pdf).
2. Deze specificatie is een addendum en beschrijft louter de voor de realisatie van routering benodigde aanvullingen en wijzigingen op de TA eOverdracht.
3. Deze specificatie maakt gebruik van de door Twiin opgestelde [TA Routering](https://www.twiin.nl/taroutering).
4. Deze specificatie maakt gebruik van de door het Ministerie van VWS gedefinieerde [generieke functie Adressering](https://minvws.github.io/generiekefuncties-docs/en/care-services.html).

### Rollen en verantwoordelijkheden

#### Eigenaar van de specificatie

- opstellen en publiceren releases van de specificatie
- in samenwerking met deelnemers bepalen inhoud en planning releases 
- informeren deelnemers en andere stakeholders over inhoud en planning releases
- vaststellen inhoud en planning releases
- faciliteren van tests van de specificaties
- uitdragen van de specificatie
- vergroten adoptie van de specificatie 

#### Deelnemer

- technische implementatie van de specificatie
- leveren input voor inhoud en planning releases

#### Implementatie-ondersteuner

- Ondersteuning van deelnemers bij technische en organoisatorische implementatie van de specificatie
- leveren input voor inhoud en planning releases

### Rollen en uitvoerders

Rol | Uitvoerder
----|--------
Eigenaar van de specificatie | Stichting Nuts
Deelnemer | eOverdracht-leverancier
Implementatie-ondersteuner | Bureau eOverdracht

#### Versiebeheer

De eigenaar van de specificatie hanteert de Semantic Versioning-specificatie voor het versiebeheer,
zie https://semver.org. Dit betekent dat het versienummer wordt weergegeven door 3 nummers die met een punt zijn
gescheiden (x.y.z waarbij x de majorrelease is, y de minor en z de patch).

#### Besluitvorming

De eigenaar van de specificatie besluit na overleg met de deelnemers en de implementatie-ondersteuner over het vaststellen van een nieuwe release en over de ‘Release roadmap’ met de onderwerpen voor een eerstvolgende release.
