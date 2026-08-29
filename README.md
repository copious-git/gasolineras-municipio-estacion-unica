# El peaje del pueblo: sobreprecio de la gasolina en municipios con una sola gasolinera

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22165792.svg)](https://doi.org/10.5281/zenodo.22165792)


Precio de la gasolina 95 E5 en cada municipio español que tiene **exactamente una** estación de
servicio, comparado con la gasolinera más barata en un radio de 25 km.

Nadie publica esta comparación municipio a municipio, así que este repositorio existe para que el
cálculo sea abierto, comprobable y reutilizable.

*English: the fuel price premium paid in Spanish municipalities served by a single petrol station,
measured against the cheapest station within 25 km. One record per municipality, 1,568 in total.*

## Qué contiene

| Fichero | Contenido |
|---|---|
| `data/single-station-fuel-premium-spain.json` | Estadísticas nacionales, medianas por provincia y un registro por cada municipio de estación única |

Cada registro municipal incluye `muni_id` (IDMunicipio de MITECO), `muni`, `prov`, `rotulo`, `lat`,
`lng`, `price_g95`, `cheapest_g95_within_25km`, `gap_eur_per_litre` y `gap_eur_per_50l_tank`.

## Cifras principales

Datos MITECO de **29 de agosto de 2026, 21:11**.

| Medida | Valor |
|---|---|
| Estaciones con gasolina 95 E5 | 10.814 |
| Municipios con una sola estación | 1.568 |
| Sobreprecio mediano por depósito de 50 litros | 7,47 € |
| Municipios con sobreprecio de 5 € o más | 68,0 % |
| Municipios con sobreprecio de 10 € o más | 28,1 % |

Provincias con la mediana más alta: **Girona** (14,85 €), **Tarragona** (13,88 €),
**Alicante** (11,23 €), **Barcelona** (11,20 €), **Zaragoza** (11,05 €).

Municipio con mayor diferencia: **Sant Mateu** (Castellón), 1,889 €/l frente a 1,485 €/l a menos de
25 km, es decir **20,20 € por depósito**.

## Método

Para cada municipio con exactamente una estación que vende gasolina 95 E5:

```
sobreprecio = precio propio − precio más barato de G95 en 25 km
```

- Municipio = `IDMunicipio` de MITECO, no el nombre, para evitar homónimos.
- La distancia es haversine sobre las coordenadas WGS84 publicadas por MITECO. La estación más
  barata puede estar en cualquier municipio, incluida otra provincia.
- El depósito de referencia es de 50 litros.
- Se ranquean solo las provincias con **5 o más** municipios de estación única. Quedan 49 provincias.
- Cálculo determinista, sin estimaciones y sin modelos de lenguaje.

En **80** de los 1.568 municipios el sobreprecio es cero o negativo: la única estación del municipio
es ya la más barata en 25 km. Esos registros se conservan.

## Qué NO mide

- **No mide un cobro abusivo.** Una estación aislada tiene costes logísticos y volúmenes distintos
  de una estación urbana. La diferencia de precio es un hecho medido; su causa no está en los datos.
- **No mide lo que paga la gente.** Muchos conductores rurales repostan donde trabajan o hacen la
  compra, no en su municipio. El sobreprecio es el que pagaría quien reposta localmente.
- **No mide el coste del desvío.** Recorrer 25 km de ida y vuelta para ahorrar 7,47 € consume
  combustible y tiempo, y ese coste no se descuenta aquí.
- **Es una foto de un instante.** Los precios de MITECO cambian a diario. Cada ejecución produce
  cifras distintas; la fecha del feed viene en el campo `fecha_miteco`.
- El rótulo (`rotulo`) es el que declara la propia estación a MITECO y no siempre coincide con la
  propiedad real de la instalación.

## Cómo citar

Reclamar.es (2026). *Sobreprecio de la gasolina en municipios espanoles con una sola estacion de servicio*. Zenodo. https://doi.org/10.5281/zenodo.22165792

El DOI anterior es el DOI de concepto: siempre apunta a la última versión. Para citar una versión concreta, use su propio DOI en el registro de Zenodo.

## Licencia y atribución

Ver [LICENSE.md](LICENSE.md). Datos de origen: MITECO, reutilizados conforme a la Ley 37/2007.
El conjunto derivado se publica como CC BY 4.0 con atribución a Reclamar.es.

## Fuentes

- API de precios de carburantes, MITECO:
  https://sedeaplicaciones.minetur.gob.es/ServiciosRESTCarburantes/PreciosCarburantes/EstacionesTerrestres/
- Portal de precios de carburantes del Ministerio:
  https://geoportalgasolineras.es/
- Precios actualizados y buscador por municipio: https://reclamar.es/precios-gasolina
